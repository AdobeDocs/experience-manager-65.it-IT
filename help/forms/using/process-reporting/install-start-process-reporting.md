---
title: Guida introduttiva a Process Reporting
seo-title: Guida introduttiva a Process Reporting
description: I passaggi da seguire per iniziare a utilizzare  AEM Forms su JEE Process Reporting
seo-description: I passaggi da seguire per iniziare a utilizzare  AEM Forms su JEE Process Reporting
uuid: 685cad39-da2c-411d-a0b0-201917438bcf
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: process-reporting
discoiquuid: 7c1fcde0-b983-4b24-bc19-fcee1d4f096b
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '1731'
ht-degree: 0%

---


# Guida introduttiva a Process Reporting{#getting-started-with-process-reporting}

Process Reporting offre agli utenti di AEM Forms la possibilità di eseguire query sulle  dei processi AEM Forms attualmente definiti nell&#39;implementazione  AEM Forms. Tuttavia, Process Reporting non accede direttamente ai dati dall&#39;archivio di AEM Forms . I dati vengono pubblicati per la prima volta nell&#39;archivio di Process Reporting su base programmata (*dal servizio ProcessDataPublisher &amp; ProcessDataStorage* s). I report e le query in Process Reporting vengono quindi generati dai dati di Process Reporting pubblicati nell&#39;archivio. Process Reporting è installato come parte del modulo di Forms Workflow.

In questo articolo vengono descritti i passaggi per abilitare la pubblicazione di  dati AEM Forms nell&#39;archivio di Process Reporting. Dopo di che, sarà possibile utilizzare Process Reporting per eseguire report e query. L&#39;articolo descrive inoltre le opzioni disponibili per configurare i servizi Process Reporting.

## Pre-richieste di reporting processo {#process-reporting-pre-requisites}

### Rimozione di processi non essenziali {#purge-non-essential-processes}

Se si sta utilizzando l&#39;Forms Workflow, il database AEM Forms  può contenere una grande quantità di dati

I servizi di pubblicazione di Process Reporting pubblicheranno tutti  dati AEM Forms attualmente disponibili nel database. Ciò implica che, se il database contiene dati legacy sui quali non si desidera eseguire report e query, anche tutti quei dati verrebbero pubblicati nell&#39;archivio anche se non sono richiesti per la creazione di report. Si consiglia di eliminare questi dati prima di eseguire i servizi per pubblicare i dati nell&#39;archivio di Process Reporting. Ciò migliorerà le prestazioni sia del servizio di pubblicazione che del servizio che invia query ai dati per la creazione di report.

