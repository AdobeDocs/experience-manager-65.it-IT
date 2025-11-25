---
title: Aggiornamento dei frammenti di contenuto per un filtro GraphQL ottimizzato
description: Scopri come aggiornare i frammenti di contenuto per il filtro ottimizzato per GraphQL in Adobe Experience Manager per la distribuzione di contenuti headless.
exl-id: d78ec052-c091-49ca-9f36-a3d24eb9edd5
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments,GraphQL,Persisted Queries,Developing
role: Admin,Developer
source-git-commit: 07289e891399a78568dcac957bc089cc08c7898c
workflow-type: tm+mt
source-wordcount: '250'
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
