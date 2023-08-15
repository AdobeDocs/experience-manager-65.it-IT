---
title: Come integrare AEM Forms con Adobe Analytics?
description: AEM Forms si integra con Adobe Analytics per acquisire e tenere traccia delle metriche delle prestazioni per i moduli pubblicati.
docset: aem65
exl-id: 030fe9f2-cd41-4290-b8a6-2f9ade6b5789
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '1805'
ht-degree: 0%

---

# Analytics tramite [!DNL Adobe Launch] {#analyticsusingadobelaunch}

AEM Forms si integra con [Adobe Analytics](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/overview.html?lang=en) per acquisire e tenere traccia delle metriche delle prestazioni per i moduli pubblicati. L’obiettivo dell’analisi di queste metriche è consentire agli utenti aziendali di ottenere informazioni sul comportamento degli utenti finali e ottimizzare l’esperienza di acquisizione dei dati. Puoi acquisire e tenere traccia del comportamento degli utenti connessi e non connessi (anonimi) tramite Adobe Analytics for Adaptive Forms.

È inoltre possibile eseguire analisi utilizzando Framework di Cloud Service. Per ulteriori informazioni su come integrare AEM Forms con Cloud Service Framework, consulta [Analytics tramite Cloud Service Framework](/help/forms/using/configure-analytics-forms-documents.md). Il vantaggio principale dell’utilizzo di Adobe Launch rispetto ad Analytics utilizzando Cloud Service Framework è che puoi anche definire eventi personalizzati, oltre a questi eventi predefiniti. Gli eventi personalizzati vengono definiti utilizzando l’editor di regole o clientlibs e sono mappati su eventi in [!DNL Adobe Analytics].

Dopo aver eseguito le azioni menzionate in questo articolo, puoi configurare e visualizzare i rapporti in [!DNL Adobe Analytics], come illustrato nel seguente video:

