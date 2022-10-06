---
title: "Database IBM DB2: Comandi in esecuzione per la manutenzione regolare"
seo-title: "IBM DB2 database: Running commands for regular maintenance"
description: In questo documento sono elencati i comandi IBM DB2 consigliati per la manutenzione regolare del database dei moduli AEM.
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

# Database IBM DB2: Esecuzione di comandi per la manutenzione regolare {#ibm-db-database-running-commands-for-regular-maintenance}

Per la manutenzione regolare del database dei moduli AEM sono consigliati i seguenti comandi IBM DB2. Per informazioni dettagliate su manutenzione e ottimizzazione delle prestazioni per il database DB2, vedere *Guida all’amministrazione di IBM DB2*.

* **runstats:** Questo comando aggiorna le statistiche che descrivono le caratteristiche fisiche di una tabella di database, insieme ai relativi indici associati. Le istruzioni SQL dinamiche generate dai moduli AEM utilizzano automaticamente queste statistiche aggiornate, ma le istruzioni SQL statiche create all&#39;interno di un database richiedono che `db2rbind` esegui anche il comando .
* **db2rbind:** Questo comando esegue il rebin di tutti i pacchetti nel database. Usa questo comando dopo l&#39;esecuzione del `runstats` Utilità per riconvalidare tutti i pacchetti nel database.
* **riorganizzazione di una tabella o di un indice:** Questo comando controlla se è necessaria una riorganizzazione di alcune tabelle e indici.

   Man mano che i database crescono e cambiano, il ricalcolo delle statistiche delle tabelle è fondamentale per migliorare le prestazioni del database e deve essere eseguito regolarmente. Questi comandi possono essere eseguiti manualmente utilizzando gli script o un cron job.

>[!NOTE]
>
>Prima di eseguire il `runstats` il database deve contenere dati e deve essere stata eseguita almeno una sincronizzazione della directory.

Per un database di piccole dimensioni, ad esempio per 10.000 utenti o 2.500 gruppi, è sufficiente richiamare il `runstats` per ridurre i tempi di sincronizzazione.

Per i database più grandi, ad esempio per 100.000 utenti o 10.000 gruppi, esegui il `reorg` prima di eseguire il comando `runstats` comando.

## Utilizzare il comando runstats nel database dei moduli AEM {#use-the-runstats-command-on-your-aem-forms-database}

Esegui il `runstats` nelle tabelle e negli indici del database dei moduli AEM seguenti.

>[!NOTE]
>
>La `runstats` deve essere eseguito solo durante la prima sincronizzazione del database. Tuttavia, deve essere eseguito due volte durante tale processo: una volta durante la sincronizzazione di Utenti e gruppi e poi durante la sincronizzazione dei membri del gruppo. Assicurati che lo script venga eseguito completamente ogni volta che lo esegui.

Per una sintassi e un utilizzo corretti, consulta la documentazione del produttore del database. Di seguito: `<schema>` viene utilizzato per indicare lo schema associato al nome utente DB2. Se si dispone di una semplice installazione predefinita DB2, questo è il nome dello schema del database.

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

## Esegui il comando di riorganizzazione nel database dei moduli AEM {#run-the-reorg-command-on-your-aem-forms-database}

Esegui il `reorg` nelle tabelle e negli indici del database dei moduli AEM seguenti. Per una sintassi e un utilizzo corretti, consulta la documentazione del produttore del database.

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
