---
title: Editor finestre di dialogo
seo-title: Dialog Editor
description: L'editor di finestre di dialogo fornisce un'interfaccia grafica per la creazione e la modifica di finestre di dialogo e scaffold
seo-description: The dialog editor provides a graphical interface for easily creating and editing dialog boxes and scaffolds
uuid: 64d3fb12-8638-441b-8595-c590d48f3072
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: b7ac457d-3689-4f5d-9ceb-ff6a9944e7eb
exl-id: 57303608-c3e1-4201-8054-1a1798613e2c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 0%

---

# Editor finestre di dialogo{#dialog-editor}

L&#39;editor di finestre di dialogo fornisce un&#39;interfaccia grafica per creare e modificare facilmente finestre di dialogo e scaffold.

Per vedere come funziona, vai a CRXDE Lite, apri la struttura ad albero dell’Explorer per `/libs/foundation/components/chart` e fai doppio clic sul nodo `dialog`:

![chlimage_1-247](assets/chlimage_1-247.png)

Il nodo della finestra di dialogo si aprirà nel **editor di finestre di dialogo**:

![screen_shot_2012-02-01at25033pm](assets/screen_shot_2012-02-01at25033pm.png)

## Panoramica dell’interfaccia utente {#user-interface-overview}

L’interfaccia dell’editor di finestre di dialogo è composta da quattro riquadri:

* Il **palette**, nell’angolo in alto a sinistra. Questo riquadro contiene i widget disponibili per la creazione di una finestra di dialogo, ad esempio pannelli di schede, campi di testo, elenchi di selezione e pulsanti. Puoi espandere le diverse categorie all’interno della palette facendo clic sulla barra di divisione desiderata.
* Il **struttura** nell&#39;angolo inferiore sinistro. Questo riquadro mostra la struttura gerarchica dei nodi che costituiscono la definizione della finestra di dialogo. Puoi visualizzare la stessa struttura espandendo il nodo della finestra di dialogo in Esplora contenuto di CRXDE Lite o CRX.
* Il **rendering** al centro della finestra. In questo riquadro viene illustrato come verrà eseguito il rendering della definizione di finestra di dialogo definita nel riquadro struttura come finestra di dialogo effettiva.
* Il **proprietà** riquadro. In questo riquadro vengono visualizzate le proprietà del nodo attualmente evidenziato nel riquadro della struttura.

### Utilizzo dell’Editor finestre di dialogo {#using-the-dialog-editor}

Per creare una finestra di dialogo, l’utente trascina gli elementi dalla palette al riquadro della struttura nella posizione all’interno della gerarchia di definizione della finestra di dialogo.

Una volta completata la struttura desiderata, l’utente fa clic su **Salva**, nella parte superiore del riquadro di rendering.

>[!CAUTION]
>
>Tieni presente che l’editor delle finestre di dialogo è destinato alla creazione di finestre di dialogo relativamente semplici e potrebbe non essere in grado di modificare definizioni di finestre di dialogo più complesse. Nei casi in cui l’editor di finestre di dialogo non consenta la modifica di una struttura di finestre di dialogo, la definizione della finestra di dialogo deve essere creata e/o modificata manualmente modificando direttamente la struttura del nodo utilizzando, ad esempio, CRXDE Lite o CRX Content Explorer.

### Creazione di una nuova finestra di dialogo {#creating-a-new-dialog}

Per creare una nuova finestra di dialogo, seleziona il componente richiesto e fai clic su **Crea...** e poi **Crea finestra...**.

Inserisci i dettagli richiesti, quindi fai clic su **Salva tutto** - ora puoi fare doppio clic sulla finestra di dialogo per aprirla con l’editor.

### Utilizzo dell&#39;Editor finestre di dialogo per gli scaffold {#using-the-dialog-editor-for-scaffolds}

Uno scaffold è una pagina speciale contenente un modulo che può essere compilato e inviato in un unico passaggio. Questo consente di creare rapidamente una pagina utilizzando il contenuto inserito.

Il modulo che costituisce uno scaffolding è definito da una definizione di finestra di dialogo, come una normale finestra di dialogo, anche se viene visualizzato nella pagina di scaffolding in un formato diverso. Poiché le definizioni delle finestre di dialogo vengono utilizzate per definire gli scaffold, questi possono essere progettati utilizzando l’editor di finestre di dialogo. Tieni presente che quando utilizzi l’editor di finestre di dialogo in questo modo, nel riquadro di rendering verrà comunque visualizzata la definizione della finestra di dialogo sotto forma di finestra di dialogo e non come scaffold.

Consulta [Scaffolding](/help/sites-authoring/scaffolding.md) per ulteriori informazioni sull&#39;utilizzo dell&#39;editor di finestre di dialogo per la creazione di scaffold.
