---
title: Funzionamento dei rapporti sui processi
description: Descrizione dei servizi che compongono AEM Forms su JEE Process Reporting e introduzione all’interfaccia utente di Process Reporting
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: process-reporting
docset: aem65
exl-id: 66dfac36-5b7e-40be-9921-efa9f2a9521c
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 2%
---
# Funzionamento dei rapporti sui processi{#how-process-reporting-works}

Process Reporting è il modulo di reporting di AEM Forms su JEE.

Reporting sui processi consente di eseguire report sui processi e sulle attività di AEM Forms.

Per pubblicare i dati di Forms, Process Reporting utilizza l&#39;archivio incorporato Process Reporting. Quindi utilizza tali dati per eseguire i rapporti.

Process Reporting è costituito dai seguenti moduli:

* [Servizio ProcessDataPublisher](#processdatapublisher-service-br-p)
* [Servizio ProcessDataStorage](#processdatastorageprovider-service-br-p)
* [Servizio OSGi](#osgi-service-br-p)
* [Query Data Servlet](#querydataservlet-service-br-p)
* [Interfaccia utente di Process Reporting](#process-reporting-user-interface-br-p)

## Architettura di report dei processi {#process-reporting-architecture-br}

![processreportingarchitecture](assets/processreportingarchitecture.png)

## Moduli di report dei processi {#process-reporting-modules}

### Servizio ProcessDataPublisher {#processdatapublisher-service-br}

Il server ProcessDataPublisher viene eseguito periodicamente sul database di AEM Forms ed estrae i dati modificati dall&#39;ultima esecuzione del servizio. Quindi pubblica i dati nel servizio Archiviazione dati processo.

Per informazioni dettagliate sulla configurazione del servizio, vedere [Configurare il servizio ProcessDataPublisher](/help/forms/using/process-reporting/install-start-process-reporting.md#p-reportconfiguration-service-p).

### Servizio ProcessDataStorageProvider {#processdatastorageprovider-service-br}

Il servizio ProcessDataStorageProvider riceve i dati di processo dal servizio ProcessDataPublisher e li salva nel repository di Process Reporting.

Per informazioni dettagliate sulla configurazione del servizio, vedere [Configurare il servizio ProcessDataStorageProvider](/help/forms/using/process-reporting/install-start-process-reporting.md#p-to-configure-the-process-reporting-repository-locations-p).

### Servizio OSGi {#osgi-service-br}

QueryDataServlet utilizza questo servizio per ottenere i dati di reporting dal repository di Process Reporting.

### Servizio QueryDataServlet {#querydataservlet-service-br}

Il servizio QueryDataServlet accetta query dall&#39;interfaccia utente di Process Reporting.

Il servizio utilizza quindi i servizi OSGi per ottenere i dati di reporting rilevanti, elabora i dati e li restituisce all’interfaccia utente.

### Interfaccia utente di Process Reporting {#process-reporting-user-interface-br}

L&#39;interfaccia utente di Process Reporting è un&#39;interfaccia basata su browser Web. Questa interfaccia consente di visualizzare le informazioni sui processi e sulle attività pubblicate dal database di AEM Forms.

Per un&#39;introduzione all&#39;interfaccia utente di Process Reporting, vedere [Interfaccia utente di Process Reporting](/help/forms/using/process-reporting/introduction-process-reporting.md).

### Servizio QueryDataServlet {#querydataservlet-service-br-1}

Il servizio QueryDataServlet accetta query dall&#39;interfaccia utente di Process Reporting.

Il servizio utilizza quindi i servizi OSGi per ottenere i dati di reporting rilevanti, elabora i dati e li restituisce all’interfaccia utente.

### Rapporti personalizzati {#custom-reports-br}

È possibile creare report personalizzati e visualizzarli nella scheda Report personalizzati dell&#39;interfaccia utente Report processi.

Per i passaggi necessari per creare un report personalizzato, vedere Per creare un report personalizzato nell&#39;articolo [Report personalizzati in Report di processo](/help/forms/using/process-reporting/process-reporting-custom-reports.md).
