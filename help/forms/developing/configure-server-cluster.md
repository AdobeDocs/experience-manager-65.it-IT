---
title: Come configurare e risolvere i problemi di un cluster di server AEM Forms su JEE?
description: Scopri come configurare e risolvere i problemi di un cluster di server AEM Forms su JEE
source-git-commit: 8502e0227819372db4120d3995fba51c7401d944
workflow-type: tm+mt
source-wordcount: '4033'
ht-degree: 0%

---

# Configurazione e risoluzione dei problemi di un AEM Forms su un cluster di server JEE {#configuring-troubleshooting-aem-forms-jee-server-cluster}

## Conoscenze preliminari {#prerequisites}

Familiarità con AEM Forms su server applicativi JEE, JBoss, WebSphere e Webogic, Red Hat Linux, SUSE Linux, Microsoft Windows, IBM AIX o Sun Solaris, ad Oracle, server di database IBM DB2 o SQL Server e ambienti web.

## Livello utente {#user-level}

Avanzate 

Un cluster AEM Forms su JEE è una topologia progettata per consentire ad AEM Forms su JEE di essere resiliente al guasto di un nodo cluster e di scalare la capacità del sistema oltre le capacità di un singolo nodo. Un cluster combina più nodi in un unico sistema logico che condivide i dati e consente alle transazioni di estendersi su più nodi nella loro esecuzione. Un cluster è il modo più generale per scalare AEM Forms su JEE, in quanto è possibile supportare qualsiasi combinazione di servizi che gestiscono qualsiasi combinazione di carichi di lavoro. Un cluster AEM Forms su JEE non è necessariamente la soluzione migliore per tutti i tipi di distribuzioni e, in particolare, in molti casi potrebbe essere appropriata un&#39;architettura non cluster con bilanciamento del carico del server.

Lo scopo di questo documento è quello di discutere i requisiti di configurazione specifici e le potenziali aree problematiche che potresti incontrare con un cluster AEM Forms su JEE.

## Cosa c&#39;è in un cluster? {#what-is-in-cluster}

I nodi del cluster AEM Forms su JEE comunicano tra loro e condividono informazioni per consentire al cluster nel suo insieme di disporre di un&#39;unica configurazione e di un unico stato dell&#39;applicazione coerenti. La condivisione delle informazioni all&#39;interno del cluster viene eseguita in diversi modi diversi simultaneamente, utilizzati in contesti diversi. I metodi di condivisione delle informazioni di base sono illustrati nella figura seguente:

![Cluster del server applicazioni](assets/application-server-cluster.jpg)

### Cluster del server applicazioni {#application-server-cluster}

Un cluster AEM Forms su JEE si basa sulle funzionalità di clustering del server applicazioni sottostante. I cluster di server applicazioni consentono di gestire la configurazione del cluster nel suo complesso e forniscono servizi cluster di basso livello come Java Naming e Directory Interface (JNDI) che consentono ai componenti software di individuarsi l&#39;un l&#39;altro all&#39;interno del cluster. La sofisticazione dei servizi cluster e le dipendenze tecniche sottostanti del server applicazioni dipendono dal server applicazioni. WebSphere e WebLogic dispongono di sofisticate funzionalità di gestione per i cluster, mentre JBoss ha un approccio molto semplice.

### Cache GemFire {#gemfire-cache}

La cache GemFire è un meccanismo di cache distribuita implementato in ogni nodo del cluster. I nodi si trovano a vicenda e creano una singola cache logica che viene mantenuta coerente tra i nodi. I nodi che si ritrovano si uniscono per mantenere una singola cache nozionale mostrata come una nuvola nella Figura 1. A differenza di GDS e database, la cache è un’entità puramente teorica. Il contenuto effettivamente memorizzato nella cache viene memorizzato in memoria e nella directory `LC_TEMP` su ciascuno dei nodi del cluster.

### Database {#database}

Il database AEM Forms su JEE, accessibile tramite le origini dati JDBC IDP_DS, EDC_DS e altri, è condiviso da tutti i nodi del cluster. La maggior parte dei dati persistenti relativi allo stato di AEM Forms su JEE, ad esempio le transazioni in corso, i dati utente associati alle transazioni correnti, i dati relativi alle modalità di impostazione delle impostazioni di sistema e così via, si trovano in questo database.

### Archiviazione globale dei documenti {#global-document-storage}

L&#39;archiviazione globale dei documenti (GDS) è un&#39;area di archiviazione basata su file system utilizzata da Document Manager (classe IDPDocument) in AEM Forms su JEE. Il GDS memorizza file di breve durata e di lunga durata che devono essere accessibili a tutti i nodi del cluster.

