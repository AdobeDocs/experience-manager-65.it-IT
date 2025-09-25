---
title: Rimozione dei dati di processo
description: I dati di processo generati quando viene richiamato un processo di lunga durata possono assumere dimensioni eccessive, con conseguente riduzione delle prestazioni dei moduli AEM e utilizzo di spazio su disco non necessario. Scopri come eliminare i dati di processo.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 0da59dbe-f050-4ee5-b74c-4380b3543b97
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '199'
ht-degree: 100%

---

# Rimozione dei dati di processo {#purging-process-data}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

I dati di processo generati quando viene richiamato un processo di lunga durata possono assumere dimensioni eccessive, con conseguente riduzione delle prestazioni dei moduli AEM e utilizzo di spazio su disco non necessario. È buona norma eliminare i dati del processo quando i record non sono più necessari. AEM Forms fornisce diversi metodi per eliminare i dati di processo:

* È possibile utilizzare la console di amministrazione per eseguire una rimozione unica dei record obsoleti correlati a processi di lunga durata o per pianificare eliminazioni automatiche regolari. (Consulta [Eliminare i record dal database di Gestione processi](/help/forms/using/admin-help/purge-records-job-manager-database.md#purge-records-from-the-job-manager-database).)
* È possibile utilizzare l’API Java e l’API del servizio web di AEM Forms per eliminare a livello di programmazione i dati di processo relativi ai processi di lunga durata. (Consulta “Rimozione dei dati di processo” in [Programmazione con AEM forms](https://www.adobe.com/go/learn_aemforms_programming_63_it).)
* Utilizza lo strumento di rimozione del processo per eliminare i processi in base al nome del processo e ad altri parametri. Per informazioni dettagliate, consulta il file readme dello strumento di eliminazione dei processi, nella directory principale di *[aem_forms]*\sdk\misc\Foundation\ProcessPurgeTool\ReadMe.txt.
