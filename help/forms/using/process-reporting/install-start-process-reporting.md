---
title: Guida introduttiva alla generazione di rapporti sui processi
seo-title: Getting Started with Process Reporting
description: I passaggi da seguire per iniziare a utilizzare AEM Forms su JEE Process Reporting
seo-description: The steps you need to follow to get started with AEM Forms on JEE Process Reporting
uuid: 685cad39-da2c-411d-a0b0-201917438bcf
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: process-reporting
discoiquuid: 7c1fcde0-b983-4b24-bc19-fcee1d4f096b
docset: aem65
exl-id: 1272e854-fa64-4bfd-b073-8fbcf210e9b5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1710'
ht-degree: 0%

---

# Guida introduttiva alla generazione di rapporti sui processi{#getting-started-with-process-reporting}

La funzione di reporting dei processi consente agli utenti di AEM Forms di inviare query alle informazioni sui processi AEM Forms attualmente definiti nell’implementazione di AEM Forms. Tuttavia, Process Reporting non accede direttamente ai dati dall&#39;archivio AEM Forms. I dati vengono pubblicati per la prima volta nell&#39;archivio di Process Reporting su base programmata (*dal servizio ProcessDataPublisher e ProcessDataStorage* s). I report e le query in Process Reporting vengono quindi generati dai dati di Process Reporting pubblicati nell&#39;archivio. Report del processo è installato come parte del modulo del Forms Workflow.

Questo articolo descrive i passaggi per abilitare la pubblicazione dei dati di AEM Forms nell’archivio di Process Reporting. Dopo di che, potrai utilizzare Report di processo per eseguire report e query. L&#39;articolo illustra anche le opzioni disponibili per configurare i servizi di reporting dei processi.

## Prerequisiti per la generazione di rapporti sui processi {#process-reporting-pre-requisites}

### Eliminare i processi non essenziali {#purge-non-essential-processes}

Se si utilizza Forms Workflow, il database AEM Forms può contenere potenzialmente una grande quantità di dati

I servizi di pubblicazione Process Reporting pubblicheranno tutti i dati di AEM Forms attualmente disponibili nel database. Ciò implica che, se il database contiene dati legacy sui quali non desideri eseguire rapporti e query, anche tutti i dati verranno pubblicati nell’archivio anche se non è necessario per il reporting. È consigliabile eliminare questi dati prima di eseguire i servizi per pubblicare i dati nell&#39;archivio di Process Reporting. Ciò migliorerà le prestazioni sia del servizio di pubblicazione che del servizio che invia query ai dati per la creazione di rapporti.

Per informazioni dettagliate sull&#39;eliminazione dei dati del processo AEM Forms, vedi [Rimozione dei dati del processo](https://help.adobe.com/en_US/livecycle/11.0/AdminHelp/WS92d06802c76abadb-5145d5d12905ce07e7-7cb2.2.html).

>[!NOTE]
>
>Per suggerimenti e trucchi di Purge Utility, vedi l&#39;articolo Adobe Developer Connection su [Rimozione di processi e processi](https://www.adobe.com/content/dam/Adobe/en/devnet/livecycle/pdfs/purging_processes_jobs.pdf).

## Configurazione dei servizi di reporting dei processi {#configuring-process-reporting-services}

### Pianificazione della pubblicazione dei dati del processo {#schedule-process-data-publishing}

I servizi di reporting dei processi pubblicano i dati dal database AEM Forms all&#39;archivio di Process Reporting su base pianificata.

Questa operazione può richiedere molte risorse e può influire sulle prestazioni dei server AEM Forms. È consigliabile pianificare questo passaggio al di fuori degli slot dedicati del server AEM Forms.

Per impostazione predefinita, la pubblicazione dei dati è pianificata per essere eseguita ogni giorno alle 2:00.

Esegui i seguenti passaggi per modificare la pianificazione della pubblicazione:

>[!NOTE]
>
>Se esegui l&#39;implementazione AEM Forms su un cluster, esegui i seguenti passaggi su ciascun nodo del cluster.

1. Arresta l’istanza del server AEM Forms.
1. &#x200B;

   * (Per Windows) Apri il `[JBoss root]/bin/run.conf.bat` in un editor.
   * (per Linux, AIX e Solaris) `[JBoss root]/bin/run.conf.sh` in un editor.

