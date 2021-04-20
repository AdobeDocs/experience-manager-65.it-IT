---
title: Incorporare un modulo adattivo o una comunicazione interattiva nell’applicazione a pagina singola AEM Sites
seo-title: Incorporare moduli adattivi o comunicazioni interattive nelle pagine AEM Sites
description: Incorporare moduli adattivi o comunicazioni interattive nelle pagine AEM Sites. Gli utenti possono compilare e inviare i moduli senza uscire dalla pagina Sites.
seo-description: È possibile incorporare moduli adattivi o comunicazioni interattive nelle pagine di AEM Sites. Gli utenti possono compilare e inviare i moduli senza uscire dalla pagina Sites.
uuid: 4c75494e-e9d2-43b9-bbae-562e0eda8abb
topic-tags: author, interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a74ed6c1-3006-4baf-bd77-ad4045e23c22
docset: aem65
feature: Adaptive Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1123'
ht-degree: 0%

---


# Incorporare un modulo adattivo o una comunicazione interattiva nell&#39;applicazione a pagina singola di AEM Sites{#embed-an-adaptive-form-or-interactive-communication-in-aem-sites-single-page-application}

## Panoramica {#overview}

AEM Forms consente agli sviluppatori di moduli di incorporare facilmente moduli adattivi e comunicazioni interattive in un’applicazione AEM Sites a pagina singola (SPA). Il modulo adattivo incorporato e la comunicazione interattiva sono completamente funzionanti e gli utenti possono compilare e inviare il modulo senza uscire dalla pagina. Consente all’utente di rimanere nel contesto di altri elementi della pagina web e di interagire contemporaneamente con il modulo adattivo o la comunicazione interattiva.

