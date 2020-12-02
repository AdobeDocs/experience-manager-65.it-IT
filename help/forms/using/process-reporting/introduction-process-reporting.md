---
title: Introduzione a Process Reporting
seo-title: Introduzione a Process Reporting
description: Introduzione e funzionalità chiave di  AEM Forms su JEE Process Reporting
seo-description: Introduzione e funzionalità chiave di  AEM Forms su JEE Process Reporting
uuid: a7f2455b-1b09-41a7-817b-e2e7a1ff9936
content-type: reference
topic-tags: process-reporting
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 4e83ed7b-3f48-4bf6-be4c-89f79949c1df
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---


# Introduzione a Process Reporting{#introduction-to-process-reporting}

![reporting dei processi](assets/process-reporting.png)

Process Reporting è uno strumento basato su browser che consente di creare e visualizzare rapporti  processi e attività AEM Forms.

Process Reporting fornisce una serie di report out-of-the-box che consentono di filtrare, visualizzare informazioni sui processi in esecuzione lunghi, la durata del processo e il volume del flusso di lavoro.

Inoltre Process Reporting fornisce un&#39;interfaccia per eseguire query ad hoc e integrare visualizzazioni di report personalizzate nell&#39;interfaccia utente di Process Reporting.

Per l&#39;elenco dei browser supportati, vedere [ piattaforme supportate da AEM Forms](/help/forms/using/aem-forms-jee-supported-platforms.md).

Process Reporting è basato su moduli che:

* Leggere i dati del processo da  database AEM Forms
* Pubblicare i dati del processo in un archivio di Process Reporting incorporato
* Fornisce un&#39;interfaccia utente basata su browser per visualizzare i rapporti

## Funzionalità chiave {#key-capabilities}

### Report sempre attivi {#always-on-reporting}

![gestione del sito](assets/site-management.png)

Visualizza l&#39;elenco dei processi con esecuzione prolungata, dei grafici della durata del processo e delle query personalizzate utilizzando i filtri.

Process Reporting (Generazione di rapporti sui processi) offre anche la possibilità di esportare i dati del rapporto e della query in formato CSV.

### Rapporti Adhoc {#adhoc-reports}

![print-and-color](assets/print-&-colour.png)

Utilizza i filtri per ottenere una visualizzazione specifica dei tuoi dati.

È possibile eseguire ricerche nei processi o nelle attività in base all&#39;ID, alla durata, alle date di inizio e di fine, all&#39;iniziatore del processo e così via.

Potete combinare più filtri per creare rapporti specifici.

Puoi quindi salvare i filtri per report da eseguire in una data o in un&#39;ora successive.

### Cronologia processo/attività {#process-task-history}

![gestione dei file](assets/file-management.png)

 server AEM Forms eseguono numerosi processi in parallelo. Questi processi continuano a passare da uno stato all’altro. Pubblicando a intervalli regolari i dati di Forms nell&#39;archivio di Process Reporting, Process Reporting conserva le informazioni di transizione sui processi in esecuzione in  AEM Forms.

### Controllo accesso {#access-control-br}

![senza titolo](assets/untitled.png)

Process Reporting fornisce l&#39;accesso basato sulle autorizzazioni all&#39;interfaccia utente.

Ciò significa che solo gli utenti con autorizzazioni di reporting hanno accesso all&#39;interfaccia utente di Process Reporting.
