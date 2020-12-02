---
title: Prova di modelli modificabili in We.Retail
seo-title: Prova di modelli modificabili in We.Retail
description: 'null'
seo-description: 'null'
uuid: 0d4b97cb-efcc-4312-a783-eae3ecd6f889
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 3cc8ac23-98ff-449f-bd76-1203c7cbbed7
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 13%

---


# Prova di modelli modificabili in We.Retail{#trying-out-editable-templates-in-we-retail}

Con i modelli modificabili, la creazione e la manutenzione dei modelli non è più un&#39;attività che interessa solo gli sviluppatori. Un tipo di utente con privilegi di potenza, chiamato autore di un modello, può ora creare dei modelli. Gli sviluppatori devono comunque occuparsi di configurare l’ambiente, creare le librerie client e i componenti da utilizzare, ma una volta che questi elementi di base sono implementati, l’autore del modello avrà la flessibilità di creare e configurare i modelli senza un progetto di sviluppo.

Tutte le pagine in We.Retail si basano su modelli modificabili, consentendo agli utenti non sviluppatori di adattare e personalizzare i modelli.

## Prova {#trying-it-out}

1. Modificare la pagina Apparecchiature della sezione master lingua.

   http://localhost:4502/editor.html/content/we-retail/language-masters/en/equipment.html

1. Il selettore di modalità non offre più una modalità Progettazione. Tutte le pagine per We.Retail si basano su modelli modificabili e per modificare la progettazione dei modelli modificabili devono essere modificate nell&#39;editor modelli.
1. Dal menu **Informazioni pagina** selezionare **Modifica modello**.
1. È in corso la modifica del modello Pagina eroica.

   La modalità struttura della pagina consente di modificare la struttura del modello. Questo include, ad esempio, i componenti consentiti nel Contenitore di layout.

   ![chlimage_1-138](assets/chlimage_1-138.png)

1. Configurare i criteri per il Contenitore di layout per definire quali componenti sono consentiti nel contenitore.

   I criteri sono l&#39;equivalente delle configurazioni di progettazione.

   ![chlimage_1-139](assets/chlimage_1-139.png)

1. Nella finestra di dialogo di progettazione del Contenitore di layout, potete

   * Selezionate un criterio esistente o create un nuovo criterio per il contenitore
   * Selezionare i componenti consentiti nel contenitore
   * Definire i componenti predefiniti da inserire quando una risorsa viene trascinata nel contenitore

   ![chlimage_1-140](assets/chlimage_1-140.png)

1. Nell’editor modelli potete modificare il criterio del componente di testo all’interno del contenitore di layout.

   Questo consente di:

   * Selezionate un criterio esistente o create un nuovo criterio per il contenitore
   * Definire le funzioni disponibili per l’autore della pagina quando si utilizza questo componente, come

      * Origine Incolla consentita
      * Opzioni di formattazione
      * Stili di paragrafo consentiti
      * Caratteri speciali consentiti

   Molti componenti basati sui componenti core consentono di configurare le opzioni a livello di componente attraverso i modelli modificabili, eliminando la necessità di personalizzazione da parte degli sviluppatori.

   ![chlimage_1-141](assets/chlimage_1-141.png)

1. Nell&#39;editor modelli, potete utilizzare il selettore modalità per passare alla modalità **Contenuto iniziale** per definire il contenuto necessario sulla pagina.

   **La modalità** Layout può essere utilizzata così come si trova su una pagina normale per definire il layout del modello.

## Ulteriori informazioni {#more-information}

Per ulteriori informazioni, consultare il documento di authoring [Creazione di modelli di pagina](/help/sites-authoring/templates.md) o il documento sviluppatore Pagina [Modelli - Modificabili](/help/sites-developing/page-templates-editable.md) per informazioni tecniche complete sui modelli modificabili.

È inoltre possibile esaminare i [componenti core](/help/sites-developing/we-retail-core-components.md). Per una panoramica tecnica, consulta il documento sull’authoring [Componenti di base](https://docs.adobe.com/content/help/it-IT/experience-manager-core-components/using/introduction.html) e il documento sullo sviluppo [Sviluppo di componenti di base](https://helpx.adobe.com/experience-manager/core-components/using/developing.html).

