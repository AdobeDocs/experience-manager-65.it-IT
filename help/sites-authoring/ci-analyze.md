---
title: Analisi delle prestazioni della pagina
description: Utilizza la pagina Insight dei contenuti per analizzare le prestazioni della pagina che stai creando
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
docset: aem65
exl-id: 14484a90-4e44-4c85-9411-b78ed11dc70d
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Integration
role: User,Admin,Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: e2c1b6d3-bb7e-4fe8-8c72-f7b403298e91
    internal-label: Authoring
  - id: 243139ec-8e41-5296-a287-31343ab1bc0f
    internal-label: Integration
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 2%
---
# Analisi delle prestazioni della pagina{#analyzing-page-performance}

Apri la pagina [Contenuto Insight](/help/sites-authoring/content-insights.md) per analizzare le prestazioni della pagina che stai creando. Configura il periodo di reporting per concentrare l’analisi.

## Apertura di Analytics e Recommendations per una pagina {#opening-analytics-and-recommendations-for-a-page}

Utilizza la procedura seguente per visualizzare le analisi e i consigli per una pagina:

1. Passare alla pagina che si desidera analizzare.
1. Nella barra degli strumenti, fai clic su **Analytics e Recommendations**.

   >[!NOTE]
   >
   >Le analisi e i consigli per una pagina vengono visualizzati solo se AEM è stato configurato per l&#39;integrazione con Adobe Analytics](/help/sites-administering/adobeanalytics-connect.md).[

   ![schermata_2019-03-05at115319](assets/screen-shot_2019-03-05at115319.png)

### Modifica del periodo di reporting {#changing-the-reporting-period}

Modifica i seguenti aspetti relativi al tempo nei rapporti di analisi:

* Periodo di tempo in cui generare il rapporto.
* Granularità dei dati.

Gli strumenti per modificare gli aspetti temporali dei rapporti vengono visualizzati nella parte superiore della pagina Insight dei contenuti. ![chlimage_1-126](assets/chlimage_1-126.png)

#### Modifica del periodo di reporting {#changing-the-reporting-period-1}

Modifica il periodo di reporting della pagina Insight dei contenuti per concentrare l’analisi dell’attività della pagina su un periodo di tempo specifico. Quando si modifica il periodo di reporting, i rapporti vengono aggiornati automaticamente. L’area ombreggiata nell’arco temporale rappresenta il periodo di reporting. Le date nell’arco temporale aumentano da sinistra a destra.

![chlimage_1-127](assets/chlimage_1-127.png)

Per modificare il periodo di reporting di una pagina di Content Insight:

1. Se l’intervallo temporale non viene visualizzato nella parte superiore della pagina, fai clic sull’icona Attiva/Disattiva intervallo temporale.

   ![Attiva/Disattiva intervallo di tempo](do-not-localize/chlimage_1-22.png)

1. Per modificare la data di inizio del periodo di reporting, trascinare il cerchio visualizzato sul lato sinistro dell&#39;area ombreggiata sulla data di inizio desiderata.

   Se il lato sinistro dell&#39;area ombreggiata non è visibile, utilizzare la barra di scorrimento per visualizzarla.

1. Per modificare la data di fine del periodo di reporting, trascinare il cerchio visualizzato sul lato destro dell&#39;area ombreggiata fino alla data di fine desiderata.

#### Modifica della granularità del periodo di reporting {#changing-the-granularity-of-the-reporting-period}

Modifica la quantità di tempo trascorsa da ogni punto dati in un rapporto. Ad esempio, quando è selezionata la granularità Settimana, ogni punto dati nel rapporto Visualizzazioni rappresenta il numero di visualizzazioni per una settimana.

![schermata_shot_2017-11-29at141001](assets/screen_shot_2017-11-29at141001.png)

La granularità influisce sui rapporti che tracciano i dati in base al tempo, ad esempio i rapporti Visualizzazioni e Media dei minuti coinvolti nella pagina. La granularità influisce anche sulla scala dell’arco temporale.

1. Se il controllo di granularità non viene visualizzato, fai clic sull’icona Attiva/Disattiva granularità.

   ![chlimage_1-128](assets/chlimage_1-128.png)

1. Fai clic sulla granularità desiderata. Una volta selezionato, il rapporto viene aggiornato automaticamente per riflettere la granularità.

### Assegnazione di attività per i consigli SEO (Search Engine Optimization) {#assigning-tasks-for-seo-recommendations}

Utilizza il rapporto SEO Recommendations (Consigli SEO) per creare attività per migliorare la visibilità delle pagine nei motori di ricerca. Per ogni consiglio del report che non ha un segno di spunta, puoi creare un&#39;attività da assegnare a un utente per eseguire il lavoro richiesto.

![chlimage_1-129](assets/chlimage_1-129.png)

Lo stato del consiglio SEO indica quando l’attività viene creata ma non ancora completata.

![chlimage_1-130](assets/chlimage_1-130.png)

Una volta creata, l’attività viene visualizzata nell’elenco Attività dell’utente. Per informazioni sulle attività, vedere [Utilizzo delle attività](/help/sites-authoring/task-content.md).

Per creare un&#39;attività per un consiglio SEO, attenersi alla procedura descritta di seguito.

1. Fai clic sull’icona delle informazioni per il consiglio SEO (Search Engine Optimization).

   ![Icona informazioni](do-not-localize/chlimage_1-23.png)

1. Fare clic sull&#39;icona del triangolo racchiuso accanto all&#39;icona delle informazioni.

   ![chlimage_1-131](assets/chlimage_1-131.png)

1. Compila i campi modulo visualizzati, quindi seleziona Crea:

   * Progetto: selezionare il progetto in cui creare l&#39;attività.
   * Nome: il nome che identifica l&#39;attività. Il nome predefinito è il titolo del consiglio SEO (Search Engine Optimization).
   * Assegna a: selezionare l&#39;utente a cui assegnare l&#39;attività. Inizia a digitare il nome dell’utente per filtrare l’elenco.
   * Descrizione: una descrizione dell&#39;attività necessaria per completare l&#39;attività. La descrizione predefinita è quella che accompagna il consiglio SEO (Search Engine Optimization).
   * Priorità attività: la priorità dell&#39;attività.
   * Data scadenza: la data entro la quale l&#39;attività deve essere completata.

   **Nota:** l&#39;attività creata include anche il percorso della pagina a cui si applica il consiglio SEO.

1. Fai clic su Fine per chiudere il messaggio Attività creata.
