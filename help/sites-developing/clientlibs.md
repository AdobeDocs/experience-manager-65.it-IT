---
title: Utilizzo delle librerie lato client
description: AEM fornisce cartelle di librerie lato client, che consentono di memorizzare il codice lato client nell’archivio, organizzarlo in categorie e definire quando e come ogni categoria di codice deve essere trasmessa al client
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
docset: aem65
exl-id: 408ac30c-60ab-4d6c-855c-d544af8d5cf9
solution: Experience Manager, Experience Manager Sites
feature: Developing,Personalization
role: Developer
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '2791'
ht-degree: 1%

---

# Utilizzo delle librerie lato client{#using-client-side-libraries}

I siti web moderni si basano in larga misura sull’elaborazione lato client guidata da codice JavaScript e CSS complesso. L’organizzazione e l’ottimizzazione della trasmissione di questo codice possono essere un problema complesso.

Per risolvere questo problema, AEM fornisce **Cartelle libreria lato client**, che consente di memorizzare il codice lato client nell&#39;archivio, organizzarlo in categorie e definire quando e come ogni categoria di codice deve essere servita al client. Il sistema di librerie lato client si occupa quindi di generare i collegamenti corretti nella pagina web finale per caricare il codice corretto.

## Funzionamento delle librerie lato client in AEM {#how-client-side-libraries-work-in-aem}

Il modo standard per includere una libreria lato client (ovvero un file JS o CSS) nel HTML di una pagina consiste semplicemente nell&#39;includere un tag `<script>` o `<link>` nella JSP per quella pagina, contenente il percorso del file in questione. Ad esempio:

```xml
...
<head>
   ...
   <script type="text/javascript" src="/etc/clientlibs/granite/jquery/source/1.8.1/jquery-1.8.1.js"></script>
   ...
</head>
...
```

Anche se questo approccio funziona nell’AEM, può causare problemi quando le pagine e i relativi componenti diventano complessi. In questi casi esiste il pericolo che più copie della stessa libreria JS possano essere incluse nell’output HTML finale. Per evitare questo problema e consentire l&#39;organizzazione logica delle librerie lato client, l&#39;AEM utilizza **cartelle di librerie lato client**.

