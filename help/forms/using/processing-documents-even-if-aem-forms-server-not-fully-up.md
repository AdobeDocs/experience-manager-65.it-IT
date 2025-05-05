---
title: AEM Forms Server avvia l’elaborazione dei documenti anche prima che tutti i servizi siano operativi.
description: AEM Forms Server avvia l’elaborazione dei documenti anche prima che tutti i servizi siano operativi sul server JEE e sul server OSGi.
exl-id: 1a1bc1cb-e0ce-49a0-9b05-ae59f900cfb2
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 9f59606bb58b9e90f07bd22e89f3213afb54a697
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 3%

---

# AEM Forms Server avvia l’elaborazione dei documenti anche prima che tutti i servizi siano operativi{#aem-forms-server-start-processing-documents-even-if-it-is-not-fully-up}

## Problema   {#issue}

<!--When user restarts AEM Forms server, the current calling processes or services still continue such as rendering PDF documents and more. It causes the restart of the AEM Forms server to not startup correctly.-->

Prima che AEM Forms Server sia completamente operativo e che tutte le applicazioni siano in esecuzione, AEM Forms Server avvia l’elaborazione dei documenti.


## Applicabile a {#applies-to}

La soluzione si applica ad AEM Forms sul server JEE e AEM Forms sul server OSGi.

## Soluzione {#solution}

Per risolvere il problema, aggiungere un argomento `Dcom.adobe.livecycle.dsc.deferServiceStart=true` al [file batch](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/command-line-start-and-stop.html?lang=it#windows-platform-start-bat-script-example) durante l&#39;avvio del server.
