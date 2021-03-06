---
title: Prova di modelli modificabili in We.Retail
seo-title: Prova di modelli modificabili in We.Retail
description: Prova di modelli modificabili in We.Retail
seo-description: 'null'
uuid: 0d4b97cb-efcc-4312-a783-eae3ecd6f889
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 3cc8ac23-98ff-449f-bd76-1203c7cbbed7
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 12%

---


# Prova i modelli modificabili in We.Retail{#trying-out-editable-templates-in-we-retail}

Con i modelli modificabili, la creazione e la manutenzione dei modelli non è più un&#39;attività riservata agli sviluppatori. Un tipo di utente avanzato, detto autore di modelli, può ora creare modelli. Gli sviluppatori devono comunque occuparsi di configurare l’ambiente, creare le librerie client e i componenti da utilizzare, ma una volta che questi elementi di base sono implementati, l’autore del modello avrà la flessibilità di creare e configurare i modelli senza un progetto di sviluppo.

Tutte le pagine in We.Retail si basano su modelli modificabili, che consentono agli sviluppatori di adattare e personalizzare i modelli.

## Prova {#trying-it-out}

1. Modificare la pagina Attrezzatura del ramo principale lingua.

   http://localhost:4502/editor.html/content/we-retail/language-masters/en/equipment.html

1. Il selettore della modalità non offre più una modalità Progettazione. Tutte le pagine per We.Retail si basano su modelli modificabili e per modificare la progettazione dei modelli modificabili è necessario modificarli nell’editor modelli.
1. Dal menu **Informazioni pagina** selezionare **Modifica modello**.
1. È in corso la modifica del modello Pagina eroe.

   La modalità struttura della pagina consente di modificare la struttura del modello. Ciò include, ad esempio, i componenti consentiti nel contenitore di layout.

   ![chlimage_1-138](assets/chlimage_1-138.png)

1. Configura i criteri per il Contenitore di layout per definire quali componenti sono consentiti nel contenitore.

   I criteri equivalgono alle configurazioni di progettazione.

   ![chlimage_1-139](assets/chlimage_1-139.png)

1. Nella finestra di dialogo di progettazione del contenitore di layout, è possibile

   * Selezionare un criterio esistente o crearne uno nuovo per il contenitore
   * Seleziona i componenti consentiti nel contenitore
   * Definisci i componenti predefiniti da inserire quando una risorsa viene trascinata nel contenitore

   ![chlimage_1-140](assets/chlimage_1-140.png)

1. Nell’editor modelli è possibile modificare il criterio del componente testo all’interno del contenitore di layout.

   Questo consente di:

   * Selezionare un criterio esistente o crearne uno nuovo per il contenitore
   * Definisci le funzioni disponibili per l’autore della pagina quando utilizzi questo componente, ad esempio

      * Incollare le origini consentite
      * Opzioni di formattazione
      * Stili di paragrafo consentiti
      * Caratteri speciali consentiti

   Molti componenti basati sui componenti core consentono di configurare opzioni a livello di componente tramite i modelli modificabili, eliminando la necessità di personalizzazione da parte degli sviluppatori.

   ![chlimage_1-141](assets/chlimage_1-141.png)

1. Sempre nell’editor modelli, puoi utilizzare il selettore della modalità per passare alla modalità **Contenuto iniziale** per definire il contenuto necessario sulla pagina.

   **** La modalità Layout può essere utilizzata così come si trova in una pagina normale per definire il layout del modello.

## Ulteriori informazioni {#more-information}

Per ulteriori informazioni, consulta il documento di authoring [Creazione di modelli di pagina](/help/sites-authoring/templates.md) o il documento per sviluppatori Pagina [Modelli - Modificabili](/help/sites-developing/page-templates-editable.md) per informazioni tecniche complete sui modelli modificabili.

È inoltre possibile esaminare [i componenti core](/help/sites-developing/we-retail-core-components.md). Per una panoramica tecnica, consulta il documento sull’authoring [Componenti core](https://docs.adobe.com/content/help/it/experience-manager-core-components/using/introduction.html) e il documento per sviluppatori [Sviluppo di componenti core](https://helpx.adobe.com/experience-manager/core-components/using/developing.html) .

