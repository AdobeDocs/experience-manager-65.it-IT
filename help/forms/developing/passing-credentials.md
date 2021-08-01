---
title: Come passare le credenziali utilizzando le intestazioni WS-security?
description: Scopri come trasmettere le credenziali utilizzando le intestazioni di sicurezza WS
source-git-commit: 9b118ef4f852e3df1e717bb27b9be272caeb0456
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---

# Trasmissione delle credenziali tramite intestazioni WS-Security {#using-execute-script-service-aem-forms-jee-workbench}

Quando si richiama un servizio AEM Forms su JEE utilizzando i servizi web, è possibile utilizzare intestazioni WS-Security per trasmettere le informazioni di autenticazione client richieste da AEM Forms su JEE. WS-Security definisce le estensioni SOAP per implementare l’autenticazione client, la riservatezza dei messaggi e l’integrità dei messaggi. Di conseguenza, puoi richiamare AEM Forms sui servizi JEE quando AEM Forms su JEE viene distribuito come server autonomo o in un ambiente cluster.

La modalità di trasmissione delle intestazioni WS-Security ad AEM Forms su JEE dipende dal fatto che si utilizzano classi Java generate da Axis o un assembly client .NET che consuma lo stack SOAP nativo di un servizio.

>[!NOTE]
>
>Ad esempio, per richiamare un servizio utilizzando intestazioni WS-Security, in questo argomento viene crittografato un documento PDF con una password richiamando il servizio di cifratura.

Questo documento tratta i seguenti argomenti:

* Passaggio dell’autenticazione client tramite classi Java generate da Axis

* Generazione dei file della libreria Axis necessari per richiamare il servizio di crittografia

* Richiamo del servizio di crittografia tramite un&#39;intestazione WS-Security

* Passaggio dell&#39;autenticazione client tramite un assembly client .NET

* Richiamo del servizio di crittografia tramite un&#39;intestazione WS-Security


## Requisiti {#requirements}

Per sfruttare al meglio questo documento, è necessario avere una solida conoscenza del software AEM Forms on JEE.

>[!MORELIKETHIS]
>
>* [Trasmissione delle credenziali tramite intestazioni WS-Security](assets/passing-credentials-using-ws-security-headers.pdf)


