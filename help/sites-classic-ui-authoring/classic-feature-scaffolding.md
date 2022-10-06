---
title: Scaffolding
seo-title: Scaffolding
description: In alcuni casi può essere necessario creare un insieme di più pagine con la stessa struttura e contenuti diversi. Con la funzione di scaffolding è invece possibile creare un modulo (scaffolding significa letteralmente impalcatura) con i campi necessari per creare la struttura desiderata per le pagine e quindi utilizzare il modulo per creare agevolmente pagine basate su tale struttura.
seo-description: Sometimes you may need to create a large set of pages that share the same structure but have differing content. With scaffolding you can create a form (a scaffold) with fields that reflect the structure you want for your pages and then use this form to easily create pages based on this structure.
uuid: 5904abc0-b256-4da4-a7d7-3c17ea299648
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: a63e5732-b1a3-4639-9838-652af401e788
docset: aem65
exl-id: 58e61302-cfb4-4a3d-98d4-3c92baa2ad42
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1448'
ht-degree: 79%

---

# Scaffolding{#scaffolding}

In alcuni casi può essere necessario creare un insieme di più pagine con la stessa struttura e contenuti diversi. Tramite l’interfaccia standard di AEM sarebbe necessario creare ogni singola pagina, trascinarvi i componenti appropriati e completarli uno a uno.

Con la funzione di scaffolding è invece possibile creare un modulo (scaffolding significa letteralmente impalcatura) con i campi necessari per creare la struttura desiderata per le pagine e quindi utilizzare il modulo per creare agevolmente pagine basate su tale struttura.

