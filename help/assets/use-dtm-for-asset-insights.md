---
title: Abilitare Assets Insights tramite DTM
description: Scopri come utilizzare Adobe Dynamic Tag Management (DTM) per abilitare Assets Insights.
contentOwner: AG
role: User, Admin
feature: Asset Insights,Asset Reports
exl-id: 80e8f84e-3235-4212-9dcd-6acdb9067893
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '631'
ht-degree: 2%

---

# Abilitare Assets Insights tramite DTM {#enable-asset-insights-through-dtm}

Adobe Dynamic Tag Management è uno strumento che attiva gli strumenti di marketing digitale. Viene fornito gratuitamente ai clienti Adobe Analytics. Puoi personalizzare il codice di tracciamento per abilitare le soluzioni CMS di terze parti a utilizzare Assets Insights oppure puoi utilizzare DTM per inserire i tag di Assets Insights. Gli approfondimenti sono supportati e forniti solo per le immagini.

>[!CAUTION]
>
>Adobe DTM è obsoleto a favore di [!DNL Adobe Experience Platform] e presto raggiungerà [la fine del ciclo di vita](https://medium.com/launch-by-adobe/dtm-plans-for-a-sunset-3c6aab003a6f). L&#39;Adobe consiglia di [utilizzare [!DNL Adobe Experience Platform] per approfondimenti risorse](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/advanced/asset-insights-launch-tutorial.html).

Segui questi passaggi per abilitare Assets Insights tramite DTM.

1. Fai clic sul logo dell&#39;Experience Manager e vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Assets]** > **[!UICONTROL Configurazione approfondimenti]**.
1. [Configurare l’implementazione di Experience Manager con il Cloud Service DTM](/help/sites-administering/dtm.md)

   Il token API dovrebbe essere disponibile dopo aver effettuato l&#39;accesso a [https://dtm.adobe.com](https://dtm.adobe.com/) e aver visitato **[!UICONTROL Impostazioni account]** nel profilo utente. Questo passaggio non è necessario dal punto di vista di Assets Insights, perché l’integrazione di Experience Manager Sites con Assets Insights è ancora in fase di elaborazione.

1. Accedere a [https://dtm.adobe.com](https://dtm.adobe.com/) e selezionare una società, a seconda delle necessità.
1. Creare o aprire una proprietà Web esistente

   * Selezionare la scheda **[!UICONTROL Proprietà Web]**, quindi fare clic su **[!UICONTROL Aggiungi proprietà]**.

   * Aggiornare i campi in base alle esigenze e fare clic su **[!UICONTROL Crea proprietà]**. Consulta la [documentazione](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=it).

   ![Crea modifica proprietà Web](assets/Create-edit-web-property.png)

1. Nella scheda **[!UICONTROL Regole]**, seleziona **[!UICONTROL Regole di caricamento pagina]** dal riquadro di navigazione e fai clic su **[!UICONTROL Crea nuova regola]**.

   ![chlimage_1-58](assets/chlimage_1-194.png)

1. Espandere **[!UICONTROL JavaScript /Third Party Tags]**. Quindi fai clic su **[!UICONTROL Aggiungi nuovo script]** nella scheda **[!UICONTROL HTML sequenziale]** per aprire la finestra di dialogo Script.

   ![chlimage_1-59](assets/chlimage_1-195.png)

1. Fai clic sul logo dell&#39;Experience Manager e passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Assets]**.
1. Fai clic su **[!UICONTROL Tracciamento pagina approfondimenti]**, copia il codice di tracciamento, quindi incollalo nella finestra di dialogo Script aperta al passaggio 6. Salva le modifiche.

   >[!NOTE]
   >
   >* Rimozione di `AppMeasurement.js` completata. Dovrebbe essere disponibile tramite lo strumento Adobe Analytics di DTM.
   >* Chiamata a `assetAnalytics.dispatcher.init()` rimossa. La funzione dovrebbe essere chiamata al termine del caricamento dello strumento Adobe Analytics di DTM.
   >* A seconda della posizione in cui è ospitato il tracciatore pagina di Assets Insights (ad Experience Manager, CDN e così via), l’origine dell’origine dello script potrebbe richiedere modifiche.
   >* Ad Experience Manager, il tracciatore di pagine in hosting, l’origine deve puntare a un’istanza Publish utilizzando il nome host dell’istanza di Dispatcher.

1. Accedi a `https://dtm.adobe.com`. Fai clic su **[!UICONTROL Panoramica]** nella proprietà Web, quindi fai clic su **[!UICONTROL Aggiungi strumento]** o apri uno strumento Adobe Analytics esistente. Durante la creazione dello strumento, è possibile impostare **[!UICONTROL Metodo di configurazione]** su **[!UICONTROL Automatico]**.

   ![Aggiungi strumento Adobe Analytics](assets/Add-Adobe-Analytics-Tool.png)

   Seleziona le suite di rapporti Staging/Produzione, a seconda delle necessità.

1. Espandi **[!UICONTROL Gestione libreria]** e assicurati che **[!UICONTROL Carica libreria in]** sia impostato su **[!UICONTROL Pagina superiore]**.

   ![chlimage_1-61](assets/chlimage_1-197.png)

1. Espandere **[!UICONTROL Personalizza codice pagina]** e fare clic su **[!UICONTROL Apri editor]**.

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
             "",  /** listVar to put comma-separated-list of Asset IDs for Asset Impression Events in tracking-call, for example, 'listVar1' */
             "",  /** eVar to put Asset ID for Asset Click Events in, for example, 'eVar3' */
             "",  /** event to include in tracking-calls for Asset Impression Events, for example, 'event8' */
             "",  /** event to include in tracking-calls for Asset Click Events, for example, 'event7' */
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

   * La regola di caricamento della pagina in DTM include solo il codice `pagetracker.js`. Tutti i campi `assetAnalytics` sono considerati sostituzioni dei valori predefiniti. Non sono obbligatori per impostazione predefinita.
   * Il codice chiama `assetAnalytics.dispatcher.init()` dopo aver verificato che `_satellite.getToolsByType('sc')[0].getS()` sia inizializzato e che `assetAnalytics,dispatcher.init` sia disponibile. Pertanto, non è necessario aggiungerla al passaggio 11.
   * Come indicato nei commenti all&#39;interno del codice di tracciamento pagina approfondimenti (**[!UICONTROL Strumenti > Assets > Tracciamento pagina approfondimenti]**), quando Tracciamento pagina non crea un oggetto `AppMeasurement`, i primi tre argomenti (RSID, Server di tracciamento e Spazio dei nomi visitatore) sono irrilevanti. Vengono invece passate stringhe vuote per evidenziarlo.\
     Gli argomenti rimanenti corrispondono a quanto configurato nella pagina Configurazione approfondimenti (**[!UICONTROL Strumenti > Assets > Configurazione approfondimenti]**).
   * L&#39;oggetto AppMeasurement viene recuperato eseguendo una query su `satelliteLib` per tutti i motori di SiteCatalyst disponibili. Se sono configurati più tag, modifica in modo appropriato l’indice del selettore di array. Le voci nell’array sono ordinate in base agli strumenti di SiteCatalyst disponibili nell’interfaccia di DTM.

1. Salvare e chiudere la finestra dell&#39;editor di codice, quindi salvare le modifiche nella configurazione dello strumento.
1. Nella scheda **[!UICONTROL Approvazioni]**, approva entrambe le approvazioni in sospeso. Il tag DTM è pronto per essere inserito nella pagina web.
