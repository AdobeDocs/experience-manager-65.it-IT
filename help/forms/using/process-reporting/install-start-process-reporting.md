---
title: Guida introduttiva a Process Reporting
seo-title: Guida introduttiva a Process Reporting
description: Procedura da seguire per iniziare a utilizzare AEM Forms su JEE Process Reporting
seo-description: Procedura da seguire per iniziare a utilizzare AEM Forms su JEE Process Reporting
uuid: 685cad39-da2c-411d-a0b0-201917438bcf
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: process-reporting
discoiquuid: 7c1fcde0-b983-4b24-bc19-fcee1d4f096b
docset: aem65
translation-type: tm+mt
source-git-commit: 8f90dc4865126d52e04effc9197ef7145b1a167e

---


# Guida introduttiva a Process Reporting{#getting-started-with-process-reporting}

Process Reporting offre agli utenti di AEM Forms la possibilità di richiedere informazioni sui processi AEM Forms attualmente definiti nell’implementazione di AEM Forms. Tuttavia, Process Reporting non accede direttamente ai dati dall&#39;archivio di AEM Forms. I dati vengono pubblicati per la prima volta nell&#39;archivio di Process Reporting su base programmata (*dai* servizi ProcessDataPublisher e ProcessDataStorage). I report e le query in Process Reporting vengono quindi generati dai dati di Process Reporting pubblicati nell&#39;archivio. Process Reporting è installato nel modulo Flusso di lavoro moduli.

Questo articolo descrive i passaggi per abilitare la pubblicazione dei dati di AEM Forms nell&#39;archivio di Process Reporting. Dopo di che, sarà possibile utilizzare Process Reporting per eseguire report e query. L&#39;articolo descrive inoltre le opzioni disponibili per configurare i servizi Process Reporting.

## Pre-richieste di rapporti processo {#process-reporting-pre-requisites}

### Rimozione di processi non essenziali {#purge-non-essential-processes}

Se si utilizza il flusso di lavoro Forms, il database AEM Forms può potenzialmente contenere una grande quantità di dati

I servizi di pubblicazione Process Reporting pubblicheranno tutti i dati di AEM Forms attualmente disponibili nel database. Ciò implica che, se il database contiene dati legacy sui quali non si desidera eseguire report e query, anche tutti quei dati verrebbero pubblicati nell&#39;archivio anche se non sono richiesti per la creazione di report. Si consiglia di eliminare questi dati prima di eseguire i servizi per pubblicare i dati nell&#39;archivio di Process Reporting. Ciò migliorerà le prestazioni sia del servizio di pubblicazione che del servizio che invia query ai dati per la creazione di report.

Per informazioni dettagliate sull&#39;eliminazione dei dati del processo di AEM Forms, consultate [Rimozione dei dati](https://help.adobe.com/en_US/livecycle/11.0/AdminHelp/WS92d06802c76abadb-5145d5d12905ce07e7-7cb2.2.html)di processo.

>[!NOTE]
>
>Per suggerimenti e trucchi di Utilità di rimozione, consultate l&#39;articolo Adobe Developer Connection sui processi e i processi di [rimozione](https://www.adobe.com/content/dam/Adobe/en/devnet/livecycle/pdfs/purging_processes_jobs.pdf).

## Configurazione di Process Reporting Services {#configuring-process-reporting-services}

### Pianificazione della pubblicazione dei dati del processo {#schedule-process-data-publishing}

I servizi Process Reporting consentono di pubblicare i dati dal database di AEM Forms all&#39;archivio di Process Reporting su base programmata.

Questa operazione può richiedere molte risorse e può avere un impatto sulle prestazioni dei server AEM Forms. È consigliabile pianificare questa operazione fuori dagli slot dedicati del server AEM Forms.

Per impostazione predefinita, la pubblicazione dei dati è pianificata per essere eseguita ogni giorno alle 2:00.

Per modificare la pianificazione di pubblicazione, effettuate le seguenti operazioni:

>[!NOTE]
>
>Se stai eseguendo l&#39;implementazione di AEM Forms su un cluster, effettua i seguenti passaggi su ciascun nodo del cluster.

1. Arrestate l&#39;istanza del server AEM Forms.
1. 

   * (Per Windows) Aprite il `[JBoss root]/bin/run.conf.bat` file in un editor.
   * (per Linux, AIX e Solaris) `[JBoss root]/bin/run.conf.sh` in un editor.

