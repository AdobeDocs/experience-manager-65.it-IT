---
title: Autenticazione per query GraphQL Adobe Experience Manager remote su frammenti di contenuto
description: Comprendi l’autenticazione necessaria per le query remote GraphQL di Adobe Experience Manager al fine di proteggere la distribuzione di contenuti headless.
feature: Content Fragments,GraphQL API
exl-id: 167f3318-7bc7-48fc-aaa9-73da43433f2f
solution: Experience Manager, Experience Manager Sites
role: Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: a642c50e-80eb-4fc1-a5d2-f3762d1f841d
    internal-label: Administration
subfeature_v2:
  - id: e9db7c79-8f65-4281-a439-c9049296d903
    internal-label: Content Fragments
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '112'
ht-degree: 41%
---
# Autenticazione per query GraphQL Adobe Experience Manager remote su frammenti di contenuto {#authentication-for-remote-aem-graphql-queries-on-content-fragments}

Un caso d&#39;uso principale per l&#39;API di GraphQL [Adobe Experience Manager (AEM) per la distribuzione di frammenti di contenuto](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md) consiste nell&#39;accettare query remote da applicazioni o servizi di terze parti. Queste query remote possono richiedere l’accesso a API autenticate, per garantire la distribuzione di contenuti headless.

>[!NOTE]
>
>Per i test e lo sviluppo è possibile inoltre accedere a API GraphQL AEM direttamente utilizzando l’[Interfaccia GraphiQL](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md#graphiql-interface).

Per l’autenticazione, il servizio di terze parti deve eseguire l’autenticazione utilizzando il nome utente e la password dell’account AEM.

<!-- 6.5.10.0 - does this content/page need to be migrated? -->

<!--
For authentication the third-party service needs to [retrieve an Access Token](#retrieving-access-token), that can then be [used in the GraphQL Request](#use-access-token-in-graphql-request).

## Retrieving an Access Token {#retrieving-access-token}

See [Generating Access Tokens for Server Side APIs](/help/sites-developing/generating-access-tokens-for-server-side-apis.md) for full details.

## Using the Access Token in a GraphQL Request {#use-access-token-in-graphql-request}

For a third-party service to connect with an AEM instance it needs to have an *Access Token*. The service must then add this token to the `Authorization` header on the POST request. 

For example, a GraphQL Authorization Header:

```xml
Authorization: Bearer <access_token>
```

## Permission Requirements {#permission-requirements}

All requests made using the access token will actually be made *by the user account that generated the token*. 

This means that you need to check that the account has the permissions required to run GraphQL queries. 

You can check this by using GraphiQL on the local instance.
-->
