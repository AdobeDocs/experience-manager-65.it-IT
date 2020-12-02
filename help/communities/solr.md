---
title: Configurazione Solr per SRP
seo-title: Configurazione Solr per SRP
description: Un'installazione Apache Solr può essere condivisa tra l'archivio nodi (Oak) e lo store comune (SRP) utilizzando raccolte diverse
seo-description: Un'installazione Apache Solr può essere condivisa tra l'archivio nodi (Oak) e lo store comune (SRP) utilizzando raccolte diverse
uuid: 7356343d-073c-4266-bdcb-c7e999281476
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: e228f1db-91ea-4ec3-86da-06d89d74bc72
translation-type: tm+mt
source-git-commit: 94bc3550a7e18b9203e7a0d495d195d7b798e012
workflow-type: tm+mt
source-wordcount: '1483'
ht-degree: 2%

---


# Configurazione Solr per SRP {#solr-configuration-for-srp}

## Solr for AEM Platform {#solr-for-aem-platform}

Un&#39;installazione [Apache Solr](https://lucene.apache.org/solr/) può essere condivisa tra [archivio nodi](../../help/sites-deploying/data-store-config.md) (Oak) e [store comune](working-with-srp.md) (SRP) utilizzando raccolte diverse.

Se le raccolte Oak e SRP vengono utilizzate intensamente, per motivi di prestazioni potrebbe essere installato un secondo Solr.

