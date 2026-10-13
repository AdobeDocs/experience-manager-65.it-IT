---
title: Limitazioni per l’editor
description: L’editor nell’interfaccia touch utilizza le sovrapposizioni per interagire con contenuti confinati in un iframe. Questa interazione crea alcune limitazioni sia nell’utilizzo dell’editor che per gli sviluppatori.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: introduction
exl-id: fd64f5dc-dfff-466b-8cdd-3c24ea1a15c8
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 10%
---
# Limitazioni per l’editor{#editor-limitations}

L’editor nell’interfaccia touch utilizza le sovrapposizioni per interagire con contenuti confinati in un iframe. Questa interazione crea alcune limitazioni sia nell’utilizzo dell’editor che per gli sviluppatori. Questa pagina riepiloga queste limitazioni e fornisce soluzioni o soluzioni alternative, ove possibile.

## Limitazioni funzionali {#functional-limitations}

Un autore può incontrare le seguenti limitazioni funzionali quando utilizza l’editor per creare pagine.

### Collegamenti non attivi {#links-not-active}

Quando [si modifica una pagina](/help/sites-authoring/editing-content.md), i collegamenti non sono attivi.

* [Passa alla modalità **Anteprima**](/help/sites-authoring/editing-content.md#preview-mode) per spostarti utilizzando i collegamenti presenti nel contenuto.

### Strutturare le pagine {#structure-pages}

Impossibile denominare le pagine `structure`. Le pagine denominate `structure` non sono modificabili nell&#39;editor di pagine.

## Limitazioni CSS {#css-limitations}

Con le interazioni dell’editor con CSS, uno sviluppatore potrebbe incontrare le seguenti limitazioni.

### Elementi con posizione assoluta {#absolutely-positioned-elements}

Gli elementi con posizionamento assoluto possono causare problemi nella posizione della sovrapposizione.

* In questo caso, assicurati che le dimensioni dell’elemento con posizionamento assoluto siano corrette perché l’editor crea una sovrapposizione con le stesse dimensioni.

### unità vh {#vh-units}

`vh` unità non sono supportate perché l&#39;altezza iframe deve essere regolata automaticamente da Adobe Experience Manager (AEM).

### Immagini di sfondo fisse {#fixed-background-images}

È possibile che le immagini di sfondo fisse non vengano visualizzate come fisse durante lo scorrimento perché sono incorporate in un iframe.

* Selezionando **Visualizza pagina come pubblicata** nelle azioni della barra dell&#39;intestazione, la pagina viene visualizzata correttamente.

### Altezza 100% {#height}

L&#39;altezza 100% non è supportata nell&#39;elemento body di una pagina.

* È possibile trovare una soluzione alternativa per implementare un corpo a schermo intero &quot;allungando&quot; l’elemento body come segue:

```xml
body {
    position: absolute;
    top: 0;
    bottom: 0;
    right: 0;
    left: 0;
}
```

### Compressione del margine {#margin-collapsing}

I problemi di compressione del margine possono essere rilevati se il primo elemento figlio dell&#39;elemento body ha un margine.

* La soluzione consiste nell’aggiungere un clearfix a livello di elemento body, come segue:

```xml
body:before, body:after{
    content: ' ';
    display: table;
}
```
