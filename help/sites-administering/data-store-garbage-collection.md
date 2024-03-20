---
title: Raccolta oggetti inattivi in archivio dati
description: Scopri come configurare Data Store Garbage Collection per liberare spazio su disco.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
docset: aem65
exl-id: 0dc4a8ce-5b0e-4bc9-a6f5-df2a67149e22
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1892'
ht-degree: 0%

---

# Raccolta oggetti inattivi in archivio dati {#data-store-garbage-collection}

Quando viene rimossa una risorsa WCM convenzionale, il riferimento al record dell’archivio dati sottostante può essere rimosso dalla gerarchia dei nodi, ma il record dell’archivio dati stesso rimane. Questo record di archivio dati senza riferimenti diventa quindi un &quot;immondizia&quot; che non deve essere conservata. Nei casi in cui sono presenti diverse risorse inutilizzate, è utile eliminarle per preservare lo spazio e ottimizzare le prestazioni di backup e manutenzione dei file system.

Nella maggior parte dei casi, un&#39;applicazione WCM tende a raccogliere informazioni, ma non a eliminarle quasi con la stessa frequenza. Sebbene vengano aggiunte nuove immagini, anche sostituendo le versioni precedenti, il sistema di controllo delle versioni mantiene quella precedente e, se necessario, supporta il ripristino. In questo modo, la maggior parte dei contenuti che consideriamo come aggiunte al sistema vengono effettivamente archiviati in modo permanente. Qual è quindi la fonte tipica di &quot;immondizia&quot; nell&#39;archivio che potremmo voler ripulire?

L’AEM utilizza l’archivio come archivio per diverse attività interne e di manutenzione:

* Pacchetti generati e scaricati
* File temporanei creati per la replica di pubblicazione
* Payload del flusso di lavoro
* Risorse create temporaneamente durante il rendering DAM

Quando uno qualsiasi di questi oggetti temporanei è abbastanza grande da richiedere l&#39;archiviazione nell&#39;archivio dati e quando l&#39;oggetto alla fine non viene più utilizzato, il record dell&#39;archivio dati stesso rimane come &quot;spazzatura&quot;. In una tipica applicazione di authoring/pubblicazione WCM, la principale fonte di rifiuti di questo tipo è solitamente il processo di attivazione della pubblicazione. Quando i dati vengono replicati in Publish, vengono raccolti per la prima volta in raccolte in un formato di dati efficiente denominato &quot;Durbo&quot; e memorizzati nell’archivio in `/var/replication/data`. I bundle di dati sono spesso più grandi della soglia di dimensione critica per l’archivio dati e quindi vengono memorizzati come record dell’archivio dati. Al termine della replica, il nodo in `/var/replication/data` viene eliminato, ma il record dell’archivio dati rimane come &quot;spazzatura&quot;.

Un&#39;altra fonte di rifiuti recuperabili sono i pacchetti. I dati del pacchetto, come tutto il resto, vengono memorizzati nell’archivio e quindi, per i pacchetti di dimensioni superiori a 4 KB, nell’archivio dati. Nel corso di un progetto di sviluppo o nel tempo, mantenendo un sistema, i pacchetti possono essere generati e ricostruiti molte volte, ciascuna build determinando un nuovo record dell’archivio dati, che orfana il record della build precedente.

## Come funziona la raccolta di oggetti inattivi dell’archivio dati? {#how-does-data-store-garbage-collection-work}

