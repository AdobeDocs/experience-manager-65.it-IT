---
title: Tecniche consigliate per il test delle prestazioni
seo-title: Best Practices for Performance Testing
description: Questo articolo illustra le strategie e le metodologie generali utilizzate per i test delle prestazioni, nonché alcuni degli strumenti disponibili per assistere il processo.
seo-description: This article outlines the overall strategies and methodologies used for performance testing as well as some of the tools that are available to assist in the process.
uuid: ab8720d6-b864-4d00-9e07-2e1699cfe7db
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 669018a0-f6ef-42b2-9c6f-83d7dd5a7095
exl-id: fcac75e1-15c1-4a37-8d43-93c95267b903
source-git-commit: b6de561422bc3533eef153b13d2c65b4cb7e0387
workflow-type: tm+mt
source-wordcount: '1897'
ht-degree: 0%

---

# Tecniche consigliate per il test delle prestazioni{#best-practices-for-performance-testing}

## Introduzione {#introduction}

Il test delle prestazioni è una parte importante di qualsiasi implementazione AEM. A seconda dei requisiti del cliente, è possibile eseguire test delle prestazioni sulle istanze di pubblicazione, sulle istanze dell’autore o su entrambe.

Questa documentazione descriverà le strategie e le metodologie generali per l’esecuzione dei test di prestazioni, nonché alcuni degli strumenti messi a disposizione dall’Adobe per facilitare il processo. Infine, analizzeremo alcuni degli strumenti disponibili nella AEM 6 per facilitare la regolazione delle prestazioni, sia dal punto di vista dell’analisi del codice che della configurazione del sistema.

### Simulazione della realtà {#simulating-reality}

La cosa più importante quando si eseguono test delle prestazioni è assicurarsi di imitare un ambiente di produzione il più vicino possibile. Anche se questo può essere spesso difficile, è imperativo garantire la precisione di tali test. Quando si lavora alla progettazione di test delle prestazioni, è importante tenere conto dei seguenti punti:

* Contenuti simili a quelli di produzione

Molte misurazioni delle prestazioni in AEM, come il tempo di risposta della query, possono essere influenzate dalle dimensioni del contenuto sul sistema. È importante assicurarsi che l’ambiente di test disponga di una copia del più simile possibile dei dati di produzione.

* Codice di produzione

La versione AEM e gli hotfix distribuiti in produzione devono essere gli stessi nell&#39;ambiente di test. È inoltre importante testare la versione del codice distribuito in produzione.

* Hardware e configurazione di rete simili a quelli della produzione

I test saranno privi di senso senza un ambiente che assomigli il più possibile alla produzione. Idealmente, le specifiche hardware, le interfacce di rete, i bilanciatori di carico e la rete CDN dovrebbero essere identici alla produzione nell&#39;ambiente di prova.

* Carico di produzione

Molti problemi di prestazioni non vengono visti finché il sistema non è sotto carico pesante. Le buone prove di prestazione dovrebbero simulare il carico che i sistemi di produzione saranno sotto il loro picco.

### Impostazione degli obiettivi {#setting-goals}

Prima di iniziare il test delle prestazioni, è necessario impostare requisiti non funzionali per specificare i tempi di caricamento e risposta. Se effettui la migrazione da un sistema esistente, assicurati che il tempo di risposta sia simile ai valori di produzione correnti. Per il carico, è meglio prendere il carico di picco corrente e raddoppiarlo. Questo assicurerà che il sito web possa continuare a funzionare bene mentre cresce.

### Strumenti {#tools}

Ci sono molti strumenti di test delle prestazioni disponibili sul mercato. Quando si esegue uno strumento di generazione del carico, è importante garantire che i computer che eseguono i test dispongano di una larghezza di banda di rete sufficiente. In caso contrario, una volta che la macchina di prova raggiunge i limiti della sua connessione, non verrà generato alcun carico aggiuntivo sull&#39;ambiente sottoposto a prova.

#### Strumenti di test {#testing-tools}

