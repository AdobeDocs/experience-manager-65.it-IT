---
title: Abilita approfondimenti risorse tramite DTM
description: Scopri come utilizzare  Gestione dinamica dei tag (DTM, Dynamic Tag Management) di Adobe per abilitare Asset Insights.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 892237699a4027e7dab406fd620cac220aa8b88b
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 2%

---


# Abilita approfondimenti risorse tramite DTM {#enable-asset-insights-through-dtm}

 Gestione tag dinamica dei Adobi è uno strumento che attiva i tuoi strumenti di marketing digitale. È disponibile gratuitamente per  clienti Adobe Analytics.

Sebbene sia possibile personalizzare il codice di tracciamento per consentire a soluzioni CMS di terze parti di utilizzare Asset Insights,  Adobe consiglia di utilizzare DTM per inserire i tag Asset Insights.

>[!NOTE]
>
>Le informazioni approfondite sono supportate e fornite solo per le immagini.

Per abilitare Asset Insights tramite Gestione dinamica dei tag, procedi come indicato di seguito.

1. Fate clic sul logo del Experience Manager , quindi andate a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Approfondimenti]**.
1. [Configurare  distribuzione Experience Manager con Cloud Service DTM](/help/sites-administering/dtm.md)

   Il token API dovrebbe essere disponibile dopo l&#39;accesso a [https://dtm.adobe.com](https://dtm.adobe.com/) e visitare Impostazioni **** account nel profilo utente. Questo passaggio non è richiesto dal punto di vista di Asset Insights, perché l&#39;integrazione di  Siti Experienci Manager con Asset Insights è ancora in corso.

