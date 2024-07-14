---
title: Guida introduttiva ai report sui processi
description: Passaggi per iniziare a utilizzare AEM Forms su JEE Process Reporting
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: process-reporting
docset: aem65
exl-id: 1272e854-fa64-4bfd-b073-8fbcf210e9b5
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '1710'
ht-degree: 0%

---

# Guida introduttiva ai report sui processi{#getting-started-with-process-reporting}

La funzione di reporting sui processi consente agli utenti di AEM Forms di eseguire query sulle informazioni sui processi di AEM Forms attualmente definiti nell’implementazione di AEM Forms. Tuttavia, il reporting dei processi non accede ai dati direttamente dall’archivio di AEM Forms. I dati vengono pubblicati per la prima volta nel repository di Process Reporting in base a una pianificazione (*dal servizio ProcessDataPublisher e ProcessDataStorage* s). I report e le query in Process Reporting vengono quindi generati dai dati di Process Reporting pubblicati nel repository. Process Reporting viene installato come parte del modulo di Forms Workflow.

Questo articolo descrive i passaggi necessari per abilitare la pubblicazione dei dati di AEM Forms nell’archivio di Process Reporting. In seguito, sarà possibile utilizzare Report processi per eseguire report e query. Nell&#39;articolo vengono inoltre illustrate le opzioni disponibili per configurare i servizi di report dei processi.

## Prerequisiti per la generazione di rapporti sui processi {#process-reporting-pre-requisites}

### Eliminare i processi non essenziali {#purge-non-essential-processes}

Se si utilizza Forms Workflow, il database di AEM Forms potrebbe contenere una grande quantità di dati

I servizi di pubblicazione di Process Reporting pubblicano tutti i dati di AEM Forms attualmente disponibili nel database. Ciò implica che se il database contiene dati legacy sui quali non desideri eseguire report e query, anche tutti i dati verranno pubblicati nell’archivio, anche se non sono necessari per il reporting. Si consiglia di eliminare questi dati prima di eseguire i servizi per pubblicare i dati nel repository di Process Reporting. In questo modo si migliorano le prestazioni sia del servizio di pubblicazione che del servizio che esegue query sui dati per il reporting.

Per informazioni dettagliate sull&#39;eliminazione dei dati di processo di AEM Forms, vedere [Rimozione dei dati di processo](/help/forms/using/admin-help/purging-process-data.md).

>[!NOTE]
>
>Per i suggerimenti e i trucchi di Purge Utility, vedere l&#39;articolo di Adobe Developer Connection su [Rimozione di processi e processi](/help/forms/using/admin-help/purging-process-data.md).

## Configurazione di Process Reporting Services {#configuring-process-reporting-services}

### Pianifica pubblicazione dati processo {#schedule-process-data-publishing}

I servizi di report dei processi pubblicano i dati dal database di AEM Forms all&#39;archivio di report dei processi su base pianificata.

Questa operazione può richiedere molte risorse e può influire sulle prestazioni dei server AEM Forms. È consigliabile pianificare questa operazione all’esterno degli slot orari occupati del server AEM Forms.

Per impostazione predefinita, la pubblicazione dei dati viene pianificata per essere eseguita ogni giorno alle 02:00.

Per modificare la pianificazione di pubblicazione, effettuare le seguenti operazioni:

>[!NOTE]
>
>Se l’implementazione di AEM Forms viene eseguita su un cluster, effettua le seguenti operazioni su ciascun nodo del cluster.

1. Arresta l&#39;istanza di AEM Forms Server.
1. &#x200B;

   * (Per Windows) Aprire il file `[JBoss root]/bin/run.conf.bat` in un editor.
   * (Per Linux®, AIX® e Solaris™) `[JBoss root]/bin/run.conf.sh` file in un editor.

1. Aggiungi l&#39;argomento JVM `-Dreporting.publisher.cron = <expression>.`

   Esempio: la seguente espressione cron induce Process Reporting a pubblicare i dati di AEM Forms nell’archivio di Process Reporting ogni cinque ore:

   * `-Dreporting.publisher.cron = 0_0_0/5_*_*_?`

1. Salvare e chiudere il file `run.conf.bat`.

