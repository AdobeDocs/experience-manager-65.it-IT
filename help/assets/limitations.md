---
title: Limiti Dynamic Media
description: 'Scopri le best practice e i limiti applicati quando crei un set di immagini o un set 360 gradi o carichi un PDF. Scopri anche le combinazioni non supportate di browser web e sistemi operativi per visualizzatori Dynamic Media. '
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/Dynamic-Media-Classic
geptopics: SG_SCENESEVENONDEMAND_PK/categories/ecatalogs
feature: Dynamic Media Classic,Asset Management,Viewers,Image Sets,Spin Sets,eCatalog
role: User
source-git-commit: cd3dcd0232e1ecf69c79b03ab960cfbfc283ee76
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 3%

---

# Limitazioni di Dynamic Media

Le sezioni seguenti descrivono le limitazioni in Dynamic Media.

Questo argomento include le sezioni seguenti:

* Best practice e limiti applicati da Dynamic Media sui tipi di risorse

<!-- * Unsupported web browser and operating system combinations for Dynamic Media Viewers -->

## Best practice e limiti applicati da Dynamic Media sui tipi di risorse

Quando crei un set 360 gradi o un set di immagini o carichi PDF per l’estrazione della pagina, Adobe consiglia le seguenti best practice e applica i seguenti limiti:

| Risorsa - Tipo limite | Best practice | Limite implementato | Modifiche al limite del 31 dicembre 2022 |
| --- | --- | --- | --- |
| **Immagine** - Numero di ritagli avanzati per immagine | 5 | 100 |  |
| **Set di immagini** - Numero di risorse duplicate per set | Nessun duplicato | 100 | 20 |
| **Set di immagini** - Numero massimo di immagini per set | 5-10 immagini per set | 1000 |
| **Set 360 gradi** - Numero massimo di righe/colonne per set 2D | 12-18 immagini per set | 1000 |
| **PDF** - Numero massimo di pagine per un PDF da considerare per l’estrazione |  | 5000 (per nuovi caricamenti) | 100 |

<!-- See also [Dynamic Media limitations](/help/assets/limitations.md). -->

<!-- ## Unsupported web browser and operating system combinations for Dynamic Media Viewers

Dynamic Media Viewers do not support following combinations of web browser and operating system.

* Internet Explorer 11 + Windows 7
* Internet Explorer 11 + Windows 8.1
* Internet Explorer 11 + Windows Phone 8.1
* Internet Explorer 11 + Windows Phone 8.1 Update
* Safari 6 + iOS 6.0.1
* Safari 7 + iOS 7.1
* Safari 7 + macOS X 10.9 Mavericks
* Safari 8 + iOS 8.4
* Safari 8 + macOS X 10.10 Yosemite -->