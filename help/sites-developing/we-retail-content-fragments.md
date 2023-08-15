---
title: Provare i frammenti di contenuto in We.Retail
description: Provare i frammenti di contenuto in We.Retail
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: 1e5d8184-7164-4984-b43e-421015e8bf52
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 14%

---

# Provare i frammenti di contenuto in We.Retail{#trying-out-content-fragments-in-we-retail}

I frammenti di contenuto consentono di creare contenuti indipendenti dal canale, con possibili varianti per canali specifici. **We.Retail** (come disponibile in un’istanza predefinita di Adobe Experience Manager) fornisce il frammento **Surf artico a Lofoten** come campione di base. Questo mostra che:

* I frammenti di contenuto di Adobe Experience Manager (AEM) vengono [creati e gestiti come risorse indipendenti dalla pagina](/help/assets/content-fragments/content-fragments.md). Consentono di creare contenuti indipendenti dal canale, con possibili varianti per canali specifici.

   * Consulta [Dove trovare le risorse dei frammenti di contenuto in We.Retail](#where-to-find-content-fragments-in-we-retail)

* Potrai quindi [utilizza questi frammenti e le relative varianti durante l’authoring](/help/sites-authoring/content-fragments.md) pagine di contenuti.

   * Consulta [Dove vengono utilizzati i frammenti di contenuto in We.Retail](#where-content-fragments-are-used-in-we-retail)

Per la documentazione completa sulla creazione, la gestione, l’utilizzo e lo sviluppo di frammenti di contenuto:

* Consulta [Ulteriori informazioni](#further-information)

>[!NOTE]
>
>I **frammenti di contenuto** e i **[frammenti di esperienza](/help/sites-authoring/experience-fragments.md)** sono funzioni diverse in AEM:
>
>* **Frammenti di contenuto** sono contenuti editoriali, principalmente testo e immagini correlate. Sono contenuti puri, senza design e layout.
>* I **frammenti di esperienza** sono contenuti completi di layout, frammenti di una pagina web.
>
>I frammenti esperienza possono includere contenuti sotto forma di frammenti di contenuto, ma non viceversa.

## Dove trovare i frammenti di contenuto in We.Retail {#where-to-find-content-fragments-in-we-retail}

In We.Retail sono presenti diversi frammenti di contenuto di esempio; naviga tramite **Risorse**, **File**, **We.Retail**, **Inglese**, **Esperienze**.

Questi includono **Surf artico a Lofoten**, un frammento con le relative risorse visive:

* Naviga tramite **Risorse**, **File**, **We.Retail**, **Inglese**, **Esperienze**, **Surf artico a Lofoten**:

   * [http://localhost:4502/assets.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten](http://localhost:4502/assets.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten)

![cf-44](assets/cf-44.png)

Puoi selezionare e modificare i **Surf artico a Lofoten** frammento:

* [http://localhost:4502/editor.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten/arctic-surfing-in-lofoten](http://localhost:4502/editor.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten/arctic-surfing-in-lofoten)

Qui è possibile [modifica e gestisci](/help/assets/content-fragments/content-fragments.md) frammento utilizzando le schede (pannello laterale sinistro):

<!--![cf-45-aa](do-not-localize/cf-45-aa.png) ![cf-45-a](do-not-localize/cf-45-a.png) ASSET does not exist-->

* **[Varianti](/help/assets/content-fragments/content-fragments-variations.md)** tra cui [Markdown](/help/assets/content-fragments/content-fragments-markdown.md)
* **[Contenuto associato](/help/assets/content-fragments/content-fragments-assoc-content.md)**
* **[Metadati](/help/assets/content-fragments/content-fragments-metadata.md)**

![cf-46](assets/cf-46.png)

## Dove vengono utilizzati i frammenti di contenuto in We.Retail {#where-content-fragments-are-used-in-we-retail}

Per illustrare [authoring delle pagine con un frammento di contenuto](/help/sites-authoring/content-fragments.md) in sono disponibili diverse pagine di esempio, ad esempio:

* [http://localhost:4502/sites.html/content/we-retail/language-masters/en/experience](http://localhost:4502/sites.html/content/we-retail/language-masters/en/experience)

Ad esempio, il **Surf artico a Lofoten** nella pagina Sites è presente un riferimento al frammento di contenuto:

* Naviga tramite **Sites**, **We.Retail**, **Master lingua**, **Inglese**, **Esperienza**. Quindi apri **Surf artico a Lofoten** per la modifica:

   * [http://localhost:4502/editor.html/content/we-retail/language-masters/en/experience/arctic-surfing-in-lofoten.html](http://localhost:4502/editor.html/content/we-retail/language-masters/en/experience/arctic-surfing-in-lofoten.html)

![cf-53](assets/cf-53.png)

## Ulteriori informazioni {#further-information}

Per ulteriori dettagli, consulta:

* [Utilizzo di frammenti di contenuto](/help/assets/content-fragments/content-fragments.md)

   * Scopri come creare, modificare e gestire le risorse dei frammenti di contenuto.

* [Authoring delle pagine con frammenti di contenuto](/help/sites-authoring/content-fragments.md)

   * Utilizza il frammento di contenuto quando crei una pagina.

* [Sviluppo AEM - Componenti per frammenti di contenuto](/help/sites-developing/components-content-fragments.md)

   * Panoramica dei componenti dei frammenti di contenuto.

* [Sviluppo ed estensione di frammenti di contenuto](/help/sites-developing/customizing-content-fragments.md)

   * Informazioni utili per sviluppare ed estendere frammenti di contenuto.
