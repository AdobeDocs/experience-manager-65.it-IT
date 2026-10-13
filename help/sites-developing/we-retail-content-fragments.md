---
title: Prova dei frammenti di contenuto in We.Retail
description: Scopri come provare i frammenti di contenuto in Adobe Experience Manager utilizzando We.Retail.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: 1e5d8184-7164-4984-b43e-421015e8bf52
solution: Experience Manager, Experience Manager Sites
feature: Content Fragments,Developing
role: Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
  - id: a642c50e-80eb-4fc1-a5d2-f3762d1f841d
    internal-label: Administration
subfeature_v2:
  - id: e9db7c79-8f65-4281-a439-c9049296d903
    internal-label: Content Fragments
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 15%
---
# Prova dei frammenti di contenuto in We.Retail{#trying-out-content-fragments-in-we-retail}

I frammenti di contenuto consentono di creare contenuti indipendenti dal canale, con possibili varianti per canali specifici. **We.Retail** (come disponibile in un&#39;istanza predefinita di Adobe Experience Manager) fornisce il frammento **Arctic Surfing in Lofoten** come esempio di base. Questo mostra che:

* I frammenti di contenuto di Adobe Experience Manager (AEM) vengono [creati e gestiti come risorse indipendenti dalla pagina](/help/assets/content-fragments/content-fragments.md). Consentono di creare contenuti indipendenti dal canale, con possibili varianti per canali specifici.

  * Vedi [Dove trovare le risorse dei frammenti di contenuto in We.Retail](#where-to-find-content-fragments-in-we-retail)

* Potrai quindi [utilizzare questi frammenti e le relative varianti durante l&#39;authoring](/help/sites-authoring/content-fragments.md) delle pagine di contenuto.

  * Vedi [Dove vengono utilizzati i frammenti di contenuto in We.Retail](#where-content-fragments-are-used-in-we-retail)

Per la documentazione completa sulla creazione, la gestione, l’utilizzo e lo sviluppo di frammenti di contenuto:

* Vedi [Ulteriori informazioni](#further-information)

>[!NOTE]
>
>I **frammenti di contenuto** e i **[frammenti di esperienza](/help/sites-authoring/experience-fragments.md)** sono funzioni diverse in AEM:
>
>* **I frammenti di contenuto** sono contenuti editoriali, principalmente testo e immagini correlate. Sono contenuti puri, senza design e layout.
>* I **frammenti di esperienza** sono contenuti completi di layout, frammenti di una pagina web.
>
>I frammenti esperienza possono includere contenuti sotto forma di frammenti di contenuto, ma non viceversa.

## Dove trovare i frammenti di contenuto in We.Retail {#where-to-find-content-fragments-in-we-retail}

In We.Retail sono presenti diversi frammenti di contenuto di esempio; naviga tramite **Assets**, **Files**, **We.Retail**, **English**, **Experiences**.

Tra questi, **Arctic Surfing in Lofoten**, un frammento con le relative risorse visive:

* Naviga tramite **Assets**, **Files**, **We.Retail**, **English**, **Experiences**, **Arctic Surfing in Lofoten**:

  * [http://localhost:4502/assets.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten](http://localhost:4502/assets.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten)

![cf-44](assets/cf-44.png)

Puoi selezionare e modificare il frammento **Arctic Surfing in Lofoten**:

* [http://localhost:4502/editor.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten/arctic-surfing-in-lofoten](http://localhost:4502/editor.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten/arctic-surfing-in-lofoten)

Qui puoi [modificare e gestire](/help/assets/content-fragments/content-fragments.md) il frammento utilizzando le schede (pannello a sinistra):

<!--![cf-45-aa](do-not-localize/cf-45-aa.png) ![cf-45-a](do-not-localize/cf-45-a.png) ASSET does not exist-->

* **[Varianti](/help/assets/content-fragments/content-fragments-variations.md)** incluso [Markdown](/help/assets/content-fragments/content-fragments-markdown.md)
* **[Contenuto associato](/help/assets/content-fragments/content-fragments-assoc-content.md)**
* **[Metadati](/help/assets/content-fragments/content-fragments-metadata.md)**

![cf-46](assets/cf-46.png)

## Dove vengono utilizzati i frammenti di contenuto in We.Retail {#where-content-fragments-are-used-in-we-retail}

Per illustrare l&#39;authoring di [pagine con un frammento di contenuto](/help/sites-authoring/content-fragments.md) sono disponibili diverse pagine di esempio in, ad esempio:

* [http://localhost:4502/sites.html/content/we-retail/language-masters/en/experience](http://localhost:4502/sites.html/content/we-retail/language-masters/en/experience)

Ad esempio, nel frammento di contenuto **Arctic Surfing in Lofoten** è presente un riferimento nella pagina Sites:

* Naviga tramite **Sites**, **We.Retail**, **Language Masters**, **English**, **Experience**. Quindi apri **Arctic Surfing in Lofoten** per la modifica:

  * [http://localhost:4502/editor.html/content/we-retail/language-masters/en/experience/arctic-surfing-in-lofoten.html](http://localhost:4502/editor.html/content/we-retail/language-masters/en/experience/arctic-surfing-in-lofoten.html)

![cf-53](assets/cf-53.png)

## Ulteriori informazioni {#further-information}

Per ulteriori dettagli, consulta:

* [Utilizzo di frammenti di contenuto](/help/assets/content-fragments/content-fragments.md)

  * Scopri come creare, modificare e gestire le risorse dei frammenti di contenuto.

* [Authoring delle pagine con frammenti di contenuto](/help/sites-authoring/content-fragments.md)

  * Utilizza il frammento di contenuto quando crei una pagina.

* [Sviluppo di AEM: componenti per frammenti di contenuto](/help/sites-developing/components-content-fragments.md)

  * Panoramica dei componenti dei frammenti di contenuto.

* [Sviluppo ed estensione di frammenti di contenuto](/help/sites-developing/customizing-content-fragments.md)

  * Informazioni utili per sviluppare ed estendere frammenti di contenuto.
