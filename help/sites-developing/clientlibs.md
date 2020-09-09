---
title: Utilizzo delle librerie lato client
seo-title: Utilizzo delle librerie lato client
description: AEM fornisce Cartelle libreria lato client che consentono di memorizzare il codice lato client nell'archivio, organizzarlo in categorie e definire quando e come ciascuna categoria di codice deve essere distribuita al client
seo-description: AEM fornisce Cartelle libreria lato client che consentono di memorizzare il codice lato client nell'archivio, organizzarlo in categorie e definire quando e come ciascuna categoria di codice deve essere distribuita al client
uuid: f12b13cc-6651-4c9a-9c52-19a22bb82b28
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 3d14837d-41a8-480a-83ba-392e32f84c65
docset: aem65
translation-type: tm+mt
source-git-commit: 5d33b48000cf607eb77c626ec539280cadab378e
workflow-type: tm+mt
source-wordcount: '2889'
ht-degree: 0%

---


# Utilizzo delle librerie lato client{#using-client-side-libraries}

I siti Web moderni si affidano in larga misura all&#39;elaborazione sul lato client basata su codice JavaScript e CSS complessi. L&#39;organizzazione e l&#39;ottimizzazione della gestione di questo codice può essere un problema complicato.

Per risolvere il problema, AEM fornisce Cartelle **libreria lato** client che consentono di memorizzare il codice lato client nell&#39;archivio, organizzarlo in categorie e definire quando e come ciascuna categoria di codice deve essere distribuita al client. Il sistema di libreria lato client si occupa quindi di generare i collegamenti corretti nella pagina Web finale per caricare il codice corretto.

## Funzionamento delle librerie lato client in AEM {#how-client-side-libraries-work-in-aem}

Il modo standard per includere una libreria lato client (ovvero un file JS o CSS) nell’HTML di una pagina consiste semplicemente nell’includere un `<script>` tag o `<link>` nel JSP per tale pagina, contenente il percorso del file in questione. Esempio,

```xml
...
<head>
   ...
   <script type="text/javascript" src="/etc/clientlibs/granite/jquery/source/1.8.1/jquery-1.8.1.js"></script>
   ...
</head>
...
```

Anche se questo approccio funziona in AEM, può causare problemi quando le pagine e i loro componenti diventano complessi. In tali casi esiste il rischio che più copie della stessa libreria JS possano essere incluse nell’output HTML finale. Per evitare questo problema e consentire l&#39;organizzazione logica delle librerie lato client AEM utilizzare le cartelle **libreria lato** client.

