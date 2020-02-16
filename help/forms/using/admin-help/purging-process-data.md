---
title: Rimozione dei dati del processo
seo-title: Rimozione dei dati del processo
description: I dati di processo generati quando viene richiamato un processo di lunga durata possono diventare troppo grandi, con conseguente riduzione delle prestazioni dei moduli AEM e dell’utilizzo di spazio su disco non necessario. Scopri come eliminare i dati del processo.
seo-description: I dati di processo generati quando viene richiamato un processo di lunga durata possono diventare troppo grandi, con conseguente riduzione delle prestazioni dei moduli AEM e dell’utilizzo di spazio su disco non necessario. Scopri come eliminare i dati del processo.
uuid: 2f04452c-71c6-452c-88c2-7560d35e7dec
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 3157bb92-4b07-40f2-be4c-8f5807f9a380
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Rimozione dei dati del processo {#purging-process-data}

I dati di processo generati quando viene richiamato un processo di lunga durata possono diventare troppo grandi, con conseguente riduzione delle prestazioni dei moduli AEM e dell’utilizzo di spazio su disco non necessario. È buona norma eliminare i dati di processo quando i record non sono più necessari. I moduli AEM forniscono diversi strumenti per eliminare i dati del processo:

* È possibile utilizzare la console di amministrazione per eseguire una rimozione una tantum di record obsoleti relativi a processi longevi o per pianificare regolarmente le eliminazioni automatiche. (vedere [Eliminare i record dal database](/help/forms/using/admin-help/purge-records-job-manager-database.md#purge-records-from-the-job-manager-database)di Gestione processi.)
* Puoi utilizzare l’API Java dei moduli AEM e l’API dei servizi Web per eliminare programmaticamente i dati di processo relativi a processi longevi. (Vedere &quot;Rimozione dei dati del processo&quot; nella [programmazione con i moduli](https://www.adobe.com/go/learn_aemforms_programming_63)AEM.)
* Utilizzare lo strumento di eliminazione del processo per eliminare i processi in base al nome del processo e ad altri parametri. Per informazioni dettagliate, consultate il file Leggimi dello strumento di eliminazione del processo, situato nella directory principale *[\sdk\misc\Foundation\ProcessPurgeTool\ReadMe.txt di]* aem_forms.

