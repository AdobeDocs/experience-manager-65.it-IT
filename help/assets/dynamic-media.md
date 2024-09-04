---
title: Utilizzo di Dynamic Media
description: Scopri come utilizzare il software per distribuire risorse per siti web, mobili e social network.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: introduction
content-type: reference
role: User, Admin
exl-id: f8a80b22-b1a6-475f-b3f1-b2f47822f21d
feature: Collaboration,Asset Management
solution: Experience Manager, Experience Manager Assets
source-git-commit: d6b9dde5201198cb073293b2b8527a458836ff0b
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 10%

---

# Utilizzo di Dynamic Media {#working-with-dynamic-media}

[Dynamic Medie](https://business.adobe.com/products/experience-manager/assets/dynamic-media.html) consente di fornire risorse di marketing e merchandising visive avanzate su richiesta, scalabili automaticamente per l&#39;utilizzo su siti Web, mobili e social network. Grazie a un insieme di risorse di origine primaria, il software genera e distribuisce in tempo reale più varianti di rich content attraverso una rete globale, scalabile e ottimizzata per le prestazioni.

Il software fornisce esperienze di visualizzazione interattive, tra cui zoom, 360 gradi rotazione e video. Integra in modo univoco i flussi di lavoro della soluzione Adobe Experience Manager di gestione delle risorse digitali (Assets) per semplificare e semplificare il processo di gestione delle campagne digitali.

<!-- >ARTICLE IS MISSING. GIVES 404 [!NOTE]
>
>A Community article is available on [Working with Adobe Experience Manager and Dynamic Media](https://helpx.adobe.com/experience-manager/using/aem_dynamic_media.html). -->

## Operazioni possibili con il software {#what-you-can-do-with-dynamic-media}

Il software consente di gestire le risorse prima di pubblicarle. Le modalità di utilizzo delle risorse in generale sono descritte in dettaglio in [Operazioni con le risorse digitali](manage-assets.md). Gli argomenti generali includono il caricamento, il download, la modifica e la pubblicazione delle risorse, la visualizzazione e la modifica delle proprietà e la ricerca delle risorse.

Le funzioni disponibili solo in Dynamic Medie includono:

* [Banner a carosello](carousel-banners.md)
* [Set di immagini](image-sets.md)
* [Immagini interattive](interactive-images.md)
* [Video interattivi](interactive-videos.md)
* [Set di file multimediali diversi](mixed-media-sets.md)
* [Immagini panoramiche](panoramic-images.md)

* [Set 360 gradi](spin-sets.md)
* [Video](video.md)
* [Distribuire elementi multimediali dinamici](delivering-dynamic-media-assets.md)
* [Gestire le risorse](managing-assets.md)
* [Creare pop-up personalizzati utilizzando Quickview](custom-pop-ups.md)

Vedere anche [Configurazione di Dynamic Medie](administering-dynamic-media.md).

>[!NOTE]
>
>Per comprendere le differenze tra l&#39;utilizzo di Dynamic Medie e l&#39;integrazione di Dynamic Media Classic con Adobe Experience Manager, vedere [Integrazione di Dynamic Media Classic rispetto a Dynamic Medie](/help/sites-administering/scene7.md#aem-scene-integration-versus-dynamic-media).

## Dynamic Medie abilitato e Dynamic Medie disabilitato {#dynamic-media-on-versus-dynamic-media-off}

È possibile stabilire se il software è abilitato (acceso) in base alle seguenti caratteristiche:

* Le rappresentazioni dinamiche sono disponibili quando si scaricano o si visualizzano in anteprima le risorse.
* Sono disponibili set di immagini, set 360 gradi, set di file multimediali diversi.
* Vengono creati rendering PTIFF.

Quando selezioni una risorsa immagine, la visualizzazione della risorsa è diversa se il software [è abilitato](config-dynamic.md#enabling-dynamic-media). Utilizza i visualizzatori HTML5 on-demand.

### Rappresentazioni dinamiche {#dynamic-renditions}

Le rappresentazioni dinamiche, come i predefiniti immagine e visualizzatore (in **[!UICONTROL Dinamico]**), sono disponibili quando il software è abilitato.

![chlimage_1-358](assets/chlimage_1-358.png)

### Set di immagini, set 360 gradi, set di file multimediali diversi {#image-sets-spins-sets-mixed-media-sets}

Se il software è abilitato, sono disponibili set di immagini, set 360 gradi e set di file multimediali diversi.

![chlimage_1-359](assets/chlimage_1-359.png)

### Rappresentazioni PTIFF {#ptiff-renditions}

Le risorse abilitate per Dynamic Medie includono `pyramid.tiffs`.

![chlimage_1-360](assets/chlimage_1-360.png)

### Modifica visualizzazioni risorse {#asset-views-change}

Se il software è abilitato, è possibile ingrandire e ridurre facendo clic sui pulsanti `+` e `-`. Puoi anche fare clic su per eseguire lo zoom in un’area specifica. Ripristina consente di tornare alla versione originale e di visualizzare l&#39;immagine a schermo intero facendo clic sulle frecce diagonali. Con il software abilitato, si presenta così:

![chlimage_1-361](assets/chlimage_1-361.png)

Con il software disattivato, è possibile ingrandire e ridurre e ripristinare le dimensioni originali:

![chlimage_1-362](assets/chlimage_1-362.png)
