---
title: '"Database IBM DB2: Esecuzione di comandi per la manutenzione regolare"'
seo-title: '"Database IBM DB2: Esecuzione di comandi per la manutenzione regolare"'
description: In questo documento sono elencati i comandi IBM DB2 consigliati per la manutenzione regolare del database dei moduli AEM.
seo-description: In questo documento sono elencati i comandi IBM DB2 consigliati per la manutenzione regolare del database dei moduli AEM.
uuid: 235d59df-b9b9-4770-8b7d-00713701c3c2
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a62b68b4-7735-49b1-8938-f0d9e4c4a051
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 0%

---


# Database IBM DB2: Esecuzione di comandi per la manutenzione regolare {#ibm-db-database-running-commands-for-regular-maintenance}

I seguenti comandi IBM DB2 sono consigliati per la manutenzione regolare del database dei moduli AEM. Per informazioni dettagliate sulla manutenzione e l&#39;ottimizzazione delle prestazioni per il database DB2, vedere *Guida all&#39;amministrazione DB2 di IBM*.

* **runstats:** Questo comando aggiorna le statistiche che descrivono le caratteristiche fisiche di una tabella di database, insieme ai relativi indici associati. Le istruzioni SQL dinamiche generate dai moduli utilizzano automaticamente queste statistiche aggiornate, ma le istruzioni SQL statiche create all&#39;interno di un database richiedono l&#39;esecuzione anche del comando `db2rbind`.
* **db2rbind:** questo comando ripristina tutti i pacchetti nel database. Utilizzare questo comando dopo l&#39;esecuzione dell&#39;utility `runstats` per convalidare nuovamente tutti i pacchetti nel database.
* **riorganizzazione tabella o indice:** questo comando controlla se è necessaria una riorganizzazione di alcune tabelle e indici.

   Con la crescita e la modifica dei database, il ricalcolo delle statistiche delle tabelle è fondamentale per migliorare le prestazioni del database e deve essere eseguito regolarmente. Questi comandi possono essere eseguiti manualmente tramite script o tramite un processo cron.

>[!NOTE]
>
>Prima di eseguire il comando `runstats`, il database deve contenere dati e deve essere stata eseguita almeno una sincronizzazione di directory.

Per un database di dimensioni ridotte, ad esempio per 10.000 utenti o 2.500 gruppi, è sufficiente richiamare il comando `runstats` per ridurre i tempi di sincronizzazione.

Per i database di dimensioni maggiori, ad esempio per 100.000 utenti o 10.000 gruppi, eseguire il comando `reorg` prima di eseguire il comando `runstats`.

## Utilizzare il comando runstats nel database dei moduli AEM {#use-the-runstats-command-on-your-aem-forms-database}

Eseguire il comando `runstats` nelle tabelle e negli indici del database dei moduli AEM seguenti.

>[!NOTE]
>
>Il comando `runstats` deve essere eseguito solo durante la prima sincronizzazione del database. Tuttavia, durante tale processo deve essere eseguito due volte: una volta durante la sincronizzazione di Utenti e Gruppi e quindi durante la sincronizzazione dei Membri del Gruppo. Assicurarsi che lo script venga eseguito completamente ogni volta che viene eseguito.

Per una sintassi e un utilizzo corretti, consultate la documentazione del produttore del database. Sotto, `<schema>` è utilizzato per indicare lo schema associato al nome utente DB2. Se si dispone di una semplice installazione DB2 predefinita, si tratta del nome dello schema del database.

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

## Eseguire il comando reorg nel database dei moduli AEM {#run-the-reorg-command-on-your-aem-forms-database}

Eseguire il comando `reorg` nelle tabelle e negli indici del database dei moduli AEM seguenti. Per una sintassi e un utilizzo corretti, consultate la documentazione del produttore del database.

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

