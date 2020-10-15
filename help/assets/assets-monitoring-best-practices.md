---
title: Best practice per [!DNL Assets] monitorare l'implementazione
description: Procedure ottimali per monitorare l'ambiente e le prestazioni dell' [!DNL Adobe Experience Manager] implementazione dopo l'implementazione.
contentOwner: AG
translation-type: tm+mt
source-git-commit: b14b377e52ab10c41355f069d97508b588d82216
workflow-type: tm+mt
source-wordcount: '1668'
ht-degree: 1%

---


# Best practice per monitorare [!DNL Adobe Experience Manager Assets] l&#39;implementazione {#assets-monitoring-best-practices}

Dal [!DNL Experience Manager Assets] punto di vista, il monitoraggio dovrebbe includere l&#39;osservazione e la segnalazione dei seguenti processi e tecnologie:

* CPU del sistema
* Utilizzo della memoria di sistema
* Tempo di attesa IO e IO del disco di sistema
* I/O di rete del sistema
* MBeans JMX per l&#39;utilizzo dell&#39;heap e processi asincroni, ad esempio flussi di lavoro
* Controlli dello stato della console OSGi

In genere, [!DNL Experience Manager Assets] è possibile monitorare i dati in due modi: dal vivo e dal lungo termine.

## Monitoraggio live {#live-monitoring}

È necessario eseguire il monitoraggio live durante la fase di test delle prestazioni del proprio sviluppo o durante situazioni di carico elevato per comprendere le caratteristiche di prestazioni dell&#39;ambiente. In genere, il monitoraggio live dovrebbe essere eseguito utilizzando una suite di strumenti. Di seguito sono riportati alcuni suggerimenti:

* [VM](https://visualvm.github.io/)visiva: La VM visiva consente di visualizzare informazioni dettagliate sulla VM Java, incluso l&#39;utilizzo della CPU, l&#39;utilizzo della memoria Java. Inoltre, consente di campionare e valutare il codice in esecuzione su una distribuzione.
* [In alto](https://man7.org/linux/man-pages/man1/top.1.html): Top è un comando Linux che apre un dashboard, che visualizza le statistiche di utilizzo, incluso l&#39;utilizzo di CPU, memoria e IO. Fornisce una panoramica di alto livello di ciò che sta accadendo in un’istanza.
* [Htop](https://hisham.hm/htop/): Htop è un visualizzatore di processo interattivo. Offre un utilizzo dettagliato della CPU e della memoria oltre a quanto può fornire Top. Htop può essere installato nella maggior parte dei sistemi Linux utilizzando `yum install htop` o `apt-get install htop`.

* Iotop: Iotop è una dashboard dettagliata per l&#39;utilizzo di I/O su disco. Vengono visualizzate barre e misuratori che rappresentano i processi che utilizzano l&#39;I/O del disco e la quantità utilizzata. Iotop può essere installato sulla maggior parte dei sistemi Linux utilizzando `yum install iotop` o `apt-get install iotop`.

* [Iftop](https://www.ex-parrot.com/pdw/iftop/): Iftop visualizza informazioni dettagliate sull&#39;utilizzo di Ethernet/rete. Iftop visualizza le statistiche sui canali di comunicazione delle entità che utilizzano Ethernet e la quantità di larghezza di banda utilizzata. Iftop può essere installato nella maggior parte dei sistemi Linux utilizzando `yum install iftop` o `apt-get install iftop`.

* Registratore di volo Java (JFR): Uno strumento commerciale di Oracle che può essere utilizzato liberamente in ambienti non di produzione. Per ulteriori dettagli, vedere [Come utilizzare il registratore di volo Java per diagnosticare problemi](https://cq-ops.tumblr.com/post/73865704329/how-to-use-java-flight-recorder-to-diagnose-cq)di runtime CQ.
* [!DNL Experience Manager] `error.log` file: È possibile esaminare il [!DNL Experience Manager] `error.log` file per informazioni dettagliate sugli errori registrati nel sistema. Utilizzate il comando `tail -F quickstart/logs/error.log` per identificare gli errori da esaminare.
* [Console](/help/sites-administering/workflows.md)Flusso di lavoro: Utilizza la console del flusso di lavoro per monitorare i flussi di lavoro che si trovano in ritardo o che restano bloccati.

In genere, questi strumenti vengono utilizzati insieme per ottenere un’idea completa delle prestazioni della [!DNL Experience Manager] distribuzione.

>[!NOTE]
>
>Questi strumenti sono strumenti standard e non sono supportati direttamente  Adobe. Non richiedono licenze aggiuntive.

![chlimage_1-33](assets/chlimage_1-143.png)

*Figura: Monitoraggio dal vivo con lo strumento Visual VM.*

![chlimage_1-32](assets/chlimage_1-142.png)

## Monitoraggio a lungo termine {#long-term-monitoring}

Il monitoraggio a lungo termine di un&#39; [!DNL Experience Manager] installazione implica il monitoraggio per un periodo più lungo delle stesse porzioni monitorate dal vivo. Include inoltre la definizione di avvisi specifici per l’ambiente.

### Aggregazione dei registri e generazione dei rapporti {#log-aggregation-and-reporting}

Sono disponibili diversi strumenti per aggregare i registri, ad esempio Splunk(TM) e Elastic Search, Logstash e Kabana (ELK). Per valutare i tempi di attività della [!DNL Experience Manager] distribuzione, è importante comprendere gli eventi di registro specifici del sistema e creare avvisi basati su di essi. Una buona conoscenza delle procedure di sviluppo e di gestione consente di comprendere meglio come ottimizzare il processo di aggregazione dei log per generare avvisi critici.

### Monitoraggio ambientale {#environment-monitoring}

Il monitoraggio ambientale include il monitoraggio dei seguenti elementi:

* Rete
* IO disco
* Memoria
* Utilizzo CPU
* JMX MBeans
* Siti Web esterni

Per monitorare ogni elemento sono necessari strumenti esterni, come NewRelic(TM) e AppDynamics(TM). Utilizzando questi strumenti, puoi definire avvisi specifici per il tuo sistema, ad esempio un elevato utilizzo del sistema, un backup del flusso di lavoro, un errore del controllo dello stato o un accesso non autenticato al tuo sito Web.  Adobe non consiglia strumenti particolari rispetto ad altri. Trovate lo strumento che funziona per voi e sfruttatelo per monitorare gli elementi discussi.

#### Monitoraggio delle applicazioni interne {#internal-application-monitoring}

Il monitoraggio interno delle applicazioni include il monitoraggio dei componenti dell&#39;applicazione che costituiscono lo [!DNL Experience Manager] stack, tra cui JVM, l&#39;archivio dei contenuti e il monitoraggio attraverso il codice dell&#39;applicazione personalizzato integrato nella piattaforma. In generale, viene eseguito tramite MBeg JMX che può essere monitorato direttamente da molte soluzioni di monitoraggio popolari, come SolarWinds (TM), HP OpenView(TM), Hyperic(TM), Zabbix(TM) e altri. Per i sistemi che non supportano una connessione diretta a JMX, è possibile scrivere script shell per estrarre i dati JMX ed esporli a tali sistemi in un formato che essi conoscono nativamente.

Per impostazione predefinita, l&#39;accesso remoto ai fagioli JMX non è attivato. Per ulteriori informazioni sul monitoraggio tramite JMX, consulta [Monitoring and Management Using JMX Technology](https://docs.oracle.com/javase/7/docs/technotes/guides/management/agent.html).

In molti casi, è necessaria una linea di base per monitorare efficacemente una statistica. Per creare una linea di base, osservare il sistema in condizioni di lavoro normali per un periodo predeterminato e quindi identificare la metrica normale.

**Monitoraggio JVM**

Come per qualsiasi stack di applicazioni basato su Java, [!DNL Experience Manager] dipende dalle risorse che gli vengono fornite tramite la macchina virtuale Java sottostante. È possibile monitorare lo stato di molte di queste risorse attraverso i meccanismi MXB della piattaforma esposti da JVM. Per ulteriori informazioni sui file MXBeans, vedere [Utilizzo dei server MBean e MXBeans](https://docs.oracle.com/javase/7/docs/technotes/guides/management/mxbeans.html)della piattaforma.

Di seguito sono riportati alcuni parametri di base che è possibile monitorare per JVM:

Memoria

* `MBean: lava.lang:type=Memory`
* URL: `/system/console/jmx/java.lang:type=Memory`
* Istanze: Tutti i server
* Soglia allarme: Quando l&#39;utilizzo della memoria heap o non heap supera il 75% della memoria massima corrispondente.
* Definizione allarme: La memoria del sistema è insufficiente o si verifica una perdita di memoria nel codice. Analizzare un dump di thread per arrivare a una definizione.

>[!NOTE]
>
>Le informazioni fornite da questo fagiolo sono espresse in byte.

Thread

* MBean: `java.lang:type=Threading`
* URL: `/system/console/jmx/java.lang:type=Threading`
* Istanze: Tutti i server
* Soglia allarme: Quando il numero di thread è maggiore del 150% della linea di base.
* Definizione allarme: È presente un processo di runtime attivo o un&#39;operazione inefficiente che consuma una grande quantità di risorse. Analizzare un dump di thread per arrivare a una definizione.

**Monitor[!DNL Experience Manager]**

[!DNL Experience Manager] espone inoltre una serie di statistiche e operazioni tramite JMX. Questi possono aiutare a valutare lo stato di salute del sistema e a identificare potenziali problemi prima che abbiano un impatto sugli utenti. Per ulteriori informazioni, consulta [la documentazione](/help/sites-administering/jmx-console.md) sugli MBeans [!DNL Experience Manager] JMX.

Di seguito sono riportati alcuni parametri di base che è possibile monitorare per [!DNL Experience Manager]:

Agenti di replica

* MBean: `com.adobe.granite.replication:type=agent,id=”<AGENT_NAME>”`
* URL: `/system/console/jmx/com.adobe.granite.replication:type=agent,id=”<AGENT_NAME>"`
* Istanze: Un autore e tutte le istanze pubblicate (per gli agenti di scaricamento)
* Soglia allarme: Quando il valore di `QueueBlocked` è `true` o il valore di `QueueNumEntries` è maggiore del 150% della linea di base.

* Definizione allarme: Presenza di una coda bloccata nel sistema per indicare che la destinazione di replica è inattiva o non raggiungibile. Spesso, problemi di rete o di infrastruttura causano la messa in coda di voci eccessive, che possono avere un impatto negativo sulle prestazioni del sistema.

>[!NOTE]
>
>Per i parametri MBean e URL, sostituite `<AGENT_NAME>` con il nome dell&#39;agente di replica da monitorare.

Contatore di sessione

* MBean: `org.apache.jackrabbit.oak:id=7,name="OakRepository Statistics",type="RepositoryStats"`
* URL: */system/console/jmx/org.apache.jackrabbit.oak:id=7,name=&quot;Statistiche OakRepository&quot;,type*=&quot;RepositoryStats&quot;
* Istanze: Tutti i server
* Soglia allarme: Quando le sessioni aperte superano la linea di base di oltre il 50%.
* Definizione allarme: Le sessioni possono essere aperte tramite un frammento di codice e non chiudersi mai. Questo può accadere lentamente nel tempo e alla fine causare perdite di memoria nel sistema. Il numero di sessioni dovrebbe variare su un sistema, ma non dovrebbe aumentare continuamente.

Verifiche stato

I controlli di integrità disponibili nel dashboard [](/help/sites-administering/operations-dashboard.md#health-reports) delle operazioni presentano MBeans JMX corrispondenti per il monitoraggio. Tuttavia, potete scrivere controlli di integrità personalizzati per esporre ulteriori statistiche di sistema.

Di seguito sono riportati alcuni controlli di stato out-of-the-box utili per monitorare:

* Verifiche di sistema
   * MBean: `org.apache.sling.healthcheck:name=systemchecks,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=systemchecks,type=HealthCheck`
   * Istanze: Un autore, tutti i server di pubblicazione
   * Soglia allarme: Quando lo stato non è OK
   * Definizione allarme: Lo stato di una delle metriche è WARN o CRITICAL. Per ulteriori informazioni sulla causa del problema, consultate l’attributo di registro.

* Coda di replica

   * MBean: `org.apache.sling.healthcheck:name=replicationQueue,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=replicationQueue,type=HealthCheck`
   * Istanze: Un autore, tutti i server di pubblicazione
   * Soglia allarme: Quando lo stato non è OK
   * Definizione allarme: Lo stato di una delle metriche è WARN o CRITICAL. Per ulteriori informazioni sulla coda che ha causato il problema, controllate l’attributo di registro.

* Prestazioni delle risposte

   * MBean: `org.apache.sling.healthcheck:name=requestsStatus,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=requestsStatus,type=HealthCheck`
   * Istanze: Tutti i server
   * Durata allarme: Quando lo stato non è OK
   * Definizione allarme: Lo stato di una delle metriche è WARN o CRITICAL. Per ulteriori informazioni sulla coda che ha causato il problema, controllate l’attributo di registro.

* Prestazioni delle query

   * MBean: `org.apache.sling.healthcheck:name=queriesStatus,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name= queriesStatus,type=HealthCheck`
   * Istanze: Un autore, tutti i server di pubblicazione
   * Soglia allarme: Quando lo stato non è OK
   * Definizione allarme: Una o più query con esecuzione lenta nel sistema. Per ulteriori informazioni sulle query che hanno causato il problema, consultate l&#39;attributo di registro.

* Bundle attivi

   * MBean: `org.apache.sling.healthcheck:name=inactiveBundles,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=inactiveBundles,type=HealthCheck`
   * Istanze: Tutti i server
   * Soglia allarme: Quando lo stato non è OK
   * Definizione allarme: Presenza nel sistema di bundle OSGi inattivi o non risolti. Per ulteriori informazioni sui bundle che hanno causato il problema, consultate l&#39;attributo di registro.

* Errori registro

   * MBean: `org.apache.sling.healthcheck:name=logErrorHealthCheck,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=logErrorHealthCheck,type=HealthCheck`
   * Istanze: Tutti i server
   * Soglia allarme: Quando lo stato non è OK
   * Definizione allarme: I file di registro presentano degli errori. Per ulteriori informazioni sulla causa del problema, consultate l’attributo di registro.

## Problemi comuni e risoluzioni  {#common-issues-and-resolutions}

Nel processo di monitoraggio, in caso di problemi, sono disponibili alcune attività di risoluzione dei problemi che è possibile eseguire per risolvere i problemi più comuni relativi [!DNL Experience Manager] alle distribuzioni:

* Se si utilizza TarMK, eseguire spesso la compattazione Tar. Per ulteriori dettagli, vedere [Gestione della directory archivio](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository).
* Controllare `OutOfMemoryError` i registri. Per ulteriori informazioni, consultate [Analizzare i problemi](https://helpx.adobe.com/experience-manager/kb/AnalyzeMemoryProblems.html)di memoria.

* Controllate i file di registro per eventuali riferimenti a query non indicizzate, traversate ad albero o traverse di indice. Ciò indica query non indicizzate o query indicizzate in modo inadeguato. Per le best practice sull&#39;ottimizzazione delle prestazioni di query e indicizzazione, vedere [Best practice per query e indicizzazione](/help/sites-deploying/best-practices-for-queries-and-indexing.md).
* Utilizzate la console del flusso di lavoro per verificare che i flussi di lavoro funzionino come previsto. Se possibile, condensa più flussi di lavoro in un unico flusso di lavoro.
* Rivedere il monitoraggio live e cercare ulteriori strozzature o elevati consumatori di risorse specifiche.
* Esaminare i punti di uscita dalla rete client e i punti di ingresso alla rete di [!DNL Experience Manager] distribuzione, incluso il dispatcher. Spesso si tratta di aree con collo di bottiglia. Per ulteriori informazioni, consulta Considerazioni sulla rete delle [risorse](/help/assets/assets-network-considerations.md).
* Ridimensionare il [!DNL Experience Manager] server. È possibile che la [!DNL Experience Manager] distribuzione non sia sufficientemente dimensionata.  Assistenza clienti di Adobe può aiutarti a identificare se il server è di dimensioni ridotte.
* Esaminare i `access.log` file e `error.log` le voci relative al momento in cui qualcosa è andato storto. Cercare pattern che possono indicare anomalie di codice potenzialmente personalizzate. Aggiungeteli all’elenco degli eventi monitorati.
