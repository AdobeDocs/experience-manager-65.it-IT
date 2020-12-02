---
title: Backup e ripristino
seo-title: Backup e ripristino
description: Scoprite come eseguire il backup e ripristinare il contenuto AEM.
seo-description: Scoprite come eseguire il backup e ripristinare il contenuto AEM.
uuid: 446a466f-f508-4430-9e50-42cd4463760e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: eb8bbb85-ca2f-4877-8ee0-bb1ee8b7d8de
translation-type: tm+mt
source-git-commit: 684d2d5f73d571a15c8155e7870134c28dc892b7
workflow-type: tm+mt
source-wordcount: '2295'
ht-degree: 0%

---


# Backup e ripristino{#backup-and-restore}

Esistono due modi per eseguire il backup e ripristinare il contenuto dell&#39;archivio in AEM:

* È possibile creare un backup esterno del repository e archiviarlo in una posizione sicura. Se il repository si rompe, è possibile ripristinarlo allo stato precedente.
* Potete creare versioni interne del contenuto del repository. Queste versioni sono memorizzate nella directory archivio insieme al contenuto, per consentire di ripristinare rapidamente nodi e strutture ad albero modificate o eliminate.

## Generale {#general}

L&#39;approccio descritto si applica al backup e al ripristino del sistema.

Se è necessario eseguire il backup e/o recuperare una piccola quantità di contenuto, che viene persa, non è necessario ripristinare il sistema:

* È possibile recuperare i dati da un altro sistema tramite un pacchetto
* oppure ripristinare il backup su un sistema temporaneo, creare un pacchetto di contenuto e distribuirlo sul sistema, dove manca questo contenuto.

