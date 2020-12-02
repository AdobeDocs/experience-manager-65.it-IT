---
title: Scaricamento dei processi
seo-title: Scaricamento dei processi
description: Scoprite come configurare e utilizzare AEM istanze in una topologia per eseguire tipi specifici di elaborazione.
seo-description: Scoprite come configurare e utilizzare AEM istanze in una topologia per eseguire tipi specifici di elaborazione.
uuid: e971d403-dfd2-471f-b23d-a67e35f1ed88
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 370151df-3b8e-41aa-b586-5c21ecb55ffe
translation-type: tm+mt
source-git-commit: 29f8e59e3fc9d3c089ee3b78c24638cd3cd2e96b
workflow-type: tm+mt
source-wordcount: '2403'
ht-degree: 1%

---


# Scaricamento di processi{#offloading-jobs}

## Introduzione {#introduction}

Lo scarico distribuisce le attività di elaborazione tra  istanze di Experience Manager in una topologia. Con lo scaricamento, potete utilizzare istanze di Experienci Manager  specifiche per eseguire specifici tipi di elaborazione. L&#39;elaborazione specializzata consente di ottimizzare l&#39;utilizzo delle risorse server disponibili.

L&#39;offload è basato sulle funzionalità [Apache Sling Discovery](https://sling.apache.org/documentation/bundles/discovery-api-and-impl.html) e Sling JobManager. Per utilizzare lo scaricamento, è possibile aggiungere  cluster di Experienci Manager a una topologia e identificare gli argomenti del processo che il cluster elabora. I cluster sono formati da una o più istanze  Experience Manager, in modo che una singola istanza sia considerata un cluster.

Per informazioni sull&#39;aggiunta di istanze a una topologia, vedere [Amministrazione delle topologie](/help/sites-deploying/offloading.md#administering-topologies).

### Distribuzione processo {#job-distribution}

Sling JobManager e JobConsumer consentono la creazione di processi elaborati in una topologia:

* JobManager: Un servizio che crea processi per argomenti specifici.
* JobConsumer: Un servizio che esegue processi relativi a uno o più argomenti. Più servizi JobConsumer possono essere registrati per lo stesso argomento.

Quando JobManager crea un processo, il framework Offloading seleziona un cluster di Experienci Manager  nella topologia per eseguire il processo:

* Il cluster deve includere una o più istanze che eseguono un JobConsumer registrato per l&#39;argomento del processo.
* L&#39;argomento deve essere abilitato per almeno un&#39;istanza del cluster.

Per informazioni sull&#39;ottimizzazione della distribuzione dei processi, vedere [Configurazione del consumo di argomenti](/help/sites-deploying/offloading.md#configuring-topic-consumption).

![chlimage_1-109](assets/chlimage_1-109.png)

Quando il framework Offloading seleziona un cluster per eseguire un processo e il cluster è composto da più istanze, Sling Distribution determina quale istanza del cluster esegue il processo.

### Payload processo {#job-payloads}

Il framework Offloading supporta i payload di processi che associano i processi alle risorse del repository. I payload dei processi sono utili quando i processi vengono creati per elaborare le risorse e il processo viene scaricato in un altro computer.

Dopo la creazione di un processo, il payload è garantito solo nell’istanza che crea il processo. Durante l&#39;offload del processo, gli agenti di replica assicurano che il payload venga creato nell&#39;istanza che alla fine consuma il processo. Al termine dell’esecuzione del processo, la replica inversa causa la copia del payload nell’istanza che ha creato il processo.

## Amministrazione delle topologie {#administering-topologies}

Le topologie sono cluster di Experienci Manager  a accoppiamento approssimativo che partecipano allo scarico. Un cluster è costituito da una o più istanze  server di Experience Manager (una singola istanza è considerata un cluster).

Ogni istanza  Experience Manager esegue i seguenti servizi relativi allo scarico:

* Servizio di individuazione: Invia richieste a un connettore topologia per partecipare alla topologia.
* Connettore topologia: Riceve le richieste di partecipazione e accetta o rifiuta ogni richiesta.

Il servizio di individuazione di tutti i membri della topologia punta al connettore topologia su uno dei membri. Nelle sezioni che seguono, questo membro viene denominato membro principale.

