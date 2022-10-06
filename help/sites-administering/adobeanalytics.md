---
title: Integrazione con Adobe Analytics
seo-title: Integrating with Adobe Analytics
description: Scopri come integrare AEM con Adobe Analytics.
seo-description: Learn how to integrate AEM with Adobe Analytics.
uuid: d8548263-6ac5-45fb-8c70-52ecd4161bbb
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 444c522e-2f33-4f41-846c-8d317e799659
docset: aem65
exl-id: 0a87ece4-57ed-4022-a78a-264c1edf4b4e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 73%

---

# Integrazione con Adobe Analytics {#integrating-with-adobe-analytics}

L’integrazione di Adobe Analytics e AEM consente di monitorare l’attività della pagina web:

* Una configurazione Adobe Analytics consente a AEM l’autenticazione con Adobe Analytics.
* Un framework identifica i dati inviati alla suite di rapporti Adobe Analytics.

I dati includono i dati di pagina e utente; ad esempio:

* dati raccolti dai componenti AEM
* clic sui collegamenti
* informazioni sull&#39;utilizzo dei video
* il numero di visite alla pagina da Adobe Analytics

Le pagine seguenti consentono di configurare l’integrazione:

* [Connessione ad Adobe Analytics e creazione di framework](/help/sites-administering/adobeanalytics-connect.md)
* [Configurazione del tracciamento dei collegamenti per Adobe Analytics](/help/sites-administering/adobeanalytics-link.md)
* [Mappatura dei dati dei componenti con le proprietà di Adobe Analytics](/help/sites-administering/adobeanalytics-mapping.md)
* [Configurazione del tracciamento video per Adobe Analytics](/help/sites-administering/adobeanalytics-video.md)
* [Classificazioni Adobe](/help/sites-administering/adobeanalytics-classifications.md)

È inoltre possibile utilizzare [Procedura guidata di Opt-in](/help/sites-administering/opt-in.md) per eseguire facilmente l’integrazione.

>[!NOTE]
>
>Vedi anche l&#39;articolo tutorial: [Integrazione di AEM con Adobe Target e Adobe Analytics tramite DTM](https://helpx.adobe.com/experience-manager/using/integrate-digital-marketing-solutions.html).

## Ulteriori informazioni {#further-information}

Consulta:

* [Estensione dell’integrazione di Adobe Analytics](/help/sites-developing/extending-analytics.md) per informazioni sullo sviluppo di componenti che raccolgono dati utente e sulla personalizzazione del framework di Adobe Analytics.
* L’articolo della knowledge base, [Integrazione di Adobe Analytics - risoluzione dei problemi](https://helpx.adobe.com/it/experience-manager/kb/sitecatalystintegrationtroubleshooting.html), per informazioni sulla risoluzione dei problemi relativi all’integrazione di Adobe Analytics.

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

