---
title: Scaffolding
description: A volte può essere necessario creare un set di pagine di grandi dimensioni con una struttura comune ma contenuti diversi. Con lo scaffolding è possibile creare un modulo (uno scaffold) con campi che riflettono la struttura desiderata per le pagine e quindi utilizzare questo modulo per creare facilmente pagine basate su questa struttura.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
docset: aem65
exl-id: 58e61302-cfb4-4a3d-98d4-3c92baa2ad42
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '1418'
ht-degree: 0%

---

# Scaffolding{#scaffolding}

A volte può essere necessario creare un set di pagine di grandi dimensioni con una struttura comune ma contenuti diversi. Tramite l’interfaccia standard di Adobe Experience Manager (AEM), è necessario creare ogni pagina, trascinare i componenti appropriati nella pagina e compilarli singolarmente.

Con lo scaffolding è possibile creare un modulo (uno scaffold) con campi che riflettono la struttura desiderata per le pagine e quindi utilizzare questo modulo per creare facilmente pagine basate su questa struttura.

>[!NOTE]
>
>Scaffolding (nell’interfaccia classica) [rispetta l’ereditarietà MSM](#scaffolding-with-msm-inheritance).

## Come funziona lo scaffolding {#how-scaffolding-works}

Le impalcature sono memorizzate in **Strumenti** console dell’amministratore del sito.

* Apri **Strumenti** e fai clic su **Scaffolding pagine predefinito**.
* Sotto fai clic su **Geometrixx**.
* Sotto **Geometrixx**, è possibile trovare un *pagina scaffold* ha chiamato **Notizie**. Fare doppio clic per aprire la pagina.

![howscaffolds_work](assets/howscaffolds_work.png)

Lo scaffold è costituito da un modulo con un campo per ogni elemento di contenuto che costituirà la pagina da creare e quattro parametri importanti a cui si accede tramite **Proprietà pagina** della pagina scaffold.

![pageprops](assets/pageprops.png)

Le proprietà della pagina di scaffolding sono:

* **Testo titolo**: nome della pagina di scaffolding stessa. In questo esempio, si chiama &quot;News&quot;.
* **Descrizione**: questo viene visualizzato sotto il titolo nella pagina di scaffolding.
* **Modello di destinazione**: questo è il modello che verrà utilizzato da questo scaffold per creare una pagina. In questo esempio, è un *Pagina contenuto Geometrixx* modello.
* **Percorso di destinazione**: questo è il percorso della pagina padre sotto la quale questo scaffold creerà le pagine. In questo esempio, il percorso è */content/geometrixx/en/news*.

Il corpo dell&#39;impalcatura è la forma. Quando un utente desidera creare una pagina utilizzando lo scaffold compila il modulo e fa clic su *Crea*, in basso. In **Notizie** esempio precedente il modulo include i campi seguenti:

* **Titolo**: questo è il nome della pagina da creare. Questo campo è sempre presente su ogni scaffold.
* **Testo**: questo campo corrisponde a un componente Testo nella pagina risultante.
* **Immagine**: questo campo corrisponde a un componente Immagine nella pagina risultante.
* **Immagine/Avanzato**: **Titolo**: titolo dell’immagine.
* **Immagine/Avanzato**: **Testo alternativo**: testo alternativo per l’immagine.
* **Immagine/Avanzato**: **Descrizione**: descrizione dell’immagine.
* **Immagine/Avanzato**: **Dimensione**: dimensione dell’immagine.
* **Tag/Parole chiave**: metadati da assegnare a questa pagina. Questo campo è sempre presente su ogni scaffold.

### Creazione di uno scaffold {#creating-a-scaffold}

Per creare uno scaffold, vai al **Strumenti** console, quindi **Scaffolding pagine predefinito** e creare una pagina. È disponibile un tipo di modello a pagina singola, il *Modello per scaffolding.*

Vai a **Proprietà pagina** della nuova pagina e imposta *Testo titolo*, *Descrizione*, *Modello di destinazione*, e *Percorso di destinazione*, come descritto in precedenza.

Successivamente, devi definire la struttura della pagina che verrà creata da questo scaffold. Per fare questo, vai in **[modalità progettazione](/help/sites-authoring/page-authoring.md#sidekick)** sulla pagina scaffold. Viene visualizzato un collegamento che consente di modificare lo scaffold in **editor di finestre di dialogo**.

![cq5_dialog_editor](assets/cq5_dialog_editor.png)

Utilizzando l’editor delle finestre di dialogo, puoi specificare le proprietà che verranno create ogni volta che viene creata una nuova pagina utilizzando questo scaffold.

La definizione della finestra di dialogo per uno scaffold funziona in modo simile a quella di un componente (vedere [Componenti](/help/sites-developing/components.md)). Tuttavia, si applicano alcune importanti differenze:

* Le definizioni delle finestre di dialogo dei componenti vengono visualizzate come normali finestre di dialogo (come mostrato ad esempio nel riquadro centrale dell’editor delle finestre di dialogo), mentre le definizioni delle finestre di dialogo di scaffold, sebbene vengano visualizzate come normali finestre di dialogo nell’editor delle finestre di dialogo, vengono visualizzate nella pagina di scaffold come un modulo di scaffold (come mostrato nella **Notizie** scaffold superiore).
* Le finestre di dialogo dei componenti forniscono campi solo per i valori necessari per definire il contenuto di un singolo componente specifico. Una finestra di dialogo di scaffold deve fornire campi per ogni proprietà in ogni paragrafo della pagina da creare.
* Se sono presenti finestre di dialogo di componenti, il componente utilizzato per riprodurre il contenuto specificato è implicito e quindi il `sling:resourceType` del paragrafo viene compilata automaticamente al momento della creazione del paragrafo. Con uno scaffold tutte le informazioni che definiscono sia il contenuto che il componente assegnato per un dato paragrafo devono essere fornite dalla finestra di dialogo stessa. Nelle finestre di dialogo dello scaffold queste informazioni devono essere fornite utilizzando *Nascosto* per inviare queste informazioni durante la creazione della pagina.

Guarda l’esempio **Notizie** la finestra di dialogo scaffold nell’editor di finestre di dialogo consente di spiegare come funziona. Passa alla modalità progettazione nella pagina scaffold e fai clic sul collegamento dell’editor delle finestre di dialogo.

Fare clic sul campo della finestra di dialogo **Finestra di dialogo > Pannello a schede > Testo > Testo**, come segue:

![textedit](assets/textedit.png)

L’elenco delle proprietà per questo campo viene visualizzato sul lato destro dell’editor di finestre di dialogo, come segue:

![list_of_properties](assets/list_of_properties.png)

Osserva la proprietà name per questo campo. Ha il valore

`./jcr:content/par/text/text`

Questo è il nome della proprietà in cui verrà scritto il contenuto del campo quando lo scaffold viene utilizzato per creare una pagina. La proprietà viene indicata come percorso relativo dal nodo che rappresenta la pagina da creare. Specifica il testo della proprietà, sotto il testo del nodo, che si trova sotto la parte del nodo, a sua volta figlio del nodo jcr:content sotto il nodo della pagina.

Consente di definire la posizione di archiviazione del contenuto per il testo che verrà immesso in questo campo. Tuttavia, è necessario specificare anche altre due caratteristiche per questo contenuto:

* Il fatto che la stringa memorizzata qui debba essere interpretata come *testo RTF*, e
* quale componente deve essere utilizzato per eseguire il rendering di questo contenuto nella pagina risultante.

In una normale finestra di dialogo di un componente non è necessario specificare queste informazioni perché sono implicite nel fatto che la finestra di dialogo è già associata a un componente specifico.

Per specificare queste due informazioni, utilizzare i campi nascosti. Fai clic sul primo campo nascosto **Finestra di dialogo > Pannello a schede > Testo > Nascosto**, come segue:

![nascosto](assets/hidden.png)

Le proprietà di questo campo nascosto sono le seguenti:

![hidden_list_props](assets/hidden_list_props.png)

La proprietà name di questo campo nascosto è

`./jcr:content/par/text/textIsRich`

Questa è una proprietà booleana utilizzata per interpretare la stringa di testo memorizzata in `./jcr:content/par/text/text`.

Poiché sappiamo che il testo deve essere interpretato come testo RTF, specifichiamo il `value` proprietà di questo campo come `true`.

>[!CAUTION]
>
>L’editor di finestre di dialogo consente all’utente di modificare i valori di *esistente* proprietà nella definizione della finestra di dialogo. Per aggiungere una nuova proprietà, l’utente deve utilizzare [CRXDE Liti](/help/sites-developing/developing-with-crxde-lite.md). Ad esempio, quando un nuovo campo nascosto viene aggiunto a una definizione di finestra di dialogo con l’editor di finestre di dialogo, non dispone di un *valore* proprietà (ovvero una proprietà denominata &quot;value&quot;). Se il campo nascosto in questione richiede l’impostazione di una proprietà di valore predefinita, questa deve essere aggiunta manualmente con uno degli strumenti CRX. Impossibile aggiungere il valore con l’editor di finestre di dialogo stesso. Tuttavia, una volta presente la proprietà, il relativo valore può essere modificato con l’editor di finestre di dialogo.

Per visualizzare il secondo campo nascosto, fai clic su di esso in questo modo:

![hidden2](assets/hidden2.png)

Le proprietà di questo campo nascosto sono le seguenti:

![hidden_list_props2](assets/hidden_list_props2.png)

La proprietà name di questo campo nascosto è

`./jcr:content/par/text/sling:resourceType`

Il valore fisso specificato per questa proprietà è

`foundation/components/textimage`

Questo specifica che il componente da utilizzare per il rendering del contenuto di testo di questo paragrafo è il *Immagine testo* componente. Utilizzo di con `isRichText` booleano specificato nell’altro campo nascosto, il componente può riprodurre la stringa di testo effettiva memorizzata in `./jcr:content/par/text/text` nel modo desiderato.

### Scaffolding con ereditarietà MSM {#scaffolding-with-msm-inheritance}

Nell’interfaccia classica, lo scaffolding è completamente integrato con l’ereditarietà MSM (se applicabile).

Quando apri una pagina in **Scaffolding** modalità (utilizzando l’icona nella parte inferiore della barra laterale), tutti i componenti soggetti a ereditarietà saranno indicati da:

* un simbolo di blocco (per la maggior parte dei componenti, ad esempio Testo e Titolo)
* una maschera con il testo **Fai clic per annullare l’ereditarietà** (per componenti Immagine)

Questi mostrano che il componente non può essere modificato fino a quando l’ereditarietà non viene annullata.

![chlimage_1](assets/chlimage_1.jpeg)

>[!NOTE]
>
>È paragonabile a [componenti ereditati durante la modifica del contenuto della pagina](/help/sites-authoring/editing-content.md#inheritedcomponentsclassicui).

Facendo clic sul simbolo del lucchetto o sull’icona dell’immagine è possibile interrompere l’ereditarietà:

* il simbolo diventa un lucchetto aperto.
* una volta sbloccato, puoi modificare il contenuto.

![chlimage_1-1](assets/chlimage_1-1.jpeg)

Dopo aver sbloccato, puoi ripristinare l’ereditarietà facendo clic sul simbolo del lucchetto sbloccato: tutte le modifiche apportate andranno perse.

>[!NOTE]
>
>Se l’ereditarietà viene annullata a livello di pagina (dalla scheda Live Copy di Proprietà pagina), tutti i componenti sono modificabili in **Scaffolding** (vengono visualizzate in stato sbloccato).
