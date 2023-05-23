---
title: "Database IBM DB2: esecuzione di comandi per manutenzione regolare"
seo-title: "IBM DB2 database: Running commands for regular maintenance"
description: In questo documento sono elencati i comandi di IBM DB2 consigliati per la manutenzione regolare del database dei moduli AEM.
seo-description: This document lists IBM DB2 commands that are recommended for regular maintenance of your AEM forms database.
uuid: 235d59df-b9b9-4770-8b7d-00713701c3c2
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a62b68b4-7735-49b1-8938-f0d9e4c4a051
exl-id: 7a4281e7-1544-473a-a471-e9a4c2819a58
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 0%

---

# Database IBM DB2: esecuzione di comandi per manutenzione regolare {#ibm-db-database-running-commands-for-regular-maintenance}

I seguenti comandi di IBM DB2 sono consigliati per la manutenzione regolare del database dei moduli AEM. Per informazioni dettagliate sulla manutenzione e l&#39;ottimizzazione delle prestazioni per il database DB2, vedere *Guida all&#39;amministrazione di IBM DB2*.

* **runstats:** Questo comando aggiorna le statistiche che descrivono le caratteristiche fisiche di una tabella di database, insieme ai relativi indici associati. Le istruzioni SQL dinamiche generate dai moduli AEM utilizzano automaticamente queste statistiche aggiornate, ma le istruzioni SQL statiche generate all&#39;interno di un database richiedono che `db2rbind` di esecuzione.
* **db2rbind:** Questo comando esegue il rebinding di tutti i pacchetti nel database. Usa questo comando dopo l&#39;esecuzione di `runstats` per riconvalidare tutti i pacchetti nel database.
* **riorganizzare la tabella o l&#39;indice:** Questo comando controlla se è necessaria la riorganizzazione di alcune tabelle e indici.

   Con la crescita e la modifica dei database, il ricalcolo delle statistiche delle tabelle è fondamentale per migliorare le prestazioni del database e deve essere eseguito regolarmente. Questi comandi possono essere eseguiti manualmente utilizzando script o un processo cron.

>[!NOTE]
>
>Prima di eseguire `runstats` , il database deve contenere dati e deve essere stata eseguita almeno una sincronizzazione della directory.

Per un database di piccole dimensioni, ad esempio per 10.000 utenti o 2.500 gruppi, è sufficiente invocare `runstats` per ridurre gli intervalli di sincronizzazione.

Per i database di grandi dimensioni, ad esempio per 100.000 utenti o 10.000 gruppi, eseguire il comando `reorg` prima di eseguire `runstats` comando.

## Utilizzare il comando runstats nel database di AEM forms {#use-the-runstats-command-on-your-aem-forms-database}

Esegui il `runstats` nelle tabelle e negli indici di database di AEM forms seguenti.

>[!NOTE]
>
>Il `runstats` il comando deve essere eseguito solo durante la prima sincronizzazione del database. Tuttavia, deve essere eseguito due volte durante tale processo: una durante la sincronizzazione di Utenti e gruppi e quindi durante la sincronizzazione di Membri del gruppo. Assicurati che lo script venga eseguito completamente ogni volta che lo esegui.

Per la sintassi e l’utilizzo corretti, consulta la documentazione del produttore del database. Sotto, `<schema>` viene utilizzato per indicare lo schema associato al nome utente DB2. Se si dispone di una semplice installazione predefinita di DB2, questo è il nome dello schema del database.

```sql
     TABLE <schema>.EDCPRINCIPALGROUPENTITY
 
     TABLE <schema>.EDCPRINCIPALGRPCTMNTENTITY
 
     TABLE <schema>.EDCPRINCIPALENTITY
 
     TABLE <schema>.EDCPRINCIPALUSERENTITY
 
     TABLE <schema>.EDCPRINCIPALEMAILALIASENTITY
 
     TABLE <schema>.EDCPRINCIPALENTITY FOR INDEXES ALL
 
     TABLE <schema>.EDCPRINCIPALEMAILALIASENTITY FOR INDEXES ALL
 
     TABLE <schema>.EDCPRINCIPALUSERENTITY FOR INDEXES ALL
 
     TABLE <schema>.EDCPRINCIPALGROUPENTITY FOR INDEXES ALL
 
     TABLE <schema>.EDCPRINCIPALGRPCTMNTENTITY FOR INDEXES ALL
```

## Eseguire il comando di riorganizzazione nel database dei moduli AEM {#run-the-reorg-command-on-your-aem-forms-database}

Esegui il `reorg` nelle tabelle e negli indici di database di AEM forms seguenti. Per la sintassi e l’utilizzo corretti, consulta la documentazione del produttore del database.

```sql
     TABLE <schema>.EDCPRINCIPALGROUPENTITY
 
     TABLE <schema>.EDCPRINCIPALGRPCTMNTENTITY
 
     TABLE <schema>.EDCPRINCIPALENTITY
 
     TABLE <schema>.EDCPRINCIPALUSERENTITY
 
     TABLE <schema>.EDCPRINCIPALEMAILALIASENTITY
 
     INDEXES ALL FOR TABLE <schema>.EDCPRINCIPALENTITY
 
     INDEXES ALL FOR TABLE <schema>.EDCPRINCIPALEMAILALIASENTITY
 
     INDEXES ALL FOR TABLE <schema>.EDCPRINCIPALUSERENTITY
 
     INDEXES ALL FOR TABLE <schema>.EDCPRINCIPALGROUPENTITY
 
     INDEXES ALL FOR TABLE <schema>.EDCPRINCIPALGRPCTMNTENTITY
```
