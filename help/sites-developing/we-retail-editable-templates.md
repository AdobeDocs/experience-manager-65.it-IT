---
title: Prova di modelli modificabili in We.Retail
description: Scopri come provare i modelli modificabili in Adobe Experience Manager utilizzando We.Retail.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: efebe66d-3d30-4033-9c4c-ae347e134f2f
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 2%

---

# Prova di modelli modificabili in We.Retail{#trying-out-editable-templates-in-we-retail}

Con i modelli modificabili, la creazione e la manutenzione dei modelli non è più un&#39;attività che riguarda solo gli sviluppatori. Un tipo di utente avanzato, detto autore di modelli, può ora creare modelli. Gli sviluppatori devono comunque configurare l’ambiente, creare le librerie client e i componenti da utilizzare, ma una volta che queste nozioni di base sono implementate, l’autore del modello avrà la flessibilità di creare e configurare i modelli senza un progetto di sviluppo.

Tutte le pagine di We.Retail sono basate su modelli modificabili, che consentono a chi non è uno sviluppatore di adattare e personalizzare i modelli.

## Prova {#trying-it-out}

1. Modificare la pagina Apparecchiature del ramo principale della lingua.

   http://localhost:4502/editor.html/content/we-retail/language-masters/en/equipment.html

1. Il selettore della modalità non offre più la modalità Progettazione. Tutte le pagine di We.Retail sono basate su modelli modificabili e per modificare la progettazione di modelli modificabili devono essere modificate nell&#39;editor di modelli.
1. Dalla sezione **Informazioni pagina** selezione menu **Modifica modello**.
1. Stai modificando il modello Pagina principale.

   La modalità struttura della pagina consente di modificare la struttura del modello. Ad esempio, i componenti consentiti nel contenitore di layout.

   ![chlimage_1-138](assets/chlimage_1-138.png)

1. Configura i criteri per Contenitore di layout per definire quali componenti sono consentiti nel contenitore.

   I criteri equivalgono alle configurazioni di progettazione.

   ![chlimage_1-139](assets/chlimage_1-139.png)

1. Nella finestra di dialogo per progettazione del contenitore di layout, puoi

   * Seleziona un criterio esistente o creane uno per il contenitore
   * Seleziona i componenti consentiti nel contenitore
   * Definisci i componenti predefiniti da inserire quando una risorsa viene trascinata nel contenitore

   ![chlimage_1-140](assets/chlimage_1-140.png)

1. Nell’editor modelli, puoi modificare il criterio del componente testo all’interno del contenitore di layout.

   Questo consente di:

   * Seleziona un criterio esistente o creane uno per il contenitore
   * Definisci le funzioni disponibili per l’autore della pagina quando utilizza questo componente, ad esempio

      * Incolla origini consentite
      * Opzioni di formattazione
      * Stili di paragrafo consentiti
      * Caratteri speciali consentiti

   Molti componenti basati sui componenti core consentono la configurazione di opzioni a livello di componente tramite i modelli modificabili, eliminando la necessità di personalizzazione da parte degli sviluppatori.

   ![chlimage_1-141](assets/chlimage_1-141.png)

1. Nell’editor modelli, puoi utilizzare il selettore modalità per passare a **Contenuto iniziale** per definire il contenuto richiesto sulla pagina.

   **Layout** La modalità può essere utilizzata così come si trova in una pagina normale per definire il layout del modello.

## Ulteriori informazioni {#more-information}

Per ulteriori informazioni, consulta il documento di authoring [Creazione di modelli di pagina](/help/sites-authoring/templates.md) o la pagina del documento per sviluppatori [Modelli - Modificabili](/help/sites-developing/page-templates-editable.md) per informazioni tecniche complete sui modelli modificabili.

Potrebbe anche voler indagare [Componenti core](/help/sites-developing/we-retail-core-components.md). Consulta il documento di authoring [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it) per una panoramica delle funzionalità dei componenti core e del documento per sviluppatori [Sviluppo di componenti core](https://helpx.adobe.com/experience-manager/core-components/using/developing.html) per una panoramica tecnica.
