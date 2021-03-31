---
title: Best practice per monitorare la distribuzione [!DNL Assets] di
description: Best practice per monitorare l’ambiente e le prestazioni della distribuzione [!DNL Adobe Experience Manager] dopo la distribuzione.
contentOwner: AG
role: Amministratore, architetto
feature: Gestione risorse
translation-type: tm+mt
source-git-commit: 174e0703ae541641e3dc602e700bcd31624ae62c
workflow-type: tm+mt
source-wordcount: '1672'
ht-degree: 1%

---


# Best practice per monitorare la distribuzione [!DNL Adobe Experience Manager Assets] {#assets-monitoring-best-practices}

Dal punto di vista [!DNL Experience Manager Assets], il monitoraggio dovrebbe includere l&#39;osservazione e la creazione di rapporti sui seguenti processi e tecnologie:

* CPU di sistema
* Utilizzo della memoria di sistema
* Tempo di attesa del disco di sistema IO e IO
* I/O di rete del sistema
* MBeans JMX per l’utilizzo degli heap e i processi asincroni, come i flussi di lavoro
* Controlli dello stato della console OSGi

In genere, [!DNL Experience Manager Assets] può essere monitorato in due modi, il monitoraggio live e a lungo termine.

## Monitoraggio live {#live-monitoring}

È necessario eseguire il monitoraggio in tempo reale durante la fase di test delle prestazioni dello sviluppo o durante le situazioni a carico elevato per comprendere le caratteristiche delle prestazioni dell&#39;ambiente. In genere, il monitoraggio live deve essere eseguito utilizzando una suite di strumenti. Ecco alcuni consigli:

