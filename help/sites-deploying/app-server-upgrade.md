---
title: Passaggi per l’aggiornamento delle installazioni del server applicazioni
description: Scopri come aggiornare le istanze di AEM distribuite tramite Application Server.
feature: Upgrading
exl-id: 86dd10ae-7f16-40c8-84b6-91ff2973a523
solution: Experience Manager, Experience Manager Sites
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: 835ee49e-9248-5578-a60a-15c097807178
    internal-label: Upgrading
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 2%
---
# Passaggi per l’aggiornamento delle installazioni del server applicazioni{#upgrade-steps-for-application-server-installations}

Questa sezione descrive la procedura da seguire per aggiornare le installazioni di AEM for Application Server.

Tutti gli esempi in questa procedura utilizzano Tomcat come server applicazioni e indicano che è già stata distribuita una versione funzionante di AEM. La procedura consente di documentare gli aggiornamenti eseguiti da **AEM versione 6.4 a 6.5**.

1. Per prima cosa, avvia TomCat. Nella maggior parte dei casi, è possibile eseguire lo script di avvio di `./catalina.sh` eseguendo questo comando dal terminale:

   ```shell
   $CATALINA_HOME/bin/catalina.sh start
   ```

1. Se AEM 6.4 è già implementato, verifica che i bundle funzionino correttamente accedendo a:

   ```shell
   https://<serveraddress:port>/cq/system/console/bundles
   ```

1. Quindi, annulla la distribuzione di AEM 6.4. Questa operazione può essere eseguita da TomCat App Manager (`http://serveraddress:serverport/manager/html`)

1. Ora esegui la migrazione dell’archivio utilizzando lo strumento di migrazione crx2oak. Per farlo, scarica la versione più recente di crx2oak da [questa posizione](https://repo1.maven.org/maven2/com/adobe/granite/crx2oak/).

   ```shell
   SLING_HOME= $AEM-HOME/crx-quickstart java -Xmx4096m -jar crx2oak.jar --load-profile segment-fds
   ```

1. Elimina le proprietà necessarie nel file sling.properties effettuando le seguenti operazioni:

   1. Apri il file in `crx-quickstart/launchpad/sling.properties`
   1. Testo del passaggio Rimuovi le seguenti proprietà e salva il file:

      1. `sling.installer.dir`

      1. `felix.cm.dir`

      1. `granite.product.version`

      1. `org.osgi.framework.system.packages`

      1. `osgi-core-packages`

      1. `osgi-compendium-services`

      1. `jre-*`

      1. `sling.run.mode.install.options`

1. Rimuovere i file e le cartelle non più necessari. Gli elementi da rimuovere in modo specifico sono:

   * Cartella **launchpad/startup**. È possibile eliminarlo eseguendo il comando seguente nel terminale: `rm -rf crx-quickstart/launchpad/startup`

   * Il file **base.jar**: `find crx-quickstart/launchpad -type f -name "org.apache.sling.launchpad.base.jar*" -exec rm -f {} \`

   * Il file **BootstrapCommandFile_timestamp.txt**: `rm -f crx-quickstart/launchpad/felix/bundle0/BootstrapCommandFile_timestamp.txt`

   * Rimuovi **sling.options.file** eseguendo: `find crx-quickstart/launchpad -type f -name "sling.options.file" -exec rm -rf`

1. Ora crea l’archivio nodi e l’archivio dati utilizzati con AEM 6.5. A tale scopo, creare due file con i seguenti nomi in `crx-quickstart\install`:

   * `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.cfg`
   * `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.cfg`

   Questi due file configurano AEM per l’utilizzo di un archivio nodi TarMK e di un archivio dati File.

1. Modifica i file di configurazione per renderli pronti per l’uso. Più precisamente:

   * Aggiungi la riga seguente a `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`:

     `customBlobStore=true`

   * Quindi aggiungere le righe seguenti a `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config`:

     ```
     path=./crx-quickstart/repository/datastore
     minRecordLength=4096
     ```

1. Ora devi modificare le modalità di esecuzione nel file .war di AEM 6.5. Per farlo, crea innanzitutto una cartella temporanea che ospiterà la guerra AEM 6.5. Il nome della cartella in questo esempio sarà `temp`. Una volta copiato il file .war, estrarre il contenuto dall&#39;interno della cartella temporanea:

   ```
   jar xvf aem-quickstart-6.5.0.war
   ```

1. Una volta estratto il contenuto, passare alla cartella **WEB-INF** e modificare il file web.xml per modificare le modalità di esecuzione. Per trovare la posizione in cui sono impostati nel file XML, cercare la stringa `sling.run.modes`. Una volta individuato, modifica le modalità di esecuzione nella riga di codice successiva, che per impostazione predefinita è impostata su author:

   ```bash
   <param-value >author</param-value>
   ```

1. Modificare il valore di authoring riportato sopra e impostare le modalità di esecuzione su: `author,crx3,crx3tar`. Il blocco di codice finale deve essere simile al seguente:

   ```
   <init-param>
   <param-name>sling.run.modes</param-name>
   <param-value>author,crx3,crx3tar</param-value>
   </init-param>
   <load-on-startup>100</load-on-startup>
   </servlet>
   ```

1. Ricrea il file jar con il contenuto modificato:

   ```bash
   jar cvf aem65.war
   ```

1. Infine, distribuire il nuovo file di guerra in TomCat.
