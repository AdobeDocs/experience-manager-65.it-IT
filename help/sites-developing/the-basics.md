---
title: AEM Concetti di base
seo-title: The Basics
description: Una panoramica dei concetti fondamentali su come AEM è strutturato e come svilupparla al di sopra, compresi JCR, Sling, OSGi, il dispatcher, i flussi di lavoro e MSM
seo-description: An overview of the core concepts of how AEM is structured and how to develop on top of it including understanding the JCR, Sling, OSGi, the dispatcher, workflows, and MSM
uuid: e49f29db-a5d6-48a0-af32-f8785156746e
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 6e913190-be92-4862-a8b9-517f8bde0044
exl-id: f6f32290-422e-4037-89d8-d9f414332e8e
source-git-commit: 2bae11eafb875f01602c39c0dba00a888e11391a
workflow-type: tm+mt
source-wordcount: '3334'
ht-degree: 1%

---

# AEM Concetti di base {#aem-core-concepts}

>[!NOTE]
>
>Prima di immergerti nei concetti di base di AEM, Adobe consiglia di completare l’esercitazione WKND nel documento [Guida introduttiva allo sviluppo per AEM Sites](/help/sites-developing/getting-started.md) per una panoramica del processo di sviluppo AEM e un’introduzione ai concetti di base.

## Prerequisiti per lo sviluppo su AEM {#prerequisites-for-developing-on-aem}

Avrai bisogno delle seguenti competenze per sviluppare su AEM:

* Conoscenza di base delle tecniche di applicazione web, tra cui:

   * il ciclo request -response (XMLHttpRequest / XMLHttpResponse)
   * HTML
   * CSS
   * JavaScript

* Conoscenza di lavoro di Experience Server (CRX), incluso Content Explorer
* Per lo sviluppo nell’interfaccia classica, è necessaria anche la conoscenza di base di JSP (JavaServer Pages), inclusa la capacità di comprendere e modificare semplici esempi JSP.

Si consiglia inoltre di leggere e seguire le [Linee guida e best practice](/help/sites-developing/dev-guidelines-bestpractices.md).

## Archivio dei contenuti Java {#java-content-repository}

Lo standard Java Content Repository (JCR) [JSR 283](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/index.html) specifica un modo indipendente dal fornitore e indipendente dall&#39;implementazione per accedere al contenuto bidirezionale a un livello granulare all&#39;interno di un archivio di contenuti.

Il piombo specifico è detenuto da Adobe Research (Svizzera) AG.

