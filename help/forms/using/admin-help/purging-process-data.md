---
title: Rimozione dati processo
description: I dati di processo generati quando si richiama un processo di lunga durata possono diventare troppo grandi, con conseguente riduzione delle prestazioni dei moduli AEM e utilizzo di spazio su disco non necessario. Scopri come eliminare i dati del processo.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 0da59dbe-f050-4ee5-b74c-4380b3543b97
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 0%

---

# Rimozione dati processo {#purging-process-data}

I dati di processo generati quando si richiama un processo di lunga durata possono diventare troppo grandi, con conseguente riduzione delle prestazioni dei moduli AEM e utilizzo di spazio su disco non necessario. È buona prassi eliminare i dati del processo quando i record non sono più necessari. I moduli AEM consentono di eliminare i dati di processo in diversi modi:

* È possibile utilizzare la console di amministrazione per eseguire una rimozione unica dei record obsoleti correlati a processi di lunga durata o per pianificare eliminazioni automatiche regolari. (Vedi [Eliminare i record dal database di Gestione processi](/help/forms/using/admin-help/purge-records-job-manager-database.md#purge-records-from-the-job-manager-database).)
* Puoi utilizzare l’API Java e l’API dei servizi web dell’AEM per eliminare a livello di programmazione i dati di processo relativi a processi di lunga durata. (Vedi &quot;Eliminazione dei dati di processo&quot; in [Programmazione con moduli AEM](https://www.adobe.com/go/learn_aemforms_programming_63).)
* Utilizzare lo strumento di rimozione del processo per eliminare i processi in base al nome del processo e ad altri parametri. Per informazioni dettagliate, vedere il file readme dello strumento di eliminazione dei processi, nella directory principale di *[aem_forms]*\sdk\misc\Foundation\ProcessPurgeTool\ReadMe.txt.
