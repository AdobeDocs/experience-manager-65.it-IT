---
title: Rimozione dei dati del processo
seo-title: Rimozione dei dati del processo
description: I dati di processo generati quando viene richiamato un processo di lunga durata possono diventare troppo grandi, riducendo le prestazioni dei moduli AEM e l'uso di spazio su disco non necessario. Scopri come eliminare i dati del processo.
seo-description: I dati di processo generati quando viene richiamato un processo di lunga durata possono diventare troppo grandi, riducendo le prestazioni dei moduli AEM e l'uso di spazio su disco non necessario. Scopri come eliminare i dati del processo.
uuid: 2f04452c-71c6-452c-88c2-7560d35e7dec
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 3157bb92-4b07-40f2-be4c-8f5807f9a380
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---


# Rimozione dei dati del processo {#purging-process-data}

I dati di processo generati quando viene richiamato un processo di lunga durata possono diventare troppo grandi, riducendo le prestazioni dei moduli AEM e l&#39;uso di spazio su disco non necessario. È buona norma eliminare i dati di processo quando i record non sono più necessari. AEM moduli offre diversi metodi per eliminare i dati del processo:

* È possibile utilizzare la console di amministrazione per eseguire una rimozione una tantum di record obsoleti relativi a processi longevi o per pianificare regolarmente le eliminazioni automatiche. (Vedere [Eliminare i record dal database di Job Manager](/help/forms/using/admin-help/purge-records-job-manager-database.md#purge-records-from-the-job-manager-database).)
* È possibile utilizzare l&#39;API Java dei moduli AEM e l&#39;API dei servizi Web per eliminare a livello di programmazione i dati di processo relativi a processi longevi. (Vedere &quot;Rimozione dei dati del processo&quot; in [Programmazione con AEM moduli](https://www.adobe.com/go/learn_aemforms_programming_63).)
* Utilizzare lo strumento di eliminazione del processo per eliminare i processi in base al nome del processo e ad altri parametri. Per informazioni dettagliate, vedere il file Leggimi dello strumento di eliminazione del processo, situato in *[aem_forms root]*\sdk\misc\Foundation\ProcessPurgeTool\ReadMe.txt.

