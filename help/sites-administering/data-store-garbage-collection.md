---
title: Archivio dati raccolta oggetti inattivi
seo-title: Archivio dati raccolta oggetti inattivi
description: Scoprite come configurare la raccolta dei dati dell'archivio dati per liberare spazio su disco.
seo-description: Scoprite come configurare la raccolta dei dati dell'archivio dati per liberare spazio su disco.
uuid: 49488a81-986a-4d1a-96c8-aeb6595fc094
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 5b1e46c5-7e56-433e-b62e-2a76ea7be0fd
docset: aem65
translation-type: tm+mt
source-git-commit: 0eda6ee61acf737abc91d1e5df731e719663b3f2
workflow-type: tm+mt
source-wordcount: '1904'
ht-degree: 0%

---


# Archivio dati raccolta oggetti inattivi {#data-store-garbage-collection}

Quando una risorsa WCM convenzionale viene rimossa, il riferimento al record dell&#39;archivio dati sottostante potrebbe essere rimosso dalla gerarchia dei nodi, ma il record dell&#39;archivio dati rimane inalterato. Questo record dell&#39;archivio dati senza riferimenti diventa quindi &quot;spazzatura&quot; che non deve essere conservata. Nei casi in cui esistono numerose risorse per la gestione dei rifiuti, è utile eliminarle per conservare lo spazio e ottimizzare le prestazioni di backup e manutenzione del file system.

Nella maggior parte dei casi, un&#39;applicazione WCM tende a raccogliere informazioni ma non a eliminarle con la stessa frequenza. Anche se vengono aggiunte nuove immagini, anche in sostituzione delle versioni precedenti, il sistema di controllo delle versioni conserva il vecchio e supporta il ripristino, se necessario. Pertanto, la maggior parte dei contenuti che consideriamo aggiunti al sistema è effettivamente memorizzata in modo permanente. Quindi qual è la fonte tipica di &quot;spazzatura&quot; nel repository che potremmo voler ripulire?

AEM utilizza il repository come archivio per una serie di attività interne e di gestione:

* Pacchetti generati e scaricati
* File temporanei creati per la replica di pubblicazione
* Payload del flusso di lavoro
* Risorse create temporaneamente durante il rendering DAM

Quando uno di questi oggetti temporanei è sufficientemente grande da richiedere l&#39;archiviazione nell&#39;archivio dati e quando l&#39;oggetto alla fine smette di essere utilizzato, il record dell&#39;archivio dati stesso rimane &quot;spazzatura&quot;. In una tipica applicazione di creazione e pubblicazione WCM, l’origine principale di rifiuti di questo tipo è in genere il processo di attivazione della pubblicazione. Quando i dati vengono replicati in Pubblica, vengono raccolti per la prima volta nelle raccolte in un formato di dati efficiente denominato &quot;Durbo&quot; e memorizzati nell&#39;archivio in `/var/replication/data`. I bundle di dati sono spesso più grandi della soglia di dimensione critica per l&#39;archivio dati e vengono quindi archiviati come record dell&#39;archivio dati. Una volta completata la replica, il nodo in `/var/replication/data` viene eliminato, ma il record dell&#39;archivio dati rimane come &quot;spazzatura&quot;.

Un&#39;altra fonte di rifiuti recuperabili sono i pacchetti. I dati del pacchetto, come tutto il resto, vengono memorizzati nella directory archivio e quindi per i pacchetti di dimensioni maggiori di 4 KB, nell&#39;archivio dati. Nel corso di un progetto di sviluppo o nel corso del tempo, durante la manutenzione di un sistema, i pacchetti possono essere costruiti e rigenerati più volte, ciascuna build risulta in un nuovo record dell&#39;archivio dati, orfando il record della build precedente.

## Come funziona la raccolta dei rifiuti nell&#39;archivio dati? {#how-does-data-store-garbage-collection-work}

Se l&#39;archivio è stato configurato con un archivio dati esterno, la raccolta dei rifiuti nell&#39;archivio dati [verrà eseguita automaticamente](/help/sites-administering/data-store-garbage-collection.md#automating-data-store-garbage-collection) come parte della finestra di manutenzione settimanale. L&#39;amministratore di sistema può anche [eseguire manualmente la raccolta dei rifiuti nell&#39;archivio dati](#running-data-store-garbage-collection) in base alle esigenze. In generale, si consiglia di eseguire periodicamente la raccolta dei rifiuti nell&#39;archivio dati, ma di tenere conto dei seguenti fattori nella pianificazione delle raccolte di rifiuti nell&#39;archivio dati:

* Le raccolte di rifiuti dell&#39;archivio dati richiedono tempo e possono avere un impatto sulle prestazioni, pertanto dovrebbero essere pianificate di conseguenza.
* La rimozione dei record inattivi dell&#39;archivio dati non influisce sulle prestazioni normali, pertanto non si tratta di un&#39;ottimizzazione delle prestazioni.
* Se l&#39;utilizzo dello storage e fattori correlati come i tempi di backup non rappresentano un problema, la raccolta dei rifiuti nell&#39;archivio dati potrebbe essere posticipata in modo sicuro.

Il Garbage Collector dell&#39;archivio dati nota innanzitutto la marca temporale corrente all&#39;inizio del processo. La raccolta viene quindi eseguita utilizzando un algoritmo con pattern di contrassegno/sweep con più passate.

Nella prima fase, il Garbage Collector dell&#39;archivio dati esegue una lettura completa di tutto il contenuto del repository. Per ogni oggetto di contenuto che ha un riferimento a un record dell&#39;archivio dati, il file si trova nel file system, eseguendo un aggiornamento dei metadati, modificando l&#39;attributo &quot;last modified&quot; o MTIME. A questo punto, i file a cui si accede in questa fase diventano più recenti rispetto alla marca temporale iniziale della linea di base.

Nella seconda fase, il Garbage Collector dell&#39;archivio dati attraversa la struttura di directory fisica dell&#39;archivio dati nello stesso modo di un &quot;find&quot;. Ha esaminato l&#39;attributo &quot;last modified&quot; o MTIME del file ed effettua le seguenti verifiche:

* Se il MTIME è più recente della marca temporale iniziale della linea di base, il file è stato trovato nella prima fase, oppure è un file completamente nuovo che è stato aggiunto al repository mentre il processo di raccolta era in corso. In uno di questi casi il record è considerato attivo e il file non deve essere eliminato.
* Se il valore MTIME è precedente alla marca temporale della linea di base iniziale, il file non è un file a cui viene fatto riferimento attivamente e viene considerato come spazzatura rimovibile.

Questo approccio funziona bene per un singolo nodo con un archivio dati privato. Tuttavia, l&#39;archivio dati può essere condiviso e, se ciò significa che i riferimenti live potenzialmente attivi ai record dell&#39;archivio dati di altri repository non sono controllati, e i file di riferimento attivi potrebbero essere eliminati per errore. È fondamentale che l&#39;amministratore di sistema comprenda la natura condivisa dell&#39;archivio dati prima di pianificare le raccolte di rifiuti e che utilizzi solo il semplice processo di raccolta di oggetti inattivi dell&#39;archivio dati incorporato quando è noto che l&#39;archivio dati non è condiviso.

>[!NOTE]
>
>Durante l&#39;esecuzione della raccolta dei dati in un&#39;impostazione dell&#39;archivio dati cluster o condiviso (con Mongo o Segment Tar), il registro potrebbe visualizzare avvisi sull&#39;impossibilità di eliminare alcuni ID BLOB. Ciò accade perché gli ID BLOB eliminati in una precedente raccolta di oggetti inattivi sono erroneamente citati da altri nodi cluster o condivisi che non dispongono di informazioni sulle eliminazioni ID. Di conseguenza, quando viene eseguita la raccolta di oggetti inattivi, viene registrato un avviso quando si tenta di eliminare un ID già eliminato nell&#39;ultima esecuzione. Questo comportamento non influisce sulle prestazioni o sulle funzionalità.

## Esecuzione della raccolta di oggetti inattivi nell&#39;archivio dati {#running-data-store-garbage-collection}

Sono disponibili tre modi per eseguire la raccolta dei rifiuti dell&#39;archivio dati, a seconda dell&#39;impostazione dell&#39;archivio dati in cui AEM in esecuzione:

1. Tramite [Revision Cleanup](/help/sites-deploying/revision-cleanup.md) - un meccanismo di raccolta dei rifiuti generalmente utilizzato per la pulizia dell&#39;archivio nodi.

