---
title: '"Database di Microsoft SQL Server: Ottimizzazione della configurazione"'
seo-title: '"Database di Microsoft SQL Server: Ottimizzazione della configurazione"'
description: Scoprite come ottimizzare la configurazione del database Microsoft SQL Server.
seo-description: Scoprite come ottimizzare la configurazione del database Microsoft SQL Server.
uuid: 2d618aab-3c67-4edb-a28f-a20904689e6f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS, SG_AEMFORMS
discoiquuid: 70559a94-42ea-411a-a32f-5f38bc17ff96
translation-type: tm+mt
source-git-commit: a929252a13f66da8ac3e52aea0655b12bdd1425f
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 0%

---


# Database di Microsoft SQL Server: Ottimizzazione della configurazione {#microsoft-sql-server-database-fine-tuning-the-configuration}

Modificare le impostazioni di configurazione predefinite quando si utilizza Microsoft SQL Server. Fare clic con il pulsante destro del mouse sul server locale in  Oracle Enterprise Manager per accedere alla finestra di dialogo delle proprietà.

## Impostazioni memoria {#memory-settings}

Modificate l&#39;allocazione minima di memoria in un numero il più grande possibile. Se il database è in esecuzione su un computer separato, utilizzare tutta la memoria. Le impostazioni predefinite non assegnano in modo aggressivo la memoria, il che ostacola le prestazioni in quasi tutti i database. Si dovrebbe essere più aggressivi nell&#39;allocazione della memoria sulle macchine di produzione.

## Impostazioni processore {#processor-settings}

Modificare le impostazioni del processore e, soprattutto, selezionare la casella di controllo Aumenta priorità SQL Server in Windows in modo che il server utilizzi il maggior numero possibile di cicli. L&#39;impostazione Usa fibre NT è meno importante, ma potrebbe essere utile selezionarla.

## Impostazioni database {#database-settings}

Modificate le impostazioni del database. L&#39;impostazione più importante è l&#39;intervallo di recupero, che specifica la quantità massima di tempo per aspettare il ripristino dopo un arresto anomalo. L’impostazione predefinita è un minuto. L&#39;utilizzo di un valore maggiore, da 5 a 15 minuti, migliora le prestazioni perché offre al server più tempo per scrivere le modifiche dal registro del database nei file del database.

>[!NOTE]
>
>Questa impostazione non compromette il comportamento delle transazioni poiché modifica solo la lunghezza della riproduzione del file di registro che deve essere eseguita all&#39;avvio.

Impostare la dimensione Spazio allocato sia per il registro che per il file di dati in modo che sia molto più grande del database iniziale. Considerate quanto può crescere il database in un anno. Idealmente, i file di registro e di dati sono allocati in modo contiguo in modo che i dati non finiscano frammentati su tutto il disco.
