---
title: Best practice per i flussi di lavoro
seo-title: Workflow Best Practices
description: Best practice per i flussi di lavoro
seo-description: null
uuid: 79be4055-c2ef-428e-9054-103c6cfde1d2
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 0be8b88c-6f57-4dcc-ae11-77b378a2decd
exl-id: 14775476-6fe5-4583-8ab5-b55fef892174
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1920'
ht-degree: 1%

---

# Best practice per i flussi di lavoro{#workflow-best-practices}

I flussi di lavoro consentono di automatizzare le attività di Adobe Experience Manager (AEM).

Spesso rappresentano una grande quantità di elaborazione che si verifica in un ambiente AEM, pertanto, quando i passaggi di un flusso di lavoro personalizzato non vengono scritti in base alle best practice, o i flussi di lavoro preconfigurati non sono configurati in modo da funzionare nel modo più efficiente possibile, il sistema può risentirne.

È quindi vivamente consigliato pianificare con attenzione le implementazioni dei flussi di lavoro.

## Configurazione {#configuration}

Durante la configurazione dei processi del flusso di lavoro (personalizzati e/o preconfigurati), è necessario tenere presenti alcuni aspetti.

### Flussi di lavoro transitori {#transient-workflows}

Per ottimizzare i carichi di ingestione elevati puoi definire un [flusso di lavoro come transitorio](/help/sites-developing/workflows.md#transient-workflows).

Quando un flusso di lavoro è transitorio, i dati di runtime relativi ai passaggi di lavoro intermedi non vengono mantenuti nel JCR quando vengono eseguiti (le rappresentazioni di output vengono ovviamente mantenute).

I vantaggi possono comprendere:

* Una riduzione del tempo di elaborazione del flusso di lavoro; fino al 10%.
* Riduzione significativa della crescita dell&#39;archivio.
* Per eliminare non sono necessari più flussi di lavoro CRUD.
* Inoltre, riduce il numero di file TAR da compattare.

>[!CAUTION]
>
>Se la tua azienda richiede la persistenza/archiviazione dei dati di runtime del flusso di lavoro a scopo di controllo, non abilitare questa funzione.

### Ottimizzazione dei flussi di lavoro DAM {#tuning-dam-workflows}

Per le linee guida per l’ottimizzazione delle prestazioni per i flussi di lavoro DAM, consulta [Guida all’ottimizzazione delle prestazioni di AEM Assets](/help/assets/performance-tuning-guidelines.md).

### Configura il numero massimo di flussi di lavoro simultanei {#configure-the-maximum-number-of-concurrent-workflows}

AEM consentire l’esecuzione simultanea di più thread di flusso di lavoro. Per impostazione predefinita, il numero di thread è configurato in modo da essere la metà del numero di core del processore sul sistema.

Nei casi in cui i flussi di lavoro in esecuzione richiedono risorse di sistema, ciò può significare che rimane poco AEM da utilizzare per altre attività, ad esempio per il rendering dell’interfaccia utente di authoring. Di conseguenza, il sistema potrebbe risultare lento durante attività come il caricamento collettivo delle immagini.

Per risolvere questo problema, l&#39;Adobe consiglia di configurare il numero di **Processi paralleli massimi** essere tra la metà e i tre quarti del numero di core del processore presenti nel sistema. Questo dovrebbe consentire al sistema di mantenere una capacità sufficiente per rimanere reattivo durante l’elaborazione di questi flussi di lavoro.

Per configurare **Processi paralleli massimi**, puoi effettuare le seguenti operazioni:

* Configura le **[Configurazione OSGi](/help/sites-deploying/configuring-osgi.md)** dalla console Web AEM; per **Coda: Coda flusso di lavoro Granite** (2) **Configurazione della coda dei processi Sling Apache**).

* Configura la coda da **Processi Sling** opzione della console Web AEM; per **Configurazione coda processi: Coda flusso di lavoro Granite**, a `http://localhost:4502/system/console/slingevent`.

