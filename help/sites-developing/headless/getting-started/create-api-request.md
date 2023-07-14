---
title: Guida rapida all’accesso e alla distribuzione di frammenti di contenuto headless
description: Scopri come utilizzare l’API REST di AEM Assets per gestire i frammenti di contenuto e l’API GraphQL per la distribuzione headless dei contenuti di frammenti di contenuto.
exl-id: 4664b3a4-4873-4f42-b59d-aadbfaa6072f
source-git-commit: 260f71acd330167572d817fdf145a018b09cbc65
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 31%

---

# Guida rapida all’accesso e alla distribuzione di frammenti di contenuto headless {#accessing-delivering-content-fragments}

Scopri come utilizzare l’API REST di AEM Assets per gestire i frammenti di contenuto e l’API GraphQL per la distribuzione headless dei contenuti di frammenti di contenuto.

## Cosa sono le API REST di GraphQL e Assets? {#what-are-the-apis}

[Dopo aver creato alcuni frammenti di contenuto,](create-content-fragment.md) puoi utilizzare le API AEM per distribuirle senza problemi.

* [API GraphQL](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md) consente di creare richieste per accedere e distribuire frammenti di contenuto.
   * Per utilizzare questo, [gli endpoint devono essere definiti e abilitati in AEM](/help/sites-developing/headless/graphql-api/graphql-endpoint.md#enabling-graphql-endpoint)e, se necessario, [Interfaccia GraphiQL installata](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md#installing-graphiql-interface).
* [API REST di Assets](/help/assets/assets-api-content-fragments.md) consente di creare e modificare frammenti di contenuto (e altre risorse).

Il resto di questa guida si concentra sull’accesso a GraphQL e sulla distribuzione di frammenti di contenuto.

## Come distribuire un frammento di contenuto con GraphQL {#how-to-deliver-a-content-fragment}

Gli architetti di informazioni devono progettare query per gli endpoint di canale per distribuire i contenuti. Queste query devono essere considerate solo una volta per endpoint per modello. Ai fini di questa guida introduttiva, è sufficiente crearne una.

1. Accedi all’AEM e accedi a [Interfaccia GraphiQL](/help/sites-developing/headless/graphql-api/graphiql-ide.md):
   * Esempio: `http://<host>:<port>/aem/graphiql.html`.

1. GraphiQL è un editor di query interno al browser per GraphQL. Puoi utilizzarlo per creare query per recuperare frammenti di contenuto e distribuirli senza problemi come JSON.
   * Il pannello a sinistra ti consente di creare la query.
   * Nel pannello a destra vengono visualizzati i risultati.
   * L’editor delle query dispone del completamento del codice e dei tasti di scelta rapida per eseguire facilmente la query.
     ![Editor GraphiQL](assets/graphiql.png)

1. Supponendo che il modello creato sia stato chiamato `person` con campi `firstName`, `lastName`, e `position`, puoi creare una semplice query per recuperare il contenuto del frammento di contenuto.

   ```text
   query 
   {
     personList {
       items {
         _path
         firstName
         lastName
         position
       }
     }
   }
   ```

1. Inserisci la query nel pannello a sinistra.
<!--
   ![GraphiQL query](assets/graphiql-query.png)
-->

1. Fai clic su **Esegui query** (freccia destra) o utilizza l’icona `Ctrl-Enter` e i risultati vengono visualizzati come JSON nel pannello di destra.
   ![Risultati GraphiQL](assets/graphiql-results.png)

1. Clic:
   * **Documentazione** in alto a destra per visualizzare la documentazione contestuale per aiutarti a creare query che si adattano ai tuoi modelli.
   * **Cronologia** nella barra degli strumenti superiore per visualizzare le query precedenti.
   * **Salva con nome** e **Salva** per salvare le query, dopodiché puoi elencarle e recuperarle dalla **Query persistenti** pannello e **Pubblica**.
     ![Documentazione di GraphiQL](assets/graphiql-documentation.png)

GraphQL consente query strutturate che possono essere indirizzate non solo a set di dati specifici o a singoli oggetti di dati, ma che possono anche fornire elementi specifici degli oggetti, risultati nidificati, offerte di supporto per variabili di query e molto altro.

GraphQL può evitare richieste API iterative e consegne eccessive. Al contrario, consente la distribuzione in blocco di ciò che è esattamente necessario per il rendering come risposta a una singola query API. Il JSON risultante può essere utilizzato per inviare dati ad altri siti o app.

## Passaggi successivi {#next-steps}

Tutto qui. Ora hai una conoscenza di base della gestione dei contenuti headless in AEM. Sono disponibili molte altre risorse da approfondire per una comprensione completa delle funzioni disponibili.

* **[Browser configurazioni](create-configuration.md)** - Per informazioni dettagliate sul browser di configurazione AEM
* **[Frammenti di contenuto](/help/assets/content-fragments/content-fragments.md)**: per informazioni dettagliate sulla creazione e la gestione dei frammenti di contenuto
* **[IDE GraphiQL](/help/sites-developing/headless/graphql-api/graphiql-ide.md)** per ulteriori dettagli sull’utilizzo dell’IDE GraphiQL
* **[Query persistenti](/help/sites-developing/headless/graphql-api/persisted-queries.md)** per ulteriori dettagli sulle query persistenti
* **[Supporto per frammenti di contenuto nell’API HTTP di AEM Assets](/help/assets/assets-api-content-fragments.md)**: per informazioni dettagliate sull’accesso diretto ai contenuti AEM tramite l’API HTTP, mediante operazioni CRUD (Crea, Leggi, Aggiorna, Elimina)
* **[API di GraphQL](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md)**: per informazioni dettagliate su come distribuire i frammenti di contenuto in modo corretto
