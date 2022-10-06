---
title: Creare o configurare una cartella controllata
seo-title: Create or Configure a watched folder
description: Scopri come creare o eliminare una cartella controllata o modificare le proprietà di una cartella controllata esistente.
seo-description: Learn how to create or delete a watched folder, or modify the properties of an existing watched folder.
uuid: 659d4d8c-99b8-40dd-b884-bfee4d476fe1
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 0ce7b338-6686-49b3-b58b-e7ab6b670708
exl-id: b15d8d3b-5e47-4c33-95fe-440fcf96be83
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1820'
ht-degree: 0%

---

# Creare o configurare una cartella controllata {#create-or-configure-a-watched-folder}

Un amministratore può configurare una cartella di rete denominata *cartella controllata* In questo modo, quando un utente inserisce un file (ad esempio un file PDF) nella cartella controllata, viene avviata un’operazione preconfigurata e il file viene manipolato. Dopo l&#39;esecuzione dell&#39;operazione specificata, il file modificato viene salvato in una cartella di output specificata. Per informazioni dettagliate sull&#39;amministrazione di una cartella controllata, vedi [Guida all’amministrazione](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md).

Puoi utilizzare l’interfaccia utente della cartella controllata per:

* Creare una cartella controllata
* Modifica delle proprietà di una cartella osservata esistente
* Eliminare una cartella controllata

## Creare una cartella controllata {#create-a-watched-folder}

Prima di configurare una cartella controllata, verifica quanto segue:

* Le cartelle controllate sono una funzionalità avanzata dei moduli AEM. Richiede il funzionamento del pacchetto aggiuntivo AEM forms. Verifica che sia installato e configurato il pacchetto aggiuntivo AEM Forms appropriato.
* È possibile creare la cartella controllata in un archivio condiviso o locale. Verificare che AEM utente dei moduli configurato per eseguire la cartella controllata disponga delle autorizzazioni di lettura e scrittura per la cartella controllata.
* Puoi utilizzare un servizio, un flusso di lavoro o uno script per automatizzare un’operazione con una cartella controllata. Assicurati che sia stato creato il servizio, il flusso di lavoro o uno script corrispondente e pronto per l’esecuzione. Per informazioni sulla creazione di un servizio, di un flusso di lavoro e di uno script, consulta [Vari metodi di elaborazione dei file](/help/forms/using/watched-folder-in-aem-forms.md#various-methods-for-processing-files).
* Una cartella controllata ha varie proprietà, vedi [Proprietà cartella controllata](watched-folder-in-aem-forms.md#watchedfolderproperties).

Esegui i seguenti passaggi per creare una cartella controllata:

1. Tocca **Adobe Experience Manager** nell’angolo in alto a sinistra dello schermo.
1. Tocca **Strumenti** > **Forms** > **Configura la cartella osservata.** Viene visualizzato un elenco di cartelle controllate già configurate.
1. Tocca **Nuovo**. Viene visualizzato un elenco dei campi necessari per creare la cartella controllata:

   * **Nome**: Identifica la cartella controllata. Per il nome è possibile utilizzare solo caratteri alfanumerici.
   * **Percorso**: Specifica il percorso della cartella controllata. In un ambiente cluster, questa impostazione deve puntare a una cartella di rete condivisa accessibile a ogni utente che esegue AEM su nodi diversi di un cluster.
   * **Elabora file tramite**: Il tipo di processo da avviare. È possibile specificare flusso di lavoro, script o servizio.
   * **Nome servizio/Percorso script/Percorso flusso di lavoro**: Il comportamento del campo è basato sul valore specificato per **Elabora file tramite** campo . Puoi specificare i seguenti valori:

      * Per Flusso di lavoro, specifica il modello di flusso di lavoro da eseguire. Ad esempio, /etc/workflow/models/&lt;workflow_name>/jcr:content/model
      * Per Script, specifica il percorso JCR dello script da eseguire. Ad esempio, /etc/watchfolder/test/testScript.ecma
      * Per Servizio , specifica il filtro utilizzato per individuare un servizio OSGi. Il servizio è registrato come implementazione dell&#39;interfaccia com.adobe.aemfd.watchfolder.service.api.ContentProcessor. Ad esempio, il codice seguente è un’implementazione personalizzata dell’interfaccia ContentProcessor con una proprietà personalizzata (foo=bar) .

   >[!NOTE]
   >
   >Se hai selezionato **Servizio** per **Elabora file tramite** campo , il valore del campo Nome servizio (inputProcessorType) deve essere racchiuso tra parentesi. Ad esempio, (foo=bar).

   ```java
   @Component(metatype = true, immediate = true, label = "WF Test Service", description = "WF Test Service")
   @Service(value = {OutputWriter.class, ContentProcessor.class})
   @Property(name = "foo", value = "bar")
   public class OutputWriter implements ContentProcessor {
   ```

   * **Pattern di file di output**: Specificare un elenco di pattern delimitato da punti e virgola (;) utilizzato da una cartella controllata per determinare il nome e la posizione dei file e delle cartelle di output. Per ulteriori informazioni sui pattern di file, vedere [Informazioni sui pattern di file](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns).


1. Tocca **Avanzate**. La scheda avanzata contiene altri campi. La maggior parte di questi campi contiene un valore predefinito.

   * **Filtro mappatore payload:** Quando si crea una cartella controllata, viene creata una struttura di cartelle all’interno della cartella controllata. La struttura delle cartelle presenta cartelle di stage, risultato, mantenimento, input e errori. La struttura delle cartelle può fungere da payload di input per il flusso di lavoro e accettare l’output da un flusso di lavoro. Può inoltre elencare eventuali punti di errore. La struttura di un payload è diversa dalla struttura di una cartella controllata. È possibile creare script personalizzati per mappare la struttura di una cartella controllata al payload. Tale script si chiama filtro di mappatura payload. Sono disponibili due implementazioni di mappatore payload pronte all’uso. Se non hai [implementazione personalizzata](/help/forms/using/watched-folder-in-aem-forms.md#creating-a-custom-payload-mapper-filter), utilizza un’implementazione standard:

      * **Mapper predefinito:** Utilizza il mappatore payload predefinito per mantenere il contenuto di input e output delle cartelle controllate in cartelle di input e output separate nel payload.
      * **Semplice mappatore del payload basato su file:** Utilizza il mappatore payload basato su file semplice per mantenere i contenuti di input e output direttamente nella cartella payload. Non crea alcuna gerarchia extra, come la mappatura predefinita.
   * **Modalità di esecuzione**: Specifica l’elenco separato da virgole delle modalità di esecuzione consentite per l’esecuzione del flusso di lavoro.
   * **Timeout file in fase dopo**: Specifica il numero di secondi di attesa prima che un file o una cartella di input già acquisito per l’elaborazione venga considerato come se fosse scaduta e contrassegnata come un errore. Il meccanismo di timeout si attiva solo quando il valore di questa proprietà è un numero positivo.
   * **Elimina i file in fase di timeout quando ridotti**: Se attivato, la **Timeout file in fase dopo** il meccanismo viene attivato solo quando la limitazione è attivata per la cartella controllata.
   * **Analizzare La Cartella Di Input Dopo Ogni:** Specificare l&#39;intervallo di tempo, in secondi, per la scansione della cartella controllata per gli input. A meno che l’impostazione di limitazione non sia abilitata, l’intervallo di polling deve essere più lungo del tempo necessario per elaborare un lavoro medio; in caso contrario, il sistema potrebbe essere sovraccarico. Il valore dell&#39;intervallo deve essere maggiore o uguale a uno.
   * **Escludi pattern file**: Specificare un elenco di pattern delimitato da punti e virgola (;) utilizzato da una cartella controllata per determinare quali file e cartelle analizzare e raccogliere. Qualsiasi file o cartella con il pattern specificato non viene analizzato per l’elaborazione. Per ulteriori informazioni sui pattern di file, vedere [Informazioni sui pattern di file](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns).
   * **Includi pattern file**: Specificare un elenco di pattern delimitato da punti e virgola (;) utilizzato dalla cartella controllata per determinare le cartelle e i file da analizzare e raccogliere. Ad esempio, se il pattern di file di inclusione è input&amp;ast;, tutti i file e le cartelle corrispondenti a input&amp;ast; vengono prelevati. Il valore predefinito è &amp;ast; e indica tutti i file e le cartelle. Per ulteriori informazioni sui pattern di file, vedere [Informazioni sui pattern di file](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns).
   * **Tempo di attesa:** Specifica il tempo, in millisecondi, da attendere prima di eseguire la scansione di una cartella o di un file dopo la creazione. Ad esempio, se il tempo di attesa è di 3.600.000 millisecondi (un&#39;ora) e il file è stato creato un minuto fa, questo file verrà acquisito dopo 59 o più minuti passati. Il valore predefinito è 0.

      Questa impostazione è utile per garantire che tutto il contenuto del file o della cartella venga copiato nella cartella di input. Ad esempio, se si dispone di un file di grandi dimensioni da elaborare e il file richiede dieci minuti per il download, impostare il tempo di attesa su 10&amp;ast;60 &amp;ast;1000 millisecondi. Questo intervallo impedisce alla cartella controllata di eseguire la scansione del file se non ha dieci minuti.

   * **Elimina risultati precedenti a:** Specificare il tempo, in numero di giorni, da attendere prima di eliminare i file e le cartelle con un valore maggiore del valore specificato. Questa impostazione è utile per evitare che la cartella dei risultati diventi piena. Il valore -1 giorni indica di non eliminare mai la cartella dei risultati. Il valore predefinito è -1.
   * **Nome cartella risultati:** Specifica il nome della cartella in cui memorizzare i risultati. Se i risultati non vengono visualizzati in questa cartella, controlla la cartella degli errori. I file di sola lettura non vengono elaborati e vengono salvati nella cartella degli errori. È possibile utilizzare un percorso assoluto o relativo con i seguenti pattern di file:

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
      * Ad esempio, se è alle 20 del 17 luglio 2009 e si specifica C:/Test/WF0/failed/%Y/%M/%D/%H/, la cartella dei risultati è C:/Test/WF0/failed/2009/07/17/20.
      * Se il percorso non è assoluto ma relativo, la cartella viene creata all’interno della cartella controllata. Il valore predefinito è result/%Y/%M/%D/, ovvero la cartella Risultato all&#39;interno della cartella controllata. Per ulteriori informazioni sui pattern di file, vedere [Informazioni sui pattern di file](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns).
   * **Nome cartella errori:** Specifica la cartella in cui vengono salvati i file non riusciti. Questa posizione è sempre relativa alla cartella controllata. È possibile utilizzare i pattern di file, come descritto per Cartella risultati.
   * **Mantieni nome cartella:** Specificare la cartella in cui vengono archiviati i file dopo la scansione e la raccolta riuscite. Il percorso può essere una directory assoluta, relativa o null. È possibile utilizzare i pattern di file, come descritto per Cartella risultati. Il valore predefinito è preserve/%Y/%M/%D/.
   * **Dimensione batch:** Specifica il numero di file o cartelle da raccogliere per scansione. Impedisce un sovraccarico del sistema; la scansione di troppi file alla volta può causare un arresto anomalo. Il valore predefinito è 2.

      Se l’intervallo di scansione è piccolo, i thread eseguono spesso la scansione della cartella di input. Se i file vengono rilasciati frequentemente nella cartella controllata, è necessario mantenere l&#39;intervallo di scansione ridotto. Se i file vengono eliminati raramente, utilizza un intervallo di scansione più ampio in modo che gli altri servizi possano utilizzare i thread.

   * **Limitazione su:** Quando questa opzione è abilitata, limita il numero di processi di cartelle controllati che AEM i processi dei moduli in un dato momento. Il valore Dimensione batch determina il numero massimo di processi. Per ulteriori informazioni, consulta [limitazione](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-throttling)
   * **Sovrascrivi file esistenti con nome simile**: Se impostato su True, i file nella cartella dei risultati e nella cartella di conservazione vengono sovrascritti. Se impostato su False, il nome verrà utilizzato per i file e le cartelle con un suffisso di indice numerico. Il valore predefinito è False.
   * **Mantieni file in caso di errore:** Se impostato su True, i file di input vengono mantenuti in caso di errore. Il valore predefinito è vero.
   * **Includi file con pattern:** Specificare un elenco di pattern delimitato da punti e virgola (;) utilizzato dalla cartella controllata per determinare le cartelle e i file da analizzare e raccogliere. Ad esempio, se viene inserito il pattern di file di inclusione, vengono prelevati tutti i file e le cartelle corrispondenti all’input. Per ulteriori informazioni, consulta [Guida all’amministrazione](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md)
   * **Richiama la cartella osservata in modo asincrono:** Identifica il tipo di chiamata come asincrono o sincrono. Il valore predefinito è asincrono. L’asincrono è consigliato per i processi a lunga durata, mentre quello sincrono è consigliato per i processi transitori o a breve durata.
   * **Abilita cartella osservata:** Quando questa opzione è abilitata, la cartella di controllo è abilitata. Il valore predefinito è True.



## Modifica delle proprietà di una cartella osservata esistente {#modify-properties-of-an-existing-watched-folder}

Oltre a modificare il nome della cartella controllata, è possibile modificare tutte le proprietà di una cartella guardata esistente. Esegui i seguenti passaggi per modificare le proprietà di una cartella di controllo esistente:

1. Tocca **Adobe Experience Manager** nell’angolo in alto a sinistra dello schermo.
1. Tocca **Strumenti** > **Forms** > **Configura la cartella osservata.** Viene visualizzato un elenco di cartelle controllate già configurate.
1. Sul lato sinistro della schermata Cartella osservata, seleziona la cartella di controllo e tocca **Modifica.** Viene visualizzato un elenco dei campi necessari per creare la cartella controllata. I campi elencati nel **Base** La scheda è obbligatoria. La scheda avanzata contiene altri campi. La maggior parte di questi campi contiene un valore predefinito. Puoi modificare queste proprietà in base alle tue esigenze.
1. Dopo aver modificato le proprietà, tocca **Aggiorna**. Le proprietà modificate vengono salvate.
