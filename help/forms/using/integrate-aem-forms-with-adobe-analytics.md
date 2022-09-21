---
title: Come integrare AEM Forms con Adobe Analytics?
seo-title: Learn how to integrate AEM Forms with Adobe Analytics.
description: AEM Forms si integra con Adobe Analytics per acquisire e monitorare le metriche delle prestazioni dei moduli pubblicati.
seo-description: To discover interaction patterns and problems users face while using adaptive forms.
uuid: e258805c-4da8-4c5d-ae91-7bea78a6a71b
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
discoiquuid: 8f776f30-ff93-4d19-94c6-c4bfe6f1fae2
docset: aem65
exl-id: be2444df-c772-4a8e-83f9-0f565c15a44e
source-git-commit: 67d492713d9e2236dbf81c5f3c781c80717ec9a6
workflow-type: tm+mt
source-wordcount: '1806'
ht-degree: 0%

---

# Analytics tramite [!DNL Adobe Launch] {#analyticsusingadobelaunch}

AEM Forms si integra con [Adobe Analytics](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/overview.html?lang=en) per acquisire e tenere traccia delle metriche delle prestazioni dei moduli pubblicati. L’obiettivo dell’analisi di queste metriche è quello di consentire agli utenti aziendali di acquisire informazioni sul comportamento degli utenti finali e di ottimizzare l’esperienza di acquisizione dei dati. È possibile acquisire e tenere traccia del comportamento degli utenti connessi e non connessi (anonimi) tramite Adobe Analytics per Adaptive Forms.

È inoltre possibile eseguire analisi utilizzando Cloud Service Framework. Per ulteriori informazioni su come integrare AEM Forms con Cloud Service Framework, consulta [Analytics con Cloud Service Framework](/help/forms/using/configure-analytics-forms-documents.md). Il vantaggio principale dell&#39;utilizzo di Adobe Launch su Analytics tramite Cloud Service Framework è che è possibile definire eventi personalizzati, oltre a questi eventi predefiniti. Gli eventi personalizzati vengono definiti utilizzando l’editor di regole o clientlibs dei clienti e mappati a eventi in [!DNL Adobe Analytics].

Dopo aver eseguito le azioni menzionate in questo articolo, puoi configurare e visualizzare i rapporti in [!DNL Adobe Analytics], come illustrato nel video seguente:

