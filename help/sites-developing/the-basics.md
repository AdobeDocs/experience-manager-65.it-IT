---
title: Concetti di base AEM
seo-title: Nozioni di base
description: Una panoramica dei concetti chiave di come AEM è strutturato e come svilupparsi al di sopra di esso, tra cui la comprensione di JCR, Sling, OSGi, il dispatcher, i flussi di lavoro e MSM
seo-description: Una panoramica dei concetti chiave di come AEM è strutturato e come svilupparsi al di sopra di esso, tra cui la comprensione di JCR, Sling, OSGi, il dispatcher, i flussi di lavoro e MSM
uuid: e49f29db-a5d6-48a0-af32-f8785156746e
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 6e913190-be92-4862-a8b9-517f8bde0044
translation-type: tm+mt
source-git-commit: 2d0e0325d1fce2587e4766bf2f60fc5d4accf45b

---


# Concetti di base AEM {#aem-core-concepts}

>[!NOTE]
>
>Prima di approfondire i concetti di base di AEM, Adobe consiglia di completare l’esercitazione WKND nel documento [Primi passi nello sviluppo di AEM Sites](/help/sites-developing/getting-started.md) per una panoramica del processo di sviluppo di AEM e per introdurre i concetti di base.

## Prerequisiti per lo sviluppo su AEM {#prerequisites-for-developing-on-aem}

Per sviluppare su AEM le seguenti competenze:

* Conoscenza di base delle tecniche di applicazione Web, tra cui:

   * il ciclo request-response (XMLHttpRequest / XMLHttpResponse)
   * HTML
   * CSS
   * JavaScript

* Conoscenza di base di Experience Server (CRX), incluso Content Explorer
* Per lo sviluppo nell’interfaccia classica, è inoltre necessaria una conoscenza di base di JSP (JavaServer Pages), compresa la capacità di comprendere e modificare semplici esempi JSP.

Si consiglia inoltre di leggere e seguire le [Linee guida e le best practice](/help/sites-developing/dev-guidelines-bestpractices.md).

## Repository di contenuti Java {#java-content-repository}

