---
title: Sviluppo di componenti AEM
seo-title: Sviluppo di componenti AEM
description: AEM componenti sono utilizzati per conservare, formattare ed eseguire il rendering del contenuto reso disponibile sulle pagine Web.
seo-description: AEM componenti sono utilizzati per conservare, formattare ed eseguire il rendering del contenuto reso disponibile sulle pagine Web.
uuid: 1f39daa6-7277-45a2-adcc-74b58c93b8e4
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 8cdb6db4-adaa-4eda-af7d-310a0b44b80b
docset: aem65
legacypath: /content/docs/en/aem/6-2/develop/components/components-touch-optimized
translation-type: tm+mt
source-git-commit: a430c4de89bde3b907d342106465d3b5a7c75cc8
workflow-type: tm+mt
source-wordcount: '3452'
ht-degree: 1%

---


# Sviluppo di componenti AEM{#developing-aem-components}

AEM componenti sono utilizzati per conservare, formattare ed eseguire il rendering del contenuto reso disponibile sulle pagine Web.

* In [pagine di authoring](/help/sites-authoring/default-components.md), i componenti consentono agli autori di modificare e configurare il contenuto.

   * Quando si crea un sito [Commerce](/help/sites-administering/ecommerce.md), i componenti possono, ad esempio, raccogliere ed eseguire il rendering delle informazioni dal catalogo.
Per ulteriori informazioni, vedere [Sviluppo di eCommerce](/help/sites-developing/ecommerce.md).

   * Quando si crea un sito [Communities](/help/communities/author-communities.md), i componenti possono fornire informazioni e raccogliere informazioni dai visitatori.
Per ulteriori informazioni, vedere [Sviluppo di community](/help/communities/communities.md).

* Nell’istanza di pubblicazione i componenti eseguono il rendering del contenuto, presentandolo come necessario ai visitatori del sito Web.

>[!NOTE]
>
>Questa pagina è una continuazione del documento [Componenti AEM - The Basics](/help/sites-developing/components-basics.md).

>[!CAUTION]
>
>I componenti sotto `/libs/cq/gui/components/authoring/dialog` sono utilizzabili solo nell’editor (finestre di dialogo dei componenti in Authoring). Se vengono utilizzati altrove (ad esempio in una finestra di dialogo della procedura guidata), potrebbero non funzionare come previsto.

## Esempi di codice {#code-samples}

Questa pagina contiene la documentazione di riferimento (o i collegamenti alla documentazione di riferimento) necessaria per sviluppare nuovi componenti per AEM. Per alcuni esempi pratici, vedere [Sviluppo di componenti AEM - Esempi di codice](/help/sites-developing/developing-components-samples.md).

## Struttura {#structure}

