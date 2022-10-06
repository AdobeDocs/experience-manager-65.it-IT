---
title: Introduzione alla generazione di rapporti sui processi
seo-title: Introduction to Process Reporting
description: Introduzione e funzionalità chiave di AEM Forms per la generazione di rapporti sui processi JEE
seo-description: Introduction and key capabilities of AEM Forms on JEE Process Reporting
uuid: a7f2455b-1b09-41a7-817b-e2e7a1ff9936
content-type: reference
topic-tags: process-reporting
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 4e83ed7b-3f48-4bf6-be4c-89f79949c1df
docset: aem65
exl-id: 674d28dc-7353-49de-9e12-b1998e1509c7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---

# Introduzione alla generazione di rapporti sui processi{#introduction-to-process-reporting}

![reportistica dei processi](assets/process-reporting.png)

Process Reporting è uno strumento basato su browser che consente di creare e visualizzare rapporti sui processi e le attività di AEM Forms.

La funzione di reporting dei processi fornisce una serie di rapporti predefiniti che ti consentono di filtrare, visualizzare informazioni sui processi in esecuzione a lungo termine, sulla durata del processo e sul volume del flusso di lavoro.

Inoltre, Process Reporting fornisce un&#39;interfaccia per eseguire query ad hoc e integrare visualizzazioni di report personalizzate nell&#39;interfaccia utente di Process Reporting.

Per l’elenco dei browser supportati, consulta [Piattaforme supportate da AEM Forms](/help/forms/using/aem-forms-jee-supported-platforms.md).

Il reporting dei processi è basato su moduli che:

* Lettura dei dati del processo dal database AEM Forms
* Pubblicare i dati del processo in un archivio incorporato di Process Reporting
* Fornisce un&#39;interfaccia utente basata su browser per visualizzare i rapporti

## Funzionalità principali {#key-capabilities}

### Generazione di rapporti sempre attiva {#always-on-reporting}

![gestione del sito](assets/site-management.png)

Visualizza l’elenco dei processi in esecuzione a lungo termine, dei grafici della durata del processo e esegue query personalizzate utilizzando i filtri.

La funzione di reporting dei processi offre anche la possibilità di esportare il rapporto e di eseguire query sui dati in formato CSV.

### Report ad hoc {#adhoc-reports}

![stampa a colori](assets/print-&-colour.png)

Utilizza i filtri per ottenere una visualizzazione specifica dei tuoi dati.

Puoi cercare processi o attività per ID, durata, date di inizio e fine, iniziatore del processo e così via.

Puoi combinare più filtri per creare rapporti specifici.

Puoi quindi salvare i filtri per i rapporti da eseguire in una data o in un’ora successive.

### Cronologia processi/task {#process-task-history}

![gestione dei file](assets/file-management.png)

I server AEM Forms eseguono numerosi processi in parallelo. Questi processi continuano a passare da uno stato all’altro. Pubblicando i dati di Forms nell’archivio di Process Reporting a intervalli regolari, Process Reporting conserva le informazioni di transizione sui processi in esecuzione in AEM Forms.

### Controllo accesso {#access-control-br}

![senza titolo](assets/untitled.png)

La funzione di reporting dei processi consente l’accesso all’interfaccia utente in base alle autorizzazioni.

Ciò significa che solo gli utenti con autorizzazioni di reporting possono accedere all’interfaccia utente di Process Reporting.
