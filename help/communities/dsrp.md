---
title: DSRP - Provider risorsa di archiviazione database relazionale
seo-title: DSRP - Relational Database Storage Resource Provider
description: Imposta AEM Communities per utilizzare un database relazionale come archivio comune
seo-description: Set up AEM Communities to use a relational database as its common store
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
source-wordcount: '629'
ht-degree: 3%

---

# DSRP - Provider risorsa di archiviazione database relazionale {#dsrp-relational-database-storage-resource-provider}

## Informazioni su DSRP {#about-dsrp}

Quando AEM Communities è configurato per utilizzare un database relazionale come archivio comune, il contenuto generato dall’utente (UGC) è accessibile da tutte le istanze di authoring e pubblicazione senza la necessità di sincronizzazione e replica.

Vedi anche [Caratteristiche delle opzioni SRP](working-with-srp.md#characteristics-of-srp-options) e [Topologie consigliate](topologies.md).

## Requisiti  {#requirements}

* [MySQL](#mysql-configuration), un database relazionale.
* [Apache Solr](#solr-configuration), una piattaforma di ricerca.

>[!NOTE]
>
>La configurazione di archiviazione predefinita è ora memorizzata nel percorso conf(`/conf/global/settings/community/srpc/defaultconfiguration`) invece del percorso etc (`/etc/socialconfig/srpc/defaultconfiguration`). Ti consigliamo di seguire la [passaggi di migrazione](#zerodt-migration-steps) per eseguire il funzionamento predefinito come previsto.

## Configurazione database relazionale {#relational-database-configuration}

### Configurazione MySQL {#mysql-configuration}

Un&#39;installazione MySQL può essere condivisa tra le funzioni di abilitazione e l&#39;archivio comune (DSRP) all&#39;interno dello stesso pool di connessioni utilizzando nomi di database (schema) diversi e connessioni diverse (server:port).

Per informazioni dettagliate sull&#39;installazione e la configurazione, consulta [Configurazione MySQL per DSRP](dsrp-mysql.md).

### Configurazione Solr {#solr-configuration}

Un&#39;installazione Solr può essere condivisa tra l&#39;archivio nodi (Oak) e l&#39;archivio comune (SRP) utilizzando diverse raccolte.

Se le raccolte Oak e SRP vengono utilizzate intensamente, è possibile installare un secondo Solr per motivi di prestazioni.

Per gli ambienti di produzione, la modalità SolrCloud offre prestazioni migliori rispetto alla modalità autonoma (una singola configurazione Solr locale).

Per informazioni dettagliate sull&#39;installazione e la configurazione, consulta [Configurazione Solr per SRP](solr.md).

### Seleziona DSRP {#select-dsrp}

La [Console di configurazione dell&#39;archiviazione](srp-config.md) consente la selezione della configurazione di storage predefinita, che identifica quale implementazione dell&#39;SRP utilizzare.

Per accedere alla console di configurazione dell&#39;archiviazione, all&#39;autore

* Accesso con privilegi di amministratore
* Da **menu principale**

   * Seleziona **[!UICONTROL Strumenti]** (dal riquadro a sinistra)
   * Seleziona **[!UICONTROL Community]**
   * Seleziona **[!UICONTROL Configurazione dell&#39;archiviazione]**

      * Ad esempio, la posizione risultante è: [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp)
      >[!NOTE]
      >
      >La configurazione di archiviazione predefinita è ora memorizzata nel percorso conf(`/conf/global/settings/community/srpc/defaultconfiguration`) invece del percorso etc (`/etc/socialconfig/srpc/defaultconfiguration`). Ti consigliamo di seguire la [passaggi di migrazione](#zerodt-migration-steps) per eseguire il funzionamento predefinito come previsto.
   ![dsrp-config](assets/dsrp-config.png)

* Seleziona **[!UICONTROL Provider di risorse di archiviazione database (DSRP)]**
* **Configurazione database**

   * **[!UICONTROL Nome origine dati JDBC]**

      Il nome assegnato alla connessione MySQL deve essere lo stesso immesso in [Configurazione JDBC OSGi](dsrp-mysql.md#configurejdbcconnections)

      *default*: community

   * **[!UICONTROL Nome database]**

      Nome assegnato allo schema in [init_schema.sql](dsrp-mysql.md#obtain-the-sql-script) script

      *default*: community

* **SolrConfiguration**

   * **[](https://cwiki.apache.org/confluence/display/solr/Using+ZooKeeper+to+Manage+Configuration+Files)Zookeeper Host**

      Lascia vuoto questo valore se esegui Solr utilizzando lo ZooKeeper interno. Else, quando si esegue in [Modalità SolrCloud](solr.md#solrcloud-mode) con uno ZooKeeper esterno, imposta questo valore sull’URI per lo ZooKeeper, ad esempio *my.server.com:80*

      *default*: *&lt;blank>*

   * **[!UICONTROL URL di Solr]**

      *default*: https://127.0.0.1:8983/solr/

   * **[!UICONTROL Collezione Solr]**

      *default*: collection1

* Seleziona **[!UICONTROL Invia]**.

### Zero passaggi di migrazione dei tempi di inattività per default srp {#zerodt-migration-steps}

Segui questi passaggi per assicurarti che la pagina predefinita srp [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp) funziona come previsto:

1. Rinomina il percorso in `/etc/socialconfig` a `/etc/socialconfig_old`in modo che la configurazione del sistema torni a jsrp (impostazione predefinita).
1. Vai alla pagina predefinita srp [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp), in cui è configurato jsrp. Fai clic sul pulsante **[!UICONTROL submit]** in modo che venga creato il nuovo nodo di configurazione predefinito in `/conf/global/settings/community/srpc`.
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

      * Sfoglia per `/etc/socialconfig/srpc/`
   * Assicurati `Only Modified` non è selezionato.
   * Seleziona **[!UICONTROL Attiva]**.


## Gestione dei dati utente {#managing-user-data}

Per informazioni riguardanti *utenti*, *profili utente* e *gruppi di utenti*, spesso inserito nell’ambiente di pubblicazione, visita:

* [Sincronizzazione utente](sync.md)
* [Gestione di utenti e gruppi di utenti](users.md)

## Solr reindicizzazione per DSRP {#reindexing-solr-for-dsrp}

Per reindicizzare DSRP Solr, segui la documentazione di [reindicizzazione MSRP](msrp.md#msrp-reindex-tool)Tuttavia, quando esegui la reindicizzazione per DSRP, utilizza invece questo URL: **/services/social/datastore/rdb/reindex**

Ad esempio, un comando curl per reindicizzare DSRP dovrebbe essere simile al seguente:

```shell
curl -u admin:password -X POST -F path=/ https://host:port/services/social/datastore/rdb/reindex
```
