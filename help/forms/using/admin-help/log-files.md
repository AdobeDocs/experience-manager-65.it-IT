---
title: File di registro
description: Eventi quali errori di runtime o di avvio vengono registrati nei file di registro del server applicazioni, che possono essere aperti utilizzando qualsiasi editor di testo.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 23a65be4-3277-4c73-9189-a9b4d7be73cd
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 0%

---

# File di registro {#log-files}

Eventi quali errori di runtime o di avvio vengono registrati nei file di registro del server applicazioni. In caso di problemi di distribuzione nel server applicazioni, è possibile utilizzare i file di registro per individuare il problema. È possibile aprire i file di registro utilizzando qualsiasi editor di testo.

(JBoss) I seguenti file di registro sono in `[appserver root]/server/'server'/log` directory:

* boot.log
* server.log.*[aaaa-mm-gg]*
* server.log

(WebLogic) I file di registro del dominio sono in `[appserverdomain]` e i file di registro del server si trovano nella `[appserverdomain]/servers/[appserver name]/logs` directory:

* `access.log`
* `[appserver name].log`
* `[appserver name].out.[incremental number]`

(WebSphere) I seguenti file di registro sono in `[appserver root]/profiles/default/logs/[appserver name]` directory:

* SystemErr.log
* SystemOut.log
* StartServer.log
