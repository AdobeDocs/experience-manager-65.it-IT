---
title: Cartella osservata in AEM Forms
seo-title: Watched folder in AEM Forms
description: Un amministratore può mettere una cartella all’orologio e avviare un flusso di lavoro, un servizio o un’operazione di script quando un file viene inserito nella cartella controllata.
seo-description: An administrator can put a folder on watch and start a workflow, service, or script operation when a file is placed in the folder being watched.
uuid: 39eac0fd-8212-46ff-b75d-8b4320d448a9
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: db38972c-be3f-49fd-8cc1-45b16ed244af
docset: aem65
exl-id: fbf5c7c3-cb01-4fda-8e5d-11d56792d4bf
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '7149'
ht-degree: 0%

---

# Cartella osservata in AEM Forms{#watched-folder-in-aem-forms}

Un amministratore può configurare una cartella di rete, nota come Cartella sottoposta a controllo, in modo che quando un utente inserisce un file (ad esempio un file PDF) nella Cartella sottoposta a controllo, un flusso di lavoro, un servizio o un&#39;operazione di script preconfigurata venga l&#39;elaborazione del file aggiunto. Dopo che il servizio esegue l&#39;operazione specificata, salva il file dei risultati in una cartella di output specificata. Per ulteriori informazioni su flusso di lavoro, servizio e script, vedi [Vari metodi di elaborazione dei file](#variousmethodsforprocessingfiles).

## Creare una cartella osservata {#create-a-watched-folder}

È possibile utilizzare uno dei metodi seguenti per creare una cartella osservata nel file system:

* Durante la configurazione delle proprietà di un nodo di configurazione di una cartella controllata, digitare il percorso completo della directory principale nella proprietà folderPath e aggiungere il nome della cartella controllata da creare, come illustrato nell&#39;esempio seguente: `C:/MyPDFs/MyWatchedFolder`
La 
`MyWatchedFolder`cartella inesistente. AEM Forms tenta di creare la cartella nel percorso specificato.