* [VM](https://visualvm.github.io/) visiva: Visual VM consente di visualizzare informazioni dettagliate su Java VM, tra cui l&#39;utilizzo della CPU, l&#39;utilizzo della memoria Java. Inoltre, ti consente di campionare e valutare il codice in esecuzione su una distribuzione.
* [Parte superiore](https://man7.org/linux/man-pages/man1/top.1.html): Top è un comando Linux che apre un dashboard, che visualizza le statistiche di utilizzo, tra cui CPU, memoria e utilizzo IO. Fornisce una panoramica di alto livello di ciò che sta accadendo in un&#39;istanza.
* [Htop](https://hisham.hm/htop/): Htop è un visualizzatore di processi interattivo. Fornisce l&#39;utilizzo dettagliato della CPU e della memoria oltre a ciò che Top può fornire. Htop può essere installato sulla maggior parte dei sistemi Linux utilizzando `yum install htop` o `apt-get install htop`.

* Iotop: Iotop è un dashboard dettagliato per l&#39;utilizzo dell&#39;IO del disco. Visualizza barre e misuratori che rappresentano i processi che utilizzano l&#39;IO del disco e la quantità che utilizzano. Iotop può essere installato sulla maggior parte dei sistemi Linux utilizzando `yum install iotop` o `apt-get install iotop`.

* [Iftop](https://www.ex-parrot.com/pdw/iftop/): Iftop visualizza informazioni dettagliate sull&#39;utilizzo di ethernet/rete. Iftop visualizza le statistiche dei canali di comunicazione sulle entità che utilizzano ethernet e la quantità di larghezza di banda utilizzata. Iftop può essere installato sulla maggior parte dei sistemi Linux utilizzando `yum install iftop` o `apt-get install iftop`.

* Registratore di volo Java (JFR): Uno strumento commerciale dall&#39;Oracle che può essere utilizzato liberamente in ambienti non di produzione. Per ulteriori dettagli, consulta [Come utilizzare il registratore di volo Java per diagnosticare i problemi runtime CQ](https://cq-ops.tumblr.com/post/73865704329/how-to-use-java-flight-recorder-to-diagnose-cq).
* [!DNL Experience Manager] `error.log` file: È possibile esaminare il  [!DNL Experience Manager] `error.log` file per i dettagli degli errori registrati nel sistema. Usa il comando `tail -F quickstart/logs/error.log` per identificare gli errori da esaminare.
* [Console](/help/sites-administering/workflows.md) del flusso di lavoro: Utilizza la console del flusso di lavoro per monitorare i flussi di lavoro in ritardo o bloccati.

In genere, questi strumenti vengono utilizzati insieme per ottenere un&#39;idea completa delle prestazioni della distribuzione [!DNL Experience Manager].

>[!NOTE]
>
>Questi strumenti sono strumenti standard e non sono supportati direttamente da Adobe. Non richiedono licenze aggiuntive.

![chlimage_1-33](assets/chlimage_1-143.png)

*Figura: Monitoraggio in tempo reale tramite lo strumento Visual VM.*

![chlimage_1-32](assets/chlimage_1-142.png)

## Monitoraggio a lungo termine {#long-term-monitoring}

Il monitoraggio a lungo termine di una distribuzione [!DNL Experience Manager] implica il monitoraggio per una durata più lunga delle stesse parti monitorate in tempo reale. Include inoltre la definizione di avvisi specifici per l’ambiente.

### Aggregazione dei registri e reporting {#log-aggregation-and-reporting}

Sono disponibili diversi strumenti per aggregare i registri, ad esempio Splunk(TM) e Elastic Search, Logstash e Kabana (ELK). Per valutare il tempo di attività della distribuzione [!DNL Experience Manager], è importante comprendere gli eventi di registro specifici del sistema e creare avvisi basati su di essi. Una buona conoscenza delle procedure di sviluppo e delle operazioni consente di comprendere meglio come ottimizzare il processo di aggregazione dei log per generare avvisi critici.

### Monitoraggio dell&#39;ambiente {#environment-monitoring}

Il monitoraggio dell&#39;ambiente include il monitoraggio dei seguenti elementi:

* Velocità effettiva di rete
* IO del disco
* Memoria
* Utilizzo della CPU
* MBeans JMX
* Siti web esterni

Per monitorare ogni elemento sono necessari strumenti esterni, ad esempio NewRelic(TM) e AppDynamics(TM). Utilizzando questi strumenti, puoi definire avvisi specifici per il tuo sistema, ad esempio un elevato utilizzo del sistema, un backup del flusso di lavoro, un errore di verifica dello stato o un accesso non autenticato al tuo sito web. L’Adobe non consiglia l’uso di strumenti particolari su altri. Trova lo strumento che funziona per te e lo sfrutta per monitorare gli elementi discussi.

#### Monitoraggio delle applicazioni interne {#internal-application-monitoring}

Il monitoraggio interno delle applicazioni include il monitoraggio dei componenti dell&#39;applicazione che compongono lo stack [!DNL Experience Manager], tra cui JVM, l&#39;archivio dei contenuti e il monitoraggio tramite codice dell&#39;applicazione personalizzato generato sulla piattaforma. In generale, viene eseguito tramite JMX Mbeans che può essere monitorato direttamente da molte soluzioni di monitoraggio popolari, come SolarWinds (TM), HP OpenView(TM), Hyperic(TM), Zabbix(TM) e altri. Per i sistemi che non supportano una connessione diretta a JMX, è possibile scrivere script di shell per estrarre i dati JMX ed esporli a questi sistemi in un formato che essi comprendono nativamente.

L&#39;accesso remoto ai Mbeans JMX non è abilitato per impostazione predefinita. Per ulteriori informazioni sul monitoraggio tramite JMX, consulta [Monitoraggio e gestione utilizzando la tecnologia JMX](https://docs.oracle.com/javase/7/docs/technotes/guides/management/agent.html).

In molti casi, è necessaria una linea di base per monitorare efficacemente una statistica. Per creare una linea di base, osservare il sistema in condizioni di lavoro normali per un periodo predeterminato e quindi identificare la metrica normale.

**Monitoraggio JVM**

Come per qualsiasi stack di applicazioni basato su Java, [!DNL Experience Manager] dipende dalle risorse che gli vengono fornite tramite la macchina virtuale Java sottostante. Puoi monitorare lo stato di molte di queste risorse tramite Platform MXBeans esposti da JVM. Per ulteriori informazioni su MXBeans, consulta [Utilizzo del server MBean e della piattaforma MXBeans](https://docs.oracle.com/javase/7/docs/technotes/guides/management/mxbeans.html).

Di seguito sono riportati alcuni parametri di base che è possibile monitorare per JVM:

Memoria

* `MBean: lava.lang:type=Memory`
* URL: `/system/console/jmx/java.lang:type=Memory`
* Istanze: Tutti i server
* Soglia allarme: Quando l&#39;utilizzo della memoria heap o non heap supera il 75% della memoria massima corrispondente.
* Definizione dell&#39;allarme: Memoria di sistema insufficiente o perdita di memoria nel codice. Analizza un dump di thread per arrivare a una definizione.

>[!NOTE]
>
>Le informazioni fornite da questo fagiolo sono espresse in byte.

Thread

* MBean: `java.lang:type=Threading`
* URL: `/system/console/jmx/java.lang:type=Threading`
* Istanze: Tutti i server
* Soglia allarme: Quando il numero di thread è maggiore del 150% della linea di base.
* Definizione dell&#39;allarme: Esiste un processo di runtime attivo o un&#39;operazione inefficiente consuma una grande quantità di risorse. Analizza un dump di thread per arrivare a una definizione.

**Monitor[!DNL Experience Manager]**

[!DNL Experience Manager] espone inoltre una serie di statistiche e operazioni attraverso JMX. Questi possono aiutare a valutare lo stato di salute del sistema e individuare potenziali problemi prima che influiscano sugli utenti. Per ulteriori informazioni, consulta [documentazione](/help/sites-administering/jmx-console.md) su [!DNL Experience Manager] MBeans JMX.

Di seguito sono riportati alcuni parametri di base che è possibile monitorare per [!DNL Experience Manager]:

Agenti di replica

* MBean: `com.adobe.granite.replication:type=agent,id=”<AGENT_NAME>”`
* URL: `/system/console/jmx/com.adobe.granite.replication:type=agent,id=”<AGENT_NAME>"`
* Istanze: Un autore e tutte le istanze di pubblicazione (per agenti flush)
* Soglia allarme: Quando il valore di `QueueBlocked` è `true` o il valore di `QueueNumEntries` è maggiore del 150% della linea di base.

* Definizione dell&#39;allarme: Presenza di una coda bloccata nel sistema che indica che la destinazione di replica è inattiva o non raggiungibile. Spesso, problemi di rete o di infrastruttura causano la messa in coda di voci eccessive, che possono influire negativamente sulle prestazioni del sistema.

>[!NOTE]
>
>Per i parametri MBean e URL, sostituisci `<AGENT_NAME>` con il nome dell&#39;agente di replica che desideri monitorare.

Contatore sessione

* MBean: `org.apache.jackrabbit.oak:id=7,name="OakRepository Statistics",type="RepositoryStats"`
* URL: */system/console/jmx/org.apache.jackrabbit.oak:id=7,name=&quot;Statistiche OakRepository&quot;,type*=&quot;RepositoryStats&quot;
* Istanze: Tutti i server
* Soglia allarme: Quando le sessioni aperte superano la linea di base di oltre il 50%.
* Definizione dell&#39;allarme: Le sessioni possono essere aperte tramite un codice e non possono mai chiudersi. Questo può accadere lentamente nel tempo e alla fine causare perdite di memoria nel sistema. Il numero di sessioni dovrebbe variare su un sistema, ma non dovrebbe aumentare continuamente.

Verifiche stato

I controlli di integrità disponibili nel [dashboard delle operazioni](/help/sites-administering/operations-dashboard.md#health-reports) dispongono dei MBeans JMX corrispondenti per il monitoraggio. Tuttavia, è possibile scrivere controlli di integrità personalizzati per esporre statistiche di sistema aggiuntive.

Di seguito sono riportati alcuni controlli di integrità predefiniti utili per il monitoraggio:

* Verifiche di sistema
   * MBean: `org.apache.sling.healthcheck:name=systemchecks,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=systemchecks,type=HealthCheck`
   * Istanze: Un autore, tutti i server di pubblicazione
   * Soglia allarme: Quando lo stato non è OK
   * Definizione dell&#39;allarme: Lo stato di una delle metriche è WARN o CRITICAL. Per ulteriori informazioni sulla causa del problema, consulta l’attributo di registro .

* Coda di replica

   * MBean: `org.apache.sling.healthcheck:name=replicationQueue,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=replicationQueue,type=HealthCheck`
   * Istanze: Un autore, tutti i server di pubblicazione
   * Soglia allarme: Quando lo stato non è OK
   * Definizione dell&#39;allarme: Lo stato di una delle metriche è WARN o CRITICAL. Controlla l&#39;attributo del registro per ulteriori informazioni sulla coda che ha causato il problema.

* Prestazioni delle risposte

   * MBean: `org.apache.sling.healthcheck:name=requestsStatus,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=requestsStatus,type=HealthCheck`
   * Istanze: Tutti i server
   * Durata dell&#39;allarme: Quando lo stato non è OK
   * Definizione dell&#39;allarme: Lo stato di una delle metriche è WARN o CRITICAL. Controlla l&#39;attributo del registro per ulteriori informazioni sulla coda che ha causato il problema.

* Prestazioni delle query

   * MBean: `org.apache.sling.healthcheck:name=queriesStatus,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name= queriesStatus,type=HealthCheck`
   * Istanze: Un autore, tutti i server di pubblicazione
   * Soglia allarme: Quando lo stato non è OK
   * Definizione dell&#39;allarme: Una o più query in esecuzione lenta nel sistema. Per ulteriori informazioni sulle query che hanno causato il problema, consulta l’attributo di registro .

* Bundle attivi

   * MBean: `org.apache.sling.healthcheck:name=inactiveBundles,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=inactiveBundles,type=HealthCheck`
   * Istanze: Tutti i server
   * Soglia allarme: Quando lo stato non è OK
   * Definizione dell&#39;allarme: Presenza di bundle OSGi inattivi o non risolti sul sistema. Controlla l&#39;attributo del registro per ulteriori informazioni sui bundle che hanno causato il problema.

* Errori registro

   * MBean: `org.apache.sling.healthcheck:name=logErrorHealthCheck,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=logErrorHealthCheck,type=HealthCheck`
   * Istanze: Tutti i server
   * Soglia allarme: Quando lo stato non è OK
   * Definizione dell&#39;allarme: Ci sono errori nei file di log. Per ulteriori informazioni sulla causa del problema, consulta l’attributo di registro .

## Problemi comuni e risoluzioni {#common-issues-and-resolutions}

Nel processo di monitoraggio, in caso di problemi, ecco alcune attività di risoluzione dei problemi che è possibile eseguire per risolvere i problemi comuni relativi alle distribuzioni [!DNL Experience Manager]:

* Se utilizzi TarMK, esegui spesso la compattazione Tar. Per ulteriori dettagli, consulta [Mantenere l&#39;archivio](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository).
* Controlla i registri `OutOfMemoryError`. Per ulteriori informazioni, vedere [Analizzare i problemi di memoria](https://helpx.adobe.com/experience-manager/kb/AnalyzeMemoryProblems.html).

* Controlla i registri per eventuali riferimenti a query non indicizzate, traversate ad albero o traversate di indici. Ciò indica query non indicizzate o query indicizzate in modo inadeguato. Per le best practice sull&#39;ottimizzazione delle prestazioni di query e indicizzazione, consulta [Best practice per query e indicizzazione](/help/sites-deploying/best-practices-for-queries-and-indexing.md).
* Utilizza la console del flusso di lavoro per verificare che i flussi di lavoro funzionino come previsto. Se possibile, riduci più flussi di lavoro in un unico flusso di lavoro.
* Rivedere il monitoraggio live e cercare ulteriori strozzature o un elevato numero di consumatori di risorse specifiche.
* Indagare i punti di uscita dalla rete client e i punti di ingresso alla rete di distribuzione [!DNL Experience Manager], incluso il dispatcher. Spesso si tratta di aree a collo di bottiglia. Per ulteriori informazioni, consulta [Considerazioni sulla rete Assets](/help/assets/assets-network-considerations.md).
* Ridimensiona il server [!DNL Experience Manager]. È possibile che le dimensioni della distribuzione [!DNL Experience Manager] siano insufficienti. L’Assistenza clienti Adobe può aiutarti a identificare se il server è di dimensioni inferiori.
* Esamina i file `access.log` e `error.log` per verificare la presenza di voci nel momento in cui si è verificato un errore. Cerca pattern che possano indicare anomalie nel codice personalizzato. Aggiungili all’elenco degli eventi monitorati.
