---
title: Esecuzione di un aggiornamento locale
seo-title: Esecuzione di un aggiornamento locale
description: Scopri come eseguire un aggiornamento locale.
seo-description: Scopri come eseguire un aggiornamento locale.
uuid: 478cb9db-1ea8-4bdb-b333-411dcbf2d927
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
discoiquuid: fcb17227-ff1f-4b47-ae94-6b7f60923876
docset: aem65
translation-type: tm+mt
source-git-commit: b8a532f45f531f36e04ff4b5f0cc2c9e729668bb
workflow-type: tm+mt
source-wordcount: '1275'
ht-degree: 0%

---


# Esecuzione di un aggiornamento locale{#performing-an-in-place-upgrade}

>[!NOTE]
>
>Questa pagina illustra la procedura di aggiornamento per AEM 6.5. Se disponete di un&#39;installazione distribuita su un server applicazione, consultate Procedura [di aggiornamento per le installazioni](/help/sites-deploying/app-server-upgrade.md)di Application Server.

## Passaggi pre-aggiornamento {#pre-upgrade-steps}

Prima di eseguire l&#39;aggiornamento, è necessario completare diversi passaggi. Per ulteriori informazioni, consulta [Aggiornamento di codice e personalizzazioni](/help/sites-deploying/upgrading-code-and-customizations.md) e attività [di manutenzione](/help/sites-deploying/pre-upgrade-maintenance-tasks.md) pre-aggiornamento. Inoltre, accertatevi che il sistema soddisfi i requisiti per la nuova versione di AEM. Scopri come il Rilevatore di pattern può aiutarti a stimare la complessità dell&#39;aggiornamento e come consultare la sezione Ambito e requisiti dell&#39;aggiornamento di [Planning Your Upgrade](/help/sites-deploying/upgrade-planning.md) per ulteriori informazioni.

<!--Finally, note that the downtime during the upgrade can be significally reduced by indexing the repository **before** performing the upgrade. For more information, see [Using Offline Reindexing To Reduce Downtime During an Upgrade](/help/sites-deploying/upgrade-offline-reindexing.md)-->

## Prerequisiti per la migrazione {#migration-prerequisites}

* **Versione Java minima richiesta:** Lo strumento di migrazione funziona solo con Java versione 7 e versioni successive. Per AEM 6.3 e versioni successive, Oracle&#39;s JRE 8 e IBM JRE 7 &amp; 8 sono le uniche versioni supportate.

* **Istanza aggiornata:** Se state effettuando l&#39;aggiornamento da una versione **precedente alla 5.6**, accertatevi di aver eseguito un aggiornamento locale a AEM 6.0 seguendo la procedura descritta nella versione 6.0 della documentazione relativa all&#39;aggiornamento.

## Preparazione del file JAR AEM Quickstart {#prep-quickstart-file}

1. Arrestate l&#39;istanza se è in esecuzione.

1. Scaricate il nuovo file AEM jar e utilizzatelo per sostituire il vecchio file esterno alla `crx-quickstart` cartella.

1. Estrai il nuovo jar di avvio rapido eseguendo:

   ```shell
   java -Xmx4096m -jar aem-quickstart.jar -unpack
   ```

## Migrazione all&#39;archivio dei contenuti {#content-repository-migration}

Questa migrazione non è necessaria se effettui l’aggiornamento da AEM 6.3. Per le versioni precedenti alla 6.3,  Adobe fornisce uno strumento che può essere utilizzato per migrare l&#39;archivio alla nuova versione della ar del segmento Oak presente nella AEM 6.3. Viene fornito come parte del pacchetto QuickStart ed è obbligatorio per tutti gli aggiornamenti che utilizzeranno TarMK. Gli aggiornamenti per gli ambienti che utilizzano MongoMK non richiedono la migrazione dell&#39;archivio. For more information on what the benefits of the new Segment Tar format are, see the [Migrating to Oak Segment Tar FAQ](/help/sites-deploying/revision-cleanup.md#online-revision-cleanup-frequently-asked-questions).

La migrazione effettiva viene eseguita utilizzando il file Jar AEM QuickStart standard, eseguito con una nuova `-x crx2oak` opzione che esegue lo strumento crx2oak per semplificare l&#39;aggiornamento e renderlo più affidabile.

>[!NOTE]
>
>Se si esegue la migrazione del contenuto dell&#39;archivio TarMK utilizzando l&#39;estensione CRX2Oak Quickstart, è possibile rimuovere la modalità di esecuzione del contenuto **di** esempio aggiungendo quanto segue alla riga di comando di migrazione:
>
>* `--promote-runmode nosamplecontent`

