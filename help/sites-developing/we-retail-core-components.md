---
title: Prova dei componenti core in We.Retail
seo-title: Prova dei componenti core in We.Retail
description: Prova dei componenti core in We.Retail
seo-description: 'null'
uuid: 8d1cea0b-99d9-49b2-b275-41f14864b1ff
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: af3cd818-61cf-4da1-bfb5-87540911ddd5
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '544'
ht-degree: 4%

---


# Prova dei componenti core in We.Retail{#trying-out-core-components-in-we-retail}

I componenti core sono componenti moderni e flessibili, con facile estensibilità e facilità di integrazione nei progetti. I componenti core sono stati costruiti intorno a diversi principi di progettazione principali come HTL, usabilità out-of-the-box, configurabilità, controllo delle versioni ed estensibilità. We.Retail è stato creato sui componenti core.

## Prova {#trying-it-out}

1. Inizia AEM con il contenuto di esempio di We.Retail e apri la [Console componenti](/help/sites-authoring/default-components-console.md).

   **Navigazione globale -> Strumenti -> Componenti**

1. Aprendo la barra nella console Componenti, puoi filtrare un particolare gruppo di componenti. I componenti core si trovano in

   * `.core-wcm`: Componenti core standard
   * `.core-wcm-form`: Componenti core per l’invio del modulo

   Choose `.core-wcm`.

   ![chlimage_1-162](assets/chlimage_1-162.png)

1. Tieni presente che tutti i componenti core sono denominati **v1**, per indicare che si tratta della prima versione di questo componente core. Verranno rilasciate versioni regolari che saranno compatibili con AEM e consentiranno un aggiornamento semplice per sfruttare le funzioni più recenti.
1. Fare clic su **Testo (v1)**.

   Vedi che il **Tipo di risorsa** del componente è `/apps/core/wcm/components/text/v1/text`. I componenti core si trovano in `/apps/core/wcm/components` e dispongono di versioni per componente.

   ![chlimage_1-163](assets/chlimage_1-163.png)

1. Fai clic sulla scheda **Documentazione** per visualizzare la documentazione per gli sviluppatori relativa al componente.

   ![chlimage_1-164](assets/chlimage_1-164.png)

1. Torna alla console Componenti. Filtra il gruppo **We.Retail** e seleziona il componente **Testo** .
1. Vedi che il **Tipo risorsa** punta a un componente come previsto in `/apps/weretail` ma il **Super Type risorsa** punta nuovamente al componente principale `/apps/core/wcm/components/text/v1/text`.

   ![chlimage_1-165](assets/chlimage_1-165.png)

1. Fai clic sulla scheda **Live Usage** per vedere sulle pagine in cui è attualmente in uso questo componente. Fai clic sulla prima pagina **Grazie** per modificare la pagina.

   ![chlimage_1-166](assets/chlimage_1-166.png)

1. Nella pagina di ringraziamento, seleziona il componente di testo e fai clic sull’icona Annulla ereditarietà nel menu di modifica del componente.

   [We.Retail dispone di una struttura di sito globalizzata in cui il contenuto viene inviato dai master lingua alle copie ](/help/sites-developing/we-retail-globalized-site-structure.md) live tramite un meccanismo chiamato ereditarietà [ ](/help/sites-administering/msm.md). Per questo motivo, l’ereditarietà deve essere annullata per consentire all’utente di modificare manualmente il testo.

   ![chlimage_1-167](assets/chlimage_1-167.png)

1. Confermare l&#39;annullamento facendo clic su **Sì**.

   ![chlimage_1-168](assets/chlimage_1-168.png)

1. Una volta annullata l’ereditarietà e selezionato i componenti di testo, sono disponibili molte altre opzioni. Fai clic su** Modifica**.

   ![chlimage_1-169](assets/chlimage_1-169.png)

1. Ora puoi vedere quali opzioni di modifica sono disponibili per il componente testo.

   ![chlimage_1-170](assets/chlimage_1-170.png)

1. Dal menu **Informazioni pagina** selezionare **Modifica modello**.
1. Nell’Editor modelli della pagina, fai clic sull’icona **Criterio** del componente Testo nel **Contenitore di layout** della pagina.

   ![chlimage_1-171](assets/chlimage_1-171.png)

1. I componenti core consentono all’autore del modello di configurare quali proprietà sono disponibili per gli autori delle pagine. Queste includono funzioni quali le origini di incolla consentite, le opzioni di formattazione, gli stili di paragrafo disponibili, ecc.

   Tali finestre di dialogo di progettazione sono disponibili per molti componenti core e funzionano insieme all’editor modelli. Una volta abilitate, queste diventano disponibili per l’autore tramite gli editor componenti.

   ![chlimage_1-172](assets/chlimage_1-172.png)

## Ulteriori informazioni {#further-information}

Per ulteriori informazioni sui componenti core, consulta il documento sull’authoring [Componenti core](https://docs.adobe.com/content/help/it/experience-manager-core-components/using/introduction.html) per una panoramica delle funzionalità dei componenti core e il documento per sviluppatori [Sviluppo di componenti core](https://helpx.adobe.com/experience-manager/core-components/using/developing.html) per una panoramica tecnica.

Inoltre, potresti voler indagare ulteriormente sui [modelli modificabili](/help/sites-developing/we-retail-editable-templates.md). Per informazioni complete sui modelli modificabili, consulta il documento di authoring [Creazione di modelli di pagina](/help/sites-authoring/templates.md) o il documento per sviluppatori Pagina [Modelli - Modificabili](/help/sites-developing/page-templates-editable.md) .