* dell’Adobe **Giorno difficile** può essere utilizzato per generare carico sulle istanze AEM e raccogliere dati sulle prestazioni. Il team di progettazione AEM di Adobe utilizza effettivamente lo strumento per eseguire il test di carico del prodotto AEM stesso. Gli script eseguiti in Tough Day sono configurati tramite file di proprietà e file XML JMX. Per ulteriori informazioni, consulta la sezione [Documentazione del giorno difficile](/help/sites-developing/tough-day.md).

* AEM fornisce strumenti pronti all’uso per visualizzare rapidamente query, richieste e messaggi di errore problematici. Per ulteriori informazioni, consulta la sezione [Strumenti di diagnosi](/help/sites-administering/operations-dashboard.md#diagnosis-tools) sezione della documentazione del dashboard delle operazioni.
* Apache fornisce un prodotto chiamato **JMeter** che può essere utilizzato per i test di prestazioni e carico e per il comportamento funzionale. È un software open source e gratuito da utilizzare, ma ha un set di funzioni più piccolo rispetto ai prodotti aziendali e una curva di apprendimento più ampia. JMeter è disponibile sul sito web di Apache all&#39;indirizzo [https://jmeter.apache.org/](https://jmeter.apache.org/)

* **Load Runner** è un prodotto di test del carico di livello enterprise. È disponibile una versione di valutazione gratuita. Ulteriori informazioni sono disponibili all&#39;indirizzo [https://www.microfocus.com/en-us/products/loadrunner-load-testing/overview](https://www.microfocus.com/en-us/products/loadrunner-load-testing/overview)

* Strumenti di test del carico basati su cloud come [Vicino](https://www.neustar.biz/services/web-performance/load-testing) può essere utilizzato anche.
* Quando si tratta di testare siti web mobili o reattivi, è necessario utilizzare un set separato di strumenti. Funzionano riducendo la larghezza di banda della rete, simulando connessioni mobili più lente come 3G o EDGE. Tra gli strumenti più utilizzati vi sono:

   * **[Condizionatore di collegamento di rete](https://nshipster.com/network-link-conditioner/)** - fornisce un&#39;interfaccia utente facile da usare e funziona a un livello abbastanza basso sullo stack di rete. Include le versioni per OS X e iOS;
   * [**Charles**](https://www.charlesproxy.com/) - applicazione proxy di debug Web che, oltre a diversi altri utilizzi, fornisce la limitazione della rete. Le versioni sono fornite per Windows, OS X e Linux.

#### Strumenti di ottimizzazione {#optimization-tools}

**Monitoraggio**

La [Monitoraggio delle prestazioni](/help/sites-deploying/monitoring-and-maintaining.md#monitoring-performance) La documentazione è una buona risorsa per strumenti e metodi che possono essere utilizzati per diagnosticare i problemi e individuare le aree per la messa a punto.

**Modalità sviluppatore nell’interfaccia utente touch**

Una delle nuove funzioni nell’interfaccia touch di AEM 6 è la modalità Sviluppatore . Così come gli autori possono passare dalla modalità di modifica a quella di anteprima, gli sviluppatori possono passare alla modalità di sviluppo nell’interfaccia utente dell’autore per visualizzare il tempo di rendering per ciascuno dei componenti della pagina e per vedere le tracce di stack di eventuali errori. Per ulteriori informazioni sulla modalità sviluppatore, consulta questo [Presentazione di CQ Gems](https://docs.adobe.com/content/ddc/en/gems/aem-6-0-developer-mode.html).

**Utilizzo di rlog.jar per leggere i registri delle richieste**

Per un&#39;analisi più completa della richiesta accede a un sistema di AEM, `rlog.jar` può essere utilizzato per cercare e ordinare `request.log` file generati AEM. Questo file jar è incluso con un&#39;installazione AEM nel `/crx-quickstart/opt/helpers` cartella. Per ulteriori informazioni sullo strumento di registro e sul registro delle richieste in generale, consulta la [Monitoraggio e manutenzione](/help/sites-deploying/monitoring-and-maintaining.md) documentazione.

**Strumento Spiega query**

La [Strumento Spiega query](/help/sites-administering/operations-dashboard.md#explain-query) in ACS AEM Tools può essere utilizzato per visualizzare gli indici utilizzati durante l&#39;esecuzione di una query. Questo può essere molto utile quando si ottimizzano le query in esecuzione lenta.

**Strumenti PageSpeed**

Gli strumenti PageSpeed di Google offrono analisi del sito per rispettare le best practice per le prestazioni della pagina, oltre a un plug-in che può essere installato insieme al dispatcher su un’istanza Apache per ulteriori ottimizzazioni. Per ulteriori informazioni, consulta la sezione [Sito Web degli strumenti PageSpeed](https://developers.google.com/speed/pagespeed/).

## Ambiente di authoring {#author-environment}

### Esecuzione dei test {#performing-tests}

Per eseguire test delle prestazioni nell’ambiente di authoring è necessario simulare l’esperienza degli autori di produzioni. Ciò significa che le installazioni dell’autore devono contenere tutti i componenti, i bundle OSGi, la personalizzazione dell’interfaccia utente, gli indici personalizzati e qualsiasi altra aggiunta in atto per le istanze dell’autore di produzione.

Sono disponibili molti framework di automazione progettati per le prestazioni e i test di carico. Gli script personalizzati possono essere registrati in questi strumenti e quindi riprodotti per simulare un picco di autori che eseguono attività di creazione e attivazione di contenuti simili contemporaneamente. Si consiglia di utilizzare lo strumento Giorno difficile per simulare attività come il caricamento di migliaia di risorse o l’attivazione di un gran numero di pagine.

Per i tipi di ambienti con requisiti di caricamento di risorse o authoring delle pagine pesanti, è fondamentale utilizzare strumenti come Tough Day per garantire che l’ambiente funzioni in modo efficiente sotto il carico di picco. [WebDAV](/help/sites-administering/webdav-access.md) è uno strumento che non richiede script e può essere utilizzato anche per caricare grandi quantità di risorse.

#### Passaggi specifici di MongoDB {#mongodb-specific-steps}

Nei sistemi con backend MongoDB, AEM fornisce diversi [JMX](/help/sites-administering/jmx-console.md) MBeans che devono essere monitorati durante l&#39;esecuzione di test di carico o prestazioni:

* La **Statistiche di cache consolidate** MBean. È accessibile direttamente da:

`https://server:port/system/console/jmx/org.apache.jackrabbit.oak%3Aid%3D6%2Cname%3D%22Consolidated+Cache+statistics%22%2Ctype%3D%22ConsolidatedCacheStats%22`

Per la cache denominata **Document-Diff**, il tasso di hit deve essere superiore `.90`. Se la percentuale di hit scende al di sotto del 90%, è probabile che sarà necessario modificare il `DocumentNodeStoreService` configurazione. Ad Adobe, il supporto per i prodotti può consigliare impostazioni ottimali per il tuo ambiente.

* La **Statistiche archivio Oak** Fagiolo. È accessibile direttamente da:

`https://server:port/system/console/jmx/org.apache.jackrabbit.oak%3Aid%3D16%2Cname%3D%22Oak+Repository+Statistics%22%2Ctype%3D%22RepositoryStats%22`

La **ObservationQueueMaxLength** la sezione mostrerà il numero di eventi nella coda di osservazione di Oak nelle ultime ore, minuti, secondi e settimane. Trova il maggior numero di eventi nella sezione &quot;per ora&quot;. Questo numero deve essere confrontato con il `oak.observation.queue-length` impostazione. Se il numero più alto indicato per la coda di osservazione supera il `queue-length` impostazione:

1. Crea un file denominato: `com.adobe.granite.repository.impl.SlingRepositoryManager.cfg` contenente il parametro `oak.observation.queue‐length=50000`
1. Posizionalo nella cartella /crx-quickstart/install .

>[!NOTE]
>Vedi anche l&#39;articolo KB su [AEM 6.x | Suggerimenti per ottimizzare le prestazioni](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html)

L’impostazione predefinita è 10.000, ma la maggior parte delle implementazioni di solito deve portarla a 20.000 o 50.000.

## Ambiente di pubblicazione {#publish-environment}

### Esecuzione dei test {#performing-tests-1}

La parte più importante di una distribuzione che deve essere soggetta a test di carico è l’ambiente di pubblicazione o dispatcher rivolto all’utente finale.

Strumenti di test automatizzati di terze parti possono essere utilizzati per testare le prestazioni del sito web. Questi strumenti ti consentono di registrare i passaggi che gli utenti attraversano sul sito ed eseguire molte di queste sessioni contemporaneamente per simulare il carico tipico di un sito web di produzione.

La maggior parte dei siti web di produzione dispone di ottimizzazioni come il caching del dispatcher e una rete di distribuzione dei contenuti. Quando esegui il test, assicurati che queste ottimizzazioni siano disponibili anche per l’ambiente di test. Oltre a monitorare i tempi di risposta per gli utenti finali, è anche necessario monitorare le metriche di sistema sui server e i dispatcher di pubblicazione per garantire che il sistema non sia vincolato dalle risorse hardware.

Su un sistema che non richiede un livello elevato di personalizzazione, il dispatcher dovrebbe memorizzare nella cache la maggior parte delle richieste. Di conseguenza, il carico sull&#39;istanza di pubblicazione dovrebbe rimanere relativamente piatto. Se è necessario un alto livello di personalizzazione, si consiglia di utilizzare tecnologie come iFrames o richieste di AJAX per il contenuto personalizzato in modo da consentire il maggior numero possibile di cache del dispatcher.

Per i test di base, Apache Bench può essere utilizzato per misurare i tempi di risposta dei server web e aiutare a creare un carico per misurare cose come perdite di memoria. Per ulteriori informazioni, consulta l’esempio nella sezione [Documentazione di monitoraggio](/help/sites-deploying/monitoring-and-maintaining.md#apache-bench).

## Risoluzione dei problemi di prestazioni {#troubleshooting-performance-issues}

Dopo aver eseguito i test delle prestazioni sull&#39;istanza dell&#39;autore, tutti i problemi dovranno essere esaminati, diagnosticati e risolti. È possibile utilizzare diversi strumenti e tecniche per eseguire analisi e risolvere i problemi:

* È possibile controllare [Registro delle prestazioni della richiesta](/help/sites-administering/operations-dashboard.md#request-performance) nel dashboard delle operazioni. Questo strumento può essere utilizzato per identificare le richieste di pagine lente
* Analizzare le query lente in esecuzione con il [Strumento Prestazioni query](/help/sites-administering/operations-dashboard.md#query-performance)

* Controlla l&#39;elenco degli errori per eventuali errori o avvisi. Per ulteriori informazioni, consulta [Registrazione](/help/sites-deploying/configure-logging.md)
* Monitorare le risorse hardware del sistema, ad esempio l&#39;utilizzo della memoria e della CPU, l&#39;I/O del disco o l&#39;I/O di rete. Tali risorse sono spesso la causa di colli di bottiglia delle prestazioni
* Ottimizza l’architettura delle pagine e il modo in cui vengono indirizzate per ridurre al minimo l’uso dei parametri URL, in modo da consentire il maggior numero possibile di memorizzazione in cache
* Segui [Ottimizzazione delle prestazioni](/help/sites-deploying/configuring-performance.md) e [Suggerimenti per l’ottimizzazione delle prestazioni](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html) documentazione

* Se sono presenti problemi nella modifica di determinate pagine o componenti nelle istanze dell&#39;autore, utilizza la modalità TouchUI Developer per controllare la pagina in questione. Questo fornisce un raggruppamento di ogni area di contenuto della pagina e del relativo tempo di caricamento
* Minimizza tutti i JS e i CSS sul sito. Per ulteriori informazioni su come eseguire questa operazione, consulta [post di blog](https://blogs.adobe.com/foxes/enable-js-and-css-minification/).
* Elimina CSS e JS incorporati dai componenti. Devono essere inclusi e minimizzati con le librerie lato client per ridurre al minimo il numero di richieste necessarie per eseguire il rendering della pagina
* Utilizza gli strumenti del browser come la scheda Rete di Chrome per controllare le richieste del server e vedere quali richiedono più tempo.

Una volta individuate le aree problematiche, il codice dell&#39;applicazione può essere esaminato per individuare ottimizzazioni delle prestazioni. Qualsiasi funzionalità preconfigurata AEM che non funziona correttamente può essere risolta con il supporto Adobe.