1. Aggiungere l&#39;argomento JVM `-Dreporting.publisher.cron = <expression>.`

   Esempio: La seguente espressione cron fa sì che Process Reporting pubblichi ogni 5 ore i dati di AEM Forms nell’archivio di Process Reporting:

   * `-Dreporting.publisher.cron = 0_0_0/5_*_*_?`

1. Salvate e chiudete il `run.conf.bat` file.

1. Riavviate l&#39;istanza del server AEM Forms.

1. Arrestate l&#39;istanza del server AEM Forms.
1. Accedere alla console di amministrazione di WebSphere. Nella struttura di navigazione fare clic su **Server** > Server **** applicazioni e quindi, nel riquadro a destra, fare clic sul nome del server.

1. In Infrastruttura server, fare clic su **Java and Process Management** > Definizione **** processo.

1. In Proprietà aggiuntive fare clic su **Java Virtual Machine**.

   Nella casella Argomenti JVM generici, aggiungere l&#39;argomento `-Dreporting.publisher.cron = <expression>.`

   **Esempio**: La seguente espressione cron fa sì che Process Reporting pubblichi ogni 5 ore i dati di AEM Forms nell’archivio di Process Reporting:

   * `-Dreporting.publisher.cron = 0_0_0/5_*_*_?`

1. Fate clic su **Applica**, su OK, quindi su **Salva direttamente nella configurazione** principale.
1. Riavviate l&#39;istanza del server AEM Forms.
1. Arrestate l&#39;istanza del server AEM Forms.
1. Accedere alla console di amministrazione WebLogic. L&#39;indirizzo predefinito della console di amministrazione WebLogic è `https://[hostname]:[port]/console`.
1. In Centro modifiche, fate clic su **Blocca e modifica**.
1. In Struttura dominio, fare clic su **Ambiente** > **Server** e, nel riquadro a destra, fare clic sul nome del server gestito.
1. Nella schermata successiva, fate clic sulla scheda **Configurazione** > scheda Avvio **** server.
1. Nella casella Argomenti, aggiungere l&#39;argomento JVM `-Dreporting.publisher.cron = <expression>`.

   **Esempio**: La seguente espressione cron fa sì che Process Reporting pubblichi ogni 5 ore i dati di AEM Forms nell’archivio di Process Reporting:

   `-Dreporting.publisher.cron = 0_0_0/5_*_*_?`

1. Fate clic su **Salva** , quindi su **Attiva modifiche**.
1. Riavviate l&#39;istanza del server AEM Forms.

![processdatapublisherservice](assets/processdatapublisherservice.png)

### Servizio ProcessDataStorage {#processdatastorage-service}

Il servizio ProcessDataStorageProvider riceve i dati del processo dal servizio ProcessDataPublisher e li salva nell&#39;archivio di Process Reporting.

In ciascun ciclo di pubblicazione, i dati vengono salvati nelle sottocartelle di una cartella principale predefinita.

Puoi usare la console di amministrazione per configurare la radice (**impostazione predefinita**: `/content/reporting/pm`) posizione e sottocartella (**impostazione predefinita**: Formato `/yyyy/mm/dd/hh/mi/ss`) gerarchia in cui verranno memorizzati i dati del processo.

#### Per configurare i percorsi dell&#39;archivio di Process Reporting {#to-configure-the-process-reporting-repository-locations}

1. Accedete ad **Amministrazione Console** con le credenziali di amministratore. L’URL predefinito della console di amministrazione è `https://[server]:[port]/adminui`
1. Passare a **Home** > **Servizi** > **Applicazioni e servizi** > Gestione **** servizi e aprire il servizio **ProcessDataStorageProvider** .

   ![process-data-storage-service](assets/process-data-storage-service.png)

   **CartellaPrincipale**

   Posizione CRX all&#39;interno della quale i dati del processo vengono memorizzati per la generazione dei rapporti.

   `Default`: `/content/reporting/pm`

   **Gerarchia cartelle**

   La gerarchia di cartelle all’interno della quale i dati del processo vengono memorizzati in base al tempo di creazione del processo.

   `Default`: `/yyyy/mm/dd/hh/mi/ss`

1. Fai clic su **Salva**.

### Servizio ReportConfiguration {#reportconfiguration-service}

Il servizio ReportConfiguration viene utilizzato da Process Reporting per configurare il servizio di query di reporting del processo.

