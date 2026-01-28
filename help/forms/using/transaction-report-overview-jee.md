---
title: Panoramica dei rapporti sulle transazioni per AEM Forms su JEE
description: Mantieni un conteggio di tutti i moduli inviati, sottoposti a rendering, documenti convertiti in un formato in un altro e altro ancora.
feature: Transaction Reports
exl-id: 77e95631-6b0d-406e-a1b8-78f8d9cceb63
role: Admin, User, Developer
solution: "Experience Manager, Experience Manager Forms"
source-git-commit: 5699f5814daf16a397eb6129b881ac2035456e39
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 2%

---


# Abilitazione e visualizzazione dei rapporti sulle transazioni per AEM Forms su JEE {#transaction-reports-overview}

<span> È stata introdotta la funzionalità di reporting delle transazioni per [AEM Forms su JEE da AEM Forms 6.5.20.0](/help/release-notes/previous/6-5-20.md#forms). Questa funzionalità è disabilitata per impostazione predefinita e può essere abilitata dall&#39;interfaccia utente amministratore.</span>

I rapporti sulle transazioni in AEM Forms su JEE ti consentono di tenere un conteggio di tutte le transazioni eseguite nella distribuzione AEM Forms. L’obiettivo è quello di fornire informazioni sull’utilizzo dei prodotti e aiutare le parti interessate a comprendere i propri volumi di elaborazione digitale. Di seguito sono riportati alcuni esempi di transazioni:

* Presentazione di un documento
* Rappresentazione di un documento
* Conversione di un documento da un formato di file a un altro

Per ulteriori informazioni su quella che viene considerata una transazione, vedere [API fatturabili](../../forms/using/transaction-reports-billable-apis-jee.md).

## Abilita reporting delle transazioni {#enable-transaction-reporting}

Per impostazione predefinita, la registrazione delle transazioni è disabilitata. Per abilitare il reporting delle transazioni, effettuare le seguenti operazioni:

1. Passa a `/adminui` nel tuo AEM Forms su JEE, ad esempio `http://10.14.18.10:8080/adminui`.
1. Accedi come **Amministratore**.
1. Vai a **Impostazioni** > **Impostazioni sistema core** > **Configurazioni**.
1. Fai clic sulla casella di controllo per **abilitare la generazione di rapporti sulle transazioni** e **salvare** le impostazioni.

   ![sample-transaction-report-jee](assets/enable-transaction-jee.png)

1. Riavvia il server.
1. A parte le modifiche sul server, sul lato client è necessario aggiornare il file `adobe-livecycle-client.jar` nel progetto, se si utilizza lo stesso.

<!--
* You can [enable transaction recording](../../forms/using/viewing-and-understanding-transaction-reports.md#setting-up-transaction-reports) from AEM Web Console. view transaction reports on author, processing, or publish instances. View transaction reports on author or processing instances for an aggregated sum of all transactions. View transaction reports on the publish instances for a count of all transactions that take place only on that publish instance from where the report is run.
-->

<!--Do not author content (Create adaptive forms, interactive communication, themes, and other authoring activities) and process documents (Use workflows, document services, and other processing activities) on the same AEM instance. Keep the transaction recording disabled for AEM Forms servers used to author content. Keep the transaction recording enabled for AEM Forms servers used to process documents.-->

## Visualizzazione del report delle transazioni {#view-transaction-report}

Quando si abilita il reporting delle transazioni, le informazioni sui conteggi delle transazioni diventano accessibili tramite il report [transazioni tramite dashboard](#transaction-report-dashboard) e un report dettagliato [transazioni tramite il file di registro](#transaction-report-logfile). Entrambi sono descritti di seguito:

### Rapporto di transazione tramite dashboard {#transaction-report-dashboard}

Il rapporto di transazione tramite dashboard fornisce il numero totale di transazioni conteggiate per ogni tipo di transazione. Ad esempio, si ottengono le informazioni sul numero totale di moduli sottoposti a rendering, convertiti e inviati come mostrato nell’immagine. Per ottenere il report delle transazioni:

1. Passa a `/adminui` nel tuo AEM Forms su JEE, ad esempio: `http://10.13.15.08:8080/adminui`.
1. Accedi come **Amministratore**.
1. Fare clic su Health Monitor.
1. Passa alla scheda **Transaction Reporter** e fai clic su **Calcola transazioni totali**. Ora puoi vedere che un grafico a torta rappresenta il numero di PDF forms inviati, sottoposti a rendering o convertiti.

![sample-transaction-report-jee](assets/transaction-piechart.png)


### Rapporto di transazione tramite file di registro {#transaction-report-logfile}

Il report delle transazioni tramite file di log fornisce informazioni dettagliate su ciascuna transazione. Per accedere ai log delle transazioni, seguire il percorso contestuale relativo all&#39;avvio del server. Per impostazione predefinita, le transazioni vengono acquisite in un file di log separato `transaction_log.log`. Il percorso del file **&#x200B;**&#x200B;è relativo al contesto di avvio del server. Il percorso predefinito per i diversi server è indicato di seguito:

```
For Jboss Turnkey:
"<AEM_Forms_Installation>/jboss/bin/transaction_log.log"

For IBM Websphere: 
"<IBM_WAS_Profile_path>/transaction_log.log"

For Oracle Weblogic:
"<Weblogic_Domain_path>/transaction_log.log"

For Jboss Cluster:
"<Jboss home>/transaction_log.log"
```

Esempio di un record di transazione di esempio:
`[2024-02-28 06:11:27] [INFO] TransactionRecord{service='GeneratePDFService', operation='HtmlFileToPDF', internalService='GeneratePDFService', internalOperation='HtmlFileToPDF', transactionOperationType='CONVERT', transactionCount=1, elapsedTime=1906, transactionDate=Wed Feb 28 06:11:25 UTC 2024}`

#### Record transazione {#transaction-record-structure-jee}

La struttura del registro delle transazioni definisce il modo in cui ogni transazione viene registrata tramite i vari parametri, ad esempio servizio, operazione, tipo di transazione e altri. Ciascuno è fornito in dettaglio di seguito. La struttura del record di transazione è la seguente:

```
TransactionRecord
{
    service='...', 
    operation='...', 
    internalService='...', 
    internalOperation='...', 
    transactionOperationType='...', 
    transactionCount=..., 
    elapsedTime=..., 
    transactionDate=...
}
```

* **servizio**: nome del servizio.
* **operazione**: nome operazione.
* **internalService**: nome del destinatario della chiamata se è presente una chiamata interna, altrimenti uguale al nome del servizio.
* **internalOperation**: il nome del destinatario della chiamata è una chiamata interna, altrimenti corrisponde al nome dell&#39;operazione.
* **transactionOperationType**: tipo di transazione (Submit, Render, Convert).
* **transactionCount**: conteggio totale della transazione.
* **elapsedTime**: tempo tra l&#39;avvio della chiamata e la risposta ricevuta.
* **transactionDate**: timestamp che indica quando è stato richiamato il servizio.

**Registro transazioni di esempio**:

```
[2024-02-14 14:23:25] [INFO] TransactionRecord
{
    service='BarcodedFormsService', 
    operation='decode', 
    internalService='BarcodedFormsService', 
    internalOperation='decode', 
    transactionOperationType='CONVERT', 
    transactionCount=1, 
    elapsedTime=47405, 
    transactionDate=Wed Feb 14 14:22:37 UTC 2024
}
```

## Frequenza di registrazione delle transazioni {#transaction-recording-frequency}

<!--Transaction persistence involves updating the total transaction count for SUBMIT, CONVERT, and RENDER operations on the server periodically: -->

La frequenza di registrazione delle transazioni è determinata dalle operazioni di aggiornamento sul server per ogni modulo inviato, sottoposto a rendering o convertito correttamente.

* In **dashboard** il conteggio delle transazioni viene aggiornato periodicamente. Il valore predefinito è 1 minuto. È possibile aggiornare la frequenza impostando la proprietà di sistema su `"com.adobe.idp.dsc.transaction.recordFrequency"`. Ad esempio, in AEM Forms per JEE su JBoss®, aggiungi `-Dcom.adobe.idp.dsc.transaction.recordFrequency=5` in `JAVA_OPTS` per impostare la frequenza di aggiornamento su 5 minuti.

* Nei **registri transazioni**, l&#39;aggiornamento di ogni transazione viene eseguito immediatamente quando un modulo viene inviato, sottoposto a rendering o convertito correttamente.

<!-- A transaction remains in the buffer for a specified period (Flush Buffer time + Reverse replication time). By default, it takes approximately 90 seconds for the transaction count to reflect in the transaction report.

Actions like submitting a PDF Form, using Agent UI to preview an interactive communication, or using non-standard form submission methods are not accounted as transactions. AEM Forms provides an API to record such transactions. Call the API from your custom implementations to record a transaction.

## Supported Topology {#supported-topology}

Transaction reports are available only on AEM Forms on OSGi environment. It supports author-publish, author-processing-publish, and only processing topologies. For example, topologies, see [Architecture and deployment topologies for AEM Forms](../../forms/using/transaction-reports-overview.md).

The transaction count is reverse replicated from publish instances to author or processing instances. An indicative author-publish topology is displayed below:

![simple-author-publish-topology](assets/simple-author-publish-topology.png)

>[!NOTE]
>
>AEM Forms transaction reports does not support topologies that contain only publish instances.

### Guidelines for using transaction reports {#guidelines-for-using-transaction-reports}

* Disable transaction reports on all author instances as reports on author instances includes transactions registered during authoring activities.
* Enable the **Show transactions from publish only** option on the author instance to view cumulative transactions from all publish instances. You can also view transaction reports on each publish instance for actual transactions on that particular publish instance only.
* Do not use author instances to run workflows and process documents.
* Before using transaction reporting, if you are have a toplogy with publish servers, ensure that the reverse replication is enabled for all the publish instances.
* Transaction data is reverse-replicated from a publish instance to only corresponding author or processing instance. The author or processing instance cannot further replicate data to another instance. For example, if you have author-processing-publish topology, aggregated transaction data is replicated only to the processing instance.-->

## Articoli correlati {#related-articles}

* [Elenco delle API fatturabili per AEM Forms su JEE](../../forms/using/transaction-reports-billable-apis-jee.md)
* [Registrare una transazione per le API dei componenti personalizzati per AEM Forms su JEE](/help/forms/using/record-transaction-custom-component-jee.md)