Una cartella libreria lato client è un nodo di tipo repository `cq:ClientLibraryFolder`. La definizione nella notazione [](https://jackrabbit.apache.org/node-type-notation.html) CND è

```shell
[cq:ClientLibraryFolder] > sling:Folder
  - dependencies (string) multiple
  - categories (string) multiple
  - embed (string) multiple
  - channels (string) multiple
```

Per impostazione predefinita, `cq:ClientLibraryFolder` i nodi possono essere posizionati ovunque all’interno delle `/apps`strutture `/libs` e `/etc` sottostrutture dell’archivio (queste impostazioni predefinite e altre impostazioni possono essere controllate tramite il pannello **Adobe Granite HTML Library Manager** della console [di](https://localhost:4502/system/console/configMgr)sistema).

Ogni file `cq:ClientLibraryFolder` viene compilato con un set di file JS e/o CSS, insieme ad alcuni file di supporto (vedete di seguito). Le proprietà `cq:ClientLibraryFolder` sono configurate come segue:

* `categories`: Identifica le categorie in cui il set di file JS e/o CSS entro questo `cq:ClientLibraryFolder` autunno. La `categories` proprietà, con un valore multiplo, consente a una cartella libreria di appartenere a più categorie (vedere di seguito per informazioni utili).

* `dependencies`: Si tratta di un elenco di altre categorie di libreria client da cui dipende la cartella libreria. Ad esempio, due `cq:ClientLibraryFolder` nodi specificati `F` e `G`, se un file in `F` richiede un altro file `G` per funzionare correttamente, almeno uno dei `categories` nodi di `G` deve essere compreso tra i `dependencies` di `F`.

* `embed`: Utilizzato per incorporare il codice da altre librerie. Se il nodo F incorpora i nodi G e H, l&#39;HTML risultante sarà una concentrazione di contenuto dai nodi G e H.
* `allowProxy`: Se una libreria client si trova in `/apps`, questa proprietà consente l&#39;accesso tramite servlet proxy. Consultate [Individuazione di una cartella della libreria client e Utilizzo del servlet](/help/sites-developing/clientlibs.md#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet) delle librerie client proxy di seguito.

## Riferimento a librerie lato client {#referencing-client-side-libraries}

Poiché HTL è la tecnologia preferita per lo sviluppo di siti AEM, HTL dovrebbe essere utilizzato per includere librerie lato client in AEM. Tuttavia è anche possibile farlo utilizzando JSP.

### Utilizzo di HTL {#using-htl}

In HTL, le librerie client vengono caricate tramite un modello helper fornito da AEM, accessibile tramite [`data-sly-use`](https://helpx.adobe.com/experience-manager/htl/using/block-statements.html#use). In questo file sono disponibili tre modelli, che possono essere richiamati tramite [ `data-sly-call`](https://helpx.adobe.com/experience-manager/htl/using/block-statements.html#template-call):

* **css** - Carica solo i file CSS delle librerie client di riferimento.
* **js** - Carica solo i file JavaScript delle librerie client di riferimento.
* **all** - Carica tutti i file delle librerie client di riferimento (sia CSS che JavaScript).

Ogni modello di supporto prevede un&#39; `categories` opzione per fare riferimento alle librerie client desiderate. Tale opzione può essere una matrice di valori stringa o una stringa contenente un elenco di valori separati da virgola.

Per ulteriori dettagli ed esempi di utilizzo, consultare la [Guida introduttiva al linguaggio](https://helpx.adobe.com/experience-manager/htl/using/getting-started.html#loading-client-libraries)per modelli HTML.

### Utilizzo di JSP {#using-jsp}

Aggiungi un `ui:includeClientLib` tag al codice JSP per aggiungere un collegamento alle librerie client nella pagina HTML generata. Per fare riferimento alle librerie, utilizzare il valore della `categories` proprietà del `ui:includeClientLib` nodo.

```
<%@taglib prefix="ui" uri="https://www.adobe.com/taglibs/granite/ui/1.0" %>
<ui:includeClientLib categories="<%= categories %>" />
```

Ad esempio, il `/etc/clientlibs/foundation/jquery` nodo è di tipo `cq:ClientLibraryFolder` con una proprietà category di valore `cq.jquery`. Il codice seguente in un file JSP fa riferimento alle librerie:

```xml
<ui:includeClientLib categories="cq.jquery"/>
```

La pagina HTML generata contiene il seguente codice:

```xml
<script type="text/javascript" src="/etc/clientlibs/foundation/jquery.js"></script>
```

Per informazioni complete, inclusi gli attributi per filtrare le librerie JS, CSS o di temi, consultate [ui:includeClientLib](/help/sites-developing/taglib.md#lt-ui-includeclientlib).

>[!CAUTION]
>
>`<cq:includeClientLib>`, che in passato veniva comunemente usato per includere le librerie client, è stato dichiarato obsoleto a partire dal AEM 5.6. [ `<ui:includeClientLib>`](/help/sites-developing/taglib.md#lt-ui-includeclientlib) devono essere utilizzati come descritto sopra.

## Creazione di cartelle libreria client {#creating-client-library-folders}

Creare un `cq:ClientLibraryFolder` nodo per definire le librerie JavaScript e Cascading Style Sheet e renderle disponibili per le pagine HTML. Utilizzare la `categories` proprietà del nodo per identificare le categorie di libreria alle quali appartiene.

Il nodo contiene uno o più file sorgente che, in fase di esecuzione, vengono uniti in un singolo file JS e/o CSS. Il nome del file generato è il nome del nodo con l’estensione `.js` o del nome del `.css` file. Ad esempio, il nodo della libreria denominato `cq.jquery` restituisce il file generato denominato `cq.jquery.js` o `cq.jquery.css`.

Le cartelle della libreria client contengono i seguenti elementi:

* I file sorgente JS e/o CSS da unire.
* Risorse che supportano gli stili CSS, ad esempio i file di immagine.

   **Nota:** Potete usare le sottocartelle per organizzare i file sorgente.
* Un `js.txt` file e/o un `css.txt` file che identifica i file sorgente da unire nei file JS e/o CSS generati.

![clientlibarch](assets/clientlibarch.png)

Per informazioni sui requisiti specifici per le librerie client per i widget, consultate [Utilizzo ed estensione dei widget](/help/sites-developing/widgets.md).

Il client Web deve disporre delle autorizzazioni per accedere al `cq:ClientLibraryFolder` nodo. È inoltre possibile esporre le librerie dalle aree protette dell&#39;archivio (vedere Incorporazione di codice da altre librerie, di seguito).

### Sostituzione delle librerie in /lib {#overriding-libraries-in-lib}

Le cartelle libreria client riportate di seguito `/apps` hanno la precedenza rispetto alle cartelle omonime che si trovano in modo simile in `/libs`. Ad esempio, `/apps/cq/ui/widgets` ha la precedenza su `/libs/cq/ui/widgets`. Quando queste librerie appartengono alla stessa categoria, `/apps` viene utilizzata la libreria sottostante.

### Individuazione di una cartella della libreria client e utilizzo del servlet delle librerie client proxy {#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet}

Nelle versioni precedenti, le cartelle della libreria client si trovavano sotto `/etc/clientlibs` nella directory archivio. Questo è ancora supportato, tuttavia è consigliabile che le librerie client si trovino ora in `/apps`. Questo consente di individuare le librerie client accanto agli altri script, che si trovano generalmente sotto `/apps` e `/libs`.

>[!NOTE]
>
>Le risorse statiche sotto la cartella della libreria client devono trovarsi in una cartella denominata *risorse*. Se non disponete delle risorse statiche, come le immagini, nelle *risorse* della cartella, non è possibile fare riferimento a tali risorse in un’istanza di pubblicazione. Esempio: https://localhost:4503/etc.clientlibs/geometrixx/components/clientlibs/resources/example.gif

>[!NOTE]
>
>Per isolare meglio il codice dal contenuto e dalla configurazione, si consiglia di individuare le librerie client al di sotto `/apps` e di esporle tramite `/etc.clientlibs` l&#39;uso della `allowProxy` proprietà.

Per rendere accessibili le librerie client `/apps` in uso, viene utilizzato un servlet proxy. Gli ACL sono ancora applicati alla cartella della libreria client, ma il servlet consente la lettura del contenuto tramite `/etc.clientlibs/` se la `allowProxy` proprietà è impostata su `true`.

Per accedere a una risorsa statica è possibile utilizzare il proxy solo se si trova sotto una risorsa sotto la cartella della libreria client.

Ad esempio:

* Hai una clientlib in `/apps/myproject/clientlibs/foo`
* L’immagine è statica in `/apps/myprojects/clientlibs/foo/resources/icon.png`

Quindi si imposta la `allowProxy` proprietà `foo` su true.

* Potete quindi richiedere `/etc.clientlibs/myprojects/clientlibs/foo.js`
* Potete quindi fare riferimento all’immagine tramite `/etc.clientlibs/myprojects/clientlibs/foo/resources/icon.png`

>[!CAUTION]
>
>Quando si utilizzano librerie client proxy, la configurazione del dispatcher AEM potrebbe richiedere un aggiornamento per garantire che gli URI con i clientlibs di estensione siano consentiti.

>[!CAUTION]
>
> Adobe consiglia di individuare le librerie client in `/apps` e renderle disponibili tramite il servlet proxy. Tuttavia, tenete presente che la best practice richiede ancora che i siti pubblici non includano mai nulla servito direttamente su un `/apps` percorso o `/libs` percorso.

### Creare una cartella libreria client {#create-a-client-library-folder}

1. Aprite il CRXDE Lite in un browser Web ([https://localhost:4502/crx/de](https://localhost:4502/crx/de)).
1. Selezionate la cartella in cui desiderate individuare la cartella della libreria client e fate clic su **Crea > Crea nodo**.
1. Immettete un nome per il file libreria e selezionate `cq:ClientLibraryFolder`. Fate clic su **OK** , quindi su **Salva tutto**.
1. Per specificare la categoria o le categorie a cui appartiene la libreria, selezionate il `cq:ClientLibraryFolder` nodo, aggiungete la seguente proprietà, quindi fate clic su **Salva tutto**:

   * Nome: category
   * Tipo: Stringa
   * Valore: Nome categoria
   * Multi: Select

1. Aggiungete i file sorgente alla cartella della libreria in qualsiasi modo. Ad esempio, utilizzate un client WebDav per copiare i file oppure create un file e create manualmente il contenuto.

   **Nota:** Se necessario, potete organizzare i file sorgente in sottocartelle.

1. Selezionate la cartella della libreria client e fate clic su **Crea > Crea file**.
1. Nella casella Nome file digitare uno dei seguenti nomi di file e fare clic su OK:

   * **`js.txt`:** Utilizzate questo nome file per generare un file JavaScript.
   * **`css.txt`:** Utilizzare questo nome file per generare un foglio di stile CSS.

1. Aprite il file e digitate il testo seguente per identificare la radice del percorso dei file sorgente:

   `#base=*[root]*`

   Sostituire * `[root]`* con il percorso della cartella che contiene i file sorgente, relativo al file TXT. Ad esempio, usate il testo seguente quando i file sorgente si trovano nella stessa cartella del file TXT:

   `#base=.`

   Il codice seguente imposta la radice come cartella denominata mobile sotto il `cq:ClientLibraryFolder` nodo:

   `#base=mobile`

1. Nelle righe seguenti `#base=[root]`, digitare i percorsi dei file sorgente relativi alla radice. Posizionare ciascun nome file su una riga separata.
1. Fate clic su **Salva tutto**.

### Collegamento a dipendenze {#linking-to-dependencies}

Quando il codice nella cartella della libreria client fa riferimento ad altre librerie, identificate le altre librerie come dipendenze. In JSP, il `ui:includeClientLib` tag che fa riferimento alla cartella della libreria client fa sì che il codice HTML includa un collegamento al file libreria generato, nonché alle dipendenze.

Le dipendenze devono essere un&#39;altra `cq:ClientLibraryFolder`. Per identificare le dipendenze, aggiungi una proprietà al `cq:ClientLibraryFolder` nodo con i seguenti attributi:

* **Nome:** dipendenze
* **Tipo:** Stringa[]
* **Valori:** Il valore della proprietà category del nodo cq:ClientLibraryFolder da cui dipende la cartella libreria corrente.

Ad esempio, / `etc/clientlibs/myclientlibs/publicmain` ha una dipendenza dalla `cq.jquery` libreria. L&#39;JSP che fa riferimento alla libreria client principale genera HTML che include il seguente codice:

```xml
<script src="/etc/clientlibs/foundation/cq.jquery.js" type="text/javascript">
<script src="/etc/clientlibs/mylibs/publicmain.js" type="text/javascript">
```

### Incorporazione Di Codice Da Altre Librerie {#embedding-code-from-other-libraries}

Potete incorporare il codice da una libreria client a un&#39;altra libreria client. In fase di esecuzione, i file JS e CSS generati dalla libreria di incorporamento includono il codice della libreria incorporata.

L&#39;incorporazione del codice è utile per fornire l&#39;accesso alle librerie memorizzate nelle aree protette dell&#39;archivio.

#### Cartelle libreria client specifiche per l&#39;app {#app-specific-client-library-folders}

È consigliabile mantenere tutti i file relativi all’applicazione nella cartella dell’applicazione sottostante `/app`. È inoltre consigliabile negare l’accesso alla `/app` cartella ai visitatori del sito Web. Per soddisfare entrambe le procedure ottimali, create una cartella della libreria client sotto la `/etc` cartella che incorpora la libreria client riportata di seguito `/app`.

Utilizzare la proprietà category per identificare la cartella della libreria client da incorporare. Per incorporare la libreria, aggiungere una proprietà al `cq:ClientLibraryFolder` nodo di incorporamento, utilizzando i seguenti attributi di proprietà:

* **Nome:** embed
* **Tipo:** Stringa[]
* **Valore:** Il valore della proprietà category del `cq:ClientLibraryFolder` nodo da incorporare.

#### Utilizzo dell&#39;incorporazione per ridurre al minimo le richieste {#using-embedding-to-minimize-requests}

In alcuni casi, l’HTML finale generato per la pagina tipica dall’istanza di pubblicazione include un numero relativamente elevato di `<script>` elementi, in particolare se il sito utilizza le informazioni contestuali del client per l’analisi o il targeting. Ad esempio, in un progetto non ottimizzato potete trovare la serie seguente di `<script>` elementi nell’HTML per una pagina:

```xml
<script type="text/javascript" src="/etc/clientlibs/granite/jquery.js"></script>
<script type="text/javascript" src="/etc/clientlibs/granite/utils.js"></script>
<script type="text/javascript" src="/etc/clientlibs/granite/jquery/granite.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/jquery.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/shared.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/personalization/kernel.js"></script>
```

In tali casi, può essere utile combinare tutti i codici libreria client richiesti in un singolo file in modo da ridurre il numero di richieste di andata e ritorno al caricamento della pagina. A questo scopo, potete inserire `embed` le librerie necessarie nella libreria client specifica per l&#39;app utilizzando la proprietà embed del `cq:ClientLibraryFolder` nodo.

Le seguenti categorie di libreria client sono incluse con AEM. È consigliabile incorporare solo quelli necessari per il funzionamento del sito specifico. Tuttavia, **è necessario mantenere l&#39;ordine elencato qui**:

1. `browsermap.standard`
1. `browsermap`
1. `jquery-ui`
1. `cq.jquery.ui`
1. `personalization`
1. `personalization.core`
1. `personalization.core.kernel`
1. `personalization.clientcontext.kernel`
1. `personalization.stores.kernel`
1. `personalization.kernel`
1. `personalization.clientcontext`
1. `personalization.stores`
1. `cq.collab.comments`
1. `cq.collab.feedlink`
1. `cq.collab.ratings`
1. `cq.collab.toggle`
1. `cq.collab.forum`
1. `cq.cleditor`

#### Percorsi nei file CSS {#paths-in-css-files}

Quando incorporate file CSS, il codice CSS generato utilizza percorsi verso risorse relative alla libreria di incorporamento. Ad esempio, la libreria con accesso pubblico `/etc/client/libraries/myclientlibs/publicmain` incorpora la libreria `/apps/myapp/clientlib` client:

![screen_shot_2012-05-29at20122pm](assets/screen_shot_2012-05-29at20122pm.png)

Il `main.css` file contiene il seguente stile:

```xml
body {
  padding: 0;
  margin: 0;
  background: url(images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

Il file CSS generato dal `publicmain` nodo contiene il seguente stile, utilizzando l&#39;URL dell&#39;immagine originale:

```xml
body {
  padding: 0;
  margin: 0;
  background: url(../../../apps/myapp/clientlib/styles/images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

### Utilizzo di una libreria per specifici gruppi di dispositivi mobili {#using-a-library-for-specific-mobile-groups}

Utilizzate la `channels` proprietà di una cartella libreria client per identificare il gruppo mobile che utilizza la libreria. La `channels` proprietà è utile quando librerie della stessa categoria sono progettate per diverse funzionalità del dispositivo.

Per associare una cartella libreria client a un gruppo di dispositivi, aggiungete una proprietà al `cq:ClientLibraryFolder` nodo con i seguenti attributi:

* **Nome:** canali
* **Tipo:** Stringa[]
* **Valori:** Nome del gruppo di dispositivi mobili. Per escludere la cartella libreria da un gruppo, aggiungete il prefisso al nome con un punto esclamativo (&quot;!&quot;).

Nella tabella seguente, ad esempio, è riportato il valore della `channels` proprietà per ogni cartella libreria client della `cq.widgets` categoria:

| Cartella libreria client | Valore della proprietà channel |
|---|---|
| `/libs/cq/analytics/widgets` | `!touch` |
| `/libs/cq/analytics/widgets/themes/default` | `!touch` |
| `/libs/cq/cloudserviceconfigs/widgets` | `!touch` |
| `/libs/cq/searchpromote/widgets` | `!touch` |
| `/libs/cq/searchpromote/widgets/themes/default` | *[nessun valore]* |
| `/libs/cq/touch/widgets` | `touch` |
| `/libs/cq/touch/widgets/themes/default` | `touch` |
| `/libs/cq/ui/widgets` | `!touch` |
| `/libs/cq/ui/widgets/themes/default` | `!touch` |

## Utilizzo dei preprocessori {#using-preprocessors}

AEM consente preprocessori plug-in e navi con supporto per [YUI Compressor](https://github.com/yui/yuicompressor#yui-compressor---the-yahoo-javascript-and-css-compressor) per CSS e JavaScript e [Google Closure Compiler (GCC)](https://developers.google.com/closure/compiler/) per JavaScript con YUI impostato AEM preprocessore predefinito.

I preprocessori collegabili consentono un utilizzo flessibile, tra cui:

* Definizione di ScriptProcessors in grado di elaborare origini di script
* I processori sono configurabili con opzioni
* I processori possono essere utilizzati per la minificazione, ma anche per i casi non minati
* clientlib può definire quale processore utilizzare

>[!NOTE]
>
>Per impostazione predefinita, AEM utilizza il compressore YUI. Per un elenco dei problemi noti, consultate la documentazione [di](https://github.com/yui/yuicompressor/issues) YUI Compressor GitHub. Il passaggio al compressore GCC per determinati clientlibs può risolvere alcuni problemi rilevati durante l’utilizzo di YUI.

>[!CAUTION]
>
>Non inserite una libreria ridotta in una libreria client. Fornite invece la libreria non elaborata e, se è necessaria la minificazione, utilizzate le opzioni dei preprocessori.

### Utilizzo {#usage}

Potete scegliere di configurare la configurazione dei preprocessori per clientlibrary o per tutta la struttura del sistema.

* Aggiungere le proprietà multivalore `cssProcessor` e `jsProcessor` sul nodo clientlibrary

* Oppure definite la configurazione predefinita del sistema tramite la configurazione OSGi di **HTML Library Manager** .

Una configurazione preprocessore sul nodo clientlib ha la precedenza rispetto alla configurazione OSGI.

### Formato ed esempi {#format-and-examples}

#### Formato {#format}

```xml
config:= mode ":" processorName options*;
mode:= "default" | "min";
processorName := "none" | <name>;
options := ";" option;
option := name "=" value;
```

#### Compressore YUI per la riduzione CSS e GCC per JS {#yui-compressor-for-css-minification-and-gcc-for-js}

```xml
cssProcessor: ["default:none", "min:yui"]
jsProcessor: ["default:none", "min:gcc;compilationLevel=advanced"]
```

#### Typescript to Preprocess (Prepara da preelaborare) e poi GCC to Minify and Obfuscate (GCC per ridurre e rendere offuscato) {#typescript-to-preprocess-and-then-gcc-to-minify-and-obfuscate}

```xml
jsProcessor: [
   "default:typescript",
   "min:typescript",
   "min:gcc;obfuscate=true"
]
```

#### Opzioni GCC aggiuntive {#additional-gcc-options}

```xml
failOnWarning (defaults to "false")
languageIn (defaults to "ECMASCRIPT5")
languageOut (defaults to "ECMASCRIPT5")
compilationLevel (defaults to "simple") (can be "whitespace", "simple", "advanced")
```

Per ulteriori dettagli sulle opzioni GCC, consulta la documentazione [](https://developers.google.com/closure/compiler/docs/compilation_levels)GCC.

### Imposta minatore predefinito del sistema {#set-system-default-minifier}

YUI è impostato come minificatore predefinito in AEM. Per modificare questa impostazione in GCC, attenetevi alla procedura seguente.

1. Andate a Apache Felix Config Manager all&#39;indirizzo [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)
1. Trovate e modificate il **Adobe Granite HTML Library Manager**.
1. Abilitate l&#39;opzione **Miniatura** (se non è già attivata).
1. Impostate il valore **JS Processor Default Configs** su `min:gcc`.

   Le opzioni possono essere passate se separate da un punto e virgola, ad esempio `min:gcc;obfuscate=true`.

1. Click **Save** to save the changes.

## Strumenti di debug {#debugging-tools}

AEM fornisce diversi strumenti per il debug e il test delle cartelle della libreria client.

### Vedere File incorporati {#see-embedded-files}

Per tracciare l&#39;origine del codice incorporato o per assicurarsi che le librerie client incorporate producano i risultati previsti, è possibile visualizzare i nomi dei file che vengono incorporati in fase di esecuzione. Per visualizzare i nomi dei file, aggiungete il `debugClientLibs=true` parametro all’URL della pagina Web. La libreria generata contiene `@import` istruzioni invece del codice incorporato.

Nell&#39;esempio della sezione precedente [Incorporamento del codice da altre librerie](/help/sites-developing/clientlibs.md#embedding-code-from-other-libraries) , la cartella della libreria `/etc/client/libraries/myclientlibs/publicmain` client incorpora la cartella della libreria `/apps/myapp/clientlib` client. L&#39;aggiunta del parametro alla pagina Web genera il seguente collegamento nel codice sorgente della pagina Web:

```xml
<link rel="stylesheet" href="/etc/clientlibs/mycientlibs/publicmain.css">
```

Quando si apre il `publicmain.css` file viene visualizzato il seguente codice:

```xml
@import url("/apps/myapp/clientlib/styles/main.css");
```

1. Nella casella dell’indirizzo del browser Web, aggiungete il testo seguente all’URL del codice HTML:

   `?debugClientLibs=true`
1. Quando la pagina viene caricata, visualizzate l’origine della pagina.
1. Fare clic sul collegamento fornito come href per l&#39;elemento di collegamento per aprire il file e visualizzare il codice sorgente.

### Scopri librerie client {#discover-client-libraries}

Il `/libs/cq/granite/components/dumplibs/dumplibs` componente genera una pagina di informazioni su tutte le cartelle della libreria client nel sistema. Il `/libs/granite/ui/content/dumplibs` nodo ha il componente come tipo di risorsa. Per aprire la pagina, usate il seguente URL (modificando l’host e la porta come richiesto):

`https://<host>:<port>/libs/granite/ui/content/dumplibs.test.html`

Le informazioni includono il percorso e il tipo della libreria (CSS o JS) e i valori degli attributi della libreria, come categorie e dipendenze. Le tabelle successive della pagina mostrano le librerie in ogni categoria e canale.

### Vedere Output generato {#see-generated-output}

Il `dumplibs` componente include un selettore di test che visualizza il codice sorgente generato per `ui:includeClientLib` i tag. La pagina include il codice per diverse combinazioni di attributi js, css e a tema.

1. Per aprire la pagina Test Output, utilizzare uno dei metodi seguenti:

   * Dalla `dumplibs.html` pagina, fai clic sul collegamento nel **clic qui per il testo di prova** dell’output.

   * Aprite il seguente URL nel browser Web (utilizzate un host e una porta diversi come richiesto):

      * `http://<host>:<port>/libs/granite/ui/content/dumplibs.html`

   La pagina predefinita mostra l&#39;output per i tag senza valore per l&#39;attributo category.

1. Per visualizzare l&#39;output di una categoria, digitare il valore della `categories` proprietà della libreria client e fare clic su **Invia query**.

## Configurazione della gestione della libreria per lo sviluppo e la produzione {#configuring-library-handling-for-development-and-production}

Il servizio HTML Library Manager elabora `cq:ClientLibraryFolder` i tag e genera le librerie in fase di esecuzione. Il tipo di ambiente, sviluppo o produzione determina la modalità di configurazione del servizio:

* Maggiore protezione: Disabilita debugging
* Prestazioni migliorate: Rimuovete gli spazi bianchi e comprimete le librerie.
* Maggiore leggibilità: Includete gli spazi bianchi e non comprimete.

Per informazioni sulla configurazione del servizio, vedere [AEM HTML Library Manager](/help/sites-deploying/osgi-configuration-settings.md#aemhtmllibrarymanager).