#### To configure the ReportingConfiguration service {#to-configure-the-reportingconfiguration-service}

1. Accedete a **Configuration Manager** con le credenziali di amministratore CRX. L&#39;URL predefinito di Configuration Manager è `https://[server]:[port]/lc/system/console/configMgr`
1. Aprire il servizio **ReportingConfiguration** .
1. **Numero di record**

   Quando si esegue una query nell&#39;archivio, un risultato può contenere un numero elevato di record. Se il set di risultati è grande, l&#39;esecuzione della query può utilizzare risorse del server.

   Per gestire set di risultati di grandi dimensioni, il servizio ReportConfiguration suddivide l&#39;elaborazione della query in batch di record. Questo riduce il carico del sistema.

   `Default`: `1000`

   **Percorso di archiviazione CRX**

   Posizione CRX all&#39;interno della quale i dati del processo devono essere memorizzati per la generazione di rapporti.

   `Default`: `/content/reporting/pm`

   >[!NOTE]
   >
   >Si tratta della stessa posizione specificata nell&#39;opzione di configurazione ProcessDataStorage **Root Folder**.
   >
   >
   >Se si aggiorna l&#39;opzione Cartella principale nella configurazione ProcessDataStorage, è necessario aggiornare il percorso del percorso di memorizzazione CRX nel servizio ReportConfiguration.

1. Fate clic su **Salva** e chiudete **CQ Configuration Manager**.

### Servizio ProcessDataPublisher {#processdatapublisher-service}

Il servizio ProcessDataPublisher importa i dati del processo dal database AEM Forms e li pubblica nel servizio ProcessDataStorageProvider per l&#39;archiviazione.

#### Per configurare il servizio ProcessDataPublisher {#to-configure-processdatapublisher-service-nbsp}

1. Accedete ad **Amministrazione Console** con le credenziali di amministratore.

   L’URL predefinito è `https://[server]:port]/adminui/`.

1. Passare a **Home** > **Servizi** > **Applicazioni e servizi** > Gestione **** servizi e aprire il servizio **ProcessDataPublisher** .

![processdatapublisherservice-1](assets/processdatapublisherservice-1.png)

**Pubblica dati**

Abilitate questa opzione per avviare la pubblicazione dei dati del processo. Per impostazione predefinita, l’opzione è disabilitata.

Abilita Process Reporting solo quando tutte le configurazioni relative ai componenti Process Reporting sono impostate correttamente.

In alternativa, utilizzare questa opzione per disabilitare la pubblicazione dei dati del processo quando non è più necessaria.

`Default`: `Off`

**Intervallo batch (sec)**

Ogni volta che il servizio ProcessDataPublisher viene eseguito, il servizio suddivide per la prima volta l&#39;ora dall&#39;ultima esecuzione del servizio in base all&#39;intervallo di batch. Il servizio elabora quindi ciascun intervallo di dati di AEM Forms separatamente.

Questo consente di controllare le dimensioni dei dati che l&#39;editore elabora e che terminano durante ogni esecuzione (batch) all&#39;interno di un ciclo.

Ad esempio, se l&#39;editore viene eseguito ogni giorno, per impostazione predefinita, invece di elaborare tutti i dati per un giorno in una singola esecuzione, suddivide l&#39;elaborazione in 24 batch di un&#39;ora l&#39;uno.

`Default`: `3600`

`Unit`: `Seconds`

**Timeout blocco (sec)**

Il servizio di pubblicazione acquisisce un blocco quando avvia l&#39;elaborazione dei dati in modo che più istanze dell&#39;editore non avviino l&#39;esecuzione e l&#39;elaborazione dei dati contemporaneamente.

Se un servizio di pubblicazione che ha acquisito un blocco è inattivo per il numero di secondi definito dal valore Blocca timeout, il blocco viene rilasciato in modo che altre istanze del servizio di pubblicazione possano continuare l&#39;elaborazione.

`Default`: `3600`

`Unit`: `Seconds`

**Pubblica dati da**

L&#39;ambiente AEM Forms contiene i dati del momento in cui è stato configurato l&#39;ambiente.

Per impostazione predefinita, il servizio ProcessDataPublisher importa tutti i dati dal database AEM Forms.

A seconda delle esigenze di reporting, se si prevede di eseguire rapporti e query sui dati dopo una determinata data e ora, è consigliabile specificare la data e l&#39;ora. Il servizio di pubblicazione pubblicherà la data a partire da tale data.

