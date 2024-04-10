---
title: Utilizzo dello strumento di migrazione CRX2Oak
description: Scopri come utilizzare lo strumento di migrazione CRX2Oak con Adobe Experience Manager. Lo strumento è progettato per facilitare la migrazione dei dati tra archivi diversi.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
feature: Upgrading
exl-id: ef3895b9-8d35-4881-8188-c864ae3f0b4c
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '1175'
ht-degree: 0%

---

# Utilizzo dello strumento di migrazione CRX2Oak{#using-the-crx-oak-migration-tool}

## Introduzione {#introduction}

CRX2Oak è uno strumento progettato per eseguire la migrazione dei dati tra archivi diversi.

Può essere utilizzato per migrare i dati dalle versioni precedenti di CQ basate su Apache Jackrabbit 2 a Oak e può anche essere utilizzato per copiare i dati tra archivi Oak.

Puoi scaricare la versione più recente di crx2oak dall’archivio di Adobi pubblico da questa posizione:
[https://repo1.maven.org/maven2/com/adobe/granite/crx2oak/](https://repo1.maven.org/maven2/com/adobe/granite/crx2oak/)

>[!NOTE]
>
>Per ulteriori informazioni su Apache Oak e sui concetti chiave della persistenza di Adobe Experience Manager (AEM), consulta [Introduzione alla piattaforma AEM](/help/sites-deploying/platform.md).

## Casi di utilizzo della migrazione {#migration-use-cases}

Lo strumento può essere utilizzato per:

* Migrazione dalle versioni precedenti di CQ 5 all’AEM 6
* Copia dei dati tra più archivi Oak
* Conversione di dati tra diverse implementazioni Oak MicroKernel.

Il supporto per la migrazione degli archivi tramite archivi BLOB esterni (comunemente noti come archivi dati) è fornito in diverse combinazioni. Un possibile percorso di migrazione proviene da un archivio CRX2 che utilizza un archivio esterno `FileDataStore` in un archivio Oak utilizzando un `S3DataStore`.

Il diagramma seguente illustra tutte le possibili combinazioni di migrazione supportate da CRX2Oak:

![chlimage_1-151](assets/chlimage_1-151.png)

## Funzioni {#features}

CRX2Oak viene chiamato durante gli aggiornamenti AEM in modo tale che l’utente possa specificare un profilo di migrazione predefinito che automatizza la riconfigurazione delle modalità di persistenza. Questa modalità è denominata modalità di avvio rapido.

Può anche essere eseguito separatamente nel caso richieda una maggiore personalizzazione. Tuttavia, in questa modalità le modifiche vengono apportate solo all’archivio e ogni ulteriore riconfigurazione dell’AEM deve essere eseguita manualmente. Questa modalità è denominata standalone.

Un altro aspetto da notare è che con le impostazioni predefinite in modalità standalone, viene eseguita la migrazione solo dell’archivio dei nodi e il nuovo archivio riutilizza il vecchio archivio binario.

### Modalità QuickStart automatizzata {#automated-quickstart-mode}

Da AEM 6.3, CRX2Oak è in grado di gestire profili di migrazione definiti dall’utente che possono essere configurati con tutte le opzioni di migrazione già disponibili. Ciò consente sia una maggiore flessibilità sia la possibilità di automatizzare la configurazione di AEM, funzioni che non sono disponibili se si utilizza lo strumento in modalità autonoma.

Per passare da CRX2Oak alla modalità quickstart, definire il percorso della cartella crx-quickstart nella directory di installazione dell&#39;AEM tramite questa variabile di ambiente del sistema operativo:

**Per i sistemi basati su UNIX e macOS:**

```shell
export SLING_HOME="/path/to/crx-quickstart"
```

**Per Windows:**

```shell
SET "SLING_HOME=/path/to/crx-quickstart"
```

#### Riprendi supporto {#resume-support}

La migrazione può essere interrotta in qualsiasi momento, con la possibilità di riprenderla in seguito.

#### Logica di aggiornamento personalizzabile {#customizable-upgrade-logic}

La logica Java™ personalizzata può essere implementata utilizzando `CommitHooks`. Personalizzato `RepositoryInitializer` Le classi possono essere implementate per inizializzare l&#39;archivio con valori personalizzati.

#### Supporto per operazioni con mapping della memoria {#support-for-memory-mapped-operations}

Per impostazione predefinita, CRX2Oak supporta anche operazioni mappate sulla memoria. La mappatura della memoria migliora notevolmente le prestazioni e deve essere utilizzata quando possibile.

>[!CAUTION]
>
>Si noti tuttavia che le operazioni mappate alla memoria non sono supportate per le piattaforme Windows. Pertanto, si consiglia di aggiungere **—disable-mmap** durante l&#39;esecuzione della migrazione su Windows.

#### Migrazione selettiva dei contenuti {#selective-migration-of-content}

Per impostazione predefinita, lo strumento migra l’intero archivio sotto il `"/"` percorso. Tuttavia, hai il controllo completo sul contenuto da migrare.

Se una parte del contenuto non è richiesta nella nuova istanza, puoi utilizzare `--exclude-path` per escludere il contenuto e ottimizzare la procedura di aggiornamento.

#### Unione percorsi {#path-merging}

Se i dati devono essere copiati tra due archivi e disponi di un percorso di contenuto diverso in entrambe le istanze, puoi definirlo in `--merge-path` parametro. In questo caso, CRX2Oak copia solo i nuovi nodi nell’archivio di destinazione e mantiene i vecchi nodi in posizione.

![chlimage_1-152](assets/chlimage_1-152.png)

#### Supporto versione {#version-support}

Per impostazione predefinita, l’AEM crea una versione di ogni nodo o pagina che viene modificata e la memorizza nell’archivio. Le versioni possono quindi essere utilizzate per ripristinare uno stato precedente della pagina.

Tuttavia, queste versioni non vengono mai eliminate anche se la pagina originale viene eliminata. Quando si gestiscono archivi che sono in funzione da molto tempo, la migrazione può rielaborare i dati ridondanti causati da versioni orfane.

Una caratteristica utile per questi tipi di situazioni è l&#39;aggiunta della `--copy-versions` parametro. Può essere utilizzato per saltare i nodi di versione durante la migrazione o la copia di un archivio.

Puoi anche scegliere se copiare le versioni orfane aggiungendo `--copy-orphaned-versions=true`.

Entrambi i parametri supportano anche una `YYYY-MM-DD` formato data, per copiare le versioni non oltre una data specifica.

![chlimage_1-153](assets/chlimage_1-153.png)

#### Apri versione sorgente {#open-source-version}

È disponibile una versione open-source di CRX2Oak sotto forma di oak-upgrade. Supporta tutte le funzioni ad eccezione di:

* Supporto CRX2
* Supporto del profilo di migrazione
* Supporto per la riconfigurazione automatica dell’AEM

Consulta la [Documentazione di Apache](https://jackrabbit.apache.org/oak/docs/migration.html) per ulteriori informazioni.

## Parametri {#parameters}

### Opzioni archivio nodi {#node-store-options}

* `--cache`: dimensione della cache in MB (il valore predefinito è `256`)

* `--mmap`: abilita l’accesso ai file mappati in memoria per l’archivio segmenti
* `--src-password:` Password per il database RDB di origine

* `--src-user:` Utente per RDB di origine

* `--user`: utente per RDB di destinazione

* `--password`: password per l’RDB di destinazione.

### Opzioni di migrazione {#migration-options}

* `--early-shutdown`: chiude l’archivio JCR2 di origine dopo la copia dei nodi e prima dell’applicazione degli hook di commit
* `--fail-on-error`: forza un errore della migrazione se i nodi non possono essere letti dall’archivio di origine.
* `--ldap`: esegue la migrazione degli utenti LDAP da un’istanza CQ 5.x a una basata su Oak. Affinché ciò funzioni, il provider di identità nella configurazione Oak deve essere denominato ldap. Per ulteriori informazioni, vedere [Documentazione LDAP](/help/sites-administering/ldap-config.md).

* `--ldap-config:` Utilizzalo con il `--ldap` parametro per gli archivi CQ 5.x che utilizzavano più server LDAP per l’autenticazione. Puoi utilizzarlo per puntare a CQ 5.x `ldap_login.conf` o `jaas.conf` file di configurazione. Il formato è `--ldapconfig=path/to/ldap_login.conf`.

### Opzioni archivio versioni {#version-store-options}

* `--copy-orphaned-versions`: non copia le versioni orfane. I parametri supportati sono: `true`, `false`, e `yyyy-mm-dd`. Impostazione predefinita `true`.

* `--copy-versions:` Copia l’archiviazione della versione. Parametri: `true`, `false`, `yyyy-mm-dd`. Impostazione predefinita `true`.

#### Opzioni percorso {#path-options}

* `--include-paths:` Elenco di percorsi separato da virgole da includere durante la copia
* `--merge-paths`: elenco di percorsi separato da virgole da unire durante la copia
* `--exclude-paths:` Elenco separato da virgole dei percorsi da escludere durante la copia.

### Opzioni archivio BLOB di origine {#source-blob-store-options}

* `--src-datastore:` Directory dell’archivio dati da utilizzare come origine `FileDataStore`

* `--src-fileblobstore`: directory dell’archivio dati da utilizzare come origine `FileBlobStore`

* `--src-s3datastore`: directory dell’archivio dati da utilizzare per l’origine `S3DataStore`

* `--src-s3config`: file di configurazione per l’origine `S3DataStore`.

### Opzioni BlobStore di destinazione {#destination-blobstore-options}

* `--datastore:` Directory dell’archivio dati da utilizzare come destinazione `FileDataStore`

* `--fileblobstore:` Directory dell’archivio dati da utilizzare come destinazione `FileBlobStore`

* `--s3datastore`: directory dell’archivio dati da utilizzare per la destinazione `S3DataStore`

* `--s3config`: file di configurazione per la destinazione `S3DataStore`.

### Opzioni della Guida {#help-options}

* `-?, -h, --help:` Visualizza informazioni della Guida.

## Debugging {#debugging}

È inoltre possibile abilitare le informazioni di debug per il processo di migrazione per la risoluzione dei problemi che potrebbero verificarsi durante il processo. È possibile eseguire questa operazione in modo diverso a seconda della modalità in cui si desidera eseguire lo strumento:

<table>
 <tbody>
  <tr>
   <td><strong>Modalità CRX2Oak</strong></td>
   <td><strong>Azione</strong></td>
  </tr>
  <tr>
   <td>Modalità Quickstart</td>
   <td>È possibile aggiungere <strong>—log-level TRACE</strong> o <strong>- DEBUG a livello di log </strong>opzioni della riga di comando quando si esegue CRX2Oak. In questa modalità, i registri vengono reindirizzati automaticamente al <strong>file upgrade.log</strong>.</td>
  </tr>
  <tr>
   <td>Modalità autonoma</td>
   <td><p>Aggiungi il <strong>- traccia</strong> opzioni della riga di comando CRX2Oak per visualizzare gli eventi TRACE sull'output standard (è necessario reindirizzare i registri utilizzando il carattere di reindirizzamento: '&gt;' o il comando 'tee' per un'ispezione successiva).</p> </td>
  </tr>
 </tbody>
</table>

## Altre considerazioni {#other-considerations}

Durante la migrazione a un set di repliche MongoDB, assicurarsi di impostare `WriteConcern` parametro a `2` su tutte le connessioni alle banche dati Mongo.

Per farlo, aggiungi il `w=2` alla fine della stringa di connessione, come segue:

```xml
java -Xmx4092m -jar crx2oak.jar crx-quickstart/repository/ mongodb://localhost:27017/aem-author?replicaset=replica1&w=2
```

>[!NOTE]
>
>Per ulteriori informazioni, consulta la documentazione sulle stringhe di connessione MongoDB su [Scrivi dubbi](https://docs.mongodb.org/manual/reference/connection-string/#write-concern-options).
