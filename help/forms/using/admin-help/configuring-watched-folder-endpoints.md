---
title: Configurazione degli endpoint delle cartelle esaminate
seo-title: Configurazione degli endpoint delle cartelle esaminate
description: Scopri come configurare gli endpoint delle cartelle esaminate.
seo-description: Scopri come configurare gli endpoint delle cartelle esaminate.
uuid: 01fb5ff8-2071-44bd-9241-7d5d41a5b26e
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 761e7909-43ba-4642-bcfc-8d76f139b9a3
translation-type: tm+mt
source-git-commit: 2cf9dcf2e9cf71c54e19e2c6ee825c9a8f00a9b7
workflow-type: tm+mt
source-wordcount: '7174'
ht-degree: 0%

---


# Configurazione degli endpoint delle cartelle esaminate {#configuring-watched-folder-endpoints}

Un amministratore può configurare una cartella di rete, nota come *cartella controllata*, in modo che quando un utente inserisce un file (ad esempio un file PDF) nella cartella esaminata, venga richiamata un&#39;operazione di servizio configurata e il file venga manipolato. Dopo che il servizio ha eseguito l&#39;operazione specificata, salva il file modificato in una cartella di output specificata.

## Configurazione del servizio Cartella esaminata {#configuring-the-watched-folder-service}

Prima di configurare l’endpoint di una cartella esaminata, configurate il servizio Cartella esaminata. I parametri di configurazione del servizio Cartelle esaminate hanno due scopi:

* Per configurare gli attributi comuni a tutti gli endpoint di cartelle osservati
* Per fornire i valori predefiniti per tutti gli endpoint delle cartelle esaminate

Dopo aver configurato il servizio Cartelle esaminate, aggiungete un endpoint Cartella osservata per il servizio di destinazione. Quando si aggiunge l&#39;endpoint, si impostano valori, quali il nome del servizio e il nome dell&#39;operazione da richiamare quando i file o le cartelle vengono inseriti nella cartella di input del servizio di cartelle esaminate configurato. Per informazioni dettagliate sulla configurazione del servizio Cartelle esaminate, vedere [Impostazioni del servizio Cartelle esaminate](/help/forms/using/admin-help/configure-service-settings.md#watched-folder-service-settings).

## Creazione di una cartella esaminata {#creating-a-watched-folder}

Potete creare una cartella esaminata in due modi:

* Quando si configurano le impostazioni per un endpoint di cartella controllato, digitare il percorso completo della directory principale nella casella Percorso e aggiungere il nome della cartella esaminata da creare, come illustrato in questo esempio:
   `  C:\MyPDFs\MyWatchedFolder`Poiché la cartella MyWatchedFolder non esiste già, AEM moduli tenta di crearla in tale posizione.

* Creare una cartella nel file system prima di configurare un endpoint di cartella controllato, quindi digitare il percorso completo nella casella Percorso.

In un ambiente cluster, la cartella che verrà utilizzata come cartella esaminata deve essere accessibile, scrivibile e condivisa sul file system o sulla rete. In questo scenario, ogni istanza del server applicazione del cluster deve avere accesso alla stessa cartella condivisa.

In Windows, se il server applicazioni è in esecuzione come servizio, deve essere avviato con l&#39;accesso appropriato alla cartella condivisa in uno dei modi seguenti:

* Configurate il servizio del server applicazione Accedi come **parametro** per avviarlo come utente specifico con accesso appropriato alla cartella condivisa controllata.
* Configurate l&#39;opzione Start as Local System del servizio server applicazione per consentire al servizio di interagire con il desktop. Questa opzione richiede che la cartella condivisa controllata sia accessibile e scrivibile a tutti.

## Concatenamento delle cartelle esaminate {#chaining-together-watched-folders}

Le cartelle esaminate possono essere concatenate insieme in modo che un documento di risultato di una cartella esaminata sia il documento di input della cartella esaminata successiva. Ogni cartella esaminata può richiamare un servizio diverso. Configurando le cartelle esaminate in questo modo, è possibile richiamare più servizi. Ad esempio, una cartella esaminata potrebbe convertire i file PDF in  Adobe PostScript® e una seconda cartella esaminata potrebbe convertire i file PostScript in formato PDF/A. A questo scopo, è sufficiente impostare la cartella *result* della cartella esaminata definita dal primo endpoint per puntare alla cartella *input* della cartella esaminata definita dal secondo endpoint.

L&#39;output della prima conversione passa a \path\result. L&#39;input per la seconda conversione è \path\result, e l&#39;output dalla seconda conversione va a \path\result\result  (o la directory definita nella casella Cartella risultati per la seconda conversione).

## Interazione degli utenti con le cartelle esaminate {#how-users-interact-with-watched-folders}

Per un endpoint di cartelle controllato, gli utenti possono richiamare copiando o trascinando i file o le cartelle di input dal desktop a una cartella controllata. I file verranno elaborati nell&#39;ordine in cui arrivano.

Per gli endpoint delle cartelle esaminate, se il processo richiede un solo file di input, l&#39;utente può copiare tale file nella directory principale della cartella esaminata.

Se il processo contiene più di un file di input, l’utente deve creare una cartella al di fuori della gerarchia delle cartelle esaminate che contenga tutti i file richiesti. Questa nuova cartella deve includere i file di input (e facoltativamente un file DDX, se richiesto dal processo). Una volta creata la cartella di processo, l’utente la copia nella cartella di input della cartella esaminata.

>[!NOTE]
>
>Verificate che il server applicazioni abbia eliminato l’accesso ai file nella cartella esaminata. Se AEM moduli non possono eliminare i file dalla cartella di input dopo la scansione, il processo associato verrà richiamato a tempo indeterminato.

## Output cartella esaminata {#watched-folder-output}

Se l&#39;input è una cartella e l&#39;output è costituito da più file, AEM moduli crea una cartella di output con lo stesso nome della cartella di input e copia i file di output in tale cartella. Quando l&#39;output è costituito da una mappa del documento contenente una coppia chiave-valore, ad esempio l&#39;output da un processo Output, la chiave verrà utilizzata come nome del file di output.

I nomi dei file di output risultanti da un processo endpoint non possono contenere caratteri diversi da lettere, numeri e un punto (.) prima dell&#39;estensione del file. AEM moduli converte altri caratteri nei relativi valori esadecimali.

Le applicazioni client raccolgono i documenti risultanti dalla cartella dei risultati della cartella esaminata. Gli errori di processo vengono registrati nella cartella degli errori della cartella esaminata.

## Funzionamento della cartella esaminata {#how-watched-folder-works}

Il modulo Cartella esaminata contiene i seguenti servizi:

* Servizio cartelle esaminate
* provider.file_scan_service
* provider.file_write_results_service

