---
title: Come impostare MongoDB per la demo
seo-title: Come impostare MongoDB per la demo
description: Come impostare MSRP per un'istanza di authoring e un'istanza di pubblicazione
seo-description: Come impostare MSRP per un'istanza di authoring e un'istanza di pubblicazione
uuid: d2035a9e-f05c-4f90-949d-7cdae9646750
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 0b126218-b142-4d33-a28c-a91ab4fe99ac
role: Admin
exl-id: 7e257b34-a0f5-47db-b1a9-e26333c287d9
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '792'
ht-degree: 1%

---

# Come impostare MongoDB per la demo {#how-to-setup-mongodb-for-demo}

## Introduzione {#introduction}

Questa esercitazione descrive come impostare [MSRP](msrp.md) per *un&#39;istanza author* e *un&#39;istanza publish*.

Con questa configurazione, il contenuto della community è accessibile sia dagli ambienti di authoring che da quelli di pubblicazione senza dover inoltrare o invertire i contenuti generati dagli utenti (UGC).

Questa configurazione è adatta per ambienti *non di produzione*, ad esempio per lo sviluppo e/o la dimostrazione.

**Un ambiente  ** produttivo dovrebbe:**

* Esegui MongoDB con un set di replica
* Usa SolrCloud
* Contenere più istanze di pubblicazione

## MongoDB {#mongodb}

### Installa MongoDB {#install-mongodb}