![chlimage_1-110](assets/chlimage_1-110.png)

Ogni cluster nella topologia contiene un&#39;istanza riconosciuta come leader. Il cluster leader interagisce con la topologia per conto degli altri membri del cluster. Quando il riempimento iniziale lascia il cluster, viene automaticamente selezionato un nuovo riempimento iniziale per il cluster.

### Visualizzazione della topologia {#viewing-the-topology}

Utilizzate il Browser topologia per esplorare lo stato della topologia a cui partecipa l&#39;istanza del Experience Manager . Il Browser topologia mostra i cluster e le istanze della topologia.

Per ciascun cluster viene visualizzato un elenco di membri del cluster che indica l&#39;ordine in cui ciascun membro è entrato nel cluster e quale membro è il membro iniziale. La proprietà Current (Corrente) indica l&#39;istanza attualmente amministrata.

Per ogni istanza del cluster, potete vedere diverse proprietà relative alla topologia:

* Un elenco consentiti  di argomenti per il consumer di posti di lavoro dell&#39;istanza.
* I punti finali esposti per la connessione con la topologia.
* Gli argomenti del processo per cui l’istanza è registrata per lo scaricamento.
* Gli argomenti del processo elaborati dall’istanza.

1. Utilizzando l&#39;interfaccia touch, fare clic sulla scheda Strumenti. ([http://localhost:4502/tools.html](http://localhost:4502/tools.html))
1. Nell&#39;area Granite Operations, fare clic su Offload Browser.
1. Nel pannello di navigazione, fate clic su Browser topologia.

   Vengono visualizzati i cluster che partecipano alla topologia.

   ![chlimage_1-111](assets/chlimage_1-111.png)

1. Fate clic su un cluster per visualizzare un elenco delle istanze presenti nel cluster e il relativo ID, stato corrente e stato riempimento iniziale.
1. Fate clic su un ID istanza per visualizzare le proprietà più dettagliate.

È inoltre possibile utilizzare la console Web per visualizzare le informazioni sulla topologia. La console fornisce ulteriori informazioni sui cluster di topologia:

* Quale istanza è l&#39;istanza locale.
* I servizi del connettore topologia utilizzati da questa istanza per connettersi alla topologia (in uscita) e i servizi che si connettono a questa istanza (in entrata).
* Modificare la cronologia per la topologia e le proprietà dell&#39;istanza.

Per aprire la pagina Gestione topologia della console Web, effettuate le seguenti operazioni:

1. Aprite la console Web nel browser. ([http://localhost:4502/system/console](http://localhost:4502/system/console))
1. Fate clic su Principale > Gestione topologia.

   ![chlimage_1-112](assets/chlimage_1-112.png)

### Configurazione dell&#39;appartenenza alla topologia {#configuring-topology-membership}

Il servizio di individuazione basata sulle risorse Apache Sling viene eseguito su ogni istanza per controllare in che modo  istanze di Experience Manager interagiscono con una topologia.

Il servizio Discovery invia richieste POST periodiche (heartbeat) ai servizi del connettore Topologia per stabilire e gestire le connessioni con la topologia. Il servizio Connettore topologia mantiene un elenco consentiti  di indirizzi IP o nomi host che possono essere aggiunti alla topologia:

* Per unire un&#39;istanza a una topologia, specificate l&#39;URL del servizio Connettore topologia del membro principale.
* Per abilitare un&#39;istanza a partecipare a una topologia, aggiungere l&#39;istanza al elenco consentiti  del servizio Connettore topologia del membro principale.

Utilizzate la console Web o un nodo sling:OsgiConfig per configurare le seguenti proprietà del servizio org.apache.sling.discovery.impt.Config:

<table>
 <tbody>
  <tr>
   <th>Nome proprietà</th>
   <th>Nome OSGi</th>
   <th>Descrizione</th>
   <th>Valore predefinito</th>
  </tr>
  <tr>
   <td>Timeout Heartbeat (secondi)</td>
   <td>heartbeatTimeout</td>
   <td>Tempo in secondi per attendere una risposta heartbeat prima che l'istanza di destinazione venga considerata non disponibile. </td>
   <td>20</td>
  </tr>
  <tr>
   <td>Intervallo heartbeat (secondi)</td>
   <td>heartbeatInterval</td>
   <td>Tempo in secondi tra heartbeat.</td>
   <td>15</td>
  </tr>
  <tr>
   <td>Ritardo minimo degli eventi (secondi)</td>
   <td>minEventDelay</td>
   <td><p>Quando si verifica una modifica alla topologia, il tempo necessario per ritardare la modifica dello stato da TOPOLOGY_CHANGING a TOPOLOGY_CHANGED. Ogni modifica che si verifica quando lo stato è TOPOLOGY_CHANGING aumenta il ritardo di questo periodo di tempo.</p> <p>Questo ritardo impedisce agli ascoltatori di essere inondati da eventi. </p> <p>Per non utilizzare ritardi, specificate 0 o un numero negativo.</p> </td>
   <td>3</td>
  </tr>
  <tr>
   <td>URL del connettore topologia</td>
   <td>topologyConnectorUrls</td>
   <td>URL dei servizi di Topology Connector per inviare messaggi heartbeat.</td>
   <td>http://localhost:4502/libs/sling/topology/connector</td>
  </tr>
  <tr>
   <td>Elenco consentiti  connettore topologia</td>
   <td>topologyConnectorWhitelist</td>
   <td>L'elenco di indirizzi IP o nomi host consentiti dal servizio locale Connettore topologia nella topologia. </td>
   <td><p>localhost</p> <p>127.0.0.1</p> </td>
  </tr>
  <tr>
   <td>Nome descrittore repository</td>
   <td>leaderElectionRepositoryDescriptor</td>
   <td> </td>
   <td>&lt;nessun valore&gt;</td>
  </tr>
 </tbody>
</table>

Per collegare un’istanza CQ al membro principale di una topologia, attenersi alla procedura descritta di seguito. La procedura punta l&#39;istanza all&#39;URL del connettore topologia del membro della topologia principale. Eseguire questa procedura su tutti i membri della topologia.

1. Aprite la console Web nel browser. ([http://localhost:4502/system/console](http://localhost:4502/system/console))
1. Fate clic su Principale > Gestione topologia.
1. Fate clic su Configura servizio di individuazione.
1. Aggiungere un elemento alla proprietà URL del connettore topologia e specificare l&#39;URL del servizio Connettore topologia principale del membro topologia. L’URL si trova nel modulo https://rootservername:4502/libs/sling/topology/connector.

Eseguire la procedura seguente sul membro principale della topologia. La procedura aggiunge i nomi degli altri membri della topologia al elenco consentiti  Discovery Service.

1. Aprite la console Web nel browser. ([http://localhost:4502/system/console](http://localhost:4502/system/console))
1. Fate clic su Principale > Gestione topologia.
1. Fate clic su Configura servizio di individuazione.
1. Per ciascun membro della topologia, aggiungete un elemento alla proprietà  elenco consentiti del connettore topologia e specificate il nome host o l&#39;indirizzo IP del membro della topologia.

## Configurazione consumo argomento {#configuring-topic-consumption}

Utilizzate il browser di scaricamento per configurare il consumo dell&#39;argomento per le istanze del Experience Manager  nella topologia. Per ogni istanza, potete specificare gli argomenti che essa consuma. Ad esempio, per configurare la topologia in modo che solo un&#39;istanza utilizzi argomenti di un tipo specifico, disattivate l&#39;argomento per tutte le istanze tranne una.

I processi vengono distribuiti tra le istanze per le quali è stato attivato l’argomento associato tramite la logica round-robin.

1. Utilizzando l&#39;interfaccia touch, fare clic sulla scheda Strumenti. ([http://localhost:4502/tools.html](http://localhost:4502/tools.html))
1. Nell&#39;area Granite Operations, fare clic su Offload Browser.
1. Nel pannello di navigazione, fate clic su Offload Browser (Offload Browser).

   Vengono visualizzati gli argomenti di scaricamento e le istanze del server che possono utilizzare gli argomenti.

   ![chlimage_1-113](assets/chlimage_1-113.png)

1. Per disabilitare l&#39;uso di un argomento per un&#39;istanza, sotto il nome dell&#39;argomento fare clic su Disattiva accanto all&#39;istanza.
1. Per configurare l’uso di tutti gli argomenti per un’istanza, fai clic sull’identificatore di istanza sotto a qualsiasi argomento.

   ![chlimage_1-114](assets/chlimage_1-114.png)

1. Fate clic su uno dei seguenti pulsanti accanto a un argomento per configurare il comportamento di consumo per l’istanza, quindi fate clic su Salva:

   * Abilitato: Questa istanza utilizza i processi di questo argomento.
   * Disattivato: In questa istanza non vengono utilizzati processi di questo argomento.
   * Esclusivo: Questa istanza utilizza solo i processi di questo argomento.

   **Nota:** quando selezionate Esclusivo per un argomento, tutti gli altri argomenti vengono impostati automaticamente su Disattivato.

### Consumatori di lavori installati {#installed-job-consumers}

Diverse implementazioni JobConsumer sono installate con  Experience Manager. Gli argomenti per i quali questi JobConsumers sono registrati vengono visualizzati nel browser di offload. Altri argomenti visualizzati sono quelli registrati da JobConsumers personalizzati. Nella tabella seguente è illustrato il processo predefinito JobConsumers.

| Argomento processo | Service PID | Descrizione |
|---|---|---|
| / | org.apache.sling.event.impl.jobs.deprecated.EventAdminBridge | Installato con Apache Sling. Elabora i processi generati dall&#39;amministratore degli eventi OSGi per garantire la compatibilità con le versioni precedenti. |
| com/day/cq/replica/job/&amp;ast; | com.day.cq.replication.impl.AgentManagerImpl | Agente di replica che replica i payload di processi. |

<!--
| com/adobe/granite/workflow/offloading |com.adobe.granite.workflow.core.offloading.WorkflowOffloadingJobConsumer |Processes jobs that the DAM Update Asset Offloader workflow generates. |
-->

### Disattivazione e abilitazione degli argomenti per un&#39;istanza {#disabling-and-enabling-topics-for-an-instance}

Il servizio Apache Sling Job Consumer Manager fornisce le proprietà dell&#39;argomento  elenco consentiti e  elenco Bloccati. Configurate queste proprietà per abilitare o disabilitare l&#39;elaborazione di argomenti specifici in un&#39;istanza di Experience Manager .

**Nota:** se l&#39;istanza appartiene a una topologia, puoi anche utilizzare Offload Browser su qualsiasi computer della topologia per attivare o disattivare gli argomenti.

La logica che crea l&#39;elenco di argomenti abilitati prima consente di tutti gli argomenti presenti nel elenco consentiti , quindi rimuove gli argomenti presenti nel elenco Bloccati . Per impostazione predefinita, tutti gli argomenti sono attivati (il valore  elenco consentiti è `*`) e non vengono disabilitati argomenti (il elenco Bloccati  non ha alcun valore).

Utilizzate Console Web o un nodo `sling:OsgiConfig` per configurare le seguenti proprietà. Per i nodi `sling:OsgiConfig`, il PID del servizio Job Consumer Manager è org.apache.sling.event.impl.jobs.JobConsumerManager.

| Nome proprietà nella console Web | OSGi ID | Descrizione |
|---|---|---|
| Elenco consentiti  argomento | job.consumermanager.whitelist | Elenco di argomenti elaborati dal servizio JobManager locale. Il valore predefinito di &amp;ast; determina l&#39;invio di tutti gli argomenti al servizio TopicConsumer registrato. |
| Elenco Bloccati  argomento | job.consumermanager.blacklist | Un elenco di argomenti che il servizio JobManager locale non elabora. |

## Creazione Di Agenti Di Replica Per Lo Scaricamento Di {#creating-replication-agents-for-offloading}

Il framework di scarico utilizza la replica per il trasporto delle risorse tra autore e lavoratore. Il framework di scaricamento crea automaticamente agenti di replica quando le istanze si uniscono alla topologia. Gli agenti vengono creati con valori predefiniti. È necessario modificare manualmente la password utilizzata dagli agenti per l&#39;autenticazione.

>[!CAUTION]
>
>Un problema noto con gli agenti di replica generati automaticamente richiede la creazione manuale di nuovi agenti di replica. Seguire la procedura descritta in [Problemi relativi all&#39;utilizzo degli agenti di replica generati automaticamente](/help/sites-deploying/offloading.md#problems-using-the-automatically-generated-replication-agents) prima di creare gli agenti per lo scarico.

Creare gli agenti di replica che trasportano i payload di processo tra le istanze per lo scarico. L&#39;illustrazione seguente mostra gli agenti che devono essere scaricati dall&#39;istanza di creazione a un&#39;istanza di lavoro. L’autore ha un Sling ID pari a 1 e l’istanza di lavoro ha un Sling ID pari a 2:

![chlimage_1-115](assets/chlimage_1-115.png)

Questa configurazione richiede i tre agenti seguenti:

1. Un agente in uscita nell&#39;istanza di creazione che viene replicato nell&#39;istanza di lavoro.
1. Un agente inverso nell&#39;istanza di creazione che estrae dalla casella in uscita l&#39;istanza di lavoro.
1. Un agente in uscita nell&#39;istanza del lavoratore.

Lo schema di replica è simile a quello utilizzato tra le istanze di creazione e pubblicazione. Tuttavia, per la situazione di scarico tutti i casi coinvolti sono istanze di authoring.

>[!NOTE]
>
>Il framework di offload utilizza la topologia per ottenere gli indirizzi IP delle istanze di scarico. Il framework quindi crea automaticamente gli agenti di replica basati su questi indirizzi IP. Se gli indirizzi IP delle istanze di scaricamento cambiano successivamente, la modifica viene propagata automaticamente sulla topologia dopo il riavvio dell&#39;istanza. Tuttavia, il framework di offload non aggiorna automaticamente gli agenti di replica per riflettere i nuovi indirizzi IP. Per evitare questa situazione, utilizzare indirizzi IP fissi per tutte le istanze della topologia.

### Denominazione degli agenti di replica per l&#39;offload di {#naming-the-replication-agents-for-offloading}

Utilizzare un formato specifico per la proprietà ***Name*** degli agenti di replica, in modo che il framework di scarico utilizzi automaticamente l&#39;agente corretto per istanze di lavoro specifiche.

**Denominazione dell’agente in uscita nell’istanza di creazione:**

`offloading_<slingid>`, dove  `<slingid>` è l&#39;ID Sling dell&#39;istanza di lavoro.

Esempio: `offloading_f5c8494a-4220-49b8-b079-360a72f71559`

**Denominazione dell’agente inverso nell’istanza di creazione:**

`offloading_reverse_<slingid>`, dove  `<slingid>` è l&#39;ID Sling dell&#39;istanza di lavoro.

Esempio: `offloading_reverse_f5c8494a-4220-49b8-b079-360a72f71559`

**Denominazione della casella in uscita nell’istanza del lavoratore:**

`offloading_outbox`

### Creazione dell&#39;agente in uscita {#creating-the-outgoing-agent}

1. Creare un **Agente di replica** sull&#39;autore. (vedere la [documentazione relativa agli agenti di replica](/help/sites-deploying/replication.md)). Specificare un **Titolo**. La **Name** deve seguire la convenzione di denominazione.
1. Create l&#39;agente utilizzando le seguenti proprietà:

   | Proprietà | Valore |
   |---|---|
   | Impostazioni > Tipo di serializzazione | Predefiniti |
   | Trasporto > URI trasporto | https://*`<ip of target instance>`*:*`<port>`*`/bin/receive?sling:authRequestLogin=1` |
   | Trasporto > Trasporto utente | Utente di replica sull&#39;istanza di destinazione |
   | Trasporto > Password trasporto | Password utente di replica nell&#39;istanza di destinazione |
   | Extended > Metodo HTTP | POST |
   | Triggers > Ignora predefiniti | Vero |

### Creazione dell&#39;agente inverso {#creating-the-reverse-agent}

1. Creare un **agente di replica inversa** sull&#39;autore. (vedere la [documentazione relativa agli agenti di replica](/help/sites-deploying/replication.md).) Specificare un **Titolo**. La **Name** deve seguire la convenzione di denominazione.
1. Create l&#39;agente utilizzando le seguenti proprietà:

   | Proprietà | Valore |
   |---|---|
   | Impostazioni > Tipo di serializzazione | Predefiniti |
   | Trasporto > URI trasporto | https://*`<ip of target instance>`*:*`<port>`*`/bin/receive?sling:authRequestLogin=1` |
   | Trasporto > Trasporto utente | Utente di replica sull&#39;istanza di destinazione |
   | Trasporto > Password trasporto | Password utente di replica nell&#39;istanza di destinazione |
   | Extended > Metodo HTTP | GET |

### Creazione dell&#39;agente di posta in uscita {#creating-the-outbox-agent}

1. Creare un **Agente di replica** nell&#39;istanza di lavoro. (vedere la [documentazione relativa agli agenti di replica](/help/sites-deploying/replication.md).) Specificare un **Titolo**. Il **Nome** deve essere `offloading_outbox`.
1. Create l&#39;agente utilizzando le proprietà seguenti.

   | Proprietà | Valore |
   |---|---|
   | Impostazioni > Tipo di serializzazione | Predefiniti |
   | Trasporto > URI trasporto | repo://var/replication/outbox |
   | Trigger > Ignore Default | Vero |

### Ricerca dell&#39;ID Sling {#finding-the-sling-id}

Ottenete l’ID Sling di un’istanza di Experience Manager  utilizzando uno dei seguenti metodi:

* Aprite la console Web e, nelle Impostazioni Sling, individuate il valore della proprietà Sling ID ([http://localhost:4502/system/console/status-slingsettings](http://localhost:4502/system/console/status-slingsettings)). Questo metodo è utile se l’istanza non fa ancora parte della topologia.
* Utilizzate il browser Topologia se l&#39;istanza fa già parte della topologia.

<!--
## Offloading the Processing of DAM Assets {#offloading-the-processing-of-dam-assets}

Configure the instances of a topology so that specific instances perform the background processing of assets that are added or updated in DAM.

By default, Experience Manager executes the [!UICONTROL DAM Update Asset] workflow when a DAM asset changes or one is added to DAM. Change the default behavior so that Experience Manager instead executes the [!UICONTROL DAM Update Asset Offloader] workflow. This workflow generates a JobManager job that has a topic of `com/adobe/granite/workflow/offloading`. Then, configure the topology so that the job is offloaded to a dedicated worker.

>[!CAUTION]
>
>No workflow should be transient when used with workflow offloading. For example, the [!UICONTROL DAM Update Asset] workflow must not be transient when used for asset offloading. To set/unset the transient flag on a workflow, see [Transient Workflows](/help/assets/performance-tuning-guidelines.md#workflows).

The following procedure assumes the following characteristics for the offloading topology:

* One or more Experience Manager instance are authoring instances that users interact with for adding or updating DAM assets.
* Users to do not directly interact with one or more Experience Manager instances that process the DAM assets. These instances are dedicated to the background processing of DAM assets.

1. On each Experience Manager instance, configure the Discovery Service so that it points to the root Topography Connector. (See [Configuring Topology Membership](#title4).)
1. Configure the root Topography Connector so that the connecting instances are on the allow list.
1. Open Offloading Browser and disable the `com/adobe/granite/workflow/offloading` topic on the instances with which users interact to upload or change DAM assets.

   ![chlimage_1-116](assets/chlimage_1-116.png)

1. On each instance that users interact with to upload or change DAM assets, configure workflow launchers to use the [!UICONTROL DAM Update Asset Offloading] workflow:

    1. Open the Workflow console.
    1. Click the Launcher tab.
    1. Locate the two Launcher configurations that execute the [!UICONTROL DAM Update Asset] workflow. One launcher configuration event type is Node Created, and the other type is Node Modified.
    1. Change both event types so that they execute the [!UICONTROL DAM Update Asset Offloading] workflow. (For information about launcher configurations, see [Starting Workflows When Nodes Change](/help/sites-administering/workflows-starting.md).)

1. On the instances that perform the background processing of DAM assets, disable the workflow launchers that execute the [!UICONTROL DAM Update Asset] workflow.
-->

## Lettura successiva {#further-reading}

Oltre ai dettagli presentati in questa pagina, potete anche leggere quanto segue:

* Per informazioni sull&#39;utilizzo delle API Java per creare posti di lavoro e consumatori di lavoro, vedere [Creazione e utilizzo di processi per lo scarico](/help/sites-developing/dev-offloading.md).
