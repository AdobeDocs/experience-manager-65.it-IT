---
title: Usa modello dati modulo
seo-title: Usa modello dati modulo
description: Scoprite come utilizzare il modello dati del modulo per creare e utilizzare moduli adattivi e comunicazioni interattive.
seo-description: Scoprite come utilizzare il modello dati del modulo per creare e utilizzare moduli adattivi e comunicazioni interattive.
uuid: 9d8d8f43-9a50-4905-a6ef-a5ea3b9c11f7
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integration
discoiquuid: 87f5f9f5-2d03-4565-830e-eacc3757e542
docset: aem65
translation-type: tm+mt
source-git-commit: ebf3f34af7da6b1a659ac8d8843152b97f30b652
workflow-type: tm+mt
source-wordcount: '1273'
ht-degree: 0%

---


# Usa modello dati modulo{#use-form-data-model}

![](do-not-localize/data-integeration.png)

&#39;integrazione dei dati AEM Forms consente di utilizzare origini dati back-end diverse per creare un modello dati del modulo da utilizzare come schema in vari moduli adattivi e flussi di lavoro di comunicazione interattiva. Richiede la configurazione delle origini dati e la creazione di un modello dati modulo basato su oggetti e servizi del modello dati disponibili nelle origini dati. Per ulteriori informazioni, consulta gli argomenti di seguito:

* [Integrazione dei dati  AEM Forms](../../forms/using/data-integration.md)
* [Configurare le origini dati](../../forms/using/configure-data-sources.md)
* [Crea modello dati modulo](../../forms/using/create-form-data-models.md)
* [Uso del modello dati del modulo](../../forms/using/work-with-form-data-model.md)

Un modello dati modulo è un&#39;estensione dello schema JSON che è possibile utilizzare per:

