---
title: Sviluppo di componenti AEM
seo-title: Sviluppo di componenti AEM
description: I componenti AEM vengono utilizzati per conservare, formattare ed eseguire il rendering del contenuto reso disponibile sulle pagine web.
seo-description: I componenti AEM vengono utilizzati per conservare, formattare ed eseguire il rendering del contenuto reso disponibile sulle pagine web.
uuid: 1f39daa6-7277-45a2-adcc-74b58c93b8e4
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 8cdb6db4-adaa-4eda-af7d-310a0b44b80b
docset: aem65
legacypath: /content/docs/en/aem/6-2/develop/components/components-touch-optimized
translation-type: tm+mt
source-git-commit: 7035c19a109ff67655ee0419aa37d1723e2189cc
workflow-type: tm+mt
source-wordcount: '3533'
ht-degree: 1%

---


# Sviluppo di componenti AEM{#developing-aem-components}

I componenti AEM vengono utilizzati per conservare, formattare ed eseguire il rendering del contenuto reso disponibile sulle pagine web.

* Quando [si creano pagine](/help/sites-authoring/default-components.md), i componenti consentono agli autori di modificare e configurare il contenuto.

   * Quando si crea un sito [Commerce](/help/sites-administering/ecommerce.md) i componenti possono, ad esempio, raccogliere ed eseguire il rendering delle informazioni dal catalogo.
Per ulteriori informazioni, consulta [Sviluppo di eCommerce](/help/sites-developing/ecommerce.md) .

   * Durante la costruzione di un sito [Communities](/help/communities/author-communities.md) i componenti possono fornire informazioni ai visitatori e raccogliere informazioni da essi.
Per ulteriori informazioni, consulta [Sviluppo di community](/help/communities/communities.md) .

* Nell’istanza di pubblicazione i componenti eseguono il rendering del contenuto, presentandolo come necessario ai visitatori del sito web.

>[!NOTE]
>
>Questa pagina è una continuazione del documento [Componenti AEM - Nozioni di base](/help/sites-developing/components-basics.md).

>[!CAUTION]
>
>I componenti riportati di seguito `/libs/cq/gui/components/authoring/dialog` devono essere utilizzati solo nell’editor (finestre di dialogo dei componenti nell’authoring). Se vengono utilizzati altrove (ad esempio in una finestra di dialogo della procedura guidata), potrebbero non comportarsi come previsto.

## Esempi di codice {#code-samples}

Questa pagina fornisce la documentazione di riferimento (o collegamenti alla documentazione di riferimento) necessaria per sviluppare nuovi componenti per AEM. Per alcuni esempi pratici, consulta [Sviluppo di componenti AEM - Esempi di codice](/help/sites-developing/developing-components-samples.md) .

## Struttura {#structure}

