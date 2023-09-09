---
title: Creare un modulo adattivo
seo-title: Learn how to create a Core Components based Adaptive Form on AEM 6.5 Forms.
description: Scopri come creare un modulo adattivo utilizzando [!DNL Experience Manager Forms]. I Forms adattivi sono moduli HTML5 reattivi che semplificano la raccolta e l’elaborazione delle informazioni. Approfondisci le modalità di creazione di un modulo adattivo basato su un modello di dati modulo e uno schema XML o JSON.
seo-description: Learn how to create an Adaptive Form using [!DNL Experience Manager Forms]. Adaptive Forms are responsive HTML5 forms that streamline information gathering and processing. Dig deeper on how to create an Adaptive Form based on a Form Data Model and XML or JSON schema.
Keywords: create adaptive form core component, create core component based adaptive form, creare adaptive form
products: SG_EXPERIENCEMANAGER/6.5/FORMS
contentOwner: Khushwant Singh
topic-tags: Adaptive Forms
docset: aem65
role: Admin, Developer
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '1794'
ht-degree: 23%

---


# Creazione di componenti core basati su Adaptive Forms {#creating-an-adaptive-form-core-components}


<span class="preview"> L’Adobe consiglia di utilizzare i Componenti core per [aggiungere un Forms adattivo a una pagina AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md) o a [creare un Forms adattivo indipendente](/help/forms/using/create-an-adaptive-form-core-components.md). </span>

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form-core-components.html?lang=it) |
| AEM 6.5 | Questo articolo |

**Si applica a:** ❎ dei componenti core del modulo adattivo ✅ [Componenti di base per moduli adattivi](/help/forms/using/create-adaptive-form.md).

I moduli adattivi consentono di creare moduli coinvolgenti e reattivi, che si rivelano, inoltre, dinamici e adattivi. AEM Forms fornisce un’interfaccia utente intuitiva per la creazione rapida di Adaptive Forms. L’interfaccia utente offre una navigazione rapida a schede per selezionare facilmente modelli, stili, campi e opzioni di invio preconfigurati e creare un modulo adattivo.

Prima di iniziare, scopri i tipi di componenti dei moduli disponibili:

* [Componenti core dei moduli adattivi](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=it): si tratta di componenti di acquisizione dati standardizzati. Questi componenti forniscono funzionalità di personalizzazione e riducono i tempi di sviluppo e i costi di manutenzione per le esperienze di registrazione digitale. Uno sviluppatore può facilmente personalizzare e assegnare uno stile a questi componenti. L’Adobe consiglia di sfruttare questi componenti moderni ed estensibili per sviluppare Forms adattivo.

* [Componenti di base dei moduli adattivi](creating-adaptive-form.md): si tratta dei classici (precedenti) componenti di acquisizione dati. Puoi continuare a utilizzarli per modificare i componenti di base esistenti basati su modulo adattivo. Se stai creando moduli, l’Adobe consiglia di utilizzare  [Componenti core Forms adattivi](/help/forms/using/create-adaptive-form.md) per creare un Forms adattivo.

## Prerequisiti

Per creare un modulo adattivo è necessario quanto segue:

* **Abilitare i componenti core Forms adattivi per il tuo ambiente**: è richiesto il progetto Archetipo AEM versione 41 o successiva per [abilitare i Componenti core per il tuo ambiente](/help/forms/using/enable-adaptive-forms-core-components.md). Quando si abilitano i Componenti core per l’ambiente, viene **Forms adattivo (componente core)** Il modello e il tema Canvas vengono aggiunti al tuo ambiente.

* **Un modello di modulo adattivo**: un modello fornisce una struttura di base e definisce l’aspetto (layout e stili) di un modulo adattivo. Include componenti preformattati contenenti determinate proprietà e struttura del contenuto. Fornisce inoltre le opzioni per definire un tema e un’azione di invio. Il tema definisce l’aspetto, mentre l’azione di invio definisce l’azione da intraprendere al momento dell’invio di un modulo adattivo. Puoi anche distribuire [modelli di esempio](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html) nell&#39;ambiente. che consentono di iniziare a creare rapidamente i moduli.

  >[!NOTE]
  >
  > Se non disponi del modello **Moduli adattivi (componente core)** nell’ambiente, [abilita la funzione Componenti core dei moduli adattivi per il tuo ambiente](/help/forms/using/enable-adaptive-forms-core-components.md). Quando abiliti i componenti core per il tuo ambiente, viene aggiunto il modello **Moduli adattivi (componente core)**.

