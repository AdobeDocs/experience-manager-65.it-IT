---
title: File di registro
seo-title: File di registro
description: Eventi quali errori di esecuzione o di avvio vengono registrati nei file di registro del server applicazione, che possono essere aperti utilizzando qualsiasi editor di testo.
seo-description: Eventi quali errori di esecuzione o di avvio vengono registrati nei file di registro del server applicazione, che possono essere aperti utilizzando qualsiasi editor di testo.
uuid: 6ed9fdcd-ff02-4b35-893f-09261a6a557a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: cf140483-470f-4bff-8870-304207508aab
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 0%

---


# File di registro {#log-files}

Eventi quali errori di esecuzione o di avvio vengono registrati nei file di registro del server dell&#39;applicazione. In caso di problemi durante l&#39;implementazione nel server dell&#39;applicazione, è possibile utilizzare i file di registro per individuare il problema. Potete aprire i file di registro utilizzando un editor di testo qualsiasi.

(JBoss) I seguenti file di registro si trovano nella directory `[appserver root]/server/'server'/log`:

* boot.log
* server.log.*[aaaa-mm-gg]*
* server.log

(WebLogic) I file di registro del dominio si trovano nella directory `[appserverdomain]` e i file di registro del server si trovano nella directory `[appserverdomain]/servers/[appserver name]/logs`:

* `access.log`
* `[appserver name].log`
* `[appserver name].out.[incremental number]`

(WebSphere) I seguenti file di registro si trovano nella directory `[appserver root]/profiles/default/logs/[appserver name]`:

* SystemErr.log
* SystemOut.log
* StartServer.log

