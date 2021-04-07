---
title: Utilizzo di Dynamic Media
description: Scopri come utilizzare Dynamic Media per distribuire risorse da utilizzare sui siti web, mobili e social.
uuid: 4dc0f436-d20e-4e8b-aeff-5515380fa44d
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: introduction
content-type: reference
discoiquuid: a8063d43-923a-42ac-9a16-0c7fadd8f73f
role: Business Practitioner, Administrator
exl-id: f8a80b22-b1a6-475f-b3f1-b2f47822f21d
feature: Collaborazione, Gestione risorse
translation-type: tm+mt
source-git-commit: c9aec973faf4caef741961d92a6f258646aeddb7
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 22%

---

# Utilizzo di Dynamic Media {#working-with-dynamic-media}

[Dynamic Media](https://www.adobe.com/solutions/web-experience-management/dynamic-media.html) permette di fornire on-demand risorse visive di marketing e merchandising, ridimensionandole automaticamente per siti web, dispositivi mobili e piattaforme social. Utilizzando un set di risorse primarie, Dynamic Media genera e distribuisce più varianti di contenuti avanzati in tempo reale attraverso la sua rete globale, scalabile e ottimizzata per le prestazioni.

Dynamic Media fornisce esperienze di visualizzazione interattive, con funzioni quali zoom, rotazione a 360° e video. Dynamic Media include i flussi di lavoro della soluzione Adobe Experience Manager per la gestione delle risorse digitali (Assets) per semplificare e ottimizzare il processo di gestione delle campagne digitali.

>[!NOTE]
>
>È disponibile un articolo della community su [Utilizzo di Adobe Experience Manager e Dynamic Media](https://helpx.adobe.com/experience-manager/using/aem_dynamic_media.html).

## Operazioni possibili con Dynamic Media {#what-you-can-do-with-dynamic-media}

Dynamic Media consente di gestire le risorse prima di pubblicarle. Come lavorare con le risorse in generale viene descritto in dettaglio in [Utilizzo di risorse digitali](manage-assets.md). Gli argomenti generali includono il caricamento, il download, la modifica e la pubblicazione delle risorse; visualizzazione e modifica delle proprietà e ricerca delle risorse.

Le funzioni solo per Dynamic Media includono quanto segue:

* [Banner a carosello](carousel-banners.md)
* [Set di immagini](image-sets.md)
* [Immagini interattive](interactive-images.md)
* [Video interattivi](interactive-videos.md)
* [Set di file multimediali diversi](mixed-media-sets.md)
* [Immagini panoramiche](panoramic-images.md)

* [Set 360 gradi](spin-sets.md)
* [Video](video.md)
* [Distribuzione di risorse Dynamic Media](delivering-dynamic-media-assets.md)
* [Gestione delle risorse](managing-assets.md)
* [Utilizzo delle visualizzazioni rapide per creare finestre a comparsa personalizzate](custom-pop-ups.md)

Vedere anche [Configurazione di Dynamic Media](administering-dynamic-media.md).

>[!NOTE]
>
>Per comprendere le differenze tra l&#39;utilizzo di Dynamic Media e l&#39;integrazione di Dynamic Media Classic con AEM, vedere [Integrazione di Dynamic Media Classic con Dynamic Media](/help/sites-administering/scene7.md#aem-scene-integration-versus-dynamic-media).

## Dynamic Media abilitato e Dynamic Media disabilitato {#dynamic-media-on-versus-dynamic-media-off}

È possibile verificare se Dynamic Media è abilitato (attivato) in base alle seguenti caratteristiche:

* Le rappresentazioni dinamiche sono disponibili quando si scaricano o visualizzano in anteprima le risorse.
* Sono disponibili set di immagini, set 360 gradi e set di file multimediali diversi.
* Vengono create rappresentazioni PTIFF.

Quando fai clic su una risorsa immagine, la visualizzazione della risorsa è diversa con Dynamic Media [abilitato](config-dynamic.md#enabling-dynamic-media). Dynamic Media utilizza i visualizzatori HTML5 on-demand.

### Rendering dinamici {#dynamic-renditions}

Le rappresentazioni dinamiche come i predefiniti per immagini e visualizzatori (in **[!UICONTROL Dynamic]**) sono disponibili quando Dynamic Media è abilitato.

![chlimage_1-358](assets/chlimage_1-358.png)

### Set di immagini, set 360 gradi, set di file multimediali diversi {#image-sets-spins-sets-mixed-media-sets}

Se Dynamic Media è abilitato, sono disponibili set di immagini, set 360 gradi e set di file multimediali diversi.

![chlimage_1-359](assets/chlimage_1-359.png)

### Rendering PTIFF {#ptiff-renditions}

Le risorse abilitate per gli elementi multimediali dinamici includono `pyramid.tiffs`.

![chlimage_1-360](assets/chlimage_1-360.png)

### Modifica delle visualizzazioni delle risorse {#asset-views-change}

Con Dynamic Media abilitato, è possibile ingrandire e ridurre facendo clic sui pulsanti `+` e `-`. Puoi anche fare clic o toccare per ingrandire una determinata area. Ripristina la versione originale consente di visualizzare l’immagine a schermo intero facendo clic sulle frecce diagonali. Dynamic Media abilitato si presenta così:

![chlimage_1-361](assets/chlimage_1-361.png)

Con Dynamic Media disattivato è possibile ingrandire e ridurre e ripristinare le dimensioni originali:

![chlimage_1-362](assets/chlimage_1-362.png)