Per informazioni dettagliate, consultate [Backup dei pacchetti](/help/sites-administering/backup-and-restore.md#package-backup) di seguito.

## Tempo {#timing}

Non eseguite il backup in parallelo con la raccolta dei rifiuti del datastore, in quanto potrebbe danneggiare i risultati di entrambi i processi.

## Backup offline {#offline-backup}

È sempre possibile eseguire un backup offline. Ciò richiede un tempo di AEM, ma può essere abbastanza efficiente in termini di tempo richiesto rispetto a un backup online.

Nella maggior parte dei casi, per creare una copia di sola lettura dell&#39;archivio in quel momento si utilizzerà un&#39;istantanea del file system. Per creare un backup offline, effettuare le seguenti operazioni:

* arrestare l&#39;applicazione
* creazione di un backup snapshot
* avviare l&#39;applicazione

Poiché il backup dello snapshot in genere richiede solo pochi secondi, l&#39;intero tempo di inattività è inferiore a pochi minuti.

## Backup online {#online-backup}

Questo metodo di backup crea un backup dell’intero repository, incluse tutte le applicazioni implementate al suo interno, come AEM. Il backup include contenuti, cronologia delle versioni, configurazione, software, hotfix, applicazioni personalizzate, file di registro, indici di ricerca e così via. Se si utilizza il clustering e se la cartella condivisa è una sottodirectory di `crx-quickstart` (fisicamente o utilizzando un softlink), viene eseguito anche il backup della directory condivisa.

È possibile ripristinare l&#39;intero repository (e qualsiasi applicazione) in un momento successivo.

Questo metodo funziona come un backup &quot;a caldo&quot; o &quot;online&quot;, in modo che possa essere eseguito durante l&#39;esecuzione del repository. Pertanto, il repository è utilizzabile durante l&#39;esecuzione del backup. Questo metodo funziona per le istanze di repository predefinite basate su archivio tar.

Durante la creazione di un backup, sono disponibili le seguenti opzioni:

* Backup di una directory tramite AEM strumento di backup integrato.
* Backup di una directory tramite uno snapshot del file system

In ogni caso, il backup crea un&#39;immagine (o istantanea) del repository. L&#39;agente di backup dei sistemi deve quindi provvedere a trasferire l&#39;immagine a un sistema di backup dedicato (unità a nastro).

>[!NOTE]
>
>Se AEM funzione di backup online viene utilizzata in un&#39;istanza AEM con una configurazione di blobstore personalizzata, si consiglia di configurare il percorso del datastore in modo che si trovi all&#39;esterno della directory &quot; `crx-quickstart`&quot; e di eseguire il backup del datastore separatamente.

>[!CAUTION]
>
>Il backup online esegue solo il backup del file system. Se archiviate il contenuto del repository e/o i file del repository in un database, è necessario eseguire il backup del database separatamente. Se utilizzate AEM con MongoDB, consultate la documentazione sull&#39;utilizzo degli [strumenti di backup nativi MongoDB](https://docs.mongodb.org/manual/tutorial/backup-with-mongodump/).

### AEM Backup online {#aem-online-backup}

Un backup online del repository consente di creare, scaricare ed eliminare i file di backup. Si tratta di una funzione di backup &quot;hot&quot; o &quot;online&quot;, che può essere eseguita mentre il repository viene utilizzato normalmente in modalità di lettura/scrittura.

>[!CAUTION]
>
>Non eseguite AEM backup online in modo simultaneo con [DataStore Garbage Collection](/help/sites-administering/data-store-garbage-collection.md) o [Revision Cleanup](/help/sites-deploying/revision-cleanup.md#how-to-run-offline-revision-cleanup). Ciò influirà negativamente sulle prestazioni del sistema.

Quando si avvia un backup è possibile specificare un **percorso di destinazione** e/o un **ritardo**.

**Target** PathI file di backup vengono in genere salvati nella cartella principale della cartella contenente il file jar di avvio rapido (.jar). Ad esempio, se il file AEM jar si trova in /InstallationKits/AEM, il backup verrà generato in /InstallationKits. Potete anche specificare una destinazione in una posizione di vostra scelta.

Se **TargetPath** è una directory, l&#39;immagine del repository viene creata in questa directory. Se la stessa directory viene utilizzata più volte (o sempre) per memorizzare il backup,

* i file modificati nell&#39;archivio vengono modificati di conseguenza in TargetPath
* i file eliminati nell&#39;archivio vengono eliminati in TargetPath
* i file creati nell&#39;archivio vengono creati in TargetPath

>[!NOTE]
>
>Se **TargetPath** è impostato su nomefile con l&#39;estensione **.zip**, il repository viene sottoposto a backup in una directory temporanea e il contenuto di questa directory temporanea viene compresso e memorizzato nel file ZIP.
>
>Questo approccio è scoraggiato, perché
>
>* durante il processo di backup è necessario ulteriore storage su disco (directory temporanea più il file zip)
>* il processo di compressione viene eseguito dall&#39;archivio e potrebbe influenzarne le prestazioni.
>* Il processo di backup viene ritardato.
>* Fino a Java 1.6 Java è in grado di creare file ZIP fino a 4 gigabyte.

>
>
Se è necessario creare un ZIP come formato di backup, è necessario eseguire il backup in una directory e quindi utilizzare un programma di compressione per creare il file zip.

**** Ritardo: indica un ritardo (in millisecondi), in modo che le prestazioni del repository non vengano alterate. Per impostazione predefinita, il backup del repository viene eseguito a tutta velocità. È possibile rallentare la creazione di un backup online, in modo da non rallentare altre attività.

Quando si utilizza un ritardo molto elevato, assicurarsi che il backup online non richieda più di 24 ore. In caso affermativo, scartare il backup, in quanto non può contenere tutti i file binari.
Un ritardo di 1 millisecondo genera in genere un utilizzo della CPU pari al 10% e un ritardo di 10 millisecondi in genere riduce l’utilizzo della CPU al 3%. Il ritardo totale in secondi può essere stimato come segue: Dimensione del repository in MB, moltiplicata per il ritardo in millisecondi, divisa per 2 (se si utilizza l&#39;opzione zip), o divisa per 4 (quando si esegue il backup su una directory). Ciò significa che un backup in una directory di un repository da 200 MB con un ritardo di 1 ms aumenta il tempo di backup di circa 50 secondi.

>[!NOTE]
>
>Per informazioni dettagliate sul processo, vedere [Funzionamento AEM backup online](#how-aem-online-backup-works).

Per creare un backup:

1. Accedete per AEM come amministratore.

1. Vai a **Strumenti - Operazioni - Backup.**
1. Fai clic su **Crea**. Viene aperta la console di backup.

   ![chlimage_1-1](assets/chlimage_1-1a.png)

1. Nella console di backup, specificate i **[Percorso di destinazione](#aem-online-backup)** e **[Ritardo](#aem-online-backup)**.

   ![chlimage_1-2](assets/chlimage_1-2a.png)

   >[!NOTE]
   >
   >La console di backup è disponibile anche tramite:
   >
   >
   >` https://<*hostname*>:<*port-number*>/libs/granite/backup/content/admin.html`

1. Fare clic su **Salva**, una barra di avanzamento indicherà l&#39;avanzamento del backup.

   >[!NOTE]
   >
   >È possibile **annullare** un backup in esecuzione in qualsiasi momento.

1. Una volta completato il backup, i file zip sono elencati nella finestra di backup.

   ![chlimage_1-3](assets/chlimage_1-3a.png)

   >[!NOTE]
   >
   >I file di backup non più necessari possono essere rimossi utilizzando la console. Selezionare il file di backup nel riquadro a sinistra, quindi fare clic su **Elimina**.

   >[!NOTE]
   >
   >Se avete eseguito il backup in una directory: al termine del processo di backup, AEM non scriverà nella directory di destinazione.

### Automazione AEM backup online {#automating-aem-online-backup}

Se possibile, il backup online dovrebbe essere eseguito quando il carico sul sistema è limitato, ad esempio la mattina.

I backup possono essere automatizzati utilizzando i client `wget` o `curl` HTTP. Di seguito sono riportati alcuni esempi di automazione del backup tramite curl.

#### Backup della directory di destinazione predefinita {#backing-up-to-the-default-target-directory}

>[!CAUTION]
>
>Nell&#39;esempio seguente potrebbero essere necessari diversi parametri nel comando `curl` per l&#39;istanza; ad esempio, il nome host ( `localhost`), la porta ( `4502`), la password amministratore ( `xyz`) e il nome del file ( `backup.zip`).

```shell
curl -u admin:admin -X POST http://localhost:4502/system/console/jmx/com.adobe.granite:type=Repository/op/startBackup/java.lang.String?target=backup.zip
```

Il file/directory di backup viene creato sul server nella cartella principale della cartella contenente la cartella `crx-quickstart` (come se si stesse creando il backup utilizzando il browser). Ad esempio, se AEM installato nella directory `/InstallationKits/crx-quickstart/`, il backup viene creato nella directory `/InstallationKits`.

Il comando curl ritorna immediatamente, quindi è necessario monitorare questa directory per vedere quando il file zip è pronto. Mentre il backup viene creato una directory temporanea (con il nome basato su quello del file zip finale) può essere visto, alla fine verrà compresso. Esempio:

* nome del file ZIP risultante: `backup.zip`
* nome della directory temporanea: `backup.f4d5.temp`

#### Backup di una directory di destinazione non predefinita {#backing-up-to-a-non-default-target-directory}

Solitamente il file/directory di backup viene creato sul server nella cartella principale della cartella contenente la cartella `crx-quickstart`.

Se si desidera salvare il backup (di entrambi gli ordini) in una posizione diversa, è possibile impostare un percorso assoluto &quot;al parametro `target` nel comando `curl`.

Ad esempio, per generare `backupJune.zip` nella directory `/Backups/2012`:

```shell
curl -u admin:admin -X POST http://localhost:4502/system/console/jmx/com.adobe.granite:type=Repository/op/startBackup/java.lang.String?target=/Backups/2012/backupJune.zip"
```

>[!CAUTION]
>
>Quando si utilizza un server applicazione diverso (ad esempio JBoss), il backup online potrebbe non funzionare come previsto, perché la directory di destinazione non è scrivibile. In questo caso, contattate l&#39;Assistenza.

>[!NOTE]
>
>È inoltre possibile attivare un backup [utilizzando gli MBeans forniti da AEM](/help/sites-administering/jmx-console.md).

### Backup snapshot del file system {#filesystem-snapshot-backup}

Il processo qui descritto è particolarmente adatto per grandi archivi.

>[!NOTE]
>
>Se si desidera utilizzare questo approccio di backup, il sistema deve supportare snapshot del file system. Ad esempio, per Linux questo significa che i file system devono essere inseriti su un volume logico.

1. Eseguite un&#39;istantanea del AEM del file system in cui è distribuita.

1. Montare lo snapshot del file system.
1. Eseguire un backup e smontare lo snapshot.

### Come funziona AEM backup online {#how-aem-online-backup-works}

AEM Backup online è costituito da una serie di azioni interne per garantire l&#39;integrità dei dati sottoposti a backup e dei file di backup creati. Questi sono elencati di seguito per gli interessati.

Il backup online utilizza il seguente algoritmo:

1. Quando create un file zip, il primo passaggio consiste nel creare o individuare la directory di destinazione.

   * Se viene eseguito il backup su un file zip, viene creata una directory temporanea. Il nome della directory inizia con `backup.` e termina con `.temp`; ad esempio `backup.f4d3.temp`.
   * Se viene eseguito il backup in una directory, viene utilizzato il nome specificato nel percorso di destinazione. È possibile utilizzare una directory esistente. In caso contrario verrà creata una nuova directory.

      Un file vuoto denominato `backupInProgress.txt` viene creato nella directory di destinazione all&#39;avvio del backup. Questo file viene eliminato al termine del backup.

1. I file vengono copiati dalla directory di origine alla directory di destinazione (o alla directory temporanea al momento della creazione di un file zip). L&#39;archivio segmenti viene copiato prima dell&#39;archivio dati per evitare il danneggiamento dell&#39;archivio. I dati di indice e cache vengono omessi durante la creazione del backup. Di conseguenza, i dati di `crx-quickstart/repository/cache` e `crx-quickstart/repository/index` non sono inclusi nel backup. L&#39;indicatore della barra di avanzamento del processo è compreso tra 0% e 70% durante la creazione di un file ZIP, oppure tra 0% e 100% se non viene creato alcun file ZIP.

1. Se il backup viene eseguito su una directory preesistente, i file &quot;vecchi&quot; nella directory di destinazione vengono eliminati. I file precedenti sono file che non esistono nella directory di origine.

I file vengono copiati nella directory di destinazione in quattro fasi:

1. Nella prima fase di copia (indicatore di avanzamento 0% - 63% quando si crea un file ZIP oppure 0% - 90% se non viene creato alcun file ZIP), tutti i file vengono copiati mentre l&#39;archivio è in esecuzione normalmente. Il processo prevede due fasi:

   * Fase A: tutto viene copiato tranne il datastore (con ritardo).
   * Fase B: viene copiato solo il datastore (con ritardo).

1. Nella seconda fase di copia (indicatore di avanzamento 63% - 65,8% quando si crea un file ZIP o 90% - 94% se non viene creato alcun file ZIP) vengono copiati solo i file creati o modificati nella directory di origine dall’avvio della prima fase di copia. A seconda dell’attività dell’archivio, questo può variare da nessun file, fino a un numero significativo di file (in genere la prima fase di copia del file richiede molto tempo). Il processo di copia è simile alla prima fase (fase A e fase B con ritardo).
1. Nella terza fase di copia (indicatore di avanzamento 65,8% - 68,6% quando si crea un file ZIP o 94% - 98% se non viene creato alcun file ZIP) vengono copiati solo i file creati o modificati nella directory di origine dall’avvio della seconda fase di copia. A seconda dell’attività dell’archivio, potrebbe non esserci alcun file da copiare o un numero molto ridotto di file (in quanto la seconda fase di copia del file è in genere rapida). Il processo di copia è simile alla seconda fase - fase A e fase B, ma senza ritardo.
1. Le fasi di copia dei file da uno a tre vengono tutte eseguite contemporaneamente mentre la directory archivio è in esecuzione. Vengono copiati solo i file creati o modificati nella directory di origine dall’avvio della terza fase di copia. A seconda dell&#39;attività del repository, potrebbe non esserci alcun file da copiare, o un numero molto, molto limitato di file (perché la seconda fase di copia del file è in genere molto veloce). Indicatore di avanzamento 68,6% - 70% quando si crea un file ZIP o 98% - 100% se non viene creato alcun file ZIP. Il processo di copia è simile alla terza fase.
1. A seconda della destinazione:

   * Se è stato specificato un file zip, ora viene creato dalla directory temporanea. Indicatore di progresso 70% - 100%. La directory temporanea viene quindi eliminata.
   * Se la destinazione era una directory, il file vuoto denominato `backupInProgress.txt` viene eliminato per indicare che il backup è terminato.

## Ripristino del backup {#restoring-the-backup}

È possibile ripristinare un backup come segue:

* Nel caso in cui si esegua un backup delle snapshot del file system, è possibile ripristinare semplicemente un&#39;immagine del sistema.
* Se avete creato il backup come file zip, decomprimete il contenuto in una nuova cartella e iniziate a AEM da tale posizione.

## Backup pacchetto {#package-backup}

Per eseguire il backup e ripristinare il contenuto, potete utilizzare uno dei servizi di gestione pacchetti, che utilizza il formato Pacchetto contenuti per eseguire il backup e il ripristino del contenuto. Gestione pacchetti offre maggiore flessibilità nella definizione e gestione dei pacchetti.

Per informazioni dettagliate sulle caratteristiche e sulle compensazioni di ciascuno di questi formati di pacchetto di contenuti, consultate [Come lavorare con i pacchetti](/help/sites-administering/package-manager.md).

### Ambito del backup {#scope-of-backup}

Quando eseguite il backup dei nodi utilizzando Gestione pacchetti o Content Zipper, CRX salva le informazioni seguenti:

* Contenuto del repository sotto la struttura selezionata.
* Definizioni dei tipi di nodo utilizzate per il contenuto di cui eseguite il backup.
* Definizioni dello spazio dei nomi utilizzate per il contenuto di cui eseguite il backup.

Durante il backup, AEM perde le seguenti informazioni:

* Cronologia delle versioni.

