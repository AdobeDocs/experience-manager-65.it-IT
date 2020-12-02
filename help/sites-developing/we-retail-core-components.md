---
title: Prova dei componenti core in We.Retail
seo-title: Prova dei componenti core in We.Retail
description: 'null'
seo-description: 'null'
uuid: 8d1cea0b-99d9-49b2-b275-41f14864b1ff
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: af3cd818-61cf-4da1-bfb5-87540911ddd5
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '539'
ht-degree: 4%

---


# Prova dei componenti core in We.Retail{#trying-out-core-components-in-we-retail}

I componenti core sono componenti moderni e flessibili, con facilità di estensibilità e che consentono una semplice integrazione nei progetti. I componenti core sono stati creati sulla base di diversi importanti principi di progettazione come HTL, usabilità out-of-the-box, configurabilità, controllo delle versioni e estensibilità. We.Retail è stato costruito su componenti core.

## Prova {#trying-it-out}

1. Iniziate a AEM con il contenuto di esempio We.Retail e aprite la [console Componenti](/help/sites-authoring/default-components-console.md).

   **Navigazione globale -> Strumenti -> Componenti**

1. Aprendo la barra laterale nella console Componenti, potete filtrare un particolare gruppo di componenti. I componenti core sono disponibili in

   * `.core-wcm`: Componenti core standard
   * `.core-wcm-form`: Componenti di base per l’invio del modulo

   Choose `.core-wcm`.

   ![chlimage_1-162](assets/chlimage_1-162.png)

1. Tenere presente che tutti i componenti core sono denominati **v1**, e ciò riflette la prima versione di questo componente core. Le versioni regolari verranno rilasciate in futuro, che saranno compatibili con le AEM e consentiranno un semplice aggiornamento per sfruttare le funzionalità più recenti.
1. Fare clic su **Testo (v1)**.

   Verificare che il **Tipo risorsa** del componente sia `/apps/core/wcm/components/text/v1/text`. I componenti core si trovano in `/apps/core/wcm/components` e dispongono di versioni per componente.

   ![chlimage_1-163](assets/chlimage_1-163.png)

1. Fare clic sulla scheda **Documentazione** per visualizzare la documentazione per lo sviluppatore del componente.

   ![chlimage_1-164](assets/chlimage_1-164.png)

1. Tornate alla console dei componenti. Filtrare il gruppo **We.Retail** e selezionare il componente **Text**.
1. Vedere che il **Tipo risorsa** punta a un componente come previsto in `/apps/weretail`, ma il **Super Type risorsa** punta nuovamente al componente principale `/apps/core/wcm/components/text/v1/text`.

   ![chlimage_1-165](assets/chlimage_1-165.png)

1. Fare clic sulla scheda **Live Usage** per vedere su quali pagine è attualmente in uso il componente. Fare clic sulla prima pagina **Grazie** per modificare la pagina.

   ![chlimage_1-166](assets/chlimage_1-166.png)

1. Nella pagina di ringraziamento, selezionate il componente di testo e, nel menu di modifica del componente, fate clic sull’icona Annulla ereditarietà.

   [We.Retail dispone di una ](/help/sites-developing/we-retail-globalized-site-structure.md) struttura del sito globalizzata in cui il contenuto viene spinto dai master delle lingue alle copie  [live attraverso un meccanismo chiamato ereditarietà](/help/sites-administering/msm.md). Per questo motivo, l&#39;ereditarietà deve essere annullata per consentire all&#39;utente di modificare manualmente il testo.

   ![chlimage_1-167](assets/chlimage_1-167.png)

1. Confermare la cancellazione facendo clic su **Sì**.

   ![chlimage_1-168](assets/chlimage_1-168.png)

1. Una volta annullata l&#39;ereditarietà e selezionata la selezione dei componenti di testo, sono disponibili molte altre opzioni. Fare clic su** Edit*.

   ![chlimage_1-169](assets/chlimage_1-169.png)

1. È ora possibile visualizzare le opzioni di modifica disponibili per il componente di testo.

   ![chlimage_1-170](assets/chlimage_1-170.png)

1. Dal menu **Informazioni pagina** selezionare **Modifica modello**.
1. Nell&#39;Editor modelli della pagina, fare clic sull&#39;icona **Policy** del componente Testo nel **Contenitore di layout** della pagina.

   ![chlimage_1-171](assets/chlimage_1-171.png)

1. I componenti core consentono a un autore del modello di configurare le proprietà disponibili per gli autori delle pagine. tra cui funzioni quali le origini di incolla consentite, le opzioni di formattazione, gli stili di paragrafo disponibili, ecc.

   Tali finestre di dialogo sono disponibili per molti componenti core e collaborano con l’editor modelli. Una volta abilitati, sono disponibili per l’autore tramite gli editor di componenti.

   ![chlimage_1-172](assets/chlimage_1-172.png)

## Ulteriori informazioni {#further-information}

Per ulteriori informazioni sui componenti core, consultare il documento sull&#39;authoring [Componenti core](https://docs.adobe.com/content/help/it-IT/experience-manager-core-components/using/introduction.html) per una panoramica delle funzionalità dei componenti core e il documento sullo sviluppatore [Developing Core Components](https://helpx.adobe.com/experience-manager/core-components/using/developing.html) per una panoramica tecnica.

È inoltre possibile esaminare ulteriormente i [modelli modificabili](/help/sites-developing/we-retail-editable-templates.md). Per informazioni dettagliate sui modelli modificabili, fare riferimento al documento di authoring [Creazione di modelli di pagina](/help/sites-authoring/templates.md) o al documento di sviluppo Pagina [Modelli - Modificabili](/help/sites-developing/page-templates-editable.md).
