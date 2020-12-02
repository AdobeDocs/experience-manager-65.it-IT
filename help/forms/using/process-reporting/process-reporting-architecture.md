---
title: Come funziona Reporting dei processi
seo-title: Come funziona Reporting dei processi
description: Descrizione dei servizi che compongono l'AEM Forms  su JEE Process Reporting e introduzione all'interfaccia utente di Process Reporting
seo-description: Descrizione dei servizi che compongono l'AEM Forms  su JEE Process Reporting e introduzione all'interfaccia utente di Process Reporting
uuid: 37e31985-088a-4ef6-ba57-10a01597a873
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: process-reporting
discoiquuid: a6ff50df-273d-48f7-b0c6-0e69e900b97f
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 0%

---


# Funzionamento di Reporting dei processi{#how-process-reporting-works}

Process Reporting è il modulo di reporting dell&#39;AEM Forms  su JEE.

Process Reporting (Generazione rapporti di processo) consente di eseguire rapporti  processi e attività AEM Forms.

Process Reporting utilizza l&#39;archivio di Process Reporting incorporato per pubblicare i dati Forms. Quindi utilizza quei dati per eseguire i report.

Process Reporting è costituito dai seguenti moduli:

* [Servizio ProcessDataPublisher](#processdatapublisher-service-br-p)
* [Servizio ProcessDataStorage](#processdatastorageprovider-service-br-p)
* [servizio OSGi](#osgi-service-br-p)
* [Server dati query](#querydataservlet-service-br-p)
* [Interfaccia utente di Process Reporting](#process-reporting-user-interface-br-p)

## Architettura di reporting dei processi {#process-reporting-architecture-br}

![processreportistica](assets/processreportingarchitecture.png)

## Moduli di generazione rapporti processo {#process-reporting-modules}

### Servizio ProcessDataPublisher {#processdatapublisher-service-br}

Il server ProcessDataPublisher viene eseguito periodicamente sul database AEM Forms  ed estrae i dati modificati dall&#39;ultima esecuzione del servizio. Quindi pubblica i dati nel servizio Process Data Storage.

Per informazioni dettagliate sulla configurazione del servizio, vedere [Configurare il servizio ProcessDataPublisher](/help/forms/using/process-reporting/install-start-process-reporting.md#p-reportconfiguration-service-p).

### Servizio ProcessDataStorageProvider {#processdatastorageprovider-service-br}

Il servizio ProcessDataStorageProvider riceve i dati del processo dal servizio ProcessDataPublisher e li salva nell&#39;archivio di Process Reporting.

Per informazioni dettagliate sulla configurazione del servizio, vedere [Configurare il servizio ProcessDataStorageProvider](/help/forms/using/process-reporting/install-start-process-reporting.md#p-to-configure-the-process-reporting-repository-locations-p).

### Servizio OSGi {#osgi-service-br}

QueryDataServlet utilizza questo servizio per ottenere i dati di reporting dall&#39;archivio di Process Reporting.

### Servizio QueryDataServlet {#querydataservlet-service-br}

Il servizio QueryDataServlet accetta le query dall&#39;interfaccia utente di Process Reporting.

Il servizio utilizza quindi i servizi OSGi per ottenere i dati di reporting rilevanti, elabora i dati e restituisce i dati all&#39;interfaccia utente.

### Interfaccia utente di Process Reporting {#process-reporting-user-interface-br}

L&#39;interfaccia utente di Process Reporting è basata su browser Web. È possibile utilizzare questa interfaccia per visualizzare le informazioni su processi e attività pubblicate dal database AEM Forms .

Per un&#39;introduzione all&#39;interfaccia utente di Process Reporting, vedere [Interfaccia utente di Process Reporting](/help/forms/using/process-reporting/introduction-process-reporting.md).

### Servizio QueryDataServlet {#querydataservlet-service-br-1}

Il servizio QueryDataServlet accetta le query dall&#39;interfaccia utente di Process Reporting.

Il servizio utilizza quindi i servizi OSGi per ottenere i dati di reporting rilevanti, elabora i dati e restituisce i dati all&#39;interfaccia utente.

### Report personalizzati {#custom-reports-br}

Potete creare rapporti personalizzati e visualizzarli nella scheda Report personalizzati dell&#39;interfaccia utente di Process Reporting.

Per i passaggi necessari per creare un rapporto personalizzato, vedere Creazione di un rapporto personalizzato nell&#39;articolo [Report personalizzati in Process Reporting](/help/forms/using/process-reporting/process-reporting-custom-reports.md).