1. Aggiungi l&#39;argomento JVM `-Dreporting.publisher.cron = <expression>.`

   Esempio: La seguente espressione cron causa la pubblicazione dei dati di AEM Forms nel repository di Process Reporting ogni 5 ore:

   * `-Dreporting.publisher.cron = 0_0_0/5_*_*_?`

1. Salva e chiudi il `run.conf.bat` file.

1. Riavvia l&#39;istanza del server AEM Forms.

1. Arresta l’istanza del server AEM Forms.
1. Accedi alla console amministrativa WebSphere. Nella struttura di navigazione, fai clic su **Server** > **Server applicazioni** quindi, nel riquadro a destra, fare clic sul nome del server.

1. In Infrastruttura server fare clic su **Java e Process Management** > **Definizione del processo**.

1. In Proprietà aggiuntive, fai clic su **Java Virtual Machine**.

   Nella casella Argomenti JVM generici, aggiungi l’argomento `-Dreporting.publisher.cron = <expression>.`

   **Esempio**: La seguente espressione cron causa la pubblicazione dei dati di AEM Forms nel repository di Process Reporting ogni 5 ore:

   * `-Dreporting.publisher.cron = 0_0_0/5_*_*_?`

1. Fai clic su **Applica**, fare clic su OK, quindi fare clic su **Salva direttamente nella configurazione principale**.
1. Riavvia l&#39;istanza del server AEM Forms.
1. Arresta l’istanza del server AEM Forms.
1. Accedi alla console di amministrazione WebLogic. L’indirizzo predefinito della console di amministrazione WebLogic è `https://[hostname]:[port]/console`.
1. In Cambia centro, fai clic su **Blocco e modifica**.
1. In Struttura del dominio, fai clic su **Ambiente** > **Server** nel riquadro a destra fare clic sul nome del server gestito.
1. Nella schermata successiva, fai clic sul pulsante **Configurazione** scheda > **Avvio server** scheda .
1. Nella casella Argomenti , aggiungi l’argomento JVM `-Dreporting.publisher.cron = <expression>`.

   **Esempio**: La seguente espressione cron causa la pubblicazione dei dati di AEM Forms nel repository di Process Reporting ogni 5 ore:

   `-Dreporting.publisher.cron = 0_0_0/5_*_*_?`

1. Fai clic su **Salva** quindi fai clic su **Attiva modifiche**.
1. Riavvia l&#39;istanza del server AEM Forms.

![processdatapublisherservice](assets/processdatapublisherservice.png)

### Servizio ProcessDataStorage {#processdatastorage-service}

Il servizio ProcessDataStorageProvider riceve i dati di processo dal servizio ProcessDataPublisher e li salva nell&#39;archivio di Process Reporting.

A ogni ciclo di pubblicazione, i dati vengono salvati in sottocartelle di una cartella principale predefinita.

Puoi usare la console di amministrazione per configurare la radice (**default**: `/content/reporting/pm`) posizione e sottocartella (**default**: `/yyyy/mm/dd/hh/mi/ss`) formato gerarchico in cui verranno memorizzati i dati del processo.

#### Per configurare le posizioni dell&#39;archivio di Process Reporting {#to-configure-the-process-reporting-repository-locations}

1. Accedi a **Console di amministrazione** con le credenziali di amministratore. L’URL predefinito della console di amministrazione è `https://'[server]:[port]'/adminui`
1. Passa a **Pagina principale** > **Servizi** > **Applicazioni e servizi** >**Gestione dei servizi** e aprire **ProcessDataStorageProvider** servizio.

   ![service di storage-data-process](assets/process-data-storage-service.png)

   **Cartella principale**

   La posizione CRX all&#39;interno della quale i dati del processo sarebbero memorizzati per il reporting.

   `Default`: `/content/reporting/pm`

   **Gerarchia cartelle**

   La gerarchia delle cartelle all&#39;interno della quale verranno memorizzati i dati del processo in base al tempo di creazione del processo.

   `Default`: `/yyyy/mm/dd/hh/mi/ss`

1. Fai clic su **Salva**.

### Servizio ReportConfiguration {#reportconfiguration-service}

Il servizio ReportConfiguration viene utilizzato da Process Reporting per configurare il servizio query di reporting del processo.

