---
title: Passaggi di aggiornamento per le installazioni di Application Server
seo-title: Passaggi di aggiornamento per le installazioni di Application Server
description: Scoprite come aggiornare le istanze di AEM distribuite tramite Application Server.
seo-description: Scoprite come aggiornare le istanze di AEM distribuite tramite Application Server.
uuid: e4020966-737c-40ea-bfaa-c63ab9a29cee
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: 1876d8d6-bffa-4a1c-99c0-f6001acea825
docset: aem65
translation-type: tm+mt
source-git-commit: 38ef8fc8d80009c8ca79aca9e45cf10bd70e1f1e
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 0%

---


# Passaggi di aggiornamento per le installazioni di Application Server{#upgrade-steps-for-application-server-installations}

In questa sezione viene descritta la procedura da seguire per aggiornare AEM per le installazioni di Application Server.

Tutti gli esempi contenuti in questa procedura utilizzano JBoss come Application Server e implicano che una versione funzionante di AEM è già distribuita. La procedura è destinata a documentare gli aggiornamenti eseguiti da **AEM versione 5.6 a 6.3**.

1. Innanzitutto, avviate JBoss. Nella maggior parte dei casi, è possibile eseguire lo script di avvio `standalone.sh`, eseguendo questo comando dal terminale:

   ```shell
   jboss-install-folder/bin/standalone.sh
   ```

1. Se AEM 5.6 è già distribuito, verificare che i bundle funzionino correttamente eseguendo:

   ```shell
   wget https://<serveraddress:port>/cq/system/console/bundles
   ```

1. Quindi, annullate la distribuzione AEM 5.6:

   ```shell
   rm jboss-install-folder/standalone/deployments/cq.war
   ```

1. Ferma JBoss.

1. Esegui la migrazione del repository utilizzando lo strumento di migrazione crx2oak:

   ```shell
   java -jar crx2oak.jar crx-quickstart/repository/ crx-quickstart/oak-repository
   ```

   >[!NOTE]
   >
   >In questo esempio, oak-repository è la directory temporanea in cui risiederà il repository convertito. Prima di eseguire questo passaggio, accertatevi di disporre della versione crx2oak.jar più recente.

1. Eliminate le proprietà necessarie nel file sling.properties effettuando le seguenti operazioni:

   1. Aprire il file che si trova in `crx-quickstart/launchpad/sling.properties`
   1. Testo del passaggio Rimuovete le seguenti proprietà e salvate il file:

      1. `sling.installer.dir`

      1. `felix.cm.dir`

      1. `granite.product.version`

      1. `org.osgi.framework.system.packages`

      1. `osgi-core-packages`

      1. `osgi-compendium-services`

      1. `jre-*`

      1. `sling.run.mode.install.options`

1. Rimuovete i file e le cartelle che non sono più necessari. Gli elementi da rimuovere sono:

   * La **cartella di avvio/avvio**. È possibile eliminarlo eseguendo il seguente comando nel terminale: `rm -rf crx-quickstart/launchpad/startup`

   * Il file **base.jar**: `find crx-quickstart/launchpad -type f -name "org.apache.sling.launchpad.base.jar*" -exec rm -f {} \`

   * Il file **BootstrapCommandFile_timestamp.txt**: `rm -f crx-quickstart/launchpad/felix/bundle0/BootstrapCommandFile_timestamp.txt`

1. Copia l’archivio segmenti appena migrato nella posizione corretta:

   ```shell
   mv crx-quickstart/oak-repository/segmentstore crx-quickstart/repository/segmentstore
   ```

1. Copiate anche il datastore:

   ```shell
   mv crx-quickstart/repository/repository/datastore crx-quickstart/repository/datastore
   ```

1. Quindi, dovete creare la cartella che conterrà le configurazioni OSGi che verranno utilizzate con la nuova istanza aggiornata. Più precisamente, è necessario creare una cartella denominata install in **crx-quickstart**.

1. A questo punto, creare l&#39;archivio nodi e l&#39;archivio dati che verrà utilizzato con AEM 6.3. A tal fine, potete creare due file con i seguenti nomi in **crx-quickstart\install**:

   * `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.cfg`

   * `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.cfg`

   Questi due file configureranno AEM per utilizzare uno store di nodi TarMK e uno store di dati File.

1. Modificate i file di configurazione per renderli pronti per l’uso. Più precisamente:

   * Aggiungi la seguente riga a **org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config**:\
      `customBlobStore=true`

   * Quindi aggiungete le seguenti righe a **org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config**:

      ```
      path=./crx-quickstart/repository/datastore
       minRecordLength=4096
      ```

1. Rimuovere la modalità di esecuzione crx2 eseguendo:

   ```shell
   find crx-quickstart/launchpad -type f -name "sling.options.file" -exec rm -rf {} \
   ```

1. È ora necessario modificare le modalità di esecuzione nel file di guerra AEM 6.3. Per fare ciò, create innanzitutto una cartella temporanea che ospiterà la guerra AEM 6.3. Il nome della cartella in questo esempio sarà **temp**. Una volta copiato il file di guerra, estrarne il contenuto dall&#39;interno della cartella temp:

   ```shell
   jar xvf aem-quickstart-6.3.0.war
   ```

1. Una volta estratto il contenuto, passare alla cartella **WEB-INF** e modificare il file `web.xml` per modificare le modalità di esecuzione. Per trovare la posizione in cui sono impostati nell&#39;XML, cercare la stringa `sling.run.modes`. Una volta trovata, modificate le modalità di esecuzione nella riga di codice successiva, che per impostazione predefinita è impostata per l’authoring:

   ```shell
   <param-value >author</param-value>
   ```

1. Modificate il valore di authoring riportato sopra e impostate le modalità di esecuzione su: author,crx3,crx3tar Il blocco di codice finale deve essere simile al seguente:

   ```
   <init-param>
   <param-name>sling.run.modes</param-name>
   <param-value>author,crx3,crx3tar</param-value>
   </init-param>
   <load-on-startup>100</load-on-startup>
   </servlet>
   ```

1. Ricreare la vaschetta con il contenuto modificato:

   ```shell
   jar cvf aem62.war
   ```

1. Infine, distribuire il nuovo file di guerra:

   ```shell
   cp temp/aem62.war jboss-install-folder/standalone/deployments/aem61.war
   ```

