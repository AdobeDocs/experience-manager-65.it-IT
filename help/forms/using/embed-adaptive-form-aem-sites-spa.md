---
title: Incorporare un modulo adattivo o una comunicazione interattiva in  applicazione AEM Sites a pagina singola
seo-title: Incorporazione di moduli adattivi o comunicazioni interattive  pagine AEM Sites
description: Incorporare moduli adattivi o comunicazioni interattive  pagine AEM Sites. Gli utenti possono compilare e inviare i moduli senza uscire dalla pagina Siti.
seo-description: È possibile incorporare moduli adattivi o comunicazioni interattive  pagine AEM Sites. Gli utenti possono compilare e inviare i moduli senza uscire dalla pagina Siti.
uuid: 4c75494e-e9d2-43b9-bbae-562e0eda8abb
topic-tags: author, interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a74ed6c1-3006-4baf-bd77-ad4045e23c22
docset: aem65
translation-type: tm+mt
source-git-commit: 46f2ae565fe4a8cfea49572eb87a489cb5d9ebd7
workflow-type: tm+mt
source-wordcount: '1121'
ht-degree: 0%

---


# Incorporare un modulo adattivo o una comunicazione interattiva in  applicazione AEM Sites a pagina singola{#embed-an-adaptive-form-or-interactive-communication-in-aem-sites-single-page-application}