`Default`: `01-01-1970 00:00:00`

`Format`: `dd-MM-yyyy HH:mm:ss`

## Accesso all&#39;interfaccia utente di Process Reporting {#accessing-the-process-reporting-user-interface}

L&#39;interfaccia utente per Process Reporting è basata su browser.

Dopo aver configurato Process Reporting (Generazione rapporti sui processi), puoi iniziare a lavorare con Process Reporting nel seguente percorso nell&#39;installazione di AEM Forms:

`https://<server>:<port>/lc/pr`

### Accesso a Process Reporting {#log-in-to-process-reporting}

Quando vi spostate sull&#39;URL di Process Reporting (https://&lt;server>:&lt;porta>/lc/pr), viene visualizzata la schermata di accesso.

Specificare le credenziali per accedere al modulo Process Reporting.

>[!NOTE]
>
>Per accedere all&#39;interfaccia utente di Process Reporting, è necessario disporre della seguente autorizzazione AEM Forms:
>
>`PERM_PROCESS_REPORTING_USER`

![Login a Process Reporting](assets/capture1_new.png)

Quando si accede a Process Reporting (Generazione rapporti processo), viene visualizzata la schermata **[!UICONTROL Home]** .

### Home page Report processo {#process-reporting-home-screen}

![process-reporting-home-screen](assets/process-reporting-home-screen.png)

**** Visualizzazione struttura Report processo: La vista ad albero sul lato sinistro della schermata Home contiene gli elementi per i moduli di Process Reporting.

La struttura è composta dai seguenti elementi di primo livello:

**** Rapporti: Questo elemento contiene i report forniti con Process Reporting.

Per informazioni dettagliate sui rapporti predefiniti, consultate Report [predefiniti in Process Reporting](/help/forms/using/process-reporting/pre-defined-reports-in-process-reporting.md).

**** Query ad hoc: Questo elemento contiene opzioni per eseguire ricerche basate sui filtri per processi e attività.

Per informazioni dettagliate sulle query ad hoc, consultate Query [ad hoc in Process Reporting](/help/forms/using/process-reporting/adhoc-queries-in-process-reporting.md).

**** Personalizzato: Il nodo Personalizzato visualizza i rapporti personalizzati creati dall&#39;utente.

Per la procedura per creare e visualizzare rapporti personalizzati, vedi Report [personalizzati in Process Reporting](/help/forms/using/process-reporting/process-reporting-custom-reports.md).

**** Barra del titolo Report processo: La barra del titolo Report processo contiene alcune opzioni generiche che è possibile utilizzare quando si lavora nell&#39;interfaccia utente.

**** Titolo Report processo: Il titolo Reporting processo viene visualizzato nell&#39;angolo sinistro della barra del titolo.

Fate clic sul titolo in qualsiasi momento per tornare alla schermata iniziale.

**** Ora ultimo aggiornamento: I dati del processo vengono pubblicati in modo pianificato dal database di AEM Forms all&#39;archivio di Process Reporting.

L&#39;Ora ultimo aggiornamento visualizza l&#39;ultima data e l&#39;ora in cui gli aggiornamenti dei dati sono stati inviati all&#39;archivio di Process Reporting.

Per informazioni dettagliate sul servizio di pubblicazione dei dati e su come pianificare il servizio, consultare [Pianificare la pubblicazione](/help/forms/using/process-reporting/install-start-process-reporting.md#p-schedule-process-data-publishing-p) dei dati del processo nell&#39;articolo Guida introduttiva ai rapporti sui processi.

**** Utente di Process Reporting: Il nome utente connesso viene visualizzato a destra dell’ora dell’ultimo aggiornamento.

**** Elenco a discesa della barra del titolo Rapporti: L&#39;elenco a discesa nell&#39;angolo destro della barra del titolo Report processo contiene le seguenti opzioni:

* **[!UICONTROL Sincronizzazione]**: Sincronizzare l&#39;archivio di Process Reporting incorporato con il database AEM Forms.
* **[!UICONTROL Aiuto]**: Visualizzare la documentazione della Guida in linea su Process Reporting.
* **[!UICONTROL Disconnessione]**: Disconnessione da Process Reporting

[Contattare il supporto](https://www.adobe.com/account/sign-in.supportportal.html)
