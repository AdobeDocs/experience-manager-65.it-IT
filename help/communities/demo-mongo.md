---
title: Come impostare MongoDB per la demo
description: Impostare MSRP per un'istanza di authoring e un'istanza di pubblicazione
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 7e257b34-a0f5-47db-b1a9-e26333c287d9
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '726'
ht-degree: 0%

---

# Come impostare MongoDB per la demo {#how-to-setup-mongodb-for-demo}

## Introduzione {#introduction}

Questo tutorial descrive come configurare [MSRP](msrp.md) per *una istanza Autore* e *una istanza Publish*.

Con questa configurazione, il contenuto della community è accessibile sia dagli ambienti di authoring che da quelli di pubblicazione senza la necessità di inoltrare o invertire i contenuti generati dagli utenti (UGC, User-Generated Content).

Questa configurazione è adatta per *ambienti non di produzione* come ad esempio per lo sviluppo e/o la dimostrazione.

**Un ambiente *produzione* deve:**

* Eseguire MongoDB con un set di repliche
* Usa SolrCloud
* Contengono più istanze di pubblicazione

## MongoDB {#mongodb}

### Installare MongoDB {#install-mongodb}

* Scarica MongoDB da [https://www.mongodb.com/](https://www.mongodb.com/)

   * Scelta del sistema operativo:

      * Linux®
      * Mac 10.8
      * Windows 7

   * Scelta versione:

      * Utilizza almeno la versione 2.6

* Configurazione di base

   * Seguire le istruzioni di installazione di MongoDB.
   * Configura per monGod:

      * Non è necessario configurare i monghi o la condivisione.

   * La cartella MongoDB installata è denominata &lt;mongo-install>.
   * Il percorso della directory dati definito è denominato &lt;mongo-dbpath>.

* MongoDB può essere eseguito sullo stesso host dell’AEM o in remoto.

### Avvia MongoDB {#start-mongodb}

* &lt;mongo-install>/bin/monGod —dbpath &lt;mongo-dbpath>

Verrà avviato un server MongoDB utilizzando la porta predefinita 27017.

* Per Mac, aumenta ulimit con argomento di inizio &#39;ulimit -n 2048&#39;

>[!NOTE]
>
>Se MongoDB viene avviato *dopo* AEM, **riavviare** tutte le **istanze AEM** in modo che si connettano correttamente a MongoDB.

### Opzione produzione demo: Imposta replica MongoDB impostata {#demo-production-option-setup-mongodb-replica-set}

I seguenti comandi sono un esempio di configurazione di un set di repliche con 3 nodi su localhost:

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

### Installare Solr {#install-solr}

* Scarica Solr da [Apache Lucene](https://archive.apache.org/dist/lucene/solr/):

   * Adatto a qualsiasi sistema operativo.
   * Solr versione 7.0.
   * Solr richiede Java™ 1.7 o versione successiva.

* Configurazione di base

   * Segui l’impostazione Solr di esempio.
   * Nessun servizio richiesto.
   * La cartella Solr installata è denominata &lt;solr-install>.

### Configurare Solr per AEM Communities {#configure-solr-for-aem-communities}

Per configurare una raccolta Solr per MSRP per la dimostrazione, è necessario prendere due decisioni (per informazioni dettagliate, seleziona i collegamenti alla documentazione principale):

1. Esegui Solr in modalità standalone o [SolrCloud](msrp.md#solrcloudmode).
1. Installa [standard](msrp.md#installingstandardmls) o [advanced](msrp.md#installingadvancedmls) ricerca multilingue (MLS).

### Solr standalone {#standalone-solr}

Il metodo di esecuzione di Solr può variare a seconda della versione e delle modalità di installazione. La [Guida di riferimento Solr](https://archive.apache.org/dist/lucene/solr/ref-guide/) è la documentazione autorevole.

Per semplicità, utilizzando la versione 4.10 come esempio, avviare Solr in modalità standalone:

* da cd a &lt;solrinstall>/esempio
* Java™ -jar start.jar

Questo processo avvia un server HTTP Solr utilizzando la porta predefinita 8983. È possibile passare alla console Solr per ottenere una console Solr da testare.

* console Solr predefinita: [http://localhost:8983/solr/](http://localhost:8983/solr/)

>[!NOTE]
>
>Se la console Solr non è disponibile, controllare i registri in &lt;solrinstall>/example/logs. Verificare se SOLR sta tentando di eseguire il binding a un nome host specifico che non può essere risolto (ad esempio, &quot;user-macbook-pro&quot;).
>
In tal caso, aggiornare il file `etc/hosts` con una nuova voce per questo nome host (ad esempio, 127.0.0.1 user-macbook-pro) in modo da avviare correttamente Solr.

### SolrCloud {#solrcloud}

Per eseguire un&#39;installazione di base (non di produzione) di solrCloud, avvia solr con:

* `java -Dbootstrap_confdir=./solr/collection1/conf -Dbootstrap_conf=true -DzkRun -jar start.jar`

## Identificare MongoDB come Common Store {#identify-mongodb-as-common-store}

Avvia l’authoring e pubblica le istanze AEM, se necessario.

Se l’AEM era in esecuzione prima dell’avvio di MongoDB, è necessario riavviare le istanze dell’AEM.

Segui le istruzioni riportate nella pagina della documentazione principale: [MSRP - MongoDB Common Store](msrp.md)

## Test {#test}

Per testare e verificare il Common Store MongoDB, pubblica un commento sull’istanza Publish e visualizzalo sull’istanza Autore, quindi visualizza il UGC in MongoDB e Solr:

1. Nell&#39;istanza di pubblicazione passare alla pagina [Guida ai componenti della community](http://localhost:4503/content/community-components/en/comments.html) e selezionare il componente Commenti.
1. Effettua l&#39;accesso per pubblicare un commento:
1. Immettere il testo nella casella di immissione testo commento e fare clic su **[!UICONTROL Post]**

   ![post-commento](assets/post-comment.png)

1. È sufficiente visualizzare il commento nell&#39;[istanza autore](http://localhost:4502/content/community-components/en/comments.html) (probabilmente è ancora connesso come amministratore/amministratore).

   ![visualizza-commento](assets/view-comment.png)

   Nota: sebbene siano presenti nodi JCR in *asipath* sull&#39;istanza di authoring, questi sono per il framework SCF. L’UGC effettivo non è in JCR, ma in MongoDB.

1. Visualizza UGC in mongodb **[!UICONTROL Communities]** > **[!UICONTROL Raccolte]** > **[!UICONTROL Contenuto]**

   ![contenuto-ugc](assets/ugc-content.png)

1. Visualizza UGC in Solr:

   * Passa alla dashboard Solr: [http://localhost:8983/solr/](http://localhost:8983/solr/).
   * Utente `core selector` per selezionare `collection1`.
   * Selezionare `Query`.
   * Selezionare `Execute Query`.

   ![ugc-solr](assets/ugc-solr.png)

## Risoluzione dei problemi {#troubleshooting}

### Nessun UGC visualizzato {#no-ugc-appears}

1. Assicurati che MongoDB sia installato e funzioni correttamente.

1. Verificare che MSRP sia stato configurato come provider predefinito:

   * Su tutte le istanze AEM di authoring e pubblicazione, visitare nuovamente la [console Configurazione archiviazione](srp-config.md) oppure controllare l&#39;archivio AEM:

   * In JCR, se [/etc/socialconfig](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/) non contiene un nodo [srpc](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc), significa che il provider di archiviazione è JSRP.
   * Se il nodo srpc esiste e contiene il nodo [defaultconfiguration](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc/defaultconfiguration), le proprietà di default configuration devono definire MSRP come provider predefinito.

1. Assicurati che l’AEM sia stato riavviato dopo la selezione di MSRP.