La struttura di base di un componente viene illustrata nella pagina [Componenti AEM - Nozioni di base](/help/sites-developing/components-basics.md#structure). Questo documento tratta sia le interfacce touch che quelle classiche. Anche se non è necessario utilizzare le impostazioni classiche nel nuovo componente, può essere utile tenerne conto quando si ereditano da componenti esistenti.

## Estensione dei componenti e delle finestre di dialogo esistenti {#extending-existing-components-and-dialogs}

A seconda del componente che desideri implementare, potrebbe essere possibile estendere o personalizzare un&#39;istanza esistente, anziché definire e sviluppare da zero l&#39;intera [struttura](#structure).

Quando estendete o personalizzate un componente o una finestra di dialogo esistente, potete copiare o replicare l’intera struttura o la struttura necessaria per la finestra di dialogo prima di apportare le modifiche.

### Estensione di un componente esistente {#extending-an-existing-component}

L&#39;estensione di un componente esistente può essere ottenuta con [Gerarchia dei tipi di risorsa](/help/sites-developing/components-basics.md#component-hierarchy-and-inheritance) e i relativi meccanismi di ereditarietà.

>[!NOTE]
>
>I componenti possono anche essere ridefiniti con una sovrapposizione in base alla logica del percorso di ricerca. Tuttavia in questo caso, [Sling Resource Merger](/help/sites-developing/sling-resource-merger.md) non verrà attivato e `/apps` deve definire l&#39;intera sovrapposizione.

>[!NOTE]
>
>Anche il [componente frammento di contenuto](/help/sites-developing/customizing-content-fragments.md) può essere personalizzato ed esteso, anche se è necessario considerare la struttura e le relazioni complete con Assets.

### Personalizzazione di una finestra di dialogo del componente esistente {#customizing-a-existing-component-dialog}

È inoltre possibile ignorare una finestra di dialogo di *componente* utilizzando [Sling Resource Merger](/help/sites-developing/sling-resource-merger.md) e definendo la proprietà `sling:resourceSuperType`.

Questo significa che devi solo ridefinire le differenze richieste, invece di ridefinire l’intera finestra di dialogo (utilizzando `sling:resourceSuperType`). Metodo consigliato per l’estensione di una finestra di dialogo di un componente

Per ulteriori informazioni, consulta [Sling Resource Merger](/help/sites-developing/sling-resource-merger.md) .

## Definizione del markup {#defining-the-markup}

Viene eseguito il rendering del componente con [HTML](https://www.w3schools.com/htmL/html_intro.asp). Il componente deve definire l’HTML necessario per prendere il contenuto richiesto e quindi eseguirne il rendering come necessario, sia negli ambienti di authoring che di pubblicazione.

### Utilizzo di HTML Template Language {#using-the-html-template-language}

Il [HTML Template Language (HTL)](https://docs.adobe.com/content/help/it-IT/experience-manager-htl/using/overview.html), introdotto con AEM 6.0, sostituisce JSP (JavaServer Pages) come sistema di modelli lato server preferito e consigliato per HTML. Per gli sviluppatori web che hanno bisogno di creare siti web aziendali affidabili, HTL consente di ottenere maggiore sicurezza ed efficienza di sviluppo.

>[!NOTE]
>
>Sebbene sia HTL che JSP possano essere utilizzati per lo sviluppo di componenti, in questa pagina verrà illustrato lo sviluppo con HTL, in quanto è il linguaggio di script consigliato per AEM.

## Sviluppo della logica dei contenuti {#developing-the-content-logic}

Questa logica facoltativa seleziona e/o calcola il contenuto di cui eseguire il rendering. Viene richiamato dalle espressioni HTL con il pattern Use-API appropriato.

Il meccanismo per separare la logica dall&#39;aspetto aiuta a chiarire ciò che viene richiesto per una determinata vista. Permette anche di usare logiche diverse per diverse viste della stessa risorsa.

### Utilizzo di Java {#using-java}

[L’API di utilizzo Java HTL abilita un file HTL per accedere a metodi helper in una classe](https://helpx.adobe.com/experience-manager/htl/using/use-api-java.html) Java personalizzata. Questo consente di utilizzare il codice Java per implementare la logica necessaria per selezionare e configurare il contenuto del componente.

### Uso di JavaScript {#using-javascript}

[L’API di utilizzo JavaScript HTL abilita un file HTL per accedere al codice helper scritto in JavaScript](https://helpx.adobe.com/experience-manager/htl/using/use-api-javascript.html). Questo consente di utilizzare il codice JavaScript per implementare la logica necessaria per selezionare e configurare il contenuto del componente.

### Utilizzo di librerie HTML lato client {#using-client-side-html-libraries}

I siti web moderni si basano fortemente sull’elaborazione lato client basata su codice JavaScript e CSS complessi. Organizzare e ottimizzare il servizio di questo codice può essere un problema complicato.

Per risolvere questo problema, AEM fornisce **Cartelle libreria lato client**, che ti consentono di memorizzare il codice lato client nell’archivio, organizzarlo in categorie e definire quando e come ogni categoria di codice deve essere trasmessa al client. Il sistema di libreria lato client si occupa quindi di produrre i collegamenti corretti nella pagina web finale per caricare il codice corretto.

Leggi [Utilizzo di librerie HTML lato client](/help/sites-developing/clientlibs.md) per ulteriori informazioni.

## Configurazione del comportamento di modifica {#configuring-the-edit-behavior}

Puoi configurare il comportamento di modifica di un componente, compresi attributi come le azioni disponibili per il componente, le caratteristiche dell’editor locale e i listener relativi agli eventi sul componente. La configurazione è comune sia all’interfaccia touch che all’interfaccia classica, anche se con alcune specifiche differenze.

Il comportamento di [modifica di un componente è configurato](/help/sites-developing/components-basics.md#edit-behavior) aggiungendo un nodo `cq:editConfig` di tipo `cq:EditConfig` sotto il nodo del componente (di tipo `cq:Component`) e aggiungendo proprietà specifiche e nodi figlio.

## Configurazione del comportamento di anteprima {#configuring-the-preview-behavior}

Il cookie [WCM Mode](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/WCMMode.html) viene impostato quando si passa alla modalità **Preview** anche quando la pagina non viene aggiornata.

Per i componenti con un rendering sensibile alla modalità WCM, è necessario definirli per aggiornarsi in modo specifico, quindi basarsi sul valore del cookie.

>[!NOTE]
>
>Nell’interfaccia touch sono utilizzati solo i valori `EDIT` e `PREVIEW` per il cookie [WCM Mode](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/WCMMode.html) .

## Creazione e configurazione di una finestra di dialogo {#creating-and-configuring-a-dialog}

Le finestre di dialogo consentono all’autore di interagire con il componente. L’utilizzo di una finestra di dialogo consente agli autori e/o agli amministratori di modificare il contenuto, configurare il componente o definire parametri di progettazione (mediante una [finestra di dialogo Progettazione](#creating-and-configuring-a-design-dialog))

### Interfaccia Coral e interfaccia Granite {#coral-ui-and-granite-ui}

[L’](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/coral-ui/coralui3/index.html) interfaccia Corale  [l’](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html) interfaccia Granite definiscono l’aspetto moderno dell’AEM.

[L’interfaccia utente Granite offre una vasta gamma di componenti di base (widget)](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html) necessari per creare una finestra di dialogo nell’ambiente di authoring. Se necessario, puoi estendere questa selezione e [creare un widget personalizzato](#creatinganewwidget).

Per ulteriori informazioni sullo sviluppo di componenti con tipi di risorse Coral e Granite, consulta: [Creazione di componenti di Experience Manager utilizzando i tipi di risorse Coral/Granite](https://helpx.adobe.com/experience-manager/using/aem64_coral_resourcetypes.html).

Per maggiori dettagli consultare:

* Interfaccia Coral

   * Fornisce un&#39;interfaccia utente coerente in tutte le soluzioni cloud
   * [Concetti dell’interfaccia AEM touch - Interfaccia Coral](/help/sites-developing/touch-ui-concepts.md#coral-ui)
   * [Guida all’interfaccia utente Coral](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/coral-ui/coralui3/index.html)

* Interfaccia Granite

   * Fornisce il markup dell’interfaccia utente Coral nei componenti Sling per la creazione di console e finestre di dialogo dell’interfaccia utente
   * [Concetti dell’interfaccia AEM touch - Interfaccia Granite](/help/sites-developing/touch-ui-concepts.md#coral-ui)
   * [Documentazione dell’interfaccia utente Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)

>[!NOTE]
>
>A causa della natura dei componenti dell’interfaccia utente Granite (e delle differenze con i widget ExtJS), esistono alcune differenze tra il modo in cui i componenti interagiscono con l’interfaccia touch e l’ [interfaccia classica](/help/sites-developing/developing-components-classic.md).

### Creazione di una nuova finestra di dialogo {#creating-a-new-dialog}

Finestre di dialogo per l’interfaccia touch:

* sono denominati `cq:dialog`.
* sono definiti come un nodo `nt:unstructured` con la proprietà `sling:resourceType` impostata.

* si trovano sotto il nodo `cq:Component` e accanto alla relativa definizione del componente.
* vengono sottoposti a rendering sul lato server (come componenti Sling), in base alla struttura del contenuto e alla proprietà `sling:resourceType` .
* utilizza il framework dell&#39;interfaccia utente Granite.
* contiene una struttura di nodo che descrive i campi all’interno della finestra di dialogo.

   * questi nodi sono `nt:unstructured` con la proprietà `sling:resourceType` richiesta.

Un esempio di struttura del nodo potrebbe essere:

```xml
newComponent (cq:Component)
  cq:dialog (nt:unstructured)
    content
      layout
      items
        column
          items
            file
            description
```

La personalizzazione di una finestra di dialogo è simile allo sviluppo di un componente, in quanto la finestra di dialogo stessa è un componente (ad esempio, il markup rappresentato da uno script di un componente insieme al comportamento/stile fornito da una libreria client).

Per esempi, consulta:

* `/libs/foundation/components/text/cq:dialog`
* `/libs/foundation/components/download/cq:dialog`

>[!NOTE]
>
>Se per un componente non è definita alcuna finestra di dialogo per l’interfaccia touch, la finestra di dialogo dell’interfaccia classica viene utilizzata come fallback all’interno di un livello di compatibilità. Per personalizzare tale finestra di dialogo, è necessario personalizzare la finestra di dialogo dell’interfaccia classica. Consulta [Componenti AEM per l&#39;interfaccia classica](/help/sites-developing/developing-components-classic.md).

### Personalizzazione dei campi della finestra di dialogo {#customizing-dialog-fields}

>[!NOTE]
>
>Consulta:
>
>* la sessione Gems AEM su [Personalizzazione dei campi di dialogo](https://docs.adobe.com/content/ddc/en/gems/customizing-dialog-fields-in-touch-ui.html).
>* il relativo codice di esempio trattato in [Esempio di codice - Come personalizzare i campi della finestra di dialogo](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields).

>



#### Creazione di un nuovo campo {#creating-a-new-field}

I widget per l’interfaccia touch sono implementati come componenti dell’interfaccia utente Granite.

Per creare un nuovo widget da utilizzare in una finestra di dialogo dei componenti per l’interfaccia utente touch, è necessario [creare un nuovo componente per campi Granite UI](/help/sites-developing/granite-ui-component.md).

>[!NOTE]
>
>Per informazioni dettagliate sull&#39;interfaccia utente Granite, consulta la [documentazione Granite UI](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html).

Se si considera la finestra di dialogo come un contenitore semplice per un elemento modulo, è anche possibile visualizzare il contenuto principale del contenuto della finestra di dialogo come campi modulo. La creazione di un nuovo campo modulo richiede la creazione di un tipo di risorsa; equivale a creare un nuovo componente. Per facilitare l’esecuzione di tale attività, l’interfaccia utente Granite offre un componente campo generico da cui ereditare (utilizzando `sling:resourceSuperType`):

`/libs/granite/ui/components/coral/foundation/form/field`

In modo più specifico, l’interfaccia utente Granite fornisce una serie di componenti per campi adatti alle finestre di dialogo (o, più in generale, nei [moduli](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/form/index.html)).

>[!NOTE]
>
>Questa funzione è diversa dall’interfaccia classica, in cui i widget sono rappresentati dai nodi `cq:Widgets`, ciascuno con un particolare `xtype` per stabilire la relazione con il relativo widget ExtJS. Dal punto di vista dell&#39;implementazione, questi widget sono stati resi sul lato client dal framework ExtJS.

Dopo aver creato il tipo di risorsa, puoi creare un’istanza del campo aggiungendo un nuovo nodo nella finestra di dialogo, con la proprietà `sling:resourceType` che fa riferimento al tipo di risorsa appena introdotto.

#### Creazione di una libreria client per stile e comportamento {#creating-a-client-library-for-style-and-behavior}

Se desideri definire stile e comportamento per il componente, puoi creare una [libreria client](/help/sites-developing/clientlibs.md) dedicata che definisce i tuoi CSS/LESS e JS personalizzati.

Per fare in modo che la libreria client venga caricata solo per la finestra di dialogo del componente (ovvero non verrà caricata per un altro componente), è necessario impostare la proprietà `extraClientlibs`** **della finestra di dialogo sul nome della categoria della libreria client appena creata. Questo è consigliabile se la libreria client è abbastanza grande e/o se il campo è specifico per tale finestra di dialogo e non sarà necessario in altre finestre di dialogo.

Per caricare la libreria client per tutte le finestre di dialogo, imposta la proprietà category della libreria client su `cq.authoring.dialog`. Questo è il nome della categoria della libreria client inclusa per impostazione predefinita durante il rendering di tutte le finestre di dialogo. Si desidera eseguire questa operazione se la libreria client è piccola e/o il campo è generico e può essere riutilizzato in altre finestre di dialogo.

Ad esempio, consulta:

* `cqgems/customizingfield/components/colorpicker/clientlibs`

   * fornito da [Esempio di codice](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

#### Estensione (ereditarietà da) un campo {#extending-inheriting-from-a-field}

A seconda delle tue esigenze, puoi:

* Estende un determinato campo dell’interfaccia Granite in base all’ereditarietà dei componenti ( `sling:resourceSuperType`)
* Estendi un determinato widget dalla libreria di widget sottostante (nel caso dell&#39;interfaccia utente Granite, questa è l&#39;interfaccia utente Coral), seguendo l&#39;API della libreria di widget (ereditarietà JS/CSS)

#### Accesso ai campi della finestra di dialogo {#access-to-dialog-fields}

È inoltre possibile utilizzare le condizioni di rendering ( `rendercondition`) per controllare chi ha accesso a schede/campi specifici nella finestra di dialogo; ad esempio:

```xml
+ mybutton
  - sling:resourceType = granite/ui/components/coral/foundation/button
  + rendercondition
    - sling:resourceType = myapp/components/renderconditions/group
    - groups = ["administrators"]
```

### Gestione degli eventi dei campi {#handling-field-events}

Il metodo di gestione degli eventi nei campi di dialogo ora viene eseguito con [listener in una libreria client personalizzata](#listeners-in-a-custom-client-library). Si tratta di una modifica rispetto al metodo precedente di avere [ascoltatori nella struttura del contenuto](#listenersinthecontentstructureclassicui).

#### Listener in una libreria client personalizzata {#listeners-in-a-custom-client-library}

Per inserire una logica nel campo, devi:

1. Indicare il campo contrassegnato con una determinata classe CSS (il *gancio*).
1. Definisci, nella libreria client, un listener JS collegato al nome della classe CSS (in questo modo la logica personalizzata viene delimitata solo nel campo e non influisce su altri campi dello stesso tipo).

Per ottenere questo risultato è necessario conoscere la libreria di widget sottostante con cui si desidera interagire. Consulta la [documentazione Coral UI](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/coral-ui/coralui3/index.html) per identificare l&#39;evento a cui desideri reagire. È molto simile al processo che si era dovuto eseguire con ExtJS in passato: trova la pagina della documentazione di un determinato widget, quindi controlla i dettagli della sua API evento.

Ad esempio, consulta:

* `cqgems/customizingfield/components/clientlibs/customizingfield`

   * fornito da [Esempio di codice](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

#### Ascoltatori nella struttura del contenuto {#listeners-in-the-content-structure}

Nell’interfaccia classica con ExtJS, nella struttura dei contenuti era solito avere ascoltatori per un determinato widget. Il raggiungimento dello stesso risultato nell’interfaccia touch è diverso perché il codice del listener JS (o qualsiasi altro codice) non è più definito nel contenuto.

la struttura del contenuto descrive la struttura semantica; non deve implicare la natura del widget sottostante. Non disponendo di codice JS nella struttura del contenuto, puoi modificare i dettagli di implementazione senza dover modificare la struttura del contenuto. In altre parole, puoi modificare la libreria dei widget senza dover toccare la struttura del contenuto.

#### Rilevamento della disponibilità della finestra di dialogo {#dialog-ready}

Se si dispone di un JavaScript personalizzato che deve essere eseguito solo quando la finestra di dialogo è disponibile e pronta, è necessario ascoltare l’evento `dialog-ready` .

Questo evento viene attivato ogni volta che la finestra di dialogo viene caricata (o ricaricata) ed è pronta per l’uso, il che significa che ogni volta che si verifica una modifica (creazione/aggiornamento) nel DOM della finestra di dialogo.

`dialog-ready` può essere utilizzato per agganciare nel codice personalizzato JavaScript che esegue personalizzazioni sui campi all’interno di una finestra di dialogo o attività simili.

### Convalida campo {#field-validation}

#### Campo obbligatorio {#mandatory-field}

Per contrassegnare un dato campo come obbligatorio, imposta la seguente proprietà sul nodo del contenuto del campo:

* Nome: `required`
* Tipo: `Boolean`

Ad esempio, consulta:

```xml
/libs/foundation/components/page/cq:dialog/content/items/tabs/items/basic/items/column/items/title/items/title
```

#### Convalida del campo (interfaccia Granite) {#field-validation-granite-ui}

La convalida dei campi nell’interfaccia Granite e nei componenti dell’interfaccia Granite (equivalenti ai widget) viene eseguita utilizzando l’API `foundation-validation` . [Per ulteriori informazioni, consulta la documentazione  `foundation-valdiation` Granite .](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/clientlibs/foundation/js/validation/index.html)

Per esempi, consulta:

* `cqgems/customizingfield/components/clientlibs/customizingfield/js/validations.js`

   * fornito da [Esempio di codice](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

* `/libs/cq/gui/components/authoring/dialog/clientlibs/dialog/js/validations.js`

## Creazione e configurazione di una finestra di dialogo di progettazione {#creating-and-configuring-a-design-dialog}

La finestra di dialogo Progettazione viene visualizzata quando un componente presenta dettagli di progettazione che possono essere modificati in [Modalità Progettazione](/help/sites-authoring/default-components-designmode.md).

La definizione è molto simile a quella di una finestra di dialogo [utilizzata per modificare il contenuto](#creating-a-new-dialog), con la differenza che è definita come nodo:

* Nome nodo: `cq:design_dialog`
* Tipo: `nt:unstructured`

## Creazione e configurazione di un editor interno {#creating-and-configuring-an-inplace-editor}

Un editor interno consente all’utente di modificare il contenuto direttamente nel flusso di paragrafi, senza la necessità di aprire una finestra di dialogo. Ad esempio, i componenti Testo e Titolo standard dispongono entrambi di un editor interno.

Un editor interno non è necessario/significativo per ogni tipo di componente.

Per ulteriori informazioni, consulta [Estensione dell’authoring delle pagine - Aggiungi nuovo editor interno](/help/sites-developing/customizing-page-authoring-touch.md#add-new-in-place-editor) .

## Personalizzazione della barra degli strumenti del componente {#customizing-the-component-toolbar}

La [Barra degli strumenti del componente](/help/sites-developing/touch-ui-structure.md#component-toolbar) consente all&#39;utente di accedere a una serie di azioni per il componente, come modificare, configurare, copiare ed eliminare.

Per ulteriori informazioni, consulta [Estensione dell’authoring delle pagine - Aggiungere una nuova azione a una barra degli strumenti di un componente](/help/sites-developing/customizing-page-authoring-touch.md#add-new-action-to-a-component-toolbar) .

## Configurazione di un componente per la barra laterale Riferimenti (prestato/prestato) {#configuring-a-component-for-the-references-rail-borrowed-lent}

Se il nuovo componente fa riferimento a contenuti di altre pagine, puoi considerare se debba avere un impatto sulle sezioni **Contenuto prestato** e **Contenuto prestato** della barra laterale [**Riferimenti**](/help/sites-authoring/basic-handling.md#references).

Il componente Riferimento AEM viene selezionato solo come componente predefinito. Per aggiungere il componente è necessario configurare il bundle OSGi **WCM Authoring Content Reference Configuration**.

Crea una nuova voce nella definizione, specificando il componente e la proprietà da controllare. Esempio:

`/apps/<*your-Project*>/components/reference@parentPath`

>[!NOTE]
>
>Quando si lavora con AEM esistono diversi metodi per gestire le impostazioni di configurazione per tali servizi. Per ulteriori informazioni e pratiche consigliate, consulta [Configurazione di OSGi](/help/sites-deploying/configuring-osgi.md) .

## Abilitazione e aggiunta del componente al sistema paragrafo {#enabling-and-adding-your-component-to-the-paragraph-system}

Una volta sviluppato, il componente deve essere abilitato per l’uso in un sistema paragrafo appropriato, in modo che possa essere utilizzato nelle pagine richieste.

Questo può essere fatto da:

* utilizzo della modalità [Progettazione](/help/sites-authoring/default-components-designmode.md) durante la modifica di una pagina specifica.
* [definizione della  `components` proprietà nel sistema paragrafo di un modello](/help/sites-developing/components-basics.md#adding-your-component-to-the-paragraph-system).

## La configurazione di un sistema di paragrafi in modo che il trascinamento di una risorsa crei un’istanza di componente {#configuring-a-paragraph-system-so-that-dragging-an-asset-creates-a-component-instance}

AEM offre la possibilità di configurare un sistema di paragrafi sulla pagina in modo che [un’istanza del nuovo componente venga creata automaticamente quando un utente trascina una risorsa (appropriata) in un’istanza della pagina](/help/sites-authoring/editing-content.md#insertingacomponenttouchoptimizedui) (anziché sempre trascinare un componente vuoto nella pagina).

Questo comportamento e la relazione risorsa-componente richiesta possono essere configurati:

1. Sotto la definizione di paragrafo della progettazione della pagina. Esempio:

   * `/etc/designs/<myApp>/page/par`

   Crea un nuovo nodo:

   * Nome: `cq:authoring`
   * Tipo: `nt:unstructured`


1. In questo crea un nuovo nodo per contenere tutte le mappature asset-to-component:

   * Nome: `assetToComponentMapping`
   * Tipo: `nt:unstructured`

1. Per ogni mappatura asset-to-component crea un nodo:

   * Nome: testo; si raccomanda che il nome indichi l’attività e il tipo di componente correlato; ad esempio, image
   * Tipo: `nt:unstructured`

   Ognuna con le seguenti proprietà:

   * `assetGroup`:

      * Tipo: `String`
      * Valore: il gruppo al quale appartiene l&#39;attività connessa; ad esempio, `media`
   * `assetMimetype`:

      * Tipo: `String`
      * Valore: il tipo MIME dell’attività correlata; ad esempio `image/*`
   * `droptarget`:

      * Tipo: `String`
      * Valore: l&#39;obiettivo di caduta; ad esempio, `image`
   * `resourceType`:

      * Tipo: `String`
      * Valore: la relativa risorsa componente; ad esempio, `foundation/components/image`
   * `type`:

      * Tipo: `String`
      * Valore: il tipo, ad esempio `Images`






Per esempi consulta:

* `/etc/designs/geometrixx/jcr:content/page/par/cq:authoring`
* `/etc/designs/geometrixx-outdoors/jcr:content/page/par/cq:authoring`
* `/etc/designs/geometrixx-media/jcr:content/article/article-content-par/cq:authoring`

CODICE SU GITHUB

Puoi trovare il codice di questa pagina su GitHub

* [Apri progetto aem-project-archetype su GitHub](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype)
* Scarica il progetto come [un file ZIP](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype/archive/master.zip)

>[!NOTE]
>
>La creazione automatica di istanze di componenti può ora essere configurata facilmente nell’interfaccia utente quando si utilizzano [Componenti core](https://docs.adobe.com/content/help/it/experience-manager-core-components/using/introduction.html) e modelli modificabili. Per ulteriori informazioni su come definire quali componenti sono associati automaticamente a determinati tipi di file multimediali, consulta [Creazione di modelli di pagina](/help/sites-authoring/templates.md#editing-a-template-structure-template-author) .

## Utilizzo dell&#39;estensione AEM Brackets {#using-the-aem-brackets-extension}

L’ [AEM Estensione parentesi graffe](/help/sites-developing/aem-brackets.md) fornisce un flusso di lavoro fluido per modificare AEM componenti e librerie client. Si basa sull’ editor di codice [Brackets](https://brackets.io/) .

Estensione:

* Semplifica la sincronizzazione (senza Maven o File Vault necessari) per aumentare l&#39;efficienza degli sviluppatori e aiuta gli sviluppatori front-end con limitata conoscenza AEM a partecipare ai progetti.
* Fornisce il supporto di [HTL](https://docs.adobe.com/content/help/en/experience-manager-htl/using/overview.html), il linguaggio del modello progettato per semplificare lo sviluppo dei componenti e aumentare la sicurezza.

>[!NOTE]
>
>Brackets è il meccanismo consigliato per la creazione di componenti. Sostituisce la funzionalità CRXDE Lite - Crea componente , progettata per l’interfaccia classica.

## Migrazione da un componente Classic {#migrating-from-a-classic-component}

Durante la migrazione di un componente progettato per l’uso con l’interfaccia classica a un componente che può essere utilizzato con l’interfaccia touch (solo o congiuntamente), è necessario tenere in considerazione i seguenti problemi:

* HTL

   * L&#39;utilizzo di [HTL](https://docs.adobe.com/content/help/en/experience-manager-htl/using/overview.html) non è obbligatorio, ma se il componente deve essere aggiornato, è il momento ideale per considerare la [migrazione da JSP a HTL](/help/sites-developing/components-basics.md#htl-vs-jsp).

* Componenti

   * Migra il codice [ `cq:listener`](/help/sites-developing/developing-components.md#migrating-cq-listener-code) che utilizza funzioni specifiche dell&#39;interfaccia classica
   * Il plug-in RTE, per ulteriori informazioni, consulta [Configurazione dell’editor Rich Text](/help/sites-administering/rich-text-editor.md).
   * [Migra  `cq:listener` ](#migrating-cq-listener-code) codice che utilizza funzioni specifiche dell’interfaccia classica

* Finestre di dialogo

   * Sarà necessario creare una nuova finestra di dialogo da utilizzare nell’interfaccia touch. Tuttavia, a fini di compatibilità, l’interfaccia touch può utilizzare la definizione di una finestra di dialogo dell’interfaccia classica, se non è stata definita alcuna finestra di dialogo per l’interfaccia touch.
   * Gli [AEM strumenti di modernizzazione](/help/sites-developing/modernization-tools.md) consentono di estendere i componenti esistenti.
   * [La mappatura di ExtJS su ](/help/sites-developing/touch-ui-concepts.md#extjs-and-corresponding-granite-ui-components) componenti dell’interfaccia Granite offre una panoramica pratica degli xtype e dei tipi di nodo ExtJS con i tipi di risorse equivalenti dell’interfaccia Granite.
   * Personalizzazione dei campi. Per ulteriori informazioni, consulta la sessione Gems AEM su [Personalizzazione dei campi di dialogo](https://docs.adobe.com/content/ddc/en/gems/customizing-dialog-fields-in-touch-ui.html).
   * Migrare da tipi a [Convalida dell&#39;interfaccia Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/clientlibs/foundation/js/validation/index.html)
   * Utilizzando gli ascoltatori JS, per ulteriori informazioni consulta [Gestione degli eventi dei campi](#handling-field-events) e la sessione Gems AEM su [Personalizzazione dei campi di dialogo](https://docs.adobe.com/content/ddc/en/gems/customizing-dialog-fields-in-touch-ui.html).

### Migrazione del codice cq:listener {#migrating-cq-listener-code}

Se stai eseguendo la migrazione di un progetto progettato per l’interfaccia classica, il codice `cq:listener` (e le clientlib relative ai componenti) potrebbe utilizzare funzioni specifiche dell’interfaccia classica (ad esempio `CQ.wcm.*`). Per la migrazione è necessario aggiornare tale codice utilizzando gli oggetti/le funzioni equivalenti nell’interfaccia touch.

Se il progetto viene migrato completamente nell’interfaccia touch, è necessario sostituire tale codice per utilizzare gli oggetti e le funzioni pertinenti all’interfaccia touch.

Tuttavia, se durante il periodo di migrazione il progetto deve essere compatibile sia con l’interfaccia classica che con quella touch (lo scenario più consueto), è necessario implementare uno switch per differenziare il codice separato che fa riferimento agli oggetti appropriati.

Questo meccanismo di commutazione può essere implementato come segue:

```
if (Granite.author) {
    // touch UI
} else {
    // classic UI
}
```

## Documentazione del componente {#documenting-your-component}

In qualità di sviluppatore, desideri accedere facilmente alla documentazione del componente per comprendere rapidamente:

* Descrizione
* Uso previsto
* Struttura e proprietà del contenuto
* API e punti di estensione esposti
* Ecc.

Per questo motivo, è abbastanza semplice rendere disponibile qualsiasi markdown della documentazione esistente all’interno del componente stesso.

È sufficiente inserire un file `README.md` nella struttura del componente. Questa Markdown verrà quindi visualizzata nella [console dei componenti](/help/sites-authoring/default-components-console.md).

![chlimage_1-7](assets/chlimage_1-7.png)

Il markdown supportato è lo stesso di quello per [frammenti di contenuto](/help/assets/content-fragments/content-fragments-markdown.md).
