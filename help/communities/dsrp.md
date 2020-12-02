---
title: DSRP - Provider di risorse di archiviazione del database relazionale
seo-title: DSRP - Provider di risorse di archiviazione del database relazionale
description: Imposta  AEM Communities per utilizzare un database relazionale come store comune
seo-description: Imposta  AEM Communities per utilizzare un database relazionale come store comune
uuid: f364e7da-ee54-4ab2-a630-7ec9239005ac
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: d23acb18-6761-4290-9e7a-a434582791bd
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 3%

---


# DSRP - Provider risorse di archiviazione del database relazionale {#dsrp-relational-database-storage-resource-provider}

## Informazioni su DSRP {#about-dsrp}

Se  AEM Communities è configurato per utilizzare un database relazionale come store comune, il contenuto generato dall’utente (UGC) è accessibile da tutte le istanze di creazione e pubblicazione senza la necessità di eseguire la sincronizzazione o la replica.

Vedere anche [Caratteristiche delle opzioni SRP](working-with-srp.md#characteristics-of-srp-options) e [Topologie consigliate](topologies.md).

## Requisiti {#requirements}

* [MySQL](#mysql-configuration), un database relazionale.
* [Apache Solr](#solr-configuration), una piattaforma di ricerca.

>[!NOTE]
>
>La configurazione di archiviazione predefinita ora è memorizzata nel percorso conf(`/conf/global/settings/community/srpc/defaultconfiguration`) invece del percorso etc (`/etc/socialconfig/srpc/defaultconfiguration`). Si consiglia di seguire le [fasi di migrazione](#zerodt-migration-steps) per eseguire le operazioni predefinite come previsto.

## Configurazione database relazionale {#relational-database-configuration}

### Configurazione MySQL {#mysql-configuration}

Un&#39;installazione MySQL può essere condivisa tra le funzioni di abilitazione e lo store comune (DSRP) all&#39;interno dello stesso pool di connessioni utilizzando nomi di database (schema) diversi e connessioni diverse (server:port).

Per informazioni sull&#39;installazione e la configurazione, vedere [Configurazione MySQL per DSRP](dsrp-mysql.md).

### Configurazione Solr {#solr-configuration}

Un&#39;installazione Solr può essere condivisa tra l&#39;archivio nodi (Oak) e lo store comune (SRP) utilizzando raccolte diverse.

Se le raccolte Oak e SRP vengono utilizzate intensamente, per motivi di prestazioni potrebbe essere installato un secondo Solr.

Per gli ambienti di produzione, la modalità SolrCloud offre prestazioni migliori rispetto alla modalità standalone (una singola configurazione Solr locale).

Per informazioni sull&#39;installazione e la configurazione, vedere [Configurazione Solr per SRP](solr.md).

### Seleziona DSRP {#select-dsrp}

La [console di configurazione dell&#39;archivio](srp-config.md) consente di selezionare la configurazione di storage predefinita, che identifica l&#39;implementazione dell&#39;SRP da utilizzare.

Per accedere alla console di configurazione dell&#39;archivio, all&#39;autore

* Accesso con privilegi di amministratore
* Dal **menu principale**

   * Selezionare **[!UICONTROL Strumenti]** (dal riquadro a sinistra)
   * Selezionare **[!UICONTROL Communities]**
   * Selezionare **[!UICONTROL Configurazione archiviazione]**

      * Ad esempio, la posizione risultante è: [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp)
      >[!NOTE]
      >
      >La configurazione di archiviazione predefinita ora è memorizzata nel percorso conf(`/conf/global/settings/community/srpc/defaultconfiguration`)      invece del percorso etc (`/etc/socialconfig/srpc/defaultconfiguration`). Si consiglia di seguire le [fasi di migrazione](#zerodt-migration-steps) per eseguire le operazioni predefinite come previsto.
   ![dsrp-config](assets/dsrp-config.png)

* Selezionare **[!UICONTROL Database Storage Resource Provider (DSRP)]**
* **Configurazione database**

   * **[!UICONTROL Nome origine dati JDBC]**

      Il nome assegnato alla connessione MySQL deve essere uguale a quello immesso nella configurazione [JDBC OSGi](dsrp-mysql.md#configurejdbcconnections)

      *predefinito*: community

   * **[!UICONTROL Nome database]**

      Nome assegnato allo schema nello script [init_schema.sql](dsrp-mysql.md#obtain-the-sql-script)

      *predefinito*: community

* **SolrConfiguration**

   * **[](https://cwiki.apache.org/confluence/display/solr/Using+ZooKeeper+to+Manage+Configuration+Files)Zookeeper Host**

      Lasciate vuoto questo valore se eseguite Solr utilizzando ZooKeeper interno. In caso contrario, in modalità [SolrCloud](solr.md#solrcloud-mode) con ZooKeeper esterno, imposta questo valore sull&#39;URI per ZooKeeper, ad esempio *my.server.com:80*

      *predefinito*:  *&lt;blank>*

   * **[!UICONTROL URL di Solr]**

      *predefinito*: https://127.0.0.1:8983/solr/

   * **[!UICONTROL Collezione Solr]**

      *predefinito*: collection1

* Seleziona **[!UICONTROL Invia]**.

### Zero passaggi di migrazione dei tempi di inattività per impostazione predefinita {#zerodt-migration-steps}

Seguite i passaggi per assicurarvi che la pagina srultsrp predefinita [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp) funzioni come previsto:

1. Rinominare il percorso in `/etc/socialconfig` in `/etc/socialconfig_old`, in modo che la configurazione del sistema torni a jsrp (impostazione predefinita).
1. Passate alla pagina [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp) predefinita, in cui è configurato jsrp. Fare clic sul pulsante **[!UICONTROL submit]** in modo che venga creato un nuovo nodo di configurazione predefinito in `/conf/global/settings/community/srpc`.
1. Eliminate la configurazione predefinita creata `/conf/global/settings/community/srpc/defaultconfiguration`.
1. Copiate la precedente configurazione `/etc/socialconfig_old/srpc/defaultconfiguration` al posto del nodo eliminato (`/conf/global/settings/community/srpc/defaultconfiguration`) nel passaggio precedente.
1. Eliminare il vecchio nodo etc `/etc/socialconfig_old`.

## Pubblicazione della configurazione {#publishing-the-configuration}

DSRP deve essere identificato come store comune in tutte le istanze di creazione e pubblicazione.

Per rendere disponibile la stessa configurazione nell’ambiente di pubblicazione:

* Per autore:

   * Passare dal menu principale a **[!UICONTROL Strumenti]** > **[!UICONTROL Operazioni]** > **[!UICONTROL Replica]**
   * Fate doppio clic su **[!UICONTROL Attiva albero]**
   * **Percorso iniziale**:

      * Passa a `/etc/socialconfig/srpc/`
   * Assicurarsi che `Only Modified` non sia selezionato.
   * Selezionare **[!UICONTROL Activate]**.


## Gestione dei dati utente {#managing-user-data}

Per informazioni relative a *utenti*, *profili utente* e *gruppi di utenti*, spesso inseriti nell&#39;ambiente di pubblicazione, visita:

* [Sincronizzazione utente](sync.md)
* [Gestione di utenti e gruppi di utenti](users.md)

## Solr di reindicizzazione per DSRP {#reindexing-solr-for-dsrp}

Per reindicizzare DSRP Solr, seguite la documentazione relativa a [reindicizzazione MSRP](msrp.md#msrp-reindex-tool), tuttavia, durante la reindicizzazione per DSRP, utilizzate questo URL: **/services/social/datastore/rdb/reindex**

Ad esempio, un comando curl per reindicizzare DSRP sarà simile al seguente:

```shell
curl -u admin:password -X POST -F path=/ https://host:port/services/social/datastore/rdb/reindex
```

