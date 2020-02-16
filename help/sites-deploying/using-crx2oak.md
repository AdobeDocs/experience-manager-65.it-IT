---
title: Utilizzo dello strumento di migrazione CRX2Oak
seo-title: Utilizzo dello strumento di migrazione CRX2Oak
description: Scoprite come utilizzare lo strumento di migrazione CRX2Oak.
seo-description: Scoprite come utilizzare lo strumento di migrazione CRX2Oak.
uuid: 9b788981-4ef0-446e-81f0-c327cdd3214b
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: e938bdc7-f8f5-4da5-81f6-7f60c6b4b8e6
translation-type: tm+mt
source-git-commit: 24290b65a126822eb918fbecc978372394b5b655

---


# Utilizzo dello strumento di migrazione CRX2Oak{#using-the-crx-oak-migration-tool}

## Introduzione {#introduction}

CRX2Oak è uno strumento progettato per migrare i dati tra diversi repository.

Può essere utilizzato per migrare i dati dalle versioni precedenti di CQ basate su Apache Jackrabbit 2 a Oak e può essere utilizzato anche per copiare i dati tra i repository Oak.

È possibile scaricare la versione più recente di crx2oak dall&#39;archivio pubblico di Adobe in questa posizione:[https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/crx2oak/](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/crx2oak/)

