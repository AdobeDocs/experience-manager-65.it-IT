---
title: Limitazioni per l’editor
seo-title: Editor Limitations
description: L’editor nell’interfaccia touch utilizza le sovrapposizioni per interagire con contenuti confinati in un iframe. Questa interazione crea alcune limitazioni sia nell’utilizzo dell’editor che per gli sviluppatori.
seo-description: The editor in the touch-enabled UI makes use of overlays to interact with content confined in an iframe. This interaction creates some limitations in both usage of the editor and also for developers.
uuid: ff524530-3f3a-4c5b-9f94-4aa9aeb9d461
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: introduction
discoiquuid: d748decb-a614-4c9e-a502-d6176b720f1a
exl-id: fd64f5dc-dfff-466b-8cdd-3c24ea1a15c8
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 10%

---

# Limitazioni per l’editor{#editor-limitations}

L’editor nell’interfaccia touch utilizza le sovrapposizioni per interagire con contenuti confinati in un iframe. Questa interazione crea alcune limitazioni sia nell’utilizzo dell’editor che per gli sviluppatori. Questa pagina riepiloga queste limitazioni e fornisce soluzioni o soluzioni alternative, ove possibile.

## Limitazioni funzionali {#functional-limitations}

Un autore può incontrare le seguenti limitazioni funzionali quando utilizza l’editor per creare pagine.

### Collegamenti non attivi {#links-not-active}

Quando [modifica di una pagina](/help/sites-authoring/editing-content.md), i collegamenti non sono attivi.

* [Passa a **Anteprima** modalità](/help/sites-authoring/editing-content.md#preview-mode) per navigare utilizzando i collegamenti presenti nel contenuto.

### Strutturare le pagine {#structure-pages}

Impossibile denominare le pagine `structure`. Pagine denominate `structure` non sarà modificabile nell’editor pagina.

## Limitazioni CSS {#css-limitations}

Con le interazioni dell’editor con CSS, uno sviluppatore potrebbe incontrare le seguenti limitazioni.

### Elementi con posizione assoluta {#absolutely-positioned-elements}

Gli elementi con posizionamento assoluto possono causare problemi nella posizione della sovrapposizione.

* In questo caso, assicurati che le dimensioni dell’elemento con posizionamento assoluto siano corrette, perché l’editor creerà una sovrapposizione con le stesse dimensioni.

### unità vh {#vh-units}

`vh` non sono supportate perché l’altezza dell’iframe deve essere regolata automaticamente dall’AEM.

### Immagini di sfondo fisse {#fixed-background-images}

È possibile che le immagini di sfondo fisse non vengano visualizzate come fisse durante lo scorrimento poiché sono incorporate in un iframe.

* Selezione **Visualizza pagina come pubblicata** nelle azioni della barra dell’intestazione, la pagina viene visualizzata correttamente.

### Altezza 100% {#height}

L&#39;altezza 100% non è supportata nell&#39;elemento body di una pagina.

* È possibile trovare una soluzione alternativa per implementare un corpo a schermo intero &quot;stirando&quot; l’elemento body come segue:

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
