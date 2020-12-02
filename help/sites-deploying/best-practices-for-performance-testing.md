---
title: Best practice per il test delle prestazioni
seo-title: Best practice per il test delle prestazioni
description: Questo articolo illustra le strategie e le metodologie globali utilizzate per i test delle prestazioni, nonché alcuni degli strumenti disponibili per assistere il processo.
seo-description: Questo articolo illustra le strategie e le metodologie globali utilizzate per i test delle prestazioni, nonché alcuni degli strumenti disponibili per assistere il processo.
uuid: ab8720d6-b864-4d00-9e07-2e1699cfe7db
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 669018a0-f6ef-42b2-9c6f-83d7dd5a7095
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1925'
ht-degree: 0%

---


# Best practice per il test delle prestazioni{#best-practices-for-performance-testing}

## Introduzione {#introduction}

Il test delle prestazioni è una parte importante di qualsiasi implementazione AEM. A seconda delle esigenze del cliente, è possibile che vengano eseguiti test delle prestazioni sulle istanze di pubblicazione, di creazione o su entrambi.

Questa documentazione descriverà le strategie e le metodologie generali per l&#39;esecuzione dei test di prestazioni, nonché alcuni degli strumenti messi a disposizione dal Adobe  per assistere il processo. Infine, analizzeremo alcuni degli strumenti disponibili in AEM 6 per l&#39;ottimizzazione delle prestazioni, sia dal punto di vista dell&#39;analisi del codice che della configurazione del sistema.

### Simulazione della realtà {#simulating-reality}

La cosa più importante nell&#39;esecuzione dei test di performance è assicurarsi che l&#39;ambiente di produzione venga riprodotto il più vicino possibile. Anche se questo può essere spesso difficile, è indispensabile garantire la precisione di tali prove. Durante la progettazione di test di prestazioni, è importante tenere conto dei seguenti punti:

* Contenuti simili a quelli della produzione

Molte misurazioni delle prestazioni in AEM, come il tempo di risposta alle query, possono essere influenzate dalle dimensioni del contenuto nel sistema. È importante assicurarsi che l&#39;ambiente di prova disponga del più vicino possibile di una copia dei dati di produzione.

* Codice produzione

La versione AEM e gli hotfix distribuiti in produzione devono essere gli stessi nell&#39;ambiente di test. È inoltre importante verificare la versione del codice distribuito in produzione.

* Configurazione hardware e di rete simile a quella della produzione

I test saranno senza senso senza un ambiente che assomigli il più possibile alla produzione. Idealmente, le specifiche hardware, le interfacce di rete, i bilanciatori del carico e la CDN dovrebbero essere identici alla produzione nell&#39;ambiente di prova.

* Carico di produzione

Molti problemi di prestazioni non vengono visti fino a quando il sistema non è sotto carico. Buone prove di prestazioni dovrebbero simulare il carico che i sistemi di produzione saranno sotto al loro picco.

### Impostazione degli obiettivi {#setting-goals}

Prima di iniziare il test delle prestazioni, è necessario impostare requisiti non funzionali per specificare i tempi di caricamento e risposta. Se state eseguendo la migrazione da un sistema esistente, accertatevi che il tempo di risposta sia simile ai valori di produzione correnti. Per il caricamento, è meglio prendere il carico di picco corrente e raddoppiarlo. In questo modo, il sito Web continuerà a funzionare correttamente e a crescere.

### Strumenti {#tools}

Sono disponibili sul mercato numerosi strumenti di test delle prestazioni disponibili in commercio. Quando si esegue uno strumento di generazione del carico, è importante garantire che i computer che eseguono i test dispongano di larghezza di banda sufficiente. In caso contrario, quando la macchina di prova raggiunge i limiti della sua connessione, non verrà generato alcun carico aggiuntivo sull&#39;ambiente in fase di test.

#### Strumenti di test {#testing-tools}

*  strumento **Tough Day** del Adobe può essere utilizzato per generare carico sulle istanze AEM e raccogliere i dati sulle prestazioni.  team tecnico AEM Adobe utilizza effettivamente lo strumento per eseguire il test del carico del prodotto AEM stesso. Gli script eseguiti nel giorno di prova sono configurati tramite file di proprietà e file XML JMX. Per ulteriori informazioni, consultare la [documentazione del giorno duro](/help/sites-developing/tough-day.md).

