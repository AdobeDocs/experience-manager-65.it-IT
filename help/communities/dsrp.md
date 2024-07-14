---
title: DSRP - Provider risorsa di archiviazione database relazionale
description: Impostare AEM Communities per l'utilizzo di un database relazionale come archivio comune
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 15b3a594-efde-4702-9233-232ba1c7e5b0
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 0%

---

# DSRP - Provider risorsa di archiviazione database relazionale {#dsrp-relational-database-storage-resource-provider}

## Informazioni su DSRP {#about-dsrp}

Quando AEM Communities è configurato per utilizzare un database relazionale come archivio comune, il contenuto generato dall’utente (UGC, User-Generated Content) è accessibile da tutte le istanze di authoring e pubblicazione senza la necessità di sincronizzazione o replica.

Vedi anche [Caratteristiche delle opzioni SRP](working-with-srp.md#characteristics-of-srp-options) e [topologie consigliate](topologies.md).

## Requisiti {#requirements}

* [MySQL](#mysql-configuration), un database relazionale.
* [Apache Solr](#solr-configuration), una piattaforma di ricerca.

>[!NOTE]
>
>La configurazione di archiviazione predefinita è ora archiviata nel percorso conf(`/conf/global/settings/community/srpc/defaultconfiguration`) invece del percorso `etc` (`/etc/socialconfig/srpc/defaultconfiguration`). Ti consigliamo di seguire i [passaggi della migrazione](#zerodt-migration-steps) per far funzionare defaultsrp come previsto.

## Configurazione database relazionale {#relational-database-configuration}

### Configurazione MySQL {#mysql-configuration}

Un&#39;installazione MySQL può essere condivisa tra le funzionalità di abilitazione e l&#39;archivio comune (DSRP) all&#39;interno dello stesso pool di connessioni utilizzando nomi di database (schema) diversi e anche connessioni diverse (server:porta).

Per informazioni dettagliate sull&#39;installazione e la configurazione, vedere [Configurazione MySQL per DSRP](dsrp-mysql.md).

### Configurazione Solr {#solr-configuration}

Un’installazione Solr può essere condivisa tra l’archivio nodi (Oak) e l’archivio comune (SRP) utilizzando raccolte diverse.

Se entrambe le raccolte Oak e SRP vengono utilizzate in modo intensivo, è possibile installare un secondo Solr per motivi di prestazioni.

Per gli ambienti di produzione, la modalità SolrCloud offre prestazioni migliori rispetto alla modalità standalone (un&#39;unica configurazione Solr locale).

Per informazioni dettagliate sull&#39;installazione e la configurazione, vedere [Configurazione Solr per SRP](solr.md).

### Seleziona DSRP {#select-dsrp}

La [console Configurazione archiviazione](srp-config.md) consente di selezionare la configurazione di archiviazione predefinita, che identifica l&#39;implementazione di SRP da utilizzare.

Per accedere alla console Configurazione archiviazione, dall’autore

* Accedi con privilegi di amministratore
* Dal **menu principale**

   * Seleziona **[!UICONTROL Strumenti]** (dal riquadro a sinistra)
   * Seleziona **[!UICONTROL Community]**
   * Seleziona **[!UICONTROL Configurazione archiviazione]**

      * Ad esempio, la posizione risultante è: [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp)

     >[!NOTE]
     >
     >La configurazione di archiviazione predefinita è ora archiviata nel percorso conf(`/conf/global/settings/community/srpc/defaultconfiguration`)      invece del percorso `etc` (`/etc/socialconfig/srpc/defaultconfiguration`). Ti consigliamo di seguire i [passaggi della migrazione](#zerodt-migration-steps) per far funzionare defaultsrp come previsto.

  ![dsrp-config](assets/dsrp-config.png)

* Seleziona **[!UICONTROL Provider risorsa di archiviazione database (DSRP)]**
* **Configurazione database**

   * **[!UICONTROL Nome origine dati JDBC]**

     Il nome assegnato alla connessione MySQL deve corrispondere a quello immesso nella [configurazione OSGi JDBC](dsrp-mysql.md#configurejdbcconnections)

     *default*: community

   * **[!UICONTROL Nome database]**

     Nome assegnato allo schema nello script [init_schema.sql](dsrp-mysql.md#obtain-the-sql-script)

     *default*: community

* **SolrConfiguration**

   * **[Zookeeper](https://solr.apache.org/guide/6_6/using-zookeeper-to-manage-configuration-files.html) Host**

     Lascia vuoto questo valore se esegui Solr utilizzando lo ZooKeeper interno. Altrimenti, quando l&#39;esecuzione avviene in [modalità SolrCloud](solr.md#solrcloud-mode) con un ZooKeeper esterno, impostare questo valore sull&#39;URI per lo ZooKeeper, ad esempio *my.server.com:80*

     *predefinito*: *&lt;vuoto>*

   * **[!UICONTROL URL Solr]**

     *predefinito*: https://127.0.0.1:8983/solr/

   * **[!UICONTROL Raccolta Solr]**

     *default*: collection1

* Seleziona **[!UICONTROL Invia]**.

### Nessuna fase di migrazione dei tempi di inattività per defaultsrp {#zerodt-migration-steps}

Per garantire che la pagina defaultsrp [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp) funzioni come previsto, eseguire la procedura seguente:

1. Rinomina il percorso in `/etc/socialconfig` in `/etc/socialconfig_old`, in modo che la configurazione di sistema torni a jsrp(default).
1. Vai alla pagina predefinita [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp), in cui è configurato jsrp. Fare clic sul pulsante **[!UICONTROL invia]** in modo che venga creato il nuovo nodo di configurazione predefinito in `/conf/global/settings/community/srpc`.
1. Eliminare la configurazione predefinita creata `/conf/global/settings/community/srpc/defaultconfiguration`.
1. Copiare la configurazione precedente `/etc/socialconfig_old/srpc/defaultconfiguration` al posto del nodo eliminato (`/conf/global/settings/community/srpc/defaultconfiguration`) nel passaggio precedente.
1. Elimina il nodo `/etc/socialconfig_old` `etc` precedente.

## Pubblicazione della configurazione {#publishing-the-configuration}

DSRP deve essere identificato come archivio comune in tutte le istanze di authoring e pubblicazione.

Per rendere disponibile la configurazione identica nell’ambiente di pubblicazione:

* All’autore:

   * Passa dal menu principale a **[!UICONTROL Strumenti]** > **[!UICONTROL Operazioni]** > **[!UICONTROL Replica]**
   * Fare doppio clic su **[!UICONTROL Attiva struttura]**
   * **Percorso iniziale**:

      * Passa a `/etc/socialconfig/srpc/`

   * Assicurarsi che `Only Modified` non sia selezionato.
   * Seleziona **[!UICONTROL Attiva]**.

## Gestione dei dati utente {#managing-user-data}

Per informazioni relative a *utenti*, *profili utente* e *gruppi di utenti*, spesso immessi nell&#39;ambiente di pubblicazione, visitare:

* [Sincronizzazione utente](sync.md)
* [Gestione di utenti e gruppi di utenti](users.md)

## Reindicizzazione Solr per DSRP {#reindexing-solr-for-dsrp}

Per reindicizzare DSRP Solr, seguire la documentazione per [reindicizzazione MSRP](msrp.md#msrp-reindex-tool). Tuttavia, durante la reindicizzazione per DSRP, utilizzare questo URL: **/services/social/datastore/rdb/reindex**

Ad esempio, un comando curl per reindicizzare DSRP sarà simile al seguente:

```shell
curl -u admin:password -X POST -F path=/ https://host:port/services/social/datastore/rdb/reindex
```