## Panoramica {#overview}

 AEM Forms consente agli sviluppatori di moduli di incorporare facilmente moduli adattivi e comunicazioni interattive in un&#39;applicazione  pagina singola (SPA) AEM Sites. Il modulo adattivo incorporato e la comunicazione interattiva sono completamente funzionanti e gli utenti possono compilare e inviare il modulo senza uscire dalla pagina. Consente agli utenti di restare nel contesto di altri elementi della pagina Web e di interagire contemporaneamente con il modulo adattivo o la comunicazione interattiva.

 applicazione AEM Sites per pagina singola, è possibile aggiungere un modulo adattivo o una comunicazione interattiva utilizzando il componente [ Contenitore SPA AEM Forms](../../forms/using/embed-adaptive-form-aem-sites-spa.md#af-component)[.](../../forms/using/embed-adaptive-form-aem-sites-spa.md#af-component) È un componente AEM Forms  per  AEM Sites SPA che potete aggiungere alla pagina Siti.

Per informazioni sull&#39;incorporamento di un modulo adattivo in un AEM Sites  non SPA, vedere [Incorporare un modulo adattivo o una comunicazione interattiva in  pagina AEM Sites](/help/forms/using/embed-adaptive-form-aem-sites.md).

## Prerequisiti {#prerequisites}

Per incorporare un modulo adattivo o una comunicazione interattiva in un sito AEM SPA utilizzando il componente  AEM Forms SPA Container, accertatevi di aver installato:

* Java SE Development Kit 8 o successivo
* Apache Maven 3.3.1 o successivo
* istanza di AEM
* [ pacchetto aggiuntivo AEM Forms 6.4.2 ](https://helpx.adobe.com/it/aem-forms/kb/aem-forms-releases.html) per l’istanza di creazione

## Installazione  componente contenitore AEM Forms SPA {#install-aem-forms-spa-container-component}

Effettuate i seguenti passaggi per installare il componente  AEM Forms SPA Container:

1. [Clona o scarica il componente AEM Forms  per SPA](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa).
1. Installate il componente  AEM Forms per SPA. Le istruzioni per installare il componente sono disponibili nel file [README.md](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa#aem-form-component).

   Il componente include un [componente React di esempio](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa/react-component) che può essere utilizzato per integrare SPA componente contenitore con un progetto SPA basato su React.

1. [Clona o scarica un progetto](https://github.com/adobe/aem-sample-we-retail-journal) SPA basato su React.
1. Integrare SPA componente contenitore con un progetto SPA basato su React utilizzando le istruzioni disponibili nel file [README.md](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa/react-component#aem-form-react-component-for-spa---editor).

   Dopo aver installato  componente AEM Forms SPA Container e integrato il componente con un progetto SPA basato su React, è possibile incorporare moduli adattivi e comunicazioni interattive nella pagina  AEM Sites.

## Incorpora un modulo adattivo o una comunicazione interattiva {#af-component}

Per incorporare un modulo adattivo o una comunicazione interattiva utilizzando  AEM Forms per SPA componente Contenitore:

1. Aprire la pagina AEM siti, in modalità di modifica, in cui si desidera incorporare un modulo adattivo o una comunicazione interattiva.
1. Inserite il componente **AEM Form per SPA** nella pagina utilizzando una delle seguenti opzioni:

   * Toccate il Contenitore di layout nella pagina Siti, toccate **+** e selezionate il componente **AEM Modulo per SPA**.

   * Dal pannello del browser Componenti, trascinare il componente **AEM Modulo per SPA** sulla pagina.
   * Cercate un modulo adattivo o una comunicazione interattiva nel browser Risorse e trascinatelo nella pagina Siti. Incorpora il modulo in un AEM Forms  per SPA contenitore di componenti.

   >[!NOTE]
   >
   >Il rendering di più componenti AEM Forms SPA Container  pagina non è supportato. Potete avere più  AEM Forms SPA Container su una pagina, ma viene eseguito il rendering di un solo componente alla volta. Per evitare discrepanze, accertatevi che sulla pagina sia visibile un solo componente.

1. Toccate il componente incorporato  AEM Forms SPA Container nella pagina dei siti, quindi toccate ![settings_icon](assets/settings_icon.png) nella barra delle azioni. Viene visualizzata la finestra di dialogo **Edit  AEM Forms SPA Container**.
1. Nella finestra di dialogo **Modifica  contenitore AEM Forms**, specificate quanto segue:

   * **Tipo risorsa:** selezionate il tipo di risorsa da incorporare. Le opzioni sono **Modulo adattivo** e **Comunicazione interattiva**

   * **Percorso** risorsa: Individuate e selezionate il modulo adattivo o la comunicazione interattiva da incorporare. Il campo viene popolato automaticamente se viene inserito un modulo adattivo o una comunicazione interattiva tramite il browser Risorse.
   * **Canale**  (Solo Comunicazione Interattiva): Selezionate il tipo di canale interattivo da incorporare. Le opzioni sono **Canale Web** e **Canale di stampa**.

   * **Tema**: Selezionate un tema che definisca lo stile dei componenti del modulo adattivo o della comunicazione interattiva. Lo stile include proprietà di aspetto quali lo stile del font, il colore di sfondo, le dimensioni e l&#39;allineamento.

1. Toccate ![done_icon](assets/done_icon.png) per salvare le impostazioni. Il modulo adattivo o la comunicazione interattiva ora è incorporato nella pagina.

## Pubblicare moduli adattivi incorporati e comunicazioni interattive {#publish-embedded-adaptive-form-and-interactive-communication}

Considerate i seguenti scenari per pubblicare una risorsa incorporata (modulo adattivo o comunicazione interattiva)  pagina AEM Sites:

* Se pubblicate per la prima volta la pagina AEM Sites  e include un modulo adattivo incorporato o una comunicazione interattiva, pubblicate la pagina Siti e la risorsa incorporata.
* Se avete modificato solo il modulo adattivo incorporato o la comunicazione interattiva in una pagina Siti pubblicati, pubblicate la risorsa originale e le modifiche si riflettono nella pagina Siti pubblicati. La pagina Siti pubblicati include un riferimento alla risorsa e non richiede la ripubblicazione della pagina.
* Se avete modificato la pagina Siti e il modulo adattivo incorporato o la comunicazione interattiva, ripubblicate la pagina Siti e la risorsa incorporata.

## Modifica del modulo adattivo incorporato e comunicazione interattiva {#modify-embedded-adaptive-form-and-interactive-communication}

AEM pagina dei siti contiene un riferimento al modulo adattivo e alla comunicazione interattiva nel  AEM Forms Container. Pertanto, tutte le configurazioni e proprietà, come il tema, gli stili e l&#39;azione Invia, configurate nel modulo adattivo originale e nella comunicazione interattiva vengono mantenute nel modulo adattivo incorporato e nella comunicazione interattiva.

Per modificare qualsiasi configurazione o proprietà del modulo adattivo incorporato e della comunicazione interattiva, effettuare una delle seguenti operazioni.

* Aprire il modulo originale nei moduli adattivi o nelle comunicazioni interattive nei rispettivi editor e modificarlo.
* Toccate il modulo adattivo o la comunicazione interattiva dalla pagina Siti in modalità di modifica, quindi toccate **Modifica in una nuova finestra**. Il modulo originale viene aperto in modalità di modifica.

## Considerazioni e best practice {#considerations-and-best-practices}

Quando si incorporano moduli adattivi nelle AEM pagine dei siti, tenere presente quanto segue:

* L&#39;intestazione e il piè di pagina del modulo originale non sono inclusi nel modulo incorporato.
* Le bozze degli utenti e gli invii dei moduli incorporati sono supportati e visibili nelle schede Bozze e Forms inviate nel portale dei moduli.
* L&#39;azione di invio configurata sul modulo originale viene mantenuta nel modulo incorporato.
* Il targeting delle esperienze e i test A/B configurati sul modulo originale non funzionano nel modulo incorporato. Tuttavia, potete utilizzare il targeting delle esperienze nella pagina Siti per presentare moduli diversi basati sui profili utente.
* Se  Adobe Analytics è stato configurato per il modulo originale, i dati di analisi del modulo incorporato vengono acquisiti in  Adobe Analytics. Tuttavia, non è disponibile nel report di analisi dei moduli.