* Scarica MongoDB da [https://www.mongodb.org/](https://www.mongodb.org/)

   * Scelta del sistema operativo:

      * Linux
      * Mac 10.8
      * Windows 7
   * Scelta della versione:

      * Come minimo, utilizza la versione 2.6 di


* Configurazione di base

   * Seguire le istruzioni di installazione di MongoDB.
   * Configura per mongod:

      * Non è necessario configurare monghi o condivisioni.
   * La cartella MongoDB installata verrà definita &lt;mongo-install>.
   * Il percorso definito della directory dati verrà indicato come &lt;mongo-dbpath>.


* MongoDB può essere eseguito sullo stesso host AEM o in remoto.

### Avvia MongoDB {#start-mongodb}

* &lt;mongo-install>/bin/mongod —dbpath  &lt;mongo-dbpath>

Verrà avviato un server MongoDB utilizzando la porta predefinita 27017.

* Per Mac, aumentare l&#39;ulimit con start &#39;ulimit -n 2048&#39;

>[!NOTE]
>
>Se MongoDB viene avviato *dopo* AEM, **riavvia** tutte le istanze **AEM** in modo che si connettano correttamente a MongoDB.

### Opzione di produzione demo: Imposta set di replica MongoDB {#demo-production-option-setup-mongodb-replica-set}

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

### Installa Solr {#install-solr}

* Scarica Solr da [Apache Lucene](https://archive.apache.org/dist/lucene/solr/):

   * Adatto a qualsiasi sistema operativo.
   * Solr versione 7.0.
   * Solr richiede Java 1.7 o versione successiva.

* Configurazione di base

   * Segui l&#39;impostazione Solr di esempio.
   * Nessun servizio necessario.
   * La cartella Solr installata verrà definita &lt;solr-install>.

### Configurare Solr per AEM Communities {#configure-solr-for-aem-communities}

Per configurare una raccolta Solr per MSRP per la demo, ci sono due decisioni da prendere (seleziona i link alla documentazione principale per i dettagli):

1. Esegui Solr in modalità autonoma o [SolrCloud](msrp.md#solrcloudmode).
1. Installa [standard](msrp.md#installingstandardmls) o [advanced](msrp.md#installingadvancedmls) multilingue search (MLS).

### Solr indipendente {#standalone-solr}

Il metodo di esecuzione di Solr può variare a seconda della versione e del modo di installazione. La [Guida di riferimento Solr](https://archive.apache.org/dist/lucene/solr/ref-guide/) è la documentazione autorevole.

Per semplicità, utilizzando la versione 4.10 come esempio, avvia Solr in modalità autonoma:

* da cd a &lt;solrinstall>/example
* java -jar start.jar

Verrà avviato un server Solr HTTP utilizzando la porta predefinita 8983. È possibile accedere alla console Solr per ottenere una console Solr da testare.

* Console Solr predefinita: [http://localhost:8983/solr/](http://localhost:8983/solr/)

>[!NOTE]
>
>Se Solr Console non è disponibile, controlla i registri in &lt;solrinstall>/example/logs. Cerca di vedere se SOLR sta tentando di eseguire un binding con un nome host specifico che non può essere risolto (ad esempio &quot;user-macbook-pro&quot;).
In tal caso, aggiorna il file etc/hosts con una nuova voce per questo nome host (ad esempio 127.0.0.1 user-macbook-pro) e Solr si avvierà correttamente.

### SolrCloud {#solrcloud}

Per eseguire una configurazione di solrCloud di base (non di produzione), inizia con:

* `java -Dbootstrap_confdir=./solr/collection1/conf -Dbootstrap_conf=true -DzkRun -jar start.jar`

## Identifica MongoDB come archivio comune {#identify-mongodb-as-common-store}

Avvia l’istanza di authoring e pubblica AEM, se necessario.

Se AEM era in esecuzione prima dell&#39;avvio di MongoDB, è necessario riavviare le istanze AEM.

Segui le istruzioni riportate nella pagina principale della documentazione: [MSRP - Archivio comune MongoDB](msrp.md)

## Prova {#test}

Per testare e verificare l&#39;archivio comune MongoDB, pubblica un commento sull&#39;istanza di pubblicazione e visualizzalo sull&#39;istanza dell&#39;autore, nonché visualizza l&#39;UGC in MongoDB e Solr:

1. Nell&#39;istanza di pubblicazione, vai alla pagina [Guida ai componenti della community](http://localhost:4503/content/community-components/en/comments.html) e seleziona il componente Commenti .
1. Accedi per pubblicare un commento:
1. Inserisci il testo nella casella di immissione testo commento e fai clic su **[!UICONTROL Post]**

   ![post-commento](assets/post-comment.png)

1. È sufficiente visualizzare il commento sull&#39; [istanza autore](http://localhost:4502/content/community-components/en/comments.html) (probabilmente ancora connesso come amministratore / amministratore).

   ![view-comment](assets/view-comment.png)

   Nota: Anche se ci sono nodi JCR sotto il *asipath* sull&#39;autore, questi sono per il framework SCF. L&#39;UGC effettivo non è in JCR, è nel MongoDB.

1. Visualizza l&#39;UGC nel mongodb **[!UICONTROL Communities]** > **[!UICONTROL Raccolte]** > **[!UICONTROL Contenuto]**

   ![contenuto in ugc](assets/ugc-content.png)

1. Visualizza l&#39;UGC in Solr:

   * Sfoglia il quadro comandi Solr: [http://localhost:8983/solr/](http://localhost:8983/solr/).
   * Utente `core selector` da selezionare `collection1`.
   * Seleziona `Query`.
   * Seleziona `Execute Query`.

   ![ugc-solr](assets/ugc-solr.png)

## Risoluzione dei problemi {#troubleshooting}

### Nessun UGC visualizzato {#no-ugc-appears}

1. Assicurati che MongoDB sia installato ed eseguito correttamente.

1. Assicurati che MSRP sia stato configurato come provider predefinito:

   * Su tutte le istanze di authoring e pubblicazione AEM, rivedi la [console di configurazione dello storage](srp-config.md) o controlla l&#39;archivio AEM:

   * In JCR, se [/etc/socialconfig](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/) non contiene un nodo [srpc](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc), significa che il provider di archiviazione è JSRP.
   * Se il nodo srpc esiste e contiene il nodo [defaultconfiguration](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc/defaultconfiguration), le proprietà della configurazione predefinita devono definire MSRP come provider predefinito.

1. Assicurati che AEM riavviato dopo aver selezionato MSRP.
