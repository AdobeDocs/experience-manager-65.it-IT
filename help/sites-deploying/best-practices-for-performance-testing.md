---
title: Best practice per i test delle prestazioni
description: Scopri le strategie e le metodologie generali utilizzate per i test delle prestazioni e alcuni degli strumenti disponibili per facilitare il processo.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: fcac75e1-15c1-4a37-8d43-93c95267b903
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '1790'
ht-degree: 0%

---

# Best practice per i test delle prestazioni{#best-practices-for-performance-testing}

## Introduzione {#introduction}

I test delle prestazioni sono una parte importante di qualsiasi implementazione dell’AEM. A seconda dei requisiti dei clienti, è possibile eseguire test delle prestazioni sulle istanze di pubblicazione, di authoring o entrambe.

Questa documentazione illustra strategie generali e metodologie per l’esecuzione di test delle prestazioni e alcuni degli strumenti resi disponibili da Adobe per facilitare la procedura. Infine, leggi un’analisi degli strumenti disponibili in AEM 6 per facilitare l’ottimizzazione delle prestazioni, sia dal punto di vista dell’analisi del codice che della configurazione del sistema.

### Simulazione della realtà {#simulating-reality}

Quando esegui i test delle prestazioni, accertati di simulare il più possibile un ambiente di produzione. Anche se questo compito può essere spesso difficile, è fondamentale garantire l&#39;accuratezza di questi test. Quando si lavora alla progettazione di test delle prestazioni, è importante prendere in considerazione i seguenti punti:

* Contenuti simili alla produzione

Molte misurazioni delle prestazioni nell’AEM, come il tempo di risposta alle query, possono essere influenzate dalle dimensioni del contenuto sul sistema. È importante assicurarsi che l’ambiente di test disponga di una copia dei dati di produzione il più simile possibile.

* Codice di produzione

La versione dell’AEM e gli hotfix implementati in produzione devono essere gli stessi nell’ambiente di test. È inoltre importante eseguire il test sulla versione del codice distribuita in produzione.

* Configurazione di rete e hardware simile alla produzione

I test sono privi di significato senza un ambiente che assomigli il più possibile a quello di produzione. Idealmente, le specifiche hardware, le interfacce di rete, i load balancer e la rete CDN dovrebbero essere identici alla produzione nell’ambiente di test.

* Carico di produzione

Molti problemi relativi alle prestazioni non vengono rilevati finché il sistema non è sottoposto a un carico elevato. Le prove di buona performance dovrebbero simulare il carico al culmine dei sistemi di produzione.

### Impostazione degli obiettivi {#setting-goals}

Prima di iniziare il test delle prestazioni, è necessario impostare requisiti non funzionali per specificare i tempi di carico e di risposta. Se esegui la migrazione da un sistema esistente, assicurati che i tempi di risposta siano simili ai valori di produzione correnti. Per il carico, è meglio prendere il carico di picco corrente e raddoppiarlo. In questo modo il sito web può continuare a funzionare bene e a crescere.

### Strumenti {#tools}

Sul mercato sono disponibili molti strumenti di test delle prestazioni. Quando si esegue uno strumento di generazione del carico, è importante assicurarsi che i computer che eseguono i test dispongano di una larghezza di banda di rete sufficiente. In caso contrario, una volta che il computer di prova raggiunge i limiti della sua connessione, non viene generato alcun carico aggiuntivo sull’ambiente in prova.

#### Strumenti di test {#testing-tools}

* Lo strumento **Giorno difficile** di Adobe può essere utilizzato per generare il carico sulle istanze AEM e raccogliere i dati sulle prestazioni. Il team di progettazione AEM di Adobe utilizza lo strumento per eseguire il test di carico del prodotto AEM stesso. Gli script eseguiti in Giornata difficile vengono configurati tramite file di proprietà e file XML JMX. Per ulteriori informazioni, consulta la [documentazione del giorno difficile](/help/sites-developing/tough-day.md).

