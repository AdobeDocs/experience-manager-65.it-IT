---
title: Prova del layout dinamico in We.Retail
description: Scopri come provare il layout dinamico in Adobe Experience Manager utilizzando We.Retail.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: 6df5fb10-a7f1-4d5d-ac00-b4be3d5d3d18
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 9%

---

# Prova del layout dinamico in We.Retail{#trying-out-responsive-layout-in-we-retail}

Tutte le pagine We.Retail utilizzano il componente Contenitore di layout per implementare una progettazione reattiva. Il contenitore layout fornisce un sistema paragrafo che consente di posizionare i componenti all’interno di una griglia reattiva. Questa griglia può ridisporre il layout in base alle dimensioni e al formato del dispositivo o della finestra. Il componente viene utilizzato insieme al **Layout** nell’editor pagina, che consente di creare e modificare il layout dinamico a seconda del dispositivo.

## Prova {#trying-it-out}

1. Modifica la pagina Arctic Surfing nella sezione Esperienze del ramo principale lingua.

   http://localhost:4502/editor.html/content/we-retail/language-masters/en/experience/arctic-surfing-in-lofoten.html

1. Passa a **Anteprima** per visualizzare la pagina così come verrebbe sottoposta a rendering per un visitatore del sito web. Scorri verso il basso fino al contenuto dell’articolo *Aloha spirits nella Norvegia settentrionale*.

   ![chlimage_1-178](assets/chlimage_1-178.png)

1. Ridimensiona la finestra del browser e osserva come il layout si adatta dinamicamente al ridimensionamento.

   ![chlimage_1-179](assets/chlimage_1-179.png)

1. Passa alla modalità Layout. La barra degli strumenti dell’emulatore viene visualizzata automaticamente e consente di pianificare il layout per dispositivo di destinazione.

   Selezionando un componente vengono visualizzate le opzioni mobile e nascosta nel menu Modifica insieme alle maniglie di ridimensionamento del componente.

   ![chlimage_1-180](assets/chlimage_1-180.png)

1. Se si trascina il quadratino di ridimensionamento del componente, viene visualizzata automaticamente la griglia di layout che consente di ridimensionarlo.

   ![chlimage_1-181](assets/chlimage_1-181.png)

## Ulteriori informazioni {#further-information}

Per ulteriori informazioni, consulta il documento di authoring [Layout reattivo](/help/sites-authoring/responsive-layout.md) o il documento dell’amministratore [Configurazione del contenitore di layout e della modalità layout](/help/sites-administering/configuring-responsive-layout.md) per dettagli tecnici completi.
