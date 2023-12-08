---
title: L’esecuzione di più servizi nonostante AEM Forms non è stata avviata.
description: Anche se AEM Forms non è stato avviato completamente, elabora più servizi.
source-git-commit: 6b24067c1808475044a612f21d5d4d2793c13e17
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 4%

---

# L’esecuzione di più servizi nonostante AEM Forms non è stata avviata completamente{#steps-to-resolve-error-after-installing-service-pack}


## Problema   {#issue}

Quando l’utente riavvia AEM Forms, i processi di chiamata correnti continuano comunque, ad esempio il rendering di documenti PDF e altro ancora. In questo modo il riavvio del server AEM Forms non viene avviato correttamente.

## Applicabile a {#applies-to}

La soluzione si applica ad AEM Forms sul server JEE e AEM Forms sul server OSGi.

## Soluzione {#solution}

Per risolvere il problema, gli utenti aggiungono un argomento `Dcom.adobe.livecycle.dsc.deferServiceStart=true` a [file batch](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/command-line-start-and-stop.html#windows-platform-start-bat-script-example) durante l&#39;avvio del server.