* [Creazione di moduli e frammenti adattivi](#create-af)
* [Creazione di comunicazioni interattive e di blocchi costitutivi come testo, frammenti di elenco e condizione](#create-ic)
* [Anteprima di comunicazioni interattive con dati di esempio](#preview-ic)
* [Precompilare moduli adattivi e comunicazioni interattive](#prefill)
* [Reinserimento dei dati del modulo adattivo inviati nelle origini dati](#write-af)
* [Richiamo di servizi utilizzando le regole del modulo adattivo](#invoke-services)

## Creazione di moduli e frammenti adattivi {#create-af}

È possibile creare [moduli adattivi](../../forms/using/creating-adaptive-form.md) e [frammenti di modulo adattivo](../../forms/using/adaptive-form-fragments.md) in base a un modello dati del modulo. Per utilizzare un modello dati modulo durante la creazione di un modulo adattivo o di un frammento di modulo adattivo, effettuare le seguenti operazioni:

1. Nella scheda Modello modulo della schermata Aggiungi proprietà, selezionare **[!UICONTROL Modello dati modulo]** nell&#39;elenco a discesa **[!UICONTROL Seleziona da]**.

   ![create-af-1-1](assets/create-af-1-1.png)

1. Toccate per espandere **[!UICONTROL Seleziona modello dati modulo]**. Vengono elencati tutti i modelli di dati del modulo disponibili.

   Selezionare un modello dati da.

   ![create-af-2-1](assets/create-af-2-1.png)

1. (**Solo frammenti di modulo adattivo**) È possibile creare un frammento di modulo adattivo basato su un solo oggetto modello dati in un modello dati del modulo. Espandi il menu a discesa **[!UICONTROL Definizioni dei modelli di dati del modulo]**. Elenca tutti gli oggetti del modello dati nel modello dati del modulo specificato. Selezionare un oggetto modello dati dall&#39;elenco.

   ![create-af-3](assets/create-af-3.png)

Una volta creato il frammento di modulo adattivo o di modulo adattivo basato su un modello dati del modulo, gli oggetti del modello dati del modulo vengono visualizzati nella scheda **[!UICONTROL Oggetti modello dati]** del browser Contenuto nell&#39;editor di moduli adattivi.

>[!NOTE]
>
>Per un frammento di modulo adattivo, nella scheda Oggetti modello dati viene visualizzato solo l&#39;oggetto modello dati selezionato al momento dell&#39;authoring e gli oggetti modello dati associati.

![data-model-objects-tab](assets/data-model-objects-tab.png)

È possibile trascinare gli oggetti modello dati sul modulo adattivo o sul frammento per aggiungere campi modulo. I campi modulo aggiunti mantengono le proprietà dei metadati e il binding con le proprietà dell&#39;oggetto modello dati. Il binding assicura che i valori dei campi siano aggiornati nelle origini dati corrispondenti all&#39;invio del modulo e precompilati al momento del rendering del modulo.

## Creazione di comunicazioni interattive {#create-ic}

È possibile creare una comunicazione interattiva basata su un modello dati modulo che è possibile utilizzare per precompilare la comunicazione interattiva con i dati provenienti da origini dati configurate. Inoltre, gli elementi costitutivi di una comunicazione interattiva, quali i frammenti di testo, elenco e condizione, possono essere basati su un modello dati del modulo.

Durante la creazione di una comunicazione interattiva o di un frammento di documento è possibile scegliere un modello di dati del modulo. Nell&#39;immagine seguente è visualizzata la scheda Generale della finestra di dialogo Crea comunicazione interattiva.

![create-ic](assets/create-ic.png)

Scheda Generale della finestra di dialogo Crea comunicazione interattiva

Per ulteriori informazioni, vedere:

[Creazione di una comunicazione interattiva](../../forms/using/create-interactive-communication.md)

[Testo nelle comunicazioni interattive](/help/forms/using/texts-interactive-communications.md)

[Condizioni nelle comunicazioni interattive](/help/forms/using/conditions-interactive-communications.md)

[Elenca frammenti](/help/forms/using/lists.md)

## Anteprima con dati di esempio {#preview-ic}

L&#39;editor dei modelli di dati per moduli consente di generare e modificare dati di esempio per gli oggetti del modello di dati nel modello di dati del modulo. È possibile utilizzare questi dati per visualizzare l&#39;anteprima e verificare le comunicazioni interattive e i moduli adattivi. È necessario generare i dati di esempio prima di visualizzare l&#39;anteprima come descritto in [Utilizzare il modello dati del modulo](../../forms/using/work-with-form-data-model.md#sample).

Per visualizzare in anteprima una comunicazione interattiva con dati del modello dati del modulo di esempio:

1. Per AEM&#39;istanza di creazione, andate a **[!UICONTROL Forms > Forms &amp; Documents]**.
1. Selezionate una comunicazione interattiva e toccate **[!UICONTROL Anteprima]** nella barra degli strumenti per selezionare **[!UICONTROL Canale Web]**, **[!UICONTROL Canale di stampa]** o **[!UICONTROL Entrambi i canali]** per visualizzare l&#39;anteprima della comunicazione interattiva.
1. Nella finestra di dialogo Anteprima [*canale*], assicurarsi che l&#39;opzione **[!UICONTROL Test Data of Form Data Model]** sia selezionata e toccare **[!UICONTROL Preview]**.

Si apre la comunicazione interattiva con dati di esempio precompilati.

![web-preview](assets/web-preview.png)

Allo stesso modo, per visualizzare in anteprima un modulo adattivo con dati di esempio, aprire il modulo adattivo in modalità di creazione e toccare **[!UICONTROL Anteprima]**.

## Precompilazione tramite il servizio del modello dati del modulo {#prefill}

 AEM Forms fornisce un servizio di precompilazione per i modelli di dati modulo integrato che è possibile abilitare per i moduli adattivi e le comunicazioni interattive basate sul modello di dati del modulo. Il servizio precompila le origini dati per gli oggetti del modello dati nel modulo adattivo e nella comunicazione interattiva e precompila quindi i dati durante il rendering del modulo o della comunicazione.

Per abilitare il servizio di precompilazione del modello di dati modulo per un modulo adattivo, aprire le proprietà del contenitore del modulo adattivo e selezionare **[!UICONTROL servizio di precompilazione del modello di dati del modulo]** dal menu a discesa **[!UICONTROL Precompila servizio]** nel pannello di navigazione Base. Quindi, salvate le proprietà.

![servizio di precompilazione](assets/prefill-service.png)

Per configurare il servizio di precompilazione del modello di dati del modulo in una comunicazione interattiva, è possibile selezionare il servizio di precompilazione del modello di dati del modulo dal menu a discesa Servizio di precompilazione durante la creazione del servizio o in un secondo momento, modificando le proprietà.

![edit-ic-props](assets/edit-ic-props.png)

Finestra di dialogo Modifica proprietà per una comunicazione interattiva

## Scrittura dei dati del modulo adattivo inviati in origini dati {#write-af}

Quando un utente invia un modulo basato su un modello dati modulo, è possibile configurare il modulo in modo che scriva i dati inviati per un oggetto modello dati alle relative origini dati. Per ottenere questo caso d&#39;uso,  AEM Forms fornisce [Form Data Model submit action](../../forms/using/configuring-submit-actions.md), disponibile out-of-the-box solo per moduli adattivi basati su un modello dati del modulo. Scrive i dati inviati per un oggetto modello dati nella relativa origine dati.

Per configurare l&#39;azione di invio del modello dati del modulo, aprire le proprietà del contenitore del modulo adattivo e selezionare **[!UICONTROL Invia utilizzando il modello dati del modulo]** dal menu a discesa Invia azione, sotto la struttura di invio. Quindi, individuare e selezionare un oggetto modello dati dal **[!UICONTROL Nome dell&#39;oggetto modello dati da inviare]** a discesa. Salvare le proprietà.

Durante l&#39;invio del modulo, i dati per l&#39;oggetto del modello dati configurato vengono scritti nella rispettiva origine dati.

![invio dei dati](assets/data-submission.png)

È inoltre possibile inviare allegati a un&#39;origine dati utilizzando la proprietà dell&#39;oggetto modello dati binario. Per inviare allegati a un&#39;origine dati JDBC, effettuare le seguenti operazioni:

1. Aggiungere un oggetto modello dati che include una proprietà binaria al modello dati del modulo.
1. Nel modulo adattivo, trascinare il componente **[!UICONTROL File Attachment]** dal browser Componenti al modulo adattivo.
1. Toccate per selezionare il componente aggiunto e toccate ![settings_icon](assets/settings_icon.png) per aprire il browser Proprietà del componente.
1. Nel campo Riferimento binding, toccare ![cartella search_18](assets/foldersearch_18.png) e selezionare la proprietà binaria aggiunta nel modello dati del modulo. Configurare altre proprietà, a seconda delle necessità.

   Toccate ![check-button](assets/check-button.png) per salvare le proprietà. Il campo attachment è ora associato alla proprietà binaria del modello dati del modulo.

1. Nella sezione Invio delle proprietà Contenitore modulo adattivo, abilitare **[!UICONTROL Invia allegati modulo]**. Invia l&#39;allegato nel campo della proprietà binaria all&#39;origine dati all&#39;invio del modulo.

## Richiamo di servizi nei moduli adattivi utilizzando le regole {#invoke-services}

In un modulo adattivo basato su un modello dati modulo, è possibile [creare regole](../../forms/using/rule-editor.md) per richiamare servizi configurati nel modello dati del modulo. L&#39;operazione **[!UICONTROL Invoke Services]** in una regola elenca tutti i servizi disponibili nel modello dati del modulo e consente di selezionare i campi di input e output per il servizio. È inoltre possibile utilizzare il tipo di regola **Imposta valore** per richiamare un servizio modello dati modulo e impostare il valore di un campo sull&#39;output restituito dal servizio.

Ad esempio, la regola seguente richiama un servizio get che utilizza l&#39;ID dipendente come input e i valori restituiti vengono compilati nei campi ID dipendente, Cognome, Nome e Genere corrispondenti nel modulo.

![invoke-service](assets/invoke-service.png)

Inoltre, potete utilizzare l&#39;API `guidelib.dataIntegrationUtils.executeOperation` per scrivere un JavaScript nell&#39;editor di codice per l&#39;editor di regole. Per informazioni dettagliate sulle API, vedere [API per richiamare il servizio del modello dati del modulo](/help/forms/using/invoke-form-data-model-services.md).
