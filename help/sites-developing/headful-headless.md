---
title: Headful e headless in AEM
description: È possibile implementare i progetti AEM in un modello headful e headless, ma la scelta non è binaria. AEM offre la flessibilità di sfruttare i vantaggi di entrambi i modelli in un unico progetto.
exl-id: c9597c78-be05-42ff-84fe-f7451119e83d
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments,GraphQL,Persisted Queries,Developing
role: Admin,Architect,Data Architect,Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '1023'
ht-degree: 88%

---

# Headful e Headless in AEM {#headful-headless}

I progetti di Adobe Experience Manager possono essere implementati sia in modelli headful che headless, ma la scelta non è binaria. AEM offre la flessibilità di sfruttare i vantaggi di entrambi i modelli in un unico progetto. Questo documento fornisce una panoramica dei diversi modelli e descrive i livelli di integrazione dell’SPA.

## Panoramica {#overview}

AEM offre potenti strumenti per gestire sia la creazione dei contenuti che la loro distribuzione in un’unica piattaforma. Si tratta di un modello “headful” tradizionale di gestione dei contenuti, in cui le persone che si occupano di creare e sviluppare i contenuti lavorano sulla stessa piattaforma per distribuire le esperienze a chi consuma i contenuti.

AEM può essere utilizzato anche per gestire semplicemente i contenuti, consentendo la gestione della presentazione e della distribuzione dei contenuti tramite un’altra piattaforma. Si tratta del modello “headless” per la gestione dei contenuti, in cui chi si occupa di creare e sviluppare i contenuti lavora su piattaforme diverse per offrire esperienza a chi consuma i contenuti.

Ma questa non deve essere una scelta binaria. AEM offre una flessibilità senza precedenti, che consente di sfruttare i vantaggi di entrambi i modelli per il progetto.

![Modelli di implementazione di AEM](/help/sites-developing/headless/getting-started/assets/aem-implementation-models.png)

In un modello headful o full stack, il contenuto viene gestito nell’archivio AEM e i componenti AEM basati su Java, HTL e così via vengono utilizzati per eseguire il rendering del contenuto per l’esperienza utente. In questo modello, la creazione del contenuto, la sua presentazione, distribuzione e attribuzione di stile avvengono in AEM.

In un modello headless, il contenuto viene gestito nell’archivio AEM, ma distribuito tramite API come REST e GraphQL a un altro sistema per eseguire il rendering del contenuto per l’esperienza utente. In questo modello, il contenuto viene creato in AEM, ma la sua presentazione, distribuzione e attribuzione di stile avvengono su un’altra piattaforma.

Le applicazioni a pagina singola (SPA) sono spesso la destinazione del contenuto headless consegnato da AEM. Tuttavia, non è necessario che questi SPA siano completamente esterni all&#39;AEM. L’AEM consente di decidere in che misura l’SPA viene integrato nell’AEM. Prendiamo un esempio.

## Esempio di negozio web {#web-shop-example}

Diciamo che hai un negozio web esistente per la tua azienda come una SPA. Contiene tutti i dettagli e le immagini del prodotto. Introduci quindi AEM per potenziare le tue attività di marketing come siti promozionali, blog e contenuti delle campagne. Come si integrano i due? AEM consente una serie di opzioni:

* **Consenti il funzionamento indipendente dei sistemi.**
* **Fornisci al negozio web contenuti limitati da AEM tramite GraphQL.** I contenuti possono essere creati dagli autori in AEM, ma solo visualizzati tramite la SPA del negozio web.
* **Incorpora la SPA del negozio web in AEM.** I contenuti possono essere creati da autori e autrici in AEM e visualizzati in AEM nel contesto del negozio web, ma non manipolati.
* **Incorpora la SPA del negozio web in AEM e abilita punti modificabili.** I contenuti possono essere creati da autori e autrici in AEM e visualizzati in AEM nel contesto del negozio web e loro hanno una capacità limitata di manipolare i contenuti della SPA del negozio web all’interno di AEM.
* **Incorpora la SPA del negozio web in AEM e abilita intere aree per l’editing.** I contenuti possono essere creati da autori e autrici in AEM e visualizzati in AEM nel contesto del negozio web e loro hanno una capacità limitata di manipolare i contenuti della SPA del negozio web all’interno di AEM.

