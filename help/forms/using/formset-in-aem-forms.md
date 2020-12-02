---
title: Set di moduli in  AEM Forms
seo-title: Set di moduli in  AEM Forms
description: In questo articolo viene presentato un set di moduli e viene illustrato come creare set di moduli unendo moduli HTML5. Questo articolo spiega anche come precompilare i dati XML per un set di moduli e come utilizzare i set di moduli nella gestione del processo.
seo-description: In questo articolo viene presentato un set di moduli e viene illustrato come creare set di moduli unendo moduli HTML5. Questo articolo spiega anche come precompilare i dati XML per un set di moduli e come utilizzare i set di moduli nella gestione del processo.
uuid: a1a2f267-26a9-4f45-bcfc-dbdedad95973
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 80e3eec4-95e0-4731-a0e5-a617e9bcb069
docset: aem65
translation-type: tm+mt
source-git-commit: 998a127ce00c6cbb3db3a81d8a89d97ab9ef7469
workflow-type: tm+mt
source-wordcount: '2860'
ht-degree: 0%

---


# Set di moduli in  AEM Forms{#form-set-in-aem-forms}

## Panoramica {#overview}

Spesso ai clienti viene richiesto di inviare più moduli per richiedere un servizio o un benefit. Si tratta di trovare tutti i moduli pertinenti; e riempirli, inviarli e tenerne traccia separatamente. Inoltre, devono compilare i dettagli comuni più volte nei diversi moduli. L&#39;intero processo diventa complesso e soggetto a errore se si tratta di un numero elevato di moduli. La funzione per i set di moduli di  AEM Forms consente di semplificare l&#39;esperienza utente in tali scenari.

Un set di moduli è un insieme di moduli HTML5 raggruppati e presentati come un singolo set di moduli per gli utenti finali. Quando gli utenti finali iniziano a compilare un set di moduli, si passa direttamente da un modulo all&#39;altro. Alla fine, è possibile inviare tutti i moduli con un solo clic.

 AEM Forms offre agli autori dei moduli un&#39;interfaccia utente intuitiva per creare, configurare e gestire i set di moduli. In qualità di autore, è possibile ordinare i moduli in una sequenza specifica che gli utenti finali dovranno seguire. È inoltre possibile applicare condizioni o espressioni di idoneità a singoli moduli per controllarne la visibilità in base agli input dell&#39;utente. Ad esempio, è possibile configurare il modulo dei dettagli del coniuge in modo che venga visualizzato solo quando lo stato del matrimonio specifica come Sposato.

È inoltre possibile configurare campi comuni in diversi moduli per condividere binding dei dati comuni. In presenza di binding dei dati appropriati, agli utenti finali viene richiesto di compilare le informazioni comuni solo una volta che tali informazioni verranno compilate automaticamente nei moduli successivi.

I set di moduli sono supportati anche &#39;app AEM Forms, consentendo al personale addetto al campo di utilizzare un set di moduli offline, di visitare i clienti, di inserire dati e di sincronizzarsi successivamente con il server AEM Forms  per inviare i dati dei moduli ai processi aziendali.

## Creazione e gestione del set di moduli {#creating-and-managing-form-set}

È possibile associare diversi XDP o modelli di modulo, creati utilizzando Designer, a un set di moduli. I set di moduli possono quindi essere utilizzati per eseguire il rendering selettivo degli XDP in base ai valori immessi dagli utenti nei moduli iniziali e nei relativi profili.

Utilizzare [ interfaccia utente AEM Forms](../../forms/using/introduction-managing-forms.md) per gestire tutti i moduli, i set di moduli e le risorse correlate.

### Creare un set di moduli {#create-a-form-set}

Per creare un set di moduli, effettuare le seguenti operazioni:

1. Selezionate Forms > Forms e documenti.
1. Selezionare Crea > Set di moduli.

