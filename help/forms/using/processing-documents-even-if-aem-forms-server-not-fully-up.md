---
title: AEM Forms Server avvia l’elaborazione dei documenti anche prima che tutti i servizi siano operativi.
description: AEM Forms Server avvia l’elaborazione dei documenti anche prima che tutti i servizi siano operativi sul server JEE e sul server OSGi.
exl-id: 1a1bc1cb-e0ce-49a0-9b05-ae59f900cfb2
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 3%
---
# AEM Forms Server avvia l’elaborazione dei documenti anche prima che tutti i servizi siano operativi{#aem-forms-server-start-processing-documents-even-if-it-is-not-fully-up}

## Problema {#issue}

<!--When user restarts AEM Forms server, the current calling processes or services still continue such as rendering PDF documents and more. It causes the restart of the AEM Forms server to not startup correctly.-->

Prima che AEM Forms Server sia completamente operativo e che tutte le applicazioni siano in esecuzione, AEM Forms Server avvia l’elaborazione dei documenti.


## Applicabile a {#applies-to}

La soluzione si applica ad AEM Forms sul server JEE e AEM Forms sul server OSGi.

## Soluzione {#solution}

Per risolvere il problema, aggiungere un argomento `Dcom.adobe.livecycle.dsc.deferServiceStart=true` al [file batch](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/command-line-start-and-stop.html?lang=it#windows-platform-start-bat-script-example) durante l&#39;avvio del server.