1. Accedete a [https://dtm.adobe.com](https://dtm.adobe.com/)e selezionate una società, a seconda delle necessità.
1. Creare o aprire una proprietà Web esistente

   * Selezionate la scheda Proprietà **** Web, quindi fate clic su **[!UICONTROL Aggiungi proprietà]**.

   * Aggiornate i campi come appropriato e fate clic su **[!UICONTROL Crea proprietà]**. Consulta [la documentazione](https://docs.adobe.com/content/help/it-IT/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html).

   ![Creare una proprietà Web di modifica](assets/Create-edit-web-property.png)

1. Nella scheda **[!UICONTROL Regole]** , selezionare Regole di caricamento **[!UICONTROL pagina]** dal riquadro di navigazione e fare clic su **[!UICONTROL Crea nuova regola]**.

   ![chlimage_1-58](assets/chlimage_1-194.png)

1. Espandere **[!UICONTROL JavaScript/Tag]** di terze parti. Fate clic su **[!UICONTROL Aggiungi nuovo script]** nella scheda HTML **** sequenziale per aprire la finestra di dialogo Script.

   ![chlimage_1-59](assets/chlimage_1-195.png)

1. Fate clic sul logo dell&#39;Experience Manager  e passate a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]**.
1. Fate clic su **[!UICONTROL Insights Page Tracker]**(Tracciatore pagina informazioni approfondite), copiate il codice di tracciamento e incollatelo nella finestra di dialogo Script aperta al punto 6. Salva le modifiche.

   >[!NOTE]
   >
   >* `AppMeasurement.js` viene rimosso. È previsto che sia disponibile tramite lo strumento Adobe Analytics  di Gestione dinamica dei tag.
   >* La chiamata a `assetAnalytics.dispatcher.init()` viene rimossa. La funzione verrà chiamata una volta terminato il caricamento dello strumento Adobe Analytics  DTM.
   >* A seconda di dove è ospitato Asset Insights Page Tracker (ad esempio  Experience Manager, CDN e così via), l&#39;origine della sorgente dello script potrebbe richiedere delle modifiche.
   >* Per  Page Tracker ospitato dal Experience Manager, l&#39;origine deve puntare a un&#39;istanza di pubblicazione utilizzando il nome host dell&#39;istanza dispatcher.


1. Accesso `https://dtm.adobe.com`. Fate clic su **[!UICONTROL Panoramica]** nella proprietà Web e fate clic su **[!UICONTROL Aggiungi strumento]** oppure aprite uno strumento Adobe Analytics  esistente. Durante la creazione dello strumento, è possibile impostare Metodo **[!UICONTROL di]** configurazione su **[!UICONTROL Automatico]**.

   ![Aggiungi  strumento Adobe Analytics](assets/Add-Adobe-Analytics-Tool.png)

   Selezionate le suite di rapporti Staging/Produzione, a seconda delle necessità.

1. Espandete Gestione **** libreria e accertatevi che **[!UICONTROL Carica libreria in]** sia impostato su **[!UICONTROL Page Top]**.

   ![chlimage_1-61](assets/chlimage_1-197.png)

1. Espandete **[!UICONTROL Personalizza codice]** pagina e fate clic su **[!UICONTROL Apri editor]**.

   ![chlimage_1-62](assets/chlimage_1-198.png)

1. Incollate il seguente codice nella finestra:

   ```Java
   var sObj;
   
   if (arguments.length > 0) {
     sObj = arguments[0];
   } else {
     sObj = _satellite.getToolsByType('sc')[0].getS();
   }
   _satellite.notify('in assetAnalytics customInit');
   (function initializeAssetAnalytics() {
     if ((!!window.assetAnalytics) && (!!assetAnalytics.dispatcher)) {
       _satellite.notify('assetAnalytics ready');
       /** NOTE:
           Copy over the call to 'assetAnalytics.dispatcher.init()' from Assets Pagetracker
           Be mindful about changing the AppMeasurement object as retrieved above.
       */
       assetAnalytics.dispatcher.init(
             "",  /** RSID to send tracking-call to */
             "",  /** Tracking Server to send tracking-call to */
             "",  /** Visitor Namespace to send tracking-call to */
             "",  /** listVar to put comma-separated-list of Asset IDs for Asset Impression Events in tracking-call, e.g. 'listVar1' */
             "",  /** eVar to put Asset ID for Asset Click Events in, e.g. 'eVar3' */
             "",  /** event to include in tracking-calls for Asset Impression Events, e.g. 'event8' */
             "",  /** event to include in tracking-calls for Asset Click Events, e.g. 'event7' */
             sObj  /** [OPTIONAL] if the webpage already has an AppMeasurement object, include the object here. If unspecified, Pagetracker Core shall create its own AppMeasurement object */
             );
       sObj.usePlugins = true;
       sObj.doPlugins = assetAnalytics.core.updateContextData;
       assetAnalytics.core.optimizedAssetInsights();
     }
     else {
       _satellite.notify('assetAnalytics not available. Consider updating the Custom Page Code', 4);
     }
   })();
   ```

   * La regola di caricamento delle pagine in Gestione dinamica dei tag include solo il `pagetracker.js` codice. Tutti `assetAnalytics` i campi sono considerati sostituzioni per i valori predefiniti. Non sono richiesti per impostazione predefinita.
   * Il codice richiama `assetAnalytics.dispatcher.init()` dopo aver verificato che `_satellite.getToolsByType('sc')[0].getS()` sia inizializzato e `assetAnalytics,dispatcher.init` sia disponibile. Pertanto, potete saltare l’aggiunta al punto 11.
   * Come indicato nei commenti all&#39;interno del codice Tracciatore pagina Insights (**[!UICONTROL Strumenti > Risorse > Tracciatore]** pagina Insights), quando il Tracker pagina non crea un `AppMeasurement` oggetto, i primi tre argomenti (RSID, Server di tracciamento e Spazio dei nomi dei visitatori) sono irrilevanti. Vengono invece passate stringhe vuote per evidenziare questo problema.\
      Gli argomenti rimanenti corrispondono a ciò che è configurato nella pagina Insights Configuration (**[!UICONTROL Strumenti > Risorse > Insights Configuration]**).
   * L&#39;oggetto AppMeasurement viene recuperato eseguendo query `satelliteLib` per tutti i motori di SiteCatalyst disponibili. Se sono configurati più tag, modificate l&#39;indice del selettore di array in modo appropriato. Le voci dell&#39;array sono ordinate in base agli strumenti di SiteCatalyst disponibili nell&#39;interfaccia DTM.

1. Salvare e chiudere la finestra Editor di codice, quindi salvare le modifiche nella configurazione dello strumento.
1. Nella scheda **[!UICONTROL Approvazioni]** , approvare entrambe le approvazioni in sospeso. Il tag DTM è pronto per essere inserito nella pagina Web. Per informazioni dettagliate su come inserire tag DTM nelle pagine Web, consulta [Integrare DTM nei modelli](https://blogs.adobe.com/experiencedelivers/experience-management/integrating-dtm-custom-aem6-page-template/)di pagina personalizzati.
