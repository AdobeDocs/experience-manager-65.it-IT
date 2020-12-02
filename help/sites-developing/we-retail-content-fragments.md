---
title: Prova di frammenti di contenuto in We.Retail
seo-title: Prova di frammenti di contenuto in We.Retail
description: 'null'
seo-description: 'null'
uuid: 66daddfe-8e98-47b6-8499-db055887ac17
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: d1326737-f378-46d0-9916-61ead4d31639
translation-type: tm+mt
source-git-commit: 759d2dd8d12861757bf7f54b77d8d3ca170887fe
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 21%

---


# Prova di frammenti di contenuto in We.Retail{#trying-out-content-fragments-in-we-retail}

I frammenti di contenuto consentono di creare contenuti versatili per i canali e varianti (eventualmente specifiche per i canali). **We.Retail** (come disponibile in un&#39;istanza out-of-the-box di AEM) fornisce il frammento  **Arctic Surfing in** Lofotenas come esempio di base. Questo dimostra che:

* I frammenti di contenuto di Adobe Experience Manager (AEM) vengono [creati e gestiti come risorse indipendenti dalla pagina](/help/assets/content-fragments/content-fragments.md). Consentono di creare contenuti versatili utilizzabili in qualsiasi canale, con possibili varianti per canali specifici.

   * Vedere [Dove trovare le risorse di frammenti di contenuto in We.Retail](#where-to-find-content-fragments-in-we-retail)

* È quindi possibile [utilizzare questi frammenti e le relative varianti durante l&#39;authoring delle pagine di contenuto.](/help/sites-authoring/content-fragments.md)

   * Vedere [Dove vengono utilizzati i frammenti di contenuto in We.Retail](#where-content-fragments-are-used-in-we-retail)

Per la documentazione completa sulla creazione, la gestione, l’utilizzo e lo sviluppo di frammenti di contenuto:

* Vedere [Ulteriori informazioni](#further-information)

>[!NOTE]
>
>I **frammenti di contenuto** e i **[frammenti esperienza](/help/sites-authoring/experience-fragments.md)** sono funzioni diverse in AEM:
>
>* I **frammenti di contenuto** sono contenuti editoriali, in particolare testo e immagini correlate. Sono contenuti puri, privi di design e layout.
>* I **frammenti esperienza** sono contenuti con un layout completo, un frammento di una pagina Web.

>
>
I frammenti esperienza possono includere contenuti sotto forma di frammenti di contenuto, ma non viceversa.

## Dove trovare i frammenti di contenuto in We.Retail {#where-to-find-content-fragments-in-we-retail}

Esistono diversi frammenti di contenuto di esempio in We.Retail; navigare tra **Risorse**, **File**, **We.Retail**, **Inglese**, **Esperienze**.

Tra questi, **Surf artico in Lofoten**, un frammento insieme alle relative risorse visive:

* Navigare tra **Risorse**, **File**, **We.Retail**, **Inglese**, **Esperienze**, **Artico Surfing in Lofoten**:

   * [http://localhost:4502/assets.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten](http://localhost:4502/assets.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten)

![cf-44](assets/cf-44.png)

È possibile selezionare e modificare il frammento **Surf artico in Lofoten**:

* [http://localhost:4502/editor.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten/arctic-surfing-in-lofoten](http://localhost:4502/editor.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten/arctic-surfing-in-lofoten)

Qui è possibile [modificare e gestire](/help/assets/content-fragments/content-fragments.md) il frammento utilizzando le schede (pannello a sinistra):

<!--![](do-not-localize/cf-45-aa.png) ![](do-not-localize/cf-45-a.png) ASSET does not exist-->

* **[](/help/assets/content-fragments/content-fragments-variations.md)** Variazioni, inclusa  [Markdown](/help/assets/content-fragments/content-fragments-markdown.md)
* **[Contenuto associato](/help/assets/content-fragments/content-fragments-assoc-content.md)**
* **[Metadati](/help/assets/content-fragments/content-fragments-metadata.md)**

![cf-46](assets/cf-46.png)

## Dove i frammenti di contenuto vengono utilizzati in We.Retail {#where-content-fragments-are-used-in-we-retail}

Per illustrare l&#39;authoring delle [pagine con un frammento di contenuto](/help/sites-authoring/content-fragments.md) sono disponibili diverse pagine di esempio, ad esempio:

* [http://localhost:4502/sites.html/content/we-retail/language-masters/en/experience](http://localhost:4502/sites.html/content/we-retail/language-masters/en/experience)

Ad esempio, il frammento di contenuto **Surf artico in Lofoten** è riportato nella pagina Siti:

* Navigare tra **Siti**, **We.Retail**, **Language Master**, **Inglese**, **Esperienza**. Quindi aprire **Arctic Surfing in Lofoten** per la modifica:

   * [http://localhost:4502/editor.html/content/we-retail/language-masters/en/experience/arctic-surfing-in-lofoten.html](http://localhost:4502/editor.html/content/we-retail/language-masters/en/experience/arctic-surfing-in-lofoten.html)

![cf-53](assets/cf-53.png)

## Ulteriori informazioni {#further-information}

Per ulteriori dettagli, consulta:

* [Utilizzo di frammenti di contenuto](/help/assets/content-fragments/content-fragments.md)

   * Scopri come creare, modificare e gestire le risorse Frammento di contenuto.

* [Authoring delle pagine con frammenti di contenuto](/help/sites-authoring/content-fragments.md)

   * Utilizzare il frammento di contenuto per la creazione di una pagina.

* [Sviluppo di AEM - Componenti per frammenti di contenuto](/help/sites-developing/components-content-fragments.md)

   * Panoramica dei componenti per i frammenti di contenuto.

* [Sviluppo ed estensione di frammenti di contenuto](/help/sites-developing/customizing-content-fragments.md)

   * Informazioni utili per sviluppare ed estendere i frammenti di contenuto.