Nell’applicazione a pagina singola di AEM Sites, puoi aggiungere un modulo adattivo o una comunicazione interattiva utilizzando il componente [Contenitore di SPA AEM Forms](../../forms/using/embed-adaptive-form-aem-sites-spa.md#af-component)[.](../../forms/using/embed-adaptive-form-aem-sites-spa.md#af-component) È un componente AEM Forms per AEM Sites SPA che puoi aggiungere alla pagina Sites .

Per informazioni sull’incorporazione di un modulo adattivo in un AEM Sites non SPA, consultare [Incorporare un modulo adattivo o una comunicazione interattiva nella pagina AEM Sites](/help/forms/using/embed-adaptive-form-aem-sites.md).

## Prerequisiti {#prerequisites}

Per incorporare un modulo adattivo o una comunicazione interattiva in siti AEM SPA utilizzando il componente Contenitore SPA AEM Forms, accertati di aver installato:

* Kit di sviluppo Java SE 8 o successivo
* Apache Maven 3.3.1 o successivo
* istanza di authoring AEM
* [AEM Forms 6.4.2 add-on ](https://helpx.adobe.com/it/aem-forms/kb/aem-forms-releases.html) packageon author instance

## Installazione del componente contenitore AEM Forms SPA {#install-aem-forms-spa-container-component}

Esegui i seguenti passaggi per installare il componente Contenitore di SPA AEM Forms:

1. [Clona o scarica il componente AEM Forms per SPA](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa).
1. Installa il componente AEM Forms per SPA. Le istruzioni per installare il componente sono disponibili nel file [README.md](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa#aem-form-component) .

   Il componente include un [componente React campione](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa/react-component) che può essere utilizzato per integrare SPA componente contenitore con un progetto SPA basato su React.

1. [Clona o scarica un progetto](https://github.com/adobe/aem-sample-we-retail-journal) SPA basato su React.
1. Integra SPA componente contenitore con un progetto SPA basato su React utilizzando le istruzioni disponibili nel file [README.md](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa/react-component#aem-form-react-component-for-spa---editor) .

   Dopo aver installato il componente AEM Forms SPA Container e aver integrato il componente con un progetto SPA basato su React, è possibile incorporare moduli adattivi e comunicazioni interattive nella pagina AEM Sites.

## Incorporare un modulo adattivo o una comunicazione interattiva {#af-component}

Per incorporare un modulo adattivo o una comunicazione interattiva tramite AEM Forms per il componente Contenitore SPA:

1. Apri la pagina AEM siti in modalità di modifica in cui desideri incorporare un modulo adattivo o una comunicazione interattiva.
1. Inserisci il modulo **AEM per SPA** sulla pagina utilizzando una delle seguenti opzioni:

   * Tocca il contenitore di layout nella pagina Sites, tocca **+** e seleziona il modulo **AEM per SPA** componente.

   * Dal pannello del browser Componenti, trascina sulla pagina il componente **AEM Form for SPA** .
   * Cerca un modulo adattivo o una comunicazione interattiva nel browser Risorse e trascinalo nella pagina Sites. Incorpora il modulo in un AEM Forms per SPA contenitore di componenti.

   >[!NOTE]
   >
   >Il rendering di più componenti contenitore di AEM Forms SPA in una pagina non è supportato. È possibile avere più contenitori di SPA AEM Forms in una pagina ma viene eseguito il rendering di un solo componente alla volta. Assicurati che in una pagina sia visibile un solo componente per evitare discrepanze.

1. Tocca il componente Contenitore di SPA AEM Forms incorporato nella pagina Sites , quindi tocca ![settings_icon](assets/settings_icon.png) nella barra delle azioni. Viene visualizzata la finestra di dialogo **Modifica contenitore SPA AEM Forms** .
1. Nella finestra di dialogo **Modifica contenitore AEM Forms** , specifica quanto segue:

   * **Tipo di risorsa:** seleziona il tipo di risorsa da incorporare. Le opzioni disponibili sono **Modulo adattivo** e **Comunicazione interattiva**

   * **Percorso** risorsa: Sfoglia e seleziona il modulo adattivo o la comunicazione interattiva da incorporare. Il campo viene compilato automaticamente se viene inserito un modulo adattivo o una comunicazione interattiva utilizzando il browser Risorse.
   * **Canale**  (solo comunicazione interattiva): Seleziona il tipo di canale interattivo da incorporare. Le opzioni sono **Canale web** e **Canale di stampa**.

   * **Tema**: Seleziona un tema che definisce lo stile dei componenti del modulo adattivo o della comunicazione interattiva. Lo stile include proprietà di aspetto quali stile font, colore di sfondo, dimensioni e allineamento.

1. Tocca ![done_icon](assets/done_icon.png) per salvare le impostazioni. Il modulo adattivo o la comunicazione interattiva è ora incorporato nella pagina .

## Pubblicare moduli adattivi incorporati e comunicazioni interattive {#publish-embedded-adaptive-form-and-interactive-communication}

Considera i seguenti scenari per la pubblicazione di una risorsa incorporata (modulo adattivo o comunicazione interattiva) nella pagina AEM Sites:

* Se pubblichi la pagina AEM Sites per la prima volta e include un modulo adattivo incorporato o una comunicazione interattiva, pubblica la pagina Sites e la risorsa incorporata.
* Se hai modificato solo il modulo adattivo incorporato o la comunicazione interattiva in una pagina Sites pubblicata, pubblica la risorsa originale e le modifiche si riflettono nella pagina Sites pubblicata. La pagina Sites pubblicata include un riferimento alla risorsa e non richiede la ripubblicazione della pagina.
* Se hai modificato la pagina Sites e il modulo adattivo incorporato o la comunicazione interattiva, ripubblica la pagina Sites e la risorsa incorporata.

## Modificare il modulo adattivo incorporato e la comunicazione interattiva {#modify-embedded-adaptive-form-and-interactive-communication}

AEM pagina Sites conserva un riferimento al modulo adattivo e alla comunicazione interattiva nel contenitore AEM Forms. Pertanto, tutte le configurazioni e le proprietà, come il tema, gli stili e l’azione di invio, configurate nel modulo adattivo originale e nella comunicazione interattiva, vengono mantenute nel modulo adattivo incorporato e nella comunicazione interattiva.

Per modificare qualsiasi configurazione o proprietà del modulo adattivo incorporato e della comunicazione interattiva, eseguire una delle operazioni seguenti.

* Apri il modulo originale in moduli adattivi o Comunicazione interattiva nei rispettivi editor e modificalo.
* Tocca il modulo adattivo o la comunicazione interattiva dalla pagina Sites in modalità di modifica, quindi tocca **Modifica in una nuova finestra**. Il modulo originale viene aperto in modalità di modifica.

## Considerazioni e best practice {#considerations-and-best-practices}

Quando incorpori moduli adattivi nelle pagine dei siti AEM tenere a mente quanto segue:

* Le intestazioni e i piè di pagina nel modulo originale non sono inclusi nel modulo incorporato.
* Le bozze degli utenti e gli invii dei moduli incorporati sono supportati e visibili nelle schede Bozze e Inviate Forms sul portale dei moduli.
* L’azione di invio configurata sul modulo originale viene mantenuta nel modulo incorporato.
* Il targeting delle esperienze e i test A/B configurati sul modulo originale non funzionano nel modulo incorporato. Tuttavia, puoi utilizzare il targeting delle esperienze nella pagina Sites per presentare moduli diversi basati sui profili utente.
* Se Adobe Analytics è stato configurato per il modulo originale, i dati analitici del modulo incorporato vengono acquisiti in Adobe Analytics. Tuttavia, non è disponibile nel rapporto di analisi dei moduli.

