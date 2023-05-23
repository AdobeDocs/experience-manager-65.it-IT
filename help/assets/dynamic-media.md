---
title: Utilizzo di Dynamic Media
description: Scopri come utilizzare Dynamic Media per distribuire risorse da utilizzare su siti web, mobili e social network.
uuid: 4dc0f436-d20e-4e8b-aeff-5515380fa44d
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: introduction
content-type: reference
discoiquuid: a8063d43-923a-42ac-9a16-0c7fadd8f73f
role: User, Admin
exl-id: f8a80b22-b1a6-475f-b3f1-b2f47822f21d
feature: Collaboration,Asset Management
source-git-commit: f4b7566abfa0a8dbb490baa0e849de6c355a3f06
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 9%

---

# Utilizzo di Dynamic Media {#working-with-dynamic-media}

[Dynamic Media](https://business.adobe.com/products/experience-manager/assets/dynamic-media.html) consente di fornire risorse di marketing e merchandising visive avanzate on-demand, scalabili automaticamente per il consumo su siti web, mobili e social network. Utilizzando un set di risorse di origine principale, Dynamic Media genera e distribuisce in tempo reale più varianti di rich content attraverso la sua rete globale, scalabile e ottimizzata per le prestazioni.

Dynamic Media offre esperienze di visualizzazione interattiva, tra cui zoom, 360 gradi in rotazione e video. Dynamic Media incorpora in modo esclusivo i flussi di lavoro della soluzione Adobe Experience Manager di gestione delle risorse digitali (Assets) per semplificare e semplificare il processo di gestione delle campagne digitali.

<!-- >ARTICLE IS MISSING. GIVES 404 [!NOTE]
>
>A Community article is available on [Working with Adobe Experience Manager and Dynamic Media](https://helpx.adobe.com/experience-manager/using/aem_dynamic_media.html). -->

## Operazioni possibili con Dynamic Media {#what-you-can-do-with-dynamic-media}

Dynamic Media consente di gestire le risorse prima di pubblicarle. Le modalità di utilizzo delle risorse in generale sono descritte in dettaglio in [Utilizzare le risorse digitali](manage-assets.md). Gli argomenti generali includono il caricamento, il download, la modifica e la pubblicazione delle risorse, la visualizzazione e la modifica delle proprietà e la ricerca delle risorse.

Le funzioni disponibili solo in Dynamic Media includono:

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

Vedi anche [Configurare Dynamic Media](administering-dynamic-media.md).

>[!NOTE]
>
>Per comprendere le differenze tra l’utilizzo di Dynamic Media e l’integrazione di Dynamic Media Classic con Adobe Experience Manager, consulta [Integrazione di Dynamic Media Classic e Dynamic Media](/help/sites-administering/scene7.md#aem-scene-integration-versus-dynamic-media).

## Dynamic Media abilitato e Dynamic Media disabilitato {#dynamic-media-on-versus-dynamic-media-off}

È possibile verificare se Dynamic Media è abilitato (attivato) in base alle seguenti caratteristiche:

* Le rappresentazioni dinamiche sono disponibili quando si scaricano o si visualizzano in anteprima le risorse.
* Sono disponibili set di immagini, set 360 gradi, set di file multimediali diversi.
* Vengono creati rendering PTIFF.

Quando selezioni una risorsa di immagine, la sua visualizzazione con Dynamic Media è diversa [abilitato](config-dynamic.md#enabling-dynamic-media). Dynamic Media utilizza i visualizzatori HTML5 on-demand.

### Rappresentazioni dinamiche {#dynamic-renditions}

Rappresentazioni dinamiche, come immagini e predefiniti visualizzatore (sotto **[!UICONTROL Dinamico]**) sono disponibili quando Dynamic Media è abilitato.

![chlimage_1-358](assets/chlimage_1-358.png)

### Set di immagini, set 360 gradi, set di file multimediali diversi {#image-sets-spins-sets-mixed-media-sets}

Se Dynamic Media è abilitato, sono disponibili set di immagini, set 360 gradi e set di file multimediali diversi.

![chlimage_1-359](assets/chlimage_1-359.png)

### Rappresentazioni PTIFF {#ptiff-renditions}

Le risorse abilitate per Dynamic Media includono `pyramid.tiffs`.

![chlimage_1-360](assets/chlimage_1-360.png)

### Modifica visualizzazioni risorse {#asset-views-change}

Con Dynamic Media abilitato, puoi ingrandire e ridurre facendo clic sul pulsante `+` e `-` pulsanti. Puoi anche fare clic o toccare per ingrandire un’area specifica. Ripristina consente di tornare alla versione originale e di visualizzare l&#39;immagine a schermo intero facendo clic sulle frecce diagonali. Dynamic Media abilitato si presenta così:

![chlimage_1-361](assets/chlimage_1-361.png)

Con Dynamic Media disabilitato puoi ingrandire e ridurre e ripristinare le dimensioni originali:

![chlimage_1-362](assets/chlimage_1-362.png)