La sezione successiva esplora più dettagliatamente questi livelli di integrazione.

>[!NOTE]
>
>Naturalmente si potrebbe anche implementare nuovamente la SPA del negozio web come una SPA di AEM pienamente funzionante [utilizzando il framework dell’editor SPA AEM.](/help/sites-developing/spa-walkthrough.md) Se hai già un AEM e desideri creare un negozio online o un altro SPA, questo è il metodo consigliato, ma non rientra nell’ambito di questo documento.

## Livelli di integrazione SPA {#integration-levels}

L’integrazione SPA si sviluppa su quattro livelli in AEM.

* **Livello 0: nessuna integrazione**
   * SPA e AEM esistono separatamente e non si scambiano informazioni.
   * I contenuti vengono creati, gestiti e distribuiti in modo indipendente in due sistemi distinti.
* **Livello 1: integrazione dei frammenti di contenuto**
   * I [Frammenti di contenuto](/help/assets/content-fragments/content-fragments.md) vengono utilizzati in AEM per creare e gestire contenuti limitati per la SPA.
   * La SPA recupera questo contenuto tramite [API GraphQL](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md) di AEM.
   * Alcuni contenuti vengono gestiti in AEM e altri in un sistema esterno.
   * Il contenuto può essere visualizzato solo nella SPA.
* **Livello 2: incorpora la SPA in AEM**
   * I [Frammenti di contenuto](/help/assets/content-fragments/content-fragments.md) vengono utilizzati in AEM per creare e gestire il contenuto per la SPA.
   * La SPA recupera questo contenuto tramite [API GraphQL](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md) di AEM.
   * Alcuni contenuti vengono gestiti in AEM e altri in un sistema esterno.
   * Il contenuto può essere visualizzato nel contesto in AEM.
   * È possibile modificare contenuto limitato in AEM.
* **Livello 3: incorpora e abilita completamente SPA in AEM**
   * I [Frammenti di contenuto](/help/assets/content-fragments/content-fragments.md) vengono utilizzati in AEM per creare e gestire il contenuto per la SPA.
   * La SPA recupera questo contenuto tramite [API GraphQL](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md) di AEM.
   * Il contenuto può essere visualizzato nel contesto in AEM.
   * La maggior parte dei contenuti può essere modificata in AEM.

Il livello 1 è un esempio di implementazione headless tipica. Tuttavia, gli autori e le autrici di contenuti possono visualizzare i propri contenuti solo nel contesto all’interno della SPA. AEM è solo uno strumento di authoring.

Il vantaggio e la flessibilità di AEM si manifestano con i livelli 2 e 3 pur mantenendo i vantaggi di SPA. Gli autori e le autrici dei contenuti possono creare i propri contenuti in AEM, ma anche visualizzarli nel contesto all’interno di AEM. La SPA acquisisce la possibilità di essere creata in AEM, ma viene comunque consegnata come SPA.

## Implementazione dei livelli di integrazione {#implementing}

Sono disponibili diversi strumenti in AEM a seconda del livello di integrazione scelto. Ogni livello si basa sugli strumenti utilizzati nel precedente. L’elenco seguente riporta alle relative risorse.

* **Livello 1:** Frammenti di contenuto e il [framework di AEM headless](/help/sites-developing/headless/introduction.md) possono essere utilizzati per distribuire contenuto AEM alla SPA.
* **Livello 2:** in aggiunta al livello 1:
   * Il [componente RemotePage](/help/sites-developing/spa-remote-page.md) può essere utilizzato per incorporare la SPA esterna in AEM dove è possibile visualizzare il contenuto AEM contestuale.
   * Alcuni punti della SPA possono anche essere abilitati per [consentire modifiche limitate in AEM.](/help/sites-developing/spa-edit-external.md)
* **Livello 3:** in aggiunta al livello 2:
   * È possibile abilitare intere aree della SPA per consentire una modifica completa in AEM.
