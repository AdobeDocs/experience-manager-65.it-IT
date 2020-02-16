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
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Come impostare MongoDB per la demo {#how-to-setup-mongodb-for-demo}

## Introduzione {#introduction}

Questa esercitazione descrive come impostare [MSRP](msrp.md) per *un’istanza di creazione* e *un’istanza di pubblicazione* .

Con questa configurazione, il contenuto della community è accessibile sia dall’ambiente di creazione che da quello di pubblicazione senza dover inoltrare o invertire il contenuto generato dall’utente (UGC).

Questa configurazione è ideale per ambienti *non di produzione* , ad esempio per lo sviluppo e/o la dimostrazione.

**Un ambiente *produttivo*dovrebbe:**

* Eseguire MongoDB con un set di repliche
* Usa SolrCloud
* Contengono più istanze di editore

## MongoDB {#mongodb}

### Installazione di MongoDB {#install-mongodb}

* Scaricate MongoDB da [https://www.mongodb.org/](https://www.mongodb.org/)

   * Scelta del sistema operativo:

      * Linux
      * Mac 10.8
      * Windows 7
   * Scelta della versione:

      * Utilizzate almeno la versione 2.6


* Configurazione di base

   * Seguire le istruzioni di installazione di MongoDB
   * Configura per mondio

      * Non è necessario configurare i logo o la condivisione
   * La cartella MongoDB installata verrà denominata &lt;mongo-install>
   * Il percorso della directory dati definita sarà denominato &lt;percorso-mongo>


* MongoDB può essere eseguito sullo stesso host di AEM o in remoto

### Avvia MongoDB {#start-mongodb}

* &lt;mongo-install>/bin/mondio —dbpath &lt;mongo-dbpath>

Verrà avviato un server MongoDB utilizzando la porta predefinita 27017.

* Per Mac, aumentare il limite con l&#39;inizio arg &#39;ulimit -n 2048&#39;

>[!NOTE]
>
>Se MongoDB viene avviato *dopo *AEM, **riavviare **tutte le istanze **AEM **in modo che si connettano correttamente a MongoDB.

### Opzione Produzione Demo: Imposta set di replica MongoDB {#demo-production-option-setup-mongodb-replica-set}

I comandi seguenti sono un esempio di configurazione di un set di repliche con 3 nodi in localhost:

* bin/mondio —port 27017 —dbpath data —replSet rs0&amp;
* bin/mongo

   * cfg = {&quot;_id&quot;: &quot;rs0&quot;,&quot;version&quot;: 1,&quot;membri&quot;: [{&quot;_id&quot;: 0,&quot;host&quot;: &quot;127.0.0.1:27017&quot;}]}
   * rs.start(cfg)

* bin/mondio —porta 27018 —dbpath data1 —replSet rs0&amp;
* bin/mondio —porta 27019 —dbpath data2 —replSet rs0&amp;
* bin/mongo

   * rs.add(&quot;127.0.0.1:27018&quot;)
   * rs.add(&quot;127.0.0.1:27019&quot;)
   * rs.status()

## Solr {#solr}

### Installa Solr {#install-solr}

* Scarica Solr da [Apache Lucene](https://archive.apache.org/dist/lucene/solr/):

   * Ideale per qualsiasi sistema operativo
   * Utilizzare la versione 4.10 o 5
   * Solr richiede Java 1.7 o versione successiva

* Configurazione di base

   * Segui l&#39;esempio di impostazione del solr
   * Nessun servizio necessario
   * La cartella Solr installata sarà denominata &lt;solr-install>

### Configurare Solr per AEM Communities {#configure-solr-for-aem-communities}

Per configurare una raccolta Solr per MSRP per la demo, sono necessarie due decisioni (per i dettagli, selezionare i collegamenti alla documentazione principale):

1. Eseguire Solr in modalità standalone o [SolrCloud](msrp.md#solrcloudmode)
1. Installare la ricerca [standard](msrp.md#installingstandardmls) o [avanzata](msrp.md#installingadvancedmls) in più lingue (MLS)

### Solar standalone {#standalone-solr}

Il metodo di esecuzione di Solr può variare a seconda della versione e del modo di installazione. La guida [di riferimento](https://archive.apache.org/dist/lucene/solr/ref-guide/) Solr è la documentazione autorevole.

Per semplicità, utilizzando la versione 4.10 come esempio, avviate Solr in modalità standalone:

* da CD a &lt;solrinstall>/example
* java -jar start.jar

Verrà avviato un server Solr HTTP utilizzando la porta predefinita 8983. Per ottenere una console Solr per il test, potete accedere alla console Solr.

* console Solr predefinita: [http://localhost:8983/solr/](http://localhost:8983/solr/)

>[!NOTE]
>
>Se Console Solr non è disponibile, controlla i registri in &lt;solrinstall>/example/logs. Verificare se SOLR sta tentando di eseguire un binding con un nome host specifico che non può essere risolto (ad es. &quot;user-macbook-pro&quot;).
In tal caso, aggiornate il file etc/hosts con una nuova voce per questo nome host (ad esempio 127.0.0.1 user-macbook-pro) e Solr verrà avviato correttamente.

### SolrCloud {#solrcloud}

Per eseguire una configurazione solrCloud di base (non di produzione), inizia da:

* java -Dbootstrap_confdir=./solr/collection1/conf -Dbootstrap_conf=true -DzkRun -jar start.jar

## Identificare MongoDB come archivio comune {#identify-mongodb-as-common-store}

Avviate le istanze di AEM, se necessario.

Se AEM era in esecuzione prima dell&#39;avvio di MongoDB, le istanze di AEM dovranno essere riavviate.

Seguite le istruzioni riportate nella pagina principale della documentazione: MSRP [- Store comune MongoDB](msrp.md)

## Prova {#test}

Per testare e verificare lo store comune MongoDB, pubblicate un commento sull’istanza di pubblicazione e visualizzatela nell’istanza di creazione, nonché visualizzate l’UGC in MongoDB e Solr:

1. Nell’istanza di pubblicazione, accedete alla pagina Guida ai componenti [community](http://localhost:4503/content/community-components/en/comments.html) e selezionate il componente Commenti.
1. Accedete per pubblicare un commento:
1. Immettete il testo nella casella di immissione del commento e fate clic su **[!UICONTROL Post]**

   ![chlimage_1-191](assets/chlimage_1-191.png)

1. È sufficiente visualizzare il commento sull’istanza [di](http://localhost:4502/content/community-components/en/comments.html) authoring (con probabilità ancora eseguito l’accesso come amministratore/amministratore).

   ![chlimage_1-192](assets/chlimage_1-192.png)

   Nota: mentre sull’autore sono presenti nodi JCR sotto il *percorso* asiatico, questi sono per il framework SCF. L&#39;UGC effettivo non è in JCR, è in MongoDB.

1. Visualizzare l&#39;UGC in **[!UICONTROL Community mongodb > Raccolte > Contenuto]**

   ![chlimage_1-193](assets/chlimage_1-193.png)

1. Visualizzare l’UGC in Solr:

   * Passa al dashboard Solr: [http://localhost:8983/solr/](http://localhost:8983/solr/)
   * Utente `core selector` da selezionare `collection1`
   * Seleziona `Query`
   * Seleziona `Execute Query`
   ![chlimage_1-194](assets/chlimage_1-194.png)

## Risoluzione dei problemi {#troubleshooting}

### Nessun UGC {#no-ugc-appears}

1. Verificare che MongoDB sia installato ed eseguito correttamente.

1. Verificate che MSRP sia stato configurato come provider predefinito:

   * Per creare e pubblicare tutte le istanze di AEM, rivisitate la console Configurazione [archiviazione](srp-config.md)
   oppure controllate l&#39;archivio AEM:

   * In JCR, se [/etc/socialconfig](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/)

      * Non contiene un nodo [srpc](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc) , significa che il provider di archiviazione è JSRP
      * Se il nodo srpc esiste e contiene il nodo [defaultconfiguration](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc/defaultconfiguration), le proprietà della configurazione predefinita devono definire MSRP come provider predefinito


1. Accertatevi che AEM sia stato riavviato dopo la selezione di MSRP.
