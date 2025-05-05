---
title: Incorporare un modulo adattivo o una comunicazione interattiva nell’applicazione a pagina singola AEM Sites
description: Incorporare moduli adattivi o comunicazioni interattive nelle pagine AEM Sites. Gli utenti possono compilare e inviare moduli senza uscire dalla pagina Sites.
topic-tags: author, interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Adaptive Forms
exl-id: b549f176-409a-4d81-8c2b-73d0dd0c6649
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '1107'
ht-degree: 0%

---

# Incorporare un modulo adattivo o una comunicazione interattiva nell’applicazione a pagina singola AEM Sites{#embed-an-adaptive-form-or-interactive-communication-in-aem-sites-single-page-application}

<span class="preview"> Adobe consiglia di utilizzare l&#39;acquisizione dati moderna ed estensibile [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=it) per [la creazione di un nuovo Forms adattivo](/help/forms/using/create-an-adaptive-form-core-components.md) o [l&#39;aggiunta di Forms adattivo alle pagine AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Questi componenti rappresentano un progresso significativo nella creazione di Forms adattivi, garantendo esperienze utente straordinarie. Questo articolo descrive un approccio precedente all’authoring di Forms adattivi utilizzando i componenti di base. </span>

## Panoramica {#overview}

AEM Forms consente agli sviluppatori di moduli di incorporare facilmente moduli adattivi e comunicazioni interattive in un’applicazione AEM Sites a pagina singola (SPA). Il modulo adattivo incorporato e la comunicazione interattiva sono completamente funzionali e gli utenti possono compilare e inviare il modulo senza uscire dalla pagina. Aiuta l’utente a rimanere nel contesto di altri elementi della pagina web e a interagire contemporaneamente con il modulo adattivo o la comunicazione interattiva.

Nell&#39;applicazione AEM Sites a pagina singola è possibile aggiungere un modulo adattivo o una comunicazione interattiva utilizzando il [componente Contenitore SPA di AEM Forms](../../forms/using/embed-adaptive-form-aem-sites-spa.md#af-component) [.](../../forms/using/embed-adaptive-form-aem-sites-spa.md#af-component) È un componente di AEM Forms per AEM Sites SPA che puoi aggiungere alla pagina Sites.

Per informazioni sull&#39;incorporamento di un modulo adattivo in un AEM Sites non SPA, consulta [Incorporare un modulo adattivo o una comunicazione interattiva nella pagina AEM Sites](/help/forms/using/embed-adaptive-form-aem-sites.md).

## Prerequisiti {#prerequisites}

Per incorporare un modulo adattivo o una comunicazione interattiva in un SPA dei siti AEM utilizzando il componente Contenitore SPA di AEM Forms, assicurati di aver installato:

* Java SE Development Kit 8 o successivo
* Apache Maven 3.3.1 o successivo
* Istanza di authoring AEM
* [Pacchetto del componente aggiuntivo AEM Forms 6.4.2](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) nell&#39;istanza di authoring

## Installare il componente Contenitore SPA di AEM Forms {#install-aem-forms-spa-container-component}

Esegui la procedura seguente per installare il componente Contenitore SPA di AEM Forms:

1. [Clona o scarica il componente AEM Forms per SPA](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa).
1. Installa il componente AEM Forms per l’SPA. Le istruzioni per installare il componente sono disponibili nel file [README.md](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa#aem-form-component).

   Il componente include un [componente React di esempio](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa/react-component) che può essere utilizzato per integrare il componente contenitore SPA con un progetto SPA basato su React.

1. [Clona o scarica un progetto SPA basato su React](https://github.com/adobe/aem-sample-we-retail-journal).
1. Integra il componente contenitore SPA con un progetto SPA basato su React utilizzando le istruzioni disponibili nel file [README.md](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa/react-component#aem-form-react-component-for-spa---editor).

   Dopo aver installato il componente Contenitore SPA di AEM Forms e aver integrato il componente con un progetto SPA basato su React, puoi incorporare moduli adattivi e comunicazioni interattive nella pagina di AEM Sites.

## Incorporare un modulo adattivo o una comunicazione interattiva {#af-component}

Per incorporare un modulo adattivo o una comunicazione interattiva utilizzando il componente Contenitore di AEM Forms per SPA:

1. Apri la pagina dei siti AEM, in modalità di modifica, in cui desideri incorporare un modulo adattivo o una comunicazione interattiva.
1. Inserire il modulo **AEM per il componente SPA** nella pagina utilizzando una delle opzioni seguenti:

   * Selezionare il contenitore di layout nella pagina Sites, selezionare **+** e selezionare il **modulo AEM per il componente SPA**.

   * Dal pannello del browser Componenti, trascina il modulo **AEM per il componente SPA** sulla pagina.
   * Cerca un modulo adattivo o una comunicazione interattiva nel browser Assets e trascinalo sulla pagina Sites. Incorpora il modulo in un contenitore di componenti AEM Forms for SPA.

   >[!NOTE]
   >
   >Il rendering di più componenti AEM Forms SPA Container in una pagina non è supportato. Puoi avere più Contenitori SPA di AEM Forms su una pagina, ma viene eseguito il rendering di un solo componente alla volta. Assicurati che in una pagina sia visibile un solo componente per evitare discrepanze.

1. Seleziona il componente Contenitore SPA di AEM Forms incorporato nella pagina Sites, quindi seleziona ![settings_icon](assets/settings_icon.png) nella barra delle azioni. Viene visualizzata la finestra di dialogo **Modifica contenitore SPA di AEM Forms**.
1. Nella finestra di dialogo **Modifica contenitore AEM Forms**, specifica quanto segue:

   * **Tipo risorsa:** Seleziona il tipo di risorsa da incorporare. Le opzioni sono **Modulo adattivo** e **Comunicazione interattiva**

   * **Percorso risorsa**: sfoglia e seleziona il modulo adattivo o la comunicazione interattiva da incorporare. Il campo viene compilato automaticamente se viene inserito un modulo adattivo o una comunicazione interattiva tramite il browser Assets.
   * **Canale** (solo comunicazione interattiva): seleziona il tipo di canale interattivo da incorporare. Le opzioni sono **Canale Web** e **Canale di stampa**.

   * **Tema**: seleziona un tema che definisca lo stile dei componenti del modulo adattivo o della comunicazione interattiva. Lo stile include proprietà di aspetto quali lo stile del carattere, il colore di sfondo, le dimensioni e l&#39;allineamento.

1. Seleziona ![icona_completato](assets/done_icon.png) per salvare le impostazioni. Il modulo adattivo o la comunicazione interattiva è ora incorporato nella pagina.

## Modulo adattivo integrato e comunicazione interattiva Publish {#publish-embedded-adaptive-form-and-interactive-communication}

Considera i seguenti scenari per la pubblicazione di una risorsa incorporata (modulo adattivo o comunicazione interattiva) sulla pagina di AEM Sites:

* Se pubblichi la pagina AEM Sites per la prima volta e include un modulo adattivo incorporato o una comunicazione interattiva, pubblica la pagina Sites e la risorsa incorporata.
* Se hai modificato solo il modulo adattivo incorporato o la comunicazione interattiva in una pagina Sites pubblicata, pubblica la risorsa originale e le modifiche si riflettono nella pagina Sites pubblicata. La pagina Sites pubblicata include un riferimento alla risorsa e non richiede la ripubblicazione della pagina.
* Se hai modificato la pagina Sites e il modulo adattivo incorporato o la comunicazione interattiva, ripubblica la pagina Sites e la risorsa incorporata.

## Modifica modulo adattivo incorporato e comunicazione interattiva {#modify-embedded-adaptive-form-and-interactive-communication}

La pagina dei siti AEM mantiene un riferimento al modulo adattivo e alla comunicazione interattiva nel contenitore di AEM Forms. Pertanto, tutte le configurazioni e le proprietà, come il tema, gli stili e l’azione di invio, configurate nel modulo adattivo originale e nella comunicazione interattiva vengono mantenute nel modulo adattivo incorporato e nella comunicazione interattiva.

Per modificare la configurazione o la proprietà del modulo adattivo incorporato e della comunicazione interattiva, effettua una delle seguenti operazioni.

* Apri il modulo originale nei moduli adattivi o nella comunicazione interattiva nei rispettivi editor e modificali.
* Selezionare il modulo adattivo o la comunicazione interattiva dalla pagina Sites in modalità di modifica, quindi selezionare **Modifica in una nuova finestra**. Il modulo originale si apre in modalità di modifica.

## Considerazioni e best practice {#considerations-and-best-practices}

Quando incorpori moduli adattivi nelle pagine dei siti AEM, considera gli aspetti seguenti:

* Intestazione e piè di pagina nel modulo originale non sono inclusi nel modulo incorporato.
* Le bozze utente e gli invii di moduli incorporati sono supportati e visibili nelle schede Bozze e Forms inviate nel portale dei moduli.
* L’azione di invio configurata nel modulo originale viene mantenuta nel modulo incorporato.
* Il targeting delle esperienze e i test A/B configurati nel modulo originale non funzionano nel modulo incorporato. Tuttavia, puoi utilizzare il targeting dell’esperienza nella pagina Sites per presentare diversi moduli in base ai profili utente.
* Se hai configurato Adobe Analytics per il modulo originale, i dati di analisi del modulo incorporato vengono acquisiti in Adobe Analytics. Tuttavia, non è disponibile nel rapporto di analisi di Forms.