>[!VIDEO](https://video.tv.adobe.com/v/337262)

È possibile utilizzare [!DNL Adobe Analytics] per individuare i pattern e i problemi di interazione che gli utenti devono affrontare durante l’utilizzo dei moduli adattivi. Pronti all’uso, [!DNL Adobe Analytics] tiene traccia e memorizza informazioni sui seguenti eventi:

* **Rendering**: numero di volte in cui un modulo viene aperto.

* **Invia**: numero di invii di un modulo.

* **Abbandona**: numero di volte in cui gli utenti se ne vanno senza completare il modulo.

* **Errore**: numero di errori rilevati nel pannello e nei relativi campi.

* **Aiuto**: numero di volte in cui un utente apre la guida di un pannello e i relativi campi.

* **Visita sul campo**: numero di volte in cui un utente visita un campo nel modulo.

* **Salva**: numero di volte in cui gli utenti salvano un modulo sul portale Forms.

Oltre a questi eventi predefiniti, puoi anche definire eventi personalizzati.

La figura seguente illustra le azioni da eseguire prima di visualizzare i rapporti in [!DNL Adobe Analytics]:

![Panoramica di Analytics](/help/forms/using/assets/analyticsworkflow.png)

## 1. Configurare [!DNL Adobe Analytics] {#Configure-adobe-analytics}

Prima della configurazione [!DNL Adobe Analytics], crea:

* Un Adobe ID a cui accedere [Adobe Experience Cloud](https://experience.adobe.com/#/home).
* A [suite di rapporti](https://experienceleague.adobe.com/docs/analytics/admin/manage-report-suites/new-report-suite/t-create-a-report-suite.html).


### Installare AEM Forms e [!DNL Adobe Analytics] estensioni {#install-extensions}

Per configurare AEM Forms e [Adobe Analytics](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/analytics/overview.html) estensioni:

1. Accedi a Adobe Experience Cloud e seleziona un nome appropriato per l’azienda.

1. Tocca **[!UICONTROL Launch/Raccolta dati]** e tocca **[!UICONTROL Vai a Launch/Raccolta dati]**.

1. Tocca **[!UICONTROL Nuova proprietà]** e specificate un nome per la configurazione.

1. Specifica un nome di dominio e tocca **[!UICONTROL Salva]** per salvare la proprietà.

1. Tocca il nome della configurazione disponibile nell’elenco Proprietà tag.

1. In **[!UICONTROL Authoring]** sezione, tocca **[!UICONTROL Estensioni]**.

1. Tocca **[!UICONTROL Catalogo]** e tocca **[!UICONTROL Installa]** per **[!UICONTROL Adobe Experience Manager Forms]** estensione. **[!UICONTROL Adobe Experience Manager Forms]** viene visualizzato nell&#39;elenco delle estensioni installate disponibili nella **Installato** scheda.

1. Tocca **[!UICONTROL Installa]** per **[!UICONTROL Adobe Analytics]** estensione.
1. Seleziona il nome della suite di rapporti in **[!UICONTROL Suite di rapporti per lo sviluppo]**, **[!UICONTROL Suite di rapporti per staging]**, e **[!UICONTROL Suite di rapporti sui prodotti]** elenchi a discesa e tocca **[!UICONTROL Salva]** per salvare l’estensione.

### Configurare gli elementi dati {#configure-data-elements}

Puoi selezionare uno qualsiasi degli elementi dati configurati in una regola creata per un evento. Quando si verifica un evento in un modulo adattivo, AEM Forms invia questi elementi di dati a [!DNL Adobe Analytics].

Dopo aver installato **[!UICONTROL Adobe Experience Manager Forms]** , puoi creare i seguenti elementi di dati:

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

Per configurare gli elementi dati, effettua le seguenti operazioni:

1. In **[!UICONTROL Authoring]** sezione, tocca **[!UICONTROL Elementi dati]**.

1. Tocca **[!UICONTROL Creare un nuovo elemento dati]**.

1. Specifica un nome per l’elemento dati. Ad esempio, Titolo modulo per il tipo di elemento dati FormTitle.

1. Specifica **[!UICONTROL Adobe Experience Manager Forms]** come nome dell’estensione.

1. Seleziona la **[!UICONTROL Tipo di elemento dati]**.

1. Tocca **[!UICONTROL Salva]** per salvare l’elemento dati.

   >[!VIDEO](https://video.tv.adobe.com/v/337472)

### Configurare le regole {#configure-rules}

Per creare regole basate su **[!UICONTROL Adobe Experience Manager Forms]** estensione:

1. In **[!UICONTROL Authoring]** sezione, tocca **[!UICONTROL Regole]**.

1. Tocca **[!UICONTROL Crea nuova regola]**.

1. Specifica un nome per la regola. Ad esempio, Invio modulo per registrare gli invii dei moduli.

1. In **[!UICONTROL Eventi]** sezione, tocca **[!UICONTROL Aggiungi]**.

1. Specifica **[!UICONTROL Adobe Experience Manager Forms]** come nome dell’estensione.

1. Seleziona il tipo di evento. Input per **[!UICONTROL Nome]** Il campo viene compilato automaticamente in base al tipo di evento selezionato.

1. Tocca **[!UICONTROL Mantieni modifiche]** per salvare l&#39;evento.

1. In **[!UICONTROL Azioni]** sezione, tocca **[!UICONTROL Aggiungi]**.

1. Specifica **[!UICONTROL Adobe Analytics]** come nome dell’estensione.

1. Seleziona **[!UICONTROL Imposta variabili]** come Tipo di azione. Le opzioni disponibili nell’elenco a discesa includono:

   * **[!UICONTROL Imposta variabili]**: utilizza questo tipo di azione per definire il tipo di evento per il quale gli elementi dati selezionati vengono inviati da AEM Forms a [!DNL Adobe Analytics].

   * **[!UICONTROL Invia beacon]**: utilizza questo tipo di azione per inviare dati da AEM Forms a [!DNL Adobe Analytics].

   * **[!UICONTROL Cancella variabili]**: utilizza questo tipo di azione per cancellare la traccia dati in modo che l’evento si registri una sola volta in [!DNL Adobe Analytics].

     L&#39;approccio consigliato è quello di utilizzare **[!UICONTROL Imposta variabili]** tipo di azione per configurare l’evento e gli elementi dati, quindi utilizza **[!UICONTROL Invia beacon]** per inviare dati e quindi utilizzare **[!UICONTROL Cancella variabili]** per cancellare la traccia dati.

1. In **[!UICONTROL Proprietà]** , mappa le opzioni della suite di rapporti disponibili nell’elenco a discesa con gli elementi dati definiti utilizzando [Configurare gli elementi dati](#configure-data-elements).

   Ad esempio, per inviare **Titolo modulo** elemento dati da AEM Forms a [!DNL Adobe Analytics] quando si invia un modulo:
   1. In **[!UICONTROL Proprietà]** , seleziona una proprietà per Titolo modulo disponibile nella suite di rapporti, quindi tocca ![Icona del database](/help/forms/using/assets/database-icon.svg) per mapparlo al Titolo modulo creato in [Configurare gli elementi dati](#configure-data-elements).

      ![define-props](/help/forms/using/assets/define-props.png)

   1. Tocca **[!UICONTROL Aggiungi un altro]** per aggiungere altri elementi dati all’elenco.

1. In **[!UICONTROL Eventi]** , seleziona un evento dalle opzioni disponibili nella suite di rapporti e tocca **[!UICONTROL Mantieni modifiche]**.

1. In **[!UICONTROL Azioni]** , tocca + e specifica **[!UICONTROL Adobe Analytics]** come nome dell’estensione.

1. Seleziona **[!UICONTROL Invia beacon]** come Tipo di azione. Nel riquadro di destra, selezionare **[!UICONTROL s.t()]** per inviare dati a [!DNL Adobe Analytics] e trattarla come una visualizzazione di pagina, oppure **[!UICONTROL s.tl()]** per inviare dati a [!DNL Adobe Analytics] e non trattarla come una visualizzazione di pagina. Tocca **[!UICONTROL Mantieni modifiche]**.

1. In **[!UICONTROL Azioni]** , tocca + e specifica **[!UICONTROL Adobe Analytics]** come nome dell’estensione.

1. Seleziona **[!UICONTROL Cancella variabili]** come Tipo di azione. Tocca **[!UICONTROL Mantieni modifiche]**. Dopo aver eseguito questi passaggi, il **[!UICONTROL Azioni]** La sezione viene visualizzata come:
   ![Configurazione azioni](/help/forms/using/assets/actions-config.png)

   Personalizzare **[!UICONTROL Azioni]** in base alle tue esigenze. Ad esempio, puoi definire due **Invia beacon** passaggi di un flusso di azioni a cui inviare i dati [!DNL Adobe Analytics] e trattarla come una visualizzazione di pagina in un unico passaggio e inviare i dati a [!DNL Adobe Analytics] e non trattarla come una visualizzazione di pagina nel secondo passaggio.

   ![Configurazione azioni](/help/forms/using/assets/actions-config-2.png)

1. Tocca **[!UICONTROL Salva]** per salvare la regola.

   Puoi creare regole per tutti i tipi di evento, ad esempio Abbandona, Errore, Visita campo, Aiuto, Rendering, Salva e Invia.

   >[!VIDEO](https://video.tv.adobe.com/v/337425)


### Flussi di pubblicazione {#publish-flow}

Dopo aver creato gli elementi dati e averli utilizzati nelle regole, pubblica la configurazione per raccogliere i dati del modulo in [!DNL Adobe Analytics].

Per pubblicare la configurazione, effettua le seguenti operazioni:

1. In **[!UICONTROL Pubblicazione]** sezione, tocca **[!UICONTROL Flusso di pubblicazione]**.

1. Tocca **[!UICONTROL Aggiungi libreria]** e specifica un nome e seleziona l’ambiente per la libreria.

1. Tocca **[!UICONTROL Aggiungi tutte le risorse modificate]** e quindi tocca **[!UICONTROL Salva e genera in sviluppo]**.

1. In **[!UICONTROL Sviluppo]** sezione, tocca ![Altre opzioni](/help/forms/using/assets/more-options-icon.svg) e quindi tocca **[!UICONTROL Approva e pubblica in produzione]**.

1. Conferma le modifiche e il flusso di pubblicazione verrà presto visualizzato in **[!UICONTROL Pubblicato]** sezione.

![Flusso di pubblicazione](/help/forms/using/assets/publish-flow.png)

## 2. Configurare AEM Forms {#configure-aem-forms}

Prima di creare la configurazione di Adobe Launch, crea un’ [Configurazione Adobe IMS con Adobe Launch come soluzione cloud](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/connect-aem-launch-adobe-io.html).

### Crea configurazione di Adobe Launch {#create-adobe-launch-configuration}

Per creare una configurazione Launch di Adobe, effettua le seguenti operazioni:

1. Nell’istanza Autore di AEM Forms, passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Configurazioni di Adobe Launch]**.

1. Seleziona una cartella per creare la configurazione e tocca **[!UICONTROL Crea]**.

1. Specifica un titolo per la configurazione nella **[!UICONTROL Titolo]** campo.

1. Seleziona la [configurazione Adobe IMS associata](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/connect-aem-launch-adobe-io.html).

1. Seleziona il nome della società utilizzato durante la [configurazione di Adobe Analytics](#Configure-adobe-analytics).

1. Seleziona il nome della proprietà creata durante la [configurazione di Adobe Analytics](#install-extensions).

1. Tocca **[!UICONTROL Salva e chiudi]**.

1. Pubblica la configurazione.

### Abilita [!DNL Adobe Analytics] per un modulo adattivo {#enable-analytics-adaptive-form}

Da utilizzare [!DNL Adobe Launch] configurazione in un modulo adattivo esistente:

1. Nell’istanza Autore di AEM Forms, passa a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e documenti]**.
1. Seleziona il modulo adattivo e tocca **[!UICONTROL Proprietà]**.
1. In **[!UICONTROL Base]** , seleziona la scheda [Contenitore configurazione](#create-adobe-launch-configuration) utilizzato durante la creazione della configurazione di Adobe Launch.
1. Tocca **[!UICONTROL Salva e chiudi]**. Il modulo adattivo è abilitato per [!DNL Adobe Analytics].
1. Pubblica il modulo.

Dopo aver abilitato [!DNL Adobe Analytics] per un modulo adattivo è possibile: [convalida](https://experienceleague.adobe.com/docs/launch-learn/implementing-in-websites-with-launch/implement-solutions/analytics.html?lang=en#validate-the-page-view-beacon) se esiste un flusso di eventi di dati appropriato tra AEM Forms e [!DNL Adobe Analytics]. L’integrazione di AEM Forms con Adobe Analytics è completa. Ora puoi [configurare e visualizzare i rapporti in Adobe Analytics](#view-reports-adobe-analytics).

>[!NOTE]
>Nel caso in cui entrambi [Analytics tramite Cloud Service Framework](/help/forms/using/configure-analytics-forms-documents.md) e **Analytics utilizzando Adobe Launch** le funzioni di siano attivate simultaneamente, **Analytics utilizzando Adobe Launch** avrà la precedenza.
> 

### Creare regole per acquisire eventi personalizzati (facoltativo) {#capture-custom-events}

Creare regole su campi specifici di un modulo adattivo utilizzando l’editor di regole per inviare dati di Analytics da un modulo adattivo a [!DNL Adobe Analytics].

In un processo in due fasi, puoi definire una regola su un campo in un modulo adattivo. La regola invia un evento. Il nome dell’evento è mappato a un evento di acquisizione personalizzato in Adobe Launch.

Per creare regole utilizzando l’editor di regole in un modulo adattivo:

1. Tocca il campo e seleziona ![Editor regole](/help/forms/using/assets/rule-editor-icon.svg) per aprire la pagina editor di regole.
1. Definire una condizione in [!UICONTROL Quando] sezione della regola.
1. In [!UICONTROL Then] sezione della regola, seleziona **[!UICONTROL Evento di invio]** dal **[!UICONTROL Seleziona azione]** elenco a discesa.
1. Specifica il nome dell’evento nel **[!UICONTROL Digita nome evento]** campo.

Ad esempio, se la data di nascita è precedente a una determinata data, AEM Forms invia il **Sicurezza** evento.

![Evento di invio](/help/forms/using/assets/security-event.png)

Per mappare l’evento a un evento di acquisizione personalizzato in [!DNL Adobe Analytics]:

1. [Creare una regola](#configure-rules).

1. In **[!UICONTROL Eventi]** sezione, tocca **[!UICONTROL Aggiungi]**.

1. Specifica **[!UICONTROL Adobe Experience Manager Forms]** come nome dell’estensione.

1. Seleziona **[!UICONTROL Acquisisci evento personalizzato]** dal **[!UICONTROL Tipo di evento]** elenco a discesa.

1. Specifica il nome dell&#39;evento specificato nel passaggio 4 durante la creazione di una regola tramite l&#39;editor di regole.

1. Tocca **Mantieni modifiche** ed eseguire le altre azioni specificate in [Configurare le regole](#configure-rules).

## 3. Configurare e visualizzare i rapporti in [!DNL Adobe Analytics] {#view-reports-adobe-analytics}

Dopo aver configurato un modulo adattivo per l’invio dei dati evento a [!DNL Adobe Analytics], puoi iniziare a visualizzare i rapporti in [!DNL Adobe Analytics]:

1. Tocca ![Seleziona prodotto](/help/forms/using/assets/select-analytics.png) e seleziona **[!UICONTROL Analytics]**.

1. Tocca **[!UICONTROL Crea progetto]** e seleziona **[!UICONTROL Progetto vuoto]**.

1. Seleziona il nome della suite di rapporti dall’elenco a discesa in alto a destra nella figura a forma libera.

1. Specifica **Titolo modulo** nel **[!UICONTROL Cercare elementi dimensionali]** testo per visualizzare tutti i titoli dei moduli.

1. Rilascia il titolo del modulo adattivo in **[!UICONTROL Rilascia qui un segmento (o qualsiasi altro componente)]** casella di testo.

1. Dalla sezione **[!UICONTROL Metriche]** , rilascia gli eventi per tenere traccia di **[!UICONTROL Rilascia qui una metrica (o qualsiasi altro componente)]** casella di testo.

1. Tocca ![Visualizzare](/help/forms/using/assets/visualization-icon.svg) e rilascia un tipo di grafico nella sezione a forma libera. Analogamente, è possibile aggiungere più tipi di grafico alla sezione a forma libera.

1. Tocca Ctrl + S e specifica un nome per salvare il progetto.

Per informazioni dettagliate sulla visualizzazione dei rapporti di Forms Analytics, consulta [Visualizzazione e comprensione dei rapporti di AEM Forms Analytics](../../forms/using/view-understand-aem-forms-analytics-reports.md).
