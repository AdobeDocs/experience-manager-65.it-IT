---
title: Richiamo di moduli AEM tramite API
seo-title: Richiamo di moduli AEM tramite API
description: 'null'
seo-description: 'null'
uuid: d100e106-e508-4d3c-ba8c-b5fe13c9e2d6
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: development-tools
discoiquuid: 1825e12c-0306-4e0a-9643-47ce1ce82132
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Richiamo di moduli AEM tramite API {#invoking-aem-forms-using-apis}

Adobe Experience Manager Forms è un software aziendale basato su J2EE composto da servizi che operano all’interno di un’infrastruttura condivisa. Le operazioni di assistenza in genere consumano o producono documenti. AEM Forms consente di combinare i flussi di lavoro dei moduli con moduli elettronici, la protezione dei documenti e la generazione di documenti in un set di servizi integrato e coerente. È possibile accedere a questi servizi dall&#39;interno e dall&#39;esterno del firewall.

Le applicazioni client possono invocare i servizi AEM Forms a livello di programmazione tramite un&#39;API Java, servizi Web, Remoting e REST. Utilizzando la console di amministrazione potete configurare un servizio per esporre un endpoint che consente ai servizi AEM Forms di essere invocati a livello di programmazione. Per impostazione predefinita, la maggior parte dei servizi è preconfigurata per esporre endpoint di tipo Remoting, Java e servizi Web.

I requisiti aziendali determinano quale metodo di chiamata utilizzare. Ad esempio, utilizzando l&#39;API Java, potete integrare la funzionalità di AEM Forms nelle applicazioni aziendali Java, come Java Entity e MessageBeg. Allo stesso modo, è possibile integrare la funzionalità di AEM Forms in progetti .NET (o altri progetti sviluppati con ambienti di sviluppo che supportano gli standard dei servizi Web) utilizzando i servizi Web.

I servizi richiedono l&#39;esecuzione di un contenitore di servizi, in modo simile a quello in cui Enterprise JavaBeans™ (EJB) richiede un contenitore J2EE. In AEM Forms è inclusa una sola implementazione di un contenitore di servizi. Il contenitore del servizio è responsabile della gestione della durata di un servizio, inclusa la distribuzione e l&#39;invio di tutte le richieste al servizio corretto. Gestisce inoltre i documenti che un servizio può consumare o produrre.

>[!NOTE]
>
>La programmazione con i moduli AEM non include informazioni su come richiamare AEM Forms utilizzando cartelle esaminate o e-mail.

