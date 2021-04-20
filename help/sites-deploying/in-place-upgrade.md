---
title: Esecuzione di un aggiornamento sul posto
seo-title: Esecuzione di un aggiornamento sul posto
description: Scopri come eseguire un aggiornamento sul posto.
seo-description: Scopri come eseguire un aggiornamento sul posto.
uuid: 478cb9db-1ea8-4bdb-b333-411dcbf2d927
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
discoiquuid: fcb17227-ff1f-4b47-ae94-6b7f60923876
docset: aem65
feature: Upgrading
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1276'
ht-degree: 0%

---


# Esecuzione di un aggiornamento sul posto{#performing-an-in-place-upgrade}

>[!NOTE]
>
>Questa pagina illustra la procedura di aggiornamento per AEM 6.5. Se si dispone di un&#39;installazione distribuita su un server applicazioni, vedere [Passaggi di aggiornamento per le installazioni di Application Server](/help/sites-deploying/app-server-upgrade.md).

## Passaggi pre-aggiornamento {#pre-upgrade-steps}

Prima di eseguire l’aggiornamento, è necessario completare diversi passaggi. Per ulteriori informazioni, consulta [Aggiornamento del codice e delle personalizzazioni](/help/sites-deploying/upgrading-code-and-customizations.md) e [Attività di manutenzione pre-aggiornamento](/help/sites-deploying/pre-upgrade-maintenance-tasks.md) . Inoltre, assicurati che il sistema soddisfi i requisiti per la nuova versione di AEM. Scopri come il rilevatore pattern può aiutarti a stimare la complessità dell’aggiornamento e consulta anche la sezione Ambito di aggiornamento e requisiti di [Pianificazione dell’aggiornamento](/help/sites-deploying/upgrade-planning.md) per ulteriori informazioni.

<!--Finally, note that the downtime during the upgrade can be significally reduced by indexing the repository **before** performing the upgrade. For more information, see [Using Offline Reindexing To Reduce Downtime During an Upgrade](/help/sites-deploying/upgrade-offline-reindexing.md)-->

## Prerequisiti per la migrazione {#migration-prerequisites}

* **Versione Java minima richiesta:** lo strumento di migrazione funziona solo con Java versione 7 e successive. Nota che per AEM 6.3 e versioni successive, JRE 8 di Oracle e JRE 7 e 8 di IBM sono le uniche versioni supportate.

* **Istanza aggiornata:** se stai effettuando l’aggiornamento da una versione  **precedente alla 5.6**, assicurati di aver eseguito un aggiornamento locale a AEM 6.0 seguendo la procedura descritta nella versione 6.0 della documentazione di aggiornamento.

## Preparazione del file jar AEM Quickstart {#prep-quickstart-file}

1. Arresta l&#39;istanza se è in esecuzione.

1. Scarica il nuovo file jar AEM e utilizzalo per sostituire il vecchio all&#39;esterno della cartella `crx-quickstart` .

1. Decomprimi il nuovo jar quickstart eseguendo:

   ```shell
   java -Xmx4096m -jar aem-quickstart.jar -unpack
   ```

## Migrazione dall’archivio dei contenuti {#content-repository-migration}

