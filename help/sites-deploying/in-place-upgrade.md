---
title: Esecuzione di un aggiornamento diretto
description: Scopri come eseguire un aggiornamento sul posto per AEM 6.5.
topic-tags: upgrading
feature: Upgrading
exl-id: aef6ef00-993c-4252-b0ad-ddc4917beaf7
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
source-wordcount: '1265'
ht-degree: 1%
---
# Esecuzione di un aggiornamento diretto{#performing-an-in-place-upgrade}

>[!NOTE]
>
>Questa pagina illustra la procedura di aggiornamento per AEM 6.5. Se si dispone di un&#39;installazione distribuita in un server applicazioni, vedere [Passaggi per l&#39;aggiornamento delle installazioni del server applicazioni](/help/sites-deploying/app-server-upgrade.md).

## Passaggi di pre-aggiornamento {#pre-upgrade-steps}

Prima di eseguire l’aggiornamento, è necessario completare diversi passaggi. Consulta [Aggiornamento del codice e delle personalizzazioni](/help/sites-deploying/upgrading-code-and-customizations.md) e [Attività di manutenzione pre-aggiornamento](/help/sites-deploying/pre-upgrade-maintenance-tasks.md) per ulteriori informazioni. Inoltre, assicurati che il sistema soddisfi i requisiti per la nuova versione di AEM. Scopri in che modo il rilevatore pattern può aiutarti a stimare la complessità dell&#39;aggiornamento e consulta anche la sezione Ambito e requisiti dell&#39;aggiornamento di [Pianificazione dell&#39;aggiornamento](/help/sites-deploying/upgrade-planning.md) per ulteriori informazioni.

<!--Finally, the downtime during the upgrade can be significally reduced by indexing the repository **before** performing the upgrade. For more information, see [Using Offline Reindexing To Reduce Downtime During an Upgrade](/help/sites-deploying/upgrade-offline-reindexing.md)-->

## Prerequisiti per la migrazione {#migration-prerequisites}

* **Versione Java minima richiesta:** Lo strumento di migrazione funziona solo con le versioni Java 7 e successive. Tieni presente che per AEM 6.3 e versioni successive, le uniche versioni supportate sono Oracle JRE 8 e IBM JRE 7 e 8.

* **Istanza aggiornata:** Se stai eseguendo l&#39;aggiornamento da una versione **precedente alla 5.6**, assicurati di aver eseguito un aggiornamento sul posto ad AEM 6.0 seguendo la procedura descritta nella versione 6.0 della documentazione per l&#39;aggiornamento.

## Preparazione del file jar Quickstart di AEM {#prep-quickstart-file}

1. Arresta l&#39;istanza se è in esecuzione.

1. Scaricare il nuovo file jar di AEM e utilizzarlo per sostituire il precedente all&#39;esterno della cartella `crx-quickstart`.

1. Decomprimi il nuovo file jar quickstart eseguendo:

   ```shell
   java -Xmx4096m -jar aem-quickstart.jar -unpack
   ```

## Migrazione archivio contenuti {#content-repository-migration}

