---
title: Creare o configurare una cartella esaminata
seo-title: Creare o configurare una cartella esaminata
description: Scoprite come creare o eliminare una cartella esaminata o come modificare le proprietà di una cartella esaminata esistente.
seo-description: Scoprite come creare o eliminare una cartella esaminata o come modificare le proprietà di una cartella esaminata esistente.
uuid: 659d4d8c-99b8-40dd-b884-bfee4d476fe1
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 0ce7b338-6686-49b3-b58b-e7ab6b670708
translation-type: tm+mt
source-git-commit: 726163106ddb80600eaa7cc09b1a2e9b035a223e
workflow-type: tm+mt
source-wordcount: '1844'
ht-degree: 0%

---


# Creare o configurare una cartella controllata {#create-or-configure-a-watched-folder}

Un amministratore può configurare una cartella di rete, nota come *cartella controllata*, in modo che quando un utente inserisce un file (ad esempio un file PDF) nella cartella esaminata, venga avviata un&#39;operazione preconfigurata e il file venga manipolato. Dopo l&#39;esecuzione dell&#39;operazione specificata, l&#39;operazione salva il file modificato in una cartella di output specificata. Per informazioni dettagliate sull&#39;amministrazione di una cartella esaminata, vedere [Guida di amministrazione](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md).

È possibile utilizzare l’interfaccia utente della cartella esaminata per:

* Creare una cartella esaminata
* Modifica delle proprietà di una cartella esaminata esistente
* Eliminare una cartella esaminata

## Creare una cartella esaminata {#create-a-watched-folder}

Prima di configurare una cartella esaminata, accertatevi di quanto segue:

* Le cartelle esaminate sono una funzione avanzata dei moduli AEM. Richiede il funzionamento AEM pacchetto aggiuntivo moduli. Verificate che  pacchetto aggiuntivo AEM Forms appropriato sia installato e configurato.
* Potete creare la cartella esaminata in un archivio condiviso o locale. Verificare che AEM&#39;utente di moduli configurato per eseguire la cartella esaminata disponga delle autorizzazioni di lettura e scrittura sulla cartella esaminata.
* È possibile utilizzare un servizio, un flusso di lavoro o uno script per automatizzare un&#39;operazione con una cartella esaminata. Assicurarsi che il servizio, il flusso di lavoro o lo script corrispondente siano stati creati e pronti per l&#39;esecuzione. Per informazioni sulla creazione di un servizio, di un flusso di lavoro e di uno script, vedere [Vari metodi di elaborazione dei file](/help/forms/using/watched-folder-in-aem-forms.md#various-methods-for-processing-files).
* Una cartella esaminata ha diverse proprietà, vedere [Proprietà cartella esaminata](watched-folder-in-aem-forms.md#watchedfolderproperties).

Per creare una cartella esaminata, effettuate le seguenti operazioni:

1. Toccate l&#39;icona **Adobe Experience Manager** nell&#39;angolo superiore sinistro dello schermo.
1. Toccate **Strumenti** > **Forms** > **Configura cartella esaminata.** Viene visualizzato un elenco di cartelle esaminate già configurate.
1. Toccate **Nuovo**. Viene visualizzato un elenco dei campi necessari per creare la cartella esaminata:

   * **Nome**: Identifica la cartella esaminata. Utilizzate solo caratteri alfanumerici per il nome.
   * **Percorso**: Specifica il percorso della cartella esaminata. In un ambiente cluster, questa impostazione deve puntare a una cartella di rete condivisa accessibile a ogni utente che esegue AEM su nodi diversi di un cluster.
   * **Elabora file utilizzando**: Il tipo di processo da avviare. È possibile specificare flusso di lavoro, script o servizio.
   * **Nome servizio/Percorso script/Percorso** flusso di lavoro: Il comportamento del campo è basato sul valore specificato per il campo  **Process Files** Using. Potete specificare i seguenti valori:

      * Per Flusso di lavoro, specificate il modello di flusso di lavoro da eseguire. Ad esempio, /etc/workflow/models/&lt;nome_flusso di lavoro>/jcr:content/model
      * Per Script, specificate il percorso JCR dello script da eseguire. Ad esempio, /etc/watchfolder/test/testScript.ecma
      * Per Servizio, specificate il filtro utilizzato per individuare un servizio OSGi. Il servizio è registrato come implementazione dell’interfaccia com.adobe.aemfd.watchfolder.service.api.ContentProcessor. Ad esempio, il codice seguente è un&#39;implementazione personalizzata dell&#39;interfaccia ContentProcessor con una proprietà personalizzata (foo=bar).

   >[!NOTE]
   >
   >Se si è selezionato **Service** per il campo **Process Files Using**, il valore del campo Service Name(inputProcessorType) deve essere racchiuso tra parentesi. Ad esempio, (foo=bar).

   ```java
   @Component(metatype = true, immediate = true, label = "WF Test Service", description = "WF Test Service")
   @Service(value = {OutputWriter.class, ContentProcessor.class})
   @Property(name = "foo", value = "bar")
   public class OutputWriter implements ContentProcessor {
   ```

   * **Pattern** file di output: Specificate un elenco delimitato da punti e virgola (;) di pattern utilizzati da una cartella esaminata per determinare il nome e la posizione dei file e delle cartelle di output. Per ulteriori informazioni sui pattern di file, vedere [Informazioni sui pattern di file](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns).


1. Toccate **Avanzate**. La scheda avanzata contiene altri campi. La maggior parte di questi campi contiene un valore predefinito.

   * **Filtro Payload Mapper:** quando create una cartella esaminata, crea una struttura di cartelle all’interno della cartella esaminata. La struttura delle cartelle contiene le cartelle stage, result, preserve, input e failure. La struttura delle cartelle può fungere da payload di input per il flusso di lavoro e accettare l’output da un flusso di lavoro. Può anche elencare i punti di errore, se presenti. La struttura di un payload è diversa dalla struttura di una cartella controllata. È possibile creare script personalizzati per mappare la struttura di una cartella esaminata al payload. Tale script è denominato filtro di mappatura payload. Sono disponibili due implementazioni di payload mapper out-of-the-box. Se non disponete di [un&#39;implementazione personalizzata](/help/forms/using/watched-folder-in-aem-forms.md#creating-a-custom-payload-mapper-filter), utilizzate un&#39;implementazione out-of-the-box:

      * **Mappatore predefinito:** utilizzate il mapping payload predefinito per mantenere il contenuto di input e output delle cartelle esaminate in cartelle di input e output separate nel payload.
      * **Mappatore di payload semplice basato su file:** utilizzate il mappatore di payload semplice basato su file per mantenere i contenuti di input e output direttamente nella cartella payload. Non crea alcuna gerarchia aggiuntiva, come il mappatore predefinito.
   * **Modalità** di esecuzione: Specificate l&#39;elenco separato da virgole delle modalità di esecuzione consentite per l&#39;esecuzione del flusso di lavoro.
   * **Timeout Dei File In Fase Dopo**: Specificate il numero di secondi di attesa prima che un file o una cartella di input già prelevato per l’elaborazione venga trattato come se fosse scaduto e contrassegnato come un errore. Il meccanismo di timeout viene attivato solo quando il valore di questa proprietà è un numero positivo.
   * **Elimina i file in fase di timeout quando vengono ridotti**: Se abilitata, il meccanismo  **Time Out** Staged Files Aftermeccanismo è attivato solo quando la limitazione è attivata per la cartella esaminata.
   * **Scansiona cartella di input dopo ogni:** specifica l’intervallo di tempo, in secondi, per la scansione della cartella controllata per gli input. A meno che l’impostazione Limita non sia abilitata, l’intervallo di sondaggio deve essere più lungo del tempo necessario per elaborare un processo medio; in caso contrario, il sistema potrebbe sovraccaricarsi. Il valore dell&#39;intervallo deve essere maggiore o uguale a uno.
   * **Escludi pattern** file: Specificate un elenco delimitato da punti e virgola (;) di pattern utilizzati da una cartella esaminata per determinare quali file e cartelle analizzare e acquisire. Qualsiasi file o cartella con il pattern specificato non viene sottoposto a scansione per l&#39;elaborazione. Per ulteriori informazioni sui pattern di file, vedere [Informazioni sui pattern di file](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns).
   * **Includi pattern** file: Specificate un elenco delimitato da punti e virgola (;) di pattern utilizzati dalla cartella esaminata per determinare quali cartelle e file analizzare e acquisire. Ad esempio, se il pattern di file Includi è input&amp;ast;, tutti i file e le cartelle che corrispondono a input&amp;ast; vengono prese. Il valore predefinito è &amp;ast; e indica tutti i file e le cartelle. Per ulteriori informazioni sui pattern di file, vedere [Informazioni sui pattern di file](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns).
   * **Tempo di attesa:** specificate il tempo, in millisecondi, di attesa prima di eseguire la scansione di una cartella o di un file dopo la creazione. Ad esempio, se il tempo di attesa è di 3.600.000 millisecondi (un&#39;ora) e il file è stato creato un minuto fa, questo file verrà recuperato dopo che sono passati 59 o più minuti. Il valore predefinito è 0.

      Questa impostazione è utile per fare in modo che tutto il contenuto del file o della cartella venga copiato nella cartella di input. Ad esempio, se si dispone di un file di grandi dimensioni da elaborare e il file richiede dieci minuti per il download, impostare il tempo di attesa su 10&amp;ast;60 &amp;ast;1000 millisecondi. Questo intervallo impedisce alla cartella esaminata di eseguire la scansione del file se non ha una durata di dieci minuti.

   * **Elimina risultati precedenti a:** specifica il tempo, in numero di giorni, da attendere prima di eliminare i file e le cartelle con un valore maggiore di quello specificato. Questa impostazione è utile per evitare che la cartella dei risultati diventi piena. Un valore pari a -1 giorni indica di non eliminare mai la cartella dei risultati. Il valore predefinito è -1.
   * **Nome cartella risultati:** specificate il nome della cartella in cui memorizzare i risultati. Se i risultati non vengono visualizzati in questa cartella, controllare la cartella degli errori. I file di sola lettura non vengono elaborati e vengono salvati nella cartella degli errori. È possibile utilizzare un percorso assoluto o relativo con i seguenti pattern di file:

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
      * Ad esempio, se il numero è alle 20 del 17 luglio 2009 e si specifica C:/Test/WF0/failure/%Y/%M/%D/%H/, la cartella dei risultati è C:/Test/WF0/failure/2009/07/17/20.
      * Se il percorso non è assoluto ma relativo, la cartella viene creata all’interno della cartella esaminata. Il valore predefinito è result/%Y/%M/%D/, ovvero la cartella dei risultati all&#39;interno della cartella esaminata. Per ulteriori informazioni sui pattern di file, vedere [Informazioni sui pattern di file](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns).
   * **Nome cartella errore:** specificate la cartella in cui vengono salvati i file con errore. Questo percorso è sempre relativo alla cartella esaminata. È possibile utilizzare i pattern di file, come descritto per Cartella risultati.
   * **Mantieni nome cartella:** specificate la cartella in cui i file vengono memorizzati dopo la scansione e il prelievo. Il percorso può essere assoluto, relativo o nullo. È possibile utilizzare i pattern di file, come descritto per Cartella risultati. Il valore predefinito è preserve/%Y/%M/%D/.
   * **Dimensione batch:** specificare il numero di file o cartelle da acquisire per scansione. impedisce un sovraccarico del sistema; la scansione di troppi file alla volta può causare un arresto anomalo. Il valore predefinito è 2.

      Se l’intervallo di scansione è ridotto, i thread eseguono spesso la scansione della cartella di input. Se i file vengono rilasciati frequentemente nella cartella esaminata, è necessario mantenere l&#39;intervallo di scansione ridotto. Se i file vengono omessi raramente, usate un intervallo di scansione maggiore in modo che gli altri servizi possano usare i thread.

   * **Limita su:** quando questa opzione è abilitata, limita il numero di processi di cartelle controllati che AEM i moduli vengono elaborati in un dato momento. Il valore Dimensione batch determina il numero massimo di processi. Per ulteriori informazioni, vedere [limitazione](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-throttling)
   * **Sovrascrivi file esistenti con nome** simile: Se è impostata su True, i file nella cartella dei risultati e nella cartella preserve vengono sovrascritti. Se è impostata su False, per il nome vengono utilizzati file e cartelle con un suffisso indice numerico. Il valore predefinito è False.
   * **Mantieni file in caso di errore:** se è impostata su True, i file di input vengono conservati in caso di errore. Il valore predefinito è true.
   * **Includi file con pattern:** specificate un elenco delimitato da punti e virgola (;) di pattern utilizzato dalla cartella esaminata per determinare le cartelle e i file da acquisire e acquisire. Ad esempio, se viene inserito il pattern di file Includi, vengono raccolti tutti i file e le cartelle corrispondenti a quello immesso. Per ulteriori informazioni, vedere [Guida di amministrazione](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md)
   * **Richiama cartella esaminata in modo asincrono:** identifica il tipo di chiamata come asincrono o sincrono. Il valore predefinito è asincrono. Asincrona è consigliato per i processi di lunga durata, mentre sincrono è consigliato per i processi transitori o di breve durata.
   * **Abilita cartella esaminata:** quando questa opzione è abilitata, la cartella di controllo è abilitata. Il valore predefinito è True.



## Modificare le proprietà di una cartella esaminata esistente {#modify-properties-of-an-existing-watched-folder}

Oltre a modificare il nome della cartella esaminata, potete modificare tutte le proprietà di una cartella esaminata esistente. Per modificare le proprietà di una cartella esaminata esistente, effettuate le seguenti operazioni:

1. Toccate l&#39;icona **Adobe Experience Manager** nell&#39;angolo superiore sinistro dello schermo.
1. Toccate **Strumenti** > **Forms** > **Configura cartella esaminata.** Viene visualizzato un elenco di cartelle esaminate già configurate.
1. Sul lato sinistro della schermata Cartella esaminata, selezionate la cartella di controllo e toccate **Modifica.** Viene visualizzato un elenco dei campi necessari per creare la cartella esaminata. I campi elencati nella scheda **Base** sono obbligatori. La scheda avanzata contiene altri campi. La maggior parte di questi campi contiene un valore predefinito. Potete modificare queste proprietà in base alle vostre esigenze.
1. Dopo aver modificato le proprietà, toccare **Aggiorna**. Le proprietà modificate vengono salvate.

