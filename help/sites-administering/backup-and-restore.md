---
title: Backup e ripristino
seo-title: Backup and Restore
description: Scopri come eseguire il backup e il ripristino del contenuto AEM.
seo-description: Learn how to backup and restore your AEM content.
uuid: 446a466f-f508-4430-9e50-42cd4463760e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: eb8bbb85-ca2f-4877-8ee0-bb1ee8b7d8de
exl-id: dd26dade-b769-483e-bc11-dcfa5ed1f87e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2283'
ht-degree: 0%

---

# Backup e ripristino{#backup-and-restore}

Esistono due modi per eseguire il backup e ripristinare il contenuto dell’archivio in AEM:

* È possibile creare un backup esterno dell&#39;archivio e archiviarlo in una posizione sicura. Se l’archivio si suddivide, puoi ripristinarlo allo stato precedente.
* Puoi creare versioni interne del contenuto dell’archivio. Queste versioni sono memorizzate nell&#39;archivio insieme al contenuto, in modo da poter ripristinare rapidamente nodi e alberi modificati o eliminati.

## Generale {#general}

L&#39;approccio descritto si applica al backup e al ripristino del sistema.

Se è necessario eseguire il backup e/o il ripristino di una piccola quantità di contenuto, che viene persa, non è necessario un ripristino del sistema:

* Puoi recuperare i dati da un altro sistema tramite un pacchetto
* oppure ripristinare il backup su un sistema temporaneo, creare un pacchetto di contenuti e distribuirlo sul sistema, dove manca questo contenuto.