#### Per configurare il servizio ReportingConfiguration {#to-configure-the-reportingconfiguration-service}

1. Accedi a **Gestione configurazione** con le credenziali di amministratore CRX. L’URL predefinito di Configuration Manager è `https://'[server]:[port]'/lc/system/console/configMgr`
1. Apri **ReportingConfiguration** servizio.
1. **Numero di record**

   Quando si esegue una query nell&#39;archivio, un risultato può contenere potenzialmente un gran numero di record. Se il set di risultati è grande, l’esecuzione della query può utilizzare risorse server.

   Per gestire set di risultati di grandi dimensioni, il servizio ReportConfiguration suddivide l&#39;elaborazione della query in batch di record. Questo riduce il carico del sistema.

   `Default`: `1000`

   **Percorso di archiviazione CRX**

   La posizione CRX all&#39;interno della quale i dati del processo devono essere memorizzati per il reporting.

   `Default`: `/content/reporting/pm`

   >[!NOTE]
   >
   >Si tratta della stessa posizione specificata nell&#39;opzione di configurazione ProcessDataStorage **Cartella principale**.
   >
   >
   >Se si aggiorna l&#39;opzione Cartella principale nella configurazione ProcessDataStorage, è necessario aggiornare il percorso di archiviazione CRX nel servizio ReportConfiguration.

1. Fai clic su **Salva** e chiudi **Gestione configurazione CQ**.

### Servizio ProcessDataPublisher {#processdatapublisher-service}

Il servizio ProcessDataPublisher importa i dati del database AEM Forms e li pubblica nel servizio ProcessDataStorageProvider per l&#39;archiviazione.

#### Per configurare il servizio ProcessDataPublisher   {#to-configure-processdatapublisher-service-nbsp}

1. Accedi a **Console di amministrazione** con le credenziali di amministratore.

   L’URL predefinito è `https://'server':port]/adminui/`.

1. Passa a **Pagina principale** > **Servizi** > **Applicazioni e servizi** >**Gestione dei servizi** e aprire **ProcessDataPublisher** servizio.

![processdatapublisherservice-1](assets/processdatapublisherservice-1.png)

**Pubblicare dati**

Abilita questa opzione per avviare la pubblicazione dei dati del processo. Per impostazione predefinita, l’opzione è disabilitata.

Abilitare la generazione di rapporti sui processi solo quando tutte le configurazioni relative ai componenti di reporting dei processi sono impostate in modo appropriato.

In alternativa, utilizza questa opzione per disabilitare la pubblicazione dei dati del processo quando non è più necessaria.

`Default`: `Off`

**Intervallo batch (sec)**

Ogni volta che il servizio ProcessDataPublisher viene eseguito, il servizio suddivide prima l&#39;ora dall&#39;ultima esecuzione del servizio dall&#39;intervallo batch. Il servizio elabora quindi separatamente ogni intervallo di dati di AEM Forms.

Questo aiuta a controllare le dimensioni dei dati che l’editore elabora end-to-end durante ogni esecuzione (batch) all’interno di un ciclo.

Ad esempio, se l’editore esegue ogni giorno, invece di elaborare tutti i dati per un giorno in una singola esecuzione, per impostazione predefinita suddivide l’elaborazione in 24 batch di un’ora ciascuno.

`Default`: `3600`

`Unit`: `Seconds`

**Timeout blocco (sec)**

Il servizio di pubblicazione acquisisce un blocco quando inizia a elaborare i dati in modo che più istanze dell’editore non inizino a eseguire ed elaborare i dati contemporaneamente.

Se un servizio di pubblicazione che ha acquisito un blocco è inattivo per il numero di secondi definiti dal valore Blocca timeout, il relativo blocco viene rilasciato in modo che altre istanze del servizio di pubblicazione possano continuare l&#39;elaborazione.

`Default`: `3600`

`Unit`: `Seconds`

**Pubblica dati da**

L’ambiente AEM Forms contiene i dati del momento in cui è stato configurato l’ambiente.

Per impostazione predefinita, il servizio ProcessDataPublisher importa tutti i dati dal database AEM Forms.

A seconda delle esigenze di reporting, se si prevede di eseguire rapporti e query sui dati dopo una data e un&#39;ora determinate, è consigliabile specificare la data e l&#39;ora. Il servizio di pubblicazione pubblicherà quindi la data a partire da tale data.

