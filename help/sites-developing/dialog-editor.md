---
title: Editor finestre di dialogo
seo-title: Editor finestre di dialogo
description: L’editor basato su finestra di dialogo offre un’interfaccia grafica per la creazione e la modifica di finestre di dialogo e pagine di scaffolding
seo-description: L’editor basato su finestra di dialogo offre un’interfaccia grafica per la creazione e la modifica di finestre di dialogo e pagine di scaffolding
uuid: 64d3fb12-8638-441b-8595-c590d48f3072
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: b7ac457d-3689-4f5d-9ceb-ff6a9944e7eb
translation-type: tm+mt
source-git-commit: 58fa0f05bae7ab5ba51491be3171b5c6ffbe870d
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 0%

---


# Editor finestre di dialogo{#dialog-editor}

L’editor basato su finestra di dialogo fornisce un’interfaccia grafica per creare e modificare facilmente finestre di dialogo e pagine di scaffolding.

Per vedere come funziona, andate al CRXDE Lite, aprite la struttura dell&#39;esploratore su `/libs/foundation/components/chart` e fate doppio clic sul nodo `dialog`:

![chlimage_1-247](assets/chlimage_1-247.png)

Il nodo della finestra di dialogo si aprirà nell&#39;editor della finestra di dialogo **a1/>:**

![screen_shot_2012-02-01at25033pm](assets/screen_shot_2012-02-01at25033pm.png)

## Panoramica dell&#39;interfaccia utente {#user-interface-overview}

L’interfaccia dell’editor basato su finestra di dialogo è composta da quattro riquadri:

* La **palette**, nell&#39;angolo superiore sinistro. Questo riquadro contiene i widget disponibili per la creazione di una finestra di dialogo, ad esempio pannelli di schede, campi di testo, elenchi di selezione e pulsanti. Per espandere le diverse categorie all’interno della palette, fare clic sulla barra di divisione desiderata.
* Il riquadro **struttura**, nell&#39;angolo inferiore sinistro. Questo riquadro mostra la struttura gerarchica dei nodi che compongono la definizione della finestra di dialogo. È possibile visualizzare la stessa struttura espandendo il nodo di dialogo in Esplora contenuti CRXDE Lite o CRX.
* Il riquadro **rendering**, al centro della finestra. Questo riquadro mostra come verrà visualizzata la definizione della finestra di dialogo definita nel riquadro della struttura come una finestra di dialogo effettiva.
* Il riquadro **properties**. Questo riquadro mostra le proprietà del nodo attualmente evidenziato nel riquadro della struttura.

### Utilizzo dell&#39;Editor finestre di dialogo {#using-the-dialog-editor}

Per creare una finestra di dialogo, l&#39;utente trascina e rilascia elementi dalla palette al riquadro della struttura in posizione all&#39;interno della gerarchia delle definizioni delle finestre di dialogo.

Una volta completata la struttura desiderata, l&#39;utente fa clic su **Salva**, nella parte superiore del riquadro di rendering.

>[!CAUTION]
>
>L’editor basato su finestra di dialogo è destinato alla creazione di finestre di dialogo relativamente semplici e potrebbe non essere in grado di modificare definizioni di dialogo più complesse. Se l’editor basato su finestra di dialogo non consente la modifica di una struttura di dialogo, la definizione della finestra di dialogo deve essere creata e/o modificata manualmente modificando direttamente la struttura del nodo utilizzando, ad esempio, CRXDE Lite o CRX Content Explorer.

### Creazione di una nuova finestra di dialogo {#creating-a-new-dialog}

Per creare una nuova finestra di dialogo, è necessario selezionare il componente richiesto, fare clic su **Crea...** e quindi **Crea finestra di dialogo...**.

Inserite i dettagli richiesti e fate clic su **Salva tutto**. Ora potete fare doppio clic sulla finestra di dialogo per aprirla con l&#39;editor.

### Utilizzo dell&#39;Editor finestra di dialogo per scaffolding {#using-the-dialog-editor-for-scaffolds}

Una pagina di scaffolding è una pagina speciale contenente un modulo che può essere compilato e inviato in un unico passaggio. Questo consente di creare rapidamente una pagina utilizzando il contenuto immesso.

Il modulo che costituisce una pagina di scaffolding è definito da una definizione di finestra di dialogo, come una normale finestra di dialogo, anche se viene visualizzato sulla pagina di scaffolding in un altro modulo. Poiché le definizioni delle finestre di dialogo vengono utilizzate per definire le pagine di scaffolding, queste possono essere progettate utilizzando l’editor basato su finestra di dialogo. Tenere presente che quando si utilizza l’editor basato su finestra di dialogo in questo modo, nel riquadro di rendering viene visualizzata la definizione della finestra di dialogo sotto forma di una finestra di dialogo non come una pagina di scaffolding.

Per ulteriori informazioni sull&#39;utilizzo dell&#39;editor basato su finestra di dialogo per creare le pagine di scaffolding, vedere [Scaffolding](/help/sites-authoring/scaffolding.md).
