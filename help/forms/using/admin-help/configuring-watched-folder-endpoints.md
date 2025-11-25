---
title: Configurazione degli endpoint della cartella controllata
description: Scopri come configurare gli endpoint della cartella controllata. Se un documento viene inserito in una cartella controllata, viene richiamata un’operazione di servizio configurata che manipola il file.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.4/FORMS
exl-id: ec169a01-a113-47eb-8803-bd783ea2c943
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 07289e891399a78568dcac957bc089cc08c7898c
workflow-type: tm+mt
source-wordcount: '7168'
ht-degree: 99%

---

# Configurazione degli endpoint della cartella controllata {#configuring-watched-folder-endpoints}

Un amministratore può configurare una cartella di rete, nota come *cartella controllata*, in modo che, quando un utente inserisce un file (ad esempio un file PDF) nella cartella controllata, venga richiamata un’operazione di servizio configurata che manipola il file. Dopo che il servizio ha eseguito l’operazione specificata, salva il file modificato in una cartella di output specificata.

## Configurazione del servizio Cartella controllata {#configuring-the-watched-folder-service}

Prima di configurare un endpoint della cartella controllata, configura il servizio Cartella controllata. I parametri di configurazione del servizio Cartella controllata hanno due scopi:

* Configurare gli attributi comuni a tutti gli endpoint della cartella controllata
* Fornire valori predefiniti per tutti gli endpoint della cartella controllata