* **Un tema per moduli adattivi**: un tema contiene dettagli sullo stile dei componenti e dei pannelli. Gli stili includono proprietà quali i colori di sfondo, i colori degli stati, la trasparenza, l’allineamento e le dimensioni. Quando applichi un tema, lo stile specificato si riflette sui componenti corrispondenti.  Il `Canvas` Il tema viene aggiunto per impostazione predefinita quando abiliti i componenti core per il tuo ambiente. È possibile  [scaricare e personalizzare i temi standard](create-or-customize-themes-for-adaptive-forms-core-components.md). Per **pronto all’uso** temi che puoi distribuire [temi di esempio](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html) nell&#39;ambiente. In questo modo è possibile iniziare a definire lo stile dei moduli e fornire una struttura di base per creare o personalizzare un tema in base alle proprie esigenze aziendali.

* **Autorizzazioni**: aggiungi gli utenti a un gruppo [!DNL forms-users]. I membri del gruppo [!DNL forms-users] dispongono delle autorizzazioni per creare un modulo adattivo. Per un elenco dettagliato dei gruppi di utenti specifici per moduli, consulta [Gruppi e autorizzazioni](forms-groups-privileges-tasks.md).

<!--
>[!NOTE]
>
>
> In addition to the given themes and templates when you enable Core Components, you can also deploy the latest out-of-the box [sample themes and templates](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html) to your AEM environment for use in Core Components based Adaptive Forms.
-->

## Creare un modulo adattivo {#create-an-adaptive-form}

1. Accedi al tuo account locale [Istanza di authoring AEM](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/deploy.html?lang=en#author-and-publish-installs).

1. Inserisci le credenziali nella pagina di accesso di Experience Manager. Dopo aver effettuato l’accesso, nell’angolo in alto a sinistra tocca **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Moduli]** > **[!UICONTROL Moduli e documenti]**.

1. Tocca **[!UICONTROL Crea]**  > **[!UICONTROL Creare un Forms adattivo]**.

1. Seleziona un modello di Componenti core Forms adattivi e fai clic su **[!UICONTROL Successivo]**.

1. Il **[!UICONTROL Aggiungi proprietà]** viene visualizzato. Specificare i valori per i seguenti campi proprietà. I campi Titolo e Nome sono obbligatori:

   * **[!UICONTROL Titolo:]** Specifica il nome visualizzato del modulo. Il titolo consente di identificare il modulo nell’interfaccia utente di [!DNL Experience Manager Forms].
   * **[!UICONTROL Nome:]** specifica il nome del modulo. Nell’archivio viene creato un nodo con il nome specificato. Quando si inizia a digitare un titolo, il valore del campo nome viene generato automaticamente. Puoi modificare il valore suggerito. Il campo nome può contenere solo caratteri alfanumerici, trattini e caratteri di sottolineatura.
   * **[!UICONTROL Descrizione:]** Specifica le informazioni dettagliate sul modulo.
   * **[!UICONTROL Libreria client tema]:** Specifica il tema per un modulo adattivo. Per impostazione predefinita, il `adaptiveform.theme.canvas3` Il tema è selezionato. Puoi anche scegliere un tema diverso dal **[!UICONTROL Libreria client tema]** menu a discesa.
   * **[!UICONTROL Contenitore configurazione:]**  Definisce un percorso in cui vengono memorizzati i file di configurazione per Adaptive Forms. Questi file di configurazione contengono impostazioni e proprietà relative al comportamento e all’aspetto di Adaptive Forms.
   * **[!UICONTROL Tag:]** Specifica i tag per identificare in modo univoco il modulo adattivo. Aiuto sui tag nella ricerca nel modulo. Per creare i tag, digita i nuovi nomi dei tag nel **[!UICONTROL Tag]** casella.
1. Tocca **[!UICONTROL Crea]**. Viene creato un modulo adattivo e viene visualizzata una finestra di dialogo per aprire il modulo per la modifica.


1. Tocca **[!UICONTROL Modifica]** per aprire il modulo appena creato in una nuova scheda. Il modulo si apre per la modifica e visualizza il contenuto disponibile nel modello. Viene inoltre visualizzata la barra laterale per personalizzare il modulo appena creato.


## Utilizzare i componenti core di Forms adattivi per creare il modulo

