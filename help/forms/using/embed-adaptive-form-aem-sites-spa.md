---
title: Incorporazione di un modulo adattivo o di una comunicazione interattiva in un'applicazione pagina singola AEM Sites
seo-title: Incorporare moduli adattivi o comunicazioni interattive nelle pagine dei AEM Sites
description: Incorporare moduli adattivi o comunicazioni interattive nelle pagine AEM Sites. Gli utenti possono compilare e inviare i moduli senza uscire dalla pagina Siti.
seo-description: È possibile incorporare moduli adattivi o comunicazioni interattive nelle pagine AEM Sites. Gli utenti possono compilare e inviare i moduli senza uscire dalla pagina Siti.
uuid: 4c75494e-e9d2-43b9-bbae-562e0eda8abb
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a74ed6c1-3006-4baf-bd77-ad4045e23c22
docset: aem65
translation-type: tm+mt
source-git-commit: bd70508b361ac8b62ebc0344538a18369a075f3e
workflow-type: tm+mt
source-wordcount: '1121'
ht-degree: 0%

---


# Incorporazione di un modulo adattivo o di una comunicazione interattiva in un&#39;applicazione pagina singola AEM Sites{#embed-an-adaptive-form-or-interactive-communication-in-aem-sites-single-page-application}

## Panoramica {#overview}

I AEM Forms consentono agli sviluppatori di moduli di incorporare facilmente moduli adattivi e comunicazioni interattive in un&#39;applicazione SPA (Single Page Application) AEM Sites. Il modulo adattivo incorporato e la comunicazione interattiva sono completamente funzionanti e gli utenti possono compilare e inviare il modulo senza uscire dalla pagina. Consente agli utenti di restare nel contesto di altri elementi della pagina Web e di interagire contemporaneamente con il modulo adattivo o la comunicazione interattiva.

