---
title: Immagini panoramiche
description: Scopri come utilizzare le immagini panoramiche in Dynamic Medie.
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
docset: aem65
feature: Panoramic Images,Asset Management
role: User, Admin
exl-id: 4d6fbeb1-94db-4154-9e41-b76033fb4398
source-git-commit: 941e5d7574d31622f50e50e717c21cd2eba2e602
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 0%

---

# Immagini panoramiche{#panoramic-images}

Questa sezione descrive come lavorare con il visualizzatore Immagine panoramica per riprodurre immagini panoramiche sferiche per un&#39;esperienza di visualizzazione a 360 gradi immersiva di una stanza, una proprietà, una posizione o un paesaggio.

Vedi anche [Gestisci predefiniti visualizzatore](/help/assets/managing-viewer-presets.md).

![panoramic-image2](assets/panoramic-image2.png)

## Carica le risorse da utilizzare con il visualizzatore immagini panoramiche {#uploading-assets-for-use-with-the-panoramic-image-viewer}

Affinché una risorsa caricata possa essere considerata un’immagine panoramica sferica da utilizzare con il visualizzatore immagini panoramiche, è necessario che la risorsa presenti uno o entrambi i seguenti elementi:

* Proporzioni pari a 2.
È possibile ignorare l&#39;impostazione predefinita di proporzioni 2 in CRXDE Liti nelle seguenti situazioni:
  `/conf/global/settings/cloudconfigs/dmscene7/jcr:content`

* Contrassegnato con le parole chiave `equirectangular`, o `spherical`e `panorama`, o `spherical` e `panoramic`. Consulta [Utilizzo dei tag](/help/sites-authoring/tags.md).

Sia le proporzioni che i criteri delle parole chiave si applicano alle risorse panoramiche della pagina dei dettagli della risorsa e `Panoramic Media` Componente WCM.

Per caricare le risorse da utilizzare con il visualizzatore immagini panoramiche, consulta [Carica risorse](/help/assets/manage-assets.md#uploading-assets).

## Configurare Dynamic Media Classic {#configuring-dynamic-media-classic-scene}

Affinché il visualizzatore Immagine panoramica funzioni correttamente in Adobe Experience Manager, sincronizza i predefiniti del visualizzatore Immagine panoramica con i metadati specifici di Dynamic Media Classic e Dynamic Media Classic in modo che i predefiniti del visualizzatore vengano aggiornati in JCR. Per eseguire questa sincronizzazione, configura Dynamic Media Classic come segue:

1. Apri [applicazione desktop Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), quindi accedi al tuo account.

1. Nell’angolo superiore destro della pagina, seleziona **[!UICONTROL Configurazione]** > **[!UICONTROL Impostazione applicazione]** > **[!UICONTROL Impostazione pubblicazione]** > **[!UICONTROL Server immagini]**.
1. Nella pagina Pubblicazione su Image Server, da **[!UICONTROL Contesto di pubblicazione]** menu a discesa nella parte superiore, seleziona **[!UICONTROL Image Server]**.

1. Nella stessa pagina di pubblicazione del server immagini, individua l’intestazione **[!UICONTROL Attributi della richiesta]**.
1. Nell’intestazione Attributi della richiesta, individua **[!UICONTROL Limite dimensioni immagine di risposta]**. Quindi, nei campi Larghezza e Altezza associati, aumenta la dimensione immagine massima consentita per le immagini panoramiche.

   Dynamic Media Classic ha un limite di 25.000.000 di pixel. Le dimensioni massime consentite per le immagini con un rapporto di formato 2:1 sono 7000 x 3500. Tuttavia, per i tipici schermi desktop, è sufficiente la risoluzione di 4096 x 2048 pixel.

   >[!NOTE]
   >
   >Sono supportate solo le immagini che rientrano nelle dimensioni massime consentite. Le richieste di immagini che superano il limite di dimensioni generano una risposta 403.

1. Nell’intestazione Attributi della richiesta, effettua le seguenti operazioni:

   * Imposta modalità di offuscamento richiesta su **[!UICONTROL Disabilitato]**.
   * Imposta modalità di blocco richieste su **[!UICONTROL Disabilitato]**.

   Queste impostazioni sono necessarie per utilizzare `Panoramic Media` Componente WCM in Experience Manager.

1. Nella parte inferiore della pagina di pubblicazione di Image Server, sul lato sinistro, seleziona **[!UICONTROL Salva]**.

1. Nell’angolo inferiore destro, seleziona **[!UICONTROL Chiudi]**.

### Risoluzione dei problemi del componente WCM per elementi multimediali panoramici {#troubleshooting-the-panoramic-media-wcm-component}

Se hai rilasciato un’immagine nel componente Elemento multimediale panoramico in WCM e il segnaposto del componente è compresso, risolvi i problemi seguenti:

* Se si verifica un errore 403 Forbidden, la causa potrebbe essere l&#39;eccessiva dimensione dell&#39;immagine richiesta. Rivedi **[!UICONTROL Limite dimensioni immagine di risposta]** impostazioni in [Configurare Dynamic Media Classic](/help/assets/panoramic-images.md#configuring-dynamic-media-classic-scene).

* Per un &quot;Blocco non valido&quot; sulla risorsa o un &quot;Errore di analisi&quot; visualizzato sulla pagina, seleziona Request Obfuscation Mode (Modalità di offuscamento richiesta) e Request Locking Mode (Modalità di blocco richiesta) per assicurarti che siano disabilitati.
* Per un errore nell’area di lavoro contaminata, imposta un percorso file definizione set regole e annulla validità CTN per le richieste precedenti per la risorsa immagine.
* Se la qualità dell’immagine si abbassa dopo una richiesta di immagine con dimensioni superiori al limite supportato, verifica che **[!UICONTROL Attributi codifica JPEG > Qualità]** l&#39;impostazione non è vuota. Impostazione tipica per **[!UICONTROL Qualità]** il campo è `95`. L&#39;impostazione è disponibile nella pagina di pubblicazione del server immagini. Per accedere alla pagina, consulta [Configurare Dynamic Media Classic](/help/assets/panoramic-images.md#configuring-dynamic-media-classic-scene).

## Anteprima immagini panoramiche {#previewing-panoramic-images}

Consulta [Anteprima risorse](/help/assets/previewing-assets.md).

## Pubblica immagini panoramiche {#publishing-panoramic-images}

Consulta [Pubblicare le risorse](/help/assets/publishing-dynamicmedia-assets.md).
