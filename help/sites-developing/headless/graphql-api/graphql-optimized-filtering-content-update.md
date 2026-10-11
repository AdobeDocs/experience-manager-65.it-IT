---
title: Aggiornamento dei frammenti di contenuto per un filtro GraphQL ottimizzato
description: Scopri come aggiornare i frammenti di contenuto per il filtro ottimizzato per GraphQL in Adobe Experience Manager per la distribuzione di contenuti headless.
exl-id: d78ec052-c091-49ca-9f36-a3d24eb9edd5
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
source-wordcount: '249'
ht-degree: 38%
---
# Aggiornamento dei frammenti di contenuto per un filtro GraphQL ottimizzato {#updating-content-fragments-for-optimized-graphql-filtering}

Per ottimizzare le prestazioni dei filtri di GraphQL, esegui una procedura per aggiornare i frammenti di contenuto.

>[!NOTE]
>
>Dopo aver aggiornato i frammenti di contenuto, puoi seguire i consigli per [Ottimizzare le query GraphQL](/help/sites-developing/headless/graphql-api/graphql-optimization.md).

## Prerequisiti {#prerequisites}

Assicurarsi di disporre almeno della versione 6.5.17.0 di AEM.

## Aggiornamento dei frammenti di contenuto {#updating-content-fragments}

Per eseguire la procedura, attenersi alla procedura descritta di seguito.

1. [Configura le impostazioni OSGi](/help/sites-deploying/configuring-osgi.md) per la **configurazione processo di migrazione frammenti di contenuto**:

   ![Configurazione processo di migrazione frammento di contenuto OSGi](assets/cfm-graphql-update-01.png "Configurazione processo di migrazione frammento di contenuto OSGi")

1. Nella finestra di dialogo, imposta questi due parametri come segue:

   * **ContentFragmentMigration:Enabled**: `1`
   * **ContentFragmentMigration:Enforce**: `1`

1. **Salva** le specifiche. Viene avviata la procedura di aggiornamento.

1. Attendere il completamento della procedura. La procedura è stata completata quando la proprietà `cfGlobalVersion` viene visualizzata in `/content/dam` ed è impostata su `1`.

1. Torna alla configurazione OSGi per disattivare la procedura.

   Nella finestra di dialogo per la **configurazione del processo di migrazione frammenti di contenuto**, imposta questi due parametri come segue:

   * **ContentFragmentMigration:Enabled**: `0`
   * **ContentFragmentMigration:Enforce**: `0`

## Limitazioni {#limitations}

Tieni presente le seguenti limitazioni:

* L’ottimizzazione delle prestazioni dei filtri di GraphQL sarà possibile solo dopo un aggiornamento completo di tutti i frammenti di contenuto (indicato dalla presenza della proprietà `cfGlobalVersion` per il nodo JCR `/content/dam`).

* Se i frammenti di contenuto vengono importati da un pacchetto di contenuti (utilizzando `crx/de`) dopo l’esecuzione della procedura di aggiornamento, tali frammenti di contenuto non vengono considerati nei risultati della query GraphQL, fino a quando la procedura di aggiornamento non viene eseguita nuovamente.