Inoltre, è disponibile una configurazione separata per il **Coda processi esterni flusso di lavoro Granite**. Viene utilizzato per i processi del flusso di lavoro che avviano binari esterni, ad esempio **InDesign Server** o **Immagine Magick**.

### Configurare singole code di lavoro {#configure-individual-job-queues}

In alcuni casi è utile configurare singole code di lavoro per controllare i thread simultanei o altre opzioni di coda, in base a un singolo processo. Puoi aggiungere e configurare una singola coda dalla console Web tramite la **Configurazione della coda dei processi Sling Apache** fabbrica. Per trovare l’argomento appropriato da elencare, esegui il modello del flusso di lavoro e cercarlo nella **Processi Sling** console; ad esempio, in `http://localhost:4502/system/console/slingevent`.

È possibile aggiungere code di lavoro individuali anche per i flussi di lavoro transitori.

### Configurare la pulizia del flusso di lavoro {#configure-workflow-purging}

In un&#39;installazione standard AEM fornisce una console di manutenzione che consente di pianificare e configurare le attività di manutenzione quotidiane e settimanali; ad esempio, in:

`http://localhost:4502/libs/granite/operations/content/maintenance.html`

Per impostazione predefinita, la **Finestra Manutenzione settimanale** ha **Eliminazione del flusso di lavoro** ma questo deve essere configurato prima che venga eseguito. Per configurare le pulizie del flusso di lavoro, una nuova **Configurazione di eliminazione del flusso di lavoro di Adobe Granite** devono essere aggiunti nella console Web.

Per ulteriori dettagli sulle attività di manutenzione in AEM, consulta la sezione [Dashboard delle operazioni](/help/sites-administering/operations-dashboard.md).

## Personalizzazione {#customization}

Quando si scrivono processi di flusso di lavoro personalizzati, è necessario tenere presenti alcuni aspetti.

### Posizioni {#locations}

Le definizioni dei modelli di flusso di lavoro, dei moduli di avvio, degli script e delle notifiche vengono conservate nel repository in base al tipo; ovvero preconfigurato, personalizzato, tra gli altri.

>[!NOTE]
>
>Vedi anche [Ristrutturazione dell’archivio in AEM 6.5](/help/sites-deploying/repository-restructuring.md).

#### Posizioni - Modelli di flusso di lavoro {#locations-workflow-models}

I modelli di flusso di lavoro vengono memorizzati nell’archivio in base al tipo:

* Le progettazioni di flussi di lavoro preconfigurate si trovano nel seguente percorso:

   `/libs/settings/workflow/models/`

   >[!CAUTION]
   >
   >Non eseguire:
   >
   >* inserisci uno dei modelli di flusso di lavoro personalizzati in questa cartella
   >* modificare qualsiasi elemento in `/libs`

   >
   >Come qualsiasi modifica può essere sovrascritta al momento dell&#39;aggiornamento o durante l&#39;installazione di hotfix, cumulative fix pack o service pack.

* Le progettazioni di flussi di lavoro personalizzate si trovano in:

   ```
   /conf/global/settings/workflow/models/...
   ```

* Le progettazioni del flusso di lavoro runtime (sia predefinite che personalizzate) si trovano nel seguente percorso:

   `/var/workflow/models/`

* Le progettazioni di flussi di lavoro legacy (sia in fase di progettazione che di runtime) si trovano nel seguente percorso:

   `/etc/workflow/models/`

   >[!NOTE]
   >
   >Se le progettazioni vengono modificate *utilizzo dell’interfaccia AEM*, i dettagli verranno copiati nelle nuove posizioni.

#### Posizioni - Workflow Launcher {#locations-workflow-launchers}

Le definizioni del modulo di avvio del flusso di lavoro vengono memorizzate anche nell’archivio in base al tipo:

* I moduli di avvio dei flussi di lavoro preconfigurati si trovano nel seguente percorso:

   `/libs/settings/workflow/launcher/`

   >[!CAUTION]
   >
   >Non eseguire:
   >
   >* inserisci uno dei moduli di avvio del flusso di lavoro personalizzati in questa cartella
   >* modificare qualsiasi elemento in `/libs`

   >
   >Come qualsiasi modifica può essere sovrascritta al momento dell&#39;aggiornamento o durante l&#39;installazione di hotfix, cumulative fix pack o service pack.