L’elenco delle modifiche e delle correzioni per la versione più recente è disponibile nelle note [sulla versione di](https://docs.adobe.com/content/help/en/experience-manager-64/release-notes/crx2oak.html)CRX2Oak.

>[!NOTE]
>
>Per ulteriori informazioni su Apache Oak e sui concetti chiave della persistenza di AEM, consultate [Introduzione alla piattaforma](/help/sites-deploying/platform.md)AEM.

## Casi di utilizzo della migrazione {#migration-use-cases}

Lo strumento può essere utilizzato per:

* Migrazione dalle versioni precedenti di CQ 5 ad AEM 6
* Copia dei dati tra più repository Oak
* Conversione di dati tra diverse implementazioni Oak MicroKernel.

Il supporto per la migrazione dei repository tramite store Blob esterni (comunemente noti come Data Store) è fornito in diverse combinazioni. Un possibile percorso di migrazione è da un repository CRX2 che utilizza un repository esterno `FileDataStore` a un repository Oak utilizzando un `S3DataStore`.

Il diagramma seguente illustra tutte le possibili combinazioni di migrazione supportate da CRX2Oak:

![chlimage_1-151](assets/chlimage_1-151.png)

## Funzioni {#features}

CRX2Oak viene chiamato durante gli aggiornamenti di AEM in un modo in cui l&#39;utente può specificare un profilo di migrazione predefinito che automatizza la riconfigurazione delle modalità di persistenza. Questa è chiamata modalità di avvio rapido.

Può anche essere eseguito separatamente nel caso in cui richieda una maggiore personalizzazione. Tuttavia, in questa modalità le modifiche vengono apportate solo all’archivio e ogni ulteriore riconfigurazione di AEM deve essere eseguita manualmente. Questa modalità è detta modalità autonoma.

Un&#39;altra cosa da notare è che con le impostazioni predefinite in modalità standalone, verrà migrato solo il Node Store e il nuovo repository riutilizzerà il vecchio archivio binario.

### Modalità QuickStart Automatizzata {#automated-quickstart-mode}

Da AEM 6.3, CRX2Oak è in grado di gestire i profili di migrazione definiti dall’utente che possono essere configurati con tutte le opzioni di migrazione già disponibili. Ciò consente sia una maggiore flessibilità sia la possibilità di automatizzare la configurazione di AEM, funzioni non disponibili se si utilizza lo strumento in modalità standalone.

Per passare da CRX2Oak alla modalità QuickStart è necessario definire il percorso della cartella crx-quickstart nella directory di installazione di AEM tramite questa variabile ambientale del sistema operativo:

**Per sistemi basati su UNIX e macOS:**

```shell
export SLING_HOME="/path/to/crx-quickstart"
```

**Per Windows:**

```shell
SET "SLING_HOME=/path/to/crx-quickstart"
```

#### Supporto di ripresa {#resume-support}

La migrazione può essere interrotta in qualsiasi momento, con la possibilità di riprenderla successivamente.

#### Logica di aggiornamento personalizzabile {#customizable-upgrade-logic}

La logica Java personalizzata può essere implementata anche utilizzando `CommitHooks`. È possibile implementare `RepositoryInitializer` classi personalizzate per inizializzare l&#39;archivio con valori personalizzati.

#### Supporto per le operazioni con mappatura memoria {#support-for-memory-mapped-operations}

CRX2Oak supporta anche le operazioni di mappatura della memoria per impostazione predefinita. La mappatura della memoria migliora notevolmente le prestazioni e dovrebbe essere utilizzata quando possibile.

>[!CAUTION]
>
>Tuttavia, le operazioni mappate sulla memoria non sono supportate per le piattaforme Windows. Pertanto, è consigliabile aggiungere il parametro **—disable-mmap** quando si esegue la migrazione in Windows.

#### Migrazione selettiva dei contenuti {#selective-migration-of-content}

Per impostazione predefinita, lo strumento esegue la migrazione dell&#39;intero repository sotto il `"/"` percorso. Tuttavia, avete il controllo completo sul contenuto da migrare.

Se nella nuova istanza è presente una parte del contenuto non necessaria, potete utilizzare il `--exclude-path` parametro per escludere il contenuto e ottimizzare la procedura di aggiornamento.

#### Unione dei percorsi {#path-merging}

Se i dati devono essere copiati tra due repository e si ha un percorso di contenuto diverso su entrambe le istanze, è possibile definirlo nel `--merge-path` parametro. Una volta fatto, CRX2Oak copierà solo i nuovi nodi nel repository di destinazione e manterrà quelli vecchi in posizione.

![chlimage_1-152](assets/chlimage_1-152.png)

#### Supporto per le versioni {#version-support}

Per impostazione predefinita, AEM crea una versione di ogni nodo o pagina che viene modificata e la archivia nella directory archivio. Le versioni possono quindi essere utilizzate per ripristinare lo stato precedente della pagina.

Tuttavia, queste versioni non vengono mai eliminate anche se la pagina originale viene eliminata. Quando si utilizzano repository in funzione da molto tempo, la migrazione potrebbe dover elaborare molti dati ridondanti causati dalle versioni orfane.

Una caratteristica utile per questi tipi di situazioni è l&#39;aggiunta del `--copy-versions` parametro. Può essere utilizzato per saltare i nodi di versione durante la migrazione o la copia di un repository.

Potete anche scegliere se copiare le versioni orfane aggiungendo `--copy-orphaned-versions=true`.

Entrambi i parametri supportano anche un formato di `YYYY-MM-DD` data, nel caso in cui si desideri copiare le versioni entro una data specifica.

![chlimage_1-153](assets/chlimage_1-153.png)

#### Open Source Version {#open-source-version}

Una versione open source di CRX2Oak è disponibile sotto forma di aggiornamento della quercia. Supporta tutte le funzioni tranne:

* Supporto CRX2
* Supporto profilo di migrazione
* Supporto per la riconfigurazione automatica di AEM

See the [Apache Documentation](https://jackrabbit.apache.org/oak/docs/migration.html) for more information.

## Parametri {#parameters}

### Opzioni store nodo {#node-store-options}

* `--cache`: Dimensione cache in MB (impostazione predefinita: `256`)

* `--mmap`: Abilita accesso ai file mappati di memoria per l&#39;archivio segmenti
* `--src-password:` Password per il database RDB di origine

* `--src-user:` Utente per l&#39;RDB di origine

* `--user`: Utente per il RDB di destinazione

* `--password`: Password per il RDB di destinazione.

### Opzioni di migrazione {#migration-options}

* `--early-shutdown`: Chiude l&#39;archivio JCR2 di origine dopo che i nodi vengono copiati e prima che vengano applicati i ganci di commit
* `--fail-on-error`: Impone un errore di migrazione se i nodi non possono essere letti dall&#39;archivio di origine.
* `--ldap`: Migra gli utenti LDAP da un’istanza CQ 5.x a una basata su Oak. Affinché questo funzioni, il provider di identità nella configurazione Oak deve essere denominato ldap. For more information, see the [LDAP documentation](/help/sites-administering/ldap-config.md).

* `--ldap-config:` Utilizzate questo insieme al `--ldap` parametro per i repository CQ 5.x che utilizzavano più server LDAP per l’autenticazione. È possibile utilizzarlo per puntare ai file CQ 5.x `ldap_login.conf` o di `jaas.conf` configurazione. Il formato è `--ldapconfig=path/to/ldap_login.conf`.

### Opzioni store versione {#version-store-options}

* `--copy-orphaned-versions`: Ignora la copia delle versioni isolate. I parametri supportati sono: `true`, `false` e `yyyy-mm-dd`. Impostazione predefinita `true`.

* `--copy-versions:` Copia l&#39;archivio delle versioni. Parameters: `true`, `false`, `yyyy-mm-dd`. Impostazione predefinita `true`.

#### Opzioni percorso {#path-options}

* `--include-paths:` Elenco di percorsi separati da virgola da includere durante la copia
* `--merge-paths`: Elenco di percorsi da unire separati da virgola durante la copia
* `--exclude-paths:` Elenco di percorsi da escludere durante la copia separati da virgole.

### Opzioni store BLOB di origine {#source-blob-store-options}

* `--src-datastore:` La directory datastore da utilizzare come origine `FileDataStore`

* `--src-fileblobstore`: La directory datastore da utilizzare come origine `FileBlobStore`

* `--src-s3datastore`: La directory del datastore da utilizzare per l&#39;origine `S3DataStore`

* `--src-s3config`: Il file di configurazione per l&#39;origine `S3DataStore`.

### Opzioni BlobStore di destinazione {#destination-blobstore-options}

* `--datastore:` La directory del datastore da utilizzare come destinazione `FileDataStore`

* `--fileblobstore:` La directory del datastore da utilizzare come destinazione `FileBlobStore`

* `--s3datastore`: La directory del datastore da utilizzare per la destinazione `S3DataStore`

* `--s3config`: Il file di configurazione per la destinazione `S3DataStore`.

### Opzioni della Guida {#help-options}

* `-?, -h, --help:` Visualizza le informazioni della guida.

## Debug {#debugging}

Potete inoltre abilitare le informazioni di debug per il processo di migrazione al fine di risolvere eventuali problemi che potrebbero verificarsi durante il processo. È possibile eseguire questa operazione in modo diverso a seconda della modalità in cui si desidera eseguire lo strumento:

<table>
 <tbody>
  <tr>
   <td><strong>Modalità CRX2Oak</strong></td>
   <td><strong>Azione</strong></td>
  </tr>
  <tr>
   <td>Modalità Quickstart</td>
   <td>Quando si esegue CRX2Oak, è possibile aggiungere alla riga di comando le <strong>opzioni DEBUG a livello di</strong> log (TRACE <strong>o </strong>di log) della riga di comando. In questa modalità i registri vengono automaticamente reindirizzati al file <strong>upgrade.log</strong>.</td>
  </tr>
  <tr>
   <td>Modalità indipendente</td>
   <td><p>Aggiungete le opzioni <strong>—trace</strong> alla riga di comando CRX2Oak per mostrare gli eventi TRACE sull'output standard (è necessario reindirizzare i log manualmente utilizzando il carattere di reindirizzamento: '&gt;' o 'tee' per un'ispezione successiva).</p> </td>
  </tr>
 </tbody>
</table>

## Altre considerazioni {#other-considerations}

Durante la migrazione a un set di repliche MongoDB, assicurarsi di impostare il `WriteConcern` parametro su `2` tutte le connessioni ai database Mongo.

A questo scopo, aggiungete il `w=2` parametro alla fine della stringa di connessione, come segue:

```xml
java -Xmx4092m -XX:MaxPermSize=1024m -jar crx2oak.jar crx-quickstart/repository/ mongodb://localhost:27017/aem-author?replicaset=replica1&w=2
```

>[!NOTE]
>
>Per ulteriori informazioni, consulta la documentazione sulla stringa di connessione MongoDB in [Write Concerns](https://docs.mongodb.org/manual/reference/connection-string/#write-concern-options).

