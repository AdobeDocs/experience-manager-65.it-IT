---
title: Monitoraggio e manutenzione dell’istanza AEM
seo-title: Monitoraggio e manutenzione dell’istanza AEM
description: Scopri come monitorare AEM.
seo-description: Scopri come monitorare AEM.
uuid: 14466552-5c92-4730-a427-85675a2b121c
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 5d2364b7-4497-4f8b-85ef-6e780bfb8c36
docset: aem65
translation-type: tm+mt
source-git-commit: 9f22cb618d487a2b02dc17149d11b81a9e9e27be
workflow-type: tm+mt
source-wordcount: '5895'
ht-degree: 1%

---


# Monitoraggio e manutenzione dell’istanza AEM{#monitoring-and-maintaining-your-aem-instance}

Dopo l&#39;implementazione delle istanze AEM, sarà necessario eseguire determinate attività per monitorare e mantenere il funzionamento, le prestazioni e l&#39;integrità.

Un fattore chiave in questo caso è che per riconoscere i potenziali problemi è necessario sapere come si presentano e si comportano i sistemi in condizioni normali. Ciò è meglio monitorando il sistema e raccogliendo informazioni in un determinato periodo di tempo.

| Seleziona | Considerazioni | Commento/Azioni |
|---|---|---|
| piano di backup. |  | Scopri come [eseguire il backup dell’istanza](/help/sites-deploying/monitoring-and-maintaining.md#backups). |
| Piano di ripristino di emergenza. | Linee guida aziendali sul disaster recovery. |  |
| Per segnalare i problemi è disponibile un sistema di monitoraggio degli errori. | Ad esempio, [bugzilla](https://www.bugzilla.org/), [jira](https://www.atlassian.com/software/jira/)o uno dei tanti altri. |  |
| I file system vengono monitorati. | Se lo spazio disponibile su disco è insufficiente, il repository CRX si blocca. e riprenderà quando sarà disponibile lo spazio. | &quot; `*ERROR* LowDiskSpaceBlocker`&quot; i messaggi possono essere visualizzati nel file di registro quando lo spazio disponibile diventa insufficiente. |
| [I file](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files) di registro vengono monitorati. |  |  |
| Il monitoraggio del sistema viene eseguito (in modo costante) in background. | CPU, memoria, disco e utilizzo della rete. Ad esempio, iostat / vmstat / perfmon. | I dati registrati vengono visualizzati e possono essere utilizzati per tenere traccia dei problemi di prestazioni. Anche i dati non elaborati sono accessibili. |
| [AEM prestazioni sono sotto controllo](/help/sites-deploying/monitoring-and-maintaining.md#monitoring-performance). | Inclusi i contatori delle [richieste](/help/sites-deploying/monitoring-and-maintaining.md#request-counters) per monitorare i livelli di traffico. | Se si riscontra una perdita significativa, o a lungo termine, dei risultati ottenuti, occorre effettuare un&#39;indagine approfondita. |
| Stai monitorando i tuoi agenti [di](/help/sites-deploying/monitoring-and-maintaining.md#monitoring-your-replication-agents)replica. |  |  |
| Elimina regolarmente le istanze del flusso di lavoro. | Dimensioni dell&#39;archivio e prestazioni del flusso di lavoro. | Consultate Sgancio [regolare delle istanze](/help/sites-administering/workflows-administering.md#regular-purging-of-workflow-instances)del flusso di lavoro. |

## Backup {#backups}

È buona prassi effettuare backup di:

* Installazione del software - prima/dopo modifiche significative nella configurazione
* Contenuto custodito all&#39;interno del repository - regolarmente

La vostra azienda avrà probabilmente una politica di backup da seguire, considerazioni aggiuntive su cosa eseguire il backup e quando includere:

* quanto sono critici il sistema e i dati.
* la frequenza con cui vengono apportate modifiche al software o ai dati.
* volume dei dati; la capacità può occasionalmente essere un problema, così come il tempo necessario per eseguire il backup.
* se è possibile eseguire il backup mentre gli utenti sono online; e, se possibile, qual è l&#39;impatto sulle prestazioni.
* la distribuzione geografica degli utilizzatori; ad esempio, quando è il momento migliore per eseguire il backup (per ridurre al minimo l&#39;impatto)?
* la politica di disaster recovery; esistono linee guida sulle aree in cui i dati di backup devono essere memorizzati (ad esempio fuori sede, supporto specifico, ecc.).

Spesso un backup completo viene eseguito a intervalli regolari (ad esempio, giornalieri, settimanali o mensili), con backup incrementali intermedi (ad esempio orari, giornalieri o settimanali).

>[!CAUTION]
>
>Durante l&#39;implementazione dei backup delle istanze di produzione, *è necessario* eseguire dei test per verificare che il backup possa essere ripristinato correttamente.
>
>Senza questo, il backup è potenzialmente inutile (scenario peggiore).

>[!NOTE]
>
>Per ulteriori informazioni sulle prestazioni di backup, consulta la sezione Prestazioni [di](/help/sites-deploying/configuring-performance.md#backup-performance) backup.

### Backup dell&#39;installazione software {#backing-up-your-software-installation}

Dopo l&#39;installazione, o modifiche significative nella configurazione, eseguire un backup dell&#39;installazione software.

A questo scopo, è necessario [eseguire il backup dell&#39;intero repository](#backing-up-your-repository) , quindi:

1. AEM.
1. Eseguire il backup dell&#39;intero `<cq-installation-dir>` file system.

>[!CAUTION]
>
>Se si utilizza un server applicazioni di terze parti, è possibile che altre cartelle si trovino in un percorso diverso e che sia necessario eseguire il backup. Per [informazioni sull&#39;installazione dei server delle applicazioni, vedere Installazione di AEM con un server](/help/sites-deploying/application-server-install.md) applicazioni. [](/content/docs/en/aem/6-3/deploy/installing.md#installing adobe experience manager with a application server)

>[!CAUTION]
>
>È supportato il backup incrementale dell&#39;archivio dati del file; quando si utilizza il backup incrementale per altri componenti (come l&#39;indice Lucene), assicurarsi che anche i file eliminati siano contrassegnati come eliminati nel backup.

>[!NOTE]
>
>Il mirroring del disco può essere utilizzato anche come meccanismo di backup.

### Backup del repository {#backing-up-your-repository}

La sezione [Backup e ripristino](/help/sites-administering/backup-and-restore.md) della documentazione CRX illustra tutti i problemi relativi ai backup del repository CRX.

Per informazioni dettagliate sulla creazione di un backup online &quot;hot&quot;, consultate [Creazione di un backup](/help/sites-administering/backup-and-restore.md#online-backup)online.

## Rimozione delle versioni {#version-purging}

Lo strumento Versioni **di** eliminazione è destinato a eliminare le versioni di un nodo o di una gerarchia di nodi nel repository. Lo scopo principale è quello di ridurre le dimensioni del repository rimuovendo le versioni precedenti dei nodi.

Questa sezione descrive le operazioni di manutenzione relative alla funzione di controllo delle versioni di AEM. Lo strumento **Svuota versione** è destinato ad eliminare le versioni di un nodo o di una gerarchia di nodi nel repository. Lo scopo principale è quello di ridurre le dimensioni del repository rimuovendo le versioni precedenti dei nodi.

### Panoramica {#overview}

Lo strumento **Rimuovi versioni** è disponibile nella console **[](/help/sites-administering/tools-consoles.md) Strumenti** in Gestione **versioni** o direttamente all’indirizzo:

`https://<server>:<port>/etc/versioning/purge.html`

![screen_shot_2012-03-15at14418pm](assets/screen_shot_2012-03-15at14418pm.png)

**Percorso** iniziale Un percorso assoluto sul quale eseguire la rimozione. Per selezionare il Percorso iniziale, fare clic sul Navigator della struttura della directory archivio.

**Ricorsivo** Quando si eliminano i dati è possibile scegliere se eseguire l&#39;operazione su un nodo o su un&#39;intera gerarchia selezionando Ricorsivo. Nell&#39;ultimo caso, il percorso specificato definisce il nodo principale della gerarchia.

**Numero massimo di versioni per mantenere** il numero massimo di versioni da mantenere per un nodo. Quando questo numero supera questo valore, vengono eliminate le versioni precedenti.

**Età** massima versione L&#39;età massima della versione di un nodo. Quando l&#39;età di una versione supera questo valore, viene eliminata.

**Prova** a secco Poiché la rimozione di versioni del contenuto è definita e non può essere ripristinata senza il ripristino di un backup, lo strumento Rimuovi versioni fornisce una modalità di esecuzione a secco che consente di visualizzare in anteprima le versioni eliminate. Per avviare una prova del processo di eliminazione, fare clic su Prova.

**Elimina** Avvia la rimozione delle versioni sul nodo definito dal Percorso iniziale.

### Rimozione delle versioni di un sito Web {#purging-versions-of-a-web-site}

Per eliminare le versioni di un sito Web, procedere come segue:

1. Passate alla **[console](/help/sites-administering/tools-consoles.md)** Strumenti **, selezionate** Controllo versioni **e fate doppio clic su** **Elimina versioni.**
1. Impostate il percorso iniziale del contenuto da rimuovere (ad es. `/content/geometrixx-outdoors`).

   * Per eliminare solo il nodo definito dal percorso, deselezionare **Ricorsivo**.
   * Se si desidera eliminare il nodo definito dal percorso e dai relativi discendenti, selezionare **Ricorsivo**.

1. Impostate il numero massimo di versioni (per ciascun nodo) che desiderate mantenere. Lasciate vuoto per non utilizzare questa impostazione.

1. Impostate l&#39;età massima della versione in giorni (per ogni nodo) che desiderate mantenere. Lasciate vuoto per non utilizzare questa impostazione.

1. Fate clic su **Prova** per visualizzare un&#39;anteprima delle operazioni di eliminazione.
1. Fate clic su **Elimina** per avviare il processo.

>[!CAUTION]
>
>I nodi eliminati non possono essere ripristinati senza il ripristino della directory archivio. Si dovrebbe prendersi cura della configurazione, quindi si consiglia di eseguire sempre una prova a secco prima di rimuovere.

### Analisi della console {#analyzing-the-console}

I processi **Prova** e **Svuota** elencano tutti i nodi elaborati. Durante il processo, un nodo può avere uno dei seguenti stati:

* `ignore (not versionnable)`: il nodo non supporta il controllo delle versioni e viene ignorato durante il processo.

* `ignore (no version)`: il nodo non dispone di alcuna versione e viene ignorato durante il processo.

* `retained`: il nodo non viene eliminato.
* `purged`: il nodo viene eliminato.

Inoltre, la console fornisce informazioni utili sulle versioni:

* `V 1.0`: il numero di versione.
* `V 1.0.1`*: la stella indica che la versione è quella corrente.

* `Thu Mar 15 2012 08:37:32 GMT+0100`: la data della versione.

Nell&#39;esempio seguente:

* Le **[!DNL Shirts]** versioni vengono eliminate perché la loro età è superiore a 2 giorni.
* Le **[!DNL Tonga Fashions!]** versioni vengono eliminate perché il loro numero è maggiore di 5.

![global_version_screenshot](assets/global_version_screenshot.png)

## Utilizzo dei record di controllo e dei file di registro {#working-with-audit-records-and-log-files}

I record di controllo e i file di registro relativi a Adobe Experience Manager (AEM) possono essere trovati in varie posizioni. Di seguito viene fornita una panoramica di ciò che è possibile trovare.

### Utilizzo dei registri {#working-with-logs}

AEM WCM registra i registri dettagliati. Dopo aver decompresso e avviato Quickstart, puoi trovare i registri in:

* `<cq-installation-dir>/crx-quickstart/logs/`

* `<cq-installation-dir>/crx-quickstart/repository/`

#### Rotazione del file di registro {#log-file-rotation}

La rotazione del file di registro si riferisce al processo che limita la crescita del file creando periodicamente un nuovo file. In AEM, un file di registro chiamato `error.log` verrà ruotato una volta al giorno in base alle regole specificate:

* Il `error.log` file viene rinominato in base al pattern {Original_filename} `.yyyy-MM-dd`. Ad esempio, l’11 luglio 2010, il file di registro corrente viene rinominato `error.log-2010-07-10`, quindi `error.og` viene creato un nuovo file.

* I file di registro precedenti non vengono eliminati, quindi è responsabilità dell&#39;utente pulire i vecchi file di registro periodicamente per limitare l&#39;utilizzo del disco.

>[!NOTE]
>
>Se si aggiorna l&#39;installazione di AEM, si noti che eventuali file di registro esistenti non più utilizzati da AEM rimarranno sul disco. Potete rimuoverli senza rischi. Tutte le nuove voci di registro verranno scritte nei nuovi file di registro.

### Ricerca dei file di registro {#finding-the-log-files}

Diversi file di registro si trovano sul file server in cui avete installato AEM:

* `<cq-installation-dir>/crx-quickstart/logs`

   * `access.log`
Tutte le richieste di accesso a AEM WCM e al repository sono registrate qui.

   * `audit.log`
Le azioni di moderazione sono registrate qui.

   * `error.log`
I messaggi di errore (con vari livelli di gravità) sono registrati qui.

   * [ `ImageServer-<PortId>-yyyy>-<mm>-<dd>.log`](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-serving-api/image-serving-api/config-admin/server-logging/c-image-server-log.html)
Questo registro viene utilizzato solo se [!DNL Dynamic Media] è abilitato. Fornisce informazioni statistiche e analitiche utilizzate per analizzare il comportamento del processo ImageServer interno.

   * `request.log`
Ogni richiesta di accesso è registrata qui insieme alla risposta.

   * [ `s7access-<yyyy>-<mm>-<dd>.log`](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-serving-api/image-serving-api/config-admin/server-logging/c-access-log.html)
Questo registro viene utilizzato solo se [!DNL Dynamic Media] è abilitato. Il registro di accesso s7access registra ogni richiesta effettuata [!DNL Dynamic Media] attraverso `/is/image` e `/is/content`.

   * `stderr.log`
Contiene i messaggi di errore, di nuovo con diversi livelli di gravità, generati durante l&#39;avvio. Per impostazione predefinita, il livello di registro è impostato su 
`Warning` ( `WARN`)

   * `stdout.log`
Contiene i messaggi di registrazione che indicano gli eventi durante l&#39;avvio.

   * `upgrade.log`
Fornisce un registro di tutte le operazioni di aggiornamento in esecuzione dalla 
`com.day.compat.codeupgrade` e `com.adobe.cq.upgradesexecutor` pacchetti.

* `<cq-installation-dir>/crx-quickstart/repository`

   * `revision.log`
Informazioni sulla registrazione delle revisioni.

>[!NOTE]
>
>I file di registro ImageServer e s7access non sono inclusi nel pacchetto **Download Full **generato dalla pagina **system/console/status-Bundlelist*. Per motivi di assistenza, in caso di [!DNL Dynamic Media] problemi, aggiungete i registri ImageServer e s7access quando contattate l’Assistenza clienti.

### Attivazione del livello di registro DEBUG {#activating-the-debug-log-level}

Il livello di registro predefinito (Configurazione[registrazione](/help/sites-deploying/osgi-configuration-settings.md#apacheslingloggingconfiguration)Apache Sling) è Informazioni, quindi i messaggi di debug non vengono registrati.

Per attivare il livello di registro di debug per un logger, impostare la proprietà `org.apache.sling.commons.log.level` su debug nell&#39;archivio. Ad esempio, per configurare `/libs/sling/config/org.apache.sling.commons.log.LogManager` la registrazione Sling Apache [globale](/help/sites-deploying/osgi-configuration-settings.md#apacheslingloggingconfiguration).

>[!CAUTION]
>
>Non lasciare il registro a livello di registro di debug più lungo del necessario, in quanto genera molte voci di registro, consumando quindi risorse.

Una riga nel file di debug in genere inizia con DEBUG, quindi fornisce il livello di registro, l&#39;azione del programma di installazione e il messaggio di registro. Esempio:

```shell
DEBUG 3 WebApp Panel: WebApp successfully deployed
```

I livelli di registro sono i seguenti:

| 0 | Errore irreversibile | L&#39;azione non è riuscita e il programma di installazione non può proseguire. |
|---|---|---|
| 1 | Errore | L&#39;azione non è riuscita. L&#39;installazione continua, ma una parte di AEM WCM non è stata installata correttamente e non funzionerà. |
| 2 | Avvertenza | L&#39;azione è riuscita ma ha incontrato dei problemi. AEM WCM potrebbe funzionare o meno correttamente. |
| 3 | Informazioni | L&#39;azione è riuscita. |

### Creare un file di registro personalizzato {#create-a-custom-log-file}

>[!NOTE]
>
>When working with Adobe Experience Manager there are several methods of managing the configuration settings for such services; see [Configuring OSGi](/help/sites-deploying/configuring-osgi.md) for more details and the recommended practices.

In alcune circostanze può essere utile creare un file di registro personalizzato con un livello di registro diverso. È possibile eseguire questa operazione nella directory archivio:

1. Se non già esistente, create una nuova cartella di configurazione ( `sling:Folder`) per il progetto `/apps/<project-name>/config`.
1. In `/apps/<project-name>/config`, create un nodo per la nuova configurazione [del log di registrazione](/help/sites-deploying/osgi-configuration-settings.md#apacheslingloggingloggerconfigurationfactoryconfiguration)Apache Sling:

   * Nome: `org.apache.sling.commons.log.LogManager.factory.config-<identifier>` (in quanto si tratta di un logger)

      Dove `<identifier>` viene sostituito da testo libero che è necessario immettere per identificare l’istanza (non è possibile omettere tali informazioni).

      Esempio, `org.apache.sling.commons.log.LogManager.factory.config-MINE`

   * Tipo: `sling:OsgiConfig`
   >[!NOTE]
   >
   >Anche se non è un requisito tecnico, è consigliabile rendere `<identifier>` unico.

1. Imposta le seguenti proprietà su questo nodo:

   * Nome: `org.apache.sling.commons.log.file`

      Tipo: Stringa

      Valore: specifica il file di registro; ad esempio, `logs/myLogFile.log`

   * Nome: `org.apache.sling.commons.log.names`

      Tipo: Stringa[] (String + Multi)

      Valore: specificare i servizi OSGi per i quali il logger deve registrare i messaggi; ad esempio, tutti i seguenti elementi:

      * `org.apache.sling`
      * `org.apache.felix`
      * `com.day`
   * Nome: `org.apache.sling.commons.log.level`

      Tipo: Stringa

      Valore: specificare il livello di registro richiesto ( `debug`, `info`, `warn` o `error`); ad esempio `debug`

   * Configurate gli altri parametri come richiesto:

      * Nome: `org.apache.sling.commons.log.pattern`

         Tipo: `String`

         Valore: specificare il pattern del messaggio di registro come richiesto; ad esempio,

         `{0,date,dd.MM.yyyy HH:mm:ss.SSS} *{4}* [{2}] {3} {5}`
   >[!NOTE]
   >
   >`org.apache.sling.commons.log.pattern` supporta fino a sei argomenti.
   >
   >{0} Il timestamp del tipo `java.util.Date`
   >
   >{1} il marcatore di registro
   >
   >{2} il nome del thread corrente
   >
   >{3} il nome del logger
   >
   >{4} il livello di registro
   >
   >{5} il messaggio di registro
   >
   >Se la chiamata di registro include una traccia `Throwable` di stack, questa viene aggiunta al messaggio.

   >[!CAUTION]
   >
   >org.apache.sling.commons.log.names deve avere un valore.

   >[!NOTE]
   >
   >I percorsi di scrittura del registro sono relativi alla `crx-quickstart` posizione.
   >
   >Pertanto, un file di registro specificato come:
   >
   >`logs/thelog.log`
   >
   >scrive in:
   >
   >`<cq-installation-dir>/crx-quickstart/logs/thelog.log`.
   >
   >E un file di registro specificato come:
   >
   >`../logs/thelog.log`
   >
   >scrive in una directory:
   >
   >`<cq-installation-dir>/logs/`\
   >(cioè accanto a `<cq-installation-dir>/crx-quickstart/`)

1. Questo passaggio è necessario solo quando è necessario un nuovo Writer (ad es. con una configurazione diversa da quella del Writer predefinito).

   >[!CAUTION]
   >
   >È necessaria una nuova configurazione per l&#39;utente che esegue l&#39;accesso solo se l&#39;impostazione predefinita esistente non è adatta.
   >
   >Se non è configurato alcun Writer esplicito, il sistema genererà automaticamente un Writer implicito in base all&#39;impostazione predefinita.

   In `/apps/<project-name>/config`, create un nodo per la nuova configurazione [del processo di registrazione](/help/sites-deploying/osgi-configuration-settings.md#apacheslingloggingwriterconfigurationfactoryconfiguration)Apache Sling:

   * Nome: `org.apache.sling.commons.log.LogManager.factory.writer-<identifier>` (in quanto si tratta di uno scrittore)

      Come con il Logger, `<identifier>` viene sostituito da testo libero che è necessario immettere per identificare l’istanza (non è possibile omettere tali informazioni). Esempio, `org.apache.sling.commons.log.LogManager.factory.writer-MINE`

   * Tipo: `sling:OsgiConfig`
   >[!NOTE]
   >
   >Anche se non è un requisito tecnico, è consigliabile rendere `<identifier>` unico.

   Imposta le seguenti proprietà su questo nodo:

   * Nome: `org.apache.sling.commons.log.file`

      Tipo: `String`

      Valore: specificare il file di registro in modo che corrisponda al file specificato nel logger;

      in questo esempio, `../logs/myLogFile.log`.

   * Configurate gli altri parametri come richiesto:

      * Nome: `org.apache.sling.commons.log.file.number`

         Tipo: `Long`

         Valore: specificare il numero di file di registro da conservare; ad esempio, `5`

      * Nome: `org.apache.sling.commons.log.file.size`

         Tipo: `String`

         Valore: specificare come necessario per controllare la rotazione del file per dimensione/data; ad esempio, `'.'yyyy-MM-dd`
   >[!NOTE]
   >
   >`org.apache.sling.commons.log.file.size` controlla la rotazione del file di registro impostando:
   >
   >* una dimensione massima del file
   >* una pianificazione di ora/data

   >
   >per indicare quando verrà creato un nuovo file (e il file esistente verrà rinominato in base al pattern del nome).
   >
   >* È possibile specificare un limite di dimensioni con un numero. Se non viene fornito alcun indicatore di dimensione, questo viene considerato come il numero di byte, oppure è possibile aggiungere uno degli indicatori di dimensione - `KB`, `MB`o `GB` (il caso viene ignorato).
   >* È possibile specificare come `java.util.SimpleDateFormat` pattern una pianificazione di ora/data. Definisce il periodo di tempo dopo il quale il file verrà ruotato; inoltre il suffisso aggiunto al file ruotato (per l’identificazione).

   >
   >Il valore predefinito è &#39;.&#39;yyyy-MM-dd (per la rotazione giornaliera del registro).
   >
   >Ad esempio, a mezzanotte del 20 gennaio 2010 (o quando il primo messaggio di registro dopo tale data sarà preciso), ../logs/error.log verrà rinominato in ../logs/error.log.2010-01-20. La registrazione per il 21 gennaio verrà restituita a (un nuovo e vuoto) ../logs/error.log finché non viene eseguito il rollback al cambio successivo del giorno.
   >
   >| `'.'yyyy-MM` | Rotazione all&#39;inizio di ogni mese |
   >|---|---|
   >| `'.'yyyy-ww` | Rotazione al primo giorno di ogni settimana (a seconda delle impostazioni internazionali). |
   >| `'.'yyyy-MM-dd` | Rotazione a mezzanotte ogni giorno. |
   >| `'.'yyyy-MM-dd-a` | Rotazione a mezzanotte e a mezzogiorno di ogni giorno. |
   >| `'.'yyyy-MM-dd-HH` | Rotazione nella parte superiore di ogni ora. |
   >| `'.'yyyy-MM-dd-HH-mm` | Rotazione all&#39;inizio di ogni minuto. |
   >
   >Nota: Quando si specifica un&#39;ora/data:
   > 1. È necessario &quot;escape&quot; testo letterale all&#39;interno di una coppia di virgolette singole (&#39; &#39;);
      >
      >     
      per evitare che alcuni caratteri vengano interpretati come lettere del pattern.
      >
      >  
   1. Utilizzate solo i caratteri consentiti per un nome di file valido in qualsiasi punto dell&#39;opzione.


1. Leggere il nuovo file di registro con lo strumento scelto.

   Il file di registro creato da questo esempio sarà `../crx-quickstart/logs/myLogFile.log`.

La console Felix fornisce inoltre informazioni sul supporto dei log Sling in `../system/console/slinglog`; ad esempio `https://localhost:4502/system/console/slinglog`.

### Ricerca dei record di controllo {#finding-the-audit-records}

I record di audit sono tenuti per fornire un record di chi ha fatto cosa e quando. Vengono generati record di controllo diversi per gli eventi WCM AEM e OSGi.

#### AEM record di controllo WCM visualizzati durante l’authoring delle pagine {#aem-wcm-audit-records-shown-when-page-authoring}

1. Aprite una pagina.
1. Dalla barra laterale è possibile selezionare la scheda con l&#39;icona a forma di lucchetto, quindi fare doppio clic su **Audit Log...**
1. Viene aperta una nuova finestra che mostra l&#39;elenco dei record di controllo per la pagina corrente.

   ![screen_shot_2012-02-02at43601pm](assets/screen_shot_2012-02-02at43601pm.png)

1. Fare clic su **OK** per chiudere la finestra.

#### AEM dei record di controllo WCM nell&#39;archivio {#aem-wcm-auditing-records-within-the-repository}

All&#39;interno della `/var/audit` cartella, i record di controllo vengono conservati in base alla risorsa. È possibile eseguire il drill-down fino a visualizzare i singoli record e le informazioni che contengono.

Queste voci contengono le stesse informazioni visualizzate durante la modifica di una pagina.

#### Record di audit OSGi dalla console Web {#osgi-audit-records-from-the-web-console}

Gli eventi OSGi generano inoltre record di controllo che possono essere visualizzati dalla scheda Stato **di** configurazione > scheda File **di** registro nella AEM console Web:

![screen_shot_2012-02-13at50346pm](assets/screen_shot_2012-02-13at50346pm.png)

## Monitoraggio degli agenti di replica {#monitoring-your-replication-agents}

È possibile monitorare le code [di](/help/sites-deploying/replication.md) replica per rilevare quando una coda è inattiva o bloccata, il che potrebbe a sua volta indicare un problema con un&#39;istanza di pubblicazione o con un sistema esterno:

* tutte le code richieste sono abilitate?
* sono ancora necessarie code per i disabili?
* tutte `enabled` le code devono avere lo stato `idle` o `active`, che indicano il normale funzionamento; non devono essere presenti code `blocked`, che è spesso un segno di problemi da parte dei ricevitori.

* se le dimensioni della coda aumentano nel tempo, potrebbe indicare una coda bloccata.

Per monitorare un agente di replica:

1. Accedere alla scheda **Strumenti** in AEM.
1. Fate clic su **Replica**.
1. Fare doppio clic sul collegamento agli agenti per l&#39;ambiente appropriato (il riquadro a sinistra o a destra); ad esempio **Agenti sull’autore**.

   Nella finestra visualizzata viene visualizzata una panoramica di tutti gli agenti di replica per l’ambiente di authoring, inclusi il target e lo stato.

1. Fate clic sul nome agente appropriato (collegamento) per visualizzare informazioni dettagliate su tale agente:

   ![chlimage_1](assets/chlimage_1.jpeg)

   È possibile:

   * Verificare se l&#39;agente è abilitato.
   * Visualizzare la destinazione di qualsiasi replica.
   * Verificare se la coda di replica è attualmente attiva (abilitata).
   * Verificare se sono presenti elementi nella coda.
   * **Aggiorna** o **Cancella** per aggiornare la visualizzazione delle voci della coda; questo consente di vedere gli elementi entrare e uscire dalla coda.

   * **Visualizzare il registro** per accedere al registro di eventuali azioni dell&#39;agente di replica.
   * **Verificare la connessione** all&#39;istanza di destinazione.
   * **Se necessario, forza il tentativo** su qualsiasi elemento della coda.

   >[!CAUTION]
   >
   >Non utilizzate il collegamento &quot;Test Connection&quot; per la replica inversa in uscita in un&#39;istanza pubblicata.
   >
   >Se viene eseguito un test di replica per una coda in uscita, tutti gli elementi che sono più vecchi della replica di test verranno rielaborati con ogni replica inversa.
   >
   >Se tali elementi esistono già in una coda, possono essere trovati con la seguente query XPath JCR e devono essere rimossi.
   >
   >`/jcr:root/var/replication/outbox//*[@cq:repActionType='TEST']`

È inoltre possibile sviluppare una soluzione per rilevare tutti gli agenti di replica (situati sotto `/etc/replication/author` o `/etc/replication/publish`), quindi controllare lo stato dell&#39;agente ( `enabled`, `disabled`) e la coda sottostante ( `active`, `idle`, `blocked`).

## Prestazioni di monitoraggio {#monitoring-performance}

[Ottimizzazione](/help/sites-deploying/configuring-performance.md) delle prestazioni è un processo interattivo che viene messo a fuoco durante lo sviluppo. Dopo la distribuzione viene in genere rivisto dopo specifici intervalli o eventi.

I metodi utilizzati per la raccolta di informazioni per l&#39;ottimizzazione possono essere utilizzati anche per il monitoraggio continuo.

>[!NOTE]
>
>È inoltre possibile verificare [le configurazioni specifiche disponibili per migliorare le prestazioni](/help/sites-deploying/configuring-performance.md#configuring-for-performance) .

Di seguito sono elencati i problemi comuni di prestazioni che si verificano, insieme alle proposte su come individuarli e contrastarli.

| Area | Sintomi | Per aumentare la capacità... | Per ridurre il volume... |
|---|---|---|---|
| Client | Utilizzo CPU client elevato. | Installare una CPU client con prestazioni più elevate. | Semplificare il layout (HTML). |
|  | Utilizzo CPU server insufficiente. | Eseguire l&#39;aggiornamento a un browser più veloce. | Miglioramento della cache lato client. |
|  | Alcuni clienti veloci, un po&#39; lenti. |  |  |
| Server |  |  |  |
| Rete | Utilizzo della CPU basso sia su server che su client. | Rimuovere eventuali colli di bottiglia della rete. | Migliorate/ottimizzate la configurazione della cache client. |
|  | La navigazione locale sul server è (relativamente) veloce. | Aumento della larghezza di banda della rete. | Riducete il peso delle pagine Web (ad es. meno immagini, HTML ottimizzato). |
| Web-server | L&#39;utilizzo della CPU sul server Web è elevato. | Cluster dei server Web. | Ridurre gli hit per pagina (visita). |
|  |  | Utilizzare un sistema hardware di bilanciamento del carico. |  |
| Applicazione | L&#39;utilizzo della CPU del server è elevato. | Cluster delle istanze AEM. | Cercare ed eliminare i cani della CPU e della memoria (usare la revisione del codice, l&#39;output dei tempi, ecc.). |
|  | Consumo di memoria elevato. |  | Miglioramento della memorizzazione nella cache a tutti i livelli. |
|  | Tempi di risposta ridotti. |  | Ottimizzare modelli e componenti (ad esempio struttura, logica). |
| Archivio |  |  |  |
| Cache |  |  |  |

I problemi di prestazioni possono derivare da una serie di cause che non hanno nulla a che fare con il sito Web, tra cui rallentamenti temporanei nella velocità di connessione, il carico della CPU e molti altri.

Può anche avere un impatto su tutti i visitatori, o solo su un sottoinsieme di essi.

Tutte queste informazioni devono essere ottenute, ordinate e analizzate prima di poter ottimizzare le prestazioni generali o risolvere problemi specifici.

* Prima di un problema di prestazioni:

   * raccogliere il maggior numero possibile di informazioni per sviluppare una buona conoscenza del sistema in circostanze normali

* In caso di problemi di prestazioni:

   * provare a replicarlo con uno (o preferibilmente più) browser web standard, su un client diverso che si sa che ha buone prestazioni generali e/o sul server stesso (se possibile)
   * verificare se qualcosa (correlato al sistema) è cambiato entro uno spazio temporale appropriato e se una di queste modifiche potrebbe avere avuto un impatto sulle prestazioni
   * fate domande come:

      * il problema si verifica solo in momenti specifici?
      * il problema si verifica solo su pagine specifiche?
      * le altre richieste sono interessate?
   * raccogliere il maggior numero possibile di informazioni da confrontare con la vostra conoscenza del sistema in circostanze normali:


### Strumenti per il monitoraggio e l&#39;analisi delle prestazioni {#tools-for-monitoring-and-analyzing-performance}

Di seguito viene fornita una breve panoramica di alcuni degli strumenti disponibili per monitorare e analizzare le prestazioni.

Alcuni di questi dipenderanno dal sistema operativo in uso.

<table>
 <tbody>
  <tr>
   <td>Strumento</td>
   <td>Utilizzato per analizzare...</td>
   <td>Utilizzo / Ulteriori informazioni...</td>
  </tr>
  <tr>
   <td>request.log</td>
   <td>Tempi di risposta e concorrenza.</td>
   <td><a href="#interpreting-the-request-log">Interpretazione di request.log</a>.</td>
  </tr>
  <tr>
   <td>truss/strass</td>
   <td>Caricamenti pagina</td>
   <td><p>Comandi Unix/Linux per tracciare chiamate di sistema e segnali. Impostare il livello di registro su <code>INFO</code>.</p> <p>Analizzare il numero di caricamenti di pagina per richiesta, quali pagine, ecc.</p> </td>
  </tr>
  <tr>
   <td>Fanelli di filettatura</td>
   <td>Osservare i thread JVM. Identificare i conteggi, le serrature e i corridori lunghi.</td>
   <td><p>A seconda del sistema operativo:<br /> - Unix/Linux: <code>kill -QUIT &lt;<em>pid</em>&gt;</code><br /> - Windows (modalità console): Ctrl-Break<br /> </p> <p>Sono disponibili anche strumenti di analisi, ad esempio <a href="https://java.net/projects/tda/">TDA</a>.<br /> </p> </td>
  </tr>
  <tr>
   <td>Cassetti heap</td>
   <td>Problemi di memoria esauriti che provocano prestazioni lente.</td>
   <td><p>Aggiungi:<br /> <code>-XX:+HeapDumpOnOutOfMemoryError</code><br /> nella chiamata Java a AEM.</p> <p>Consulta la Guida alla <a href="https://java.sun.com/javase/6/webnotes/trouble/TSG-VM/html/clopts.html#gbzrr">risoluzione dei problemi per Java SE 6 con HotSpot VM</a>.</p> </td>
  </tr>
  <tr>
   <td>Chiamate di sistema</td>
   <td>Identificare i problemi di temporizzazione.</td>
   <td><p>Le chiamate a <code>System.currentTimeMillis()</code> or <code>com.day.util</code>.Timing vengono utilizzate per generare marche temporali dal codice o tramite commenti <a href="#html-comments"></a>HTML.</p> <p><strong>Nota:</strong> Devono essere attuate in modo da poter essere attivate o disattivate secondo necessità; quando un sistema funziona senza problemi, l'onere della raccolta delle statistiche non sarà necessario.</p> </td>
  </tr>
  <tr>
   <td>Apache Bench</td>
   <td>Identificare le perdite di memoria, analizzare in modo selettivo il tempo di risposta.</td>
   <td><p>utilizzo di base:</p> <p><code>ab -k -n &lt;<em>requests</em>&gt; -c &lt;<em>concurrency</em>&gt; &lt;<em>url</em>&gt;</code></p> <p>Per maggiori informazioni, consulta <a href="#apache-bench">Apache Bench</a> e la pagina <a href="https://httpd.apache.org/docs/2.2/programs/ab.html">man</a> ab.</p> </td>
  </tr>
  <tr>
   <td>Analisi di ricerca</td>
   <td> </td>
   <td>Eseguire query di ricerca offline, identificare il tempo di risposta della query, verificare e confermare il set di risultati.<br /> </td>
  </tr>
  <tr>
   <td>JMeter</td>
   <td>Test di carico e di funzionamento.</td>
   <td><a href="https://jakarta.apache.org/jmeter/">https://jakarta.apache.org/jmeter/</a></td>
  </tr>
  <tr>
   <td>JProfiler</td>
   <td>Profiling approfondito della CPU e della memoria.</td>
   <td><a href="https://www.ej-technologies.com/">https://www.ej-technologies.com/</a></td>
  </tr>
  <tr>
   <td>JConsole</td>
   <td>Osservare le metriche e i thread JVM.</td>
   <td><p>Utilizzo: jconsole</p> <p>Consulta <a href="https://java.sun.com/developer/technicalArticles/J2SE/jconsole.html">jconsole</a> e <a href="#monitoring-performance-using-jconsole">Monitoring Performance utilizzando JConsole</a>.</p> <p><strong>Nota:</strong> Con JDK 1.6, JConsole è estensibile con i plug-in; ad esempio, Top o TDA (Thread Dump Analyzer).</p> </td>
  </tr>
  <tr>
   <td>Java VisualVM</td>
   <td>Osservare le metriche JVM, i thread, la memoria e il profiling.</td>
   <td><p>Utilizzo: jvisualvm o visualvm<br /> </p> <p>Vedere <a href="https://java.sun.com/javase/6/docs/technotes/tools/share/jvisualvm.html">jvisualvm</a>, <a href="https://visualvm.dev.java.net/">visualvm</a> e <a href="#monitoring-performance-using-j-visualvm">Monitoring Performance utilizzando (J)VisualVM</a>.</p> <p><strong>Nota:</strong> Con JDK 1.6, VisualVM è estensibile con i plug-in.</p> </td>
  </tr>
  <tr>
   <td>truss/strass, lsof</td>
   <td>Approfondimenti di chiamata e analisi del processo del kernel (Unix).</td>
   <td>Comandi Unix/Linux.</td>
  </tr>
  <tr>
   <td>Statistiche di temporizzazione</td>
   <td>Consultate le statistiche sui tempi per il rendering della pagina.</td>
   <td><p>Per visualizzare le statistiche sui tempi di rendering della pagina, potete usare <strong>Ctrl+Maiusc+U</strong> insieme a <code>?debugClientLibs=true</code> un’impostazione nell’URL.</p> </td>
  </tr>
  <tr>
   <td>Strumento di profilazione CPU e memoria<br /> </td>
   <td><a href="#interpreting-the-request-log">Utilizzato per l'analisi di richieste lente durante lo sviluppo</a>.</td>
   <td>Ad esempio, <a href="https://www.yourkit.com/">YourKit</a>.</td>
  </tr>
  <tr>
   <td><a href="#information-collection">Raccolta informazioni</a></td>
   <td>Lo stato dell’installazione in corso.</td>
   <td>Conoscere il più possibile l'installazione può anche aiutarti a tenere traccia di ciò che potrebbe aver causato un cambiamento nelle prestazioni e se queste modifiche sono giustificate. Queste metriche devono essere raccolte a intervalli regolari per poter vedere facilmente cambiamenti significativi.</td>
  </tr>
 </tbody>
</table>

### Interpretazione di request.log {#interpreting-the-request-log}

Questo file registra le informazioni di base su ogni richiesta effettuata per AEM. Da queste preziose conclusioni si possono trarre.

L&#39; `request.log` offerta offre un modo integrato per vedere quanto tempo le richieste richiedono. A scopo di sviluppo è utile per `tail -f` il `request.log` e guardare per tempi di risposta lenti. Per analizzare un numero maggiore `request.log` consigliamo l&#39; [utilizzo di `rlog.jar` cui è possibile ordinare e filtrare i tempi](#using-rlog-jar-to-find-requests-with-long-duration-times)di risposta.

Si consiglia di isolare le pagine &quot;lente&quot; dal `request.log`pannello, quindi di sintonizzarle singolarmente per ottenere prestazioni migliori. In genere questo viene fatto includendo le metriche delle prestazioni per componente o utilizzando uno strumento di profiling delle prestazioni come ` [yourkit](https://www.yourkit.com/)`.

#### Monitoraggio del traffico sul sito Web {#monitoring-traffic-on-your-website}

Il registro delle richieste registra ogni richiesta effettuata, insieme alla risposta ricevuta:

```xml
09:43:41 [66] -> GET /author/y.html HTTP/1.1
09:43:41 [66] <- 200 text/html 797ms
```

Se si sommano tutte le voci di GET entro un periodo specifico (ad esempio per diversi periodi di 24 ore), è possibile inserire nel sito Web delle istruzioni relative al traffico medio.

#### Monitoraggio dei tempi di risposta con request.log {#monitoring-response-times-with-the-request-log}

Un buon punto di partenza per l&#39;analisi delle prestazioni è il registro delle richieste:

`<cq-installation-dir>/crx-quickstart/logs/request.log`

Il registro si presenta come segue (le righe vengono abbreviate per semplicità):

```xml
31/Mar/2009:11:32:57 +0200 [379] -> GET /path/x HTTP/1.1
31/Mar/2009:11:32:57 +0200 [379] <- 200 text/html 33ms
31/Mar/2009:11:33:17 +0200 [380] -> GET /path/y HTTP/1.1
31/Mar/2009:11:33:17 +0200 [380] <- 200 application/json 39ms
```

Questo registro ha una riga per richiesta o risposta:

* Data in cui è stata effettuata ogni richiesta o risposta.
* Il numero della richiesta, tra parentesi quadre. Questo numero corrisponde alla richiesta e alla risposta.
* Una freccia che indica se si tratta di una richiesta (freccia rivolta verso destra) o di una risposta (freccia verso sinistra).
* Per le richieste, la riga contiene:

   * il metodo (in genere, GET, HEAD o POST)
   * la pagina richiesta
   * il protocollo

* Per le risposte, la riga contiene:

   * il codice di stato (200 significa &quot;successo&quot;, 404 significa &quot;pagina non trovata&quot;
   * il tipo MIME
   * il tempo di risposta

Utilizzando script di piccole dimensioni, è possibile estrarre le informazioni richieste dal file di registro e assemblare le statistiche desiderate. Da questi elementi potete vedere quali pagine o tipi di pagine sono lenti e se le prestazioni complessive sono soddisfacenti.

#### Monitoraggio dei tempi di risposta della ricerca con request.log {#monitoring-search-response-times-with-the-request-log}

Le richieste di ricerca sono registrate anche nel file di registro:

```xml
31/Mar/2009:11:35:34 +0200 [338] -> GET /author/playground/en/tools/search.html?query=dilbert&size=5&dispenc=utf-8 HTTP/1.1
31/Mar/2009:11:35:34 +0200 [338] <- 200 text/html 1562ms
```

Come sopra, potete utilizzare gli script per estrarre le informazioni rilevanti e generare statistiche.

Tuttavia, una volta determinato il tempo di risposta, potrebbe essere necessario analizzare il motivo per cui la richiesta prende il tempo necessario e cosa può essere fatto per migliorare la risposta.

#### Monitoraggio del numero e dell’impatto degli utenti simultanei {#monitoring-the-number-and-impact-of-concurrent-users}

Anche in questo caso, `request.log` è possibile monitorare la concorrenza e la reazione del sistema.

Devono essere eseguiti test per determinare quanti utenti simultanei il sistema può gestire prima che venga visto un impatto negativo. Anche in questo caso gli script possono essere utilizzati per estrarre i risultati dal file di registro:

* monitorare il numero di richieste effettuate entro un periodo di tempo specifico, ad esempio un minuto
* sottoporre a test gli effetti di un numero specifico di utenti che fanno tutte le stesse richieste allo stesso tempo (il più vicino possibile); Ad esempio, 30 utenti fanno clic su **Salva** contemporaneamente.

```xml
31/Mar/2009:11:45:29 +0200 [333] -> GET /author/libs/Personalize/content/statics.close.gif HTTP/1.1
31/Mar/2009:11:45:29 +0200 [334] -> GET /author/libs/Personalize/content/statics.detach.gif HTTP/1.1
31/Mar/2009:11:45:30 +0200 [335] -> GET /author/libs/CFC/content/imgs/logo.rZMNURccynWcTpCxyuBNiTCoiBMmw000.default.gif HTTP/1.1
31/Mar/2009:11:45:32 +0200 [335] <- 304 text/html 0ms
31/Mar/2009:11:45:33 +0200 [334] <- 200 image/gif 31ms
31/Mar/2009:11:45:38 +0200 [333] <- 200 image/gif 31ms
31/Mar/2009:11:45:42 +0200 [336] -> GET /author/libs/CFC/content/imgs/logo.rZMNURccynWcTZRXunQbbQtvuuCMbRRBuWXz0000.default.gif HTTP/1.1
31/Mar/2009:11:45:43 +0200 [337] -> GET /author/titlebar_bg.gif HTTP/1.1
31/Mar/2009:11:45:43 +0200 [336] <- 304 text/html 0ms
31/Mar/2009:11:45:44 +0200 [337] <- 304 text/html 0ms
```

### Utilizzo di rlog.jar per trovare le richieste con tempi di durata prolungati {#using-rlog-jar-to-find-requests-with-long-duration-times}

AEM include vari strumenti di supporto in:
`<cq-installation-dir>/crx-quickstart/opt/helpers`

Una di queste `rlog.jar`funzioni può essere utilizzata per ordinare rapidamente `request.log` in modo che le richieste vengano visualizzate per durata, dal più lungo al più breve tempo possibile.

Il seguente comando mostra gli argomenti possibili:

```shell
$java -jar rlog.jar
Request Log Analyzer Version 21584 Copyright 2005 Day Management AG
Usage:
  java -jar rlog.jar [options] <filename>
Options:
  -h               Prints this usage.
  -n <maxResults>  Limits output to <maxResults> lines.
  -m <maxRequests> Limits input to <maxRequest> requests.
  -xdev            Exclude POST request to CRXDE.
```

Ad esempio, potete eseguirlo specificando `request.log` il file come parametro e mostrare le 10 prime richieste con la durata più lunga:

```shell
$ java -jar ../opt/helpers/rlog.jar -n 10 request.log
*Info * Parsed 464 requests.
*Info * Time for parsing: 22ms
*Info * Time for sorting: 2ms
*Info * Total Memory: 1mb
*Info * Free Memory: 1mb
*Info * Used Memory: 0mb
------------------------------------------------------
     18051ms 31/Mar/2009:11:15:34 +0200 200 GET /content/geometrixx/en/company.html text/ html
      2198ms 31/Mar/2009:11:15:20 +0200 200 GET /libs/cq/widgets.js application/x-javascript
      1981ms 31/Mar/2009:11:15:11 +0200 200 GET /libs/wcm/content/welcome.html text/html
      1973ms 31/Mar/2009:11:15:52 +0200 200 GET /content/campaigns/geometrixx.teasers..html text/html
      1883ms 31/Mar/2009:11:15:20 +0200 200 GET /libs/security/cq-security.js application/x-javascript
      1876ms 31/Mar/2009:11:15:20 +0200 200 GET /libs/tagging/widgets.js application/x-javascript
      1869ms 31/Mar/2009:11:15:20 +0200 200 GET /libs/tagging/widgets/themes/default.js application/x-javascript
      1729ms 30/Mar/2009:16:45:56 +0200 200 GET /libs/wcm/content/welcome.html text/html; charset=utf-8
      1510ms 31/Mar/2009:11:15:34 +0200 200 GET /bin/wcm/contentfinder/asset/view.json/ content/dam?_dc=1238490934657&query=&mimeType=image&_charset_=utf-8 application/json
      1462ms 30/Mar/2009:17:23:08 +0200 200 GET /libs/wcm/content/welcome.html text/html; charset=utf-8
```

Se è necessario eseguire questa operazione su un esempio di dati di grandi dimensioni, potrebbe essere necessario concatenare `request.log` i singoli file.

### Apache Bench {#apache-bench}

Per ridurre al minimo l&#39;impatto di casi speciali (come il processo di garbage collection, ecc.), si consiglia di utilizzare uno strumento come `apachebench` (vedere, ad esempio, [ab](https://httpd.apache.org/docs/2.2/programs/ab.html) per ulteriori documenti) per identificare le perdite di memoria e analizzare in modo selettivo il tempo di risposta.

Apache Bench può essere utilizzato nel modo seguente:

```shell
$ ab -c 5 -k -n 1000 "https://localhost:4503/content/geometrixx/en/company.html"
This is ApacheBench, Version 2.3 <$Revision: 655654 $>
Copyright 1996 Adam Twiss, Zeus Technology Ltd, https://www.zeustech.net/
Licensed to The Apache Software Foundation, https://www.apache.org/

Benchmarking localhost (be patient)
Completed 100 requests
Completed 200 requests
Completed 300 requests
Completed 400 requests
Completed 500 requests
Completed 600 requests
Completed 700 requests
Completed 800 requests
Completed 900 requests
Completed 1000 requests
Finished 1000 requests

Server Software: Day-Servlet-Engine/4.1.52
Server Hostname: localhost
Server Port: 4503

Document Path: /content/geometrixx/en/company.html
Document Length: 24127 bytes

Concurrency Level: 5
Time taken for tests: 69.766 seconds
Complete requests: 1000
Failed requests: 998
(Connect: 0, Receive: 0, Length: 998, Exceptions: 0)
Write errors: 0
Keep-Alive requests: 0
Total transferred: 24160923 bytes
HTML transferred: 24010923 bytes
Requests per second: 14.33 /sec (mean)
Time per request: 348.828 [ms] (mean)
Time per request: 69.766 [ms] (mean, across all concurrent requests)
Transfer rate: 338.20 [Kbytes/sec] received

Connection Times (ms)
min mean[+/-sd] median max
Connect: 0 1 3.9 0 58
Processing: 138 347 568.5 282 8106
Waiting: 137 344 568.1 281 8106
Total: 139 348 568.4 283 8106

Percentage of the requests served within a certain time (ms)
50% 283
66% 323
75% 356
80% 374
90% 439
95% 512
98% 1047
99% 1132
100% 8106 (longest request)
```

I numeri riportati sopra sono tratti da un notebook standard MAcBook Pro (metà 2010) che accede alla pagina aziendale geometrixx, come incluso in un&#39;installazione AEM predefinita. La pagina è molto semplice, ma non ottimizzata per le prestazioni.

`apachebench` visualizza anche il tempo per richiesta come media, per tutte le richieste simultanee; vedere `Time per request: 54.595 [ms]` (media, per tutte le richieste simultanee). Potete modificare il valore del parametro di concorrenza `-c` (numero di richieste multiple da eseguire alla volta) per visualizzare eventuali effetti.

### Contatori richieste {#request-counters}

Le informazioni sul traffico delle richieste (numero di richieste durante un periodo di tempo specifico) indicano il carico sull’istanza. Queste informazioni possono essere estratte da [request.log](#interpreting-the-request-log), anche se l&#39;utilizzo di contatori automatizza la raccolta dei dati per consentirti di visualizzare:

* differenze significative nell&#39;attività (ossia distinguere tra &quot;molte richieste&quot; e &quot;attività bassa&quot;
* quando un&#39;istanza non viene utilizzata
* eventuali riavvii (i contatori vengono reimpostati su 0)

Per automatizzare la raccolta delle informazioni è inoltre possibile installare RequestFilter per incrementare un contatore su ogni richiesta. Più contatori possono essere utilizzati per periodi di tempo diversi.

Le informazioni raccolte possono essere utilizzate per indicare:

* cambiamenti significativi dell&#39;attività
* un&#39;istanza ridondante
* eventuali riavvii (contatore reimpostato su 0)

### Commenti HTML {#html-comments}

È consigliabile che ogni progetto includa `html comments` le prestazioni del server. Si possono trovare molti buoni esempi pubblici; selezionate una pagina, aprite l’origine della pagina per visualizzarla e scorrete verso il basso, con un codice come quello che segue:

```xml
</body>
 </html>
        <!--
        Page took 58 milliseconds to be rendered by server
         -->
```

### Monitoraggio delle prestazioni con JConsole {#monitoring-performance-using-jconsole}

Il comando tool `jconsole` è disponibile con il JDK.

1. Avviate l’istanza AEM.
1. Esegui `jconsole.`
1. Selezionate l’istanza AEM e **Connect**.

1. Dall’interno dell’ `Local` applicazione, fare doppio clic `com.day.crx.quickstart.Main`; la Panoramica verrà visualizzata come impostazione predefinita:

   ![chlimage_1-1](assets/chlimage_1-1.png)

   Dopo questo è possibile selezionare altre opzioni.

### Monitoraggio delle prestazioni con (J)VisualVM {#monitoring-performance-using-j-visualvm}

A partire da JDK 1.6, il comando tool `jvisualvm` è disponibile. Dopo aver installato JDK 1.6 è possibile:

1. Avviate l’istanza AEM.

   >[!NOTE]
   >
   >Se si utilizza Java 5 è possibile aggiungere l&#39; `-Dcom.sun.management.jmxremote` argomento alla riga di comando java che avvia la JVM. JMX è abilitato per impostazione predefinita con Java 6.

1. Eseguire:

   * `jvisualvm`: nella cartella bin JDK 1.6 (versione testata)
   * `visualvm`: può essere scaricato da [VisualVM](https://visualvm.dev.java.net/) (versione del bordo di dissanguamento)

1. Dall’interno dell’ `Local` applicazione, fare doppio clic `com.day.crx.quickstart.Main`; la Panoramica verrà visualizzata come impostazione predefinita:

   ![chlimage_1-2](assets/chlimage_1-2.png)

   Dopo questo, potete selezionare altre opzioni, tra cui Monitor:

   ![chlimage_1-3](assets/chlimage_1-3.png)

È possibile utilizzare questo strumento per generare i ribaltamenti di filettatura e i rigetti di testine di memoria. Queste informazioni sono spesso richieste dal team di assistenza tecnica.

### Raccolta informazioni {#information-collection}

Conoscere il più possibile l&#39;installazione può aiutarti a tenere traccia di ciò che potrebbe aver causato un cambiamento nelle prestazioni e se queste modifiche sono giustificate. Queste metriche devono essere raccolte a intervalli regolari per poter vedere facilmente cambiamenti significativi.

Le seguenti informazioni possono essere utili:

* [Quanti autori lavorano con il sistema?](#how-many-authors-are-working-with-the-system)
* [Qual è il numero medio di attivazioni di pagina al giorno?](#what-is-the-average-number-of-page-activations-per-day)
* [Quante pagine si trovano attualmente nel sistema?](#how-many-pages-do-you-currently-maintain-on-this-system)
* [Se utilizzate MSM, qual è il numero medio di rollout al mese?](#if-you-use-msm-what-is-the-average-number-of-rollouts-per-month)
* [Qual è il numero medio di Live Copy al mese?](#what-is-the-average-number-of-live-copies-per-month)
* [Se utilizzate  AEM Assets, quante risorse mantenete attualmente in Risorse?](#ifyouusecqdamhowmanyassetsdoyoucurrentlymaintainincqdam)
* [Qual è la dimensione media delle risorse?](#what-is-the-average-size-of-the-assets)
* [Quanti modelli sono attualmente utilizzati?](#how-many-templates-are-currently-used)
* [Quanti componenti sono attualmente utilizzati?](#how-many-components-are-currently-used)
* [Quante richieste all’ora si verificano nel sistema di authoring in fase di picco?](#how-many-requests-per-hour-do-you-have-on-the-author-system-at-peak-time)
* [Quante richieste all’ora si verificano nel sistema di pubblicazione in fase di picco?](#how-many-requests-per-hour-do-you-have-on-the-publish-system-at-peak-time)

#### Quanti autori lavorano con il sistema? {#how-many-authors-are-working-with-the-system}

Per visualizzare il numero di autori che hanno utilizzato il sistema dall&#39;installazione, utilizzare la riga di comando:

```shell
cd <cq-installation-dir>/crx-quickstart/logs
cut -d " " -f 3 access.log | sort -u | wc -l
```

Per visualizzare il numero di autori che lavorano su una data specifica:

```shell
grep "<date>" access.log | cut -d " " -f 3 | sort -u | wc -l
```

#### Qual è il numero medio di attivazioni di pagina al giorno? {#what-is-the-average-number-of-page-activations-per-day}

Per visualizzare il numero totale di attivazioni di pagina dall&#39;installazione del server, utilizzare una query del repository; tramite CRXDE - Strumenti - Query:

* **Tipo** `XPath`

* **Percorso** `/`

* **Query** `//element(*, cq:AuditEvent)[@cq:type='Activate']`

Quindi calcolare il numero di giorni trascorsi dall&#39;installazione per calcolare la media.

#### Quante pagine si trovano attualmente nel sistema? {#how-many-pages-do-you-currently-maintain-on-this-system}

Per visualizzare il numero di pagine attualmente sul server, utilizzare una query sull&#39;archivio; tramite CRXDE - Strumenti - Query:

* **Tipo** `XPath`

* **Percorso** `/`

* **Query** `//element(*, cq:Page)`

#### Se utilizzate MSM, qual è il numero medio di rollout al mese? {#if-you-use-msm-what-is-the-average-number-of-rollouts-per-month}

Per determinare il numero totale di rollout dall&#39;installazione utilizzando una query dell&#39;archivio; tramite CRXDE - Strumenti - Query:

* **Tipo** `XPath`

* **Percorso** `/`

* **Query** `//element(*, cq:AuditEvent)[@cq:type='PageRolledOut']`

Calcolare il numero di mesi trascorsi dall&#39;installazione per calcolare la media.

#### Qual è il numero medio di Live Copy al mese? {#what-is-the-average-number-of-live-copies-per-month}

Per determinare il numero totale di Live Copy effettuate dall&#39;installazione utilizzando una query sull&#39;archivio; tramite CRXDE - Strumenti - Query:

* **Tipo** `XPath`

* **Percorso** `/`

* **Query** `//element(*, cq:LiveSyncConfig)`

Utilizzate di nuovo il numero di mesi trascorsi dall&#39;installazione per calcolare la media.

#### Se utilizzate  AEM Assets, quante risorse mantenete attualmente in Risorse? {#if-you-use-aem-assets-how-many-assets-do-you-currently-maintain-in-assets}

Per verificare il numero di risorse DAM attualmente gestite, utilizzate una query sull&#39;archivio; tramite CRXDE - Strumenti - Query:

* **Tipo** `XPath`
* **Percorso** `/`
* **Query** `/jcr:root/content/dam//element(*, dam:Asset)`

#### Qual è la dimensione media delle risorse? {#what-is-the-average-size-of-the-assets}

Per determinare la dimensione totale della `/var/dam` cartella:

1. Utilizzare WebDAV per mappare l&#39;archivio sul file system locale.

1. Utilizzare la riga di comando:

   ```shell
   cd /Volumes/localhost/var
   du -sh dam/
   ```

   Per ottenere la dimensione media, dividete la dimensione globale per il numero totale di risorse in `/var/dam` (ottenuto sopra).

#### Quanti modelli sono attualmente utilizzati? {#how-many-templates-are-currently-used}

Per visualizzare il numero di modelli attualmente sul server, utilizzare una query sull&#39;archivio; tramite CRXDE - Strumenti - Query:

* **Tipo** `XPath`
* **Percorso** `/`
* **Query** `//element(*, cq:Template)`

#### Quanti componenti sono attualmente utilizzati? {#how-many-components-are-currently-used}

Per visualizzare il numero di componenti attualmente presenti sul server, utilizzare una query dell&#39;archivio; tramite CRXDE - Strumenti - Query:

* **Tipo** `XPath`
* **Percorso** `/`
* **Query** `//element(*, cq:Component)`

#### Quante richieste all’ora si verificano nel sistema di authoring in fase di picco? {#how-many-requests-per-hour-do-you-have-on-the-author-system-at-peak-time}

Per determinare le richieste per ora nel sistema di authoring in fase di picco:

1. Per determinare il numero totale di richieste dall&#39;installazione, utilizzare la riga di comando:

   ```shell
   cd <cq-installation-dir>/crx-quickstart/logs
   grep -R "\->" request.log | wc -l
   ```

1. Per determinare le date di inizio e di fine:

   ```shell
   vim request.log
   G / 1G: for the last/first lines
   ```

   Utilizzate questi valori per calcolare il numero di ore trascorse dall&#39;installazione, quindi il numero medio di richieste all&#39;ora.

#### Quante richieste all’ora si verificano nel sistema di pubblicazione in fase di picco? {#how-many-requests-per-hour-do-you-have-on-the-publish-system-at-peak-time}

Ripetete la procedura descritta sopra nell’istanza di pubblicazione.

## Analisi di scenari specifici {#analyzing-specific-scenarios}

Di seguito è riportato un elenco di suggerimenti su come verificare se si verificano alcuni problemi di prestazioni. L&#39;elenco non è (purtroppo) del tutto esaustivo.

>[!NOTE]
>
>Per ulteriori informazioni, consultate anche i seguenti articoli:
>
>* [Fanelli di filettatura](https://helpx.adobe.com/experience-manager/kb/TakeThreadDump.html)
>* [Analisi dei problemi di memoria](https://helpx.adobe.com/experience-manager/kb/AnalyzeMemoryProblems.html)
>* [Analisi mediante il profiler incorporato](https://helpx.adobe.com/experience-manager/kb/AnalyzeUsingBuiltInProfiler.html)
>* [Analizzare i processi lenti e bloccati](https://helpx.adobe.com/experience-manager/kb/AnalyzeSlowAndBlockedProcesses.html)

>



### CPU al 100% {#cpu-at}

Se la CPU del sistema è in esecuzione costantemente al 100%, vedere:

* La Knowledge Base:

   * [Analizzare i processi lenti e bloccati](https://helpx.adobe.com/experience-manager/kb/AnalyzeSlowAndBlockedProcesses.html)

### Memoria insufficiente {#out-of-memory}

Anche se tali errori devono essere rilevati durante lo sviluppo e la verifica, alcuni scenari possono scivolare.

Se il sistema non dispone di memoria sufficiente, questo può essere visualizzato in vari modi, tra cui il degrado delle prestazioni e i messaggi di errore, incluso il sottotitolo:

`java.lang.OutOfMemoryError`

In questi casi controllare:

* Impostazioni JVM utilizzate per [avviare AEM](/help/sites-deploying/deploy.md#getting-started)
* La Knowledge Base:

   * [Analisi dei problemi di memoria](https://helpx.adobe.com/experience-manager/kb/AnalyzeMemoryProblems.html)

### I/O disco {#disk-i-o}

Se il sistema non dispone di spazio su disco sufficiente, oppure se si nota che il disco è danneggiato, vedere:

* Se avete disabilitato la raccolta di informazioni di debug; può essere configurato in diverse posizioni, tra cui:

   * [Apache Sling Script Handler](/help/sites-deploying/osgi-configuration-settings.md#apacheslingjspscripthandler)
   * [Apache Sling Java Script Handler](/help/sites-deploying/osgi-configuration-settings.md#apacheslingjavascripthandler)
   * [Configurazione Registrazione Apache Sling](/help/sites-deploying/osgi-configuration-settings.md#apacheslingloggingconfiguration)
   * [CQ HTML Library Manager](/help/sites-deploying/osgi-configuration-settings.md#daycqhtmllibrarymanager)
   * [Filtro debug CQ WCM](/help/sites-deploying/osgi-configuration-settings.md#daycqwcmdebugfilter)
   * [Registratori](/help/sites-deploying/monitoring-and-maintaining.md#activating-the-debug-log-level) [](/help/sites-deploying/configuring.md#loggersandwritersforindividualservices)

* Se e come avete configurato [Version Purging](/help/sites-deploying/version-purging.md)
* La Knowledge Base:

   * [Troppi file aperti](https://helpx.adobe.com/experience-manager/kb/TooManyOpenFiles.html)
   * [Il journal consuma troppo spazio su disco](https://helpx.adobe.com/experience-manager/kb/JournalTooMuchDiskSpace.html)

### Degradazione regolare delle prestazioni {#regular-performance-degradation}

Se le prestazioni dell’istanza si deteriorano dopo ogni riavvio (a volte una settimana o più dopo), è possibile verificare quanto segue:

* [Memoria insufficiente](#outofmemory)
* La Knowledge Base:

   * [Sessioni non chiuse](https://helpx.adobe.com/experience-manager/kb/AnalyzeUnclosedSessions.html)

### Sintonizzazione JVM {#jvm-tuning}

Java Virtual Machine (JVM) è notevolmente migliorata rispetto al tuning (soprattutto da Java 7). Per questo motivo, spesso è consigliabile specificare una dimensione JVM fissa ragionevole e utilizzare i valori predefiniti.

Se le impostazioni predefinite non sono adatte, è importante stabilire un metodo per monitorare e valutare le prestazioni GC prima di tentare di sintonizzare la JVM; questo può includere fattori di monitoraggio, tra cui la dimensione dell&#39;heap, l&#39;algoritmo e altri aspetti.

Alcune scelte comuni sono:

* VerboseGC:

   ```
   -verbose:gc \
    -Xloggc:$LOGS/verbosegc.log \
    -XX:+PrintGCDetails \
    -XX:+PrintGCDateStamps
   ```

Il registro risultante può essere assimilato da un visualizzatore GC, ad esempio:

` [https://www.ibm.com/developerworks/library/j-ibmtools2/](https://www.ibm.com/developerworks/library/j-ibmtools2/)`

O JConsole:

* Queste impostazioni sono per una connessione JMX &quot;wide open&quot;:

   ```
   -Dcom.sun.management.jmxremote \
    -Dcom.sun.management.jmxremote.port=8889 \
    -Dcom.sun.management.jmxremote.authenticate=false \
    -Dcom.sun.management.jmxremote.ssl=false
   ```

* Collegare quindi la JVM con la JConsole; vedere:
   ` [https://docs.oracle.com/javase/6/docs/technotes/guides/management/jconsole.html](https://docs.oracle.com/javase/6/docs/technotes/guides/management/jconsole.html)`

Questo vi aiuterà a vedere quanto memoria viene utilizzata, quali algoritmi GC vengono utilizzati, quanto tempo sono necessari per l&#39;esecuzione e quale effetto ha sulle prestazioni dell&#39;applicazione. Senza questo, sintonizzazione è solo &quot;manopole casuali&quot;.

>[!NOTE]
>
>Per la VM di Oracle sono inoltre disponibili informazioni su:
>
>[https://docs.oracle.com/javase/7/docs/technotes/guides/vm/server-class.html](https://docs.oracle.com/javase/7/docs/technotes/guides/vm/server-class.html)