* I moduli di avvio dei flussi di lavoro personalizzati si trovano in:

   ```
   /conf/global/settings/workflow/launcher/...
   ```

* I moduli di avvio dei flussi di lavoro legacy si trovano nel seguente percorso:

   `/etc/workflow/launcher/`

   >[!NOTE]
   >
   >Se queste definizioni vengono modificate *utilizzo dell’interfaccia AEM*, i dettagli verranno copiati nelle nuove posizioni.

#### Posizioni - Script del flusso di lavoro {#locations-workflow-scripts}

Gli script di flusso di lavoro vengono inoltre memorizzati nell’archivio in base al tipo:

* Gli script di flusso di lavoro preconfigurati vengono mantenuti nel seguente percorso:

   `/libs/workflow/scripts/`

   >[!CAUTION]
   >
   >Non eseguire:
   >
   >* inserisci uno degli script di flusso di lavoro personalizzati in questa cartella
   >* modificare qualsiasi elemento in `/libs`

   >
   >Come qualsiasi modifica può essere sovrascritta al momento dell&#39;aggiornamento o durante l&#39;installazione di hotfix, cumulative fix pack o service pack.

* Gli script di flusso di lavoro personalizzati si trovano in:

   ```
   /apps/workflow/scripts/...
   ```

* Gli script di flusso di lavoro legacy vengono memorizzati nel seguente percorso:

   `/etc/workflow/scripts/`

#### Posizioni - Notifiche flusso di lavoro {#locations-workflow-notifications}

Le notifiche del flusso di lavoro vengono memorizzate anche nell’archivio in base al tipo:

* Le definizioni delle notifiche del flusso di lavoro preconfigurate vengono mantenute nel seguente percorso:

   `/libs/settings/workflow/notification/`

   >[!CAUTION]
   >
   >Non eseguire:
   >
   >* inserisci una delle definizioni di notifica del flusso di lavoro personalizzato in questa cartella
   >* modificare qualsiasi elemento in `/libs`

   >
   >Come qualsiasi modifica può essere sovrascritta al momento dell&#39;aggiornamento o durante l&#39;installazione di hotfix, cumulative fix pack o service pack.

* Le definizioni di notifiche di flusso di lavoro personalizzate sono disponibili in:

   ```
   /conf/global/settings/workflow/notification/...
   ```

   >[!NOTE]
   >
   >Se desideri sovrascrivere un testo di notifica di un flusso di lavoro, crea un percorso sovrapposto in:
   >
   >
   >`/conf/global/settings/workflow/notification/<path-under-libs>`

* Le definizioni delle notifiche del flusso di lavoro legacy vengono mantenute nel seguente percorso:

   `/etc/workflow/notification/`

### Sessioni di processo {#process-sessions}

Come in qualsiasi sviluppo personalizzato, si consiglia sempre di utilizzare una sessione utente quando possibile:

* per rispettare al meglio le linee guida sulla sicurezza
* per consentire al sistema di gestire l&#39;apertura e la chiusura della sessione

Quando si implementa un processo di flusso di lavoro:

* Viene fornita una sessione del flusso di lavoro che deve essere utilizzata a meno che non vi sia un motivo convincente per non farlo.
* Le nuove sessioni non devono essere create dai passaggi del flusso di lavoro, in quanto ciò causa incoerenze negli stati e possibili problemi di concorrenza nel motore del flusso di lavoro.
* Non devi acquisire una nuova sessione JCR dall&#39;interno di una fase del processo in un flusso di lavoro; devi adattare la sessione del flusso di lavoro fornita dall’API Process Step a una sessione jcr. Esempio:

```
public void execute(WorkItem item, WorkflowSession workflowSession, MetaDataMap args) throws WorkflowException {
        // to obtain a jcr session:
        javax.jcr.Session jcrSession = workflowSession.adaptTo(javax.jcr.Session.class);

        // to obtain a sling resource resolver:
        org.apache.sling.api.resource.ResourceResolver slingResourceResolver = workflowSession.adaptTo(org.apache.sling.api.resource.ResourceResolver.class);
```

