---
title: Chiamata  AEM Forms tramite API
seo-title: Chiamata  AEM Forms tramite API
description: Chiamata  AEM Forms tramite API
uuid: d100e106-e508-4d3c-ba8c-b5fe13c9e2d6
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding, development-tools
discoiquuid: 1825e12c-0306-4e0a-9643-47ce1ce82132
translation-type: tm+mt
source-git-commit: a873cf3e7efd3bc9cd4744bf09078d9040efcdda
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 0%

---


# Chiamata  AEM Forms tramite API {#invoking-aem-forms-using-apis}

 Adobe Experience Manager Forms è un software aziendale basato su J2EE che consiste in servizi che operano all&#39;interno di un&#39;infrastruttura condivisa. Le operazioni di assistenza in genere consumano o producono documenti. Utilizzando  AEM Forms, è possibile combinare il flusso di lavoro dei moduli con moduli elettronici, la protezione dei documenti e la generazione di documenti in un set di servizi integrato e coerente. È possibile accedere a questi servizi dall&#39;interno e dall&#39;esterno del firewall.

Le applicazioni client possono invocare  servizi AEM Forms a livello di programmazione utilizzando un&#39;API Java, servizi Web, Remoting e REST. Utilizzando la console di amministrazione, è possibile configurare un servizio per esporre un endpoint che consente  servizi AEM Forms invocato a livello di programmazione. Per impostazione predefinita, la maggior parte dei servizi è preconfigurata per esporre endpoint di tipo Remoting, Java e servizi Web.

I requisiti aziendali determinano quale metodo di chiamata utilizzare. Ad esempio, utilizzando l&#39;API Java, potete integrare  funzionalità AEM Forms nelle applicazioni aziendali Java, ad esempio Java Entity e MessageFave. Allo stesso modo, è possibile integrare  funzionalità AEM Forms in progetti .NET (o altri progetti sviluppati con ambienti di sviluppo che supportano gli standard dei servizi Web) utilizzando i servizi Web.

I servizi richiedono l&#39;esecuzione di un contenitore di servizi, in modo simile a quello in cui Enterprise JavaBeans™ (EJB) richiede un contenitore J2EE.  AEM Forms include solo un&#39;implementazione di un contenitore di servizi. Il contenitore del servizio è responsabile della gestione della durata di un servizio, inclusa la distribuzione e l&#39;invio di tutte le richieste al servizio corretto. Gestisce inoltre i documenti che un servizio può consumare o produrre.

>[!NOTE]
>
>La programmazione con AEM moduli non include informazioni su come richiamare  AEM Forms utilizzando Cartelle esaminate o e-mail.

