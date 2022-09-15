---
title: Utilizzo delle librerie lato client
seo-title: Using Client-Side Libraries
description: AEM fornisce Cartelle libreria lato client, che consentono di memorizzare il codice lato client nell’archivio, organizzarlo in categorie e definire quando e come ogni categoria di codice deve essere trasmessa al client
seo-description: AEM provides Client-side Library Folders, which allow you to store your client-side code in the repository, organize it into categories, and define when and how each category of code is to be served to the client
uuid: f12b13cc-6651-4c9a-9c52-19a22bb82b28
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 3d14837d-41a8-480a-83ba-392e32f84c65
docset: aem65
exl-id: 408ac30c-60ab-4d6c-855c-d544af8d5cf9
source-git-commit: 7ceee6819618d785f04029b9ac1c6f763995b3ac
workflow-type: tm+mt
source-wordcount: '2861'
ht-degree: 2%

---

# Utilizzo delle librerie lato client{#using-client-side-libraries}

I siti web moderni si basano fortemente sull’elaborazione lato client basata su codice JavaScript e CSS complessi. Organizzare e ottimizzare il servizio di questo codice può essere un problema complicato.

Per risolvere questo problema, AEM fornisce **Cartelle libreria lato client**, che ti consente di memorizzare il codice lato client nell’archivio, organizzarlo in categorie e definire quando e come ogni categoria di codice deve essere trasmessa al client. Il sistema di libreria lato client si occupa quindi di produrre i collegamenti corretti nella pagina Web finale per caricare il codice corretto.

## Funzionamento delle librerie lato client in AEM {#how-client-side-libraries-work-in-aem}

Il modo standard per includere una libreria lato client (cioè un file JS o CSS) nel HTML di una pagina è semplicemente quello di includere un `<script>` o `<link>` nel JSP per quella pagina, contenente il percorso del file in questione. Ad esempio:

```xml
...
<head>
   ...
   <script type="text/javascript" src="/etc/clientlibs/granite/jquery/source/1.8.1/jquery-1.8.1.js"></script>
   ...
</head>
...
```

Anche se questo approccio funziona in AEM, può causare problemi quando le pagine e i loro componenti diventano complessi. In tali casi esiste il pericolo che più copie della stessa libreria JS possano essere incluse nell’output finale di HTML. Per evitare questo problema e consentire l’organizzazione logica delle librerie lato client AEM utilizza **cartelle libreria lato client**.

