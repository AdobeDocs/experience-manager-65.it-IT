---
title: "Database IBM DB2: esecuzione di comandi per manutenzione regolare"
description: In questo documento sono elencati i comandi di IBM DB2 consigliati per la manutenzione regolare del database dei moduli AEM.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 7a4281e7-1544-473a-a471-e9a4c2819a58
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 0%

---

# Database IBM DB2: esecuzione di comandi per manutenzione regolare {#ibm-db-database-running-commands-for-regular-maintenance}

I seguenti comandi di IBM DB2 sono consigliati per la manutenzione regolare del database dei moduli AEM. Per informazioni dettagliate sulla manutenzione e l&#39;ottimizzazione delle prestazioni per il database DB2, vedere *IBM DB2 Administration Guide*.

* **runstats:** Questo comando aggiorna le statistiche che descrivono le caratteristiche fisiche di una tabella di database, insieme ai relativi indici associati. Le istruzioni SQL dinamiche generate dai moduli AEM utilizzano automaticamente queste statistiche aggiornate, ma le istruzioni SQL statiche create all&#39;interno di un database richiedono l&#39;esecuzione anche del comando `db2rbind`.
* **db2rbind:** Questo comando riassocia tutti i pacchetti nel database. Utilizzare questo comando dopo aver eseguito l&#39;utilità `runstats` per riconvalidare tutti i pacchetti nel database.
* **riorganizzazione tabella o indice:** Questo comando verifica se è necessaria la riorganizzazione di alcune tabelle e indici.

  Con la crescita e la modifica dei database, il ricalcolo delle statistiche delle tabelle è fondamentale per migliorare le prestazioni del database e deve essere eseguito regolarmente. Questi comandi possono essere eseguiti manualmente utilizzando script o un processo cron.

>[!NOTE]
>
>Prima di eseguire il comando `runstats`, è necessario che il database contenga dati e che sia stata eseguita almeno una sincronizzazione della directory.

Per un database di piccole dimensioni, ad esempio per 10.000 utenti o 2.500 gruppi, è sufficiente richiamare il comando `runstats` per ridurre gli intervalli di sincronizzazione.

Per i database di dimensioni maggiori, ad esempio per 100.000 utenti o 10.000 gruppi, eseguire il comando `reorg` prima di eseguire il comando `runstats`.

## Utilizzare il comando runstats nel database di AEM forms {#use-the-runstats-command-on-your-aem-forms-database}

Eseguire il comando `runstats` sulle tabelle e sugli indici di database AEM forms seguenti.

>[!NOTE]
>
>Il comando `runstats` deve essere eseguito solo durante la prima sincronizzazione del database. Tuttavia, deve essere eseguito due volte durante tale processo: una durante la sincronizzazione di Utenti e gruppi e quindi durante la sincronizzazione di Membri del gruppo. Assicurati che lo script venga eseguito completamente ogni volta che lo esegui.

Per la sintassi e l’utilizzo corretti, consulta la documentazione del produttore del database. Di seguito, `<schema>` viene utilizzato per indicare lo schema associato al nome utente DB2. Se si dispone di una semplice installazione predefinita di DB2, questo è il nome dello schema del database.

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

Eseguire il comando `reorg` sulle tabelle e sugli indici di database AEM forms seguenti. Per la sintassi e l’utilizzo corretti, consulta la documentazione del produttore del database.

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