### Altre voci {#other-items}

Oltre a queste risorse condivise principali, ci sono altri elementi che hanno un comportamento specifico del cluster, come il quarzo. Il quarzo è un sottosistema di pianificazione utilizzato da AEM Forms su JEE e utilizza tabelle di database per conoscere cosa è stato pianificato e quali attività pianificate sono in esecuzione. Il quarzo deve essere configurato in modo diverso per installazioni e cluster a nodo singolo e prende spunto da altre impostazioni AEM Forms su JEE.

## Problemi comuni di configurazione {#common-configuration}

Una delle cose più frustranti riguardo alla manutenzione o alla risoluzione dei problemi di un cluster AEM Forms su JEE è che non c&#39;è un singolo posto per cercare di confermare positivamente che il cluster è sano. Per confermare che tutto è a posto nel cluster, è necessario eseguire delle indagini e delle analisi, e ci sono diverse modalità di errore per il funzionamento del cluster, a seconda di ciò che è sbagliato nella configurazione del cluster. La figura seguente illustra un cluster configurato in modo errato in cui diverse risorse condivise vengono condivise in modo errato.

![Cluster configurato male](assets/bad-configuration-cluster.png)

Una cosa interessante e importante da tenere a mente è che è necessario avere familiarità con il modo in cui funziona il clustering e il tipo di cose da cercare e verificare in un cluster, anche se non si intende eseguire AEM Forms su JEE in un cluster. Questo perché alcune parti di AEM Forms su JEE potrebbero prendere i loro suggerimenti su come operare in un cluster in modo errato e assumere un comportamento cluster che non ti aspetti.

Cosa c&#39;è di sbagliato nella configurazione di condivisione di Figura sopra? Le sezioni seguenti descrivono i problemi:

### (1) Configurazione del cluster GemFire {#gemfire-cluster-configuration}

Diverse cose possono andare storte con la cache Gemfire. Due scenari tipici sono:

* I nodi che dovrebbero essere in grado di trovarsi l&#39;un l&#39;altro non sono in grado di farlo.

* I nodi che non devono essere raggruppati si trovano a vicenda e condividono una cache quando non dovrebbero.

Se si dispone di nodi che si intende raggruppare, è essenziale che si trovino a vicenda sulla rete. Per impostazione predefinita, lo fanno tramite messaggi UDP multicast. Ogni nodo invia messaggi di trasmissione pubblicitari in cui è presente e ogni nodo che riceve un messaggio di questo tipo inizia a parlare con gli altri nodi che trova. Questo tipo di metodo di autoscoperta è molto comune, e molti tipi di software ed elettrodomestici lo fanno.

Un problema comune con l&#39;individuazione automatica è rappresentato dal fatto che i messaggi multicast possono essere filtrati dalla rete nell&#39;ambito dei criteri di rete o a causa di regole del firewall software, o semplicemente non possono essere indirizzati attraverso la rete esistente tra i nodi. A causa della difficoltà generale di ottenere il rilevamento automatico UDP per funzionare in reti complesse, è prassi comune per le distribuzioni di produzione utilizzare un metodo di individuazione alternativo: Localizzatori TCP. Una discussione generale dei localizzatori TCP si trova nei riferimenti.

**Come posso sapere se uso locators o UDP?**

Le seguenti proprietà JVM controllano il metodo utilizzato dalla cache GemFire per trovare altri nodi.

Impostazioni multicast:

* `adobe.cache.multicast-port`: La porta multicast utilizzata per comunicare con altri membri del sistema distribuito. Se questo valore è impostato su zero, il multicast viene disabilitato sia per l&#39;individuazione dei membri che per la distribuzione.

* `gemfire.mcast-address` (facoltativo): Sostituisce l’indirizzo IP predefinito utilizzato da Gemfire.

Impostazioni del localizzatore TCP:

* `adobe.cache.cluster-locators`: Indirizzo IP/nome host del localizzatore TCP e della porta localizzatore TCP per tutti i localizzatori utilizzati dai membri del sistema per comunicare con localizzatori in esecuzione.

L&#39;elenco deve includere tutti i localizzatori attualmente in uso e deve essere configurato in modo coerente per ogni membro del sistema cluster.

Se l&#39;elenco del localizzatore TCP è vuoto, i localizzatori non vengono utilizzati e viene utilizzato il metodo multicast.

**Come posso verificare se il localizzatore TCP è in esecuzione?**

In primo luogo, se i localizzatori TCP sono in uso, è necessario che i localizzatori TCP siano elencati nella seguente proprietà JVM su tutti i nodi cluster:

`-Dadobe.cache.cluster-locators=aix01.adobe.com[22345],aix02.adobe.com[22345]`

Non è necessario eseguire i localizzatori sui nodi del cluster AEM Forms su JEE, se necessario possono essere eseguiti su altri sistemi separati dal cluster. Più di un sistema può eseguire localizzatori, e in genere è considerata buona pratica avere localizzatori in esecuzione in due posizioni rispetto alla possibilità che un singolo errore dei localizzatori potrebbe causare un problema con il riavvio del cluster. Su ciascuno dei sistemi che eseguono localizzatori, è necessario essere in grado di verificare che siano in esecuzione utilizzando i seguenti comandi su tali computer:

`netstat -an | grep 22345`

La risposta attesa dovrebbe essere la seguente:

`tcp 0 0 *.22345 *.* LISTEN`

Un altro comando di verifica è questo:

`ps -ef | grep gemfire`

La risposta attesa dovrebbe essere simile alla seguente:

`livecycl 331984 1 0 10:14:51 pts/0 0:03 java -cp ./gemfire.jar: -Dgemfire.license-type=production -Dlocators=localhost[22345] com.gemstone.gemfire.distributed.Locator 22345`

**Come faccio a vedere quali nodi GemFire pensa siano nel cluster?**

GemFire produce informazioni di registrazione che possono essere utilizzate per diagnosticare quali membri del cluster sono stati trovati e adottati dalla cache GemFire. Questo può essere utilizzato per verificare che tutti i membri del cluster corretti siano trovati e che non si stia verificando alcuna individuazione di nodi cluster aggiuntiva o errata. Il file di registro per GemFire si trova nella directory temporanea AEM Forms configurata su JEE:

`.../LC_TEMP/adobeZZ__123456/Caching/Gemfire.log`

La stringa numerica dopo `adobeZZ_` è univoca per il nodo del server, pertanto è necessario cercare il contenuto effettivo della directory temporanea. I due caratteri dopo `adobe` dipendono dal tipo di server dell&#39;applicazione: `wl`, `jb` o `ws`.

I registri di esempio seguenti mostrano cosa accade quando un cluster a due nodi si trova.

Sul primo nodo, AP-HP8:

```xml
[config 2011/08/05 09:28:09.143 EDT GemfireCacheAdapter <server.startup : 0> tid=0x65] This member, ap-hp8(4268):18763, is becoming group coordinator.
[info 2011/08/05 09:28:09.151 EDT GemfireCacheAdapter <server.startup : 0> tid=0x65] Entered into membership in group GF6.5.1.17 with ID ap-hp8(4268)<v0>:18763/56449.
[info 2011/08/05 09:28:09.152 EDT GemfireCacheAdapter <server.startup : 0> tid=0x65] Starting DistributionManager ap-hp8(4268)<v0>:18763/56449.
[info 2011/08/05 09:28:09.153 EDT GemfireCacheAdapter <server.startup : 0> tid=0x65] Initial (membershipManager) view =  [ap-hp8(4268)<v0>:18763/56449]
[info 2011/08/05 09:28:09.153 EDT GemfireCacheAdapter <server.startup : 0> tid=0x65] Admitting member <ap-hp8(4268)<v0>:18763/56449>. Now there are 1 non-admin member(s).
[info 2011/08/05 09:28:09.154 EDT GemfireCacheAdapter <server.startup : 0> tid=0x65] ap-hp8(4268)<v0>:18763/56449 is the elder and the only member.
[info 2011/08/05 09:28:09.163 EDT GemfireCacheAdapter <server.startup : 0> tid=0x65] Did not hear back from any other system. I am the first one.
[info 2011/08/05 09:28:09.164 EDT GemfireCacheAdapter <server.startup : 0> tid=0x65] DistributionManager ap-hp8(4268)<v0>:18763/56449 started on 239.192.81.1[33456]. There were 0 other DMs. others: []
[info 2011/08/05 09:28:20.841 EDT GemfireCacheAdapter <Pooled Message Processor 1> tid=0xc4] New administration member detected at ap-hp7(2821)<v1>:19498/59136.
```

Sull&#39;altro nodo, AP-HP7:

```xml
[info 2011/08/05 09:28:09.830 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] Attempting to join distributed system whose membership coordinator is ap-hp8(4268)<v0>:18763 using membership ID ap-hp7(2821):19498
[info 2011/08/05 09:28:10.058 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] Entered into membership in group GF6.5.1.17 with ID ap-hp7(2821)<v1>:19498/59136.
[info 2011/08/05 09:28:10.059 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] Starting DistributionManager ap-hp7(2821)<v1>:19498/59136.
[info 2011/08/05 09:28:10.060 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] Initial (membershipManager) view =  [ap-hp8(4268)<v0>:18763/56449, ap-hp7(2821)<v1>:19498/59136]
[info 2011/08/05 09:28:10.060 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] Admitting member <ap-hp8(4268)<v0>:18763/56449>. Now there are 1 non-admin member(s).
[info 2011/08/05 09:28:10.060 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] Admitting member <ap-hp7(2821)<v1>:19498/59136>. Now there are 2 non-admin member(s).
[info 2011/08/05 09:28:10.128 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] DistributionManager ap-hp7(2821)<v1>:19498/59136 started on 239.192.81.1[33456]. There were 1 other DMs. others: [ap-hp8(4268)<v0>:18763/56449]
```

**E se GemFire stesse trovando nodi che non dovrebbero?**

Ogni cluster distinto che condivide una rete aziendale deve utilizzare un set separato di localizzatori TCP, se vengono utilizzati locatori TCP, o un numero di porta UDP separato se viene utilizzata la configurazione UDP multicast. Poiché l’individuazione automatica UDP è la configurazione predefinita per AEM Forms su JEE e la stessa porta predefinita, 33456, può essere utilizzata da più cluster, è possibile che i cluster che non devono tentare di comunicare lo facciano in modo imprevisto, ad esempio i cluster di produzione e controllo qualità dovrebbero rimanere separati, ma potrebbero connettersi tra loro tramite multicast UDP.

La situazione più comune quando si potrebbero scoprire porte duplicate in una rete a cui il clustering GemFire è impropriamente durante il bootstrap di un cluster. Quello che si può scoprire è che il processo di bootstrap fallisce senza una causa chiara. In genere vengono visualizzati errori come questo:

```xml
Caused by: com.ibm.ejs.container.UnknownLocalException: nested exception is: com.adobe.pof.schema.ObjectTypeNotFoundException: Object Type: dsc.sc_service_configuration not found.
                at com.adobe.pof.schema.POFDefaultDomain.getObjectType(POFDefaultDomain.java:93)
                at com.adobe.idp.dsc.initializer.DSCInitializerBean.serviceConfigAuditAttributeExists(DSCInitializerBean.java:225)
                at com.adobe.idp.dsc.initializer.DSCInitializerBean.installSchema(DSCInitializerBean.java:186)
                at com.adobe.idp.dsc.initializer.DSCInitializerBean.bootstrap(DSCInitializerBean.java:94)
                at com.adobe.idp.dsc.initializer.EJSLocalStatelessDSCInitializerBeanLocalEJB_7bb34e85.bootstrap(Unknown Source)
                at com.adobe.livecycle.bootstrap.bootstrappers.DSCBootstrapper.bootstrap(DSCBootstrapper.java:68)
```

In questo caso, il programma di avvio sta lavorando con GemFire per accedere alle tabelle richieste, e c&#39;è un&#39;incoerenza tra le tabelle accessibili tramite JDBC e le informazioni della tabella memorizzate nella cache restituite da GemFire, che proviene da un cluster diverso con un database sottostante diverso.

Anche se una porta duplicata diventerà spesso evidente durante l&#39;avvio, è possibile che questa situazione venga visualizzata in seguito, quando un cluster viene riavviato dopo essere stato disattivato quando si è verificato il bootstrap dell&#39;altro cluster, o quando la configurazione di rete viene modificata per rendere visibili i cluster che erano stati precedentemente isolati, a scopo multicast, l&#39;uno dall&#39;altro.

Per diagnosticare queste situazioni, è meglio guardare i log di GemFire e considerare attentamente se vengono trovati solo i nodi previsti. Per correggere il problema, è necessario modificare il

`adobe.cache.multicast-port`

a un valore diverso su uno o entrambi i cluster.

### 2) Condivisione GDS {#gds-sharing}

La condivisione GDS è configurata al di fuori di AEM Forms su JEE, a livello di O/S, dove è necessario disporre che la stessa struttura di directory condivisa sia disponibile per tutti i nodi del cluster. Nei sistemi di tipo Windows, questa operazione viene solitamente eseguita impostando una condivisione di file da un nodo all&#39;altro o da un filesystem remoto, come un accessorio NAS, a tutti i nodi. Nei sistemi UNIX, la condivisione GDS viene generalmente eseguita tramite condivisione file NFS, di nuovo, da un nodo all&#39;altro, o da un accessorio NAS.

Una possibile modalità di errore per il cluster è se la condivisione file remota non è disponibile o presenta problemi di scarsa rilevanza. Un montaggio remoto potrebbe non riuscire a causa di problemi di rete, impostazioni di protezione o configurazione errata. Un riavvio del sistema può causare modifiche di configurazione effettuate con giorni o settimane di anticipo, e questo può causare sorprese.