1. Tramite [Data Store Garbage Collection](/help/sites-administering/data-store-garbage-collection.md#running-data-store-garbage-collection-via-the-operations-dashboard) - un meccanismo di raccolta dei rifiuti specifico per gli archivi di dati esterni, disponibile nel dashboard delle operazioni.
1. Tramite la [console JMX](/help/sites-administering/jmx-console.md).

Se TarMK viene utilizzato sia come archivio nodi che come archivio dati, Revision Cleanup può essere utilizzato per la raccolta dei rifiuti sia dell&#39;archivio nodi che dell&#39;archivio dati. Tuttavia, se è configurato un archivio dati esterno, ad esempio Archivio dati del file system, la raccolta dei rifiuti dell&#39;archivio dati deve essere attivata in modo esplicito e separato dalla funzione Revision Cleanup. È possibile attivare la raccolta dei rifiuti dell&#39;archivio dati tramite il dashboard delle operazioni o la console JMX.

Nella tabella seguente è illustrato il tipo di raccolta di oggetti inattivi dell&#39;archivio dati che è necessario utilizzare per tutte le distribuzioni dell&#39;archivio dati supportate in AEM 6:

<table>
 <tbody>
  <tr>
   <td><strong>Archivio nodi</strong><br /> </td>
   <td><strong>Archivio dati</strong></td>
   <td><strong>Meccanismo di raccolta rifiuti</strong><br /> </td>
  </tr>
  <tr>
   <td>TarMK</td>
   <td>TarMK</td>
   <td>Pulizia delle revisioni (i file binari sono allineati con Segment Store)</td>
  </tr>
  <tr>
   <td>TarMK</td>
   <td>File system esterno</td>
   <td><p>Attività di raccolta dei dati dall'archivio dati tramite il dashboard operativo</p> <p>Console JMX</p> </td>
  </tr>
  <tr>
   <td>MongoDB</td>
   <td>MongoDB</td>
   <td><p>Attività di raccolta dei dati dall'archivio dati tramite il dashboard operativo</p> <p>Console JMX</p> </td>
  </tr>
  <tr>
   <td>MongoDB</td>
   <td>File system esterno</td>
   <td><p>Attività di raccolta dei dati dall'archivio dati tramite il dashboard operativo</p> <p>Console JMX</p> </td>
  </tr>
 </tbody>
</table>

### Esecuzione della raccolta di oggetti inattivi nell&#39;archivio dati tramite il dashboard delle operazioni {#running-data-store-garbage-collection-via-the-operations-dashboard}

La finestra di manutenzione settimanale integrata, disponibile tramite il [Pannello operazioni](/help/sites-administering/operations-dashboard.md), contiene un&#39;attività incorporata per attivare la raccolta dei dati da parte dell&#39;archivio dati alle 1 del mattino della domenica.

Se è necessario eseguire la raccolta dei rifiuti dell&#39;archivio dati al di fuori di questo intervallo di tempo, può essere attivata manualmente tramite il Pannello operazioni.

Prima di eseguire la raccolta dei rifiuti dell&#39;archivio dati è necessario verificare che al momento non siano in esecuzione backup.

1. Aprite il Pannello operazioni **Navigazione** -> **Strumenti** -> **Operazioni** -> **Manutenzione**.
1. Tocca o fai clic su **Finestra manutenzione settimanale**.

   ![chlimage_1-64](assets/chlimage_1-64.png)

1. Selezionare l&#39;attività **Data Store Garbage Collection**, quindi fare clic o toccare l&#39;icona **Esegui**.

   ![chlimage_1-65](assets/chlimage_1-65.png)

1. Viene eseguito il processo di garbage collection dell&#39;archivio dati e il relativo stato viene visualizzato nel dashboard.

   ![chlimage_1-66](assets/chlimage_1-66.png)

>[!NOTE]
>
>L&#39;attività di raccolta dei dati nell&#39;archivio dati sarà visibile solo se hai configurato un archivio dati file esterno. Per informazioni su come impostare un archivio dati file, vedere [Configurazione di archivi di nodi e di archivi dati in AEM 6](/help/sites-deploying/data-store-config.md#file-data-store).

### Esecuzione della raccolta di oggetti indesiderati dall&#39;archivio dati tramite la console JMX {#running-data-store-garbage-collection-via-the-jmx-console}

In questa sezione viene illustrato come eseguire manualmente la raccolta dei rifiuti dell&#39;archivio dati tramite la console JMX. Se l&#39;installazione è impostata senza un archivio dati esterno, questo non si applica all&#39;installazione. Al contrario, vedere le istruzioni su come eseguire la pulizia delle revisioni in [Gestione dell&#39;archivio](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository).

>[!NOTE]
>
>Se si esegue TarMK con un archivio dati esterno, è necessario eseguire prima Revision Cleanup per rendere efficace la raccolta dei rifiuti.

Per eseguire la raccolta di oggetti inattivi:

1. Nella console di gestione Apache Felix OSGi, evidenziare la scheda **Principale** e selezionare **JMX** dal menu seguente.
1. Quindi, cercare e fare clic su **Repository Manager** MBean (o passare a `https://<host>:<port>/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Drepository+manager%2Ctype%3DRepositoryManagement`).
1. Fare clic su **startDataStoreGC(boolean markOnly)**.
1. immettere &quot;`true`&quot; per il parametro `markOnly`, se necessario:

   | **Opzione** | **Descrizione** |
   |---|---|
   | boolean markOnly | Impostate su true solo per contrassegnare i riferimenti e non per eseguire lo sweep nell&#39;operazione di mark e sweep. Questa modalità deve essere utilizzata quando il BlobStore sottostante è condiviso tra più repository diversi. Per tutti gli altri casi, impostatelo su false per eseguire la raccolta completa dei rifiuti. |

1. Fare clic su **Richiama**. CRX esegue il processo di garbage collection e indica quando è stato completato.

>[!NOTE]
>
>La raccolta dei rifiuti dell&#39;archivio dati non raccoglierà i file che sono stati eliminati nelle ultime 24 ore.

>[!NOTE]
>
>L&#39;attività di raccolta dei rifiuti dell&#39;archivio dati verrà avviata solo se è stato configurato un archivio dati file esterno. Se l&#39;archivio dati del file esterno non è stato configurato, l&#39;attività restituirà il messaggio `Cannot perform operation: no service of type BlobGCMBean found` dopo la chiamata. Per informazioni su come impostare un archivio dati file, vedere [Configurazione di archivi di nodi e di archivi dati in AEM 6](/help/sites-deploying/data-store-config.md#file-data-store).

## Automazione della raccolta di oggetti inattivi nell&#39;archivio dati {#automating-data-store-garbage-collection}

Se possibile, la raccolta dei rifiuti nell&#39;archivio dati deve essere eseguita quando il carico sul sistema è limitato, ad esempio la mattina.

La finestra di manutenzione settimanale integrata, disponibile tramite il [Pannello operazioni](/help/sites-administering/operations-dashboard.md), contiene un&#39;attività incorporata per attivare la raccolta dei dati da parte dell&#39;archivio dati alle 1 del mattino della domenica. È inoltre necessario verificare che al momento non siano in esecuzione backup. L&#39;inizio della finestra di manutenzione può essere personalizzato tramite il dashboard, a seconda delle necessità.

>[!NOTE]
>
>Il motivo per non eseguire contemporaneamente è che anche i file dell&#39;archivio dati vecchi (e inutilizzati) vengono sottoposti a backup, in modo che se è necessario ripristinare una vecchia revisione, i file binari sono ancora presenti nel backup.

Se non si desidera eseguire la raccolta dei rifiuti dell&#39;archivio dati con la finestra Manutenzione settimanale nel Pannello operazioni, è possibile automatizzarla anche tramite client HTTP wget o curl. Di seguito è riportato un esempio di come automatizzare il backup utilizzando curl:

>[!CAUTION]
>
>Nell&#39;esempio seguente `curl` potrebbero essere necessari diversi parametri per la vostra istanza; ad esempio, il nome host ( `localhost`), la porta ( `4502`), la password amministratore ( `xyz`) e vari parametri per la raccolta di oggetti inattivi dell&#39;archivio dati effettiva.

Di seguito è riportato un comando curl di esempio per richiamare la raccolta di oggetti indesiderati nell&#39;archivio dati tramite la riga di comando:

```shell
curl -u admin:admin -X POST --data markOnly=true  https://localhost:4503/system/console/jmx/org.apache.jackrabbit.oak"%"3Aname"%"3Drepository+manager"%"2Ctype"%"3DRepositoryManagement/op/startDataStoreGC/boolean
```

Il comando curl ritorna immediatamente.

## Verifica della coerenza dell&#39;archivio dati {#checking-data-store-consistency}

La verifica della coerenza dell&#39;archivio dati segnalerà eventuali file binari dell&#39;archivio dati mancanti ma a cui viene fatto ancora riferimento. Per avviare un controllo di coerenza, procedere come segue:

1. Passate alla console JMX. Per informazioni sull&#39;utilizzo della console JMX, consultate [questo articolo](/help/sites-administering/jmx-console.md#using-the-jmx-console).
1. Cercare il fagiolo **BlobGarbageCollection** e fare clic su di esso.
1. Fare clic sul collegamento `checkConsistency()`.

Al termine della verifica di coerenza, verrà visualizzato un messaggio che indica il numero di file binari segnalati come mancanti. Se il numero è maggiore di 0, controllare la `error.log` per ulteriori dettagli sui file binari mancanti.

Di seguito è riportato un esempio di come i file binari mancanti vengono segnalati nei file di registro:

```xml
11:32:39.673 INFO [main] MarkSweepGarbageCollector.java:600 Consistency check found [1] missing blobs
```

```xml
11:32:39.673 WARN [main] MarkSweepGarbageCollector.java:602 Consistency check failure intheblob store : DataStore backed BlobStore [org.apache.jackrabbit.oak.plugins.blob.datastore.OakFileDataStore], check missing candidates in file /tmp/gcworkdir-1467352959243/gccand-1467352959243
```

