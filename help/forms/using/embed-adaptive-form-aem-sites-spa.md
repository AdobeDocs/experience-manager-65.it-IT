---
title: Incorporare un modulo adattivo o una comunicazione interattiva nell’applicazione a pagina singola AEM Sites
seo-title: Embed adaptive forms or Interactive Communications in AEM Sites pages
description: Incorporare moduli adattivi o comunicazioni interattive nelle pagine AEM Sites. Gli utenti possono compilare e inviare i moduli senza uscire dalla pagina Sites.
seo-description: You can embed adaptive forms or Interactive Communication in AEM Sites pages. Users can fill and submit forms without leaving the Sites page.
uuid: 4c75494e-e9d2-43b9-bbae-562e0eda8abb
topic-tags: author, interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a74ed6c1-3006-4baf-bd77-ad4045e23c22
docset: aem65
feature: Adaptive Forms
exl-id: b549f176-409a-4d81-8c2b-73d0dd0c6649
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1088'
ht-degree: 0%

---

# Incorporare un modulo adattivo o una comunicazione interattiva nell’applicazione a pagina singola AEM Sites{#embed-an-adaptive-form-or-interactive-communication-in-aem-sites-single-page-application}

## Panoramica {#overview}

AEM Forms consente agli sviluppatori di moduli di incorporare facilmente moduli adattivi e comunicazioni interattive in un’applicazione AEM Sites a pagina singola (SPA). Il modulo adattivo incorporato e la comunicazione interattiva sono completamente funzionanti e gli utenti possono compilare e inviare il modulo senza uscire dalla pagina. Consente all’utente di rimanere nel contesto di altri elementi della pagina web e di interagire contemporaneamente con il modulo adattivo o la comunicazione interattiva.

Nell’applicazione a pagina singola di AEM Sites, è possibile aggiungere un modulo adattivo o una comunicazione interattiva utilizzando la [Componente contenitore SPA AEM Forms](../../forms/using/embed-adaptive-form-aem-sites-spa.md#af-component)[.](../../forms/using/embed-adaptive-form-aem-sites-spa.md#af-component) È un componente AEM Forms per AEM Sites SPA che puoi aggiungere alla pagina Sites .

Per informazioni sull’incorporazione di un modulo adattivo in un AEM Sites non SPA, consulta [Incorporare un modulo adattivo o una comunicazione interattiva nella pagina AEM Sites](/help/forms/using/embed-adaptive-form-aem-sites.md).

## Prerequisiti {#prerequisites}

Per incorporare un modulo adattivo o una comunicazione interattiva in siti AEM SPA utilizzando il componente Contenitore SPA AEM Forms, accertati di aver installato:

* Kit di sviluppo Java SE 8 o successivo
* Apache Maven 3.3.1 o successivo
* istanza di authoring AEM
* [Pacchetto aggiuntivo di AEM Forms 6.4.2](https://helpx.adobe.com/it/aem-forms/kb/aem-forms-releases.html) sull’istanza dell’autore

## Installare il componente Contenitore di AEM Forms SPA {#install-aem-forms-spa-container-component}

Esegui i seguenti passaggi per installare il componente Contenitore di SPA AEM Forms:

1. [Clona o scarica il componente AEM Forms per SPA](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa).
1. Installa il componente AEM Forms per SPA. Le istruzioni per installare il componente sono disponibili nella sezione [README.md](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa#aem-form-component) file.

   Il componente include un [componente React campione](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa/react-component) che può essere utilizzato per integrare SPA componente contenitore con un progetto SPA basato su React.

1. [Clona o scarica un progetto SPA basato su React](https://github.com/adobe/aem-sample-we-retail-journal).
1. Integra SPA componente contenitore con un progetto SPA basato su React utilizzando le istruzioni disponibili in [README.md](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa/react-component#aem-form-react-component-for-spa---editor) file.

   Dopo aver installato il componente AEM Forms SPA Container e aver integrato il componente con un progetto SPA basato su React, è possibile incorporare moduli adattivi e comunicazioni interattive nella pagina AEM Sites.

## Incorporare un modulo adattivo o una comunicazione interattiva {#af-component}

Per incorporare un modulo adattivo o una comunicazione interattiva tramite AEM Forms per il componente Contenitore SPA:

1. Apri la pagina AEM siti in modalità di modifica in cui desideri incorporare un modulo adattivo o una comunicazione interattiva.
1. Inserisci **AEM modulo per SPA** nella pagina utilizzando una delle seguenti opzioni:

   * Tocca il contenitore di layout nella pagina Sites e tocca **+** e seleziona la **AEM modulo per SPA** componente.

   * Dal pannello del browser Componenti, trascina **AEM modulo per SPA** nella pagina.
   * Cerca un modulo adattivo o una comunicazione interattiva nel browser Risorse e trascinalo nella pagina Sites. Incorpora il modulo in un AEM Forms per SPA contenitore di componenti.

   >[!NOTE]
   >
   >Il rendering di più componenti contenitore di AEM Forms SPA in una pagina non è supportato. È possibile avere più contenitori di SPA AEM Forms in una pagina ma viene eseguito il rendering di un solo componente alla volta. Assicurati che in una pagina sia visibile un solo componente per evitare discrepanze.

1. Tocca il componente Contenitore di SPA AEM Forms incorporato nella pagina Sites , quindi tocca ![settings_icon](assets/settings_icon.png) sulla barra delle azioni. La **Modifica contenitore SPA AEM Forms** viene visualizzata la finestra di dialogo .
1. In **Modifica contenitore AEM Forms** specifica quanto segue:

   * **Tipo risorsa:** Seleziona il tipo di risorsa da incorporare. Le opzioni sono **Modulo adattivo** e **Comunicazione interattiva**

   * **Percorso risorsa**: Sfoglia e seleziona il modulo adattivo o la comunicazione interattiva da incorporare. Il campo viene compilato automaticamente se viene inserito un modulo adattivo o una comunicazione interattiva utilizzando il browser Risorse.
   * **Canale** (Solo Comunicazione Interattiva): Seleziona il tipo di canale interattivo da incorporare. Le opzioni sono **Canale web** e **Canale di stampa**.

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
