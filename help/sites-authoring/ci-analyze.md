---
title: Analisi delle prestazioni delle pagine
seo-title: Analyzing Page Performance
description: Utilizza la pagina Content Insight per analizzare le prestazioni della pagina che stai creando
seo-description: Use the Content Insight page to analyze the performance of the page that you are authoring
uuid: 563d3e98-20d9-4cca-a174-bafd6e65c1bb
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 57cd61d5-78f2-4f8c-99ee-75e100c052ef
docset: aem65
exl-id: 14484a90-4e44-4c85-9411-b78ed11dc70d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '662'
ht-degree: 0%

---

# Analisi delle prestazioni delle pagine{#analyzing-page-performance}

Apri [Approfondimenti contenuto](/help/sites-authoring/content-insights.md) per analizzare le prestazioni della pagina che si sta creando. Configura il periodo di reporting per concentrare l’analisi.

## Apertura di Analytics e Recommendations per una pagina {#opening-analytics-and-recommendations-for-a-page}

Per visualizzare Analytics e Recommendations per una pagina, utilizza la procedura seguente:

1. Passare alla pagina che si desidera analizzare.
1. Nella barra degli strumenti, tocca o fai clic su **Analytics e Recommendations**.

   >[!NOTE]
   >
   >Analytics e Recommendations per una pagina vengono visualizzati solo se l’AEM è stato configurato per [integrare con Adobe Analytics](/help/sites-administering/adobeanalytics-connect.md).

   ![schermata_2019-03-05at115319](assets/screen-shot_2019-03-05at115319.png)

### Modifica del periodo di reporting {#changing-the-reporting-period}

Modifica i seguenti aspetti relativi al tempo nei rapporti di analisi:

* Periodo di tempo in cui generare il rapporto.
* Granularità dei dati.

Gli strumenti per modificare gli aspetti temporali dei rapporti vengono visualizzati nella parte superiore della pagina Approfondimenti contenuto. ![chlimage_1-126](assets/chlimage_1-126.png)

#### Modifica del periodo di reporting {#changing-the-reporting-period-1}

Modifica il periodo di reporting della pagina di approfondimento dei contenuti per focalizzare l’analisi dell’attività della pagina su un periodo di tempo specifico. Quando si modifica il periodo di reporting, i rapporti vengono aggiornati automaticamente. L’area ombreggiata nell’arco temporale rappresenta il periodo di reporting. Le date nell’arco temporale aumentano da sinistra a destra.

![chlimage_1-127](assets/chlimage_1-127.png)

Per modificare il periodo di reporting di una pagina di approfondimento dei contenuti:

1. Se l’intervallo temporale non viene visualizzato nella parte superiore della pagina, tocca o fai clic sull’icona Attiva/Disattiva intervallo temporale.

   ![](do-not-localize/chlimage_1-22.png)

1. Per modificare la data di inizio del periodo di reporting, trascinare il cerchio visualizzato sul lato sinistro dell&#39;area ombreggiata sulla data di inizio desiderata.

   Se il lato sinistro dell&#39;area ombreggiata non è visibile, utilizzare la barra di scorrimento per visualizzarla.

1. Per modificare la data di fine del periodo di reporting, trascinare il cerchio visualizzato sul lato destro dell&#39;area ombreggiata fino alla data di fine desiderata.

#### Modifica della granularità del periodo di reporting {#changing-the-granularity-of-the-reporting-period}

Modifica la quantità di tempo trascorsa da ogni punto dati in un rapporto. Ad esempio, quando è selezionata la granularità Settimana, ogni punto dati nel rapporto Visualizzazioni rappresenta il numero di visualizzazioni per una settimana.

![screen_shot_2017-11-29at141001](assets/screen_shot_2017-11-29at141001.png)

La granularità influisce sui rapporti che tracciano i dati in base al tempo, ad esempio i rapporti Visualizzazioni e Media dei minuti coinvolti nella pagina. La granularità influisce anche sulla scala dell’arco temporale.

1. Se il controllo di granularità non viene visualizzato, tocca o fai clic sull’icona Attiva/Disattiva granularità.

   ![chlimage_1-128](assets/chlimage_1-128.png)

1. Tocca o fai clic sulla granularità desiderata. Una volta selezionato, il rapporto viene aggiornato automaticamente per riflettere la granularità.

### Assegnazione di attività per SEO Recommendations {#assigning-tasks-for-seo-recommendations}

Utilizza il rapporto SEO Recommendations per creare attività volte a migliorare la visibilità delle pagine nei motori di ricerca. Per ogni consiglio del report che non ha un segno di spunta, puoi creare un&#39;attività da assegnare a un utente per eseguire il lavoro richiesto.

![chlimage_1-129](assets/chlimage_1-129.png)

Lo stato del consiglio SEO indica quando l’attività viene creata ma non ancora completata.

![chlimage_1-130](assets/chlimage_1-130.png)

Una volta creata, l’attività viene visualizzata nell’elenco Attività dell’utente. Per informazioni sulle attività, consulta [Utilizzo delle attività](/help/sites-authoring/task-content.md).

Per creare un&#39;attività per un consiglio SEO, attenersi alla procedura descritta di seguito.

1. Tocca o fai clic sull’icona delle informazioni per il consiglio SEO (Search Engine Optimization).

   ![](do-not-localize/chlimage_1-23.png)

1. Fare clic sull&#39;icona del triangolo racchiuso accanto all&#39;icona delle informazioni.

   ![chlimage_1-131](assets/chlimage_1-131.png)

1. Compila i campi modulo visualizzati e tocca Crea:

   * Progetto: selezionare il progetto in cui creare l&#39;attività.
   * Nome: il nome che identifica l&#39;attività. Il nome predefinito è il titolo del consiglio SEO (Search Engine Optimization).
   * Assegna a: selezionare l&#39;utente a cui assegnare l&#39;attività. Inizia a digitare il nome dell’utente per filtrare l’elenco.
   * Descrizione: una descrizione dell&#39;attività necessaria per completare l&#39;attività. La descrizione predefinita è quella che accompagna il consiglio SEO (Search Engine Optimization).
   * Priorità attività: la priorità dell&#39;attività.
   * Data scadenza: la data entro la quale l&#39;attività deve essere completata.

   **Nota:** L’attività creata include anche il percorso della pagina a cui si applica il consiglio SEO (Search Engine Optimization).

1. Tocca o fai clic su Fine per chiudere il messaggio Attività creata.
