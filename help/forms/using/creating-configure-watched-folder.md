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

Un amministratore può configurare una cartella di rete, nota come *cartella controllata*, in modo che, quando un utente inserisce un file (ad esempio un file PDF) nella cartella controllata, venga avviata un’operazione preconfigurata e il file venga manipolato. Dopo aver eseguito l&#39;operazione specificata, il file modificato viene salvato in una cartella di output specificata. Per informazioni dettagliate sull’amministrazione di una cartella controllata, consulta [Aiuto per l’amministrazione](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md).

Puoi utilizzare l’interfaccia utente della cartella controllata per:

* Creare una cartella controllata
* Modificare le proprietà di una cartella controllata esistente
* Eliminare una cartella controllata

## Creare una cartella controllata {#create-a-watched-folder}

Prima di configurare una cartella controllata, verifica quanto segue:

* Le cartelle controllate sono una funzione avanzata dei moduli AEM. Per funzionare è necessario il pacchetto aggiuntivo AEM forms. Verifica che sia installato e configurato il pacchetto del componente aggiuntivo AEM Forms appropriato.
* Puoi creare la cartella controllata in un archivio condiviso o in un archivio locale. Verificare che l&#39;utente di moduli AEM configurato per eseguire la cartella controllata disponga di autorizzazioni di lettura e scrittura per la cartella controllata.
* Puoi utilizzare un servizio, un flusso di lavoro o uno script per automatizzare un’operazione con una cartella controllata. Assicurati che il servizio, il flusso di lavoro o uno script corrispondente sia stato creato e sia pronto per l’esecuzione. Per informazioni sulla creazione di un servizio, un flusso di lavoro e uno script, consulta [Vari metodi di elaborazione dei file](/help/forms/using/watched-folder-in-aem-forms.md#various-methods-for-processing-files).
* Una cartella controllata ha varie proprietà, vedi [Proprietà cartella controllata](watched-folder-in-aem-forms.md#watchedfolderproperties).

Per creare una cartella controllata, effettua le seguenti operazioni:

1. Seleziona **Adobe Experience Manager** nell&#39;angolo superiore sinistro dello schermo.
1. Seleziona **Strumenti** > **Forms** > **Configura cartella controllata.** Viene visualizzato un elenco delle cartelle controllate già configurate.
1. Seleziona **Nuovo**. Viene visualizzato un elenco dei campi necessari per creare la cartella controllata:

   * **Nome**: identifica la cartella controllata. Utilizza solo caratteri alfanumerici per il nome.
   * **Percorso**: specifica il percorso della cartella controllata. In un ambiente cluster, questa impostazione deve puntare a una cartella di rete condivisa accessibile a tutti gli utenti che eseguono AEM su nodi diversi di un cluster.
   * **Elabora file tramite**: tipo di processo da avviare. Puoi specificare flusso di lavoro, script o servizio.
   * **Nome servizio/Percorso script/Percorso flusso di lavoro**: il comportamento del campo è basato sul valore specificato per **Elabora file tramite** campo. È possibile specificare i seguenti valori:

      * Per Flusso di lavoro, specifica il modello di flusso di lavoro da eseguire. Ad esempio, /etc/workflow/models/&lt;workflow_name>/jcr:content/model
      * Per Script, specifica il percorso JCR dello script da eseguire. Ad esempio, /etc/watchfolder/test/testScript.ecma
      * Per Servizio, specifica il filtro utilizzato per individuare un servizio OSGi. Il servizio è registrato come implementazione dell’interfaccia com.adobe.aemfd.watchfolder.service.api.ContentProcessor. Ad esempio, il codice seguente è un’implementazione personalizzata dell’interfaccia ContentProcessor con una proprietà personalizzata (foo=bar).

   >[!NOTE]
   >
   >Se hai selezionato **Servizio** per **Elabora file tramite** , il valore del campo Nome servizio (inputProcessorType) deve essere racchiuso tra parentesi. Ad esempio (foo=bar).

   ```java
   @Component(metatype = true, immediate = true, label = "WF Test Service", description = "WF Test Service")
   @Service(value = {OutputWriter.class, ContentProcessor.class})
   @Property(name = "foo", value = "bar")
   public class OutputWriter implements ContentProcessor {
   ```

   * **Pattern file di output**: specifica un elenco delimitato da punti e virgola (;) di pattern utilizzati da una cartella controllata per determinare il nome e la posizione dei file e delle cartelle di output. Per ulteriori informazioni sui modelli di file, vedere [Informazioni sui pattern dei file](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns).

1. Seleziona **Avanzate**. La scheda avanzata contiene altri campi. La maggior parte di questi campi contiene un valore predefinito.

   * **Filtro mappatore payload:** Quando si crea una cartella controllata, viene creata una struttura di cartelle all&#39;interno della cartella controllata. La struttura di cartelle include cartelle di staging, risultato, conservazione, input e errore. La struttura di cartelle può fungere da payload di input per il flusso di lavoro e accettare l’output da un flusso di lavoro. Può anche elencare eventuali punti di errore. La struttura di un payload è diversa da quella di una cartella controllata. Puoi scrivere script personalizzati per mappare la struttura di una cartella controllata al payload. Tale script è denominato filtro di mappatura payload. Sono disponibili due implementazioni predefinite per la mappatura del payload. Se non ha [un’implementazione personalizzata](/help/forms/using/watched-folder-in-aem-forms.md#creating-a-custom-payload-mapper-filter), utilizza un’implementazione preconfigurata:

      * **Mappatore predefinito:** Utilizza il mappatore del payload predefinito per mantenere i contenuti di input e output delle cartelle controllate in cartelle di input e output separate nel payload.
      * **Semplice mappatura del payload basato su file:** Utilizza Simple File-based Payload Mapper per mantenere i contenuti di input e output direttamente nella cartella del payload. Non crea alcuna gerarchia aggiuntiva, come l’mappatore predefinito.

   * **Modalità di esecuzione**: specifica l’elenco separato da virgole delle modalità di esecuzione consentite per l’esecuzione del flusso di lavoro.
   * **Esegui il timeout di file di staging dopo**: specifica per quanti secondi si deve attendere che un file/una cartella di input già prelevato per l’elaborazione venga considerato scaduto e contrassegnato come non riuscito. Il meccanismo di timeout si attiva solo quando il valore di questa proprietà è un numero positivo.
   * **Elimina i file di staging con timeout con limitazione**: se abilitata, la **Esegui il timeout di file di staging dopo** il meccanismo è attivato solo quando è attivata la limitazione per la cartella controllata.
   * **Scansiona cartella di input ogni:** Specifica l’intervallo di tempo, in secondi, per la scansione della cartella controllata per gli input. Se l&#39;impostazione Limitazione non è abilitata, l&#39;intervallo di polling deve essere più lungo del tempo necessario per elaborare un processo medio. In caso contrario, il sistema potrebbe sovraccaricare. Il valore dell&#39;intervallo deve essere maggiore o uguale a uno.
   * **Escludi motivo file**: specifica un elenco delimitato da punti e virgola (;) di pattern utilizzati da una cartella controllata per determinare quali file e cartelle analizzare e raccogliere. Qualsiasi file o cartella con il modello specificato non viene analizzato per l&#39;elaborazione. Per ulteriori informazioni sui modelli di file, vedere [Informazioni sui pattern dei file](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns).
   * **Includi pattern file**: specifica un elenco delimitato da punti e virgola (;) di pattern che la cartella controllata utilizza per determinare quali cartelle e file analizzare e raccogliere. Ad esempio, se Includi modello file è input&amp;ast;, vengono selezionati tutti i file e le cartelle che corrispondono a input&amp;ast;. Il valore predefinito è &amp;ast; e indica tutti i file e le cartelle. Per ulteriori informazioni sui modelli di file, vedere [Modelli di file](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns).
   * **Tempo di attesa:** Specifica il tempo, in millisecondi, di attesa prima della scansione di una cartella o di un file dopo la creazione. Ad esempio, se il tempo di attesa è di 3.600.000 millisecondi (un’ora) e il file è stato creato un minuto fa, questo file verrà acquisito dopo 59 o più minuti. Il valore predefinito è 0.

     Questa impostazione è utile per garantire che tutto il contenuto del file o della cartella venga copiato nella cartella di input. Ad esempio, se si dispone di un file di grandi dimensioni da elaborare e il download richiede dieci minuti, impostare il tempo di attesa su 10&amp;ast;60 &amp;ast;1000 millisecondi. Questo intervallo impedisce alla cartella controllata di eseguire la scansione del file se non ha dieci minuti.

   * **Elimina risultati più vecchi di:** Specifica il tempo, in numero di giorni, di attesa prima di eliminare i file e le cartelle più vecchi del valore specificato. Questa impostazione è utile per garantire che la cartella dei risultati non sia piena. Un valore pari a -1 giorni indica di non eliminare mai la cartella dei risultati. Il valore predefinito è -1.
   * **Nome cartella risultati:** Specifica il nome della cartella in cui memorizzare i risultati. Se i risultati non vengono visualizzati in questa cartella, selezionare la cartella con errori. I file di sola lettura non vengono elaborati e vengono salvati nella cartella degli errori. È possibile utilizzare un percorso assoluto o relativo con i seguenti modelli di file:

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
      * Se il percorso non è assoluto ma relativo, la cartella viene creata all’interno della cartella controllata. Il valore predefinito è result/%Y/%M/%D/, ovvero la cartella Result all&#39;interno della cartella controllata. Per ulteriori informazioni sui modelli di file, vedere [Informazioni sui pattern dei file](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns).

   * **Nome cartella errore:** Specificare la cartella in cui vengono salvati i file non riusciti. Questo percorso è sempre relativo alla cartella controllata. È possibile utilizzare i modelli di file, come descritto per Cartella risultati.
   * **Mantieni nome cartella:** Specificare la cartella in cui vengono archiviati i file dopo la scansione e il ritiro. Il percorso può essere una directory assoluta, relativa o null. È possibile utilizzare i modelli di file, come descritto per Cartella risultati. Il valore predefinito è preserve/%Y/%M/%D/.
   * **Dimensione batch:** Specifica il numero di file o cartelle da raccogliere per scansione. Impedisce un sovraccarico sul sistema; la scansione di troppi file contemporaneamente può causare un arresto anomalo. Il valore predefinito è 2.

     Se l&#39;intervallo di scansione è ridotto, i thread eseguono spesso la scansione della cartella di input. Se i file vengono rilasciati frequentemente nella cartella controllata, è necessario mantenere l&#39;intervallo di scansione ridotto. Se i file vengono eliminati raramente, utilizzare un intervallo di scansione più ampio in modo che gli altri servizi possano utilizzare i thread.

   * **Limitazione attivata:** Quando questa opzione è abilitata, limita il numero di processi delle cartelle controllate che AEM elabora in un dato momento. Il valore Dimensione batch determina il numero massimo di processi. Per ulteriori informazioni, consulta [limitazione](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-throttling)
   * **Sovrascrivi file esistenti con un nome simile**: quando è impostato su True, i file nella cartella dei risultati e nella cartella di mantenimento vengono sovrascritti. Se è impostato su False, vengono utilizzati file e cartelle con un suffisso di indice numerico per il nome. Il valore predefinito è False.
   * **Mantieni file in caso di errore:** Se è impostato su True, i file di input vengono conservati in caso di errore. Il valore predefinito è true.
   * **Includi file con pattern:** Specifica un elenco delimitato da punti e virgola (;) di pattern utilizzati dalla cartella controllata per determinare quali cartelle e file analizzare e raccogliere. Ad esempio, se viene immesso il Pattern di inclusione file, vengono selezionati tutti i file e le cartelle che corrispondono all&#39;input. Per ulteriori informazioni, consulta [Aiuto per l’amministrazione](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md)
   * **Richiama cartella controllata in modo asincrono:** Identifica il tipo di chiamata come asincrona o sincrona. Il valore predefinito è asincrono. L&#39;asincronia è consigliata per i processi di lunga durata, mentre la sincronia è consigliata per i processi transitori o di breve durata.
   * **Abilita cartella controllata:** Quando questa opzione è attivata, la cartella di controllo è attivata. Il valore predefinito è True.

## Modificare le proprietà di una cartella controllata esistente {#modify-properties-of-an-existing-watched-folder}

Oltre a modificare il nome della cartella controllata, è possibile modificare tutte le proprietà di una cartella controllata esistente. Per modificare le proprietà di una cartella controllata esistente, effettua le seguenti operazioni:

1. Seleziona la **Adobe Experience Manager** nell’angolo in alto a sinistra dello schermo.
1. Seleziona **Strumenti** > **Forms** > **Configura cartella controllata.** Viene visualizzato un elenco delle cartelle controllate già configurate.
1. Nella parte sinistra della schermata Cartella controllata, seleziona la cartella di controllo e fai clic su **Modifica.** Viene visualizzato un elenco dei campi necessari per creare la cartella controllata. I campi elencati nella **Base** La tabulazione è obbligatoria. La scheda avanzata contiene altri campi. La maggior parte di questi campi contiene un valore predefinito. Puoi modificare queste proprietà in base alle tue esigenze.
1. Dopo aver modificato le proprietà, seleziona **Aggiorna**. Le proprietà modificate vengono salvate.