Nell’applicazione AEM Sites pagina singola, è possibile aggiungere un modulo adattivo o una comunicazione interattiva utilizzando il componente [contenitore SPA](../../forms/using/embed-adaptive-form-aem-sites-spa.md#af-component)[AEM Forms.](../../forms/using/embed-adaptive-form-aem-sites-spa.md#af-component) È un componente AEM Forms per gli SPA AEM Sites che potete aggiungere alla pagina Siti.

Per informazioni sull&#39;incorporazione di un modulo adattivo in un AEM Sites non SPA, vedere [Incorporare un modulo adattivo o comunicare interattiva nella pagina](/help/forms/using/embed-adaptive-form-aem-sites.md)AEM Sites.

## Prerequisiti {#prerequisites}

Per incorporare un modulo adattivo o una comunicazione interattiva in un sito AEM SPA utilizzando il componente AEM Forms SPA Container, accertatevi di aver installato:

* Java SE Development Kit 8 o successivo
* Apache Maven 3.3.1 o successivo
* istanza di creazione AEM
* [Pacchetto](https://helpx.adobe.com/it/aem-forms/kb/aem-forms-releases.html) aggiuntivo AEM Forms 6.4.2 per l’istanza di creazione

## Installazione del componente Contenitore SPA AEM Forms {#install-aem-forms-spa-container-component}

Effettuate i seguenti passaggi per installare il componente AEM Forms SPA Container:

1. [Clona o scarica il componente AEM Forms per SPA](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa).
1. Installate il componente AEM Forms per SPA. Le istruzioni per installare il componente sono disponibili nel file [README.md](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa#aem-form-component) .

   Il componente include un [esempio di componente](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa/react-component) React che può essere utilizzato per integrare il componente contenitore SPA con un progetto SPA basato su React.

1. [Clona o scarica un progetto](https://github.com/adobe/aem-sample-we-retail-journal)SPA basato su React.
1. Integrare il componente contenitore SPA con un progetto SPA basato su React utilizzando le istruzioni disponibili nel file [README.md](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa/react-component#aem-form-react-component-for-spa---editor) .

   Dopo aver installato il componente AEM Forms SPA Container e integrato il componente con un progetto SPA basato su React, è possibile incorporare moduli adattivi e comunicazioni interattive nella pagina AEM Sites.

## Incorporare un modulo adattivo o una comunicazione interattiva {#af-component}

Per incorporare un modulo adattivo o una comunicazione interattiva utilizzando AEM Forms per il componente Contenitore SPA:

1. Aprite la pagina Siti AEM, in modalità di modifica, in cui desiderate incorporare un modulo adattivo o una comunicazione interattiva.
1. Inserite nella pagina il componente Modulo **AEM per SPA** utilizzando una delle seguenti opzioni:

   * Toccate il Contenitore di layout nella pagina Siti, toccate **+** e selezionate il componente Modulo **AEM per SPA** .

   * Dal pannello del browser Componenti, trascina sulla pagina il componente Modulo **AEM per SPA** .
   * Cercate un modulo adattivo o una comunicazione interattiva nel browser Risorse e trascinatelo nella pagina Siti. Incorpora il modulo in un AEM Forms per il contenitore di componenti SPA.

   >[!NOTE]
   >
   >Il rendering di più componenti SPA Container AEM Forms in una pagina non è supportato. Potete avere più AEM Forms SPA Container su una pagina, ma viene eseguito il rendering di un solo componente alla volta. Per evitare discrepanze, accertatevi che sulla pagina sia visibile un solo componente.

1. Toccate il componente AEM Forms SPA Container nella pagina dei siti, quindi toccate ![settings_icon](assets/settings_icon.png) sulla barra delle azioni. Viene visualizzata la finestra di dialogo **Edit AEM Forms SPA Container** .
1. Nella finestra di dialogo **Modifica contenitore** AEM Forms, specificate quanto segue:

   * **Tipo risorsa:** Selezionate il tipo di risorsa da incorporare. Le opzioni sono Modulo **** adattivo e Comunicazione **interattiva**

   * **Percorso** risorsa: Individuate e selezionate il modulo adattivo o la comunicazione interattiva da incorporare. Il campo viene popolato automaticamente se viene inserito un modulo adattivo o una comunicazione interattiva tramite il browser Risorse.
   * **Canale** (Solo Comunicazione Interattiva): Selezionate il tipo di canale interattivo da incorporare. Le opzioni sono Canale **** Web e Canale **** di stampa.

   * **Tema**: Selezionate un tema che definisca lo stile dei componenti del modulo adattivo o della comunicazione interattiva. Lo stile include proprietà di aspetto quali lo stile del font, il colore di sfondo, le dimensioni e l&#39;allineamento.

1. Toccate ![done_icon](assets/done_icon.png) per salvare le impostazioni. Il modulo adattivo o la comunicazione interattiva ora è incorporato nella pagina.

## Pubblicare un modulo adattivo incorporato e Comunicazione interattiva {#publish-embedded-adaptive-form-and-interactive-communication}

Considerate i seguenti scenari per pubblicare una risorsa incorporata (modulo adattivo o comunicazione interattiva) nella pagina AEM Sites:

* Se pubblicate la pagina AEM Sites per la prima volta e include un modulo adattivo incorporato o una comunicazione interattiva, pubblicate la pagina Siti e la risorsa incorporata.
* Se avete modificato solo il modulo adattivo incorporato o la comunicazione interattiva in una pagina Siti pubblicati, pubblicate la risorsa originale e le modifiche si riflettono nella pagina Siti pubblicati. La pagina Siti pubblicati include un riferimento alla risorsa e non richiede la ripubblicazione della pagina.
* Se avete modificato la pagina Siti e il modulo adattivo incorporato o la comunicazione interattiva, ripubblicate la pagina Siti e la risorsa incorporata.

## Modifica di moduli adattivi incorporati e comunicazione interattiva {#modify-embedded-adaptive-form-and-interactive-communication}

Nella pagina dei siti AEM viene mantenuto un riferimento al modulo adattivo e alla comunicazione interattiva nel contenitore AEM Forms. Pertanto, tutte le configurazioni e proprietà, come il tema, gli stili e l&#39;azione Invia, configurate nel modulo adattivo originale e nella comunicazione interattiva vengono mantenute nel modulo adattivo incorporato e nella comunicazione interattiva.

Per modificare qualsiasi configurazione o proprietà del modulo adattivo incorporato e della comunicazione interattiva, effettuare una delle seguenti operazioni.

* Aprire il modulo originale nei moduli adattivi o nelle comunicazioni interattive nei rispettivi editor e modificarlo.
* Toccate il modulo adattivo o la comunicazione interattiva dalla pagina Siti in modalità di modifica, quindi toccate **Modifica in una nuova finestra**. Il modulo originale viene aperto in modalità di modifica.

## Considerations and best practices {#considerations-and-best-practices}

Quando incorporate moduli adattivi nelle pagine dei siti AEM, tenete presente quanto segue:

* L&#39;intestazione e il piè di pagina del modulo originale non sono inclusi nel modulo incorporato.
* Le bozze degli utenti e gli invii dei moduli incorporati sono supportati e visibili nelle schede Bozze e Moduli inviati nel portale dei moduli.
* L&#39;azione di invio configurata sul modulo originale viene mantenuta nel modulo incorporato.
* Il targeting delle esperienze e i test A/B configurati sul modulo originale non funzionano nel modulo incorporato. Tuttavia, potete utilizzare il targeting delle esperienze nella pagina Siti per presentare moduli diversi basati sui profili utente.
* Se per il modulo originale è stato configurato Adobe  Analytics, i dati di analisi del modulo incorporato vengono acquisiti in Adobe  Analytics. Tuttavia, non è disponibile nel report di analisi dei moduli.

