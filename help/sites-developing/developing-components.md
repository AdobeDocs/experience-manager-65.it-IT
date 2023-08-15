---
title: Sviluppo di componenti AEM
seo-title: Developing AEM Components
description: I componenti AEM vengono utilizzati per memorizzare, formattare ed eseguire il rendering dei contenuti resi disponibili sulle pagine web.
seo-description: AEM components are used to hold, format, and render the content made available on your webpages.
uuid: 1f39daa6-7277-45a2-adcc-74b58c93b8e4
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 8cdb6db4-adaa-4eda-af7d-310a0b44b80b
docset: aem65
legacypath: /content/docs/en/aem/6-2/develop/components/components-touch-optimized
exl-id: 573cdc36-e9c3-4803-9c4e-cebd0cf0a56f
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '3454'
ht-degree: 2%

---

# Sviluppo di componenti AEM{#developing-aem-components}

I componenti AEM vengono utilizzati per memorizzare, formattare ed eseguire il rendering dei contenuti resi disponibili sulle pagine web.

* Quando [authoring delle pagine](/help/sites-authoring/default-components.md), i componenti consentono agli autori di modificare e configurare il contenuto.

   * Durante la costruzione di un [Commerce](/help/commerce/cif-classic/administering/ecommerce.md) sito i componenti possono, ad esempio, raccogliere ed eseguire il rendering delle informazioni dal catalogo.
Consulta [Sviluppo dell’eCommerce](/help/commerce/cif-classic/developing/ecommerce.md) per ulteriori informazioni.

   * Durante la costruzione di un [Community](/help/communities/author-communities.md) sito i componenti possono fornire informazioni e raccogliere informazioni dai visitatori.
Consulta [Comunità in via di sviluppo](/help/communities/communities.md) per ulteriori informazioni.

* Nell’istanza di pubblicazione, i componenti eseguono il rendering del contenuto e lo presentano come necessario ai visitatori del sito web.

>[!NOTE]
>
>Questa pagina è una continuazione del documento [Componenti AEM - Nozioni di base](/help/sites-developing/components-basics.md).

>[!CAUTION]
>
>Componenti di seguito `/libs/cq/gui/components/authoring/dialog` devono essere utilizzati solo nell’editor (finestre di dialogo dei componenti in Authoring). Se vengono utilizzati altrove (ad esempio in una finestra di dialogo della procedura guidata), potrebbero non comportarsi come previsto.

## Esempi di codice {#code-samples}

Questa pagina fornisce la documentazione di riferimento (o collegamenti alla documentazione di riferimento) necessaria per sviluppare nuovi componenti per l’AEM. Consulta [Sviluppo di componenti AEM - Esempi di codice](/help/sites-developing/developing-components-samples.md) per alcuni esempi pratici.

## Struttura {#structure}

