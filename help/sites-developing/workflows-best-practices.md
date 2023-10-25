---
title: Best practice per i flussi di lavoro
seo-title: Workflow Best Practices
description: Scopri le best practice per l’utilizzo dei flussi di lavoro in Adobe Experience Manager.
seo-description: null
uuid: 79be4055-c2ef-428e-9054-103c6cfde1d2
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 0be8b88c-6f57-4dcc-ae11-77b378a2decd
exl-id: 14775476-6fe5-4583-8ab5-b55fef892174
source-git-commit: b703f356f9475eeeafb1d5408c650d9c6971a804
workflow-type: tm+mt
source-wordcount: '1929'
ht-degree: 1%

---

# Best practice per i flussi di lavoro{#workflow-best-practices}

I flussi di lavoro consentono di automatizzare le attività di Adobe Experience Manager (AEM).

Spesso rappresentano una grande quantità di elaborazione che si verifica in un ambiente AEM, quindi quando i passaggi del flusso di lavoro personalizzati non vengono scritti in base alle best practice o i flussi di lavoro preconfigurati non sono configurati per essere eseguiti nel modo più efficiente possibile, il sistema può risentirne.

Pertanto, si consiglia vivamente di pianificare con attenzione le implementazioni dei flussi di lavoro.

## Configurazione {#configuration}

Durante la configurazione dei processi del flusso di lavoro (personalizzati e/o preconfigurati), è necessario tenere presente alcuni aspetti.

### Flussi di lavoro transitori {#transient-workflows}