Questa migrazione non è necessaria se esegui l’aggiornamento da AEM 6.3. Per le versioni precedenti alla 6.3, Adobe fornisce uno strumento che può essere utilizzato per migrare l’archivio alla nuova versione del Segment Tar Oak presente nella AEM 6.3. Viene fornito come parte del pacchetto quickstart ed è obbligatorio per tutti gli aggiornamenti che utilizzeranno TarMK. Gli aggiornamenti per gli ambienti che utilizzano MongoMK non richiedono la migrazione dell’archivio. Per ulteriori informazioni sui vantaggi del nuovo formato Segment Tar, consulta le [Domande frequenti sulla migrazione a Oak Segment Tar](/help/sites-deploying/revision-cleanup.md#online-revision-cleanup-frequently-asked-questions) .

La migrazione effettiva viene eseguita utilizzando il file jar standard AEM quickstart, eseguito con una nuova opzione `-x crx2oak` che esegue lo strumento crx2oak per semplificare l&#39;aggiornamento e renderlo più affidabile.

>[!NOTE]
>
>Se esegui la migrazione dei contenuti dell’archivio TarMK utilizzando l’estensione CRX2Oak Quickstart, puoi rimuovere la modalità runmode **samplecontent** aggiungendo quanto segue alla riga di comando di migrazione:
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
   <td><strong>Archivio di origine</strong></td>
   <td><strong>Archivio di Target</strong></td>
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
   <td>TarMK senza archivio dati</td>
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

* `mongo-port` è la porta del server MongoDB (ad esempio: (27017)

* `mongo-database-name` rappresenta il nome del database (ad esempio: aem-author)

**È inoltre possibile richiedere opzioni aggiuntive per i seguenti scenari:**

* Se esegui l&#39;aggiornamento su un sistema Windows in cui la mappatura della memoria Java non è gestita correttamente, aggiungi il parametro `--disable-mmap` al comando.

* Se utilizzi Java 7, aggiungi il parametro `-XX:MaxPermSize=2048m` subito dopo il parametro `-Xmx` .

Per ulteriori istruzioni sull&#39;utilizzo dello strumento crx2oak, consulta Utilizzo dello [strumento di migrazione CRX2Oak](/help/sites-deploying/using-crx2oak.md). L&#39;helper crx2oak JAR può essere aggiornato manualmente, se necessario, sostituendolo manualmente con le versioni più recenti dopo aver decompresso l&#39;avvio rapido. La posizione nella cartella di installazione AEM è: `<aem-install>/crx-quickstart/opt/extensions/crx2oak.jar`. L’ultima versione dello strumento di migrazione CRX2Oak è disponibile per il download dall’archivio Adobe all’indirizzo: [https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/crx2oak/](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/crx2oak/)

Se la migrazione è stata completata con successo, lo strumento uscirà con un codice di uscita pari a zero. Inoltre, controlla i messaggi WARN e ERROR nel file `upgrade.log`, situato sotto `crx-quickstart/logs` nella directory di installazione AEM, in quanto questi potrebbero indicare errori non fatali che si sono verificati durante la migrazione.

Controlla i file di configurazione sotto la cartella `crx-quickstart/install` . Se è stata necessaria una migrazione, queste verranno aggiornate per riflettere l’archivio di destinazione.

**Una nota sui datastore:**

Anche se `FileDataStore` è la nuova impostazione predefinita per le installazioni AEM 6.3, non è necessario utilizzare un datastore esterno. L’utilizzo di un datastore esterno è consigliato come best practice per le distribuzioni di produzione, ma non è un prerequisito per l’aggiornamento. A causa della complessità già presente nell’aggiornamento AEM, si consiglia di eseguire l’aggiornamento senza eseguire una migrazione al datastore. Se lo desideri, una migrazione all’archivio dati può essere eseguita successivamente come sforzo separato.

## Risoluzione dei problemi relativi alla migrazione {#troubleshooting-migration-issues}

Ignora questa sezione se stai effettuando l’aggiornamento dalla versione 6.3. Anche se i profili crx2oak forniti devono soddisfare le esigenze della maggior parte dei clienti, ci sono momenti in cui saranno necessari parametri aggiuntivi. Se si verifica un errore durante la migrazione, è possibile che ci siano alcuni aspetti dell’ambiente che richiedono opzioni di configurazione aggiuntive da fornire. In tal caso, si verificherà probabilmente il seguente errore:

**I checkpoint non verranno copiati perché non è stato specificato alcun datastore esterno. Questo si tradurrà nella reindicizzazione completa del repository al primo avvio. Utilizza —salta-punti di controllo per forzare la migrazione oppure consulta https://jackrabbit.apache.org/oak/docs/migration.html#Checkpoints_migration per ulteriori informazioni.**

Per qualche motivo, il processo di migrazione richiede l’accesso ai binari nel datastore e non è in grado di trovarlo. Per specificare la configurazione del datastore, includi i seguenti flag nella sezione `<<ADDITIONAL_FLAGS>>` del comando di migrazione:

**Per i datastore S3:**

```shell
--src-s3config=/path/to/SharedS3DataStore.config --src-s3datastore=/path/to/datastore
```

Dove `/path/to/SharedS3DataStore.config` rappresenta il percorso del file di configurazione del datastore S3 e `/path/to/datastore` rappresenta il percorso del datastore S3.

**Per i datastore dei file:**

```shell
--src-datastore=/path/to/datastore
```

Dove `/path/to/datastore` rappresenta il percorso del file Datastore.

## Esecuzione dell&#39;aggiornamento {#performing-the-upgrade}

**Se si utilizza S3:**

1. Rimuovi eventuali jar sotto `crx-quickstart/install` associati a una versione precedente del connettore S3.

1. Scarica la versione più recente del connettore S3 1.10.x da [https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/com.adobe.granite.oak.s3connector/](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/com.adobe.granite.oak.s3connector/)

1. Estrai il pacchetto in una cartella temporanea e copia il contenuto di `jcr_root/libs/system/install` nella cartella `crx-quickstart/install`.

### Determinazione del comando di avvio dell&#39;aggiornamento corretto {#determining-the-correct-upgrade-start-command}

Per eseguire l&#39;aggiornamento, è importante iniziare a AEM utilizzando il file jar per visualizzare l&#39;istanza. Per l’aggiornamento alla versione 6.5, consulta anche altre opzioni di ristrutturazione e migrazione dei contenuti in [Migrazione dei contenuti pigri](/help/sites-deploying/lazy-content-migration.md) che puoi scegliere con il comando di aggiornamento.

>[!IMPORTANT]
>
>Se esegui Oracle Java 11 (o in genere versioni di Java successive a 8), all&#39;avvio di AEM dovrai aggiungere altri switch alla riga di comando. Per ulteriori informazioni, consulta [Considerazioni su Java 11](/help/sites-deploying/custom-standalone-install.md#java-considerations).

Tieni presente che l’avvio AEM dallo script iniziale non avvierà l’aggiornamento. La maggior parte dei clienti inizia a AEM utilizzando lo script di avvio e ha personalizzato questo script di avvio per includere switch per configurazioni di ambiente quali impostazioni di memoria, certificati di sicurezza, ecc. Per questo motivo, si consiglia di seguire questa procedura per determinare il comando di aggiornamento corretto:

1. In un&#39;istanza AEM in esecuzione, esegui quanto segue dalla riga di comando:

   ```shell
   ps -ef | grep java
   ```

1. Cerca il processo AEM. Avrà un aspetto simile a:

   ```shell
   /usr/bin/java -server -Xmx1024m -XX:MaxPermSize=256M -Djava.awt.headless=true -Dsling.run.modes=author,crx3,crx3tar -jar crx-quickstart/app/cq-quickstart-6.2.0-standalone-quickstart.jar start -c crx-quickstart -i launchpad -p 4502 -Dsling.properties=conf/sling.properties
   ```

1. Modifica il comando sostituendo il percorso del jar esistente ( `crx-quickstart/app/aem-quickstart*.jar` in questo caso) con il nuovo jar di pari livello della cartella `crx-quickstart`. Utilizzando il comando precedente come esempio, il nostro comando sarebbe:

   ```shell
   /usr/bin/java -server -Xmx1024m -XX:MaxPermSize=256M -Djava.awt.headless=true -Dsling.run.modes=author,crx3,crx3tar -jar cq-quickstart-6.5.0.jar -c crx-quickstart -p 4502 -Dsling.properties=conf/sling.properties
   ```

   In questo modo verranno applicate tutte le impostazioni di memoria, le modalità di esecuzione personalizzate e altri parametri ambientali appropriati per l’aggiornamento. Una volta completato l’aggiornamento, l’istanza può essere avviata dallo script iniziale nelle prossime avviazioni.

## Distribuire una base di codice aggiornata {#deploy-upgraded-codebase}

Una volta completato il processo di aggiornamento sul posto, la base di codice aggiornata deve essere distribuita. I passaggi per aggiornare la base di codice in modo che funzioni nella versione di destinazione di AEM si trovano nella [pagina Aggiorna codice e personalizzazioni](/help/sites-deploying/upgrading-code-and-customizations.md).

## Esegui verifiche post-aggiornamento e risoluzione dei problemi {#perform-post-upgrade-check-troubleshooting}

Consulta [Controlli post aggiornamento e risoluzione dei problemi](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md).