1. Riavvia l’istanza di AEM Forms Server.

1. Arresta l&#39;istanza di AEM Forms Server.
1. Accedere a WebSphere® Administrative Console. Nell&#39;albero di spostamento fare clic su **Server** > **Server applicazioni** e quindi nel riquadro di destra fare clic sul nome del server.

1. In Infrastruttura server fare clic su **Java™ e Gestione processi** > **Definizione processi**.

1. In Proprietà aggiuntive fare clic su **Java™ Virtual Machine**.

   Nella casella Argomenti JVM generici aggiungere l&#39;argomento `-Dreporting.publisher.cron = <expression>.`

   **Esempio**: la seguente espressione cron fa in modo che Process Reporting pubblichi i dati di AEM Forms nell&#39;archivio di Process Reporting ogni cinque ore:

   * `-Dreporting.publisher.cron = 0_0_0/5_*_*_?`

1. Fare clic su **Applica**, scegliere OK, quindi fare clic su **Salva direttamente nella configurazione principale**.
1. Riavvia l’istanza di AEM Forms Server.
1. Arresta l&#39;istanza di AEM Forms Server.
1. Accedere alla console di amministrazione WebLogic. L&#39;indirizzo predefinito della console di amministrazione WebLogic è `https://[hostname]:[port]/console`.
1. In Centro modifiche fare clic su **Blocca e modifica**.
1. In Struttura dominio fare clic su **Ambiente** > **Server** e nel riquadro di destra fare clic sul nome del server gestito.
1. Nella schermata successiva, fare clic sulla scheda **Configurazione** > **Avvio server**.
1. Nella casella Argomenti aggiungere l&#39;argomento JVM `-Dreporting.publisher.cron = <expression>`.

   **Esempio**: la seguente espressione cron fa in modo che Process Reporting pubblichi i dati di AEM Forms nell&#39;archivio di Process Reporting ogni cinque ore:

   `-Dreporting.publisher.cron = 0_0_0/5_*_*_?`

1. Fai clic su **Salva** e quindi su **Attiva modifiche**.
1. Riavvia l’istanza di AEM Forms Server.

![processdatapublisherservice](assets/processdatapublisherservice.png)

>[!NOTE]
>
> Per riavviare l&#39;SDK, si consiglia di utilizzare il comando &#39;Ctrl + C&#39;. Il riavvio dell’SDK dell’AEM con metodi alternativi, ad esempio l’arresto dei processi Java, può causare incongruenze nell’ambiente di sviluppo dell’AEM.

### Servizio ProcessDataStorage {#processdatastorage-service}

Il servizio ProcessDataStorageProvider riceve i dati di processo dal servizio ProcessDataPublisher e li salva nel repository di Process Reporting.

A ogni ciclo di pubblicazione, i dati vengono salvati nelle sottocartelle di una cartella principale predefinita.

È possibile utilizzare la console di amministrazione per configurare il formato della gerarchia radice (**default**: `/content/reporting/pm`) e della sottocartella (**default**: `/yyyy/mm/dd/hh/mi/ss`) in cui archiviare i dati del processo.

#### Per configurare i percorsi dell&#39;archivio di report dei processi {#to-configure-the-process-reporting-repository-locations}

1. Accedere a **Console di amministrazione** con le credenziali di amministratore. L&#39;URL predefinito della console di amministrazione è `https://'[server]:[port]'/adminui`
1. Passa alla **Home** > **Servizi** > **Applicazioni e servizi** >**Gestione servizi** e apri il servizio **ProcessDataStorageProvider**.

   ![process-data-storage-service](assets/process-data-storage-service.png)

   **CartellaPrincipale**

   Percorso CRX in cui memorizzare i dati del processo per il reporting.

   `Default`: `/content/reporting/pm`

   **Gerarchia cartelle**

   Gerarchia di cartelle in cui memorizzare i dati del processo in base all&#39;ora di creazione del processo.

   `Default`: `/yyyy/mm/dd/hh/mi/ss`

1. Fai clic su **Salva**.

### Servizio ReportConfiguration {#reportconfiguration-service}

Il servizio ReportConfiguration viene utilizzato da Process Reporting per la configurazione del servizio query di report dei processi.