La struttura di base di un componente è illustrata nella pagina [Componenti AEM - Nozioni di base](/help/sites-developing/components-basics.md#structure). Questo documento descrive sia le interfacce utente touch che quelle classiche. Anche se non devi utilizzare le impostazioni classiche nel nuovo componente, può essere utile tenerne conto durante l’ereditarietà dai componenti esistenti.

## Estensione di finestre di dialogo e componenti esistenti {#extending-existing-components-and-dialogs}

A seconda del componente che desideri implementare, potrebbe essere possibile estendere o personalizzare un’istanza esistente, anziché definire e sviluppare l’intera [struttura](#structure) da zero.

Quando estendi o personalizzi un componente o una finestra di dialogo esistente, puoi copiare o replicare l’intera struttura o la struttura necessaria per la finestra di dialogo prima di apportare le modifiche.

### Estensione di un componente esistente {#extending-an-existing-component}

L’estensione di un componente esistente può essere ottenuta con [Gerarchia dei tipi di risorsa](/help/sites-developing/components-basics.md#component-hierarchy-and-inheritance) e i relativi meccanismi di ereditarietà.

>[!NOTE]
>
>I componenti possono anche essere ridefiniti con una sovrapposizione in base alla logica del percorso di ricerca. Tuttavia, in tal caso, [Sling Resource Merger](/help/sites-developing/sling-resource-merger.md) non viene attivato e `/apps` deve definire l’intera sovrapposizione.

>[!NOTE]
>
>Il [componente frammento di contenuto](/help/sites-developing/customizing-content-fragments.md) può anche essere personalizzata ed estesa, anche se occorre considerare l’intera struttura e le relazioni con Assets.

### Personalizzazione di una finestra di dialogo di componente esistente {#customizing-a-existing-component-dialog}

È inoltre possibile sovrascrivere un *finestra di dialogo del componente* utilizzando [Sling Resource Merger](/help/sites-developing/sling-resource-merger.md) e la definizione della proprietà `sling:resourceSuperType`.

Ciò significa che è sufficiente ridefinire le differenze richieste, anziché ridefinire l’intera finestra di dialogo (utilizzando `sling:resourceSuperType`). Questo è ora un metodo consigliato per estendere la finestra di dialogo di un componente

Consulta la [Sling Resource Merger](/help/sites-developing/sling-resource-merger.md) per ulteriori dettagli.

## Definizione del markup {#defining-the-markup}

Il rendering del componente verrà eseguito con [HTML](https://www.w3schools.com/htmL/html_intro.asp). Il componente deve definire le HTML necessarie per acquisire il contenuto richiesto e quindi eseguirne il rendering come richiesto, sia nell’ambiente di authoring che in quello di pubblicazione.

### Utilizzo di HTML Template Language {#using-the-html-template-language}

Il [HTL (HTML Template Language)](https://experienceleague.adobe.com/docs/experience-manager-htl/using/overview.html?lang=it), introdotto con AEM 6.0, sostituisce JSP (JavaServer Pages) come sistema di modelli lato server preferito e consigliato per HTML. Per gli sviluppatori web che devono creare solidi siti web aziendali, HTL consente di ottenere una maggiore sicurezza ed efficienza dello sviluppo.

>[!NOTE]
>
>Anche se sia HTL che JSP possono essere utilizzati per lo sviluppo di componenti, in questa pagina verrà illustrato lo sviluppo con HTL, in quanto è il linguaggio di script consigliato per l’AEM.

## Sviluppo della logica dei contenuti {#developing-the-content-logic}

Questa logica facoltativa seleziona e/o calcola il contenuto di cui eseguire il rendering. Viene richiamato da espressioni HTL con il pattern Use-API appropriato.

Il meccanismo per separare la logica dall&#39;aspetto aiuta a chiarire ciò che viene chiamato per una determinata vista. Consente inoltre una logica diversa per le diverse viste della stessa risorsa.

### Utilizzo di Java {#using-java}

[Java Use-API per HTL consente a un file HTL di accedere a metodi helper in una classe Java personalizzata](https://experienceleague.adobe.com/docs/experience-manager-htl/content/java-use-api.html?lang=en). Questo consente di utilizzare il codice Java per implementare la logica per selezionare e configurare il contenuto del componente.

### Utilizzo di JavaScript {#using-javascript}

[JavaScript Use-API per HTL consente a un file HTL di accedere a codice helper scritto in JavaScript](https://experienceleague.adobe.com/docs/experience-manager-htl/content/java-use-api.html?lang=en). Questo consente di utilizzare il codice JavaScript per implementare la logica per selezionare e configurare il contenuto del componente.

### Utilizzo delle librerie HTML lato client {#using-client-side-html-libraries}

I siti web moderni si basano fortemente sull’elaborazione lato client guidata da codice JavaScript e CSS complesso. L’organizzazione e l’ottimizzazione della trasmissione di questo codice possono essere un problema complesso.

Per risolvere questo problema, l’AEM fornisce **Cartelle libreria lato client**, che consente di memorizzare il codice lato client nell’archivio, organizzarlo in categorie e definire quando e come ogni categoria di codice deve essere trasmessa al client. Il sistema di librerie lato client si occupa quindi di generare i collegamenti corretti nella pagina web finale per caricare il codice corretto.

Letto [Utilizzo delle librerie HTML lato client](/help/sites-developing/clientlibs.md) per ulteriori informazioni.

## Configurazione del comportamento di modifica {#configuring-the-edit-behavior}

Puoi configurare il comportamento di modifica di un componente, inclusi gli attributi quali le azioni disponibili per il componente, le caratteristiche dell’editor locale e i listener relativi agli eventi sul componente. La configurazione è comune sia all’interfaccia touch che a quella classica, anche se con alcune differenze specifiche.

Il [il comportamento di modifica di un componente è configurato](/help/sites-developing/components-basics.md#edit-behavior) aggiungendo un `cq:editConfig` nodo di tipo `cq:EditConfig` sotto il nodo del componente (di tipo `cq:Component`) e aggiungendo proprietà e nodi secondari specifici.

## Configurazione del comportamento di anteprima {#configuring-the-preview-behavior}

Il [Modalità WCM](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/WCMMode.html) cookie viene impostato quando si passa a **Anteprima** anche quando la pagina non viene aggiornata.

Per i componenti con un rendering sensibili alla modalità WCM, è necessario definirli per aggiornarsi in modo specifico e quindi basarsi sul valore del cookie.

>[!NOTE]
>
>Nell’interfaccia touch, solo i valori `EDIT` e `PREVIEW` vengono utilizzati per [Modalità WCM](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/WCMMode.html) cookie.

## Creazione e configurazione di una finestra di dialogo {#creating-and-configuring-a-dialog}

Le finestre di dialogo vengono utilizzate per consentire all’autore di interagire con il componente. L’utilizzo di una finestra di dialogo consente agli autori e/o agli amministratori di modificare il contenuto, configurare il componente o definire i parametri di progettazione (utilizzando un’ [Finestra di dialogo per progettazione](#creating-and-configuring-a-design-dialog))

### Coral UI e Granite UI {#coral-ui-and-granite-ui}

[Coral UI](https://developer.adobe.com/experience-manager/reference-materials/6-5/coral-ui/coralui3/index.html) e [Interfaccia utente Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html) definire il look and feel moderno dell’AEM.

[L’interfaccia utente Granite offre una vasta gamma di componenti di base (widget)](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html) necessario per creare la finestra di dialogo nell’ambiente di authoring. Se necessario, puoi estendere questa selezione e [crea un widget personalizzato](#creatinganewwidget).

Per maggiori dettagli, consulta:

* Coral UI

   * Fornisce un’interfaccia utente coerente per tutte le soluzioni cloud
   * [Concetti dell’interfaccia touch dell’AEM - Coral UI](/help/sites-developing/touch-ui-concepts.md#coral-ui)
   * [Guida all’interfaccia utente Coral](https://developer.adobe.com/experience-manager/reference-materials/6-5/coral-ui/coralui3/index.html)

* Interfaccia utente Granite

   * Fornisce il markup dell’interfaccia utente Coral racchiuso nei componenti Sling per la creazione di console e finestre di dialogo dell’interfaccia utente
   * [Concetti dell’interfaccia touch dell’AEM - Interfaccia utente Granite](/help/sites-developing/touch-ui-concepts.md#coral-ui)
   * [Documentazione dell’interfaccia utente Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html)

>[!NOTE]
>
>A causa della natura dei componenti dell’interfaccia utente Granite (e delle differenze rispetto ai widget ExtJS), esistono alcune differenze tra il modo in cui i componenti interagiscono con l’interfaccia touch e il [interfaccia classica](/help/sites-developing/developing-components-classic.md).

### Creazione di una nuova finestra di dialogo {#creating-a-new-dialog}

Finestre di dialogo per l’interfaccia touch:

* sono denominati `cq:dialog`.
* sono definiti come `nt:unstructured` nodo con `sling:resourceType` proprietà impostata.

* si trovano sotto il loro `cq:Component` e accanto alla relativa definizione del componente.
* vengono sottoposti a rendering sul lato server (come componenti Sling), in base alla struttura del contenuto e al `sling:resourceType` proprietà.
* utilizza il framework dell’interfaccia utente Granite.
* contiene una struttura di nodi che descrive i campi all’interno della finestra di dialogo.

   * questi nodi sono `nt:unstructured` con il necessario `sling:resourceType` proprietà.

Un esempio di struttura dei nodi potrebbe essere:

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

La personalizzazione di una finestra di dialogo è simile allo sviluppo di un componente, in quanto la finestra di dialogo stessa è un componente (ovvero un markup rappresentato da uno script di componente insieme al comportamento/stile fornito da una libreria client).

Per esempi, consulta:

* `/libs/foundation/components/text/cq:dialog`
* `/libs/foundation/components/download/cq:dialog`

>[!NOTE]
>
>Se per un componente non è stata definita alcuna finestra di dialogo per l’interfaccia touch, come fallback viene utilizzata la finestra di dialogo dell’interfaccia classica all’interno di un livello di compatibilità. Per personalizzare tale finestra di dialogo è necessario personalizzare la finestra di dialogo dell’interfaccia classica. Consulta [Componenti AEM per l’interfaccia classica](/help/sites-developing/developing-components-classic.md).

### Personalizzazione dei campi della finestra di dialogo {#customizing-dialog-fields}

>[!NOTE]
>
>Consulta:
>
>* la sessione AEM Gems del [Personalizzazione dei campi della finestra di dialogo](https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2015/aem-customizing-dialog-fields-in-touch-ui.html?lang=en).
>* il relativo codice di esempio di cui [Esempio di codice: come personalizzare i campi della finestra di dialogo](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields).
>

#### Creazione di un nuovo campo {#creating-a-new-field}

I widget per l’interfaccia utente touch vengono implementati come componenti dell’interfaccia utente Granite.

Per creare un nuovo widget da utilizzare nella finestra di dialogo di un componente per l’interfaccia utente touch, è necessario: [creare un nuovo componente campo dell’interfaccia utente Granite](/help/sites-developing/granite-ui-component.md).

>[!NOTE]
>
>Per informazioni dettagliate sull’interfaccia utente di Granite, consulta la sezione [Documentazione dell’interfaccia utente Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html).

Se consideri la finestra di dialogo come un semplice contenitore per un elemento del modulo, puoi anche visualizzare il contenuto principale della finestra di dialogo come campi del modulo. La creazione di un nuovo campo modulo richiede la creazione di un tipo di risorsa, il che equivale alla creazione di un nuovo componente. Per facilitare questa attività, l’interfaccia utente Granite offre un componente campo generico da cui ereditare (utilizzando `sling:resourceSuperType`):

`/libs/granite/ui/components/coral/foundation/form/field`

Più precisamente, l’interfaccia utente Granite offre una serie di componenti di campo adatti all’utilizzo nelle finestre di dialogo (o, più in generale, in [moduli](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/form/index.html)).

>[!NOTE]
>
>Questo è diverso dall’interfaccia classica, dove i widget sono rappresentati da `cq:Widgets` nodi, ciascuno con un particolare `xtype` per stabilire la relazione con il widget ExtJS corrispondente. Dal punto di vista dell’implementazione, questi widget sono stati sottoposti a rendering sul lato client dal framework ExtJS.

Dopo aver creato il tipo di risorsa, puoi creare un’istanza del campo aggiungendo un nuovo nodo nella finestra di dialogo, con la proprietà `sling:resourceType` facendo riferimento al tipo di risorsa appena introdotto.

#### Creazione di una libreria client per stile e comportamento {#creating-a-client-library-for-style-and-behavior}

Se desideri definire lo stile e il comportamento del componente, puoi creare una [libreria client](/help/sites-developing/clientlibs.md) che definisce i file CSS/LESS e JS personalizzati.

Per caricare la libreria client solo per la finestra di dialogo del componente, ovvero non per un altro componente, è necessario impostare la proprietà `extraClientlibs`** **della finestra di dialogo al nome della categoria della libreria client appena creata. Questa opzione è consigliata se la libreria client è molto grande e/o il campo è specifico per tale finestra di dialogo e non sarà necessario in altre finestre di dialogo.

Per caricare la libreria client per tutte le finestre di dialogo, imposta la proprietà category della libreria client su `cq.authoring.dialog`. Questo è il nome della categoria della libreria client che viene inclusa per impostazione predefinita durante il rendering di tutte le finestre di dialogo. Puoi eseguire questa operazione se la libreria client è piccola e/o il campo è generico e potrebbe essere riutilizzato in altre finestre di dialogo.

Ad esempio, consulta:

* `cqgems/customizingfield/components/colorpicker/clientlibs`

   * fornite da [Esempio di codice](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

#### Estensione (ereditarietà) di un campo {#extending-inheriting-from-a-field}

A seconda delle tue esigenze, puoi effettuare le seguenti operazioni:

* Estendere un determinato campo dell’interfaccia utente Granite per ereditarietà di componenti ( `sling:resourceSuperType`)
* Estendere un determinato widget dalla libreria di widget sottostante (nel caso dell’interfaccia utente Granite, Coral UI), seguendo l’API della libreria di widget (ereditarietà JS/CSS)

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

Il metodo di gestione degli eventi sui campi della finestra di dialogo ora è fatto con [listener in una libreria client personalizzata](#listeners-in-a-custom-client-library). Si tratta di un cambiamento rispetto al metodo precedente di avere [listener nella struttura del contenuto](#listenersinthecontentstructureclassicui).

#### Listener in una libreria client personalizzata {#listeners-in-a-custom-client-library}

Per inserire la logica nel campo, è necessario:

1. Contrassegnare il campo con una determinata classe CSS (il *gancio*).
1. Definisci, nella libreria client un listener JS collegato al nome di classe CSS (in modo che la logica personalizzata abbia ambito solo sul tuo campo e non influisca su altri campi dello stesso tipo).

A questo scopo, è necessario conoscere la libreria di widget sottostante con cui desideri interagire. Consulta la [Documentazione dell’interfaccia utente Coral](https://developer.adobe.com/experience-manager/reference-materials/6-5/coral-ui/coralui3/index.html) per identificare a quale evento desideri reagire. Questo processo è molto simile a quello che dovevi eseguire con ExtJS in passato: trova la pagina della documentazione di un dato widget, quindi controlla i dettagli dell&#39;API dell&#39;evento.

Ad esempio, consulta:

* `cqgems/customizingfield/components/clientlibs/customizingfield`

   * fornite da [Esempio di codice](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

#### Listener nella struttura del contenuto {#listeners-in-the-content-structure}

Nell’interfaccia classica con ExtJS, solitamente i listener per un determinato widget erano inclusi nella struttura del contenuto. Ottenere lo stesso risultato nell’interfaccia touch è diverso in quanto il codice del listener JS (o qualsiasi codice) non è più definito nel contenuto.

La struttura del contenuto descrive la struttura semantica; non dovrebbe (deve) implicare la natura del widget sottostante. Se nella struttura del contenuto non è presente codice JS, puoi modificare i dettagli di implementazione senza dover modificare la struttura del contenuto. In altre parole, è possibile modificare la libreria dei widget senza dover toccare la struttura del contenuto.

#### Rilevamento della disponibilità della finestra di dialogo {#dialog-ready}

Se disponi di un JavaScript personalizzato che deve essere eseguito solo quando la finestra di dialogo è disponibile e pronta, è necessario ascoltare `dialog-ready` evento.

Questo evento viene attivato ogni volta che la finestra di dialogo viene caricata (o ricaricata) ed è pronta per l’uso, ovvero ogni volta che si verifica una modifica (creazione/aggiornamento) nel DOM della finestra di dialogo.

`dialog-ready` può essere utilizzato per hook nel codice personalizzato JavaScript che esegue personalizzazioni sui campi all’interno di una finestra di dialogo o attività simili.

### Convalida campo {#field-validation}

#### Campo obbligatorio {#mandatory-field}

Per contrassegnare un determinato campo come obbligatorio, imposta la seguente proprietà sul nodo di contenuto del campo:

* Nome: `required`
* Tipo: `Boolean`

Ad esempio, consulta:

```xml
/libs/foundation/components/page/cq:dialog/content/items/tabs/items/basic/items/column/items/title/items/title
```

#### Convalida del campo (interfaccia utente Granite) {#field-validation-granite-ui}

La convalida dei campi nell’interfaccia utente Granite e nei relativi componenti (equivalenti ai widget) viene eseguita utilizzando `foundation-validation` API. [Consulta la `foundation-valdiation` Documentazione di Granite per i dettagli.](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/clientlibs/foundation/js/validation/index.html)

Per esempi, consulta:

* `cqgems/customizingfield/components/clientlibs/customizingfield/js/validations.js`

   * fornite da [Esempio di codice](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

* `/libs/cq/gui/components/authoring/dialog/clientlibs/dialog/js/validations.js`

## Creazione e configurazione di una finestra di dialogo per progettazione {#creating-and-configuring-a-design-dialog}

La finestra di dialogo per progettazione viene visualizzata quando un componente presenta dettagli di progettazione che è possibile modificare in [Modalità Progettazione](/help/sites-authoring/default-components-designmode.md).

La definizione è molto simile a quella di [finestra di dialogo utilizzata per la modifica del contenuto](#creating-a-new-dialog), con la differenza che è definito come nodo:

* Nome nodo: `cq:design_dialog`
* Tipo: `nt:unstructured`

## Creazione e configurazione di un Inplace Editor {#creating-and-configuring-an-inplace-editor}

Un editor locale consente all’utente di modificare il contenuto direttamente nel flusso di paragrafo, senza dover aprire una finestra di dialogo. Ad esempio, i componenti standard Testo e Titolo dispongono entrambi di un editor locale.

Un editor locale non è necessario/significativo per ogni tipo di componente.

Consulta [Estensione dell’authoring delle pagine - Aggiunta di un nuovo editor locale](/help/sites-developing/customizing-page-authoring-touch.md#add-new-in-place-editor) per ulteriori informazioni.

## Personalizzazione della barra degli strumenti del componente {#customizing-the-component-toolbar}

Il [Barra degli strumenti del componente](/help/sites-developing/touch-ui-structure.md#component-toolbar) consente all’utente di accedere a una serie di azioni per il componente, ad esempio modifica, configura, copia ed elimina.

Consulta [Estensione dell’authoring delle pagine - Aggiunta di una nuova azione alla barra degli strumenti di un componente](/help/sites-developing/customizing-page-authoring-touch.md#add-new-action-to-a-component-toolbar) per ulteriori informazioni.

## Configurazione di un componente per la barra dei riferimenti (in prestito/preso in prestito) {#configuring-a-component-for-the-references-rail-borrowed-lent}

Se il nuovo componente fa riferimento al contenuto di altre pagine, puoi valutare se influire sul **Contenuto in prestito** e **Contenuto prestato** sezioni del [**Riferimenti**](/help/sites-authoring/basic-handling.md#references) Ferrovia.

L’AEM preconfigurato controlla solo il componente Reference. Per aggiungere il componente è necessario configurare il bundle OSGi **Configurazione di riferimento per l’authoring dei contenuti WCM**.

Crea una nuova voce nella definizione, specificando il componente, insieme alla proprietà da controllare. Ad esempio:

`/apps/<*your-Project*>/components/reference@parentPath`

>[!NOTE]
>
>Quando si lavora con AEM, sono disponibili diversi metodi di gestione delle impostazioni di configurazione per tali servizi. Per ulteriori dettagli e procedure consigliate, consulta [Configurazione di OSGi](/help/sites-deploying/configuring-osgi.md).

## Abilitazione e aggiunta del componente al sistema dei paragrafi {#enabling-and-adding-your-component-to-the-paragraph-system}

Una volta sviluppato, il componente deve essere abilitato per l’utilizzo in un sistema paragrafo appropriato, in modo da poter essere utilizzato nelle pagine richieste.

Questa operazione può essere eseguita da:

* utilizzo [Modalità progettazione](/help/sites-authoring/default-components-designmode.md) durante la modifica di una pagina specifica.
* [definizione di `components` proprietà nel sistema paragrafo di un modello](/help/sites-developing/components-basics.md#adding-your-component-to-the-paragraph-system).

## Configurazione di un sistema di paragrafi in modo che il trascinamento di una risorsa crei un’istanza di componente {#configuring-a-paragraph-system-so-that-dragging-an-asset-creates-a-component-instance}

L’AEM offre la possibilità di configurare un sistema paragrafo sulla pagina in modo che [un’istanza del nuovo componente viene creata automaticamente quando un utente trascina una risorsa (appropriata) su un’istanza della pagina](/help/sites-authoring/editing-content.md#insertingacomponenttouchoptimizedui) (invece di dover sempre trascinare un componente vuoto nella pagina).

È possibile configurare questo comportamento e la relazione risorsa-componente richiesta:

1. Nella definizione del paragrafo della progettazione della pagina. Ad esempio:

   * `/etc/designs/<myApp>/page/par`

   Crea un nuovo nodo:

   * Nome: `cq:authoring`
   * Tipo: `nt:unstructured`

1. Crea un nuovo nodo che contenga tutti i mapping risorsa-componente:

   * Nome: `assetToComponentMapping`
   * Tipo: `nt:unstructured`

1. Per ogni mappatura da risorsa a componente, crea un nodo:

   * Nome: testo; si consiglia che il nome indichi la risorsa e il tipo di componente correlato, ad esempio immagine
   * Tipo: `nt:unstructured`

   Ognuno con le seguenti proprietà:

   * `assetGroup`:

      * Tipo: `String`
      * Valore: il gruppo a cui appartiene l’attività correlata; per esempio, `media`

   * `assetMimetype`:

      * Tipo: `String`
      * Valore: il tipo MIME della relativa risorsa, ad esempio `image/*`

   * `droptarget`:

      * Tipo: `String`
      * Valore: il target di rilascio; ad esempio, `image`

   * `resourceType`:

      * Tipo: `String`
      * Valore: la risorsa del componente correlato, ad esempio `foundation/components/image`

   * `type`:

      * Tipo: `String`
      * Valore: il tipo, ad esempio `Images`

Per esempi, consulta:

* `/etc/designs/geometrixx/jcr:content/page/par/cq:authoring`
* `/etc/designs/geometrixx-outdoors/jcr:content/page/par/cq:authoring`
* `/etc/designs/geometrixx-media/jcr:content/article/article-content-par/cq:authoring`

CODICE SU GITHUB

Puoi trovare il codice di questa pagina su GitHub

* [Apri progetto aem-project-archetype su GitHub](https://github.com/adobe/aem-project-archetype)
* Scarica il progetto come [un file ZIP](https://github.com/adobe/aem-project-archetype/archive/master.zip)

>[!NOTE]
>
>La creazione automatica delle istanze dei componenti ora può essere configurata facilmente nell’interfaccia utente quando si utilizza [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it) e modelli modificabili. Consulta [Creazione di modelli di pagina](/help/sites-authoring/templates.md#editing-a-template-structure-template-author) per ulteriori informazioni sulla definizione dei componenti associati automaticamente a determinati tipi di file multimediali.

## Utilizzo dell’estensione per Brackets dell’AEM {#using-the-aem-brackets-extension}

Il [Estensione parentesi AEM](/help/sites-developing/aem-brackets.md) fornisce un flusso di lavoro fluido per modificare i componenti AEM e le librerie client. Si basa sulla [Parentesi](https://brackets.io/) editor di codice.

L’estensione:

* Semplifica la sincronizzazione (non è richiesto Maven o File Vault) per aumentare l’efficienza degli sviluppatori e aiuta gli sviluppatori front-end con conoscenze AEM limitate a partecipare ai progetti.
* Fornisce alcuni [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/using/overview.html?lang=it) supporto, linguaggio di modelli progettato per semplificare lo sviluppo di componenti e aumentare la sicurezza.

>[!NOTE]
>
>Brackets è il meccanismo consigliato per la creazione di componenti. Sostituisce la funzionalità CRXDE Liti - Crea componente, progettata per l’interfaccia classica.

## Migrazione da un componente classico {#migrating-from-a-classic-component}

Quando si migra un componente progettato per essere utilizzato con l’interfaccia classica a un componente che può essere utilizzato con l’interfaccia touch (singolarmente o congiuntamente), è necessario considerare i seguenti problemi:

* HTL

   * Uso di [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/using/overview.html?lang=it) non è obbligatorio, ma se il componente deve essere aggiornato, è il momento ideale per prendere in considerazione [migrazione da JSP a HTL](/help/sites-developing/components-basics.md#htl-vs-jsp).

* Componenti

   * Migra [`cq:listener`](/help/sites-developing/developing-components.md#migrating-cq-listener-code) codice che utilizza funzioni classiche specifiche per l’interfaccia utente
   * Plug-in dell’editor Rich Text; per ulteriori informazioni consulta [Configurazione dell’editor Rich Text](/help/sites-administering/rich-text-editor.md).
   * [Migra `cq:listener` codice](#migrating-cq-listener-code) che utilizza funzioni specifiche dell’interfaccia classica

* Finestre di dialogo

   * Crea una finestra di dialogo da utilizzare nell’interfaccia touch. Tuttavia, a scopo di compatibilità, l’interfaccia touch può utilizzare la definizione di finestra di dialogo dell’interfaccia classica, se non è stata definita alcuna finestra di dialogo per tale interfaccia.
   * Il [Strumenti di modernizzazione AEM](/help/sites-developing/modernization-tools.md) vengono fornite per facilitare l’estensione dei componenti esistenti.
   * [Mappatura di ExtJS ai componenti dell’interfaccia utente Granite](/help/sites-developing/touch-ui-concepts.md#extjs-and-corresponding-granite-ui-components) fornisce una pratica panoramica degli xtype e dei tipi di nodo ExtJS con i corrispondenti tipi di risorse dell’interfaccia utente Granite.
   * Personalizzazione dei campi; per ulteriori informazioni consulta la sessione AEM Gems su [Personalizzazione dei campi della finestra di dialogo](https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2015/aem-customizing-dialog-fields-in-touch-ui.html?lang=en).
   * Migra da tipi a [Convalida dell’interfaccia utente Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/clientlibs/foundation/js/validation/index.html)
   * Utilizzando i listener JS, per ulteriori informazioni consulta [Gestione degli eventi dei campi](#handling-field-events) e la sessione Gems dell’AEM [Personalizzazione dei campi della finestra di dialogo](https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2015/aem-customizing-dialog-fields-in-touch-ui.html?lang=en).

### Migrazione di cq:codice listener {#migrating-cq-listener-code}

Se stai eseguendo la migrazione di un progetto progettato per l’interfaccia utente classica, il `cq:listener` (e clientlibs relative ai componenti) potrebbero utilizzare funzioni specifiche dell’interfaccia classica (ad esempio `CQ.wcm.*`). Per la migrazione è necessario aggiornare tale codice utilizzando gli oggetti/le funzioni equivalenti nell’interfaccia utente touch.

Se il progetto viene completamente migrato all’interfaccia touch, devi sostituire tale codice per utilizzare gli oggetti e le funzioni rilevanti per tale interfaccia.

Tuttavia, se il progetto deve soddisfare sia l’interfaccia utente classica che quella touch durante il periodo di migrazione (lo scenario usuale), devi implementare un’opzione per differenziare il codice separato che fa riferimento agli oggetti appropriati.

Questo meccanismo di cambio può essere implementato come:

```
if (Granite.author) {
    // touch UI
} else {
    // classic UI
}
```

## Documentazione del componente {#documenting-your-component}

In qualità di sviluppatore, desideri poter accedere facilmente alla documentazione dei componenti per comprendere rapidamente:

* Descrizione
* Uso previsto
* Struttura e proprietà del contenuto
* API e punti di estensione esposti
* E così via

Per questo motivo, è facile creare qualsiasi markdown della documentazione esistente disponibile all’interno del componente stesso.

Inserisci un `README.md` nella struttura dei componenti. Questo markdown viene visualizzato nel [console dei componenti](/help/sites-authoring/default-components-console.md).

![chlimage_1-7](assets/chlimage_1-7.png)

Il markdown supportato è lo stesso di [frammenti di contenuto](/help/assets/content-fragments/content-fragments-markdown.md).