Dopo aver configurato il servizio Cartella controllata, aggiungi un endpoint della Cartella controllata per il servizio di destinazione. Quando aggiungi l’endpoint, puoi impostare valori quali il nome del servizio e il nome dell’operazione da richiamare quando i file o le cartelle vengono inseriti nella cartella di input del servizio Cartella controllata configurato. Per informazioni dettagliate sulla configurazione del servizio Cartella controllata, consulta [Impostazioni del servizio Cartella controllata](/help/forms/using/admin-help/configure-service-settings.md#watched-folder-service-settings).

## Creazione di una cartella controllata {#creating-a-watched-folder}

Puoi creare una cartella controllata nei due modi seguenti:

* Quando configuri le impostazioni per un endpoint di una cartella controllata, digita il percorso completo della directory principale nella casella Percorso e aggiungi il nome della cartella controllata da creare, come illustrato nell’esempio seguente:
  `  C:\MyPDFs\MyWatchedFolder`Poiché la cartella MyWatchedFolder non esiste, AEM Forms tenta di crearla nel percorso specificato.

* Crea una cartella nel file system prima di configurare un endpoint di una cartella controllata, quindi digita il percorso completo nella casella Percorso.

In un ambiente cluster, la cartella utilizzata come cartella controllata deve essere accessibile, scrivibile e condivisa nel file system o in rete. In questo scenario, ogni istanza del server applicazioni del cluster deve avere accesso alla stessa cartella condivisa.

In Windows, se il server applicazioni è in esecuzione come servizio, deve essere avviato con l’accesso appropriato alla cartella condivisa in uno dei modi seguenti:

* Configura il servizio del server applicazioni Accedi come **parametro** per iniziare come utente specifico con l’accesso appropriato alla cartella controllata condivisa.
* Configura l’opzione Avvia come sistema locale del servizio del server applicazioni per consentire al servizio di interagire con il desktop. Questa opzione richiede che la cartella controllata condivisa sia accessibile e scrivibile da tutti.

## Concatenamento di cartelle controllate {#chaining-together-watched-folders}

Le cartelle controllate possono essere concatenate in modo che il documento risultante di una cartella controllata sia il documento di input della cartella controllata successiva. Ogni cartella controllata può richiamare un servizio diverso. Configurando in questo modo le cartelle controllate, è possibile richiamare più servizi. Ad esempio, una cartella controllata può convertire i file PDF in Adobe PostScript® e una seconda cartella controllata può convertire i file PostScript in formato PDF/A. A questo scopo, imposta semplicemente la cartella *dei risultati* della cartella controllata definita dal primo endpoint in modo che punti alla cartella *input* della cartella controllata definita dal secondo endpoint.

L’output della prima conversione passerebbe a \path\result. L’input per la seconda conversione sarebbe \path\result e l’output della seconda conversione passerebbe a \path\result\result (oppure alla directory definita nella casella Cartella dei risultati per la seconda conversione).

## In che modo gli utenti interagiscono con le cartelle controllate {#how-users-interact-with-watched-folders}

Per un endpoint di una cartella controllata, gli utenti possono richiamare copiando o trascinando file o cartelle di input dai propri desktop a una cartella controllata. I file verranno elaborati nell’ordine in cui arrivano.

Per gli endpoint della cartella controllata, se il processo richiede un solo file di input, l’utente può copiare tale file nella directory principale della cartella controllata.

Se il processo contiene più di un file di input, l’utente deve creare una cartella al di fuori della gerarchia delle cartelle controllate che contenga tutti i file richiesti. Questa nuova cartella deve includere i file di input (e facoltativamente un file DDX se richiesto dal processo). Una volta creata la cartella dei processi, l’utente la copia nella cartella di input della cartella controllata.

>[!NOTE]
>
>Verifica che il server applicazioni abbia eliminato l’accesso ai file nella cartella controllata. Se AEM Forms non è in grado di eliminare i file dalla cartella di input dopo la scansione, il processo associato verrà richiamato per un tempo indefinito.

## Output della cartella controllata {#watched-folder-output}

Quando l’input è una cartella e l’output è costituito da più file, AEM Forms crea una cartella di output con lo stesso nome della cartella di input e copia i file di output in tale cartella. Quando l’output è costituito da una mappa documento contenente una coppia chiave-valore, ad esempio l’output di un processo di output, la chiave viene utilizzata come nome del file di output.

I nomi dei file di output risultanti da un processo di endpoint non possono contenere caratteri diversi da lettere, numeri e un punto (.) prima dell’estensione del file. AEM Forms converte gli altri caratteri nei rispettivi valori esadecimali.

Le applicazioni client prelevano i documenti risultanti dalla cartella dei risultati della cartella controllata. Gli errori di processo vengono registrati nella cartella degli errori della cartella controllata.

## Funzionamento della cartella controllata {#how-watched-folder-works}

Il modulo Cartella controllata contiene i seguenti servizi:

* Servizio cartella controllata
* provider.file_scan_service
* provider.file_write_results_service

Oltre ai servizi elencati in precedenza, la cartella controllata dipende anche da altri servizi, tra cui il servizio Modulo di pianificazione per la pianificazione dei processi e il servizio Gestione processi per supportare la chiamata asincrona dei servizi di destinazione.

### Elaborazione di una richiesta di chiamata da parte della cartella controllata {#how-watched-folder-processes-an-invocation-request}

Il servizio Cartella controllata gestisce la creazione, l’aggiornamento e l’eliminazione degli endpoint. Dopo che l’amministratore ha creato gli endpoint, questi vengono pianificati per essere attivati dal servizio Modulo di pianificazione in base all’intervallo di ripetizione o all’espressione cron specificati.

Questo diagramma illustra come la cartella controllata elabora una richiesta di chiamata.

![en_watchedfolder](assets/en_watchedfolder.png)

Il processo di chiamata di un servizio utilizzando le cartelle controllate è il seguente:

1. Un’applicazione client inserisce file o cartelle nella cartella di input della cartella controllata.
1. Quando si verifica l’intervallo di scansione del processo, il servizio Modulo di pianificazione richiama il provider.file_scan_service per elaborare i file o le cartelle nella cartella di input.
1. Il provider.file_scan_service esegue le seguenti operazioni:


   * Esegue la scansione della cartella di input per individuare i file o le cartelle che corrispondono al pattern del file di inclusione ed esclude i file o le cartelle per il modello di file di esclusione specificato. I file o le cartelle meno recenti vengono prelevati per primi. Vengono selezionati anche i file e le cartelle precedenti al tempo di attesa. In una scansione, il numero di file o cartelle elaborati dipende dalle dimensioni del batch. Per informazioni sui pattern di file, consulta [Informazioni sui pattern di file](configuring-watched-folder-endpoints.md#about-file-patterns). Per informazioni sull’impostazione della dimensione del batch, consulta [Impostazioni del servizio Cartelle controllate](/help/forms/using/admin-help/configure-service-settings.md#watched-folder-service-settings).
   * Raccoglie i file o le cartelle da elaborare. Se i file o le cartelle non vengono scaricati completamente, vengono rilevati nella scansione successiva. Per assicurarsi che le cartelle siano completamente scaricate, gli amministratori devono creare una cartella con un nome utilizzando il pattern del di esclusione. Una volta che la cartella contiene tutti i file, è necessario rinominarla in base al pattern specificato nel pattern del file di inclusione. Questo passaggio garantisce che la cartella disponga di tutti i file necessari per richiamare il servizio. Per ulteriori informazioni sulla verifica del completamento del download delle cartelle, consulta [Suggerimenti per le cartelle controllate](configuring-watched-folder-endpoints.md#tips-and-tricks-for-watched-folders).
   * Sposta i file o le cartelle nella cartella di staging dopo averli selezionati per l’elaborazione.
   * Converte i file o le cartelle nella cartella di staging all’input appropriato in base alle mappature dei parametri di input dell’endpoint. Per esempi di mappatura dei parametri di input, consulta [Suggerimenti per le cartelle controllate](configuring-watched-folder-endpoints.md#tips-and-tricks-for-watched-folders).


1. Il servizio di destinazione configurato per l’endpoint viene richiamato in modo sincrono o asincrono. Il servizio di destinazione viene richiamato utilizzando il nome utente e la password configurati per l’endpoint.

   * La chiamata sincrona chiama direttamente il servizio di destinazione e gestisce immediatamente la risposta.
   * Nella chiamata asincrona, il servizio di destinazione viene chiamato tramite il servizio Gestione processi, che inserisce la richiesta in una coda. Il servizio Gestione processi, a sua volta, chiama provider.file_write_results_service per la gestione dei risultati.

1. provider.file_write_results_service gestisce la risposta o l’errore della chiamata al servizio di destinazione. In caso di esito positivo, l’output viene salvato nella cartella dei risultati in base alla configurazione dell’endpoint. provider.file_write_results_service conserva anche l’origine se l’endpoint è configurato per conservare i risultati dopo il completamento.

   Quando la chiamata del servizio di destinazione genera un errore, provider.file_write_results_service registra il motivo dell’errore in un file failure.log e inserisce tale file nella cartella degli errori. La cartella degli errori viene creata in base ai parametri di configurazione specificati per l’endpoint. Quando l’amministratore imposta l’opzione Mantieni in caso di errore per la configurazione dell’endpoint, provider.file_write_results_service copia anche i file di origine nella cartella degli errori. Per informazioni sul ripristino dei file dalla cartella degli errori, consulta [Punti di errore e ripristino](configuring-watched-folder-endpoints.md#failure-points-and-recovery).


## Impostazioni endpoint cartella controllata {#watched-folder-endpoint-settings}

Utilizza le seguenti impostazioni per configurare un endpoint per le cartelle controllate.

**Nome:** (obbligatorio) identifica l’endpoint. Non includere un carattere &lt; o il nome visualizzato in Workspace verrà troncato. Se immetti come nome dell’endpoint un URL, accertati che sia conforme alle regole di sintassi specificate in RFC1738.

**Descrizione:** descrizione dell’endpoint. Non includere un carattere &lt; o la descrizione visualizzata in Workspace verrà troncata.

**Percorso:** (obbligatorio) specifica il percorso della cartella controllata. In un ambiente cluster, questa impostazione deve puntare a una cartella di rete condivisa accessibile da tutti i computer nel cluster.

**Asincrona:** identifica il tipo di chiamata come asincrona o sincrona. Il valore predefinito è asincrono. L’asincronia è consigliata per i processi di lunga durata, mentre la sincronia è consigliata per i processi transitori o di breve durata.

**Espressione Cron:** immetti un’espressione cron se la cartella controllata deve essere pianificata utilizzando un’espressione cron. Quando questa impostazione è configurata, l’Intervallo di ripetizione viene ignorato.

**Intervallo di ripetizione:** l’intervallo in secondi per l’analisi della cartella controllata per l’input. A meno che l’impostazione Limitazione non sia attivata, l’intervallo di ripetizione deve essere più lungo del tempo necessario per elaborare un processo medio. In caso contrario, il sistema potrebbe diventare sovraccarico. Il valore predefinito è 5. Per ulteriori informazioni, consulta la descrizione relativa a Dimensione batch.

**Conteggio ripetizioni:** numero di volte che la cartella controllata analizza la cartella o la directory. Il valore -1 indica una scansione indefinita. Il valore predefinito è -1.

**Limitazione:** quando questa opzione è selezionata, limita il numero di processi della cartella controllata che AEM forms elabora in un dato momento. Il numero massimo di processi è determinato dal valore Dimensione batch. (Consulta Informazioni sulla limitazione.)

**Nome utente:** (obbligatorio) il nome utente viene utilizzato quando si richiama un servizio di destinazione dalla cartella controllata. Il valore predefinito è SuperAdmin.

**Nome dominio:** (obbligatorio) Il dominio dell’utente. Il valore predefinito è DefaultDom.

**Dimensione batch:** il numero di file o cartelle da acquisire per scansione. Da utilizzare per evitare un sovraccarico del sistema; la scansione di troppi file contemporaneamente può causare un arresto anomalo. Il valore predefinito è 2.

Le impostazioni Intervallo di ripetizione e Dimensione batch determinano il numero di file che la cartella esaminata può raccogliere in ogni analisi. La cartella esaminata utilizza un pool di thread Quartz per analizzare la cartella di input. Il pool di thread è condiviso con altri servizi. Se l’intervallo di scansione è ridotto, i thread eseguiranno spesso la scansione della cartella di input. Se i file vengono rilasciati frequentemente nella cartella controllata, è necessario mantenere l’intervallo di scansione ridotto. Se i file vengono eliminati raramente, utilizza un intervallo di scansione più ampio in modo che gli altri servizi possano utilizzare i thread.

Se elimini un grande volume di file, ingrandisci la dimensione del batch. Ad esempio, se il servizio richiamato dall’endpoint della cartella esaminata è in grado di elaborare 700 file al minuto e gli utenti rilasciano i file nella cartella di input alla stessa velocità, impostare Dimensione batch su 350 e Intervallo di ripetizione su 30 secondi migliorerà le prestazioni della cartella controllata senza incorrere troppo nel costo della scansione della stessa.

Quando i file vengono rilasciati nella cartella controllata, vengono elencati i file nell’input, il che può ridurre le prestazioni se la scansione viene eseguita ogni secondo. L’aumento dell’intervallo di scansione può migliorare le prestazioni. Se il volume dei file da eliminare è piccolo, regola di conseguenza le dimensioni del batch e l’intervallo di ripetizione. Ad esempio, se vengono rilasciati 10 file al secondo, prova a impostare Intervallo di ripetizione su 1 secondo e Dimensione batch su 10.

**Tempo di attesa:** il tempo di attesa, espresso in millisecondi, prima della scansione di una cartella o di un file dopo la creazione. Ad esempio, se il tempo di attesa è di 3.600.000 millisecondi (un’ora) e il file è stato creato un minuto fa, questo file verrà acquisito dopo 59 o più minuti. Il valore predefinito è 0.

Questa impostazione è utile per garantire che un file o una cartella sia completamente copiato nella cartella di input. Ad esempio, se si dispone di un file di grandi dimensioni da elaborare e il download richiede dieci minuti, imposta il tempo di attesa su 10&ast;60 &ast;1000 millisecondi. Questo impedisce alla cartella controllata di eseguire la scansione del file se non sono disponibili dieci minuti.

**Escludi motivo file:** un punto e virgola **;** ha delimitato un elenco di pattern utilizzati da una cartella controllata per determinare quali file e cartelle scansionare e acquisire. Qualsiasi file o cartella con questo motivo non verrà scansionato per l’elaborazione.

Questa impostazione è utile quando l’input è una cartella con più file. Il contenuto della cartella può essere copiato in una cartella con un nome che verrà acquisito dalla cartella controllata. Questo impedisce alla cartella controllata di acquisire una cartella da elaborare prima che questa venga completamente copiata nella cartella di input.

Puoi utilizzare i modelli file per escludere:

* File con estensioni di nome file specifiche, ad esempio .dat, .xml, .pdf.
* File con nomi specifici, ad esempio dati.&ast; escluderebbe i file e le cartelle denominati *data1*, *data2* e così via.
* File con espressioni composite nel nome e nell’estensione, come negli esempi seguenti:

   * Dati`[0-9][0-9][0-9]`.`[dD][aA]`&#39;porta&#39;
   * &ast;.`[dD][aA]`&#39;porta&#39;
   * &ast;.`[Xx][Mm][Ll]`

Per ulteriori informazioni sui modelli di file, consulta [Informazioni sui modelli di file](configuring-watched-folder-endpoints.md#about-file-patterns).

**Pattern di file di inclusione:** (obbligatorio) elenco di pattern delimitati da punto e virgola **;** utilizzati dalla cartella controllata per determinare quali cartelle e file analizzare e raccogliere. Ad esempio, se il pattern di file di inclusione è input&ast;, vengono selezionati tutti i file e le cartelle che corrispondono a input&ast;. Questo include file e cartelle denominati input1, input2 e così via.

Il valore predefinito è &ast; e corrisponde a tutti i file e le cartelle.

Puoi utilizzare i pattern di file per includere:

* File con estensioni di nome file specifiche, ad esempio .dat, .xml, .pdf.
* File con nomi specifici, ad esempio dati.&ast; includerebbe i file e le cartelle con nome *dati1*, *dati2* e così via.
* File con espressioni composite nel nome e nell’estensione, come negli esempi seguenti:

   * Dati`[0-9][0-9][0-9]`.`[dD][aA]`&#39;porta&#39;
   * &ast;.`[dD][aA]`&#39;porta&#39;
   * &ast;.`[Xx][Mm][Ll]`

Per ulteriori informazioni sui pattern di file, consulta [Informazioni sui pattern di file](configuring-watched-folder-endpoints.md#about-file-patterns).


**Cartella dei risultati:** cartella in cui sono archiviati i risultati salvati. Se i risultati non vengono visualizzati in questa cartella, seleziona la cartella errori. I file di sola lettura non vengono elaborati e verranno salvati nella cartella degli errori. Questo valore può essere un percorso assoluto o relativo con i seguenti pattern di file:

* %F = prefisso del nome file
* %E = estensione del nome file
* %Y = anno (completo)
* %y = anno (ultime due cifre)
* %M = mese
* %D = giorno del mese
* %d = giorno dell’anno
* %H = ora (24 ore)
* %h = ora (12 ore)
* %m = minuto
* %s = secondo
* %l = millisecondo
* %R = numero casuale (tra 0 e 9)
* %P = ID processo

Se ad esempio sono le 20:00 del 17 luglio 2009 e specifichi `C:/Test/WF0/failure/%Y/%M/%D/%H/`, la cartella dei risultati sarà `C:/Test/WF0/failure/2009/07/17/20`.

Se il percorso non è assoluto ma relativo, la cartella verrà creata all’interno della cartella controllata. Il valore predefinito è result/%Y/%M/%D/, ovvero la cartella Result all’interno della cartella controllata. Per ulteriori informazioni sui pattern di file, consulta [Informazioni sui pattern di file](configuring-watched-folder-endpoints.md#about-file-patterns).

>[!NOTE]
>
>Minore è la dimensione delle cartelle dei risultati, migliori saranno le prestazioni della cartella controllata. Ad esempio, se il carico stimato per la cartella controllata è di 1000 file l’ora, prova un pattern come `result/%Y%M%D%H` in modo che venga creata una nuova sottocartella ogni ora. Se il caricamento è più piccolo (ad esempio 1000 file al giorno), puoi utilizzare un pattern come `result/%Y%M%D`.

**Cartella di conservazione:** percorso in cui vengono archiviati i file dopo il completamento dell’analisi e del prelievo. Il percorso può essere un percorso di directory assoluto, relativo o nullo. Puoi utilizzare i modelli di file, come descritto per la Cartella dei risultati. Il valore predefinito è mantieni/%A/%M/%G/.

**Cartella errori:** cartella in cui vengono salvati i file degli errori. Questo percorso è sempre relativo alla cartella controllata. Puoi utilizzare i modelli di file, come descritto per la Cartella dei risultati.

I file di sola lettura non vengono elaborati e verranno salvati nella cartella degli errori.

Il valore predefinito è errore/%A/%M/%G/.

**Mantieni in caso di errore:** mantieni i file di input in caso di errore durante l’esecuzione dell’operazione su un servizio. Il valore predefinito è vero.

**Sovrascrivi nomi file duplicati:** se è impostato su vero, i file nella cartella dei risultati e la cartella di conservazione vengono sovrascritti. Se è impostato su falso, vengono utilizzati file e cartelle con un suffisso di indice numerico per il nome. Il valore predefinito è falso.

**Durata eliminazione:** (obbligatorio) i file e le cartelle nella cartella dei risultati vengono eliminati quando sono precedenti al valore specificato. Questo valore è misurato in giorni. Questa impostazione è utile per garantire che la cartella dei risultati non si riempia.

Un valore pari a -1 giorni indica di non eliminare mai la cartella dei risultati. Il valore predefinito è -1.

**Nome operazione:** (obbligatorio) elenco di operazioni che possono essere assegnate all’endpoint della cartella controllata.

**Mappatura parametri di input:** utilizzata per configurare l’input necessario per elaborare il servizio e l’operazione. Le impostazioni disponibili dipendono dal servizio che utilizza l’endpoint della cartella controllata. Di seguito sono riportati i due tipi di input:

**Letterale:** la cartella controllata utilizza il valore immesso nel campo così come viene visualizzato. Sono supportati tutti i tipi Java di base. Ad esempio, se un’API utilizza input come String, long, int e booleano, la stringa viene convertita nel tipo corretto e il servizio viene richiamato.

**Variabile:** il valore immesso è un modello di file utilizzato dalla cartella controllata per scegliere l’input. Se, ad esempio, è disponibile il servizio di crittografia delle password, in cui il documento di input deve essere un file PDF, l’utente può utilizzare &ast;.pdf come modello di file. La cartella controllata raccoglierà tutti i file della cartella controllata che corrispondono a questo modello e richiamerà il servizio per ogni file. Quando si utilizza una variabile, tutti i file di input vengono convertiti in documenti. Sono supportate solo le API che utilizzano Documento come tipo di input.

**Mappature dei parametri di output:** utilizzate per configurare gli output del servizio e dell’operazione. Le impostazioni disponibili dipendono dal servizio che utilizza l’endpoint della cartella controllata.

L’output della cartella controllata può essere un singolo documento, un elenco di documenti o una mappa di documenti. Questi documenti di output vengono quindi salvati nella cartella dei risultati, utilizzando il pattern specificato nella Mappatura dei parametri di output.

>[!NOTE]
>
>Specificare i nomi che determinano nomi di file di output univoci migliora le prestazioni. Consideriamo, ad esempio, il caso in cui il servizio restituisce un documento di output e la mappatura dei parametri di output lo associa a `%F.%E` (il nome file e l’estensione del file di input). In questo caso, se gli utenti rilasciano i file con lo stesso nome ogni minuto e la cartella dei risultati è configurata su `result/%Y/%M/%D`, e l’impostazione Sovrascrivi nome file duplicato è disattivata, la cartella controllata tenterà di risolvere i nomi dei file duplicati. Il processo di risoluzione dei nomi di file duplicati può influire sulle prestazioni. In questa situazione, modificare la mappatura dei parametri di output in `%F_%h_%m_%s_%l` per aggiungere ore, minuti, secondi e millisecondi al nome o verificare che i file rilasciati abbiano nomi univoci può migliorare le prestazioni.

## Informazioni sui pattern dei file {#about-file-patterns}

Gli amministratori possono specificare il tipo di file che può richiamare un servizio. Si possono stabilire più pattern di file per ogni cartella controllata. Un pattern di file può essere rappresentato da una delle seguenti proprietà di file:

* File con estensioni del nome file specifiche. Ad esempio, &ast;.dat, &ast;.xml, &ast;.pdf
* File con nomi specifici. Ad esempio, data.&ast;
* File con espressioni composite nel nome e nell’estensione, come negli esempi seguenti:

   * Dati`[0-9][0-9][0-9]`.`[dD][aA]`&#39;porta&#39;
   * &ast;.`[dD][aA]`&#39;porta&#39;
   * &ast;.`[Xx][Mm][Ll]`

L’amministratore può definire il modello di file della cartella di output in cui memorizzare i risultati. Per le cartelle di output (risultati, conservazione ed errori), l’amministratore può specificare uno dei seguenti modelli di file:

* %Y = anno (completo)
* %y = anno (ultime due cifre)
* %M = mese,
* %D = giorno del mese,
* %d = giorno dell’anno,
* %h = ora,
* %m = minuto,
* %s = secondo,
* %R = numero casuale compreso tra 0 e 9
* %J = Nome processo

Ad esempio, il percorso della cartella dei risultati potrebbe essere `C:\Adobe\Adobe_Experience_Manager_forms\BarcodedForms\%y\%m\%d`.

Le mappature dei parametri di output possono inoltre specificare pattern aggiuntivi, ad esempio:

* %F = Nome file di origine
* %E = Estensione nome file di origine

Se il modello di mappatura dei parametri di output termina con “File.separator” (il separatore di percorso), viene creata una cartella e il contenuto viene copiato in tale cartella. Se il modello non termina con “File.separator”, il contenuto (file di risultati o cartella) viene creato con tale nome. Per ulteriori informazioni sulle mappature dei parametri di output, consulta [Suggerimenti per le cartelle controllate](configuring-watched-folder-endpoints.md#tips-and-tricks-for-watched-folders).

## Informazioni sulla limitazione {#about-throttling}

Quando è abilitata per un endpoint della cartella controllata, la limitazione limita il numero di processi della cartella controllata che possono essere elaborati in un determinato momento. Il numero massimo di processi è determinato dal valore Dimensione batch, anch’esso configurabile nell’endpoint della cartella controllata. I documenti in arrivo nella directory di input della cartella controllata non vengono sottoposti a polling quando viene raggiunto il valore massimo per la limitazione. Inoltre i documenti rimangono inoltre nella directory di input fino al completamento di altri processi della cartella controllata e di un altro tentativo di polling. In caso di elaborazione sincrona, tutti i processi elaborati in un singolo processo di polling vengono conteggiati ai fini del valore massimo di limitazione, anche se i processi vengono elaborati consecutivamente in un singolo thread.

>[!NOTE]
>
>La limitazione non viene ridimensionata con un cluster. Quando la limitazione è abilitata, il cluster nel suo insieme non elaborerà un numero di processi superiore a quello specificato in Dimensione batch in un momento dato. Questo limite è relativo all’intero cluster e non specifico per ogni nodo del cluster. Ad esempio, con una dimensione batch pari a 2, è possibile raggiungere il valore massimo di limitazione con un singolo nodo che elabora due processi, e nessun altro nodo può eseguire il polling della directory di input fino al completamento di uno dei processi.

### Come funziona la limitazione {#how-throttling-works}

La cartella controllata esegue la scansione della cartella di input a ogni intervallo di ripetizione, rileva il numero di file specificato in Dimensione batch e richiama il servizio di destinazione per ciascuno di questi file. Se ad esempio la dimensione del batch è quattro, a ogni scansione la cartella controllata seleziona quattro file, crea quattro richieste di chiamata e richiama il servizio di destinazione. Prima del completamento di queste richieste, se viene richiamata la cartella controllata, vengono avviati di nuovo quattro processi, indipendentemente dal fatto che i quattro processi precedenti siano stati completati o meno.

La limitazione impedisce che la cartella controllata richiami nuovi processi quando i processi precedenti non sono ancora completati. La cartella controllata rileva i processi in corso ed elabora i nuovi processi in base alle dimensioni del batch meno i processi in corso. Ad esempio, nella seconda chiamata, se i processi completati sono solo tre e un processo è ancora in corso, la cartella controllata richiama solo altri tre processi.

* La cartella controllata si basa sul numero di file presenti nella cartella di fase per individuare quanti processi sono in corso. Se i file rimangono non elaborati nella cartella di fase, la cartella controllata non richiama altri processi. Se ad esempio la dimensione del batch è quattro e tre processi sono in stallo, la cartella controllata richiama solo un processo nelle chiamate successive. Esistono più scenari che possono bloccare l’elaborazione dei file nella cartella di fase. Quando i processi vengono bloccati, l’amministratore può terminare il processo nella pagina di amministrazione del flusso di lavoro dei moduli in modo che la cartella controllata sposti i file fuori dalla cartella di fase.
* Se il server di Forms si blocca prima che la cartella controllata possa richiamare i processi, l’amministratore può spostare i file fuori dalla cartella di fase. Per informazioni, consulta [Punti di errore e ripristino](configuring-watched-folder-endpoints.md#failure-points-and-recovery).
* Se il server Forms è in esecuzione ma la cartella controllata non è in esecuzione quando il servizio Gestione processi risponde, il che si verifica quando i servizi non si avviano nella sequenza ordinata, l’amministratore può spostare i file fuori dalla cartella di fase. Per informazioni, consulta [Punti di errore e ripristino](configuring-watched-folder-endpoints.md#failure-points-and-recovery).


## Prestazioni e scalabilità {#performance-and-scalability}

La cartella controllata può servire in totale 100 cartelle su un singolo nodo. Le prestazioni della cartella controllata dipendono dalle prestazioni del server Forms. Per la chiamata asincrona, le prestazioni dipendono più dal carico del sistema e dai processi presenti nella coda di Gestione processo.

È possibile migliorare le prestazioni della cartella controllata aggiungendo nodi al cluster. I processi delle cartelle controllate vengono distribuiti tra i nodi del cluster in virtù del modulo di pianificazione Quartz e, in caso di richieste asincrone, dal servizio Gestione processo. Tutti i processi vengono mantenuti nel database.

La cartella controllata dipende dal servizio del modulo di pianificazione per la pianificazione, l’annullamento della pianificazione e la ripianificazione dei processi. Sono disponibili altri servizi, come Gestione eventi, Gestione utenti e Provider di posta elettronica, che condividono il pool di thread del servizio di modulo di pianificazione. Questo può influire sulle prestazioni della cartella controllata. L&#39;ottimizzazione del pool di thread del servizio di modulo di pianificazione sarà necessaria quando tutti i servizi inizieranno a utilizzarlo.

## Cartelle controllate in un cluster {#watched-folders-in-a-cluster}

In un cluster, la cartella controllata dipende dal modulo di pianificazione Quartz e dal servizio Gestione processi per il bilanciamento del carico e il failover. Per ulteriori informazioni sul comportamento del cluster Quartz, consulta la [Documentazione Quartz](https://www.quartz-scheduler.org/documentation).

La cartella controllata esegue queste tre attività principali a ogni sondaggio:

* Scarica la cartella
* Richiama il servizio di destinazione
* Gestisci i risultati

Il comportamento di bilanciamento del carico e failover cambia a seconda che la cartella controllata sia configurata per la chiamata sincrona o asincrona.

### Cartella controllata sincrona in un cluster {#synchronous-watched-folder-in-a-cluster}

Per le chiamate sincrone, il load balancer Quartz decide quale nodo riceverà l’evento di polling. Il nodo che riceve l’evento di polling eseguirà tutte le attività seguenti: eseguirà la scansione della cartella, richiamerà il servizio di destinazione e gestirà i risultati.

![en_synchwatchedfoldercluster](assets/en_synchwatchedfoldercluster.png)

Per le chiamate sincrone, quando un nodo non riesce, il modulo di pianificazione Quartz invia nuovi eventi di polling ad altri nodi. Le chiamate avviate sul nodo non riuscito andranno perse. Per ulteriori informazioni su come recuperare i file associati al processo non riuscito, consulta [Punti di errore e recupero](configuring-watched-folder-endpoints.md#failure-points-and-recovery).


### Cartella controllata asincrona in un cluster {#asynchronous-watched-folder-in-a-cluster}

Per le chiamate asincrone, il load balancer Quartz decide quale nodo riceverà l’evento di polling. Il nodo che riceve l’evento di polling eseguirà la scansione della cartella di input e richiamerà il servizio di destinazione posizionando la richiesta nella coda del servizio Gestione processi. Il load balancer del servizio di Gestione processi, a sua volta, è responsabile della decisione sul nodo che elaborerà la richiesta di chiamata. È possibile che, anche se il nodo A ha creato la richiesta di chiamata, il nodo B finisca per elaborarla. In alternativa, anche il nodo che ha avviato la richiesta di chiamata potrebbe finire per elaborare la richiesta.

![en_asynchwatchedfoldercluster](assets/en_asynchwatchedfoldercluster.png)

Per le chiamate asincrone, quando un nodo non riesce, il modulo di pianificazione Quartz invia nuovi eventi di polling ad altri nodi. Le richieste di chiamata create nel nodo non riuscito verranno inserite nella coda del servizio Gestione processi e verranno inviate ad altri nodi per l’elaborazione. I file per i quali non vengono create richieste di chiamata rimarranno nella cartella di staging. Per ulteriori informazioni su come recuperare i file associati al processo non riuscito, consulta [Punti di errore e recupero](configuring-watched-folder-endpoints.md#failure-points-and-recovery).


## Punti di errore e recupero {#failure-points-and-recovery}

A ogni evento di polling, la cartella controllata blocca la cartella di input, sposta i file che corrispondono al modello di file di inclusione nella cartella di staging e quindi sblocca la cartella di input. Il blocco è necessario in modo che due thread non acquisiscano lo stesso set di file ed elaborino due volte. Le probabilità che ciò accada aumentano con un piccolo intervallo di ripetizione e una grande dimensione batch. Una volta spostati i file nella cartella di staging, la cartella di input viene sbloccata in modo che altri thread possano eseguire la scansione. Questo passaggio fornisce un throughput elevato perché altri thread possono eseguire la scansione mentre un thread sta elaborando i file.

Una volta spostati i file nella cartella di staging, vengono create richieste di chiamata per ciascun file e viene richiamato il servizio di destinazione. In alcuni casi, la cartella controllata non è in grado di recuperare i file nella cartella di staging:

* Se il server si blocca prima che la cartella controllata possa creare la richiesta di chiamata, i file nella cartella di staging rimangono nella stessa cartella e non vengono recuperati.
* Se la cartella controllata ha creato correttamente la richiesta di chiamata per ciascuno dei file presenti nella cartella di staging e il server si blocca, esistono due comportamenti in base al tipo di chiamata:

**Sincrona:** se la cartella controllata è configurata per richiamare il servizio in modalità sincrona, tutti i file nella cartella di staging rimangono non elaborati nella stessa cartella.

**Asincrona:** in questo caso, la cartella controllata si basa sul servizio Gestione processi. Se il servizio Gestione processi richiama la cartella controllata, i file nella cartella di staging vengono spostati nella cartella di conservazione o di errore in base ai risultati della chiamata. Se il servizio Gestione processi non richiama la cartella controllata, i file rimarranno non elaborati nella cartella di fase. Questa situazione si verifica quando la cartella controllata non è in esecuzione al momento in cui Gestione processi richiama.

### Recuperare file di origine non elaborati nella cartella di fase {#recovering-unprocessed-source-files-in-the-stage-folder}

Quando la cartella controllata non è in grado di elaborare i file di origine nella cartella di fase, puoi recuperare i file non elaborati.

1. Riavvia il server applicazioni o il nodo.
1. (Facoltativo) Impedisci alla cartella controllata di elaborare nuovi file di input. Se salti questo passaggio, sarà molto più difficile determinare quali file non sono elaborati nella cartella di fase. Per impedire che la cartella controllata elabori nuovi file di input, esegui una delle operazioni seguenti:

   * In Applicazioni e servizi, modifica il parametro Includi modelli file per l’endpoint della cartella controllata in modo che non corrisponda a nessuno dei nuovi file di input (ad esempio, immetti `NOMATCH`).
   * Sospendi il processo di creazione dei nuovi file di input.

   Attendi il ripristino e l’elaborazione di tutti i file da parte di AEM Forms. La maggior parte dei file verrà recuperata e i nuovi file di input verranno elaborati correttamente. Il tempo di attesa per il recupero e l’elaborazione dei file da parte della cartella controllata dipende dalla durata dell’operazione di chiamata e dal numero di file da recuperare.

1. Determina quali file non possono essere elaborati. Se hai atteso un periodo di tempo adeguato e hai completato il passaggio precedente e nella cartella dell’area di visualizzazione sono ancora presenti file non elaborati, procedi al passaggio successivo.

   >[!NOTE]
   >
   >Puoi controllare la data e l’ora dei file nella directory di fase. A seconda del numero di file e del tempo di elaborazione normale, puoi determinare quali file sono abbastanza vecchi da poter essere considerati bloccati.

1. Copia i file non elaborati dalla directory di fase alla directory di input.
1. Se nel passaggio 2 hai impedito l’elaborazione di nuovi file di input nella cartella controllata, ripristina il valore precedente del campo Includi modelli file o riattiva il processo che hai disattivato.

## Considerazioni sulla protezione delle cartelle controllate {#security-considerations-for-watched-folders}

Ogni cartella controllata è configurata con un nome utente e una password. Queste credenziali vengono utilizzate quando si richiamano i servizi. La cartella controllata si basa sul fatto che la cartella condivisa è protetta con il file system di protezione sottostante, in modo che solo il proprietario della cartella controllata possa accedere alla cartella condivisa.

## Suggerimenti per le cartelle controllate {#tips-and-tricks-for-watched-folders}

Di seguito sono riportati alcuni suggerimenti utili per la configurazione dell’endpoint cartella controllata:

* Se in Windows è presente una cartella controllata che elabora i file immagine, specificare i valori per l’opzione Includi modelli file o Escludi modelli file per impedire che il file Thumbs.db generato automaticamente da Windows venga sottoposto a polling dalla cartella controllata.
* Se è specificata un’espressione Cron, l’intervallo di ripetizione viene ignorato. L’utilizzo dell’espressione Cron si basa sul sistema di pianificazione dei processi open source Quartz, versione 1.4.0.
* La dimensione batch è il numero di file o cartelle che verranno raccolte in ogni scansione della cartella controllata. Se la dimensione batch è impostata su due e nella cartella di input della cartella controllata vengono rilasciati dieci file o cartelle, in ogni scansione verranno raccolti solo due file o cartelle. Nella scansione successiva, che si verifica dopo il tempo specificato nell’intervallo di ripetizione, verranno raccolti i due file successivi.
* Per i pattern di file, gli amministratori possono specificare espressioni regolari con il supporto aggiuntivo di pattern con caratteri jolly. La cartella controllata modifica l’espressione regolare per supportare i pattern con caratteri jolly, come &ast;.&ast; o &ast;.pdf. Questi pattern con caratteri jolly non sono supportati dalle espressioni regolari.
* La cartella controllata analizza l’input della cartella di input ma non verifica che il file o la cartella di origine sia stato completamente copiato nella cartella di input prima di iniziare l’elaborazione. Per assicurarti che il file o la cartella di origine sia stato completamente copiato nella cartella di input della cartella controllata prima che il file o la cartella venga prelevato, esegui le operazioni seguenti:

   * Usa il tempo di attesa, ovvero il tempo in millisecondi per il quale la cartella controllata resta in attesa dall’ora dell’ultima modifica. Utilizza questa funzione se devi elaborare file di grandi dimensioni. Ad esempio, se il download di un file richiede 10 minuti, specifica il tempo di attesa come 10&ast;60 &ast;1000 millisecondi. In tal modo la cartella controllata non raccogliere il file se non esisste da almeno 10 minuti.
   * Utilizza il pattern di file di esclusione e il pattern di file di inclusione. Se ad esempio il pattern di file di esclusione è `ex*` e il pattern di file di inclusione è `in*`, la cartella controllata raccoglierà i file che iniziano con “in” e non raccoglierà i file che iniziano con “ex”. Per copiare file o cartelle di grandi dimensioni, rinomina il file o la cartella in modo che il nome inizi con “ex”. Dopo aver copiato completamente il file o la cartella denominata “ex” nella cartella controllata, rinominala come “in&ast;”.

* Utilizza la durata di eliminazione per mantenere pulita la cartella dei risultati. La cartella controllata elimina tutti i file più vecchi della durata indicata nella durata di eliminazione. La durata è in giorni.
* Quando aggiungi un endpoint cartella controllata, dopo la selezione del nome dell’operazione, viene popolata la mappatura dei parametri di input. Per ogni input dell’operazione viene generato un campo di mappatura dei parametri di input. Di seguito sono riportati alcuni esempi di mappature dei parametri di input:

   * Per l’input `com.adobe.idp.Document`: se l’operazione di servizio ha un input di tipo `Document`, l’amministratore può specificare il tipo di mappatura come `Variable`. La cartella controllata preleverà l’input dalla cartella di input della cartella controllata in base al pattern di file specificato per il parametro di input. Se l’amministratore specifica come parametro `*.pdf`, ogni file con estensione .pdf verrà prelevato e convertito in `com.adobe.idp.Document` e verrà richiamato il servizio.
   * Per l’input `java.util.Map`: se l’operazione del servizio ha un input di tipo `Map`, l’amministratore può specificare il tipo di mappatura come `Variable` e immettere un valore di mappatura con un pattern come `*.pdf`. Ad esempio, un servizio richiede una mappatura di due oggetti `com.adobe.idp.Document` che rappresentano due file nella cartella di input, come 1.pdf e 2.pdf. Nella cartella controllata verrà creata una mappatura con la chiave come nome del file e `com.adobe.idp.Document` come valore.
   * Per l’input `java.util.List`: se l’operazione di servizio ha un input di tipo elenco, l’amministratore può specificare il tipo di mappatura come `Variable` e immettere un valore di mappatura con un pattern come `*.pdf`. Quando i file PDF vengono rilasciati nella cartella di input, la cartella controllata creerà un elenco degli oggetti `com.adobe.idp.Document` che rappresenta questi file e richiamerà il servizio di destinazione.
   * Per `java.lang.String`: l’amministratore ha due opzioni. In primo luogo, l’amministratore può specificare il tipo di mappatura come `Literal` e immettere un valore di mappatura come stringa, ad esempio `hello.` e la cartella controllata richiamerà il servizio con la stringa `hello`. In secondo luogo, l’amministratore può specificare il tipo di mappatura come `Variable` e immettere un valore di mappatura con un pattern come `*.txt`. In quest’ultimo caso i file con estensione .txt verranno letti come un documento con valore imposto stringa per richiamare il servizio.
   * Tipo Java primario: l’amministratore può specificare il tipo di mappatura come `Literal` e fornire il valore. La cartella controllata richiamerà il servizio con il valore specificato.

* La cartella controllata è concepita per funzionare con i documenti. Gli output supportati sono `com.adobe.idp.Document`, `org.w3c.Document`, `org.w3c.Node` e un elenco e una mappa di questi tipi. Qualsiasi altro tipo genererà un output di errore nella cartella errori.
* Se non sono presenti risultati nella cartella dei risultati, verifica la cartella errori per confermare se si è verificato un errore.
* La cartella controllata funziona meglio se utilizzata in modalità asincrona. In questa modalità la cartella controllata inserisce la richiesta di chiamata nella coda ed esegue la richiamata. La coda viene quindi elaborata in modo asincrono. Quando l’opzione Asincrono non è impostata, la cartella controllata richiama il servizio di destinazione in modo sincrono e il motore di processo attende che il servizio venga eseguito insieme alla richiesta e che vengano prodotti i risultati. Se l’elaborazione della richiesta da parte del servizio di destinazione richiede molto tempo, nella cartella controllata potrebbero verificarsi errori di timeout.
* La creazione di cartelle controllate per le operazioni di importazione ed esportazione non consente l’astrazione dell’estensione del nome file. Quando si richiama il servizio di integrazione dei dati del modulo utilizzando le cartelle controllate, il tipo di estensione del nome file per il file di output potrebbe non corrispondere al formato di output previsto per il tipo di oggetto documento. Se ad esempio il file di input di una cartella controllata che richiama l’operazione di esportazione è un modulo XFA contenente dati, l’output deve essere un file di dati XDP. Per ottenere un file di output con l’estensione corretta, puoi specificarlo nella mappatura dei parametri di output. In questo esempio puoi utilizzare %F.xdp come mappatura dei parametri di output.
* La cartella controllata può elaborare i file di input prima che vengano copiati completamente nella cartella. Il blocco dei file non è obbligatorio in UNIX, ma lo è in Windows. Per questo motivo, quando un file viene copiato in una cartella controllata, la cartella controllata può spostare il file nella cartella di fase senza attendere il completamento della copia del file stesso. Questo comportamento fa sì che venga elaborata solo una parte del file di input. Attualmente esistono due soluzioni alternative:

   * Soluzione alternativa 1

      1. Specifica un pattern per Pattern di file di esclusione, ad esempio temp&ast;.ps.
      1. Copia i file che iniziano con temp (ad esempio, temp1.ps) nella cartella controllata.
      1. Dopo che il file è stato copiato completamente nella cartella controllata, rinomina il file in modo che corrisponda al pattern specificato per Pattern di file di inclusione. La cartella controllata sposta quindi il file completato nella cartella di fase.

   * Soluzione alternativa 2

     Se conosci il tempo massimo necessario per copiare i file in una cartella controllata, specifica il tempo di attesa in secondi. La cartella controllata attende quindi il periodo di tempo specificato prima di spostare il file nella cartella di fase.

     Questo non è un problema per i file su Windows, perché Windows blocca un file quando un thread sta scrivendo. Tuttavia, questo rappresenta problema per le cartelle su Windows. Per le cartelle devi seguire i passaggi descritti in Soluzione 1.

* Se l’attributo dell’endpoint Mantieni nome cartella per la cartella controllata è impostato su un percorso di directory null, la directory di fase non viene cancellata come previsto. La directory contiene ancora il file elaborato e la cartella temporanea.

## Raccomandazioni specifiche per i servizi per le cartelle controllate {#service-specific-recommendations-for-watched-folders}

Per tutti i servizi, è necessario regolare la dimensione batch e l’intervallo di ripetizione della cartella controllata, in modo che la frequenza con cui la cartella controllata seleziona nuovi file e cartelle da elaborare non superi la frequenza dei processi che possono essere elaborati dal server AEM Forms. I parametri effettivi da utilizzare possono variare a seconda del numero di cartelle controllate configurate, dei servizi che utilizzano le cartelle controllate e dell’intensità dei processi nel processore.

### Consigli sul servizio Genera PDF {#generate-pdf-service-recommendations}

* Il servizio Genera PDF può convertire un solo file alla volta per questi tipi di file: Microsoft Word, Microsoft Excel, Microsoft PowerPoint, Microsoft Project, AutoCAD, Adobe Photoshop®, Adobe FrameMaker® e Adobe PageMaker®. Si tratta di processi con tempi di esecuzione lunghi; pertanto, assicurati di mantenere le dimensioni del batch su un’impostazione bassa. Aumenta anche l’intervallo di ripetizione se il cluster contiene più nodi.
* Per PostScript (PS), Encapsulated PostScript (EPS) e i tipi di file di immagine, il servizio Genera PDF può elaborare diversi file in parallelo. Devi regolare con attenzione la dimensione del pool dei bean di sessione (che determina il numero di conversioni che verranno eseguite in parallelo) in base alla capacità del server e al numero di nodi nel cluster. Quindi aumenta la dimensione del batch a un numero pari alla dimensione del pool dei bean di sessione per i tipi di file che si sta tentando di convertire. La frequenza di polling deve essere determinata dal numero di nodi nel cluster. Tuttavia, poiché il servizio Genera PDF elabora questi tipi di processi abbastanza rapidamente, puoi configurare l’intervallo di ripetizione su un valore basso, ad esempio 5 o 10.
* Anche se il servizio Generate PDF è in grado di convertire un solo file OpenOffice alla volta, la conversione è abbastanza veloce. La logica di cui sopra per le conversioni di PS, EPS e immagini si applica anche alle conversioni OpenOffice.
* Per abilitare la distribuzione uniforme del carico nel cluster, mantieni bassa la dimensione del batch e aumenta l’intervallo di ripetizione.

### consigli sul servizio di moduli con codice a barre {#barcoded-forms-service-recommendations}

* Per ottenere prestazioni ottimali durante l’elaborazione di moduli con codice a barre (file di piccole dimensioni), immettere `10` per Dimensione batch e `2` per Intervallo di ripetizione.
* Quando nella cartella di input vengono inseriti molti file, potrebbero verificarsi errori con i file nascosti denominati *thumbs.db*. È pertanto consigliabile impostare il modello file da includere per i file da includere sullo stesso valore specificato per la variabile di input (ad esempio, `*.tiff`). Questo impedisce a Cartella controllata di elaborare i file DB.
* Un valore con Dimensione batch di `5` e Intervallo di ripetizione di `2` in genere sufficiente perché il servizio Moduli con codice a barre impiega in genere circa 0,5 secondi per elaborare un codice a barre.
* La cartella controllata non attende che il motore del processo abbia terminato il lavoro prima di raccogliere nuovi file o cartelle. Continua a esaminare la cartella controllata e a richiamare il servizio di destinazione. Questo comportamento può sovraccaricare il motore, causando problemi di risorse e timeout. Assicurati di utilizzare l’intervallo di ripetizione e la dimensione del batch per limitare l’input della cartella controllata. Puoi aumentare l’intervallo di ripetizione e ridurre la dimensione del batch, se sono presenti più cartelle controllate, oppure abilitare la limitazione sull’endpoint. Per informazioni sulla limitazione, consulta [Informazioni sulla limitazione](configuring-watched-folder-endpoints.md#about-throttling).
* La cartella controllata rappresenta l’utente specificato nel nome utente e nel nome del dominio. Watched Folder richiama il servizio come questo utente se richiamato direttamente o se il processo ha una durata breve. Per un processo di lunga durata, il processo viene richiamato con il contesto di sistema. Gli amministratori possono impostare i criteri del sistema operativo per la cartella controllata per determinare a quale utente concedere o negare l’accesso.
* Utilizza i pattern di file per organizzare i risultati, gli errori e mantenere le cartelle. (Consulta [Informazioni sui pattern di file](configuring-watched-folder-endpoints.md#about-file-patterns).)

* La cartella controllata si basa sul modulo di pianificazione Quartz per la scansione delle cartelle controllate. Il modulo di pianificazione Quartz dispone di un pool di thread per la scansione. Se l’intervallo di ripetizione per la cartella controllata è molto basso (&lt; 5 secondi) e la dimensione del batch è elevata (> 2), può verificarsi una situazione di tipo “race condition”. Quando si verifica questa condizione, un file viene raccolto da due thread Quartz:

   * Uno dei thread trova correttamente il file e richiama il servizio di destinazione con il file.
   * Il secondo thread visualizza il file, ma non riesce quando tenta di verificare se il file è valido (file di lettura o scrittura), causando falsi errori che indicano che il file non può essere elaborato perché è di sola lettura. Ciò si verifica solo con un intervallo di ripetizione basso e una dimensione del batch elevata.
