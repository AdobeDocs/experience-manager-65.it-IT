---
title: Creare o configurare una cartella controllata
description: Scopri come creare o eliminare una cartella controllata o modificare le proprietà di una cartella controllata esistente.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
exl-id: b15d8d3b-5e47-4c33-95fe-440fcf96be83
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: Admin, User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '1831'
ht-degree: 0%

---

# Creare o configurare una cartella controllata {#create-or-configure-a-watched-folder}

Un amministratore può configurare una cartella di rete, nota come *cartella controllata*, in modo che, quando un utente inserisce un file (ad esempio un file PDF) nella cartella controllata, venga avviata un&#39;operazione preconfigurata e il file venga manipolato. Dopo aver eseguito l&#39;operazione specificata, il file modificato viene salvato in una cartella di output specificata. Per informazioni dettagliate sull&#39;amministrazione di una cartella controllata, vedere [Guida per l&#39;amministrazione](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md).

Puoi utilizzare l’interfaccia utente della cartella controllata per:

* Creare una cartella controllata
* Modificare le proprietà di una cartella controllata esistente
* Eliminare una cartella controllata

## Creare una cartella controllata {#create-a-watched-folder}

Prima di configurare una cartella controllata, verifica quanto segue:

* Le cartelle controllate sono una funzione avanzata dei moduli AEM. Per funzionare è necessario il pacchetto aggiuntivo AEM forms. Verifica che sia installato e configurato il pacchetto del componente aggiuntivo AEM Forms appropriato.
* Puoi creare la cartella controllata in un archivio condiviso o in un archivio locale. Verificare che l&#39;utente di moduli AEM configurato per eseguire la cartella controllata disponga di autorizzazioni di lettura e scrittura per la cartella controllata.
* Puoi utilizzare un servizio, un flusso di lavoro o uno script per automatizzare un’operazione con una cartella controllata. Assicurati che il servizio, il flusso di lavoro o uno script corrispondente sia stato creato e sia pronto per l’esecuzione. Per informazioni sulla creazione di un servizio, un flusso di lavoro e uno script, vedere [Vari metodi di elaborazione dei file](/help/forms/using/watched-folder-in-aem-forms.md#various-methods-for-processing-files).
* Una cartella controllata ha diverse proprietà. Vedere [Proprietà cartella controllata](watched-folder-in-aem-forms.md#watchedfolderproperties).

Per creare una cartella controllata, effettua le seguenti operazioni:

1. Seleziona l&#39;icona **Adobe Experience Manager** nell&#39;angolo superiore sinistro dello schermo.
1. Seleziona **Strumenti** > **Forms** > **Configura cartella controllata.** Viene visualizzato un elenco delle cartelle già configurate.
1. Seleziona **Nuovo**. Viene visualizzato un elenco dei campi necessari per creare la cartella controllata:

   * **Nome**: identifica la cartella controllata. Utilizza solo caratteri alfanumerici per il nome.
   * **Percorso**: specifica il percorso della cartella controllata. In un ambiente cluster, questa impostazione deve puntare a una cartella di rete condivisa accessibile a tutti gli utenti che eseguono AEM su nodi diversi di un cluster.
   * **Elabora file tramite**: tipo di processo da avviare. Puoi specificare flusso di lavoro, script o servizio.
   * **Nome servizio/Percorso script/Percorso flusso di lavoro**: il comportamento del campo si basa sul valore specificato per il campo **File di processo che utilizzano**. È possibile specificare i seguenti valori:

      * Per Flusso di lavoro, specifica il modello di flusso di lavoro da eseguire. Ad esempio, /etc/workflow/models/&lt;nome_flusso di lavoro>/jcr:content/model
      * Per Script, specifica il percorso JCR dello script da eseguire. Ad esempio, /etc/watchfolder/test/testScript.ecma
      * Per Servizio, specifica il filtro utilizzato per individuare un servizio OSGi. Il servizio è registrato come implementazione dell’interfaccia com.adobe.aemfd.watchfolder.service.api.ContentProcessor. Ad esempio, il codice seguente è un’implementazione personalizzata dell’interfaccia ContentProcessor con una proprietà personalizzata (foo=bar).

   >[!NOTE]
   >
   >Se hai selezionato **Servizio** per il campo **Elabora file tramite**, il valore del campo Nome servizio(inputProcessorType) deve essere racchiuso tra parentesi. Ad esempio (foo=bar).

   ```java
   @Component(metatype = true, immediate = true, label = "WF Test Service", description = "WF Test Service")
   @Service(value = {OutputWriter.class, ContentProcessor.class})
   @Property(name = "foo", value = "bar")
   public class OutputWriter implements ContentProcessor {
   ```

   * **Pattern file di output**: specificare un elenco delimitato da punti e virgola (;) dei pattern utilizzati da una cartella controllata per determinare il nome e il percorso dei file e delle cartelle di output. Per ulteriori informazioni sui modelli di file, vedere [Informazioni sui modelli di file](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns).

1. Seleziona **Avanzate**. La scheda avanzata contiene altri campi. La maggior parte di questi campi contiene un valore predefinito.

   * **Filtro mappatore payload:** Quando si crea una cartella controllata, viene creata una struttura di cartelle all&#39;interno della cartella controllata. La struttura di cartelle include cartelle di staging, risultato, conservazione, input e errore. La struttura di cartelle può fungere da payload di input per il flusso di lavoro e accettare l’output da un flusso di lavoro. Può anche elencare eventuali punti di errore. La struttura di un payload è diversa da quella di una cartella controllata. Puoi scrivere script personalizzati per mappare la struttura di una cartella controllata al payload. Tale script è denominato filtro di mappatura payload. Sono disponibili due implementazioni predefinite per la mappatura del payload. Se non disponi di [un&#39;implementazione personalizzata](/help/forms/using/watched-folder-in-aem-forms.md#creating-a-custom-payload-mapper-filter), utilizza un&#39;implementazione preconfigurata:

      * **Mapper predefinito:** Utilizza il mapper del payload predefinito per mantenere i contenuti di input e output delle cartelle controllate in cartelle di input e output separate nel payload.
      * **Mappatore payload semplice basato su file:** Utilizzare il mapper payload semplice basato su file per mantenere i contenuti di input e output direttamente nella cartella del payload. Non crea alcuna gerarchia aggiuntiva, come l’mappatore predefinito.

   * **Modalità di esecuzione**: specificare l&#39;elenco separato da virgole delle modalità di esecuzione consentite per l&#39;esecuzione del flusso di lavoro.
   * **Timeout file di staging dopo**: specificare il numero di secondi di attesa prima che un file o una cartella di input già raccolti per l&#39;elaborazione venga considerato come scaduto e contrassegnato come errore. Il meccanismo di timeout si attiva solo quando il valore di questa proprietà è un numero positivo.
   * **Elimina file di staging con timeout con limitazione**: se attivato, il meccanismo **Esegui timeout file di staging dopo** viene attivato solo quando la limitazione è attivata per la cartella controllata.
   * **Scansiona cartella di input ogni:** Specificare l&#39;intervallo di tempo, in secondi, per la ricerca di input nella cartella controllata. Se l&#39;impostazione Limitazione non è abilitata, l&#39;intervallo di polling deve essere più lungo del tempo necessario per elaborare un processo medio. In caso contrario, il sistema potrebbe sovraccaricare. Il valore dell&#39;intervallo deve essere maggiore o uguale a uno.
   * **Escludi pattern file**: specificare un elenco delimitato da punti e virgola (;) di pattern utilizzati da una cartella controllata per determinare quali file e cartelle analizzare e raccogliere. Qualsiasi file o cartella con il modello specificato non viene analizzato per l&#39;elaborazione. Per ulteriori informazioni sui modelli di file, vedere [Informazioni sui modelli di file](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns).
   * **Includi pattern file**: specificare un elenco delimitato da punti e virgola (;) di pattern utilizzati dalla cartella controllata per determinare quali cartelle e file analizzare e raccogliere. Ad esempio, se il modello di file di inclusione è input&ast;, vengono selezionati tutti i file e le cartelle che corrispondono a input&ast;. Il valore predefinito è &ast; e indica tutti i file e le cartelle. Per ulteriori informazioni sui modelli di file, vedere [Informazioni sui modelli di file](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns).
   * **Tempo di attesa:** Specificare il tempo, in millisecondi, di attesa prima della scansione di una cartella o di un file dopo la creazione. Ad esempio, se il tempo di attesa è di 3.600.000 millisecondi (un’ora) e il file è stato creato un minuto fa, questo file verrà acquisito dopo 59 o più minuti. Il valore predefinito è 0.

     Questa impostazione è utile per garantire che tutto il contenuto del file o della cartella venga copiato nella cartella di input. Ad esempio, se si dispone di un file di grandi dimensioni da elaborare e il download richiede dieci minuti, impostare il tempo di attesa su 10&ast;60 &ast;1000 millisecondi. Questo intervallo impedisce alla cartella controllata di eseguire la scansione del file se non ha dieci minuti.

   * **Elimina risultati precedenti a:** Specificare il tempo, in numero di giorni, di attesa prima dell&#39;eliminazione dei file e delle cartelle precedenti al valore specificato. Questa impostazione è utile per garantire che la cartella dei risultati non sia piena. Un valore pari a -1 giorni indica di non eliminare mai la cartella dei risultati. Il valore predefinito è -1.
   * **Nome cartella risultati:** Specificare il nome della cartella in cui archiviare i risultati. Se i risultati non vengono visualizzati in questa cartella, selezionare la cartella con errori. I file di sola lettura non vengono elaborati e vengono salvati nella cartella degli errori. È possibile utilizzare un percorso assoluto o relativo con i seguenti modelli di file:

      * %F = prefisso nome file
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
      * Ad esempio, se sono le 20:00 del 17 luglio 2009 e si specifica C:/Test/WF0/failure/%Y/%M/%D/%H/, la cartella dei risultati sarà C:/Test/WF0/failure/2009/07/17/20.
      * Se il percorso non è assoluto ma relativo, la cartella viene creata all’interno della cartella controllata. Il valore predefinito è result/%Y/%M/%D/, ovvero la cartella Result all&#39;interno della cartella controllata. Per ulteriori informazioni sui modelli di file, vedere [Informazioni sui modelli di file](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns).

   * **Nome cartella errore:** Specificare la cartella in cui vengono salvati i file non riusciti. Questo percorso è sempre relativo alla cartella controllata. È possibile utilizzare i modelli di file, come descritto per Cartella risultati.
   * **Mantieni nome cartella:** Specificare la cartella in cui sono archiviati i file dopo l&#39;analisi e il prelievo completati. Il percorso può essere una directory assoluta, relativa o null. È possibile utilizzare i modelli di file, come descritto per Cartella risultati. Il valore predefinito è preserve/%Y/%M/%D/.
   * **Dimensione batch:** Specificare il numero di file o cartelle da prelevare per analisi. Impedisce un sovraccarico sul sistema; la scansione di troppi file contemporaneamente può causare un arresto anomalo. Il valore predefinito è 2.

     Se l&#39;intervallo di scansione è ridotto, i thread eseguono spesso la scansione della cartella di input. Se i file vengono rilasciati frequentemente nella cartella controllata, è necessario mantenere l&#39;intervallo di scansione ridotto. Se i file vengono eliminati raramente, utilizzare un intervallo di scansione più ampio in modo che gli altri servizi possano utilizzare i thread.

   * **Limitazione attivata:** Quando questa opzione è abilitata, limita il numero di processi delle cartelle controllate che l&#39;AEM elabora in un dato momento. Il valore Dimensione batch determina il numero massimo di processi. Per ulteriori informazioni, vedere [limitazione](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-throttling)
   * **Sovrascrivi file esistenti con nome simile**: se è impostato su True, i file presenti nella cartella dei risultati e nella cartella di conservazione vengono sovrascritti. Se è impostato su False, vengono utilizzati file e cartelle con un suffisso di indice numerico per il nome. Il valore predefinito è False.
   * **Mantieni file in caso di errore:** Se è impostato su True, i file di input vengono conservati in caso di errore. Il valore predefinito è true.
   * **Includi file con pattern:** Specificare un elenco delimitato da punti e virgola (;) dei pattern utilizzati dalla cartella controllata per determinare quali cartelle e file analizzare e raccogliere. Ad esempio, se viene immesso il Pattern di inclusione file, vengono selezionati tutti i file e le cartelle che corrispondono all&#39;input. Per ulteriori informazioni, vedere [Guida per l&#39;amministrazione](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md)
   * **Richiama cartella controllata in modo asincrono:** identifica il tipo di chiamata come asincrona o sincrona. Il valore predefinito è asincrono. L&#39;asincronia è consigliata per i processi di lunga durata, mentre la sincronia è consigliata per i processi transitori o di breve durata.
   * **Abilita cartella controllata:** Quando questa opzione è abilitata, la cartella di controllo è abilitata. Il valore predefinito è True.

## Modificare le proprietà di una cartella controllata esistente {#modify-properties-of-an-existing-watched-folder}

Oltre a modificare il nome della cartella controllata, è possibile modificare tutte le proprietà di una cartella controllata esistente. Per modificare le proprietà di una cartella controllata esistente, effettua le seguenti operazioni:

1. Seleziona l&#39;icona **Adobe Experience Manager** nell&#39;angolo superiore sinistro dello schermo.
1. Seleziona **Strumenti** > **Forms** > **Configura cartella controllata.** Viene visualizzato un elenco delle cartelle già configurate.
1. Nella parte sinistra della schermata Cartella controllata, selezionare la cartella di controllo e selezionare **Modifica.** Viene visualizzato un elenco dei campi necessari per creare la cartella controllata. I campi elencati nella scheda **Base** sono obbligatori. La scheda avanzata contiene altri campi. La maggior parte di questi campi contiene un valore predefinito. Puoi modificare queste proprietà in base alle tue esigenze.
1. Dopo aver modificato le proprietà, selezionare **Aggiorna**. Le proprietà modificate vengono salvate.