Salvataggio di una sessione:

* All’interno di un processo di flusso di lavoro, se `WorkflowSession` viene utilizzato per modificare l&#39;archivio e non salvare esplicitamente la sessione - il flusso di lavoro salverà la sessione al termine.
* `Session.Save` non deve essere invocato dall’interno di un passaggio di flusso di lavoro:

   * si consiglia di adattare la sessione jcr del flusso di lavoro; then `save` non è necessario in quanto il motore del flusso di lavoro salva automaticamente la sessione una volta completata l’esecuzione del flusso di lavoro.
   * non è consigliato per un passaggio del processo creare la propria sessione jcr.

* Eliminando i risparmi non necessari, è possibile ridurre il sovraccarico e rendere quindi i flussi di lavoro più efficienti.

>[!CAUTION]
>
>Se, nonostante i consigli qui, crei una tua sessione jcr, allora dovrà essere salvato.

### Ridurre al minimo il numero/ambito dei moduli di avvio {#minimize-the-number-scope-of-launchers}

C&#39;è un ascoltatore che è responsabile di tutti [lanciatori di flussi di lavoro](/help/sites-administering/workflows-starting.md#workflows-launchers) registrati:

* Ascolterà i cambiamenti in tutti i percorsi specificati nelle proprietà globbing degli altri lanciatori.
* Quando un evento viene inviato, il motore del flusso di lavoro valuta ogni modulo di avvio per determinare se deve essere eseguito.

La creazione di un numero eccessivo di moduli di avvio rallenta il processo di valutazione.

La creazione di un percorso globbing nella directory principale dell’archivio su un singolo modulo di avvio causerebbe al motore del flusso di lavoro l’ascolto e la valutazione degli eventi di creazione/modifica per ogni nodo dell’archivio. Per questo motivo, si consiglia di creare solo lanciatori che sono necessari e di rendere il percorso globbing il più specifico possibile.

A causa dell’impatto di questi moduli di avvio sul comportamento del flusso di lavoro, può essere utile disattivare eventuali moduli di avvio pronti all’uso non in uso.

### Miglioramenti alla configurazione per i moduli di avvio {#configuration-enhancements-for-launchers}

L&#39;utente personalizzato [configurazione del modulo di avvio](/help/sites-administering/workflows-starting.md#workflows-launchers) è stato migliorato per supportare i seguenti elementi:

* Hanno più condizioni &quot;AND&quot; insieme.
* Avere condizioni OR in un’unica condizione.
* Disabilita/abilita i moduli di avvio in base all’abilitazione o meno di un flag di funzione.
* Supporta regex nelle condizioni di avvio.

### Non avviare flussi di lavoro da altri flussi di lavoro {#do-not-start-workflows-from-other-workflows}

I flussi di lavoro possono avere una notevole quantità di overhead, sia in termini di oggetti creati nella memoria che di nodi tracciati nel repository. Per questo motivo, è meglio che un flusso di lavoro esegua l’elaborazione all’interno di sé anziché avviare flussi di lavoro aggiuntivi.

Un esempio di questo potrebbe essere un flusso di lavoro che implementa un processo aziendale su un set di contenuti e poi lo attiva. È meglio creare un processo di flusso di lavoro personalizzato che attivi ciascuno di questi nodi, anziché avviare un **Attiva contenuto** modello per ciascuno dei nodi di contenuto da pubblicare. Questo approccio richiede un ulteriore lavoro di sviluppo, ma è più efficiente quando viene eseguito che avviare un&#39;istanza di flusso di lavoro separata per ogni attivazione.

Un altro esempio potrebbe essere un flusso di lavoro che elabora un certo numero di nodi, crea un pacchetto di flusso di lavoro, quindi attiva tale pacchetto. Invece di creare il pacchetto e quindi avviare un flusso di lavoro separato con il pacchetto come payload, puoi modificare il payload del flusso di lavoro nel passaggio che crea il pacchetto e quindi chiamare il passaggio per attivare il pacchetto all’interno dello stesso modello di flusso di lavoro.

