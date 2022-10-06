---
title: "Database di Microsoft SQL Server: Ottimizzazione della configurazione"
seo-title: "Microsoft SQL Server database: Fine-tuning the configuration"
description: Scopri come ottimizzare la configurazione del database Microsoft SQL Server.
seo-description: Learn how you can fine tune the configuration of your Microsoft SQL Server database.
uuid: 2d618aab-3c67-4edb-a28f-a20904689e6f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS, SG_AEMFORMS
discoiquuid: 70559a94-42ea-411a-a32f-5f38bc17ff96
exl-id: 9c570827-86e2-47d5-b8ae-66c0767bff2e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---

# Database Microsoft SQL Server: Ottimizzazione della configurazione {#microsoft-sql-server-database-fine-tuning-the-configuration}

È necessario modificare le impostazioni di configurazione predefinite quando si utilizza Microsoft SQL Server. Fare clic con il pulsante destro del mouse sul server locale in Oracle Enterprise Manager per accedere alla finestra di dialogo delle proprietà.

## Impostazioni della memoria {#memory-settings}

Modifica l&#39;allocazione minima della memoria in un numero quanto più grande possibile. Se il database è in esecuzione su un computer separato, utilizzare tutta la memoria. Le impostazioni predefinite non allocano in modo aggressivo la memoria, il che ostacola le prestazioni in quasi tutti i database. Dovresti essere più aggressivo nell&#39;allocare la memoria sulle macchine di produzione.

## Impostazioni del processore {#processor-settings}

Modificare le impostazioni del processore e, soprattutto, selezionare la casella di controllo Aumenta la priorità di SQL Server su Windows in modo che il server utilizzi il maggior numero possibile di cicli. L&#39;impostazione Usa fibre NT è meno importante, ma è consigliabile selezionarla.

## Impostazioni del database {#database-settings}

Modificare le impostazioni del database. L&#39;impostazione più importante è l&#39;intervallo di recupero, che specifica la quantità massima di tempo da attendere per il ripristino dopo un arresto anomalo. L&#39;impostazione predefinita è di un minuto. L&#39;utilizzo di un valore più grande, da 5 a 15 minuti, migliora le prestazioni perché dà al server più tempo per scrivere le modifiche dal log del database nei file di database.

>[!NOTE]
>
>Questa impostazione non compromette il comportamento transazionale perché modifica solo la lunghezza della riproduzione del file di registro che deve essere eseguita all’avvio.

Impostare le dimensioni Allocate dello spazio per il registro e il file di dati in modo che siano molto più grandi del database iniziale. Considera quanto il database può crescere in un anno. Idealmente, i file di log e di dati sono allocati in modo contiguo in modo che i dati non finiscano frammentati in tutto il disco.