* Crea una cartella sul file system prima di configurare un endpoint Watched Folder e quindi fornisci il percorso completo nella proprietà folderPath. Per informazioni dettagliate sulla proprietà folderPath, vedere [Proprietà delle cartelle controllate](#watchedfolderproperties).

>[!NOTE]
>
>In un ambiente cluster, la cartella utilizzata come cartella sottoposta a controllo deve essere accessibile, scrivibile e condivisa sul file system o sulla rete. Ogni istanza del server applicazioni del cluster deve avere accesso alla stessa cartella condivisa. In Windows, creare un&#39;unità di rete mappata su tutti i server e specificare il percorso dell&#39;unità di rete mappata nella proprietà folderPath.

## Crea nodo di configurazione della cartella di controllo {#create-watched-folder-configuration-node}

Per configurare una cartella sottoposta a controllo, crea un nodo di configurazione della cartella sottoposta a controllo. Esegui i seguenti passaggi per creare il nodo di configurazione:

1. Accedi a CRX-DE lite come amministratore e vai alla cartella /etc/fd/watchfolder/config .

1. Crea un nodo di tipo `nt:unstructured`. Ad esempio, watchedfolder

   >[!NOTE]
   >
   >Il nome del nodo Cartella controllata non può includere spazi e caratteri speciali.

1. Aggiungi le seguenti proprietà al nodo :

   * `folderPath`
   * `inputProcessorType`
   * `inputProcessorId`
   * `outputFilePattern`

   Per un elenco completo delle proprietà supportate, vedi [Proprietà delle cartelle controllate](#watchedfolderproperties).

1. Fai clic su **Salva tutto**. Dopo la creazione del nodo e il salvataggio delle proprietà. La `input`, `result`, `failure`, `preserve`e `stage`le cartelle vengono create nel percorso specificato nel `folderPath` proprietà.

   Il processo di scansione inizia la scansione della cartella osservata a un intervallo di tempo definito.

## Proprietà delle cartelle controllate {#watchedfolderproperties}

È possibile configurare le seguenti proprietà per una cartella sottoposta a controllo.

* **folderPath (String)**: Percorso della cartella da analizzare a intervalli di tempo definiti. Per un ambiente cluster, la cartella deve trovarsi in un percorso condiviso con tutti i server che dispongono dell&#39;accesso completo al server. È una proprietà obbligatoria.
* **inputProcessorType (String)**: Il tipo di processo da avviare. È possibile specificare flusso di lavoro, script o servizio. È una proprietà obbligatoria.
* **inputProcessorId (stringa)**: Il comportamento della proprietà inputProcessorId si basa sul valore specificato per la proprietà inputProcessorType. È una proprietà obbligatoria. Nell&#39;elenco seguente sono descritti tutti i possibili valori della proprietà inputProcessorType e il relativo requisito per la proprietà inputProcessorType:

   * Per il flusso di lavoro, specifica il modello di flusso di lavoro da eseguire. Ad esempio, /etc/workflow/models/&lt;workflow_name>/jcr:content/model
   * Per lo script, specifica il percorso JCR dello script da eseguire. Ad esempio, /etc/fd/watchfolder/test/testScript.ecma
   * Per il servizio , specifica il filtro utilizzato per individuare un servizio OSGi. Il servizio è registrato come implementazione dell&#39;interfaccia com.adobe.aemfd.watchfolder.service.api.ContentProcessor.

* **runModes (String)**: Elenco separato da virgole delle modalità di esecuzione consentite per l’esecuzione del flusso di lavoro. Alcuni esempi sono:

   * author

   * pubblicazione

   * creazione,pubblicazione

   * pubblicare, autore

>[!NOTE]
>
>Se il server che ospita la cartella sottoposta a controllo non dispone della modalità di esecuzione specificata, la cartella sottoposta a controllo si attiva sempre indipendentemente dalle modalità di esecuzione sul server.

* **outputFilePattern (String)**: Pattern del file di output. È possibile specificare una cartella o un pattern di file. Se viene specificato un pattern di cartelle, i file di output hanno nomi come descritto nei flussi di lavoro. Se viene specificato un pattern di file, i file di output hanno nomi come descritto nel pattern di file. [Pattern di file e cartelle](../../forms/using/watched-folder-in-aem-forms.md#p-file-and-folder-patterns-p) può anche specificare una struttura di directory per i file di output. È una proprietà obbligatoria.

* **stageFileExpirationDuration (Long, default -1)**: Il numero di secondi di attesa prima che un file o una cartella di input sia già stato prelevato per l’elaborazione deve essere considerato come se si trattasse di un timeout e contrassegnato come un errore. Questo meccanismo di scadenza si attiva solo quando il valore di questa proprietà è un numero positivo.

>[!NOTE]
>
>Anche quando un input viene contrassegnato come timeout utilizzando questo meccanismo, potrebbe essere ancora in fase di elaborazione in background, ma richiede più tempo del previsto. Se il contenuto di input è stato utilizzato prima dell’avvio del meccanismo di timeout, l’elaborazione potrebbe persino procedere al completamento in un secondo momento e l’output potrebbe essere scaricato nella cartella dei risultati. Se i contenuti non sono stati utilizzati prima del timeout, è molto probabile che l’elaborazione si interrompa in un secondo momento quando si tenta di consumare il contenuto, e questo errore verrà registrato anche nella cartella degli errori per lo stesso input. D’altro canto, se l’elaborazione per l’input non si attiva mai a causa di un errore di processo/flusso di lavoro intermittente (che è lo scenario che il meccanismo di scadenza intende affrontare), ovviamente non si verificherà nessuna di queste due eventualità. Quindi, per tutte le voci nella cartella dei guasti contrassegnate come errori a causa di un timeout (cercare i messaggi del modulo &quot;File non elaborato dopo un periodo di tempo significativo, contrassegnandoli come errori!&quot; nel registro degli errori), è consigliabile analizzare la cartella dei risultati (e anche la cartella degli errori stessa per un’altra voce per lo stesso input) per verificare se si è verificata una delle eventualità descritte in precedenza.

* **deleteExpiredStageFileOnlyWhenThrottled (Boolean, impostazione predefinita true):** Se il meccanismo di scadenza deve attivarsi solo quando la cartella di controllo è limitata. Il meccanismo è più pertinente per le cartelle di controllo a griglia, in quanto un numero limitato di file che rimangono in uno stato non elaborato (a causa di errori intermittenti di processo/flusso di lavoro) ha il potenziale di soffocare l&#39;elaborazione per l&#39;intero batch quando la limitazione è abilitata. Se questa proprietà viene mantenuta come true (opzione predefinita), il meccanismo di scadenza non viene attivato per le cartelle di controllo che non sono soggette a limitazione. Se la proprietà viene mantenuta come false, il meccanismo viene sempre attivato purché la proprietà stageFileExpirationDuration sia un numero positivo.

* **pollInterval (Long)**: Intervallo in secondi per la scansione della cartella sottoposta a controllo per l&#39;input. A meno che l’impostazione di limitazione non sia abilitata, l’intervallo di polling deve essere più lungo del tempo necessario per elaborare un lavoro medio; in caso contrario, il sistema potrebbe sovraccaricarsi. Il valore predefinito è 5. Per ulteriori informazioni, consulta la descrizione di Dimensione batch . Il valore dell&#39;intervallo di polling deve essere maggiore o uguale a uno.
* **excludeFilePattern (String)**: Un elenco delimitato da punti e virgola (;) di pattern utilizzati da una cartella sottoposta a controllo per determinare quali file e cartelle analizzare e raccogliere. Qualsiasi file o cartella con questo pattern non viene analizzato per l’elaborazione. Questa impostazione è utile quando l’input è una cartella con più file. Il contenuto della cartella può essere copiato in una cartella con un nome scelto dalla cartella sottoposta a controllo. Questo impedisce alla cartella sottoposta a controllo di raccogliere una cartella da elaborare prima che la cartella venga copiata completamente nella cartella di input. Il valore predefinito è null.
È possibile utilizzare [pattern di file](../../forms/using/watched-folder-in-aem-forms.md#p-file-and-folder-patterns-p) da escludere:

   * File con estensioni di file specifiche; ad esempio, &#42;.dat, &#42;.xml, .pdf, &#42;.&#42;
   * File con nomi specifici; ad esempio, dati&#42; escluderebbe i file e le cartelle denominati data1, data2 e così via.
   * File con espressioni composite nel nome e nell&#39;estensione, come in questi esempi:

      * Dati[0-9][0-9][0-9].[dD][aA]&#39;port&#39;
      * &#42;.[dD][Aa]&#39;port&#39;
      * &#42;.[Xx][Mm][Ll]

Per ulteriori informazioni sui pattern di file, vedere [Informazioni sui pattern di file](../../forms/using/watched-folder-in-aem-forms.md#p-file-and-folder-patterns-p).

* **includeFilePattern (String)**: Un elenco delimitato da punti e virgola (;) di pattern utilizzati dalla cartella sottoposta a controllo per determinare le cartelle e i file da analizzare e raccogliere. Ad esempio, se viene specificato IncludeFilePattern&#42;, tutti i file e le cartelle corrispondenti all&#39;input&#42; vengono prelevati. Ciò include i file e le cartelle denominati input1, input2 e così via. Il valore predefinito è &#42; e indica tutti i file e le cartelle. È possibile utilizzare i pattern di file per includere:

   * File con estensioni di file specifiche; ad esempio, &#42;.dat, &#42;.xml, .pdf, &#42;.&#42;
   * File con nomi specifici; ad esempio, data.&#42; includerebbero file e cartelle denominati data1, data2 e così via.

* File con espressioni composite nel nome e nell&#39;estensione, come in questi esempi:

   * Dati[0-9][0-9][0-9].[dD][aA]&#39;port&#39;

      * &#42;.[dD][Aa]&#39;port&#39;
      * &#42;.[Xx][Mm][Ll]

Per ulteriori informazioni sui pattern di file, vedere [Informazioni sui pattern di file](../../forms/using/watched-folder-in-aem-forms.md#p-file-and-folder-patterns-p)

* **waitTime (Long)**: Tempo, in millisecondi, di attesa prima di eseguire la scansione di una cartella o di un file dopo la creazione. Ad esempio, se il tempo di attesa è di 3.600.000 millisecondi (un&#39;ora) e il file è stato creato un minuto fa, questo file verrà acquisito dopo 59 o più minuti passati. Il valore predefinito è 0. Questa impostazione è utile per garantire che un file o una cartella venga copiata completamente nella cartella di input. Ad esempio, se devi elaborare un file di grandi dimensioni e il download del file richiede dieci minuti, imposta il tempo di attesa su 10&#42;60 &#42;1000 millisecondi. In questo modo si impedisce alla cartella sottoposta a controllo di eseguire la scansione del file se non ha una durata di dieci minuti.
* **purgeDuration (Long)**: I file e le cartelle nella cartella dei risultati vengono eliminati quando sono più vecchi di questo valore. Questo valore viene misurato in giorni. Questa impostazione è utile per evitare che la cartella dei risultati diventi piena. Il valore -1 giorni indica di non eliminare mai la cartella dei risultati. Il valore predefinito è -1.
* **resultFolderName (String)**: Cartella in cui vengono archiviati i risultati salvati. Se i risultati non vengono visualizzati in questa cartella, controlla la cartella degli errori. I file di sola lettura non vengono elaborati e vengono salvati nella cartella degli errori. Questo valore può essere un percorso assoluto o relativo con i seguenti pattern di file:

   * %F = prefisso del nome del file
   * %E = estensione del nome file
   * %Y = anno (completo)
   * %y = anno (ultime due cifre)
   * %M = mese
   * %D = giorno del mese
   * %d = giorno dell&#39;anno
   * %H = ora (24 ore)
   * %h = ora (12 ore)
   * %m = minuto
   * %s = secondo
   * %l = millisecondi
   * %R = numero casuale (tra 0 e 9)
   * %P = ID processo o processo

   Ad esempio, se è alle 20 del 17 luglio 2009 e si specifica C:/Test/WF0/failed/%Y/%M/%D/%H/, la cartella dei risultati è C:/Test/WF0/failed/2009/07/17/20

   Se il percorso non è assoluto ma relativo, la cartella viene creata all’interno della cartella sottoposta a controllo. Il valore predefinito è risultato/%Y/%M/%D/, che è la cartella Risultato all&#39;interno della cartella controllata. Per ulteriori informazioni sui pattern di file, vedere [Informazioni sui pattern di file](../../forms/using/watched-folder-in-aem-forms.md#p-file-and-folder-patterns-p).

>[!NOTE]
>
>Minore è la dimensione delle cartelle dei risultati, migliore è l&#39;esecuzione della cartella osservata. Ad esempio, se il carico stimato per la cartella sottoposta a controllo è di 1000 file ogni ora, provare un pattern come risultato/%Y%M%D%H in modo che venga creata una nuova sottocartella ogni ora. Se il caricamento è più piccolo (ad esempio, 1000 file al giorno), è possibile utilizzare un pattern come risultato/%Y%M%D.

* **failedFolderName (String)**: Cartella in cui vengono salvati i file di errore. Questa posizione è sempre relativa alla cartella osservata. È possibile utilizzare i pattern di file, come descritto per Cartella risultati. I file di sola lettura non vengono elaborati e vengono salvati nella cartella degli errori. Il valore predefinito è Errore/%Y/%M/%D/.
* **preserveFolderName (String):** Il percorso in cui i file vengono memorizzati dopo l’elaborazione. Il percorso può essere assoluto, relativo o nullo. È possibile utilizzare i pattern di file, come descritto per Cartella risultati. Il valore predefinito è preserve/%Y/%M/%D/.
* **batchSize (Long)**: Numero di file o cartelle da raccogliere per scansione. Utilizzare per evitare un sovraccarico sul sistema; la scansione di troppi file alla volta può causare un arresto anomalo. Il valore predefinito è 2.

   Le impostazioni Intervallo di polling e Dimensione batch determinano il numero di file recuperati da Cartella osservata in ogni scansione. Cartella osservata utilizza un pool di thread Quartz per eseguire la scansione della cartella di input. Il pool di thread è condiviso con altri servizi. Se l’intervallo di scansione è piccolo, i thread eseguono spesso la scansione della cartella di input. Se i file vengono rilasciati frequentemente nella cartella controllata, è necessario mantenere l&#39;intervallo di scansione ridotto. Se i file vengono eliminati raramente, utilizza un intervallo di scansione più ampio in modo che gli altri servizi possano utilizzare i thread.

   Se c&#39;è un grande volume di file da eliminare, rendere la dimensione del batch grande. Ad esempio, se il servizio avviato dall&#39;endpoint Cartella sottoposta a controllo può elaborare 700 file al minuto e gli utenti rilasciano i file nella cartella di input allo stesso ritmo, impostando Dimensione batch su 350 e Intervallo di polling su 30 secondi, è possibile migliorare le prestazioni della Cartella sottoposta a controllo senza dover sostenere troppo spesso i costi di scansione della Cartella sottoposta a controllo.

   Quando i file vengono rilasciati nella cartella controllata, elenca i file nell’input, il che può ridurre le prestazioni se la scansione si verifica ogni secondo. L&#39;aumento dell&#39;intervallo di scansione può migliorare le prestazioni. Se il volume dei file da rilasciare è piccolo, regolare di conseguenza le dimensioni del batch e l&#39;intervallo di polling. Ad esempio, se vengono eliminati 10 file al secondo, provare a impostare pollInterval a 1 secondo e la dimensione batch a 10

* **throttleOn (booleano)**: Quando questa opzione è selezionata, limita il numero di processi delle cartelle esaminate elaborati da AEM Forms in un dato momento. Il numero massimo di processi è determinato dal valore Dimensione batch. Il valore predefinito è vero. (Vedi [Informazioni sulla limitazione](../../forms/using/watched-folder-in-aem-forms.md#p-about-throttling-p).)

* **overwriteDuplicateFilename (booleano)**: Se impostato su True, i file nella cartella dei risultati e nella cartella di conservazione vengono sovrascritti. Se impostato su False, il nome verrà utilizzato per i file e le cartelle con un suffisso di indice numerico. Il valore predefinito è False.
* **preserveOnFailure (booleano)**: Mantieni i file di input in caso di errore durante l&#39;esecuzione dell&#39;operazione su un servizio. Il valore predefinito è vero.
* **inputFilePattern (String)**: Specifica il pattern dei file di input per una cartella controllata. Crea un inserire nell&#39;elenco Consentiti dei file.
* **asynch (booleano)**: Identifica il tipo di chiamata come asincrono o sincrono. Il valore predefinito è true (asincrono). L’elaborazione dei file richiede risorse, mantieni il valore del flag di asincronia su true per evitare di soffocare il thread principale del processo di scansione. In un ambiente cluster, è fondamentale mantenere il flag true per abilitare il bilanciamento del carico per i file elaborati nei server disponibili. Se il flag è false, il processo di scansione tenta di eseguire l&#39;elaborazione di ciascun file/cartella di livello principale in sequenza all&#39;interno del proprio thread. Non impostare il flag su false senza un motivo specifico, ad esempio l&#39;elaborazione basata su un flusso di lavoro in una configurazione a server singolo.

>[!NOTE]
>
>Per progettazione, i flussi di lavoro sono asincroni. Anche se imposti il valore su false, i flussi di lavoro vengono avviati in modalità asincrona.

* **abilitato (booleano)**: Disattiva e attiva la scansione di una cartella sottoposta a controllo. Imposta abilitato su true per iniziare la scansione della cartella sottoposta a controllo. Il valore predefinito è vero.
* **payloadMapperFilter:** Quando una cartella è configurata come cartella controllata, viene creata una struttura di cartelle all’interno della cartella controllata. La struttura dispone di cartelle per fornire input, ricevere output (risultati), salvare dati per errori, conservare dati per processi a lunga durata e salvare dati per varie fasi. La struttura delle cartelle di una cartella sottoposta a controllo può fungere da payload dei flussi di lavoro incentrati su Forms. Una mappatura payload consente di definire la struttura di un payload che utilizza una cartella sottoposta a controllo per l’input, l’output e l’elaborazione. Ad esempio, se utilizzi la mappatura predefinita, associa il contenuto della cartella sottoposta a controllo con [carico utile]\input e [carico utile]\cartella di output. Sono disponibili due implementazioni di mappatore payload pronte all’uso. Se non hai [implementazione personalizzata](../../forms/using/watched-folder-in-aem-forms.md#creating-a-custom-payload-mapper-filter), utilizza un’implementazione standard:

   * **Mapper predefinito:** Utilizza il mappatore payload predefinito per mantenere il contenuto di input e output delle cartelle controllate in cartelle di input e output separate nel payload. Inoltre, nel percorso di payload di un flusso di lavoro, utilizza [carico utile]/input/ e [carico utile]/percorsi di output per recuperare e salvare il contenuto.

   * **Semplice mappatore del payload basato su file:** Utilizza il mappatore payload basato su file semplice per mantenere i contenuti di input e output direttamente nella cartella payload. Non crea alcuna gerarchia extra, come la mappatura predefinita.

### Parametri di configurazione personalizzati {#custom-configuration-parameters}

Insieme alle proprietà di configurazione di Watched Folder elencate sopra, puoi anche specificare parametri di configurazione personalizzati. I parametri personalizzati vengono passati al codice di elaborazione del file. Consente al codice di modificare il proprio comportamento in base al valore del parametro . Per specificare un parametro:

1. Accedi a CRXDE-Lite e naviga al nodo di configurazione Watched Folder.
1. Aggiungi un parametro di proprietà.&lt;property_name> nel nodo di configurazione della cartella controllata. Il tipo della proprietà può essere solo booleano, data, decimale, doppio, lungo e stringa. È possibile specificare proprietà a valore singolo e multiplo.

>[!NOTE]
>
>Se il tipo di dati della proprietà è Double, specificare un punto decimale nel valore di tali proprietà. Per tutte le proprietà, in cui il tipo di dati è Double e nel valore non è specificato alcun punto decimale, il tipo viene convertito in Long.

Queste proprietà vengono passate come mappa immutabile di tipo Mappa&lt;string object=&quot;&quot;> al codice di elaborazione. Il codice di elaborazione può essere uno script ECMAS, un flusso di lavoro o un servizio. I valori forniti per le proprietà sono disponibili come coppie chiave-valore nella mappa. Chiave è il nome della proprietà e il valore è il valore della proprietà. Per ulteriori informazioni sui parametri di configurazione personalizzati, consulta la seguente immagine:

![Un esempio di nodo di configurazione della cartella di controllo con proprietà obbligatorie, alcune proprietà facoltative, alcuni parametri di configurazione](assets/custom-configuration-parameters.png)

Un nodo di configurazione della cartella di controllo di esempio con proprietà obbligatorie, alcune proprietà facoltative, alcuni parametri di configurazione.

#### Variabili mutabili per flussi di lavoro {#mutable-variables-for-workflows}

Puoi creare variabili mutabili per i metodi di elaborazione dei file basati su flusso di lavoro. Queste variabili fungono da contenitori per lo scorrimento dei dati tra i passaggi di un flusso di lavoro. Per creare tali variabili:

1. Accedi a CRXDE-Lite e naviga al nodo di configurazione Watched Folder.

1. Aggiungi una proprietà workflow.var.&lt;variable_name> nel nodo di configurazione della cartella controllata.

   Il tipo della proprietà può essere solo booleano, data, decimale, doppio, lungo e stringa. Sono supportate anche le proprietà con più valori. Per le proprietà con più valori, il valore disponibile per il passaggio del flusso di lavoro è una matrice di tipo specificato.

   >[!NOTE]
   >
   >Se il tipo di dati della proprietà è Double, specificare un punto decimale nel valore di tali proprietà. Per tutte le proprietà, in cui il tipo di dati è Double e nel valore non è specificato alcun punto decimale, il tipo viene convertito in Long.

>[!NOTE]
>
>La specifica JCR richiede un valore predefinito per le proprietà. I valori predefiniti sono disponibili per i passaggi di un flusso di lavoro per l’elaborazione. Quindi, specifica i valori predefiniti corretti.

![custom-configuration-parameters2](assets/custom-configuration-parameters2.png)

## Vari metodi di elaborazione dei file {#variousmethodsforprocessingfiles}

È possibile avviare un flusso di lavoro, un servizio o uno script per elaborare i documenti in una cartella di controllo.

### Utilizzo di un servizio per elaborare i file di una cartella osservata   {#using-a-service-to-process-files-of-a-watched-folder-nbsp}

Un servizio è un’implementazione personalizzata del `com.adobe.aemfd.watchfolder.service.api.ContentProcessor` interfaccia. È registrato con OSGi insieme ad alcune proprietà personalizzate. Le proprietà personalizzate dell’implementazione la rendono unica e facilitano l’identificazione dell’implementazione.

#### Implementazione personalizzata dell&#39;interfaccia ContentProcessor {#custom-implementation-of-the-contentprocessor-interface}

L’implementazione personalizzata accetta un contesto di elaborazione (un oggetto di tipo com.adobe.aemfd.watchfolder.service.api.ProcessorContext), legge i documenti di input e i parametri di configurazione dal contesto, elabora gli input e aggiunge l’output al contesto. ProcessorContext dispone delle seguenti API:

* **getWatchFolderId**: Restituisce l&#39;ID della cartella controllata.
* **getInputMap**: Restituisce una mappa di tipo Mappa. Le chiavi della mappa sono il nome del file di input e un oggetto documento contenente il contenuto del file. Utilizza l’API getinputMap per leggere i file di input.
* **getConfigParameters**: Restituisce una mappa immutabile di tipo Mappa. La mappa contiene i parametri di configurazione di una cartella osservata.

* **setResult**: L’implementazione di ContentProcessor utilizza l’API per scrivere il documento di output nella cartella dei risultati. È possibile fornire un nome per il file di output all&#39;API setResult. L’API potrebbe scegliere di utilizzare o ignorare il file fornito a seconda della cartella o del pattern di file di output specificato. Se viene specificato un pattern di cartelle, i file di output hanno nomi come descritto nei flussi di lavoro. Se viene specificato un pattern di file, i file di output hanno nomi come descritto nel pattern di file.

Ad esempio, il codice seguente è un’implementazione personalizzata dell’interfaccia ContentProcessor con una proprietà foo=bar personalizzata.

```java
@Component(metatype = true, immediate = true, label = "WF Test Service", description = "WF Test Service")
@Service(value = {OutputWriter.class, ContentProcessor.class})
@Property(name = "foo", value = "bar")
public class OutputWriter implements ContentProcessor {
```

Quando [configurazione di una cartella controllata](../../forms/using/watched-folder-in-aem-forms.md#p-create-watched-folder-configuration-node-p), se si specifica la proprietà inputProcessorId come (foo=bar) e la proprietà inputProcessorType come Service, il servizio di cui sopra (implementazione personalizzata) viene utilizzato per elaborare i file di input della Cartella controllata.

L’esempio seguente è anche un’implementazione personalizzata dell’interfaccia ContentProcessor . Nell&#39;esempio, il Servizio accetta i file di input, copia i file in una posizione temporanea e restituisce un oggetto documento con il contenuto del file. Il contenuto dell&#39;oggetto documento viene salvato nella cartella dei risultati. Il percorso fisico della cartella dei risultati è configurato nel [nodo di configurazione delle cartelle controllate](../../forms/using/watched-folder-in-aem-forms.md#p-create-watched-folder-configuration-node-p).

```java
@Component(immediate = true)
@Service(value = ContentProcessor.class)
@Property(name = "serviceSelector", value = "testProcessor1")
public class TestContentProcessor1 implements ContentProcessor {
    @Override
    public void processInputs(ProcessorContext context) throws Exception {
        Map.Entry<String, Document> e = context.getInputMap().entrySet().iterator().next();
        File f = new File((String) context.getConfigParameters().get("tempDir"),
                context.getConfigParameters().get("outPrefix") + e.getKey());
        e.getValue().copyToFile(f);
        context.setResult(f.getName(), new Document(f, true));
    }
}
```

### Utilizzo di script per elaborare i file di una cartella sottoposta a controllo {#using-scripts-to-process-files-of-a-watched-folder}

Gli script sono il codice personalizzato del reclamo ECMAScript scritto per elaborare i documenti inseriti nella cartella sottoposta a controllo. Uno script è rappresentato come un nodo JCR. Oltre alle variabili ECMAScript standard (log, sling e altro), lo Script dispone di una variabile processorContext. La variabile è di tipo ProcessorContext. ProcessorContext dispone delle seguenti API:

* **getWatchFolderId**: Restituisce l&#39;ID della cartella controllata.
* **getInputMap**: Restituisce una mappa di tipo Mappa. Le chiavi della mappa sono il nome del file di input e un oggetto documento contenente il contenuto del file. Utilizza l’API getinputMap per leggere i file di input.
* **getConfigParameters**: Restituisce una mappa immutabile di tipo Mappa. La mappa contiene i parametri di configurazione di una cartella osservata.
* **setResult**: L’implementazione di ContentProcessor utilizza l’API per scrivere il documento di output nella cartella dei risultati. È possibile fornire un nome per il file di output all&#39;API setResult. L’API potrebbe scegliere di utilizzare o ignorare il file fornito a seconda della cartella o del pattern di file di output specificato. Se viene specificato un pattern di cartelle, i file di output hanno nomi come descritto nei flussi di lavoro. Se viene specificato un pattern di file, i file di output hanno nomi come descritto nel pattern di file.

Il codice seguente è un esempio ECMAScript. Accetta i file di input, copia i file in una posizione temporanea e restituisce un oggetto documento con il contenuto del file. Il contenuto dell&#39;oggetto documento viene salvato nella cartella dei risultati. Il percorso fisico della cartella dei risultati è configurato nel [nodo di configurazione delle cartelle controllate](../../forms/using/watched-folder-in-aem-forms.md#p-create-watched-folder-configuration-node-p).

>[!NOTE]
>
>La cartella di output e il prefisso del nome del file vengono decisi in base ai parametri di configurazione delle cartelle controllate.

```java
var inputMap = processorContext.getInputMap();
var params = processorContext.getConfigParameters();
var entry = inputMap.entrySet().iterator().next();
var tempFile = new Packages.java.io.File(params.get("tempDir"), params.get("outPrefix") + entry.getKey());
entry.getValue().copyToFile(tempFile);
processorContext.setResult(tempFile.getName(), new Packages.com.adobe.aemfd.docmanager.Document(tempFile, true));
```

#### Posizione degli script e considerazioni sulla sicurezza {#location-of-scripts-and-security-considerations}

Per impostazione predefinita, viene fornita una cartella contenitore (/etc/fd/watchfolder/scripts) in cui i clienti possono inserire i propri script e l’utente predefinito del servizio utilizzato dal framework di cartelle di controllo dispone delle autorizzazioni necessarie per la lettura degli script da questo percorso.

Se si prevede di posizionare gli script in un percorso personalizzato, è probabile che l&#39;utente predefinito del servizio non disponga delle autorizzazioni di lettura sulla posizione personalizzata. Per tale scenario, esegui i seguenti passaggi per fornire le autorizzazioni necessarie per la posizione personalizzata:

1. Crea un utente di sistema a livello di programmazione o tramite la console https://&#39;[server]:[porta]&#39;/crx/explorer. È inoltre possibile utilizzare un utente di sistema esistente. È importante lavorare con gli utenti del sistema qui invece che con gli utenti normali.
1. Fornire le autorizzazioni di lettura all&#39;utente di sistema appena creato o esistente nel percorso personalizzato in cui sono memorizzati gli script. Puoi avere più posizioni personalizzate. Fornire almeno le autorizzazioni di lettura a tutte le posizioni personalizzate.
1. Nella console di configurazione Felix (/system/console/configMgr), individua la mappatura utente del servizio per le cartelle di controllo. Questa mappatura è simile a &#39;Mapping: adobe-aemds-core-watch-folder=...&#39;.
1. Fai clic sulla mappatura. Per la voce &#39;adobe-aemds-core-watch-folder:scripts=fd-service&#39;, cambia fd-service in ID dell&#39;utente di sistema personalizzato. Fai clic su Salva.

Ora è possibile utilizzare il percorso personalizzato configurato per salvare gli script.

### Utilizzo di un flusso di lavoro per elaborare i file di una cartella sottoposta a controllo {#using-a-workflow-to-process-files-of-a-watched-folder}

I flussi di lavoro consentono di automatizzare le attività di Experience Manager. I flussi di lavoro consistono in una serie di passaggi eseguiti in un ordine specifico. Ogni passaggio esegue un’attività distinta, ad esempio l’attivazione di una pagina o l’invio di un messaggio e-mail. I flussi di lavoro possono interagire con le risorse nell’archivio, gli account utente e i servizi Experience Manager. Pertanto, i flussi di lavoro possono coordinarsi in modo complicato.

* Prima di creare un flusso di lavoro, considera i seguenti punti:
* L&#39;output di un passaggio deve essere disponibile per tutti i passaggi successivi.
I passaggi devono essere in grado di aggiornare (o addirittura eliminare) gli output esistenti generati dai passaggi precedenti.
* Le variabili mutabili vengono utilizzate per far scorrere i dati dinamici personalizzati tra i passaggi.

Esegui i seguenti passaggi per elaborare i file utilizzando i flussi di lavoro:

1. Creare un’implementazione del `com.adobe.aemfd.watchfolder.workflow.api.WorkflowContextProcessor` interfaccia. È simile all’implementazione creata per un servizio.

   >[!NOTE]
   >
   >È possibile creare l&#39;implementazione completa interamente in ECMAScript.

1. In un passaggio di Workflow, individua il servizio OSGi di tipo com.adobe.aemfd.watchfolder.workflow.api.WorkflowContextService e chiama il metodo execute() del servizio con i seguenti argomenti.

   * Implementazione personalizzata dell&#39;interfaccia WorkflowContextProcessor
   * workItem
   * workflowSession
   * metadati

Se utilizzi il linguaggio di programmazione Java per implementare il flusso di lavoro, il motore del flusso di lavoro AEM fornisce valore per le variabili workItem, workflowSession e metadati. Queste variabili vengono passate come argomenti al metodo execute() dell’implementazione personalizzata di WorkflowProcess.

Se si utilizza ECMAScript per implementare il flusso di lavoro, il motore del flusso di lavoro AEM fornisce valore per le variabili graniteWorkItem, graniteWorkflowSession e metadati. Queste variabili vengono passate come argomenti al metodo WorkflowContextService.execute() .

L&#39;argomento to processWorkflowContext() è un oggetto di tipo com.adobe.aemfd.watchfolder.workflow.api.WorkflowContext. L&#39;interfaccia WorkflowContext dispone delle seguenti API per facilitare le considerazioni specifiche del flusso di lavoro di cui sopra:

* getWorkItem: Restituisce il valore della variabile WorkItem. Le variabili vengono passate al metodo WorkflowContextService.execute() .
* getWorkflowSession: Restituisce il valore della variabile WorkflowSession. Le variabili vengono passate al metodo WorkflowContextService.execute() .
* getMetadata: Restituisce il valore della variabile Metadata. Le variabili vengono passate al metodo WorkflowContextService.execute() .
* getImpittatoVariables: Restituisce una mappa dell&#39;oggetto di sola lettura che rappresenta le variabili impostate dai passaggi precedenti. Se una variabile non viene modificata in nessuno dei passaggi precedenti, viene restituito il valore predefinito specificato durante la configurazione della cartella sottoposta a controllo.
* getImpmitResults: Restituisce una mappa documento di sola lettura. La mappa rappresenta i file di output generati dai passaggi precedenti.
* setVariable: L&#39;implementazione di WorkflowContextProcessor utilizza la variabile per manipolare le variabili che rappresentano i dati dinamici personalizzati che scorrono tra i passaggi. Il nome e il tipo delle variabili sono identici al nome delle variabili specificate durante [configurazione della cartella controllata](../../forms/using/watched-folder-in-aem-forms.md#p-configure-the-watched-folder-p). Per modificare il valore di una variabile, invoca l’API setVariable con un valore non nullo. Per rimuovere una variabile, invoca setVariable() con un valore null.

Sono disponibili anche le seguenti API ProcessorContext:

* getWatchFolderId: Restituisce l&#39;ID della cartella controllata.
* getInputMap: Restituisce una mappa di tipo Mappa&lt;string document=&quot;&quot;>. Le chiavi della mappa sono il nome del file di input e un oggetto documento contenente il contenuto del file. Utilizza l’API getinputMap per leggere i file di input.
* getConfigParameters: Restituisce una mappa immutabile di tipo Mappa&lt;string object=&quot;&quot;>. La mappa contiene i parametri di configurazione di una cartella osservata.
* setResult: L’implementazione di ContentProcessor utilizza l’API per scrivere il documento di output nella cartella dei risultati. È possibile fornire un nome per il file di output all&#39;API setResult. L’API potrebbe scegliere di utilizzare o ignorare il file fornito a seconda della cartella o del pattern di file di output specificato. Se viene specificato un pattern di cartelle, i file di output hanno nomi come descritto nei flussi di lavoro. Se viene specificato un pattern di file, i file di output hanno nomi come descritto nel pattern di file

Considerazione per l’API setResult, se utilizzata nei flussi di lavoro:

* Per aggiungere un nuovo documento di output che contribuisce all’output del flusso di lavoro complessivo, invoca l’API setResult con un nome di file che non è stato utilizzato come nome di file di output da alcun passaggio precedente.
* Per aggiornare un output generato da un passaggio precedente, chiama l&#39;API setResult con un nome di file già utilizzato da un passaggio precedente.
* Per eliminare un output generato da un passaggio precedente, chiama setResult con un nome file già utilizzato da un passaggio precedente e null come contenuto.

>[!NOTE]
>
>Se si invoca l’API setResult con contenuto nullo in qualsiasi altro scenario, si verifica un errore.

L’esempio seguente viene implementato come passaggio del flusso di lavoro. Nell&#39;esempio, ECMAscript utilizza una variabile stepCount per tenere traccia del numero di volte in cui un passaggio viene chiamato nell&#39;istanza di flusso di lavoro corrente.
Il nome della cartella di output è una combinazione del numero del passaggio corrente, del nome del file originale e del prefisso specificato nel parametro outPrefix.

ECMAScript ottiene un riferimento al servizio di contesto del flusso di lavoro e crea un&#39;implementazione dell&#39;interfaccia WorkflowContextProcessor. L&#39;implementazione WorkflowContextProcessor accetta i file di input, copia il file in una posizione temporanea e restituisce un documento che rappresenta il file copiato. In base al valore della variabile booleana purgePrevious, il passaggio corrente elimina l&#39;output generato l&#39;ultima volta dallo stesso passaggio quando il passaggio è stato avviato nell&#39;istanza di flusso di lavoro corrente. Alla fine, viene richiamato il metodo wfSvc.execute per eseguire l’implementazione WorkflowContextProcessor . Il contenuto del documento di output viene salvato nella cartella dei risultati nel percorso fisico indicato nel nodo di configurazione Cartella controllata.

```javascript
log.error("Watch-folder workflow script called for step: " + graniteWorkItem.getNode().getTitle());
var wfSvc = sling.getService(Packages.com.adobe.aemfd.watchfolder.workflow.api.WorkflowContextService);
// Custom WorkflowContextProcessor implementation which defines the processWorkflowContext() method purely in JS
var impl = { processWorkflowContext: function (wfContext) {
    var wfId = wfContext.getWatchFolderId();
    var inputMap = wfContext.getInputMap();
    var paramMap = wfContext.getConfigParameters();
    var preResults = wfContext.getCommittedResults();
    var preVars = wfContext.getCommittedVariables();
    log.info("WF ID: " + wfId); // workflowId of type String
    log.info("Inputs: " + inputMap); // Input map of type Map<String, Document>
    log.info("Params: " + paramMap); // Config params of type Map<String, Object>
    log.info("Old results: " + preResults);
    log.info("Old variables: " + preVars);
    var currStepNumber = new Packages.java.lang.Long(new Packages.java.lang.Long(preVars.get("stepCount")).longValue() + 1);
    log.info("Current step number: " + currStepNumber);
    wfContext.setVariable("stepCount", currStepNumber);
    var entry = inputMap.entrySet().iterator().next();
    var tempFile = new Packages.java.io.File(paramMap.get("tempDir"), paramMap.get("outPrefix") + "STEP-" + currStepNumber + "-" + entry.getKey());
    entry.getValue().copyToFile(tempFile);
    var fName = tempFile.getName();
    var outDoc = new Packages.com.adobe.aemfd.docmanager.Document(tempFile, true);
    wfContext.setResult(tempFile.getName(), outDoc);
    var prevStepOutName = paramMap.get("outPrefix") + "STEP-" + (currStepNumber - 1) + "-" + entry.getKey();
    if (preResults.containsKey(prevStepOutName) && paramMap.get("purgePrevious").booleanValue()) {
        log.info("Purging previous step output " + prevStepOutName);
        wfContext.setResult(prevStepOutName, null);
    }
} }
wfSvc.execute(impl, graniteWorkItem, graniteWorkflowSession, metaData);
log.info("Exiting workflow script!")
```

### Crea filtro di mappatura payload per mappare la struttura di una cartella controllata al payload di un flusso di lavoro {#create-payload-mapper-filter-to-map-structure-of-a-watched-folder-to-the-payload-of-a-workflow}

Quando si crea una cartella controllata, viene creata una struttura di cartelle all’interno della cartella controllata. La struttura delle cartelle presenta cartelle di stage, risultato, mantenimento, input e errori. La struttura delle cartelle può fungere da payload di input per il flusso di lavoro e accettare l’output da un flusso di lavoro. Può inoltre elencare eventuali punti di errore.

Se la struttura di un payload è diversa dalla struttura della cartella controllata, è possibile scrivere script personalizzati per mappare la struttura della cartella controllata al payload. Tale script si chiama filtro di mappatura payload. Con AEM Forms è disponibile un filtro di mappatura payload per mappare la struttura della cartella controllata a un payload.

#### Creazione di un filtro di mappatura payload personalizzato {#creating-a-custom-payload-mapper-filter}

1. Scarica [Adobe Client SDK](https://repo1.maven.org/maven2/com/adobe/aemfd/aemfd-client-sdk/).
1. Imposta l’SDK client nel percorso di creazione del progetto basato su Maven. Per iniziare, puoi scaricare e aprire il seguente progetto basato su Maven nell’IDE che preferisci.
1. Modifica il codice del filtro mappatore payload disponibile nel bundle di esempio in base alle tue esigenze.
1. Utilizza maven per creare un bundle del filtro Payload Mapper personalizzato.
1. Utilizzo [Console AEM bundle](https://localhost:4502/system/console/bundles) per installare il bundle.

   Ora, il filtro di mappatura payload personalizzato è elencato nell’interfaccia utente AEM cartelle controllate. Puoi utilizzarlo con il tuo flusso di lavoro.

   Nell&#39;esempio seguente viene implementata una semplice mappatura basata su file per i file salvati in relazione a un payload. Puoi usarlo per iniziare.

   ```java
   package com.adobe.aemfd.watchfolder.workflow;
   import com.adobe.aemfd.docmanager.Document;
   import com.adobe.aemfd.watchfolder.workflow.api.payload.PayloadMapper;
   import com.adobe.aemfd.watchfolder.workflow.api.payload.WorkflowExecutionContext;
   import com.adobe.aemfd.watchfolder.workflow.api.payload.WorkflowInitializationContext;
   import com.adobe.aemfd.watchfolder.workflow.api.payload.WorkflowVariable;
   import com.adobe.granite.workflow.exec.Workflow;
   import org.apache.felix.scr.annotations.Component;
   import org.apache.felix.scr.annotations.Service;
   import org.apache.sling.api.resource.ResourceResolver;
   import javax.jcr.Binary;
   import javax.jcr.Node;
   import java.util.Collection;
   import java.util.HashMap;
   import java.util.Map;
   @Component(immediate = true)
   @Service(value = PayloadMapper.class)
   public class SimpleFileBasedPayloadMapper implements PayloadMapper {
   @Override
   public Node createPayload(WorkflowInitializationContext wfInitCtxt, Node stagingFolder, String uniquePayloadName,
   Map<String, Binary> inputs, Collection<WorkflowVariable> variableDefs) throws Exception {
   Node dirNode = stagingFolder.addNode(uniquePayloadName, "sling:Folder");
   for (Map.Entry<String, Binary> bins: inputs.entrySet()) {
   Node fileNode = dirNode.addNode(bins.getKey(), "nt:file");
   Node resNode = fileNode.addNode ("jcr:content", "nt:resource");
   resNode.setProperty("jcr:data", bins.getValue());
   }
   return dirNode;
   }
   @Override
   public Map<String, Document> getInputs(WorkflowInitializationContext wfInitCtxt, WorkflowExecutionContext wfExecCtxt,
   Node payload, ResourceResolver resourceResolver) throws Exception {
   return null; //To change body of implemented methods use File | Settings | File Templates.
   }
   @Override
   public void setOutput(WorkflowInitializationContext wfInitCtxt, WorkflowExecutionContext wfExecCtxt, Node payload,
   String fileName, Binary contents, int outputMode) throws Exception {
   //To change body of implemented methods use File | Settings | File Templates.
   }
   @Override
   public Map<String, Document> getIntermediateOutputs(WorkflowInitializationContext wfInitCtxt,
   WorkflowExecutionContext wfExecCtxt, Node payload,
   ResourceResolver resourceResolver) throws Exception {
   return null; //To change body of implemented methods use File | Settings | File Templates.
   }
   @Override
   public Map<String, Document> getFinalOutputs(WorkflowInitializationContext wfInitCtxt, Workflow workflow, Node payload,
   ResourceResolver resourceResolver) throws Exception {
   Map<String, Object> params = wfInitCtxt.getConfigParameters();
   Map<String, Document> result = new HashMap<String, Document>();
   for (Map.Entry<String, Object> me: params.entrySet()) {
   String key = me.getKey();
   if (key.startsWith("pm.outfile.")) {
   String fName = (String) me.getValue();
   Document d = new Document(payload.getPath() + "/" + fName, resourceResolver);
   result.put(fName, d);
   }
   }
   return result;
   }
   @Override
   public void setVariable(WorkflowInitializationContext wfInitCtxt, WorkflowExecutionContext wfExecCtxt, Node payload,
   WorkflowVariable variable) throws Exception {
   //To change body of implemented methods use File | Settings | File Templates.
   }
   @Override
   public Map<String, Object> getVariables(WorkflowInitializationContext wfInitCtxt, WorkflowExecutionContext wfExecCtxt,
   Node payload) throws Exception {
   return null; //To change body of implemented methods use File | Settings | File Templates.
   }
   }
   ```

## Interazione degli utenti con una cartella sottoposta a controllo {#how-users-interact-with-a-watched-folder}

Per un endpoint per cartelle controllate, gli utenti possono avviare le operazioni di elaborazione dei file copiando o trascinando i file o le cartelle di input dal proprio desktop in una cartella controllata. I file vengono elaborati in ordine di arrivo.

Per gli endpoint per cartelle controllate, se un processo richiede un solo file di input, l&#39;utente può copiare tale file nella directory principale della cartella controllata.

Se il processo contiene più di un file di input, l’utente deve creare una cartella al di fuori della gerarchia delle cartelle controllate che contiene tutti i file richiesti. Questa nuova cartella deve includere i file di input (ed eventualmente un file DDX, se richiesto dal processo). Dopo la creazione della cartella di lavoro, l’utente la copia nella cartella di input della cartella sottoposta a controllo.

>[!NOTE]
>
>Assicurati che il server applicazioni abbia eliminato l&#39;accesso ai file nella cartella controllata. Se AEM Forms non è in grado di eliminare i file dalla cartella di input dopo la scansione, il processo associato verrà avviato indefinitamente.

## Informazioni aggiuntive sulle cartelle controllate {#additional-information-about-the-watched-folders}

### Informazioni sulla limitazione {#about-throttling}

Quando la limitazione è abilitata per un endpoint della cartella di controllo, limita il numero di processi della cartella di controllo elaborati in un dato momento. Il numero massimo di processi è determinato dal valore Dimensione batch, configurabile anche nell&#39;endpoint Cartella controllata. Al raggiungimento del limite di limitazione, i documenti in entrata nella directory di input della cartella sottoposta a controllo non vengono sottoposti a polling. Il documento rimane anche nella directory di input fino al completamento di altri processi Cartella osservata e viene effettuato un altro tentativo di sondaggio. Per l’elaborazione sincrona, tutti i processi elaborati in un singolo poll vengono conteggiati verso il limite di limitazione, anche se i processi vengono elaborati consecutivamente in un singolo thread.

>[!NOTE]
>
>La limitazione non viene ridimensionata con un cluster. Quando la limitazione è abilitata, il cluster nel suo insieme non elaborerà più del numero di processi specificati in Dimensione batch in un dato momento. Questo limite è a livello di cluster e non è specifico per ogni nodo del cluster. Ad esempio, con una dimensione batch pari a 2, è possibile raggiungere il limite di limitazione con un singolo nodo che elabora due processi e nessun altro nodo esegue il polling della directory di input fino al completamento di uno dei processi.

#### Come funziona la limitazione {#how-throttling-works}

Cartella osservata esegue la scansione della cartella di input in ogni pollInterval, rileva il numero di file specificati in Dimensione batch e richiama il servizio di destinazione per ciascuno di questi file. Ad esempio, se la dimensione del batch è quattro, ad ogni scansione, la cartella sottoposta a controllo raccoglie quattro file, crea quattro richieste di chiamata e richiama il servizio di destinazione. Prima del completamento di queste richieste, se viene richiamata la cartella sottoposta a controllo, vengono avviati di nuovo quattro processi, indipendentemente dal fatto che i quattro processi precedenti siano stati completati o meno.

La limitazione impedisce alla cartella controllata di richiamare nuovi lavori quando i processi precedenti non sono stati completati. Cartella osservata rileva i lavori in corso ed elabora nuovi processi in base alla dimensione del batch meno i lavori in corso. Ad esempio, nella seconda invocazione, se il numero di processi completati è solo tre e un processo è ancora in corso, la cartella osservata richiama solo altri tre lavori.

* Cartella osservata si basa sul numero di file presenti nella cartella stage per scoprire quanti processi sono in corso. Se i file rimangono non elaborati nella cartella dell’area di visualizzazione, la cartella sottoposta a controllo non richiama altri processi. Ad esempio, se le dimensioni del batch sono quattro e tre processi sono in stallo, Cartella osservata richiama un solo processo nelle chiamate successive. Ci sono diversi scenari che possono far sì che i file rimangano non elaborati nella cartella stage. Quando i processi vengono bloccati, l&#39;amministratore può interrompere il processo nella pagina di amministrazione di Gestione processi in modo che Cartella controllata sposta i file fuori dalla cartella dell&#39;area di visualizzazione.
* Se il server AEM Forms si abbassa prima che la cartella Watched richiama i processi, l’amministratore può spostare i file fuori dalla cartella stage. Per informazioni, consulta [Punti di errore e ripristino](../../forms/using/watched-folder-in-aem-forms.md#p-failure-points-and-recoveryfailure-points-and-recovery-p).
* Se il server AEM Forms è in esecuzione ma la cartella Watched non è in esecuzione quando il servizio Job Manager effettua una chiamata di ritorno, che si verifica quando i servizi non si avviano nella sequenza ordinata, l’amministratore può spostare i file fuori dalla cartella stage. Per informazioni, consulta [Punti di errore e ripristino](../../forms/using/watched-folder-in-aem-forms.md#p-failure-points-and-recoveryfailure-points-and-recovery-p).

### Punti di errore e punti recoveryFailure e ripristino {#failure-points-and-recoveryfailure-points-and-recovery}

A ogni evento di sondaggio, Cartella osservata blocca la cartella di input, sposta i file che corrispondono al pattern di file di inclusione nella cartella stage e quindi sblocca la cartella di input. Il blocco è necessario in modo che due thread non raccolgano lo stesso set di file ed elaborarli due volte. Le probabilità che questo accada aumentano con un piccolo pollInterval e una grande dimensione batch. Una volta spostati i file nella cartella stage, la cartella di input viene sbloccata in modo che altri thread possano eseguire la scansione della cartella. Questo passaggio consente di fornire un throughput elevato perché altri thread possono eseguire la scansione mentre un thread elabora i file.

Una volta spostati i file nella cartella stage, vengono create richieste di chiamata per ogni file e viene richiamato il servizio di destinazione. Ci possono essere casi in cui la cartella Watched non può recuperare i file nella cartella stage:

* Se il server si spegne prima che la cartella Watched possa creare la richiesta di chiamata, i file nella cartella stage rimangono nella cartella stage e non vengono recuperati.

* Se la cartella Watched ha creato correttamente la richiesta di chiamata per ciascuno dei file nella cartella stage e il server si blocca, esistono due comportamenti in base al tipo di chiamata:

   * **Sincrono**: Se la cartella Watched è configurata per richiamare il servizio in modo sincrono, tutti i file nella cartella stage non vengono elaborati nella cartella stage.
   * **Asincrono**: In questo caso, Watched Folder si basa sul servizio Job Manager. Se il servizio Job Manager richiama la cartella Watched, i file nella cartella stage vengono spostati nella cartella preserve o failed in base ai risultati della chiamata. Se il servizio Job Manager non richiama la cartella osservata, i file rimarranno non elaborati nella cartella stage. Questa situazione si verifica quando la cartella osservata non è in esecuzione quando viene richiamato il Job Manager.

#### Recuperare i file di origine non elaborati nella cartella stage {#recover-unprocessed-source-files-in-the-stage-folder}

Se la cartella di controllo non è in grado di elaborare i file di origine nella cartella dell&#39;area di visualizzazione, è possibile recuperare i file non elaborati.

1. Riavvia il server applicazioni o il nodo.

1. Interrompe l&#39;elaborazione di nuovi file di input da parte della cartella di controllo. Se salti questo passaggio, sarà molto più difficile determinare quali file non vengono elaborati nella cartella stage. Per evitare che la cartella di controllo elabori nuovi file di input, eseguire una delle operazioni seguenti:

   * Modificare la proprietà includeFilePattern per la cartella Watched in modo che non corrisponda a nessuno dei nuovi file di input (ad esempio, immettere NOMATCH).
   * Sospendi il processo di creazione di nuovi file di input.

   Attendi che AEM Forms recuperi ed elabori tutti i file. La maggior parte dei file dovrebbe essere recuperata e tutti i nuovi file di input elaborati correttamente. Il tempo di attesa per il recupero e l&#39;elaborazione dei file da parte della cartella Watched dipenderà dalla lunghezza dell&#39;operazione da richiamare e dal numero di file da recuperare.

1. Determinare quali file non possono essere elaborati. Se hai aspettato un periodo di tempo appropriato e hai completato il passaggio precedente e nella cartella Stage sono ancora presenti file non elaborati, passa al passaggio successivo.

   >[!NOTE]
   >
   >È possibile esaminare la data e l’ora dei file nella directory stage. A seconda del numero di file e del tempo di elaborazione normale, è possibile determinare quali file sono abbastanza grandi da essere considerati bloccati.

1. Copia i file non elaborati dalla directory dell’area di visualizzazione nella directory di input.

1. Se nel passaggio 2 non è stato possibile elaborare nuovi file di input in Watched Folder, modificare Include File Pattern sul valore precedente o riattivare il processo disattivato.

### Cartelle controllate a catena {#chain-watched-folders-together}

Le cartelle controllate possono essere collegate tra loro in modo che un documento dei risultati di una cartella osservata sia il documento di input della cartella osservata successiva. Ogni cartella osservata può richiamare un servizio diverso. Configurando le cartelle controllate in questo modo, è possibile richiamare più servizi. Ad esempio, una cartella controllata può convertire i file PDF in Adobe PostScript® e una seconda cartella controllata può convertire i file PostScript in formato PDF/A. A questo scopo, imposta semplicemente la cartella dei risultati della cartella osservata definita dal primo endpoint in modo che punti alla cartella di input della cartella osservata definita dal secondo endpoint.

L&#39;output della prima conversione passerebbe a \path\result. L&#39;input per la seconda conversione sarebbe \path\result e l&#39;output della seconda conversione andrebbe a \path\result\result  (o la directory definita nella casella Cartella risultati per la seconda conversione).

### Pattern di file e cartelle {#file-and-folder-patterns}

Gli amministratori possono specificare il tipo di file che può richiamare un servizio. È possibile stabilire più pattern di file per ciascuna cartella sottoposta a controllo. Un pattern di file può essere costituito da una delle seguenti proprietà:

* File con estensioni di nomi di file specifiche; ad esempio, &#42;.dat, &#42;.xml, .pdf, &#42;.&#42;
* File con nomi specifici; ad esempio, data.&#42;
* File con espressioni composite nel nome e nell&#39;estensione, come in questi esempi:

   * Dati[0-9][0-9][0-9].[dD][aA]&#39;port&#39;
   * &#42;.[dD][Aa]&#39;port&#39;
   * &#42;.[Xx][Mm][Ll]

* L’amministratore può definire il pattern di file della cartella di output in cui memorizzare i risultati. Per le cartelle di output (risultato, mantenimento e errore), l&#39;amministratore può specificare uno dei seguenti pattern di file:
* %Y = anno (completo)
* %y = anno (ultime due cifre)
* %M = mese,
* %D = giorno del mese,
* %d = giorno dell&#39;anno,
* %h = ora,
* %m = minuto,
* %s = secondo,
* %R = numero casuale compreso tra 0-9
* %J = Nome processo

Ad esempio, il percorso della cartella dei risultati potrebbe essere C:\Adobe\Adobe LiveCycle ES4\BarcodedForms\%y\%m\%d.

Le mappature dei parametri di output possono inoltre specificare pattern aggiuntivi, ad esempio:

* %F = Nome file di origine
* %E = Estensione nome file di origine

Se il pattern di mappatura del parametro di output termina con &quot;File.separator&quot; (che è il separatore di percorso), viene creata una cartella e il contenuto viene copiato in tale cartella. Se il pattern non termina con &quot;File.separator&quot;, il contenuto (file di risultato o cartella) viene creato con quel nome.

## Utilizzo di PDF Generator con una cartella osservata {#using-pdf-generator-with-a-watched-folder}

È possibile configurare una cartella sottoposta a controllo per avviare un flusso di lavoro, un servizio o uno script per elaborare i file di input. Nella sezione seguente verrà configurata una cartella sottoposta a controllo per avviare uno script ECMAScript. Per convertire i documenti di Microsoft Word (.docx) in documenti PDF, ECMAScript utilizzerà PDF Generator.

Esegui i seguenti passaggi per configurare una cartella osservata con PDF Generator:

1. [Creare uno script ECMAScript](../../forms/using/watched-folder-in-aem-forms.md#p-create-an-ecmascript-p)
1. [Creare un flusso di lavoro](../../forms/using/watched-folder-in-aem-forms.md#p-create-a-workflow-p)
1. [Configurare la cartella controllata](../../forms/using/watched-folder-in-aem-forms.md#p-configure-the-watched-folder-p)

### Creare uno script ECMAScript {#create-an-ecmascript}

ECMAScript utilizzerebbe l’API createPDF di PDF Generator per convertire i documenti Microsoft Word (.docx) in documenti PDF. Esegui i seguenti passaggi per creare lo script:

1. Apri CRXDE lite in una finestra del browser. L’URL è https://&#39;[server]:[porta]&quot;/crx/de.

1. Passa a /etc/workflow/scripts e crea una cartella denominata PDFG.

1. Nella cartella PDFG, crea un file denominato pdfg-openOffice-sample.ecma e aggiungi il seguente codice al file :

   ```javascript
   var wfSvc = sling.getService(Packages.com.adobe.aemfd.watchfolder.workflow.api.WorkflowContextService);
   // Custom ContentProcessor implementation which defines the processInputs() method purely in JS
   var impl = { processWorkflowContext: function (wrkfContext) {
   
     //  var logger = Packages.org.slf4j.LoggerFactory.getLogger("cmb-mergeandprint-sample.ecma");
                   var inputMap=wrkfContext.getInputMap();
   
                   var distiller = sling.getService(com.adobe.pdfg.service.api.DistillerService);
                   var generatePDF = sling.getService(com.adobe.pdfg.service.api.GeneratePDFService);
                   var pdfgConfig = sling.getService(com.adobe.pdfg.service.api.PDFGConfigService);
       var result = new Packages.java.util.HashMap();
       var entry = inputMap.entrySet().iterator().next();
       var pdfgOut = generatePDF.createPDF(entry.getValue(), ".docx", "Standard OpenOffice", "Standard", "No Security", null, null);
                   var convertedDoc = pdfgOut.get("ConvertedDoc");
   //   logger.info("SuccessFully saved the document to Ouput Node");
       wrkfContext.setResult(entry.getKey().substring(0, entry.getKey().lastIndexOf('.'))+".pdf",convertedDoc); // Ownership flag set to true for auto temp-file deletion.
   
   } }
   
   wfSvc.execute(impl, graniteWorkItem, graniteWorkflowSession, metaData);
   ```

1. Salva e chiudi il file 

### Creare un flusso di lavoro {#create-a-workflow}

1. Apri AEM’interfaccia utente del flusso di lavoro in una finestra del browser.
   <https://[servername>]: &#39;port&#39;/workflow

1. Nella visualizzazione Modelli, fai clic su **Nuovo**. Nella finestra di dialogo Nuovo flusso di lavoro, specifica **Titolo** e fai clic su **OK**.

   ![create-a-workflow-pdf](assets/create-a-workflow-pdf.png)

1. Seleziona il flusso di lavoro appena creato e fai clic su **Modifica**. Il flusso di lavoro si apre in una nuova finestra.

1. Elimina il passaggio del flusso di lavoro predefinito. Trascina il Passaggio processo dalla barra laterale al flusso di lavoro.

   ![create-a-workflow-pdf2](assets/create-a-workflow-pdf2.png)

1. Fai clic con il pulsante destro del mouse sul passaggio del processo e seleziona **Modifica**. Viene visualizzata la finestra Proprietà passaggio.

1. Nella scheda Processo, selezionare ECMAScript. Ad esempio, lo script pdfg-openOffice-sample.ecma creato in [Creare uno script ECMAScript](#p-create-an-ecmascript-p). Abilita la **Avanzamento gestore** e fai clic su **OK**.

   ![create-a-workflow3-pdf](assets/create-a-workflow3-pdf.png)

### Configurare la cartella controllata {#configure-the-watched-folder}

1. Apri CRXDE lite in una finestra del browser. https://&#39;[server]:[porta]&quot;/crx/de/

1. Passa alla cartella /etc/fd/watchfolder/config/ e crea un nodo di tipo nt:unstructured.

   ![configure-the-watch-folder-pdf](assets/configure-the-watched-folder-pdf.png)

1. Aggiungi le seguenti proprietà al nodo :

   * folderPath (String): Percorso della cartella da analizzare a intervalli di tempo definiti. La cartella deve trovarsi in una posizione condivisa con tutti i server che dispongono dell&#39;accesso completo al server.
inputProcessorType (String): Il tipo di processo da avviare. In questa esercitazione, specifica il flusso di lavoro.

   * inputProcessorId (String): Il comportamento della proprietà inputProcessorId si basa sul valore specificato per la proprietà inputProcessorType. In questo esempio, il valore della proprietà inputProcessorType è workflow. Quindi, per la proprietà inputProcessorId specifica il seguente percorso del flusso di lavoro PDFG: /etc/workflow/models/pdfg/jcr:content/model

   * outputFilePattern (String): Pattern del file di output. È possibile specificare una cartella o un pattern di file. Se viene specificato un pattern di cartelle, i file di output hanno nomi come descritto nei flussi di lavoro. Se viene specificato un pattern di file, i file di output hanno nomi come descritto nel pattern di file.
   Oltre alle proprietà obbligatorie menzionate in precedenza, anche le cartelle esaminate supportano alcune proprietà facoltative. Per un elenco completo e una descrizione delle proprietà facoltative, consulta [Proprietà delle cartelle controllate](#watchedfolderproperties).

## Problemi noti {#watched-folder-known-issues}

All&#39;avvio di AEM 6.5 Forms su JEE, i file iniziano ad essere elaborati prima che JBoss si avvii completamente e i file non vengono elaborati. Per evitarlo, prima di avviare JBoss, cancella tutte le cartelle controllate.
