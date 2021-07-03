---
title: Immagini panoramiche
description: Scopri come utilizzare le immagini panoramiche in Dynamic Media.
uuid: ced3e5bd-93c8-4d5f-a397-1380d4d0a5e7
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
discoiquuid: 632a9074-b747-49a1-a57d-1f42bba1f4e9
docset: aem65
feature: Immagini panoramiche, Gestione delle risorse
role: User, Admin
exl-id: 4d6fbeb1-94db-4154-9e41-b76033fb4398
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 0%

---

# Immagini panoramiche{#panoramic-images}

Questa sezione descrive come utilizzare il visualizzatore di immagini panoramiche per riprodurre immagini panoramiche sferiche per un’esperienza di visualizzazione a 360° di una stanza, una proprietà, una posizione o un paesaggio.

Consulta anche [Gestione dei predefiniti per visualizzatori](/help/assets/managing-viewer-presets.md).

![panoramico-immagine2](assets/panoramic-image2.png)

## Caricamento delle risorse da utilizzare con il visualizzatore di immagini panoramiche {#uploading-assets-for-use-with-the-panoramic-image-viewer}

Affinché una risorsa caricata possa qualificarsi come immagine panoramica sferica che intendi utilizzare con il visualizzatore di immagini panoramiche, la risorsa deve avere uno o entrambi i seguenti elementi:

* Rapporto di formato 2.
È possibile ignorare l’impostazione predefinita per le proporzioni di 2 in CRXDE Lite nei seguenti casi:
   `/conf/global/settings/cloudconfigs/dmscene7/jcr:content`

* Tag con le parole chiave `equirectangular`, `spherical`e `panorama`, o `spherical` e `panoramic`. Consulta [Uso dei tag](/help/sites-authoring/tags.md).

Sia le proporzioni che i criteri delle parole chiave si applicano alle risorse panoramiche della pagina dei dettagli delle risorse che il componente `Panoramic Media` WCM.

Per caricare le risorse da utilizzare con il visualizzatore di immagini panoramiche, consulta [Caricamento delle risorse](/help/assets/manage-assets.md#uploading-assets).

## Configurazione di Dynamic Media Classic {#configuring-dynamic-media-classic-scene}

Affinché il visualizzatore di immagini panoramiche funzioni correttamente in Adobe Experience Manager, sincronizza i predefiniti per visualizzatori di immagini panoramiche con i metadati specifici di Dynamic Media Classic e Dynamic Media Classic in modo che i predefiniti per visualizzatori vengano aggiornati nel JCR. Per eseguire questa sincronizzazione, configura Dynamic Media Classic come segue:

1. Apri l&#39; [applicazione desktop Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), quindi accedi al tuo account.

1. Fai clic su **[!UICONTROL Configurazione]** > **[!UICONTROL Impostazione applicazione]** > **[!UICONTROL Impostazioni pubblicazione]** > **[!UICONTROL Server immagini]** nell’angolo in alto a destra della pagina.
1. Nella pagina Pubblica su Image Server, dal menu a discesa **[!UICONTROL Contesto pubblicazione]** vicino alla parte superiore, seleziona **[!UICONTROL Image Serving]**.

1. Nella stessa pagina Pubblica su Image Server, individua l’intestazione **[!UICONTROL Richiedi attributi]**.
1. Sotto l&#39;intestazione Request Attributes (Richiedi attributi), individua **[!UICONTROL Reply Image Size Limit]** (Limite dimensioni immagine di risposta). Quindi, nei campi Larghezza e Altezza associati, aumenta la dimensione massima consentita per le immagini panoramiche.

   Dynamic Media Classic ha un limite di 25.000.000 pixel. Le dimensioni massime consentite per le immagini con un rapporto di formato 2:1 sono 7000 x 3500. Tuttavia, per gli schermi desktop tipici, sono sufficienti 4096 x 2048 pixel.

   >[!NOTE]
   >
   >Sono supportate solo le immagini che rientrano nella dimensione massima consentita. Le richieste di immagini che superano il limite di dimensione danno luogo a una risposta 403.

1. Sotto l&#39;intestazione Attributi di richiesta, procedi come segue:

   * Imposta la modalità di offuscamento richieste su **[!UICONTROL Disabilitato]**.
   * Impostare la modalità di blocco delle richieste su **[!UICONTROL Disabilitato]**.

   Queste impostazioni sono necessarie per utilizzare il componente `Panoramic Media` WCM in Experience Manager.

1. Nella parte inferiore della pagina Pubblicazione su Image Server, a sinistra, fai clic su **[!UICONTROL Salva]**.

1. Nell&#39;angolo in basso a destra, fai clic su **[!UICONTROL Chiudi]**.

### Risoluzione dei problemi relativi al componente WCM per elementi multimediali panoramici {#troubleshooting-the-panoramic-media-wcm-component}

Se hai rilasciato un’immagine nel componente Elemento multimediale panoramico in WCM e il segnaposto del componente è stato compresso, risolvi i seguenti problemi:

* Se si verifica un errore 403 Vietato, potrebbe essere causato dalla dimensione dell&#39;immagine richiesta troppo grande. Rivedi le impostazioni **[!UICONTROL Limite dimensione immagine di risposta]** in [Configurazione di Dynamic Media Classic](/help/assets/panoramic-images.md#configuring-dynamic-media-classic-scene).

* Per un &quot;blocco non valido&quot; sulla risorsa o un &quot;errore di analisi&quot; visualizzato sulla pagina, controlla Modalità offuscamento richieste e Modalità blocco richieste per assicurarti che siano disattivate.
* Per un errore di area di lavoro contaminata, imposta un Percorso file definizione set regole e Annulla validità CTN per le richieste precedenti per la risorsa immagine.
* Se la qualità dell&#39;immagine diventa bassa dopo una richiesta di immagine con dimensioni superiori al limite supportato, controlla che l&#39;impostazione **[!UICONTROL Attributi di codifica JPEG > Qualità]** non sia vuota. Un&#39;impostazione tipica per il campo **[!UICONTROL Quality]** è `95`. Puoi trovare l’impostazione nella pagina Pubblica su Image Server . Per accedere alla pagina, consulta [Configurazione di Dynamic Media Classic](/help/assets/panoramic-images.md#configuring-dynamic-media-classic-scene).

## Anteprima delle immagini panoramiche {#previewing-panoramic-images}

Consulta [Anteprima delle risorse](/help/assets/previewing-assets.md).

## Pubblicazione di immagini panoramiche {#publishing-panoramic-images}

Consulta [Pubblicazione di risorse](/help/assets/publishing-dynamicmedia-assets.md).