Una cartella di libreria lato client è un nodo di repository di tipo `cq:ClientLibraryFolder`. La sua definizione nella [notazione CND](https://jackrabbit.apache.org/node-type-notation.html) è

```shell
[cq:ClientLibraryFolder] > sling:Folder
  - dependencies (string) multiple
  - categories (string) multiple
  - embed (string) multiple
  - channels (string) multiple
```

Per impostazione predefinita, i nodi `cq:ClientLibraryFolder` possono trovarsi ovunque nelle sottostrutture `/apps`, `/libs` e `/etc` dell&#39;archivio (queste impostazioni predefinite e altre impostazioni possono essere controllate tramite il pannello **Adobe Granite HTML Library Manager** della [Console di sistema](https://localhost:4502/system/console/configMgr)).

Ogni `cq:ClientLibraryFolder` è compilato con un set di file JS e/o CSS, insieme ad alcuni file di supporto (vedi sotto). Le proprietà di `cq:ClientLibraryFolder` sono configurate come segue:

* `categories`: identifica le categorie in cui rientra il set di file JS e/o CSS in `cq:ClientLibraryFolder`. La proprietà `categories`, essendo multivalore, consente a una cartella di libreria di far parte di più di una categoria (vedere di seguito per informazioni sull&#39;utilità di questa proprietà).

* `dependencies`: questo è un elenco di altre categorie di librerie client da cui dipende la cartella della libreria. Ad esempio, dati due nodi `cq:ClientLibraryFolder` `F` e `G`, se un file in `F` richiede un altro file in `G` per funzionare correttamente, almeno uno dei `categories` di `G` deve essere tra i `dependencies` di `F`.

* `embed`: utilizzato per incorporare il codice da altre librerie. Se il nodo F incorpora i nodi G e H, il HTML risultante sarà una concentrazione di contenuto dai nodi G e H.
* `allowProxy`: se una libreria client si trova in `/apps`, questa proprietà consente l&#39;accesso tramite servlet proxy. Consulta [Individuazione di una cartella di librerie client e utilizzo del servlet delle librerie client proxy](/help/sites-developing/clientlibs.md#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet) di seguito.

## Riferimento a librerie lato client {#referencing-client-side-libraries}

Poiché HTL è la tecnologia preferita per lo sviluppo dei siti AEM, deve essere utilizzato per includere le librerie lato client nell’AEM. Tuttavia, è anche possibile farlo utilizzando JSP.

### Utilizzo di HTL {#using-htl}

In HTL, le librerie client vengono caricate tramite un modello helper fornito da AEM, a cui è possibile accedere tramite [`data-sly-use`](https://helpx.adobe.com/experience-manager/htl/using/block-statements.html#use). In questo file sono disponibili tre modelli, che possono essere richiamati tramite [`data-sly-call`](https://helpx.adobe.com/experience-manager/htl/using/block-statements.html#template-call):

* **css** - Carica solo i file CSS delle librerie client di riferimento.
* **js** - Carica solo i file JavaScript delle librerie client di riferimento.
* **all** - Carica tutti i file delle librerie client di riferimento (sia CSS che JavaScript).

Ogni modello helper richiede un’opzione `categories` per fare riferimento alle librerie client desiderate. Tale opzione può essere una matrice di valori stringa o una stringa contenente un elenco di valori separati da virgola.

Per ulteriori dettagli ed esempi di utilizzo, vedi il documento [Guida introduttiva a HTML Template Language](https://helpx.adobe.com/experience-manager/htl/using/getting-started.html#loading-client-libraries).

### Utilizzo di JSP {#using-jsp}

Aggiungi un tag `ui:includeClientLib` al codice JSP per aggiungere un collegamento alle librerie client nella pagina HTML generata. Per fare riferimento alle librerie, utilizzare il valore della proprietà `categories` del nodo `ui:includeClientLib`.

```
<%@taglib prefix="ui" uri="https://www.adobe.com/taglibs/granite/ui/1.0" %>
<ui:includeClientLib categories="<%= categories %>" />
```

Ad esempio, il nodo `/etc/clientlibs/foundation/jquery` è di tipo `cq:ClientLibraryFolder` con una proprietà Categories di valore `cq.jquery`. Il codice seguente in un file JSP fa riferimento alle librerie:

```xml
<ui:includeClientLib categories="cq.jquery"/>
```

La pagina HTML generata contiene il seguente codice:

```xml
<script type="text/javascript" src="/etc/clientlibs/foundation/jquery.js"></script>
```

Per informazioni complete, inclusi gli attributi per filtrare le librerie JS, CSS o theme, vedi [ui:includeClientLib](/help/sites-developing/taglib.md#lt-ui-includeclientlib).

>[!CAUTION]
>
>`<cq:includeClientLib>`, che in passato veniva comunemente utilizzato per includere le librerie client, è stato dichiarato obsoleto a partire da AEM 5.6. Utilizzare [`<ui:includeClientLib>`](/help/sites-developing/taglib.md#lt-ui-includeclientlib) come descritto in precedenza.

## Creazione di cartelle di librerie client {#creating-client-library-folders}

Crea un nodo `cq:ClientLibraryFolder` per definire le librerie dei fogli di stile JavaScript e Cascading e renderle disponibili per le pagine HTML. Utilizzare la proprietà `categories` del nodo per identificare le categorie di libreria a cui appartiene.

Il nodo contiene uno o più file di origine che, in fase di esecuzione, vengono uniti in un singolo file JS e/o CSS. Il nome del file generato è il nome del nodo con estensione `.js` o `.css`. Ad esempio, il nodo della libreria denominato `cq.jquery` genera il file generato denominato `cq.jquery.js` o `cq.jquery.css`.

Le cartelle delle librerie client contengono i seguenti elementi:

* I file sorgente JS e/o CSS da unire.
* Risorse che supportano gli stili CSS, ad esempio i file di immagine.

  **Nota:** è possibile utilizzare le sottocartelle per organizzare i file di origine.
* Un file `js.txt` e/o un file `css.txt` che identifica i file di origine da unire nei file JS e/o CSS generati.

![clientlibarch](assets/clientlibarch.png)

Per informazioni sui requisiti specifici delle librerie client per i widget, vedere [Utilizzo ed estensione dei widget](/help/sites-developing/widgets.md).

Il client Web deve disporre delle autorizzazioni per accedere al nodo `cq:ClientLibraryFolder`. Puoi anche esporre le librerie da aree protette dell’archivio (vedi Incorporazione di codice da altre librerie, di seguito).

### Sovrascrittura delle librerie in /lib {#overriding-libraries-in-lib}

Le cartelle della libreria client che si trovano sotto `/apps` hanno la precedenza rispetto alle cartelle con lo stesso nome che si trovano in `/libs`. `/apps/cq/ui/widgets`, ad esempio, ha la precedenza su `/libs/cq/ui/widgets`. Quando queste librerie appartengono alla stessa categoria, viene utilizzata la libreria seguente `/apps`.

### Individuazione di una cartella di librerie client e utilizzo del servlet delle librerie client proxy {#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet}

Nelle versioni precedenti, le cartelle della libreria client si trovavano sotto `/etc/clientlibs` nell&#39;archivio. Questo è ancora supportato, tuttavia si consiglia di individuare le librerie client in `/apps`. Questo consente di individuare le librerie client in prossimità degli altri script, che si trovano generalmente sotto `/apps` e `/libs`.

>[!NOTE]
>
>Le risorse statiche nella cartella della libreria client devono trovarsi in una cartella denominata *resources*. Se non disponi di risorse statiche, come immagini, nella cartella *resources*, non puoi farvi riferimento in un&#39;istanza pubblicata. Ecco un esempio: https://localhost:4503/etc.clientlibs/geometrixx/components/clientlibs/resources/example.gif

>[!NOTE]
>
>Per isolare meglio il codice dal contenuto e dalla configurazione, si consiglia di individuare le librerie client in `/apps` ed esporle tramite `/etc.clientlibs` utilizzando la proprietà `allowProxy`.

Per rendere accessibili le librerie client in `/apps`, viene utilizzato un servlet proxy. Gli ACL sono ancora applicati nella cartella della libreria client, ma il servlet consente la lettura del contenuto tramite `/etc.clientlibs/` se la proprietà `allowProxy` è impostata su `true`.

È possibile accedere a una risorsa statica solo tramite il proxy, se si trova al di sotto di una risorsa nella cartella della libreria client.

Ad esempio:

* Hai una libreria client in `/apps/myproject/clientlibs/foo`
* È presente un&#39;immagine statica in `/apps/myprojects/clientlibs/foo/resources/icon.png`

Quindi impostare la proprietà `allowProxy` su `foo` su true.

* È quindi possibile richiedere `/etc.clientlibs/myprojects/clientlibs/foo.js`
* È quindi possibile fare riferimento all&#39;immagine tramite `/etc.clientlibs/myprojects/clientlibs/foo/resources/icon.png`

>[!CAUTION]
>
>Quando si utilizzano le librerie client abilitate al proxy, la configurazione del Dispatcher AEM può richiedere un aggiornamento per garantire che gli URI con le clientlibs dell’estensione siano consentiti.

>[!CAUTION]
>
>L&#39;Adobe consiglia di individuare le librerie client in `/apps` e di renderle disponibili utilizzando il servlet proxy. Tuttavia, è importante tenere presente che la best practice richiede comunque che i siti pubblici non includano mai elementi che vengono serviti direttamente in un percorso `/apps` o `/libs`.

### Creare una cartella della libreria client {#create-a-client-library-folder}

1. Apri CRXDE Lite in un browser Web ([https://localhost:4502/crx/de](https://localhost:4502/crx/de)).
1. Selezionare la cartella in cui individuare la cartella della libreria client e fare clic su **Crea > Crea nodo**.
1. Immettere un nome per il file di libreria e nell&#39;elenco Tipo selezionare `cq:ClientLibraryFolder`. Fare clic su **OK** e quindi su **Salva tutto**.
1. Per specificare la categoria o le categorie a cui appartiene la libreria, selezionare il nodo `cq:ClientLibraryFolder`, aggiungere la seguente proprietà e quindi fare clic su **Salva tutto**:

   * Nome: categorie
   * Tipo: String
   * Valore: il nome della categoria
   * Multiplo: Seleziona

1. Aggiungere i file di origine alla cartella della libreria in qualsiasi modo. Ad esempio, utilizza un client WebDav per copiare i file oppure crea un file e crea il contenuto manualmente.

   **Nota:** Se lo desideri, puoi organizzare i file di origine in sottocartelle.

1. Selezionare la cartella della libreria client e fare clic su **Crea > Crea file**.
1. Nella casella Nome file digitare uno dei seguenti nomi di file e fare clic su OK:

   * **`js.txt`:** Utilizzare questo nome di file per generare un file JavaScript.
   * **`css.txt`:** Utilizzare questo nome di file per generare un foglio di stile CSS.

1. Apri il file e digita il testo seguente per identificare la directory principale del percorso dei file di origine:

   `#base=*[root]*`

   Sostituire * `[root]`* con il percorso della cartella che contiene i file di origine, relativo al file TXT. Ad esempio, utilizza il testo seguente quando i file di origine si trovano nella stessa cartella del file TXT:

   `#base=.`

   Il codice seguente imposta la radice come cartella denominata mobile sotto il nodo `cq:ClientLibraryFolder`:

   `#base=mobile`

1. Nelle righe sottostanti `#base=[root]`, digitare i percorsi dei file di origine relativi alla radice. Posizionare ogni nome di file su una riga separata.
1. Fare clic su **Salva tutto**.

### Collegamento alle dipendenze {#linking-to-dependencies}

Quando il codice nella cartella della libreria client fa riferimento ad altre librerie, identifica le altre librerie come dipendenze. Nel JSP, il tag `ui:includeClientLib` che fa riferimento alla cartella della libreria client fa in modo che il codice HTML includa un collegamento al file di libreria generato e alle dipendenze.

Le dipendenze devono essere un altro `cq:ClientLibraryFolder`. Per identificare le dipendenze, aggiungere una proprietà al nodo `cq:ClientLibraryFolder` con i seguenti attributi:

* **Nome:** dipendenze
* **Tipo:** Stringa[]
* **Valori:** il valore della proprietà Categories del nodo cq:ClientLibraryFolder da cui dipende la cartella della libreria corrente.

Ad esempio, / `etc/clientlibs/myclientlibs/publicmain` ha una dipendenza dalla libreria `cq.jquery`. La JSP che fa riferimento alla libreria client principale genera HTML che include il seguente codice:

```xml
<script src="/etc/clientlibs/foundation/cq.jquery.js" type="text/javascript">
<script src="/etc/clientlibs/mylibs/publicmain.js" type="text/javascript">
```

### Incorporazione Di Codice Da Altre Librerie {#embedding-code-from-other-libraries}

Puoi incorporare il codice da una libreria client a un’altra libreria client. In fase di esecuzione, i file JS e CSS generati della libreria di incorporamento includono il codice della libreria incorporata.

L’incorporamento del codice è utile per fornire accesso alle librerie memorizzate in aree protette dell’archivio.

#### Cartelle Libreria Client Specifiche Per L&#39;App {#app-specific-client-library-folders}

È consigliabile mantenere tutti i file relativi all&#39;applicazione nella cartella dell&#39;applicazione al di sotto di `/apps`. È inoltre consigliabile negare l&#39;accesso alla cartella `/apps` ai visitatori del sito Web. Per soddisfare entrambe le best practice, creare una cartella della libreria client sotto `/apps` e renderla accessibile tramite il servlet proxy come descritto in [Individuazione di una cartella della libreria client e utilizzo del servlet delle librerie client proxy](/help/sites-developing/clientlibs.md#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet).

Utilizzare la proprietà Categories per identificare la cartella della libreria client da incorporare. Per incorporare la libreria, aggiungere una proprietà al nodo `cq:ClientLibraryFolder` che incorpora, utilizzando i seguenti attributi di proprietà:

* **Nome:** incorporato
* **Tipo:** Stringa[]
* **Valore:** il valore della proprietà Categories del nodo `cq:ClientLibraryFolder` da incorporare.

#### Utilizzo dell’incorporamento per ridurre al minimo le richieste {#using-embedding-to-minimize-requests}

In alcuni casi è possibile che il HTML finale generato per la pagina tipica dall&#39;istanza Publish includa un numero relativamente elevato di elementi `<script>`, in particolare se il sito utilizza informazioni sul contesto client per l&#39;analisi o il targeting. In un progetto non ottimizzato, ad esempio, è possibile trovare la seguente serie di elementi `<script>` nel HTML per una pagina:

```xml
<script type="text/javascript" src="/etc/clientlibs/granite/jquery.js"></script>
<script type="text/javascript" src="/etc/clientlibs/granite/utils.js"></script>
<script type="text/javascript" src="/etc/clientlibs/granite/jquery/granite.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/jquery.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/shared.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/personalization/kernel.js"></script>
```

In questi casi, può essere utile combinare in un unico file tutto il codice libreria client richiesto, in modo da ridurre il numero di richieste avanti e indietro al caricamento della pagina. A questo scopo, puoi `embed` le librerie richieste nella libreria client specifica per l&#39;app utilizzando la proprietà embed del nodo `cq:ClientLibraryFolder`.

Le seguenti categorie di librerie client sono incluse con AEM. Devi incorporare solo quelli necessari per il funzionamento del tuo particolare sito. Tuttavia, **devi mantenere l&#39;ordine elencato qui**:

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

Quando incorpori file CSS, il codice CSS generato utilizza i percorsi delle risorse relativi alla libreria di incorporamento. Ad esempio, la libreria `/etc/client/libraries/myclientlibs/publicmain` accessibile al pubblico incorpora la libreria client `/apps/myapp/clientlib`:

![schermata_shot_2012-05-29at20122pm](assets/screen_shot_2012-05-29at20122pm.png)

Il file `main.css` contiene il seguente stile:

```xml
body {
  padding: 0;
  margin: 0;
  background: url(images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

Il file CSS generato dal nodo `publicmain` contiene il seguente stile, che utilizza l&#39;URL dell&#39;immagine originale:

```xml
body {
  padding: 0;
  margin: 0;
  background: url(../../../apps/myapp/clientlib/styles/images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

### Utilizzo di una libreria per gruppi mobili specifici {#using-a-library-for-specific-mobile-groups}

Utilizzare la proprietà `channels` di una cartella della libreria client per identificare il gruppo mobile che utilizza la libreria. La proprietà `channels` è utile quando le librerie della stessa categoria sono progettate per funzionalità di dispositivi diverse.

Per associare una cartella della libreria client a un gruppo di dispositivi, aggiungere una proprietà al nodo `cq:ClientLibraryFolder` con i seguenti attributi:

* **Nome:** canali
* **Tipo:** Stringa[]
* **Valori:** il nome del gruppo mobile. Per escludere la cartella della libreria da un gruppo, aggiungi al nome un punto esclamativo (&quot;!&quot;).

Nella tabella seguente, ad esempio, viene elencato il valore della proprietà `channels` per ogni cartella della libreria client della categoria `cq.widgets`:

| Cartella libreria client | Valore della proprietà dei canali |
|---|---|
| `/libs/cq/analytics/widgets` | `!touch` |
| `/libs/cq/analytics/widgets/themes/default` | `!touch` |
| `/libs/cq/cloudserviceconfigs/widgets` | `!touch` |
| `/libs/cq/touch/widgets` | `touch` |
| `/libs/cq/touch/widgets/themes/default` | `touch` |
| `/libs/cq/ui/widgets` | `!touch` |
| `/libs/cq/ui/widgets/themes/default` | `!touch` |

<!-- Search&Promote is end of life as of September 1, 2022 | `/libs/cq/searchpromote/widgets` | `!touch` | -->
<!-- Search&Promote is end of life as of September 1, 2022 | `/libs/cq/searchpromote/widgets/themes/default` |*[no value]* -->

## Utilizzo dei preprocessori {#using-preprocessors}

AEM consente preprocessori collegabili e viene fornito con il supporto per [Compressore YUI](https://github.com/yui/yuicompressor#yui-compressor---the-yahoo-javascript-and-css-compressor) per CSS e JavaScript e [Compilatore di chiusura Google (GCC)](https://developers.google.com/closure/compiler/) per JavaScript con YUI impostato come preprocessore predefinito dell&#39;AEM.

I preprocessori collegabili consentono un utilizzo flessibile, tra cui:

* Definizione di ScriptProcessors che possono elaborare origini script
* I processori sono configurabili con opzioni
* I processori possono essere utilizzati per la minimizzazione, ma anche per i casi non minimizzati
* La libreria client può definire quale processore utilizzare

>[!NOTE]
>
>Per impostazione predefinita, l’AEM utilizza il compressore YUI. Per un elenco dei problemi noti, consulta la [documentazione GitHub per il compressore YUI](https://github.com/yui/yuicompressor/issues). Il passaggio al compressore GCC per particolari clientlibs può risolvere alcuni problemi osservati durante l’utilizzo di YUI.

>[!CAUTION]
>
>Non inserire una libreria minimizzata in una libreria client. Fornisci invece la libreria raw e, se è richiesta la minimizzazione, utilizza le opzioni dei preprocessori.

### Utilizzo {#usage}

È possibile scegliere di configurare la configurazione dei preprocessori per libreria client o a livello di sistema.

* Aggiungere le proprietà multivalore `cssProcessor` e `jsProcessor` nel nodo clientlibrary

* Oppure definisci la configurazione predefinita del sistema tramite la configurazione OSGi di **HTML Library Manager**

Una configurazione del preprocessore sul nodo clientlib ha la precedenza sulla configurazione OSGI.

### Formato ed esempi {#format-and-examples}

#### Formato {#format}

```xml
config:= mode ":" processorName options*;
mode:= "default" | "min";
processorName := "none" | <name>;
options := ";" option;
option := name "=" value;
```

#### Compressore YUI per minimizzazione CSS e GCC per JS {#yui-compressor-for-css-minification-and-gcc-for-js}

```xml
cssProcessor: ["default:none", "min:yui"]
jsProcessor: ["default:none", "min:gcc;compilationLevel=advanced"]
```

#### Script da pre-elaborare e poi GCC da minimizzare e oscurare {#typescript-to-preprocess-and-then-gcc-to-minify-and-obfuscate}

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

Per ulteriori dettagli sulle opzioni GCC, consulta la [documentazione GCC](https://developers.google.com/closure/compiler/docs/compilation_levels).

### Imposta minimizzatore predefinito di sistema {#set-system-default-minifier}

YUI è impostato come minimizzatore predefinito in AEM. Per cambiare in GCC, segui la procedura riportata di seguito.

1. Vai a Apache Felix Config Manager all&#39;indirizzo [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)
1. Trova e modifica **Adobe Granite HTML Library Manager**.
1. Abilita l&#39;opzione **Minify** (se non già abilitata).
1. Imposta il valore **Configurazioni predefinite processore JS** su `min:gcc`.

   Le opzioni possono essere passate se separate da un punto e virgola, ad esempio `min:gcc;obfuscate=true`.

1. Fai clic su **Salva** per salvare le modifiche.

## Strumenti di debug {#debugging-tools}

AEM fornisce diversi strumenti per il debug e il test delle cartelle delle librerie client.

### Vedi File incorporati {#see-embedded-files}

Per tracciare l’origine del codice incorporato o per garantire che le librerie client incorporate producano i risultati previsti, puoi visualizzare i nomi dei file incorporati in fase di esecuzione. Per visualizzare i nomi dei file, aggiungi il parametro `debugClientLibs=true` all&#39;URL della pagina Web. La libreria generata contiene `@import` istruzioni invece del codice incorporato.

Nell&#39;esempio della precedente sezione [Incorporazione di codice da altre librerie](/help/sites-developing/clientlibs.md#embedding-code-from-other-libraries), la cartella della libreria client `/etc/client/libraries/myclientlibs/publicmain` incorpora la cartella della libreria client `/apps/myapp/clientlib`. L’aggiunta del parametro alla pagina web genera il seguente collegamento nel codice sorgente della pagina web:

```xml
<link rel="stylesheet" href="/etc/clientlibs/mycientlibs/publicmain.css">
```

L&#39;apertura del file `publicmain.css` rivela il seguente codice:

```xml
@import url("/apps/myapp/clientlib/styles/main.css");
```

1. Nella casella dell’indirizzo del browser web, aggiungi il testo seguente all’URL del tuo HTML:

   `?debugClientLibs=true`
1. Al caricamento della pagina, visualizza l’origine della pagina.
1. Fai clic sul collegamento fornito come href per l’elemento collegamento per aprire il file e visualizzare il codice sorgente.

### Scopri le librerie client {#discover-client-libraries}

Il componente `/libs/cq/granite/components/dumplibs/dumplibs` genera una pagina di informazioni su tutte le cartelle delle librerie client nel sistema. Il nodo `/libs/granite/ui/content/dumplibs` ha il componente come tipo di risorsa. Per aprire la pagina, utilizza il seguente URL (modificando l’host e la porta come richiesto):

`https://<host>:<port>/libs/granite/ui/content/dumplibs.test.html`

Le informazioni includono il percorso e il tipo della libreria (CSS o JS) e i valori degli attributi della libreria, come categorie e dipendenze. Le tabelle successive nella pagina mostrano le librerie in ogni categoria e canale.

### Vedi Output generato {#see-generated-output}

Il componente `dumplibs` include un selettore di test che visualizza il codice sorgente generato per i tag `ui:includeClientLib`. La pagina include il codice per diverse combinazioni di attributi js, css e a tema.

1. Per aprire la pagina Output test, utilizzare uno dei metodi seguenti:

   * Dalla pagina `dumplibs.html`, fai clic sul collegamento nel testo **Fai clic qui per il test dell&#39;output**.

   * Apri il seguente URL nel browser web (utilizza un host e una porta diversi, a seconda delle necessità):

      * `http://<host>:<port>/libs/granite/ui/content/dumplibs.html`

   La pagina predefinita mostra l’output per i tag senza alcun valore per l’attributo categorie.

1. Per visualizzare l&#39;output di una categoria, digitare il valore della proprietà `categories` della libreria client e fare clic su **Invia query**.

## Configurazione della gestione della libreria per lo sviluppo e la produzione {#configuring-library-handling-for-development-and-production}

Il servizio HTML Library Manager elabora i tag `cq:ClientLibraryFolder` e genera le librerie in fase di esecuzione. Il tipo di ambiente, sviluppo o produzione determina come configurare il servizio:

* Aumentare la sicurezza: disabilitare il debug
* Migliorare le prestazioni: rimuovi gli spazi vuoti e comprimi le librerie.
* Migliora la leggibilità: includi gli spazi vuoti e non comprimi.

Per informazioni sulla configurazione del servizio, vedere [Gestione libreria HTML AEM](/help/sites-deploying/osgi-configuration-settings.md#aemhtmllibrarymanager).