La struttura di base di un componente è riportata nella pagina [AEM Componenti - The Basics](/help/sites-developing/components-basics.md#structure). Questo documento copre sia l’interfaccia touch che quella classica. Anche se non è necessario utilizzare le impostazioni classiche nel nuovo componente, può essere utile conoscerle quando si eredita da componenti esistenti.

## Estensione di componenti e finestre di dialogo esistenti {#extending-existing-components-and-dialogs}

A seconda del componente che si desidera implementare, potrebbe essere possibile estendere o personalizzare un&#39;istanza esistente, anziché definire e sviluppare da zero l&#39;intera [struttura](#structure).

Durante l’estensione o la personalizzazione di un componente o di una finestra di dialogo esistente, potete copiare o replicare l’intera struttura o la struttura necessaria per la finestra di dialogo prima di apportare le modifiche.

### Estensione di un componente esistente {#extending-an-existing-component}

Per estendere un componente esistente è possibile utilizzare [Gerarchia dei tipi di risorse](/help/sites-developing/components-basics.md#component-hierarchy-and-inheritance) e i relativi meccanismi di ereditarietà.

>[!NOTE]
>
>I componenti possono essere ridefiniti con una sovrapposizione basata sulla logica del percorso di ricerca. In questo caso, tuttavia, la [fusione risorse Sling](/help/sites-developing/sling-resource-merger.md) non verrà attivata e `/apps` deve definire l&#39;intera sovrapposizione.

>[!NOTE]
>
>Anche il componente [frammento di contenuto](/help/sites-developing/customizing-content-fragments.md) può essere personalizzato ed esteso, anche se è necessario considerare la struttura e le relazioni complete con le risorse.

### Personalizzazione di una finestra di dialogo componente esistente {#customizing-a-existing-component-dialog}

È inoltre possibile ignorare una finestra di dialogo *componente* utilizzando la [Sling Resource Merger](/help/sites-developing/sling-resource-merger.md) e definendo la proprietà `sling:resourceSuperType`.

Ciò significa che è sufficiente ridefinire le differenze richieste, anziché ridefinire l&#39;intera finestra di dialogo (utilizzando `sling:resourceSuperType`). Metodo consigliato per l’estensione della finestra di dialogo di un componente

Per ulteriori informazioni, vedere [Sling Resource Merger](/help/sites-developing/sling-resource-merger.md).

## Definizione del codice {#defining-the-markup}

Il componente verrà rappresentato con [HTML](https://www.w3schools.com/htmL/html_intro.asp). Il componente deve definire l’HTML necessario per acquisire il contenuto richiesto e eseguirne il rendering come necessario, sia nell’ambiente di creazione che nell’ambiente di pubblicazione.

### Utilizzo del linguaggio HTML Template Language {#using-the-html-template-language}

Il [HTML Template Language (HTL)](https://docs.adobe.com/content/help/it-IT/experience-manager-htl/using/overview.html), introdotto con AEM 6.0, sostituisce JSP (JavaServer Pages) come sistema di modelli lato server preferito e consigliato per HTML. Per gli sviluppatori Web che hanno bisogno di creare siti Web aziendali affidabili, HTL contribuisce a migliorare la sicurezza e l’efficienza dello sviluppo.

>[!NOTE]
>
>Sebbene sia HTL che JSP possano essere utilizzati per lo sviluppo di componenti, in questa pagina verrà illustrato lo sviluppo con HTL, in quanto è il linguaggio di script consigliato per AEM.

## Sviluppo della logica dei contenuti {#developing-the-content-logic}

Questa logica facoltativa seleziona e/o calcola il contenuto di cui eseguire il rendering. Viene richiamato dalle espressioni HTL con il pattern Use-API appropriato.

Il meccanismo per separare la logica dall&#39;aspetto aiuta a chiarire ciò che viene richiesto per una determinata vista. Consente inoltre logiche diverse per diverse viste della stessa risorsa.

### Utilizzo di Java {#using-java}

[L&#39;API Use-API Java HTL consente a un file HTL di accedere ai metodi helper in una classe](https://helpx.adobe.com/experience-manager/htl/using/use-api-java.html) Java personalizzata. Questo consente di utilizzare il codice Java per implementare la logica di selezione e configurazione del contenuto del componente.

### Uso di JavaScript {#using-javascript}

[L&#39;API Use-API JavaScript HTL consente a un file HTL di accedere al codice helper scritto in JavaScript](https://helpx.adobe.com/experience-manager/htl/using/use-api-javascript.html). Questo consente di utilizzare il codice JavaScript per implementare la logica necessaria per selezionare e configurare il contenuto del componente.

### Utilizzo di librerie HTML lato client {#using-client-side-html-libraries}

I siti Web moderni si affidano in larga misura all&#39;elaborazione sul lato client basata su codice JavaScript e CSS complessi. L&#39;organizzazione e l&#39;ottimizzazione della gestione di questo codice può essere un problema complicato.

Per risolvere il problema, AEM fornisce **Cartelle libreria lato client** che consentono di memorizzare il codice lato client nell&#39;archivio, organizzarlo in categorie e definire quando e come ciascuna categoria di codice deve essere distribuita al client. Il sistema di libreria lato client si occupa quindi di generare i collegamenti corretti nella pagina Web finale per caricare il codice corretto.

Leggi [Utilizzo di librerie HTML lato client](/help/sites-developing/clientlibs.md) per ulteriori informazioni.

## Configurazione del comportamento di modifica {#configuring-the-edit-behavior}

È possibile configurare il comportamento di modifica di un componente con attributi quali le azioni disponibili per il componente, le caratteristiche dell’editor locale e i listener relativi agli eventi sul componente. La configurazione è comune sia all’interfaccia touch che all’interfaccia classica, anche se con alcune specifiche differenze.

Il comportamento di [modifica di un componente è configurato](/help/sites-developing/components-basics.md#edit-behavior) aggiungendo un nodo `cq:editConfig` di tipo `cq:EditConfig` sotto il nodo del componente (di tipo `cq:Component`) e aggiungendo proprietà e nodi secondari specifici.

## Configurazione del comportamento di anteprima {#configuring-the-preview-behavior}

Il cookie [WCM Mode](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/WCMMode.html) viene impostato quando si passa alla modalità **Anteprima** anche quando la pagina non viene aggiornata.

Per i componenti con un rendering sensibile alla modalità WCM, è necessario definirli per aggiornarsi in modo specifico, quindi basarsi sul valore del cookie.

>[!NOTE]
>
>Nell&#39;interfaccia touch sono utilizzati solo i valori `EDIT` e `PREVIEW` per il cookie [WCM Mode](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/WCMMode.html).

## Creazione e configurazione di una finestra di dialogo {#creating-and-configuring-a-dialog}

Le finestre di dialogo consentono all’autore di interagire con il componente. Utilizzando una finestra di dialogo gli autori e/o gli amministratori possono modificare il contenuto, configurare il componente o definire i parametri di progettazione (mediante una [finestra di dialogo Progettazione](#creating-and-configuring-a-design-dialog))

### Interfaccia utente Coral e interfaccia Granite {#coral-ui-and-granite-ui}

[L’](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/coral-ui/coralui3/index.html) interfaccia utente Coral  [e l’](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html) interfaccia utente Granite definiscono l’aspetto e il comportamento moderni delle AEM.

[L’interfaccia utente Granite offre una vasta gamma di componenti di base (widget) ](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html) necessari per creare una finestra di dialogo nell’ambiente di authoring. Se necessario, puoi estendere questa selezione e [creare un widget personalizzato](#creatinganewwidget).

Per ulteriori informazioni sullo sviluppo di componenti con tipi di risorse Corallo e Granite, vedi: [Creazione di componenti  Experience Manager utilizzando i tipi di risorse Corallo/Granite](https://helpx.adobe.com/experience-manager/using/aem64_coral_resourcetypes.html).

Per maggiori dettagli, consulta:

* Interfaccia utente Coral

   * Fornisce un&#39;interfaccia utente coerente in tutte le soluzioni cloud
   * [Concetti dell’interfaccia AEM touch - Interfaccia Coral](/help/sites-developing/touch-ui-concepts.md#coral-ui)
   * [Guida all’interfaccia utente Coral](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/coral-ui/coralui3/index.html)

* Interfaccia Granite

   * Fornisce il codice Coral UI racchiuso nei componenti Sling per la creazione di console e finestre di dialogo dell&#39;interfaccia utente
   * [Concetti dell’interfaccia AEM touch - Interfaccia Granite](/help/sites-developing/touch-ui-concepts.md#coral-ui)
   * [Documentazione di Granite UI](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)

>[!NOTE]
>
>A causa della natura dei componenti dell’interfaccia Granite (e delle differenze con i widget ExtJS), esistono delle differenze tra il modo in cui i componenti interagiscono con l’interfaccia touch e l’ [interfaccia classica](/help/sites-developing/developing-components-classic.md).

### Creazione di una nuova finestra di dialogo {#creating-a-new-dialog}

Finestre di dialogo per l’interfaccia touch:

* sono denominati `cq:dialog`.
* sono definiti come un nodo `nt:unstructured` con la proprietà `sling:resourceType` impostata.

* si trovano sotto il nodo `cq:Component` e accanto alla definizione del componente.
* viene eseguito il rendering sul lato server (come componenti Sling), in base alla struttura del contenuto e alla proprietà `sling:resourceType`.
* utilizzate il framework di interfaccia utente Granite.
* contiene una struttura di nodi che descrive i campi all’interno della finestra di dialogo.

   * questi nodi sono `nt:unstructured` con la proprietà `sling:resourceType` richiesta.

Esempio di struttura del nodo:

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

La personalizzazione di una finestra di dialogo è simile allo sviluppo di un componente, in quanto la finestra di dialogo è di per sé un componente (ad es. markup rappresentato da uno script di componente insieme al comportamento/stile fornito da una libreria client).

Per esempi, vedete:

* `/libs/foundation/components/text/cq:dialog`
* `/libs/foundation/components/download/cq:dialog`

>[!NOTE]
>
>Se per un componente non è definita alcuna finestra di dialogo per l’interfaccia touch, la finestra di dialogo dell’interfaccia classica viene utilizzata come fallback all’interno di un livello di compatibilità. Per personalizzare tale finestra di dialogo è necessario personalizzare la finestra di dialogo dell’interfaccia classica. Consultate [AEM Componenti per l&#39;interfaccia classica](/help/sites-developing/developing-components-classic.md).

### Personalizzazione dei campi di dialogo {#customizing-dialog-fields}

>[!NOTE]
>
>Consulta:
>
>* la sessione AEM Gems su [Personalizzazione dei campi di dialogo](https://docs.adobe.com/content/ddc/en/gems/customizing-dialog-fields-in-touch-ui.html).
>* il relativo codice di esempio riportato in [Esempio di codice - Come personalizzare i campi di dialogo](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields).

>



#### Creazione di un nuovo campo {#creating-a-new-field}

I widget per l’interfaccia touch sono implementati come componenti dell’interfaccia Granite.

Per creare un nuovo widget da usare in una finestra di dialogo di componenti per l’interfaccia touch, è necessario [creare un nuovo componente Campo interfaccia Granite](/help/sites-developing/granite-ui-component.md).

>[!NOTE]
>
>Per informazioni dettagliate sull&#39;interfaccia utente Granite, consultate la [documentazione Granite UI](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html).

Se si considera la finestra di dialogo come un semplice contenitore per un elemento modulo, è anche possibile visualizzare il contenuto principale del contenuto della finestra di dialogo come campi modulo. La creazione di un nuovo campo modulo richiede la creazione di un tipo di risorsa; equivale a creare un nuovo componente. Per facilitare l&#39;esecuzione di tale attività, l&#39;interfaccia utente Granite offre un componente campo generico da cui ereditare (utilizzando `sling:resourceSuperType`):

`/libs/granite/ui/components/coral/foundation/form/field`

Più precisamente, l&#39;interfaccia utente Granite offre una serie di componenti per i campi che possono essere utilizzati nelle finestre di dialogo (o, più in generale, nei [moduli](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/form/index.html)).

>[!NOTE]
>
>Ciò è diverso dall&#39;interfaccia classica, dove i widget sono rappresentati da `cq:Widgets` nodi, ciascuno con un `xtype` particolare per stabilire la relazione con il widget ExtJS corrispondente. Dal punto di vista dell’implementazione, questi widget sono stati sottoposti a rendering sul lato client dal framework ExtJS.

Dopo aver creato il tipo di risorsa, è possibile creare un&#39;istanza del campo aggiungendo un nuovo nodo nella finestra di dialogo, con la proprietà `sling:resourceType` che fa riferimento al tipo di risorsa appena introdotto.

#### Creazione di una libreria client per stile e comportamento {#creating-a-client-library-for-style-and-behavior}

Se desiderate definire lo stile e il comportamento del componente, potete creare una [libreria client](/help/sites-developing/clientlibs.md) dedicata che definisca CSS/LESS e JS personalizzati.

Per fare in modo che la libreria client venga caricata solo per la finestra di dialogo del componente (ovvero non verrà caricata per un altro componente), è necessario impostare la proprietà `extraClientlibs`** **della finestra di dialogo sul nome della categoria della libreria client appena creata. Questo è consigliabile se la libreria client è abbastanza grande e/o se il campo è specifico per tale finestra di dialogo e non sarà necessario in altre finestre di dialogo.

Per fare in modo che la libreria client venga caricata per tutte le finestre di dialogo, impostate la proprietà category della libreria client su `cq.authoring.dialog`. Questo è il nome della categoria della libreria client che è inclusa per impostazione predefinita quando si esegue il rendering di tutte le finestre di dialogo. Se la libreria client è piccola e/o il campo è generico e può essere riutilizzato in altre finestre di dialogo,

Ad esempio, vedete:

* `cqgems/customizingfield/components/colorpicker/clientlibs`

   * fornito da [Esempio di codice](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

#### Estensione (ereditarietà da) di un campo {#extending-inheriting-from-a-field}

A seconda delle esigenze, potete:

* Estende un determinato campo dell&#39;interfaccia Granite in base all&#39;ereditarietà del componente ( `sling:resourceSuperType`)
* Estendi un determinato widget dalla libreria di widget sottostante (nel caso dell’interfaccia utente Granite, si tratta dell’interfaccia utente Coral), seguendo l’API della libreria di widget (ereditarietà JS/CSS)

#### Accesso ai campi di dialogo {#access-to-dialog-fields}

Potete anche utilizzare le condizioni di rendering ( `rendercondition`) per controllare chi ha accesso a schede/campi specifici nella finestra di dialogo; ad esempio:

```xml
+ mybutton
  - sling:resourceType = granite/ui/components/coral/foundation/button
  + rendercondition
    - sling:resourceType = myapp/components/renderconditions/group
    - groups = ["administrators"]
```

### Gestione degli eventi dei campi {#handling-field-events}

Il metodo di gestione degli eventi nei campi di dialogo ora viene eseguito con [listener in una libreria client personalizzata](#listeners-in-a-custom-client-library). Si tratta di una modifica rispetto al metodo precedente, che consiste nell&#39;avere [listener nella struttura del contenuto](#listenersinthecontentstructureclassicui).

#### Listener in una libreria client personalizzata {#listeners-in-a-custom-client-library}

Per inserire la logica nel campo, è necessario:

1. Indicare che il campo deve essere contrassegnato con una determinata classe CSS (il *gancio*).
1. Definite, nella libreria client, un listener JS collegato al nome della classe CSS (in questo modo la logica personalizzata viene limitata all&#39;ambito del campo e non influisce sugli altri campi dello stesso tipo).

Per ottenere questo risultato è necessario conoscere la libreria di widget sottostante con cui si desidera interagire. Consultate la [documentazione Coral UI](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/coral-ui/coralui3/index.html) per identificare l&#39;evento a cui desiderate reagire. Questa procedura è molto simile a quella che era necessario eseguire con ExtJS in passato: trova la pagina della documentazione di un determinato widget, quindi controlla i dettagli della relativa API evento.

Ad esempio, vedete:

* `cqgems/customizingfield/components/clientlibs/customizingfield`

   * fornito da [Esempio di codice](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

#### Listener nella struttura del contenuto {#listeners-in-the-content-structure}

Nell’interfaccia classica con ExtJS, nella struttura del contenuto era solito inserire i listener per un determinato widget. La stessa procedura nell’interfaccia touch è diversa, in quanto il codice listener JS (o qualsiasi altro codice) non è più definito nel contenuto.

La struttura del contenuto descrive la struttura semantica; non deve implicare la natura del widget sottostante. Se il codice JS non è presente nella struttura del contenuto, potete modificare i dettagli di implementazione senza dover modificare la struttura del contenuto. In altre parole, potete modificare la libreria dei widget senza dover toccare la struttura del contenuto.

### Convalida del campo {#field-validation}

#### Campo obbligatorio {#mandatory-field}

Per contrassegnare un dato campo come obbligatorio, impostare la seguente proprietà sul nodo di contenuto del campo:

* Nome: `required`
* Tipo: `Boolean`

Ad esempio, vedete:

```xml
/libs/foundation/components/page/cq:dialog/content/items/tabs/items/basic/items/column/items/title/items/title
```

#### Convalida dei campi (interfaccia utente Granite) {#field-validation-granite-ui}

La convalida dei campi nell&#39;interfaccia utente Granite e nei componenti dell&#39;interfaccia utente Granite (equivalenti ai widget) viene eseguita utilizzando l&#39;API `foundation-validation`. [Per ulteriori informazioni, consulta la documentazione  `foundation-valdiation` Granite.](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/clientlibs/foundation/js/validation/index.html)

Per esempi, vedete:

* `cqgems/customizingfield/components/clientlibs/customizingfield/js/validations.js`

   * fornito da [Esempio di codice](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

* `/libs/cq/gui/components/authoring/dialog/clientlibs/dialog/js/validations.js`

## Creazione e configurazione di una finestra di dialogo Progettazione {#creating-and-configuring-a-design-dialog}

La finestra di dialogo Progettazione viene visualizzata quando un componente dispone di dettagli di progettazione che possono essere modificati in [Modalità progettazione](/help/sites-authoring/default-components-designmode.md).

La definizione è molto simile a quella di una finestra di dialogo [utilizzata per modificare i contenuti](#creating-a-new-dialog), con la differenza che è definita come nodo:

* Nome nodo: `cq:design_dialog`
* Tipo: `nt:unstructured`

## Creazione e configurazione di un editor interno {#creating-and-configuring-an-inplace-editor}

Un editor interno consente all&#39;utente di modificare il contenuto direttamente nel flusso di paragrafi, senza dover aprire una finestra di dialogo. Ad esempio, i componenti Testo standard e Titolo dispongono entrambi di un editor locale.

Un editor locale non è necessario/significativo per ogni tipo di componente.

Per ulteriori informazioni, consultate [Estensione dell&#39;authoring delle pagine - Aggiungi nuovo editor interno](/help/sites-developing/customizing-page-authoring-touch.md#add-new-in-place-editor).

## Personalizzazione della barra degli strumenti del componente {#customizing-the-component-toolbar}

La [barra degli strumenti del componente](/help/sites-developing/touch-ui-structure.md#component-toolbar) consente all&#39;utente di accedere a una serie di azioni per il componente, come modificare, configurare, copiare ed eliminare.

Per ulteriori informazioni, consultate [Estensione dell&#39;authoring delle pagine - Aggiungi nuova azione a una barra degli strumenti di un componente](/help/sites-developing/customizing-page-authoring-touch.md#add-new-action-to-a-component-toolbar).

## Configurazione di un componente per la barra laterale Riferimenti (in prestito/in prestito) {#configuring-a-component-for-the-references-rail-borrowed-lent}

Se il nuovo componente fa riferimento a contenuti provenienti da altre pagine, è possibile valutare se l&#39;effetto delle sezioni **Contenuto in prestito** e **Contenuto in prestito** della Barra [**Riferimenti**](/help/sites-authoring/basic-handling.md#references).

Il componente Riferimento viene AEM solo dal componente Predefinito. Per aggiungere il componente è necessario configurare il bundle OSGi **Configurazione di riferimento per l’authoring WCM**.

Create una nuova voce nella definizione, specificando il componente e la proprietà da controllare. Esempio:

`/apps/<*your-Project*>/components/reference@parentPath`

>[!NOTE]
>
>Quando lavorate con AEM esistono diversi metodi per gestire le impostazioni di configurazione per tali servizi. Per ulteriori informazioni e procedure consigliate, vedere [Configurazione di OSGi](/help/sites-deploying/configuring-osgi.md).

## Abilitazione e aggiunta del componente al sistema paragrafo {#enabling-and-adding-your-component-to-the-paragraph-system}

Dopo che il componente è stato sviluppato, deve essere abilitato per l’uso in un sistema paragrafo appropriato, in modo che possa essere utilizzato nelle pagine richieste.

A tale scopo:

* utilizzo della modalità [Progettazione](/help/sites-authoring/default-components-designmode.md) durante la modifica di una pagina specifica.
* [definizione della  `components` proprietà nel sistema paragrafo di un modello](/help/sites-developing/components-basics.md#adding-your-component-to-the-paragraph-system).

## Configurazione di un sistema paragrafo in modo che il trascinamento di una risorsa crei un&#39;istanza di componente {#configuring-a-paragraph-system-so-that-dragging-an-asset-creates-a-component-instance}

AEM offre la possibilità di configurare un sistema paragrafo sulla pagina in modo che [un&#39;istanza del nuovo componente venga creata automaticamente quando un utente trascina una risorsa (appropriata) su un&#39;istanza della pagina](/help/sites-authoring/editing-content.md#insertingacomponenttouchoptimizedui) (invece di dover sempre trascinare un componente vuoto sulla pagina).

Questo comportamento e la relazione tra risorse e componenti richiesta possono essere configurati:

1. Nella definizione di paragrafo della struttura della pagina. Esempio:

   * `/etc/designs/<myApp>/page/par`

   Crea un nuovo nodo:

   * Nome: `cq:authoring`
   * Tipo: `nt:unstructured`


1. In questa sezione, crea un nuovo nodo per contenere tutte le mappature asset-to-component:

   * Nome: `assetToComponentMapping`
   * Tipo: `nt:unstructured`

1. Per ogni mappatura risorsa-componente, crea un nodo:

   * Nome: text; si raccomanda che il nome indichi la risorsa e il tipo di componente correlato; ad esempio, image
   * Tipo: `nt:unstructured`

   Ciascuno con le seguenti proprietà:

   * `assetGroup`:

      * Tipo: `String`
      * Valore: il gruppo cui appartiene l’attività correlata; ad esempio, `media`
   * `assetMimetype`:

      * Tipo: `String`
      * Valore: il tipo mime dell’attività correlata; ad esempio `image/*`
   * `droptarget`:

      * Tipo: `String`
      * Valore: il bersaglio di caduta; ad esempio, `image`
   * `resourceType`:

      * Tipo: `String`
      * Valore: la risorsa componente correlata; ad esempio, `foundation/components/image`
   * `type`:

      * Tipo: `String`
      * Valore: il tipo, ad esempio `Images`






Per esempi, vedete:

* `/etc/designs/geometrixx/jcr:content/page/par/cq:authoring`
* `/etc/designs/geometrixx-outdoors/jcr:content/page/par/cq:authoring`
* `/etc/designs/geometrixx-media/jcr:content/article/article-content-par/cq:authoring`

CODICE SU GITHUB

Puoi trovare il codice di questa pagina su GitHub

* [Apri progetto aem-project-archetype su GitHub](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype)
* Scarica il progetto come [un file ZIP](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype/archive/master.zip)

>[!NOTE]
>
>La creazione automatica di istanze di componenti ora può essere configurata facilmente nell&#39;interfaccia utente quando si utilizzano [Componenti di base](https://docs.adobe.com/content/help/it-IT/experience-manager-core-components/using/introduction.html) e Modelli modificabili. Per ulteriori informazioni sulla definizione dei componenti automaticamente associati a determinati tipi di supporti, vedere [Creazione di modelli di pagina](/help/sites-authoring/templates.md#editing-a-template-structure-template-author).

## Utilizzo dell&#39;estensione AEM parentesi quadre {#using-the-aem-brackets-extension}

L&#39;estensione [AEM parentesi quadre](/help/sites-developing/aem-brackets.md) offre un flusso di lavoro fluido per la modifica AEM componenti e librerie client. Si basa sull&#39;editor di codice [Brackets](https://brackets.io/).

L&#39;estensione:

* Semplifica la sincronizzazione (non sono necessari Maven o File Vault) per migliorare l&#39;efficienza degli sviluppatori e aiuta gli sviluppatori front-end con AEM limitata conoscenza a partecipare ai progetti.
* Fornisce supporto [HTL](https://docs.adobe.com/content/help/en/experience-manager-htl/using/overview.html), il linguaggio di modello progettato per semplificare lo sviluppo dei componenti e aumentare la sicurezza.

>[!NOTE]
>
>Le parentesi sono il meccanismo consigliato per la creazione di componenti. Sostituisce la funzionalità CRXDE Lite - Crea componente, progettata per l’interfaccia classica.

## Migrazione da un componente classico {#migrating-from-a-classic-component}

Durante la migrazione di un componente progettato per l’uso con l’interfaccia classica a un componente che può essere utilizzato con l’interfaccia touch (solo o insieme), devono essere considerati i seguenti problemi:

* HTL

   * L&#39;utilizzo di [HTL](https://docs.adobe.com/content/help/en/experience-manager-htl/using/overview.html) non è obbligatorio, ma se il componente deve essere aggiornato è il momento ideale per prendere in considerazione la migrazione da JSP a HTL](/help/sites-developing/components-basics.md#htl-vs-jsp).[

* Componenti

   * Migrare il codice [ `cq:listener`](/help/sites-developing/developing-components.md#migrating-cq-listener-code) che utilizza funzioni specifiche dell&#39;interfaccia classica
   * Per ulteriori informazioni, vedere [Configurazione dell&#39;editor Rich Text](/help/sites-administering/rich-text-editor.md).
   * [Migra  `cq:listener` ](#migrating-cq-listener-code) codice che utilizza funzioni specifiche dell’interfaccia classica

* Finestre di dialogo

   * Sarà necessario creare una nuova finestra di dialogo da usare nell’interfaccia touch. Tuttavia, a fini di compatibilità, l’interfaccia touch può usare la definizione di una finestra di dialogo dell’interfaccia classica, se non è stata definita alcuna finestra di dialogo per l’interfaccia touch.
   * [Dialog Conversion Tool](/help/sites-developing/dialog-conversion.md) (Strumento di conversione finestra) consente di estendere i componenti esistenti.
   * [La mappatura di ExtJS su ](/help/sites-developing/touch-ui-concepts.md#extjs-and-corresponding-granite-ui-components) componenti dell&#39;interfaccia Granite fornisce una panoramica pratica degli xtype e dei tipi di nodi ExtJS con i tipi di risorse equivalenti dell&#39;interfaccia Granite.
   * Per ulteriori informazioni, consultate la sessione AEM Gems in [Customizing Dialog Fields](https://docs.adobe.com/content/ddc/en/gems/customizing-dialog-fields-in-touch-ui.html) (Personalizzazione dei campi di dialogo).
   * Migrazione da tipi a [Convalida dell&#39;interfaccia utente Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/clientlibs/foundation/js/validation/index.html)
   * Utilizzando i listener JS, per ulteriori informazioni vedere [Gestione degli eventi dei campi](#handling-field-events) e la sessione AEM Gems su [Personalizzazione dei campi di dialogo](https://docs.adobe.com/content/ddc/en/gems/customizing-dialog-fields-in-touch-ui.html).

### Migrazione del codice cq:listener {#migrating-cq-listener-code}

Se state eseguendo la migrazione di un progetto progettato per l&#39;interfaccia classica, il codice `cq:listener` (e i client correlati ai componenti) potrebbe utilizzare funzioni specifiche dell&#39;interfaccia classica (ad esempio `CQ.wcm.*`). Per la migrazione è necessario aggiornare tale codice utilizzando gli oggetti/le funzioni equivalenti nell’interfaccia touch.

Se il progetto viene migrato completamente nell’interfaccia touch, è necessario sostituire tale codice per utilizzare gli oggetti e le funzioni pertinenti all’interfaccia touch.

Tuttavia, se il progetto deve soddisfare sia l’interfaccia classica che l’interfaccia touch durante il periodo di migrazione (lo scenario più consueto), è necessario implementare uno switch per distinguere il codice separato che fa riferimento agli oggetti appropriati.

Questo meccanismo di commutazione può essere implementato come segue:

```
if (Granite.author) {
    // touch UI
} else {
    // classic UI
}
```

## Documentazione del componente {#documenting-your-component}

In qualità di sviluppatore, è necessario disporre di un accesso semplice alla documentazione del componente per comprendere rapidamente:

* Descrizione
* Uso previsto
* Struttura del contenuto e proprietà
* API e punti di estensione esposti
* Ecc.

Per questo motivo, è abbastanza semplice rendere disponibile qualsiasi marcatura della documentazione esistente all’interno del componente stesso.

È sufficiente inserire un file `README.md` nella struttura del componente. Questa sezione verrà visualizzata nella [console dei componenti](/help/sites-authoring/default-components-console.md).

![chlimage_1-7](assets/chlimage_1-7.png)

La riduzione supportata è la stessa di quella per [frammenti di contenuto](/help/assets/content-fragments/content-fragments-markdown.md).
