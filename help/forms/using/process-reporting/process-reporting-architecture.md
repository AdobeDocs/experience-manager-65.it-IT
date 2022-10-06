---
title: Come funziona il reporting dei processi
seo-title: How Process Reporting Works
description: Descrizione dei servizi che compongono AEM Forms su JEE Process Reporting e introduzione all'interfaccia utente di Process Reporting
seo-description: Description of the services that make up the AEM Forms on JEE Process Reporting and an introduction to the Process Reporting UI
uuid: 37e31985-088a-4ef6-ba57-10a01597a873
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: process-reporting
discoiquuid: a6ff50df-273d-48f7-b0c6-0e69e900b97f
docset: aem65
exl-id: 66dfac36-5b7e-40be-9921-efa9f2a9521c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 0%

---

# Come funziona il reporting dei processi{#how-process-reporting-works}

Process Reporting è il modulo di reporting di AEM Forms su JEE.

Reporting dei processi consente di eseguire rapporti sui processi e sulle attività di AEM Forms.

Process Reporting utilizza l&#39;archivio integrato Process Reporting per pubblicare i dati di Forms. Quindi utilizza quei dati per eseguire i rapporti.

Report dei processi è costituito dai seguenti moduli:

* [Servizio ProcessDataPublisher](#processdatapublisher-service-br-p)
* [Servizio ProcessDataStorage](#processdatastorageprovider-service-br-p)
* [Servizio OSGi](#osgi-service-br-p)
* [Servlet dati query](#querydataservlet-service-br-p)
* [Interfaccia utente di Process Reporting](#process-reporting-user-interface-br-p)

## Architettura di Reporting dei processi {#process-reporting-architecture-br}

![architettura di reportistica](assets/processreportingarchitecture.png)

## Moduli di reporting dei processi {#process-reporting-modules}

### Servizio ProcessDataPublisher {#processdatapublisher-service-br}

Il server ProcessDataPublisher viene eseguito periodicamente sul database AEM Forms ed estrae i dati modificati dall&#39;ultima esecuzione del servizio. Pubblica quindi i dati nel servizio Process Data Storage.

Per informazioni dettagliate sulla configurazione del servizio, vedi [Configura il servizio ProcessDataPublisher](/help/forms/using/process-reporting/install-start-process-reporting.md#p-reportconfiguration-service-p).

### Servizio ProcessDataStorageProvider {#processdatastorageprovider-service-br}

Il servizio ProcessDataStorageProvider riceve i dati di processo dal servizio ProcessDataPublisher e li salva nell&#39;archivio di Process Reporting.

Per informazioni dettagliate sulla configurazione del servizio, vedi [Configura il servizio ProcessDataStorageProvider](/help/forms/using/process-reporting/install-start-process-reporting.md#p-to-configure-the-process-reporting-repository-locations-p).

### Servizio OSGi {#osgi-service-br}

QueryDataServlet utilizza questo servizio per ottenere i dati di reporting dall&#39;archivio di Process Reporting.

### Servizio QueryDataServlet {#querydataservlet-service-br}

Il servizio QueryDataServlet accetta query dall&#39;interfaccia utente di Process Reporting.

Il servizio utilizza quindi i servizi OSGi per ottenere i dati di reporting rilevanti, elabora i dati e restituisce i dati all’interfaccia utente.

### Interfaccia utente di Process Reporting {#process-reporting-user-interface-br}

L&#39;interfaccia utente di Process Reporting è un&#39;interfaccia basata su browser Web. Utilizzare questa interfaccia per visualizzare le informazioni relative a processi e attività pubblicate dal database AEM Forms.

Per un&#39;introduzione all&#39;interfaccia utente di Process Reporting, vedi [Interfaccia utente di Process Reporting](/help/forms/using/process-reporting/introduction-process-reporting.md).

### Servizio QueryDataServlet {#querydataservlet-service-br-1}

Il servizio QueryDataServlet accetta query dall&#39;interfaccia utente di Process Reporting.

Il servizio utilizza quindi i servizi OSGi per ottenere i dati di reporting rilevanti, elabora i dati e restituisce i dati all’interfaccia utente.

### Report personalizzati {#custom-reports-br}

Puoi creare rapporti personalizzati e visualizzarli nella scheda Report personalizzati dell&#39;interfaccia utente di Process Reporting.

Per i passaggi necessari per creare un rapporto personalizzato, consulta Creazione di un rapporto personalizzato nell’articolo [Report personalizzati in Reporting dei processi](/help/forms/using/process-reporting/process-reporting-custom-reports.md).
