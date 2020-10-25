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
source-git-commit: cec6c4f9a1a75eb049dd4b8461c36c8d58d46f79
workflow-type: tm+mt
source-wordcount: '586'
ht-degree: 0%

---


# Panoramic images{#panoramic-images}

Questa sezione descrive come utilizzare il visualizzatore immagini panoramiche per riprodurre immagini panoramiche sferiche per un’esperienza di visualizzazione a 360° di una stanza, una proprietà, una posizione o un paesaggio.

See also [Managing Viewer Presets](/help/assets/managing-viewer-presets.md).

![panoramic-image2](assets/panoramic-image2.png)

## Caricamento delle risorse da usare con il visualizzatore immagini panoramiche {#uploading-assets-for-use-with-the-panoramic-image-viewer}

Affinché una risorsa caricata possa essere considerata un’immagine panoramica sferica che intendete usare con il visualizzatore immagini panoramiche, la risorsa deve contenere una o entrambe le opzioni seguenti:

* Proporzioni di 2.
Potete ignorare l’impostazione predefinita delle proporzioni pari a 2 in CRXDE Lite:
   `/conf/global/settings/cloudconfigs/dmscene7/jcr:content`

* Sono stati assegnati tag con le parole chiave `equirectangular`, oppure `spherical`e `panorama`, `spherical` e `panoramic`. Consultate [Utilizzo dei tag](/help/sites-authoring/tags.md).

Both the aspect ratio and keyword criteria apply to panoramic assets for the asset details page and the `Panoramic Media` WCM component.

Per caricare le risorse da usare con il visualizzatore immagini panoramiche, consultate [Caricamento delle risorse](/help/assets/manage-assets.md#uploading-assets).

## Configurazione di Dynamic Media Classic (Scene7) {#configuring-dynamic-media-classic-scene}

Affinché il visualizzatore di immagini panoramiche funzioni correttamente all’interno AEM, è necessario sincronizzare i predefiniti per visualizzatori di immagini panoramiche con i metadati specifici di Dynamic Media Classic (Scene7) e Dynamic Media Classic (Scene7), in modo che i predefiniti per visualizzatori vengano aggiornati nel JCR. A questo scopo, configura Dynamic Media Classic (Scene7) nel modo seguente:

1. [Accedete all’istanza di Dynamic Media Classic (Scene7)](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html) per ciascun account aziendale.

1. Nell’angolo in alto a destra della pagina, fate clic su **[!UICONTROL Configurazione > Impostazione applicazione > Impostazione pubblicazione > Server immagini.]**
1. Nella pagina Pubblica su Image Server, selezionate Server **[!UICONTROL immagini dal menu a discesa Contesto]** di **[!UICONTROL pubblicazione accanto alla parte superiore.]**

1. Nella stessa pagina Pubblica su Image Server, individuate l’intestazione Attributi **[!UICONTROL richiesta.]**
1. Sotto l’intestazione Attributi richiesta, individuate Limite dimensione immagine risposta. **** Quindi, nei campi Larghezza e Altezza associati, aumentate la dimensione massima consentita per le immagini panoramiche.

   Dynamic Media Classic (Scene7) ha un limite di 25.000.000 pixel. La dimensione massima consentita per le immagini con proporzioni 2:1 è 7000 x 3500. Tuttavia, per gli schermi desktop tipici, sono sufficienti 4096 x 2048 pixel.

   >[!NOTE]
   >
   >Sono supportate solo le immagini che rientrano nella dimensione massima consentita per le immagini. Le richieste di immagini che superano il limite di dimensione genereranno una risposta di 403.

1. Nell’intestazione Attributi richiesta, effettuate le seguenti operazioni:

   * Impostate la modalità di offuscamento richieste su **[!UICONTROL Disattivato.]**
   * Impostate la modalità di blocco della richiesta su **[!UICONTROL Disabilitata.]**

   Queste impostazioni sono necessarie per utilizzare il componente `Panoramic Media` WCM in AEM.

1. Nella parte inferiore della pagina Pubblica su Image Server, fate clic su **[!UICONTROL Salva a sinistra.]**

1. Nell’angolo inferiore destro, fate clic su **[!UICONTROL Chiudi.]**

### Risoluzione dei problemi relativi al componente WCM per file multimediali panoramici {#troubleshooting-the-panoramic-media-wcm-component}

Se un’immagine viene rilasciata nel componente Contenuti multimediali panoramici in WCM e il segnaposto del componente viene compresso, potrebbe essere utile risolvere i seguenti problemi:

* Se si verifica un errore 403 Vietato, la dimensione dell&#39;immagine richiesta potrebbe essere eccessiva. Consultate le impostazioni Limite **[!UICONTROL dimensioni immagine risposta in]** Configurazione di Dynamic Media Classic (Scene7) [](/help/assets/panoramic-images.md#configuring-dynamic-media-classic-scene).

* Per un &quot;blocco non valido&quot; sulla risorsa o un &quot;errore di analisi&quot; visualizzato sulla pagina, controllate Modalità offuscamento richieste e Modalità blocco richieste per verificare che siano disattivate.
* Per un errore di tela colorata, imposta un percorso per il file di definizione del set di regole e Annulla validità CTN per le richieste precedenti per la risorsa immagine.
* Se dopo una richiesta di immagini con dimensioni superiori al limite supportato, la qualità dell’immagine diventa molto bassa, verificate che l’impostazione **[!UICONTROL JPEG Encoding Attributes (Attributi di codifica JPEG) > Quality (Qualità]** ) non sia vuota. Un&#39;impostazione tipica per il campo **[!UICONTROL Qualità]** è `95`. L’impostazione è disponibile nella pagina Pubblica su Image Server. Per accedere alla pagina, consultate [Configurazione di Dynamic Media Classic (Scene7)](/help/assets/panoramic-images.md#configuring-dynamic-media-classic-scene).

## Anteprima delle immagini panoramiche {#previewing-panoramic-images}

Consultate [Anteprima delle risorse](/help/assets/previewing-assets.md).

## Pubblicazione di immagini panoramiche {#publishing-panoramic-images}

Consultate [Pubblicazione delle risorse](/help/assets/publishing-dynamicmedia-assets.md).
