---
title: Prova del layout responsive in We.Retail
description: Scopri come provare il layout dinamico in Adobe Experience Manager utilizzando We.Retail.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: 6df5fb10-a7f1-4d5d-ac00-b4be3d5d3d18
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 13%
---
# Prova del layout responsive in We.Retail{#trying-out-responsive-layout-in-we-retail}

Tutte le pagine We.Retail utilizzano il componente Contenitore di layout per implementare una progettazione reattiva. Il contenitore layout fornisce un sistema paragrafo che consente di posizionare i componenti all’interno di una griglia reattiva. Questa griglia può ridisporre il layout in base alle dimensioni e al formato del dispositivo o della finestra. Il componente viene utilizzato insieme alla modalità **Layout** nell&#39;editor pagina, che consente di creare e modificare il layout dinamico in base al dispositivo.

## Prova {#trying-it-out}

1. Modifica la pagina Arctic Surfing nella sezione Esperienze del ramo principale lingua.

   http://localhost:4502/editor.html/content/we-retail/language-masters/en/experience/arctic-surfing-in-lofoten.html

1. Passa a **Anteprima** per visualizzare la pagina così come verrebbe visualizzata da un visitatore del sito Web. Scorri verso il basso fino al contenuto dell&#39;articolo *Aloha spirits in Norther Norway*.

   ![chlimage_1-178](assets/chlimage_1-178.png)

1. Ridimensiona la finestra del browser e osserva come il layout si adatta dinamicamente al ridimensionamento.

   ![chlimage_1-179](assets/chlimage_1-179.png)

1. Passa alla modalità Layout. La barra degli strumenti dell’emulatore viene visualizzata automaticamente e consente di pianificare il layout per dispositivo di destinazione.

   Selezionando un componente vengono visualizzate le opzioni mobile e nascosta nel menu Modifica insieme alle maniglie di ridimensionamento del componente.

   ![chlimage_1-180](assets/chlimage_1-180.png)

1. Se si trascina il quadratino di ridimensionamento del componente, viene visualizzata automaticamente la griglia di layout che consente di ridimensionarlo.

   ![chlimage_1-181](assets/chlimage_1-181.png)

## Ulteriori informazioni {#further-information}

Per ulteriori informazioni, vedere il documento di creazione [Layout reattivo](/help/sites-authoring/responsive-layout.md) o il documento dell&#39;amministratore [Configurazione del contenitore di layout e della modalità di layout](/help/sites-administering/configuring-responsive-layout.md) per informazioni tecniche complete.
