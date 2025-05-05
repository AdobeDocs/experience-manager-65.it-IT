---
title: Sviluppo di componenti AEM
description: I componenti AEM vengono utilizzati per memorizzare, formattare ed eseguire il rendering dei contenuti resi disponibili sulle pagine web.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
docset: aem65
legacypath: /content/docs/en/aem/6-2/develop/components/components-touch-optimized
exl-id: 573cdc36-e9c3-4803-9c4e-cebd0cf0a56f
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '3246'
ht-degree: 0%

---

# Sviluppo di componenti AEM{#developing-aem-components}

I componenti AEM vengono utilizzati per memorizzare, formattare ed eseguire il rendering dei contenuti resi disponibili sulle pagine web.

* Durante l&#39;authoring di [pagine](/help/sites-authoring/default-components.md), i componenti consentono agli autori di modificare e configurare il contenuto.

   * Durante la costruzione di un sito [Commerce](/help/commerce/cif-classic/administering/ecommerce.md) i componenti possono, ad esempio, raccogliere ed eseguire il rendering delle informazioni dal catalogo.
Per ulteriori informazioni, vedere [Sviluppo di eCommerce](/help/commerce/cif-classic/developing/ecommerce.md).

   * Durante la costruzione di un sito [Communities](/help/communities/author-communities.md), i componenti possono fornire informazioni ai visitatori e raccoglierle.
Per ulteriori informazioni, vedere [Sviluppo di community](/help/communities/communities.md).

* Nell’istanza di pubblicazione, i componenti eseguono il rendering del contenuto e lo presentano come necessario ai visitatori del sito web.

>[!NOTE]
>
>Questa pagina è una continuazione del documento [Componenti AEM - Nozioni di base](/help/sites-developing/components-basics.md).

>[!CAUTION]
>
>I componenti sotto `/libs/cq/gui/components/authoring/dialog` devono essere utilizzati solo nell&#39;editor (finestre di dialogo dei componenti in Authoring). Se vengono utilizzati altrove (ad esempio in una finestra di dialogo della procedura guidata), potrebbero non comportarsi come previsto.

## Esempi di codice {#code-samples}

Questa pagina fornisce la documentazione di riferimento (o collegamenti alla documentazione di riferimento) necessaria per sviluppare nuovi componenti per l’AEM. Per alcuni esempi pratici, consulta [Sviluppo di componenti AEM: esempi di codice](/help/sites-developing/developing-components-samples.md).

## Struttura {#structure}