Una cartella libreria lato client è un nodo del repository di tipo `cq:ClientLibraryFolder`. È una definizione in [Notazione CND](https://jackrabbit.apache.org/node-type-notation.html) è

```shell
[cq:ClientLibraryFolder] > sling:Folder
  - dependencies (string) multiple
  - categories (string) multiple
  - embed (string) multiple
  - channels (string) multiple
```

Per impostazione predefinita, `cq:ClientLibraryFolder` i nodi possono essere posizionati in qualsiasi punto `/apps`, `/libs` e `/etc` le sottostrutture dell’archivio (queste impostazioni predefinite e altre impostazioni possono essere controllate tramite **Adobe Granite HTML Library Manager** pannello [Console di sistema](https://localhost:4502/system/console/configMgr)).

Ogni `cq:ClientLibraryFolder` viene popolato con un set di file JS e/o CSS, insieme ad alcuni file di supporto (vedi di seguito). Proprietà delle `cq:ClientLibraryFolder` sono configurati come segue:

* `categories`: Identifica le categorie in cui il set di file JS e/o CSS all’interno di questo `cq:ClientLibraryFolder` cadere. La `categories` , con più valori, consente a una cartella libreria di far parte di più di una categoria (consulta di seguito per informazioni su come ciò possa essere utile).

* `dependencies`: Elenco di altre categorie della libreria client da cui dipende la cartella della libreria. Ad esempio, due `cq:ClientLibraryFolder` nodes `F` e `G`, se un file in `F` richiede un altro file in `G` per funzionare correttamente, almeno una delle `categories` di `G` devono essere tra i `dependencies` di `F`.

* `embed`: Utilizzato per incorporare il codice da altre librerie. Se il nodo F incorpora i nodi G e H, il HTML risultante sarà una concentrazione di contenuto dai nodi G e H.
* `allowProxy`: Se una libreria client si trova in `/apps`, questa proprietà consente l&#39;accesso a esso tramite servlet proxy. Vedi [Individuazione di una cartella della libreria client e utilizzo del servlet delle librerie client proxy](/help/sites-developing/clientlibs.md#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet) sotto.

## Riferimento a librerie lato client {#referencing-client-side-libraries}

Poiché HTL è la tecnologia preferita per lo sviluppo di siti AEM, HTL deve essere utilizzato per includere librerie lato client in AEM. Tuttavia è anche possibile farlo utilizzando JSP.

### Utilizzo di HTL {#using-htl}

In HTL, le librerie client vengono caricate tramite un modello helper fornito da AEM, a cui è possibile accedere tramite [ `data-sly-use`](https://helpx.adobe.com/experience-manager/htl/using/block-statements.html#use). In questo file sono disponibili tre modelli, che possono essere richiamati tramite [ `data-sly-call`](https://helpx.adobe.com/experience-manager/htl/using/block-statements.html#template-call):

* **css** - Carica solo i file CSS delle librerie client a cui viene fatto riferimento.
* **js** - Carica solo i file JavaScript delle librerie client a cui si fa riferimento.
* **tutto** - Carica tutti i file delle librerie client a cui si fa riferimento (sia CSS che JavaScript).

Ogni modello helper richiede un’opzione `categories` per fare riferimento alle librerie client desiderate. Tale opzione può essere una matrice di valori stringa o una stringa contenente un elenco di valori separati da virgola.

Per ulteriori dettagli ed esempi di utilizzo, consulta il documento [Guida introduttiva a HTML Template Language](https://helpx.adobe.com/experience-manager/htl/using/getting-started.html#loading-client-libraries).

### Utilizzo di JSP {#using-jsp}

Aggiungi un `ui:includeClientLib` aggiungi un tag al codice JSP per aggiungere un collegamento alle librerie client nella pagina HTML generata. Per fare riferimento alle librerie, utilizza il valore del `categories` proprietà `ui:includeClientLib` nodo.

```
<%@taglib prefix="ui" uri="https://www.adobe.com/taglibs/granite/ui/1.0" %>
<ui:includeClientLib categories="<%= categories %>" />
```

Ad esempio, il `/etc/clientlibs/foundation/jquery` il nodo è di tipo `cq:ClientLibraryFolder` con una proprietà categories di valore `cq.jquery`. Il seguente codice in un file JSP fa riferimento alle librerie:

```xml
<ui:includeClientLib categories="cq.jquery"/>
```

La pagina HTML generata contiene il seguente codice:

```xml
<script type="text/javascript" src="/etc/clientlibs/foundation/jquery.js"></script>
```

Per informazioni complete, inclusi gli attributi per filtrare JS, CSS o librerie di temi, vedi [ui:includeClientLib](/help/sites-developing/taglib.md#lt-ui-includeclientlib).

>[!CAUTION]
>
>`<cq:includeClientLib>`, che in passato veniva comunemente utilizzato per includere le librerie client, è stato dichiarato obsoleto a partire dalla AEM 5.6. [ `<ui:includeClientLib>`](/help/sites-developing/taglib.md#lt-ui-includeclientlib) devono essere utilizzati come descritto in precedenza.

## Creazione di cartelle della libreria client {#creating-client-library-folders}

Crea un `cq:ClientLibraryFolder` nodo per definire le librerie JavaScript e Cascading Style Sheet e renderle disponibili per le pagine di HTML. Utilizza la `categories` proprietà del nodo per identificare le categorie della libreria a cui appartiene.

Il nodo contiene uno o più file di origine che, in fase di runtime, vengono uniti in un singolo file JS e/o CSS. Il nome del file generato è il nome del nodo con il `.js` o `.css` estensione del nome file. Ad esempio, il nodo della libreria denominato `cq.jquery` restituisce il file generato denominato `cq.jquery.js` o `cq.jquery.css`.

Le cartelle della libreria client contengono i seguenti elementi:

* I file di origine JS e/o CSS da unire.
* Risorse che supportano gli stili CSS, ad esempio i file di immagine.

   **Nota:** È possibile utilizzare le sottocartelle per organizzare i file di origine.
* Uno `js.txt` file e/o uno `css.txt` file che identifica i file di origine da unire nei file JS e/o CSS generati.

![clientlibarch](assets/clientlibarch.png)

Per informazioni sui requisiti specifici delle librerie client per i widget, consulta [Utilizzo ed estensione dei Widget](/help/sites-developing/widgets.md).

Il client web deve disporre delle autorizzazioni di accesso al `cq:ClientLibraryFolder` nodo. Puoi anche esporre le librerie dalle aree protette dell’archivio (consulta Incorporamento di codice da altre librerie, di seguito).

### Sovrascrittura delle librerie in /lib {#overriding-libraries-in-lib}

Cartelle della libreria client situate sotto `/apps` hanno la precedenza sulle cartelle con lo stesso nome che si trovano in modo simile in `/libs`. Ad esempio: `/apps/cq/ui/widgets` ha la precedenza `/libs/cq/ui/widgets`. Quando queste librerie appartengono alla stessa categoria, la libreria sottostante `/apps` viene utilizzato.

### Individuazione di una cartella della libreria client e utilizzo del servlet delle librerie client proxy {#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet}

Nelle versioni precedenti, le cartelle della libreria client si trovavano qui sotto `/etc/clientlibs` nel repository. Questo è ancora supportato, tuttavia si consiglia di individuare le librerie client in `/apps`. Questo per individuare le librerie client vicino agli altri script, che sono generalmente trovati di seguito `/apps` e `/libs`.

>[!NOTE]
>
>Le risorse statiche sotto la cartella della libreria client devono trovarsi in una cartella denominata *risorse*. Se la cartella non contiene le risorse statiche, ad esempio le immagini *risorse*, non può essere referenziato in un&#39;istanza di pubblicazione. Ecco un esempio: https://localhost:4503/etc.clientlibs/geometrixx/components/clientlibs/resources/example.gif

>[!NOTE]
>
>Per isolare meglio il codice dal contenuto e dalla configurazione, si consiglia di individuare le librerie client in `/apps` e li espongono tramite `/etc.clientlibs` sfruttando le `allowProxy` proprietà.

Per le librerie client in `/apps` per essere accessibile, viene utilizzato un servlet proxy. Le ACL sono ancora applicate nella cartella della libreria client, ma il servlet consente la lettura del contenuto tramite `/etc.clientlibs/` se `allowProxy` è impostata su `true`.

È possibile accedere a una risorsa statica tramite il proxy solo se si trova sotto una risorsa sotto la cartella della libreria client.

Ad esempio:

* Hai una clientlib in `/apps/myproject/clientlibs/foo`
* Hai un&#39;immagine statica in `/apps/myprojects/clientlibs/foo/resources/icon.png`

Quindi imposta la `allowProxy` proprietà su `foo` su true.

* È quindi possibile richiedere `/etc.clientlibs/myprojects/clientlibs/foo.js`
* È quindi possibile fare riferimento all&#39;immagine tramite `/etc.clientlibs/myprojects/clientlibs/foo/resources/icon.png`

>[!CAUTION]
>
>Quando si utilizzano librerie client proxy, la configurazione di Dispatcher AEM potrebbe richiedere un aggiornamento per garantire che siano consentiti gli URI con le clientlibs dell’estensione.

>[!CAUTION]
>
>Adobe consiglia di individuare le librerie client in `/apps` e renderli disponibili utilizzando il servlet proxy. Tuttavia, ricorda che la migliore pratica richiede ancora che i siti pubblici non includano mai ciò che viene servito direttamente su un `/apps` o `/libs` percorso.

### Creare una cartella della libreria client {#create-a-client-library-folder}

1. Apri CRXDE Lite in un browser Web ([https://localhost:4502/crx/de](https://localhost:4502/crx/de)).
1. Selezionare la cartella in cui si desidera individuare la cartella della libreria client e fare clic su **Crea > Crea nodo**.
1. Immettere un nome per il file della libreria e selezionare nell&#39;elenco Tipo `cq:ClientLibraryFolder`. Fai clic su **OK** quindi fai clic su **Salva tutto**.
1. Per specificare la categoria o le categorie a cui appartiene la libreria, seleziona la `cq:ClientLibraryFolder` , aggiungi la seguente proprietà, quindi fai clic su **Salva tutto**:

   * Nome: categorie
   * Tipo: Stringa
   * Valore: Nome della categoria
   * Multi: Seleziona

1. Aggiungi i file di origine alla cartella della libreria in qualsiasi modo. Ad esempio, utilizza un client WebDav per copiare i file oppure crea un file e crea il contenuto manualmente.

   **Nota:** Se necessario, è possibile organizzare i file di origine in sottocartelle.

1. Seleziona la cartella della libreria client e fai clic su **Crea > Crea file**.
1. Nella casella Nome file digitare uno dei seguenti nomi di file e fare clic su OK:

   * **`js.txt`:** Usa questo nome file per generare un file JavaScript.
   * **`css.txt`:** Utilizzare questo nome file per generare un foglio di stile a cascata.

1. Apri il file e digita il seguente testo per identificare la radice del percorso dei file di origine:

   `#base=*[root]*`

   Sostituisci * `[root]`* con il percorso della cartella che contiene i file di origine, relativo al file TXT. Ad esempio, utilizzare il testo seguente quando i file di origine si trovano nella stessa cartella del file TXT:

   `#base=.`

   Il codice seguente imposta la radice come cartella denominata mobile sotto la `cq:ClientLibraryFolder` nodo:

   `#base=mobile`

1. Sulle linee seguenti `#base=[root]`, digita i percorsi dei file di origine relativi alla radice. Posizionare ogni nome di file su una riga separata.
1. Fai clic su **Salva tutto**.

### Collegamento a dipendenze {#linking-to-dependencies}

Quando il codice nella cartella della libreria client fa riferimento ad altre librerie, identifica le altre librerie come dipendenze. Nel JSP, la `ui:includeClientLib` Se si fa riferimento alla cartella della libreria client, il codice HTML include un collegamento al file della libreria generato e alle dipendenze.

Le dipendenze devono essere un&#39;altra `cq:ClientLibraryFolder`. Per identificare le dipendenze, aggiungi una proprietà al tuo `cq:ClientLibraryFolder` con i seguenti attributi:

* **Nome:** dipendenze
* **Tipo:** Stringa[]
* **Valori:** Il valore della proprietà categories del nodo cq:ClientLibraryFolder da cui dipende la cartella corrente della libreria.

Ad esempio, il / `etc/clientlibs/myclientlibs/publicmain` dipende da `cq.jquery` libreria. Il JSP che fa riferimento alla libreria client principale genera HTML che include il seguente codice:

```xml
<script src="/etc/clientlibs/foundation/cq.jquery.js" type="text/javascript">
<script src="/etc/clientlibs/mylibs/publicmain.js" type="text/javascript">
```

### Incorporazione Di Codice Da Altre Librerie {#embedding-code-from-other-libraries}

Puoi incorporare il codice da una libreria client in un&#39;altra libreria client. In fase di runtime, i file JS e CSS generati dalla libreria di incorporamento includono il codice della libreria incorporata.

L&#39;incorporamento del codice è utile per fornire l&#39;accesso alle librerie memorizzate nelle aree protette dell&#39;archivio.

#### Cartelle della libreria client specifiche per l’app {#app-specific-client-library-folders}

È consigliabile mantenere tutti i file relativi all’applicazione nella cartella dell’applicazione sottostante `/apps`. È inoltre consigliabile negare l’accesso ai visitatori del sito web `/apps` cartella. Per soddisfare entrambe le best practice, crea una cartella della libreria client di seguito `/apps`e renderlo accessibile tramite il servlet proxy come descritto in [Individuazione di una cartella della libreria client e utilizzo del servlet delle librerie client proxy](/help/sites-developing/clientlibs.md#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet).

Utilizzare la proprietà categories per identificare la cartella della libreria client da incorporare. Per incorporare la libreria, aggiungi una proprietà all&#39;incorporamento `cq:ClientLibraryFolder` utilizzando i seguenti attributi di proprietà:

* **Nome:** incorporare
* **Tipo:** Stringa[]
* **Valore:** Il valore della proprietà categories del `cq:ClientLibraryFolder` nodo da incorporare.

#### Utilizzo dell’incorporamento per ridurre al minimo le richieste {#using-embedding-to-minimize-requests}

In alcuni casi, potresti riscontrare che il HTML finale generato per la pagina tipica dall’istanza di pubblicazione include un numero relativamente elevato di `<script>` , in particolare se il sito utilizza informazioni di contesto client per l&#39;analisi o il targeting. Ad esempio, in un progetto non ottimizzato potresti trovare la seguente serie di `<script>` elementi in HTML per una pagina:

```xml
<script type="text/javascript" src="/etc/clientlibs/granite/jquery.js"></script>
<script type="text/javascript" src="/etc/clientlibs/granite/utils.js"></script>
<script type="text/javascript" src="/etc/clientlibs/granite/jquery/granite.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/jquery.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/shared.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/personalization/kernel.js"></script>
```

In questi casi, può essere utile combinare tutto il codice della libreria client richiesto in a un singolo file in modo che il numero di richieste avanti e indietro al caricamento della pagina venga ridotto. Per fare questo puoi `embed` le librerie richieste nella libreria client specifica dell’app tramite la proprietà embed della `cq:ClientLibraryFolder` nodo.

Le seguenti categorie di librerie client sono incluse in AEM. Devi incorporare solo quelli necessari per il funzionamento del tuo sito specifico. Tuttavia, **è necessario mantenere l&#39;ordine indicato qui**:

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

Quando incorpori file CSS, il codice CSS generato utilizza percorsi verso risorse relative alla libreria di incorporamento. Ad esempio, la libreria accessibile al pubblico `/etc/client/libraries/myclientlibs/publicmain` incorpora `/apps/myapp/clientlib` libreria client:

![screen_shot_2012-05-29at20122pm](assets/screen_shot_2012-05-29at20122pm.png)

La `main.css` il file contiene lo stile seguente:

```xml
body {
  padding: 0;
  margin: 0;
  background: url(images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

Il file CSS che `publicmain` node genera contiene il seguente stile, utilizzando l’URL dell’immagine originale:

```xml
body {
  padding: 0;
  margin: 0;
  background: url(../../../apps/myapp/clientlib/styles/images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

### Utilizzo di una libreria per gruppi mobili specifici {#using-a-library-for-specific-mobile-groups}

Utilizza la `channels` di una cartella libreria client per identificare il gruppo mobile che utilizza la libreria. La `channels` Questa proprietà è utile quando le librerie della stessa categoria sono progettate per diverse funzionalità dei dispositivi.

Per associare una cartella libreria client a un gruppo di dispositivi, aggiungi una proprietà al `cq:ClientLibraryFolder` con i seguenti attributi:

* **Nome:** canali
* **Tipo:** Stringa[]
* **Valori:** Nome del gruppo mobile. Per escludere la cartella della libreria da un gruppo, aggiungi al nome un punto esclamativo (&quot;!&quot;).

Ad esempio, nella tabella seguente viene elencato il valore di `channels` per ogni cartella della libreria client `cq.widgets` categoria:

| Cartella libreria client | Valore della proprietà channels |
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

AEM consente preprocessori inseribili e navi con supporto per [Compressore YUI](https://github.com/yui/yuicompressor#yui-compressor---the-yahoo-javascript-and-css-compressor) per CSS e JavaScript e [Google Closure Compiler (GCC)](https://developers.google.com/closure/compiler/) per JavaScript con YUI impostato come preprocessore predefinito AEM.

I preprocessori inseribili consentono un utilizzo flessibile, tra cui:

* Definizione di ScriptProcessors in grado di elaborare origini script
* I processori sono configurabili con le opzioni
* I processori possono essere utilizzati per la minimizzazione, ma anche per i casi non minimizzati
* clientlib può definire quale processore utilizzare

>[!NOTE]
>
>Per impostazione predefinita, AEM utilizza il compressore YUI. Consulta la sezione [Documentazione GitHub del compressore YUI](https://github.com/yui/yuicompressor/issues) per un elenco dei problemi noti. Il passaggio al compressore GCC per particolari clientlibs può risolvere alcuni problemi osservati quando si utilizza YUI.

>[!CAUTION]
>
>Non inserire una libreria minimizzata in una libreria client. Fornisci invece la libreria non elaborata e, se è necessaria la minimizzazione, utilizza le opzioni dei preprocessori.

### Utilizzo {#usage}

Puoi scegliere di configurare la configurazione dei preprocessori per clientlibrary o a livello di sistema.

* Aggiungere le proprietà multivalore `cssProcessor` e `jsProcessor` sul nodo clientlibrary

* Oppure definisci la configurazione predefinita del sistema tramite la **HTML Library Manager** Configurazione OSGi

Una configurazione preprocessore sul nodo clientlib ha la precedenza sulla configurazione OSGI.

### Formato ed esempi {#format-and-examples}

#### Formato {#format}

```xml
config:= mode ":" processorName options*;
mode:= "default" | "min";
processorName := "none" | <name>;
options := ";" option;
option := name "=" value;
```

#### Compressore YUI per la minimizzazione CSS e GCC per JS {#yui-compressor-for-css-minification-and-gcc-for-js}

```xml
cssProcessor: ["default:none", "min:yui"]
jsProcessor: ["default:none", "min:gcc;compilationLevel=advanced"]
```

#### Script per la preelaborazione e quindi GCC per minimizzare e offuscare {#typescript-to-preprocess-and-then-gcc-to-minify-and-obfuscate}

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

Per ulteriori dettagli sulle opzioni GCC, consulta la sezione [Documentazione GCC](https://developers.google.com/closure/compiler/docs/compilation_levels).

### Imposta il minatore predefinito di sistema {#set-system-default-minifier}

YUI è impostato come minificatore predefinito in AEM. Per modificare questo valore in GCC, segui questi passaggi.

1. Vai a Apache Felix Config Manager in [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)
1. Trova e modifica le **Adobe Granite HTML Library Manager**.
1. Abilita la **Miniatura** (se non è già abilitato).
1. Imposta il valore **Configurazioni predefinite del processore JS** a `min:gcc`.

   Le opzioni possono essere passate se separate da un punto e virgola, ad esempio `min:gcc;obfuscate=true`.

1. Fai clic su **Salva** per salvare le modifiche.

## Strumenti di debug {#debugging-tools}

AEM fornisce diversi strumenti per il debug e il test delle cartelle della libreria client.

### Vedere File incorporati {#see-embedded-files}

Per tracciare l&#39;origine del codice incorporato o per garantire che le librerie client incorporate producano i risultati previsti, puoi vedere i nomi dei file che vengono incorporati in fase di esecuzione. Per visualizzare i nomi dei file, aggiungi il `debugClientLibs=true` all&#39;URL della pagina web. La libreria generata contiene `@import` istruzioni invece del codice incorporato.

Nell&#39;esempio precedente [Incorporazione Di Codice Da Altre Librerie](/help/sites-developing/clientlibs.md#embedding-code-from-other-libraries) la sezione `/etc/client/libraries/myclientlibs/publicmain` la cartella della libreria client incorpora `/apps/myapp/clientlib` cartella della libreria client. L&#39;aggiunta del parametro alla pagina web produce il seguente collegamento nel codice sorgente della pagina web:

```xml
<link rel="stylesheet" href="/etc/clientlibs/mycientlibs/publicmain.css">
```

Apertura `publicmain.css` il file rivela il seguente codice:

```xml
@import url("/apps/myapp/clientlib/styles/main.css");
```

1. Nella casella dell’indirizzo del browser Web, aggiungi il seguente testo all’URL del HTML:

   `?debugClientLibs=true`
1. Quando la pagina viene caricata, visualizza l&#39;origine della pagina.
1. Fare clic sul collegamento fornito come href per l&#39;elemento di collegamento per aprire il file e visualizzare il codice sorgente.

### Scopri librerie client {#discover-client-libraries}

La `/libs/cq/granite/components/dumplibs/dumplibs` component genera una pagina di informazioni su tutte le cartelle della libreria client sul sistema. La `/libs/granite/ui/content/dumplibs` il componente è impostato come tipo di risorsa. Per aprire la pagina, utilizza il seguente URL (modificando l’host e la porta come richiesto):

`https://<host>:<port>/libs/granite/ui/content/dumplibs.test.html`

Le informazioni includono il percorso e il tipo della libreria (CSS o JS) e i valori degli attributi della libreria, ad esempio categorie e dipendenze. Le tabelle successive nella pagina mostrano le librerie in ogni categoria e canale.

### Vedere Output generato {#see-generated-output}

La `dumplibs` il componente include un selettore di test che visualizza il codice sorgente generato per `ui:includeClientLib` tag. La pagina include il codice per diverse combinazioni di attributi js, css e a tema.

1. Utilizza uno dei metodi seguenti per aprire la pagina Test output:

   * Da `dumplibs.html` , fai clic sul collegamento nel **Fai clic qui per il test dell’output** testo.

   * Apri il seguente URL nel browser Web (utilizza un host e una porta diversi come richiesto):

      * `http://<host>:<port>/libs/granite/ui/content/dumplibs.html`

   La pagina predefinita mostra l’output per i tag senza valore per l’attributo categories.

1. Per visualizzare l&#39;output di una categoria, digitare il valore della libreria client `categories` e fai clic su **Invia query**.

## Configurazione della gestione delle librerie per lo sviluppo e la produzione {#configuring-library-handling-for-development-and-production}

Il servizio HTML Library Manager elabora `cq:ClientLibraryFolder` assegna tag e genera le librerie in fase di esecuzione. Il tipo di ambiente, sviluppo o produzione determina la modalità di configurazione del servizio:

* Maggiore sicurezza: Disattiva il debug
* Migliorare le prestazioni: Rimuovere spazi bianchi e comprimere le librerie.
* Migliorare la leggibilità: Includi spazio vuoto e non comprimere.

Per informazioni sulla configurazione del servizio, vedi [AEM HTML Library Manager](/help/sites-deploying/osgi-configuration-settings.md#aemhtmllibrarymanager).