Lo standard Java Content Repository (JCR), [JSR 283](https://docs.adobe.com/content/docs/en/spec/jcr/2.0/index.html), specifica un modo indipendente dal fornitore e indipendente dall&#39;implementazione per accedere ai contenuti bidirezionalmente su un livello granulare all&#39;interno di un repository di contenuti.

Il lead della specifica è detenuto da Adobe Research (Svizzera) AG.

Il pacchetto [JCR API 2.0](https://docs.adobe.com/docs/en/spec/javax.jcr/javadocs/jcr-2.0/index.html) , javax.jcr. &amp;ast; viene utilizzato per l&#39;accesso diretto e la manipolazione del contenuto del repository.

## Experience Server (CRX) e Jackrabbit {#experience-server-crx-and-jackrabbit}

Experience Server offre i servizi Experience Services su cui AEM è basato e che possono essere utilizzati per creare applicazioni personalizzate e incorpora il repository dei contenuti basato su Jackrabbit.

[Apache Jackrabbit](https://jackrabbit.apache.org/) è un&#39;implementazione open source, completamente conforme, dell&#39;API JCR 2.0.

## Elaborazione richiesta Sling {#sling-request-processing}

### Introduzione alla Sling {#introduction-to-sling}

AEM è basato su [Sling](https://sling.apache.org/site/index.html), un framework di applicazione Web basato su principi REST che fornisce un facile sviluppo di applicazioni orientate ai contenuti. Sling utilizza un archivio JCR, come Apache Jackrabbit, o nel caso di AEM, CRX Content Repository, come archivio di dati. Sling ha contribuito alla Apache Software Foundation - ulteriori informazioni sono reperibili presso Apache.

Con Sling, il tipo di contenuto di cui eseguire il rendering non è il primo criterio di elaborazione. La considerazione principale è stabilire se l&#39;URL corrisponde a un oggetto contenuto per il quale è possibile trovare uno script per eseguire il rendering. Questo offre un eccellente supporto agli autori di contenuti Web per creare pagine facilmente personalizzate in base alle loro esigenze.

I vantaggi di questa flessibilità sono evidenti nelle applicazioni con un&#39;ampia gamma di elementi di contenuto diversi, o quando è necessario creare pagine che possano essere facilmente personalizzate. In particolare, quando si implementa un sistema di gestione dei contenuti Web come WCM nella soluzione AEM.

Consulta [Scoprire Sling in 15 minuti](https://sling.apache.org/documentation/getting-started/discover-sling-in-15-minutes.html) per i primi passi di sviluppo con Sling.

Nel diagramma seguente viene illustrata la risoluzione dello script Sling: mostra come passare dalla richiesta HTTP al nodo contenuto, dal nodo di contenuto al tipo di risorsa, dal tipo di risorsa allo script e quali variabili di script sono disponibili.

![chlimage_1-84](assets/chlimage_1-97.png)

Il diagramma seguente illustra tutti i parametri di richiesta nascosti ma potenti che è possibile utilizzare per gestire SlingPostServlet, il gestore predefinito per tutte le richieste POST che offre infinite opzioni per creare, modificare, eliminare, copiare e spostare i nodi nell&#39;archivio.

![chlimage_1-85](assets/chlimage_1-98.png)

### Sling è incentrato sui contenuti {#sling-is-content-centric}

Sling è incentrato sul ** contenuto. Ciò significa che l&#39;elaborazione è incentrata sul contenuto, in quanto ogni richiesta (HTTP) viene mappata sul contenuto sotto forma di risorsa JCR (un nodo del repository):

* la prima destinazione è la risorsa (nodo JCR) che contiene il contenuto
* in secondo luogo, la rappresentazione, o script, si trova dalle proprietà della risorsa in combinazione con alcune parti della richiesta (ad es. selettori e/o estensione)

### Sling RESTful {#restful-sling}

Grazie alla filosofia incentrata sui contenuti, Sling implementa un server orientato al REST e quindi offre un nuovo concetto nei framework delle applicazioni Web. I vantaggi sono:

* molto RESTful, non solo sulla superficie; le risorse e le rappresentazioni vengono modellate correttamente all&#39;interno del server
* rimuove uno o più modelli di dati

   * in precedenza erano necessari i seguenti elementi: struttura URL, oggetti aziendali, schema DB;
   * ora è ridotto a: URL = resource = JCR structure

### Scomposizione URL {#url-decomposition}

In Sling, l&#39;elaborazione è guidata dall&#39;URL della richiesta dell&#39;utente. Definisce il contenuto che deve essere visualizzato dagli script appropriati. A questo scopo, le informazioni vengono estratte dall’URL.

Se analizziamo il seguente URL:

```xml
https://myhost/tools/spy.printable.a4.html/a/b?x=12
```

Possiamo suddividerlo nelle sue parti composite:

| protocol | host | percorso contenuto | selettori | extension |  | suffisso |  | param(s) |
|---|---|---|---|---|---|---|---|---|
| https:// | mihost | strumenti/spia | .printable.a4. | viene | / | a/b | ? | x=12 |

**protocollo** HTTP

**host** Nome del sito Web.

**percorso** contenuto Percorso che specifica il contenuto di cui eseguire il rendering. è utilizzato in combinazione con l&#39;estensione; in questo esempio vengono tradotti in tools/spy.html.

**selettori** utilizzati per metodi alternativi di rendering del contenuto; in questo esempio, una versione compatibile con la stampante in formato A4.

**formato contenuto estensione** ; specifica inoltre lo script da utilizzare per il rendering.

**suffisso** Può essere utilizzato per specificare ulteriori informazioni.

**param(s)** Eventuali parametri richiesti per il contenuto dinamico.

#### Da URL a contenuto e script {#from-url-to-content-and-scripts}

Seguire questi principi:

* la mappatura utilizza il percorso contenuto estratto dalla richiesta per individuare la risorsa
* quando si trova la risorsa appropriata, viene estratto il tipo di risorsa sling e utilizzato per individuare lo script da utilizzare per il rendering del contenuto

La figura riportata di seguito illustra il meccanismo utilizzato, che sarà discusso più dettagliatamente nelle sezioni seguenti.

![chlimage_1-86](assets/chlimage_1-86a.png)

Con Sling, si specifica quale script esegue il rendering di una determinata entità (impostando la `sling:resourceType` proprietà nel nodo JCR). Questo meccanismo offre più libertà di uno in cui lo script accede alle entità dati (come un&#39;istruzione SQL in uno script PHP farebbe) in quanto una risorsa può avere diverse rappresentazioni.

#### Mappatura delle richieste alle risorse {#mapping-requests-to-resources}

La richiesta è ripartita e vengono estratte le informazioni necessarie. Nella directory archivio viene ricercata la risorsa richiesta (nodo contenuto):

* first Sling controlla se un nodo esiste nella posizione specificata nella richiesta;ad esempio `../content/corporate/jobs/developer.html`
* se non viene trovato alcun nodo, l&#39;estensione viene eliminata e la ricerca viene ripetuta;ad esempio `../content/corporate/jobs/developer`
* se non viene trovato alcun nodo, Sling restituirà il codice http 404 (Non trovato).

Sling permette anche cose diverse dai nodi JCR di essere risorse, ma questa è una funzione avanzata.

### Individuazione dello script {#locating-the-script}

Quando si trova la risorsa appropriata (nodo di contenuto), viene estratto il tipo **di risorsa** sling. Si tratta di un percorso che individua lo script da utilizzare per il rendering del contenuto.

Il percorso specificato da `sling:resourceType` può essere:

* assoluto
* relativo, a un parametro di configurazione

   I percorsi relativi sono consigliati da Adobe in quanto aumentano la portabilità.

Tutti gli script Sling sono memorizzati in sottocartelle di `/apps` o `/libs`, che verranno cercati in questo ordine (consultate [Personalizzazione di componenti e altri elementi](/help/sites-developing/dev-guidelines-bestpractices.md#customizing-components-and-other-elements)).

Alcuni altri punti da sottolineare sono:

* quando il metodo (GET, POST) è richiesto, sarà specificato in maiuscolo come in base alla specifica HTTP, ad esempio, job.POST.esp (vedere di seguito)
* sono supportati diversi motori di script:

   * `.esp, .ecma`: ECMAScript (JavaScript) Pages (esecuzione lato server)
   * `.jsp`: Java Server Pages (esecuzione lato server)
   * `.java`: Compilatore Servlet Java (esecuzione lato server)
   * `.jst`: Modelli JavaScript (esecuzione lato client)

L’elenco dei motori di script supportati dalla data istanza di AEM è elencato nella console di gestione di Flash ( `http://<host>:<port>/system/console/slingscripting`).

Inoltre, Apache Sling supporta l&#39;integrazione con altri popolari motori di script (ad esempio, Groovy, JRuby, Freemarker) e fornisce un modo per integrare nuovi motori di script.

Utilizzando l&#39;esempio precedente, se `sling:resourceType` è `hr/jobs` quindi per:

* Richieste GET/HEAD e URL che terminano con .html (tipi di richiesta predefiniti, formato predefinito)

   Lo script sarà /apps/hr/jobs/jobs.esp; l’ultima sezione di sling:resourceType rappresenta il nome del file.

* Richieste POST (tutti i tipi di richiesta eccetto GET/HEAD, il nome del metodo deve essere maiuscolo)

   POST verrà utilizzato nel nome dello script.

   Lo script sarà `/apps/hr/jobs/jobs.POST.esp`.

* URL in altri formati, che non terminano con .html

   Esempio `../content/corporate/jobs/developer.pdf`

   Lo script sarà `/apps/hr/jobs/jobs.pdf.esp`; il suffisso viene aggiunto al nome dello script.

* URL con selettori

   I selettori possono essere utilizzati per visualizzare lo stesso contenuto in un formato alternativo. Ad esempio, una versione semplice della stampante, un feed rss o un riepilogo.

   Se si considera una versione compatibile con la stampante, il selettore potrebbe essere *stampato*; come `../content/corporate/jobs/developer.print.html`

   Lo script sarà `/apps/hr/jobs/jobs.print.esp`; il selettore viene aggiunto al nome dello script.

* Se non è stato definito alcun sling:resourceType, procedere come segue:

   * il percorso del contenuto verrà utilizzato per cercare uno script appropriato (se è attivo ResourceTypeProvider basato sul percorso).

      Ad esempio, lo script per `../content/corporate/jobs/developer.html` genererebbe una ricerca in `/apps/content/corporate/jobs/`.

   * verrà utilizzato il tipo di nodo principale.

* Se non viene trovato alcuno script, verrà utilizzato lo script predefinito.

   Al momento la rappresentazione predefinita è supportata come testo normale (.txt), HTML (.html) e JSON (.json), che elencano tutte le proprietà del nodo (formattato in modo appropriato). La rappresentazione predefinita per l’estensione .res, o richieste senza estensione di richiesta, consiste nello spool della risorsa (ove possibile).
* Per la gestione degli errori HTTP (codici 403 o 404), Sling cerca uno script all’indirizzo:

   * il percorso /apps/sling/servlet/errorhandler per gli script [personalizzati](/help/sites-developing/customizing-errorhandler-pages.md)
   * oppure la posizione degli script standard /libs/sling/servlet/errorhandler/403.esp o 404.esp, rispettivamente.

Se per una determinata richiesta sono richiesti più script, viene selezionato lo script con la corrispondenza migliore. Più specifica è una partita, meglio è. in altre parole, più il selettore corrisponde meglio, indipendentemente da eventuali estensioni di richiesta o dalla corrispondenza del nome del metodo.

Ad esempio, prendere in considerazione una richiesta per accedere alla risorsa`/content/corporate/jobs/developer.print.a4.html`di tipo`sling:resourceType="hr/jobs"`

Presupponendo che sia presente il seguente elenco di script nella posizione corretta:

1. `GET.esp`
1. `jobs.esp`
1. `html.esp`
1. `print.esp`
1. `print.html.esp`
1. `print/a4.esp`
1. `print/a4/html.esp`
1. `print/a4.html.esp`

Quindi l&#39;ordine delle preferenze sarebbe (8) - (7) - (6) - (5) - (4) - (3) - (2) - (1).

Oltre ai tipi di risorse (definiti principalmente dalla `sling:resourceType` proprietà) è presente anche il super type della risorsa. Questo è generalmente indicato dalla `sling:resourceSuperType` proprietà. Questi super tipi vengono considerati anche quando si tenta di trovare uno script. Il vantaggio dei super tipi di risorse è che possono formare una gerarchia di risorse in cui il tipo di risorsa predefinito `sling/servlet/default` (utilizzato dai servlet predefiniti) è effettivamente il livello principale.

Il super tipo di risorsa può essere definito in due modi:

* dalla `sling:resourceSuperType` proprietà della risorsa.
* dalla `sling:resourceSuperType` proprietà del nodo a cui `sling:resourceType` punta.

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




La gerarchia di tipo /x è [ c, b, a, &lt;default>] mentre per /y la gerarchia è [ c, a,

#### Gli script Sling non possono essere chiamati direttamente {#sling-scripts-cannot-be-called-directly}

All&#39;interno di Sling, gli script non possono essere richiamati direttamente in quanto ciò violerebbe il concetto rigoroso di server REST; potete combinare risorse e rappresentazioni.

Se si chiama la rappresentazione (lo script) direttamente, si nasconde la risorsa all&#39;interno dello script, in modo che il framework (Sling) non ne sia più a conoscenza. Così si perdono alcune caratteristiche:

* gestione automatica di metodi http diversi da GET, inclusi:

   * POST, PUT, DELETE che vengono gestiti con un&#39;implementazione standard
   * lo `POST.jsp` script nel percorso sling:resourceType

* l&#39;architettura del codice non è più pulita né strutturata come dovrebbe; di importanza primaria per lo sviluppo su larga scala

### API Sling {#sling-api}

Questo utilizza il pacchetto Sling API, org.apache.sling.&amp;ast; e librerie di tag.

### Riferimento a elementi esistenti mediante sling:include {#referencing-existing-elements-using-sling-include}

Una considerazione finale è la necessità di fare riferimento agli elementi esistenti all&#39;interno degli script.

Script più complessi (aggregazione di script) potrebbero dover accedere a più risorse (ad esempio, navigazione, barra laterale, piè di pagina, elementi di un elenco) e farlo includendo la *risorsa*.

A questo scopo è possibile utilizzare il comando sling:include(&quot;/&lt;percorso>/&lt;risorsa>&quot;). Ciò includerà effettivamente la definizione della risorsa di riferimento, come nell&#39;istruzione seguente che fa riferimento a una definizione esistente per il rendering delle immagini:

```xml
%><sling:include resourceType="geometrixx/components/image/img"/><%
```

## OSGI {#osgi}

OSGi definisce un&#39;architettura per lo sviluppo e la distribuzione di applicazioni e librerie modulari (o sistema di moduli dinamici per Java). I contenitori OSGi consentono di suddividere l’applicazione in singoli moduli (file JAR con ulteriori metadati e denominati bundle nella terminologia OSGi) e di gestire le interdipendenze tra di essi con:

* servizi implementati all&#39;interno del contenitore
* un contratto tra il contenitore e la vostra applicazione

Questi servizi e contratti forniscono un&#39;architettura che consente ai singoli elementi di scoprire l&#39;un l&#39;altro in modo dinamico per la collaborazione.

Un framework OSGi offre quindi il caricamento/scaricamento dinamico, la configurazione e il controllo di questi bundle, senza necessità di riavvio.

>[!NOTE]
>
>Informazioni complete sulla tecnologia OSGi sono disponibili sul sito Web [OSGi](https://www.osgi.org).
>
>In particolare, la pagina Basic Education contiene una serie di presentazioni ed esercitazioni.

Questa architettura consente di estendere Sling con moduli specifici dell&#39;applicazione. Sling, e quindi CQ5, utilizza l’implementazione [Apache Felix](https://felix.apache.org/) di OSGI (iniziativa Open Services Gateway) e si basa sulle specifiche OSGi Service Platform Release 4 versione 4.2. Sono entrambe raccolte di bundle OSGi in esecuzione in un framework OSGi.

Questo consente di eseguire le azioni seguenti su uno dei pacchetti all&#39;interno dell&#39;installazione:

* install
* start
* stop
* aggiorna
* uninstall
* vedere lo stato corrente
* accedere a informazioni più dettagliate (ad esempio nome simbolico, versione, posizione, ecc.) sui bundle specifici

Per ulteriori informazioni, consulta [Console](/help/sites-deploying/web-console.md)Web, Configurazione [](/help/sites-deploying/configuring-osgi.md) OSGI e Impostazioni [di configurazione](/help/sites-deploying/osgi-configuration-settings.md) OSGi.

## Oggetti di sviluppo nell’ambiente AEM {#development-objects-in-the-aem-environment}

Sono interessati allo sviluppo:

**Elemento** Un elemento è un nodo o una proprietà.

Per informazioni dettagliate sulla manipolazione degli oggetti Item, vedere [Javadocs](https://docs.adobe.com/docs/en/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Item.html) dell&#39;interfaccia javax.jcr.Item

**I nodi (e le relative proprietà)** e le relative proprietà sono definiti nella specifica JCR API 2.0 (JSR 283). memorizzano il contenuto, le definizioni degli oggetti, gli script di rendering e altri dati.

I nodi definiscono la struttura del contenuto e le relative proprietà memorizzano il contenuto e i metadati effettivi.

I nodi di contenuto guidano il rendering. Sling ottiene il nodo di contenuto dalla richiesta in entrata. La proprietà sling:resourceType di questo nodo punta al componente di rendering Sling da utilizzare.

Un nodo, che è un nome JCR, è anche chiamato risorsa nell&#39;ambiente Sling.

Ad esempio, per ottenere le proprietà del nodo corrente, è possibile utilizzare il seguente codice nello script:

`PropertyIterator properties = currentNode.getProperties();`

Con currentNode come oggetto nodo corrente.

Per ulteriori informazioni sulla manipolazione degli oggetti Node, vedere [Javadocs](https://docs.adobe.com/docs/en/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Node.html).

**Widget** In AEM tutti gli input dell’utente vengono gestiti tramite widget. Spesso sono utilizzati per controllare la modifica di un contenuto.

Le finestre di dialogo sono create combinando i widget.

AEM è stato sviluppato utilizzando la libreria ExtJS di widget.

**Finestra di dialogo** Una finestra di dialogo è un tipo speciale di widget.

Per modificare il contenuto, AEM utilizza le finestre di dialogo definite dallo sviluppatore di applicazioni. Combinano una serie di widget per presentare all’utente tutti i campi e le azioni necessari per modificare il contenuto correlato.

Le finestre di dialogo vengono inoltre utilizzate per modificare i metadati e per vari strumenti amministrativi.

**Componente** Un componente software è un elemento di sistema che offre un servizio o un evento predefinito e può comunicare con altri componenti.

In AEM un componente viene spesso utilizzato per rappresentare il contenuto di una risorsa. Quando la risorsa è una pagina, il componente che la rende è un componente di primo livello o un componente di pagina. Tuttavia, un componente non deve eseguire il rendering del contenuto né essere collegato a una risorsa specifica; ad esempio, un componente di navigazione visualizzerà informazioni su più risorse.

La definizione di un componente include:,

* il codice utilizzato per il rendering del contenuto
* una finestra di dialogo per l&#39;input dell&#39;utente e la configurazione del contenuto risultante.

**Modello** Un modello è la base per un tipo specifico di pagina. Quando create una pagina nella scheda Siti Web, l’utente deve selezionare un modello. La nuova pagina viene quindi creata copiando questo modello.

Un modello è una gerarchia di nodi con la stessa struttura della pagina da creare, ma senza alcun contenuto effettivo.

Definisce il componente della pagina utilizzato per rappresentare la pagina e il contenuto predefinito (contenuto principale principale). Il contenuto definisce il rendering come AEM è incentrato sui contenuti.

**Componente pagina (componente di livello principale)** Il componente da utilizzare per il rendering della pagina.

**Pagina** Una pagina è un&#39;istanza di un modello.

Una pagina ha un nodo gerarchico di tipo cq:Page e un nodo di contenuto di tipo cq:PageContent. La proprietà sling:resourceType del nodo di contenuto punta al componente Pagina utilizzato per il rendering della pagina.

Ad esempio, per ottenere il nome della pagina corrente, è possibile utilizzare il seguente codice nello script:

S`tring pageName = currentPage.getName();`

Con currentPage come oggetto pagina corrente. Per ulteriori informazioni sulla manipolazione degli oggetti Page, vedere [Javadocs](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/Page.html).

**Page Manager** Il gestore pagine è un&#39;interfaccia che fornisce metodi per le operazioni a livello di pagina.

Ad esempio, per ottenere la pagina contenente una risorsa, è possibile utilizzare il seguente codice nello script:

Page myPage = pageManager.getContainPage(myResource);

PageManager è l&#39;oggetto di gestione delle pagine e myResource un oggetto risorsa. Per ulteriori informazioni sui metodi forniti dal gestore delle pagine, vedere [Javadocs](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageManager.html).

## Struttura all&#39;interno del repository {#structure-within-the-repository}

L&#39;elenco seguente fornisce una panoramica della struttura che verrà visualizzata nella directory archivio.

>[!CAUTION]
>
>Le modifiche a questa struttura, o ai file al suo interno, devono essere apportate con attenzione.
>
>Le modifiche sono necessarie quando si sta sviluppando, ma occorre fare in modo di comprendere appieno le implicazioni delle modifiche apportate.

>[!CAUTION]
>
>Non è necessario modificare nulla nel `/libs` percorso. Per la configurazione e altre modifiche, copiate l’elemento da `/libs` a `/apps` e apportate eventuali modifiche all’interno di `/apps`.

* `/apps`

   Applicazione correlata; include definizioni di componenti specifiche per il sito Web. I componenti che si sviluppano possono essere basati sui componenti forniti in `/libs/foundation/components`.

* `/content`

   Contenuto creato per il sito Web.

* `/etc`

* `/home`

   Informazioni utente e gruppo.

* `/libs`

   Librerie e definizioni che appartengono al nucleo di AEM. Le sottocartelle in `/libs` rappresentano le funzioni predefinite di AEM, ad esempio ricerca o replica. Il contenuto di non `/libs` deve essere modificato in quanto influisce sul funzionamento di AEM. Le funzioni specifiche del sito Web devono essere sviluppate in `/apps` (consultate [Personalizzazione di componenti e altri elementi](/help/sites-developing/dev-guidelines-bestpractices.md#customizing-components-and-other-elements)).

* `/tmp`

   Area di lavoro temporanea.

* `/var`

   file che cambiano e vengono aggiornati dal sistema; come registri di controllo, statistiche, gestione degli eventi. La sottocartella `/var/classes` contiene i servlet Java nei moduli di origine e compilati generati dagli script dei componenti.

## Ambienti {#environments}

Con AEM un ambiente di produzione è spesso costituito da due tipi diversi di istanze: le istanze [](/help/sites-deploying/deploy.md#author-and-publish-installs)Autore e Pubblica.

## Il dispatcher {#the-dispatcher}

Il dispatcher è lo strumento di Adobe per il caching e/o il bilanciamento del carico. Ulteriori informazioni sono disponibili [nel Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/user-guide.html).

## FileVault (sistema di revisione dell&#39;origine) {#filevault-source-revision-system}

FileVault fornisce al repository JCR la mappatura del file system e il controllo della versione. Può essere utilizzato per gestire progetti di sviluppo AEM con il supporto completo per la memorizzazione e il controllo delle versioni di codice di progetto, contenuti, configurazioni e così via, nei sistemi di controllo delle versioni standard (ad esempio, Subversion).

Per informazioni dettagliate, consultate la documentazione dello strumento [](/help/sites-developing/ht-vlttool.md) FileVault.

## Flussi di lavoro {#workflows}

Il contenuto è spesso soggetto a processi organizzativi, compresi passaggi quali l&#39;approvazione e la disconnessione da parte di vari partecipanti. Questi processi possono essere rappresentati come flussi di lavoro, [definiti e sviluppati in AEM](/help/sites-developing/workflows-models.md), quindi applicati alle pagine [di contenuto](/help/sites-administering/workflows.md) appropriate o alle risorse [](/help/assets/assets-workflow.md) digitali, a seconda delle necessità.

Workflow Engine viene utilizzato per gestire l’implementazione dei flussi di lavoro e la successiva applicazione ai contenuti.

## Gestione multisito {#multi-site-management}

Multi Site Manager (MSM) consente di gestire facilmente più siti Web che condividono contenuti comuni. MSM consente di definire le relazioni tra i siti in modo che le modifiche di contenuto in un sito vengano automaticamente replicate in altri siti.

Ad esempio, i siti Web sono spesso disponibili in più lingue per il pubblico internazionale. Quando il numero di siti nella stessa lingua è basso (da tre a cinque), è possibile eseguire un processo manuale per la sincronizzazione dei contenuti tra siti. Tuttavia, non appena il numero dei siti cresce o quando sono coinvolte più lingue, diventa più efficiente automatizzare il processo.

* Gestire in modo efficiente versioni in diverse lingue di un sito Web.
* Aggiorna automaticamente uno o più siti in base a un sito di origine:

   * Applica una struttura di base comune e utilizza contenuti comuni per più siti.
   * Ottimizzate l&#39;utilizzo delle risorse disponibili.
   * Mantenere un aspetto e un aspetto comuni.
   * Concentrate gli sforzi sulla gestione dei contenuti che differiscono tra i siti.

Per ulteriori informazioni, consulta [Multi Site Manager](/help/sites-administering/msm.md).