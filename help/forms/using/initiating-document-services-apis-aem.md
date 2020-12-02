---
title: Avviare le API Document Services dal flusso di lavoro AEM
seo-title: Avviare le API Document Services dal flusso di lavoro AEM
description: Scoprite come richiamare AEM Document Services su DDX o in input forniti. Vedere anche come convertire PDF in PDF/A
seo-description: Scoprite come richiamare AEM Document Services su DDX o in input forniti. Vedere anche come convertire PDF in PDF/A
uuid: aacec2df-1ad6-4ff2-a99d-ef206efcdc09
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: 8b85bdc7-3864-49c9-81b0-cf15b8e986d9
translation-type: tm+mt
source-git-commit: 7caf09f7020c066072eac04a349a19b144dfeb7b
workflow-type: tm+mt
source-wordcount: '1199'
ht-degree: 0%

---


# Avviare le API Document Services dal flusso di lavoro AEM {#initiate-document-services-apis-from-aem-workflow}

## Assemblatore {#assembler}

 AEM Forms fornisce flussi di lavoro personalizzati per richiamare le seguenti API del servizio Assembler:

* **invoke**: Richiama le operazioni specificate nel DDX di input sugli input forniti.
* **toPDFA**: Converte il documento PDF di input in documento PDF/A.

### Richiama flusso di lavoro DDX {#invoke-ddx-workflow}

Il flusso di lavoro **Richiama DDX** richiama l&#39;API del servizio Assembler `Invoke`, che consente di assemblare o smontare documenti, aggiungere filigrane a un PDF e così via.

1. Trascinare il passaggio del flusso di lavoro **[!UICONTROL Richiama DDX]** nella scheda Forms Workflow nella barra laterale.
1. Fate doppio clic sul passaggio del flusso di lavoro aggiunto per modificare il componente.
1. Nella finestra di dialogo Modifica componente, configurate i documenti di input, le opzioni dell&#39;ambiente e i documenti di output, quindi fate clic su **[!UICONTROL OK]**.

#### Documenti di input {#input-documents}

Il flusso di lavoro Richiama DDX richiede i seguenti documenti di input:

* **DDX**: È un input obbligatorio per il passaggio del flusso di lavoro Richiama DDX e può essere specificato selezionando una delle seguenti opzioni dal menu a discesa di input DDX.

   * *Relativo Al Payload*: Il file di input DDX è relativo alla cartella payload per l&#39;elemento del flusso di lavoro.
   * *Usa payload*: Il payload per l&#39;elemento del flusso di lavoro viene utilizzato come documento DDX di input.
   * *Percorso* assoluto: Percorso assoluto del documento DDX nell&#39;archivio CRX.

* **Crea mappa da PayLoad**: Quando è selezionata questa opzione, tutti i documenti contenuti nella cartella payload vengono aggiunti alla Mappa del documento di input per l&#39; `invoke` API in Assembler. Il nome del nodo per ciascun documento viene utilizzato come chiave nella mappa.

* **Mappa** del documento di input: Specifica la mappa del documento di input. È possibile aggiungere un numero qualsiasi di voci, in cui ogni voce specifica la chiave del documento nella mappa e l&#39;origine del documento.

#### Opzioni ambiente {#environment-options}

La scheda Opzioni ambiente consente di impostare diverse opzioni di elaborazione per l&#39;API invoke.

* *Livello* registro processo: Specifica il livello di registro per i registri di elaborazione.
* *Solo* convalida: Controlla la validità del DDX di input.

* *Errore In Caso Di Errore*: Specifica se la chiamata al servizio Assembler deve fallire in caso di errore. Il valore predefinito è False.

#### Documenti di output {#output-documents}

A seconda del DDX di input, l&#39;API invoke può produrre più documenti di output. La scheda Documenti di output consente di selezionare la posizione in cui verrà salvato il documento di output.

1. *Salva output in payload*: Salva i documenti di output nella cartella payload o sovrascrive il payload, se il payload è un file.
1. *Mappa* del documento di output: Consente di specificare in modo esplicito dove salvare ciascun documento di output aggiungendo una voce per documento di output. Ogni voce specifica il documento e dove salvarlo. Un documento di output può sovrascrivere il payload o salvarlo nella cartella payload. È utile in presenza di più documenti di output.

1. *Registro* processo: Specifica dove salvare il documento del registro dei processi, utile per la risoluzione dei problemi.

### Flusso di lavoro Converti in PDF/A {#convert-to-pdf-a-workflow}

Il passaggio del flusso di lavoro Converti in PDF/A richiama l&#39;API del servizio Assembler `toPDFA`. Viene utilizzato per convertire documenti PDF in documenti conformi allo standard PDF/A.

1. Trascinare il passaggio del flusso di lavoro **[!UICONTROL ConvertToPDFA]** nella scheda Forms Workflow nella barra laterale.

1. Fate doppio clic sul passaggio del flusso di lavoro aggiunto per modificare il componente.
1. Nella finestra di dialogo Modifica componente, configurate i documenti di input, le opzioni di conversione e di output e fate clic su **[!UICONTROL OK]**.

#### Documenti di input {#input-documents-1}

Specificare l&#39;origine del documento da convertire in documento conforme con lo standard PDF/A in uno dei modi seguenti.

