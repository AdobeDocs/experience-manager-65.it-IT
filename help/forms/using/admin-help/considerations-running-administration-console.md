---
title: Considerazioni durante l’esecuzione di Administration Console
description: In questo documento sono elencati alcuni punti da considerare durante l'esecuzione di Administration Console.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: e15dae6f-d30d-4770-a5ca-34f522a01d31
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
source-wordcount: '147'
ht-degree: 8%
---
# Considerazioni durante l’esecuzione di Administration Console {#considerations-when-running-administrationconsole}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

Di seguito sono riportati alcuni aspetti da considerare durante l’esecuzione di Administration Console:

* Se si accede alla console di amministrazione utilizzando l&#39;URL `https://[hostname]:'port'/adminui`, il nome host specificato non può contenere caratteri di sottolineatura. In caso contrario, i collegamenti ad alcune aree della console di amministrazione potrebbero non funzionare correttamente.
* Se si esegue una console di amministrazione in Esplora risorse su un sistema operativo giapponese, è possibile che si verifichino i seguenti problemi:

  * Facendo clic su un collegamento si ritorna alla pagina di accesso anziché al collegamento previsto.
  * Quando si fa clic su un collegamento, viene visualizzato un errore di autorizzazione.

  La best practice prevede di eseguire la console di amministrazione da un altro browser, come Mozilla Firefox, per garantire che nessun collegamento non riesca.

* Non utilizzare i caratteri barra rovesciata () durante l’esecuzione di ricerche nella console di amministrazione.
