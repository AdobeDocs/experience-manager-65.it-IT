---
title: DSRP - Provider risorsa di archiviazione database relazionale
description: Impostare AEM Communities per l'utilizzo di un database relazionale come archivio comune
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 15b3a594-efde-4702-9233-232ba1c7e5b0
source-git-commit: f0dd1ac3ab9c17a8b331f5048d84ec97dd23924f
workflow-type: tm+mt
source-wordcount: '617'
ht-degree: 3%

---

# DSRP - Provider risorsa di archiviazione database relazionale {#dsrp-relational-database-storage-resource-provider}

## Informazioni su DSRP {#about-dsrp}

Quando AEM Communities è configurato per utilizzare un database relazionale come archivio comune, il contenuto generato dall’utente (UGC, User-Generated Content) è accessibile da tutte le istanze di authoring e pubblicazione senza la necessità di sincronizzazione o replica.

Vedi anche [Caratteristiche delle opzioni SRP](working-with-srp.md#characteristics-of-srp-options) e [Topologie consigliate](topologies.md).

## Requisiti {#requirements}

* [MySQL](#mysql-configuration), un database relazionale.
* [Apache Solr](#solr-configuration), una piattaforma di ricerca.

>[!NOTE]
>
>La configurazione di archiviazione predefinita è ora memorizzata in conf path(`/conf/global/settings/community/srpc/defaultconfiguration`) invece di `etc` percorso (`/etc/socialconfig/srpc/defaultconfiguration`). È consigliabile seguire le istruzioni [passaggi di migrazione](#zerodt-migration-steps) per fare in modo che default srp funzioni come previsto.

## Configurazione database relazionale {#relational-database-configuration}

### Configurazione MySQL {#mysql-configuration}

Un&#39;installazione MySQL può essere condivisa tra le funzionalità di abilitazione e l&#39;archivio comune (DSRP) all&#39;interno dello stesso pool di connessioni utilizzando nomi di database (schema) diversi e anche connessioni diverse (server:porta).

Per informazioni dettagliate sull’installazione e la configurazione, consulta [Configurazione MySQL per DSRP](dsrp-mysql.md).

### Configurazione Solr {#solr-configuration}

Un’installazione Solr può essere condivisa tra l’archivio nodi (Oak) e l’archivio comune (SRP) utilizzando raccolte diverse.

Se entrambe le raccolte Oak e SRP vengono utilizzate in modo intensivo, è possibile installare un secondo Solr per motivi di prestazioni.

Per gli ambienti di produzione, la modalità SolrCloud offre prestazioni migliori rispetto alla modalità standalone (un&#39;unica configurazione Solr locale).

Per informazioni dettagliate sull’installazione e la configurazione, consulta [Configurazione Solr per SRP](solr.md).

### Seleziona DSRP {#select-dsrp}

Il [Console di configurazione archiviazione](srp-config.md) consente di selezionare la configurazione di archiviazione predefinita, che identifica l&#39;implementazione di SRP da utilizzare.

Per accedere alla console Configurazione archiviazione, dall’autore

* Accedi con privilegi di amministratore
* Dalla sezione **menu principale**

   * Seleziona **[!UICONTROL Strumenti]** (dal riquadro di sinistra)
   * Seleziona **[!UICONTROL Community]**
   * Seleziona **[!UICONTROL Configurazione archiviazione]**

      * Ad esempio, la posizione risultante è: [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp)

     >[!NOTE]
     >
     >La configurazione di archiviazione predefinita è ora memorizzata in conf path(`/conf/global/settings/community/srpc/defaultconfiguration`) invece di `etc` percorso (`/etc/socialconfig/srpc/defaultconfiguration`). È consigliabile seguire le istruzioni [passaggi di migrazione](#zerodt-migration-steps) per fare in modo che default srp funzioni come previsto.

  ![dsrp-config](assets/dsrp-config.png)

* Seleziona **[!UICONTROL Provider risorsa di archiviazione database (DSRP)]**
* **Configurazione database**

   * **[!UICONTROL Nome origine dati JDBC]**

     Il nome assegnato alla connessione MySQL deve essere uguale a quello immesso in [Configurazione JDBC OSGi](dsrp-mysql.md#configurejdbcconnections)

     *predefinito*: community

   * **[!UICONTROL Nome database]**

     Nome assegnato allo schema in [init_schema.sql](dsrp-mysql.md#obtain-the-sql-script) script

     *predefinito*: community

* **SolrConfiguration**

   * **[](https://solr.apache.org/guide/6_6/using-zookeeper-to-manage-configuration-files.html)Zookeeper Host**

     Lascia vuoto questo valore se esegui Solr utilizzando lo ZooKeeper interno. Altrimenti, durante l’esecuzione in [Modalità SolrCloud](solr.md#solrcloud-mode) con uno ZooKeeper esterno, impostare questo valore sull&#39;URI dello ZooKeeper, ad esempio *my.server.com:80*

     *predefinito*: *&lt;blank>*

   * **[!UICONTROL URL di Solr]**

     *predefinito*: https://127.0.0.1:8983/solr/

   * **[!UICONTROL Collezione Solr]**

     *predefinito*: collection1

* Seleziona **[!UICONTROL Invia]**.

### Nessuna fase di migrazione dei tempi di inattività per defaultsrp {#zerodt-migration-steps}

Per assicurarsi che la pagina defaultsrp [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp) funziona come previsto, segui questi passaggi:

1. Rinomina il percorso in corrispondenza di `/etc/socialconfig` a `/etc/socialconfig_old`, in modo che la configurazione del sistema torni a jsrp (impostazione predefinita).
1. Vai a pagina predefinita [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp): in cui è configurato jsrp. Fai clic su **[!UICONTROL invia]** in modo che il nuovo nodo di configurazione predefinito venga creato `/conf/global/settings/community/srpc`.
1. Elimina la configurazione predefinita creata `/conf/global/settings/community/srpc/defaultconfiguration`.
1. Copia la vecchia configurazione `/etc/socialconfig_old/srpc/defaultconfiguration` al posto del nodo eliminato (`/conf/global/settings/community/srpc/defaultconfiguration`) nel passaggio precedente.
1. Elimina il vecchio `etc` nodo `/etc/socialconfig_old`.

## Pubblicazione della configurazione {#publishing-the-configuration}

DSRP deve essere identificato come archivio comune in tutte le istanze di authoring e pubblicazione.

Per rendere disponibile la configurazione identica nell’ambiente di pubblicazione:

* All’autore:

   * Passa dal menu principale a **[!UICONTROL Strumenti]** > **[!UICONTROL Operazioni]** > **[!UICONTROL Replica]**
   * Doppio clic **[!UICONTROL Attiva albero]**
   * **Percorso iniziale**:

      * Sfoglia per `/etc/socialconfig/srpc/`

   * Assicurare `Only Modified` non è selezionato.
   * Seleziona **[!UICONTROL Attiva]**.

## Gestione dei dati utente {#managing-user-data}

Per informazioni su *utenti*, *profili utente* e *gruppi di utenti*, spesso immessi nell’ambiente di pubblicazione, visita:

* [Sincronizzazione utente](sync.md)
* [Gestione di utenti e gruppi di utenti](users.md)

## Reindicizzazione Solr per DSRP {#reindexing-solr-for-dsrp}

Per reindicizzare DSRP Solr, segui la documentazione di [reindicizzazione MSRP](msrp.md#msrp-reindex-tool), tuttavia, quando si reindicizza per DSRP, utilizza questo URL: **/services/social/datastore/rdb/reindex**

Ad esempio, un comando curl per reindicizzare DSRP sarà simile al seguente:

```shell
curl -u admin:password -X POST -F path=/ https://host:port/services/social/datastore/rdb/reindex
```
