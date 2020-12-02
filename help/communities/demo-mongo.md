---
title: Come impostare MongoDB per la demo
seo-title: Come impostare MongoDB per la demo
description: Come impostare MSRP per un’istanza di creazione e un’istanza di pubblicazione
seo-description: Come impostare MSRP per un’istanza di creazione e un’istanza di pubblicazione
uuid: d2035a9e-f05c-4f90-949d-7cdae9646750
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 0b126218-b142-4d33-a28c-a91ab4fe99ac
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '792'
ht-degree: 1%

---


# Come impostare MongoDB per la demo {#how-to-setup-mongodb-for-demo}

## Introduzione {#introduction}

Questa esercitazione descrive come impostare [MSRP](msrp.md) per *un&#39;istanza di autore* e *un&#39;istanza di pubblicazione*.

Con questa configurazione, il contenuto della community è accessibile sia dall’ambiente di creazione che da quello di pubblicazione senza dover inoltrare o invertire il contenuto generato dall’utente (UGC).

Questa configurazione è adatta per ambienti *non di produzione*, ad esempio per lo sviluppo e/o la dimostrazione.

**Un ambiente  ** produttivo dovrebbe:**

* Eseguire MongoDB con un set di repliche
* Usa SolrCloud
* Contengono più istanze di editore

## MongoDB {#mongodb}

### Installazione di MongoDB {#install-mongodb}