>[!NOTE]
>
>Lo Scaffolding (nell’interfaccia classica) [rispetta l’ereditarietà MSM](#scaffolding-with-msm-inheritance).

## Utilizzo dello scaffolding {#how-scaffolding-works}

Le pagine di scaffolding sono memorizzate in **Strumenti** console dell’amministratore del sito.

* Apri la console **Strumenti** e fai clic su **Scaffolding pagine predefinito**.
* Quindi fai clic su **geometrixx**.
* In **geometrixx** è disponibile una *pagina di scaffolding* denominata **News**. Fai doppio clic sulla pagina per aprirla.

![howscaffolds_work](assets/howscaffolds_work.png)

La pagina di scaffolding è costituita da un modulo con un campo per ogni elemento di contenuto che forma la pagina da creare, oltre a quattro parametri importanti a cui è possibile accedere tramite il pulsante **Proprietà pagina** della pagina di scaffolding.

![pageprops](assets/pageprops.png)

Le proprietà della pagina di scaffolding sono:

* **Testo titolo**: nome della pagina di scaffolding stessa. In questo esempio è denominata “News”.
* **Descrizione**: visualizzata sotto il titolo della pagina di scaffolding.
* **Modello di destinazione**: modello che verrà utilizzato dalla pagina di scaffolding per creare una nuova pagina. In questo esempio il modello è *Pagina contenuto Geometrixx*.
* **Percorso di destinazione**: percorso della pagina padre in cui la pagina di scaffolding dovrà creare le nuove pagine. In questo esempio il percorso è */content/geometrixx/en/news*.

Il corpo della pagina di scaffolding è costituito dal modulo. Se un utente desidera creare una pagina tramite la pagina di scaffolding, deve compilare il modulo e fare clic su *Crea* in basso. Il modulo **News** dell’esempio precedente include i campi seguenti:

* **Titolo**: nome della pagina da creare. Questo campo è presente in tutte le pagine di scaffolding.
* **Testo**: questo campo corrisponde a un componente di testo nella pagina risultante.
* **Immagine**: Questo campo corrisponde a un componente immagine nella pagina risultante.
* **Immagine/Avanzato** - **Titolo**: titolo dell’immagine.
* **Immagine/Avanzato** - **Testo Alt**: testo alternativo dell’immagine.
* **Immagine/Avanzato**: **Descrizione**: Descrizione dell’immagine.
* **Immagine/Avanzato**: **Dimensione**: dimensione dell’immagine.
* **Tag/Parole chiave**: metadati da assegnare alla pagina. Questo campo è presente in tutte le pagine di scaffolding.

### Creazione di uno scaffolding {#creating-a-scaffold}

Per creare una nuova pagina di scaffolding, vai alla sezione **Strumenti** console, quindi **Scaffolding pagina predefinito** e crea una nuova pagina. Sarà disponibile un singolo tipo di modello di pagina, il *Modello per scaffolding.*

Vai a **Proprietà pagina** della nuova pagina e imposta il *Testo titolo*, *Descrizione*, *Modello di Target* e *Percorso di Target*, come descritto in precedenza.

Occorre quindi definire la struttura della pagina che verrà creata dalla pagina di scaffolding. Per eseguire questa operazione, vai in **[modalità di progettazione](/help/sites-authoring/page-authoring.md#sidekick)** nella pagina di scaffolding. Viene visualizzato un collegamento che consente di modificare la pagina di scaffolding nell’**editor basato su finestra di dialogo**.

![cq5_dialog_editor](assets/cq5_dialog_editor.png)

Tramite l’editor basato su finestra di dialogo è possibile specificare le proprietà che verranno create ogni volta che si crea una nuova pagina utilizzando questo scaffolding.

La definizione della finestra di dialogo per una pagina di scaffolding funziona in modo simile a quella di un componente (vedi [Componenti](/help/sites-developing/components.md)). Esistono tuttavia alcune importanti differenze:

* Le definizioni delle finestre di dialogo dei componenti sono rappresentate da normali finestre di dialogo (come mostrato nel riquadro centrale dell’editor basato su finestra di dialogo, ad esempio). Le definizioni delle finestre di dialogo delle pagine di scaffolding sono invece rappresentate come moduli nella pagina di scaffolding, anche se appaiono come normali finestre di dialogo nell’editor basato su finestra di dialogo (come mostrato nella pagina di scaffolding **News** qui sopra).
* Le finestre di dialogo dei componenti contengono solo i campi corrispondenti ai valori necessari per definire il contenuto di un particolare componente . Le finestre di dialogo delle pagine di scaffolding devono includere campi per tutte le proprietà di ogni paragrafo della pagina da creare.
* Nel caso delle finestre di dialogo dei componenti, il componente utilizzato per rappresentare il contenuto specificato è implicito, pertanto la proprietà del paragrafo `sling:resourceType` viene compilata automaticamente alla creazione del paragrafo. Per una pagina di scaffolding, la finestra di dialogo stessa deve includere tutte le informazioni che definiscono sia il contenuto che il componente assegnato per un determinato paragrafo. Nelle finestre di dialogo delle pagine di scaffolding tali informazioni devono essere fornite utilizzando campi *nascosti*, in modo da inviare le informazioni al momento della creazione della pagina.

Per comprendere il funzionamento, è possibile osservare la finestra di dialogo della pagina di scaffolding **News** nell’esempio nell’editor basato su finestra di dialogo. Apri la pagina di scaffolding in modalità progettazione e fai clic sul collegamento per l’editor basato su finestra di dialogo.

Ora fai clic sul campo della finestra di dialogo **Finestra di dialogo > Pannello a schede > Testo > Testo**, come riportato di seguito:

![textedit](assets/textedit.png)

Sul lato destro dell’editor basato su finestra di dialogo viene visualizzato l’elenco delle proprietà del campo:

![list_of_properties](assets/list_of_properties.png)

Osserva la proprietà nome per questo campo, con valore

`./jcr:content/par/text/text`

Questo è il nome della proprietà in cui verrà scritto il contenuto del campo quando la pagina di scaffolding verrà utilizzata per creare una pagina. La proprietà è definita come percorso relativo rispetto al nodo che rappresenta la pagina da creare. Specifica la proprietà text, sotto il nodo text, che si trova sotto il nodo par, che a sua volta è un nodo figlio del nodo jcr:content sotto il nodo della pagina.

Tale valore definisce il percorso di memorizzazione del contenuto per il testo che dovrà essere inserito in questo campo. È tuttavia necessario specificare altre due caratteristiche per il contenuto, ovvero:

* Il fatto che la stringa memorizzata in tale percorso deve essere interpretata come *testo RTF* e
* il componente da utilizzare per rappresentare il contenuto nella pagina risultante.

Nella finestra di dialogo di un componente normale, non sarebbe necessario specificare tali informazioni perché sono implicite, essendo la finestra di dialogo già associata a un componente specifico.

Per specificare queste due informazioni si utilizzano i campi nascosti. Fai clic sul primo campo nascosto **Finestra di dialogo > Pannello a schede > Testo > Nascosto**, come riportato di seguito:

![nascosto](assets/hidden.png)

Le proprietà di questo campo nascosto sono le seguenti:

![hidden_list_props](assets/hidden_list_props.png)

La proprietà nome del campo nascosto è

`./jcr:content/par/text/textIsRich`

Si tratta di una proprietà booleana utilizzata per interpretare la stringa di testo memorizzata in `./jcr:content/par/text/text`.

Poiché sappiamo che il testo deve essere interpretato come testo RTF, specifichiamo il `value` proprietà del campo come `true`.

>[!CAUTION]
>
>L’editor basato su finestra di dialogo consente all’utente di modificare i valori di *esistente* nella definizione della finestra di dialogo. Per aggiungere una nuova proprietà, l’utente deve utilizzare [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md). Ad esempio, i nuovi campi nascosti aggiunti alla definizione di una finestra di dialogo con l’editor basato su finestra di dialogo non dispongono della proprietà *valore*, ovvero una proprietà di nome &quot;valore&quot;. Se per il campo nascosto in questione è necessario impostare una proprietà *valore* predefinita, quest’ultima dovrà essere aggiunta manualmente tramite uno degli strumenti CRX. Il valore non può essere aggiunto direttamente tramite l’editor basato su finestra di dialogo. Se tuttavia la proprietà è già presente, è possibile modificarne il valore tramite l’editor basato su finestra di dialogo.

Il secondo campo nascosto può essere visualizzato facendo clic su di esso, come mostrato nella figura:

![hidden2](assets/hidden2.png)

Le proprietà di questo campo nascosto sono le seguenti:

![hidden_list_props2](assets/hidden_list_props2.png)

La proprietà nome del campo nascosto è

`./jcr:content/par/text/sling:resourceType`

e il valore fisso specificato per tale proprietà è

`foundation/components/textimage`

Tale valore indica che per rappresentare il contenuto di testo del paragrafo è necessario utilizzare il componente *Testo e immagine*. Utilizzo con `isRichText` Valore booleano specificato nell’altro campo nascosto, il componente può eseguire il rendering della stringa di testo effettiva memorizzata in `./jcr:content/par/text/text` nel modo desiderato.

### Scaffolding con ereditarietà MSM {#scaffolding-with-msm-inheritance}

Nell’interfaccia classica, lo scaffolding è completamente integrato con l’ereditarietà MSM (se applicabile).

Quando apri una pagina nella modalità di **scaffolding** (utilizzando l’icona nella parte inferiore di supporto) tutti i componenti che sono soggetti a ereditarietà verranno visualizzati da:

* un lucchetto (per la maggior parte dei componenti; ad esempio Testo e Titolo)
* una maschera con la dicitura **Fai clic per cancellare l’ereditarietà** (per componenti Immagine)

Questi mostrano che il componente non può essere modificato fino a quando l’ereditarietà non viene annullata.

![chlimage_1](assets/chlimage_1.jpeg)

>[!NOTE]
>
>È paragonabile ai [componenti ereditati quando si modifica il contenuto della pagina](/help/sites-authoring/editing-content.md#inheritedcomponentsclassicui).

Facendo clic sul simbolo del lucchetto o sull’icona dell’immagine è possibile interrompere l’ereditarietà:

* Il simbolo si trasforma in un lucchetto aperto.
* Una volta sbloccato, è possibile modificare il contenuto.

![chlimage_1-1](assets/chlimage_1-1.jpeg)

Dopo lo sblocco è possibile ripristinare l’ereditarietà con un clic sul simbolo del lucchetto aperto; tutte le modifiche apportate andranno perdute.

>[!NOTE]
>
>Se l’ereditarietà viene annullata a livello di pagina (dalla scheda Livecopy di Proprietà pagina), tutti i componenti saranno modificabili in **Scaffolding** (verranno visualizzati in stato sbloccato).