>



Per determinare il comando da eseguire, utilizzare il comando seguente:

```shell
java -Xmx4096m -jar aem-quickstart.jar -v -x crx2oak -xargs -- --load-profile <<YOUR_PROFILE>> <<ADDITIONAL_FLAGS>>
```

Dove `<<YOUR_PROFILE>>` e `<<ADDITIONAL_FLAGS>>` sono sostituiti con il profilo e i contrassegni elencati nella seguente tabella:

<table>
 <tbody>
  <tr>
   <td><strong>Repository di origine</strong></td>
   <td><strong>Repository di Target</strong></td>
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
   <td>Nessuna migrazione necessaria</td>
   <td> </td>
  </tr>
 </tbody>
</table>

**Dove:**

* `mongo-host` è l&#39;IP del server MongoDB (ad esempio, 127.0.0.1)

* `mongo-port` è la porta del server MongoDB (ad esempio: (27017)

* `mongo-database-name` rappresenta il nome del database (ad esempio: aem-author)

**Potete anche richiedere opzioni aggiuntive per i seguenti scenari:**

* Se si esegue l&#39;aggiornamento in un sistema Windows in cui la mappatura della memoria Java non viene gestita correttamente, aggiungere il `--disable-mmap` parametro al comando.

* Se utilizzate Java 7, aggiungete il `-XX:MaxPermSize=2048m` parametro subito dopo il `-Xmx` parametro.

Per ulteriori istruzioni sull&#39;utilizzo dello strumento crx2oak, vedere Utilizzo dello strumento [di migrazione](/help/sites-deploying/using-crx2oak.md)CRX2Oak. Il supporto crx2oak JAR può essere aggiornato manualmente, se necessario, sostituendolo manualmente con le versioni più recenti dopo aver disimballato il QuickStart. Il percorso nella cartella di installazione AEM è: `<aem-install>/crx-quickstart/opt/extensions/crx2oak.jar`. La versione più recente dello strumento di migrazione CRX2Oak è disponibile per il download dall&#39;archivio  Adobi all&#39;indirizzo: [https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/crx2oak/](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/crx2oak/)

Se la migrazione è stata completata correttamente, lo strumento uscirà con un codice di uscita pari a zero. Inoltre, verificare la presenza di messaggi WARN e ERROR nel `upgrade.log` file, situato `crx-quickstart/logs` nella directory di installazione AEM, in quanto questi potrebbero indicare errori non irreversibili che si sono verificati durante la migrazione.

Controllate i file di configurazione al di sotto della `crx-quickstart/install` cartella. Se fosse necessaria una migrazione, queste verranno aggiornate per riflettere il repository di destinazione.

**Una nota sulle attività di datastores:**

Sebbene `FileDataStore` sia il nuovo valore predefinito per le installazioni AEM 6.3, non è necessario utilizzare un datastore esterno. Anche se l&#39;utilizzo di un archivio dati esterno è consigliato come procedura ottimale per le distribuzioni di produzione, non è un prerequisito per l&#39;aggiornamento. A causa della complessità già presente nel AEM di aggiornamento, si consiglia di eseguire l&#39;aggiornamento senza eseguire una migrazione degli archivi di dati. Se necessario, una migrazione degli archivi di dati può essere eseguita successivamente come sforzo separato.

## Risoluzione dei problemi di migrazione {#troubleshooting-migration-issues}

Ignora questa sezione se stai effettuando l&#39;aggiornamento dalla versione 6.3. Anche se i profili crx2oak forniti devono soddisfare le esigenze della maggior parte dei clienti, ci sono volte in cui saranno necessari parametri aggiuntivi. Se si verifica un errore durante la migrazione, è possibile che alcuni aspetti dell&#39;ambiente richiedano ulteriori opzioni di configurazione. In tal caso, si verificherà probabilmente il seguente errore:

**I punti di controllo non verranno copiati perché non è stato specificato alcun archivio dati esterno. Questo si tradurrà nella reindicizzazione completa del repository al primo avvio. Utilizzate —skip-checkpoint per forzare la migrazione o consultate https://jackrabbit.apache.org/oak/docs/migration.html#Checkpoints_migration per ulteriori informazioni.**

Per qualche motivo, il processo di migrazione ha bisogno dell&#39;accesso ai file binari nel datastore e non è in grado di trovarlo. Per specificare la configurazione del datastore, includi i seguenti flag nella `<<ADDITIONAL_FLAGS>>` parte del comando di migrazione:

**Per i datastores S3:**

```shell
--src-s3config=/path/to/SharedS3DataStore.config --src-s3datastore=/path/to/datastore
```

Dove `/path/to/SharedS3DataStore.config` rappresenta il percorso del file di configurazione del datastore S3 e `/path/to/datastore` rappresenta il percorso del datastore S3.

**Per i file di archivio dati:**

```shell
--src-datastore=/path/to/datastore
```

Dove `/path/to/datastore` rappresenta il percorso del datastore del file.

## Esecuzione Dell&#39;Aggiornamento {#performing-the-upgrade}

**Se si utilizza S3:**

1. Rimuovere eventuali barattoli sotto `crx-quickstart/install` associati a una versione precedente del connettore S3.

1. Scaricate l&#39;ultima versione del connettore S3 1.10.x da [https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/com.adobe.granite.oak.s3connector/](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/com.adobe.granite.oak.s3connector/)

1. Estraete il pacchetto in una cartella temporanea e copiate il contenuto di tale pacchetto `jcr_root/libs/system/install` nella `crx-quickstart/install` cartella.

### Determinazione del comando di avvio dell&#39;aggiornamento corretto {#determining-the-correct-upgrade-start-command}

Per eseguire l&#39;aggiornamento, è importante iniziare a AEM utilizzando il file jar per visualizzare l&#39;istanza. Per l&#39;aggiornamento alla versione 6.5, potete vedere anche altre opzioni di ristrutturazione e migrazione dei contenuti in Migrazione [dei contenuti](/help/sites-deploying/lazy-content-migration.md) Lazy che potete scegliere con il comando di aggiornamento.

>[!IMPORTANT]
>
>Se si esegue Oracle Java 11 (o in genere versioni di Java successive a 8), all&#39;avvio della AEM è necessario aggiungere alla riga di comando ulteriori switch. Per ulteriori informazioni, consultate Considerazioni relative a [Java 11](/help/sites-deploying/custom-standalone-install.md#java-considerations).

L&#39;avvio AEM dallo script iniziale non avvia l&#39;aggiornamento. La maggior parte dei clienti inizia AEM utilizzare lo script iniziale e ha personalizzato questo script iniziale per includere opzioni per le configurazioni di ambiente quali le impostazioni di memoria, i certificati di protezione, ecc. Per questo motivo, si consiglia di seguire questa procedura per determinare il comando di aggiornamento corretto:

1. In un&#39;istanza AEM in esecuzione, eseguire quanto segue dalla riga di comando:

   ```shell
   ps -ef | grep java
   ```

1. Cercare il processo AEM. Sarà simile a:

   ```shell
   /usr/bin/java -server -Xmx1024m -XX:MaxPermSize=256M -Djava.awt.headless=true -Dsling.run.modes=author,crx3,crx3tar -jar crx-quickstart/app/cq-quickstart-6.2.0-standalone-quickstart.jar start -c crx-quickstart -i launchpad -p 4502 -Dsling.properties=conf/sling.properties
   ```

1. Modificate il comando sostituendo il percorso della cartella esistente ( `crx-quickstart/app/aem-quickstart*.jar` in questo caso) con la nuova vasca di pari livello della `crx-quickstart` cartella. Utilizzando il nostro precedente comando come esempio, il nostro comando sarebbe:

   ```shell
   /usr/bin/java -server -Xmx1024m -XX:MaxPermSize=256M -Djava.awt.headless=true -Dsling.run.modes=author,crx3,crx3tar -jar cq-quickstart-6.5.0.jar -c crx-quickstart -p 4502 -Dsling.properties=conf/sling.properties
   ```

   In questo modo tutte le impostazioni di memoria corrette, le modalità di esecuzione personalizzate e altri parametri ambientali verranno applicati per l&#39;aggiornamento. Al termine dell&#39;aggiornamento, l&#39;istanza potrebbe essere avviata a partire dallo script iniziale per le prossime startup.

## Distribuisci Codebase Aggiornata {#deploy-upgraded-codebase}

Una volta completato il processo di aggiornamento locale, è necessario distribuire la base di codice aggiornata. I passaggi per aggiornare la base di codice in modo che funzioni nella versione di destinazione di AEM si trovano nella pagina [](/help/sites-deploying/upgrading-code-and-customizations.md)Aggiorna codice e personalizzazioni.

## Esegui verifiche e risoluzione dei problemi post-aggiornamento {#perform-post-upgrade-check-troubleshooting}

Consulta Controllo [post aggiornamento e risoluzione dei problemi](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md).
