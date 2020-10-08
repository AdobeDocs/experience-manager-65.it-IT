---
title: MSRP - Provider di risorse di storage MongoDB
seo-title: MSRP - Provider di risorse di storage MongoDB
description: Imposta  AEM Communities per utilizzare un database relazionale come store comune
seo-description: Imposta  AEM Communities per utilizzare un database relazionale come store comune
uuid: 9fc06d4f-a60f-4ce3-8586-bcc836aa7de6
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 048f7b30-20c3-4567-bd32-38cf2643cf39
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '1209'
ht-degree: 1%

---


# MSRP - Provider di risorse di storage MongoDB {#msrp-mongodb-storage-resource-provider}

## Informazioni su MSRP {#about-msrp}

Quando  AEM Communities è configurato per utilizzare MSRP come store comune, il contenuto generato dall’utente (UGC) è accessibile da tutte le istanze di creazione e pubblicazione senza la necessità di eseguire la sincronizzazione e la replica.

Vedere anche [Caratteristiche delle opzioni](working-with-srp.md#characteristics-of-srp-options) SRP e topologie [](topologies.md)consigliate.

## Requisiti {#requirements}

* [MongoDB](https://www.mongodb.org/):

   * Versione 2.6 o successiva
   * Non è necessario configurare i logo o la condivisione
   * Consiglia vivamente l&#39;utilizzo di un set di [replica](#mongoreplicaset)
   * Può essere eseguito sullo stesso host AEM o in remoto

* [Apache Solr](https://lucene.apache.org/solr/):

   * Solr versione 7.0
   * Solr richiede Java 1.7 o versione successiva
   * Nessun servizio necessario
   * Scelta delle modalità di esecuzione:
      * Modalità indipendente
      * [Modalità](solr.md#solrcloud-mode) SolrCloud (consigliato per gli ambienti di produzione)
   * Scelta della ricerca multilingue (MLS):
      * [Installazione di MLS standard](solr.md#installing-standard-mls)
      * [Installazione di MLS avanzate](solr.md#installing-advanced-mls)

## MongoDB Configuration {#mongodb-configuration}

### Select MSRP {#select-msrp}

La console [Configurazione](srp-config.md) storage consente di selezionare la configurazione di storage predefinita, che identifica l&#39;implementazione di SRP da utilizzare.

Per accedere alla console di configurazione dell&#39;archivio, all&#39;autore:

* Dalla navigazione globale, selezionate **[!UICONTROL Strumenti]** > **[!UICONTROL Community]** > Configurazione **** archiviazione.

![msrp](assets/msrp.png)

* Select **[!UICONTROL MongoDB Storage Resource Provider (MSRP)]**
* **[!UICONTROL Configurazione mongoDB]**

   * **[!UICONTROL URI di mongoDB]**

      *predefinito*: mongodb://localhost/?maxPoolSize=10&amp;waitQueueMultiple=5&amp;readPreference=secondaryPreferred

   * **[!UICONTROL Database di mongoDB]**

      *predefinito*: community

   * **[!UICONTROL Raccolta UGC di mongoDB]**

      *predefinito*: content

   * **[!UICONTROL Raccolta allegati mongoDB]**

      *predefinito*: allegati

* **[!UICONTROL SolrConfiguration]**

   * **[](https://cwiki.apache.org/confluence/display/solr/Using+ZooKeeper+to+Manage+Configuration+Files)Zookeeper Host**

      In modalità [SolrCloud](solr.md#solrcloud-mode) con un ZooKeeper esterno, imposta questo valore su `HOST:PORT` per ZooKeeper, ad esempio *my.server.com:2181*

      Per un ensemble ZooKeeper, inserite `HOST:PORT` valori separati da virgole, ad esempio *host1:2181,host2:2181*

      Lasciate vuoto se eseguite Solr in modalità standalone utilizzando ZooKeeper interno.
      *Predefinito*: *&lt;blank>*

      * **[!UICONTROL URL]**solare L’URL utilizzato per comunicare con Solr in modalità standalone.
Lasciate vuoto se eseguite in modalità SolrCloud.

         *Predefinito*: https://127.0.0.1:8983/solr/

      * **[!UICONTROL Raccolta]**Solr Il nome della raccolta Solr.

         *Predefinito*: collection1

* Seleziona **[!UICONTROL Invia]**

>[!NOTE]
>
>Il database mongoDB, che per impostazione predefinita corrisponde al nome `communities`, non deve essere impostato sul nome di un database utilizzato per gli archivi di [nodi o gli archivi](../../help/sites-deploying/data-store-config.md)di dati (binari). Vedere anche [Elementi di storage in AEM 6.5](../../help/sites-deploying/storage-elements-in-aem-6.md).

### Set di replica MongoDB {#mongodb-replica-set}

Per l&#39;ambiente di produzione, si consiglia vivamente di impostare un set di repliche, un cluster di server MongoDB che implementa la replica primaria secondaria e il failover automatizzato.

Per ulteriori informazioni sui set di repliche, consultare la documentazione [Replica](https://docs.mongodb.org/manual/replication/) di MongoDB.

Per utilizzare i set di repliche e definire le connessioni tra le applicazioni e le istanze MongoDB, consultare la documentazione relativa al formato [URI della stringa di](https://docs.mongodb.org/manual/reference/connection-string/) connessione di MongoDB.

#### Url di esempio per la connessione a un set di replica  {#example-url-for-connecting-to-a-replica-set}

```shell
# Example url for:
# servers "mongoserver1", "mongoserver2", "mongoserver3"
# replica set 'rs0'
# port numbers only necessary if not default port 27017
mongodb://mongoserver1:<mongoport1>,mongoserver2:<mongoport2>,mongoserver3:<mongoport3>/?replicaSet=rs0&maxPoolSize=100&waitQueueMultiple=50&readPreference=secondaryPreferred
```

## Configurazione Solr {#solr-configuration}

Un&#39;installazione Solr può essere condivisa tra l&#39;archivio nodi (Oak) e lo store comune (MSRP) utilizzando raccolte diverse.

Se le raccolte Oak e MSRP vengono utilizzate intensamente, per motivi di prestazioni potrebbe essere installato un secondo Solr.

Per gli ambienti di produzione, la modalità [](solr.md#solrcloud-mode) SolrCloud offre prestazioni migliori rispetto alla modalità standalone (una singola configurazione Solr locale).

Per informazioni dettagliate sulla configurazione, consultate Configurazione [Solr per SRP](solr.md).

### Aggiornamento {#upgrading}

Se si esegue l&#39;aggiornamento da una versione precedente configurata con MSRP, sarà necessario:

1. Eseguire l&#39; [aggiornamento a  AEM Communities](upgrade.md)
1. Installare nuovi file di configurazione Solr
   * Per MLS [standard](solr.md#installing-standard-mls)
   * Per MLS [avanzati](solr.md#installing-advanced-mls)
1. Reindicizzare la sezione MSRPSee [MSRP Reindex Tool](#msrp-reindex-tool)

## Pubblicazione della configurazione {#publishing-the-configuration}

MSRP deve essere identificato come store comune in tutte le istanze di creazione e pubblicazione.

Per rendere disponibile la stessa configurazione nell’ambiente di pubblicazione, effettuate l’accesso all’istanza di creazione e seguite i passaggi seguenti:

* Passare dal menu principale a **[!UICONTROL Strumenti]** > **[!UICONTROL Operazioni]** > **[!UICONTROL Replica]**.
* Seleziona **[!UICONTROL Attiva albero]**
* **[!UICONTROL Percorso iniziale]**:
   * Passa a `/etc/socialconfig/srpc/`
* Seleziona **[!UICONTROL attiva]**

## Gestione dei dati utente {#managing-user-data}

Per informazioni sugli *utenti*, i profili ** utente e i gruppi *di* utenti, spesso inseriti nell’ambiente di pubblicazione, visita

* [Sincronizzazione utente](sync.md)
* [Gestione di utenti e gruppi di utenti](users.md)

## Strumento Reindicizzazione MSRP {#msrp-reindex-tool}

Esiste un endpoint HTTP per la reindicizzazione Solr per MSRP quando si installano nuovi file di configurazione o si ripara un indice Solr danneggiato.

Con questo strumento, MongoDB è la fonte di *verità* per MSRP; i backup devono essere eseguiti solo da MongoDB.

L&#39;intero albero UGC può essere reindicizzato, o solo un sottoalbero specifico, come specificato dal parametro *path *data.

Questo strumento può essere eseguito dalla riga di comando utilizzando cURL o qualsiasi altro strumento HTTP.

Durante la reindicizzazione, esiste un compromesso tra memoria e prestazioni controllato dal parametro *batchSize *data, che specifica quanti record UGC vengono reindicizzati per batch.

Un valore predefinito ragionevole è 5000:

* Se la memoria è un problema, specificate un numero più piccolo
* Se la velocità è un problema, specificate un numero maggiore per aumentare la velocità

### Esecuzione dello strumento di reindicizzazione MSRP tramite il comando cURL {#running-msrp-reindex-tool-using-curl-command}

Il seguente comando cURL mostra ciò che è necessario per una richiesta HTTP per reindicizzare UGC memorizzato in MSRP.

Il formato di base è:

cURL -u *signin* -d *data* *reindex-url*

*signin* = administrator-id:passwordAd esempio: admin:admin

*data* = &quot;batchSize=*size*&amp;path=*path&quot;*

*size* = quante voci UGC reindicizzare per operazione
`/content/usergenerated/asi/mongo/`

*path* = posizione radice della struttura ad albero di UGC da reindicizzare

* Per reindicizzare tutti gli UGC, specificate il valore della `asipath`proprietà di
   `/etc/socialconfig/srpc/defaultconfiguration`
* Per limitare l’indice ad alcuni UGC, specificate una sottostruttura di `asipath`

*reindex-url* = l&#39;endpoint per la reindicizzazione di SRP
`http://localhost:4503/services/social/datastore/mongo/reindex`

>[!NOTE]
>
>Se state [reindicizzando DSRP Solr](dsrp.md), l’URL è **/services/social/datastore/rdb/reindex**

### Esempio di reindicizzazione MSRP {#msrp-reindex-example}

```shell
curl -s -u admin:admin -d 'batchSize=10000&path=/content/usergenerated/asi/mongo/' http://localhost:4503/services/social/datastore/mongo/reindex
```

## Come demo MSRP {#how-to-demo-msrp}

Per impostare MSRP per un ambiente di dimostrazione o di sviluppo, vedere [Come impostare MongoDB per Demo](demo-mongo.md).

## Risoluzione dei problemi {#troubleshooting}

### UGC non visibile in MongoDB {#ugc-not-visible-in-mongodb}

Verificate che MSRP sia stato configurato come provider predefinito, verificando la configurazione dell&#39;opzione di archiviazione. Per impostazione predefinita, il provider delle risorse di storage è JSRP.

Per tutte le istanze di creazione e pubblicazione AEM, rivedete la console [Configurazione](srp-config.md) archiviazione o controllate l&#39;archivio AEM:

* In JCR, se [/etc/socialconfig](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/)

   * Non contiene un nodo [srpc](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc) , significa che il provider di archiviazione è JSRP.
   * Se il nodo srpc esiste e contiene il nodo [defaultconfiguration](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc/defaultconfiguration), le proprietà della configurazione predefinita devono definire MSRP come provider predefinito.

### UGC scompare dopo l&#39;aggiornamento {#ugc-disappears-after-upgrade}

Se si esegue l&#39;aggiornamento da un sito AEM Communities 6.0  esistente, qualsiasi UGC preesistente deve essere convertito in modo da essere conforme alla struttura richiesta per l&#39;API [SRP](srp.md) dopo l&#39;aggiornamento a  AEM Communities 6.3.

È disponibile uno strumento open source su GitHub per questo scopo:

* [AEM Communities UGC Migration Tool](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)

Lo strumento di migrazione può essere personalizzato per esportare UGC da versioni precedenti di AEM social community da importare in  AEM Communities 6.1 o versioni successive.

### Errore - provider_id campo non definito {#error-undefined-field-provider-id}

Se nei registri viene visualizzato il seguente errore, significa che il file dello schema Solr non è configurato correttamente.

#### JsonMappingException: field provider_id non definito {#jsonmappingexception-undefined-field-provider-id}

```xml
Caused by: com.fasterxml.jackson.databind.JsonMappingException: undefined field provider_id
at com.fasterxml.jackson.databind.ser.DefaultSerializerProvider.serializeValue(DefaultSerializerProvider.java:129)
at com.fasterxml.jackson.databind.ObjectMapper.writeValue(ObjectMapper.java:1819)
at com.adobe.cq.social.scf.core.BaseSocialComponent.toJSONString(BaseSocialComponent.java:196)
... 124 common frames omitted
```

Per risolvere l&#39;errore, quando si seguono le istruzioni per l&#39; [installazione di MLS](solr.md#installing-standard-mls)standard, verificare quanto segue:

* I file di configurazione XML sono stati copiati nel percorso Solr corretto.
* Solr è stato riavviato dopo che i nuovi file di configurazione hanno sostituito quelli esistenti.

### Connessione sicura a MongoDB non riuscita {#secure-connection-to-mongodb-fails}

Se un tentativo di connessione protetta al server MongoDB non riesce a causa di una definizione di classe mancante, è necessario aggiornare il bundle del driver MongoDB, `mongo-java-driver`, disponibile dall&#39;archivio pubblico del server.

1. Scaricate il driver da [https://search.maven.org/#artifactdetails%7Corg.mongodb%7Cmongo-java-driver%7C2.13.2%7Cjar](https://search.maven.org/#artifactdetails%7Corg.mongodb%7Cmongo-java-driver%7C2.13.2%7Cjar) (versione 2.13.2 o successiva).
1. Copiate il bundle nella cartella &quot;crx-quickstart/install&quot; per un’istanza AEM.
1. Riavviate l&#39;istanza AEM.

## Riferimenti {#resources}

* [AEM con MongoDB](../../help/sites-deploying/aem-with-mongodb.md)
* [Documentazione MongoDB](https://docs.mongodb.org/)