Per gli ambienti di produzione, la [modalità SolrCloud](#solrcloud-mode) offre prestazioni migliori rispetto alla modalità standalone (una singola configurazione Solr locale).

### Requisiti {#requirements}

Scarica e installa Apache Solr:

* [Versione 7.0](https://archive.apache.org/dist/lucene/solr/7.0.0/)

* Solr richiede Java 1.7 o versione successiva
* Nessun servizio necessario
* Scelta delle modalità di esecuzione:

   * Modalità indipendente
   * [Modalità](#solrcloud-mode)  SolrCloud (consigliato per ambienti di produzione)

* Scelta della ricerca multilingue (MLS)

   * [Installazione di MLS standard](#installing-standard-mls)
   * [Installazione di MLS avanzate](#installing-advanced-mls)

## Modalità SolrCloud {#solrcloud-mode}

[La modalità ](https://cwiki.apache.org/confluence/display/solr/SolrCloud) SolrCloudmode è consigliata per gli ambienti di produzione. In modalità SolrCloud, SolrCloud deve essere installato e configurato prima di installare MLS (Multilingual Search).

La raccomandazione è di seguire le istruzioni di SolrCloud da installare:

* 3 nodi SolrCloud sullo stesso server.
* Uno ZooKeeper Apache esterno.

Si consiglia inoltre di configurare JVM per ottimizzare l&#39;utilizzo della memoria e la raccolta dei rifiuti.

### Esempio di configurazione JVM {#jvm-configuration-example}

```shell
JVM_OPTS="-server -Xmx2048m -XX:MaxPermSize=768M -XX:+UseConcMarkSweepGC -XX:+CMSClassUnloadingEnabled -Xloggc:../logs/gc.log -XX:+PrintGCDetails -XX:+PrintGCDateStamps -Djava.awt.headless=true"
```

### Comandi di installazione di SolrCloud {#solrcloud-setup-commands}

In modalità SolrCloud, prima dell&#39;installazione di MLS è necessario utilizzare e conoscere i seguenti comandi di configurazione di SolrCloud.

#### 1. Carica una configurazione in ZooKeeper {#upload-a-configuration-to-zookeeper}

Riferimento:
[https://cwiki.apache.org/confluence/display/solr/Command+Line+Utilities](https://cwiki.apache.org/confluence/display/solr/Command+Line+Utilities)

Utilizzo:
sh./scripts/cloud-scripts/zkcli.sh \
-cmd upconfig \
-zkhost *server:porta* \
-confname *myconfig-name *\
-solrhome *solr-home-path* \
-confdir *config-dir*

#### 2. Creare una raccolta {#create-a-collection}

Riferimento:
[https://cwiki.apache.org/confluence/display/solr/Solr+Start+Script+Reference#SolrStartScriptReference-Create](https://cwiki.apache.org/confluence/display/solr/Solr+Start+Script+Reference#SolrStartScriptReference-Create)

Utilizzo:
./bin/solr create \
-c *mycollection-name*\
-d *config-dir* \
-n *myconfig-name* \
-p *porta*\
-s *numero di frammenti* \
-rf *numero di repliche*

#### 3. Collegare una raccolta a un set di configurazione {#link-a-collection-to-a-configuration-set}

Collegate una raccolta a una configurazione già caricata in ZooKeeper.

Riferimento:
[https://cwiki.apache.org/confluence/display/solr/Command+Line+Utilities](https://cwiki.apache.org/confluence/display/solr/Command+Line+Utilities)

Utilizzo:
sh./scripts/cloud-scripts/zkcli.sh \
-cmd linkconfig \
-zkhost *server:porta* \
-collection *mycollection-name* \
-confname *myconfig-name*

### Confronto tra MLS standard e avanzato {#comparison-of-standard-and-advanced-mls}

La ricerca multilingue (MLS) per  AEM Communities è stata creata per la piattaforma Solr per fornire una ricerca migliore in tutte le lingue supportate, incluso l&#39;inglese.

MLS per le comunità AEM è disponibile sia come standard MLS che come Advanced MLS. MLS standard include solo le impostazioni di configurazione Solr ed esclude eventuali plug-in o file di risorse. MLS avanzato è la soluzione più completa e include le impostazioni di configurazione Solr, i plug-in e le relative risorse

MLS standard include miglioramenti per la ricerca di contenuti per le seguenti lingue:

* Inglese: È stato migliorato lo stemmer per cercare di far corrispondere le derivazioni di parole.
* Giapponese: Miglioramento della personalizzazione giapponese per i caratteri a mezza larghezza.

MLS avanzate include miglioramenti per la ricerca di contenuti per le seguenti lingue:

* Inglese: Sgombro sostituito con limmatizzatore.
* Tedesco: Aggiunto decompositunder.
* Francese: È stata aggiunta la gestione delle immagini.
* Cinese (semplificato): È stato aggiunto un token più intelligente.
* Varie lingue: È stato aggiunto uno stemmer, un elenco di parole di arresto e un normalizzatore.

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
| Finlandese | Lettone | Thai |
| Francese | Lituano | Turco |

#### Confronto tra AEM 6.1 Solr search, Standard MLS e Advanced MLS {#comparison-of-aem-solr-search-standard-mls-and-advanced-mls}

**Nota**: AEM 6.1 si riferisce al AEM 6.1 FP3 delle Comunità europee e versioni precedenti.

![compare-solr-mls](assets/compare-solr-mls.png)

### Installazione di MLS standard {#installing-standard-mls}

Per la raccolta SRP (MSRP o DSRP), per supportare la ricerca multilingue standard (MLS) è necessario modificare due dei file di configurazione di Solr:

* **schema.xml**
* **solrconfig.xml**

File MLS standard (schema.xml, solrconfig.xml) per Solr 4.10.

File MLS standard (schema.xml, solrconfig.xml) per Solr 5.x.

I file MLS standard vengono memorizzati nell&#39;archivio AEM.

**Nota**: Mentre i file Solr sono memorizzati nella cartella msrp/, sono anche per DSRP (non sono necessarie modifiche).

**Istruzioni** di download: Sostituire  `solrX` con  `solr4` o  `solr5` secondo necessità.

1. Utilizzando CRXDE|Lite, individuare:

   * `/libs/social/config/datastore/msrp/solrX/schema.xml`
   * `/libs/social/config/datastore/msrp/solrX/solrconfig.xml`

1. Scaricate il file nel server locale in cui è distribuito Solr.

   * Individuare la proprietà `jcr:content` del nodo `jcr:data`.
   * Selezionare `view` per avviare il download.
   * Assicurarsi che i file siano salvati con i nomi e la codifica appropriati (UTF8).

1. Seguite le istruzioni di installazione per la modalità standalone o SolrCloud.

#### Modalità SolrCloud - MLS standard {#solrcloud-mode-standard-mls}

1. Installa e configura Solr in modalità SolrCloud.
1. Preparare una nuova configurazione:

   1. Create new-config-dir*, ad esempio `solr-install-dir*/myconfig/`

   1. Copiare il contenuto della directory di configurazione Solr esistente in *new-config-dir*

      * Per Solr4: copia `solr-install-dir/example/solr/collection1/conf/`
      * Per Solr5: copia `solr-install-dir/server/solr/configsets/data_driven_schema_configs/`
   1. Copiate i file **schema.xml** e **solrconfig.xml** scaricati in *new-config-dir* per sovrascrivere i file esistenti.


1. [Caricate la nuova ](#upload-a-configuration-to-zookeeper) configurazione in ZooKeeper.
1. [Create una ](#create-a-collection) raccolta specificando i parametri necessari, ad esempio il numero di frammenti, il numero di repliche e il nome della configurazione.
1. Se il nome di configurazione non è stato *fornito durante la creazione della raccolta, [collegare la raccolta appena creata ](#link-a-collection-to-a-configuration-set) con la configurazione caricata su ZooKeeper.

1. Per MSRP, eseguire [MSRP Reindex Tool](msrp.md#msrp-reindex-tool), a meno che non si tratti di una nuova installazione.

#### Modalità standalone - MLS standard {#standalone-mode-standard-mls}

1. Installare Solr in modalità standalone.
1. Se eseguite Solr5, create una raccolta1 (simile a Solr4):

   * `./bin/solr start`
   * `./bin/solr create_core -c collection1 -d sample_techproducts_configs`

1. Eseguire il backup di **schema.xml** e **solrconfig.xml** nella directory di configurazione Solr, ad esempio:

   * Per Solr4: `solr-install-dir/example/solr/collection1/conf/`
   * Creato per Solr5: `solr-install-dir/server/solr/collection1/conf/`

1. Copiate i file **schema.xml** e **solrconfig.xml** scaricati nella stessa directory.

1. Riavvia Solr.
1. Per MSRP, eseguire [MSRP Reindex Tool](#msrpreindextool), a meno che non si tratti di una nuova installazione.

### Installazione di MLS avanzate {#installing-advanced-mls}

Affinché l&#39;insieme SRP (MSRP o DSRP) supporti MLS avanzati, sono necessari nuovi plug-in Solr, oltre a uno schema personalizzato e a una configurazione Solr. Tutti gli elementi richiesti vengono assemblati in un file zip scaricabile. Inoltre, è incluso uno script di installazione da utilizzare quando Solr viene distribuito in modalità standalone.

Per ottenere il pacchetto MLS avanzato, vedere [AEM MLS avanzate](deploy-communities.md#aem-advanced-mls) nella sezione relativa alla distribuzione della documentazione.

Per iniziare a utilizzare l&#39;installazione per SolrCloud o la modalità standalone:

* Scarica AEM-SOLR-MLS archivio zip sul server in cui è installato Solr.
* Estrarre l&#39;archivio.

#### Modalità SolrCloud - MLS avanzate {#solrcloud-mode-advanced-mls}

Istruzioni di installazione - notare alcune differenze per Solr4 e Solr5:

1. Installa e configura Solr in modalità SolrCloud.
1. Estrarre su disco il contenuto del pacchetto MLS avanzato. Il contenuto deve includere:

   * **schema.xml**
   * **solrconfig.xml**
   * **stopwords/** folder
   * **profili/** cartella
   * **libs/** folder

1. Preparare una nuova configurazione:

   1. Creare una *nuova configurazione-dir*

      * Ad esempio `solr-install-dir/myconfig/`
      * Creare sottocartelle `stopwords/` e `lang/`
   1. Copiare il contenuto della directory di configurazione Solr esistente su *new-config-dir*

      * Per Solr4: Copia `solr-install-dir/example/solr/collection1/conf/`
      * Per Solr5: Copia `solr-install-dir/server/solr/configsets/data_driven_schema_configs/`
   1. Copiate le **schema.xml** e **solrconfig.xml** estratte in *new-config-dir* per sovrascrivere i file esistenti.
   1. Per Solr5: Copia `solr_install_dir/server/solr/configsets/sample_techproducts_configs/conf/lang/*.txt` in `new-config-dir/lang/`
   1. Copiare la cartella **stopwords/** estratta in *new-config-dir* con il risultato di `new-config-dir/stopwords/*.txt`



1. [Carica la nuova ](#upload-a-configuration-to-zookeeper) configurazione in ZooKeeper
1. Copiate la nuova cartella **profile/** ...

   * Per Solr4: Copia nella cartella risorse/risorse di ciascun nodo
   * Per Solr5: Copiare nella cartella server/risorse/ di ogni installazione Solr. Se tutti i nodi si trovano nella stessa directory di installazione Solr, questo passaggio viene eseguito solo una volta.

1. Create una cartella **lib/** nella directory solr-home (contiene solr.xml) di ciascun nodo in SolrCloud. Copiare le barre dalle seguenti posizioni nella nuova cartella lib/ su ciascun nodo:

   * **libs extra/** estratto dal pacchetto MLS avanzato
   * *solr-install-dir/citazione/estrazione/lib/*.jar
   * *solr-install-dir/dist/solr-cell*.jar
   * *solr-install-dir/Contributo/clustering/lib/*.jar
   * *solr-install-dir/dist/solr-clustering*.jar
   * *solr-install-dir/Contributo/langid/lib/*.jar
   * *solr-install-dir/dist/solr-langid*.jar
   * *solr-install-dir/citazione/velocità/lib/*.jar
   * *solr-install-dir/dist/solr-velocity*.jar
   * *solr-install-dir/citazione/analysis-extras/lib/*.jar
   * *solr-install-dir/contribuzione/analysis-extras/lucene-libs/*.jar

1. [Create una ](#create-a-collection) raccolta specificando i parametri necessari, ad esempio il numero di frammenti, il numero di repliche e il nome della configurazione.
1. Se il nome della configurazione era *not* fornito durante la creazione della raccolta, [collegare la raccolta appena creata](#link-a-collection-to-a-configuration-set) con la configurazione caricata in ZooKeeper.

1. Per MSRP, eseguire [MSRP Reindex Tool](#msrpreindextool), a meno che non si tratti di una nuova installazione.

#### Modalità indipendente - MLS avanzate {#standalone-mode-advanced-mls}

Uno script di installazione è incluso nel pacchetto MLS avanzato.

Dopo aver estratto il contenuto del pacchetto sul server che ospita il server Solr standalone, eseguite semplicemente lo script di installazione per installare le risorse e i file di configurazione necessari.

* Installare Solr in modalità standalone.
* Se eseguite Solr5, create una raccolta1 (simile a Solr4):

   * `./bin/solr start`
   * `./bin/solr create_core -c collection1 -d sample_techproducts_configs`

* Eseguire lo script di installazione: Installazione di [-v 4|5] [-d solrhome] [-c collectionpath]
dove:

   * -d solrhome

      Directory di installazione Solr

   * -c percorso di raccolta

      Percorso raccolta in solr

   * --aiuto

      Stampa, opzioni della riga di comando

   * -v [4|5]

      Imposta versione per solr

* Esempio per Solr 4.10.4:

   * Install.bat -v 4 -d c:/solr-4.10.4 -c c:/solr-4.10.4/example/solr/collection1

* Esempio per Solr 5.4.0:

   * Install.sh -v 5 -d /tmp/solr-5.4.0 -c /tmp/solr-5.4.0/server/solr/collection1

**Nota**:

* Lo script di installazione eseguirà il backup di schema.xml e solrconfig.xml prima di installare nuove versioni aggiungendo &quot;.orig&quot;

### Informazioni su solrconfig.xml {#about-solrconfig-xml}

Il file **solrconfig.xml** controlla l&#39;intervallo di commit automatico e la visibilità della ricerca e richiederà test e tuning.

`<autoCommit>`: Per impostazione predefinita, l’intervallo di AutoCommit, che è un commit rigido per lo storage stabile, è impostato su 15 secondi. Per impostazione predefinita, la visibilità della ricerca utilizza l’indice di pre-commit.

Per modificare la ricerca in modo da utilizzare un indice aggiornato per riflettere le modifiche dovute al commit, imposta su true il contenuto `openSearcher`.

`autoSoftCommit`: Un commit &#39;soft&#39; garantisce che le modifiche siano visibili (l&#39;indice viene aggiornato), ma non garantisce che le modifiche siano sincronizzate su un archivio stabile (commit rigido). Il risultato è un miglioramento delle prestazioni. Per impostazione predefinita, `autoSoftCommit` è disabilitato con il contenuto `maxTime` impostato su -1.