* *Relativo Al Payload*: Il documento di input è relativo alla cartella payload dell’elemento del flusso di lavoro.
* *Usa payload*: Il payload per l&#39;elemento del flusso di lavoro viene utilizzato come documento di input.
* *Percorso* assoluto: Percorso assoluto del documento di input nel repository CRX.

#### Opzioni di conversione {#conversion-options}

Le opzioni di conversione consentono di specificare opzioni che modificano il processo di conversione PDF/A.

* *Conformità* : Specifica lo standard PDF/A a cui il PDF/A di output deve conformarsi.
* *Livello*  risultato: Specifica il livello di registro da utilizzare per i registri di conversione PDF/A.
* *Firme* : Specifica la modalità di elaborazione delle firme nel documento di input durante la conversione.
* *Spazio*  colore: Specifica lo spazio colore predefinito da utilizzare per il documento PDF/A di output.
* ** VerifyConversion: Specifica se il documento PDF/A convertito deve essere verificato per la conformità PDF/A dopo la conversione.
* *Livello*  registro processo: Specifica il livello di registro da utilizzare per l&#39;elaborazione dei registri.

* *Schema*  estensione metadati: Specifica il percorso dello schema di estensione dei metadati da utilizzare per XMP proprietà nei metadati del documento PDF.

#### Documenti di output {#output-documents-1}

La scheda Documenti di output consente di specificare la destinazione dei documenti di output

* *Documento* PDFA: Specifica la posizione in cui viene salvato il documento PDF/A convertito. Può sovrascrivere il documento di payload o salvarlo nella cartella payload.
* *Registro* conversione: Specifica la posizione in cui vengono salvati i registri di conversione. Può sovrascrivere il documento di payload o può essere salvato nella cartella payload.

## Forms {#forms}

Il flusso di lavoro Rendering modulo PDF è un wrapper per l&#39;API del servizio Forms `renderPDFForm` per creare un modulo PDF utilizzando un modello XDP e un file XML di dati.

### Rendering del flusso di lavoro del modulo PDF {#render-pdf-form-workflow}

1. Trascinare il passaggio del flusso di lavoro Rendering modulo PDF sotto la scheda Forms Workflow nella barra laterale.
1. Fate doppio clic sul passaggio del flusso di lavoro aggiunto per modificare il componente.
1. Nella finestra di dialogo Modifica componente, configurate i documenti di input, i documenti di output e altri parametri, quindi fate clic su **[!UICONTROL OK]**.

#### Documenti di input {#input-documents-2}

* *File* modello: Specifica la posizione del modello XDP. È un campo obbligatorio.

* *Documento* dati: Specifica la posizione del file xml di dati da unire al modello.

#### Documenti di output {#output-documents-2}

* *Documento* di output: - Specifica il nome del modulo PDF generato.

#### Parametri aggiuntivi {#additional-parameters}

* *Radice* contenuto: Specifica il percorso della cartella nell&#39;archivio in cui sono memorizzati i frammenti o le immagini utilizzati nel modello XDP di input.
* *Invia Url*: Specifica l&#39;URL di invio predefinito per il modulo PDF generato.
* *Impostazioni internazionali*: Specifica le impostazioni internazionali predefinite per il modulo PDF generato.
* *versione* Acrobat: Specifica la versione di destinazione  Acrobat per il modulo PDF generato.
* *PDF* con tag: Specifica se rendere accessibile il PDF generato.
* *Documento* XCI: Specifica il percorso del file XCI.

## Output {#output}

Il flusso di lavoro Genera PDF non interattivo è un wrapper per l&#39;API del servizio di output `generatePDFOutput`. Viene utilizzato per generare documenti PDF non interattivi dal modello XDP e dal file XML dei dati.

### Genera flusso di lavoro Output PDF non interattivo   {#generate-non-interactive-pdf-output-workflow-nbsp}

1. Trascinare il flusso di lavoro Genera output PDF non interattivo nella scheda Forms Workflow della barra laterale.
1. Fate doppio clic sul passaggio del flusso di lavoro aggiunto per modificare il componente.
1. Nella finestra di dialogo Modifica componente, configurate i documenti di input, i documenti di output e altri parametri, quindi fate clic su **[!UICONTROL OK]**.

#### Documenti di input {#input-documents-3}

* *File* modello: Specifica la posizione del modello XDP. È un campo obbligatorio.

* *Documento* dati: Specifica la posizione dell&#39;XML di dati che deve essere unito al modello.

#### Documento di output {#output-document}

*Documento* di output: Specifica il nome del modulo PDF generato.

#### Parametri aggiuntivi {#additional-parameters-1}

* *Radice* contenuto: Specifica il percorso della cartella nell&#39;archivio in cui sono memorizzati i frammenti o le immagini utilizzati nel modello XDP di input.
* *Impostazioni internazionali*: Specifica le impostazioni internazionali predefinite per il modulo PDF generato.
* *versione* Acrobat: Specifica la versione di destinazione  Acrobat per il modulo PDF generato.
* PDF lineare: Specifica se ottimizzare il PDF generato per la visualizzazione Web.
* *PDF* con tag: Specifica se rendere accessibile il PDF generato.
* *Documento* XCI: Specifica il percorso del file XCI.