* AEM fornisce strumenti predefiniti per visualizzare rapidamente query, richieste e messaggi di errore problematici. Per ulteriori informazioni, vedere la sezione [Strumenti di diagnostica](/help/sites-administering/operations-dashboard.md#diagnosis-tools) della documentazione del dashboard operazioni.
* Apache fornisce un prodotto denominato **JMeter** che può essere utilizzato per il test delle prestazioni e del carico e per il comportamento funzionale. È un software open-source e libero da usare, ma ha un set di funzioni più piccolo rispetto ai prodotti aziendali e una curva di apprendimento più ripida. JMeter è disponibile sul sito web di Apache all&#39;indirizzo [https://jmeter.apache.org/](https://jmeter.apache.org/)

* **Load Runner** è un prodotto di test del carico di livello Enterprise. È disponibile una versione di valutazione gratuita. Ulteriori informazioni sono disponibili all&#39;indirizzo [https://www.microfocus.com/en-us/portfolio/performance-engineering/overview](https://www.microfocus.com/en-us/portfolio/performance-engineering/overview)

* È inoltre possibile utilizzare strumenti di test del caricamento del sito Web come [Vercara](https://vercara.com/website-performance-management).
* Quando si esegue il test di siti web mobili o reattivi, è necessario utilizzare un set di strumenti separato. Funzionano limitando la larghezza di banda della rete, simulando connessioni mobili più lente come 3G o EDGE. Tra gli strumenti più utilizzati vi sono:

   * **[Condizionatore collegamento di rete](https://nshipster.com/network-link-conditioner/)** - fornisce un&#39;interfaccia utente di facile utilizzo e funziona a un livello abbastanza basso nello stack di rete. Include versioni per OS X e iOS;
   * [**Charles**](https://www.charlesproxy.com/) - un&#39;applicazione proxy di debug Web che, oltre a diversi altri utilizzi, fornisce la limitazione della rete. Sono disponibili versioni per Windows, OS X e Linux®.

#### Strumenti di ottimizzazione {#optimization-tools}

**Monitoraggio**

La documentazione di [Monitoraggio delle prestazioni](/help/sites-deploying/monitoring-and-maintaining.md#monitoring-performance) è una buona risorsa per strumenti e metodi che possono essere utilizzati per diagnosticare problemi e individuare aree per l&#39;ottimizzazione.

**Modalità sviluppatore nell&#39;interfaccia utente touch**

Una delle nuove funzioni nell’interfaccia utente touch di AEM 6 è la Modalità sviluppatore. Così come gli autori possono passare dalla modalità di modifica a quella di anteprima, gli sviluppatori possono passare alla modalità sviluppatore nell’interfaccia utente di authoring. In questo modo puoi visualizzare il tempo di rendering per ciascuno dei componenti della pagina e le tracce dello stack di eventuali errori. Per ulteriori informazioni sulla modalità sviluppatore, consulta questa [presentazione CQ Gems](https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2014/aem-developer-mode.html).

**Utilizzo di rlog.jar per leggere i registri di richiesta**

Per un&#39;analisi più completa dei log delle richieste su un sistema AEM, è possibile utilizzare `rlog.jar` per eseguire ricerche e ordinare i file `request.log` generati dall&#39;AEM. Questo file jar è incluso in un&#39;installazione AEM nella cartella `/crx-quickstart/opt/helpers`. Per ulteriori informazioni sullo strumento rlog e sul log delle richieste generale, vedere la documentazione [Monitoraggio e manutenzione](/help/sites-deploying/monitoring-and-maintaining.md).

**Strumento Explain Query**

Lo strumento [Explain Query](/help/sites-administering/operations-dashboard.md#explain-query) in ACS AEM Tools può essere utilizzato per visualizzare gli indici utilizzati durante l&#39;esecuzione di una query. Questo strumento è utile quando si ottimizzano le query con esecuzione lenta.

**Strumenti PageSpeed**

Gli strumenti PageSpeed di Google offrono l’analisi del sito per il rispetto delle best practice per le prestazioni della pagina e un plug-in che può essere installato accanto a Dispatcher in un’istanza Apache per ulteriori ottimizzazioni.
Consulta il [sito Web degli strumenti PageSpeed](https://developers.google.com/speed).

## Ambiente di authoring {#author-environment}

### Esecuzione dei test {#performing-tests}

Per eseguire test delle prestazioni nell’ambiente di authoring, è necessario simulare l’esperienza degli autori di produzione. In altre parole, le installazioni dell’autore devono contenere tutti i componenti, i bundle OSGi, la personalizzazione dell’interfaccia utente, gli indici personalizzati e tutte le altre aggiunte disponibili per le istanze dell’autore di produzione.

Sono disponibili molti framework di automazione progettati per il test delle prestazioni e del carico. In questi strumenti è possibile registrare script personalizzati e riprodurli per simulare un picco di autori che eseguono contemporaneamente attività simili di creazione e attivazione di contenuti. Si consiglia di utilizzare lo strumento Giornata difficile per simulare attività quali il caricamento di migliaia di risorse o l’attivazione di un numero elevato di pagine.

Per i tipi di ambienti che richiedono il caricamento di risorse pesanti o l’authoring delle pagine, è fondamentale utilizzare strumenti come Digiuno duro. In questo modo l’ambiente funziona in modo efficiente durante i picchi di carico. [WebDAV](/help/sites-administering/webdav-access.md) è uno strumento che non richiede script e può essere utilizzato anche per caricare grandi quantità di risorse.

#### Passaggi specifici di MongoDB {#mongodb-specific-steps}

Sui sistemi con backend MongoDB, AEM fornisce diversi [JMX](/help/sites-administering/jmx-console.md) MBean che devono essere monitorati durante l&#39;esecuzione dei test di carico o delle prestazioni:

* **Statistiche cache consolidata** MBean. È accessibile direttamente da:

`https://server:port/system/console/jmx/org.apache.jackrabbit.oak%3Aid%3D6%2Cname%3D%22Consolidated+Cache+statistics%22%2Ctype%3D%22ConsolidatedCacheStats%22`

Per la cache denominata **Document-Diff**, la frequenza di hit deve essere superiore a `.90`. Se la percentuale di hit scende al di sotto del 90%, è probabile che sia necessario modificare la configurazione di `DocumentNodeStoreService`. Il supporto di prodotto di Adobe può consigliare impostazioni ottimali per il tuo ambiente.

* Mbean **Statistiche Archivio Oak**. È accessibile direttamente da:

`https://server:port/system/console/jmx/org.apache.jackrabbit.oak%3Aid%3D16%2Cname%3D%22Oak+Repository+Statistics%22%2Ctype%3D%22RepositoryStats%22`

La sezione **ObservationQueueMaxLength** mostra il numero di eventi nella coda di osservazione di Oak nelle ultime ore, minuti, secondi e settimane. Nella sezione &quot;all’ora&quot; puoi trovare il numero più alto di eventi. Confrontare questo numero con l&#39;impostazione `oak.observation.queue-length`. Se il numero più alto visualizzato per la coda di osservazione supera l&#39;impostazione `queue-length`:

1. Crea un file denominato: `com.adobe.granite.repository.impl.SlingRepositoryManager.cfg` contenente il parametro `oak.observation.queue‐length=50000`
1. Inseriscilo nella cartella /crx--quickstart/install.

>[!NOTE]
>Vedere [AEM 6.x | Suggerimenti per l&#39;ottimizzazione delle prestazioni](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/configuring-performance.html?lang=it)

L’impostazione predefinita è 10.000, ma la maggior parte delle distribuzioni deve portarla a 20.000 o 50.000.

## Ambiente di pubblicazione {#publish-environment}

### Esecuzione dei test {#performing-tests-1}

La parte più importante di una distribuzione che deve essere sottoposta a test di carico è l’ambiente di pubblicazione o Dispatcher rivolto all’utente finale.

È possibile utilizzare strumenti di test automatizzati di terze parti per testare le prestazioni del sito web. Questi strumenti ti consentono di registrare i passaggi che gli utenti visitano sul sito ed eseguono molte di queste sessioni contemporaneamente per simulare il caricamento tipico di un sito web di produzione.

La maggior parte dei siti web di produzione dispone di ottimizzazioni come il caching di Dispatcher e una rete per la distribuzione dei contenuti. Durante il test, assicurati che queste ottimizzazioni siano disponibili anche per l’ambiente di test. Oltre a monitorare i tempi di risposta per gli utenti finali, monitora le metriche di sistema sui server di pubblicazione e sui dispatcher per garantire che il sistema non sia vincolato dalle risorse hardware.

Su un sistema che non richiede un livello elevato di personalizzazione, Dispatcher deve memorizzare in cache la maggior parte delle richieste. Di conseguenza, il carico sull’istanza Publish dovrebbe rimanere relativamente piatto. Se è necessario un alto livello di personalizzazione, si consiglia di utilizzare tecnologie come iFrame o le richieste AJAX per i contenuti personalizzati, per consentire il maggior numero possibile di memorizzazione in cache di Dispatcher.

Per i test di base, Apache Bench può essere utilizzato per misurare i tempi di risposta del server web e aiutare a creare un carico per misurare elementi come le perdite di memoria. Vedi l&#39;esempio nella [documentazione sul monitoraggio](/help/sites-deploying/monitoring-and-maintaining.md#apache-bench).

## Risoluzione dei problemi di prestazioni {#troubleshooting-performance-issues}

Dopo aver eseguito i test delle prestazioni sull’istanza di authoring, è necessario indagare, diagnosticare e risolvere eventuali problemi. Puoi utilizzare diversi strumenti e tecniche per eseguire analisi e risolvere problemi:

* È possibile esaminare il [registro prestazioni richieste](/help/sites-administering/operations-dashboard.md#request-performance) nel dashboard operazioni. Questo strumento può essere utilizzato per identificare le richieste di pagine lente
* Analizza le query con esecuzione lenta con lo strumento [Prestazioni query](/help/sites-administering/operations-dashboard.md#query-performance)

* Controllare il registro degli errori per individuare eventuali errori o avvisi. Per ulteriori informazioni, vedere [Registrazione](/help/sites-deploying/configure-logging.md).
* Monitorare le risorse hardware di sistema come l&#39;utilizzo della memoria e della CPU, l&#39;I/O del disco o l&#39;I/O di rete. Queste risorse sono spesso la causa dei colli di bottiglia delle prestazioni.
* Ottimizza l’architettura delle pagine e il modo in cui vengono indirizzate per ridurre al minimo l’utilizzo dei parametri URL per consentire il maggior numero possibile di operazioni di caching.
* Segui la documentazione di [Ottimizzazione delle prestazioni](/help/sites-deploying/configuring-performance.md) e [Suggerimenti per l&#39;ottimizzazione delle prestazioni](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/configuring-performance.html?lang=it).

* In caso di problemi durante la modifica di determinate pagine o componenti nelle istanze di authoring, utilizza la modalità sviluppatore dell’interfaccia utente touch per esaminare la pagina in questione. Questa operazione fornisce un raggruppamento di ogni area di contenuto sulla pagina e il relativo tempo di caricamento.
* Minimizza tutti i file JS e CSS sul sito. Vedi questo [post di blog](https://blogs.adobe.com/foxes/enable-js-and-css-minification/).
* Elimina CSS e JS incorporati dai componenti. Devono essere incluse e ridotte con le librerie lato client per ridurre al minimo il numero di richieste necessarie per il rendering della pagina.
* Per esaminare le richieste del server e vedere quali richiedono più tempo, utilizza strumenti del browser come la scheda Rete di Chrome.

Una volta identificate le aree problematiche, è possibile controllare il codice dell&#39;applicazione per ottimizzare le prestazioni. Qualsiasi funzione AEM preconfigurata che non funziona correttamente può essere gestita con il supporto Adobe.