#### Per configurare il servizio ReportingConfiguration {#to-configure-the-reportingconfiguration-service}

1. Accedere a **Configuration Manager** con le credenziali di amministratore CRX. L&#39;URL predefinito di Configuration Manager è `https://'[server]:[port]'/lc/system/console/configMgr`
1. Apri il servizio **ReportingConfiguration**.
1. **Numero di record**

   Quando si esegue una query nel repository, un risultato può potenzialmente contenere molti record. Se il set di risultati è grande, l’esecuzione della query può utilizzare risorse del server.

   Per gestire set di risultati di grandi dimensioni, il servizio ReportConfiguration suddivide l&#39;elaborazione della query in batch di record. In questo modo si riduce il carico del sistema.

   `Default`: `1000`

   **Percorso archiviazione CRX**

   Posizione CRX in cui archiviare i dati del processo per il reporting.

   `Default`: `/content/reporting/pm`

   >[!NOTE]
   >
   >Il percorso è uguale a quello specificato nell&#39;opzione di configurazione ProcessDataStorage **Root Folder**.
   >
   >
   >Se si aggiorna l&#39;opzione Root Folder nella configurazione ProcessDataStorage, è necessario aggiornare il percorso di archiviazione di CRX nel servizio ReportConfiguration.

1. Fai clic su **Salva** e chiudi **CQ Configuration Manager**.

### Servizio ProcessDataPublisher {#processdatapublisher-service}

Il servizio ProcessDataPublisher importa i dati di processo dal database di AEM Forms e li pubblica nel servizio ProcessDataStorageProvider per l&#39;archiviazione.

#### Per configurare il servizio ProcessDataPublisher   {#to-configure-processdatapublisher-service-nbsp}

1. Accedere a **Console di amministrazione** con le credenziali di amministratore.

   URL predefinito: `https://'server':port]/adminui/`.

1. Passa alla **Home** > **Servizi** > **Applicazioni e servizi** >**Gestione servizi** e apri il servizio **ProcessDataPublisher**.

![processdatapublisherservice-1](assets/processdatapublisherservice-1.png)

**Dati Publish**

Abilita questa opzione per avviare la pubblicazione dei dati del processo. Per impostazione predefinita, l’opzione è disabilitata.

Abilitare Process Reporting solo quando tutte le configurazioni correlate ai componenti di Process Reporting sono impostate in modo appropriato.

In alternativa, utilizzare questa opzione per disabilitare la pubblicazione dei dati di processo quando non è più necessaria.

`Default`: `Off`

**Intervallo batch (sec)**

Ogni volta che viene eseguito il servizio ProcessDataPublisher, il servizio suddivide per l&#39;intervallo batch il tempo trascorso dall&#39;ultima esecuzione del servizio. Il servizio elabora quindi separatamente ogni intervallo di dati di AEM Forms per controllare la dimensione dei dati elaborati dall’editore in modalità end-to-end durante ogni esecuzione (batch) di un ciclo.

Ad esempio, se l’editore viene eseguito ogni giorno, invece di elaborare tutti i dati per un giorno in una singola esecuzione, per impostazione predefinita l’elaborazione viene suddivisa in 24 batch da un’ora ciascuno.

`Default`: `3600`

`Unit`: `Seconds`

**Timeout blocco (sec)**

Il servizio di pubblicazione acquisisce un blocco quando inizia l&#39;elaborazione dei dati in modo che più istanze dell&#39;autore non inizino a eseguire ed elaborare i dati contemporaneamente.

Se un servizio di pubblicazione che ha acquisito un blocco è inattivo per il numero di secondi definito dal valore di Timeout blocco, il relativo blocco viene rilasciato in modo che altre istanze del servizio di pubblicazione possano continuare l&#39;elaborazione.

`Default`: `3600`

`Unit`: `Seconds`

**Dati Publish Da**

L’ambiente AEM Forms contiene i dati relativi al momento in cui è stato configurato.

Per impostazione predefinita, il servizio ProcessDataPublisher importa tutti i dati dal database di AEM Forms.

A seconda delle esigenze di reporting, se prevedi di eseguire rapporti e query sui dati dopo una certa data e ora, è consigliabile specificare la data e l’ora. Il servizio di pubblicazione pubblica quindi la data da tale data in poi.

