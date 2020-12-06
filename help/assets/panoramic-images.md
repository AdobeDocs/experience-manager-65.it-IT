---
title: Immagini panoramiche
description: Scopri come lavorare con immagini panoramiche in Dynamic Media.
uuid: ced3e5bd-93c8-4d5f-a397-1380d4d0a5e7
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
discoiquuid: 632a9074-b747-49a1-a57d-1f42bba1f4e9
docset: aem65
translation-type: tm+mt
source-git-commit: 10dae6e9f49e93d2f4923cee754c1d23d9d4b25e
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 0%

---


# Immagini panoramiche{#panoramic-images}

Questa sezione descrive come utilizzare il visualizzatore immagini panoramiche per riprodurre immagini panoramiche sferiche per un’esperienza di visualizzazione a 360° di una stanza, una proprietà, una posizione o un paesaggio.

Consultate anche [Gestione dei predefiniti per visualizzatori](/help/assets/managing-viewer-presets.md).

![panoramico-immagine2](assets/panoramic-image2.png)

## Caricamento delle risorse da usare con il visualizzatore immagini panoramiche {#uploading-assets-for-use-with-the-panoramic-image-viewer}

Affinché una risorsa caricata possa essere considerata un’immagine panoramica sferica che intendete usare con il visualizzatore immagini panoramiche, la risorsa deve contenere una o entrambe le opzioni seguenti:

* Proporzioni di 2.
Potete ignorare l’impostazione predefinita delle proporzioni pari a 2 in CRXDE Lite:
   `/conf/global/settings/cloudconfigs/dmscene7/jcr:content`

* Tag con le parole chiave `equirectangular`, `spherical`e `panorama`, oppure `spherical` e `panoramic`. Vedere [Utilizzo dei tag](/help/sites-authoring/tags.md).

Sia le proporzioni che i criteri delle parole chiave si applicano alle risorse panoramiche per la pagina dei dettagli delle risorse che per il componente `Panoramic Media` WCM.

Per caricare le risorse da usare con il visualizzatore immagini panoramiche, consultate [Caricamento di risorse](/help/assets/manage-assets.md#uploading-assets).

## Configurazione di Dynamic Media Classic {#configuring-dynamic-media-classic-scene}

Affinché il visualizzatore di immagini panoramiche funzioni correttamente all’interno AEM, è necessario sincronizzare i predefiniti per visualizzatori di immagini panoramiche con i metadati specifici di Dynamic Media Classic e Dynamic Media Classic, in modo che i predefiniti per visualizzatori vengano aggiornati nel JCR. A questo scopo, configura Dynamic Media Classic nel modo seguente:

1. [Accedi alla tua istanza di Dynamic Media ](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html) Classicfor per ogni account aziendale.

1. Nell’angolo superiore destro della pagina, fate clic su **[!UICONTROL Configurazione > Impostazione applicazione > Impostazione pubblicazione > Server immagini.]**
1. Nella pagina Pubblica su Image Server, nel menu a discesa **[!UICONTROL Contesto pubblicazione]** accanto alla parte superiore, selezionate **[!UICONTROL Server immagini.]**

1. Nella stessa pagina Pubblica su Image Server, individuate l&#39;intestazione **[!UICONTROL Richiedi attributi.]**
1. Sotto l&#39;intestazione Attributi richiesta, individuare **[!UICONTROL Limite dimensioni immagine risposta.]** Quindi, nei campi Larghezza e Altezza associati, aumentate la dimensione massima consentita per le immagini panoramiche.

   Dynamic Media Classic ha un limite di 25.000.000 pixel. La dimensione massima consentita per le immagini con proporzioni 2:1 è 7000 x 3500. Tuttavia, per gli schermi desktop tipici, sono sufficienti 4096 x 2048 pixel.

   >[!NOTE]
   >
   >Sono supportate solo le immagini che rientrano nella dimensione massima consentita per le immagini. Le richieste di immagini che superano il limite di dimensione genereranno una risposta di 403.

1. Nell’intestazione Attributi richiesta, effettuate le seguenti operazioni:

   * Imposta la modalità di offuscamento richieste su **[!UICONTROL Disattivato.]**
   * Impostare la modalità di blocco richiesta su **[!UICONTROL Disattivato.]**

   Queste impostazioni sono necessarie per utilizzare il componente `Panoramic Media` WCM in AEM.

1. Nella parte inferiore della pagina Pubblica su Image Server, a sinistra, fate clic su **[!UICONTROL Salva.]**

1. Nell&#39;angolo inferiore destro, fare clic su **[!UICONTROL Chiudi.]**

### Risoluzione dei problemi relativi al componente WCM per supporti panoramici {#troubleshooting-the-panoramic-media-wcm-component}

Se un’immagine viene rilasciata nel componente Contenuti multimediali panoramici in WCM e il segnaposto del componente viene compresso, potrebbe essere utile risolvere i seguenti problemi:

* Se si verifica un errore 403 Vietato, la dimensione dell&#39;immagine richiesta potrebbe essere eccessiva. Rivedete le impostazioni **[!UICONTROL Reply Image Size Limit]** (Limite dimensioni immagine risposta&lt;a1/>) in [Configuring Dynamic Media Classic](/help/assets/panoramic-images.md#configuring-dynamic-media-classic-scene) (Configurazione di Dynamic Media Classic&lt;a3/>).

* Per un &quot;blocco non valido&quot; sulla risorsa o un &quot;errore di analisi&quot; visualizzato sulla pagina, controllate Modalità offuscamento richieste e Modalità blocco richieste per verificare che siano disattivate.
* Per un errore di tela colorata, imposta un percorso per il file di definizione del set di regole e Annulla validità CTN per le richieste precedenti per la risorsa immagine.
* Se dopo una richiesta di immagini con dimensioni superiori al limite supportato la qualità delle immagini risulta molto bassa, verificate che l&#39;impostazione **[!UICONTROL JPEG Encoding Attributes > Quality]** non sia vuota. Un&#39;impostazione tipica per il campo **[!UICONTROL Quality]** è `95`. L’impostazione è disponibile nella pagina Pubblica su Image Server. Per accedere alla pagina, vedere [Configurazione di Dynamic Media Classic](/help/assets/panoramic-images.md#configuring-dynamic-media-classic-scene).

## Anteprima delle immagini panoramiche {#previewing-panoramic-images}

Consultate [Anteprima delle risorse](/help/assets/previewing-assets.md).

## Pubblicazione di immagini panoramiche {#publishing-panoramic-images}

Consultate [Pubblicazione di risorse](/help/assets/publishing-dynamicmedia-assets.md).