### Avanzamento gestore {#handler-advance}

Quando si progetta un modello di flusso di lavoro è possibile abilitare l’avanzamento del gestore nei passaggi del flusso di lavoro. In alternativa, puoi aggiungere codice al passaggio del flusso di lavoro per determinare quale passaggio deve essere eseguito e quindi eseguirlo.

Si consiglia di utilizzare l&#39;avanzamento del gestore in quanto fornisce prestazioni migliori.

### Fasi del flusso di lavoro {#workflow-stages}

Puoi definire [fasi del flusso di lavoro](/help/sites-developing/workflows.md#workflow-stages), quindi assegna attività/passaggi a una specifica fase del flusso di lavoro.

Queste informazioni vengono utilizzate per visualizzare l&#39;avanzamento di un flusso di lavoro quando fai clic sul pulsante [**Informazioni sul flusso di lavoro** scheda di un elemento di lavoro **Inbox**](/help/sites-authoring/workflows-participating.md#opening-a-workflow-item-to-view-details-and-take-actions). È possibile modificare i modelli di flusso di lavoro esistenti per aggiungere aree di visualizzazione.

### Attiva passaggio del processo della pagina {#activate-page-process-step}

La **Attiva processo pagina** Il passaggio ti attiverà le pagine, ma non troverà automaticamente le risorse DAM di riferimento e le attiverà anche.

Tieni presente questo aspetto se intendi utilizzare questo passaggio come parte di un modello di flusso di lavoro.

### Considerazioni sull’aggiornamento {#upgrade-considerations}

Quando aggiorni l’istanza:

* prima di aggiornare un’istanza, assicurati che venga eseguito il backup di eventuali modelli di flusso di lavoro personalizzati.
* conferma che nessuno dei flussi di lavoro personalizzati è memorizzato in [posizione](#locations):

   * `/libs/settings/workflow/models/projects`

>[!NOTE]
>
>Vedi anche [Ristrutturazione dell’archivio in AEM 6.5](/help/sites-deploying/repository-restructuring.md).

## Strumenti di sistema {#system-tools}

Sono disponibili numerosi strumenti di sistema per il monitoraggio, la manutenzione e la risoluzione dei problemi dei flussi di lavoro. Tutti gli URL di esempio utilizzati di seguito `localhost:4502`, ma dovrebbe essere disponibile su qualsiasi istanza di authoring ( `<hostname>:<port>`).

### Console Sling Job Handling {#sling-job-handling-console}

`http://localhost:4502/system/console/slingevent`

La console Sling Job Handling mostra:

* Statistiche sullo stato dei lavori nel sistema dall&#39;ultimo riavvio.
* Inoltre, mostrerà le configurazioni per tutte le code di lavoro e fornirà un collegamento per modificarle nel gestore della configurazione.

### Strumento per il rapporto sui flussi di lavoro {#workflow-report-tool}

Lo strumento di reporting del flusso di lavoro viene rimosso nella versione 6.3 per evitare il degrado delle prestazioni.

### MBean delle operazioni di manutenzione del flusso di lavoro {#workflow-maintenance-operations-mbean}

`http://localhost:4502/system/console/jmx/com.adobe.granite.workflow:type=Maintenance`

La MBean di manutenzione del flusso di lavoro espone diverse utili routine di manutenzione, come l&#39;eliminazione dei flussi di lavoro completati e il recupero delle statistiche del flusso di lavoro.

## Ulteriori informazioni {#further-information}

Per ulteriori informazioni, consulta:

* [Utilizzo dei flussi di lavoro](/help/sites-authoring/workflows.md)
* [Amministrazione dei flussi di lavoro](/help/sites-administering/workflows.md)
* [Sviluppo ed estensione dei flussi di lavoro](/help/sites-developing/workflows.md)
* [Ottimizzazione delle prestazioni](/help/sites-deploying/configuring-performance.md)
