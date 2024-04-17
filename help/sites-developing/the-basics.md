---
title: Concetti di base dell’AEM
description: Panoramica dei concetti fondamentali della struttura di Adobe Experience Manager (AEM) e del suo sviluppo, inclusa la comprensione di JCR, Sling, OSGi, Dispatcher, flussi di lavoro e MSM.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
exl-id: f6f32290-422e-4037-89d8-d9f414332e8e
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '3251'
ht-degree: 0%

---

# Concetti di base dell’AEM {#aem-core-concepts}

>[!NOTE]
>
>Prima di passare ai concetti di base di Adobe Experience Manager (AEM), l’Adobe consiglia di completare l’esercitazione WKND nella sezione [Guida introduttiva allo sviluppo per AEM Sites](/help/sites-developing/getting-started.md) documento. Esso include una panoramica del processo di sviluppo dell’AEM e un’introduzione ai concetti fondamentali.

## Prerequisiti per lo sviluppo sull’AEM {#prerequisites-for-developing-on-aem}

Per sviluppare in aggiunta all’AEM, ha bisogno delle seguenti competenze:

* Conoscenza di base delle tecniche di applicazione web, tra cui:

   * ciclo request-response (XMLHttpRequest / XMLHttpResponse)
   * HTML
   * CSS
   * JavaScript

* Conoscenza operativa di Experience Server (CRX), incluso Content Explorer
* Per lo sviluppo nell’interfaccia classica, è necessaria anche una conoscenza di base di JSP (JavaServer Pages), inclusa la possibilità di comprendere e modificare semplici esempi JSP.

Si consiglia inoltre di leggere e seguire i [Linee guida e best practice](/help/sites-developing/dev-guidelines-bestpractices.md).

## Archivio dei contenuti Java™ {#java-content-repository}

Lo standard Java™ Content Repository (JCR), [JSR 283](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/2.0/index.html)specifica un modo indipendente dal fornitore e indipendente dall’implementazione per accedere al contenuto in modo bidirezionale a livello granulare all’interno di un archivio di contenuti.

Il piombo delle specifiche è detenuto da Adobe Research (Switzerland) AG.

