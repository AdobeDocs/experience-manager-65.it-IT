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
source-git-commit: f696b1081f14ba379cde51a3542a5b1b5f9668e2
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 0%

---


# Passaggi di aggiornamento per le installazioni di Application Server{#upgrade-steps-for-application-server-installations}

In questa sezione viene descritta la procedura da seguire per aggiornare AEM per le installazioni di Application Server.

Tutti gli esempi in questa procedura utilizzano Tomcat come Application Server e indicano che è già stata implementata una versione funzionante di AEM. La procedura è destinata a documentare gli aggiornamenti eseguiti da **AEM versione 6.4 a 6.5**.

1. Per prima cosa, iniziate TomCat. Nella maggior parte dei casi, è possibile eseguire lo script di avvio `./catalina.sh`, eseguendo questo comando dal terminale:

   ```shell
   $CATALINA_HOME/bin/catalina.sh start
   ```

1. Se AEM 6.4 è già distribuito, verificate che i bundle funzionino correttamente accedendo a:

   ```shell
   https://<serveraddress:port>/cq/system/console/bundles
   ```

1. Quindi, annullate la distribuzione AEM 6.4. Questo può essere fatto da TomCat App Manager (`http://serveraddress:serverport/manager/html`)

1. Esegui la migrazione del repository utilizzando lo strumento di migrazione crx2oak. Per farlo, scarica l&#39;ultima versione di crx2oak da [questa posizione](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/crx2oak).

   ```shell
   SLING_HOME= $AEM-HOME/crx-quickstart java -Xmx4096m -XX:MaxPermSize=2048M -jar crx2oak.jar --load-profile segment-fds
   ```

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

   * Rimuovere **sling.options.file** eseguendo: `find crx-quickstart/launchpad -type f -name "sling.options.file" -exec rm -rf`

1. A questo punto, creare l&#39;archivio nodi e l&#39;archivio dati da utilizzare con AEM 6.5. A tal fine, potete creare due file con i seguenti nomi in `crx-quickstart\install`:

   * `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.cfg`
   * `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.cfg`

   Questi due file configureranno AEM per utilizzare uno store di nodi TarMK e uno store di dati File.

1. Modificate i file di configurazione per renderli pronti per l’uso. Più precisamente:

   * Aggiungete la seguente riga a `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`:

      ```customBlobStore=true```

   * Quindi aggiungete le seguenti righe a `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config`:

      ```
      path=./crx-quickstart/repository/datastore
      minRecordLength=4096
      ```

1. È ora necessario modificare le modalità di esecuzione nel file di guerra AEM 6.5. Per fare ciò, create innanzitutto una cartella temporanea che ospiterà la guerra AEM 6.5. Il nome della cartella in questo esempio sarà `temp`. Una volta copiato il file di guerra, estrarne il contenuto dall&#39;interno della cartella temp:

   ```
   jar xvf aem-quickstart-6.5.0.war
   ```

1. Una volta estratto il contenuto, andate alla cartella **WEB-INF** e modificate il file web.xml per modificare le modalità di esecuzione. Per trovare la posizione in cui sono impostati nell&#39;XML, cercare la stringa `sling.run.modes`. Una volta trovata, modificate le modalità di esecuzione nella riga di codice successiva, che per impostazione predefinita è impostata per l’authoring:

   ```bash
   <param-value >author</param-value>
   ```

1. Modificate il valore di authoring riportato sopra e impostate le modalità di esecuzione su: `author,crx3,crx3tar`. Il blocco di codice finale deve essere simile al seguente:

   ```
   <init-param>
   <param-name>sling.run.modes</param-name>
   <param-value>author,crx3,crx3tar</param-value>
   </init-param>
   <load-on-startup>100</load-on-startup>
   </servlet>
   ```

1. Ricreare la vaschetta con il contenuto modificato:

   ```bash
   jar cvf aem65.war
   ```

1. Infine, schierate il nuovo file di guerra in TomCat.