Dopo aver aperto il modulo per la modifica, puoi utilizzare i componenti core Forms adattivi disponibili per aggiungere campi modulo al modulo. Puoi trascinare e rilasciare o utilizzare il tasto + [inserisci componente] per aggiungere questi componenti a un modulo. Per informazioni sulle funzioni disponibili, consulta la documentazione sui Componenti core AEM [Componenti core Forms adattivi](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=it#components). Puoi anche visitare [https://aemcomponents.dev/](https://aemcomponents.dev/) per visualizzare i componenti core disponibili in azione.

## Configurare l’azione di invio per un modulo adattivo {#configure-submit-action-for-form}

Un’azione di invio consente di scegliere la destinazione dei dati acquisiti tramite un modulo adattivo. Viene attivato quando un utente fa clic sul pulsante Invia in un modulo adattivo. I moduli adattivi includono alcune azioni di invio pronte all’uso. Puoi anche estendere un’azione di invio predefinita per creare un’azione di invio personalizzata. Per configurare un&#39;azione di invio per il modulo:

1. Apri il browser Contenuto e seleziona la **[!UICONTROL Contenitore guida]** componente del modulo adattivo.
1. Fai clic sulle proprietà Contenitore guida ![Proprietà guida](/help/forms/using/assets/configure-icon.svg) icona. Viene visualizzata la finestra di dialogo Contenitore modulo adattivo (Adaptive Form Container).

1. Fai clic su  **[!UICONTROL Invio]** scheda.

   ![Fai clic sull’icona chiave inglese per aprire la finestra di dialogo Contenitore modulo adattivo e configurare un’azione di invio](/help/forms/using/assets/adaptive-forms-submit-message.png)

1. Seleziona e configura un **[!UICONTROL Azione di invio]**, in base alle tue esigenze. Per informazioni dettagliate sulle azioni di invio, vedere [Azione di invio modulo adattivo](/help/forms/using/configuring-submit-actions.md)

<!--
    
    ![Click the Wrench icon to open Adaptive Form Container dialog box to configure Data Models for the Adaptive Form Container component](/help/forms/assets/adaptive-forms-container.png)

-->

## Reindirizza l’utente a una pagina o mostra un messaggio di ringraziamento all’invio del modulo

All&#39;invio di un modulo è possibile reindirizzare l&#39;utente a un&#39;altra pagina Web o a un messaggio. Per reindirizzare l’utente o configurare il messaggio di ringraziamento:

1. Apri il browser Contenuto e seleziona la **[!UICONTROL Contenitore guida]** componente del modulo adattivo.
1. Fai clic sulle proprietà Contenitore guida ![Proprietà guida](/help/forms/using/assets/configure-icon.svg) icona. Viene visualizzata la finestra di dialogo Contenitore modulo adattivo (Adaptive Form Container).
1. Apri **[!UICONTROL Invio]** scheda.

   ![Fai clic sull’icona chiave inglese per aprire la finestra di dialogo Contenitore modulo adattivo per configurare una pagina di reindirizzamento o un messaggio di ringraziamento](/help/forms/using/assets/adaptive-forms-submit-message.png)

   * Per configurare un URL di reindirizzamento, per l’opzione Invia seleziona la **[!UICONTROL Reindirizza a URL]** e sfoglia e seleziona una pagina AEM Sites oppure specifica l’URL di una pagina esterna.

   * Per configurare un messaggio personalizzato o di ringraziamento, per all’opzione Invia, seleziona la **[!UICONTROL Mostra messaggio]** e inserisci un messaggio nella sezione **[!UICONTROL Contenuto del messaggio]** casella. Si tratta di una casella di testo RTF, è possibile utilizzare l&#39;opzione a schermo intero per visualizzare tutti gli elementi RTF disponibili.

## Configurare uno schema o un modello di dati del modulo per un modulo adattivo {#configure-schema-or-data-model-for-form}

È possibile utilizzare il modello dati modulo per collegare un modulo a un&#39;origine dati per inviare e ricevere dati in base alle azioni degli utenti. Puoi anche collegare un modulo a uno schema JSON per ricevere i dati inviati in un formato predefinito. In base al requisito, connetti il modulo a uno schema JSON o a un modello di dati del modulo:

* [Creare uno schema JSON e caricarlo nell’ambiente](/help/forms/using/adaptive-form-json-schema-form-model.md)
* [Creare un modello di dati modulo](/help/forms/using/create-form-data-models.md)

### Configurare uno schema JSON o un modello dati modulo per il modulo

Per configurare uno schema JSON o un modello dati modulo per il modulo:

1. Apri il browser Contenuto e seleziona la **[!UICONTROL Contenitore guida]** componente del modulo adattivo.
1. Fai clic sulle proprietà Contenitore guida ![Proprietà guida](/help/forms/using/assets/configure-icon.svg) icona. Viene visualizzata la finestra di dialogo Contenitore modulo adattivo (Adaptive Form Container).
1. Apri **[!UICONTROL Modello dati]** scheda.

   ![Fai clic sull’icona chiave inglese per aprire la finestra di dialogo Contenitore modulo adattivo per configurare uno schema JSON o un modello di dati del modulo](/help/forms/using/assets/adaptive-forms-select-form-data-model-or-json-schema.png)

1. Seleziona e configura uno schema JSON o un modello dati modulo, in base ai requisiti:

   * Quando selezioni il **[!UICONTROL Modello modulo]** , utilizza **[!UICONTROL Seleziona modello dati modulo]** per selezionare un modello di dati modulo preconfigurato.
   * Quando selezioni il **[!UICONTROL Schema]** , utilizza **[!UICONTROL Schema]** per selezionare uno schema JSON per il modulo.

1. Clic **[!UICONTROL Fine]**.

>[!NOTE]
>
> Puoi modificare lo schema JSON o il modello dati del modulo per un modulo adattivo utilizzando le proprietà Contenitore guida.

## Configurare un servizio di precompilazione  {#configure-prefill-service-for-form}

Puoi utilizzare il servizio di precompilazione per compilare automaticamente i campi di un modulo adattivo utilizzando dati esistenti. Quando un utente apre un modulo, i valori di tali campi vengono precompilati. Operazioni disponibili:

* [Creare un servizio di precompilazione personalizzato](/help/forms/using/prepopulate-adaptive-form-fields.md)
* [Utilizza il servizio di precompilazione del modello dati del modulo](#fdm-prefill-service)

### Utilizzare il servizio di precompilazione del modello dati modulo per precompilare i campi di un modulo adattivo {#fdm-prefill-service}

È possibile utilizzare il servizio di precompilazione del modello dati modulo per precompilare i campi di un modulo adattivo utilizzando un modello dati modulo o un servizio di precompilazione personalizzato. Il servizio di precompilazione del modello dati del modulo utilizza [Ottieni il servizio del modello di dati del modulo configurato](work-with-form-data-model.md#add-data-model-objects-and-services-add-data-model-objects-and-services) per recuperare i dati. Per utilizzare il servizio di precompilazione del modello dati modulo per un modulo adattivo:

1. Apri il browser Contenuto e seleziona la **[!UICONTROL Contenitore guida]** componente del modulo adattivo.
1. Fai clic sulle proprietà Contenitore guida ![Proprietà guida](/help/forms/using/assets/configure-icon.svg) icona. Viene visualizzata la finestra di dialogo Contenitore modulo adattivo (Adaptive Form Container).
1. Fai clic sulle proprietà Contenitore modulo adattivo ![Proprietà contenitore modulo adattivo](/help/forms/using/assets/configure-icon.svg) icona. Viene visualizzata la finestra di dialogo Contenitore modulo adattivo per configurare i modelli dati.
   ![Fai clic sull’icona chiave inglese per aprire la finestra di dialogo Contenitore modulo adattivo per configurare una pagina di reindirizzamento o un messaggio di ringraziamento](/help/forms/using/assets/adaptive-forms-container-prefill-service.png)
1. Seleziona un modello di dati modulo. Apri **[!UICONTROL Base]** scheda. Nel servizio di preriempimento, seleziona **[!UICONTROL Servizio preriempimento modello dati modulo]**.
1. Clic **[!UICONTROL Fine]**. Il modulo adattivo è ora configurato per l’utilizzo della precompilazione del modello dati del modulo. Ora è possibile utilizzare [editor di regole](rule-editor.md) per creare regole per precompilare i campi del modulo.

<!--
## Edit Form Model properties of an Adaptive Form {#edit-form-model}

1. Select the Adaptive Form and tap ![Page information](/help/forms/using/assets/configure-icon.svg) > **[!UICONTROL Open Properties]**. The Form Properties page opens. 

1. Go to the **[!UICONTROL Form Model]** tab and choose a form model. If the Adaptive Form is without a form model, you have the freedom to choose either a JSON schema or a form data model. On the other hand, if the Adaptive Form is already based on a form model, you have the option to switch to another form model of the same type. For instance, if the form is using a JSON schema, you can easily switch to another JSON schema, and similarly if the form is using a Form Data Model, you can switch to another Form Data Model. 

1. Tap **[!UICONTROL Save]** to save the properties.
-->

## Passaggio successivo

* [Utilizza l’editor di regole per aggiungere un comportamento dinamico al modulo](rule-editor.md)
* [Creazione o personalizzazione di temi per Forms adattivo basato su Componenti core](create-or-customize-themes-for-adaptive-forms-core-components.md)


## Consulta anche

* [Creare componenti core basati sul modulo adattivo](create-an-adaptive-form-core-components.md)
* [Creare o aggiungere un modulo adattivo a una pagina o a un frammento di esperienza di AEM Sites](create-or-add-an-adaptive-form-to-aem-sites-page.md)
* [Modelli di temi e modelli di dati modulo di esempio](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html)