Se l’archivio è stato configurato con un archivio dati esterno, [la raccolta di oggetti inattivi dell’archivio dati verrà eseguita automaticamente](/help/sites-administering/data-store-garbage-collection.md#automating-data-store-garbage-collection) come parte della finestra Manutenzione settimanale. L&#39;amministratore di sistema può inoltre [esegui manualmente la raccolta di oggetti inattivi dell’archivio dati](#running-data-store-garbage-collection) in base alle necessità. In generale, si consiglia di eseguire periodicamente la raccolta di oggetti inattivi dell’archivio dati, ma di tenere conto dei seguenti fattori nella pianificazione della raccolta di oggetti inattivi dell’archivio dati:

* Le raccolte di oggetti inattivi dell’archivio dati richiedono tempo e possono influire sulle prestazioni, pertanto devono essere pianificate di conseguenza.
* La rimozione dei record di Garbage dell’archivio dati non influisce sulle normali prestazioni, pertanto non si tratta di un’ottimizzazione delle prestazioni.
* Se l&#39;utilizzo dello storage e fattori correlati, come i tempi di backup, non rappresentano un problema, la raccolta di rifiuti dell&#39;archivio dati potrebbe essere rinviata in modo sicuro.

Il Garbage Collector dell’archivio dati prende nota della marca temporale corrente all’inizio del processo. La raccolta viene quindi eseguita utilizzando un algoritmo di pattern a più passate di marcatura/sweep.

Nella prima fase, il Garbage Collector dell’archivio dati esegue un attraversamento completo di tutto il contenuto dell’archivio. Per ogni oggetto di contenuto che ha un riferimento a un record dell&#39;archivio dati, il file viene individuato nel file system, eseguendo un aggiornamento dei metadati, modificando l&#39;attributo &quot;last modified&quot; (ultima modifica) o MTIME. A questo punto, i file a cui si accede in questa fase diventano più recenti della marca temporale della linea di base iniziale.

Nella seconda fase, il garbage collector dell’archivio dati attraversa la struttura della directory fisica dell’archivio dati in modo molto simile a un &quot;find&quot; (trova). Ha esaminato l’attributo &quot;last modified&quot; o MTIME del file e ha determinato quanto segue:

* Se il MTIME è più recente della marca temporale della linea di base iniziale, il file è stato trovato nella prima fase oppure è un file completamente nuovo che è stato aggiunto all’archivio mentre il processo di raccolta era in corso. In entrambi i casi il record è considerato attivo e il file non è cancellato.
* Se l’MTIME è precedente alla marca temporale della linea di base iniziale, il file non è un file a cui si fa riferimento attivamente ed è considerato un’area di cestino rimovibile.

Questo approccio funziona bene per un singolo nodo con un archivio dati privato. Tuttavia, l’archivio dati potrebbe essere condiviso e, in tal caso, i riferimenti live potenzialmente attivi ai record dell’archivio dati provenienti da altri archivi non verranno controllati e i file di riferimento attivi potrebbero essere rimossi per errore. È fondamentale che l’amministratore di sistema comprenda la natura condivisa dell’archivio dati prima di pianificare eventuali raccolte di rifiuti e utilizzi il semplice processo integrato di raccolta dei rifiuti dell’archivio dati solo quando è noto che l’archivio dati non è condiviso.

>[!NOTE]
>
>Quando si esegue la Garbage Collection in una configurazione di archivio dati condiviso o in cluster (con Mongo o Segment Tar), il registro potrebbe visualizzare avvisi sull’impossibilità di eliminare determinati ID BLOB. Ciò si verifica perché agli ID BLOB eliminati in una precedente raccolta di oggetti inattivi viene fatto nuovamente riferimento in modo errato da altri cluster o nodi condivisi che non dispongono di informazioni sulle eliminazioni degli ID. Di conseguenza, quando viene eseguita la raccolta di oggetti inattivi, registra un avviso quando tenta di eliminare un ID che è già stato eliminato nell’ultima esecuzione. Questo comportamento non influisce sulle prestazioni o sulle funzionalità.

## Esecuzione della raccolta oggetti inattivi dell’archivio dati {#running-data-store-garbage-collection}

Esistono tre modi per eseguire la raccolta di oggetti inattivi dell’archivio dati, a seconda della configurazione dell’archivio dati su cui è in esecuzione AEM:

1. Via [Pulizia revisioni](/help/sites-deploying/revision-cleanup.md) - un meccanismo di raccolta dei rifiuti solitamente utilizzato per la pulizia dell’archivio nodi.

1. Via [Raccolta oggetti inattivi dell’archivio dati](/help/sites-administering/data-store-garbage-collection.md#running-data-store-garbage-collection-via-the-operations-dashboard) : meccanismo di raccolta dei rifiuti specifico per gli archivi di dati esterni, disponibile nel dashboard operazioni.
1. Attraverso il [Console JMX](/help/sites-administering/jmx-console.md).

Se si utilizza TarMK sia come archivio nodi che come archivio dati, è possibile utilizzare Pulizia revisioni per la raccolta di oggetti inattivi sia dell’archivio nodi che dell’archivio dati. Tuttavia, se è configurato un archivio dati esterno, ad esempio Archivio dati del file system, la raccolta di oggetti inattivi dell’archivio dati deve essere attivata in modo esplicito e separata da Pulizia revisioni. La raccolta di oggetti inattivi dell’archivio dati può essere attivata tramite il dashboard operazioni o la console JMX.

La tabella seguente mostra il tipo di raccolta di oggetti inattivi dell’archivio dati che deve essere utilizzato per tutte le distribuzioni dell’archivio dati supportate nell’AEM 6:

<table>
 <tbody>
  <tr>
   <td><strong>Archivio nodi</strong><br /> </td>
   <td><strong>Archivio dati</strong></td>
   <td><strong>Meccanismo di raccolta dei rifiuti</strong><br /> </td>
  </tr>
  <tr>
   <td>TarMK</td>
   <td>TarMK</td>
   <td>Pulizia delle revisioni (i file binari sono allineati con l’archivio segmenti)</td>
  </tr>
  <tr>
   <td>TarMK</td>
   <td>File system esterno</td>
   <td><p>Attività di raccolta oggetti inattivi archivio dati tramite dashboard operazioni</p> <p>Console JMX</p> </td>
  </tr>
  <tr>
   <td>MongoDB</td>
   <td>MongoDB</td>
   <td><p>Attività di raccolta oggetti inattivi archivio dati tramite dashboard operazioni</p> <p>Console JMX</p> </td>
  </tr>
  <tr>
   <td>MongoDB</td>
   <td>File system esterno</td>
   <td><p>Attività di raccolta oggetti inattivi archivio dati tramite dashboard operazioni</p> <p>Console JMX</p> </td>
  </tr>
 </tbody>
</table>

### Esecuzione della raccolta di oggetti inattivi dell’archivio dati tramite il dashboard operazioni {#running-data-store-garbage-collection-via-the-operations-dashboard}

Finestra di manutenzione settimanale integrata, disponibile tramite [Dashboard operazioni](/help/sites-administering/operations-dashboard.md), contiene un’attività incorporata per attivare Data Store Garbage Collection all’1 di domenica.

Se devi eseguire la raccolta di oggetti inattivi dell’archivio dati al di fuori di questo periodo di tempo, può essere attivata manualmente tramite il dashboard operazioni.

Prima di eseguire la raccolta di oggetti inattivi dell’archivio dati, verifica che non siano in esecuzione backup in quel momento.

1. Aprire il dashboard operazioni con **Navigazione** > **Strumenti** > **Operazioni** > **Manutenzione**.
1. Fai clic su **Finestra di manutenzione settimanale**.

   ![chlimage_1-64](assets/chlimage_1-64.png)

1. Seleziona la **Raccolta oggetti inattivi dell’archivio dati** e quindi fare clic sul pulsante **Esegui** icona.

   ![chlimage_1-65](assets/chlimage_1-65.png)

1. La raccolta di oggetti inattivi dell’archivio dati viene eseguita e il relativo stato viene visualizzato nel dashboard.

   ![chlimage_1-66](assets/chlimage_1-66.png)

>[!NOTE]
>
>L’attività Raccolta oggetti inattivi dell’archivio dati sarà visibile solo se hai configurato un archivio dati di file esterno. Consulta [Configurazione degli archivi dei nodi e dei dati in AEM 6](/help/sites-deploying/data-store-config.md#file-data-store) per informazioni su come impostare un archivio dati di file.

### Esecuzione della raccolta di oggetti inattivi dell’archivio dati tramite la console JMX {#running-data-store-garbage-collection-via-the-jmx-console}

Questa sezione riguarda l’esecuzione manuale della raccolta di oggetti inattivi dell’archivio dati tramite la console JMX. Se l’installazione è configurata senza un archivio dati esterno, ciò non si applica all’installazione. Vedi invece le istruzioni su come eseguire la pulizia delle revisioni in [Gestione dell’archivio](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository).

>[!NOTE]
>
>Se si esegue TarMK con un archivio dati esterno, è necessario eseguire prima Pulizia revisioni per rendere effettiva la raccolta di oggetti inattivi.

Per eseguire la raccolta di oggetti inattivi:

1. Nella console di gestione OSGi Apache Felix, evidenzia **Principale** e seleziona **JMX** dal menu seguente.
1. Quindi, cerca e fai clic su **Gestione archivio** MBean (o vai a `https://<host>:<port>/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Drepository+manager%2Ctype%3DRepositoryManagement`).
1. Clic **startDataStoreGC(markOnly booleano)**.
1. immetti &quot;`true`&quot; per `markOnly` parametro, se necessario:

   | **Opzione** | **Descrizione** |
   |---|---|
   | markOnly booleano | Impostare su true per contrassegnare solo i riferimenti e non eseguire la sweep nell&#39;operazione di contrassegno e di sweep. Questa modalità deve essere utilizzata quando il BlobStore sottostante è condiviso tra più archivi diversi. Per tutti gli altri casi, impostalo su false per eseguire la raccolta completa dei rifiuti. |

1. Clic **Richiama**. CRX esegue la raccolta di oggetti inattivi e indica quando è stata completata.

>[!NOTE]
>
>La raccolta di oggetti inattivi dell’archivio dati non raccoglierà i file eliminati nelle ultime 24 ore.

>[!NOTE]
>
>L’attività di Garbage Collection dell’archivio dati verrà avviata solo se hai configurato un archivio dati di file esterno. Se non è stato configurato un archivio dati di file esterno, l&#39;attività restituirà il messaggio `Cannot perform operation: no service of type BlobGCMBean found` dopo aver richiamato. Consulta [Configurazione degli archivi dei nodi e dei dati in AEM 6](/help/sites-deploying/data-store-config.md#file-data-store) per informazioni su come impostare un archivio dati di file.

## Automazione della raccolta di oggetti inattivi dell’archivio dati {#automating-data-store-garbage-collection}

Se possibile, la raccolta di oggetti inattivi dell’archivio dati deve essere eseguita quando il carico sul sistema è ridotto, ad esempio al mattino.

Finestra di manutenzione settimanale integrata, disponibile tramite [Dashboard operazioni](/help/sites-administering/operations-dashboard.md), contiene un’attività incorporata per attivare Data Store Garbage Collection all’1 di domenica. È inoltre consigliabile verificare che al momento non sia in esecuzione alcun backup. L’inizio della finestra di manutenzione può essere personalizzato tramite la dashboard, a seconda delle necessità.

>[!NOTE]
>
>Il motivo per cui non deve essere eseguito contemporaneamente è che viene eseguito anche il backup dei file di archivio dati vecchi (e inutilizzati), in modo che se è necessario eseguire il rollback a una revisione precedente, i file binari siano ancora presenti nel backup.

Se non desideri eseguire la raccolta di oggetti inattivi dell’archivio dati con la finestra Manutenzione settimanale nel dashboard Operazioni, puoi anche automatizzarla utilizzando i client HTTP wget o curl. Di seguito è riportato un esempio di come automatizzare la raccolta di oggetti inattivi utilizzando curl:

>[!CAUTION]
>
>Nell’esempio seguente `curl` comandi potrebbe essere necessario configurare vari parametri per l’istanza; ad esempio, il nome host ( `localhost`), porta ( `4502`), password amministratore ( `xyz`) e vari parametri per l’effettiva raccolta di rifiuti dell’archivio dati.

Di seguito è riportato un comando curl di esempio per richiamare la raccolta di oggetti inattivi dell’archivio dati tramite la riga di comando:

```shell
curl -u admin:admin -X POST --data markOnly=true  https://localhost:4503/system/console/jmx/org.apache.jackrabbit.oak"%"3Aname"%"3Drepository+manager"%"2Ctype"%"3DRepositoryManagement/op/startDataStoreGC/boolean
```

Il comando curl restituisce immediatamente.

## Verifica della coerenza dell’archivio dati {#checking-data-store-consistency}

La verifica di coerenza dell’archivio dati segnala eventuali dati binari mancanti ma a cui si fa ancora riferimento. Per avviare una verifica di coerenza, effettua le seguenti operazioni:

1. Passa alla console JMX. Per informazioni su come utilizzare la console JMX, consulta [questo articolo](/help/sites-administering/jmx-console.md#using-the-jmx-console).
1. Cerca **BlobGarbageCollection** Mbean e fai clic su di esso.
1. Fai clic su `checkConsistency()` collegamento.

Al termine della verifica di coerenza, un messaggio mostra il numero di dati binari segnalati come mancanti. Se il numero è maggiore di 0, controllare `error.log` per ulteriori dettagli sui file binari mancanti.

Di seguito è riportato un esempio di come i file binari mancanti vengono segnalati nei registri:

```xml
11:32:39.673 INFO [main] MarkSweepGarbageCollector.java:600 Consistency check found [1] missing blobs
```

```xml
11:32:39.673 WARN [main] MarkSweepGarbageCollector.java:602 Consistency check failure intheblob store : DataStore backed BlobStore [org.apache.jackrabbit.oak.plugins.blob.datastore.OakFileDataStore], check missing candidates in file /tmp/gcworkdir-1467352959243/gccand-1467352959243
```