1. Nella pagina Aggiungi proprietà, aggiungi i seguenti dettagli e fai clic su Avanti.

   * Titolo: Specifica il titolo del documento. Il titolo consente di identificare il set di moduli nell’interfaccia utente  di AEM Forms.
   * Descrizione: Specifica le informazioni dettagliate sul documento.
   * Tag: Specifica i tag per identificare in modo univoco il set di moduli. I tag consentono di effettuare ricerche nel set di moduli. Per creare i tag, digitate nuovi nomi di tag nella casella Tag.
   * Invia URL: Specifica l&#39;URL in cui vengono inviati i dati per il caso di rappresentazione autonoma del set di moduli (caso di utilizzo di app AEM Forms non ). I dati vengono inviati a questo endpoint come multipart/formdata con il seguente parametro di richiesta:
   * dataXML: Questo parametro contiene una rappresentazione XML dei dati del set di moduli inviati. Se tutti i moduli del set di moduli utilizzano uno schema comune, l&#39;XML viene generato in base a tale schema. In caso contrario, il tag XML principale contiene un tag secondario per ciascun modulo compilato nel set di moduli che contiene i dati per gli allegati del modulo.
   * formsetPath: Percorso del modulo impostato in CRXDE, inviato.
   * Profilo di rendering HTML: È possibile configurare determinate opzioni, quali campi mobili, allegati e supporto delle bozze (per le rappresentazioni dei set di moduli indipendenti) per personalizzare l&#39;aspetto, il comportamento e le interazioni del set di moduli. È possibile personalizzare o estendere il profilo esistente per modificare eventuali impostazioni del profilo modulo HTML.

   ![Set di moduli: aggiungi proprietà](assets/createformset1.png)

1. Nella schermata Seleziona moduli vengono visualizzati i moduli XDP o i file XDP disponibili. Cercare e selezionare i moduli da includere nel set di moduli, quindi fare clic su Aggiungi al set di moduli. Se necessario, cercare di nuovo i moduli da aggiungere. Dopo aver aggiunto tutti i moduli al set di moduli, fare clic su Avanti.

   >[!NOTE]
   >
   >Assicurarsi che i nomi dei campi nei moduli XDP non contengano il carattere punto. In caso contrario, gli script che tentano di risolvere i campi, contenenti caratteri punto, non sono in grado di risolverli.

1. Nella pagina Configura moduli è possibile effettuare le seguenti operazioni:

   * Ordine modulo: Trascinare i moduli per riordinarli. L&#39;ordine del modulo definisce l&#39;ordine in cui i moduli vengono visualizzati all&#39;utente finale nell&#39;app  AEM Forms e nella rappresentazione autonoma.
   * Identificatore modulo: Specifica un&#39;identità univoca per i moduli da utilizzare nelle espressioni di idoneità.
   * Radice dati: Per ciascun modulo del set di moduli, l&#39;autore può configurare l&#39;XPATH in cui i dati di quel particolare modulo sono posizionati nel codice XML inviato. Il valore predefinito è /. Se tutti i moduli del set di moduli sono associati allo schema e condividono lo stesso schema XML, è possibile modificare questo valore. È consigliabile che ogni campo del modulo disponga di un binding dati appropriato specificato in XDP. Se due campi di due moduli diversi condividono il binding dei dati comune, nel campo del secondo modulo vengono visualizzati i valori precompilati del primo modulo. Non eseguire il binding di due sottomoduli con lo stesso contenuto interno con lo stesso nodo XML. Per ulteriori informazioni sulla struttura XML del set di moduli, vedere [Precompila XML per il set di moduli](../../forms/using/formset-in-aem-forms.md#p-prefill-xml-for-form-set-p).
   * Espressione di idoneità: Specifica un&#39;espressione JavaScript che valuta un valore booleano e indica se un modulo in un set di moduli è idoneo alla compilazione. Se è false, all&#39;utente non viene chiesto né mostrato il modulo da compilare. In genere, l&#39;espressione si basa sui valori dei campi acquisiti prima del modulo. Le espressioni contengono anche chiamate all&#39;API fs.valueOf set di moduli per estrarre i valori compilati dall&#39;utente in un campo di un modulo del set di moduli:

   *fs.valueOf(&lt;form Identifier=&quot;&quot;>,  &lt;fieldsom expression=&quot;&quot;>) >  &lt;value>*

   Ad esempio, se nel set di moduli sono presenti due moduli: spese aziendali e spese di viaggio, è possibile aggiungere uno snippet JavaScript nel campo Espressione di idoneità per entrambi i moduli per controllare l&#39;input dell&#39;utente per il tipo di spesa in un modulo. Se l&#39;utente sceglie Spese commerciali, viene eseguito il rendering del modulo Spese aziendali per l&#39;utente finale. Oppure, se l&#39;utente sceglie le spese di viaggio, all&#39;utente finale verrà eseguito il rendering di un altro modulo. Per ulteriori informazioni, vedere Espressione di idoneità.

   Inoltre, l&#39;autore può anche scegliere di rimuovere un modulo dal set di moduli utilizzando l&#39;icona Elimina presente nell&#39;angolo destro di ciascuna riga o aggiungere un altro set di moduli utilizzando l&#39;icona &quot;**+**&quot; nella barra degli strumenti. Questa icona &quot;**+**&quot; indirizza l&#39;utente al passaggio precedente della procedura guidata, utilizzato per selezionare i moduli. Le selezioni esistenti vengono mantenute e ogni ulteriore selezione effettuata deve essere aggiunta al set di moduli utilizzando l&#39;icona Aggiungi a set di moduli nella pagina.

   ![Set di moduli: Configurare i moduli](assets/createformset2.png)

   >[!NOTE]
   >
   >Tutti i moduli utilizzati nel set di moduli sono gestiti &#39;interfaccia utente di AEM Forms.

