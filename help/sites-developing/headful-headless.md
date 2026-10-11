---
title: Headful e headless in AEM
description: È possibile implementare i progetti AEM in un modello headful e headless, ma la scelta non è binaria. AEM offre la flessibilità di sfruttare i vantaggi di entrambi i modelli in un unico progetto.
exl-id: c9597c78-be05-42ff-84fe-f7451119e83d
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments,GraphQL,Persisted Queries,Developing
role: Admin,Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: bfd4bc52-c397-5127-8f86-8953ba9fc0a3
    internal-label: Headless
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
  - id: a642c50e-80eb-4fc1-a5d2-f3762d1f841d
    internal-label: Administration
  - id: d429a63e-ade4-4117-b04e-9b996d1c94ef
    internal-label: Integrations
  - id: c124fa01-25c5-42ec-adf6-21d1c114058b
    internal-label: Developer tools
subfeature_v2:
  - id: e9db7c79-8f65-4281-a439-c9049296d903
    internal-label: Content Fragments
  - id: a02b73a7-bdfc-4225-bdfd-69f7891ab55e
    internal-label: GraphQL
  - id: d781bc8f-52af-43f6-84d0-b73e59a130d5
    internal-label: Persisted queries
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '1031'
ht-degree: 71%
---
# Headful e Headless in AEM {#headful-headless}

I progetti di Adobe Experience Manager possono essere implementati sia in modelli headful che headless, ma la scelta non è binaria. AEM offre la flessibilità di sfruttare i vantaggi di entrambi i modelli in un unico progetto. Questo documento fornisce una panoramica dei diversi modelli e descrive i livelli di integrazione delle applicazioni a pagina singola.

## Panoramica {#overview}

AEM offre potenti strumenti per gestire sia la creazione dei contenuti che la loro distribuzione in un’unica piattaforma. Si tratta di un modello “headful” tradizionale di gestione dei contenuti, in cui le persone che si occupano di creare e sviluppare i contenuti lavorano sulla stessa piattaforma per distribuire le esperienze a chi consuma i contenuti.

AEM può essere utilizzato anche per gestire semplicemente i contenuti, consentendo la gestione della presentazione e della distribuzione dei contenuti tramite un’altra piattaforma. Si tratta del modello “headless” per la gestione dei contenuti, in cui chi si occupa di creare e sviluppare i contenuti lavora su piattaforme diverse per offrire esperienza a chi consuma i contenuti.

Ma questa non deve essere una scelta binaria. AEM offre una flessibilità senza precedenti, che consente di sfruttare i vantaggi di entrambi i modelli per il progetto.

![Modelli di implementazione di AEM](/help/sites-developing/headless/getting-started/assets/aem-implementation-models.png)

In un modello headful o full stack, il contenuto viene gestito nell’archivio AEM e i componenti AEM basati su Java, HTL e così via vengono utilizzati per eseguire il rendering del contenuto per l’esperienza utente. In questo modello, la creazione del contenuto, la sua presentazione, distribuzione e attribuzione di stile avvengono in AEM.

In un modello headless, il contenuto viene gestito nell’archivio AEM, ma distribuito tramite API come REST e GraphQL a un altro sistema per eseguire il rendering del contenuto per l’esperienza utente. In questo modello, il contenuto viene creato in AEM, ma la sua presentazione, distribuzione e attribuzione di stile avvengono su un’altra piattaforma.

Le applicazioni a pagina singola (SPA) sono spesso la destinazione del contenuto headless consegnato da AEM. Tuttavia, queste applicazioni a pagina singola non devono essere completamente esterne ad AEM. AEM consente di decidere in che misura le applicazioni a pagina singola vengono integrate in AEM. Prendiamo un esempio.

## Esempio di negozio web {#web-shop-example}

Diciamo che hai un negozio web esistente per la tua azienda come una SPA. Contiene tutti i dettagli e le immagini del prodotto. Introduci quindi AEM per potenziare le tue attività di marketing come siti promozionali, blog e contenuti delle campagne. Come si integrano i due? AEM consente una serie di opzioni:

* **Consenti il funzionamento indipendente dei sistemi.**
* **Fornisci al Web shop contenuti limitati provenienti da AEM tramite GraphQL.** I contenuti possono essere creati dagli autori in AEM, ma sono visibili solo tramite l’applicazione a pagina singola del web shop.
* **Incorpora l&#39;applicazione a pagina singola del Web shop in AEM.** I contenuti possono essere creati dagli autori in AEM e visualizzati in AEM nel contesto del web shop, ma non manipolati.
* **Incorpora l&#39;applicazione a pagina singola del Web shop in AEM e abilita i punti modificabili.** I contenuti possono essere creati dagli autori in AEM e visualizzati in AEM nel contesto del web shop; inoltre, gli autori hanno una capacità limitata di manipolare il contenuto dell’applicazione a pagina singola del web shop all’interno di AEM.
* **Incorpora l&#39;applicazione a pagina singola di webs shop in AEM e abilita intere zone per la modifica.** I contenuti possono essere creati dagli autori in AEM e visualizzati in AEM nel contesto del web shop; inoltre, gli autori hanno una capacità limitata di manipolare il contenuto dell’applicazione a pagina singola del web shop all’interno di AEM.

La sezione successiva esplora più dettagliatamente questi livelli di integrazione.

>[!NOTE]
>
>Naturalmente puoi anche reimplementare l’applicazione a pagina singola del web shop come applicazione a pagina singola di AEM [completamente funzionante utilizzando il framework dell’editor di applicazioni a pagina singola di AEM.](/help/sites-developing/spa-walkthrough.md) Se disponi già di AEM e desideri creare un Web shop o un’altra applicazione a pagina singola, questo è il metodo consigliato, ma non è incluso nell’ambito di questo documento.

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
