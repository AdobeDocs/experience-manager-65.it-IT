---
title: Integrazione con Adobe Analytics
seo-title: Integrazione con Adobe Analytics
description: Scoprite come integrare AEM con  Adobe Analytics.
seo-description: Scoprite come integrare AEM con  Adobe Analytics.
uuid: d8548263-6ac5-45fb-8c70-52ecd4161bbb
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 444c522e-2f33-4f41-846c-8d317e799659
docset: aem65
translation-type: tm+mt
source-git-commit: ca25e66b280db479f69c487753a557b0240233da
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 21%

---


# Integrazione con Adobe Analytics{#integrating-with-adobe-analytics}

L’integrazione  Adobe Analytics e AEM consente di monitorare l’attività della pagina Web:

* Una configurazione Adobe Analytics  consente AEM l&#39;autenticazione con  Adobe Analytics.
* Un framework identifica i dati inviati alla suite di rapporti Adobe Analytics .

I dati comprendono i dati di pagina e utente; ad esempio:

* dati raccolti AEM componenti
* clic collegamento
* informazioni sull’utilizzo video
* il numero di visite di pagina da  Adobe Analytics

Le pagine seguenti consentono di configurare l&#39;integrazione:

* [Connessione a  Adobe Analytics e creazione di framework](/help/sites-administering/adobeanalytics-connect.md)
* [Configurazione del tracciamento dei collegamenti per  Adobe Analytics](/help/sites-administering/adobeanalytics-link.md)
* [Mappatura dei dati dei componenti con  delle proprietà Adobe Analytics](/help/sites-administering/adobeanalytics-mapping.md)
* [Configurazione del tracciamento video per  Adobe Analytics](/help/sites-administering/adobeanalytics-video.md)
* [Classificazioni  Adobe](/help/sites-administering/adobeanalytics-classifications.md)

Per eseguire facilmente l&#39;integrazione è inoltre possibile utilizzare la [procedura guidata di consenso](/help/sites-administering/opt-in.md).

>[!NOTE]
>
>Consultate anche l’articolo introduttivo: [Integrazione AEM con  Adobe Target e  Adobe Analytics mediante DTM](https://helpx.adobe.com/experience-manager/using/integrate-digital-marketing-solutions.html).

## Ulteriori informazioni {#further-information}

Consulta:

* [Estensione  ](/help/sites-developing/extending-analytics.md) Integrazione Adobe Analytics per informazioni sullo sviluppo di componenti che raccolgono dati utente e la personalizzazione del framework Adobe Analytics .
* L&#39;articolo della knowledge base, [ integrazione Adobe Analytics - risoluzione dei problemi](https://helpx.adobe.com/experience-manager/kb/sitecatalystintegrationtroubleshooting.html), per informazioni sulla risoluzione dei problemi relativi all&#39;integrazione  Adobe Analytics.

>[!NOTE]
>
>Se utilizzi Adobe Analytics con una configurazione proxy personalizzata, devi [configurare due bundle OSGi](/help/sites-deploying/configuring-osgi.md) (ad esempio, con la console web), necessari per le configurazioni proxy **Apache HTTP Client**. Entrambi sono necessari, poiché alcune funzionalità di AEM utilizzano le API 3.x, mentre altre le API 4.x. Configurazione:
>
>* **Day Commons HTTP Client 3.1** per configurare l&#39;API 3.x;
   >  ad esempio, [https://localhost:4502/system/console/configMgr/com.day.commons.httpclient](https://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
   >
   >
* **Configurazione proxy** dei componenti Apache HTTP per configurare l&#39;API 4.x;
   >  ad esempio, [https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)

>