### Gestione di un set di moduli {#managing-a-form-set}

Una volta creato il set di moduli, è possibile effettuare le seguenti operazioni su tale set di moduli:

* Con un solo clic: Quando il set di moduli viene creato ed elencato nella pagina della risorsa principale, è possibile fare clic sul set di moduli per visualizzarlo. Un set di moduli si apre e visualizza tutti i modelli di modulo (XDP) presenti in tale set.
* Modifica: Facendo clic su Modifica dopo aver selezionato un set di moduli, si apre la schermata Configura modulo visualizzata sopra in Passaggi per creare un set di moduli. È possibile eseguire tutte le funzionalità descritte in questo punto.
* Copia + Incolla: Questo consente di copiare l’intero set di moduli da una posizione e incollarlo nello stesso percorso o in qualsiasi altra cartella.
* Scarica: È possibile scaricare il set di moduli con tutte le relative dipendenze.
* Avvia/Gestisci revisione: Una volta creato il set di moduli, è possibile configurarne la revisione facendo clic su Avvia revisione. Una volta avviata la revisione per un set di moduli, l&#39;opzione Gestisci revisione viene visualizzata all&#39;utente. Nella schermata Gestisci revisione potete aggiornare/terminare la revisione. Per le revisioni aggiunte, potete controllare la revisione e aggiungere eventuali commenti.
* Elimina: Elimina l&#39;intero set di moduli. I moduli nel set di moduli eliminato rimangono nella directory archivio.
* Pubblica/Annulla pubblicazione: Questo consente di pubblicare/annullare la pubblicazione del set di moduli insieme a tutti i moduli in esso contenuti e alle relative risorse.
* Anteprima: Anteprima offre due opzioni: Visualizzate l&#39;anteprima come HTML (senza dati) e l&#39;anteprima personalizzata con i dati di esempio.
* Visualizza/Modifica proprietà: È possibile visualizzare/modificare le proprietà dei metadati di un set di moduli selezionato.

![createformset3](assets/createformset3.png)

### Modificare un set di moduli {#edit-a-form-set}

Per modificare un set di moduli, effettuare le seguenti operazioni:

1. Selezionate Forms > Forms e documenti.
1. Individuare il set di moduli da modificare. Passate il puntatore del mouse sopra di esso e selezionate Modifica ( ![editicon](assets/editicon.png)).
1. Nella pagina Configura moduli è possibile modificare quanto segue:

   * Ordine modulo
   * Identificatore  modulo
   * Radice dati
   * Espressione di idoneità

   È inoltre possibile fare clic sull&#39;icona Elimina corrispondente per eliminare il modulo dal set di moduli.

## Set di moduli in Process Management {#form-set-in-process-management}

Dopo aver creato un set di moduli utilizzando &#39;interfaccia utente di AEM Forms Management, è possibile utilizzare il set di moduli in un punto iniziale o in un&#39;attività Assegna attività tramite Workbench.