Per maggiori dettagli, vedi [Backup dei pacchetti](/help/sites-administering/backup-and-restore.md#package-backup) sotto.

## Tempi {#timing}

Non eseguire il backup in parallelo con la Garbage Collection del datastore, in quanto potrebbe danneggiare i risultati di entrambi i processi.

## Backup offline {#offline-backup}

Puoi sempre eseguire un backup offline. Questo richiede un tempo di AEM, ma può essere abbastanza efficiente in termini di tempo richiesto rispetto a un backup online.

Nella maggior parte dei casi, per creare una copia di sola lettura dell&#39;archivio in quel momento, verrà utilizzata un&#39;istantanea del file system. Per creare un backup offline, esegui questi passaggi:

* interrompe l&#39;applicazione
* creare un backup snapshot
* avviare l&#39;applicazione

Poiché il backup dello snapshot richiede in genere solo pochi secondi, l&#39;intero downtime è inferiore a pochi minuti.

## Backup online {#online-backup}

Questo metodo di backup crea un backup dell&#39;intero archivio, incluse tutte le applicazioni distribuite al suo interno, ad esempio AEM. Il backup include contenuti, cronologia delle versioni, configurazione, software, hotfix, applicazioni personalizzate, file di registro, indici di ricerca e così via. Se utilizzi il clustering e se la cartella condivisa è una sottodirectory di `crx-quickstart` (fisicamente o utilizzando un collegamento software), viene eseguito anche il backup della directory condivisa.

Puoi ripristinare l’intero archivio (e qualsiasi applicazione) in un momento successivo.

Questo metodo funziona come backup &quot;a caldo&quot; o &quot;online&quot; in modo che possa essere eseguito mentre l&#39;archivio è in esecuzione. Pertanto l&#39;archivio è utilizzabile durante l&#39;esecuzione del backup. Questo metodo funziona per le istanze dell&#39;archivio Tar predefinite basate su archiviazione.

Quando crei un backup, hai le seguenti opzioni:

* Eseguire il backup di una directory utilizzando AEM strumento di backup integrato.
* Backup di una directory tramite un’istantanea del file system

In ogni caso, il backup crea un&#39;immagine (o un&#39;istantanea) dell&#39;archivio. Quindi l&#39;agente di backup dei sistemi dovrebbe fare attenzione a trasferire questa immagine a un sistema di backup dedicato (unità a nastro).

>[!NOTE]
>
>Se AEM funzione di backup online viene utilizzata in un&#39;istanza AEM con una configurazione di blobstore personalizzata, si consiglia di configurare il percorso dell&#39;archivio dati in modo che sia all&#39;esterno del &quot; `crx-quickstart`&quot; directory e backup del datastore separatamente.

>[!CAUTION]
>
>Il backup online esegue solo il backup del file system. Se si memorizzano il contenuto del repository e/o i file del repository in un database, è necessario eseguire il backup separatamente. Se utilizzi AEM con MongoDB, consulta la documentazione su come utilizzare il [Strumenti di backup nativi MongoDB](https://docs.mongodb.org/manual/tutorial/backup-with-mongodump/).

### Backup online AEM {#aem-online-backup}

Un backup online dell&#39;archivio consente di creare, scaricare ed eliminare file di backup. Si tratta di una funzione di backup &quot;hot&quot; o &quot;online&quot;, quindi può essere eseguita mentre l&#39;archivio viene utilizzato normalmente in modalità di lettura-scrittura.

>[!CAUTION]
>
>Non eseguire AEM backup online contemporaneamente con [Raccolta rifiuti di Datastore](/help/sites-administering/data-store-garbage-collection.md) o [Pulizia revisioni](/help/sites-deploying/revision-cleanup.md#how-to-run-offline-revision-cleanup). Influirà negativamente sulle prestazioni del sistema.

Quando si avvia un backup è possibile specificare un **Percorso di Target** e/o a **Ritardo**.

**Percorso di Target** I file di backup vengono generalmente salvati nella cartella padre della cartella che contiene il file jar quickstart (.jar). Ad esempio, se il file jar AEM si trova in /InstallationKits/AEM, il backup verrà generato in /InstallationKits. Puoi anche specificare un target per una posizione di tua scelta.

Se la **TargetPath** è una directory, l&#39;immagine dell&#39;archivio viene creata in questa directory. Se la stessa directory viene utilizzata più volte (o sempre) per memorizzare il backup,

* I file modificati nell&#39;archivio vengono modificati di conseguenza in TargetPath
* I file eliminati nel repository vengono eliminati in TargetPath
* i file creati nell&#39;archivio vengono creati in TargetPath

>[!NOTE]
>
>Se **TargetPath** è impostato su nomefile con estensione **.zip**, il repository viene sottoposto a backup in una directory temporanea e il contenuto di questa directory temporanea viene compresso e memorizzato nel file ZIP.
>
>Questo approccio è scoraggiato, perché
>
>* richiede ulteriore archiviazione su disco durante il processo di backup (directory temporanea più il file zip)
>* il processo di compressione viene eseguito dall&#39;archivio e potrebbe influire sulle sue prestazioni.
>* Ritarda il processo di backup.
>* Fino a Java 1.6 Java è in grado di creare file ZIP fino a una dimensione di 4 gigabyte.
>
>Se devi creare un file ZIP come formato di backup, devi eseguire il backup in una directory e quindi utilizzare un programma di compressione per creare il file zip.

**Ritardo** Indica un ritardo (in millisecondi), in modo che le prestazioni del repository non vengano influenzate. Per impostazione predefinita, il backup dell&#39;archivio viene eseguito a piena velocità. È possibile rallentare la creazione di un backup online in modo che non rallenti altre attività.

Quando utilizzi un ritardo molto elevato, assicurati che il backup online non richieda più di 24 ore. Se lo ha fatto, scarta questo backup, in quanto potrebbe non contenere tutti i binari.
Un ritardo di 1 millisecondo in genere si traduce in un utilizzo della CPU del 10% e un ritardo di 10 millisecondi di solito si traduce in meno del 3% dell&#39;utilizzo della CPU. Il ritardo totale in secondi può essere stimato come segue: Dimensione del repository in MB, moltiplicata per il ritardo in millisecondi, divisa per 2 (se si utilizza l&#39;opzione zip), o divisa per 4 (quando si esegue il backup su una directory). Ciò significa che un backup su una directory di un archivio da 200 MB con un ritardo di 1 ms aumenta il tempo di backup di circa 50 secondi.

>[!NOTE]
>
>Vedi [Come funziona AEM backup online](#how-aem-online-backup-works) per informazioni interne sul processo.

Per creare un backup:

1. Accedi a AEM come amministratore.

1. Vai a **Strumenti - Operazioni - Backup.**
1. Fai clic su **Crea**. Viene aperta la console di backup.

   ![chlimage_1-1](assets/chlimage_1-1a.png)

1. Nella console di backup, specifica l’ **[Percorso di Target](#aem-online-backup)** e **[Ritardo](#aem-online-backup)**.

   ![chlimage_1-2](assets/chlimage_1-2a.png)

   >[!NOTE]
   >
   >La console di backup è disponibile anche utilizzando:
   >
   >
   >` https://<*hostname*>:<*port-number*>/libs/granite/backup/content/admin.html`

1. Fai clic su **Salva**, una barra di avanzamento indicherà l’avanzamento del backup.

   >[!NOTE]
   >
   >È possibile **Annulla** un backup in esecuzione in qualsiasi momento.

1. Una volta completato il backup, i file zip vengono elencati nella finestra di backup.

   ![chlimage_1-3](assets/chlimage_1-3a.png)

   >[!NOTE]
   >
   >I file di backup non più necessari possono essere rimossi tramite la console. Selezionare il file di backup nel riquadro a sinistra, quindi fare clic su **Elimina**.

   >[!NOTE]
   >
   >Se hai eseguito il backup su una directory: al termine del processo di backup, AEM non scriverà nella directory di destinazione.

### Automazione AEM backup online {#automating-aem-online-backup}

Se possibile, il backup online deve essere eseguito quando il sistema non è caricato, ad esempio la mattina.

I backup possono essere automatizzati utilizzando `wget` o `curl` Client HTTP. Di seguito sono riportati alcuni esempi di come automatizzare il backup utilizzando curl.

#### Backup della directory di Target predefinita {#backing-up-to-the-default-target-directory}

>[!CAUTION]
>
>Nell’esempio seguente, vari parametri nel `curl` potrebbe essere necessario configurare il comando per la tua istanza; ad esempio, il nome host ( `localhost`), porta ( `4502`), password amministratore ( `xyz`) e il nome del file ( `backup.zip`).

```shell
curl -u admin:admin -X POST http://localhost:4502/system/console/jmx/com.adobe.granite:type=Repository/op/startBackup/java.lang.String?target=backup.zip
```

Il file/directory di backup viene creato sul server nella cartella padre della cartella contenente il `crx-quickstart` come se si stesse creando il backup utilizzando il browser. Ad esempio, se hai installato AEM nella directory `/InstallationKits/crx-quickstart/`, quindi il backup viene creato nel `/InstallationKits` directory.

Il comando curl ritorna immediatamente, quindi è necessario monitorare questa directory per vedere quando il file zip è pronto. Mentre il backup viene creato una directory temporanea (con il nome basato su quello del file zip finale) può essere visto, alla fine sarà compresso. Esempio:

* nome del file zip risultante: `backup.zip`
* nome della directory temporanea: `backup.f4d5.temp`

#### Backup di una directory di Target non predefinita {#backing-up-to-a-non-default-target-directory}

Di solito il file/directory di backup viene creato sul server nella cartella padre della cartella contenente il `crx-quickstart` cartella.

Se desideri salvare il backup (di entrambi gli ordini) in una posizione diversa, puoi impostare un percorso assoluto &quot;al `target` nel `curl` comando.

Ad esempio, per generare `backupJune.zip` nella directory `/Backups/2012`:

```shell
curl -u admin:admin -X POST http://localhost:4502/system/console/jmx/com.adobe.granite:type=Repository/op/startBackup/java.lang.String?target=/Backups/2012/backupJune.zip"
```

>[!CAUTION]
>
>Quando si utilizza un server applicativo diverso (come JBoss), il backup online potrebbe non funzionare come previsto, perché la directory di destinazione non è scrivibile. In questo caso, contatta il supporto.

>[!NOTE]
>
>È inoltre possibile attivare un backup [utilizzando i MBeans forniti da AEM](/help/sites-administering/jmx-console.md).

### Backup snapshot del file system {#filesystem-snapshot-backup}

Il processo qui descritto è particolarmente adatto per grandi archivi.

>[!NOTE]
>
>Se desideri utilizzare questo approccio di backup, il sistema deve supportare le istantanee del file system. Ad esempio, per Linux questo significa che i file system devono essere posizionati su un volume logico.

1. Esegui un&#39;istantanea del AEM del filesystem distribuito in.

1. Montare lo snapshot del file system.
1. Esegui un backup e smonta lo snapshot.

### Come funziona AEM backup online {#how-aem-online-backup-works}

AEM Online Backup è costituito da una serie di azioni interne per garantire l&#39;integrità dei dati sottoposti a backup e dei file di backup in fase di creazione. Questi sono elencati di seguito per gli interessati.

Il backup online utilizza il seguente algoritmo:

1. Quando si crea un file zip, il primo passo è quello di creare o individuare la directory di destinazione.

   * Se si esegue il backup su un file zip, viene creata una directory temporanea. Il nome della directory inizia con `backup.` e termina con `.temp`; per esempio `backup.f4d3.temp`.
   * Se si esegue il backup su una directory, viene utilizzato il nome specificato nel percorso di destinazione. È possibile utilizzare una directory esistente, altrimenti verrà creata una nuova directory.

      Un file vuoto denominato `backupInProgress.txt` viene creato nella directory di destinazione all&#39;avvio del backup. Questo file viene eliminato al termine del backup.

1. I file vengono copiati dalla directory di origine alla directory di destinazione (o directory temporanea durante la creazione di un file zip). Il segmentstore viene copiato prima del datastore per evitare la corruzione dell&#39;archivio. I dati dell&#39;indice e della cache vengono omessi durante la creazione del backup. Di conseguenza, i dati da `crx-quickstart/repository/cache` e `crx-quickstart/repository/index` non è incluso nel backup. L&#39;indicatore della barra di avanzamento del processo è compreso tra 0% - 70% quando si crea un file zip, o tra 0% - 100% se non viene creato alcun file zip.

1. Se il backup viene effettuato su una directory preesistente, i file &quot;vecchi&quot; nella directory di destinazione vengono eliminati. I file precedenti sono file che non esistono nella directory di origine.

I file vengono copiati nella directory di destinazione in quattro fasi:

1. Nella prima fase di copia (indicatore di avanzamento 0% - 63% quando si crea un file zip o 0% - 90% se non viene creato), tutti i file vengono copiati mentre l&#39;archivio è in esecuzione normale. Il processo prevede due fasi:

   * Fase A: tutto viene copiato ad eccezione dell&#39;archivio dati (con ritardo).
   * Fase B: viene copiato solo il datastore (con ritardo).

1. Nella seconda fase di copia (indicatore di avanzamento 63% - 65,8% quando si crea un file zip o 90% - 94% se non viene creato) vengono copiati solo i file creati o modificati nella directory di origine dall&#39;avvio della prima fase di copia. A seconda dell’attività dell’archivio, questo potrebbe variare da nessun file, fino a un numero significativo di file (perché la prima fase di copia del file in genere richiede molto tempo). Il processo di copia è simile alla prima fase (fase A e fase B con ritardo).
1. Nella terza fase di copia (indicatore di avanzamento 65,8% - 68,6% quando si crea un file zip o 94% - 98% se non viene creato) vengono copiati solo i file creati o modificati nella directory di origine dall&#39;avvio della seconda fase di copia. A seconda dell’attività dell’archivio, potrebbe non esserci alcun file da copiare, o un numero molto ridotto di file (perché la seconda fase di copia del file è in genere veloce). Il processo di copia è simile alla seconda fase - fase A e fase B ma senza indugio.
1. Le fasi da una a tre della copia del file vengono eseguite contemporaneamente mentre l&#39;archivio è in esecuzione. Vengono copiati solo i file creati o modificati nella directory di origine dall’avvio della terza fase di copia. A seconda dell’attività dell’archivio, potrebbe non esserci alcun file da copiare, o un numero molto, molto ridotto di file (perché la seconda fase di copia del file di solito è molto veloce). Indicatore di avanzamento 68,6% - 70% quando si crea un file zip o 98% - 100% se non viene creato alcun file zip. Il processo di copia è simile alla terza fase.
1. A seconda del target:

   * Se è stato specificato un file zip, questo viene ora creato dalla directory temporanea. Indicatore di avanzamento 70% - 100%. La directory temporanea viene quindi eliminata.
   * Se la destinazione era una directory, il file vuoto denominato `backupInProgress.txt` viene eliminato per indicare che il backup è terminato.

## Ripristino del backup {#restoring-the-backup}

È possibile ripristinare un backup come segue:

* Nel caso in cui si esegua un FileSystem Snapshot Backup, è possibile semplicemente ripristinare un&#39;immagine del sistema.
* Se hai creato il backup come file zip, decomprimi il contenuto in una nuova cartella e inizia a AEM da tale posizione.

## Backup dei pacchetti {#package-backup}

Per eseguire il backup e il ripristino del contenuto, puoi utilizzare una delle Gestione pacchetti, che utilizza il formato Pacchetto contenuti per eseguire il backup e il ripristino del contenuto. Gestione pacchetti offre maggiore flessibilità nella definizione e gestione dei pacchetti.

Per informazioni dettagliate sulle caratteristiche e sui compromessi di ciascuno di questi formati di pacchetti di contenuti, consulta [Come lavorare con i pacchetti](/help/sites-administering/package-manager.md).

### Ambito del backup {#scope-of-backup}

Quando esegui il backup dei nodi utilizzando Gestione pacchetti o Content Zipper, CRX salva le seguenti informazioni:

* Il contenuto del repository sotto la struttura selezionata.
* Definizioni dei tipi di nodo utilizzate per il contenuto di cui esegui il backup.
* Definizioni dello spazio dei nomi utilizzate per il contenuto di cui esegui il backup.

Durante il backup, AEM perde le seguenti informazioni:

* La cronologia delle versioni.
