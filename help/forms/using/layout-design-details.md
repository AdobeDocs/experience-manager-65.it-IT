---
title: Progettazione layout
seo-title: Progettazione layout
description: Dettagli progettazione layout spiega come creare layout da utilizzare per le lettere o le comunicazioni interattive.
seo-description: Dettagli progettazione layout spiega come creare layout da utilizzare per le lettere o le comunicazioni interattive.
uuid: 469a8a71-88f7-4102-bb02-38ed05390f6c
content-type: reference
topic-tags: correspondence-management, interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 683809ac-089b-49bf-a72c-67d32439081f
docset: aem65
feature: Correspondence Management
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2192'
ht-degree: 0%

---


# Progettazione layout{#layout-design}

I modelli di modulo XFA o XDP sono i modelli per:

* [Lettere](/help/forms/using/create-letter.md)
* [Canale ](/help/forms/using/web-channel-print-channel.md#printchannel) di stampa delle comunicazioni  [interattive](/help/forms/using/interactive-communications-overview.md)

* Frammenti di layout

Un XDP è progettato in Adobe Forms Designer. Questo articolo fornisce dettagli su come progettare XDP per creare corrispondenze/comunicazioni interattive efficaci, ad esempio dove utilizzare i campi del modulo o le aree di destinazione e quando utilizzare i frammenti di layout.

## Creazione di un layout per le lettere o per il canale di stampa delle comunicazioni interattive {#creating-a-layout-for-letters-or-for-interactive-communications-print-channel}

Un layout definisce il layout grafico di un canale lettera/stampa di una comunicazione interattiva. Il layout può contenere campi modulo tipici, ad esempio &quot;Indirizzo&quot; e &quot;Numero di riferimento&quot;. Contiene inoltre sottomoduli vuoti che indicano le aree di destinazione. Crea il layout in form designer e, una volta completato, lo specialista dell&#39;applicazione lo carica AEM server. Da lì è possibile selezionare il layout quando si crea un modello di corrispondenza o un canale di stampa di una comunicazione interattiva.

![Designer: creare un layout](assets/claimsubrogationlayout.png)

Segui questi passaggi per creare layout per lettere/canale di stampa delle comunicazioni interattive:

1. Analizzare il layout e determinare il contenuto che viene ripetuto su tutte le pagine; in genere l’intestazione e il piè di pagina rientrano in questa categoria. Questo contenuto viene inserito nelle pagine master di layout. Il contenuto rimanente viene indirizzato alle pagine corpo del layout. In una giacca di criterio, il logo e l’indirizzo dell’azienda possono essere aggiunti all’intestazione e al piè di pagina della pagina master. Ad esempio, Avviso di annullamento utilizza lo stesso layout.
1. Durante la progettazione delle pagine corpo, suddividi il contenuto della pagina in sezioni. Ciascuna sezione è progettata come un sottomodulo incorporato nel layout stesso o come layout di frammento. Se la sezione contiene una tabella, modellare la sezione come frammento di layout.
1. Un Layout può essere progettato come segue:

   1. Creare ogni sezione come sottomodulo separato contenente tutti gli elementi della sezione.
   1. Creare un sottomodulo di sezione secondario dello stesso sottomodulo principale. Il layout del sottomodulo principale è impostato in modo da consentire lo scorrimento verso il basso delle sezioni nel caso di dati di grandi dimensioni che vengono uniti nelle sezioni precedenti.
   1. Sezione residenza primaria può essere riutilizzato anche in altri layout. Crea come layout di frammento.
   1. Sezione Ulteriori dettagli di interesse contengono solo due elementi posizionati uno sotto l&#39;altro, possono contenere dati di grandi dimensioni ed è progettato come flusso.
   1. Altre sezioni contengono elementi in posizioni specifiche in modo che siano progettati come layout posizionato.
   1. Suddividi una sezione in sottomoduli se la sezione contiene elementi in posizioni specifiche e questi elementi contengono grandi quantità di dati. Quindi, disporre i sottomoduli per ottenere il comportamento desiderato.
   1. Per la sezione Residenza principale, aggiungere un&#39;area di destinazione segnaposto. Questo segnaposto è destinato a frammentare la residenza primaria al momento della progettazione della lettera/comunicazione interattiva.
   1. Carica il layout (e l’eventuale frammento che utilizza il layout) nel server AEM Forms.

### Utilizzare un sottomodulo in un modello XDP {#usesubformxdp}

Una volta analizzato il layout necessario per creare la comunicazione interattiva, è possibile creare sottomoduli nel modello XDP utilizzando Forms Designer. I componenti sottomodulo vuoti utilizzati nel modello XDP consentono di visualizzare le aree di destinazione nel canale Stampa della comunicazione interattiva.

>[!NOTE]
>
>Aggiungere contenuto al canale Stampa della comunicazione interattiva anziché aggiungere contenuto al componente sottomodulo nel modello XDP. Aggiungere contenuto alle aree di destinazione nel canale Stampa utilizzando [frammenti di documento, grafici, immagini](create-interactive-communication.md#step2) e frammenti di layout.

Per utilizzare un sottomodulo in un modello XDP, effettua le seguenti operazioni:

1. Apri Forms Designer, seleziona **File** > **Nuovo** > **Utilizza un modulo vuoto**, tocca **Avanti**, quindi tocca **Fine** per aprire il modulo per la creazione del modello.

   Assicurati che le opzioni **Libreria oggetto** e **Oggetto** siano selezionate dal menu **Finestra**.

1. Trascina il componente **Sottomodulo** dalla **Libreria oggetto** al modulo.

   ![Progettazione componenti](assets/subform_component_designer_new.png)

1. Selezionare il sottomodulo per visualizzare le opzioni del sottomodulo nella finestra **Oggetto** del riquadro di destra.
1. Selezionare la scheda **Sottomodulo** e selezionare **Flusso** dall&#39;elenco a discesa **Contenuto**. Trascinare l’endpoint sinistro del sottomodulo per regolare la lunghezza.

   ![Sottomodulo scorrevole](assets/object_subform_flowed_new.png)

1. Nella scheda **Binding** :

   1. Specificare un nome per il sottomodulo nel campo **Nome**.
   1. Selezionare **Nessun binding di dati** dall&#39;elenco a discesa **Binding dei dati**.

1. Allo stesso modo, selezionare il sottomodulo principale dal riquadro a sinistra.

   ![Sottomodulo principale](assets/root_subform_designer_new.png)

1. Selezionare la scheda **Sottomodulo** e selezionare **Flusso** dall&#39;elenco a discesa **Contenuto**. Nella scheda **Binding** :

   1. Specificare un nome per il sottomodulo nel campo **Nome**.
   1. Selezionare **Nessun binding di dati** dall&#39;elenco a discesa **Binding dei dati**.

   Ripetere i passaggi da 2 a 5 per aggiungere altri sottomoduli al modello XDP. Aggiungere [testo, frammenti di documento, immagini e grafici](create-interactive-communication.md#step2) alle aree di destinazione solo durante la creazione della comunicazione interattiva.

1. Selezionare **File** > **Salva con nome** per salvare il file sul file system locale:

   1. Passa alla posizione in cui salvare il file e specifica un nome per il modello XDP.
   1. Seleziona **.xdp** dall&#39;elenco a discesa **Salva come**.

   1. Tocca **Salva**.

### Utilizza il componente Campo immagine in un modello XDP {#use-image-field-component-in-an-xdp-template}

Utilizza il componente Campo immagine o Sottomodulo nel modello XDP e aggiungi un’immagine durante la creazione della comunicazione interattiva.

>[!NOTE]
>
>Aggiungere un’immagine al canale Stampa della comunicazione interattiva invece di aggiungere un’immagine al componente Campo immagine o Sottomodulo nel modello XDP. Per ulteriori informazioni, consulta [Aggiunta di contenuto alla comunicazione interattiva](../../forms/using/create-interactive-communication.md#step2).

Esegui i seguenti passaggi per utilizzare il componente Campo immagine in un modello XDP:

1. Trascina il componente **Campo immagine** dalla **Libreria oggetto** al modulo.
1. Selezionare il sottomodulo per visualizzare le opzioni del sottomodulo nella finestra **Oggetto** del riquadro di destra.
1. Nella scheda **Binding** :

   1. Specifica un nome per il campo immagine nel campo **Nome** .
   1. Selezionare **Nessun binding di dati** dall&#39;elenco a discesa **Binding dei dati**.

### Creare un modello XDP per frammenti di layout {#xdplayoutfragments}

Utilizzare il componente Tabella in Forms Designer per creare frammenti di layout e quindi utilizzarli per creare tabelle durante la creazione del canale Stampa di comunicazione interattiva. L’utilizzo di frammenti di layout per creare tabelle assicura che il contenuto della tabella mantenga la struttura quando il canale web viene generato automaticamente utilizzando il canale di stampa.

>[!NOTE]
>
>Immettere il testo nelle celle della tabella o [creare un binding con gli oggetti del modello dati del modulo](create-interactive-communication.md#step2) solo durante la creazione della comunicazione interattiva.

Esegui i seguenti passaggi per utilizzare il componente Tabella nel modello XDP utilizzando Forms Designer:

1. Trascina il componente **Tabella** dalla **Libreria oggetto** al modulo.
1. Nella finestra di dialogo **Inserisci tabella**:

   1. Specifica il numero di righe e colonne per la tabella.
   1. Selezionare la casella di controllo **Includi riga di intestazione nella tabella** per includere una riga per l&#39;intestazione della tabella.
   1. Toccare **OK**.

1. Tocca **+** nel riquadro a sinistra accanto al nome della tabella, fai clic con il pulsante destro del mouse sui nomi delle celle inclusi nell&#39;intestazione e nelle altre righe e seleziona **Rinomina oggetto** per rinominare le celle della tabella.
1. Fare clic sui campi di testo dell&#39;intestazione della tabella in **Visualizzazione struttura** e rinominarli.
1. Trascina il componente **Campo di testo** dalla **Libreria oggetto** in ogni cella della tabella nella **Visualizzazione struttura**. Eseguire questo passaggio per eseguire il binding delle celle della tabella con gli oggetti del modello di dati del modulo durante la creazione della comunicazione interattiva.

   ![Campi di testo in una tabella](assets/text_fields_table_new.png)

1. Selezionare il nome della riga dal riquadro a sinistra e selezionare **Oggetto** > **Binding** > **Ripeti riga per ogni elemento dati**. Eseguire questo passaggio per garantire che, se viene creato un binding tra le celle della tabella di questa riga e gli oggetti modello dati modulo di tipo raccolta, la riga della tabella venga ripetuta automaticamente per ogni elemento dati disponibile nel database.

   Immettere il testo nelle celle della tabella o [creare un binding con gli oggetti del modello dati del modulo](create-interactive-communication.md#step2) solo durante la creazione della comunicazione interattiva.

1. Selezionare **File** > **Salva con nome** per salvare il file sul file system locale:

   1. Passa alla posizione in cui salvare il file e specifica il nome del modello XDP.
   1. Seleziona **.xdp** dall&#39;elenco a discesa **Salva come**.

   1. Tocca **Salva**.

### Carica il modello XDP sul server AEM Forms {#uploadxdptemplate}

Dopo aver creato un modello XDP utilizzando Forms Designer, è necessario caricarlo sul server AEM Forms in modo che sia disponibile per l’utilizzo durante la creazione della comunicazione interattiva.

1. Seleziona **Forms** > **Forms &amp; Documents**.
1. Tocca **Crea** > **Caricamento file**.
1. Passa alla posizione del modello XDP nel file system locale e tocca **Apri** per importare il modello XDP nel server AEM Forms.

## Utilizzo dello schema {#using-schema}

È possibile utilizzare uno schema in un frammento di layout o di layout , ma non è obbligatorio. Se utilizzi uno schema, verifica quanto segue:

1. Il layout e tutti i layout di frammento utilizzati in una comunicazione lettera/interattiva utilizzano lo stesso schema della comunicazione lettera/interattiva.
1. Tutti i campi necessari per essere compilati con i dati sono associati allo schema.

## Creazione di campi correlati {#creating-relatable-fields}

Per impostazione predefinita, tutti i campi sono considerati correlati a varie altre origini dati. Se il layout contiene campi che non sono correlati a un’origine dati, denominare il campo con un suffisso &quot;_int&quot; (interno); ad esempio, pageCount_int.

Un campo relativo deve:

* essere un XFA &lt;field> o &lt;exclGroup>
* dispongono di un riferimento di binding XFA
* se si tratta di un &lt;exclGroup>, deve avere almeno un campo pulsante di scelta figlio; in caso contrario, non è possibile determinare il relativo tipo di valore

Un campo relativo deve:

* hanno un nome

Un campo relativo non deve:

* Includi un suffisso &quot;_int&quot; nel nome
* hanno un binding impostato come &quot;none&quot;
* essere figlio di un elemento &lt;exclGroup>

Se un campo relativo soddisfa i criteri sopra descritti, può trovarsi in qualsiasi posizione e a qualsiasi profondità di nidificazione nel layout. È possibile utilizzare campi correlati all’interno delle pagine master.

I campi sono più flessibili nella configurazione del layout rispetto ai sottomoduli dell’area di destinazione; tuttavia sono legati a un singolo tipo di valore. È possibile ingrandire un campo oppure impostarlo su una larghezza e un&#39;altezza fisse e così via. Il risultato del modulo o della regola risolti viene inviato nel campo .

## Decidere quando utilizzare sottomoduli e campi di testo {#deciding-when-to-use-subforms-and-text-nbsp-fields}

Utilizzare un sottomodulo se si desidera acquisire più contenuti del modulo in un layout verticale dall’alto verso il basso (più paragrafi o immagini). Il layout deve gestire l’aumento dell’altezza del sottomodulo per adattarne il contenuto. Se non si può essere certi che la lunghezza del contenuto associato al sottomodulo o alla destinazione non superi mai lo spazio riservato al sottomodulo nel layout, creare il sottomodulo come elemento secondario all’interno di un contenitore di sottomoduli scorrevole. Questo processo assicura che gli oggetti layout al di sotto del sottomodulo scorrano verso il basso man mano che il sottomodulo cresce.

Utilizzare un campo se si desidera acquisire i dati del modulo o i dati degli elementi del dizionario dati nello schema del layout (in quanto i campi sono associati ai dati) o per visualizzare il contenuto del modulo in una pagina master. Tenere presente che il contenuto di una pagina master non può fluire con il contenuto della pagina corpo, pertanto è necessario assicurarsi che il campo immagine sia utilizzato come logo intestazione. Questa tabella fornisce ulteriori criteri per decidere quando utilizzare un sottomodulo o un campo in un layout.

<table>
 <tbody>
  <tr>
   <td><p><strong>Utilizzare un sottomodulo quando</strong></p> </td>
   <td><p><strong>Utilizzare un campo di testo quando</strong></p> </td>
  </tr>
  <tr>
   <td><p>Contiene una combinazione di elementi, ad esempio Cognome e Nome</p> </td>
   <td><p>Contiene un singolo elemento, ad esempio un numero di criterio.</p> </td>
  </tr>
  <tr>
   <td><p>Include più paragrafi</p> </td>
   <td><p>Il testo è racchiuso e giustificato</p> </td>
  </tr>
  <tr>
   <td><p>I gruppi di dati ripetuti, facoltativi e condizionali sono associati a sottomoduli, per ridurre il rischio di errori di progettazione che possono verificarsi se vengono utilizzati script per ottenere gli stessi risultati</p> </td>
   <td><p>Elementi come il logo e l’indirizzo dell’organizzazione vengono visualizzati su tutte le pagine di una lettera/comunicazione interattiva. In questo caso, creare campi modulo per tali elementi e inserirli nella pagina master. Se si imposta il binding dei campi su "Nessun binding dei dati", i campi nessun vengono visualizzati come campi correlati nell’Editor di comunicazione interattiva/Lettera. Se si desidera associare un certo tipo di contenuto a questi campi, è necessario che il binding sia impostato su .</p> <p>Se l'indirizzo dell'azienda contiene più di una riga di dati, utilizzare il campo di testo con l'opzione "Consenti righe multiple" per rappresentare l'indirizzo nel layout.</p> <p>Se il tipo di dati di un campo di testo è impostato su testo normale, viene utilizzata la versione di testo normale dell’output del modulo invece della versione RTF (tutta la formattazione viene scartata). Per mantenere la formattazione, impostare il tipo di dati del campo di testo su RTF.</p> </td>
  </tr>
  <tr>
   <td><p>Il testo è scorrevole</p> </td>
   <td><p>I campi di testo e i campi immagine vengono utilizzati nelle pagine master. Le pagine master non possono utilizzare i sottomoduli come aree di destinazione.</p> </td>
  </tr>
  <tr>
   <td><p>Gli oggetti sono raggruppati e organizzati senza eseguire il binding del sottomodulo con un elemento dati</p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p>All’interno del sottomodulo è presente un campo di testo. Il sottomodulo può espandersi e non sovrascrivere gli altri oggetti sottostanti al layout.</p> </td>
   <td><p>È necessario un facile accesso ai suoi dati nel processo di post-produzione.</p> </td>
  </tr>
 </tbody>
</table>

## Impostazione di elementi ripetitivi {#setting-up-repetitive-elements}

Quando elementi quali il logo e l’indirizzo dell’organizzazione vengono visualizzati su tutte le pagine di una lettera/comunicazione interattiva, creare campi modulo per tali elementi e inserirli nella pagina master. Utilizzare il binding Nome (Nome campo) per questi campi.

## Specifica il formato di rendering del server {#specify-the-server-nbsp-render-format}

Utilizzare il formato di rendering del server del layout nel modulo XML dinamico; in caso contrario, non sarà possibile eseguire correttamente il rendering di lettere/comunicazioni interattive basate su questo layout. Per impostazione predefinita, il formato di rendering del server in Forms Designer è impostato su Modulo XML dinamico. Per assicurarti di utilizzare il formato corretto:

* In Designer, fare clic su **File** > **Proprietà modulo** > **Valori predefiniti** e assicurarsi che l’impostazione Rendering/Formato PDF sia impostata su Modulo XML dinamico.

