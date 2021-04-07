---
title: Dashboard operazioni
seo-title: Dashboard operazioni
description: Scopri come utilizzare il dashboard delle operazioni.
seo-description: Scopri come utilizzare il dashboard delle operazioni.
uuid: ef24813f-a7a8-4b26-a496-6f2a0d9efef6
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: b210f5d7-1d68-49ee-ade7-667c6ab11d2b
docset: aem65
exl-id: f9a88156-91a2-4c85-9bc9-8f23700c2cbd
feature: Operazioni
translation-type: tm+mt
source-git-commit: 9134130f349c6c7a06ad9658a87f78a86b7dbf9c
workflow-type: tm+mt
source-wordcount: '6199'
ht-degree: 2%

---

# Dashboard operazioni {#operations-dashboard}

## Introduzione {#introduction}

Il dashboard delle operazioni nel AEM 6 aiuta gli operatori di sistema a monitorare AEM lo stato del sistema a colpo d&#39;occhio. Fornisce inoltre informazioni di diagnosi generate automaticamente sugli aspetti rilevanti della AEM e consente di configurare ed eseguire l&#39;automazione della manutenzione autonoma per ridurre in modo significativo le operazioni di progetto e i casi di supporto. Il dashboard delle operazioni può essere esteso con controlli di integrità personalizzati e attività di manutenzione. Inoltre, i dati del dashboard delle operazioni sono accessibili da strumenti di monitoraggio esterni tramite JMX.

**Dashboard delle operazioni:**

* È uno stato di sistema con un solo clic per aiutare i reparti operativi a ottenere efficienza
* Offre una panoramica dello stato di salute del sistema in un&#39;unica posizione centralizzata
* Riduzione del tempo necessario per trovare, analizzare e risolvere i problemi
* Offre automazione autonoma che consente di ridurre in modo significativo i costi delle operazioni di progetto

È possibile accedervi andando su **Strumenti** - **Operazioni** dalla schermata di benvenuto AEM.

>[!NOTE]
>
>Per poter accedere al Dashboard delle operazioni, l&#39;utente connesso deve far parte del gruppo di utenti &quot;Operatori&quot;. Per ulteriori informazioni, consulta la documentazione su [Amministrazione di utenti, gruppi e diritti di accesso](/help/sites-administering/user-group-ac-admin.md).

## Rapporti stato {#health-reports}

Il sistema di rapporto sullo stato di salute fornisce informazioni sullo stato di un&#39;istanza AEM tramite Sling Health Checks. Questo può essere fatto tramite OSGI, JMX, richieste HTTP (tramite JSON) o tramite l&#39;interfaccia utente touch. Offre misurazioni e soglia di determinati contatori configurabili e, in alcuni casi, offrirà informazioni su come risolvere il problema.

Presenta diverse funzioni, descritte di seguito.

## Verifiche stato {#health-checks}

Le **relazioni sulla salute** sono un sistema di carte che indicano una buona o cattiva salute per quanto riguarda una specifica area di prodotto. Queste schede sono visualizzazioni degli Sling Health Checks, che aggregano i dati da JMX e altre fonti ed espongono di nuovo le informazioni elaborate come MBeans. Questi MBeans possono anche essere ispezionati nella [console web JMX](/help/sites-administering/jmx-console.md), nel dominio **org.apache.sling.health.check** .

L&#39;interfaccia dei rapporti sullo stato è accessibile tramite il menu **Strumenti** - **Operazioni** - **Rapporti sullo stato** nella schermata di benvenuto AEM o direttamente tramite il seguente URL:

`https://<serveraddress>:port/libs/granite/operations/content/healthreports/healthreportlist.html`

![chlimage_1-116](assets/chlimage_1-116.png)

Il sistema di carte espone tre possibili stati: **OK**, **WARN** e **CRITICO**. Gli stati sono il risultato di regole e soglie, che possono essere configurate passando il mouse sulla scheda e facendo clic sull&#39;icona a forma di ingranaggio nella barra delle azioni:

![chlimage_1-117](assets/chlimage_1-117.png)

### Tipi di controllo integrità {#health-check-types}

Nella AEM 6 esistono due tipi di controlli sanitari:

1. Controlli di integrità individuali
1. Controlli di integrità compositi

Un **controllo integrità individuale** è un singolo controllo dello stato che corrisponde a una scheda di stato. I controlli di integrità individuali possono essere configurati con regole o soglie e possono fornire uno o più suggerimenti e collegamenti per risolvere problemi di salute identificati. Prendiamo il controllo &quot;Log Errors&quot; come esempio: se ci sono voci ERROR nei log di istanza, le troverai nella pagina dei dettagli del controllo di integrità. Nella parte superiore della pagina viene visualizzato un collegamento all’analizzatore &quot;Log Message&quot; nella sezione Strumenti di diagnosi, che consente di analizzare questi errori in modo più dettagliato e riconfigurare i logger.

Una **Verifica dello stato composito** è un controllo che aggrega le informazioni provenienti da diversi controlli individuali.

I controlli di integrità compositi sono configurati con l&#39;ausilio di **tag filtro**. In sostanza, tutti i controlli singoli con lo stesso tag di filtro verranno raggruppati come un controllo di integrità composito. Un controllo di integrità composito avrà uno stato OK solo se tutti i controlli singoli che aggrega hanno anche lo stato OK.

### Come creare controlli di integrità {#how-to-create-health-checks}

Nel Dashboard delle operazioni è possibile visualizzare il risultato dei controlli di integrità individuali e compositi.

### Creazione di un singolo controllo dello stato {#creating-an-individual-health-check}

La creazione di un singolo controllo integrità prevede due passaggi: implementazione di un controllo dello stato di Sling e aggiunta di una voce per il controllo dello stato nei nodi di configurazione del dashboard.

1. Per creare un Sling Health Check, è necessario creare un componente OSGI che implementa l&#39;interfaccia Sling HealthCheck. Questo componente verrà aggiunto all’interno di un bundle. Le proprietà del componente identificano completamente il controllo dello stato. Una volta installato il componente, verrà automaticamente creato un MBean JMX per il controllo dello stato. Per ulteriori informazioni, consulta la [Documentazione Sling Health Check](https://sling.apache.org/documentation/bundles/sling-health-check-tool.html) .

   Esempio di un componente Sling Health Check, scritto con annotazioni del componente del servizio OSGI:

   ```java
   @Component(service = HealthCheck.class,
   property = {
       HealthCheck.NAME + "=Example Check",
       HealthCheck.TAGS + "=example",
       HealthCheck.TAGS + "=test",
       HealthCheck.MBEAN_NAME + "=exampleHealthCheckMBean"
   })
    public class ExampleHealthCheck implements HealthCheck {
       @Override
       public Result execute() {
           // health check code
       }
    }
   ```

   >[!NOTE]
   >
   >La proprietà `MBEAN_NAME` definisce il nome del mbean che verrà generato per questo controllo di integrità.

1. Dopo aver creato un controllo dello stato, è necessario creare un nuovo nodo di configurazione, per renderlo accessibile nell&#39;interfaccia del dashboard delle operazioni. Per questo passaggio, è necessario conoscere il nome JMX Mbean del controllo di integrità (la proprietà `MBEAN_NAME`). Per creare una configurazione per il controllo dello stato, apri CRXDE e aggiungi un nuovo nodo (di tipo **nt:unstructured**) nel seguente percorso: `/apps/settings/granite/operations/hc`

   Le seguenti proprietà devono essere impostate sul nuovo nodo:

   * **Nome:** `sling:resourceType`

      * **Tipo:** `String`
      * **Valore:** `granite/operations/components/mbean`
   * **Nome:** `resource`

      * **Tipo:** `String`
      * **Valore:** `/system/sling/monitoring/mbeans/org/apache/sling/healthcheck/HealthCheck/exampleHealthCheck`

   >[!NOTE]
   >
   >Il percorso della risorsa di cui sopra viene creato come segue: se il nome del fagiolo del controllo di integrità è &quot;test&quot;, aggiungi &quot;test&quot; alla fine del percorso `/system/sling/monitoring/mbeans/org/apache/sling/healthcheck/HealthCheck`
   >
   >Quindi il percorso finale sarà:
   >
   >`/system/sling/monitoring/mbeans/org/apache/sling/healthcheck/HealthCheck/test`

   >[!NOTE]
   >
   >Assicurati che le seguenti proprietà del percorso `/apps/settings/granite/operations/hc` siano impostate su true:
   >
   >
   >`sling:configCollectionInherit`
   >
   >`sling:configPropertyInherit`
   >
   >
   >Questo dirà al gestore di configurazione di unire le nuove configurazioni con quelle esistenti da `/libs`.

