---
title: File di registro
seo-title: Log files
description: Eventi quali errori di runtime o di avvio vengono registrati nei file di registro del server applicazioni, che possono essere aperti utilizzando qualsiasi editor di testo.
seo-description: Events such as run-time or startup errors are recorded to the application server log files, which can be  opened using any text editor.
uuid: 6ed9fdcd-ff02-4b35-893f-09261a6a557a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: cf140483-470f-4bff-8870-304207508aab
exl-id: 23a65be4-3277-4c73-9189-a9b4d7be73cd
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 0%

---

# File di registro {#log-files}

Eventi quali errori di runtime o di avvio vengono registrati nei file di registro del server applicazioni. In caso di problemi di distribuzione nel server applicazioni, è possibile utilizzare i file di registro per individuare il problema. È possibile aprire i file di registro utilizzando qualsiasi editor di testo.

(JBoss) I seguenti file di registro si trovano nella `[appserver root]/server/'server'/log` directory:

* boot.log
* server.log.*[aaaa-mm-gg]*
* server.log

(WebLogic) I file di registro del dominio si trovano nel `[appserverdomain]` e i file di registro del server si trovano nella `[appserverdomain]/servers/[appserver name]/logs` directory:

* `access.log`
* `[appserver name].log`
* `[appserver name].out.[incremental number]`

(WebSphere) I seguenti file di registro si trovano nella `[appserver root]/profiles/default/logs/[appserver name]` directory:

* SystemErr.log
* SystemOut.log
* StartServer.log