Questa migrazione non è necessaria per l’aggiornamento da AEM 6.3. Per le versioni precedenti alla 6.3, Adobe fornisce uno strumento che può essere utilizzato per migrare l’archivio alla nuova versione del Tar del segmento di Oak presente in AEM 6.3. Viene fornito come parte del pacchetto quickstart ed è obbligatorio per tutti gli aggiornamenti che utilizzeranno TarMK. Gli aggiornamenti per gli ambienti che utilizzano MongoMK non richiedono la migrazione dell’archivio. Per ulteriori informazioni sui vantaggi del nuovo formato Tar segmento, consulta le [Domande frequenti sulla migrazione ad Oak Segment Tar](/help/sites-deploying/revision-cleanup.md#online-revision-cleanup-frequently-asked-questions).

La migrazione effettiva viene eseguita utilizzando il file jar AEM quickstart standard, eseguito con una nuova opzione `-x crx2oak` che esegue lo strumento crx2oak per semplificare l&#39;aggiornamento e renderlo più robusto.

>[!NOTE]
>
>Se esegui la migrazione del contenuto dell&#39;archivio TarMK utilizzando l&#39;estensione Quickstart di CRX2Oak, puoi rimuovere la modalità di esecuzione **samplecontent** aggiungendo quanto segue alla riga di comando di migrazione:
>
>* `--promote-runmode nosamplecontent`
>

Per determinare il comando da eseguire, utilizzare il comando seguente:

```shell
java -Xmx4096m -jar aem-quickstart.jar -v -x crx2oak -xargs -- --load-profile <<YOUR_PROFILE>> <<ADDITIONAL_FLAGS>>
```

Dove `<<YOUR_PROFILE>>` e `<<ADDITIONAL_FLAGS>>` vengono sostituiti con il profilo e i flag elencati nella tabella seguente:

<table>
 <tbody>
  <tr>
   <td><strong>Archivio Source</strong></td>
   <td><strong>Archivio di destinazione</strong></td>
   <td><strong>Profilo</strong></td>
   <td><strong>Flag aggiuntivi</strong><br /> </td>
  </tr>
  <tr>
   <td>crx2 o TarMK con <code>FileDataStore</code></td>
   <td>TarMK</td>
   <td>segment-fds</td>
   <td>Consulta la sezione Risoluzione dei problemi di seguito</td>
  </tr>
  <tr>
   <td>crx2</td>
   <td>MongoMK</td>
   <td>mongo-from-crx2 </td>
   <td><code>-T mongo-uri=mongo://mongo-host:mongo-port -T mongo-db=mongo-database-name</code></td>
  </tr>
  <tr>
   <td>TarMK o crx2 con <code>S3DataStore</code></td>
   <td>TarMK</td>
   <td>segment-custom-ds</td>
   <td>Consulta la sezione Risoluzione dei problemi di seguito</td>
  </tr>
  <tr>
   <td>TarMK senza datastore</td>
   <td>TarMK</td>
   <td>segment-no-ds</td>
   <td> </td>
  </tr>
  <tr>
   <td>MongoMK</td>
   <td>MongoMK</td>
   <td>Non è necessaria alcuna migrazione</td>
   <td> </td>
  </tr>
 </tbody>
</table>

**Dove:**

* `mongo-host` è l&#39;IP del server MongoDB (ad esempio, 127.0.0.1)

* `mongo-port` è la porta del server MongoDB (ad esempio: 27017)

* `mongo-database-name` rappresenta il nome del database (ad esempio: aem-author)

**Potrebbero essere necessari ulteriori switch per i seguenti scenari:**

* Se l&#39;aggiornamento viene eseguito su un sistema Windows in cui il mapping della memoria Java non viene gestito correttamente, aggiungere il parametro `--disable-mmap` al comando.

Per ulteriori istruzioni sull&#39;utilizzo dello strumento crx2oak, vedere Utilizzo dello strumento di migrazione [CRX2Oak](/help/sites-deploying/using-crx2oak.md). Il JAR helper crx2oak può essere aggiornato manualmente, se necessario, sostituendolo manualmente con versioni più recenti dopo aver decompresso quickstart. La posizione nella cartella di installazione di AEM è: `<aem-install>/crx-quickstart/opt/extensions/crx2oak.jar`. La versione più recente dello strumento di migrazione di CRX2Oak è disponibile per il download dall&#39;archivio Adobe all&#39;indirizzo: [https://repo1.maven.org/maven2/com/adobe/granite/crx2oak/](https://repo1.maven.org/maven2/com/adobe/granite/crx2oak/)

Se la migrazione è stata completata correttamente, lo strumento verrà chiuso con un codice di uscita pari a zero. Inoltre, verificare la presenza di messaggi WARN ed ERROR nel file `upgrade.log`, che si trova in `crx-quickstart/logs` nella directory di installazione di AEM, poiché potrebbero indicare errori non irreversibili che si sono verificati durante la migrazione.

Controllare i file di configurazione nella cartella `crx-quickstart/install`. Se era necessaria una migrazione, questa verrà aggiornata per riflettere l’archivio di destinazione.

**Nota sugli archivi dati:**

Sebbene `FileDataStore` sia il nuovo valore predefinito per le installazioni di AEM 6.3, non è necessario utilizzare un datastore esterno. L’utilizzo di un archivio dati esterno è consigliato come best practice per le distribuzioni di produzione, ma non è un prerequisito per l’aggiornamento. A causa della complessità già presente nell’aggiornamento di AEM, Adobe consiglia di eseguire l’aggiornamento senza eseguire una migrazione dell’archivio dati. Se lo desideri, puoi eseguire successivamente una migrazione dell’archivio dati come sforzo separato.

## Risoluzione dei problemi di migrazione {#troubleshooting-migration-issues}

Ignora questa sezione se stai eseguendo l&#39;aggiornamento da 6.3. Anche se i profili crx2oak forniti devono soddisfare le esigenze della maggior parte dei clienti, ci sono momenti in cui saranno necessari parametri aggiuntivi. Se riscontri un errore durante la migrazione, è possibile che alcuni aspetti dell’ambiente richiedano l’inserimento di opzioni di configurazione aggiuntive. In tal caso, è probabile che si verifichi il seguente errore:

**I punti di controllo non vengono copiati perché non è stato specificato alcun archivio dati esterno. Questo comporterà la reindicizzazione completa dell’archivio al primo avvio. Utilizzare —skip-checkpoint per forzare la migrazione o visitare il sito https://jackrabbit.apache.org/oak/docs/migration.html#Checkpoints_migration per ulteriori informazioni.**

Per qualche motivo, il processo di migrazione necessita dell’accesso ai dati binari nell’archivio dati e non è in grado di trovarli. Per specificare la configurazione dell&#39;archivio dati, includere i seguenti flag nella sezione `<<ADDITIONAL_FLAGS>>` del comando di migrazione:

**Per archivi dati S3:**

```shell
--src-s3config=/path/to/SharedS3DataStore.config --src-s3datastore=/path/to/datastore
```

Dove `/path/to/SharedS3DataStore.config` rappresenta il percorso del file di configurazione dell&#39;archivio dati S3 e `/path/to/datastore` rappresenta il percorso dell&#39;archivio dati S3.

**Per archivi dati file:**

```shell
--src-datastore=/path/to/datastore
```

Dove `/path/to/datastore` rappresenta il percorso del file datastore.

## Esecuzione Dell&#39;Aggiornamento {#performing-the-upgrade}

**Se si utilizza S3:**

1. Rimuovi eventuali file jar al di sotto di `crx-quickstart/install` associati a una versione precedente del connettore S3.

1. Scarica la versione più recente del connettore 1.10.x S3 da [https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.oak.s3connector/](https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.oak.s3connector/)

1. Estrarre il pacchetto in una cartella temporanea e copiare il contenuto di `jcr_root/libs/system/install` nella cartella `crx-quickstart/install`.

### Determinazione del comando di avvio dell&#39;aggiornamento corretto {#determining-the-correct-upgrade-start-command}

Per eseguire l’aggiornamento, è importante avviare AEM utilizzando il file jar per visualizzare l’istanza. Per l&#39;aggiornamento alla versione 6.5, vedere altre opzioni di ristrutturazione e migrazione dei contenuti in [Lazy Content Migration](/help/sites-deploying/lazy-content-migration.md) che è possibile scegliere con il comando di aggiornamento.

>[!IMPORTANT]
>
>Se esegui Oracle Java 11 (o generalmente versioni di Java più recenti di 8), è necessario aggiungere opzioni aggiuntive alla riga di comando all’avvio di AEM. Per ulteriori informazioni, vedere [Java 11 Considerazioni](/help/sites-deploying/custom-standalone-install.md#java-considerations).

L’avvio di AEM dallo script di avvio non avvierà l’aggiornamento. La maggior parte dei clienti avvia AEM utilizzando lo script di avvio e ha personalizzato questo script di avvio in modo da includere gli switch per le configurazioni dell’ambiente, ad esempio le impostazioni di memoria, i certificati di sicurezza e così via. Per questo motivo, Adobe consiglia di seguire questa procedura per determinare il comando di aggiornamento corretto:

1. In un’istanza di AEM in esecuzione, esegui quanto segue dalla riga di comando:

   ```shell
   ps -ef | grep java
   ```

1. Cerca il processo AEM. Avrà un aspetto simile a:

   ```shell
   /usr/bin/java -server -Xmx1024m -Djava.awt.headless=true -Dsling.run.modes=author,crx3,crx3tar -jar crx-quickstart/app/cq-quickstart-6.5.0-standalone-quickstart.jar start -c crx-quickstart -i launchpad -p 4502 -Dsling.properties=conf/sling.properties
   ```

1. Modificare il comando sostituendo il percorso del file jar esistente ( `crx-quickstart/app/aem-quickstart*.jar` in questo caso) con il nuovo file jar di pari livello della cartella `crx-quickstart`. Utilizzando il comando precedente come esempio, il comando sarà:

   ```shell
   /usr/bin/java -server -Xmx1024m -Djava.awt.headless=true -Dsling.run.modes=author,crx3,crx3tar -jar cq-quickstart-6.5.0.jar -c crx-quickstart -p 4502 -Dsling.properties=conf/sling.properties
   ```

   In questo modo, per l’aggiornamento verranno applicate tutte le impostazioni di memoria appropriate, le modalità di esecuzione personalizzate e altri parametri ambientali. Al termine dell’aggiornamento, l’istanza può essere avviata dallo script di avvio alle avviazioni future.

## Distribuisci codebase aggiornata {#deploy-upgraded-codebase}

Al termine del processo di aggiornamento sul posto, deve essere distribuita la base di codice aggiornata. I passaggi per aggiornare la base di codice in modo che funzioni nella versione di destinazione di AEM sono disponibili nella [pagina Aggiorna codice e personalizzazioni](/help/sites-deploying/upgrading-code-and-customizations.md).

## Eseguire controlli post-aggiornamento e risoluzione dei problemi {#perform-post-upgrade-check-troubleshooting}

Consulta [Controlli post aggiornamento e risoluzione dei problemi](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md).