Il pacchetto [JCR API 2.0](https://docs.adobe.com/docs/en/spec/javax.jcr/javadocs/jcr-2.0/index.html), javax.jcr.&amp;ast; viene utilizzato per l’accesso diretto e la manipolazione del contenuto dell’archivio.

## Experience Server (CRX) e Jackrabbit {#experience-server-crx-and-jackrabbit}

Experience Server fornisce i servizi Experience AEM basati su e che possono essere utilizzati per creare applicazioni personalizzate e incorpora l’archivio dei contenuti basato su Jackrabbit.

[Apache ](https://jackrabbit.apache.org/) Jackrabbitis è un’implementazione open source, completamente conforme, di JCR API 2.0.

## Elaborazione delle richieste Sling {#sling-request-processing}

### Introduzione a Sling {#introduction-to-sling}

AEM viene creato utilizzando [Sling](https://sling.apache.org/site/index.html), un framework di applicazione web basato sui principi REST che fornisce un facile sviluppo di applicazioni orientate ai contenuti. Sling utilizza un archivio JCR, come Apache Jackrabbit, o nel caso di AEM, il CRX Content Repository, come archivio dati. Sling è stato contribuito a Apache Software Foundation - ulteriori informazioni sono disponibili su Apache.

Utilizzando Sling, il tipo di contenuto di cui eseguire il rendering non è il primo aspetto di elaborazione. La considerazione principale è se l’URL viene risolto in un oggetto di contenuto per il quale è quindi possibile trovare uno script per eseguire il rendering. Questo offre un supporto eccellente agli autori di contenuti web per creare pagine facilmente personalizzate in base alle loro esigenze.

I vantaggi di questa flessibilità sono evidenti nelle applicazioni con una vasta gamma di elementi di contenuto diversi, o quando è necessario personalizzare pagine facilmente. In particolare, quando si implementa un sistema di gestione dei contenuti web come WCM nella soluzione AEM.

Per i primi passaggi da sviluppare con Sling, consulta [Scopri Sling in 15 minuti](https://sling.apache.org/documentation/getting-started/discover-sling-in-15-minutes.html) .

Il diagramma seguente spiega la risoluzione dello script Sling: mostra come passare dalla richiesta HTTP al nodo del contenuto, dal nodo del contenuto al tipo di risorsa, dal tipo di risorsa allo script e quali variabili di script sono disponibili.

![Comprensione della risoluzione degli script Apache Sling](assets/sling-cheatsheet-01.png)

Il diagramma seguente illustra tutti i parametri di richiesta nascosti ma potenti che è possibile utilizzare quando si gestisce lo SlingPostServlet, il gestore predefinito per tutte le richieste POST che offre infinite opzioni per la creazione, la modifica, l’eliminazione, la copia e lo spostamento dei nodi nell’archivio.

![Utilizzo di SlingPostServlet](assets/sling-cheatsheet-02.png)

### Sling è incentrato sul contenuto {#sling-is-content-centric}

Sling è *incentrato sul contenuto*. Ciò significa che l’elaborazione è incentrata sul contenuto, in quanto ogni richiesta (HTTP) viene mappata sul contenuto sotto forma di una risorsa JCR (un nodo di archivio):

* il primo target è la risorsa (nodo JCR) che contiene il contenuto
* in secondo luogo, la rappresentazione, o script, si trova dalle proprietà della risorsa in combinazione con alcune parti della richiesta (ad esempio selettori e/o estensione)

### Sling RESTful {#restful-sling}

Grazie alla filosofia incentrata sui contenuti, Sling implementa un server orientato al REST e quindi presenta un nuovo concetto nei framework delle applicazioni web. I vantaggi sono:

* molto RESTful, non solo sulla superficie; le risorse e le rappresentazioni vengono modellate correttamente all’interno del server
* rimuove uno o più modelli di dati

   * in precedenza erano necessari i seguenti elementi: struttura URL, oggetti aziendali, schema DB;
   * ora è ridotto a: URL = resource = JCR structure

### Decomposizione URL {#url-decomposition}

In Sling, l&#39;elaborazione è guidata dall&#39;URL della richiesta dell&#39;utente. Definisce il contenuto da visualizzare dagli script appropriati. A questo scopo, le informazioni vengono estratte dall’URL.

Se analizziamo il seguente URL:

```xml
https://myhost/tools/spy.printable.a4.html/a/b?x=12
```

Possiamo suddividerlo nelle sue parti composite:

| protocollo | host | percorso del contenuto | selettori | estensione |  | suffisso |  | param(i) |
|---|---|---|---|---|---|---|---|---|
| https:// | mihost | strumenti/spia | .printable.a4. | viene | / | a/b | ? | x=12 |

**** protocolHTTP

**** hostName del sito web.

**content** pathPath che specifica il contenuto di cui eseguire il rendering. è utilizzato in combinazione con l&#39;estensione; in questo esempio si traducono in tools/spy.html.

**selettori** utilizzati per metodi alternativi di rendering del contenuto; in questo esempio, una versione compatibile con la stampante in formato A4.

**** formato extensionContent; specifica anche lo script da utilizzare per il rendering.

**** suffixCan può essere utilizzato per specificare informazioni aggiuntive.

**parametri** Qualsiasi parametro necessario per il contenuto dinamico.

#### Da URL a contenuto e script {#from-url-to-content-and-scripts}

Seguendo questi principi:

* la mappatura utilizza il percorso del contenuto estratto dalla richiesta per individuare la risorsa
* quando si trova la risorsa appropriata, il tipo di risorsa sling viene estratto e utilizzato per individuare lo script da utilizzare per il rendering del contenuto

La figura seguente illustra il meccanismo utilizzato, che sarà discusso più dettagliatamente nelle sezioni seguenti.

![chlimage_1-86](assets/chlimage_1-86a.png)

Con Sling, si specifica quale script esegue il rendering di una determinata entità (impostando la proprietà `sling:resourceType` nel nodo JCR). Questo meccanismo offre più libertà di una in cui lo script accede alle entità dati (come farebbe un&#39;istruzione SQL in uno script PHP) in quanto una risorsa può avere diverse rappresentazioni.

#### Mappatura delle richieste alle risorse {#mapping-requests-to-resources}

La richiesta è suddivisa ed estrae le informazioni necessarie. Nell’archivio viene eseguita la ricerca della risorsa richiesta (nodo di contenuto):

* il primo Sling controlla se un nodo esiste nella posizione specificata nella richiesta; ad esempio `../content/corporate/jobs/developer.html`
* se non viene trovato alcun nodo, l&#39;estensione viene eliminata e la ricerca viene ripetuta; ad esempio `../content/corporate/jobs/developer`
* se non viene trovato alcun nodo, Sling restituirà il codice http 404 (Non trovato).

Sling consente anche di usare risorse diverse dai nodi JCR, ma questa è una funzione avanzata.

### Individuazione dello script {#locating-the-script}

Quando si trova la risorsa appropriata (nodo di contenuto), viene estratto il **tipo di risorsa sling**. Si tratta di un percorso che individua lo script da utilizzare per il rendering del contenuto.

Il percorso specificato da `sling:resourceType` può essere:

* assoluto
* relativo, a un parametro di configurazione

   I percorsi relativi sono consigliati per Adobe in quanto aumentano la portabilità.

Tutti gli script Sling sono memorizzati in sottocartelle di `/apps` o `/libs`, che verranno cercate in questo ordine (consulta [Personalizzazione di componenti e altri elementi](/help/sites-developing/dev-guidelines-bestpractices.md#customizing-components-and-other-elements)).

Alcuni altri punti da sottolineare sono:

* quando il metodo (GET, POST) è obbligatorio, viene specificato in maiuscolo come in base alla specifica HTTP, ad esempio jobs.POST.esp (vedi sotto)
* sono supportati diversi motori di script:

   * HTL (HTML Template Language - Sistema di modelli lato server preferito e consigliato da Adobe Experience Manager per HTML): `.html`
   * ECMAScript (JavaScript) Pagine (esecuzione lato server): `.esp, .ecma`
   * Java Server Pages (esecuzione lato server): `.jsp`
   * Compilatore Java Servlet (esecuzione lato server): `.java`
   * Modelli JavaScript (esecuzione lato client): `.jst`

L&#39;elenco dei motori di script supportati dalla data istanza di AEM è elencato nella console di gestione Felix ( `http://<host>:<port>/system/console/slingscripting`).

Inoltre, Apache Sling supporta l’integrazione con altri motori di script popolari (ad esempio, Groovy, JRuby, Freemarker) e fornisce un modo per integrare nuovi motori di script.

Utilizzando l’esempio precedente, se il valore `sling:resourceType` è `hr/jobs`, utilizza:

* Richieste GET/HEAD e URL che terminano con .html (tipi di richiesta predefiniti, formato predefinito)

   Lo script sarà /apps/hr/jobs/jobs.esp; l&#39;ultima sezione dell&#39;sling:resourceType forma il nome del file.

* Richieste POST (tutti i tipi di richiesta ad eccezione di GET/HEAD, il nome del metodo deve essere maiuscolo)

   POST verrà utilizzato nel nome dello script.

   Lo script sarà `/apps/hr/jobs/jobs.POST.esp`.

* URL in altri formati, che non terminano con .html

   Esempio `../content/corporate/jobs/developer.pdf`

   Lo script sarà `/apps/hr/jobs/jobs.pdf.esp`; il suffisso viene aggiunto al nome dello script.

* URL con selettori

   I selettori possono essere utilizzati per visualizzare lo stesso contenuto in un formato alternativo. Ad esempio, una versione compatibile con la stampante, un feed rss o un riepilogo.

   Se si considera una versione compatibile con la stampante in cui il selettore potrebbe essere *print*; come in `../content/corporate/jobs/developer.print.html`

   Lo script sarà `/apps/hr/jobs/jobs.print.esp`; il selettore viene aggiunto al nome dello script.

* Se non è stato definito alcun sling:resourceType , allora:

   * il percorso del contenuto verrà utilizzato per cercare uno script appropriato (se ResourceTypeProvider basato sul percorso è attivo).

      Ad esempio, lo script per `../content/corporate/jobs/developer.html` genererebbe una ricerca in `/apps/content/corporate/jobs/`.

   * verrà utilizzato il tipo di nodo principale.

* Se non viene trovato alcuno script, verrà utilizzato lo script predefinito.

   Il rendering predefinito è attualmente supportato come testo normale (.txt), HTML (.html) e JSON (.json), tutti i quali elencheranno le proprietà del nodo (formattato in modo appropriato). Il rendering predefinito per l&#39;estensione .res, o richieste senza estensione di richiesta, consiste nello spool della risorsa (dove possibile).
* Per la gestione degli errori http (codici 403 o 404) Sling cerca uno script in:

   * la posizione /apps/sling/servlet/errorhandler per [script personalizzati](/help/sites-developing/customizing-errorhandler-pages.md)
   * o la posizione degli script standard /libs/sling/servlet/errorhandler/403.esp o 404.esp rispettivamente.

Se per una determinata richiesta sono validi più script, viene selezionato lo script con la migliore corrispondenza. Più una partita è specifica, meglio è. in altre parole, più il selettore corrisponde meglio, indipendentemente da eventuali estensioni di richiesta o dalla corrispondenza del nome del metodo.

Ad esempio, considera una richiesta per accedere alla risorsa
`/content/corporate/jobs/developer.print.a4.html`
di tipo
`sling:resourceType="hr/jobs"`

Presupponendo che il seguente elenco di script sia nella posizione corretta:

1. `GET.esp`
1. `jobs.esp`
1. `html.esp`
1. `print.esp`
1. `print.html.esp`
1. `print/a4.esp`
1. `print/a4/html.esp`
1. `print/a4.html.esp`

Quindi l&#39;ordine di preferenza sarebbe (8) - (7) - (6) - (5) - (4) - (3) - (2) - (1).

Oltre ai tipi di risorse (definiti principalmente dalla proprietà `sling:resourceType` ), è presente anche il super tipo di risorsa. Questo è generalmente indicato dalla proprietà `sling:resourceSuperType` . Questi super tipi vengono considerati anche quando si cerca di trovare uno script. I super tipi di risorse possono essere costituiti da una gerarchia di risorse in cui il tipo di risorsa predefinito `sling/servlet/default` (utilizzato dai servlet predefiniti) è effettivamente la radice.

Il super tipo di risorsa può essere definito in due modi:

* dalla proprietà `sling:resourceSuperType` della risorsa.
* dalla proprietà `sling:resourceSuperType` del nodo a cui punta `sling:resourceType`.

Esempio:

* /

   * una sessione lavagna 
   * b

      * sling:resourceSuperType = a
   * c

      * sling:resourceSuperType = b
   * x

      * sling:resourceType = c
   * y

      * sling:resourceType = c
      * sling:resourceSuperType = a




La gerarchia dei tipi di:

* `/x`
   * è `[ c, b, a, <default>]`
* while per `/y`
   * la gerarchia è `[ c, a, <default>]`

Questo perché `/y` dispone della proprietà `sling:resourceSuperType` , mentre `/x` non lo fa e quindi il relativo supertipo viene prelevato dal relativo tipo di risorsa.

#### Gli script Sling non possono essere chiamati direttamente {#sling-scripts-cannot-be-called-directly}

All’interno di Sling, gli script non possono essere chiamati direttamente in quanto ciò violerebbe il concetto rigoroso di server REST; puoi combinare risorse e rappresentazioni.

Se chiami direttamente la rappresentazione (lo script), nascondi la risorsa all’interno dello script, in modo che il framework (Sling) non ne sia più a conoscenza. Così si perdono alcune caratteristiche:

* gestione automatica dei metodi http diversi da GET, compresi:

   * POST, PUT, DELETE che vengono gestiti con un’implementazione predefinita sling
   * lo script `POST.jsp` nella posizione sling:resourceType

* la tua architettura del codice non è più pulita né strutturata come dovrebbe; di importanza primaria per lo sviluppo su larga scala

### API Sling {#sling-api}

Questo utilizza il pacchetto API Sling, org.apache.sling.&amp;ast; e librerie di tag.

### Riferimento a elementi esistenti utilizzando sling:include {#referencing-existing-elements-using-sling-include}

Una considerazione finale è la necessità di fare riferimento agli elementi esistenti all&#39;interno degli script.

Gli script più complessi (aggregazione degli script) potrebbero dover accedere a più risorse (ad esempio navigazione, barra laterale, piè di pagina, elementi di un elenco) e farlo includendo la *risorsa*.

A questo scopo puoi usare il comando sling:include(&quot;/&lt;percorso>/&lt;risorsa>&quot;). Questo includerà effettivamente la definizione della risorsa di riferimento, come nell’istruzione seguente che fa riferimento a una definizione esistente per il rendering delle immagini:

```xml
%><sling:include resourceType="geometrixx/components/image/img"/><%
```

## OSGI {#osgi}

OSGi definisce un’architettura per lo sviluppo e la distribuzione di applicazioni e librerie modulari (noto anche come Sistema di moduli dinamici per Java). I contenitori OSGi ti consentono di suddividere l’applicazione in singoli moduli (sono file jar con metadati aggiuntivi e chiamati bundle nella terminologia OSGi) e di gestire le dipendenze trasversali tra di loro con:

* servizi implementati all’interno del contenitore
* un contratto tra il contenitore e la tua applicazione

Questi servizi e contratti offrono un&#39;architettura che consente ai singoli elementi di scoprirsi l&#39;un l&#39;altro in modo dinamico per la collaborazione.

Un framework OSGi ti offre quindi il caricamento/scaricamento dinamico, la configurazione e il controllo di questi bundle, senza dover riavviare.

>[!NOTE]
>
>Informazioni complete sulla tecnologia OSGi sono disponibili sul sito web [OSGi](https://www.osgi.org).
>
>In particolare, la pagina Basic Education contiene una raccolta di presentazioni ed esercitazioni.

Questa architettura consente di estendere Sling con moduli specifici per le applicazioni. Sling, e quindi CQ5, utilizza l’ [Apache Felix](https://felix.apache.org/) implementazione di OSGI (Open Services Gateway Initiative) e si basa sulle specifiche della versione 4.2 di OSGi Service Platform. Sono entrambe raccolte di bundle OSGi in esecuzione all&#39;interno di un framework OSGi.

Questo consente di eseguire le seguenti azioni su uno qualsiasi dei pacchetti all’interno dell’installazione:

* installare
* start
* stop
* aggiorna
* disinstallare
* vedere lo stato corrente
* accedere a informazioni più dettagliate (ad esempio nome simbolico, versione, posizione, ecc.) sui bundle specifici

Per ulteriori informazioni, consulta [Console web](/help/sites-deploying/web-console.md), [Configurazione OSGI](/help/sites-deploying/configuring-osgi.md) e [Impostazioni di configurazione OSGi](/help/sites-deploying/osgi-configuration-settings.md) .

## Oggetti di sviluppo nell&#39;ambiente AEM {#development-objects-in-the-aem-environment}

Sono di interesse per lo sviluppo:

**** ItemUn elemento è un nodo o una proprietà.

Per informazioni dettagliate sulla manipolazione degli oggetti Item, consulta [Javadocs](https://docs.adobe.com/docs/en/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Item.html) dell&#39;interfaccia javax.jcr.Item

**I nodi (e le relative proprietà)**  e le relative proprietà sono definiti nella specifica JCR API 2.0 (JSR 283). Memorizzano il contenuto, le definizioni degli oggetti, gli script di rendering e altri dati.

I nodi definiscono la struttura del contenuto e le loro proprietà memorizzano il contenuto e i metadati effettivi.

I nodi di contenuto guidano il rendering. Sling ottiene il nodo del contenuto dalla richiesta in arrivo. La proprietà sling:resourceType di questo nodo punta al componente di rendering Sling da utilizzare.

Un nodo, che è un nome JCR, è anche chiamato una risorsa nell&#39;ambiente Sling.

Ad esempio, per ottenere le proprietà del nodo corrente, è possibile utilizzare il seguente codice nello script:

`PropertyIterator properties = currentNode.getProperties();`

Con currentNode come oggetto nodo corrente.

Per ulteriori informazioni sulla manipolazione degli oggetti Node, consulta [Javadocs](https://docs.adobe.com/docs/en/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Node.html).

**** WidgetIn AEM tutti gli input dell&#39;utente sono gestiti da widget. Spesso sono utilizzati per controllare la modifica di un contenuto.

Le finestre di dialogo sono create combinando i Widget.

AEM è stato sviluppato utilizzando la libreria ExtJS di widget.

**** DialogUna finestra di dialogo è un tipo speciale di widget.

Per modificare il contenuto, AEM utilizza le finestre di dialogo definite dallo sviluppatore dell’applicazione. Questi combinano una serie di widget per presentare all’utente tutti i campi e le azioni necessarie per modificare il contenuto correlato.

Le finestre di dialogo vengono utilizzate anche per la modifica dei metadati e da vari strumenti amministrativi.

**** ComponenteUn componente software è un elemento di sistema che offre un servizio o un evento predefinito e in grado di comunicare con altri componenti.

All’interno di AEM un componente viene spesso utilizzato per eseguire il rendering del contenuto di una risorsa. Quando la risorsa è una pagina, il rendering del componente è denominato Componente di primo livello o Componente di pagina. Tuttavia, un componente non deve eseguire il rendering del contenuto, né deve essere collegato a una risorsa specifica; ad esempio, un componente di navigazione visualizza informazioni su più risorse.

La definizione di un componente include:,

* il codice utilizzato per il rendering del contenuto
* una finestra di dialogo per l’input dell’utente e la configurazione del contenuto risultante.

**** ModelloUn modello è la base per un tipo specifico di pagina. Quando crei una pagina nella scheda Siti web , l’utente deve selezionare un modello. La nuova pagina viene quindi creata copiando questo modello.

Un modello è una gerarchia di nodi con la stessa struttura della pagina da creare, ma senza alcun contenuto effettivo.

Definisce il componente pagina utilizzato per eseguire il rendering della pagina e del contenuto predefinito (contenuto principale primario). Il contenuto definisce il rendering come AEM è incentrato sul contenuto.

**Componente pagina (componente di primo livello)** Il componente da utilizzare per il rendering della pagina.

**** La paginaA è un&#39;istanza di un modello.

Una pagina ha un nodo gerarchico di tipo cq:Page e un nodo di contenuto di tipo cq:PageContent. La proprietà sling:resourceType del nodo del contenuto punta al componente Pagina utilizzato per il rendering della pagina.

Ad esempio, per ottenere il nome della pagina corrente, è possibile utilizzare il seguente codice nello script:

S`tring pageName = currentPage.getName();`

Con currentPage come oggetto pagina corrente. Per ulteriori informazioni sulla manipolazione degli oggetti Page, consulta [Javadocs](https://helpx.adobe.com/it/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/Page.html).

**Page** ManagerIl gestore pagine è un&#39;interfaccia che fornisce metodi per le operazioni a livello di pagina.

Ad esempio, per ottenere la pagina contenente una risorsa, puoi utilizzare il seguente codice nello script:

Page myPage = pageManager.getContainPage(myResource);

Con pageManager come oggetto page manager e myResource come oggetto risorsa. Per ulteriori informazioni sui metodi forniti dal gestore di pagine, consulta [Javadocs](https://helpx.adobe.com/it/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageManager.html).

## Struttura all’interno dell’archivio {#structure-within-the-repository}

L’elenco seguente fornisce una panoramica della struttura che verrà visualizzata all’interno dell’archivio.

>[!CAUTION]
>
>Le modifiche a questa struttura, o ai relativi file, devono essere effettuate con attenzione.
>
>Sono necessarie modifiche durante lo sviluppo, ma accertati di comprendere appieno le implicazioni di eventuali modifiche apportate.

>[!CAUTION]
>
>Non è necessario modificare nulla nel percorso `/libs`. Per la configurazione e altre modifiche, copia l’elemento da `/libs` a `/apps` e apporta eventuali modifiche all’interno di `/apps`.

* `/apps`

   Applicazione correlata; include definizioni di componenti specifiche del sito web. I componenti sviluppati possono essere basati sui componenti predefiniti disponibili in `/libs/foundation/components`.

* `/content`

   Contenuto creato per il sito web.

* `/etc`

* `/home`

   Informazioni utente e gruppo.

* `/libs`

   Librerie e definizioni che appartengono al nucleo di AEM. Le sottocartelle in `/libs` rappresentano le funzionalità predefinite AEM come ad esempio ricerca o replica. Il contenuto in `/libs` non deve essere modificato in quanto influisce sul funzionamento AEM. Le funzioni specifiche del sito web devono essere sviluppate in `/apps` (consulta [Personalizzazione di componenti e altri elementi](/help/sites-developing/dev-guidelines-bestpractices.md#customizing-components-and-other-elements)).

* `/tmp`

   Area di lavoro temporanea.

* `/var`

   File che cambiano e vengono aggiornati dal sistema; come i registri di controllo, le statistiche, la gestione degli eventi.

## Ambienti {#environments}

Con AEM un ambiente di produzione spesso è costituito da due diversi tipi di istanze: un [Author e un&#39;istanza Publish](/help/sites-deploying/deploy.md#author-and-publish-installs).

## Dispatcher {#the-dispatcher}

Dispatcher è lo strumento di Adobe per la memorizzazione in cache e/o il bilanciamento del carico. Ulteriori informazioni sono disponibili in [Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/user-guide.html).

## FileVault (sistema di revisione sorgente) {#filevault-source-revision-system}

FileVault fornisce al tuo archivio JCR la mappatura del file system e il controllo della versione. Può essere utilizzato per gestire progetti di sviluppo AEM con supporto completo per l’archiviazione e il controllo delle versioni del codice di progetto, del contenuto, delle configurazioni e così via, nei sistemi di controllo delle versioni standard (ad esempio, Subversion).

Per informazioni dettagliate, consulta la documentazione [FileVault tool](/help/sites-developing/ht-vlttool.md) .

## Flussi di lavoro {#workflows}

Il contenuto è spesso soggetto a processi organizzativi, compresi passaggi quali l’approvazione e l’approvazione da parte di vari partecipanti. Questi processi possono essere rappresentati come flussi di lavoro, [definiti e sviluppati all&#39;interno di AEM](/help/sites-developing/workflows-models.md), quindi applicati alle [pagine di contenuto appropriate](/help/sites-administering/workflows.md) o [risorse digitali](/help/assets/assets-workflow.md) come necessario.

Il motore di flusso di lavoro viene utilizzato per gestire l’implementazione dei flussi di lavoro e la loro successiva applicazione ai contenuti.

## Gestione multisito {#multi-site-management}

Multi Site Manager (MSM) consente di gestire facilmente più siti web che condividono contenuti comuni. MSM consente di definire le relazioni tra i siti in modo che le modifiche di contenuto in un sito vengano replicate automaticamente in altri siti.

Ad esempio, i siti web sono spesso disponibili in più lingue per il pubblico internazionale. Quando il numero di siti nella stessa lingua è basso (da tre a cinque), è possibile eseguire un processo manuale per la sincronizzazione dei contenuti tra siti diversi. Tuttavia, non appena il numero di siti cresce o quando sono coinvolte più lingue, diventa più efficiente automatizzare il processo.

* Gestire in modo efficiente diverse versioni linguistiche di un sito web.
* Aggiorna automaticamente uno o più siti in base a un sito di origine:

   * Applica una struttura di base comune e utilizza contenuti comuni su più siti.
   * Ottimizza l’utilizzo delle risorse disponibili.
   * Mantenere un aspetto comune.
   * Concentrati sulla gestione dei contenuti che differiscono tra i siti.

Per ulteriori informazioni, consulta [Multi Site Manager](/help/sites-administering/msm.md).
