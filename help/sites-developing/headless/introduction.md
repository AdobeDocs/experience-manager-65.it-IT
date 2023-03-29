---
title: Sviluppo headless per siti AEM 6.5
description: Scopri come le potenti funzionalità headless di AEM 6.5 come Modelli di contenuto, Frammenti di contenuto e API GraphQL collaborano per consentire di gestire le esperienze a livello centrale e distribuirle tra i vari canali.
exl-id: b6598bcf-b2ce-403a-87cf-6895fec8a91b
source-git-commit: ac70fb534a95c9eee6f8340d9b8720a607b9f79f
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 38%

---

# Sviluppo headless per siti AEM 6.5 {#headless-development}

Scopri come le potenti funzionalità headless di AEM 6.5 come Modelli di contenuto, Frammenti di contenuto e API GraphQL collaborano per consentire di gestire le esperienze a livello centrale e distribuirle tra i vari canali.

## Panoramica {#overview}

L’implementazione headless sta diventando sempre più importante per la distribuzione di esperienze al pubblico, ovunque si trovi e indipendentemente dal canale utilizzato.

L’implementazione headless ignora la gestione di pagine e componenti come avviene nelle soluzioni complete e ibride e si concentra sulla creazione di frammenti di contenuto riutilizzabili e indipendenti dal canale, che possono essere distribuiti in modalità cross-channel. Si tratta di un modello di sviluppo moderno e dinamico per l’implementazione di esperienze web.

![Modelli di implementazione di AEM](/help/sites-developing/headless/getting-started/assets/aem-implementation-models.png)

## Confronto tra headful e headless {#headful-headless}

Questo documento si concentra sul modello di implementazione senza testa di AEM completo. Ma la scelta tra headful e headless non deve essere per forza binaria in AEM. Le funzioni headless consentono di gestire e distribuire i contenuti a diversi endpoint, consentendo agli autori di contenuti di modificare applicazioni a pagina singola. Tutto questo direttametne in AEM.

>[!TIP]
>
>Per saperne di più, consulta il documento [Headful e headless in AEM](/help/sites-developing/headful-headless.md).

## AEM 6.5 e headless {#aem-headless}

AEM 6.5 è uno strumento flessibile per il modello di implementazione headless offrendo tre potenti servizi:

1. Modelli di contenuto
   * I modelli di contenuto sono rappresentazioni strutturate di contenuti.
   * Questi sono definiti dagli architetti delle informazioni nell’editor AEM modello di frammento di contenuto .
   * I modelli di contenuto fungono da base per i frammenti di contenuto.
1. Frammenti di contenuto
   * I frammenti di contenuto sono istanze di modelli di contenuto.
   * Vengono create dagli autori di contenuti tramite l’editor Frammento di contenuto AEM.
   * Vengono memorizzati in AEM Assets e gestiti nell’interfaccia utente di amministrazione delle risorse.
1. API per la distribuzione dei contenuti
   * L’API GraphQL di AEM supporta la distribuzione di frammenti di contenuto.
   * L’API REST di AEM Assets supporta le operazioni CRUD relative ai frammenti di contenuto.
   * La consegna diretta dei contenuti è possibile anche con [Esportazione JSON del componente core Frammento di contenuto.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=it)

## Primi passi con AEM headless {#first-steps}

Sono disponibili numerose risorse per iniziare a utilizzare AEM funzionalità headless. Sono destinati a diversi casi d’uso, ma tutti offrono una panoramica solida delle AEM funzioni headless.

| Risorsa | Descrizione | Tipo | Pubblico | Tempo stimato |
|---|---|---|---|---|
| [Percorso per sviluppatori headless](/help/journey-headless/developer/overview.md) | **Per gli utenti nuovi a AEM e headless** tecnologie, inizia qui per un&#39;introduzione completa a AEM e le sue caratteristiche headless dalla teoria dei headless attraverso il vivere con il tuo primo progetto headless. | Guida | Sviluppatori **senza esperienza di AEM e headless** | 1 ora |
| [Guida introduttiva di Headless](/help/sites-developing/headless/getting-started/introduction.md) | **Se sei un utente esperto di AEM** che necessita di un riepilogo delle principali funzioni headless di AEM, consulta questa breve panoramica. | Guida introduttiva | Sviluppatori e amministratori **con esperienza di AEM** | 20 minuti |
| [Guida introduttiva a AEM tutorial pratico headless](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html?lang=it) | **Se preferisci un approccio pratico e hai familiarità con AEM**, questa esercitazione si divide direttamente nella creazione di un semplice progetto headless. | Tutorial | Sviluppatori | 2 ore |