`Default`: `01-01-1970 00:00:00`

`Format`: `dd-MM-yyyy HH:mm:ss`

## Accesso all&#39;interfaccia utente di Process Reporting {#accessing-the-process-reporting-user-interface}

L&#39;interfaccia utente di Process Reporting è basata su browser.

Dopo aver impostato Report processi, puoi iniziare a utilizzare Reporting processi nella seguente posizione nell’installazione di AEM Forms:

`https://<server>:<port>/lc/pr`

### Accedi a Reporting processi {#log-in-to-process-reporting}

Quando si passa all&#39;URL di Process Reporting (https://&lt;server>:&lt;port>/lc/pr), viene visualizzata la schermata di accesso.

Per accedere al modulo Report processi, specificare le credenziali.

>[!NOTE]
>
>Per accedere all&#39;interfaccia utente di Process Reporting, è necessario disporre delle seguenti autorizzazioni AEM Forms:
>
>`PERM_PROCESS_REPORTING_USER`

![Accesso al report dei processi](assets/capture1_new.png)

Quando accedi a Reporting processi, viene visualizzata la schermata **[!UICONTROL Home]**.

### Schermata Home di Process Reporting {#process-reporting-home-screen}

![process-reporting-home-screen](assets/process-reporting-home-screen.png)

**Visualizzazione struttura report processi:** La visualizzazione struttura sul lato sinistro della schermata iniziale contiene gli elementi per i moduli Report processi.

La struttura ad albero è costituita dai seguenti elementi di primo livello:

**Report:** questo elemento contiene i report preconfigurati forniti con Process Reporting.

Per informazioni dettagliate sui report predefiniti, vedere [Report predefiniti in Process Reporting](/help/forms/using/process-reporting/pre-defined-reports-in-process-reporting.md).

**Query ad hoc:** questo elemento contiene opzioni per eseguire ricerche basate su filtri per processi e attività.

Per informazioni dettagliate sulle query ad hoc, vedere [Query ad hoc in Report processi](/help/forms/using/process-reporting/adhoc-queries-in-process-reporting.md).

**Personalizzato:** Nel nodo Personalizzato vengono visualizzati i report personalizzati creati dall&#39;utente.

Per la procedura per la creazione e la visualizzazione di report personalizzati, vedere [Report personalizzati in Report di processo](/help/forms/using/process-reporting/process-reporting-custom-reports.md).

**Barra del titolo di Report di processo:** La barra del titolo di Report di processo contiene alcune opzioni generiche che è possibile utilizzare quando si lavora nell&#39;interfaccia utente.

**Titolo report processi:** Il titolo Report processi viene visualizzato nell&#39;angolo sinistro della barra del titolo.

Fare clic sul titolo in qualsiasi momento per tornare alla schermata iniziale.

**Ora ultimo aggiornamento:** i dati del processo vengono pubblicati dal database di AEM Forms nell&#39;archivio di Process Reporting in base alla pianificazione.

Ora ultimo aggiornamento visualizza la data e l&#39;ora dell&#39;ultimo push degli aggiornamenti dei dati all&#39;archivio di report dei processi.

Per informazioni dettagliate sul servizio di pubblicazione dei dati e sulla pianificazione di questo servizio, vedere [Pianificare la pubblicazione dei dati del processo](/help/forms/using/process-reporting/install-start-process-reporting.md#p-schedule-process-data-publishing-p) nell&#39;articolo Guida introduttiva al reporting dei processi.

**Utente report processi:** il nome utente connesso viene visualizzato a destra dell&#39;ora dell&#39;ultimo aggiornamento.

**Elenco a discesa della barra del titolo del report processi:** L&#39;elenco a discesa nell&#39;angolo destro della barra del titolo del report processi contiene le opzioni seguenti:

* **[!UICONTROL Sincronizza]**: sincronizza l&#39;archivio di report dei processi incorporato con il database di AEM Forms.
* **[!UICONTROL Guida]**: visualizza la documentazione della Guida sul reporting dei processi.
* **[!UICONTROL Disconnessione]**: disconnessione da Report processi