### Creazione di un controllo dello stato composito {#creating-a-composite-health-check}

Il ruolo di un controllo dello stato composito consiste nell&#39;aggregare un certo numero di controlli di integrità individuali che condividono un insieme di funzioni comuni. Ad esempio, il Security Composite Health Check raggruppa tutti i singoli controlli di integrità che eseguono verifiche relative alla sicurezza. Il primo passo per creare un controllo composito è quello di aggiungere una nuova configurazione OSGI. Affinché possa essere visualizzato nel Dashboard delle operazioni, è necessario aggiungere un nuovo nodo di configurazione, come abbiamo fatto per un semplice controllo.

1. Vai a Web Configuration Manager nella console OSGI. Per farlo, accedi a `https://serveraddress:port/system/console/configMgr`
1. Cerca la voce denominata **Verifica dello stato composito di Apache Sling**. Una volta trovato, noterai che sono già disponibili due configurazioni: uno per i controlli di sistema e un altro per i controlli di sicurezza.
1. Crea una nuova configurazione premendo il pulsante &quot;+&quot; sul lato destro della configurazione. Viene visualizzata una nuova finestra, come illustrato di seguito:

   ![chlimage_1-23](assets/chlimage_1-23.jpeg)

1. Crea una configurazione e salvala. Verrà creato un Mbean con la nuova configurazione.

   Lo scopo di ciascuna proprietà di configurazione è il seguente:

   * **Nome (hc.name):** il nome del controllo di integrità composito. Si consiglia di assegnare un nome significativo.
   * **Tag (hc.tags):** i tag per questo controllo di integrità. Se questo controllo di integrità composito è destinato a far parte di un altro controllo di integrità composito (ad esempio in una gerarchia di controlli di integrità), aggiungere i tag a cui questo composito è correlato.
   * **Nome MBean (hc.mbean.name):** il nome del Mbean che verrà dato al MBean JMX di questo controllo di integrità composito.
   * **Tag filtro (filter.tags):** si tratta di una proprietà specifica dei controlli di integrità compositi. Questi sono i tag che il composito deve aggregare. Il controllo di integrità composito si aggrega sotto il suo gruppo tutti i controlli di integrità che hanno qualsiasi tag corrispondente a uno dei tag di filtro di questo composito. Ad esempio, un controllo di integrità composito con i tag filtro **test** e **check** aggregherà tutti i controlli di integrità individuali e compositi che hanno uno dei tag **test** e **check** nella relativa proprietà tag ( `hc.tags`).

   >[!NOTE]
   >
   >Viene creato un nuovo Mbean JMX per ogni nuova configurazione di Apache Sling Composite Health Check.**

1. Infine, è necessario aggiungere la voce del controllo di integrità composito appena creato nei nodi di configurazione del dashboard delle operazioni. La procedura è la stessa dei controlli sanitari individuali: è necessario creare un nodo di tipo **nt:unstructured** in `/apps/settings/granite/operations/hc`. La proprietà della risorsa del nodo sarà definita dal valore di **hc.media.name** nella configurazione OSGI.

   Se, ad esempio, hai creato una configurazione e impostato il valore **hc.mbean.name** su **diskusage**, i nodi di configurazione avranno questo aspetto:

   * **Nome:** `Composite Health Check`

      * **Tipo:** `nt:unstructured`

   Con le seguenti proprietà:

   * **Nome:** `sling:resourceType`

      * **Tipo:** `String`
      * **Valore:** `granite/operations/components/mbean`
   * **Nome:** `resource`

      * **Tipo:** `String`
      * **Valore:** `/system/sling/monitoring/mbeans/org/apache/sling/healthcheck/HealthCheck/diskusage`

   >[!NOTE]
   >
   >Se crei controlli di integrità individuali che logicamente appartengono a un controllo composito già presente nel dashboard per impostazione predefinita, questi verranno acquisiti automaticamente e raggruppati sotto il rispettivo controllo composito. Per questo motivo, non è necessario creare un nuovo nodo di configurazione per questi controlli.
   >
   >Ad esempio, se crei un singolo controllo di integrità della sicurezza, tutto ciò che devi fare è assegnargli il tag &quot;**security**&quot; e viene installato, apparirà automaticamente sotto il controllo composito Controlli di sicurezza nel dashboard delle operazioni.

### Controlli di integrità forniti con AEM {#health-checks-provided-with-aem}

