---
title: Prova dei componenti core in We.Retail
description: Scopri come provare i componenti core in Adobe Experience Manager utilizzando We.Retail.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: b5f2be67-c93c-4dbc-acc0-3edd8f1a282f
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 4%

---

# Prova dei componenti core in We.Retail{#trying-out-core-components-in-we-retail}

I componenti core sono componenti moderni e flessibili, facilmente estensibili e semplici da integrare nei progetti. I componenti core sono stati progettati in base a diversi principi di progettazione principali, come HTL, facilità d’uso, configurabilità, controllo delle versioni ed estensibilità. We.Retail è stato creato su componenti core.

## Prova {#trying-it-out}

1. Avvia Adobe Experience Manager (AEM) con il contenuto di esempio We.Retail e apri [la console Componenti](/help/sites-authoring/default-components-console.md).

   **Navigazione globale > Strumenti > Componenti**

1. Aprendo la barra nella console Componenti, puoi filtrare per un particolare gruppo di componenti. I Componenti core sono disponibili in

   * `.core-wcm`: Componenti core standard
   * `.core-wcm-form`: componenti core per l&#39;invio dei moduli

   Scegli `.core-wcm`.

   ![chlimage_1-162](assets/chlimage_1-162.png)

1. Tutti i componenti core sono denominati **v1**, a indicare che si tratta della prima versione di questo componente core. Versioni regolari verranno rilasciate in futuro, che saranno compatibili con le versioni di AEM e consentiranno un facile aggiornamento in modo da poter sfruttare le funzioni più recenti.
1. Fare clic su **Testo (v1)**.

   Vedi che il **tipo di risorsa** del componente è `/apps/core/wcm/components/text/v1/text`. I componenti core si trovano in `/apps/core/wcm/components` e dispongono di versioni per componente.

   ![chlimage_1-163](assets/chlimage_1-163.png)

1. Fai clic sulla scheda **Documentazione** per visualizzare la documentazione per gli sviluppatori del componente.

   ![chlimage_1-164](assets/chlimage_1-164.png)

1. Torna alla console Componenti. Filtra per il gruppo **We.Retail** e seleziona il componente **Text**.
1. Verificare che il **Tipo risorsa** punti a un componente come previsto in `/apps/weretail`, ma il **Super Tipo risorsa** punti al componente di base `/apps/core/wcm/components/text/v1/text`.

   ![chlimage_1-165](assets/chlimage_1-165.png)

1. Fai clic sulla scheda **Utilizzo live** per vedere su quali pagine viene utilizzato questo componente. Fai clic sulla prima pagina di **ringraziamento** per modificare la pagina.

   ![chlimage_1-166](assets/chlimage_1-166.png)

1. Nella pagina di ringraziamento, seleziona il componente testo e fai clic sull’icona Annulla ereditarietà nel menu Modifica del componente.

   [We.Retail ha una struttura globalizzata del sito](/help/sites-developing/we-retail-globalized-site-structure.md) in cui il contenuto viene inviato dalle rappresentazioni master del linguaggio a [Live Copy tramite un meccanismo denominato ereditarietà](/help/sites-administering/msm.md). Per questo motivo, è necessario annullare l’ereditarietà per consentire a un utente di modificare manualmente il testo.

   ![chlimage_1-167](assets/chlimage_1-167.png)

1. Confermare l&#39;annullamento facendo clic su **Sì**.

   ![chlimage_1-168](assets/chlimage_1-168.png)

1. Una volta annullata l’ereditarietà e selezionati i componenti di testo, sono disponibili molte altre opzioni. Fai clic su **Modifica**.

   ![chlimage_1-169](assets/chlimage_1-169.png)

1. Ora puoi vedere quali opzioni di modifica sono disponibili per il componente testo.

   ![chlimage_1-170](assets/chlimage_1-170.png)

1. Dal menu **Informazioni pagina**, selezionare **Modifica modello**.
1. Nell&#39;Editor modelli della pagina fare clic sull&#39;icona **Policy** del componente Testo nel **Contenitore layout** della pagina.

   ![chlimage_1-171](assets/chlimage_1-171.png)

1. I Componenti core consentono all’autore di un modello di configurare quali proprietà sono disponibili per gli autori di pagine. Queste includono funzioni quali le origini Incolla consentite, le opzioni di formattazione e gli stili di paragrafo disponibili.

   Tali finestre di dialogo di progettazione sono disponibili per molti componenti core e funzionano in parallelo con l’editor di modelli. Una volta abilitate, sono disponibili per l’autore tramite gli editor dei componenti.

   ![chlimage_1-172](assets/chlimage_1-172.png)

## Ulteriori informazioni {#further-information}

Per ulteriori informazioni sui Componenti core, vedi il documento di authoring [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it) per una panoramica delle funzionalità dei Componenti core e il documento per sviluppatori [Sviluppo di Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/overview.html?lang=it) per una panoramica tecnica.

È inoltre possibile esaminare ulteriormente [modelli modificabili](/help/sites-developing/we-retail-editable-templates.md). Per informazioni complete sui modelli modificabili, consultare il documento di creazione [Creazione di modelli di pagina](/help/sites-authoring/templates.md) o il documento per sviluppatori Pagina [Modelli - Modificabili](/help/sites-developing/page-templates-editable.md).
