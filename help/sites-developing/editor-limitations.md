---
title: Limitazioni per l’editor
seo-title: Limitazioni per l’editor
description: L’editor nell’interfaccia touch utilizza le sovrapposizioni per interagire con contenuti confinati in un iframe. Questa interazione crea alcune limitazioni sia nell'utilizzo dell'editor che per gli sviluppatori.
seo-description: L’editor nell’interfaccia touch utilizza le sovrapposizioni per interagire con contenuti confinati in un iframe. Questa interazione crea alcune limitazioni sia nell'utilizzo dell'editor che per gli sviluppatori.
uuid: ff524530-3f3a-4c5b-9f94-4aa9aeb9d461
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: introduction
discoiquuid: d748decb-a614-4c9e-a502-d6176b720f1a
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Limitazioni per l’editor{#editor-limitations}

L’editor nell’interfaccia touch utilizza le sovrapposizioni per interagire con contenuti confinati in un iframe. Questa interazione crea alcune limitazioni sia nell&#39;utilizzo dell&#39;editor che per gli sviluppatori. In questa pagina vengono riepilogati questi limiti e vengono fornite soluzioni o soluzioni alternative, laddove possibile.

## Limitazioni funzionali {#functional-limitations}

Un autore può incontrare le seguenti limitazioni funzionali quando utilizza l’editor per creare le pagine.

### Collegamenti non attivi {#links-not-active}

Durante la [modifica di una pagina](/help/sites-authoring/editing-content.md), i collegamenti non sono attivi.

* [Passate alla modalità **Anteprima** per](/help/sites-authoring/editing-content.md#preview-mode) spostarsi utilizzando i collegamenti presenti nel contenuto.

## Limitazioni CSS {#css-limitations}

Uno sviluppatore può incontrare le seguenti limitazioni con le interazioni dell&#39;editor con CSS.

### Elementi posizionati in modo assoluto {#absolutely-positioned-elements}

Gli elementi posizionati in modo assoluto possono causare problemi nella posizione della sovrapposizione.

* In questo caso, accertatevi che le dimensioni dell’elemento con posizione assoluta siano corrette perché l’editor creerà una sovrapposizione con le stesse dimensioni.

### unità VH {#vh-units}

`vh` le unità non sono supportate perché l&#39;altezza iframe deve essere regolata automaticamente da AEM.

### Immagini di sfondo fisse {#fixed-background-images}

Le immagini di sfondo fisse potrebbero non essere visualizzate come fisse durante lo scorrimento a causa del fatto che sono incorporate all&#39;interno di un iframe.

* Selezionando **Visualizza pagina come pubblicata** nelle azioni della barra dell’intestazione, la pagina viene visualizzata correttamente.

### 100% Height {#height}

Altezza 100% non supportata nell&#39;elemento body di una pagina.

* È possibile una soluzione alternativa per implementare un corpo a schermo intero &quot;allungando&quot; l&#39;elemento body come segue:

```xml
body {
    position: absolute;
    top: 0;
    bottom: 0;
    right: 0;
    left: 0;
}
```

### Riduzione margini {#margin-collapsing}

I problemi di riduzione del margine possono essere visti se il primo elemento figlio dell&#39;elemento body ha un margine.

* La soluzione consiste nell&#39;aggiungere una correzione a livello di elemento body, come segue:

```xml
body:before, body:after{
    content: ' ';
    display: table;
}
```

