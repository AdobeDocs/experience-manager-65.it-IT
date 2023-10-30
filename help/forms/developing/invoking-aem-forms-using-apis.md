---
title: Come si richiama AEM Forms utilizzando le API?
description: Richiama i servizi AEM Forms utilizzando un’API Java, i servizi web, la comunicazione remota e REST.
uuid: d100e106-e508-4d3c-ba8c-b5fe13c9e2d6
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding, development-tools
discoiquuid: 1825e12c-0306-4e0a-9643-47ce1ce82132
role: Developer
exl-id: 0e92d1ad-12bd-4bfd-81cc-9be8e376c5ca
source-git-commit: 0e5b89617d481c69882ec5d4658e76855aa9b691
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 0%

---

# Richiamare AEM Forms tramite API {#invoking-aem-forms-using-apis}

**Gli esempi e gli esempi contenuti in questo documento sono solo per l’ambiente AEM Forms su JEE.**

Adobe Experience Manager Forms è un software aziendale basato su J2EE costituito da servizi che operano all&#39;interno di un&#39;infrastruttura condivisa. In genere, le operazioni di assistenza utilizzano o producono documenti. Utilizzando AEM Forms, puoi combinare il flusso di lavoro dei moduli con i moduli elettronici, la sicurezza dei documenti e la generazione di documenti in un set di servizi integrato e coeso. Questi servizi sono accessibili dall&#39;interno e dall&#39;esterno del firewall.

Le applicazioni client possono richiamare in modo programmatico i servizi AEM Forms utilizzando un’API Java, servizi web, comunicazione remota e REST. Utilizzando la console di amministrazione, puoi configurare un servizio in modo da esporre un endpoint che consenta ai servizi di AEM Forms di essere richiamati a livello di programmazione. Per impostazione predefinita, la maggior parte dei servizi è preconfigurata per esporre endpoint di tipo remoto, Java e servizio Web.

I requisiti aziendali determinano il metodo di chiamata da utilizzare. Ad esempio, utilizzando l’API Java, puoi integrare la funzionalità AEM Forms nelle applicazioni aziendali Java, come Java Entity e Message Beans. Analogamente, è possibile integrare le funzionalità di AEM Forms nei progetti .NET (o in altri progetti sviluppati con ambienti di sviluppo che supportano gli standard dei servizi Web) utilizzando i servizi Web.

I servizi richiedono l’esecuzione di un contenitore di servizi, in modo analogo a come gli EJB (Enterprise JavaBeans™) richiedono un contenitore J2EE. AEM Forms include una sola implementazione di un contenitore di servizi. Il contenitore di servizi è responsabile della gestione della durata di un servizio, inclusa la sua distribuzione e la garanzia che tutte le richieste vengano inviate al servizio corretto. Gestisce inoltre i documenti utilizzati o prodotti da un servizio.

>[!NOTE]
>
>La programmazione con i moduli AEM non include informazioni su come richiamare AEM Forms utilizzando Cartelle controllate o posta elettronica.
