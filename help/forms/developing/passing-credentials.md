---
title: Trasmettere le credenziali utilizzando le intestazioni WS-security
description: Scopri come trasmettere le credenziali utilizzando le intestazioni di sicurezza WS
exl-id: 519d57ad-81ab-4caf-ae25-4390ae2eee13
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Security
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 50158d81-1c06-57f7-8bd7-e8ff76a93f85
    internal-label: Document Security
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
source-wordcount: '228'
ht-degree: 3%
---
# Passaggio delle credenziali tramite intestazioni WS-Security {#using-execute-script-service-aem-forms-jee-workbench}

Quando si richiama un servizio AEM Forms su JEE utilizzando i servizi web, è possibile utilizzare le intestazioni WS-Security per trasmettere le informazioni di autenticazione client richieste da AEM Forms su JEE. WS-Security definisce le estensioni SOAP per implementare l&#39;autenticazione client, la riservatezza dei messaggi e l&#39;integrità dei messaggi. Di conseguenza, puoi richiamare AEM Forms sui servizi JEE quando AEM Forms su JEE viene distribuito come server autonomo o in un ambiente cluster.

La modalità di trasmissione delle intestazioni WS-Security ad AEM Forms su JEE dipende dal fatto che si utilizzino classi Java generate da Axis o assembly client .NET che utilizzano lo stack nativo di SOAP di un servizio.

>[!NOTE]
>
>Come esempio di chiamata di un servizio tramite intestazioni WS-Security, in questo argomento viene crittografato un documento PDF con una password richiamando il servizio Crittografia.

Questo documento tratta i seguenti argomenti:

* Passaggio dell&#39;autenticazione client tramite classi Java generate da Axis

* Generazione dei file della libreria Axis necessari per richiamare il servizio Crittografia

* Richiamare il servizio Encryption utilizzando un&#39;intestazione WS-Security

* Passaggio dell&#39;autenticazione client tramite un assembly client .NET

* Richiamare il servizio Encryption utilizzando un&#39;intestazione WS-Security


## Requisiti {#requirements}

Per trarre il massimo da questo documento, è necessario avere una solida conoscenza del software AEM Forms su JEE.

>[!MORELIKETHIS]
>
>* [Passaggio delle credenziali tramite intestazioni WS-Security](assets/passing-credentials-using-ws-security-headers.pdf)