Per ottimizzare i carichi di acquisizione elevati puoi definire una [flusso di lavoro come transitorio](/help/sites-developing/workflows.md#transient-workflows).

Quando un flusso di lavoro è transitorio, i dati di runtime relativi ai passaggi di lavoro intermedi non vengono memorizzati nel JCR quando vengono eseguiti (le rappresentazioni di output vengono mantenute, ovviamente).

I vantaggi includono:

* Riduzione del tempo di elaborazione del flusso di lavoro, fino al 10%.
* Riduzione significativa della crescita dell&#39;archivio.
* Non sono necessari altri flussi di lavoro CRUD per l’eliminazione.
* Inoltre, riduce il numero di file TAR da compattare.

>[!CAUTION]
>
>Se l’azienda richiede la persistenza o l’archiviazione dei dati runtime del flusso di lavoro a scopo di audit, non abilitare questa funzione.

### Ottimizzazione dei flussi di lavoro DAM {#tuning-dam-workflows}

Per le linee guida per l’ottimizzazione delle prestazioni per i flussi di lavoro DAM, vedi [Guida all’ottimizzazione delle prestazioni di AEM Assets](/help/assets/performance-tuning-guidelines.md).

### Configurare il numero massimo di flussi di lavoro simultanei {#configure-the-maximum-number-of-concurrent-workflows}

L’AEM può consentire l’esecuzione simultanea di più thread di flusso di lavoro. Per impostazione predefinita, il numero di thread è configurato in modo da essere la metà del numero di core del processore presenti sul sistema.

Nei casi in cui i flussi di lavoro in esecuzione richiedono risorse di sistema, questo può significare che l’AEM non può utilizzare molto per altre attività, come il rendering dell’interfaccia utente di authoring. Di conseguenza, il sistema potrebbe risultare lento durante attività quali il caricamento di immagini in massa.

Per risolvere questo problema, l’Adobe consiglia di configurare il numero di **Numero massimo processi paralleli** tra la metà e i tre quarti del numero di core del processore presenti nel sistema. Questo dovrebbe consentire al sistema di mantenere una capacità sufficiente per rispondere durante l’elaborazione di questi flussi di lavoro.

Per configurare **Numero massimo processi paralleli**, puoi effettuare le seguenti operazioni:

* Configurare **[Configurazione OSGi](/help/sites-deploying/configuring-osgi.md)** dalla console web dell’AEM; per **Coda: coda del flusso di lavoro Granite** (an **Configurazione coda processi Apache Sling**).

* Configurare la coda può da **Processi Sling** della console web AEM; per **Configurazione coda processi: coda del flusso di lavoro Granite**, in corrispondenza di `http://localhost:4502/system/console/slingevent`.

Inoltre, è disponibile una configurazione separata per **Coda processo processo esterno flusso di lavoro Granite**. Viene utilizzato per i processi del flusso di lavoro che avviano i file binari esterni, ad esempio **InDesign Server** o **Image Magick**.

### Configurare singole code di processi {#configure-individual-job-queues}

In alcuni casi è utile configurare singole code di job per controllare thread simultanei o altre opzioni di coda su base di job individuale. È possibile aggiungere e configurare una singola coda dalla console Web tramite **Configurazione coda processi Apache Sling** fabbrica. Per trovare l’argomento appropriato da elencare, esegui il modello del flusso di lavoro e cercalo in **Processi Sling** console; ad esempio, in `http://localhost:4502/system/console/slingevent`.

È possibile aggiungere singole code di processi anche per flussi di lavoro transitori.

### Configurare la rimozione dei flussi di lavoro {#configure-workflow-purging}

In un’installazione standard, l’AEM fornisce una console di manutenzione in cui è possibile pianificare e configurare le attività di manutenzione giornaliere e settimanali; ad esempio, all’indirizzo:

`http://localhost:4502/libs/granite/operations/content/maintenance.html`

Per impostazione predefinita, il **Finestra di manutenzione settimanale** ha un **Svuotamento flusso di lavoro** ma deve essere configurato prima che venga eseguito. Per configurare le eliminazioni del flusso di lavoro, è necessario **Adobe configurazione eliminazione flusso di lavoro Granite** devono essere aggiunti nella console Web.

Per maggiori dettagli sulle attività di manutenzione nell&#39;AEM, vedi [Dashboard operazioni](/help/sites-administering/operations-dashboard.md).

## Personalizzazione {#customization}

Durante la scrittura di processi di flusso di lavoro personalizzati, è necessario tenere presenti alcuni aspetti.

### Posizioni {#locations}

Le definizioni di modelli di flusso di lavoro, moduli di avvio, script e notifiche vengono conservate nell’archivio in base al tipo, tra cui preconfigurata, personalizzata.

>[!NOTE]
>
>Vedi anche [Ristrutturazione dell’archivio in AEM 6.5](/help/sites-deploying/repository-restructuring.md).

#### Posizioni - Modelli di flusso di lavoro {#locations-workflow-models}

I modelli di flusso di lavoro vengono memorizzati nell’archivio in base al tipo:

* Le progettazioni predefinite dei flussi di lavoro si trovano nel seguente percorso:

  `/libs/settings/workflow/models/`

  >[!CAUTION]
  >
  >Non:
  >
  >* inserisci uno dei modelli di flusso di lavoro personalizzati in questa cartella
  >* modificare qualsiasi elemento in `/libs`
  >
  >Poiché eventuali modifiche possono essere sovrascritte durante l&#39;aggiornamento o l&#39;installazione di hotfix, Cumulative Fix Pack o Service Pack.

* Le progettazioni dei flussi di lavoro personalizzati si trovano in:

  ```
  /conf/global/settings/workflow/models/...
  ```

* Le progettazioni dei flussi di lavoro in fase di esecuzione (sia pronte all’uso che personalizzate) si trovano nel seguente percorso:

  `/var/workflow/models/`

* Le progettazioni dei flussi di lavoro legacy (sia in fase di progettazione che in fase di runtime) si trovano nel seguente percorso:

  `/etc/workflow/models/`

  >[!NOTE]
  >
  >Se questi progetti vengono modificati *utilizzo dell’interfaccia utente dell’AEM*, quindi i dettagli verranno copiati nelle nuove posizioni.

#### Posizioni - Moduli di avvio dei flussi di lavoro {#locations-workflow-launchers}

Anche le definizioni del modulo di avvio dei flussi di lavoro vengono memorizzate nell’archivio in base al tipo:

* I moduli di avvio dei flussi di lavoro preconfigurati si trovano nel seguente percorso:

  `/libs/settings/workflow/launcher/`

  >[!CAUTION]
  >
  >Non:
  >
  >* inserisci uno dei moduli di avvio dei flussi di lavoro personalizzati in questa cartella
  >* modificare qualsiasi elemento in `/libs`
  >
  >Poiché eventuali modifiche possono essere sovrascritte durante l&#39;aggiornamento o l&#39;installazione di hotfix, Cumulative Fix Pack o Service Pack.

* I moduli di avvio dei flussi di lavoro personalizzati si trovano in:

  ```
  /conf/global/settings/workflow/launcher/...
  ```

* I moduli di avvio dei flussi di lavoro legacy si trovano nel seguente percorso:

  `/etc/workflow/launcher/`

  >[!NOTE]
  >
  >Se queste definizioni vengono modificate *utilizzo dell’interfaccia utente dell’AEM*, quindi i dettagli verranno copiati nelle nuove posizioni.

#### Posizioni - Script del flusso di lavoro {#locations-workflow-scripts}

Anche gli script di flusso di lavoro vengono memorizzati nell’archivio in base al tipo:

* Gli script di flusso di lavoro predefiniti sono disponibili nel seguente percorso:

  `/libs/workflow/scripts/`

  >[!CAUTION]
  >
  >Non:
  >
  >* inserisci uno degli script di flusso di lavoro personalizzati in questa cartella
  >* modificare qualsiasi elemento in `/libs`
  >
  >Poiché eventuali modifiche possono essere sovrascritte durante l&#39;aggiornamento o l&#39;installazione di hotfix, Cumulative Fix Pack o Service Pack.

* Gli script di flusso di lavoro personalizzati si trovano in:

  ```
  /apps/workflow/scripts/...
  ```

* Gli script di flusso di lavoro legacy si trovano nel percorso seguente:

  `/etc/workflow/scripts/`

#### Posizioni - Notifiche flusso di lavoro {#locations-workflow-notifications}

Le notifiche del flusso di lavoro vengono memorizzate anche nell’archivio in base al tipo:

* Le definizioni predefinite delle notifiche dei flussi di lavoro si trovano nel seguente percorso:

  `/libs/settings/workflow/notification/`

  >[!CAUTION]
  >
  >Non:
  >
  >* inserisci una delle definizioni di notifica del flusso di lavoro personalizzato in questa cartella
  >* modificare qualsiasi elemento in `/libs`
  >
  >Poiché eventuali modifiche possono essere sovrascritte durante l&#39;aggiornamento o l&#39;installazione di hotfix, Cumulative Fix Pack o Service Pack.

* Le definizioni di notifica del flusso di lavoro personalizzate si trovano in:

  ```
  /conf/global/settings/workflow/notification/...
  ```

  >[!NOTE]
  >
  >Se desideri ignorare il testo di una notifica del flusso di lavoro, crea un percorso sovrapposto in:
  >
  >
  >`/conf/global/settings/workflow/notification/<path-under-libs>`

* Le definizioni delle notifiche dei flussi di lavoro legacy si trovano nel percorso seguente:

  `/etc/workflow/notification/`

### Sessioni di elaborazione {#process-sessions}

Come in qualsiasi sviluppo personalizzato, si consiglia sempre di utilizzare la sessione di un utente quando possibile:

* per aderire in modo ottimale alle linee guida sulla sicurezza
* per consentire al sistema di gestire l&#39;apertura e la chiusura della sessione

Quando si implementa un processo di workflow:

* Verrà fornita una sessione di flusso di lavoro che deve essere utilizzata a meno che non vi siano motivi validi per non farlo.
* Non è consigliabile creare nuove sessioni dai passaggi del flusso di lavoro, in quanto ciò causa incoerenze negli stati e possibili problemi di concorrenza nel motore del flusso di lavoro.
* Non devi acquisire una nuova sessione JCR dall’interno di un passaggio del processo in un flusso di lavoro; devi adattare la sessione del flusso di lavoro fornita dall’API della fase del processo a una sessione JCR. Ad esempio:

```
public void execute(WorkItem item, WorkflowSession workflowSession, MetaDataMap args) throws WorkflowException {
        // to obtain a jcr session:
        javax.jcr.Session jcrSession = workflowSession.adaptTo(javax.jcr.Session.class);

        // to obtain a sling resource resolver:
        org.apache.sling.api.resource.ResourceResolver slingResourceResolver = workflowSession.adaptTo(org.apache.sling.api.resource.ResourceResolver.class);
```

Salvataggio di una sessione

* All’interno di un processo del flusso di lavoro, se `WorkflowSession` viene utilizzato per modificare l’archivio e non salvare esplicitamente la sessione; al termine, il flusso di lavoro salverà la sessione.
* `Session.Save` non deve essere chiamato dall&#39;interno di un passaggio del flusso di lavoro:

   * si consiglia di adattare la sessione jcr del flusso di lavoro; quindi `save` non è necessario in quanto il motore del flusso di lavoro salva la sessione automaticamente al termine dell’esecuzione del flusso di lavoro.
   * non è consigliabile che una fase del processo crei una propria sessione jcr.

* Eliminando i risparmi non necessari, è possibile ridurre il sovraccarico e quindi rendere più efficienti i flussi di lavoro.

>[!CAUTION]
>
>Se, nonostante i consigli qui riportati, crei una tua sessione JCR, allora sarà necessario salvarla.

### Riduci al minimo il numero e l&#39;ambito dei moduli di avvio {#minimize-the-number-scope-of-launchers}

Esiste un solo ascoltatore responsabile di tutte le [moduli di avvio dei flussi di lavoro](/help/sites-administering/workflows-starting.md#workflows-launchers) che sono registrati:

* Ascolterà le modifiche in tutti i percorsi specificati nelle proprietà globbing degli altri moduli di avvio.
* Quando viene inviato un evento, il motore del flusso di lavoro valuta quindi ogni modulo di avvio per determinare se deve essere eseguito.

Se si creano troppi moduli di avvio, il processo di valutazione verrà eseguito più lentamente.

La creazione di un percorso globbing nella directory principale dell’archivio su un singolo modulo di avvio fa in modo che il motore del flusso di lavoro ascolti e valuti gli eventi di creazione/modifica per ogni nodo dell’archivio. Per questo motivo, si consiglia di creare solo i moduli di avvio necessari e di rendere il percorso di globbing il più specifico possibile.

A causa dell’impatto di questi moduli di avvio sul comportamento del flusso di lavoro, può essere utile disabilitare anche tutti i moduli di avvio predefiniti che non sono in uso.

### Miglioramenti alla configurazione dei moduli di avvio {#configuration-enhancements-for-launchers}

La personalizzazione [configurazione modulo di avvio](/help/sites-administering/workflows-starting.md#workflows-launchers) è stato migliorato per supportare:

* Avere più condizioni &quot;AND&quot; insieme.
* Hanno condizioni OR all’interno di una singola condizione.
* Disabilita/abilita i moduli di avvio a seconda che un flag di funzione sia abilitato o disabilitato.
* Supporta regex in condizioni di avvio.

### Non avviare flussi di lavoro da altri flussi di lavoro {#do-not-start-workflows-from-other-workflows}

I flussi di lavoro possono comportare un sovraccarico significativo, sia in termini di oggetti creati in memoria che di nodi tracciati nell’archivio. Per questo motivo, è preferibile che un flusso di lavoro esegua l’elaborazione al suo interno, anziché avviare flussi di lavoro aggiuntivi.

Un esempio potrebbe essere un flusso di lavoro che implementa un processo aziendale su un set di contenuti e quindi attiva tali contenuti. È meglio creare un processo di flusso di lavoro personalizzato che attivi ciascuno di questi nodi, piuttosto che avviare un **Attiva contenuto** modello per ciascuno dei nodi di contenuto da pubblicare. Questo approccio richiederà un ulteriore lavoro di sviluppo, ma è più efficiente quando viene eseguito rispetto all’avvio di un’istanza di flusso di lavoro separata per ogni attivazione.

Un altro esempio potrebbe essere un flusso di lavoro che elabora una serie di nodi, crea un pacchetto di flusso di lavoro, quindi attiva tale pacchetto. Invece di creare il pacchetto e quindi avviare un flusso di lavoro separato con il pacchetto come payload, puoi modificare il payload del flusso di lavoro nel passaggio che crea il pacchetto e quindi chiamare il passaggio per attivare il pacchetto all’interno dello stesso modello di flusso di lavoro.

### Avanzamento gestore {#handler-advance}

Durante la progettazione di un modello di flusso di lavoro, puoi abilitare l’avanzamento del gestore nei passaggi del flusso di lavoro. In alternativa, puoi aggiungere codice al passaggio del flusso di lavoro per determinare quale passaggio deve essere eseguito successivamente, quindi eseguirlo.

Si consiglia di utilizzare l’avanzamento del gestore, in quanto offre prestazioni migliori.

### Fasi flusso di lavoro {#workflow-stages}

Puoi definire [fasi del flusso di lavoro](/help/sites-developing/workflows.md#workflow-stages), quindi assegna attività/passaggi a una fase specifica del flusso di lavoro.

Queste informazioni vengono utilizzate per visualizzare l’avanzamento di un flusso di lavoro quando fai clic sul pulsante [**Informazioni flusso di lavoro** scheda di un elemento di lavoro da **Casella in entrata**](/help/sites-authoring/workflows-participating.md#opening-a-workflow-item-to-view-details-and-take-actions). I modelli di flusso di lavoro esistenti possono essere modificati per aggiungere fasi.

### Passaggio di attivazione processo pagina {#activate-page-process-step}

Il **Processo di attivazione pagina** Questo passaggio attiva automaticamente le pagine, ma non trova e attiva automaticamente le risorse DAM di riferimento.

Questo è un aspetto da tenere presente se intendi utilizzare questo passaggio come parte di un modello di flusso di lavoro.

### Considerazioni sull’aggiornamento {#upgrade-considerations}

Durante l’aggiornamento dell’istanza:

* assicurati che sia stato eseguito il backup di tutti i modelli di flusso di lavoro personalizzati prima di aggiornare un’istanza.
* conferma che nessuno dei flussi di lavoro personalizzati è memorizzato in [posizione](#locations):

   * `/libs/settings/workflow/models/projects`

>[!NOTE]
>
>Vedi anche [Ristrutturazione dell’archivio in AEM 6.5](/help/sites-deploying/repository-restructuring.md).

## Strumenti di sistema {#system-tools}

Sono disponibili molti strumenti di sistema per il monitoraggio, la manutenzione e la risoluzione dei problemi dei flussi di lavoro. Tutti gli URL di esempio seguenti utilizzano `localhost:4502`, ma deve essere disponibile su qualsiasi istanza di authoring ( `<hostname>:<port>`).

### Console per la gestione dei processi Sling {#sling-job-handling-console}

`http://localhost:4502/system/console/slingevent`

La console Gestione processi Sling mostrerà:

* Statistiche sullo stato dei processi nel sistema dall&#39;ultimo riavvio.
* Mostrerà inoltre le configurazioni per tutte le code di processi e fornirà un collegamento per modificarle nella gestione della configurazione.

### Strumento Report di flusso di lavoro {#workflow-report-tool}

È in corso la rimozione dello strumento di reporting per flussi di lavoro nella versione 6.3 per evitare il deterioramento delle prestazioni.

### MBean operazioni manutenzione flusso di lavoro {#workflow-maintenance-operations-mbean}

`http://localhost:4502/system/console/jmx/com.adobe.granite.workflow:type=Maintenance`

Il MBean di manutenzione del flusso di lavoro espone diverse utili routine di manutenzione, come la rimozione dei flussi di lavoro completati e il recupero delle statistiche del flusso di lavoro.

## Ulteriori informazioni {#further-information}

Per ulteriori informazioni, consulta:

* [Utilizzo dei flussi di lavoro](/help/sites-authoring/workflows.md)
* [Amministrazione dei flussi di lavoro](/help/sites-administering/workflows.md)
* [Sviluppo ed estensione dei flussi di lavoro](/help/sites-developing/workflows.md)
* [Ottimizzazione delle prestazioni](/help/sites-deploying/configuring-performance.md)
