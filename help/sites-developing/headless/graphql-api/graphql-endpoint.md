---
title: Gestire gli endpoint GraphQL in AEM
description: Scopri come gestire gli endpoint GraphQL in Adobe Experience Manager per la distribuzione di contenuti headless.
exl-id: a59a5e50-0787-4c1c-a83d-bb3eac1479a8
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
source-wordcount: '510'
ht-degree: 91%
---
# Gestire gli endpoint GraphQL in AEM {#graphql-aem-endpoint}

L’endpoint è il percorso utilizzato per accedere a GraphQL per AEM. Utilizzando questo percorso (o la tua app) puoi:

* accedere allo schema GraphQL;
* inviare le query GraphQL;
* ricevere le risposte (alle query GraphQL).

Esistono due tipi di endpoint in AEM:

* Globale
  * Disponibile per tutti i siti.
  * Questo endpoint può utilizzare tutti i modelli per frammenti di contenuto di tutte le configurazioni di Sites (definite nella sezione [Browser configurazioni](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser)).
  * Se esistono modelli per frammenti di contenuto che devono essere condivisi tra le configurazioni di Sites, questi devono essere creati nelle configurazioni globali di Sites.
* Configurazioni di Sites:
  * Corrisponde a una configurazione Sites, come definita nella sezione [Browser configurazioni](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser).
  * Sono specifiche per un determinato sito o progetto.
  * Un endpoint specifico per la configurazione di Sites utilizzerà i modelli di frammento di contenuto di quella specifica configurazione di Sites insieme a quelli della configurazione globale di Sites.

>[!CAUTION]
>
>L’Editor frammento di contenuto può consentire a un frammento di contenuto di una configurazione Sites di fare riferimento a un frammento di contenuto di un’altra configurazione Sites (tramite criteri).
>
>In questo caso non tutti i contenuti saranno recuperabili utilizzando un endpoint specifico per la configurazione Sites.
>
>L’autore del contenuto deve controllare questo scenario; ad esempio, potrebbe essere utile inserire modelli per frammenti di contenuto condivisi nella configurazione globale di Sites.

Il percorso dell’archivio di GraphQL per l’endpoint globale di AEM è:

`/content/cq:graphql/global/endpoint`

Per cui l’app può utilizzare il seguente percorso nell’URL della richiesta:

`/content/_cq_graphql/global/endpoint.json`

Per abilitare un endpoint per GraphQL per AEM è necessario:

* [Abilitare l’endpoint GraphQL](#enabling-graphql-endpoint)
* [Pubblicare l’endpoint GraphQL](#publishing-graphql-endpoint)

## Abilitazione dell’endpoint GraphQL {#enabling-graphql-endpoint}

Per abilitare un endpoint GraphQL è innanzitutto necessario disporre di una configurazione appropriata. Vedi la sezione [Frammenti di contenuto - Browser configurazioni](/help/assets/content-fragments/content-fragments-configuration-browser.md).

>[!CAUTION]
>
>Se l’[utilizzo di modelli per frammenti di contenuto non è stato abilitato](/help/assets/content-fragments/content-fragments-configuration-browser.md), l’opzione **Crea** non sarà disponibile.

Per abilitare l’endpoint corrispondente:

1. Passa a **Strumenti**, **Risorse**, quindi seleziona **GraphQL**.
1. Seleziona **Crea**.
1. Si apre la finestra di dialogo **Crea nuovo endpoint GraphQL**. Qui potrai definire:
   * **Nome**: nome dell’endpoint; puoi immettere qualsiasi testo.
   * **Utilizza lo schema GraphQL fornito da**: dal menu a discesa, seleziona il sito o il progetto richiesto.

   >[!NOTE]
   >
   >Nella finestra di dialogo viene visualizzato il seguente avviso:
   >
   >* *Se non vengono gestiti con attenzione, gli endpoint GraphQL possono causare problemi di prestazioni e sicurezza dei dati. Assicurarsi di impostare le autorizzazioni appropriate dopo la creazione di un endpoint.*

1. Per confermare, fai clic su **Crea**.
1. La finestra di dialogo **Passaggi successivi** fornisce un collegamento diretto alla console Sicurezza per verificare che l’endpoint appena creato disponga delle autorizzazioni appropriate.

   >[!CAUTION]
   >
   >L’endpoint è accessibile a tutti. Questo può creare problemi di sicurezza, soprattutto per le istanze di pubblicazione, in quanto le query GraphQL possono imporre un carico pesante sul server.
   >
   >Puoi impostare sull’endpoint eventuali ACL appropriate al tuo caso d’uso.

## Pubblicazione dell’endpoint GraphQL {#publishing-graphql-endpoint}

Seleziona il nuovo endpoint e scegli **Pubblica** per renderlo completamente disponibile in tutti gli ambienti.

>[!CAUTION]
>
>L’endpoint è accessibile a tutti.
>
>Nelle istanze di pubblicazione questo può rappresentare un problema di sicurezza, in quanto le query GraphQL possono imporre un carico pesante sul server.
>
>Configura sull’endpoint le ACL appropriate al tuo caso d’uso.
