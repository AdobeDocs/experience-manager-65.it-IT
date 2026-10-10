---
title: Integrazione con Adobe Analytics
description: Scopri come integrare Adobe Experience Manager (AEM) con Adobe Analytics.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
docset: aem65
exl-id: 0a87ece4-57ed-4022-a78a-264c1edf4b4e
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: 243139ec-8e41-5296-a287-31343ab1bc0f
    internal-label: Integration
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 59%
---
# Integrazione con Adobe Analytics{#integrating-with-adobe-analytics}

L’integrazione di Adobe Analytics e AEM consente di monitorare l’attività della pagina web:

* Una configurazione Adobe Analytics consente a AEM l’autenticazione con Adobe Analytics.
* Un framework identifica i dati inviati alla suite di rapporti Adobe Analytics.

I dati includono dati della pagina e dell’utente; ad esempio:

* dati raccolti dai componenti AEM
* clic sui collegamenti
* informazioni sull&#39;utilizzo dei video
* il numero di visite alla pagina da Adobe Analytics

Le pagine seguenti sono utili per configurare l’integrazione:

* [Connessione ad Adobe Analytics e creazione di framework](/help/sites-administering/adobeanalytics-connect.md)
* [Configurazione del tracciamento dei collegamenti per Adobe Analytics](/help/sites-administering/adobeanalytics-link.md)
* [Mappatura dei dati dei componenti con le proprietà di Adobe Analytics](/help/sites-administering/adobeanalytics-mapping.md)
* [Configurazione del tracciamento video per Adobe Analytics](/help/sites-administering/adobeanalytics-video.md)
* [Classificazioni Adobe](/help/sites-administering/adobeanalytics-classifications.md)

È inoltre possibile utilizzare la procedura guidata [Opt-in](/help/sites-administering/opt-in.md) per eseguire facilmente l&#39;integrazione.

>[!NOTE]
>
>Consulta anche l&#39;articolo tutorial: [Integrazione di AEM con Adobe Target e Adobe Analytics utilizzando DTM](https://helpx.adobe.com/experience-manager/using/integrate-digital-marketing-solutions.html).

## Ulteriori informazioni {#further-information}

Consulta:

* [Estensione dell&#39;integrazione Adobe Analytics](/help/sites-developing/extending-analytics.md) per informazioni sullo sviluppo di componenti che raccolgono dati utente e sulla personalizzazione del framework Adobe Analytics.

>[!NOTE]
>
>Se utilizzi Adobe Analytics con una configurazione proxy personalizzata, devi [configurare due bundle OSGi](/help/sites-deploying/configuring-osgi.md) (ad esempio, con la console web), necessari per le configurazioni proxy **Apache HTTP Client**. Entrambi sono necessari, poiché alcune funzionalità di AEM utilizzano le API 3.x, mentre altre le API 4.x. Configurare:
>
>* **Client HTTP Day Commons 3.1** per configurare l’API 3.x;
>  ad esempio, [https://localhost:4502/system/console/configMgr/com.day.commons.httpclient](https://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>
>* **Configurazione proxy dei componenti HTTP Apache** per configurare l’API 4.x;
>  ad esempio, [https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)
>
