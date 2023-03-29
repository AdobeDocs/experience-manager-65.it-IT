---
title: Utilizzo dell’IDE GraphiQL in AEM
description: Scopri come utilizzare l’IDE GraphiQL in Adobe Experience Manager.
source-git-commit: ad0f0bd8b0c230e002c734adca87da22bfa3a7cd
workflow-type: tm+mt
source-wordcount: '792'
ht-degree: 97%

---

# Utilizzo dell’IDE GraphiQL {#graphiql-ide}

Un’implementazione dell’IDE [GraphiQL](https://graphql.org/learn/serving-over-http/#graphiql) standard è disponibile con l’API GraphQL di Adobe Experience Manager (AEM).

>[!NOTE]
>
>GraphiQL è incluso in tutti gli ambienti di AEM (ma sarà accessibile/visibile solo quando configuri gli endpoint).
>
>Nelle versioni precedenti, era necessario un pacchetto per installare l’IDE GraphiQL. Se installato, ora è possibile rimuoverlo.

>[!NOTE]
>Prima di utilizzare l’IDE GraphiQL, devi avere [configurato gli endpoint](/help/sites-developing/headless/graphql-api/graphql-endpoint.md) nel [browser delle configurazioni](/help/assets/content-fragments/content-fragments-configuration-browser.md).

Lo strumento **GraphiQL** consente di testare ed eseguire il debug delle query GraphQL consentendoti di:

* selezionare l’**Endpoint** appropriato per la configurazione Sites da utilizzare per le query;
* inserire direttamente nuove query;
* creare e accedere a **[query persistenti](/help/sites-developing/headless/graphql-api/persisted-queries.md)**;
* eseguire le query per visualizzare immediatamente i risultati;
* gestire **variabili di query**;
* salvare e gestire **query persistenti**;
* pubblicare o annullare la pubblicazione di **query persistenti** (ad esempio, a/da `dev-publish`);
* vedere la **cronologia** delle query precedenti;
* utilizzare **Esplora documentazione** per accedere alla documentazione, per scoprire e comprendere i metodi disponibili.

Puoi accedere all’editor delle query da:

* **Strumenti** -> **Generale** -> **Editor query GraphQL**
* direttamente; ad esempio `http://localhost:4502/aem/graphiql.html`

![Interfaccia di GraphiQL](assets/cfm-graphiql-interface.png "Interfaccia di GraphiQL")

Puoi utilizzare GraphiQL nel tuo sistema in modo che le query possano essere richieste dall’applicazione client mediante richieste GET, nonché per pubblicarle. Per l’utilizzo in produzione, puoi quindi [spostare le query nell’ambiente di produzione](/help/sites-developing/headless/graphql-api/persisted-queries.md#transfer-persisted-query-production). Inizialmente devi spostarle nell’istanza Author dell’ambiente di produzione per convalidare i contenuti appena creati con le query, e infine nell’istanza Publish di produzione per l’utilizzo live.

## Selezione dell’endpoint {#selecting-endpoint}

Come primo passo è necessario selezionare l’**[endpoint](/help/sites-developing/headless/graphql-api/graphql-endpoint.md)** da utilizzare per le query. L’endpoint è appropriato per la configurazione Sites che desideri utilizzare per le query.

È disponibile dall’elenco a discesa in alto a destra.

## Creazione e persistenza di una nuova query {#creating-new-query}

Puoi inserire la nuova query nell’editor, che si trova nel pannello centrale a sinistra, direttamente sotto il logo GraphiQL.

>[!NOTE]
>
>Se hai già selezionato una query persistente, ed è visualizzata nel pannello editor, seleziona `+` (accanto a **query persistenti**) per svuotare l’editor approntandolo per la nuova query.

A questo punto è sufficiente iniziare a digitare. L’editor, inoltre:

* mostra ulteriori informazioni sugli elementi al passaggio del mouse;
* fornisce funzioni quali evidenziazione della sintassi, completamento automatico e suggerimento automatico.

>[!NOTE]
>
>Le query GraphQL in genere iniziano con un carattere `{`.
>
>Le righe che iniziano con `#` vengono ignorate.

Utilizza **Salva con nome** per rendere persistente la nuova query.

## Aggiornamento della query persistente {#updating-persisted-query}

Seleziona la query da aggiornare dall’elenco nel pannello delle **[query persistenti](/help/sites-developing/headless/graphql-api/persisted-queries.md)** (a sinistra).

La query viene visualizzata nel pannello dell’editor. Apporta le modifiche necessarie, quindi utilizza **Salva** per confermare gli aggiornamenti della query persistente.

## Esecuzione delle query {#running-queries}

Puoi eseguire immediatamente una nuova query oppure caricare ed eseguire una query persistente. Per caricare una query persistente, selezionala dall’elenco: la query viene visualizzata nel pannello dell’editor.

In entrambi i casi, la query visualizzata nel pannello dell’editor è quella che verrà eseguita quando:

* tocchi o fai clic sull’icona **Esegui query**;
* utilizzi la scelta rapida di tastiera `Control-Enter`.

## Variabili di query {#query-variables}

<!-- more details needed here? -->

L’IDE GraphiQL consente inoltre di gestire le [variabili di query](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md#graphql-variables).

Esempio:

![Variabili GraphQL](assets/cfm-graphqlapi-03.png "Variabili GraphQL")

<!--
## Managing cache for your persisted queries {#managing-cache}

[Persisted queries](/help/headless/graphql-api/persisted-queries.md) are recommended as they can be cached at the dispatcher and CDN layers, ultimately improving the performance of the requesting client application. By default AEM will invalidate the Content Delivery Network (CDN) cache based on a default Time To Live (TTL).

>[!NOTE]
>
>Custom rewrite rules on the Dispatcher might override defaults from AEM publish. 
>
>In the case that you are sending TTL-based cache-control headers from the dispatcher, based on a location match pattern, then, if necessary, you might want to exclude `/graphql/execute.json/*` from the matches.

Using GraphQL you can configure the HTTP Cache Headers  to control these parameters for your individual persisted query.

1. The **Headers** option is accessible via the three vertical dots to the right of the persisted query name (far left panel):

   ![Persisted Query HTTP Cache Headers](assets/cfm-graphqlapi-headers-01.png "Persisted Query HTTP Cache Headers")

1. Selecting this will open the **Cache Configuration** dialog:

   ![Persisted Query HTTP Cache Header Settings](assets/cfm-graphqlapi-headers-02.png "Persisted Query HTTP Cache Header Settings")

1. Select the appropriate parameter, then adjust the value as required:

   * **cache-control** - **max-age**
     Caches can store this content for specified number of seconds. Typically this is the browser TTL (Time To Live).
   * **surrogate-control** - **s-maxage**
     Same as max-age but applies specifically to proxy caches.
   * **surrogate-control** - **stale-while-revalidate**
     Caches may continue to serve a cached response after it becomes stale, for up to the specified number of seconds.
   * **surrogate-control** - **stale-if-error**
     Caches may continue to serve a cached response in case of or origin error, for up to the specified number of seconds.

1. Select **Save** to persist the changes.
-->

## Pubblicazione di query persistenti {#publishing-persisted-queries}

Una volta selezionato il [query persistente](/help/sites-developing/headless/graphql-api/persisted-queries.md) dall’elenco (pannello a sinistra) puoi utilizzare il **Pubblica** e **Annulla pubblicazione** azioni. Queste consentono di attivarle nell’ambiente di pubblicazione (ad esempio, `dev-publish`) per renderle facilmente accessibili dalle applicazioni in fase di test.

>[!NOTE]
>
>La definizione della cache della query persistente `Time To Live` {&quot;cache-control&quot;:&quot;parameter&quot;:value} ha un valore predefinito di 2 ore (7200 secondi).

## Copiare l’URL per accedere direttamente alla query {#copy-url}

L’opzione **Copia URL** consente di simulare una query copiando l’URL utilizzato per accedere direttamente alla query persistente e visualizzare i risultati. Questa può quindi essere utilizzata per i test; ad esempio, accedendo in un browser:

<!--
  >[!NOTE]
  >
  >The URL will need [encoding before using programmatically](/help/headless/graphql-api/persisted-queries.md#encoding-query-url).
  >
  >The target environment might need adjusting, depending on your requirements.
-->

Esempio:

`http://localhost:4502/graphql/execute.json/global/article-list-01`

Utilizzando questo URL in un browser, puoi confermare i risultati:

![GraphiQL - Copia URL](assets/cfm-graphiql-copy-url.png "GraphiQL - Copia URL")

L’opzione **Copia URL** è accessibile tramite i tre punti verticali a destra del nome della query persistente (pannello a sinistra):

![GraphiQL - Copia URL](assets/cfm-graphiql-persisted-query-options.png "GraphiQL - Copia URL")

## Eliminazione delle query persistenti {#deleting-persisted-queries}

L’opzione **Elimina** è anch’essa accessibile tramite i tre punti verticali a destra del nome della query persistente (pannello a sinistra).

<!-- what happens if you try to delete something that is still published? -->


## Installazione della query persistente nell’ambiente di produzione {#installing-persisted-query-production}

Dopo aver sviluppato e testato la query persistente con GraphiQL, occorre [trasferirla all’ambiente di produzione](/help/sites-developing/headless/graphql-api/persisted-queries.md#transfer-persisted-query-production) in modo che possa essere utilizzata dalle applicazioni.

## Scelte rapide da tastiera {#keyboard-shortcuts}

Nell’IDE è disponibile una selezione di scelte rapide da tastiera per accedere direttamente alle icone di azione:

* Migliora query: `Shift-Control-P`
* Unisci query: `Shift-Control-M`
* Esegui query: `Control-Enter`
* Completamento automatico: `Control-Space`

>[!NOTE]
>
>Su alcune tastiere il tasto `Control` è etichettato come `Ctrl`.
