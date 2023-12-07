---
title: Approfondimenti contenuto
description: Content Insight fornisce informazioni sulle prestazioni delle pagine utilizzando analisi web e consigli SEO (Search Engine Optimization)
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
exl-id: 187f3cde-a0db-4c02-9e8b-08272987a67d
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 3%

---

# Approfondimenti contenuto{#content-insight}

Content Insight fornisce informazioni sulle prestazioni della pagina utilizzando l’analisi web e i consigli SEO (Search Engine Optimization). Utilizza Content Insight per prendere decisioni su come modificare le pagine o per scoprire in che modo le modifiche precedenti hanno cambiato le prestazioni. Per ogni pagina creata, puoi aprire Content Insight per analizzare la pagina.

![chlimage_1-311](assets/chlimage_1-311.png)

Il layout della pagina Content Insight cambia in base alle dimensioni dello schermo e all’orientamento del dispositivo in uso.

## Dati del rapporto

La pagina Approfondimenti contenuto include rapporti che utilizzano dati di Adobe SiteCatalyst, Adobe Target, Adobe Social e BrightEdge:

* SiteCatalyst: sono disponibili rapporti per le metriche seguenti:

   * Visualizzazioni pagina
   * Tempo medio trascorso sulla pagina
   * Origini

* Target: rapporti sull’attività della campagna per la quale la pagina include offerte.
* BrightEdge: segnala le funzioni della pagina che migliorano la visibilità della pagina ai motori di ricerca e consiglia le funzioni che devono essere implementate.

Consulta [Apertura di Analytics e Recommendations per una pagina](/help/sites-authoring/ci-analyze.md#opening-analytics-and-recommendations-for-a-page).

## Periodo di segnalazione

I rapporti mostrano i dati per un periodo di tempo controllato. Quando si modifica il periodo di reporting, i rapporti vengono aggiornati automaticamente con i dati relativi a tale periodo. I suggerimenti visivi indicano il momento in cui sono cambiate le versioni delle pagine, in modo da poter confrontare le prestazioni di ogni versione.

>[!NOTE]
>
>La timeline per il dashboard Content Insight è in `GMT`.

Puoi anche specificare la granularità dei dati segnalati, ad esempio visualizzare dati giornalieri, settimanali, mensili o annuali.

Consulta [Modifica del periodo di reporting](/help/sites-authoring/ci-analyze.md#changing-the-reporting-period).

>[!NOTE]
>
>I rapporti Content Insights richiedono che l’amministratore abbia integrato AEM con SiteCatalyst, Target e BrightEdge. Consulta [Integrazione con SightCatalyst](/help/sites-administering/adobeanalytics.md), [Integrazione con Adobe Target](/help/sites-administering/target.md), e [Integrazione con BrightEdge](/help/sites-administering/brightedge.md).

## Il rapporto Visualizzazioni {#the-views-report}

Il rapporto Visualizzazioni include le seguenti funzioni per la valutazione del traffico di pagina:

* Numero totale di visualizzazioni per una pagina per il periodo di reporting.
* Un grafico del numero di visualizzazioni nel periodo di reporting:

   * Visualizzazioni totali.
   * Visitatori univoci.

![chlimage_1-312](assets/chlimage_1-312.png)

## Rapporto Media pagine coinvolte {#the-page-average-engaged-report}

Il rapporto Media pagine coinvolte include le seguenti funzioni per valutare l’efficacia della pagina:

* Tempo medio in cui la pagina rimane aperta per l&#39;intero periodo di reporting.
* Un grafico della lunghezza media di una visualizzazione pagina nel periodo di reporting.

![chlimage_1-313](assets/chlimage_1-313.png)

## Rapporto Sorgenti {#the-sources-report}

Il rapporto Sources (Origini) indica il modo in cui gli utenti sono passati alla pagina, ad esempio, dai risultati del motore di ricerca o utilizzando l’URL noto.

![chlimage_1-314](assets/chlimage_1-314.png)

## Rapporto Rimbalzi {#the-bounces-report}

Il rapporto Rimbalzi include un grafico che mostra il numero di mancati recapiti verificatisi per una pagina nel periodo di reporting selezionato.

![chlimage_1-315](assets/chlimage_1-315.png)

## Rapporto sull’attività della campagna {#the-campaign-activity-report}

Per ogni campagna per la quale è attiva la pagina, viene visualizzato un rapporto denominato *Nome campagna* Attività. Il rapporto mostra le impression e le conversioni di pagina per ciascun segmento per il quale viene fornita un’offerta.

![chlimage_1-316](assets/chlimage_1-316.png)

## Il rapporto SEO Recommendations {#the-seo-recommendations-report}

Il rapporto SEO Recommendations contiene i risultati dell’analisi BrightEdge per la pagina. Il rapporto è un elenco di controllo delle funzioni di pagina che indica quali funzioni la pagina include o meno per massimizzare la reperibilità utilizzando i motori di ricerca.

Il rapporto consente di creare attività in modo da migliorare la reperibilità delle pagine. Recommendations indica che sono state create attività per l’implementazione del consiglio. Consulta [Assegnazione di attività per SEO Recommendations](/help/sites-authoring/ci-analyze.md#assigning-tasks-for-seo-recommendations).

![chlimage_1-317](assets/chlimage_1-317.png)