**Cosa succede se una condivisione NFS non viene caricata?**

Su UNIX, il modo in cui i montaggi NFS sono mappati alla struttura della directory può consentire la disponibilità di una directory GDS apparentemente utilizzabile, anche se il montaggio non riesce. Considera:

* Server NAS: Cartella condivisa NFS /u01/iapply/livecycle_gds
* Nodo 1: un punto di montaggio della cartella condivisa (ospitata sul server DB) che si trova qui: /u01/iapply/livecycle_gds
* Nodo 2: un punto di montaggio della cartella condivisa (ospitata sul server DB) che si trova qui: /u01/iapply/livecycle_gds

* LCES specifica il percorso di GDS: /u01/iapply/livecycle_gds

Se il montaggio sul nodo 1 non riesce, la struttura della directory conterrà ancora un percorso /u01/iapply/livecycle_gds al punto di montaggio vuoto e il nodo apparirà funzionare correttamente. Tuttavia, poiché il contenuto GDS non viene effettivamente condiviso con l’altro nodo, il cluster non funzionerà correttamente. Questo può e accade, e il risultato è che il cluster fallisce in modi misteriosi.

La migliore pratica è quella di organizzare le cose in modo che il punto di montaggio Linux non venga utilizzato come radice del GDS, ma piuttosto qualche directory al suo interno viene utilizzata come radice GDS:

* Se si dispone di un server NFS, potrebbe avere una directory: /some/storage/lc_cluster_dev/LC_GDS
* E sul tuo nodo cluster hai un punto di montaggio: /u01/iapply/shared
* Server_nfs: /some/storage/lc_cluster_dev/u01/iapply/shared
* Posiziona il tuo GDS su /u01/iapply/shared/LC_GDS

Ora, se per qualche motivo il montaggio non ha successo, il punto di montaggio non contiene una directory LC_GDS e il tuo cluster avrà un errore prevedibile, in quanto non può trovare alcun GDS.

**Come posso verificare che tutti i nodi visualizzino gli stessi GDS e dispongano delle autorizzazioni?**

La verifica dell’accesso e della condivisione GDS è più efficace tramite l’accesso a ciascun nodo come utente interattivo, tramite SSH o telnet ai nodi UNIX, o tramite desktop remoto ai sistemi Windows. Dovresti essere in grado di accedere alla directory o al file system GDS configurato su ogni nodo e creare file di prova da ogni nodo che sono visibili in tutti gli altri nodi.

Presta attenzione all&#39;ID utente in base al quale opera AEM Forms su JEE. Nelle installazioni chiavi in mano di Windows, si tratta di un amministratore locale. Su UNIX, può essere come un utente di servizio specifico configurato nello script di avvio o nella configurazione dell&#39;application server. È importante che questo ID utente sia in grado di creare e manipolare file GDS allo stesso modo su tutti i nodi.

Nei sistemi UNIX, le configurazioni NFS vengono spesso utilizzate per impostazione predefinita per non fidare della proprietà principale o dei diritti di accesso radice a file e oggetti. Se si esegue l&#39;application server come utente principale, è necessario specificare le opzioni del server NFS, del nodo che monta i file oppure entrambe per consentire l&#39;accesso e il controllo bilaterali dei file creati da un nodo e a cui si accede da un altro.

### (3) Condivisione del database {#database-sharing}

Affinché un cluster funzioni correttamente, è essenziale che lo stesso database sia condiviso da tutti i membri del cluster. L&#39;opportunità di sbagliare è approssimativamente:

* l&#39;impostazione accidentale di IDP_DS, EDC_DS, AdobeDefaultSA_DS o altre origini dati richieste in modo diverso su nodi cluster separati, in modo che i nodi puntino a database diversi.
* impostare accidentalmente più nodi separati per condividere un database quando non dovrebbero.

A seconda del server dell&#39;applicazione, può essere naturale che la connessione JDBC sia definita in un ambito cluster, in modo che definizioni diverse non siano possibili su nodi diversi. Su Jboss, tuttavia, è del tutto possibile impostare le cose in modo che un&#39;origine dati, come IDP_DS, punti a un database sul nodo 1, ma punta a qualcos&#39;altro sul nodo 2.

Il problema inverso è in realtà più comune, ovvero una situazione in cui più AEM Forms standalone (o cluster) sui nodi JEE accidentalmente puntano allo stesso schema quando non sono destinati a. Questo accade più spesso quando un DBA invia inconsapevolmente un singolo AEM Forms sulle informazioni di connessione del database JEE ai team di configurazione DEV e QA, nessuno di loro si rende conto che le istanze DEV e QA richiedono database separati.