* Scarica MongoDB da [https://www.mongodb.org/](https://www.mongodb.org/)

   * Scelta del sistema operativo:

      * Linux
      * Mac 10.8
      * Windows 7
   * Scelta della versione:

      * Utilizzate almeno la versione 2.6


* Configurazione di base

   * Seguite le istruzioni di installazione di MongoDB.
   * Configura per mondio:

      * Non è necessario configurare i logo o la condivisione.
   * La cartella MongoDB installata verrà denominata &lt;mongo-install>.
   * Il percorso definito della directory dati verrà denominato &lt;percorso-mongo>.


* MongoDB può essere eseguito sullo stesso host AEM o eseguito in remoto.

### Avvia MongoDB {#start-mongodb}

* &lt;mongo-install>/bin/mondio —dbpath  &lt;mongo-dbpath>

Verrà avviato un server MongoDB utilizzando la porta predefinita 27017.

* Per Mac, aumentare il limite con l&#39;inizio arg &#39;ulimit -n 2048&#39;

>[!NOTE]
>
>Se MongoDB viene avviato *dopo* AEM, **riavviare** tutte le istanze **AEM** in modo che si connettano correttamente a MongoDB.

### Opzione Produzione Demo: Imposta set di replica MongoDB {#demo-production-option-setup-mongodb-replica-set}

I comandi seguenti sono un esempio di configurazione di un set di repliche con 3 nodi in localhost:

* `bin/mongod --port 27017 --dbpath data --replSet rs0&`
* `bin/mongo`

   * `cfg = {"_id": "rs0","version": 1,"members": [{"_id": 0,"host": "127.0.0.1:27017"}]}`
   * `rs.initiate(cfg)`

* `bin/mongod --port 27018 --dbpath data1 --replSet rs0&`
* `bin/mongod --port 27019 --dbpath data2 --replSet rs0&`
* `bin/mongo`

   * `rs.add("127.0.0.1:27018")`
   * `rs.add("127.0.0.1:27019")`
   * `rs.status()`

## Solr {#solr}

### Installazione di Solr {#install-solr}

* Scarica Solr da [Apache Lucene](https://archive.apache.org/dist/lucene/solr/):

   * Ideale per qualsiasi sistema operativo.
   * Solr versione 7.0.
   * Solr richiede Java 1.7 o versione successiva.

* Configurazione di base

   * Seguite l&#39;esempio di impostazione Solr.
   * Nessun servizio necessario.
   * La cartella Solr installata verrà denominata &lt;solr-install>.

### Configurare Solr per  AEM Communities {#configure-solr-for-aem-communities}

Per configurare una raccolta Solr per MSRP per la demo, sono necessarie due decisioni (per i dettagli, selezionare i collegamenti alla documentazione principale):

1. Eseguire Solr in modalità standalone o [SolrCloud](msrp.md#solrcloudmode).
1. Installate [standard](msrp.md#installingstandardmls) o [advanced](msrp.md#installingadvancedmls) multilingual search (MLS).

### Solr autonomo {#standalone-solr}

Il metodo di esecuzione di Solr può variare a seconda della versione e del modo di installazione. La [Guida di riferimento Solr](https://archive.apache.org/dist/lucene/solr/ref-guide/) è la documentazione autorevole.

Per semplicità, utilizzando la versione 4.10 come esempio, avviate Solr in modalità standalone:

* da CD a &lt;solrinstall>/example
* java -jar start.jar

Verrà avviato un server Solr HTTP utilizzando la porta predefinita 8983. Per ottenere una console Solr da testare, è possibile accedere alla console Solr.

* console Solr predefinita: [http://localhost:8983/solr/](http://localhost:8983/solr/)

>[!NOTE]
>
>Se Console Solr non è disponibile, controlla i registri in &lt;solrinstall>/example/logs. Verificare se SOLR sta tentando di eseguire un binding con un nome host specifico che non può essere risolto (ad es. &quot;user-macbook-pro&quot;).
In tal caso, aggiornate il file etc/hosts con una nuova voce per questo nome host (ad esempio 127.0.0.1 user-macbook-pro) e Solr verrà avviato correttamente.

### SolrCloud {#solrcloud}

Per eseguire una configurazione solrCloud di base (non di produzione), inizia da:

* `java -Dbootstrap_confdir=./solr/collection1/conf -Dbootstrap_conf=true -DzkRun -jar start.jar`

## Identificare MongoDB come archivio comune {#identify-mongodb-as-common-store}

Avviate le istanze di creazione e pubblicazione AEM, se necessario.

Se AEM in esecuzione prima dell&#39;avvio di MongoDB, è necessario riavviare le istanze AEM.

Seguite le istruzioni riportate nella pagina principale della documentazione: [MSRP - MongoDB Common Store](msrp.md)

## Prova {#test}

Per testare e verificare lo store comune MongoDB, pubblicate un commento sull’istanza di pubblicazione e visualizzatela nell’istanza di creazione, nonché visualizzate l’UGC in MongoDB e Solr:

1. Nell&#39;istanza di pubblicazione, andare alla pagina [Guida ai componenti della community](http://localhost:4503/content/community-components/en/comments.html) e selezionare il componente Commenti.
1. Accedete per pubblicare un commento:
1. Immettete il testo nella casella di immissione del commento e fate clic su **[!UICONTROL Post]**

   ![post-commento](assets/post-comment.png)

1. È sufficiente visualizzare il commento sull&#39; [istanza di creazione](http://localhost:4502/content/community-components/en/comments.html) (probabilmente ancora eseguito l&#39;accesso come amministratore / amministratore).

   ![view-comment](assets/view-comment.png)

   Nota: Sebbene sull&#39;autore siano presenti nodi JCR sotto il percorso *asipath*, questi sono per il framework SCF. L&#39;UGC effettivo non è in JCR, è in MongoDB.

1. Visualizzare l&#39;UGC in mongodb **[!UICONTROL Communities]** > **[!UICONTROL Collections]** > **[!UICONTROL Content]**

   ![ugc-content](assets/ugc-content.png)

1. Visualizzare l’UGC in Solr:

   * Passa al dashboard Solr: [http://localhost:8983/solr/](http://localhost:8983/solr/).
   * Utente `core selector` per selezionare `collection1`.
   * Seleziona `Query`.
   * Seleziona `Execute Query`.

   ![ugc-solr](assets/ugc-solr.png)

## Risoluzione dei problemi {#troubleshooting}

### Nessun UGC visualizzato {#no-ugc-appears}

1. Verificare che MongoDB sia installato ed eseguito correttamente.

1. Verificate che MSRP sia stato configurato come provider predefinito:

   * Per tutte le istanze di creazione e pubblicazione AEM, rivisitate la [console di configurazione dell&#39;archivio](srp-config.md) o verificate l&#39;archivio AEM:

   * In JCR, se [/etc/socialconfig](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/) non contiene un nodo [srpc](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc), significa che il provider di storage è JSRP.
   * Se il nodo srpc esiste e contiene il nodo [defaultconfiguration](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc/defaultconfiguration), le proprietà della configurazione predefinita devono definire MSRP come provider predefinito.

1. Verificare che AEM sia stato riavviato dopo aver selezionato MSRP.
