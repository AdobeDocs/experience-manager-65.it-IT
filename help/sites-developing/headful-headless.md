---
title: Cefalea e senza testa in AEM
description: AEM progetti possono essere implementati in un modello headful e headless, ma la scelta non è binaria. AEM offre la flessibilità di sfruttare i vantaggi di entrambi i modelli in un unico progetto.
source-git-commit: cf7e9061bac9004c7efd2f045b4900e4a92d67e9
workflow-type: tm+mt
source-wordcount: '1011'
ht-degree: 0%

---

# Cefalea e senza testa in AEM {#headful-headless}

I progetti Adobe Experience Manager possono essere implementati sia in modelli headful che headless, ma la scelta non è binaria. AEM offre la flessibilità di sfruttare i vantaggi di entrambi i modelli in un unico progetto. Questo documento fornisce una panoramica dei diversi modelli e descrive i livelli di integrazione SPA.

## Panoramica {#overview}

AEM offre potenti strumenti per gestire sia la creazione dei contenuti che la loro distribuzione in un’unica piattaforma. Si tratta di un modello tradizionale di gestione dei contenuti, in cui autori e sviluppatori di contenuti lavorano sulla stessa piattaforma per distribuire le esperienze ai consumatori di contenuti.

AEM può essere utilizzato anche per gestire semplicemente i contenuti, consentendo la presentazione e la distribuzione dei contenuti da gestire tramite un’altra piattaforma. Si tratta del modello &quot;headless&quot; per la gestione dei contenuti, in cui autori e sviluppatori di contenuti lavorano su piattaforme diverse per offrire esperienza ai consumatori di contenuti.

Ma questa non deve essere una scelta binaria. AEM offre una flessibilità senza precedenti, che consente di sfruttare i vantaggi di entrambi i modelli per il progetto.

![Modelli di implementazione AEM](headless/assets/aem-implementation-models.png)

In un modello headful o full-stack, il contenuto viene gestito nell’archivio AEM e nei componenti AEM basati su Java, HTL, ecc. vengono utilizzati per eseguire il rendering del contenuto per l’esperienza utente. In questo modello, la creazione del contenuto, lo stile, la presentazione e la distribuzione avvengono in AEM.

In un modello headless, il contenuto viene gestito nell’archivio AEM, ma distribuito tramite API come REST e GraphQL a un altro sistema per eseguire il rendering del contenuto per l’esperienza utente. In questo modello, il contenuto viene creato in AEM, ma formattandolo, presentandolo e distribuendolo avviene su un’altra piattaforma.

Le applicazioni a pagina singola (SPA) sono spesso la destinazione del contenuto consegnato inavvertitamente da AEM. Tuttavia, questi SPA non devono essere del tutto esterni all&#39;AEM. AEM consente di decidere in che misura le SPA sono integrate in AEM. Prendiamo un esempio.

## Esempio di negozio web {#web-shop-example}

Diciamo che hai un negozio web esistente per la tua azienda come SPA. Contiene tutti i dettagli del prodotto e le immagini. Poi introduci AEM per potenziare le tue attività di marketing come siti promozionali, blog e contenuti delle campagne. Come si integrano i due? AEM consente una serie di opzioni:

* **Consentire il funzionamento indipendente dei sistemi.**
* **Fornisci al negozio web contenuti limitati da AEM tramite GraphQL.** I contenuti possono essere creati dagli autori in AEM, ma solo visualizzati tramite il SPA web shop.
* **Incorpora il web shop SPA in AEM.** I contenuti possono essere creati dagli autori in AEM e visualizzati in AEM nel contesto del web shop, ma non manipolati.
* **Incorpora il negozio web SPA in AEM e abilita punti modificabili.** I contenuti possono essere creati dagli autori in AEM e visualizzati in AEM nel contesto del web shop, e gli autori hanno una capacità limitata di manipolare i contenuti del web shop SPA all&#39;interno di AEM.
* **Incorpora il negozio di webs SPA in AEM e abilita intere aree per l&#39;editing.** I contenuti possono essere creati dagli autori in AEM e visualizzati in AEM nel contesto del web shop, e gli autori hanno una capacità limitata di manipolare i contenuti del web shop SPA all&#39;interno di AEM.