## Cluster del server applicazioni {#application-server-cluster-1}

Per avere un AEM Forms con successo sul cluster JEE, è essenziale che il server applicazioni sia configurato e funzioni correttamente come cluster. In WebSphere e Weblogic, questo è un processo semplice e ben documentato. In Jboss, la configurazione del cluster è un po&#39; più pratica, e assicurarsi che i nodi siano configurati per agire come un cluster e in realtà trovare e comunicare tra di loro può essere una sfida. JBoss si basa internamente su JGroups, che utilizza il multicast UDP per trovare e coordinare con nodi peer, e possono verificarsi alcuni dei problemi menzionati con GemFire, come nodi che non riescono a trovarsi l&#39;un l&#39;altro quando dovrebbero, o che si trovano a vicenda quando non dovrebbero.

Riferimenti:

* [Servizi aziendali ad alta disponibilità tramite cluster JBoss](https://docs.jboss.org/jbossas/jboss4guide/r4/html/cluster.chapt.html)

* [Server Oracle WebLogic - Utilizzo dei cluster](https://docs.oracle.com/cd/E12840_01/wls/docs103/pdf/cluster.pdf)

### Come posso verificare che JBoss sia stato raggruppato correttamente? {#check-jboss-clustering}

Quando JBoss si avvia, quando i membri del cluster vengono scoperti, i messaggi di livello INFO sul nodo che fa parte del cluster vengono registrati nel file di log/console.

Se durante l&#39;esecuzione è stato specificato un nome cluster tramite l&#39;opzione della riga di comando -g, verranno visualizzati messaggi simili ai seguenti:

```xml
GMS: address is 10.36.34.44:55200 (cluster=QE_cluster)
GMS: address is 10.36.34.44:55200 (cluster=QE_cluster-HAPartitionCache)
and ones like:

[org.jboss.ha.framework.interfaces.HAPartition.QE_cluster] (JBoss System Threads(1)-3) Number of cluster members: 1
2011-07-14 11:34:03,072 INFO  [org.jboss.ha.framework.interfaces.HAPartition.QE_cluster] (JBoss System Threads(1)-3) Other members: 0
2011-07-14 11:34:03,138 INFO  [org.jboss.cache.RPCManagerImpl] (main) Received new cluster view: [10.36.34.44:55200|0] [10.36.34.44:55200]
2011-07-14 11:34:03,139 INFO  [org.jboss.cache.RPCManagerImpl] (main) Cache local address is 10.36.34.44:55200
```

### Programmatore al quarzo {#quartz-scheduler}

Nella maggior parte dei casi, AEM Forms sull&#39;utilizzo da parte di JEE della pianificazione interna al quarzo in un cluster è destinato a seguire automaticamente la configurazione globale del cluster di AEM Forms su JEE in generale. C&#39;è, tuttavia, un bug, #2794033, che causa il fallimento della configurazione automatica del cluster di quarzo se i localizzatori TCP vengono utilizzati per Gemfire invece del rilevamento automatico multicast. In questo caso, Quartz verrà eseguito in modo errato in una modalità non cluster. Questo creerà deadlock e corruzione dei dati nelle tabelle del quarzo. Gli effetti collaterali sono peggiori nella versione 8.2.x rispetto alla versione 9.0, in quanto il quarzo non è usato così tanto, ma è ancora lì.

Per questo problema sono disponibili le seguenti correzioni: 8.2.1.2 QF2.143 e 9.0.0.2 QF2.44.

C&#39;è anche una soluzione alternativa, che consiste nell&#39;impostare entrambe queste proprietà:

* `-Dadobe.cache.cluster.locators=xxx`

* `-Dadobe.cache.cluster-locators=xxx`

Nota che un&#39;impostazione utilizza un punto tra &quot;cluster&quot; e &quot;locators&quot; e l&#39;altra utilizza un trattino. Questo è facile da implementare e meno rischioso rispetto all&#39;applicazione di una patch software, ma comporta la creazione artificiale di un&#39;impostazione di configurazione aggiuntiva confusa e con nomi errati.

### Come posso verificare che Quartz sia in esecuzione come un singolo nodo o cluster? {#check-quartz}

Per determinare come Quartz si è configurato, è necessario esaminare i messaggi generati dal servizio AEM Forms on JEE Scheduler durante l&#39;avvio. Questi messaggi vengono generati con la gravità INFO e potrebbe essere necessario regolare il livello di log e riavviare per ottenere i messaggi. All&#39;interno della sequenza di avvio di AEM Forms su JEE, l&#39;inizializzazione di Quartz inizia con la seguente riga:

INFO `[com.adobe.idp.scheduler.SchedulerServiceImpl]` IDPSchedulerService onLoad
È importante individuare questa prima riga nei registri perché alcuni server applicativi utilizzano anche Quartz e le relative istanze Quartz non devono essere confuse con l’istanza utilizzata dal servizio AEM Forms on JEE Scheduler. Questo è l&#39;indicazione che il servizio di pianificazione è in fase di avvio e le linee che lo seguono vi indicheranno se sta iniziando o meno in modalità cluster correttamente. In questa sequenza compaiono diversi messaggi, ed è l’ultimo messaggio &quot;avviato&quot; che rivela la configurazione del quarzo:

Qui viene fornito il nome dell&#39;istanza Quartz: `IDPSchedulerService_$_ap-hp8.ottperflab.corp.adobe.com1312883903975`. Il nome dell&#39;istanza Quartz dello scheduler inizierà sempre con la stringa `IDPSchedulerService_$_`. La stringa aggiunta alla fine indica se quarz è in esecuzione o meno in modalità cluster. L&#39;identificatore univoco lungo generato dal nome host del nodo e una lunga stringa di cifre, in questo caso `ap-hp8.ottperflab.corp.adobe.com1312883903975`, indica che funziona in un cluster. Se funziona come un singolo nodo, l&#39;identificatore sarà un numero a due cifre, &quot;20&quot;:

INFO `[org.quartz.core.QuartzScheduler]` Pianificazione `IDPSchedulerService_$_20` avviata.
Questo controllo deve essere eseguito separatamente su tutti i nodi del cluster, in quanto la pianificazione di ciascun nodo determina in modo indipendente se operare in modalità cluster.

### Quali tipi di problemi si verificano se il quarzo è in esecuzione in modalità sbagliata? {#quartz-running-in-wrong-mode}

Se Quartz è configurato per l&#39;esecuzione come un singolo nodo, ma è in esecuzione in un cluster e la condivisione di tabelle di database Quartz con altri nodi, questo si tradurrà in un funzionamento inaffidabile del servizio AEM Forms su JEE Scheduler e sarà solitamente accompagnato da deadlock del database. Questa è una traccia di stack abbastanza tipica che si potrebbe vedere in questa situazione:

```xml
[1/20/11 10:40:57:584 EST] 00000035 ErrorLogger   E org.quartz.core.ErrorLogger schedulerError An error occured while marking executed job complete. job= 'Asynchronous.TaskFormDataSaved:12955380518320.5650479324757354'
 org.quartz.JobPersistenceException: Couldn't remove trigger: ORA-00060: deadlock detected while waiting for resource  [See nested exception: java.sql.SQLException: ORA-00060: deadlock detected while waiting for resource ]
        at org.quartz.impl.jdbcjobstore.JobStoreSupport.removeTrigger(JobStoreSupport.java:1405)
        at org.quartz.impl.jdbcjobstore.JobStoreSupport.triggeredJobComplete(JobStoreSupport.java:2888)
        at org.quartz.impl.jdbcjobstore.JobStoreSupport$38.execute(JobStoreSupport.java:2872)
        at org.quartz.impl.jdbcjobstore.JobStoreSupport$40.execute(JobStoreSupport.java:3628)
        at org.quartz.impl.jdbcjobstore.JobStoreSupport.executeInNonManagedTXLock(JobStoreSupport.java:3662)
        at org.quartz.impl.jdbcjobstore.JobStoreSupport.executeInNonManagedTXLock(JobStoreSupport.java:3624)
        at org.quartz.impl.jdbcjobstore.JobStoreSupport.triggeredJobComplete(JobStoreSupport.java:2868)
        at org.quartz.core.QuartzScheduler.notifyJobStoreJobComplete(QuartzScheduler.java:1698)
        at org.quartz.core.JobRunShell.run(JobRunShell.java:273)
        at org.quartz.simpl.SimpleThreadPool$WorkerThread.run(SimpleThreadPool.java:529)
Caused by: java.sql.SQLException: ORA-00060: deadlock detected while waiting for resource
```

### Come si sincronizzano gli orologi di sistema in un cluster? {#ynchronize-system-clocks-cluster}

Affinché un cluster funzioni senza problemi, è essenziale che gli orologi su tutti i nodi del cluster siano strettamente sincronizzati. Questo non può essere fatto adeguatamente a mano e deve essere fatto da una qualche forma di servizio di sincronizzazione del tempo che viene eseguito molto regolarmente. Gli orologi su tutti i nodi devono essere entro un secondo l&#39;uno dall&#39;altro. La best practice prevede la sincronizzazione non solo dei nodi del cluster, ma anche del load balancer, del server di database, del server NAS GDS e di qualsiasi altro componente.

La sincronizzazione dell&#39;ora di Windows tende ad essere nel controller di dominio. I sistemi UNIX possono sincronizzarsi utilizzando NTP in un&#39;altra origine temporale. È consigliabile se tutti i sistemi, sia i nodi AEM Forms su JEE che altri componenti di sistema, si sincronizzano con la stessa origine, se possibile.

Non è assolutamente sufficiente, anche negli ambienti di test più temporanei, impostare manualmente gli orologi sui nodi. L&#39;impostazione manuale degli orologi non darà una sincronizzazione abbastanza precisa, e gli orologi sui due nodi inevitabilmente si sposteranno l&#39;uno rispetto all&#39;altro, anche in un periodo di un solo giorno. Un meccanismo di sincronizzazione del tempo attivo è essenziale per un funzionamento affidabile del cluster.

### Load Balancer {#load-balancer}

Un requisito tipico per un cluster che fornisce servizi interattivi utente è un load balancer HTTP che distribuirà le richieste HTTP tra il cluster. L&#39;utilizzo corretto di un load balancer con un cluster AEM Forms su JEE richiede la configurazione di quanto segue:

* viscosità

* Regole di riscrittura URL

* controllo integrità nodo

### Cosa devo fare riguardo alla funzione di controllo dello stato di salute del Load Balancer? {#load-balancer-health-check}

È possibile configurare alcuni bilanciatori di carico per eseguire un controllo periodico dello stato dei nodi in fase di bilanciamento del carico. Di solito, si tratta di un URL di una funzione di applicazione a cui il load balancer tenta di accedere. Se il carico ha esito positivo, il nodo viene considerato integro e mantenuto nel set di bilanciamento del carico. Se l’URL non viene caricato, si presume che il nodo sia errato e viene eliminato dal set. Di solito, l&#39;URL del controllo dello stato di salute è semplicemente connesso alla pagina di accesso di AEM Forms su JEE AdminUI. Questo non è un controllo di integrità ideale per un membro del cluster, e sarebbe meglio implementare un processo di breve durata e utilizzare l’URL API REST come funzione di controllo dello stato.

## Percorso file temporaneo e impostazioni cluster simili {#temporary-file-path-cluster-settings}

Alcune impostazioni del percorso file all&#39;interno di AEM Forms su JEE sono stabilite a livello di cluster e hanno la stessa impostazione effettiva su ogni nodo, ma vengono interpretate in modo indipendente su ogni nodo per fare riferimento a file locali. Le impostazioni principali a cui pensare sono il percorso del font e le impostazioni della directory temporanea. Vai alla schermata Configurazioni core AdminUI (Home > Impostazioni > Sistema core > Configurazioni core)

Controllare le impostazioni seguenti:

1. Posizione della directory temporanea
1. Posizione della directory Font del server Adobe
1. Posizione della directory Font del cliente
1. Posizione della directory dei font di sistema
1. Posizione del file di configurazione dei servizi dati

Il cluster dispone di una sola impostazione di percorso per ciascuna di queste impostazioni di configurazione. Ad esempio, la posizione della directory Temp potrebbe essere `/home/project/QA2/LC_TEMP`. In un cluster, è necessario che ogni nodo abbia effettivamente questo particolare percorso accessibile. Se un nodo ha il percorso del file temporaneo previsto e un altro nodo no, il nodo che non funziona correttamente.

Anche se questi file e percorsi possono essere condivisi tra i nodi o posizionati separatamente, o su file system remoti, è generalmente consigliabile che siano copie locali sull&#39;archiviazione disco del nodo locale.

Il percorso della directory temporanea, in particolare, non deve essere condiviso tra i nodi. Per verificare che la directory temporanea non sia condivisa, si deve utilizzare una procedura simile a quella descritta per verificare il GDS: vai su ogni nodo, crea un file temporaneo nel percorso indicato dall&#39;impostazione del percorso, quindi verifica che gli altri nodi non condividano il file. Se possibile, il percorso della directory temporanea deve fare riferimento all&#39;archiviazione locale del disco su ciascun nodo e deve essere controllato.

Per ciascuna delle impostazioni del percorso, assicurati che il percorso esista effettivamente e sia accessibile da ogni nodo del cluster, utilizzando l&#39;identità di utilizzo effettiva in cui viene eseguito AEM Forms su JEE. Il contenuto della directory dei font deve essere leggibile. La directory temporanea deve consentire la lettura, la scrittura e il controllo.
















