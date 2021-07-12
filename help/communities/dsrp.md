---
title: DSRP - Provider risorsa di archiviazione database relazionale
seo-title: DSRP - Provider risorsa di archiviazione database relazionale
description: Imposta AEM Communities per utilizzare un database relazionale come archivio comune
seo-description: Imposta AEM Communities per utilizzare un database relazionale come archivio comune
uuid: f364e7da-ee54-4ab2-a630-7ec9239005ac
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: d23acb18-6761-4290-9e7a-a434582791bd
role: Admin
exl-id: 15b3a594-efde-4702-9233-232ba1c7e5b0
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 3%

---

# DSRP - Provider risorsa di archiviazione database relazionale {#dsrp-relational-database-storage-resource-provider}

## Informazioni su DSRP {#about-dsrp}

Quando AEM Communities è configurato per utilizzare un database relazionale come archivio comune, il contenuto generato dall’utente (UGC) è accessibile da tutte le istanze di authoring e pubblicazione senza la necessità di sincronizzazione e replica.

Vedere anche [Caratteristiche delle opzioni SRP](working-with-srp.md#characteristics-of-srp-options) e [Topologie consigliate](topologies.md).

## Requisiti {#requirements}

* [MySQL](#mysql-configuration), un database relazionale.
* [Apache Solr](#solr-configuration), una piattaforma di ricerca.

>[!NOTE]
>
>La configurazione di archiviazione predefinita è ora memorizzata nel percorso conf(`/conf/global/settings/community/srpc/defaultconfiguration`) invece del percorso etc (`/etc/socialconfig/srpc/defaultconfiguration`). Si consiglia di seguire i [passaggi di migrazione](#zerodt-migration-steps) per far funzionare default srp come previsto.

## Configurazione database relazionale {#relational-database-configuration}

### Configurazione MySQL {#mysql-configuration}

Un&#39;installazione MySQL può essere condivisa tra le funzioni di abilitazione e l&#39;archivio comune (DSRP) all&#39;interno dello stesso pool di connessioni utilizzando nomi di database (schema) diversi e connessioni diverse (server:port).

Per informazioni sull&#39;installazione e la configurazione, vedere [Configurazione MySQL per DSRP](dsrp-mysql.md).

### Configurazione Solr {#solr-configuration}

Un&#39;installazione Solr può essere condivisa tra l&#39;archivio nodi (Oak) e l&#39;archivio comune (SRP) utilizzando diverse raccolte.

Se le raccolte Oak e SRP vengono utilizzate intensamente, è possibile installare un secondo Solr per motivi di prestazioni.

Per gli ambienti di produzione, la modalità SolrCloud offre prestazioni migliori rispetto alla modalità autonoma (una singola configurazione Solr locale).

Per informazioni sull&#39;installazione e la configurazione, vedere [Configurazione del solare per SRP](solr.md).

### Seleziona DSRP {#select-dsrp}

La [console di configurazione dello storage](srp-config.md) consente di selezionare la configurazione di archiviazione predefinita, che identifica l&#39;implementazione dell&#39;SRP da utilizzare.

Per accedere alla console di configurazione dell&#39;archiviazione, all&#39;autore

* Accesso con privilegi di amministratore
* Dal menu principale ****

   * Seleziona **[!UICONTROL Strumenti]** (dal riquadro a sinistra)
   * Seleziona **[!UICONTROL Community]**
   * Seleziona **[!UICONTROL Configurazione archiviazione]**

      * Ad esempio, la posizione risultante è: [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp)
      >[!NOTE]
      >
      >La configurazione di archiviazione predefinita è ora memorizzata nel percorso conf(`/conf/global/settings/community/srpc/defaultconfiguration`)      invece del percorso etc (`/etc/socialconfig/srpc/defaultconfiguration`). Si consiglia di seguire i [passaggi di migrazione](#zerodt-migration-steps) per far funzionare default srp come previsto.
   ![dsrp-config](assets/dsrp-config.png)

* Selezionare **[!UICONTROL Provider di risorse di archiviazione database (DSRP)]**
* **Configurazione database**

   * **[!UICONTROL Nome origine dati JDBC]**

      Il nome assegnato alla connessione MySQL deve essere lo stesso immesso nella configurazione [JDBC OSGi](dsrp-mysql.md#configurejdbcconnections)

      *predefinito*: community

   * **[!UICONTROL Nome database]**

      Nome assegnato allo schema nello script [init_schema.sql](dsrp-mysql.md#obtain-the-sql-script)

      *predefinito*: community

* **SolrConfiguration**

   * **[](https://cwiki.apache.org/confluence/display/solr/Using+ZooKeeper+to+Manage+Configuration+Files)Zookeeper Host**

      Lascia vuoto questo valore se esegui Solr utilizzando lo ZooKeeper interno. Altrimenti, quando si esegue in modalità [SolrCloud](solr.md#solrcloud-mode) con un ZooKeeper esterno, imposta questo valore sull&#39;URI per ZooKeeper, ad esempio *my.server.com:80*

      *predefinito*:  *&lt;blank>*

   * **[!UICONTROL URL di Solr]**

      *predefinito*: https://127.0.0.1:8983/solr/

   * **[!UICONTROL Collezione Solr]**

      *predefinito*: collection1

* Seleziona **[!UICONTROL Invia]**.

### Zero passaggi di migrazione dei tempi di inattività per default srp {#zerodt-migration-steps}

Segui questi passaggi per garantire che la pagina predefinita della srp [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp) funzioni come previsto:

1. Rinomina il percorso in `/etc/socialconfig` in `/etc/socialconfig_old` in modo che la configurazione del sistema torni a jsrp (impostazione predefinita).
1. Vai alla pagina predefinita [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp), in cui è configurato jsrp. Fai clic sul pulsante **[!UICONTROL invia]** in modo che venga creato un nuovo nodo di configurazione predefinito in `/conf/global/settings/community/srpc`.
1. Elimina la configurazione predefinita creata `/conf/global/settings/community/srpc/defaultconfiguration`.
1. Copia la vecchia configurazione `/etc/socialconfig_old/srpc/defaultconfiguration` al posto del nodo eliminato (`/conf/global/settings/community/srpc/defaultconfiguration`) nel passaggio precedente.
1. Elimina il vecchio nodo etc `/etc/socialconfig_old`.

## Pubblicazione della configurazione {#publishing-the-configuration}

DSRP deve essere identificato come archivio comune su tutte le istanze di authoring e pubblicazione.

Per rendere disponibile nell’ambiente di pubblicazione la stessa configurazione:

* Autore:

   * Passa dal menu principale a **[!UICONTROL Strumenti]** > **[!UICONTROL Operazioni]** > **[!UICONTROL Replica]**
   * Fate doppio clic su **[!UICONTROL Attiva albero]**
   * **Percorso iniziale**:

      * Vai a `/etc/socialconfig/srpc/`
   * Assicurati che `Only Modified` non sia selezionato.
   * Selezionare **[!UICONTROL Attiva]**.


## Gestione dei dati utente {#managing-user-data}

Per informazioni sugli *utenti*, *profili utente* e *gruppi di utenti*, spesso inseriti nell&#39;ambiente di pubblicazione, visita:

* [Sincronizzazione utente](sync.md)
* [Gestione di utenti e gruppi di utenti](users.md)

## Solr reindicizzazione per DSRP {#reindexing-solr-for-dsrp}

Per reindicizzare DSRP Solr, segui la documentazione relativa a [reindicizzazione MSRP](msrp.md#msrp-reindex-tool), tuttavia quando esegui la reindicizzazione per DSRP, utilizza al suo posto questo URL: **/services/social/datastore/rdb/reindex**

Ad esempio, un comando curl per reindicizzare DSRP dovrebbe essere simile al seguente:

```shell
curl -u admin:password -X POST -F path=/ https://host:port/services/social/datastore/rdb/reindex
```