* AEM fornisce strumenti preconfigurati per visualizzare rapidamente query problematiche, richieste e messaggi di errore. Per ulteriori informazioni, consultare la sezione [Strumenti di diagnostica](/help/sites-administering/operations-dashboard.md#diagnosis-tools) della documentazione del Pannello operazioni.
* Apache fornisce un prodotto denominato **JMeter** che può essere utilizzato per il test delle prestazioni e del carico e per il comportamento funzionale. È un software open source e gratuito da usare, ma ha un set di funzioni più piccolo rispetto ai prodotti aziendali e una curva di apprendimento più ampia. JMeter è disponibile sul sito Web di Apache all&#39;indirizzo [https://jmeter.apache.org/](https://jmeter.apache.org/)

* **Load** Runnerè un prodotto di test del carico di livello Enterprise. È disponibile una versione di valutazione gratuita. Ulteriori informazioni sono disponibili all&#39;indirizzo [https://www.microfocus.com/en-us/products/loadrunner-load-testing/overview](https://www.microfocus.com/en-us/products/loadrunner-load-testing/overview)

* È inoltre possibile utilizzare strumenti di test del carico basati su cloud come [Neustar](https://www.neustar.biz/services/web-performance/load-testing).
* Quando si tratta di testare siti Web mobili o reattivi, è necessario utilizzare un set di strumenti separato. Funzionano rallentando la larghezza di banda della rete, simulando connessioni mobili lente come 3G o EDGE. Tra gli strumenti più diffusi:

   * **[Condizionatore](https://nshipster.com/network-link-conditioner/)**  di collegamento di rete: consente di utilizzare facilmente l&#39;interfaccia utente e funziona a un livello abbastanza basso nello stack di rete. Include versioni per OS X e iOS; [](https://nshipster.com/network-link-conditioner/)
   * [**Charles**](https://www.charlesproxy.com/)  - un&#39;applicazione proxy di debug Web che, oltre a diversi altri usi, fornisce la limitazione della rete. Sono disponibili versioni per Windows, OS X e Linux. [](https://www.charlesproxy.com/)

#### Strumenti di ottimizzazione {#optimization-tools}

**Monitoraggio**

La documentazione [Monitoring Performance](/help/sites-deploying/monitoring-and-maintaining.md#monitoring-performance) è una buona risorsa per strumenti e metodi che possono essere utilizzati per diagnosticare le aree problematiche e individuare le aree da sottoporre a tuning.

**Modalità Sviluppatore nell’interfaccia utente touch**

Una delle nuove funzioni nell’interfaccia touch di AEM 6 è la modalità Sviluppatore. Così come gli autori possono passare dalle modalità di modifica a quella di anteprima, gli sviluppatori possono passare alla modalità di sviluppo nell’interfaccia utente dell’autore per visualizzare il tempo di rendering di ciascuno dei componenti sulla pagina e per visualizzare le tracce degli stack di eventuali errori. Per ulteriori informazioni sulla modalità di sviluppo, consultate questa [presentazione CQ Gems](https://docs.adobe.com/content/ddc/en/gems/aem-6-0-developer-mode.html).

**Utilizzo di rlog.jar per leggere i registri delle richieste**

Per un&#39;analisi più completa dei log di richiesta su un sistema AEM, `rlog.jar` può essere utilizzato per cercare e ordinare i file `request.log` generati AEM. Questo file JAR è incluso con un&#39;installazione AEM nella cartella `/crx-quickstart/opt/helpers`. Per ulteriori informazioni sullo strumento di registro e sul registro delle richieste in generale, consultare la documentazione [Monitoring and Maintenance](/help/sites-deploying/monitoring-and-maintaining.md) (Monitoraggio e manutenzione).

**Lo strumento Spiega query**

Per visualizzare gli indici utilizzati durante l&#39;esecuzione di una query, è possibile utilizzare lo [strumento Spiega query](/help/sites-administering/operations-dashboard.md#explain-query) in ACS AEM Tools. Questo può essere molto utile quando si ottimizzano query in esecuzione lenta.

**Strumenti PageSpeed**

Gli strumenti PageSpeed di Google offrono un’analisi del sito per garantire il rispetto delle best practice per le prestazioni delle pagine, nonché un plug-in che può essere installato insieme al dispatcher in un’istanza Apache per ulteriori ottimizzazioni. Per ulteriori informazioni, vedere il [Sito Web degli strumenti di velocità della pagina](https://developers.google.com/speed/pagespeed/).

## Ambiente di authoring {#author-environment}

### Esecuzione di test {#performing-tests}

Per eseguire test delle prestazioni nell’ambiente di authoring è necessario simulare l’esperienza degli autori di produzioni. Ciò significa che le installazioni dell’autore devono contenere tutti i componenti, i bundle OSGi, la personalizzazione dell’interfaccia utente, gli indici personalizzati e qualsiasi altra aggiunta disponibile per le istanze dell’autore della produzione.

Sono disponibili molti framework di automazione progettati per il test delle prestazioni e del carico. Gli script personalizzati possono essere registrati in questi strumenti e quindi riprodotti per simulare un numero elevato di autori che eseguono contemporaneamente attività simili di creazione e attivazione dei contenuti. È consigliabile utilizzare lo strumento Giorno difficile per simulare attività quali il caricamento di migliaia di risorse o l’attivazione di un numero elevato di pagine.

Per i tipi di ambienti che richiedono un carico di risorse o un’authoring intensivo delle pagine, è fondamentale utilizzare strumenti come Tough Day per garantire che l’ambiente funzioni in modo efficiente sotto il carico di picco. [](/help/sites-administering/webdav-access.md) WebDAV è uno strumento che non richiede script e può essere utilizzato anche per caricare grandi quantità di risorse.

#### Passaggi specifici di MongoDB {#mongodb-specific-steps}

Sui sistemi con back-end MongoDB, AEM fornisce diversi [JMX](/help/sites-administering/jmx-console.md) MBeans che devono essere monitorati durante l&#39;esecuzione di test di carico o prestazioni:

* Le **Statistiche cache consolidate** MBean. È possibile accedervi direttamente scegliendo:

`https://server:port/system/console/jmx/org.apache.jackrabbit.oak%3Aid%3D6%2Cname%3D%22Consolidated+Cache+statistics%22%2Ctype%3D%22ConsolidatedCacheStats%22`

Per la cache denominata **Document-Diff**, la frequenza di hit deve essere superiore a `.90`. Se la percentuale di hit è inferiore al 90%, è probabile che sarà necessario modificare la configurazione `DocumentNodeStoreService`.  supporto Adobe dei prodotti può consigliare impostazioni ottimali per il vostro ambiente.

* Le **Statistiche repository Oak** Mava. È possibile accedervi direttamente scegliendo:

`https://server:port/system/console/jmx/org.apache.jackrabbit.oak%3Aid%3D16%2Cname%3D%22Oak+Repository+Statistics%22%2Ctype%3D%22RepositoryStats%22`

La sezione **ObservationQueueMaxLength** mostrerà il numero di eventi nella coda di osservazione di Oak nelle ultime ore, minuti, secondi e settimane. Trovate il maggior numero di eventi nella sezione &quot;per ora&quot;. Questo numero deve essere confrontato con l&#39;impostazione `oak.observation.queue-length` che si trova nel componente **SlingRepositoryManager** nella console [OSGi](/help/sites-deploying/web-console.md). Se il numero più alto indicato per la coda di osservazione supera l&#39;impostazione `queue-length`, contattare  supporto del Adobe per assistenza nell&#39;aumentare l&#39;impostazione. L&#39;impostazione predefinita è 1.000, ma la maggior parte delle distribuzioni deve in genere portarla a 20.000 o 50.000.

## Ambiente di pubblicazione {#publish-environment}

### Esecuzione di test {#performing-tests-1}

La parte più importante di una distribuzione che deve essere sottoposta a test di carico è l’ambiente di pubblicazione o dispatcher che l’utente finale deve affrontare.

Gli strumenti di test automatizzati di terze parti possono essere utilizzati per verificare le prestazioni del sito Web. Questi strumenti consentono di registrare i passaggi che gli utenti passeranno attraverso il sito ed eseguire contemporaneamente molte di queste sessioni per simulare il carico tipico di un sito Web di produzione.

La maggior parte dei siti Web di produzione dispone di ottimizzazioni come il caching dei dispatcher e la creazione di una rete di distribuzione dei contenuti. Durante il test, dovete assicurarvi che queste ottimizzazioni siano disponibili anche per l&#39;ambiente di test. Oltre a monitorare i tempi di risposta per gli utenti finali, è anche necessario monitorare le metriche di sistema sui server e sui dispatcher di pubblicazione per garantire che il sistema non sia vincolato dalle risorse hardware.

In un sistema che non richiede un livello elevato di personalizzazione, il dispatcher deve memorizzare la maggior parte delle richieste nella cache. Di conseguenza, il carico sull’istanza di pubblicazione deve rimanere relativamente piatto. Se è richiesto un elevato livello di personalizzazione, si consiglia di utilizzare tecnologie come iFrame o richieste AJAX per il contenuto personalizzato, in modo da consentire il maggior numero possibile di cache del dispatcher.

Per i test di base, Apache Bench può essere utilizzato per misurare i tempi di risposta dei server web e aiutare a creare il carico per misurare cose come perdite di memoria. Per ulteriori informazioni, vedere l&#39;esempio riportato nella [Documentazione di monitoraggio](/help/sites-deploying/monitoring-and-maintaining.md#apache-bench).

## Risoluzione dei problemi relativi alle prestazioni {#troubleshooting-performance-issues}

Dopo aver eseguito i test delle prestazioni sull’istanza di creazione, eventuali problemi dovranno essere analizzati, diagnosticati e risolti. Potete utilizzare diversi strumenti e tecniche per eseguire analisi e risolvere i problemi:

* È possibile ispezionare il [Registro prestazioni richieste](/help/sites-administering/operations-dashboard.md#request-performance) nel Pannello operazioni. Questo strumento può essere utilizzato per identificare le richieste di pagina lente
* Analizzare query lente con lo [strumento Prestazioni query](/help/sites-administering/operations-dashboard.md#query-performance)

* Controllate l&#39;elenco degli errori per eventuali errori o avvisi. Per ulteriori informazioni, vedere [Registrazione](/help/sites-deploying/configure-logging.md)
* Monitorare le risorse hardware del sistema come la memoria e l&#39;utilizzo della CPU, l&#39;I/O del disco o l&#39;I/O della rete. Tali risorse sono spesso la causa di colli di bottiglia delle prestazioni
* Ottimizzate l&#39;architettura delle pagine e come vengono indirizzate per ridurre al minimo l&#39;uso dei parametri URL per consentire il maggior numero possibile di cache
* Seguire la documentazione [Performance Optimization](/help/sites-deploying/configuring-performance.md) e [Performance tuning tips](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html)

* Se sono presenti problemi durante la modifica di determinate pagine o componenti in istanze di autori, utilizzate la modalità TouchUI Developer per ispezionare la pagina in questione. Questo fornisce un&#39;analisi approfondita di ciascuna area di contenuto della pagina e del relativo tempo di caricamento
* Riducete tutti i file JS e CSS presenti sul sito. Per ulteriori informazioni su come eseguire questa operazione, consultare questo [post di blog](https://blogs.adobe.com/foxes/enable-js-and-css-minification/).
* Elimina CSS e JS incorporati dai componenti. Devono essere inclusi e ridotti con le librerie lato client per ridurre al minimo il numero di richieste necessarie per eseguire il rendering della pagina
* Utilizzate gli strumenti del browser come la scheda Rete di Chrome per esaminare le richieste del server e vedere quali richiedono il tempo più lungo.

Una volta identificate le aree problematiche, il codice dell&#39;applicazione può essere analizzato per verificare la disponibilità di ottimizzazioni delle prestazioni. Tutte le funzioni predefinite AEM le cui prestazioni non sono corrette possono essere affrontate con  supporto del Adobe.
