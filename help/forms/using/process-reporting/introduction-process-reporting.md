---
title: Introduzione alla generazione di rapporti sui processi
seo-title: Introduction to Process Reporting
description: Introduzione e funzionalità chiave di AEM Forms su JEE Process Reporting
seo-description: Introduction and key capabilities of AEM Forms on JEE Process Reporting
uuid: a7f2455b-1b09-41a7-817b-e2e7a1ff9936
content-type: reference
topic-tags: process-reporting
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 4e83ed7b-3f48-4bf6-be4c-89f79949c1df
docset: aem65
exl-id: 674d28dc-7353-49de-9e12-b1998e1509c7
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 0%

---

# Introduzione alla generazione di rapporti sui processi{#introduction-to-process-reporting}

![reporting sui processi](assets/process-reporting.png)

Process Reporting è uno strumento basato su browser che consente di creare e visualizzare report sui processi e le attività di AEM Forms.

Report processi fornisce una serie di report predefiniti che consentono di filtrare e visualizzare informazioni sui processi a esecuzione prolungata, sulla durata del processo e sul volume del flusso di lavoro.

Process Reporting fornisce inoltre un&#39;interfaccia per l&#39;esecuzione di query ad hoc e per l&#39;integrazione di visualizzazioni report personalizzate nell&#39;interfaccia utente di Process Reporting.

Per un elenco dei browser supportati consulta [Piattaforme supportate da AEM Forms](/help/forms/using/aem-forms-jee-supported-platforms.md).

Process Reporting è basato su moduli che:

* Leggi dati processo da AEM Forms Database
* Pubblicare i dati del processo in un repository Process Reporting incorporato
* Fornisce un&#39;interfaccia utente basata su browser per visualizzare i rapporti

## Funzionalità principali {#key-capabilities}

### Reporting sempre attivo {#always-on-reporting}

![gestione dei siti](assets/site-management.png)

Visualizzare l&#39;elenco dei processi con tempi di esecuzione lunghi, elaborare grafici della durata ed eseguire query personalizzate utilizzando i filtri.

Process Reporting offre inoltre la possibilità di esportare il report ed eseguire query sui dati in formato CSV.

### Rapporti ad hoc {#adhoc-reports}

![stampa e colori](assets/print-&-colour.png)

Utilizza i filtri per ottenere una visualizzazione specifica dei dati.

È possibile cercare i processi o le attività in base all&#39;ID, alla durata, alle date di inizio e di fine, all&#39;iniziatore del processo e così via.

Puoi combinare più filtri per creare rapporti specifici.

Puoi quindi salvare i filtri del rapporto in modo che vengano eseguiti in una data o in un’ora successiva.

### Cronologia processi/attività {#process-task-history}

![gestione dei file](assets/file-management.png)

I server AEM Forms eseguono numerosi processi in parallelo. Questi processi continuano a passare da uno stato all’altro. Pubblicando i dati di Forms nel repository di Process Reporting a intervalli regolari, Process Reporting conserva le informazioni di transizione sui processi in esecuzione in AEM Forms.

### Controllo accesso {#access-control-br}

![senza titolo](assets/untitled.png)

Process Reporting fornisce un accesso basato su autorizzazioni all&#39;interfaccia utente.

Ciò significa che solo gli utenti con autorizzazioni di reporting hanno accesso all’interfaccia utente di Process Reporting.
