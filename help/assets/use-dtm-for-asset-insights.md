---
title: Abilitare Assets Insights tramite DTM
description: Scopri come utilizzare Adobe Dynamic Tag Management (DTM) per abilitare Asset Insights.
contentOwner: AG
role: User, Admin
feature: Asset Insights,Asset Reports
exl-id: 80e8f84e-3235-4212-9dcd-6acdb9067893
source-git-commit: afc72fb6b324cf2e0ad8168f783d9c1a6f96c614
workflow-type: tm+mt
source-wordcount: '647'
ht-degree: 2%

---

# Abilitare Assets Insights tramite DTM {#enable-asset-insights-through-dtm}

Adobe Dynamic Tag Management è uno strumento che attiva i tuoi strumenti di marketing digitale. È disponibile gratuitamente per i clienti Adobe Analytics. Puoi personalizzare il codice di tracciamento per abilitare soluzioni CMS di terze parti all’utilizzo di Asset Insights oppure puoi utilizzare DTM per inserire i tag Assets Insights. Gli approfondimenti sono supportati e forniti solo per le immagini.

>[!CAUTION]
>
>Adobe DTM è obsoleto a favore di [!DNL Adobe Experience Platform] e raggiungerà presto [fine vita](https://medium.com/launch-by-adobe/dtm-plans-for-a-sunset-3c6aab003a6f). L’Adobe consiglia di [use [!DNL Adobe Experience Platform] informazioni sulle risorse](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/advanced/asset-insights-launch-tutorial.html).

Esegui questi passaggi per abilitare Asset Insights tramite DTM.

1. Fai clic sul logo dell’Experience Manager e vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Configurazione approfondimenti]**.
1. [Configurare la distribuzione Experience Manager con il Cloud Service DTM](/help/sites-administering/dtm.md)

   Il token API deve essere disponibile una volta effettuato l’accesso a [https://dtm.adobe.com](https://dtm.adobe.com/) e visita **[!UICONTROL Impostazioni account]** nel profilo utente. Questo passaggio non è necessario dal punto di vista di Assets Insights, perché l’integrazione di Experience Manager Sites con Assets Insights è ancora in corso.

1. Accedi a [https://dtm.adobe.com](https://dtm.adobe.com/), quindi seleziona una società a seconda dei casi.
1. Creare o aprire una proprietà Web esistente

   * Seleziona la **[!UICONTROL Proprietà Web]** , quindi fai clic su **[!UICONTROL Aggiungi proprietà]**.

   * Aggiorna i campi appropriati e fai clic su **[!UICONTROL Crea proprietà]**. Vedi [documentazione](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=it).

   ![Creare una proprietà Web di modifica](assets/Create-edit-web-property.png)

1. In **[!UICONTROL Regole]** scheda , seleziona **[!UICONTROL Regole di caricamento pagina]** dal riquadro di navigazione e fai clic su **[!UICONTROL Crea nuova regola]**.

   ![chlimage_1-58](assets/chlimage_1-194.png)

1. Espandi **[!UICONTROL Tag JavaScript/di terze parti]**. Quindi fai clic su **[!UICONTROL Aggiungi nuovo script]** in **[!UICONTROL HTML sequenziale]** per aprire la finestra di dialogo Script.

   ![chlimage_1-59](assets/chlimage_1-195.png)

1. Fai clic sul logo dell’Experience Manager e vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]**.
1. Fai clic su **[!UICONTROL Tracciamento pagina approfondimenti]**, copia il codice tracker e incollalo nella finestra di dialogo Script aperta al punto 6. Salva le modifiche.

   >[!NOTE]
   >
   >* `AppMeasurement.js` viene rimosso. È previsto che sia disponibile tramite lo strumento Adobe Analytics di DTM.
   >* La chiamata a `assetAnalytics.dispatcher.init()` viene rimosso. La funzione deve essere chiamata una volta terminato il caricamento dello strumento Adobe Analytics di DTM.
   >* A seconda della posizione in cui è ospitato il Tracciamento pagina di Asset Insights (ad Experience Manager, CDN e così via), l’origine dell’origine dello script potrebbe richiedere modifiche.
   >* Ad Experience Manager, Page Tracker ospitato da , l&#39;origine dovrebbe puntare a un&#39;istanza di pubblicazione utilizzando il nome host dell&#39;istanza del dispatcher.


1. Accesso `https://dtm.adobe.com`. Fai clic su **[!UICONTROL Panoramica]** nella proprietà web e fai clic su **[!UICONTROL Aggiungi strumento]** oppure apri uno strumento Adobe Analytics esistente. Durante la creazione dello strumento, è possibile impostare **[!UICONTROL Metodo di configurazione]** a **[!UICONTROL Automatico]**.

   ![Aggiunta dello strumento Adobe Analytics](assets/Add-Adobe-Analytics-Tool.png)

   Seleziona le suite di rapporti Staging/Produzione , a seconda dei casi.

1. Espandi **[!UICONTROL Gestione libreria]** e assicurano che **[!UICONTROL Carica libreria in]** è impostato su **[!UICONTROL Page Top]**.

   ![chlimage_1-61](assets/chlimage_1-197.png)

1. Espandi **[!UICONTROL Personalizza codice pagina]** e fai clic su **[!UICONTROL Open Editor]**.

   ![chlimage_1-62](assets/chlimage_1-198.png)

1. Incolla il seguente codice nella finestra:

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

   * La regola di caricamento della pagina in DTM include solo `pagetracker.js` codice. Qualsiasi `assetAnalytics` i campi sono considerati sostituzioni per i valori predefiniti. Non sono richieste per impostazione predefinita.
   * Le chiamate al codice `assetAnalytics.dispatcher.init()` dopo aver verificato che `_satellite.getToolsByType('sc')[0].getS()` è inizializzato e `assetAnalytics,dispatcher.init` è disponibile. Pertanto, puoi saltare l’aggiunta al passaggio 11.
   * Come indicato nei commenti all&#39;interno del codice di tracciamento pagina approfondimenti (**[!UICONTROL Strumenti > Risorse > Tracciamento pagina approfondimenti]**), quando il Tracker pagina non crea un `AppMeasurement` i primi tre argomenti (RSID, Tracking Server e Visitor Namespace) sono irrilevanti. Vengono invece passate stringhe vuote per evidenziarle.\
      Gli argomenti rimanenti corrispondono a ciò che è configurato nella pagina Configurazione approfondimenti (**[!UICONTROL Strumenti > Risorse > Configurazione approfondimenti]**).
   * L&#39;oggetto AppMeasurement viene recuperato eseguendo una query `satelliteLib` per tutti i motori di SiteCatalyst disponibili. Se sono configurati più tag, modificare opportunamente l’indice del selettore dell’array. Le voci dell&#39;array sono ordinate in base agli strumenti di SiteCatalyst disponibili nell&#39;interfaccia DTM.

1. Salvare e chiudere la finestra Editor di codice, quindi salvare le modifiche nella configurazione dello strumento.
1. In **[!UICONTROL Approvazioni]** approvare entrambe le approvazioni in sospeso. Il tag DTM è pronto per essere inserito nella pagina web.
