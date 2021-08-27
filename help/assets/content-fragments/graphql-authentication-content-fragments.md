---
title: Autenticazione per query GraphQL AEM remote su frammenti di contenuto
description: Comprendere l’autenticazione necessaria per le query GraphQL AEM remote al fine di proteggere la distribuzione di contenuti headless.
feature: Content Fragments,GraphQL API
source-git-commit: 2f647fc640d3809dc684bce397831ab37fb94b07
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 0%

---

# Autenticazione per query GraphQL AEM remote su frammenti di contenuto {#authentication-for-remote-aem-graphql-queries-on-content-fragments}

Un caso d&#39;uso principale per l&#39; [API GraphQL di Adobe Experience Manager (AEM) per la distribuzione dei frammenti di contenuto](/help/assets/content-fragments/graphql-api-content-fragments.md) è quello di accettare query remote da applicazioni o servizi di terze parti. Queste query remote possono richiedere l’accesso alle API autenticate per garantire la distribuzione di contenuti headless.

>[!NOTE]
>
>Per i test e lo sviluppo è inoltre possibile accedere all&#39;API GraphQL AEM direttamente utilizzando l&#39;interfaccia [GraphiQL](/help/assets/content-fragments/graphql-api-content-fragments.md#graphiql-interface) .

Per l&#39;autenticazione, il servizio di terze parti deve [recuperare un token di accesso](#retrieving-access-token), che può quindi essere [utilizzato nella richiesta GraphQL](#use-access-token-in-graphql-request).

## Recupero di un token di accesso {#retrieving-access-token}

<!-- 6.5.10.0 - does this page need to be migrated? -->

<!--
See [Generating Access Tokens for Server Side APIs](/help/sites-developing/generating-access-tokens-for-server-side-apis.md) for full details.
-->

## Utilizzo del token di accesso in una richiesta GraphQL {#use-access-token-in-graphql-request}

Affinché un servizio di terze parti possa connettersi a un&#39;istanza AEM, deve disporre di un *token di accesso*. Il servizio deve quindi aggiungere questo token all’intestazione `Authorization` nella richiesta di POST.

Ad esempio, un’intestazione di autorizzazione GraphQL:

```xml
Authorization: Bearer <access_token>
```

## Requisiti delle autorizzazioni {#permission-requirements}

Tutte le richieste effettuate utilizzando il token di accesso saranno in realtà effettuate *dall&#39;account utente che ha generato il token*.

Ciò significa che devi verificare che l’account disponga delle autorizzazioni necessarie per eseguire le query GraphQL.

Puoi controllare questo usando GraphiQL sull&#39;istanza locale.
