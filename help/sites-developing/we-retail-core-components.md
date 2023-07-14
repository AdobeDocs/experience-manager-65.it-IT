---
title: Prova dei componenti core in We.Retail
description: Prova dei componenti core in We.Retail
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: b5f2be67-c93c-4dbc-acc0-3edd8f1a282f
source-git-commit: 69346a710708ee659ee97e9fdc193c8ea2658fe6
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 5%

---

# Prova dei componenti core in We.Retail{#trying-out-core-components-in-we-retail}

I componenti core sono componenti moderni e flessibili, facilmente estensibili e semplici da integrare nei progetti. I componenti core sono stati progettati in base a diversi principi di progettazione principali, come HTL, facilità d’uso, configurabilità, controllo delle versioni ed estensibilità. We.Retail è stato creato su componenti core.

## Prova {#trying-it-out}

1. Avvia Adobe Experience Manager (AEM) con il contenuto di esempio We.Retail e apri [Console Componenti](/help/sites-authoring/default-components-console.md).

   **Navigazione globale -> Strumenti -> Componenti**

1. Aprendo la barra nella console Componenti, puoi filtrare per un particolare gruppo di componenti. I Componenti core sono disponibili in

   * `.core-wcm`: Componenti core standard
   * `.core-wcm-form`: componenti core per l’invio dei moduli

   Scegli `.core-wcm`.

   ![chlimage_1-162](assets/chlimage_1-162.png)

1. Tutti i componenti core sono denominati **v1**, a indicare che si tratta della prima versione di questo componente core. Versioni regolari verranno rilasciate in futuro, che saranno compatibili con le versioni di AEM e consentiranno un facile aggiornamento in modo da poter sfruttare le funzioni più recenti.
1. Clic **Testo (v1)**.

   Vedi che il **Tipo di risorsa** del componente è `/apps/core/wcm/components/text/v1/text`. I componenti core si trovano in `/apps/core/wcm/components` Le versioni di e sono suddivise per componente.

   ![chlimage_1-163](assets/chlimage_1-163.png)

1. Fai clic su **Documentazione** per visualizzare la documentazione per gli sviluppatori del componente.

   ![chlimage_1-164](assets/chlimage_1-164.png)

1. Torna alla console Componenti. Filtro per il gruppo **We.Retail** e seleziona la **Testo** componente.
1. Vedi che il **Tipo di risorsa** punta a un componente come previsto in `/apps/weretail` ma il **Super Type risorsa** torna al componente core `/apps/core/wcm/components/text/v1/text`.

   ![chlimage_1-165](assets/chlimage_1-165.png)

1. Fai clic su **Utilizzo live** per vedere su quali pagine viene utilizzato questo componente. Fai clic sul primo **Grazie** per modificare la pagina.

   ![chlimage_1-166](assets/chlimage_1-166.png)

1. Nella pagina di ringraziamento, seleziona il componente testo e fai clic sull’icona Annulla ereditarietà nel menu Modifica del componente.

   [We.Retail ha una struttura del sito globalizzata](/help/sites-developing/we-retail-globalized-site-structure.md) in cui il contenuto viene inviato da lingue master a [live copy tramite un meccanismo denominato ereditarietà](/help/sites-administering/msm.md). Per questo motivo, è necessario annullare l’ereditarietà per consentire a un utente di modificare manualmente il testo.

   ![chlimage_1-167](assets/chlimage_1-167.png)

1. Conferma l’annullamento facendo clic su **Sì**.

   ![chlimage_1-168](assets/chlimage_1-168.png)

1. Una volta annullata l’ereditarietà e selezionati i componenti di testo, sono disponibili molte altre opzioni. Clic **Modifica**.

   ![chlimage_1-169](assets/chlimage_1-169.png)

1. Ora puoi vedere quali opzioni di modifica sono disponibili per il componente testo.

   ![chlimage_1-170](assets/chlimage_1-170.png)

1. Dalla sezione **Informazioni pagina** menu, seleziona **Modifica modello**.
1. Nell’Editor modelli della pagina, fai clic su **Policy** del componente Testo nella sezione **Contenitore di layout** della pagina.

   ![chlimage_1-171](assets/chlimage_1-171.png)

1. I Componenti core consentono all’autore di un modello di configurare quali proprietà sono disponibili per gli autori di pagine. Queste includono funzioni quali le origini Incolla consentite, le opzioni di formattazione e gli stili di paragrafo disponibili.

   Tali finestre di dialogo di progettazione sono disponibili per molti componenti core e funzionano in parallelo con l’editor di modelli. Una volta abilitate, sono disponibili per l’autore tramite gli editor dei componenti.

   ![chlimage_1-172](assets/chlimage_1-172.png)

## Ulteriori informazioni {#further-information}

Per ulteriori informazioni sui Componenti core, consulta il documento di authoring [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it) per una panoramica delle funzionalità dei componenti core e del documento per sviluppatori [Sviluppo di componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/overview.html?lang=it) per una panoramica tecnica.

Inoltre, potrebbe essere utile approfondire le indagini [modelli modificabili](/help/sites-developing/we-retail-editable-templates.md). Consulta il documento di authoring [Creazione di modelli di pagina](/help/sites-authoring/templates.md) o la pagina del documento per sviluppatori [Modelli - Modificabili](/help/sites-developing/page-templates-editable.md) per informazioni complete sui modelli modificabili.