### Utilizzo del set di moduli in Task o nel punto iniziale {#using-form-set-in-task-or-start-point}

1. Durante la progettazione di un processo, nella sezione Presentazione e dati di Assign Task/Start Point, selezionare **utilizza una risorsa CRX**. Viene visualizzato il browser Risorse CRX.

   ![Progettare un processo: usare una risorsa CRX](assets/formsetinprocessmgmt1.png)

1. Selezionare il set di moduli per filtrare il set di moduli AEM repository (CRX).

   ![Progettare un processo: Seleziona risorsa modulo, finestra di dialogo](assets/formsetinprocessmgmt2.png)

1. Seleziona un set di moduli e fai clic su OK.

## Espressioni di idoneità {#eligibility-expressions}

Le espressioni di idoneità in un set di moduli vengono utilizzate per definire e controllare in modo dinamico i moduli visualizzati dall&#39;utente. Ad esempio, per visualizzare un modulo specifico solo se l’utente appartiene a un particolare gruppo di età. Specificare e modificare un&#39;espressione di idoneità utilizzando Forms Manager.

Un&#39;espressione di idoneità può essere qualsiasi istruzione JavaScript valida che restituisce un valore booleano. L&#39;ultima istruzione nello snippet di codice JavaScript è trattata come un valore booleano che determina l&#39;idoneità del modulo in base all&#39;elaborazione nelle altre (righe precedenti) dello snippet di codice JavaScript. Se il valore dell&#39;espressione è true, il modulo può essere visualizzato all&#39;utente. Tali moduli sono noti come moduli idonei.

>[!NOTE]
>
>L&#39;espressione di idoneità per il primo modulo del set di moduli non è eseguita. Il primo modulo viene sempre visualizzato indipendentemente dalla relativa espressione di idoneità.

Oltre alle funzioni JavaScript standard, il set di moduli espone anche l&#39;API fs.valueOf che fornisce l&#39;accesso al valore di un campo di un modulo in un set di moduli. Utilizzare questa API per accedere al valore di un campo modulo in un set di moduli. La sintassi API è fs.valueOf (formUid, fieldSOM), dove:

* formUid (stringa): Un ID univoco di un modulo nel set di moduli. È possibile specificarlo durante la creazione del set di moduli nell&#39;interfaccia utente di Forms Manager. Per impostazione predefinita, è il nome del modulo.
* fieldSOM (stringa): Un&#39;espressione SOM del campo nel modulo specificato da formUid. L&#39;espressione SOM o l&#39;espressione del modello di oggetto script viene utilizzata per fare riferimento a valori, proprietà e metodi all&#39;interno di un particolare modello di oggetto documento (DOM). È possibile visualizzarlo in Form Designer sotto la scheda Script mentre il campo è selezionato.

>[!NOTE]
>
>Entrambi i parametri formUid e fieldSOM devono essere stringhe letterali.

### Esempi {#examples}

Utilizzo valido dell&#39;API:

`fs.valueOf("form1", "xfa.form.form1.subform1.field1")`

Utilizzo non valido dell&#39;API:

```javascript
var formUid = "form1";
 var fieldSOM = “xfa.form.form1.subform1.field1"; fs.valueOf(formUid, fieldSOM);
```

## Precompila XML per il set di moduli {#prefill-xml-for-form-set}

Set di moduli è un insieme di più moduli HTML5 con schemi comuni o diversi. Il set di moduli supporta la precompilazione dei campi modulo mediante l&#39;uso di un file XML. È possibile associare un file XML a un set di moduli, in modo che quando si apre un modulo nel set di moduli, alcuni dei campi del modulo vengano precompilati.

Il file XML di precompilazione viene specificato utilizzando il parametro dataRef dell&#39;URL del set di moduli. Il parametro dataRef specifica il percorso assoluto del file XML di dati unito al set di moduli.

Ad esempio, nel set di moduli sono presenti tre moduli (modulo1, modulo2 e modulo3) con la struttura seguente:

form1

field
form1, campo

form2

field
form2field

form3

field
form3field

Ogni modulo ha un campo denominato comune, denominato &quot;field&quot; e un campo denominato in modo univoco denominato &quot;form&lt;i>field&quot;.