`Default`: `01-01-1970 00:00:00`

`Format`: `dd-MM-yyyy HH:mm:ss`

## Accesso all’interfaccia utente di Process Reporting {#accessing-the-process-reporting-user-interface}

L&#39;interfaccia utente per Process Reporting è basata su browser.

Dopo aver impostato Process Reporting, puoi iniziare a lavorare con Process Reporting nel seguente percorso nell&#39;installazione di AEM Forms:

`https://<server>:<port>/lc/pr`

### Accedere a Report sul processo {#log-in-to-process-reporting}

Quando passi all&#39;URL di reporting del processo (https://)&lt;server>:&lt;port>/lc/pr), viene visualizzata la schermata di accesso.

Specificare le credenziali per accedere al modulo Report processo.

>[!NOTE]
>
>Per accedere all&#39;interfaccia utente di Process Reporting è necessario disporre della seguente autorizzazione AEM Forms:
>
>`PERM_PROCESS_REPORTING_USER`

![Accesso a Report di processo](assets/capture1_new.png)

Quando si accede a Reporting del processo, la **[!UICONTROL Pagina principale]** viene visualizzato lo schermo.

### Schermata Home di Report del processo {#process-reporting-home-screen}

![processo-reporting-home-screen](assets/process-reporting-home-screen.png)

**Visualizzazione struttura Report processi:** La visualizzazione ad albero sul lato sinistro della schermata Home contiene gli elementi per i moduli di Reporting del processo.

La vista ad albero è costituita dai seguenti elementi di primo livello:

**Rapporti:** Questo elemento contiene i report preconfigurati forniti con Report processi.

Per informazioni dettagliate sui rapporti predefiniti, vedi [Rapporti predefiniti nel reporting dei processi](/help/forms/using/process-reporting/pre-defined-reports-in-process-reporting.md).

**Query ad hoc:** Questo elemento contiene opzioni per eseguire ricerche basate su filtri per processi e attività.

Per informazioni dettagliate sulle query ad hoc, vedi [Query ad hoc nel reporting dei processi](/help/forms/using/process-reporting/adhoc-queries-in-process-reporting.md).

**Personalizzato:** Il nodo Personalizzato visualizza i rapporti personalizzati creati dall&#39;utente.

Per la procedura di creazione e visualizzazione dei rapporti personalizzati, consulta [Report personalizzati in Reporting dei processi](/help/forms/using/process-reporting/process-reporting-custom-reports.md).

**Barra del titolo del report del processo:** La barra del titolo Report del processo contiene alcune opzioni generiche che è possibile utilizzare quando si lavora nell&#39;interfaccia utente.

**Titolo del report del processo:** Il titolo Reporting del processo viene visualizzato nell&#39;angolo sinistro della barra del titolo.

Fare clic sul titolo in qualsiasi momento per tornare alla schermata iniziale.

**Ora ultimo aggiornamento:** I dati del processo vengono pubblicati dal database AEM Forms all&#39;archivio di Process Reporting su base pianificata.

L&#39;ora ultimo aggiornamento visualizza la data e l&#39;ora fino a cui gli aggiornamenti dei dati sono stati inviati all&#39;archivio di Process Reporting.

Per informazioni dettagliate sul servizio di pubblicazione dei dati e su come pianificare il servizio, consulta [Pianificazione della pubblicazione dei dati del processo](/help/forms/using/process-reporting/install-start-process-reporting.md#p-schedule-process-data-publishing-p) nell&#39;articolo Guida introduttiva alla generazione di rapporti sui processi.

**Utente di Report del processo:** Il nome utente connesso viene visualizzato a destra dell&#39;ora dell&#39;ultimo aggiornamento.

**Elenco a discesa Barra del titolo del rapporto di processo:** L&#39;elenco a discesa nell&#39;angolo a destra della barra del titolo Report processo contiene le seguenti opzioni:

* **[!UICONTROL Sincronizzazione]**: Sincronizzare l&#39;archivio di Process Reporting incorporato con il database AEM Forms.
* **[!UICONTROL Aiuto]**: Visualizzare la documentazione della Guida in linea su Reporting dei processi.
* **[!UICONTROL Logout]**: Esci da Report processo
