---
title: Offload dei processi
description: Scopri come configurare e utilizzare le istanze AEM in una topologia per eseguire tipi specifici di elaborazione.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
feature: Configuring
exl-id: 429c96ff-4185-4215-97e8-9bd2c130a9b1
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '2317'
ht-degree: 1%

---

# Offload dei processi{#offloading-jobs}

## Introduzione {#introduction}

L&#39;offload distribuisce le attività di elaborazione tra le istanze di Experience Manager in una topologia. L&#39;offload consente di utilizzare istanze di Experience Manager specifiche per l&#39;esecuzione di tipi specifici di elaborazione. L&#39;elaborazione specializzata consente di ottimizzare l&#39;utilizzo delle risorse server disponibili.

L&#39;offload si basa sul [Apache Sling Discovery](https://sling.apache.org/documentation/bundles/discovery-api-and-impl.html) e Sling Job Manager. Per utilizzare l&#39;offload, è possibile aggiungere cluster di Experienci Manager a una topologia e identificare gli argomenti dei processi elaborati dal cluster. I cluster sono composti da una o più istanze di Experience Manager, in modo che una singola istanza venga considerata un cluster.

Per informazioni sull&#39;aggiunta di istanze a una topologia, vedere [Amministrazione delle topologie](/help/sites-deploying/offloading.md#administering-topologies).

### Distribuzione dei processi {#job-distribution}

Sling JobManager e JobConsumer consentono la creazione di processi elaborati in una topologia:

* JobManager: servizio che crea processi per argomenti specifici.
* JobConsumer: servizio che esegue processi di uno o più argomenti. È possibile registrare più servizi JobConsumer per lo stesso argomento.

Quando JobManager crea un processo, il framework Offload seleziona un cluster di Experienci Manager nella topologia per eseguire il processo:

* Il cluster deve includere una o più istanze che eseguono un JobConsumer registrato per l&#39;argomento del processo.
* L&#39;argomento deve essere abilitato per almeno un&#39;istanza nel cluster.