Oltre ai servizi elencati in precedenza, Cartella esaminata dipende anche da altri servizi, incluso il servizio Pianificazione per la pianificazione dei processi e il servizio Gestione processi per supportare la chiamata asincrona dei servizi di destinazione.

### Modalità di elaborazione di una richiesta di chiamata {#how-watched-folder-processes-an-invocation-request} in una cartella esaminata

Il servizio Cartelle esaminate gestisce la creazione, l&#39;aggiornamento e l&#39;eliminazione degli endpoint. Dopo che l&#39;amministratore ha creato gli endpoint, è pianificato che vengano attivati dal servizio di pianificazione in base all&#39;intervallo di ripetizione o all&#39;espressione cron specificata.

Questo diagramma illustra il modo in cui la cartella esaminata elabora una richiesta di chiamata.

![en_watchedfolder](assets/en_watchedfolder.png)

Il processo di richiamo di un servizio utilizzando le cartelle esaminate è il seguente:

1. Un&#39;applicazione client inserisce i file o le cartelle nella cartella di input della cartella esaminata.
1. Quando si verifica l&#39;intervallo di scansione del processo, il servizio Scheduler richiama provider.file_scan_service per elaborare i file o le cartelle nella cartella di input.
1. Provider.file_scan_service esegue le seguenti attività:


   * Esegue l&#39;analisi della cartella di input per i file o le cartelle che corrispondono al pattern di file include ed esclude i file o le cartelle per il pattern di file escluso specificato. I file o le cartelle meno recenti vengono estratti per primi. Vengono inoltre raccolti i file e le cartelle meno recenti del tempo di attesa. In una sola scansione, il numero di file o cartelle elaborati dipende dalla dimensione del batch. Per informazioni sui pattern di file, vedere [Informazioni sui pattern di file](configuring-watched-folder-endpoints.md#about-file-patterns). Per informazioni sull&#39;impostazione della dimensione batch, vedere [Impostazioni del servizio Cartella esaminata](/help/forms/using/admin-help/configure-service-settings.md#watched-folder-service-settings).
   * Raccoglie i file o le cartelle per l’elaborazione. Se i file o le cartelle non sono completamente scaricati, vengono raccolti nella scansione successiva. Per essere certi che le cartelle siano completamente scaricate, gli amministratori devono creare una cartella con un nome utilizzando il pattern di file di esclusione. Dopo che la cartella ha tutti i file, deve essere rinominata nel pattern specificato nel pattern di file include. Questo passaggio garantisce che la cartella contenga tutti i file necessari per richiamare il servizio. Per ulteriori informazioni su come garantire che le cartelle siano completamente scaricate, consultate [Suggerimenti e trucchi per le cartelle esaminate](configuring-watched-folder-endpoints.md#tips-and-tricks-for-watched-folders).
   * Sposta i file o le cartelle nella cartella dell’area di visualizzazione dopo averli selezionati per l’elaborazione.
   * Converte i file o le cartelle nella cartella dell’area di visualizzazione in un input appropriato in base alle mappature dei parametri di input dell’endpoint. Per esempi di mappature dei parametri di input, consultate [Suggerimenti e trucchi per le cartelle esaminate](configuring-watched-folder-endpoints.md#tips-and-tricks-for-watched-folders).


1. Il servizio di destinazione configurato per l&#39;endpoint viene richiamato in modo sincrono o asincrono. Il servizio di destinazione viene richiamato utilizzando il nome utente e la password configurati per l&#39;endpoint.

   * La chiamata sincrona chiama il servizio di destinazione direttamente e immediatamente gestisce la risposta.
   * Per la chiamata asincrona, il servizio di destinazione viene chiamato tramite il servizio Job Manager, che mette la richiesta in coda. Il servizio Job Manager, a sua volta, chiama il provider.file_write_result_service per gestire i risultati.

1. Provider.file_write_result_service gestisce la risposta o l&#39;errore della chiamata al servizio di destinazione. In caso di esito positivo, l&#39;output viene salvato nella cartella dei risultati in base alla configurazione dell&#39;endpoint. Provider.file_write_result_service mantiene l&#39;origine anche se l&#39;endpoint è configurato per mantenere i risultati al termine dell&#39;operazione.

   Quando la chiamata del servizio di destinazione genera un errore, il provider.file_write_Results_service registra il motivo dell&#39;errore in un file failure.log e inserisce il file nella cartella degli errori. La cartella di errore viene creata in base ai parametri di configurazione specificati per l&#39;endpoint. Quando l&#39;amministratore imposta l&#39;opzione Mantieni su errore per la configurazione dell&#39;endpoint, il provider.file_write_Results_service copia anche i file sorgente nella cartella degli errori. Per informazioni sul recupero dei file dalla cartella degli errori, vedere [Punti di errore e ripristino](configuring-watched-folder-endpoints.md#failure-points-and-recovery).


## Impostazioni endpoint cartella esaminata {#watched-folder-endpoint-settings}

Utilizzate le seguenti impostazioni per configurare un endpoint di cartella controllato.

**Nome:** (obbligatorio) Identifica l’endpoint. Non includete un carattere &lt; perché troncherà il nome visualizzato in Workspace. Se immettete un URL come nome dell’endpoint, accertatevi che sia conforme alle regole di sintassi specificate in RFC1738.

**Descrizione:** una descrizione dell’endpoint. Non includete un carattere &lt; perché troncherà la descrizione visualizzata in Workspace.

**Percorso:** (obbligatorio) Specifica il percorso della cartella esaminata. In un ambiente cluster, questa impostazione deve puntare a una cartella di rete condivisa accessibile da ogni computer del cluster.

**Asincrono:** identifica il tipo di chiamata come asincrono o sincrono. Il valore predefinito è asincrono. Asincrona è consigliato per i processi di lunga durata, mentre sincrono è consigliato per i processi transitori o di breve durata.

**Espressione cron:** inserite un&#39;espressione cron se la cartella esaminata deve essere pianificata utilizzando un&#39;espressione cron. Quando questa impostazione è configurata, l&#39;intervallo di ripetizione viene ignorato.

**Intervallo di ripetizione:** l’intervallo in secondi per la scansione della cartella esaminata per l’input. A meno che l’impostazione Limita non sia attivata, l’intervallo di ripetizione deve essere più lungo del tempo necessario per elaborare un processo medio; in caso contrario, il sistema potrebbe sovraccaricarsi. Il valore predefinito è 5. Per ulteriori informazioni, consultate la descrizione per Dimensione batch.

**Conteggio ripetizioni:** numero di volte in cui la cartella controllata esegue la scansione della cartella o della directory. Il valore -1 indica una scansione indefinita. Il valore predefinito è -1.

**Limitazione:** quando questa opzione è selezionata, limita il numero di processi di cartelle controllati che AEM i moduli vengono elaborati in un dato momento. Il numero massimo di processi è determinato dal valore Dimensione batch. (Vedere Informazioni sulla limitazione.)

**Nome utente:** (obbligatorio) Il nome utente utilizzato per richiamare un servizio di destinazione dalla cartella esaminata. Il valore predefinito è SuperAdmin.

**Nome dominio:** (obbligatorio) il dominio dell&#39;utente. Il valore predefinito è DefaultDom.

**Dimensione batch:** il numero di file o cartelle da raccogliere per scansione. utilizzare per evitare un sovraccarico del sistema; la scansione di troppi file alla volta può causare un arresto anomalo. Il valore predefinito è 2.

Le impostazioni Intervallo di ripetizione e Dimensione batch determinano quanti file vengono raccolti da Cartella esaminata in ogni scansione. Cartella esaminata utilizza un pool di thread Quartz per eseguire la scansione della cartella di input. Il pool di thread è condiviso con altri servizi. Se l&#39;intervallo di scansione è ridotto, i thread eseguiranno spesso la scansione della cartella di input. Se i file vengono rilasciati frequentemente nella cartella esaminata, è necessario mantenere l&#39;intervallo di scansione ridotto. Se i file vengono omessi raramente, usate un intervallo di scansione maggiore in modo che gli altri servizi possano usare i thread.

Se un grande volume di file viene eliminato, ingrandire la dimensione del batch. Ad esempio, se il servizio richiamato dall’endpoint delle cartelle esaminate può elaborare 700 file al minuto e gli utenti rilasciano i file nella cartella di input allo stesso ritmo, impostando quindi la dimensione batch su 350 e l’intervallo di ripetizione su 30 secondi sarà più facile per le prestazioni delle cartelle esaminate senza dover sostenere troppo spesso il costo di scansione della cartella esaminata.

Quando i file vengono rilasciati nella cartella esaminata, elenca i file nell&#39;input, il che può ridurre le prestazioni se la scansione avviene ogni secondo. Aumentare l&#39;intervallo di scansione può migliorare le prestazioni. Se il volume di file rilasciato è piccolo, regolare le dimensioni del batch e l&#39;intervallo di ripetizione di conseguenza. Ad esempio, se 10 file vengono eliminati ogni secondo, provate a impostare l’intervallo di ripetizione su 1 secondo e la dimensione del batch su 10.

**Tempo di attesa:** tempo, in millisecondi, di attesa prima di eseguire la scansione di una cartella o di un file al termine della creazione. Ad esempio, se il tempo di attesa è di 3.600.000 millisecondi (un&#39;ora) e il file è stato creato un minuto fa, questo file verrà recuperato dopo che sono passati 59 o più minuti. Il valore predefinito è 0.

Questa impostazione è utile per fare in modo che un file o una cartella venga copiato completamente nella cartella di input. Ad esempio, se si dispone di un file di grandi dimensioni da elaborare e il file richiede dieci minuti per il download, impostare il tempo di attesa su 10&amp;ast;60 &amp;ast;1000 millisecondi. In questo modo si evita che la cartella esaminata esegua la scansione del file se non ha una durata di dieci minuti.

**Escludi pattern di file:** un punto e virgola  **;elenco** delimitato di pattern utilizzati da una cartella esaminata per determinare quali file e cartelle acquisire. I file o le cartelle con questo pattern non verranno analizzati per l&#39;elaborazione.

Questa impostazione è utile quando l’input è una cartella con più file. Il contenuto della cartella può essere copiato in una cartella con un nome che verrà scelto dalla cartella esaminata. In questo modo si evita che la cartella esaminata raccolga una cartella da elaborare prima che la cartella venga completamente copiata nella cartella di input.

È possibile utilizzare i pattern di file per escludere:

* file con specifiche estensioni di file; ad esempio, &amp;ast;.dat, &amp;ast;.xml, &amp;ast;.pdf.
* File con nomi specifici; ad esempio, data.&amp;ast; escluderebbe i file e le cartelle denominati *data1*, *data2* e così via.
* File con espressioni composite nel nome e nell&#39;estensione, come negli esempi seguenti:

   * Data[0-9][0-9][0-9].[dD][aA]&#39;port
   * &amp;ast;.[dD][Aa]&#39;port
   * &amp;ast;.[Xx][Mm][Ll]

Per ulteriori informazioni sui pattern di file, vedere [Informazioni sui pattern di file](configuring-watched-folder-endpoints.md#about-file-patterns).

**Includi pattern file:** (obbligatorio) Un punto e virgola  **;un elenco** delimitato di pattern utilizzato dalla cartella esaminata per determinare le cartelle e i file da analizzare e raccogliere. Ad esempio, se il pattern di file Includi è input&amp;ast;, tutti i file e le cartelle che corrispondono a input&amp;ast; vengono prese. Sono inclusi file e cartelle denominati input1, input2 e così via.

Il valore predefinito è &amp;ast; e indica tutti i file e le cartelle.

È possibile utilizzare i pattern di file per includere:

* file con specifiche estensioni di file; ad esempio, &amp;ast;.dat, &amp;ast;.xml, &amp;ast;.pdf.
* File con nomi specifici; ad esempio, data.&amp;ast; includerebbe file e cartelle denominati *data1*, *data2* e così via.
* File con espressioni composite nel nome e nell&#39;estensione, come negli esempi seguenti:

   * Data[0-9][0-9][0-9].[dD][aA]&#39;port
   * &amp;ast;.[dD][Aa]&#39;port
   * &amp;ast;.[Xx][Mm][Ll]

Per ulteriori informazioni sui pattern di file, vedere [Informazioni sui pattern di file](configuring-watched-folder-endpoints.md#about-file-patterns).


**Cartella risultati:** la cartella in cui sono memorizzati i risultati salvati. Se i risultati non vengono visualizzati in questa cartella, controllare la cartella degli errori. I file di sola lettura non vengono elaborati e verranno salvati nella cartella degli errori. Questo valore può essere un percorso assoluto o relativo con i seguenti pattern di file:

* %F = prefisso del nome del file
* %E = estensione del nome del file
* %Y = anno (completo)
* %y = anno (ultime due cifre)
* %M = mese
* %D = giorno del mese
* %d = giorno dell&#39;anno
* %H = ora (24 ore)
* %h = ora (orologio da 12 ore)
* %m = minuto
* %s = secondo
* %l = millisecondi
* %R = numero casuale (tra 0 e 9)
* %P = ID processo o processo

Ad esempio, se il valore è alle 20 del 17 luglio 2009 e si specifica `C:/Test/WF0/failure/%Y/%M/%D/%H/`, la cartella dei risultati è `C:/Test/WF0/failure/2009/07/17/20`.

Se il percorso non è assoluto ma relativo, la cartella verrà creata all’interno della cartella esaminata. Il valore predefinito è result/%Y/%M/%D/, ovvero la cartella dei risultati all&#39;interno della cartella esaminata. Per ulteriori informazioni sui pattern di file, vedere [Informazioni sui pattern di file](configuring-watched-folder-endpoints.md#about-file-patterns).

>[!NOTE]
>
>Più piccole sono le dimensioni delle cartelle dei risultati, migliori saranno le prestazioni delle cartelle esaminate. Ad esempio, se il carico stimato per la cartella esaminata è di 1000 file ogni ora, provate a creare un pattern come `result/%Y%M%D%H` in modo che venga creata una nuova sottocartella ogni ora. Se il carico è minore (ad esempio, 1000 file al giorno), è possibile utilizzare un pattern come `result/%Y%M%D`.

**Mantieni cartella:** percorso in cui i file vengono memorizzati dopo l’analisi e la raccolta. Il percorso può essere assoluto, relativo o nullo. È possibile utilizzare i pattern di file, come descritto per Cartella risultati. Il valore predefinito è preserve/%Y/%M/%D/.

**Cartella degli errori:** la cartella in cui vengono salvati i file degli errori. Questo percorso è sempre relativo alla cartella esaminata. È possibile utilizzare i pattern di file, come descritto per Cartella risultati.

I file di sola lettura non vengono elaborati e verranno salvati nella cartella degli errori.

Il valore predefinito è failure/%Y/%M/%D/.

**Mantieni in caso di errore:** mantenere i file di input in caso di mancata esecuzione dell&#39;operazione su un servizio. Il valore predefinito è true.

**Sovrascrivi nomi file duplicati:** se è impostata su True, i file nella cartella dei risultati e nella cartella preserve vengono sovrascritti. Se è impostata su False, per il nome vengono utilizzati file e cartelle con un suffisso indice numerico. Il valore predefinito è False.

**Durata rimozione:** (Obbligatorio) I file e le cartelle nella cartella dei risultati vengono eliminati quando sono più vecchi di questo valore. Questo valore viene misurato in giorni. Questa impostazione è utile per evitare che la cartella dei risultati diventi piena.

Un valore pari a -1 giorni indica di non eliminare mai la cartella dei risultati. Il valore predefinito è -1.

**Nome operazione:** (obbligatorio) Elenco di operazioni che possono essere assegnate all’endpoint della cartella esaminata.

**Mappature parametri di input:** utilizzato per configurare l&#39;input richiesto per elaborare il servizio e il funzionamento. Le impostazioni disponibili dipendono dal servizio che utilizza l’endpoint delle cartelle esaminate. Di seguito sono elencati i due tipi di ingressi:

**Letterale:** nella cartella esaminata viene utilizzato il valore immesso nel campo così come viene visualizzato. Sono supportati tutti i tipi Java di base. Ad esempio, se un&#39;API utilizza input quali String, long, int e Boolean, la stringa viene convertita nel tipo corretto e il servizio viene richiamato.

**Variabile:** il valore immesso è un pattern di file utilizzato dalla cartella esaminata per selezionare l&#39;input. Ad esempio, nel caso del servizio di crittografia della password, dove il documento di input deve essere un file PDF, l&#39;utente può utilizzare &amp;ast;.pdf come pattern di file. La cartella controllata recupererà tutti i file nella cartella controllata che corrispondono a questo pattern e richiamerà il servizio per ogni file. Quando si utilizza una variabile, tutti i file di input vengono convertiti in documenti. Sono supportate solo le API che utilizzano Document come tipo di input.

**Mappature parametri di output:** utilizzato per configurare gli output del servizio e dell&#39;operazione. Le impostazioni disponibili dipendono dal servizio che utilizza l’endpoint delle cartelle esaminate.

L’output delle cartelle esaminate può essere un singolo documento, un elenco di documenti o una mappa di documenti. Questi documenti di output vengono quindi salvati nella cartella dei risultati, utilizzando il pattern specificato in Mapping parametri di output.

>[!NOTE]
>
>La specifica di nomi che generano nomi di file di output univoci migliora le prestazioni. Ad esempio, si consideri il caso in cui il servizio restituisca un documento di output e la mappatura dei parametri di output lo mappa su `%F.%E` (il nome del file e l&#39;estensione del file di input). In questo caso, se gli utenti rilasciano file con lo stesso nome ogni minuto, e la cartella dei risultati è configurata su `result/%Y/%M/%D`, e l&#39;impostazione Sovrascrivi nome file duplicato è disattivata, Cartella esaminata tenterà di risolvere i nomi di file duplicati. Il processo di risoluzione dei nomi di file duplicati può influire sulle prestazioni. In questa situazione, modificando il mapping dei parametri di output in `%F_%h_%m_%s_%l` per aggiungere ore, minuti, secondi e millisecondi al nome, oppure garantendo che i file rilasciati abbiano nomi univoci possa migliorare le prestazioni.

## Informazioni sui pattern di file {#about-file-patterns}

Gli amministratori possono specificare il tipo di file che può richiamare un servizio. È possibile stabilire più pattern di file per ciascuna cartella esaminata. Un pattern di file può essere una delle seguenti proprietà:

* File con estensioni di nomi file specifiche; ad esempio, &amp;ast;.dat, &amp;ast;.xml, &amp;ast;.pdf,;
* File con nomi specifici; ad esempio, data.&amp;ast;
* File con espressioni composite nel nome e nell&#39;estensione, come negli esempi seguenti:

   * Data[0-9][0-9][0-9].[dD][aA]&#39;port
   * &amp;ast;.[dD][Aa]&#39;port
   * &amp;ast;.[Xx][Mm][Ll]

L&#39;amministratore può definire il pattern di file della cartella di output in cui memorizzare i risultati. Per le cartelle di output (risultato, mantenimento e errore), l’amministratore può specificare uno dei seguenti pattern di file:

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

Ad esempio, il percorso della cartella dei risultati potrebbe essere `C:\Adobe\Adobe_Experience_Manager_forms\BarcodedForms\%y\%m\%d`.

Le mappature dei parametri di output possono inoltre specificare pattern aggiuntivi, ad esempio:

* %F = Nome file di origine
* %E = Estensione nome file di origine

Se il pattern di mappatura dei parametri di output termina con &quot;File.separator&quot; (che è il separatore di percorso), viene creata una cartella e il contenuto viene copiato in tale cartella. Se il pattern non termina con &quot;File.separator&quot;, il contenuto (file o cartella di risultati) viene creato con tale nome. Per ulteriori informazioni sulle mappature dei parametri di output, vedere [Suggerimenti e trucchi per le cartelle esaminate](configuring-watched-folder-endpoints.md#tips-and-tricks-for-watched-folders).

## Informazioni sulla limitazione {#about-throttling}

Quando la limitazione è abilitata per l’endpoint di una cartella di controllo, limita il numero di processi di cartelle controllati che possono essere elaborati in un dato momento. Il numero massimo di processi è determinato dal valore Dimensione batch, anch’esso configurabile nell’endpoint Cartella esaminata. I documenti in entrata nella directory di input della cartella esaminata non verranno sottoposti a polling quando viene raggiunto il limite di limitazione. I documenti rimarranno inoltre nella directory di input fino al completamento di altri processi di cartelle controllati e al successivo tentativo di sondaggio. Nel caso dell’elaborazione sincrona, tutti i processi elaborati in un singolo sondaggio vengono conteggiati verso il limite di limitazione, anche se i processi vengono elaborati consecutivamente in un singolo thread.

>[!NOTE]
>
>La limitazione non viene ridimensionata con un cluster. Quando la limitazione è attivata, il cluster nel suo insieme non elaborerà più del numero di processi specificato in Dimensione batch in un dato momento. Questo limite è a livello di cluster e non è specifico per ciascun nodo del cluster. Ad esempio, con una dimensione batch pari a 2, il limite di limitazione potrebbe essere raggiunto con un singolo nodo che elabora due processi, e nessun altro nodo eseguirebbe il polling della directory di input fino al completamento di uno dei processi.

### Funzionamento della limitazione {#how-throttling-works}

Cartella esaminata analizza la cartella di input in ogni intervallo di ripetizione, rileva il numero di file specificato in Dimensione batch e richiama il servizio di destinazione per ciascuno di questi file. Ad esempio, se la dimensione del batch è quattro, ad ogni scansione la cartella esaminata raccoglierà quattro file, creerà quattro richieste di chiamata e richiamerà il servizio di destinazione. Prima del completamento di queste richieste, se viene richiamata la cartella esaminata, verranno avviati di nuovo quattro processi, indipendentemente dal fatto che i quattro processi precedenti siano stati completati o meno.

La limitazione impedisce alla cartella esaminata di richiamare nuovi processi quando i processi precedenti non sono completati. La cartella esaminata rileva i processi in corso ed elabora i nuovi processi in base alle dimensioni del batch meno i processi in corso. Ad esempio, nella seconda chiamata, se il numero di processi completati è di soli tre e un processo è ancora in corso, Cartella esaminata richiama solo altri tre processi.

* La cartella esaminata si basa sul numero di file presenti nella cartella dell’area di visualizzazione per verificare quanti processi sono in corso. Se i file non vengono elaborati nella cartella dell’area di visualizzazione, la cartella esaminata non richiamerà altri processi. Ad esempio, se la dimensione del batch è pari a quattro e tre processi sono in stato di stallo, in Cartella esaminata verrà richiamato un solo processo nelle chiamate successive. Esistono diversi scenari in cui i file possono rimanere non elaborati nella cartella dell’area di visualizzazione. Quando i processi vengono bloccati, l’amministratore può terminare il processo nella pagina di amministrazione del flusso di lavoro dei moduli in modo che la cartella esaminata sposta i file fuori dalla cartella dell’area di visualizzazione.
* Se il server moduli va giù prima che la cartella esaminata possa richiamare i processi, l’amministratore può spostare i file fuori dalla cartella dell’area di visualizzazione. Per informazioni, vedere [Punti di errore e ripristino](configuring-watched-folder-endpoints.md#failure-points-and-recovery).
* Se il server dei moduli è in esecuzione ma la cartella esaminata non è in esecuzione quando il servizio Job Manager effettua una nuova chiamata, che si verifica quando i servizi non vengono avviati nella sequenza ordinata, l&#39;amministratore può spostare i file fuori dalla cartella dell&#39;area di visualizzazione. Per informazioni, vedere [Punti di errore e ripristino](configuring-watched-folder-endpoints.md#failure-points-and-recovery).


## Prestazioni e scalabilità {#performance-and-scalability}

La cartella esaminata può contenere un totale di 100 cartelle su un singolo nodo. Le prestazioni di Watched Folder dipendono dalle prestazioni del server dei moduli. Per le chiamate asincrone, le prestazioni dipendono maggiormente dal carico di sistema e dai processi che si trovano nella coda di Job Manager.

Le prestazioni delle cartelle esaminate possono essere migliorate aggiungendo nodi al cluster. I processi delle cartelle esaminate sono distribuiti tra i nodi del cluster in virtù del programma Quartz e, nel caso di richieste asincrone, dal servizio Job Manager. Tutti i processi vengono memorizzati nel database.

La cartella esaminata dipende dal servizio Pianificazione per la pianificazione, la disprogrammazione e la riprogrammazione dei processi. Sono disponibili altri servizi, come il servizio Gestione eventi, il servizio Gestione utenti e il servizio Fornitori e-mail, che condividono il pool di thread del servizio Scheduler. Questo può influire sulle prestazioni delle cartelle esaminate. Il tuning del pool di thread del servizio Scheduler sarà necessario quando tutti i servizi inizieranno a utilizzarlo.

## Cartelle esaminate in un cluster {#watched-folders-in-a-cluster}

In un cluster, la cartella esaminata dipende dal programma Quartz e dal servizio Job Manager per il bilanciamento del carico e il failover. Per ulteriori informazioni sul comportamento del cluster Quartz, vedere [Documentazione quarz](https://www.quartz-scheduler.org/documentation).

Cartella esaminata esegue le tre attività principali seguenti in ogni sondaggio:

* Digitalizzare la cartella
* Richiamo del servizio di destinazione
* Gestione dei risultati

Il comportamento di bilanciamento del carico e failover varia a seconda che la cartella esaminata sia configurata per la chiamata sincrona o asincrona.

### Cartella esaminata sincrona in un cluster {#synchronous-watched-folder-in-a-cluster}

Per le chiamate sincrone, il sistema di bilanciamento del carico Quartz decide quale nodo deve ricevere l’evento di polling. Il nodo che ottiene l&#39;evento di polling eseguirà tutte le attività: eseguire la scansione della cartella, richiamare il servizio di destinazione e gestire i risultati.

![en_synchwatchedfoldercluster](assets/en_synchwatchedfoldercluster.png)

Per le chiamate sincrone, quando un nodo non riesce, il pianificatore quarzo invia nuovi eventi di polling ad altri nodi. Le chiamate avviate sul nodo non riuscito andranno perse. Per ulteriori informazioni su come recuperare i file associati al processo non riuscito, vedere [Punti di errore e ripristino](configuring-watched-folder-endpoints.md#failure-points-and-recovery).


### Cartella osservata asincrona in un cluster {#asynchronous-watched-folder-in-a-cluster}

Per le chiamate asincrone, il sistema di bilanciamento del carico Quartz decide quale nodo riceverà l’evento di polling. Il nodo che ottiene l’evento di polling eseguirà la scansione della cartella di input e richiamerà il servizio di destinazione inserendo la richiesta nella coda del servizio Job Manager. Il sistema di bilanciamento del carico del servizio Job Manager, a sua volta, è responsabile per decidere quale nodo elaborerà la richiesta di chiamata. È possibile che anche se il nodo A ha creato la richiesta di chiamata, il nodo B finisca per elaborare la richiesta. Oppure, il nodo che ha avviato la richiesta di chiamata potrebbe anche finire per elaborare la richiesta.

![en_asincronchwatchedfoldercluster](assets/en_asynchwatchedfoldercluster.png)

Per le chiamate asincrone, quando un nodo non riesce, il pianificatore quarzo invia nuovi eventi di polling ad altri nodi. Le richieste di convocazione create sul nodo non riuscito si troveranno nella coda del servizio Job Manager e verranno inviate ad altri nodi per l&#39;elaborazione. I file per i quali non vengono create richieste di chiamata rimarranno nella cartella dell’area di visualizzazione. Per ulteriori informazioni su come recuperare i file associati al processo non riuscito, vedere [Punti di errore e ripristino](configuring-watched-folder-endpoints.md#failure-points-and-recovery).


## Punti di errore e ripristino {#failure-points-and-recovery}

A ogni evento di sondaggio, Cartella osservata blocca la cartella di input, sposta i file che corrispondono al pattern di file include nella cartella dell’area di visualizzazione, quindi sblocca la cartella di input. Il blocco è necessario in modo che due thread non raccolgano lo stesso set di file ed elaborino due volte. Le possibilità che ciò accada aumentano con un piccolo intervallo di ripetizione e una grande dimensione batch. Dopo aver spostato i file nella cartella dell’area di visualizzazione, la cartella di input viene sbloccata in modo che altri thread possano eseguire la scansione della cartella. Questo passaggio consente di ottenere un throughput elevato perché altri thread possono eseguire la scansione mentre un thread elabora i file.

Dopo aver spostato i file nella cartella dell’area di visualizzazione, vengono create richieste di chiamata per ciascun file e viene richiamato il servizio di destinazione. In alcuni casi la cartella esaminata non è in grado di recuperare i file nella cartella dell’area di visualizzazione:

* Se il server va giù prima che la cartella esaminata possa creare la richiesta di chiamata, i file nella cartella dell’area di visualizzazione rimangono nella cartella dell’area di visualizzazione e non vengono recuperati.
* Se la cartella esaminata ha creato correttamente la richiesta di chiamata per ciascuno dei file nella cartella dell’area di visualizzazione e si verificano gli arresti anomali del server, in base al tipo di chiamata sono disponibili due comportamenti:

**Sincronia:** se la cartella esaminata è configurata per richiamare il servizio in modo sincrono, tutti i file nella cartella dell’area di visualizzazione non vengono elaborati nella cartella dell’area di visualizzazione.

**Asincrono:** In questo caso, Cartella esaminata si basa sul servizio Job Manager. Se il servizio Job Manager richiama la cartella esaminata, i file nella cartella dell’area di visualizzazione vengono spostati nella cartella preserve o failure in base ai risultati della chiamata. Se il servizio Job Manager non richiama la cartella esaminata, i file non verranno elaborati nella cartella dell’area di visualizzazione. Questa situazione si verifica quando la cartella esaminata non è in esecuzione quando viene richiamato il manager del processo.

### Ripristino di file sorgente non elaborati nella cartella dell’area di visualizzazione {#recovering-unprocessed-source-files-in-the-stage-folder}

Se la cartella esaminata non è in grado di elaborare i file sorgente nella cartella dell’area di visualizzazione, è possibile recuperare i file non elaborati.

1. Riavviate il server applicazione o il nodo.
1. (Facoltativo) Interrompe l&#39;elaborazione di nuovi file di input da parte della cartella esaminata. Se saltate questo passaggio, sarà molto più difficile determinare quali file non vengono elaborati nella cartella dell’area di visualizzazione. Per evitare che la cartella esaminata elabori nuovi file di input, effettuare una delle seguenti operazioni:

   * In Applicazioni e servizi, modificare il parametro Includi pattern file per l&#39;endpoint della cartella esaminata in modo che non corrisponda ad alcun nuovo file di input (ad esempio, immettere `NOMATCH`).
   * Sospendere il processo di creazione di nuovi file di input.

   Attendere che AEM moduli recuperi ed elabori tutti i file. La maggior parte dei file dovrebbe essere recuperato e tutti i nuovi file di input elaborati correttamente. Il tempo di attesa per la cartella esaminata per recuperare ed elaborare i file dipenderà dalla lunghezza dell&#39;operazione da richiamare e il numero di file da recuperare.

1. Determinare quali file non possono essere elaborati. Se avete atteso un periodo di tempo adeguato e avete completato il passaggio precedente e se nella cartella dell’area di visualizzazione sono ancora presenti file non elaborati, passate al passaggio successivo.

   >[!NOTE]
   >
   >Potete vedere la data e l’ora dei file nella directory dell’area di visualizzazione. A seconda del numero di file e del tempo di elaborazione normale, è possibile determinare quali file sono abbastanza grandi da essere considerati bloccati.

1. Copiate i file non elaborati dalla directory dell’area di visualizzazione alla directory di input.
1. Se non è stato possibile elaborare i nuovi file di input nel passaggio 2 della cartella esaminata, modificare il pattern di file Includi nel valore precedente o riattivare il processo disabilitato.

## Considerazioni sulla sicurezza per le cartelle esaminate {#security-considerations-for-watched-folders}

Ogni cartella esaminata è configurata con un nome utente e una password. Queste credenziali vengono utilizzate quando si richiamano i servizi. La cartella esaminata si basa sul fatto che la cartella condivisa è protetta con il file system di protezione sottostante, in modo che solo il proprietario della cartella esaminata possa accedere alla cartella condivisa.

## Suggerimenti e trucchi per le cartelle esaminate {#tips-and-tricks-for-watched-folders}

Di seguito sono riportati alcuni suggerimenti e consigli per la configurazione dell’endpoint della cartella esaminata:

* Se in Windows è presente una cartella esaminata che elabora i file immagine, specificate i valori per l&#39;opzione Includi pattern file o Escludi pattern file per evitare che il file Thumbs.db generato automaticamente da Windows venga analizzato dalla cartella esaminata.
* Se viene specificata un&#39;espressione cron, l&#39;intervallo di ripetizione viene ignorato. L&#39;utilizzo dell&#39;espressione cron si basa sul sistema di programmazione dei processi open source Quartz, versione 1.4.0.
* Le dimensioni batch corrispondono al numero di file o cartelle che verranno raccolti in ogni scansione della cartella esaminata. Se la dimensione del batch è impostata su due e dieci file o cartelle vengono ignorati nella cartella di input della cartella esaminata, solo due verranno raccolti in ogni scansione. Nella scansione successiva, che si verificherà dopo il tempo specificato nell&#39;intervallo di ripetizione, i due file successivi verranno prelevati.
* Per i pattern di file, gli amministratori possono specificare espressioni regolari con il supporto di pattern di caratteri jolly per specificare i pattern di file. Cartella esaminata modifica l&#39;espressione regolare per supportare i pattern di caratteri jolly come &amp;ast;.&amp;ast; o &amp;ast;.pdf. Questi pattern wild card non sono supportati dalle espressioni regolari.
* Cartella esaminata analizza la cartella di input per l’input e non sa se il file o la cartella di origine viene completamente copiato nella cartella di input prima che inizi l’elaborazione del file o della cartella. Per fare in modo che il file o la cartella di origine sia completamente copiato nella cartella di input della cartella controllata prima che il file o la cartella venga prelevata, eseguire le operazioni seguenti:

   * Usa tempo di attesa, ovvero l’ora in millisecondi che la cartella esaminata attende dall’ultima modifica. Utilizzate questa funzione se disponete di file di grandi dimensioni da elaborare. Ad esempio, se il download di un file richiede 10 minuti, specificare il tempo di attesa come 10&amp;ast;60 &amp;ast;1000 millisecondi. In questo modo si evita che la cartella esaminata raccolga il file se non ha la stessa età di 10 minuti.
   * Utilizzare il pattern di file exclude e includere il pattern di file. Ad esempio, se il pattern di file di esclusione è `ex*` e il pattern di file di inclusione è `in*`, la cartella esaminata raccoglierà i file che iniziano con &quot;in&quot; e non recupererà i file che iniziano con &quot;ex&quot;. Per copiare file o cartelle di grandi dimensioni, rinominare innanzitutto il file o la cartella in modo che il nome inizi con &quot;ex&quot;. Dopo aver copiato completamente il file o la cartella denominata &quot;ex&quot; nella cartella esaminata, rinominatelo in &quot;in&amp;ast;&quot;.

* Usate la durata di eliminazione per mantenere pulita la cartella dei risultati. Cartella esaminata elimina tutti i file che sono più vecchi della durata indicata nella durata di eliminazione. La durata è espressa in giorni.
* Quando si aggiunge un endpoint cartella esaminata, dopo aver selezionato il nome dell&#39;operazione viene compilata la mappatura dei parametri di input. Per ogni input dell&#39;operazione, viene generato un campo di mappatura dei parametri di input. Di seguito sono riportati alcuni esempi di mappature dei parametri di input:

   * Per l&#39;input `com.adobe.idp.Document`: Se l&#39;operazione del servizio ha un input di tipo `Document`, l&#39;amministratore può specificare il tipo di mappatura come `Variable`. Cartella esaminata recupera l’input dalla cartella di input della cartella esaminata in base al pattern di file specificato per il parametro di input. Se l&#39;amministratore specifica `*.pdf` come parametro, ogni file con estensione .pdf verrà prelevato, convertito in `com.adobe.idp.Document` e richiamato il servizio.
   * Per l&#39;input `java.util.Map`: Se l&#39;operazione del servizio ha un input di tipo `Map`, l&#39;amministratore può specificare il tipo di mappatura come `Variable` e immettere un valore di mappatura con un pattern come `*.pdf`. Ad esempio, un servizio richiede una mappa di due oggetti `com.adobe.idp.Document` che rappresentano due file nella cartella di input, come 1.pdf e 2.pdf. Cartella esaminata crea una mappa con la chiave come nome file e il valore come `com.adobe.idp.Document`.
   * Per l&#39;input `java.util.List`: Se l&#39;operazione del servizio include un input di tipo Elenco, l&#39;amministratore può specificare il tipo di mappatura come `Variable` e immettere un valore di mappatura con un pattern come `*.pdf`. Quando i file PDF vengono eliminati nella cartella di input, la cartella esaminata crea un elenco degli oggetti `com.adobe.idp.Document` che rappresentano tali file e richiama il servizio di destinazione.
   * Per `java.lang.String`: L&#39;amministratore ha due opzioni. Innanzitutto, l&#39;amministratore può specificare il tipo di mappatura come `Literal` e immettere un valore di mappatura come stringa, ad esempio `hello.` Watched Folder richiamerà il servizio con la stringa `hello`. In secondo luogo, l&#39;amministratore può specificare il tipo di mappatura come `Variable` e immettere un valore di mappatura con un pattern come `*.txt`. In quest&#39;ultimo caso, i file con estensione .txt verranno letti come un documento forzato come una stringa per richiamare il servizio.
   * Java primitive type: L&#39;amministratore può specificare il tipo di mappatura come `Literal` e fornire il valore. La cartella esaminata richiamerà il servizio con il valore specificato.

* Cartella esaminata è progettata per lavorare con i documenti. Le uscite supportate sono `com.adobe.idp.Document`, `org.w3c.Document`, `org.w3c.Node`, nonché un elenco e una mappa di questi tipi. Qualsiasi altro tipo causerà un errore nella cartella degli errori.
* Se i risultati non si trovano nella cartella dei risultati, verificare se si è verificato un errore nella cartella dei risultati.
* Cartella esaminata funziona meglio se utilizzata in modalità asincrona. In questa modalità, Cartella esaminata inserisce la richiesta di chiamata nella coda e richiama nuovamente. La coda viene quindi elaborata in modo asincrono. Se l&#39;opzione Asincrona non è impostata, la cartella esaminata richiama il servizio di destinazione in modo sincrono e il motore di processo attende che il servizio venga completato con la richiesta e vengano prodotti i risultati. Se il servizio di destinazione impiega molto tempo per elaborare la richiesta, la cartella esaminata potrebbe presentare degli errori di timeout.
* La creazione di cartelle esaminate per le operazioni di importazione ed esportazione non consente l’astrazione delle estensioni dei nomi file. Quando si richiama il servizio di integrazione dati modulo utilizzando le cartelle esaminate, il tipo di estensione del nome file per il file di output potrebbe non corrispondere al formato di output previsto per il tipo di oggetto documento. Ad esempio, se il file di input in una cartella esaminata che richiama l’operazione di esportazione è un modulo XFA che contiene dati, l’output deve essere un file di dati XDP. Per ottenere un file di output con la corretta estensione del nome file, potete specificarlo nella mappatura dei parametri di output. In questo esempio, potete utilizzare %F.xdp per la mappatura dei parametri di output.
* La cartella esaminata può elaborare i file di input prima che vengano completamente copiati nella cartella. Il blocco dei file non è obbligatorio in UNIX così come in Windows. Per questo motivo, quando un file viene copiato in una cartella esaminata, la cartella esaminata potrebbe spostare il file nell’area di visualizzazione senza attendere il completamento della copia del file. Questo comportamento determina l&#39;elaborazione di solo una parte del file di input. Esistono attualmente due soluzioni alternative:

   * Soluzione 1

      1. Specificare un pattern per Escludi pattern file, ad esempio temp&amp;ast;.ps.
      1. Copiate i file che iniziano con temp (ad esempio, temp1.ps) nella cartella esaminata.
      1. Dopo aver copiato completamente il file nella cartella esaminata, rinominare il file in modo che corrisponda al pattern specificato per Includi pattern file. Watched Folder (Cartella esaminata) e quindi sposta il file completato nell&#39;area di visualizzazione.
   * Soluzione 2

      Se si conosce il tempo massimo necessario per copiare i file in una cartella esaminata, specificare il tempo in secondi per Tempo di attesa. La cartella esaminata attende quindi il tempo specificato prima di spostare il file nell’area di visualizzazione.

      Questo non è un problema per i file in Windows perché Windows blocca un file quando un thread è in fase di scrittura. Tuttavia, si tratta di un problema relativo alle cartelle in Windows. Per le cartelle, è necessario seguire i passaggi descritti in Soluzione 1.


* Se l&#39;attributo dell&#39;endpoint Mantieni nome cartella per la cartella esaminata è impostato su un percorso di directory null, la directory di gestione temporanea non viene eliminata come dovrebbe essere. La directory contiene ancora il file elaborato e la cartella temporanea.

## Suggerimenti specifici per il servizio per le cartelle esaminate {#service-specific-recommendations-for-watched-folders}

Per tutti i servizi, è necessario regolare la dimensione batch e l&#39;intervallo di ripetizione della cartella esaminata in modo che la frequenza con cui la cartella esaminata raccoglie nuovi file e cartelle da elaborare non superi la frequenza dei processi che possono essere elaborati dal server moduli AEM. I parametri effettivi da utilizzare possono variare a seconda del numero di cartelle esaminate configurate, dei servizi che utilizzano le cartelle esaminate e dell&#39;intensità dei processi nel processore.

### Genera raccomandazioni servizio PDF {#generate-pdf-service-recommendations}

* Il servizio Genera PDF può convertire un solo file alla volta per i seguenti tipi di file: Microsoft Word, Microsoft Excel, Microsoft PowerPoint, Microsoft Project, AutoCAD,  Adobe Photoshop®,  Adobe FrameMaker® e  Adobe PageMaker®. Si tratta di lavori a lungo termine; pertanto, accertatevi di mantenere le dimensioni del batch su un valore basso. Se nel cluster sono presenti più nodi, aumentate anche l’intervallo di ripetizione.
* Per i tipi di file PostScript (PS), Encapsulated PostScript (EPS) e di immagini, il servizio Genera PDF può elaborare diversi file in parallelo. È necessario ottimizzare attentamente la dimensione del pool di fagioli di sessione (che regola il numero di conversioni che verranno eseguite in parallelo) in base alla capacità del server e al numero di nodi nel cluster. Quindi aumentate la dimensione del batch in un numero uguale alla dimensione del pool di fagioli di sessione per i tipi di file che si sta tentando di convertire. La frequenza di polling deve essere determinata dal numero di nodi nel cluster; tuttavia, poiché il servizio Genera PDF elabora questi tipi di processi abbastanza velocemente, è possibile configurare l&#39;intervallo di ripetizione su un valore basso come 5 o 10.
* Anche se il servizio Genera PDF può convertire un solo file OpenOffice alla volta, la conversione è abbastanza veloce. La logica precedente per le conversioni di PS, EPS e immagini si applica anche alle conversioni di OpenOffice.
* Per abilitare la distribuzione uniforme del carico nel cluster, mantenere bassa la dimensione del batch e aumentare l&#39;intervallo di ripetizione.

### raccomandazioni del servizio moduli codici a barre {#barcoded-forms-service-recommendations}

* Per ottenere prestazioni ottimali durante l&#39;elaborazione di moduli con codice a barre (file di piccole dimensioni), immettere `10` per Dimensione batch e `2` per Intervallo di ripetizione.
* Quando molti file vengono inseriti nella cartella di input, possono verificarsi errori con file nascosti denominati *thumbs.db*. Si consiglia pertanto di impostare il pattern di file Includi per i file di inclusione sullo stesso valore specificato per la variabile di input (ad esempio, `*.tiff`). Ciò impedisce l&#39;elaborazione dei file DB da parte della cartella esaminata.
* Il valore Dimensione batch di `5` e Intervallo di ripetizione di `2` è in genere sufficiente perché il servizio Forms con codice a barre in genere richiede circa 0,5 secondi per elaborare un codice a barre.
* La cartella esaminata non attende che il motore di elaborazione finisca il processo prima che recuperi nuovi file o cartelle. Continua a eseguire la scansione della cartella esaminata e a richiamare il servizio di destinazione. Questo comportamento può sovraccaricare il motore, causando problemi di risorse e timeout. Assicurarsi di utilizzare l&#39;intervallo di ripetizione e le dimensioni batch per limitare l&#39;input della cartella esaminata. È possibile aumentare l&#39;intervallo di ripetizione e ridurre la dimensione del batch se esistono più cartelle esaminate o abilitare la limitazione sull&#39;endpoint. Per informazioni sulla limitazione, vedere [Informazioni sulla limitazione](configuring-watched-folder-endpoints.md#about-throttling).
* Cartella esaminata rappresenta l’utente specificato nel nome utente e nel nome di dominio. La cartella esaminata richiama il servizio come utente se richiamato direttamente o se il processo ha una durata limitata. Per un processo di lunga durata, il processo viene richiamato con il contesto di sistema. Gli amministratori possono impostare i criteri del sistema operativo per Cartella esaminata per determinare a quale utente consentire o negare l&#39;accesso.
* Utilizzare i pattern di file per organizzare risultati, errori e mantenere le cartelle. (Vedere [Informazioni sui pattern di file](configuring-watched-folder-endpoints.md#about-file-patterns).)

* Cartella esaminata si basa sul pianificatore quarz per la scansione delle cartelle esaminate. Il pianificatore quarzo dispone di un pool di thread per la scansione. Se l&#39;intervallo di ripetizione per la cartella esaminata è molto basso (&lt; 5 secondi) e la dimensione del batch è alta (> 2), può verificarsi una condizione di gara. Quando si verifica questa condizione, un file viene prelevato da due thread Quartz:

   * Uno dei thread trova il file e richiama il servizio di destinazione con il file.
   * Il secondo thread visualizza il file ma non riesce quando tenta di verificare se il file è valido (file di lettura o scrittura), causando errori falsi che indicano che il file non può essere elaborato perché è di sola lettura. Questo accade solo con un intervallo di ripetizione basso e una dimensione batch elevata.

