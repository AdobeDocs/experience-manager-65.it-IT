---
title: "Database di Microsoft SQL Server: ottimizzazione della configurazione"
description: Scopri come ottimizzare la configurazione del database di Microsoft SQL Server.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS, SG_AEMFORMS
exl-id: 9c570827-86e2-47d5-b8ae-66c0767bff2e
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 0%

---

# Database di Microsoft SQL Server: ottimizzazione della configurazione {#microsoft-sql-server-database-fine-tuning-the-configuration}

È consigliabile modificare le impostazioni di configurazione predefinite quando si utilizza Microsoft SQL Server. Fare clic con il pulsante destro del mouse sul server locale in Oracle Enterprise Manager per accedere alla finestra di dialogo delle proprietà.

## Impostazioni della memoria {#memory-settings}

Impostare l&#39;allocazione minima della memoria su un numero il più grande possibile. Se il database è in esecuzione su un computer separato, utilizzare tutta la memoria. Le impostazioni predefinite non allocano in modo aggressivo la memoria, il che ostacola le prestazioni su quasi tutti i database. Deve essere più aggressivo nell’allocare memoria sui macchinari di produzione.

## Impostazioni processore {#processor-settings}

Modificare le impostazioni del processore e, soprattutto, selezionare la casella di controllo Aumenta priorità SQL Server in Windows in modo che il server utilizzi il maggior numero di cicli possibile. L&#39;impostazione Usa fibre NT è meno importante, ma potrebbe essere necessario selezionarla.

## Impostazioni del database {#database-settings}

Modificare le impostazioni del database. L&#39;impostazione più importante è Intervallo di ripristino, che specifica il tempo massimo di attesa del ripristino dopo un arresto anomalo. L&#39;impostazione predefinita è un minuto. L&#39;utilizzo di un valore più grande, da 5 a 15 minuti, migliora le prestazioni perché consente al server di disporre di più tempo per scrivere le modifiche dal log del database nei file del database.

>[!NOTE]
>
>Questa impostazione non compromette il comportamento transazionale perché modifica solo la lunghezza della ripetizione del file di log che deve essere eseguita all&#39;avvio.

Impostare la dimensione Spazio allocato sia per il file di log che per il file di dati in modo che sia molto più grande del database iniziale. Considera la crescita del database nell&#39;arco di un anno. Idealmente, i file di registro e i file di dati vengono allocati in un&#39;estensione contigua in modo che i dati non finiscano frammentati su tutto il disco.
