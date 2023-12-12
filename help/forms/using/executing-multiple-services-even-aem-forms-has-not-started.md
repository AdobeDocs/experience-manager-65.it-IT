---
title: L’esecuzione di più servizi nonostante AEM Forms non è stata avviata.
description: Anche se AEM Forms non è stato avviato completamente, elabora più servizi.
exl-id: 4ec40412-15b1-434b-a919-2cf23f48077c
source-git-commit: faa628ac4a4631564141f68f3efc9d69a67e5c40
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 4%

---

# L’esecuzione di più servizi nonostante AEM Forms non è stata avviata completamente{#steps-to-resolve-error-after-installing-service-pack}


## Problema   {#issue}

Quando l’utente riavvia AEM Forms, i processi di chiamata correnti continuano comunque, ad esempio il rendering di documenti PDF e altro ancora. In questo modo il riavvio del server AEM Forms non viene avviato correttamente.

## Applicabile a {#applies-to}

La soluzione si applica ad AEM Forms sul server JEE e AEM Forms sul server OSGi.

## Soluzione {#solution}

Per risolvere il problema, aggiungi un argomento `Dcom.adobe.livecycle.dsc.deferServiceStart=true` a [file batch](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/command-line-start-and-stop.html#windows-platform-start-bat-script-example) durante l&#39;avvio del server.