Per informazioni dettagliate sulla rimozione  dati del processo AEM Forms, vedere [Rimozione dei dati del processo](https://help.adobe.com/en_US/livecycle/11.0/AdminHelp/WS92d06802c76abadb-5145d5d12905ce07e7-7cb2.2.html).

>[!NOTE]
>
>Per suggerimenti e trucchi di Utilità di rimozione, consultate l&#39;articolo Adobe Developer Connection su [Processi e processi di rimozione](https://www.adobe.com/content/dam/Adobe/en/devnet/livecycle/pdfs/purging_processes_jobs.pdf).

## Configurazione di Process Reporting Services {#configuring-process-reporting-services}

### Pianificazione della pubblicazione dei dati del processo {#schedule-process-data-publishing}

Process Reporting Services pubblica i dati dal database AEM Forms  all&#39;archivio di Process Reporting su base programmata.

Questa operazione può richiedere molte risorse e può influire sulle prestazioni dei server AEM Forms . Si consiglia di pianificare questa operazione al di fuori degli slot dedicati  server AEM Forms.

Per impostazione predefinita, la pubblicazione dei dati è pianificata per essere eseguita ogni giorno alle 2:00.

Per modificare la pianificazione di pubblicazione, effettuate le seguenti operazioni:

>[!NOTE]
>
>Se state eseguendo l&#39;implementazione AEM Forms  su un cluster, eseguite i seguenti passaggi su ciascun nodo del cluster.

1. Arrestate l&#39;istanza  server AEM Forms.
1. &#x200B;

   * (Per Windows) Aprite il file `[JBoss root]/bin/run.conf.bat` in un editor.
   * (per Linux, AIX e Solaris) `[JBoss root]/bin/run.conf.sh` in un editor.

1. Aggiungere l&#39;argomento JVM `-Dreporting.publisher.cron = <expression>.`

   Esempio: La seguente espressione cron fa sì che Process Reporting pubblichi  dati AEM Forms nell&#39;archivio di Process Reporting ogni 5 ore:

   * `-Dreporting.publisher.cron = 0_0_0/5_*_*_?`

1. Salvate e chiudete il file `run.conf.bat`.

1. Riavviate l&#39;istanza  server AEM Forms.

1. Arrestate l&#39;istanza  server AEM Forms.
1. Accedete alla console di amministrazione di WebSphere. Nella struttura di navigazione fare clic su **Server** > **Application Server**, quindi fare clic sul nome del server nel riquadro a destra.

1. In Infrastruttura server, fare clic su **Java and Process Management** > **Definizione processo**.

1. In Proprietà aggiuntive, fare clic su **Java Virtual Machine**.

   Nella casella Argomenti JVM generici, aggiungere l&#39;argomento `-Dreporting.publisher.cron = <expression>.`

   **Esempio**: La seguente espressione cron fa sì che Process Reporting pubblichi  dati AEM Forms nell&#39;archivio di Process Reporting ogni 5 ore:

   * `-Dreporting.publisher.cron = 0_0_0/5_*_*_?`

1. Fare clic su **Applica**, fare clic su OK, quindi su **Salva direttamente nella configurazione principale**.
1. Riavviate l&#39;istanza  server AEM Forms.
1. Arrestate l&#39;istanza  server AEM Forms.
1. Accedere alla console di amministrazione WebLogic. L&#39;indirizzo predefinito della console di amministrazione WebLogic è `https://[hostname]:[port]/console`.
1. In Centro modifiche fare clic su **Blocca e modifica**.
1. In Struttura dominio fare clic su **Ambiente** > **Server** e, nel riquadro a destra, fare clic sul nome del server gestito.
1. Nella schermata successiva, fare clic sulla scheda **Configuration** > **Server Start**.
1. Nella casella Argomenti, aggiungere l&#39;argomento JVM `-Dreporting.publisher.cron = <expression>`.

   **Esempio**: La seguente espressione cron fa sì che Process Reporting pubblichi  dati AEM Forms nell&#39;archivio di Process Reporting ogni 5 ore:

   `-Dreporting.publisher.cron = 0_0_0/5_*_*_?`

1. Fare clic su **Salva**, quindi fare clic su **Attiva modifiche**.
1. Riavviate l&#39;istanza  server AEM Forms.

![processdatapublisherservice](assets/processdatapublisherservice.png)

### Servizio ProcessDataStorage {#processdatastorage-service}

Il servizio ProcessDataStorageProvider riceve i dati del processo dal servizio ProcessDataPublisher e li salva nell&#39;archivio di Process Reporting.

In ciascun ciclo di pubblicazione, i dati vengono salvati nelle sottocartelle di una cartella principale predefinita.

È possibile utilizzare la console di amministrazione per configurare la radice (**predefinita**: `/content/reporting/pm`) posizione e sottocartella (**predefinita**: `/yyyy/mm/dd/hh/mi/ss`) formato gerarchico in cui vengono memorizzati i dati del processo.

#### Per configurare i percorsi del repository di Process Reporting {#to-configure-the-process-reporting-repository-locations}

1. Accedete a **Console di amministrazione** con le credenziali di amministratore. L&#39;URL predefinito della console di amministrazione è `https://'[server]:[port]'/adminui`
1. Andate a **Home** > **Services** > **Applicazioni e servizi** >**Gestione dei servizi** e aprite il servizio **ProcessDataStorageProvider**.

   ![process-data-storage-service](assets/process-data-storage-service.png)

   **CartellaPrincipale**

   Posizione CRX all&#39;interno della quale i dati del processo vengono memorizzati per la generazione dei rapporti.

   `Default`: `/content/reporting/pm`

   **Gerarchia cartelle**

   La gerarchia di cartelle all’interno della quale i dati del processo vengono memorizzati in base al tempo di creazione del processo.

   `Default`:  `/yyyy/mm/dd/hh/mi/ss`

1. Fai clic su **Salva**.

### Servizio ReportConfiguration {#reportconfiguration-service}

Il servizio ReportConfiguration viene utilizzato da Process Reporting per configurare il servizio di query di reporting del processo.

#### Per configurare il servizio ReportingConfiguration {#to-configure-the-reportingconfiguration-service}

1. Accedete a **Configuration Manager** con le credenziali di amministratore CRX. L&#39;URL predefinito di Configuration Manager è `https://'[server]:[port]'/lc/system/console/configMgr`
1. Aprire il servizio **ReportingConfiguration**.
1. **Numero di record**

   Quando si esegue una query nell&#39;archivio, un risultato può contenere un numero elevato di record. Se il set di risultati è grande, l&#39;esecuzione della query può utilizzare risorse del server.

   Per gestire set di risultati di grandi dimensioni, il servizio ReportConfiguration suddivide l&#39;elaborazione della query in batch di record. Questo riduce il carico del sistema.

   `Default`:  `1000`

   **Percorso di archiviazione CRX**

   Posizione CRX all&#39;interno della quale i dati del processo devono essere memorizzati per la generazione di rapporti.

   `Default`:  `/content/reporting/pm`

   >[!NOTE]
   >
   >Si tratta della stessa posizione specificata nell&#39;opzione di configurazione ProcessDataStorage **Cartella principale**.
   >
   >
   >Se si aggiorna l&#39;opzione Cartella principale nella configurazione ProcessDataStorage, è necessario aggiornare il percorso del percorso di memorizzazione CRX nel servizio ReportConfiguration.

1. Fare clic su **Save** e chiudere **CQ Configuration Manager**.

### Servizio ProcessDataPublisher {#processdatapublisher-service}

Il servizio ProcessDataPublisher importa i dati del processo dal database AEM Forms  e li pubblica nel servizio ProcessDataStorageProvider per l&#39;archiviazione.

#### Per configurare il servizio ProcessDataPublisher   {#to-configure-processdatapublisher-service-nbsp}

1. Accedete a **Console di amministrazione** con le credenziali di amministratore.

   L&#39;URL predefinito è `https://'server':port]/adminui/`.

1. Andate a **Home** > **Servizi** > **Applicazioni e servizi** >**Gestione dei servizi** e aprite il servizio **ProcessDataPublisher**.

![processdatapublisherservice-1](assets/processdatapublisherservice-1.png)

**Pubblica dati**

Abilitate questa opzione per avviare la pubblicazione dei dati del processo. Per impostazione predefinita, l’opzione è disabilitata.

Abilita Process Reporting solo quando tutte le configurazioni relative ai componenti Process Reporting sono impostate correttamente.

In alternativa, utilizzare questa opzione per disabilitare la pubblicazione dei dati del processo quando non è più necessaria.

`Default`:  `Off`

**Intervallo batch (sec)**

Ogni volta che il servizio ProcessDataPublisher viene eseguito, il servizio suddivide per la prima volta l&#39;ora dall&#39;ultima esecuzione del servizio in base all&#39;intervallo di batch. Il servizio elabora quindi ciascun intervallo di  dati AEM Forms separatamente.

Questo consente di controllare le dimensioni dei dati che l&#39;editore elabora e che terminano durante ogni esecuzione (batch) all&#39;interno di un ciclo.

Ad esempio, se l&#39;editore viene eseguito ogni giorno, per impostazione predefinita, invece di elaborare tutti i dati per un giorno in una singola esecuzione, suddivide l&#39;elaborazione in 24 batch di un&#39;ora l&#39;uno.

`Default`:  `3600`

`Unit`:  `Seconds`

**Timeout blocco (sec)**

Il servizio di pubblicazione acquisisce un blocco quando avvia l&#39;elaborazione dei dati in modo che più istanze dell&#39;editore non avviino l&#39;esecuzione e l&#39;elaborazione dei dati contemporaneamente.

Se un servizio di pubblicazione che ha acquisito un blocco è inattivo per il numero di secondi definito dal valore Blocca timeout, viene rilasciato il relativo blocco in modo che altre istanze del servizio di pubblicazione possano continuare l&#39;elaborazione.

`Default`:  `3600`

`Unit`:  `Seconds`

**Pubblica dati da**

 ambiente AEM Forms contiene i dati dal momento in cui è stato configurato l&#39;ambiente.

Per impostazione predefinita, il servizio ProcessDataPublisher importa tutti i dati dal database AEM Forms .

A seconda delle esigenze di reporting, se si prevede di eseguire rapporti e query sui dati dopo una determinata data e ora, è consigliabile specificare la data e l&#39;ora. Il servizio di pubblicazione pubblicherà quindi la data a partire da tale data.

`Default`:  `01-01-1970 00:00:00`

`Format`:  `dd-MM-yyyy HH:mm:ss`

## Accesso all&#39;interfaccia utente di Process Reporting {#accessing-the-process-reporting-user-interface}

L&#39;interfaccia utente per Process Reporting è basata su browser.

Dopo aver configurato Process Reporting (Generazione rapporti sui processi), puoi iniziare a utilizzare Process Reporting (Generazione rapporti sui processi) nel seguente percorso nell&#39;installazione  AEM Forms:

`https://<server>:<port>/lc/pr`

### Accedere a Process Reporting {#log-in-to-process-reporting}

Quando vi spostate sull&#39;URL di Process Reporting (https://&lt;server>:&lt;porta>/lc/pr), viene visualizzata la schermata di accesso.

Specificare le credenziali per accedere al modulo Process Reporting.

>[!NOTE]
>
>Per accedere all&#39;interfaccia utente di Process Reporting, è necessario disporre delle seguenti autorizzazioni  AEM Forms:
>
>`PERM_PROCESS_REPORTING_USER`

![Login a Process Reporting](assets/capture1_new.png)

Quando si accede a Process Reporting (Generazione rapporti processo), viene visualizzata la schermata **[!UICONTROL Home]**.

### Schermata principale Report processo {#process-reporting-home-screen}

![process-reporting-home-screen](assets/process-reporting-home-screen.png)

**Visualizzazione struttura Report processo:** La vista struttura a sinistra della schermata Home contiene gli elementi per i moduli Report processo.

La struttura è composta dai seguenti elementi di primo livello:

**Rapporti:** questo elemento contiene i report out-of-the-box forniti con Process Reporting.

Per informazioni dettagliate sui report predefiniti, vedere [Report predefiniti in Process Reporting](/help/forms/using/process-reporting/pre-defined-reports-in-process-reporting.md).

**Query ad hoc:** questo elemento contiene opzioni per eseguire ricerche basate sui filtri per processi e attività.

Per informazioni dettagliate sulle query ad hoc, vedere [Query ad hoc in Process Reporting](/help/forms/using/process-reporting/adhoc-queries-in-process-reporting.md).

**Personalizzato:** il nodo Personalizzato visualizza i rapporti personalizzati creati dall&#39;utente.

Per la procedura per creare e visualizzare rapporti personalizzati, vedere [Report personalizzati in Process Reporting](/help/forms/using/process-reporting/process-reporting-custom-reports.md).

**Barra del titolo Report processo:** la barra del titolo Report processo contiene alcune opzioni generiche che è possibile utilizzare quando si lavora nell&#39;interfaccia utente.

**Titolo Report processo:** il titolo Report processo viene visualizzato nell&#39;angolo sinistro della barra del titolo.

Fate clic sul titolo in qualsiasi momento per tornare alla schermata iniziale.

**Ora ultimo aggiornamento:** i dati del processo vengono pubblicati dal database AEM Forms  al repository di Process Reporting su base programmata.

L&#39;Ora ultimo aggiornamento visualizza l&#39;ultima data e l&#39;ora in cui gli aggiornamenti dei dati sono stati inviati all&#39;archivio di Process Reporting.

Per informazioni dettagliate sul servizio di pubblicazione dei dati e su come pianificare il servizio, consultare [Pianificare la pubblicazione dei dati del processo](/help/forms/using/process-reporting/install-start-process-reporting.md#p-schedule-process-data-publishing-p) nell&#39;articolo Guida introduttiva ai rapporti sui processi.

**Utente di Process Reporting:** il nome utente connesso viene visualizzato a destra dell&#39;ora dell&#39;ultimo aggiornamento.

**Elenco a discesa Barra del titolo Rapporti processi:** L&#39;elenco a discesa nell&#39;angolo destro della barra del titolo Report processo contiene le seguenti opzioni:

* **[!UICONTROL Sincronizzazione]**: Sincronizzare l&#39;archivio di Process Reporting incorporato con il database AEM Forms .
* **[!UICONTROL Aiuto]**: Visualizzare la documentazione della Guida in linea su Process Reporting (Generazione rapporti sui processi).
* **[!UICONTROL Disconnessione]**: Disconnessione da Process Reporting
