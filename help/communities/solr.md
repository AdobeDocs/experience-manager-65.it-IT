---
title: Configurazione Solr per SRP
description: Un’installazione Apache Solr può essere condivisa tra l’archivio nodi (Oak) e l’archivio comune (SRP) utilizzando raccolte diverse
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: a9fc9c06-b9e6-4a5e-ab5e-0930ecd4b51b
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1423'
ht-degree: 2%

---

# Configurazione Solr per SRP {#solr-configuration-for-srp}

## Solr per la piattaforma AEM {#solr-for-aem-platform}

Un [Apache Solr](https://solr.apache.org/) può essere condivisa tra [archivio nodi](../../help/sites-deploying/data-store-config.md) (Oak) [archivio comune](working-with-srp.md) (SRP) utilizzando raccolte diverse.

Se entrambe le raccolte Oak e SRP vengono utilizzate in modo intensivo, è possibile installare un secondo Solr per motivi di prestazioni.

Per gli ambienti di produzione, [Modalità SolrCloud](#solrcloud-mode) offre prestazioni migliori rispetto alla modalità standalone (un&#39;unica configurazione Solr locale).

### Requisiti {#requirements}

Scarica e installa Apache Solr:

* [Versione 7.0](https://archive.apache.org/dist/lucene/solr/7.0.0/)

* Solr richiede Java™ 1.7 o versione successiva
* Non è necessario alcun servizio
* Scelta delle modalità di esecuzione:

   * Modalità autonoma
   * [Modalità SolrCloud](#solrcloud-mode) (consigliato per ambienti di produzione)

* Scelta di ricerca multilingue (MLS)

   * [Installazione di MLS standard](#installing-standard-mls)
   * [Installazione di Advanced MLS](#installing-advanced-mls)

## Modalità SolrCloud {#solrcloud-mode}

[SolrCloud](https://solr.apache.org/guide/6_6/solrcloud.html) è consigliata per gli ambienti di produzione. Quando viene eseguito in modalità SolrCloud, SolrCloud deve essere installato e configurato prima di installare la ricerca multilingue (MLS).

Si consiglia di seguire le istruzioni di SolrCloud per installare:

* 3 nodi SolrCloud sullo stesso server.
* Un Apache ZooKeeper esterno.

Si consiglia inoltre di configurare JVM per regolare l’utilizzo della memoria e la raccolta di oggetti inattivi.

### Esempio di configurazione JVM {#jvm-configuration-example}

```shell
JVM_OPTS="-server -Xmx2048m -XX:+UseConcMarkSweepGC -XX:+CMSClassUnloadingEnabled -Xloggc:../logs/gc.log -XX:+PrintGCDetails -XX:+PrintGCDateStamps -Djava.awt.headless=true"
```

### Comandi di configurazione SolrCloud {#solrcloud-setup-commands}

Quando l’esecuzione avviene in modalità SolrCloud, prima dell’installazione di MLS è necessario utilizzare e conoscere i seguenti comandi di configurazione di SolrCloud.

#### 1. Carica una configurazione in ZooKeeper {#upload-a-configuration-to-zookeeper}

Riferimento:
[https://solr.apache.org/guide/6_6/command-line-utilities.html](https://solr.apache.org/guide/6_6/command-line-utilities.html)

Utilizzo: sh ./scripts/cloud-scripts/zkcli.sh \
-cmd upconfig \
-zkhost *server:porta* \
-conname *nome-configurazione*\
-solrhome *solr-home-path* \
-condir *config-dir*

#### 2. Creare una raccolta {#create-a-collection}

Riferimento:
[https://solr.apache.org/guide/6_6/solr-control-script-reference.html#SolrControlScriptReference-Create](https://solr.apache.org/guide/6_6/solr-control-script-reference.html#SolrControlScriptReference-Create)

Utilizzo: ./bin/solr crea \
-c *mycollection-name*\
d *config-dir* \
-n *myconfig-name* \
-p *porta*\
-s *numero di frammenti* \
-rf *numero di repliche*

#### 3. Collegare una raccolta a un set di configurazione {#link-a-collection-to-a-configuration-set}

Collega una raccolta a una configurazione già caricata in ZooKeeper.

Riferimento:
[https://solr.apache.org/guide/6_6/command-line-utilities.html](https://solr.apache.org/guide/6_6/command-line-utilities.html)

Utilizzo: sh ./scripts/cloud-scripts/zkcli.sh \
-cmd linkconfig \
-zkhost *server:porta* \
-collection *mycollection-name* \
-confname *myconfig-name*

### Confronto tra standard e avanzato MLS {#comparison-of-standard-and-advanced-mls}

La funzione di ricerca multilingue (MLS) per AEM Communities è stata creata per la piattaforma Solr al fine di migliorare le funzioni di ricerca in tutte le lingue supportate, incluso l’inglese.

MLS per AEM Communities è disponibile come MLS standard o come MLS avanzato. MLS standard include solo le impostazioni di configurazione Solr ed esclude eventuali plug-in o file di risorse. Advanced MLS è la soluzione più completa e include le impostazioni di configurazione Solr, i plug-in e le risorse correlate

MLS standard include miglioramenti per la ricerca di contenuti per le seguenti lingue:

* Inglese: è stato migliorato lo stemmer per il tentativo di corrispondenza con le derivazioni di parole.
* Giapponese: è stata migliorata la tokenizzazione giapponese per i caratteri ridotti.

Advanced MLS include miglioramenti per la ricerca di contenuti per le seguenti lingue:

* Inglese: Sostituito stemmer con lemmatizzatore.
* Tedesco: aggiunto decompositore.
* Francese: aggiunta della gestione delle eliezioni.
* Cinese (semplificato): aggiunto un token più intelligente.
* Varie lingue: aggiunta di uno stemmer, di un elenco di parole non significative e di un normalizzatore.

In tutto, le seguenti 33 lingue sono supportate in Advanced MLS.

| Arabo | Tedesco | Norvegese |
|---|---|---|
| Bulgaro | Greco | Polacco |
| Cinese (semplificato) | Creolo haitiano | Portoghese |
| Cinese (tradizionale) | Ebraico | Rumeno |
| Ceco | Ungherese | Russo |
| Danese | Indonesiano | Slovacco |
| Olandese | Italiano | Sloveno |
| Inglese | Giapponese | Spagnolo |
| Estone | Coreano | Svedese |
| Finlandese | Lettone | Thailandese |
| Francese | Lituano | Turco |

#### Confronto tra ricerca Solr AEM 6.1, MLS standard e MLS avanzata {#comparison-of-aem-solr-search-standard-mls-and-advanced-mls}

**Nota**: AEM 6.1 si riferisce al 3° PQ della Comunità dell’AEM 6.1 e versioni precedenti.

![compare-solr-mls](assets/compare-solr-mls.png)

### Installazione di MLS standard {#installing-standard-mls}

Per la raccolta SRP (MSRP o DSRP), per supportare la ricerca multilingue standard (MLS) è necessario modificare due dei file di configurazione di Solr:

* **schema.xml**
* **solrconfig.xml**

File MLS standard (schema.xml, solrconfig.xml) per Solr 4.10.

File MLS standard (schema.xml, solrconfig.xml) per Solr 5.x.

I file MLS standard sono memorizzati nel repository AEM.

**Nota**: i file Solr vengono memorizzati nella cartella msrp/, ma sono anche per DSRP (non sono necessarie modifiche).

**Istruzioni per il download**: Sostituisci `solrX` con `solr4` o `solr5` se del caso.

1. Utilizzando CRXDE|Lite, individua:

   * `/libs/social/config/datastore/msrp/solrX/schema.xml`
   * `/libs/social/config/datastore/msrp/solrX/solrconfig.xml`

1. Scarica sul server locale in cui è implementato Solr.

   * Individua il `jcr:content` del nodo `jcr:data` proprietà.
   * Per avviare il download, seleziona `view`.
   * Assicurati di salvare i file con i nomi e la codifica appropriati (UTF8).

1. Seguire le istruzioni di installazione per la modalità standalone o SolrCloud.

#### Modalità SolrCloud - MLS standard {#solrcloud-mode-standard-mls}

1. Installare e configurare Solr in modalità SolrCloud.
1. Prepara una nuova configurazione:

   1. Creare new-config-dir*, ad esempio `solr-install-dir*/myconfig/`

   1. Copia il contenuto della directory di configurazione Solr esistente in *new-config-dir*

      * Per Solr4: copia `solr-install-dir/example/solr/collection1/conf/`
      * Per Solr5: copia `solr-install-dir/server/solr/configsets/data_driven_schema_configs/`

   1. Copia il scaricato **schema.xml** e **solrconfig.xml** a *new-config-dir* per sovrascrivere i file esistenti.

1. [Carica la nuova configurazione](#upload-a-configuration-to-zookeeper) a ZooKeeper.
1. [Creare una raccolta](#create-a-collection) specifica dei parametri necessari, ad esempio il numero di condivisioni, il numero di repliche e il nome della configurazione.
1. Se il nome della configurazione *non è stato *fornito durante la creazione della raccolta, [collega questa raccolta appena creata](#link-a-collection-to-a-configuration-set) con la configurazione caricata in ZooKeeper.

1. Per MSRP, eseguire [Strumento Reindicizzazione MSRP](msrp.md#msrp-reindex-tool), a meno che questa installazione non sia nuova.

#### Modalità standalone - MLS standard {#standalone-mode-standard-mls}

1. Installare Solr in modalità standalone.
1. Se si esegue Solr5, creare una raccolta1 (simile a Solr4):

   * `./bin/solr start`
   * `./bin/solr create_core -c collection1 -d sample_techproducts_configs`

1. Backup **schema.xml** e **solrconfig.xml** nella directory di configurazione Solr, ad esempio:

   * Per Solr4: `solr-install-dir/example/solr/collection1/conf/`
   * Creato per Solr5: `solr-install-dir/server/solr/collection1/conf/`

1. Copia il scaricato **schema.xml** e **solrconfig.xml** nella stessa directory.

1. Riavviare Solr.
1. Per MSRP, eseguire [Strumento Reindicizzazione MSRP](#msrpreindextool), a meno che questa installazione non sia nuova.

### Installazione di Advanced MLS {#installing-advanced-mls}

Affinché la raccolta SRP (MSRP o DSRP) supporti MLS avanzati, sono necessari nuovi plug-in Solr oltre a uno schema personalizzato e alla configurazione Solr. Tutti gli elementi richiesti vengono inseriti in un file zip scaricabile. Inoltre, è incluso uno script di installazione da utilizzare quando Solr è distribuito in modalità standalone.

Per ottenere il pacchetto MLS avanzato, vedi [AEM Advanced MLS](deploy-communities.md#aem-advanced-mls) nella sezione distribuzione della documentazione.

Per iniziare a installare in modalità SolrCloud o standalone:

* Scarica l&#39;archivio zip AEM-SOLR-MLS sul server che ospita Solr.
* Decomprimi l’archivio.

#### Modalità SolrCloud - MLS avanzato {#solrcloud-mode-advanced-mls}

Istruzioni di installazione - notare le poche differenze per Solr4 e Solr5:

1. Installare e configurare Solr in modalità SolrCloud.
1. Estrarre il contenuto del pacchetto MLS avanzato su disco. Il contenuto deve includere:

   * **schema.xml**
   * **solrconfig.xml**
   * **stopwords/** cartella
   * **profili/** cartella
   * **extra-libs/** cartella

1. Prepara una nuova configurazione:

   1. Creare un *new-config-dir*

      * Ad esempio `solr-install-dir/myconfig/`
      * Creare sottocartelle `stopwords/` e `lang/`

   1. Copia il contenuto della directory di configurazione Solr esistente in *new-config-dir*

      * Per Solr4: Copia `solr-install-dir/example/solr/collection1/conf/`
      * Per Solr5: Copia `solr-install-dir/server/solr/configsets/data_driven_schema_configs/`

   1. Copia il file estratto **schema.xml** e **solrconfig.xml** a *new-config-dir* per sovrascrivere i file esistenti.
   1. Per Solr5: Copia `solr_install_dir/server/solr/configsets/sample_techproducts_configs/conf/lang/*.txt` a `new-config-dir/lang/`
   1. Copia il file estratto **stopwords/** cartella a *new-config-dir* che si traduce `new-config-dir/stopwords/*.txt`

1. [Carica la nuova configurazione](#upload-a-configuration-to-zookeeper) a ZooKeeper
1. Copia il nuovo **profili/** cartella...

   * Per Solr4: copia nella cartella/risorse di ciascun nodo
   * Per Solr5: copia nella cartella server/resources/ di ogni installazione Solr. Se tutti i nodi si trovano nella stessa directory di installazione Solr, questo passaggio viene eseguito una sola volta.

1. Creare un **lib/** cartella nella directory solr-home (contiene solr.xml) di ciascun nodo in SolrCloud. Copia i file jar dalle seguenti posizioni nella nuova libreria o cartella su ciascun nodo:

   * **extra-libs/** estratto dal pacchetto MLS avanzato
   * *solr-install-dir/contrib/extraction/lib/*.jar
   * *solr-install-dir/dist/solr-cell*.jar
   * *solr-install-dir/contrib/clustering/lib/*.jar
   * *solr-install-dir/dist/solr-clustering*.jar
   * *solr-install-dir/contrib/langid/lib/*.jar
   * *solr-install-dir/dist/solr-langid*.jar
   * *solr-install-dir/contrib/velocity/lib/*.jar
   * *solr-install-dir/dist/solr-velocity*.jar
   * *solr-install-dir/contrib/analysis-extras/lib/*.jar
   * *solr-install-dir/contrib/analysis-extras/lucene-libs/*.jar

1. [Creare una raccolta](#create-a-collection) specifica dei parametri necessari, ad esempio il numero di condivisioni, il numero di repliche e il nome della configurazione.
1. Se il nome della configurazione era *non* fornite durante la creazione della collezione, [collega questa raccolta appena creata](#link-a-collection-to-a-configuration-set) con la configurazione caricata in ZooKeeper.

1. Per MSRP, eseguire [Strumento Reindicizzazione MSRP](#msrpreindextool), a meno che questa installazione non sia nuova.

#### Modalità standalone - Advanced MLS {#standalone-mode-advanced-mls}

Uno script di installazione è incluso nel pacchetto MLS avanzato.

Dopo aver estratto il contenuto del pacchetto nel server che ospita il server Solr standalone, eseguire lo script di installazione per installare le risorse e i file di configurazione necessari.

* Installare Solr in modalità standalone.
* Se si esegue Solr5, creare una raccolta1 (simile a Solr4):

   * `./bin/solr start`
   * `./bin/solr create_core -c collection1 -d sample_techproducts_configs`

* Esegui lo script di installazione: Installa [-v 4|5] [-d solrhome] [-c percorso raccolta]
dove:

   * -d solrhome

     Directory di installazione Solr

   * -c percorso raccolta

     Percorso raccolta in solr

   * —aiuto

     Opzioni della riga di comando Stampa

   * -v [4|5]

     Imposta versione per solr

* Esempio per Solr 4.10.4:

   * Install.bat -v 4 -d c:/solr-4.10.4 -c c:/solr-4.10.4/example/solr/collection1

* Esempio per Solr 5.4.0:

   * Install.sh -v 5 -d /tmp/solr-5.4.0 -c /tmp/solr-5.4.0/server/solr/collection1

**Nota**:

* Lo script di installazione esegue il backup di schema.xml e solrconfig.xml prima di installare nuove versioni aggiungendo &quot;.orig&quot;

### Informazioni su solrconfig.xml {#about-solrconfig-xml}

Il **solrconfig.xml** file controlla l&#39;intervallo di commit automatico e la visibilità della ricerca e richiede test e tuning.

`<autoCommit>`: per impostazione predefinita, l&#39;intervallo di AutoCommit, ovvero un impegno rigido per l&#39;archiviazione stabile, è impostato su 15 secondi. Per impostazione predefinita, la visibilità della ricerca utilizza l’indice di pre-commit.

Per modificare la ricerca in modo da utilizzare un indice aggiornato per riflettere le modifiche dovute al commit, modifica il contenuto `openSearcher` su true.

`autoSoftCommit`: un commit &quot;soft&quot; assicura che le modifiche siano visibili (l’indice viene aggiornato), ma non assicura che le modifiche siano sincronizzate con l’archiviazione stabile (commit rigido). Il risultato è un miglioramento delle prestazioni. Per impostazione predefinita, `autoSoftCommit` è disabilitato con il contenuto `maxTime` impostare su -1.
