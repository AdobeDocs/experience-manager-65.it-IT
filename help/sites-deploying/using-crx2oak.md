---
title: Utilizzo dello strumento di migrazione CRX2Oak
seo-title: Using the CRX2Oak Migration Tool
description: Scopri come utilizzare lo strumento di migrazione CRX2Oak.
seo-description: Learn how to use the CRX2Oak migration tool.
uuid: 9b788981-4ef0-446e-81f0-c327cdd3214b
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: e938bdc7-f8f5-4da5-81f6-7f60c6b4b8e6
feature: Upgrading
exl-id: ef3895b9-8d35-4881-8188-c864ae3f0b4c
source-git-commit: 08e7cbe50fbfb301b38c3c36dfa22bfc1024e181
workflow-type: tm+mt
source-wordcount: '1248'
ht-degree: 0%

---

# Utilizzo dello strumento di migrazione CRX2Oak{#using-the-crx-oak-migration-tool}

## Introduzione {#introduction}

CRX2Oak è uno strumento progettato per migrare i dati tra archivi diversi.

Può essere utilizzato per migrare i dati dalle versioni precedenti di CQ basate su Apache Jackrabbit 2 a Oak e può anche essere utilizzato per copiare i dati tra archivi Oak.

Puoi scaricare la versione più recente di crx2oak dall&#39;archivio pubblico di Adobe in questa posizione:
[https://repo1.maven.org/maven2/com/adobe/granite/crx2oak/](https://repo1.maven.org/maven2/com/adobe/granite/crx2oak/)

L&#39;elenco delle modifiche e delle correzioni per la versione più recente si trova nella [Note sulla versione di CRX2Oak](https://docs.adobe.com/content/help/en/experience-manager-64/release-notes/crx2oak.html).

>[!NOTE]
>
>Per ulteriori informazioni su Apache Oak e sui concetti chiave della persistenza AEM, consulta [Introduzione alla piattaforma AEM](/help/sites-deploying/platform.md).

## Casi di utilizzo della migrazione {#migration-use-cases}

Lo strumento può essere utilizzato per:

* Migrazione dalle versioni precedenti di CQ 5 a AEM 6
* Copia dei dati tra più archivi Oak
* Conversione di dati tra diverse implementazioni di Oak MicroKernel.

Il supporto per la migrazione degli archivi tramite Blob Store esterni (comunemente noti come Data Store) è fornito in diverse combinazioni. Un possibile percorso di migrazione è tratto da un archivio CRX2 che utilizza un `FileDataStore` a un archivio Oak utilizzando `S3DataStore`.

Il diagramma seguente illustra tutte le possibili combinazioni di migrazione supportate da CRX2Oak:

![chlimage_1-151](assets/chlimage_1-151.png)

## Funzioni {#features}

CRX2Oak viene chiamato durante gli aggiornamenti AEM in un modo in cui l&#39;utente può specificare un profilo di migrazione predefinito che automatizza la riconfigurazione delle modalità di persistenza. Si chiama modalità quickstart .

Può anche essere eseguito separatamente nel caso in cui richieda una maggiore personalizzazione. Tuttavia, in questa modalità le modifiche vengono apportate solo all’archivio e ogni ulteriore riconfigurazione di AEM deve essere eseguita manualmente. Si chiama modalità autonoma.

Un&#39;altra cosa da notare è che con le impostazioni predefinite in modalità autonoma, verrà effettuata la migrazione solo del Node Store e il nuovo archivio riutilizzerà il vecchio archivio binario.

### Modalità Quickstart automatica {#automated-quickstart-mode}

A partire dalla versione 6.3 di AEM, CRX2Oak è in grado di gestire profili di migrazione definiti dall’utente che possono essere configurati con tutte le opzioni di migrazione già disponibili. Ciò consente sia una maggiore flessibilità sia la possibilità di automatizzare la configurazione di AEM, funzioni che non sono disponibili se si utilizza lo strumento in modalità autonoma.

Per passare da CRX2Oak alla modalità quickstart è necessario definire il percorso della cartella crx-quickstart nella directory di installazione AEM tramite questa variabile ambientale del sistema operativo:

**Per i sistemi basati su UNIX e macOS:**

```shell
export SLING_HOME="/path/to/crx-quickstart"
```

**Per Windows:**

```shell
SET "SLING_HOME=/path/to/crx-quickstart"
```

#### Riprendi supporto {#resume-support}

La migrazione può essere interrotta in qualsiasi momento, con la possibilità di riprenderla successivamente.

#### Logica di aggiornamento personalizzabile {#customizable-upgrade-logic}

Puoi implementare una logica Java personalizzata e anche utilizzando `CommitHooks`. Personalizzato `RepositoryInitializer` è possibile implementare le classi per inizializzare l&#39;archivio con valori personalizzati.

#### Supporto per le operazioni con mappatura della memoria {#support-for-memory-mapped-operations}

CRX2Oak supporta anche le operazioni mappate in memoria per impostazione predefinita. La mappatura della memoria migliora notevolmente le prestazioni e deve essere utilizzata quando possibile.

>[!CAUTION]
>
>Tuttavia, le operazioni mappate in memoria non sono supportate per le piattaforme Windows. Pertanto, si consiglia di aggiungere il **—disable-mmap** quando si esegue la migrazione su Windows.

#### Migrazione selettiva dei contenuti {#selective-migration-of-content}

Per impostazione predefinita, lo strumento esegue la migrazione dell’intero archivio sotto la `"/"` percorso. Tuttavia, hai il controllo completo sul contenuto da migrare.

Se nella nuova istanza è presente una parte del contenuto non necessaria, puoi utilizzare la funzione `--exclude-path` per escludere il contenuto e ottimizzare la procedura di aggiornamento.

#### Unione dei percorsi {#path-merging}

Se i dati devono essere copiati tra due archivi e si dispone di un percorso di contenuto diverso in entrambe le istanze, è possibile definirli nel `--merge-path` parametro . Una volta fatto, CRX2Oak copierà solo i nuovi nodi nell&#39;archivio di destinazione e manterrà quelli vecchi al posto.

![chlimage_1-152](assets/chlimage_1-152.png)

#### Supporto per le versioni {#version-support}

Per impostazione predefinita, AEM creerà una versione di ogni nodo o pagina che viene modificato e la memorizzerà nell&#39;archivio. Le versioni possono quindi essere utilizzate per ripristinare lo stato precedente della pagina.

Tuttavia, queste versioni non vengono mai eliminate anche se la pagina originale viene eliminata. Quando gestisci archivi che sono in funzione da molto tempo, la migrazione potrebbe dover elaborare molti dati ridondanti causati da versioni orfane.

Una caratteristica utile per questi tipi di situazioni è l&#39;aggiunta di `--copy-versions` parametro . Può essere utilizzato per saltare i nodi di versione durante la migrazione o la copia di un archivio.

Puoi anche scegliere se copiare le versioni orfane aggiungendo `--copy-orphaned-versions=true`.

Entrambi i parametri supportano anche un `YYYY-MM-DD` formato data, nel caso in cui si desideri copiare le versioni entro una data specifica.

![chlimage_1-153](assets/chlimage_1-153.png)

#### Open Source Version {#open-source-version}

Una versione open source di CRX2Oak è disponibile sotto forma di oak-upgrade. Supporta tutte le funzioni eccetto:

* Supporto CRX2
* Supporto del profilo di migrazione
* Supporto per la riconfigurazione AEM automatizzata

Consulta la sezione [Documentazione di Apache](https://jackrabbit.apache.org/oak/docs/migration.html) per ulteriori informazioni.

## Parametri {#parameters}

### Opzioni archivio nodi {#node-store-options}

* `--cache`: Dimensione della cache in MB (il valore predefinito è `256`)

* `--mmap`: Abilita l&#39;accesso ai file mappati in memoria per l&#39;archivio segmenti
* `--src-password:` Password per il database RDB di origine

* `--src-user:` Utente per il database RDB di origine

* `--user`: Utente per il RDB di destinazione

* `--password`: Password per il RDB di destinazione.

### Opzioni di migrazione {#migration-options}

* `--early-shutdown`: Chiude l&#39;archivio JCR2 di origine dopo la copia dei nodi e prima che vengano applicati gli hook di commit
* `--fail-on-error`: Forza un errore di migrazione se i nodi non possono essere letti dall&#39;archivio di origine.
* `--ldap`: Esegue la migrazione degli utenti LDAP da un&#39;istanza CQ 5.x a una basata su Oak. Affinché questo funzioni, il provider di identità nella configurazione Oak deve essere denominato ldap. Per ulteriori informazioni, consulta la sezione [Documentazione LDAP](/help/sites-administering/ldap-config.md).

* `--ldap-config:` Utilizza questa funzione in combinazione con `--ldap` parametro per gli archivi CQ 5.x che utilizzavano più server LDAP per l&#39;autenticazione. Puoi usarlo per puntare a CQ 5.x `ldap_login.conf` o `jaas.conf` file di configurazione. Il formato è `--ldapconfig=path/to/ldap_login.conf`.

### Opzioni dell&#39;archivio versioni {#version-store-options}

* `--copy-orphaned-versions`: Ignora la copia delle versioni orfane. I parametri supportati sono: `true`, `false` e `yyyy-mm-dd`. Impostazione predefinita `true`.

* `--copy-versions:` Copia l&#39;archivio delle versioni. Parametri: `true`, `false`, `yyyy-mm-dd`. Impostazione predefinita `true`.

#### Opzioni percorso {#path-options}

* `--include-paths:` Elenco di percorsi da includere durante la copia separati da virgole
* `--merge-paths`: Elenco dei percorsi da unire separati da virgole durante la copia
* `--exclude-paths:` Elenco di percorsi da escludere durante la copia separati da virgole.

### Opzioni archivio BLOB di origine {#source-blob-store-options}

* `--src-datastore:` Directory del datastore da utilizzare come origine `FileDataStore`

* `--src-fileblobstore`: Directory del datastore da utilizzare come origine `FileBlobStore`

* `--src-s3datastore`: Directory del datastore da utilizzare per la sorgente `S3DataStore`

* `--src-s3config`: File di configurazione per l&#39;origine `S3DataStore`.

### Opzioni BlobStore di destinazione {#destination-blobstore-options}

* `--datastore:` Directory del datastore da utilizzare come destinazione `FileDataStore`

* `--fileblobstore:` Directory del datastore da utilizzare come destinazione `FileBlobStore`

* `--s3datastore`: Directory del datastore da utilizzare per la destinazione `S3DataStore`

* `--s3config`: Il file di configurazione per la destinazione `S3DataStore`.

### Opzioni della Guida {#help-options}

* `-?, -h, --help:` Visualizza le informazioni della guida.

## Debugging {#debugging}

È inoltre possibile abilitare le informazioni di debug per il processo di migrazione al fine di risolvere eventuali problemi che potrebbero verificarsi durante il processo. Puoi eseguire questa operazione in modo diverso a seconda della modalità in cui desideri eseguire lo strumento:

<table>
 <tbody>
  <tr>
   <td><strong>Modalità CRX2Oak</strong></td>
   <td><strong>Azione</strong></td>
  </tr>
  <tr>
   <td>Modalità Quickstart</td>
   <td>Puoi aggiungere la <strong>—TRACE a livello di log</strong> o <strong>- DEBUG a livello di log </strong>opzioni alla riga di comando quando si esegue CRX2Oak. In questa modalità i registri vengono automaticamente reindirizzati al <strong>file upgrade.log</strong>.</td>
  </tr>
  <tr>
   <td>Modalità autonoma</td>
   <td><p>Aggiungi il <strong>—trace</strong> opzioni alla riga di comando CRX2Oak per visualizzare gli eventi di TRACE sull'output standard (è necessario reindirizzare i registri manualmente utilizzando il carattere di reindirizzamento: comando '&gt;' o 'tee' per un'ispezione successiva).</p> </td>
  </tr>
 </tbody>
</table>

## Altre considerazioni {#other-considerations}

Durante la migrazione a un set di repliche MongoDB, assicurarsi di impostare la `WriteConcern` parametro a `2` su tutte le connessioni ai database Mongo.

Per eseguire questa operazione, aggiungi la variabile `w=2` alla fine della stringa di connessione, come riportato di seguito:

```xml
java -Xmx4092m -XX:MaxPermSize=1024m -jar crx2oak.jar crx-quickstart/repository/ mongodb://localhost:27017/aem-author?replicaset=replica1&w=2
```

>[!NOTE]
>
>Per ulteriori informazioni, consulta la documentazione sulla stringa di connessione MongoDB in [Scrivi problemi](https://docs.mongodb.org/manual/reference/connection-string/#write-concern-options).