La sezione successiva esplora più dettagliatamente questi livelli di integrazione.

>[!NOTE]
>
>Naturalmente si potrebbe anche riimplementare il negozio web SPA come un AEM pienamente funzionante SPA [utilizzando il framework di AEM SPA Editor.](/help/sites-developing/spa-walkthrough.md) Se hai già AEM e desideri creare un nuovo web shop o un altro SPA, questo è il metodo consigliato, ma non rientra nell&#39;ambito di questo documento.

## Livelli di integrazione SPA {#integration-levels}

L&#39;integrazione SPA si sviluppa su uno spettro di quattro livelli in AEM.

* **Livello 0: Nessuna integrazione**
   * I SPA e i AEM esistono separatamente e non si scambiano informazioni.
   * I contenuti vengono creati, gestiti e distribuiti in modo indipendente in due sistemi distinti.
* **Livello 1: Integrazione dei frammenti di contenuto**
   * [Frammenti di contenuto](/help/assets/content-fragments/content-fragments.md) vengono utilizzati in AEM per creare e gestire contenuti limitati per il SPA.
   * Il SPA recupera questo contenuto tramite AEM [API GraphQL.](/help/assets/content-fragments/graphql-api-content-fragments.md)
   * Alcuni contenuti vengono gestiti in AEM e altri in un sistema esterno.
   * Il contenuto può essere visualizzato solo nel SPA.
* **Livello 2: Incorpora il SPA in AEM**
   * [Frammenti di contenuto](/help/assets/content-fragments/content-fragments.md) vengono utilizzati in AEM per creare e gestire il contenuto per il SPA.
   * Il SPA recupera questo contenuto tramite AEM [API GraphQL.](/help/assets/content-fragments/graphql-api-content-fragments.md)
   * Alcuni contenuti vengono gestiti in AEM e altri in un sistema esterno.
   * Il contenuto può essere visualizzato nel contesto in AEM.
   * È possibile modificare contenuto limitato in AEM.
* **Livello 3: Incorpora e abilita completamente SPA in AEM**
   * [Frammenti di contenuto](/help/assets/content-fragments/content-fragments.md) vengono utilizzati in AEM per creare e gestire il contenuto per il SPA.
   * Il SPA recupera questo contenuto tramite AEM [API GraphQL.](/help/assets/content-fragments/graphql-api-content-fragments.md)
   * Il contenuto può essere visualizzato nel contesto in AEM.
   * La maggior parte dei contenuti può essere modificata in AEM.

Il livello 1 è un esempio di implementazione headless tipica. Tuttavia, gli autori di contenuti possono visualizzare i propri contenuti solo nel contesto all’interno del SPA. AEM è solo uno strumento di authoring.

Il vantaggio e la flessibilità di AEM si manifestano con i livelli 2 e 3 pur mantenendo i vantaggi di SPA. Gli autori dei contenuti possono creare i propri contenuti in AEM, ma anche visualizzarli nel contesto all’interno di AEM. Il SPA ha la possibilità di essere creato in AEM, ma viene comunque consegnato come SPA.

## Implementazione dei livelli di integrazione {#implementing}

Sono disponibili diversi strumenti in AEM a seconda del livello di integrazione scelto. Ogni livello si basa sugli strumenti utilizzati nel precedente. Nell’elenco seguente sono riportati i collegamenti alle relative risorse.

* **Livello 1:** Frammenti di contenuto e [AEM quadro headless](/help/sites-developing/headless/introduction.md) può essere utilizzato per distribuire AEM contenuto al SPA.
* **Livello 2:** Oltre al livello 1:
   * [Componente RemotePage](/help/sites-developing/spa-remote-page.md) può essere utilizzato per incorporare il SPA esterno in AEM dove è possibile visualizzare AEM contenuto contestuale.
   * Alcuni punti della SPA possono anche essere abilitati a [consente modifiche limitate in AEM.](/help/sites-developing/spa-edit-external.md)
* **Livello 3:** Oltre al livello 2:
   * È possibile abilitare intere aree del SPA per consentire una modifica completa in AEM.
