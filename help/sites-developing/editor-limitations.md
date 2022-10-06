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

Un autore può incontrare le seguenti limitazioni funzionali quando utilizza l’editor per creare le pagine.

### Collegamenti non attivi {#links-not-active}

Quando [modifica di una pagina](/help/sites-authoring/editing-content.md), i collegamenti non sono attivi.

* [Passa a **Anteprima** modalità](/help/sites-authoring/editing-content.md#preview-mode) per spostarsi utilizzando i collegamenti presenti nel contenuto.

### Pagine struttura {#structure-pages}

Le pagine non possono essere denominate `structure`. Pagine denominate `structure` non sarà modificabile nell’editor pagina.

## Limitazioni CSS {#css-limitations}

Uno sviluppatore può incontrare le seguenti limitazioni con le interazioni dell’editor con i CSS.

### Elementi posizionati in modo assoluto {#absolutely-positioned-elements}

Gli elementi posizionati in modo assoluto possono causare problemi nella posizione della sovrapposizione.

* In questo caso, accertati che le dimensioni dell’elemento con posizione assoluta siano corrette perché l’editor creerà una sovrapposizione con le stesse dimensioni.

### unità vh {#vh-units}

`vh` le unità non sono supportate perché l&#39;altezza dell&#39;iframe deve essere regolata automaticamente da AEM.

### Immagini di sfondo fisse {#fixed-background-images}

Le immagini di sfondo fisse potrebbero non essere visualizzate come fisse durante lo scorrimento a causa del fatto che sono incorporate in un iframe.

* Selezione **Visualizza pagina come pubblicata** nella barra dell’intestazione le azioni visualizzano la pagina correttamente.

### Altezza 100% {#height}

L’altezza del 100% non è supportata nell’elemento corpo di una pagina.

* È possibile una soluzione alternativa per implementare un corpo a schermo intero &quot;allungando&quot; l&#39;elemento corpo come segue:

```xml
body {
    position: absolute;
    top: 0;
    bottom: 0;
    right: 0;
    left: 0;
}
```

### Riduzione dei margini {#margin-collapsing}

I problemi di compressione del margine possono essere visti se il primo elemento figlio dell&#39;elemento corpo ha un margine.

* La soluzione è quella di aggiungere un clearfix a livello di elemento corpo, come segue:

```xml
body:before, body:after{
    content: ' ';
    display: table;
}
```