<table>
 <tbody>
  <tr>
   <td><strong>Nome zHealthcheck</strong></td>
   <td><strong>Descrizione</strong></td>
  </tr>
  <tr>
   <td>Prestazioni delle query</td>
   <td><p>Questo controllo dello stato di salute è stato semplificato <strong>in AEM 6.4</strong> e ora controlla l'attributo <code>Oak QueryStats</code> MBean, refactored di recente, in particolare l'attributo <code>SlowQueries </code>. Se le statistiche contengono query lente, il controllo di integrità restituisce un avviso. In caso contrario, restituisce lo stato OK.<br /> </p> <p>L'MBean per questo controllo di integrità è <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DqueriesStatus%2Ctype%3DHealthCheck">org.apache.sling.health.check:name=queryStatus,type=HealthCheck</a>.</p> </td>
  </tr>
  <tr>
   <td>Lunghezza coda di osservazione</td>
   <td><p>La lunghezza della coda di osservazione esegue un iterazione su tutti gli ascoltatori di eventi e gli osservatori di background, confronta i loro <code>queueSize </code>con i loro <code>maxQueueSize</code> e:</p>
    <ul>
     <li>restituisce lo stato Critico se il valore <code>queueSize</code> supera il valore <code>maxQueueSize</code> (ovvero quando gli eventi vengono eliminati)</li>
     <li>restituisce Avvisa se il valore <code>queueSize</code> è superiore a <code>maxQueueSize * WARN_THRESHOLD</code> (il valore predefinito è 0,75) </li>
    </ul> <p>La lunghezza massima di ogni coda proviene da configurazioni separate (Oak e AEM) e non è configurabile da questo controllo di integrità. L'MBean per questo controllo di integrità è <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DObservationQueueLengthHealthCheck%2Ctype%3DHealthCheck">org.apache.sling.health.check:name=ObservationQueueLengthHealthCheck,type=HealthCheck</a>.</p> </td>
  </tr>
  <tr>
   <td>Limiti di attraversamento per query</td>
   <td><p>I limiti di attraversamento delle query controllano i MBean <code>QueryEngineSettings</code>, in particolare gli attributi <code>LimitInMemory</code> e <code>LimitReads</code>, e restituisce il seguente stato:</p>
    <ul>
     <li>restituisce lo stato Avvisa se uno dei limiti è uguale o superiore al valore <code>Integer.MAX_VALUE</code></li>
     <li>restituisce lo stato Avvisa se uno dei limiti è inferiore a 10000 (l'impostazione consigliata da Oak)</li>
     <li>restituisce lo stato Critico se non è possibile recuperare il valore <code>QueryEngineSettings</code> o uno dei limiti</li>
    </ul> <p>Il Mbean per questo controllo di integrità è <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DqueryTraversalLimitsBundle%2Ctype%3DHealthCheck">org.apache.sling.health.check:name=queryTraversalLimitsBundle,type=HealthCheck</a>.</p> </td>
  </tr>
  <tr>
   <td>Orologi sincronizzati</td>
   <td><p>Questo controllo è pertinente solo per i cluster <a href="https://github.com/apache/sling-old-svn-mirror/blob/4df9ab2d6592422889c71fa13afd453a10a5a626/bundles/extensions/discovery/oak/src/main/java/org/apache/sling/discovery/oak/SynchronizedClocksHealthCheck.java">document nodestore</a>. Restituisce il seguente stato:</p>
    <ul>
     <li>restituisce lo stato Avvisa quando gli orologi dell’istanza non vengono sincronizzati e superano una soglia minima predefinita</li>
     <li>restituisce lo stato Critico quando gli orologi dell’istanza non vengono sincronizzati e superano una soglia elevata predefinita</li>
    </ul> <p>Il Mbean per questo controllo di integrità è <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DslingDiscoveryOakSynchronizedClocks%2Ctype%3DHealthCheck">org.apache.sling.health.check:name=slingDiscoveryOakSynchronizedClocks,type=HealthCheck</a>.</p> </td>
  </tr>
  <tr>
   <td>Indici asincroni</td>
   <td><p>Controllo degli indici asincroni:</p>
    <ul>
     <li>restituisce lo stato critico se almeno una corsia di indicizzazione non riesce</li>
     <li>controlla la <code>lastIndexedTime</code> per tutte le corsie di indicizzazione e:
      <ul>
       <li>restituisce lo stato Critico se è più di 2 ore fa </li>
       <li>restituisce lo stato di avviso se è compreso tra 2 ore e 45 minuti fa </li>
       <li>restituisce lo stato OK se è meno di 45 minuti fa </li>
      </ul> </li>
     <li>se nessuna di queste condizioni è soddisfatta, restituisce lo stato OK</li>
    </ul> <p>Le soglie di stato Critico e Avvisa sono configurabili. Il Mbean per questo controllo di integrità è <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DasyncIndexHealthCheck%2Ctype%3DHealthCheck">org.apache.sling.health.check:name=asyncIndexHealthCheck,type=HealthCheck</a>.</p> <p><strong>Nota:  </strong>Questo controllo dello stato di salute è disponibile con AEM 6.4 ed è stato riportato al AEM 6.3.0.1.</p> </td>
  </tr>
  <tr>
   <td>Indici Lucene di grandi dimensioni</td>
   <td><p>Questo controllo utilizza i dati esposti da <code>Lucene Index Statistics</code> MBean per identificare indici di grandi dimensioni e restituisce:</p>
    <ul>
     <li>uno stato di avviso se esiste un indice con più di 1 miliardo di documenti</li>
     <li>uno stato critico se esiste un indice con più di 1,5 miliardi di documenti</li>
    </ul> <p>Le soglie sono configurabili e l'MBean per il controllo dello stato di salute è <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DlargeIndexHealthCheck%2Ctype%3DHealthCheck">org.apache.sling.health.check:name=largeIndexHealthCheck,type=HealthCheck.</a></p> <p><strong>Nota:  </strong>Questo controllo è disponibile con AEM 6.4 ed è stato riportato a AEM 6.3.2.0.</p> </td>
  </tr>
  <tr>
   <td>Manutenzione sistema</td>
   <td><p>La Manutenzione del sistema è un controllo composito che restituisce l'OK se tutte le attività di manutenzione sono in esecuzione come configurato. Tieni presente che:</p>
    <ul>
     <li>ogni operazione di manutenzione è accompagnata da un relativo controllo dello stato di salute</li>
     <li>se un'attività non viene aggiunta a una finestra di manutenzione, la relativa verifica dello stato restituirà Critico</li>
     <li>è necessario configurare le attività di manutenzione Audit Log e Workflow Purge o rimuoverle dalle finestre di manutenzione. Se non viene configurata, queste attività non avranno esito positivo al primo tentativo di esecuzione, pertanto il controllo di manutenzione del sistema restituirà lo stato Critico.</li>
     <li><strong>Con AEM 6.4</strong>, c'è anche un controllo per  <a href="/help/sites-administering/operations-dashboard.md#automated-maintenance-tasks">Lucene Binaries </a> Maintenancetask</li>
     <li>in AEM 6.2 e versioni precedenti, il controllo di manutenzione del sistema restituisce uno stato di avviso subito dopo l'avvio, in quanto le attività non vengono mai eseguite. A partire dalla versione 6.3, restituiranno OK se la prima finestra di manutenzione non è ancora stata raggiunta.</li>
    </ul> <p>L'MBean per questo controllo di integrità è <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3Dsystemchecks%2Ctype%3DHealthCheck">org.apache.sling.health.check:name=systemChecks,type=HealthCheck</a>.</p> </td>
  </tr>
  <tr>
   <td>Coda di replica</td>
   <td><p>Questo controllo esegue iterazioni sugli agenti di replica e controlla le loro code. Per l'elemento nella parte superiore della coda, il controllo controlla quante volte l'agente ha effettuato un nuovo tentativo di replica. Se l'agente ha effettuato un nuovo tentativo di replica oltre il valore del parametro <code>numberOfRetriesAllowed</code>, restituisce un avviso. Il parametro <code>numberOfRetriesAllowed</code> è configurabile. </p> <p>L'MBean per questo controllo di integrità è <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DreplicationQueue%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.health.check:name=replicationQueue,type=HealthCheck</a>.</p> </td>
  </tr>
  <tr>
   <td>Processi Sling</td>
   <td>
    <div>
      Sling Jobs controlla il numero di processi in coda nel JobManager, confrontandolo con il
     <code>maxNumQueueJobs</code> soglia e:
    </div>
    <ul>
     <li>restituisce Critico se sono presenti più <code>maxNumQueueJobs</code> rispetto alla coda</li>
     <li>restituisce Critico se sono presenti processi attivi di lunga durata con più di 1 ora</li>
     <li>restituisce Critico se sono presenti processi in coda e l'ultima ora di lavoro completata è maggiore di 1 ora</li>
    </ul> <p>È configurabile solo il numero massimo di processi in coda e il valore predefinito è 1000.</p> <p>La MBean per questo controllo di integrità è <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DslingJobs%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.health.check:name=slingJobs,type=HealthCheck</a>.</p> </td>
  </tr>
  <tr>
   <td>Prestazioni delle richieste</td>
   <td><p>Questo controllo esamina la <code>granite.request.metrics.timer</code> <a href="http://localhost:4502/system/console/slingmetrics" target="_blank">metrica Sling </a>e:</p>
    <ul>
     <li>restituisce Critico se il valore del 75° percentile supera la soglia critica (il valore predefinito è 500 millisecondi)</li>
     <li>restituisce Avvisa se il valore del 75° percentile supera la soglia di avviso (il valore predefinito è 200 millisecondi)</li>
    </ul> <p>L'MBean per questo controllo di integrità è<em> </em><a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DrequestsStatus%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.healthcheck:name=requestsStatus,type=HealthCheck</a>.</p> </td>
  </tr>
  <tr>
   <td>Errori registro</td>
   <td><p>Questo controllo restituisce lo stato Avvisa in caso di errori nel registro.</p> <p>L'MBean per questo controllo di integrità è <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DlogErrorHealthCheck%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.health.check:name=logErrorHealthCheck,type=HealthCheck</a>.</p> </td>
  </tr>
  <tr>
   <td>Spazio su disco</td>
   <td><p>Il controllo Spazio su disco esamina la <code>FileStoreStats</code> MBean, recupera le dimensioni del Node Store e la quantità di spazio su disco utilizzabile sulla partizione Node Store e:</p>
    <ul>
     <li>restituisce Avvisa se il rapporto spazio su disco utilizzabile con dimensione archivio è inferiore alla soglia di avviso (il valore predefinito è 10)</li>
     <li>restituisce Critico se il rapporto spazio su disco utilizzabile con dimensione archivio è inferiore alla soglia critica (il valore predefinito è 2)</li>
    </ul> <p>Entrambe le soglie sono configurabili. Il controllo funziona solo sulle istanze con un archivio segmenti.</p> <p>La MBean per questo controllo di integrità è <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DDiskSpaceHealthCheck%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.health.check:name=DiskSpaceHealthCheck,type=HealthCheck</a>.</p> </td>
  </tr>
  <tr>
   <td>Verifica stato modulo di pianificazione</td>
   <td><p>Questo controllo restituisce un avviso se l’istanza dispone di processi Quartz in esecuzione per più di 60 secondi. La soglia di durata accettabile è configurabile.</p> <p>La MBean per questo controllo di integrità è <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DslingCommonsSchedulerHealthCheck%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.health.check:name=slingCommonsSchedulerHealthCheck,type=HealthCheck</a><em>.</em></p> </td>
  </tr>
  <tr>
   <td>Verifiche di sicurezza</td>
   <td><p>Il controllo di sicurezza è un composito che aggrega i risultati di più controlli relativi alla sicurezza. Questi controlli di integrità individuali risolvono problemi diversi dalla lista di controllo della sicurezza disponibile nella pagina di documentazione <a href="/help/sites-administering/security-checklist.md">Lista di controllo della sicurezza .</a> Il controllo è utile come prova di fumo di sicurezza all'avvio dell'istanza. </p> <p>L'MBean per questo controllo di integrità è <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3Dsecuritychecks%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.health.check:name=securityChecks,type=HealthCheck</a></p> </td>
  </tr>
  <tr>
   <td>Bundle attivi</td>
   <td><p>Bundle attivi controlla lo stato di tutti i bundle e:</p>
    <ul>
     <li>restituisce lo stato Avvisa se uno dei bundle non è attivo o (a partire, con attivazione pigra)</li>
     <li>ignora lo stato dei bundle nell'elenco ignora</li>
    </ul> <p>Il parametro di elenco di ignoramenti è configurabile.</p> <p>L'MBean per questo controllo di integrità è <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DinactiveBundles%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.health.check:name=inactiveBundles,type=HealthCheck</a>.</p> </td>
  </tr>
  <tr>
   <td>Controllo della cache del codice</td>
   <td><p>Questo è un controllo dello stato che verifica diverse condizioni JVM che possono attivare un bug CodeCache presente in Java 7:</p>
    <ul>
     <li>restituisce Avvisa se l'istanza è in esecuzione su Java 7, con lo scaricamento della cache del codice abilitato</li>
     <li>restituisce Avvisa se l'istanza è in esecuzione su Java 7 e la dimensione della cache del codice riservato è inferiore a una soglia minima (il valore predefinito è 90 MB)</li>
    </ul> <p>La soglia <code>minimum.code.cache.size</code> è configurabile. Per ulteriori informazioni sul bug, <a href="https://bugs.java.com/bugdatabase/view_bug.do?bug_id=8012547">controlla</a><a href="https://bugs.java.com/bugdatabase/view_bug.do?bug_id=8012547"></a><a href="https://bugs.java.com/bugdatabase/view_bug.do?bug_id=8012547"></a><a href="https://bugs.java.com/bugdatabase/view_bug.do?bug_id=8012547"> questa pagina</a>.</p> <p>L'MBean per questo controllo di integrità è <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DcodeCacheHealthCheck%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.health.check:name=codeCacheHealthCheck,type=HealthCheck</a>.</p> </td>
  </tr>
  <tr>
   <td>Errori nel percorso di ricerca delle risorse</td>
   <td><p>Controlla se sono presenti risorse nel percorso <code>/apps/foundation/components/primary</code> e:</p>
    <ul>
     <li>restituisce Avvisa se sono presenti nodi figlio in <code>/apps/foundation/components/primary</code></li>
    </ul> <p>L'MBean per questo controllo di integrità è <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DresourceSearchPathErrorHealthCheck%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.health.check:name=resourceSearchPathErrorHealthCheck,type=HealthCheck</a>.</p> </td>
  </tr>
 </tbody>
</table>

## Monitoraggio con Nagios {#monitoring-with-nagios}

Il dashboard di controllo dello stato può integrarsi con Nagios tramite il GRANITE JMX Mbeans. L&#39;esempio seguente illustra come aggiungere un controllo che mostra la memoria utilizzata sul server che esegue AEM.

1. Configurare e installare Nagios sul server di monitoraggio.
1. Quindi, installare il plugin remoto Nagios (NRPE).

   >[!NOTE]
   >
   >Per ulteriori informazioni su come installare Nagios e NRPE sul tuo sistema, consulta la [Documentazione di Nagios](https://library.nagios.com/library/products/nagioscore/manuals/).

1. Aggiungi una definizione host per il server AEM. Questo può essere fatto tramite l&#39;interfaccia Web Nagios XI, utilizzando Configuration Manager:

   1. Aprire un browser e puntare al server Nagios.
   1. Premere il pulsante **Configura** nel menu principale.
   1. Nel riquadro a sinistra, premere **Core Config Manager** in **Advanced Configuration**.
   1. Premi il collegamento **Host** nella sezione **Monitoraggio** .
   1. Aggiungi la definizione dell&#39;host:

   ![chlimage_1-118](assets/chlimage_1-118.png)

   Di seguito è riportato un esempio di file di configurazione dell&#39;host, nel caso in cui utilizzi Nagios Core:

   ```xml
   define host {
      address 192.168.0.5
      max_check_attempts 3
      check_period 24x7
      check-command check-host-alive
      contacts admin
      notification_interval 60
      notification_period 24x7
   }
   ```

1. Installa Nagios e NRPE sul server AEM.
1. Installa il plug-in [check_http_json](https://github.com/phrawzty/check_http_json) su entrambi i server.
1. Definire un comando di controllo JSON generico su entrambi i server:

   ```xml
   define command{
   
       command_name    check_http_json-int
   
       command_line    /usr/lib/nagios/plugins/check_http_json --user "$ARG1$" --pass "$ARG2$" -u 'https://$HOSTNAME$:$ARG3$/$ARG4$' -e '$ARG5$' -w '$ARG6$' -c '$ARG7$'
   
   }
   ```

1. Aggiungi un servizio per la memoria utilizzata sul server AEM:

   ```xml
   define service {
   
       use generic-service
   
       host_name my.remote.host
   
       service_description AEM Author Used Memory
   
       check_command  check_http_json-int!<cq-user>!<cq-password>!<cq-port>!system/sling/monitoring/mbeans/java/lang/Memory.infinity.json!{noname}.mbean:attributes.HeapMemoryUsage.mbean:attributes.used.mbean:value!<warn-threshold-in-bytes>!<critical-threshold-in-bytes>
   
       }
   ```

1. Controlla il tuo dashboard di Nagios per il servizio appena creato:

   ![chlimage_1-119](assets/chlimage_1-119.png)

## Strumenti di diagnosi {#diagnosis-tools}

Il dashboard dell&#39;operazione fornisce anche l&#39;accesso agli strumenti di diagnosi che possono aiutare a trovare e risolvere le cause principali degli avvisi provenienti dal dashboard di controllo dello stato, nonché fornire informazioni di debug importanti per gli operatori di sistema.

Tra le sue caratteristiche più importanti:

* Un analizzatore di messaggi di log
* La possibilità di accedere alle immagini heap e thread
* Richieste e analisi delle prestazioni delle query

Per accedere alla schermata Strumenti di diagnosi, vai a **Strumenti - Operazioni - Diagnosi** dalla schermata di benvenuto AEM. Puoi anche accedere direttamente alla schermata accedendo direttamente al seguente URL: `https://serveraddress:port/libs/granite/operations/content/diagnosis.html`

![chlimage_1-120](assets/chlimage_1-120.png)

### Messaggi del registro {#log-messages}

Per impostazione predefinita, l&#39;interfaccia utente dei messaggi di log visualizza tutti i messaggi ERROR. Se desideri visualizzare più messaggi di log, devi configurare un logger con il livello di log appropriato.

I messaggi di log utilizzano un appender del log in memoria e quindi non sono correlati ai file di log. Un’altra conseguenza è che la modifica dei livelli di registro in questa interfaccia utente non modificherà le informazioni registrate nei file di registro tradizionali. L’aggiunta e la rimozione di logger in questa interfaccia utente influirà solo sul logger di memoria in . Inoltre, si noti che la modifica delle configurazioni del logger si rifletterà nel futuro del logger di memoria - le voci che sono già registrate e non sono più rilevanti non vengono eliminate, ma voci simili non verranno registrate in futuro.

Puoi configurare ciò che viene registrato fornendo configurazioni del logger dal pulsante in alto a sinistra dell’ingranaggio nell’interfaccia utente. Qui puoi aggiungere, rimuovere o aggiornare le configurazioni del logger. Una configurazione del logger è composta da un **livello di log** (WARN / INFO / DEBUG) e da un **nome filtro**. Il **nome filtro** ha il ruolo di filtrare l&#39;origine dei messaggi di log che vengono registrati. In alternativa, se un logger deve acquisire tutti i messaggi di log per il livello specificato, il nome del filtro deve essere &quot;**root**&quot;. L’impostazione del livello di un logger attiverà l’acquisizione di tutti i messaggi con un livello uguale o superiore a quello specificato.

Esempi:

* Se prevedi di acquisire tutti i messaggi **ERROR**, non è necessaria alcuna configurazione. Tutti i messaggi ERROR vengono acquisiti per impostazione predefinita.
* Se prevedi di acquisire tutti i messaggi **ERROR**, **WARN** e **INFO**, il nome del logger deve essere impostato su: &quot;**root**&quot; e il livello di logger a: **INFO**.

* Se prevedi di acquisire tutti i messaggi provenienti da un determinato pacchetto (ad esempio com.adobe.granite) - il nome del logger deve essere impostato su: &quot;com.adobe.granite&quot; e il livello di logger è: **DEBUG** (questo acquisirà tutti i messaggi **ERROR**, **WARN**, **INFO** e **DEBUG**), come mostrato nell&#39;immagine seguente.

![chlimage_1-121](assets/chlimage_1-121.png)

>[!NOTE]
>
>Non è possibile impostare un nome di logger per acquisire solo i messaggi ERROR tramite un filtro specificato. Per impostazione predefinita, tutti i messaggi ERROR vengono acquisiti.

>[!NOTE]
>
>L&#39;interfaccia utente dei messaggi di log non riflette l&#39;effettivo registro degli errori. A meno che non si configurino altri tipi di messaggi di log nell&#39;interfaccia utente, verranno visualizzati solo i messaggi ERROR. Per informazioni su come visualizzare messaggi di log specifici, consulta le istruzioni riportate sopra.

>[!NOTE]
>
>Le impostazioni nella pagina di diagnosi non influenzano ciò che viene registrato nei file di log e viceversa. Pertanto, anche se il registro degli errori potrebbe rilevare i messaggi INFO, potrebbero non essere visualizzati nell&#39;interfaccia utente dei messaggi di log. Inoltre, attraverso l&#39;interfaccia utente è possibile catturare i messaggi DEBUG da alcuni pacchetti senza che questo influisca sul registro degli errori. Per ulteriori informazioni su come configurare i file di registro, consulta [Logging](/help/sites-deploying/configure-logging.md).

>[!NOTE]
>
>**Con AEM 6.4**, le attività di manutenzione vengono disconnesse in un formato più ricco di informazioni a livello INFO. Ciò consente una migliore visibilità dello stato delle attività di manutenzione.
>
>Se utilizzi strumenti di terze parti (come Splunk) per monitorare e reagire all’attività di manutenzione, puoi utilizzare le seguenti istruzioni di registro:

```
Log level: INFO
DATE+TIME [MaintanceLogger] Name=<MT_NAME>, Status=<MT_STATUS>, Time=<MT_TIME>, Error=<MT_ERROR>, Details=<MT_DETAILS>
```

### Prestazioni della richiesta {#request-performance}

La pagina Prestazioni richiesta consente di analizzare le richieste di pagina più lente elaborate. Solo le richieste di contenuto verranno registrate in questa pagina. In particolare, verranno acquisite le seguenti richieste:

1. Richieste di accesso alle risorse in `/content`
1. Richieste di accesso alle risorse in `/etc/design`
1. Richieste con estensione `".html"`

![chlimage_1-122](assets/chlimage_1-122.png)

Viene visualizzata la pagina:

* Data e ora della richiesta
* L’URL e il metodo di richiesta
* Durata in millisecondi

Per impostazione predefinita, vengono acquisite le 20 richieste di pagina più lente, ma il limite può essere modificato in Configuration Manager.

### Prestazioni delle query {#query-performance}

La pagina Prestazioni query consente di analizzare le query più lente eseguite dal sistema. Queste informazioni sono fornite dall&#39;archivio in un Mbean JMX. In Jackrabbit, il `com.adobe.granite.QueryStat` JMX Mbean fornisce queste informazioni, mentre nell&#39;archivio Oak, è offerto da `org.apache.jackrabbit.oak.QueryStats.`

Viene visualizzata la pagina:

* Data e ora in cui è stata effettuata la query
* Lingua della query
* Numero di volte in cui è stata emessa la query
* Istruzione della query
* Durata in millisecondi

![chlimage_1-123](assets/chlimage_1-123.png)

### Spiega query {#explain-query}

Per qualsiasi query specifica, Oak cerca di trovare il modo migliore per eseguire in base agli indici Oak definiti nell&#39;archivio sotto il nodo **oak:index**. A seconda della query, Oak può scegliere indici diversi. La comprensione di come Oak sta eseguendo una query è il primo passaggio per ottimizzare la query.

La query di spiegazione è uno strumento che spiega come Oak sta eseguendo una query. È possibile accedervi andando su **Strumenti - Operazioni - Diagnosi** dalla schermata di benvenuto AEM, quindi facendo clic su **Prestazioni query** e passando alla scheda **Spiega query** .

**Funzioni**

* Supporta i linguaggi di query Xpath, JCR-SQL e JCR-SQL2
* Segnala il tempo di esecuzione effettivo della query fornita
* Rileva query lente e avvisa di query potenzialmente lente
* Segnala l’indice Oak utilizzato per eseguire la query
* Visualizza la spiegazione effettiva del motore di query Oak
* Elenco di clic-to-load delle query lente e popolari

Una volta nell&#39;interfaccia utente di Explain Query, tutto ciò che devi fare per usarla è inserire la query e premere il pulsante **Spiega**:

![chlimage_1-124](assets/chlimage_1-124.png)

La prima voce nella sezione Spiegazione query è la spiegazione effettiva. Nella spiegazione verrà visualizzato il tipo di indice utilizzato per eseguire la query.

La seconda voce è il piano di esecuzione.

Quando si fa clic sulla casella **Includi tempo di esecuzione** prima di eseguire la query, viene visualizzata anche la quantità di tempo in cui la query è stata eseguita, consentendo ulteriori informazioni che possono essere utilizzate per ottimizzare gli indici per l’applicazione o la distribuzione.

![chlimage_1-125](assets/chlimage_1-125.png)

### Index Manager {#the-index-manager}

Lo scopo di Gestione indici è quello di facilitare la gestione degli indici, ad esempio la manutenzione degli indici o la visualizzazione del loro stato.

Per accedervi, vai su **Strumenti - Operazioni - Diagnosi **dalla schermata iniziale, quindi fai clic sul pulsante **Gestione indici** .

È inoltre possibile accedervi direttamente a questo URL: `https://serveraddress:port/libs/granite/operations/content/diagnosistools/indexManager.html`

![screen-shot_2019-06-18at154754](assets/screen-shot_2019-06-18at154754.png)

L’interfaccia utente può essere utilizzata per filtrare gli indici nella tabella digitando i criteri del filtro nella casella di ricerca nell’angolo in alto a sinistra dello schermo.

### Scarica ZIP stato {#download-status-zip}

Questo attiverà il download di un file ZIP contenente informazioni utili sullo stato e sulla configurazione del sistema. L&#39;archivio contiene configurazioni di istanza, un elenco di bundle, OSGI, metriche Sling e statistiche e questo può portare a un file di grandi dimensioni. È possibile ridurre l&#39;impatto dei file di stato di grandi dimensioni utilizzando la finestra **Scarica ZIP stato**. È possibile accedere alla finestra da:**AEM > Strumenti > Operazioni > Diagnosi > Scarica ZIP stato.**

Da questa finestra è possibile selezionare gli elementi da esportare (file di registro e o immagini di thread) e il numero di giorni di log inclusi nel download rispetto alla data corrente.

![download_status_zip](assets/download_status_zip.png)

### Scarica immagine thread {#download-thread-dump}

Questo attiverà il download di un file ZIP contenente informazioni sui thread presenti nel sistema. Vengono fornite informazioni su ogni thread, ad esempio il suo stato, il classloader e lo stacktrace.

### Scarica immagine heap {#download-heap-dump}

È inoltre possibile scaricare un’istantanea dell’heap, in modo da analizzarla in un secondo momento. Tieni presente che questo attiverà il download di un file di grandi dimensioni, nell’ordine di centinaia di megabyte.

## Attività di manutenzione automatizzata {#automated-maintenance-tasks}

La pagina Attività di manutenzione automatica è un luogo in cui è possibile visualizzare e tenere traccia delle attività di manutenzione consigliate pianificate per l’esecuzione periodica. Le attività sono integrate con il sistema di controllo dello stato di salute. Le attività possono anche essere eseguite manualmente dall’interfaccia .

Per passare alla pagina Manutenzione nel Dashboard delle operazioni, è necessario passare a **Strumenti - Operazioni - Dashboard - Manutenzione** dalla schermata di benvenuto AEM oppure seguire direttamente questo collegamento:

`https://serveraddress:port/libs/granite/operations/content/maintenance.html`

Le seguenti attività sono disponibili nel dashboard delle operazioni:

1. L&#39;attività **Pulizia revisioni** si trova nel menu **Finestra manutenzione giornaliera**.
1. L&#39;attività **Pulizia binari Lucene**, situata nel menu **Finestra manutenzione giornaliera**.
1. L&#39;attività **Pulizia del flusso di lavoro**, che si trova nel menu **Finestra di manutenzione settimanale**.
1. L&#39;attività **Archivio dati raccolta oggetti inattivi**, che si trova nel menu **Finestra manutenzione settimanale**.
1. L&#39;attività **Manutenzione log di controllo**, situata nel menu **Finestra manutenzione settimanale**.
1. L&#39;attività **Manutenzione eliminazione versione**, che si trova nel menu **Finestra manutenzione settimanale**.

Il tempo predefinito per la finestra di manutenzione giornaliera è compreso tra 2 e 5. Le attività configurate per l&#39;esecuzione nella finestra di manutenzione settimanale verranno eseguite tra le 1 e le 2 del mattino del sabato.

È inoltre possibile configurare i tempi premendo l&#39;icona ingranaggio su una delle due schede di manutenzione:

![chlimage_1-126](assets/chlimage_1-126.png)

>[!NOTE]
>
>A partire dal AEM 6.1, le finestre di manutenzione esistenti possono essere configurate per l&#39;esecuzione mensile.

### Pulizia revisioni {#revision-clean-up}

Per ulteriori informazioni sull&#39;esecuzione del cleanup delle revisioni, [consulta questo articolo dedicato](/help/sites-deploying/revision-cleanup.md).

### Pulizia binary di Lucene {#lucene-binaries-cleanup}

Utilizzando l&#39;attività Pulizia binari Lucene, è possibile eliminare i binari lucene e ridurre il fabbisogno di dimensioni dell&#39;archivio dati in esecuzione. Questo perché l&#39;abbandono binario di lucene verrà ririchiesto quotidianamente invece della dipendenza precedente da un&#39;esecuzione [garbage collection dell&#39;archivio dati](/help/sites-administering/data-store-garbage-collection.md) riuscita.

Anche se l&#39;attività di manutenzione è stata sviluppata per ridurre i rifiuti di revisione relativi a Lucene, ci sono miglioramenti generali di efficienza quando si esegue l&#39;attività:

* L&#39;esecuzione settimanale dell&#39;attività di raccolta degli oggetti inattivi dell&#39;archivio dati verrà completata più rapidamente
* Può anche migliorare leggermente le prestazioni complessive AEM

Puoi accedere all’attività Pulizia binari Lucene da: **AEM > Strumenti > Operazioni > Manutenzione > Finestra Manutenzione giornaliera > Pulizia binari Lucene**.

### Archivio dati raccolta oggetti inattivi {#data-store-garbage-collection}

Per informazioni dettagliate sulla raccolta degli oggetti inattivi nell&#39;archivio dati, vedere la [pagina dedicata di documentazione](/help/sites-administering/data-store-garbage-collection.md).

### Eliminazione del flusso di lavoro {#workflow-purge}

I flussi di lavoro possono anche essere eliminati dal dashboard di manutenzione. Per eseguire l’attività Elimina flusso di lavoro, è necessario:

1. Fare clic sulla pagina **Finestra di manutenzione settimanale**.
1. Nella pagina seguente, fai clic sul pulsante **Play** nella scheda **Pulizia del flusso di lavoro**.

>[!NOTE]
>
>Per informazioni più dettagliate sulla manutenzione del flusso di lavoro, consulta [questa pagina](/help/sites-administering/workflows-administering.md#regular-purging-of-workflow-instances).

### Manutenzione del registro di controllo {#audit-log-maintenance}

Per la manutenzione del registro di controllo, vedere la [pagina della documentazione separata.](/help/sites-administering/operations-audit-log.md)

### Pulizia delle versioni {#version-purge}

È possibile pianificare l&#39;attività di manutenzione Pulizia versione per eliminare automaticamente le versioni precedenti. Di conseguenza, questo riduce al minimo la necessità di utilizzare manualmente gli [strumenti di eliminazione delle versioni](/help/sites-deploying/version-purging.md). È possibile pianificare e configurare l&#39;attività Pulizia versione accedendo a **Strumenti > Operazioni > Manutenzione > Finestra manutenzione settimanale** e seguendo questi passaggi:

1. Fai clic sul pulsante **Aggiungi** .
1. Scegli **Pulizia versione** dal menu a discesa.

   ![version_purge_Maintenanceancetask](assets/version_purge_maintenancetask.png)

1. Per configurare l&#39;attività Pulizia versione, fai clic sull&#39;icona **ingranaggi** nella scheda di manutenzione Pulizia versione appena creata.

   ![version_purge_taskconfiguration](assets/version_purge_taskconfiguration.png)

**Con AEM 6.4**, puoi interrompere l’attività di manutenzione Pulizia versione come segue:

* Automaticamente - Se la finestra di manutenzione programmata viene chiusa prima del completamento dell&#39;attività, l&#39;attività viene arrestata automaticamente. Viene ripreso quando si apre la prossima finestra di manutenzione.
* Manualmente - Per interrompere manualmente l&#39;attività, nella scheda di manutenzione Pulizia versione fare clic sull&#39;icona **Interrompi**. All’esecuzione successiva, l’attività riprenderà in modo sicuro.

>[!NOTE]
>
>Per interrompere l’attività di manutenzione, sospenderne l’esecuzione senza perdere traccia del processo già in corso.

>[!CAUTION]
>
>Per ottimizzare le dimensioni del repository, è necessario eseguire frequentemente l&#39;attività di eliminazione della versione. L&#39;attività deve essere pianificata al di fuori dell&#39;orario di lavoro quando vi è una quantità limitata di traffico.

## Attività di manutenzione personalizzate {#custom-maintenance-tasks}

Le attività di manutenzione personalizzate possono essere implementate come servizi OSGi. Poiché l’infrastruttura delle attività di manutenzione si basa sulla gestione dei processi di Apache Sling, un’attività di manutenzione deve implementare l’interfaccia java ` [org.apache.sling.event.jobs.consumer.JobExecutor](https://sling.apache.org/apidocs/sling7/org/apache/sling/event/jobs/consumer/JobExecutor.html)`. Inoltre, deve dichiarare diverse proprietà di registrazione del servizio da rilevare come attività di manutenzione, come indicato di seguito:

<table>
 <tbody>
  <tr>
   <td><strong>Nome proprietà servizio</strong><br /> </td>
   <td><strong>Descrizione</strong></td>
   <td><strong>Esempio</strong><br /> </td>
   <td><strong>Tipo</strong></td>
  </tr>
  <tr>
   <td>granite.maintenance.isStoppable</td>
   <td>Attributo booleano che definisce se l’attività può essere interrotta dall’utente. Se un'attività dichiara di essere arrestata, deve verificare durante la sua esecuzione se è stata arrestata e agire di conseguenza. Il valore predefinito è false.</td>
   <td>vero</td>
   <td>Facoltativo</td>
  </tr>
  <tr>
   <td>granite.maintenance.mandatory</td>
   <td>Attributo booleano che definisce se un'attività è obbligatoria e deve essere eseguita periodicamente. Se un'attività è obbligatoria, ma al momento non è presente in alcuna finestra di pianificazione attiva, un controllo integrità segnalerà l'errore. Il valore predefinito è false.</td>
   <td>vero</td>
   <td>Facoltativo</td>
  </tr>
  <tr>
   <td>granite.maintenance.name</td>
   <td>Nome univoco dell'attività, utilizzato per fare riferimento all'attività. Questo è solitamente un nome semplice.</td>
   <td>AttivitàManutenzionePersonale</td>
   <td>Obbligatorio</td>
  </tr>
  <tr>
   <td>granite.maintenance.title</td>
   <td>Titolo visualizzato per l'attività</td>
   <td>Attività di manutenzione speciale</td>
   <td>Obbligatorio</td>
  </tr>
  <tr>
   <td>job.topics</td>
   <td>Questo è un argomento unico dell'attività di manutenzione.<br /> La gestione dei processi Apache Sling avvierà un processo con esattamente questo argomento per eseguire l'attività di manutenzione e quando l'attività viene registrata per questo argomento viene eseguita.<br /> L'argomento deve iniziare con  <i>com/adobe/granite/maintenance/job/</i></td>
   <td>com/adobe/granite/maintenance/job/MyMaintenanceTask</td>
   <td>Obbligatorio</td>
  </tr>
 </tbody>
</table>

Oltre alle proprietà del servizio di cui sopra, il metodo `process()` dell&#39;interfaccia `JobConsumer` deve essere implementato aggiungendo il codice da eseguire per l&#39;attività di manutenzione. Il `JobExecutionContext` fornito può essere utilizzato per generare informazioni sullo stato, controllare se il processo viene interrotto dall&#39;utente e creare un risultato (riuscito o non riuscito).

Per le situazioni in cui un’attività di manutenzione non deve essere eseguita su tutte le installazioni (ad esempio, eseguita solo sull’istanza di pubblicazione), puoi fare sì che il servizio richieda una configurazione per essere attivo aggiungendo `@Component(policy=ConfigurationPolicy.REQUIRE)`. Puoi quindi contrassegnare la configurazione in base alla modalità di esecuzione a seconda dell’archivio. Per ulteriori informazioni, consulta [Configurazione di OSGi](/help/sites-deploying/configuring-osgi.md#creating-the-configuration-in-the-repository).

Di seguito è riportato un esempio di un&#39;attività di manutenzione personalizzata che elimina i file da una directory temporanea configurabile che sono stati modificati nelle ultime 24 ore:

src/main/java/com/adobe/granite/samples/maintenance/impl/DeleteTempFilesTask.java

<table>
 <tbody>
  <tr>
   <td><p> </p> <p><code>/*</code></p> <p><code> * #%L</code></p> <p><code> * sample-maintenance-task</code></p> <p><code> * %%</code></p> <p><code> * Copyright (C) 2014 Adobe</code></p> <p><code> * %%</code></p> <p><code> * Licensed under the Apache License, Version 2.0 (the "License");</code></p> <p><code> * you may not use this file except in compliance with the License.</code></p> <p><code> * You may obtain a copy of the License at</code></p> <p><code> * </code></p> <p><code> * <a href="https://www.apache.org/licenses/LICENSE-2.0">https://www.apache.org/licenses/LICENSE-2.0</a></code></p> <p><code> * </code></p> <p><code> * Unless required by applicable law or agreed to in writing, software</code></p> <p><code> * distributed under the License is distributed on an "AS IS" BASIS,</code></p> <p><code> * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.</code></p> <p><code> * See the License for the specific language governing permissions and</code></p> <p><code> * limitations under the License.</code></p> <p><code> * #L%</code></p> <p><code> */</code></p> <p><code> </code></p> <p><code>package com.adobe.granite.samples.maintenance.impl;</code></p> <p><code> </code></p> <p><code>import java.io.File;</code></p> <p><code>import java.util.Calendar;</code></p> <p><code>import java.util.Collection;</code></p> <p><code>import java.util.Map;</code></p> <p><code> </code></p> <p><code>import org.apache.commons.io.FileUtils;</code></p> <p><code>import org.apache.commons.io.filefilter.IOFileFilter;</code></p> <p><code>import org.apache.commons.io.filefilter.TrueFileFilter;</code></p> <p><code>import org.apache.felix.scr.annotations.Activate;</code></p> <p><code>import org.apache.felix.scr.annotations.Component;</code></p> <p><code>import org.apache.felix.scr.annotations.Properties;</code></p> <p><code>import org.apache.felix.scr.annotations.Property;</code></p> <p><code>import org.apache.felix.scr.annotations.Service;</code></p> <p><code>import org.apache.sling.commons.osgi.PropertiesUtil;</code></p> <p><code>import org.apache.sling.event.jobs.Job;</code></p> <p><code>import org.apache.sling.event.jobs.consumer.JobConsumer;</code></p> <p><code>import org.apache.sling.event.jobs.consumer.JobExecutionContext;</code></p> <p><code>import org.apache.sling.event.jobs.consumer.JobExecutionResult;</code></p> <p><code>import org.apache.sling.event.jobs.consumer.JobExecutor;</code></p> <p><code>import org.slf4j.Logger;</code></p> <p><code>import org.slf4j.LoggerFactory;</code></p> <p><code> </code></p> <p><code>import com.adobe.granite.maintenance.MaintenanceConstants;</code></p> <p><code> </code></p> <p><code>@Component(metatype = true,</code></p> <p><code> label = "Delete Temp Files Maintenance Task",</code></p> <p><code> description = "Maintatence Task which deletes files from a configurable temporary directory which have been modified in the last 24 hours.")</code></p> <p><code>@Service</code></p> <p><code>@Properties({</code></p> <p><code> @Property(name = MaintenanceConstants.PROPERTY_TASK_NAME, value = "DeleteTempFilesTask", propertyPrivate = true),</code></p> <p><code> @Property(name = MaintenanceConstants.PROPERTY_TASK_TITLE, value = "Delete Temp Files", propertyPrivate = true),</code></p> <p><code> @Property(name = JobConsumer.PROPERTY_TOPICS, value = MaintenanceConstants.TASK_TOPIC_PREFIX</code></p> <p><code> + "DeleteTempFilesTask", propertyPrivate = true) })</code></p> <p><code>public class DeleteTempFilesTask implements JobExecutor {</code></p> <p><code> </code></p> <p><code> private static final Logger log = LoggerFactory.getLogger(DeleteTempFilesTask.class);</code></p> <p><code> </code></p> <p><code> @Property(label = "Temporary Directory", description="Temporary Directory. Defaults to the java.io.tmpdir system property.")</code></p> <p><code> private static final String PROP_TEMP_DIR = "temp.dir";</code></p> <p><code> </code></p> <p><code> private File tempDir;</code></p> <p><code> </code></p> <p><code> @Activate</code></p> <p><code> private void activate(Map&lt;string, object=""&gt; properties) {</code></p> <p><code> this.tempDir = new File(PropertiesUtil.toString(properties.get(PROP_TEMP_DIR),</code></p> <p><code> System.getProperty("java.io.tmpdir")));</code></p> <p><code> }</code></p> <p><code> </code></p> <p><code> @Override</code></p> <p><code> public JobExecutionResult process(Job job, JobExecutionContext context) {</code></p> <p><code> log.info("Deleting old temp files from {}.", tempDir.getAbsolutePath());</code></p> <p><code> Collection&lt;file&gt; files = FileUtils.listFiles(tempDir, new LastModifiedBeforeYesterdayFilter(),</code></p> <p><code> TrueFileFilter.INSTANCE);</code></p> <p><code> int counter = 0;</code></p> <p><code> for (File file : files) {</code></p> <p><code> log.debug("Deleting file {}.", file.getAbsolutePath());</code></p> <p><code> counter++;</code></p> <p><code> file.delete();</code></p> <p><code> // TODO - capture the output of delete() and do something useful with it</code></p> <p><code> }</code></p> <p><code> return context.result().message(String.format("Deleted %s files.", counter)).succeeded();</code></p> <p><code> }</code></p> <p><code> </code></p> <p><code> /**</code></p> <p><code> * IOFileFilter which filters out files which have been modified in the last 24 hours.</code></p> <p><code> *</code></p> <p><code> */</code></p> <p><code> private static class LastModifiedBeforeYesterdayFilter implements IOFileFilter {</code></p> <p><code> </code></p> <p><code> private final long minTime;</code></p> <p><code> </code></p> <p><code> private LastModifiedBeforeYesterdayFilter() {</code></p> <p><code> Calendar cal = Calendar.getInstance();</code></p> <p><code> cal.add(Calendar.DATE, -1);</code></p> <p><code> this.minTime = cal.getTimeInMillis();</code></p> <p><code> }</code></p> <p><code> </code></p> <p><code> @Override</code></p> <p><code> public boolean accept(File dir, String name) {</code></p> <p><code> // this method is never actually called.</code></p> <p><code> return false;</code></p> <p><code> }</code></p> <p><code> </code></p> <p><code> @Override</code></p> <p><code> public boolean accept(File file) {</code></p> <p><code> return file.lastModified() <= this.minTime;</code></p> <p><code> }</code></p> <p><code> }</code></p> <p><code> </code></p> <p><code>}</code></p> <p><code>&lt;file&gt;&lt;/string,&gt;</code></p> <p> </p> </td>
  </tr>
 </tbody>
</table>

[experiencemanager-java-maintenance-ancetask-sample](https://github.com/Adobe-Marketing-Cloud/experiencemanager-java-maintenancetask-sample) -  [src/main/java/com/adobe/granite/samples/maintenance/impl/DeleteTempFilesTask.java](https://github.com/Adobe-Marketing-Cloud/experiencemanager-java-maintenancetask-sample/blob/master/src/main/java/com/adobe/granite/samples/maintenance/impl/DeleteTempFilesTask.java)

Una volta implementato, il servizio viene esposto all&#39;interfaccia utente del dashboard delle operazioni. È possibile aggiungerlo a una delle pianificazioni di manutenzione disponibili:

![chlimage_1-127](assets/chlimage_1-127.png)

Verrà aggiunta una risorsa corrispondente in /apps/granite/operations/config/maintenance/`schedule`/`taskname`. Se l&#39;attività dipende dalla modalità di esecuzione, la proprietà granite.operations.Conditions.runmode deve essere impostata su quel nodo con i valori delle modalità di esecuzione che devono essere attive per questa attività di manutenzione.

## Panoramica sistema {#system-overview}

Il **Dashboard panoramica sistema** visualizza una panoramica di alto livello della configurazione, dell&#39;hardware e dello stato dell&#39;istanza AEM. Ciò significa che lo stato di integrità del sistema è trasparente e che tutte le informazioni sono aggregate in un unico dashboard.

>[!NOTE]
>
>Puoi anche [guardare questo video](https://video.tv.adobe.com/v/21340) per un&#39;introduzione al dashboard Panoramica sistema.

### Come accedere a {#how-to-access}

Per accedere al dashboard Panoramica sistema, passa a **Strumenti > Operazioni > Panoramica del sistema**.

![system_overview_dashboard](assets/system_overview_dashboard.png)

### Dashboard di panoramica del sistema {#system-overview-dashboard-explained}

La tabella seguente descrive tutte le informazioni visualizzate nel dashboard Panoramica sistema. Tieni presente che quando non sono presenti informazioni rilevanti da mostrare (ad esempio, il backup non è in corso, non sono presenti controlli di integrità critici) nella rispettiva sezione verrà visualizzato il messaggio &quot;Nessuna voce&quot;.

È inoltre possibile scaricare un file `JSON` che riepiloga le informazioni del dashboard facendo clic sul pulsante **Scarica** nell&#39;angolo in alto a destra del dashboard.L&#39;endpoint `JSON` è `/libs/granite/operations/content/systemoverview/export.json` e può essere utilizzato in uno script `curl` per il monitoraggio esterno.

<table>
 <tbody>
  <tr>
   <td><strong>Sezione</strong></td>
   <td><strong>Informazioni visualizzate</strong></td>
   <td><strong>Quando è critico</strong></td>
   <td><strong>Collegamenti a</strong></td>
  </tr>
  <tr>
   <td>Verifiche stato</td>
   <td>
    <ul>
     <li>un elenco dei controlli in stato critico</li>
     <li>un elenco dei controlli in stato di avviso</li>
    </ul> </td>
   <td>Indicato visivamente:<br />
    <ul>
     <li>un tag rosso per i controlli critici</li>
     <li>un tag arancione per i controlli Avvisa</li>
    </ul> </td>
   <td>
    <ul>
     <li>Pagina Rapporti stato</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Attività di manutenzione</td>
   <td>
    <ul>
     <li>elenco delle attività non riuscite</li>
     <li>un elenco delle attività attualmente in esecuzione</li>
     <li>un elenco delle attività completate nell'ultima esecuzione</li>
     <li>un elenco delle attività che non sono mai state eseguite</li>
     <li>un elenco di attività non pianificate</li>
    </ul> </td>
   <td><p>Indicato visivamente:</p>
    <ul>
     <li>un tag rosso per le attività non riuscite</li>
     <li>un tag arancione per l’esecuzione delle attività (in quanto potrebbero influire sulle prestazioni)</li>
     <li>tag grigi per ogni altro stato</li>
    </ul> </td>
   <td>
    <ul>
     <li>Pagina Attività di manutenzione</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Sistema</td>
   <td>
    <ul>
     <li>sistema operativo e versione del sistema operativo (ad esempio, Mac OS X)</li>
     <li>media del carico del sistema, come recuperato da <a href="https://docs.oracle.com/javase/8/docs/api/java/lang/management/OperatingSystemMXBean.html#getSystemLoadAverage--">OperatingSystemMXBeaneable</a></li>
     <li>spazio su disco (sulla partizione in cui si trova la home directory)</li>
     <li>heap massimo, come restituito da <a href="https://docs.oracle.com/javase/8/docs/api/java/lang/management/MemoryMXBean.html#getHeapMemoryUsage--">MemoryMXBean</a></li>
    </ul> </td>
   <td>N/D</td>
   <td>N/D</td>
  </tr>
  <tr>
   <td>Istanza</td>
   <td>
    <ul>
     <li>la versione AEM</li>
     <li>elenco delle modalità di esecuzione</li>
     <li>la data di avvio dell’istanza</li>
    </ul> </td>
   <td>N/D</td>
   <td>N/D</td>
  </tr>
  <tr>
   <td>Archivio</td>
   <td>
    <ul>
     <li>la versione Oak</li>
     <li>tipo di archivio nodi (Segment Tar o Document)
      <ul>
       <li>se il tipo è documento, viene visualizzato il tipo di archivio documenti (RDB o Mongo)</li>
      </ul> </li>
     <li>se è presente un archivio dati personalizzato:
      <ul>
       <li>per un archivio dati file, viene visualizzato il percorso</li>
       <li>per un archivio dati S3, viene visualizzato il nome del bucket S3</li>
       <li>per un archivio dati S3 condiviso, viene visualizzato il nome del bucket S3</li>
       <li>per un archivio dati di Azure, viene visualizzato il contenitore</li>
      </ul> </li>
     <li>in assenza di un datastore esterno personalizzato, viene visualizzato un messaggio che indica che questo fatto è</li>
    </ul> </td>
   <td>N/D</td>
   <td>N/D</td>
  </tr>
  <tr>
   <td>Agenti di distribuzione</td>
   <td>
    <ul>
     <li>un elenco di agenti con code bloccate</li>
     <li>un elenco di agenti non configurati correttamente ("Errore di configurazione")</li>
     <li>un elenco di agenti in attesa di elaborazione della coda</li>
     <li>un elenco degli agenti inattivi</li>
     <li>un elenco di agenti in esecuzione (che stanno elaborando voci)</li>
    </ul> </td>
   <td><p>Indicato visivamente:</p>
    <ul>
     <li>un tag rosso per gli agenti bloccati o gli errori di configurazione</li>
     <li>un tag arancione per gli agenti in pausa</li>
     <li>un tag grigio per agenti in pausa, inattivi o in esecuzione<br /> </li>
    </ul> </td>
   <td>Pagina di distribuzione<br /> </td>
  </tr>
  <tr>
   <td>Agenti di replica</td>
   <td>
    <ul>
     <li>un elenco di agenti con code bloccate</li>
     <li>un elenco degli agenti inattivi</li>
     <li>un elenco di agenti in esecuzione (che stanno elaborando voci)</li>
    </ul> </td>
   <td><p>Indicato visivamente:<br /> </p>
    <ul>
     <li>un tag rosso per gli agenti bloccati</li>
     <li>un tag grigio per gli agenti in pausa</li>
    </ul> </td>
   <td>Pagina di replica</td>
  </tr>
  <tr>
   <td>Flussi di lavoro</td>
   <td>
    <ul>
     <li>Processi flusso di lavoro:
      <ul>
       <li>numero di processi del flusso di lavoro non riusciti (se presenti)</li>
       <li>numero di processi del flusso di lavoro annullati (se presenti)</li>
      </ul> </li>
    </ul>
    <ul>
     <li>Conteggi flussi di lavoro - numero di flussi di lavoro in un dato stato (se presenti):
      <ul>
       <li>esecuzione</li>
       <li>non riuscito</li>
       <li>sospeso</li>
       <li>interrotto</li>
      </ul> </li>
    </ul> <p>Per ciascuno degli stati presentati sopra viene eseguita una query con un limite di 400 millisecondi. A 400 millisecondi viene visualizzato il numero di voci ottenute fino a quel momento.</p> </td>
   <td><p>Non interpretato:</p>
    <ul>
     <li>l’utente deve indagare in caso di flussi di lavoro e processi con stati imprevisti.</li>
    </ul> </td>
   <td>Pagina Errori di flusso di lavoro</td>
  </tr>
  <tr>
   <td>Processi Sling</td>
   <td><p>Conteggi dei processi Sling - numero di processi in uno stato specifico (se presenti):</p>
    <ul>
     <li>non riuscito</li>
     <li>in coda</li>
     <li>annullato</li>
     <li>attivi</li>
    </ul> </td>
   <td><p>Non interpretato:</p>
    <ul>
     <li>l’utente deve indagare quando ci sono processi in stati imprevisti o con conteggi elevati.</li>
    </ul> </td>
   <td>N/D</td>
  </tr>
  <tr>
   <td>Conteggi nodi stimati</td>
   <td><p>Numero stimato di:</p>
    <ul>
     <li>pagine</li>
     <li>assets</li>
     <li>tag</li>
     <li>autorizzabili</li>
     <li>numero totale di nodi<br /> </li>
    </ul> <p>Il numero totale di nodi viene ottenuto da nodeCounterMBean, mentre il resto delle statistiche viene ottenuto da IndexInfoService.</p> </td>
   <td>N/D</td>
   <td>N/D</td>
  </tr>
  <tr>
   <td>Backup</td>
   <td>Visualizza "Backup online in corso" se questo è il caso.</td>
   <td>N/D</td>
   <td>N/D</td>
  </tr>
  <tr>
   <td>Indicizzazione</td>
   <td><p>Display:</p>
    <ul>
     <li>"Indicizzazione in corso"</li>
     <li>"Query in corso"</li>
    </ul> <p>Se un thread di indicizzazione o query è presente nel dump di thread.</p> </td>
   <td>N/D</td>
   <td>N/D</td>
  </tr>
 </tbody>
</table>
