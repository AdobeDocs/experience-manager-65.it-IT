---
title: 'Database di Microsoft SQL Server: ottimizzazione della configurazione'
description: Scopri come ottimizzare la configurazione del database di Microsoft SQL Server.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS, SG_AEMFORMS
exl-id: 9c570827-86e2-47d5-b8ae-66c0767bff2e
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
source-wordcount: '299'
ht-degree: 100%
---
# Database di Microsoft SQL Server: ottimizzazione della configurazione {#microsoft-sql-server-database-fine-tuning-the-configuration}

È consigliabile modificare le impostazioni di configurazione predefinite quando si utilizza Microsoft SQL Server. Fai clic con il pulsante destro del mouse sul server locale in Oracle Enterprise Manager per accedere alla finestra di dialogo delle proprietà.

## Impostazioni della memoria {#memory-settings}

Imposta l’allocazione minima della memoria sul numero più grande possibile. Se il database è in esecuzione su un computer separato, utilizza tutta la memoria. Le impostazioni predefinite non allocano in modo deciso la memoria, pertanto le prestazioni vengono ostacolate su quasi tutti i database. L’allocazione della memoria nei computer deve essere più decisa.

## Impostazioni del processore {#processor-settings}

Modifica le impostazioni del processore e, soprattutto, seleziona la casella di controllo Aumenta la priorità di SQL Server su Windows in modo che il server utilizzi il maggior numero di cicli possibile. L’impostazione Usa NT Fibers è meno importante, ma potrebbe essere necessario selezionarla comunque.

## Impostazioni del database {#database-settings}

Modifica le impostazioni del database. L’impostazione più importante è Intervallo di ripristino che specifica il tempo massimo di attesa per il ripristino dopo un arresto anomalo. L’impostazione predefinita è un minuto. L’utilizzo di un valore più grande, da 5 a 15 minuti, migliora le prestazioni perché dà al server più tempo per scrivere le modifiche dal registro del database ai file del database.

>[!NOTE]
>
>Questa impostazione non compromette il comportamento transazionale perché modifica solo la lunghezza della riesecuzione del file di registro che avviene all’avvio.

Imposta la dimensione dello spazio allocato sia per il file di registro sia per il file di dati in modo che sia molto più grande del database iniziale. Prendi in considerazione la possibile crescita del database nell’arco di un anno. Idealmente, i file di registro e di dati sono allocati in un’estensione contigua in modo che i dati non vengano frammentati su tutto il disco.
