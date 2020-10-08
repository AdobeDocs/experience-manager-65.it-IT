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


# DSRP - Provider di risorse di archiviazione del database relazionale {#dsrp-relational-database-storage-resource-provider}

## Informazioni su DSRP {#about-dsrp}

Se  AEM Communities è configurato per utilizzare un database relazionale come store comune, il contenuto generato dall’utente (UGC) è accessibile da tutte le istanze di creazione e pubblicazione senza la necessità di eseguire la sincronizzazione o la replica.

Vedere anche [Caratteristiche delle opzioni](working-with-srp.md#characteristics-of-srp-options) SRP e topologie [](topologies.md)consigliate.

## Requisiti {#requirements}

* [MySQL](#mysql-configuration), un database relazionale.
* [Apache Solr](#solr-configuration), una piattaforma di ricerca.

>[!NOTE]
>
>La configurazione di storage predefinita ora è memorizzata nel percorso (`/conf/global/settings/community/srpc/defaultconfiguration`) conf anziché nel percorso (`/etc/socialconfig/srpc/defaultconfiguration`) etc. È consigliabile seguire i passaggi [di](#zerodt-migration-steps) migrazione per fare in modo che i predefiniti funzionino come previsto.

## Configurazione database relazionale {#relational-database-configuration}

### Configurazione MySQL {#mysql-configuration}

Un&#39;installazione MySQL può essere condivisa tra le funzioni di abilitazione e lo store comune (DSRP) all&#39;interno dello stesso pool di connessioni utilizzando nomi di database (schema) diversi e connessioni diverse (server:port).

Per i dettagli di installazione e configurazione, consultate Configurazione [MySQL per DSRP](dsrp-mysql.md).

### Configurazione Solr {#solr-configuration}

Un&#39;installazione Solr può essere condivisa tra l&#39;archivio nodi (Oak) e lo store comune (SRP) utilizzando raccolte diverse.

Se le raccolte Oak e SRP vengono utilizzate intensamente, per motivi di prestazioni potrebbe essere installato un secondo Solr.

Per gli ambienti di produzione, la modalità SolrCloud offre prestazioni migliori rispetto alla modalità standalone (una singola configurazione Solr locale).

Per i dettagli di installazione e configurazione, consultate Configurazione [solr per SRP](solr.md).

### Seleziona DSRP {#select-dsrp}

La console [Configurazione](srp-config.md) storage consente di selezionare la configurazione di storage predefinita, che identifica l&#39;implementazione di SRP da utilizzare.

Per accedere alla console di configurazione dell&#39;archivio, all&#39;autore

* Accesso con privilegi di amministratore
* Dal menu **principale**

   * Seleziona **[!UICONTROL Strumenti]** (dal riquadro a sinistra)
   * Seleziona **[!UICONTROL community]**
   * Seleziona configurazione **[!UICONTROL archiviazione]**

      * Ad esempio, la posizione risultante è: [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp)
      >[!NOTE]
      >
      >La configurazione di storage predefinita ora è memorizzata nel percorso (`/conf/global/settings/community/srpc/defaultconfiguration`) conf anziché nel percorso (`/etc/socialconfig/srpc/defaultconfiguration`) etc. È consigliabile seguire i passaggi [di](#zerodt-migration-steps) migrazione per fare in modo che i predefiniti funzionino come previsto.
   ![dsrp-config](assets/dsrp-config.png)

* Select **[!UICONTROL Database Storage Resource Provider (DSRP)]**
* **Configurazione database**

   * **[!UICONTROL Nome origine dati JDBC]**

      Il nome assegnato alla connessione MySQL deve essere uguale a quello immesso nella configurazione OSGi [JDBC](dsrp-mysql.md#configurejdbcconnections)

      *predefinito*: community

   * **[!UICONTROL Nome database]**

      Nome assegnato allo schema nello script [init_schema.sql](dsrp-mysql.md#obtain-the-sql-script)

      *predefinito*: community

* **SolrConfiguration**

   * **[](https://cwiki.apache.org/confluence/display/solr/Using+ZooKeeper+to+Manage+Configuration+Files)Zookeeper Host**

      Lasciate vuoto questo valore se eseguite Solr utilizzando ZooKeeper interno. In caso contrario, quando si esegue in modalità [SolrCloud](solr.md#solrcloud-mode) con uno ZooKeeper esterno, imposta questo valore sull’URI per ZooKeeper, ad esempio *my.server.com:80*

      *predefinito*: *&lt;blank>*

   * **[!UICONTROL URL di Solr]**

      *predefinito*: https://127.0.0.1:8983/solr/

   * **[!UICONTROL Collezione Solr]**

      *predefinito*: collection1

* Seleziona **[!UICONTROL Invia]**.

### Zero passaggi di migrazione dei tempi di inattività per i record predefiniti {#zerodt-migration-steps}

Per assicurarsi che la pagina [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp) predefinita funzioni come previsto, effettuate le seguenti operazioni:

1. Rinominare il percorso `/etc/socialconfig` in in `/etc/socialconfig_old`, in modo che la configurazione del sistema ricada su jsrp (impostazione predefinita).
1. Passate alla pagina [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp)predefinita, in cui è configurato jsrp. Fare clic sul pulsante **[!UICONTROL Invia]** per creare il nuovo nodo di configurazione predefinito in `/conf/global/settings/community/srpc`.
1. Eliminate la configurazione predefinita creata `/conf/global/settings/community/srpc/defaultconfiguration`.
1. Copiate la vecchia configurazione `/etc/socialconfig_old/srpc/defaultconfiguration` al posto del nodo eliminato (`/conf/global/settings/community/srpc/defaultconfiguration`) nel passaggio precedente.
1. Elimina il vecchio nodo etc `/etc/socialconfig_old`.

## Pubblicazione della configurazione {#publishing-the-configuration}

DSRP deve essere identificato come store comune in tutte le istanze di creazione e pubblicazione.

Per rendere disponibile la stessa configurazione nell’ambiente di pubblicazione:

* Per autore:

   * Passare dal menu principale a **[!UICONTROL Strumenti]** > **[!UICONTROL Operazioni]** > **[!UICONTROL Replica]**
   * Fate doppio clic su **[!UICONTROL Attiva albero]**
   * **Percorso iniziale**:

      * Passa a `/etc/socialconfig/srpc/`
   * Assicurarsi che non `Only Modified` sia selezionato.
   * Selezionate **[!UICONTROL Attiva]**.


## Gestione dei dati utente {#managing-user-data}

Per informazioni sugli *utenti*, i profili ** utente e i gruppi *di* utenti, spesso inseriti nell’ambiente di pubblicazione, visitate:

* [Sincronizzazione utente](sync.md)
* [Gestione di utenti e gruppi di utenti](users.md)

## Solr di reindicizzazione per DSRP {#reindexing-solr-for-dsrp}

Per reindicizzare DSRP Solr, seguite la documentazione per la [reindicizzazione MSRP](msrp.md#msrp-reindex-tool), ma quando effettuate la reindicizzazione per DSRP, utilizzate invece questo URL: **/services/social/datastore/rdb/reindex**

Ad esempio, un comando curl per reindicizzare DSRP sarà simile al seguente:

```shell
curl -u admin:password -X POST -F path=/ https://host:port/services/social/datastore/rdb/reindex
```