Il [API JCR 2.0](https://developer.adobe.com/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/index.html) pacchetto, javax.jcr.&amp;ast; viene utilizzato per l&#39;accesso diretto e la manipolazione del contenuto del repository.

## Experience Server (CRX) e Jackrabbit {#experience-server-crx-and-jackrabbit}

Experience Server fornisce i servizi di esperienza su cui si basa l’AEM, che possono essere utilizzati per creare applicazioni personalizzate e incorpora il Content Repository basato su Jackrabbit.

[Apache Jackrabbit](https://jackrabbit.apache.org/jcr/index.html) è un’implementazione open source, pienamente conforme, dell’API 2.0 JCR.

## Elaborazione richiesta Sling {#sling-request-processing}

### Introduzione a Sling {#introduction-to-sling}

L’AEM viene creato utilizzando [Sling](https://sling.apache.org/index.html): framework di applicazioni web basato sui principi REST che consente di sviluppare facilmente applicazioni orientate ai contenuti. Sling utilizza come archivio dati un archivio JCR, come Apache Jackrabbit o, in presenza di AEM, l’archivio contenuti CRX. Sling ha contribuito alla Apache Software Foundation; ulteriori informazioni sono disponibili su Apache.

Utilizzando Sling, il tipo di contenuto di cui eseguire il rendering non è la prima considerazione di elaborazione. Al contrario, la considerazione principale è se l’URL viene risolto in un oggetto di contenuto per il quale è possibile trovare uno script per eseguire il rendering. Questo fornisce un supporto eccellente agli autori di contenuti web per creare pagine facilmente personalizzate in base alle loro esigenze.

I vantaggi di questa flessibilità sono evidenti nelle applicazioni con un’ampia gamma di elementi di contenuto diversi o quando servono pagine facilmente personalizzabili. In particolare, quando si implementa un sistema di gestione dei contenuti web come WCM nella soluzione AEM.

Consulta [Scopri Sling in 15 minuti](https://sling.apache.org/documentation/getting-started/discover-sling-in-15-minutes.html) per i primi passaggi per lo sviluppo con Sling.

Il diagramma seguente spiega la risoluzione dello script Sling. Mostra come passare dalla richiesta HTTP al nodo di contenuto, dal nodo di contenuto al tipo di risorsa, dal tipo di risorsa allo script e quali variabili di script sono disponibili.

![Informazioni sulla risoluzione dello script Apache Sling](assets/sling-cheatsheet-01.png)

Il diagramma seguente spiega tutti i potenti, nascosti, parametri di richiesta che è possibile utilizzare quando si tratta di SlingPostServlet. Include il gestore predefinito per tutte le richieste POST, che offre opzioni infinite per la creazione, la modifica, l’eliminazione, la copia e lo spostamento dei nodi nell’archivio.

![Utilizzo di SlingPostServlet](assets/sling-cheatsheet-02.png)

### Sling è incentrato sui contenuti {#sling-is-content-centric}

Sling è *incentrato sui contenuti*. Ciò significa che l’elaborazione si concentra sul contenuto, in quanto ogni richiesta (HTTP) è mappata sul contenuto sotto forma di risorsa JCR (un nodo dell’archivio):

* la prima destinazione è la risorsa (nodo JCR) contenente il contenuto
* in secondo luogo, la rappresentazione, o script, si trova dalle proprietà della risorsa combinate con alcune parti della richiesta (ad esempio, selettori e/o estensione)

### Sling RESTful {#restful-sling}

Grazie alla filosofia incentrata sui contenuti, Sling implementa un server orientato a REST e quindi presenta un nuovo concetto nei framework delle applicazioni web. I vantaggi sono i seguenti:

* RESTful, non solo sulla superficie; le risorse e le rappresentazioni sono modellate correttamente all&#39;interno del server
* rimuove uno o più modelli di dati

   * in precedenza erano necessari i seguenti elementi: struttura URL, oggetti di business, schema DB;
   * ora è ridotto a: URL = risorsa = struttura JCR

### Scomposizione URL {#url-decomposition}

In Sling, l’elaborazione è guidata dall’URL della richiesta dell’utente. Questo definisce il contenuto da visualizzare con gli script appropriati. A questo scopo, le informazioni vengono estratte dall’URL.

Se analizzi il seguente URL:

```xml
https://myhost/tools/spy.printable.a4.html/a/b?x=12
```

È possibile suddividerlo nelle sue parti composite:

| protocollo | host | percorso contenuto | selettori | estensione |  | suffisso |  | parametri |
|---|---|---|---|---|---|---|---|---|
| https:// | miohost | strumenti/spia | .stampabile.a4. | html | / | a/b | ? | x=12 |

**protocollo** HTTP

**host** Nome del sito web.

**percorso contenuto** Percorso che specifica il contenuto da riprodurre. Utilizzato con l’estensione. In questo esempio, traducono in `tools/spy.html`.

**selettori** Utilizzato per metodi alternativi di rendering del contenuto; in questo esempio, una versione in formato A4 compatibile con la stampante.

**estensione** Formato contenuto; specifica anche lo script da utilizzare per il rendering.

**suffisso** Può essere utilizzato per specificare informazioni aggiuntive.

**parametri** Qualsiasi parametro necessario per il contenuto dinamico.

#### Da URL a contenuto e script {#from-url-to-content-and-scripts}

Utilizzando questi principi:

* la mappatura utilizza il percorso del contenuto estratto dalla richiesta per individuare la risorsa
* quando si trova la risorsa appropriata, il tipo di risorsa sling viene estratto e utilizzato per individuare lo script da utilizzare per il rendering del contenuto

L’immagine seguente illustra il meccanismo utilizzato, descritto più dettagliatamente nelle sezioni seguenti.

![chlimage_1-86](assets/chlimage_1-86a.png)

Con Sling, puoi specificare quale script esegue il rendering di una determinata entità (impostando il `sling:resourceType` nel nodo JCR. Questo meccanismo offre maggiore libertà rispetto a uno in cui lo script accede alle entità di dati (come farebbe un’istruzione SQL in uno script PHP) in quanto una risorsa può avere diverse rappresentazioni.

#### Mappatura delle richieste alle risorse {#mapping-requests-to-resources}

La richiesta è suddivisa ed è possibile estrarre le informazioni necessarie. Nell’archivio viene eseguita la ricerca della risorsa richiesta (nodo del contenuto):

* in primo luogo, Sling controlla se un nodo esiste nella posizione specificata nella richiesta; ad esempio, `../content/corporate/jobs/developer.html`
* se non viene trovato alcun nodo, l’estensione viene rilasciata e la ricerca ripetuta; ad esempio, `../content/corporate/jobs/developer`
* Se non viene trovato alcun nodo, Sling restituisce il codice http 404 (Not Found).

Sling consente anche di utilizzare come risorse elementi diversi dai nodi JCR, ma si tratta di una funzione avanzata.

### Individuazione dello script {#locating-the-script}

Quando si trova la risorsa appropriata (nodo di contenuto), il **tipo di risorsa sling** viene estratto. Questo è un percorso che individua lo script da utilizzare per il rendering del contenuto.

Percorso specificato da `sling:resourceType` può essere:

* assoluto
* relativo a un parametro di configurazione

  I percorsi relativi sono consigliati da Adobe in quanto aumentano la portabilità.

Tutti gli script Sling vengono memorizzati nelle sottocartelle di `/apps` o `/libs`, che viene ricercato in questo ordine (vedi [Personalizzazione di componenti e altri elementi](/help/sites-developing/dev-guidelines-bestpractices.md#customizing-components-and-other-elements)).

Altri punti da notare sono:

* quando il metodo (GET, POST) è obbligatorio, viene specificato in maiuscolo in base alla specifica HTTP, ad esempio jobs.POST.esp (vedi di seguito)
* sono supportati vari motori di script:

   * HTL (HTML Template Language, sistema di modelli lato server preferito e consigliato di Adobe Experience Manager per HTML): `.html`
   * Pagine ECMAScript (JavaScript) (esecuzione lato server): `.esp, .ecma`
   * Pagine Java™ Server (esecuzione lato server): `.jsp`
   * Java™ Servlet Compiler (esecuzione lato server): `.java`
   * Modelli JavaScript (esecuzione lato client): `.jst`

L&#39;elenco dei motori di script supportati dall&#39;istanza di AEM specificata è elencato nella console di gestione Felix ( `http://<host>:<port>/system/console/slingscripting`).

Inoltre, Apache Sling supporta l’integrazione con altri motori di script popolari (ad esempio Groovy, JRuby, Freemarker) e offre un modo per integrare nuovi motori di script.

Utilizzando l&#39;esempio precedente, se `sling:resourceType` è `hr/jobs` quindi per:

* Richieste GET/HEAD e URL con estensione html (tipi di richiesta predefiniti, formato predefinito)

  Lo script è /apps/hr/jobs/jobs.esp; l’ultima sezione di sling:resourceType forma il nome del file.

* Richieste POST (tutti i tipi di richiesta tranne GET/HEAD, il nome del metodo deve essere in maiuscolo)

  POST viene utilizzato nel nome dello script.

  Lo script è `/apps/hr/jobs/jobs.POST.esp`.

* URL in altri formati, che non terminano con .html

  Ad esempio `../content/corporate/jobs/developer.pdf`

  Lo script è `/apps/hr/jobs/jobs.pdf.esp`; il suffisso viene aggiunto al nome dello script.

* URL con selettori

  I selettori possono essere utilizzati per visualizzare lo stesso contenuto in un formato alternativo. Ad esempio, una versione compatibile con la stampante, un feed rss o un riepilogo.

  Se si considera una versione compatibile con la stampante in cui il selettore potrebbe essere *stampa*, come in `../content/corporate/jobs/developer.print.html`

  Lo script è `/apps/hr/jobs/jobs.print.esp`; il selettore viene aggiunto al nome dello script.

* Se non è definito sling:resourceType:

   * il percorso del contenuto viene utilizzato per cercare uno script appropriato (se ResourceTypeProvider basato sul percorso è attivo).

     Ad esempio, lo script per `../content/corporate/jobs/developer.html` genera una ricerca in `/apps/content/corporate/jobs/`.

   * viene utilizzato il tipo di nodo principale.

* Se non viene trovato alcuno script, viene utilizzato lo script predefinito.

  La rappresentazione predefinita è supportata come testo normale (.txt), HTML (.html) e JSON (.json), che elencano tutte le proprietà del nodo (formattate in modo appropriato). La rappresentazione predefinita per l’estensione .res, o per le richieste senza estensione di richiesta, consiste nello spool della risorsa (ove possibile).
* Per la gestione degli errori http (codici 403 o 404) Sling cerca uno script in:

   * la posizione /apps/sling/servlet/errorhandler per [script personalizzati](/help/sites-developing/customizing-errorhandler-pages.md)
   * o la posizione degli script standard /libs/sling/servlet/errorhandler/403.esp o 404.esp rispettivamente.

Se per una determinata richiesta sono applicabili più script, viene selezionato lo script con la corrispondenza migliore. Più specifica è una corrispondenza, migliore sarà; in altre parole, più il selettore corrisponderà, indipendentemente da qualsiasi estensione di richiesta o corrispondenza del nome del metodo.

Ad esempio, considera una richiesta di accesso alla risorsa
`/content/corporate/jobs/developer.print.a4.html`
di tipo
`sling:resourceType="hr/jobs"`

Supponendo di avere il seguente elenco di script nella posizione corretta:

1. `GET.esp`
1. `jobs.esp`
1. `html.esp`
1. `print.esp`
1. `print.html.esp`
1. `print/a4.esp`
1. `print/a4/html.esp`
1. `print/a4.html.esp`

Quindi l&#39;ordine di preferenza sarebbe (8) - (7) - (6) - (5) - (4) - (3) - (2) - (1).

Oltre ai tipi di risorse (definiti principalmente dalla `sling:resourceType` proprietà ), esiste anche il super tipo di risorsa. Questo è indicato dal `sling:resourceSuperType` proprietà. Questi super tipi vengono considerati anche quando si tenta di trovare uno script. Il vantaggio dei super-tipi di risorse è che possono formare una gerarchia di risorse in cui il tipo di risorsa predefinito `sling/servlet/default` (utilizzato dai servlet predefiniti) è effettivamente la radice.

Il super tipo di risorsa di una risorsa può essere definito in due modi:

* da `sling:resourceSuperType` della risorsa.
* da `sling:resourceSuperType` proprietà del nodo a cui è associato `sling:resourceType` punti.

Ad esempio:

* /

   * a
   * b

      * sling:resourceSuperType = a

   * c

      * sling:resourceSuperType = b

   * x

      * sling:resourceType = c

   * y

      * sling:resourceType = c
      * sling:resourceSuperType = a

Gerarchia dei tipi di:

* `/x`
   * è `[ c, b, a, <default>]`
* mentre per `/y`
   * la gerarchia è `[ c, a, <default>]`

Questo perché `/y` ha `sling:resourceSuperType` proprietà mentre `/x` does not e pertanto il relativo supertipo viene preso dal relativo tipo di risorsa.

#### Gli script Sling non possono essere chiamati direttamente {#sling-scripts-cannot-be-called-directly}

All’interno di Sling, gli script non possono essere chiamati direttamente in quanto ciò infrangerebbe il concetto rigoroso di server REST; è possibile combinare risorse e rappresentazioni.

Se chiami direttamente la rappresentazione (lo script), nascondi la risorsa all’interno dello script, pertanto il framework (Sling) non ne è più a conoscenza. In questo modo si perdono alcune funzionalità:

* gestione automatica di metodi http diversi da GET, tra cui:

   * POST, PUT, DELETE gestito con un’implementazione sling predefinita
   * il `POST.jsp` script nel percorso sling:resourceType

* l&#39;architettura del codice non è più pulita né strutturata in modo chiaro come dovrebbe essere; di primaria importanza per lo sviluppo su larga scala

### API Sling {#sling-api}

Questo utilizza il pacchetto API Sling, org.apache.sling.&amp;ast; e le librerie di tag.

### Riferimento a elementi esistenti mediante sling:include {#referencing-existing-elements-using-sling-include}

Un&#39;ultima considerazione è la necessità di fare riferimento agli elementi esistenti all&#39;interno degli script.

Gli script più complessi (aggregazione di script) devono accedere a più risorse (ad esempio, navigazione, barra laterale, piè di pagina, elementi di un elenco) e a tale scopo includere *resource*.

A questo scopo, utilizza sling:include(&quot;/&lt;path>/&lt;resource>&quot;). Ciò include effettivamente la definizione della risorsa di riferimento, come nell’istruzione seguente che fa riferimento a una definizione esistente per il rendering delle immagini:

```xml
%><sling:include resourceType="geometrixx/components/image/img"/><%
```

## OSGI {#osgi}

OSGi definisce un’architettura per lo sviluppo e la distribuzione di librerie e applicazioni modulari (nota anche come Dynamic Module System per Java™). I contenitori OSGi ti consentono di suddividere l’applicazione in singoli moduli (file jar con metadati aggiuntivi e denominati bundle nella terminologia OSGi) e di gestire le dipendenze incrociate tra di essi con:

* servizi implementati all’interno del contenitore
* un contratto tra il contenitore e l’applicazione

Questi servizi e contratti forniscono un’architettura che consente ai singoli elementi di scoprirsi dinamicamente a vicenda per collaborare.

Un framework OSGi offre quindi operazioni dinamiche di caricamento/scaricamento, configurazione e controllo di questi bundle, senza richiedere riavvii.

>[!NOTE]
>
>Per informazioni complete sulla tecnologia OSGi, visitare il sito [Sito Web OSGi](https://www.osgi.org).
>
>In particolare, la pagina Istruzione di base contiene una raccolta di presentazioni e tutorial.

Questa architettura consente di estendere Sling con moduli specifici per le applicazioni. Sling, e quindi CQ5, utilizza [Apache Felix](https://felix.apache.org/documentation/index.html) implementazione di OSGI (Open Services Gateway initiative) basata sulle specifiche della piattaforma di servizi OSGi Release 4 Version 4.2. Sono entrambe raccolte di bundle OSGi in esecuzione all’interno di un framework OSGi.

Questo consente di eseguire le azioni seguenti su uno qualsiasi dei pacchetti all’interno dell’installazione:

* installare
* inizio
* stop
* aggiorna
* disinstalla
* vedi lo stato
* accedere a informazioni più dettagliate (ad esempio, nome simbolico, versione e posizione) sui bundle specifici

Consulta [la console web](/help/sites-deploying/web-console.md), [Configurazione OSGI](/help/sites-deploying/configuring-osgi.md), e [Impostazioni configurazione OSGi](/help/sites-deploying/osgi-configuration-settings.md) per ulteriori informazioni.

## Oggetti di sviluppo nell’ambiente AEM {#development-objects-in-the-aem-environment}

Di seguito sono riportati gli elementi di maggiore interesse per lo sviluppo:

**Elemento** Un elemento è un nodo o una proprietà.

Per informazioni dettagliate sulla manipolazione degli oggetti Item, vedere [Documenti Java™](https://developer.adobe.com/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Item.html) dell’interfaccia javax.jcr.Item

**Nodo (e relative proprietà)** I nodi e le loro proprietà sono definiti nella specifica JCR API 2.0 (JSR 283). Memorizzano il contenuto, le definizioni degli oggetti, gli script di rendering e altri dati.

I nodi definiscono la struttura del contenuto e le relative proprietà memorizzano il contenuto effettivo e i metadati.

I nodi di contenuto guidano il rendering. Sling ottiene il nodo del contenuto dalla richiesta in ingresso. La proprietà sling:resourceType di questo nodo punta al componente di rendering Sling da utilizzare.

Un nodo, che è un nome JCR, è anche chiamato risorsa nell’ambiente Sling.

Ad esempio, per ottenere le proprietà del nodo corrente, puoi utilizzare il seguente codice nello script:

`PropertyIterator properties = currentNode.getProperties();`

CurrentNode è l&#39;oggetto nodo corrente.

Per ulteriori informazioni sulla manipolazione degli oggetti Node, vedere [Documenti Java™](https://developer.adobe.com/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Node.html).

**Widget** In AEM tutti gli input dell&#39;utente sono gestiti da widget. Queste vengono spesso utilizzate per controllare la modifica di un contenuto.

Le finestre di dialogo vengono create combinando widget.

L’AEM è stato sviluppato utilizzando la libreria ExtJS di widget.

**Finestra di dialogo** Una finestra di dialogo è un tipo speciale di widget.

Per modificare il contenuto, l’AEM utilizza le finestre di dialogo definite dallo sviluppatore dell’applicazione. Combinano una serie di widget per presentare all’utente tutti i campi e le azioni necessari per modificare il contenuto correlato.

Le finestre di dialogo vengono utilizzate anche per la modifica dei metadati e da vari strumenti di amministrazione.

**Componente** Un componente software è un elemento di sistema che offre un servizio o un evento predefinito e in grado di comunicare con altri componenti.

All’interno dell’AEM, un componente viene spesso utilizzato per riprodurre il contenuto di una risorsa. Quando la risorsa è una pagina, il componente di cui viene eseguito il rendering è denominato Componente di livello principale o Componente pagina. Tuttavia, un componente non deve eseguire il rendering del contenuto né essere collegato a una risorsa specifica. Ad esempio, un componente di navigazione visualizza informazioni su più risorse.

La definizione di un componente include quanto segue:

* il codice utilizzato per il rendering del contenuto
* una finestra di dialogo per l’input dell’utente e la configurazione del contenuto risultante.

**Modello** Un modello è la base per un tipo specifico di pagina. Durante la creazione di una pagina nella scheda Siti Web, l’utente deve selezionare un modello. La nuova pagina viene quindi creata copiando questo modello.

Un modello è una gerarchia di nodi con la stessa struttura della pagina da creare, ma senza alcun contenuto effettivo.

Definisce il componente Pagina utilizzato per eseguire il rendering della pagina e il contenuto predefinito (contenuto principale di primo livello). Il contenuto definisce il modo in cui viene riprodotto poiché l’AEM è incentrato sui contenuti.

**Componente Pagina (Componente Di Livello Superiore)** Componente da utilizzare per il rendering della pagina.

**Pagina** Una pagina è un’istanza di un modello.

Una pagina ha un nodo di gerarchia di tipo cq:Page e un nodo di contenuto di tipo cq:PageContent. La proprietà sling:resourceType del nodo di contenuto punta al componente Pagina utilizzato per il rendering della pagina.

Ad esempio, per ottenere il nome della pagina corrente, è possibile utilizzare il codice seguente nello script:

S`tring pageName = currentPage.getName();`

TcurrentPage è l&#39;oggetto della pagina corrente. Per ulteriori informazioni sulla manipolazione degli oggetti Page, vedere [Documenti Java™](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/Page.html).

**Gestione pagine** Il gestore pagine è un&#39;interfaccia che fornisce metodi per le operazioni a livello di pagina.

Ad esempio, per ottenere la pagina contenitore di una risorsa, puoi utilizzare il seguente codice nello script:

Page myPage = pageManager.getContainingPage(myResource);

PageManager è l&#39;oggetto di gestione pagina e myResource un oggetto risorsa. Per ulteriori informazioni sui metodi forniti dal gestore della pagina, vedi [Documenti Java™](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/PageManager.html).

## Struttura all’interno del repository {#structure-within-the-repository}

L’elenco seguente offre una panoramica della struttura visualizzata all’interno dell’archivio.

>[!CAUTION]
>
>Le modifiche a questa struttura, o ai file al suo interno, devono essere effettuate con cautela.
>
>Le modifiche sono necessarie durante lo sviluppo, ma è necessario assicurarsi di comprendere appieno le implicazioni di qualsiasi modifica apportata.

>[!CAUTION]
>
>Non modificare nulla nella `/libs` percorso. Per la configurazione e altre modifiche, copia l’elemento da `/libs` a `/apps` e apporta le modifiche necessarie entro `/apps`.

* `/apps`

  Relativo all’applicazione; include definizioni di componenti specifiche del sito web. I componenti sviluppati possono essere basati sui componenti predefiniti disponibili all’indirizzo `/libs/foundation/components`.

* `/content`

  Contenuto creato per il sito web.

* `/etc`

* `/home`

  Informazioni su utenti e gruppi.

* `/libs`

  Librerie e definizioni che appartengono al nucleo dell’AEM. Le sottocartelle in `/libs` rappresenta le funzioni predefinite dell’AEM, ad esempio ricerca o replica. Il contenuto in `/libs` non deve essere modificato in quanto influisce sul modo in cui funziona l’AEM. Le funzioni specifiche del sito web devono essere sviluppate in `/apps` (vedere [Personalizzazione di componenti e altri elementi](/help/sites-developing/dev-guidelines-bestpractices.md#customizing-components-and-other-elements)).

* `/tmp`

  Area di lavoro temporanea.

* `/var`

  File che vengono modificati e aggiornati dal sistema, ad esempio registri di controllo, statistiche e gestione degli eventi.

## Ambienti {#environments}

Con l’AEM, un ambiente di produzione è spesso costituito da due diversi tipi di istanze: [Creazione e pubblicazione di istanze](/help/sites-deploying/deploy.md#author-and-publish-installs).

## Dispatcher {#the-dispatcher}

Dispatcher è uno strumento di Adobe per il caching e/o il bilanciamento del carico. Ulteriori informazioni sono disponibili nella sezione [Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=it).

## FileVault (sistema di revisione sorgente) {#filevault-source-revision-system}

FileVault fornisce all’archivio JCR la mappatura del file system e il controllo della versione. Può essere utilizzato per gestire progetti di sviluppo AEM con supporto completo per l’archiviazione e il controllo delle versioni del codice del progetto, del contenuto, delle configurazioni e così via, nei sistemi di controllo delle versioni standard (ad esempio, Subversion).

Consulta la [Strumento FileVault](/help/sites-developing/ht-vlttool.md) per informazioni dettagliate.

## Flussi di lavoro {#workflows}

I contenuti sono spesso soggetti a processi organizzativi, tra cui passaggi quali l’approvazione e l’approvazione da parte di vari partecipanti. Questi processi possono essere rappresentati come flussi di lavoro, [definito e sviluppato nell’ambito dell’AEM](/help/sites-developing/workflows-models.md), quindi applicato al [pagine di contenuto appropriate](/help/sites-administering/workflows.md) o [risorse digitali](/help/assets/assets-workflow.md) secondo necessità.

Il motore dei flussi di lavoro consente di gestire l’implementazione dei flussi di lavoro e della successiva applicazione ai contenuti.

## Gestione multisito {#multi-site-management}

Multi Site Manager (MSM) consente di gestire facilmente più siti Web che condividono contenuti comuni. MSM consente di definire relazioni tra i siti in modo che le modifiche al contenuto in un sito vengano automaticamente replicate in altri siti.

Ad esempio, i siti web sono spesso disponibili in più lingue per il pubblico internazionale. Quando il numero di siti nella stessa lingua è basso (da tre a cinque), è possibile un processo manuale per la sincronizzazione dei contenuti tra siti diversi. Tuttavia, quando il numero di siti aumenta o sono coinvolte più lingue, diventa più efficiente automatizzare il processo.

* Gestire in modo efficiente le diverse versioni linguistiche di un sito Web.
* Aggiorna automaticamente uno o più siti in base a un sito di origine:

   * Applicazione di una struttura di base comune e utilizzo di contenuti comuni su più siti.
   * Ottimizzare l’utilizzo delle risorse disponibili.
   * Mantenere un aspetto comune.
   * Concentrare gli sforzi sulla gestione dei contenuti che differiscono tra i siti.

Per ulteriori informazioni, consulta [Gestore multisito](/help/sites-administering/msm.md).