È possibile precompilare questo set di moduli utilizzando un XML con la struttura seguente:

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<formSetRootTag>
 <field>common field value</field>
 <form1field>value1</form1field>
 <form2field>value2</form2field>
 <form3field>value3</form3field>
</formSetRootTag>
```

>[!NOTE]
>
>Il tag XML principale può avere un nome qualsiasi, ma i tag degli elementi corrispondenti ai campi devono avere lo stesso nome del campo. La gerarchia dell&#39;XML deve simulare la gerarchia del modulo, il che significa che l&#39;XML deve avere i tag corrispondenti per racchiudere i sottomoduli.

Lo snippet XML di cui sopra mostra che l&#39;XML di precompilazione per il set di moduli è un&#39;unione degli snippet XML di precompilazione dei singoli moduli. Se alcuni campi nei diversi moduli presentano una gerarchia di dati o uno schema simile, i campi vengono precompilati con gli stessi valori. In questo esempio, tutti e tre i moduli sono precompilati con lo stesso valore per il campo comune &quot;field&quot;. Si tratta di un modo semplice per trasmettere i dati da un modulo all&#39;altro. Ciò può essere ottenuto anche mediante il binding dei campi con lo stesso schema o riferimento dati. Se si desidera separare i dati del set di moduli in base allo schema del modulo. Questo può essere ottenuto specificando l&#39;attributo &quot;data root&quot; del modulo, durante la creazione del set di moduli (il valore predefinito è &quot;/&quot;, che viene mappato sul tag principale del set di moduli).

Nell&#39;esempio precedente, se si specificano le origini dati: &quot;/form1&quot;, &quot;/form2&quot; e &quot;/form3&quot; rispettivamente per i tre moduli, è necessario utilizzare un XML di precompilazione della struttura seguente:

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<formSetRootTag>
 <form1>
  <field>field value1</field>
  <form1field>value1</form1field>
 </form1>
 <form2>
  <field>field value2</field>
  <form2field>value2</form2field>
 </form2>
 <form3>
  <field>field value3</field>
  <form3field>value3</form3field>
 </form3>
</formSetRootTag>
```

In un set di moduli, l&#39;XML ha definito uno schema XML con la sintassi seguente:

```xml
<formset>
 <fs_data>
  <xdp:xdp xmlns:xdp="https://ns.adobe.com/xdp/">
  <xfa:datasets xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/">
   <xfa:data>
   <rootElement>
    ... data ....
   </rootElement>
   </xfa:data>
  </xfa:datasets>
  </xdp:xdp>
 </fs_data>
 <fs_draft>
  ... private data...
 </fs_draft>
</formset>
```

>[!NOTE]
>
>Se nel file XML di precompilazione sono presenti due moduli con origini dati sovrapposte o la gerarchia di elementi di un modulo si sovrappone alla gerarchia di dati principale di un altro modulo, i valori degli elementi sovrapposti vengono uniti. L&#39;XML di invio ha una struttura simile all&#39;XML di precompilazione, ma l&#39;XML di invio ha più tag wrapper e alcuni tag di dati contestuali del set di moduli sono aggiunti alla fine.

### Descrizione degli elementi XML precompilati {#prefill-xml-elements-description}

Regole di sintassi per la creazione di un file XML di precompilazione:

* elementi padre: elementi che possono essere il relativo elemento principale, dove null indica che l&#39;elemento può trovarsi alla radice del codice XML.
* cardinalità: rappresenta il numero di volte in cui l&#39;elemento può essere utilizzato all&#39;interno del relativo elemento padre.
* submitXML: indica se l&#39;elemento è sempre presente(P) o facoltativo(O) nell&#39;invio di XML.
* prefillXML: indica se l&#39;elemento è obbligatorio(R) o facoltativo(O) nel file XML di precompilazione.
* bambini: indica quali elementi possono essere i relativi elementi secondari.

### FORMSET {#formset}

`parent elements:`

`null`

`cardinality: [0,1]`

`submitXML: P`

`prefillXML: O`

`children: fs_data`

L&#39;elemento principale del set di moduli XML. È consigliabile non utilizzare questa parola come nome del sottomodulo root di alcun modulo del set di moduli.

### FS_DATA {#fs-data}

`parent elements:`

`formset`

cardinalità: [1]