>[!VIDEO](https://video.tv.adobe.com/v/337262)

È possibile utilizzare [!DNL Adobe Analytics] per scoprire pattern di interazione e problemi incontrati dagli utenti durante l’utilizzo di moduli adattivi. Fuori dalla scatola, [!DNL Adobe Analytics] tiene traccia e memorizza informazioni sui seguenti eventi:

* **Rendering**: Numero di volte in cui il modulo viene aperto.

* **Invia**: Numero di volte in cui il modulo viene inviato.

* **Abbandonare**: Numero di volte in cui gli utenti si fermano senza compilare il modulo.

* **Errore**: Numero di errori riscontrati nel pannello e nei campi del pannello.

* **Aiuto**: Numero di volte in cui un utente apre la guida di un pannello e dei campi del pannello.

* **Visita sul campo**: Numero di volte in cui un utente visita un campo del modulo.

* **Salva**: Numero di volte in cui gli utenti salvano un modulo sul portale Forms.

Oltre a questi eventi predefiniti, puoi anche definire eventi personalizzati.

La figura seguente illustra le azioni da eseguire prima di visualizzare i rapporti in [!DNL Adobe Analytics]:

![Panoramica di Analytics](/help/forms/using/assets/analyticsworkflow.png)

## 1. Configura [!DNL Adobe Analytics] {#Configure-adobe-analytics}

Prima di configurare [!DNL Adobe Analytics], crea:

* Un Adobe ID a cui accedere [Adobe Experience Cloud](https://experience.adobe.com/#/home).
* A [suite di rapporti](https://experienceleague.adobe.com/docs/analytics/admin/manage-report-suites/new-report-suite/t-create-a-report-suite.html).


### Installare AEM Forms e [!DNL Adobe Analytics] estensioni {#install-extensions}

Esegui i seguenti passaggi per configurare AEM Forms e [Adobe Analytics](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/analytics/overview.html) estensioni:

1. Accedi a Adobe Experience Cloud e seleziona un nome appropriato per l’azienda.

1. Tocca **[!UICONTROL Launch/Raccolta dati]** e toccare **[!UICONTROL Vai a Launch/Raccolta dati]**.

1. Tocca **[!UICONTROL Nuova proprietà]** e specifica un nome per la configurazione.

1. Specifica un nome di dominio e tocca **[!UICONTROL Salva]** per salvare la proprietà.

1. Toccare il nome di configurazione disponibile nell’elenco delle Proprietà dei tag.

1. In **[!UICONTROL Authoring]** sezione, toccare **[!UICONTROL Estensioni]**.

1. Tocca **[!UICONTROL Catalogo]** e toccare **[!UICONTROL Installa]** per **[!UICONTROL Adobe Experience Manager Forms]** estensione. **[!UICONTROL Adobe Experience Manager Forms]** viene visualizzato nell’elenco delle estensioni installate disponibile nella **Installato** scheda .

1. Tocca **[!UICONTROL Installa]** per **[!UICONTROL Adobe Analytics]** estensione.
1. Seleziona il nome della suite di rapporti nel **[!UICONTROL Suite di rapporti per lo sviluppo]**, **[!UICONTROL Suite di rapporti per staging]** e **[!UICONTROL Suite di rapporti prodotto]** elenchi a discesa e toccare **[!UICONTROL Salva]** per salvare l&#39;estensione .

### Configurare gli elementi dati {#configure-data-elements}

Puoi selezionare uno qualsiasi degli elementi dati configurati in una regola creata per un evento. Quando si verifica un evento su un modulo adattivo, AEM Forms invia tali elementi dati a [!DNL Adobe Analytics].

Dopo aver installato **[!UICONTROL Adobe Experience Manager Forms]** Puoi creare i seguenti elementi dati:

<table>
 <tbody>
  <tr>
   <td>NomeCampo</th>
   <td>FieldTitle</th>
   <td>FormInstance</th>
  </tr>
  <tr>
   <td>NomeModulo<br /> </td>
   <td>FormTitle<br /> </td>
   <td>NomePagina</td>
  </tr>
  <tr>
   <td>PageURL<br /> </td>
   <td>PanelTitle<br /> </td>
   <td>TimeSpent</td>
  </tr>
 </tbody>
</table>

Esegui i seguenti passaggi per configurare gli elementi dati:

1. In **[!UICONTROL Authoring]** sezione, toccare **[!UICONTROL Elementi dati]**.

1. Tocca **[!UICONTROL Crea nuovo elemento dati]**.

1. Specifica un nome per l’elemento dati. Ad esempio, Titolo modulo per il tipo di elemento dati FormTitle.

1. Specifica **[!UICONTROL Adobe Experience Manager Forms]** come nome dell&#39;estensione.

1. Seleziona la **[!UICONTROL Tipo di elemento dati]**.

1. Tocca **[!UICONTROL Salva]** per salvare l’elemento dati.

   >[!VIDEO](https://video.tv.adobe.com/v/337472)

### Configurare le regole {#configure-rules}

Esegui i seguenti passaggi per creare regole basate su **[!UICONTROL Adobe Experience Manager Forms]** estensione:

1. In **[!UICONTROL Authoring]** sezione, toccare **[!UICONTROL Regole]**.

1. Tocca **[!UICONTROL Crea nuova regola]**.

1. Specifica un nome per la regola. Ad esempio, Invia modulo per registrare gli invii dei moduli.

1. In **[!UICONTROL Eventi]** sezione, toccare **[!UICONTROL Aggiungi]**.

1. Specifica **[!UICONTROL Adobe Experience Manager Forms]** come nome dell&#39;estensione.

1. Seleziona il tipo di evento. L&#39;input per **[!UICONTROL Nome]** viene compilato automaticamente in base al tipo di evento selezionato.

1. Tocca **[!UICONTROL Mantieni modifiche]** per salvare l’evento.

1. In **[!UICONTROL Azioni]** sezione, toccare **[!UICONTROL Aggiungi]**.

1. Specifica **[!UICONTROL Adobe Analytics]** come nome dell&#39;estensione.

1. Seleziona **[!UICONTROL Imposta variabili]** come Tipo di azione. Le opzioni disponibili nell’elenco a discesa includono:

   * **[!UICONTROL Imposta variabili]**: Utilizza questo tipo di azione per definire il tipo di evento per il quale gli elementi dati selezionati vengono inviati da AEM Forms a [!DNL Adobe Analytics].

   * **[!UICONTROL Invia beacon]**: Utilizza questo tipo di azione per inviare dati da AEM Forms a [!DNL Adobe Analytics].

   * **[!UICONTROL Cancella variabili]**: Utilizzare questo tipo di azione per cancellare il percorso dati in modo che l&#39;evento si registri una sola volta [!DNL Adobe Analytics].

      L’approccio consigliato consiste nell’utilizzare il **[!UICONTROL Imposta variabili]** tipo di azione per configurare l’evento e gli elementi dati, quindi utilizza **[!UICONTROL Invia beacon]** per inviare dati e quindi utilizzare **[!UICONTROL Cancella variabili]** cancellare la traccia dati.

1. In **[!UICONTROL Proprietà]** mappa le opzioni della suite di rapporti disponibili nell’elenco a discesa con gli elementi dati definiti utilizzando [Configurare gli elementi dati](#configure-data-elements).

   Ad esempio, per inviare **Titolo modulo** elemento dati da AEM Forms a [!DNL Adobe Analytics] quando si invia un modulo:
   1. In **[!UICONTROL Proprietà]** seleziona una proprietà per il titolo del modulo disponibile nella suite di rapporti, quindi tocca ![Icona del database](/help/forms/using/assets/database-icon.svg) per mapparlo su Titolo modulo creato in [Configurare gli elementi dati](#configure-data-elements).

      ![proprietà di definizione](/help/forms/using/assets/define-props.png)

   1. Tocca **[!UICONTROL Aggiungi un altro]** per aggiungere altri elementi dati all’elenco.

1. In **[!UICONTROL Eventi]** seleziona un evento dalle opzioni disponibili nella suite di rapporti e tocca **[!UICONTROL Mantieni modifiche]**.

1. In **[!UICONTROL Azioni]** sezione , tocca + e specifica **[!UICONTROL Adobe Analytics]** come nome dell&#39;estensione.

1. Seleziona **[!UICONTROL Invia beacon]** come Tipo di azione. Nel riquadro di destra, seleziona **[!UICONTROL s.t()]** per inviare dati a [!DNL Adobe Analytics] e lo considera come visualizzazione di una pagina o **[!UICONTROL s.tl()]** per inviare dati a [!DNL Adobe Analytics] e non trattarlo come visualizzazione di pagina. Tocca **[!UICONTROL Mantieni modifiche]**.

1. In **[!UICONTROL Azioni]** sezione , tocca + e specifica **[!UICONTROL Adobe Analytics]** come nome dell&#39;estensione.

1. Seleziona **[!UICONTROL Cancella variabili]** come Tipo di azione. Tocca **[!UICONTROL Mantieni modifiche]**. Dopo aver eseguito questi passaggi, la **[!UICONTROL Azioni]** viene visualizzata come:
   ![Configurazione azioni](/help/forms/using/assets/actions-config.png)

   Personalizzare **[!UICONTROL Azioni]** in base alle tue esigenze. Ad esempio, puoi definirne due **Invia beacon** passaggi di un flusso di azioni a cui inviare i dati [!DNL Adobe Analytics] e trattalo come una visualizzazione di pagina in un unico passaggio e invia i dati a [!DNL Adobe Analytics] e non trattarlo come visualizzazione di pagina nel secondo passaggio.

   ![Configurazione azioni](/help/forms/using/assets/actions-config-2.png)

1. Tocca **[!UICONTROL Salva]** per salvare la regola.

   Puoi creare regole per tutti i tipi di evento, ad esempio Abbandonare, Errore, Visita campo, Guida, Rendering, Salva e Invia.

   >[!VIDEO](https://video.tv.adobe.com/v/337425)


### Flussi di pubblicazione {#publish-flow}

Dopo aver creato gli elementi dati e averli utilizzati nelle regole, pubblica la configurazione per raccogliere i dati del modulo in [!DNL Adobe Analytics].

Esegui i seguenti passaggi per pubblicare la configurazione:

1. In **[!UICONTROL Pubblicazione]** sezione, toccare **[!UICONTROL Flusso di pubblicazione]**.

1. Tocca **[!UICONTROL Aggiungi libreria]** e specifica un nome e seleziona l&#39;ambiente per la libreria.

1. Tocca **[!UICONTROL Aggiungi tutte le risorse modificate]** quindi tocca **[!UICONTROL Salva e genera in sviluppo]**.

1. In **[!UICONTROL Sviluppo]** sezione, toccare ![Altre opzioni](/help/forms/using/assets/more-options-icon.svg) quindi tocca **[!UICONTROL Approvare e pubblicare in produzione]**.

1. Conferma le modifiche e il flusso di pubblicazione viene visualizzato presto nella sezione **[!UICONTROL Pubblicato]** sezione .

![Flusso di pubblicazione](/help/forms/using/assets/publish-flow.png)

## 2. Configurare AEM Forms {#configure-aem-forms}

Prima di creare la configurazione di Adobe Launch, crea un [Configurazione di Adobe IMS tramite Adobe Launch come soluzione Cloud](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/connect-aem-launch-adobe-io.html).

### Crea configurazione di Adobe Launch {#create-adobe-launch-configuration}

Esegui i seguenti passaggi per creare una configurazione di Adobe Launch:

1. Nell’istanza di authoring di AEM Forms, passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Configurazioni di Adobe Launch]**.

1. Seleziona una cartella per creare la configurazione e tocca **[!UICONTROL Crea]**.

1. Specifica un titolo per la configurazione nella **[!UICONTROL Titolo]** campo .

1. Seleziona la [configurazione Adobe IMS associata](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/connect-aem-launch-adobe-io.html).

1. Seleziona il nome della società utilizzata durante la [configurazione di Adobe Analytics](#Configure-adobe-analytics).

1. Seleziona il nome della proprietà creata mentre [configurazione di Adobe Analytics](#install-extensions).

1. Tocca **[!UICONTROL Salva e chiudi]**.

1. Pubblica la configurazione.

### Abilita [!DNL Adobe Analytics] per un modulo adattivo {#enable-analytics-adaptive-form}

Per utilizzare [!DNL Adobe Launch] configurazione in un modulo adattivo esistente:

1. Nell’istanza di authoring di AEM Forms, passa a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e documenti]**.
1. Seleziona il modulo adattivo e tocca **[!UICONTROL Proprietà]**.
1. In **[!UICONTROL Base]** seleziona la scheda [contenitore di configurazione](#create-adobe-launch-configuration) utilizzato durante la creazione della configurazione di Adobe Launch.
1. Tocca **[!UICONTROL Salva e chiudi]**. Il modulo adattivo è abilitato per [!DNL Adobe Analytics].
1. Pubblicare il modulo.

Dopo aver abilitato [!DNL Adobe Analytics] per un modulo adattivo, puoi [validate](https://experienceleague.adobe.com/docs/launch-learn/implementing-in-websites-with-launch/implement-solutions/analytics.html?lang=en#validate-the-page-view-beacon) se esiste un flusso di eventi di dati appropriato tra AEM Forms e [!DNL Adobe Analytics]. L’integrazione di AEM Forms con Adobe Analytics è completa. Ora puoi [configurare e visualizzare i rapporti in Adobe Analytics](#view-reports-adobe-analytics).

>[!NOTE]
>Nel caso in cui entrambi [Analytics con Cloud Service Framework](/help/forms/using/configure-analytics-forms-documents.md) e **Analytics con Adobe Launch** le funzioni sono abilitate simultaneamente, **Analytics con Adobe Launch** avrà la precedenza.

### Creare regole per acquisire eventi personalizzati (facoltativo) {#capture-custom-events}

Creare regole su campi specifici di un modulo adattivo utilizzando l’editor di regole per inviare dati di Analytics da un modulo adattivo a [!DNL Adobe Analytics].

In un processo in due fasi, si definisce una regola su un campo in un modulo adattivo. La regola invia un evento . Il nome dell’evento viene mappato su un evento di acquisizione personalizzato in Adobe Launch.

Per creare regole utilizzando l’editor di regole in un modulo adattivo:

1. Tocca il campo e seleziona ![Editor regole](/help/forms/using/assets/rule-editor-icon.svg) per aprire la pagina editor di regole.
1. Definire una condizione nel [!UICONTROL Quando] della regola.
1. In [!UICONTROL Then] sezione della regola, seleziona **[!UICONTROL Evento di invio]** dal **[!UICONTROL Seleziona azione]** elenco a discesa.
1. Specifica il nome dell’evento nel **[!UICONTROL Nome evento tipo]** campo .

Ad esempio, se la data di nascita è precedente a una data specifica, AEM Forms invia il **Sicurezza** evento.

![Evento di invio](/help/forms/using/assets/security-event.png)

Per mappare l’evento a un evento di acquisizione personalizzato in [!DNL Adobe Analytics]:

1. [Creare una regola](#configure-rules).

1. In **[!UICONTROL Eventi]** sezione, toccare **[!UICONTROL Aggiungi]**.

1. Specifica **[!UICONTROL Adobe Experience Manager Forms]** come nome dell&#39;estensione.

1. Seleziona **[!UICONTROL Acquisisci evento personalizzato]** dal **[!UICONTROL Tipo evento]** elenco a discesa.

1. Specifica il nome dell&#39;evento specificato al passaggio 4 durante la creazione di una regola utilizzando l&#39;editor di regole.

1. Tocca **Mantieni modifiche** ed esegue le altre azioni specificate in [Configurare le regole](#configure-rules).

## 3. Configurare e visualizzare i rapporti in [!DNL Adobe Analytics] {#view-reports-adobe-analytics}

Dopo aver configurato un modulo adattivo a cui inviare i dati dell’evento [!DNL Adobe Analytics], puoi iniziare a visualizzare i rapporti in [!DNL Adobe Analytics]:

1. Tocca ![Seleziona prodotto](/help/forms/using/assets/select-analytics.png) e seleziona **[!UICONTROL Analytics]**.

1. Tocca **[!UICONTROL Crea progetto]** e seleziona **[!UICONTROL Progetto vuoto]**.

1. Seleziona il nome della suite di rapporti dall’elenco a discesa in alto a destra nella forma libera.

1. Specifica **Titolo modulo** in **[!UICONTROL Ricerca di elementi dimensionali]** testo per visualizzare tutti i titoli dei moduli.

1. Rilascia il titolo del modulo adattivo al **[!UICONTROL Rilascia un segmento qui (o qualsiasi altro componente)]** casella di testo.

1. Da **[!UICONTROL Metriche]** , rilascia gli eventi a cui eseguire il tracciamento **[!UICONTROL Rilascia una metrica qui (o qualsiasi altro componente)]** casella di testo.

1. Tocca ![Visualizzazioni](/help/forms/using/assets/visualization-icon.svg) e rilascia un tipo di grafico nella sezione a forma libera. Analogamente, è possibile aggiungere più tipi di grafico alla sezione a forma libera.

1. Tocca Ctrl + S tasti e specifica un nome per salvare il progetto.

Per informazioni dettagliate sulla visualizzazione dei rapporti di analisi dei moduli, vedere [Visualizzazione e comprensione dei rapporti di AEM Forms Analytics](../../forms/using/view-understand-aem-forms-analytics-reports.md).