Consulta [Configurazione del consumo di argomenti](/help/sites-deploying/offloading.md#configuring-topic-consumption) per informazioni sull&#39;ottimizzazione della distribuzione dei processi.

![chlimage_1-109](assets/chlimage_1-109.png)

Quando il framework di offload seleziona un cluster per eseguire un processo e il cluster è composto da più istanze, la Distribuzione Sling determina quale istanza nel cluster esegue il processo.

### Payload processo {#job-payloads}

Il framework Offload supporta i payload dei job che associano i job alle risorse del repository. I payload dei processi sono utili quando vengono creati processi per l&#39;elaborazione delle risorse e il processo viene scaricato in un altro computer.

Al momento della creazione di un processo, il payload si trova solo sull’istanza che lo crea. Quando si esegue l’offload del processo, gli agenti di replica garantiscono che il payload venga creato sull’istanza che alla fine lo utilizza. Al termine dell’esecuzione del processo, la replica inversa fa sì che il payload venga copiato nuovamente nell’istanza che ha creato il processo.

## Amministrazione delle topologie {#administering-topologies}

Le topologie sono cluster di Experienci Manager liberamente accoppiati che partecipano all&#39;offload. Un cluster è costituito da una o più istanze del server di Experience Manager (una singola istanza viene considerata un cluster).

Ogni istanza di Experience Manager esegue i seguenti servizi relativi all&#39;offload:

* Servizio di individuazione: invia le richieste a un connettore di topologia per la connessione alla topologia.
* Connettore topologia: riceve le richieste di unione e accetta o rifiuta ciascuna richiesta.

Il servizio di individuazione di tutti i membri della topologia punta al connettore topologia su uno dei membri. Nelle sezioni successive, questo membro viene definito membro radice.

![chlimage_1-110](assets/chlimage_1-110.png)

Ogni cluster nella topologia contiene un&#39;istanza riconosciuta come leader. La coordinata del cluster interagisce con la topologia per conto degli altri membri del cluster. Quando la linea guida lascia il cluster, viene automaticamente scelta una nuova linea guida per il cluster.

### Visualizzazione della topologia {#viewing-the-topology}

Utilizzare il browser Topologia per esplorare lo stato della topologia a cui appartiene l&#39;istanza Experience Manager. Visualizzatore topologia mostra i cluster e le istanze della topologia.

Per ogni cluster viene visualizzato un elenco di membri del cluster che indica l&#39;ordine in cui ogni membro è stato aggiunto al cluster e quale membro è il responsabile. La proprietà Current indica l&#39;istanza che si sta amministrando.

Per ogni istanza del cluster, è possibile visualizzare diverse proprietà relative alla topologia:

* Elenco consentiti di argomenti per l’utente del processo dell’istanza.
* Endpoint esposti per la connessione alla topologia.
* Argomenti del processo per i quali l&#39;istanza è registrata per l&#39;offload.
* Gli argomenti del processo elaborati dall’istanza.

1. Utilizzando l’interfaccia utente touch, fai clic sulla scheda Strumenti. ([http://localhost:4502/tools.html](http://localhost:4502/tools.html))
1. Nell&#39;area Operazioni Granite fare clic su Offload browser.
1. Nel pannello di navigazione, fate clic su Browser topologia.

   Vengono visualizzati i cluster che partecipano alla topologia.

   ![chlimage_1-111](assets/chlimage_1-111.png)

1. Fare clic su un cluster per visualizzare un elenco delle istanze nel cluster e il relativo ID, stato corrente e stato guida.
1. Fai clic su un ID istanza per visualizzare proprietà più dettagliate.

È inoltre possibile utilizzare la console Web per visualizzare informazioni sulla topologia. La console fornisce ulteriori informazioni sui cluster di topologia:

* Quale istanza è l’istanza locale.
* I servizi Connettore topologia utilizzati da questa istanza per connettersi alla topologia (in uscita) e i servizi che si connettono a questa istanza (in ingresso).
* Cronologia delle modifiche per la topologia e le proprietà dell&#39;istanza.

Per aprire la pagina Gestione topologia della console Web, attenersi alla procedura descritta di seguito.

1. Apri la console Web nel browser. ([http://localhost:4502/system/console](http://localhost:4502/system/console))
1. Fai clic su Principale > Gestione topologia.

   ![chlimage_1-112](assets/chlimage_1-112.png)

### Configurazione dell&#39;appartenenza alla topologia {#configuring-topology-membership}

Apache Sling Resource-Based Discovery Service viene eseguito su ogni istanza per controllare il modo in cui le istanze Experience Manager interagiscono con una topologia.

Il servizio Discovery invia richieste POST periodiche (heartbeat) ai servizi del connettore topologia per stabilire e mantenere connessioni con la topologia. Il servizio Connettore topologia gestisce un elenco consentiti di indirizzi IP o nomi host che possono essere aggiunti alla topologia:

* Per unire un&#39;istanza a una topologia, specificare l&#39;URL del servizio Connettore topologia del membro radice.
* Per consentire a un&#39;istanza di unirsi a una topologia, aggiungere l&#39;istanza all&#39;elenco consentiti del servizio Connettore topologia del membro radice.

Utilizza la console web o un nodo sling:OsgiConfig per configurare le seguenti proprietà del servizio org.apache.sling.discovery.impt.Config:

<table>
 <tbody>
  <tr>
   <th>Nome proprietà</th>
   <th>Nome OSGi</th>
   <th>Descrizione</th>
   <th>Valore predefinito</th>
  </tr>
  <tr>
   <td>Timeout heartbeat (secondi)</td>
   <td>heartbeatTimeout</td>
   <td>Il tempo di attesa in secondi di una risposta heartbeat prima che l’istanza di destinazione sia considerata non disponibile. </td>
   <td>20</td>
  </tr>
  <tr>
   <td>Intervallo heartbeat (secondi)</td>
   <td>heartbeatInterval</td>
   <td>La quantità di tempo in secondi tra gli heartbeat.</td>
   <td>15</td>
  </tr>
  <tr>
   <td>Ritardo evento minimo (secondi)</td>
   <td>minEventDelay</td>
   <td><p>Quando si verifica una modifica alla topologia, il tempo necessario per ritardare la modifica dello stato da TOPOLOGY_CHANGING a TOPOLOGY_CHANGED. Ogni modifica che si verifica quando lo stato è TOPOLOGY_CHANGING aumenta il ritardo di questo periodo di tempo.</p> <p>Questo ritardo impedisce agli ascoltatori di essere inondati da eventi. </p> <p>Per non utilizzare alcun ritardo, specificare 0 o un numero negativo.</p> </td>
   <td>3</td>
  </tr>
  <tr>
   <td>URL del connettore topologia</td>
   <td>topologyConnectorUrls</td>
   <td>Gli URL dei servizi Connettore topologia per l’invio di messaggi heartbeat.</td>
   <td>http://localhost:4502/libs/sling/topology/connector</td>
  </tr>
  <tr>
   <td>Elenco consentiti connettore topologia</td>
   <td>topologyConnectorWhitelist</td>
   <td>Elenco di indirizzi IP o nomi host consentiti dal servizio Connettore topologia locale nella topologia. </td>
   <td><p>localhost</p> <p>127.0.0.1</p> </td>
  </tr>
  <tr>
   <td>Nome descrittore archivio</td>
   <td>leaderElectionRepositoryDescriptor</td>
   <td> </td>
   <td>&lt;no value&gt;</td>
  </tr>
 </tbody>
</table>

Per connettere un&#39;istanza CQ al membro radice di una topologia, attenersi alla procedura descritta di seguito. La procedura punta l&#39;istanza all&#39;URL del connettore topologia del membro della topologia radice. Eseguire questa procedura su tutti i membri della topologia.

1. Apri la console Web nel browser. ([http://localhost:4502/system/console](http://localhost:4502/system/console))
1. Fai clic su Principale > Gestione topologia.
1. Fare clic su Configura servizio di individuazione.
1. Aggiungere un elemento alla proprietà URL del connettore topologia e specificare l&#39;URL del servizio Connettore topologia del membro radice. L’URL è nel formato https://rootservername:4502/libs/sling/topology/connector.

Eseguire la procedura seguente sul membro radice della topologia. La procedura aggiunge i nomi degli altri membri della topologia al relativo elenco consentiti del servizio di individuazione.

1. Apri la console Web nel browser. ([http://localhost:4502/system/console](http://localhost:4502/system/console))
1. Fai clic su Principale > Gestione topologia.
1. Fare clic su Configura servizio di individuazione.
1. Per ogni membro della topologia, aggiungere un elemento alla proprietà di elenco consentiti Connettore topologia e specificare il nome host o l&#39;indirizzo IP del membro della topologia.

## Configurazione del consumo di argomenti {#configuring-topic-consumption}

Utilizzare il browser Offload per configurare l&#39;utilizzo degli argomenti per le istanze di Experience Manager nella topologia. Per ogni istanza, puoi specificare gli argomenti utilizzati. Ad esempio, per configurare la topologia in modo che una sola istanza utilizzi argomenti di un tipo specifico, disattivare l&#39;argomento su tutte le istanze tranne una.

I job vengono distribuiti tra le istanze che hanno l&#39;argomento associato abilitato utilizzando la logica round robin.

1. Utilizzando l’interfaccia utente touch, fai clic sulla scheda Strumenti. ([http://localhost:4502/tools.html](http://localhost:4502/tools.html))
1. Nell&#39;area Operazioni Granite fare clic su Offload browser.
1. Nel pannello di navigazione, fate clic su Offload browser (Offload Browser).

   Vengono visualizzati gli argomenti di scaricamento e le istanze del server che possono utilizzarli.

   ![chlimage_1-113](assets/chlimage_1-113.png)

1. Per disattivare l&#39;utilizzo di un argomento per un&#39;istanza, sotto il nome dell&#39;argomento fare clic su Disattiva accanto all&#39;istanza.
1. Per configurare l’utilizzo di tutti gli argomenti per un’istanza, fai clic sull’identificatore dell’istanza sotto qualsiasi argomento.

   ![chlimage_1-114](assets/chlimage_1-114.png)

1. Fare clic su uno dei seguenti pulsanti accanto a un argomento per configurare il comportamento di consumo per l&#39;istanza, quindi fare clic su Salva:

   * Abilitata: questa istanza utilizza i processi di questo argomento.
   * Disabilitata: questa istanza non utilizza processi di questo argomento.
   * Esclusivo: questa istanza utilizza solo processi di questo argomento.

   **Nota:** Quando si seleziona Esclusivo per un argomento, tutti gli altri argomenti vengono automaticamente impostati su Disabilitato.

### Consumatori processi installati {#installed-job-consumers}

Con Experience Manager vengono installate diverse implementazioni di JobConsumer. Gli argomenti per i quali sono registrati questi JobConsumers vengono visualizzati nel browser Offload. Ulteriori argomenti visualizzati sono quelli registrati da JobConsumers personalizzati. Nella tabella seguente vengono descritti i valori predefiniti di JobConsumers.

| Argomento lavoro | Servizio PID | Descrizione |
|---|---|---|
| / | org.apache.sling.event.impl.jobs.deprecated.EventAdminBridge | Installato con Apache Sling. Elabora i processi generati dall’amministratore degli eventi OSGi per garantire la compatibilità con le versioni precedenti. |
| com/day/cq/replication/job/&amp;ast; | com.day.cq.replication.impl.AgentManagerImpl | Agente di replica che replica i payload dei processi. |

<!--
| com/adobe/granite/workflow/offloading |com.adobe.granite.workflow.core.offloading.WorkflowOffloadingJobConsumer |Processes jobs that the DAM Update Asset Offloader workflow generates. |
-->

### Disabilitazione e abilitazione di argomenti per un’istanza {#disabling-and-enabling-topics-for-an-instance}

Il servizio Apache Sling Job Consumer Manager fornisce proprietà di elenco consentiti e elenco Bloccati per argomenti. Configura queste proprietà per abilitare o disabilitare l&#39;elaborazione di argomenti specifici in un&#39;istanza di Experience Manager.

**Nota:** Se l&#39;istanza appartiene a una topologia, è inoltre possibile utilizzare Offload Browser in qualsiasi computer della topologia per attivare o disattivare gli argomenti.

La logica che crea l&#39;elenco degli argomenti abilitati consente innanzitutto tutti gli argomenti presenti nell&#39;elenco consentiti e quindi rimuove gli argomenti presenti nell&#39;elenco Bloccati. Per impostazione predefinita, tutti gli argomenti sono abilitati (il valore di elenco consentiti è `*`) e nessun argomento è disabilitato (l&#39;elenco Bloccati non ha valore).

Utilizza la console web o un `sling:OsgiConfig` per configurare le seguenti proprietà. Per `sling:OsgiConfig` PID del servizio Job Consumer Manager: org.apache.sling.event.impl.jobs.JobConsumerManager.

| Nome proprietà nella console web | ID OSGi | Descrizione |
|---|---|---|
| Elenco consentiti argomento | job.consumermanager.whitelist | Elenco di argomenti elaborati dal servizio JobManager locale. Con il valore predefinito &amp;ast; tutti gli argomenti vengono inviati al servizio TopicConsumer registrato. |
| Elenco Bloccati argomento | job.consumermanager.blacklist | Elenco di argomenti non elaborati dal servizio JobManager locale. |

## Creazione Di Agenti Di Replica Per L&#39;Offload {#creating-replication-agents-for-offloading}

Il framework di offload utilizza la replica per trasportare le risorse tra l&#39;istanza di authoring e quella di lavoro. Il framework di offload crea automaticamente agenti di replica quando le istanze si uniscono alla topologia. Gli agenti vengono creati con valori predefiniti. Modificare manualmente la password utilizzata dagli agenti per l&#39;autenticazione.

>[!CAUTION]
>
>Un problema noto con gli agenti di replica generati automaticamente richiede la creazione manuale di nuovi agenti di replica.

Creare gli agenti di replica che trasportano i payload dei processi tra le istanze per l&#39;offload. La figura seguente mostra gli agenti necessari per eseguire l&#39;offload dall&#39;istanza di authoring a un&#39;istanza di lavoro. L’autore ha un ID Sling pari a 1 e l’istanza di lavoro ha un ID Sling pari a 2:

![chlimage_1-115](assets/chlimage_1-115.png)

Questa configurazione richiede i tre agenti seguenti:

1. Agente in uscita sull&#39;istanza di authoring che esegue la replica nell&#39;istanza di lavoro.
1. Agente inverso sull’istanza di authoring che richiama dalla casella in uscita sull’istanza di lavoro.
1. Un agente di posta in uscita sull’istanza di lavoro.

Questo schema di replica è simile a quello utilizzato tra le istanze di authoring e di pubblicazione. Tuttavia, per la situazione di scaricamento, tutte le istanze coinvolte sono istanze di authoring.

>[!NOTE]
>
>Il framework di offload utilizza la topologia per ottenere gli indirizzi IP delle istanze di offload. Il framework crea quindi automaticamente gli agenti di replica in base a questi indirizzi IP. Se gli indirizzi IP delle istanze di offload cambiano successivamente, la modifica viene propagata automaticamente sulla topologia dopo il riavvio dell&#39;istanza. Tuttavia, il framework di offload non aggiorna automaticamente gli agenti di replica in modo che riflettano i nuovi indirizzi IP. Per evitare questa situazione, utilizzare indirizzi IP fissi per tutte le istanze nella topologia.

### Denominazione degli agenti di replica per l&#39;offload {#naming-the-replication-agents-for-offloading}

Utilizza un formato specifico per ***Nome*** degli agenti di replica in modo che il framework di offload utilizzi automaticamente l&#39;agente corretto per istanze di lavoro specifiche.

**Denominazione dell’agente in uscita nell’istanza di authoring:**

`offloading_<slingid>`, dove `<slingid>` è l’ID Sling dell’istanza di lavoro.

Esempio: `offloading_f5c8494a-4220-49b8-b079-360a72f71559`

**Denominazione dell’agente inverso nell’istanza di authoring:**

`offloading_reverse_<slingid>`, dove `<slingid>` è l’ID Sling dell’istanza di lavoro.

Esempio: `offloading_reverse_f5c8494a-4220-49b8-b079-360a72f71559`

**Denominazione della casella in uscita nell’istanza di lavoro:**

`offloading_outbox`

### Creazione dell&#39;agente in uscita {#creating-the-outgoing-agent}

1. Creare un **Agente di replica** sull&#39;autore. (consultare la [documentazione per gli agenti di replica](/help/sites-deploying/replication.md)). Specifica qualsiasi **Titolo**. Il **Nome** deve seguire la convenzione di denominazione.
1. Crea l’agente utilizzando le seguenti proprietà:

   | Proprietà | Valore |
   |---|---|
   | Impostazioni > Tipo di serializzazione | Predefiniti |
   | Trasporto >URI trasporto | https://*`<ip of target instance>`*:*`<port>`*`/bin/receive?sling:authRequestLogin=1` |
   | Trasporto >Utente trasporto | Utente di replica sull’istanza di destinazione |
   | Trasporto >Password trasporto | Password utente di replica nell’istanza di destinazione |
   | Esteso > Metodo HTTP | POST |
   | Triggers > Ignora predefinito | True |

### Creazione dell’agente inverso {#creating-the-reverse-agent}

1. Creare un **Agente replica inversa** sull&#39;autore. (consultare la [documentazione per gli agenti di replica](/help/sites-deploying/replication.md).) Specifica qualsiasi **Titolo**. Il **Nome** deve seguire la convenzione di denominazione.
1. Crea l’agente utilizzando le seguenti proprietà:

   | Proprietà | Valore |
   |---|---|
   | Impostazioni > Tipo di serializzazione | Predefiniti |
   | Trasporto >URI trasporto | https://*`<ip of target instance>`*:*`<port>`*`/bin/receive?sling:authRequestLogin=1` |
   | Trasporto >Utente trasporto | Utente di replica sull’istanza di destinazione |
   | Trasporto >Password trasporto | Password utente di replica nell’istanza di destinazione |
   | Esteso > Metodo HTTP | GET |

### Creazione dell’agente di posta in uscita {#creating-the-outbox-agent}

1. Creare un **Agente di replica** sull&#39;istanza del lavoratore. (consultare la [documentazione per gli agenti di replica](/help/sites-deploying/replication.md).) Specifica qualsiasi **Titolo**. Il **Nome** deve essere `offloading_outbox`.
1. Crea l’agente utilizzando le seguenti proprietà.

   | Proprietà | Valore |
   |---|---|
   | Impostazioni > Tipo di serializzazione | Predefiniti |
   | Trasporto >URI trasporto | repo://var/replication/outbox |
   | Trigger > Ignora predefinito | True |

### Ricerca dell’ID Sling {#finding-the-sling-id}

Ottieni l’ID Sling di un’istanza Experience Manager utilizzando uno dei seguenti metodi:

* Apri la console web e, nelle Impostazioni Sling, individua il valore della proprietà Sling ID ([http://localhost:4502/system/console/status-slingsettings](http://localhost:4502/system/console/status-slingsettings)). Questo metodo è utile se l&#39;istanza non fa ancora parte della topologia.
* Utilizzare il browser Topologia se l&#39;istanza fa già parte della topologia.

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

## Ulteriori informazioni {#further-reading}

Oltre ai dettagli presentati in questa pagina, puoi leggere quanto segue:

* Per informazioni sull’utilizzo delle API Java per creare processi e consumer di processi, consulta [Creazione e utilizzo di processi per l&#39;offload](/help/sites-developing/dev-offloading.md).
