---
title: Integrazione di AEM e Adobe Commerce tramite Commerce integration framework
description: AEM e Adobe Commerce sono perfettamente integrati tramite la Commerce integration framework (CIF). L’CIF consente all’AEM di accedere a un’istanza di Adobe Commerce e comunicare con Adobe Commerce tramite GraphQL. Consente inoltre agli autori dell’AEM di utilizzare i selettori di prodotti e categorie e la console Prodotti per sfogliare i dati di prodotti e categorie recuperati on-demand da Adobe Commerce. Inoltre, CIF fornisce una vetrina pronta all’uso che può accelerare i progetti di commerce.
thumbnail: aem-magento-architecture.jpg
exl-id: f843784c-5ff7-41d1-97c5-13facb8459b2
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 23%

---

# Integrazione di AEM e Adobe Commerce (Magento) tramite Commerce integration framework {#aem-commerce-framework}

L’Experience Manager e Adobe Commerce sono integrati direttamente tramite la Commerce integration framework (CIF). L&#39;CIF consente all&#39;AEM di accedere e comunicare direttamente con l&#39;istanza di Commerce utilizzando le [API GraphQL](https://devdocs.magento.com/guides/v2.4/graphql/) di Adobe Commerce.

>[!NOTE]
>
>La versione minima supportata dell’API GraphQL è la 2.3.5. Alcune funzioni sono supportate solo nelle versioni più recenti o solo nell’edizione Adobe Commerce.

## Panoramica dell’architettura {#overview}

L’architettura generale è la seguente:

![Panoramica dell’architettura CIF &#x200B;](../assets/AEM_Magento_Architecture.png)

All’interno dell’CIF è disponibile il supporto di modelli di comunicazione lato server e lato client.
Le chiamate API lato server vengono implementate utilizzando il [client GraphQL](https://github.com/adobe/commerce-cif-graphql-client) integrato e generico in combinazione con un [set di modelli di dati generati](https://github.com/adobe/commerce-cif-magento-graphql) per lo schema commerce GraphQL. Inoltre, è possibile utilizzare qualsiasi query GraphQL o mutazione in formato GQL.

Per i componenti lato client, creati con [React](https://reactjs.org/), viene utilizzato il [client Apollo](https://www.apollographql.com/docs/react/).

## Architettura dei componenti core CIF dell’AEM {#cif-core-components}

![Architettura dei componenti core CIF di AEM](../assets/cif-component-architecture.jpg)

[I componenti core CIF dell&#39;AEM](https://github.com/adobe/aem-core-cif-components) seguono modelli di progettazione e best practice molto simili a quelli dei [componenti core WCM dell&#39;AEM](https://github.com/adobe/aem-core-wcm-components).

La logica di business e la comunicazione back-end con Adobe Commerce per i componenti core CIF dell’AEM sono implementate in modelli Sling. Nel caso sia necessario personalizzare questa logica per soddisfare i requisiti specifici del progetto, è possibile utilizzare il Pattern di delega per modelli Sling.

>[!TIP]
>
>La pagina [Personalizzazione dei componenti core CIF di AEM &#x200B;](../customizing/customize-cif-components.md) offre un esempio dettagliato e best practice per personalizzare i componenti core CIF.

All’interno dei progetti, i componenti core CIF dell’AEM e i componenti di progetto personalizzati possono facilmente recuperare il client configurato per un archivio Adobe Commerce associato a una pagina AEM tramite la configurazione Sling Context-Aware.
