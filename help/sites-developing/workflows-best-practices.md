---
title: Best practice per i flussi di lavoro
seo-title: Best practice per i flussi di lavoro
description: 'null'
seo-description: 'null'
uuid: 79be4055-c2ef-428e-9054-103c6cfde1d2
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 0be8b88c-6f57-4dcc-ae11-77b378a2decd
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1922'
ht-degree: 0%

---


# Best practice del flusso di lavoro{#workflow-best-practices}

I flussi di lavoro consentono di automatizzare le attività di Adobe Experience Manager (AEM).

Spesso rappresentano una grande quantità di elaborazione che si verifica in un ambiente AEM, pertanto quando i passaggi di flusso di lavoro personalizzati non vengono scritti in base alle best practice, o i flussi di lavoro out-of-the-box non sono configurati per essere eseguiti nel modo più efficiente possibile, il sistema può risentirne.

È quindi vivamente consigliato pianificare con attenzione le implementazioni dei flussi di lavoro.

## Configurazione {#configuration}

Per la configurazione dei processi di workflow (personalizzati e/o out-of-the-box), è necessario tenere presenti alcuni aspetti.

### Flussi di lavoro transitori {#transient-workflows}

Per ottimizzare i carichi di caricamento elevati, è possibile definire un flusso di lavoro [transitorio](/help/sites-developing/workflows.md#transient-workflows).

Quando un flusso di lavoro è transitorio, i dati di runtime relativi ai passaggi di lavoro intermedi non vengono memorizzati nel JCR quando vengono eseguiti (le rappresentazioni di output sono ovviamente persistenti).

I vantaggi possono includere:

* Una riduzione del tempo di elaborazione del flusso di lavoro; fino al 10%.
* Ridurre significativamente la crescita del repository.
* Per eliminare i flussi di lavoro CRUD non sono necessari altri flussi di lavoro CRUD.
* Inoltre, riduce il numero di file TAR a dimensioni compatte.

>[!CAUTION]
>
>Se l&#39;azienda specifica di mantenere/archiviare i dati di runtime del flusso di lavoro a scopo di controllo, non attivare questa funzione.

### Ottimizzazione dei flussi di lavoro DAM {#tuning-dam-workflows}

Per le linee guida per l&#39;ottimizzazione delle prestazioni per i flussi di lavoro DAM, vedere la [ AEM Assets Performance Tuning Guide](/help/assets/performance-tuning-guidelines.md).

### Configurare il numero massimo di flussi di lavoro simultanei {#configure-the-maximum-number-of-concurrent-workflows}

AEM consentire l&#39;esecuzione simultanea di più thread del flusso di lavoro. Per impostazione predefinita, il numero di thread è configurato per la metà del numero di core del processore sul sistema.

Nei casi in cui i flussi di lavoro in esecuzione richiedono risorse di sistema, può essere necessario AEM utilizzare poco per altre attività, come il rendering dell’interfaccia utente di authoring. Di conseguenza, il sistema potrebbe risultare lento durante attività quali il caricamento di immagini in massa.

Per risolvere questo problema,  Adobe consiglia di configurare il numero di **Processi paralleli massimi** in modo che sia compreso tra la metà e i tre quarti del numero di core del processore presenti nel sistema. Ciò dovrebbe consentire al sistema di rimanere reattivo durante l&#39;elaborazione di tali flussi di lavoro.

Per configurare **Processi paralleli massimi**, potete:

* Configurare la **[configurazione OSGi](/help/sites-deploying/configuring-osgi.md)** dalla console Web AEM; per **Coda: Coda flusso di lavoro Granite** (una **configurazione della coda di lavoro Apache Sling**).

* Configurare la coda può essere dall&#39;opzione **Processi Sling** della console Web AEM; per **Configurazione coda di lavoro: Granite Workflow Queue**, in `http://localhost:4502/system/console/slingevent`.

È inoltre disponibile una configurazione separata per la **coda processi esterni del flusso di lavoro Granite**. Viene utilizzato per i processi di workflow che avviano file binari esterni, ad esempio **InDesign Server** o **Image Magick**.

### Configurare le singole code di processo {#configure-individual-job-queues}

In alcuni casi, è utile configurare le singole code di processo per controllare i thread simultanei o altre opzioni di coda su base individuale. È possibile aggiungere e configurare una singola coda dalla console Web tramite la fabbrica **Apache Sling Job Queue Configuration**. Per trovare l&#39;argomento appropriato da elencare, eseguite il modello del flusso di lavoro e cercatelo nella console **Sling Jobs**; ad esempio, in `http://localhost:4502/system/console/slingevent`.

È possibile aggiungere code di lavoro individuali anche per flussi di lavoro transitori.

### Configurare lo svuotamento del flusso di lavoro {#configure-workflow-purging}

In un&#39;installazione standard AEM una console di manutenzione in cui è possibile pianificare e configurare le attività di manutenzione giornaliere e settimanali; ad esempio, in:

`http://localhost:4502/libs/granite/operations/content/maintenance.html`

Per impostazione predefinita, la **Finestra di manutenzione settimanale** ha un&#39;attività **Rimozione flusso di lavoro**, ma questo deve essere configurato prima che venga eseguita. Per configurare le epurazioni del flusso di lavoro, nella console Web è necessario aggiungere una nuova **Adobe Granite Workflow Purge Configuration**.

Per ulteriori dettagli sulle attività di manutenzione in AEM, vedere il [Pannello operazioni](/help/sites-administering/operations-dashboard.md).

## Personalizzazione {#customization}

Quando si scrivono processi di flusso di lavoro personalizzati, è necessario tenere presenti alcuni aspetti.

### Posizioni {#locations}

Le definizioni di modelli di flusso di lavoro, avviatori, script e notifiche sono memorizzate nel repository in base al tipo; ovvero out-of-the-box, personalizzata, tra gli altri.

>[!NOTE]
>
>Vedere anche [Ristrutturazione repository in AEM 6.5](/help/sites-deploying/repository-restructuring.md).

#### Posizioni - Modelli di flussi di lavoro {#locations-workflow-models}

I modelli di flussi di lavoro vengono memorizzati nella directory archivio in base al tipo:

* Le progettazioni del flusso di lavoro pronte all’uso si trovano nel seguente percorso:

   `/libs/settings/workflow/models/`

   >[!CAUTION]
   >
   >Non eseguire:
   >
   >* inserire un modello di flusso di lavoro personalizzato in questa cartella
   >* modificare qualsiasi cosa in `/libs`

   >
   >Eventuali modifiche possono essere sovrascritte al momento dell&#39;aggiornamento o dell&#39;installazione di hotfix, pacchetti di correzione o Service Pack cumulativi.

* Le progettazioni di flussi di lavoro personalizzate si trovano in:

   ```
   /conf/global/settings/workflow/models/...
   ```

* Le progettazioni del flusso di lavoro runtime (sia predefinite che personalizzate) si trovano nel percorso seguente:

   `/var/workflow/models/`

* Le progettazioni di flussi di lavoro precedenti (sia in fase di progettazione che di runtime) si trovano nel seguente percorso:

   `/etc/workflow/models/`

   >[!NOTE]
   >
   >Se queste progettazioni vengono modificate *utilizzando l&#39;interfaccia AEM*, i dettagli verranno copiati nelle nuove posizioni.

#### Posizioni - Avviatori flusso di lavoro {#locations-workflow-launchers}

Le definizioni del modulo di avvio del flusso di lavoro vengono memorizzate anche nella directory archivio in base al tipo:

* Gli avviatori di workflow integrati si trovano nel seguente percorso:

   `/libs/settings/workflow/launcher/`

   >[!CAUTION]
   >
   >Non eseguire:
   >
   >* inserite in questa cartella eventuali avviatori di flussi di lavoro personalizzati
   >* modificare qualsiasi cosa in `/libs`

   >
   >Eventuali modifiche possono essere sovrascritte al momento dell&#39;aggiornamento o dell&#39;installazione di hotfix, pacchetti di correzione o Service Pack cumulativi.

* Gli avviatori di flussi di lavoro personalizzati si trovano in:

   ```
   /conf/global/settings/workflow/launcher/...
   ```

* I precedenti avviatori di flussi di lavoro si trovano nel seguente percorso:

   `/etc/workflow/launcher/`

   >[!NOTE]
   >
   >Se queste definizioni vengono modificate *utilizzando l&#39;interfaccia AEM*, i dettagli verranno copiati nelle nuove posizioni.

#### Posizioni - Script del flusso di lavoro {#locations-workflow-scripts}

Gli script del flusso di lavoro vengono inoltre memorizzati nell&#39;archivio in base al tipo:

* Gli script del flusso di lavoro forniti dall&#39;utente si trovano nel percorso seguente:

   `/libs/workflow/scripts/`

   >[!CAUTION]
   >
   >Non eseguire:
   >
   >* inserire uno script di flusso di lavoro personalizzato in questa cartella
   >* modificare qualsiasi cosa in `/libs`

   >
   >Eventuali modifiche possono essere sovrascritte al momento dell&#39;aggiornamento o dell&#39;installazione di hotfix, pacchetti di correzione o Service Pack cumulativi.

* Gli script di flusso di lavoro personalizzati si trovano in:

   ```
   /apps/workflow/scripts/...
   ```

* Gli script di flusso di lavoro legacy si trovano nel percorso seguente:

   `/etc/workflow/scripts/`

#### Posizioni - Notifiche flusso di lavoro {#locations-workflow-notifications}

Le notifiche del flusso di lavoro vengono memorizzate anche nella directory archivio in base al tipo:

* Le definizioni delle notifiche del flusso di lavoro pronte all&#39;uso si trovano nel percorso seguente:

   `/libs/settings/workflow/notification/`

   >[!CAUTION]
   >
   >Non eseguire:
   >
   >* inserire una delle definizioni di notifica del flusso di lavoro personalizzate in questa cartella
   >* modificare qualsiasi cosa in `/libs`

   >
   >Eventuali modifiche possono essere sovrascritte al momento dell&#39;aggiornamento o dell&#39;installazione di hotfix, pacchetti di correzione o Service Pack cumulativi.

* Le definizioni delle notifiche dei flussi di lavoro personalizzate sono memorizzate in:

   ```
   /conf/global/settings/workflow/notification/...
   ```

   >[!NOTE]
   >
   >Per sovrascrivere un testo di notifica di un flusso di lavoro, create un percorso sovrapposto in:
   >
   >
   >`/conf/global/settings/workflow/notification/<path-under-libs>`

* Le definizioni delle notifiche del flusso di lavoro legacy si trovano nel percorso seguente:

   `/etc/workflow/notification/`

### Sessioni di processo {#process-sessions}

Come in qualsiasi sviluppo personalizzato, si consiglia sempre di utilizzare una sessione utente quando possibile:

* per una migliore conformità alle linee guida sulla sicurezza
* per consentire al sistema di gestire l&#39;apertura e la chiusura della sessione

Durante l&#39;implementazione di un processo di workflow:

* Viene fornita una sessione del flusso di lavoro che deve essere utilizzata a meno che non vi sia un motivo convincente per non farlo.
* Le nuove sessioni non devono essere create dai passaggi del flusso di lavoro, in quanto ciò causa incoerenze negli stati e possibili problemi di concorrenza nel motore del flusso di lavoro.
* non acquisire una nuova sessione JCR da un passaggio di processo in un flusso di lavoro; devi adattare la sessione del flusso di lavoro fornita dall&#39;API Process Step a una sessione jcr. Esempio:

```
public void execute(WorkItem item, WorkflowSession workflowSession, MetaDataMap args) throws WorkflowException {
        // to obtain a jcr session:
        javax.jcr.Session jcrSession = workflowSession.adaptTo(javax.jcr.Session.class);

        // to obtain a sling resource resolver:
        org.apache.sling.api.resource.ResourceResolver slingResourceResolver = workflowSession.adaptTo(org.apache.sling.api.resource.ResourceResolver.class);
```

Salvataggio di una sessione:

* All&#39;interno di un processo di workflow, se la `WorkflowSession` viene utilizzata per modificare l&#39;archivio, non salvate in modo esplicito la sessione. Al termine, il flusso di lavoro salverà la sessione.
* `Session.Save` non devono essere richiamati da un passaggio di workflow:

   * si consiglia di adattare la sessione del flusso di lavoro jcr; quindi `save` non è necessario in quanto il motore del flusso di lavoro salva automaticamente la sessione al termine dell&#39;esecuzione del flusso di lavoro.
   * non è consigliato per un passaggio del processo creare una propria sessione jcr.

* Eliminando i risparmi non necessari, puoi ridurre il sovraccarico e rendere quindi i flussi di lavoro più efficienti.

>[!CAUTION]
>
>Se, nonostante le raccomandazioni qui, crei la tua sessione jcr, allora dovrà essere salvata.

### Ridurre al minimo il numero e l&#39;ambito di avviatori {#minimize-the-number-scope-of-launchers}

Esiste un listener responsabile per tutti i [avviatori di workflow](/help/sites-administering/workflows-starting.md#workflows-launchers) registrati:

* Ascolterà i cambiamenti in tutti i percorsi specificati nelle proprietà globbing degli altri lanciatori.
* Quando un evento viene inviato, il motore del flusso di lavoro valuterà ciascun avvio per determinare se deve essere eseguito.

La creazione di troppi avviatori causa un rallentamento del processo di valutazione.

La creazione di un percorso globbing alla radice del repository su un singolo avviatore causerebbe l&#39;ascolto e la valutazione degli eventi create/modified per ogni nodo del repository. Per questo motivo, si consiglia di creare solo i lanciatori necessari e di rendere il percorso globbing il più specifico possibile.

A causa dell&#39;impatto di questi avviatori sul comportamento del flusso di lavoro, può essere utile disattivare eventuali avviatori out-of-the-box non in uso.

### Miglioramenti della configurazione per gli avviatori {#configuration-enhancements-for-launchers}

La configurazione [di avvio ](/help/sites-administering/workflows-starting.md#workflows-launchers) personalizzata è stata migliorata per supportare quanto segue:

* Avere più condizioni &quot;AND&quot; insieme.
* Avere condizioni OR in un&#39;unica condizione.
* Disattiva/abilita gli avviatori in base all&#39;attivazione o meno di un flag di funzione.
* Supporto del regex nelle condizioni di avvio.

### Non avviare flussi di lavoro da altri flussi di lavoro {#do-not-start-workflows-from-other-workflows}

I flussi di lavoro possono avere un notevole carico di lavoro, sia in termini di oggetti creati nella memoria che di nodi tracciati nella directory archivio. Per questo motivo, è meglio che un flusso di lavoro esegua l&#39;elaborazione all&#39;interno di se stesso anziché avviare flussi di lavoro aggiuntivi.

Un esempio potrebbe essere un flusso di lavoro che implementa un processo aziendale su un set di contenuti e quindi attiva tale contenuto. È meglio creare un processo di flusso di lavoro personalizzato che attivi ciascuno di questi nodi, anziché avviare un modello **Activate Content** per ciascuno dei nodi di contenuto da pubblicare. Questo approccio richiede un ulteriore lavoro di sviluppo, ma è più efficiente se eseguito rispetto all&#39;avvio di un&#39;istanza di flusso di lavoro separata per ogni attivazione.

Un altro esempio potrebbe essere un flusso di lavoro che elabora un certo numero di nodi, crea un pacchetto di workflow e quindi attiva il pacchetto specificato. Invece di creare il pacchetto e avviare un flusso di lavoro separato con il pacchetto come payload, potete modificare il payload del flusso di lavoro nel passaggio che crea il pacchetto e quindi chiamare il passaggio per attivare il pacchetto all&#39;interno dello stesso modello di flusso di lavoro.

### Avanzamento gestore {#handler-advance}

Durante la progettazione di un modello di workflow è possibile abilitare l&#39;avanzamento del gestore nei passaggi del flusso di lavoro. In alternativa, puoi aggiungere del codice al passaggio del flusso di lavoro per determinare quale passaggio eseguire e quindi eseguirlo.

Si consiglia di utilizzare l&#39;avanzamento del gestore per ottenere prestazioni migliori.

### Fasi del flusso di lavoro {#workflow-stages}

È possibile definire [fasi del flusso di lavoro](/help/sites-developing/workflows.md#workflow-stages), quindi assegnare attività/passaggi a una fase del flusso di lavoro specifica.

Queste informazioni vengono utilizzate per visualizzare l&#39;avanzamento di un flusso di lavoro quando si fa clic sulla scheda [**Informazioni sul flusso di lavoro** di un elemento di lavoro dalla **Casella in entrata**](/help/sites-authoring/workflows-participating.md#opening-a-workflow-item-to-view-details-and-take-actions). I modelli di workflow esistenti possono essere modificati per aggiungere fasi.

### Attiva passo processo pagina {#activate-page-process-step}

Il passaggio **Attiva processo pagina** attiverà le pagine, ma non troverà automaticamente le risorse DAM di riferimento e non le attiverà.

Questo è qualcosa da tenere a mente se prevedete di utilizzare questo passaggio come parte di un modello di workflow.

### Considerazioni sull&#39;aggiornamento {#upgrade-considerations}

Durante l&#39;aggiornamento dell&#39;istanza:

* prima di aggiornare un&#39;istanza, verificate che venga eseguito il backup di eventuali modelli di flusso di lavoro personalizzati.
* verificate che nessuno dei flussi di lavoro personalizzati sia memorizzato nella cartella [location](#locations):

   * `/libs/settings/workflow/models/projects`

>[!NOTE]
>
>Vedere anche [Ristrutturazione repository in AEM 6.5](/help/sites-deploying/repository-restructuring.md).

## Strumenti di sistema {#system-tools}

Sono disponibili numerosi strumenti di sistema per il monitoraggio, la manutenzione e la risoluzione dei problemi. Tutti gli URL di esempio riportati di seguito utilizzano `localhost:4502`, ma devono essere disponibili in qualsiasi istanza di creazione ( `<hostname>:<port>`).

### Console Sling Job Handling {#sling-job-handling-console}

`http://localhost:4502/system/console/slingevent`

La console Sling Job Handling mostra:

* Statistiche sullo stato dei processi nel sistema dall’ultimo riavvio.
* Vengono inoltre visualizzate le configurazioni per tutte le code di processo e viene fornito un collegamento per modificarle in Gestione configurazione.

### Strumento Report flusso di lavoro {#workflow-report-tool}

Lo strumento di reporting del flusso di lavoro viene rimosso in 6.3 per evitare il deterioramento delle prestazioni.

### Operazioni di manutenzione del flusso di lavoro MBean {#workflow-maintenance-operations-mbean}

`http://localhost:4502/system/console/jmx/com.adobe.granite.workflow:type=Maintenance`

MBean di manutenzione del flusso di lavoro espone diverse utili procedure di manutenzione, come l&#39;eliminazione dei flussi di lavoro completati e il recupero delle statistiche del flusso di lavoro.

## Ulteriori informazioni {#further-information}

Per ulteriori informazioni, consulta:

* [Utilizzo dei flussi di lavoro](/help/sites-authoring/workflows.md)
* [Amministrazione dei flussi di lavoro](/help/sites-administering/workflows.md)
* [Sviluppo ed estensione dei flussi di lavoro](/help/sites-developing/workflows.md)
* [Ottimizzazione delle prestazioni](/help/sites-deploying/configuring-performance.md)