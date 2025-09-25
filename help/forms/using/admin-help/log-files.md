---
title: File di registro
description: Eventi quali errori di runtime o di avvio vengono registrati nei file di registro del server applicazioni, che possono essere aperti utilizzando qualsiasi editor di testo.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 23a65be4-3277-4c73-9189-a9b4d7be73cd
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: ht
source-wordcount: '115'
ht-degree: 100%

---

# File di registro {#log-files}

Eventi quali errori di runtime o di avvio vengono registrati nei file di registro del server applicazioni. In caso di problemi relativi all’implementazione nel server applicazioni, è possibile utilizzare i file di registro per aiutarti a individuare il problema. È possibile aprire i file di registro utilizzando qualsiasi editor di testo.

(JBoss) I seguenti file di registro si trovano nella directory `[appserver root]/server/'server'/log`:

* boot.log
* server.log.*[dd/mm/yyyy]*
* server.log

(WebLogic) I file di registro del dominio si trovano nella directory `[appserverdomain]` e i file di registro del server si trovano nella directory `[appserverdomain]/servers/[appserver name]/logs`:

* `access.log`
* `[appserver name].log`
* `[appserver name].out.[incremental number]`

(WebSphere) I seguenti file di registro si trovano nella directory `[appserver root]/profiles/default/logs/[appserver name]`:

* SystemErr.log
* SystemOut.log
* StartServer.log
