---
title: Considerazioni sull’esecuzione di AdministrationConsole
seo-title: Considerations when running AdministrationConsole
description: In questo documento sono elencati alcuni punti da considerare durante l'esecuzione della console di amministrazione.
seo-description: This document lists a few points to consider when running Administration Console.
uuid: e260f187-4728-44f3-a5c1-7388ff3965c4
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 525c4afc-e109-4546-b78c-1efee63edc43
exl-id: e15dae6f-d30d-4770-a5ca-34f522a01d31
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 0%

---

# Considerazioni sull’esecuzione della console di amministrazione {#considerations-when-running-administrationconsole}

Di seguito sono riportati alcuni aspetti da considerare durante l’esecuzione della console di amministrazione:

* Se accedi alla console di amministrazione utilizzando l’URL `https://[hostname]:'port'/adminui`, il nome host specificato non può contenere caratteri di sottolineatura. In caso contrario, i collegamenti ad alcune aree della console di amministrazione potrebbero non funzionare correttamente.
* Se si esegue la console di amministrazione in Esplora risorse su un sistema operativo giapponese, è possibile che si verifichino i seguenti problemi:

   * Facendo clic su un collegamento si torna alla pagina di accesso anziché al collegamento previsto.
   * Facendo clic su un collegamento viene visualizzato un errore di autorizzazione.

   Si consiglia di eseguire la console di amministrazione da un altro browser, ad esempio Mozilla Firefox, per garantire che nessun collegamento abbia esito negativo.

* Non utilizzare i caratteri barra rovesciata () quando si eseguono ricerche nella console di amministrazione.
