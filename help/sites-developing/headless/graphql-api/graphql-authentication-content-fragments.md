---
title: Autenticazione per query GraphQL Adobe Experience Manager remote su frammenti di contenuto
description: Comprendi l’autenticazione necessaria per le query Remote Adobe Experience Manager GraphQL al fine di proteggere la distribuzione di contenuti headless.
feature: Content Fragments,GraphQL API
exl-id: 167f3318-7bc7-48fc-aaa9-73da43433f2f
source-git-commit: e068cee192c0837f1473802143e0793674d400e8
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%

---

# Autenticazione per query GraphQL Adobe Experience Manager remote su frammenti di contenuto {#authentication-for-remote-aem-graphql-queries-on-content-fragments}

Un caso d’uso principale per [API GraphQL di Adobe Experience Manager (AEM) per la distribuzione dei frammenti di contenuto](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md) accetta query remote da applicazioni o servizi di terze parti. Queste query remote possono richiedere l’accesso alle API autenticate per garantire la distribuzione sicura dei contenuti headless.

>[!NOTE]
>
>Per i test e lo sviluppo, puoi anche accedere all’API GraphQL dell’AEM direttamente utilizzando [Interfaccia GraphiQL](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md#graphiql-interface).

Per l’autenticazione, il servizio di terze parti deve eseguire l’autenticazione utilizzando il nome utente e la password dell’account AEM.

<!-- 6.5.10.0 - does this content/page need to be migrated? -->

<!--
For authentication the third party service needs to [retrieve an Access Token](#retrieving-access-token), that can then be [used in the GraphQL Request](#use-access-token-in-graphql-request).

## Retrieving an Access Token {#retrieving-access-token}

See [Generating Access Tokens for Server Side APIs](/help/sites-developing/generating-access-tokens-for-server-side-apis.md) for full details.

## Using the Access Token in a GraphQL Request {#use-access-token-in-graphql-request}

For a third party service to connect with an AEM instance it needs to have an *Access Token*. The service must then add this token to the `Authorization` header on the POST request. 

For example, a GraphQL Authorization Header:

```xml
Authorization: Bearer <access_token>
```

## Permission Requirements {#permission-requirements}

All requests made using the access token will actually be made *by the user account that generated the token*. 

This means that you need to check that the account has the permissions required to run GraphQL queries. 

You can check this by using GraphiQL on the local instance.
-->