submitXML: P

prefillXML: O

`children: xdp:xdp/rootElement`

La sottostruttura ad albero indica i dati dei moduli nel set di moduli. L&#39;elemento è facoltativo nel codice XML di precompilazione solo se l&#39;elemento set di moduli non è presente

### XDP:XDP {#xdp-xdp}

`parent elements: fs_data/null`

`cardinality: [0,1]`

`submitXML: O`

`prefillXML: O`

`children: xfa:datasets`

Questo tag indica l’inizio di HTML5 Form XML. Questo viene aggiunto nel file XML di invio se è presente nel file XML di precompilazione o se non è presente alcun XML di precompilazione. Questo tag può essere rimosso dall’XML di precompilazione.

### XFA:DATASETS {#xfa-datasets}

`parent elements: xdp:xdp`

`cardinality: [1]`

`submitXML: O`

`prefillXML: O`

`children: xfa:data`

### XFA:DATA {#xfa-data}

`parent elements: xfa:datasets`

`cardinality: [1]`

`submitXML: O`

`prefillXML: O`

`children: rootElement`

### ROOTELEMENT {#rootelement}

`parent elements: xfa:datasets/fs_data/null`

`cardinality: [0,1]`

`submitXML: P`

`prefillXML: O`

`children: controlled by the Forms in Form set`

Il nome rootElement è solo un segnaposto. Il nome effettivo viene selezionato dai moduli utilizzati nel set di moduli. La struttura ad albero secondaria che inizia con rootElement contiene i dati dei campi e dei sottomoduli all&#39;interno dell&#39;Forms nel set di moduli. Esistono più fattori che determinano la struttura dell&#39;elemento rootElement e dei relativi elementi secondari.

In XML di precompilazione, questo tag è facoltativo, ma se manca, l&#39;intero XML viene ignorato.

NOME DEL TAG ELEMENTO PRINCIPALE

Nel caso in cui vi sia un elemento principale nel file XML di precompilazione, il nome di tale elemento viene assunto anche nel file XML di invio. Se non è presente un codice xml di precompilazione, il nome dell&#39;elemento rootElement è il nome del sottomodulo principale del primo modulo del set di moduli con una proprietà dataRoot impostata su &quot;/&quot;. In assenza di tale modulo, il nome rootElement è **fs_dummy_root**, che è una parola chiave riservata.

## Set di moduli in  app AEM Forms {#formset-in-workspace-app}

&#39;app AEM Forms consente ai lavoratori del campo di sincronizzare i loro dispositivi mobili con un server AEM Forms  e di lavorare sulle loro attività. L&#39;applicazione funziona anche quando il dispositivo è offline, salvando i dati localmente sul dispositivo. Utilizzando le funzioni di annotazione, come le fotografie, i dipendenti sul campo possono fornire informazioni precise da integrare nei processi aziendali.

<!-- Update link as it is a 404 - For more information on AEM Forms app, see [AEM Forms app overview](/help/forms/using/mobile-workspace-overview.md).-->

## Limitazioni note - pattern non completamente supportati nel set di moduli {#known-limitations-patterns-not-fully-supported-in-form-set}

I seguenti pattern di dati non sono completamente supportati nel set di moduli:

<table>
 <tbody>
  <tr>
   <td><strong>Pattern non completamente supportato nel set di moduli</strong></td>
   <td><strong>Esempio</strong></td>
  </tr>
  <tr>
   <td>Dimensioni input e dimensioni pattern non corrispondenti</td>
   <td><p>Quando pattern= num{z,zzz}</p> <p>E input=</p> <p>12,345 o</p> <p>1,23</p> </td>
  </tr>
  <tr>
   <td>Pattern di clausola immagine con parentesi quadre "(" ")"</td>
   <td>num{(zz,zzz)}</td>
  </tr>
  <tr>
   <td>Pattern di dati multipli</td>
   <td>num{zz,zzz} | num{z,zzz,zzz}</td>
  </tr>
  <tr>
   <td>Pattern di abbreviazione </td>
   <td><p>num.integer{},</p> <p>num.decimal{},</p> <p>num.percentuale{}, oppure</p> <p>num.currency{}</p> </td>
  </tr>
 </tbody>
</table>

