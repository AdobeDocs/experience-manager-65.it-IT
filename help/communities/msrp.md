---
title: MSRP - Provider risorsa di archiviazione MongoDB
seo-title: MSRP - Provider risorsa di archiviazione MongoDB
description: Imposta AEM Communities per utilizzare un database relazionale come archivio comune
seo-description: Imposta AEM Communities per utilizzare un database relazionale come archivio comune
uuid: 9fc06d4f-a60f-4ce3-8586-bcc836aa7de6
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 048f7b30-20c3-4567-bd32-38cf2643cf39
role: Admin
exl-id: 799d5ae1-caac-4c92-8835-696ad25de553
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '1209'
ht-degree: 1%

---

# MSRP - Provider risorsa di archiviazione MongoDB {#msrp-mongodb-storage-resource-provider}

## Informazioni su MSRP {#about-msrp}

Quando AEM Communities è configurato per utilizzare MSRP come archivio comune, il contenuto generato dall’utente (UGC) è accessibile da tutte le istanze di authoring e pubblicazione senza la necessità di sincronizzazione e replica.

Vedere anche [Caratteristiche delle opzioni SRP](working-with-srp.md#characteristics-of-srp-options) e [Topologie consigliate](topologies.md).

## Requisiti {#requirements}

* [MongoDB](https://www.mongodb.org/):

   * Versione 2.6 o successiva
   * Non è necessario configurare i monghi o la condivisione
   * Consiglia vivamente l&#39;uso di un [set di repliche](#mongoreplicaset)
   * Può essere eseguito sullo stesso host AEM o eseguito in remoto

* [Apache Solr](https://lucene.apache.org/solr/):

   * Solr versione 7.0
   * Solr richiede Java 1.7 o versione successiva
   * Nessun servizio necessario
   * Scelta delle modalità di esecuzione:
      * Modalità autonoma
      * [Modalità SolrCloud](solr.md#solrcloud-mode)  (consigliata per ambienti di produzione)
   * Scelta della ricerca multilingue (MLS):
      * [Installazione di MLS standard](solr.md#installing-standard-mls)
      * [Installazione di MLS avanzate](solr.md#installing-advanced-mls)

## Configurazione MongoDB {#mongodb-configuration}

### Seleziona MSRP {#select-msrp}

La [console di configurazione dello storage](srp-config.md) consente di selezionare la configurazione di archiviazione predefinita, che identifica l&#39;implementazione dell&#39;SRP da utilizzare.

Per accedere alla console di configurazione dell&#39;archiviazione, all&#39;autore:

* Dalla navigazione globale, selezionare **[!UICONTROL Strumenti]** > **[!UICONTROL Community]** > **[!UICONTROL Configurazione archiviazione]**.

![msrp](assets/msrp.png)

* Selezionare **[!UICONTROL Provider risorsa di archiviazione MongoDB (MSRP)]**
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

      Per un gruppo ZooKeeper, immetti valori `HOST:PORT` separati da virgole, ad esempio *host1:2181,host2:2181*

      Lasciare vuoto se si esegue Solr in modalità autonoma utilizzando lo ZooKeeper interno.
      *Predefinito*:  *&lt;blank>*

      * **[!UICONTROL Solr]**
URLTl&#39;URL utilizzato per comunicare con Solr in modalità autonoma.
Lascia vuoto se l’esecuzione è in modalità SolrCloud.

         *Predefinito*: https://127.0.0.1:8983/solr/

      * **[!UICONTROL Solr]**
CollectionNome della raccolta Solr.

         *Predefinito*: collection1

* Seleziona **[!UICONTROL Invia]**

>[!NOTE]
>
>Il database mongoDB, che per impostazione predefinita corrisponde al nome `communities`, non deve essere impostato sul nome di un database utilizzato per [archivi nodi o archivi dati (binari)](../../help/sites-deploying/data-store-config.md). Vedere anche [Elementi di storage in AEM 6.5](../../help/sites-deploying/storage-elements-in-aem-6.md).

### Set di replica MongoDB {#mongodb-replica-set}

Per l&#39;ambiente di produzione, si consiglia vivamente di configurare un set di repliche, un cluster di server MongoDB che implementa la replica primaria-secondaria e il failover automatizzato.

Per ulteriori informazioni sui set di repliche, visita la documentazione di MongoDB [Replica](https://docs.mongodb.org/manual/replication/) .

Per utilizzare i set di repliche e imparare a definire le connessioni tra le applicazioni e le istanze MongoDB, visita la documentazione di MongoDB [Formato URI stringa di connessione](https://docs.mongodb.org/manual/reference/connection-string/) .

#### Url di esempio per la connessione a un set di replica  {#example-url-for-connecting-to-a-replica-set}

```shell
# Example url for:
# servers "mongoserver1", "mongoserver2", "mongoserver3"
# replica set 'rs0'
# port numbers only necessary if not default port 27017
mongodb://mongoserver1:<mongoport1>,mongoserver2:<mongoport2>,mongoserver3:<mongoport3>/?replicaSet=rs0&maxPoolSize=100&waitQueueMultiple=50&readPreference=secondaryPreferred
```

## Configurazione Solr {#solr-configuration}

Un&#39;installazione Solr può essere condivisa tra l&#39;archivio nodi (Oak) e l&#39;archivio comune (MSRP) utilizzando diverse raccolte.

Se le raccolte Oak e MSRP vengono utilizzate intensamente, è possibile installare un secondo Solr per motivi di prestazioni.

Per gli ambienti di produzione, la [modalità SolrCloud](solr.md#solrcloud-mode) offre prestazioni migliori rispetto alla modalità autonoma (una singola configurazione Solr locale).

Per i dettagli di configurazione, consulta [Configurazione solare per SRP](solr.md).

### Aggiornamento {#upgrading}

Se esegui l’aggiornamento da una versione precedente configurata con MSRP, sarà necessario:

1. Esegui l’ [aggiornamento ad AEM Communities](upgrade.md)
1. Installa nuovi file di configurazione Solr
   * Per [MLS standard](solr.md#installing-standard-mls)
   * Per [MLS avanzate](solr.md#installing-advanced-mls)
1. Reindicizza MSRP
Vedere la sezione [Strumento di reindicizzazione MSRP](#msrp-reindex-tool)

## Pubblicazione della configurazione {#publishing-the-configuration}

MSRP deve essere identificato come archivio comune su tutte le istanze di authoring e pubblicazione.

Per rendere disponibile nell’ambiente di pubblicazione la configurazione identica, accedi all’istanza dell’autore e segui i passaggi seguenti:

* Passa dal menu principale a **[!UICONTROL Strumenti]** > **[!UICONTROL Operazioni]** > **[!UICONTROL Replica]**.
* Seleziona **[!UICONTROL Attiva albero]**
* **[!UICONTROL Percorso iniziale]**:
   * Vai a `/etc/socialconfig/srpc/`
* Seleziona **[!UICONTROL Attiva]**

## Gestione dei dati utente {#managing-user-data}

Per informazioni sugli *utenti*, *profili utente* e *gruppi di utenti*, spesso inseriti nell&#39;ambiente di pubblicazione, visita

* [Sincronizzazione utente](sync.md)
* [Gestione di utenti e gruppi di utenti](users.md)

## Strumento di reindicizzazione MSRP {#msrp-reindex-tool}

Esiste un endpoint HTTP per la reindicizzazione di Solr per MSRP quando si installano nuovi file di configurazione o si ripara un indice Solr danneggiato.

Con questo strumento, MongoDB è la fonte di *verità* per MSRP; i backup devono essere eseguiti solo da MongoDB.

L&#39;intero albero UGC può essere reindicizzato, o solo un sottoalbero specifico, come specificato dal parametro *path *data.

Questo strumento può essere eseguito dalla riga di comando utilizzando cURL o qualsiasi altro strumento HTTP.

Durante la reindicizzazione, esiste un compromesso tra memoria e prestazioni controllato dal parametro *batchSize *data, che specifica quanti record UGC vengono reindicizzati per batch.

Un valore di default ragionevole è 5000:

* Se la memoria è un problema, specifica un numero più piccolo
* Se la velocità è un problema, specifica un numero maggiore per aumentare la velocità

### Esecuzione dello strumento di reindicizzazione MSRP tramite il comando cURL {#running-msrp-reindex-tool-using-curl-command}

Il seguente comando cURL mostra ciò che è necessario per una richiesta HTTP per reindicizzare UGC memorizzato in MSRP.

Il formato di base è:

cURL -u *signin* -d *data* *reindex-url*

*signin* = administrator-id:password Ad esempio: admin:admin

*data* = &quot;batchSize=*size*&amp;path=*path&quot;*

*size*  = quante voci UGC reindicizzare per operazione 
`/content/usergenerated/asi/mongo/`

*path* = la posizione principale dell&#39;albero dell&#39;UGC da reindicizzare

* Per reindicizzare tutti gli UGC, specifica il valore della proprietà `asipath`di
   `/etc/socialconfig/srpc/defaultconfiguration`
* Per limitare l&#39;indice ad alcuni UGC, specifica una sottostruttura di `asipath`

*reindex-url* = l&#39;endpoint per la reindicizzazione dell&#39;SRP 
`http://localhost:4503/services/social/datastore/mongo/reindex`

>[!NOTE]
>
>Se stai [reindicizzando DSRP Solr](dsrp.md), l&#39;URL è **/services/social/datastore/rdb/reindex**

### Esempio di reindicizzazione MSRP {#msrp-reindex-example}

```shell
curl -s -u admin:admin -d 'batchSize=10000&path=/content/usergenerated/asi/mongo/' http://localhost:4503/services/social/datastore/mongo/reindex
```

## Come demo MSRP {#how-to-demo-msrp}

Per configurare MSRP per un ambiente di dimostrazione o sviluppo, consulta [Come impostare MongoDB per Demo](demo-mongo.md).

## Risoluzione dei problemi {#troubleshooting}

### UGC non visibile in MongoDB {#ugc-not-visible-in-mongodb}

Assicurati che MSRP sia stato configurato come provider predefinito controllando la configurazione dell&#39;opzione di archiviazione. Per impostazione predefinita, il provider delle risorse di archiviazione è JSRP.

Su tutte le istanze di authoring e pubblicazione AEM, rivedi la [console di configurazione dello storage](srp-config.md) o controlla l&#39;archivio AEM:

* In JCR, se [/etc/socialconfig](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/)

   * Non contiene un nodo [srpc](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc), significa che il provider di archiviazione è JSRP.
   * Se il nodo srpc esiste e contiene il nodo [defaultconfiguration](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc/defaultconfiguration), le proprietà della configurazione predefinita devono definire MSRP come provider predefinito.

### UGC scompare dopo l&#39;aggiornamento {#ugc-disappears-after-upgrade}

Se esegui l’aggiornamento da un sito AEM Communities 6.0 esistente, qualsiasi UGC preesistente deve essere convertito in conformità alla struttura richiesta per l’ [SRP](srp.md) API dopo l’aggiornamento ad AEM Communities 6.3.

È disponibile uno strumento open source su GitHub a questo scopo:

* [Strumento di migrazione UGC di AEM Communities](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)

Lo strumento di migrazione può essere personalizzato per esportare UGC da versioni precedenti di AEM social community per l’importazione in AEM Communities 6.1 o versioni successive.

### Errore - id_provider del campo non definito {#error-undefined-field-provider-id}

Se nei registri viene visualizzato il seguente errore, indica che il file dello schema Solr non è configurato correttamente.

#### JsonMappingException: field provider_id non definito {#jsonmappingexception-undefined-field-provider-id}

```xml
Caused by: com.fasterxml.jackson.databind.JsonMappingException: undefined field provider_id
at com.fasterxml.jackson.databind.ser.DefaultSerializerProvider.serializeValue(DefaultSerializerProvider.java:129)
at com.fasterxml.jackson.databind.ObjectMapper.writeValue(ObjectMapper.java:1819)
at com.adobe.cq.social.scf.core.BaseSocialComponent.toJSONString(BaseSocialComponent.java:196)
... 124 common frames omitted
```

Per risolvere l&#39;errore, quando segui le istruzioni per [Installazione di MLS standard](solr.md#installing-standard-mls), assicurati:

* I file di configurazione XML sono stati copiati nel percorso Solr corretto.
* Solr è stato riavviato dopo che i nuovi file di configurazione hanno sostituito quelli esistenti.

### Connessione sicura a MongoDB non riuscita {#secure-connection-to-mongodb-fails}

Se un tentativo di stabilire una connessione protetta al server MongoDB non riesce a causa di una definizione di classe mancante, è necessario aggiornare il bundle del driver MongoDB, `mongo-java-driver`, disponibile dall&#39;archivio maven pubblico.

1. Scarica il driver da [https://search.maven.org/#artifactdetails%7Corg.mongodb%7Cmongo-java-driver%7C2.13.2%7Cjar](https://search.maven.org/#artifactdetails%7Corg.mongodb%7Cmongo-java-driver%7C2.13.2%7Cjar) (versione 2.13.2 o successiva).
1. Copia il bundle nella cartella &quot;crx-quickstart/install&quot; per un&#39;istanza AEM.
1. Riavvia l&#39;istanza AEM.

## Riferimenti {#resources}

* [AEM con MongoDB](../../help/sites-deploying/aem-with-mongodb.md)
* [Documentazione MongoDB](https://docs.mongodb.org/)
