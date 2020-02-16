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

---


# Prova dei componenti core in We.Retail{#trying-out-core-components-in-we-retail}

I componenti core sono componenti moderni e flessibili, con facilità di estensibilità e per una semplice integrazione nei progetti. I componenti core sono stati creati sulla base di diversi importanti principi di progettazione come HTL, usabilità out-of-the-box, configurabilità, controllo delle versioni e estensibilità. We.Retail è stato costruito su componenti core.

## Provarci {#trying-it-out}

1. Avviate AEM con il contenuto di esempio We.Retail e aprite la console [](/help/sites-authoring/default-components-console.md)Componenti.

   **Navigazione globale -> Strumenti -> Componenti**

1. Aprendo la barra laterale nella console Componenti, potete filtrare un particolare gruppo di componenti. I componenti core sono disponibili in

   * `.core-wcm`: Componenti core standard
   * `.core-wcm-form`: Componenti di base per l’invio del modulo
   Choose `.core-wcm`.

   ![chlimage_1-162](assets/chlimage_1-162.png)

1. Tutti i componenti core sono denominati **v1**, riflettendo che si tratta della prima versione di questo componente core. Verranno rilasciate versioni regolari che saranno compatibili con le versioni di AEM e consentiranno un aggiornamento semplice per sfruttare le funzionalità più recenti.
1. Fate clic su **Testo (v1)**.

   Verificare che il tipo **di** risorsa del componente sia `/apps/core/wcm/components/text/v1/text`. I componenti core si trovano in `/apps/core/wcm/components` e dispongono di versioni per componente.

   ![chlimage_1-163](assets/chlimage_1-163.png)

1. Fate clic sulla scheda **Documentazione** per visualizzare la documentazione per lo sviluppatore del componente.

   ![chlimage_1-164](assets/chlimage_1-164.png)

1. Tornate alla console dei componenti. Filtrare il gruppo **We.Retail** e selezionare il componente **Testo** .
1. Vedere che il tipo **di** risorsa punta a un componente come previsto in `/apps/weretail` ma il Super Type **** risorsa punta nuovamente al componente principale `/apps/core/wcm/components/text/v1/text`.

   ![chlimage_1-165](assets/chlimage_1-165.png)

1. Fate clic sulla scheda **Live Usage (Uso** dinamico) per vedere sulle pagine in cui il componente è attualmente in uso. Fate clic sulla prima pagina di **ringraziamento** per modificare la pagina.

   ![chlimage_1-166](assets/chlimage_1-166.png)

1. Nella pagina di ringraziamento, selezionate il componente di testo e, nel menu di modifica del componente, fate clic sull’icona Annulla ereditarietà.

   [We.Retail ha una struttura](/help/sites-developing/we-retail-globalized-site-structure.md) del sito globalizzata in cui il contenuto viene spinto dai master delle lingue alle copie [live attraverso un meccanismo chiamato ereditarietà](/help/sites-administering/msm.md). Per questo motivo, l&#39;ereditarietà deve essere annullata per consentire all&#39;utente di modificare manualmente il testo.

   ![chlimage_1-167](assets/chlimage_1-167.png)

1. Confermate l&#39;annullamento facendo clic su **Sì**.

   ![chlimage_1-168](assets/chlimage_1-168.png)

1. Una volta annullata l&#39;ereditarietà e selezionata la selezione dei componenti di testo, sono disponibili molte altre opzioni. Fare clic su** Edit*.

   ![chlimage_1-169](assets/chlimage_1-169.png)

1. È ora possibile visualizzare le opzioni di modifica disponibili per il componente di testo.

   ![chlimage_1-170](assets/chlimage_1-170.png)

1. Dal menu Informazioni **** pagina, selezionate **Modifica modello**.
1. Nell&#39;Editor modelli della pagina, fare clic sull&#39;icona **Criterio** del componente Testo nel Contenitore **di** layout della pagina.

   ![chlimage_1-171](assets/chlimage_1-171.png)

1. I componenti core consentono a un autore del modello di configurare le proprietà disponibili per gli autori delle pagine. tra cui funzioni quali le sorgenti Incolla consentite, le opzioni di formattazione, gli stili di paragrafo disponibili, ecc.

   Tali finestre di dialogo sono disponibili per molti componenti core e collaborano con l’editor modelli. Una volta abilitati, sono disponibili per l’autore tramite gli editor componenti.

   ![chlimage_1-172](assets/chlimage_1-172.png)

## Ulteriori informazioni {#further-information}

Per ulteriori informazioni sui componenti core, consulta il documento di authoring [Core Components](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html) (Componenti [di base) per una panoramica delle funzionalità dei componenti core e il documento di sviluppo](https://helpx.adobe.com/experience-manager/core-components/using/developing.html) Developing Core Components (Sviluppo di componentidi base) per una panoramica tecnica.

È inoltre possibile esaminare ulteriormente i modelli [](/help/sites-developing/we-retail-editable-templates.md)modificabili. Per informazioni dettagliate sui modelli modificabili, fare riferimento al documento di authoring [Creazione di modelli](/help/sites-authoring/templates.md) di pagina o al documento di sviluppo [Modelli di pagina - Modificabili](/help/sites-developing/page-templates-editable.md) .
