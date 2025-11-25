---
title: 'Best practice per monitorare l''implementazione  [!DNL Assets] '
description: Best practice per monitorare l'ambiente e le prestazioni della distribuzione  [!DNL Adobe Experience Manager]  dopo la distribuzione.
contentOwner: AG
role: Admin, Developer
feature: Asset Management
exl-id: a9e1bd6b-c768-4faa-99a3-7110693998dc
solution: Experience Manager, Experience Manager Assets
source-git-commit: 07289e891399a78568dcac957bc089cc08c7898c
workflow-type: tm+mt
source-wordcount: '1638'
ht-degree: 1%

---

# Best practice per monitorare la distribuzione di [!DNL Adobe Experience Manager Assets] {#assets-monitoring-best-practices}

Dal punto di vista di [!DNL Experience Manager Assets], il monitoraggio deve includere l&#39;osservazione e la creazione di report sui processi e le tecnologie seguenti:

* CPU di sistema
* Utilizzo della memoria di sistema
* Tempo di attesa I/O del disco di sistema
* I/O di rete del sistema
* MBean JMX per l’utilizzo dell’heap e i processi asincroni, come i flussi di lavoro
* Controlli di integrità della console OSGi

In genere, [!DNL Experience Manager Assets] può essere monitorato in due modi: tramite monitoraggio in tempo reale e tramite monitoraggio a lungo termine.

## Monitoraggio live {#live-monitoring}

È necessario eseguire il monitoraggio in tempo reale durante la fase di test delle prestazioni dello sviluppo o durante situazioni di carico elevato per comprendere le caratteristiche delle prestazioni dell’ambiente. In genere, il monitoraggio in tempo reale deve essere eseguito utilizzando una suite di strumenti. Di seguito sono riportati alcuni consigli:

* [VM visiva](https://visualvm.github.io/): la VM visiva consente di visualizzare informazioni dettagliate sulla VM Java, tra cui l&#39;utilizzo di CPU e della memoria Java. Inoltre, ti consente di campionare e valutare il codice in esecuzione su una distribuzione.
* [Top](https://man7.org/linux/man-pages/man1/top.1.html): Top è un comando Linux che apre un dashboard che visualizza le statistiche di utilizzo, inclusi CPU, memoria e utilizzo IO. Offre una panoramica di alto livello di ciò che accade in un’istanza.
* [Htop](https://hisham.hm/htop/): Htop è un visualizzatore di processi interattivo. Fornisce informazioni dettagliate sull’utilizzo di CPU e memoria, oltre a ciò che Top può fornire. Htop può essere installato sulla maggior parte dei sistemi Linux utilizzando `yum install htop` o `apt-get install htop`.

* Iotop: Iotop è un dashboard dettagliato per l&#39;utilizzo di I/O su disco. Vengono visualizzate barre e contatori che illustrano i processi che utilizzano operazioni di I/O su disco e la quantità utilizzata. Iotop può essere installato sulla maggior parte dei sistemi Linux utilizzando `yum install iotop` o `apt-get install iotop`.

* [Iftop](https://www.ex-parrot.com/pdw/iftop/): Iftop visualizza informazioni dettagliate sull&#39;utilizzo di Ethernet/rete. Inftop visualizza le statistiche per canale di comunicazione sulle entità che utilizzano Ethernet e la quantità di larghezza di banda che utilizzano. Iftop può essere installato nella maggior parte dei sistemi Linux utilizzando `yum install iftop` o `apt-get install iftop`.

* Java Flight Recorder (JFR): uno strumento commerciale di Oracle che puoi utilizzare liberamente in ambienti non di produzione. Per ulteriori dettagli, consulta [Come utilizzare Java Flight Recorder per diagnosticare i problemi di runtime di CQ](https://cq-ops.tumblr.com/post/73865704329/how-to-use-java-flight-recorder-to-diagnose-cq).
* File [!DNL Experience Manager] `error.log`: è possibile analizzare il file [!DNL Experience Manager] `error.log` per i dettagli degli errori registrati nel sistema. Utilizzare il comando `tail -F quickstart/logs/error.log` per identificare gli errori da analizzare.
* [Console flusso di lavoro](/help/sites-administering/workflows.md): sfrutta la console del flusso di lavoro per monitorare i flussi di lavoro in ritardo o bloccati.

In genere, questi strumenti vengono utilizzati insieme per ottenere un&#39;idea completa delle prestazioni della distribuzione di [!DNL Experience Manager].

>[!NOTE]
>
>Questi strumenti sono standard e non sono direttamente supportati da Adobe. Non richiedono licenze aggiuntive.

![chlimage_1-33](assets/chlimage_1-143.png)

*Figura: monitoraggio in tempo reale tramite lo strumento Visual VM.*

![chlimage_1-32](assets/chlimage_1-142.png)

## Monitoraggio a lungo termine {#long-term-monitoring}

Il monitoraggio a lungo termine di una distribuzione [!DNL Experience Manager] prevede il monitoraggio per un periodo di tempo più lungo delle stesse parti monitorate in tempo reale. Include inoltre la definizione di avvisi specifici per l’ambiente.

### Aggregazione dei registri e reporting {#log-aggregation-and-reporting}

Sono disponibili diversi strumenti per aggregare i registri, ad esempio Splunk(TM) e Elastic Search, Logstash e Kabana (ELK). Per valutare il tempo di attività della distribuzione di [!DNL Experience Manager], è importante comprendere gli eventi di registro specifici del sistema e creare avvisi basati su di essi. Una buona conoscenza delle procedure di sviluppo e operative consente di comprendere meglio come ottimizzare il processo di aggregazione dei registri per generare avvisi critici.

### Monitoraggio dell’ambiente {#environment-monitoring}

Il monitoraggio dell’ambiente include il monitoraggio di quanto segue:

* Velocità effettiva di rete
* I/O disco
* Memoria
* Utilizzo di CPU
* MBean JMX
* Siti Web esterni

Per monitorare ogni elemento sono necessari strumenti esterni, come NewRelic(TM) e AppDynamics(TM). Utilizzando questi strumenti, puoi definire avvisi specifici per il tuo sistema, ad esempio un elevato utilizzo del sistema, il backup del flusso di lavoro, gli errori del controllo di integrità o l’accesso non autenticato al tuo sito web. Adobe non consiglia strumenti particolari rispetto ad altri. Trova lo strumento adatto e utilizzalo per monitorare gli elementi discussi.

#### Monitoraggio interno delle applicazioni {#internal-application-monitoring}

Il monitoraggio interno dell&#39;applicazione include il monitoraggio dei componenti dell&#39;applicazione che compongono lo stack [!DNL Experience Manager], inclusi JVM, l&#39;archivio dei contenuti e il monitoraggio tramite codice dell&#39;applicazione personalizzato creato sulla piattaforma. In generale, viene eseguito tramite Mbeans JMX che possono essere monitorati direttamente da molte soluzioni di monitoraggio popolari, come SolarWinds (TM), HP OpenView(TM), Hyperic(TM), Zabbix(TM) e altri. Per i sistemi che non supportano una connessione diretta a JMX, puoi scrivere script di shell per estrarre i dati JMX ed esporli a questi sistemi in un formato che sono in grado di comprendere in modo nativo.

Per impostazione predefinita, l’accesso remoto ai JMX Mbeans non è abilitato. Per ulteriori informazioni sul monitoraggio tramite JMX, vedere [Monitoraggio e gestione tramite la tecnologia JMX](https://docs.oracle.com/javase/7/docs/technotes/guides/management/agent.html).

In molti casi, è necessaria una linea di base per monitorare efficacemente una statistica. Per creare una baseline, osservare il sistema in condizioni di lavoro normali per un periodo predeterminato e quindi identificare la metrica normale.

**Monitoraggio JVM**

Come per qualsiasi stack di applicazioni basato su Java, [!DNL Experience Manager] dipende dalle risorse fornite tramite la macchina virtuale Java sottostante. È possibile monitorare lo stato di molte di queste risorse tramite Platform MXBean esposti da JVM. Per ulteriori informazioni su MXBeans, vedere [Utilizzo di Platform MBean Server e Platform MXBeans](https://docs.oracle.com/javase/7/docs/technotes/guides/management/mxbeans.html).

Di seguito sono riportati alcuni parametri di base che è possibile monitorare per JVM:

Memoria

* `MBean: lava.lang:type=Memory`
* URL: `/system/console/jmx/java.lang:type=Memory`
* Istanze: tutti i server
* Soglia di allarme: quando l’utilizzo della memoria heap o non-heap supera il 75% della memoria massima corrispondente.
* Definizione allarme: memoria di sistema insufficiente o perdita di memoria nel codice. Analizza un’immagine thread per ottenere una definizione.

>[!NOTE]
>
>Le informazioni fornite da questo bean sono espresse in byte.

Threads

* MBean: `java.lang:type=Threading`
* URL: `/system/console/jmx/java.lang:type=Threading`
* Istanze: tutti i server
* Soglia di allarme: quando il numero di thread è maggiore del 150% della linea di base.
* Definizione allarme: è in corso un processo di runaway attivo oppure un&#39;operazione inefficiente consuma una grande quantità di risorse. Analizza un’immagine thread per ottenere una definizione.

**Monitora[!DNL Experience Manager]**

[!DNL Experience Manager] espone anche un set di statistiche e operazioni tramite JMX. Queste funzionalità consentono di valutare lo stato del sistema e identificare i potenziali problemi prima che abbiano un impatto sugli utenti. Per ulteriori informazioni, consulta la [documentazione](/help/sites-administering/jmx-console.md) su [!DNL Experience Manager] MBean JMX.

Di seguito sono riportati alcuni parametri di base che è possibile monitorare per [!DNL Experience Manager]:

Agenti di replica

* MBean: `com.adobe.granite.replication:type=agent,id="<AGENT_NAME>"`
* URL: `/system/console/jmx/com.adobe.granite.replication:type=agent,id="<AGENT_NAME>"`
* Istanze: un autore e tutte le istanze di pubblicazione (per gli agenti di svuotamento)
* Soglia di allarme: quando il valore di `QueueBlocked` è `true` o il valore di `QueueNumEntries` è maggiore del 150% della linea di base.

* Definizione allarme: presenza di una coda bloccata nel sistema che indica che la destinazione di replica è inattiva o non raggiungibile. Spesso, problemi di rete o di infrastruttura causano l&#39;inserimento in coda di voci eccessive, che possono influire negativamente sulle prestazioni del sistema.

>[!NOTE]
>
>Per i parametri MBean e URL, sostituire `<AGENT_NAME>` con il nome dell&#39;agente di replica che si desidera monitorare.

Contatore sessioni

* MBean: `org.apache.jackrabbit.oak:id=7,name="OakRepository Statistics",type="RepositoryStats"`
* URL: */system/console/jmx/org.apache.jackrabbit.oak:id=7,name=&quot;Statistiche OakRepository&quot;,type*=&quot;RepositoryStats&quot;
* Istanze: tutti i server
* Soglia di allarme: quando le sessioni aperte superano la linea di base di oltre il 50%.
* Definizione dell’allarme: le sessioni possono essere aperte tramite codice e non chiudono mai. Questo può avvenire lentamente nel tempo e causare perdite di memoria nel sistema. Il numero di sessioni dovrebbe variare su un sistema, ma non dovrebbe aumentare continuamente.

Verifiche stato

I controlli di integrità disponibili nel [dashboard operazioni](/help/sites-administering/operations-dashboard.md#health-reports) dispongono di MBean JMX corrispondenti per il monitoraggio. Tuttavia, è possibile scrivere controlli di integrità personalizzati per esporre statistiche di sistema aggiuntive.

Di seguito sono riportati alcuni controlli di integrità pronti all’uso che sono utili per monitorare:

* Verifiche di sistema
   * MBean: `org.apache.sling.healthcheck:name=systemchecks,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=systemchecks,type=HealthCheck`
   * Istanze: un unico autore, tutti i server di pubblicazione
   * Soglia di allarme: quando lo stato non è OK
   * Definizione allarme: lo stato di una delle metriche è WARN o CRITICAL. Per ulteriori informazioni sulla causa del problema, controlla l’attributo del registro.

* Coda di replica

   * MBean: `org.apache.sling.healthcheck:name=replicationQueue,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=replicationQueue,type=HealthCheck`
   * Istanze: un unico autore, tutti i server di pubblicazione
   * Soglia di allarme: quando lo stato non è OK
   * Definizione allarme: lo stato di una delle metriche è WARN o CRITICAL. Per ulteriori informazioni sulla coda che ha causato il problema, controlla l’attributo del registro.

* Prestazioni delle risposte

   * MBean: `org.apache.sling.healthcheck:name=requestsStatus,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=requestsStatus,type=HealthCheck`
   * Istanze: tutti i server
   * Durata allarme: quando lo stato non è OK
   * Definizione allarme: lo stato di una delle metriche è WARN o CRITICAL. Per ulteriori informazioni sulla coda che ha causato il problema, controlla l’attributo del registro.

* Prestazioni delle query

   * MBean: `org.apache.sling.healthcheck:name=queriesStatus,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name= queriesStatus,type=HealthCheck`
   * Istanze: un unico autore, tutti i server di pubblicazione
   * Soglia di allarme: quando lo stato non è OK
   * Definizione allarme: una o più query eseguite lentamente nel sistema. Per ulteriori informazioni sulle query che hanno causato il problema, controlla l’attributo del registro.

* Bundle attivi

   * MBean: `org.apache.sling.healthcheck:name=inactiveBundles,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=inactiveBundles,type=HealthCheck`
   * Istanze: tutti i server
   * Soglia di allarme: quando lo stato non è OK
   * Definizione allarme: presenza di bundle OSGi inattivi o non risolti sul sistema. Per ulteriori informazioni sui bundle che hanno causato il problema, controlla l’attributo del registro.

* Errori registro

   * MBean: `org.apache.sling.healthcheck:name=logErrorHealthCheck,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=logErrorHealthCheck,type=HealthCheck`
   * Istanze: tutti i server
   * Soglia di allarme: quando lo stato non è OK
   * Definizione allarme: nei file di registro sono presenti errori. Per ulteriori informazioni sulla causa del problema, controlla l’attributo del registro.

## Problemi comuni e risoluzioni  {#common-issues-and-resolutions}

Nel processo di monitoraggio, se si verificano problemi, ecco alcune attività di risoluzione dei problemi che è possibile eseguire per risolvere problemi comuni con [!DNL Experience Manager] distribuzioni:

* Se si utilizza TarMK, eseguire spesso la compattazione Tar. Per ulteriori dettagli, vedere [Gestione del repository](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository).
* Controlla `OutOfMemoryError` registri. Per ulteriori informazioni, vedere [Analizzare i problemi di memoria](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17482.html).

* Controlla i registri per eventuali riferimenti a query non indicizzate, attraversamenti struttura o attraversamenti indice. Ciò indica query non indicizzate o query indicizzate in modo inadeguato. Per le best practice sull&#39;ottimizzazione delle prestazioni di query e indicizzazione, vedere [Best practice per query e indicizzazione](/help/sites-deploying/best-practices-for-queries-and-indexing.md).
* Utilizza la console Flusso di lavoro per verificare che i flussi di lavoro funzionino come previsto. Se possibile, condensa più flussi di lavoro in un unico flusso di lavoro.
* Rivedi il monitoraggio live e cerca ulteriori colli di bottiglia o utenti elevati di risorse specifiche.
* Esaminare i punti di uscita dalla rete client e i punti di ingresso alla rete di distribuzione [!DNL Experience Manager], incluso Dispatcher. Spesso si tratta di aree con colli di bottiglia. Per ulteriori informazioni, vedere [Considerazioni sulla rete Assets](/help/assets/assets-network-considerations.md).
* Ridimensiona il server [!DNL Experience Manager]. È possibile che la distribuzione di [!DNL Experience Manager] non sia stata dimensionata correttamente. L’Assistenza clienti Adobe può aiutarti a identificare se il tuo server è di dimensioni inferiori a quelle reali.
* Esaminare i file `access.log` e `error.log` per individuare eventuali voci in relazione a un problema. Cerca i pattern che possono potenzialmente indicare anomalie nel codice personalizzato. Aggiungili all’elenco degli eventi monitorati.
