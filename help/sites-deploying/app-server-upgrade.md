---
title: Passaggi di aggiornamento per le installazioni di Application Server
seo-title: Passaggi di aggiornamento per le installazioni di Application Server
description: Scopri come aggiornare le istanze di AEM distribuite tramite Application Server.
seo-description: Scopri come aggiornare le istanze di AEM distribuite tramite Application Server.
uuid: e4020966-737c-40ea-bfaa-c63ab9a29cee
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: 1876d8d6-bffa-4a1c-99c0-f6001acea825
docset: aem65
feature: Aggiornamento
exl-id: 86dd10ae-7f16-40c8-84b6-91ff2973a523
translation-type: tm+mt
source-git-commit: d99f4ce072688f8e7d453199742618f0b2357d07
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 0%

---

# Passaggi di aggiornamento per le installazioni di Application Server{#upgrade-steps-for-application-server-installations}

Questa sezione descrive la procedura da seguire per aggiornare AEM per le installazioni di Application Server.

Tutti gli esempi in questa procedura utilizzano Tomcat come Application Server e implicano che sia già stata implementata una versione funzionante di AEM. La procedura è destinata a documentare gli aggiornamenti eseguiti da **AEM versione 6.4 a 6.5**.

1. Per prima cosa, avviate TomCat. Nella maggior parte delle situazioni, è possibile eseguire lo script di avvio `./catalina.sh` eseguendo questo comando dal terminale:

   ```shell
   $CATALINA_HOME/bin/catalina.sh start
   ```

1. Se AEM 6.4 è già distribuito, controlla che i bundle funzionino correttamente accedendo a:

   ```shell
   https://<serveraddress:port>/cq/system/console/bundles
   ```

1. Quindi, disdistribuire AEM 6.4. Questo può essere fatto da TomCat App Manager (`http://serveraddress:serverport/manager/html`)

1. Ora, effettua la migrazione dell&#39;archivio utilizzando lo strumento di migrazione crx2oak. Per farlo, scarica l&#39;ultima versione di crx2oak da [questa posizione](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/crx2oak).

   ```shell
   SLING_HOME= $AEM-HOME/crx-quickstart java -Xmx4096m -XX:MaxPermSize=2048M -jar crx2oak.jar --load-profile segment-fds
   ```

1. Elimina le proprietà necessarie nel file sling.properties facendo quanto segue:

   1. Apri il file che si trova in `crx-quickstart/launchpad/sling.properties`
   1. Testo del passaggio Rimuovi le seguenti proprietà e salva il file:

      1. `sling.installer.dir`

      1. `felix.cm.dir`

      1. `granite.product.version`

      1. `org.osgi.framework.system.packages`

      1. `osgi-core-packages`

      1. `osgi-compendium-services`

      1. `jre-*`

      1. `sling.run.mode.install.options`

1. Rimuovi i file e le cartelle non più necessari. Gli elementi da rimuovere sono:

   * La **cartella launchpad/startup**. È possibile eliminarlo eseguendo il seguente comando nel terminale: `rm -rf crx-quickstart/launchpad/startup`

   * Il file **base.jar**: `find crx-quickstart/launchpad -type f -name "org.apache.sling.launchpad.base.jar*" -exec rm -f {} \`

   * Il file **BootstrapCommandFile_timestamp.txt**: `rm -f crx-quickstart/launchpad/felix/bundle0/BootstrapCommandFile_timestamp.txt`

   * Rimuovi **sling.options.file** eseguendo: `find crx-quickstart/launchpad -type f -name "sling.options.file" -exec rm -rf`

1. A questo punto, crea l&#39;archivio nodi e l&#39;archivio dati che verranno utilizzati con AEM 6.5. Puoi farlo creando due file con i seguenti nomi in `crx-quickstart\install`:

   * `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.cfg`
   * `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.cfg`

   Questi due file configureranno AEM per utilizzare un archivio nodi TarMK e un archivio dati File.

1. Modifica i file di configurazione per renderli pronti all’uso. Più precisamente:

   * Aggiungi la riga seguente a `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`:

      ```customBlobStore=true```

   * Quindi aggiungi le seguenti righe a `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config`:

      ```
      path=./crx-quickstart/repository/datastore
      minRecordLength=4096
      ```

1. È ora necessario modificare le modalità di esecuzione nel file di guerra AEM 6.5. Per farlo, crea innanzitutto una cartella temporanea che ospiterà la guerra AEM 6.5. Il nome della cartella in questo esempio sarà `temp`. Una volta copiato il file WAR, estrarne il contenuto eseguendo la cartella temporanea:

   ```
   jar xvf aem-quickstart-6.5.0.war
   ```

1. Una volta estratto il contenuto, vai alla cartella **WEB-INF** e modifica il file web.xml per modificare le modalità di esecuzione. Per trovare la posizione in cui sono impostati nell&#39;XML, cercare la stringa `sling.run.modes`. Una volta trovato, modifica le modalità di esecuzione nella riga di codice successiva, che per impostazione predefinita è impostata per l’authoring:

   ```bash
   <param-value >author</param-value>
   ```

1. Modifica il valore dell&#39;autore riportato sopra e imposta le modalità di esecuzione su: `author,crx3,crx3tar`. Il blocco di codice finale deve essere simile al seguente:

   ```
   <init-param>
   <param-name>sling.run.modes</param-name>
   <param-value>author,crx3,crx3tar</param-value>
   </init-param>
   <load-on-startup>100</load-on-startup>
   </servlet>
   ```

1. Ricrea il jar con il contenuto modificato:

   ```bash
   jar cvf aem65.war
   ```

1. Infine, distribuisci il nuovo file di guerra in TomCat.
