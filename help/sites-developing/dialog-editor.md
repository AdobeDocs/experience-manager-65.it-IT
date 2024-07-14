---
title: Editor finestre di dialogo
description: L'editor di finestre di dialogo fornisce un'interfaccia grafica per creare e modificare facilmente finestre di dialogo e scaffold.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
exl-id: 57303608-c3e1-4201-8054-1a1798613e2c
solution: Experience Manager, Experience Manager Sites
feature: Developing,Developer Tools
role: Developer
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 0%

---

# Editor finestre di dialogo{#dialog-editor}

L&#39;editor di finestre di dialogo fornisce un&#39;interfaccia grafica per creare e modificare facilmente finestre di dialogo e scaffold.

Per vedere come funziona, passa a CRXDE Lite, apri la struttura dell&#39;elenco delle cartelle a `/libs/foundation/components/chart` e fai doppio clic sul nodo `dialog`:

![chlimage_1-247](assets/chlimage_1-247.png)

Il nodo della finestra di dialogo si apre nell&#39;editor di **finestre di dialogo**:

![schermata_shot_2012-02-01at25033pm](assets/screen_shot_2012-02-01at25033pm.png)

## Panoramica dell’interfaccia utente {#user-interface-overview}

L’interfaccia dell’editor di finestre di dialogo è composta da quattro riquadri:

* La **palette**, nell&#39;angolo superiore sinistro. Questo riquadro contiene i widget disponibili per la creazione di una finestra di dialogo, ad esempio i pannelli delle schede, i campi di testo, gli elenchi di selezione e i pulsanti. Puoi espandere le diverse categorie all’interno della palette facendo clic sulla barra di divisione desiderata.
* Il riquadro **struttura**, nell&#39;angolo inferiore sinistro. Questo riquadro mostra la struttura gerarchica dei nodi che costituiscono la definizione della finestra di dialogo. Per visualizzare la stessa struttura, espandi il nodo della finestra di dialogo in Esplora contenuto di CRXDE Lite o CRX.
* Il riquadro **render**, al centro della finestra. In questo riquadro viene illustrato il rendering della definizione di finestra di dialogo definita nel riquadro struttura come finestra di dialogo effettiva.
* Il riquadro **proprietà**. In questo riquadro vengono visualizzate le proprietà del nodo evidenziato nel riquadro struttura.

### Utilizzo dell’Editor finestre di dialogo {#using-the-dialog-editor}

Per creare una finestra di dialogo, l’utente trascina gli elementi dalla palette al riquadro della struttura nella posizione all’interno della gerarchia di definizione della finestra di dialogo.

Una volta completata la struttura desiderata, l&#39;utente fa clic su **Salva** nella parte superiore del riquadro di rendering.

>[!CAUTION]
>
>L’editor delle finestre di dialogo consente di creare finestre di dialogo semplici. Potrebbe non essere in grado di modificare definizioni di finestre di dialogo più complesse. Nei casi in cui l’editor di finestre di dialogo non consenta la modifica di una struttura di finestre di dialogo, la definizione della finestra di dialogo deve essere creata o modificata manualmente, oppure entrambe. A tale scopo, puoi modificare direttamente la struttura dei nodi utilizzando, ad esempio, CRXDE Lite o CRX Content Explorer.

### Creazione di una nuova finestra di dialogo {#creating-a-new-dialog}

Per creare una finestra di dialogo, selezionare il componente richiesto, fare clic su **Crea...** e quindi su **Crea finestra di dialogo...**.

Immetti i dettagli richiesti quindi fai clic su **Salva tutto**. Ora puoi fare doppio clic sulla finestra di dialogo per aprirla con l&#39;editor.

### Utilizzo dell&#39;Editor finestre di dialogo per gli scaffold {#using-the-dialog-editor-for-scaffolds}

Uno scaffold è una pagina speciale contenente un modulo che può essere compilato e inviato in un unico passaggio. Questo consente di creare rapidamente una pagina utilizzando il contenuto inserito.

Il modulo che costituisce uno scaffolding è definito da una definizione di finestra di dialogo, come una normale finestra di dialogo, anche se viene visualizzato nella pagina di scaffolding in un formato diverso. Poiché le definizioni delle finestre di dialogo vengono utilizzate per definire gli scaffold, questi possono essere progettati utilizzando l’editor di finestre di dialogo. Quando si utilizza l’editor di finestre di dialogo in questo modo, il riquadro di rendering visualizza comunque la definizione della finestra di dialogo sotto forma di finestra di dialogo e non come scaffold.

Consulta [Scaffolding](/help/sites-authoring/scaffolding.md) per ulteriori informazioni sull&#39;utilizzo dell&#39;editor di finestre di dialogo per creare scaffold.