La struttura di base di un componente è illustrata nella pagina [Componenti AEM - Nozioni di base](/help/sites-developing/components-basics.md#structure). Questo documento descrive sia le interfacce utente touch che quelle classiche. Anche se non devi utilizzare le impostazioni classiche nel nuovo componente, può essere utile tenerne conto durante l’ereditarietà dai componenti esistenti.

## Estensione di finestre di dialogo e componenti esistenti {#extending-existing-components-and-dialogs}

A seconda del componente che si desidera implementare, è possibile estendere o personalizzare un&#39;istanza esistente anziché definire e sviluppare l&#39;intera [struttura](#structure) da zero.

Quando estendi o personalizzi un componente o una finestra di dialogo esistente, puoi copiare o replicare l’intera struttura o la struttura necessaria per la finestra di dialogo prima di apportare le modifiche.

### Estensione di un componente esistente {#extending-an-existing-component}

L&#39;estensione di un componente esistente può essere ottenuta con [Resource Type Hierarchy](/help/sites-developing/components-basics.md#component-hierarchy-and-inheritance) e i relativi meccanismi di ereditarietà.

>[!NOTE]
>
>I componenti possono anche essere ridefiniti con una sovrapposizione in base alla logica del percorso di ricerca. Tuttavia, in questo caso, [Sling Resource Merger](/help/sites-developing/sling-resource-merger.md) non viene attivato e `/apps` deve definire l&#39;intera sovrapposizione.

>[!NOTE]
>
>Anche il componente [frammento di contenuto](/help/sites-developing/customizing-content-fragments.md) può essere personalizzato ed esteso, anche se è necessario considerare l&#39;intera struttura e le relazioni con Assets.

### Personalizzazione di una finestra di dialogo di componente esistente {#customizing-a-existing-component-dialog}

È inoltre possibile ignorare una *finestra di dialogo del componente* utilizzando [Sling Resource Merger](/help/sites-developing/sling-resource-merger.md) e definendo la proprietà `sling:resourceSuperType`.

Ciò significa che è sufficiente ridefinire le differenze richieste, anziché ridefinire l&#39;intera finestra di dialogo (utilizzando `sling:resourceSuperType`). Questo è ora un metodo consigliato per estendere la finestra di dialogo di un componente

Per ulteriori dettagli, vedi [Sling Resource Merger](/help/sites-developing/sling-resource-merger.md).

## Definizione del markup {#defining-the-markup}

Il rendering del componente verrà eseguito con [HTML](https://www.w3schools.com/htmL/html_intro.asp). Il componente deve definire le HTML necessarie per acquisire il contenuto richiesto e quindi eseguirne il rendering come richiesto, sia nell’ambiente di authoring che in quello di pubblicazione.

### Utilizzo di HTML Template Language {#using-the-html-template-language}

[HTML Template Language (HTL)](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html?lang=it), introdotto con AEM 6.0, sostituisce JSP (JavaServer Pages) come sistema di modelli lato server preferito e consigliato per HTML. Per gli sviluppatori web che devono creare solidi siti web aziendali, HTL consente di ottenere una maggiore sicurezza ed efficienza dello sviluppo.

>[!NOTE]
>
>Anche se sia HTL che JSP possono essere utilizzati per lo sviluppo di componenti, in questa pagina verrà illustrato lo sviluppo con HTL, in quanto è il linguaggio di script consigliato per l’AEM.

## Sviluppo della logica dei contenuti {#developing-the-content-logic}

Questa logica facoltativa seleziona e/o calcola il contenuto di cui eseguire il rendering. Viene richiamato da espressioni HTL con il pattern Use-API appropriato.

Il meccanismo per separare la logica dall&#39;aspetto aiuta a chiarire ciò che viene chiamato per una determinata vista. Consente inoltre una logica diversa per le diverse viste della stessa risorsa.

### Utilizzo di Java {#using-java}

[Java Use-API per HTL consente a un file HTL di accedere a metodi helper in una classe Java personalizzata](https://experienceleague.adobe.com/docs/experience-manager-htl/content/java-use-api.html?lang=it). Questo consente di utilizzare il codice Java per implementare la logica per selezionare e configurare il contenuto del componente.

### Utilizzo di JavaScript {#using-javascript}

[HTL JavaScript Use-API consente a un file HTL di accedere a codice helper scritto in JavaScript](https://experienceleague.adobe.com/docs/experience-manager-htl/content/java-use-api.html?lang=it). Questo consente di utilizzare il codice JavaScript per implementare la logica per la selezione e la configurazione del contenuto del componente.

### Utilizzo delle librerie HTML lato client {#using-client-side-html-libraries}

I siti web moderni si basano in larga misura sull’elaborazione lato client guidata da codice JavaScript e CSS complesso. L’organizzazione e l’ottimizzazione della trasmissione di questo codice possono essere un problema complesso.

Per risolvere questo problema, AEM fornisce **Cartelle libreria lato client**, che consente di memorizzare il codice lato client nell&#39;archivio, organizzarlo in categorie e definire quando e come ogni categoria di codice deve essere servita al client. Il sistema di librerie lato client si occupa quindi di generare i collegamenti corretti nella pagina web finale per caricare il codice corretto.

Per ulteriori informazioni, leggere [Utilizzo delle librerie HTML lato client](/help/sites-developing/clientlibs.md).

## Configurazione del comportamento di modifica {#configuring-the-edit-behavior}

Puoi configurare il comportamento di modifica di un componente, inclusi gli attributi quali le azioni disponibili per il componente, le caratteristiche dell’editor locale e i listener relativi agli eventi sul componente. La configurazione è comune sia all’interfaccia touch che a quella classica, anche se con alcune differenze specifiche.

Il comportamento di [modifica di un componente è configurato](/help/sites-developing/components-basics.md#edit-behavior) aggiungendo un nodo `cq:editConfig` di tipo `cq:EditConfig` sotto il nodo del componente (di tipo `cq:Component`) e aggiungendo proprietà specifiche e nodi figlio.

## Configurazione del comportamento di anteprima {#configuring-the-preview-behavior}

Il cookie della modalità [WCM](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/WCMMode.html) viene impostato quando si passa alla modalità **Anteprima** anche se la pagina non viene aggiornata.

Per i componenti con un rendering sensibili alla modalità WCM, è necessario definirli per aggiornarsi in modo specifico e quindi basarsi sul valore del cookie.

>[!NOTE]
>
>Nell&#39;interfaccia utente touch vengono utilizzati solo i valori `EDIT` e `PREVIEW` per il cookie [Modalità WCM](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/WCMMode.html).

## Creazione e configurazione di una finestra di dialogo {#creating-and-configuring-a-dialog}

Le finestre di dialogo vengono utilizzate per consentire all’autore di interagire con il componente. Una finestra di dialogo consente agli autori e/o agli amministratori di modificare il contenuto, configurare il componente o definire i parametri di progettazione (utilizzando una [finestra di dialogo per progettazione](#creating-and-configuring-a-design-dialog))

### Coral UI e Granite UI {#coral-ui-and-granite-ui}

[Coral UI](https://developer.adobe.com/experience-manager/reference-materials/6-5/coral-ui/coralui3/index.html) e [Granite UI](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html) definiscono l&#39;aspetto moderno dell&#39;AEM.

[L&#39;interfaccia utente Granite fornisce una vasta gamma di componenti di base (widget)](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html) necessari per creare la finestra di dialogo nell&#39;ambiente di authoring. Se necessario, puoi estendere questa selezione e [creare un widget personalizzato](#creatinganewwidget).

Per maggiori dettagli, consulta:

* Coral UI

   * Fornisce un’interfaccia utente coerente per tutte le soluzioni cloud
   * [Concetti dell’interfaccia touch dell’AEM - Coral UI](/help/sites-developing/touch-ui-concepts.md#coral-ui)
   * [Guida all&#39;interfaccia utente Coral](https://developer.adobe.com/experience-manager/reference-materials/6-5/coral-ui/coralui3/index.html)

* Interfaccia utente Granite

   * Fornisce il markup dell’interfaccia utente Coral racchiuso nei componenti Sling per la creazione di console e finestre di dialogo dell’interfaccia utente
   * [Concetti dell’interfaccia touch dell’AEM - Interfaccia utente Granite](/help/sites-developing/touch-ui-concepts.md#coral-ui)
   * [Documentazione dell&#39;interfaccia utente Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html)

>[!NOTE]
>
>A causa della natura dei componenti dell&#39;interfaccia utente Granite (e delle differenze con i widget ExtJS), ci sono alcune differenze tra il modo in cui i componenti interagiscono con l&#39;interfaccia touch e l&#39;[interfaccia classica](/help/sites-developing/developing-components-classic.md).

### Creazione di una nuova finestra di dialogo {#creating-a-new-dialog}

Finestre di dialogo per l’interfaccia touch:

* sono denominati `cq:dialog`.
* sono definiti come nodo `nt:unstructured` con la proprietà `sling:resourceType` impostata.

* si trovano sotto il nodo `cq:Component` e accanto alla relativa definizione di componente.
* vengono sottoposte a rendering sul lato server (come componenti Sling), in base alla struttura del contenuto e alla proprietà `sling:resourceType`.
* utilizza il framework dell’interfaccia utente Granite.
* contiene una struttura di nodi che descrive i campi all’interno della finestra di dialogo.

   * questi nodi sono `nt:unstructured` con la proprietà `sling:resourceType` richiesta.

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

La personalizzazione di una finestra di dialogo è simile allo sviluppo di un componente, in quanto la finestra di dialogo stessa è un componente (ovvero, un markup rappresentato da uno script di componente insieme al comportamento/stile fornito da una libreria client).

Per esempi, consulta:

* `/libs/foundation/components/text/cq:dialog`
* `/libs/foundation/components/download/cq:dialog`

>[!NOTE]
>
>Se per un componente non è stata definita alcuna finestra di dialogo per l’interfaccia touch, come fallback viene utilizzata la finestra di dialogo dell’interfaccia classica all’interno di un livello di compatibilità. Per personalizzare tale finestra di dialogo è necessario personalizzare la finestra di dialogo dell’interfaccia classica. Consulta [Componenti AEM per l&#39;interfaccia classica](/help/sites-developing/developing-components-classic.md).

### Personalizzazione dei campi della finestra di dialogo {#customizing-dialog-fields}

>[!NOTE]
>
>Consulta:
>
>* la sessione AEM Gems su [Personalizzazione dei campi della finestra di dialogo](https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2015/aem-customizing-dialog-fields-in-touch-ui.html?lang=it).
>* il codice di esempio correlato è trattato in [Esempio di codice - Come personalizzare i campi della finestra di dialogo](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields).
>

#### Creazione di un nuovo campo {#creating-a-new-field}

I widget per l’interfaccia utente touch vengono implementati come componenti dell’interfaccia utente Granite.

Per creare un widget da utilizzare in una finestra di dialogo di un componente per l&#39;interfaccia utente touch, è necessario [creare un componente campo dell&#39;interfaccia utente Granite](/help/sites-developing/granite-ui-component.md).

>[!NOTE]
>
>Per informazioni dettagliate sull&#39;interfaccia utente Granite, consulta la [documentazione dell&#39;interfaccia utente Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html).

Se consideri la finestra di dialogo come un semplice contenitore per un elemento del modulo, puoi anche visualizzare il contenuto principale della finestra di dialogo come campi del modulo. La creazione di un campo modulo richiede la creazione di un tipo di risorsa, il che equivale alla creazione di un componente. Per facilitare questa attività, l&#39;interfaccia utente Granite offre un componente campo generico da cui ereditare (utilizzando `sling:resourceSuperType`):

`/libs/granite/ui/components/coral/foundation/form/field`

Più precisamente, l&#39;interfaccia utente Granite fornisce una serie di componenti di campo adatti all&#39;utilizzo nelle finestre di dialogo (o, più in generale, in [moduli](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/form/index.html)).

>[!NOTE]
>
>Questo differisce dall&#39;interfaccia classica, in cui i widget sono rappresentati da `cq:Widgets` nodi, ciascuno con un particolare `xtype` per stabilire la relazione con il widget ExtJS corrispondente. Dal punto di vista dell’implementazione, questi widget sono stati sottoposti a rendering sul lato client dal framework ExtJS.

Dopo aver creato il tipo di risorsa, è possibile creare un&#39;istanza del campo aggiungendo un nuovo nodo nella finestra di dialogo, con la proprietà `sling:resourceType` che fa riferimento al tipo di risorsa appena introdotto.

#### Creazione di una libreria client per stile e comportamento {#creating-a-client-library-for-style-and-behavior}

Se desideri definire lo stile e il comportamento del componente, puoi creare una [libreria client](/help/sites-developing/clientlibs.md) dedicata che definisce i tuoi file CSS/LESS e JS personalizzati.

Per caricare la libreria client solo per la finestra di dialogo del componente, ovvero non per un altro componente, è necessario impostare la proprietà `extraClientlibs` della finestra di dialogo sul nome della categoria della libreria client creata. Questa opzione è consigliata se la libreria client è molto grande e/o il campo è specifico per tale finestra di dialogo e non sarà necessario in altre finestre di dialogo.

Per caricare la libreria client per tutte le finestre di dialogo, impostare la proprietà category della libreria client su `cq.authoring.dialog`. Questo è il nome della categoria della libreria client che viene inclusa per impostazione predefinita durante il rendering di tutte le finestre di dialogo. Puoi eseguire questa operazione se la libreria client è piccola e/o il campo è generico e potrebbe essere riutilizzato in altre finestre di dialogo.

Ad esempio, consulta:

* `cqgems/customizingfield/components/colorpicker/clientlibs`

   * fornito da [Esempio di codice](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

#### Estensione (ereditarietà) di un campo {#extending-inheriting-from-a-field}

A seconda delle tue esigenze, puoi effettuare le seguenti operazioni:

* Estendere un determinato campo dell&#39;interfaccia utente Granite per ereditarietà del componente ( `sling:resourceSuperType`)
* Estendere un determinato widget dalla libreria di widget sottostante (se è presente l’interfaccia utente Granite, è l’interfaccia utente Coral), seguendo l’API della libreria di widget (ereditarietà JS/CSS)

#### Accesso ai campi della finestra di dialogo {#access-to-dialog-fields}

È inoltre possibile utilizzare le condizioni di rendering ( `rendercondition`) per controllare chi ha accesso a schede/campi specifici nella finestra di dialogo, ad esempio:

```xml
+ mybutton
  - sling:resourceType = granite/ui/components/coral/foundation/button
  + rendercondition
    - sling:resourceType = myapp/components/renderconditions/group
    - groups = ["administrators"]
```

### Gestione degli eventi dei campi {#handling-field-events}

Il metodo di gestione degli eventi nei campi della finestra di dialogo è ora eseguito con [listener in una libreria client personalizzata](#listeners-in-a-custom-client-library). Si tratta di una modifica rispetto al metodo precedente di avere [listener nella struttura del contenuto](#listenersinthecontentstructureclassicui).

#### Listener in una libreria client personalizzata {#listeners-in-a-custom-client-library}

Per inserire la logica nel campo, è necessario:

1. Il campo deve essere contrassegnato con una determinata classe CSS (l&#39;*hook*).
1. Definisci, nella libreria client un listener JS collegato al nome di classe CSS (in modo che la logica personalizzata abbia ambito solo sul tuo campo e non influisca su altri campi dello stesso tipo).

A questo scopo, è necessario conoscere la libreria di widget sottostante con cui desideri interagire. Consulta la [documentazione dell&#39;interfaccia utente Coral](https://developer.adobe.com/experience-manager/reference-materials/6-5/coral-ui/coralui3/index.html) per identificare l&#39;evento a cui desideri reagire. Questo processo è molto simile a quello che dovevi eseguire con ExtJS in passato: trova la pagina della documentazione di un dato widget, quindi controlla i dettagli dell&#39;API dell&#39;evento.

Ad esempio, consulta:

* `cqgems/customizingfield/components/clientlibs/customizingfield`

   * fornito da [Esempio di codice](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

#### Listener nella struttura del contenuto {#listeners-in-the-content-structure}

Nell’interfaccia classica con ExtJS, solitamente i listener per un determinato widget erano inclusi nella struttura del contenuto. Ottenere lo stesso risultato nell’interfaccia touch è diverso in quanto il codice del listener JS (o qualsiasi codice) non è più definito nel contenuto.

La struttura del contenuto descrive la struttura semantica; non dovrebbe (deve) implicare la natura del widget sottostante. Se nella struttura del contenuto non è presente codice JS, puoi modificare i dettagli di implementazione senza dover modificare la struttura del contenuto. In altre parole, è possibile modificare la libreria dei widget senza dover toccare la struttura del contenuto.

#### Rilevamento della disponibilità della finestra di dialogo {#dialog-ready}

Se si dispone di un JavaScript personalizzato che deve essere eseguito solo quando la finestra di dialogo è disponibile e pronta, è necessario ascoltare l&#39;evento `dialog-ready`.

Questo evento viene attivato ogni volta che la finestra di dialogo viene caricata (o ricaricata) ed è pronta per l’uso, ovvero ogni volta che si verifica una modifica (creazione/aggiornamento) nel DOM della finestra di dialogo.

`dialog-ready` può essere utilizzato per eseguire l&#39;hook nel codice personalizzato di JavaScript che esegue personalizzazioni sui campi all&#39;interno di una finestra di dialogo o attività simili.

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

La convalida dei campi nell&#39;interfaccia utente Granite e nei componenti dell&#39;interfaccia utente Granite (equivalenti ai widget) viene eseguita utilizzando l&#39;API `foundation-validation`. [Per informazioni dettagliate, vedere la documentazione di `foundation-valdiation` Granite.](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/clientlibs/foundation/js/validation/index.html)

Per esempi, consulta:

* `cqgems/customizingfield/components/clientlibs/customizingfield/js/validations.js`

   * fornito da [Esempio di codice](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

* `/libs/cq/gui/components/authoring/dialog/clientlibs/dialog/js/validations.js`

## Creazione e configurazione di una finestra di dialogo per progettazione {#creating-and-configuring-a-design-dialog}

La finestra di dialogo per progettazione viene visualizzata quando un componente presenta dettagli di progettazione che è possibile modificare in [Modalità progettazione](/help/sites-authoring/default-components-designmode.md).

La definizione è molto simile a quella di una [finestra di dialogo utilizzata per modificare il contenuto](#creating-a-new-dialog), con la differenza che è definita come nodo:

* Nome nodo: `cq:design_dialog`
* Tipo: `nt:unstructured`

## Creazione e configurazione di un Inplace Editor {#creating-and-configuring-an-inplace-editor}

Un editor locale consente all’utente di modificare il contenuto direttamente nel flusso di paragrafo, senza dover aprire una finestra di dialogo. Ad esempio, i componenti standard Testo e Titolo dispongono entrambi di un editor locale.

Un editor locale non è necessario/significativo per ogni tipo di componente.

Per ulteriori informazioni, vedere [Estensione dell&#39;authoring delle pagine - Aggiunta di un nuovo editor locale](/help/sites-developing/customizing-page-authoring-touch.md#add-new-in-place-editor).

## Personalizzazione della barra degli strumenti del componente {#customizing-the-component-toolbar}

La [Barra degli strumenti del componente](/help/sites-developing/touch-ui-structure.md#component-toolbar) consente all&#39;utente di accedere a una serie di azioni per il componente, ad esempio modifica, configurazione, copia ed eliminazione.

Per ulteriori informazioni, vedere [Estensione dell&#39;authoring delle pagine - Aggiunta di una nuova azione alla barra degli strumenti di un componente](/help/sites-developing/customizing-page-authoring-touch.md#add-new-action-to-a-component-toolbar).

## Configurazione di un componente per la barra dei riferimenti (in prestito/preso in prestito) {#configuring-a-component-for-the-references-rail-borrowed-lent}

Se il nuovo componente fa riferimento a contenuto proveniente da altre pagine, puoi valutare se influire sulle sezioni **Contenuto in prestito** e **Contenuto prestato** della barra [**Riferimenti**](/help/sites-authoring/basic-handling.md#references).

L’AEM preconfigurato controlla solo il componente Reference. Per aggiungere il componente è necessario configurare il bundle OSGi **WCM Authoring Content Reference Configuration**.

Crea una voce nella definizione, specificando il componente, insieme alla proprietà da controllare. Ad esempio:

`/apps/<*your-Project*>/components/reference@parentPath`

>[!NOTE]
>
>Quando si lavora con l’AEM, esistono diversi metodi per gestire le impostazioni di configurazione di tali servizi. Per ulteriori dettagli e procedure consigliate, vedere [Configurazione di OSGi](/help/sites-deploying/configuring-osgi.md).

## Abilitazione e aggiunta del componente al sistema dei paragrafi {#enabling-and-adding-your-component-to-the-paragraph-system}

Una volta sviluppato, il componente deve essere abilitato per l’utilizzo in un sistema paragrafo appropriato, in modo da poter essere utilizzato nelle pagine richieste.

Questa operazione può essere eseguita da:

* utilizzo della [modalità progettazione](/help/sites-authoring/default-components-designmode.md) durante la modifica di una pagina specifica.
* [definizione della proprietà `components` nel sistema paragrafo di un modello](/help/sites-developing/components-basics.md#adding-your-component-to-the-paragraph-system).

## Configurazione di un sistema di paragrafi in modo che il trascinamento di una risorsa crei un’istanza di componente {#configuring-a-paragraph-system-so-that-dragging-an-asset-creates-a-component-instance}

AEM offre la possibilità di configurare un sistema paragrafo nella pagina in modo che [un&#39;istanza del nuovo componente venga creata automaticamente quando un utente trascina una risorsa (appropriata) in un&#39;istanza della pagina](/help/sites-authoring/editing-content.md#insertingacomponenttouchoptimizedui) (invece di dover sempre trascinare un componente vuoto nella pagina).

È possibile configurare questo comportamento e la relazione risorsa-componente richiesta:

1. Nella definizione del paragrafo della progettazione della pagina. Ad esempio:

   * `/etc/designs/<myApp>/page/par`

   Crea un nodo:

   * Nome: `cq:authoring`
   * Tipo: `nt:unstructured`

1. In questo caso, crea un nodo che contenga tutti i mapping risorsa-componente:

   * Nome: `assetToComponentMapping`
   * Tipo: `nt:unstructured`

1. Per ogni mappatura da risorsa a componente, crea un nodo:

   * Nome: testo; si consiglia che il nome indichi la risorsa e il tipo di componente correlato, ad esempio immagine
   * Tipo: `nt:unstructured`

   Ognuno con le seguenti proprietà:

   * `assetGroup`:

      * Tipo: `String`
      * Valore: il gruppo a cui appartiene la risorsa correlata, ad esempio `media`

   * `assetMimetype`:

      * Tipo: `String`
      * Valore: il tipo MIME della risorsa correlata, ad esempio `image/*`

   * `droptarget`:

      * Tipo: `String`
      * Valore: destinazione di rilascio; ad esempio, `image`

   * `resourceType`:

      * Tipo: `String`
      * Valore: la risorsa componente correlata, ad esempio `foundation/components/image`

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
* Scarica il progetto come [file ZIP](https://github.com/adobe/aem-project-archetype/archive/master.zip)

>[!NOTE]
>
>La creazione automatica delle istanze dei componenti può ora essere configurata facilmente nell&#39;interfaccia utente quando si utilizzano [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it) e modelli modificabili. Consulta [Creazione di modelli di pagina](/help/sites-authoring/templates.md#editing-a-template-structure-template-author) per ulteriori informazioni su come definire quali componenti sono automaticamente associati ai tipi di file multimediali specificati.

## Utilizzo dell’estensione per Brackets dell’AEM {#using-the-aem-brackets-extension}

L&#39;estensione [Brackets AEM](/help/sites-developing/aem-brackets.md) fornisce un flusso di lavoro fluido per modificare i componenti AEM e le librerie client. È basato sull&#39;editor di codice [Brackets](https://brackets.io/).

L’estensione:

* Semplifica la sincronizzazione (non è richiesto Maven o File Vault) per aumentare l’efficienza degli sviluppatori e aiuta gli sviluppatori front-end con conoscenze AEM limitate a partecipare ai progetti.
* Fornisce il supporto di [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html?lang=it), il linguaggio del modello progettato per semplificare lo sviluppo dei componenti e aumentare la sicurezza.

>[!NOTE]
>
>Brackets è il meccanismo consigliato per la creazione di componenti. Sostituisce la funzionalità CRXDE Liti - Crea componente, progettata per l’interfaccia classica.

## Migrazione da un componente classico {#migrating-from-a-classic-component}

Quando si migra un componente progettato per essere utilizzato con l’interfaccia classica a un componente che può essere utilizzato con l’interfaccia touch (singolarmente o congiuntamente), è necessario considerare i seguenti problemi:

* HTL

   * L&#39;utilizzo di [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html?lang=it) non è obbligatorio, ma se il componente deve essere aggiornato, è il momento ideale per valutare la possibilità di [migrare da JSP a HTL](/help/sites-developing/components-basics.md#htl-vs-jsp).

* Componenti

   * Migra il codice [`cq:listener`](/help/sites-developing/developing-components.md#migrating-cq-listener-code) che utilizza le funzioni classiche specifiche dell&#39;interfaccia utente
   * Plug-in RTE. Per ulteriori informazioni, vedere [Configurazione dell&#39;editor Rich Text](/help/sites-administering/rich-text-editor.md).
   * [Esegui migrazione di `cq:listener` codice](#migrating-cq-listener-code) che utilizza funzioni specifiche dell&#39;interfaccia utente classica

* Finestre di dialogo

   * Crea una finestra di dialogo da utilizzare nell’interfaccia touch. Tuttavia, a scopo di compatibilità, l’interfaccia touch può utilizzare la definizione di finestra di dialogo dell’interfaccia classica, se non è stata definita alcuna finestra di dialogo per tale interfaccia.
   * Gli [strumenti di modernizzazione AEM](/help/sites-developing/modernization-tools.md) sono forniti per aiutarti a estendere i componenti esistenti.
   * [La mappatura di ExtJS ai componenti dell&#39;interfaccia utente Granite](/help/sites-developing/touch-ui-concepts.md#extjs-and-corresponding-granite-ui-components) fornisce una pratica panoramica degli xtype ExtJS e dei tipi di nodo con i corrispondenti tipi di risorse dell&#39;interfaccia utente Granite.
   * Personalizzazione dei campi. Per ulteriori informazioni, vedere la sessione AEM Gems su [Personalizzazione dei campi della finestra di dialogo](https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2015/aem-customizing-dialog-fields-in-touch-ui.html?lang=it).
   * Migra da vtypes a [Convalida interfaccia utente Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/clientlibs/foundation/js/validation/index.html)
   * Utilizzando i listener JS, per ulteriori informazioni vedi [Gestione degli eventi dei campi](#handling-field-events) e la sessione AEM Gems su [Personalizzazione dei campi della finestra di dialogo](https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2015/aem-customizing-dialog-fields-in-touch-ui.html?lang=it).

### Migrazione di cq:codice listener {#migrating-cq-listener-code}

Se si sta eseguendo la migrazione di un progetto progettato per l&#39;interfaccia utente classica, è possibile che il codice `cq:listener` (e le clientlibs correlate al componente) utilizzino funzioni specifiche dell&#39;interfaccia utente classica (ad esempio `CQ.wcm.*`). Per la migrazione è necessario aggiornare tale codice utilizzando gli oggetti/le funzioni equivalenti nell’interfaccia utente touch.

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

Inserire un file `README.md` nella struttura del componente. Questo markdown viene visualizzato nella [console componenti](/help/sites-authoring/default-components-console.md).

![chlimage_1-7](assets/chlimage_1-7.png)

Il markdown supportato è lo stesso dei [frammenti di contenuto](/help/assets/content-fragments/content-fragments-markdown.md).
