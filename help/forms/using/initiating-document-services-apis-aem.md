---
title: Avviare le API di Document Services dal flusso di lavoro AEM
description: Scopri come richiamare i servizi di documentazione AEM su DDX o gli input forniti. Vedi anche come convertire PDF in PDF/A
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
exl-id: 123087a2-9d09-4579-9185-2ccd7d25bf8d
solution: Experience Manager, Experience Manager Forms
feature: Interactive Communication
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '1167'
ht-degree: 0%

---

# Avviare le API di Document Services dal flusso di lavoro AEM  {#initiate-document-services-apis-from-aem-workflow}

## Assemblatore {#assembler}

AEM Forms fornisce flussi di lavoro personalizzati per richiamare le seguenti API del servizio Assembler:

* **invoke**: richiama le operazioni specificate in DDX di input sugli input forniti.
* **toPDFA**: converte un documento di input PDF in un documento PDF/A.

### Richiama flusso di lavoro DDX {#invoke-ddx-workflow}

Il flusso di lavoro **Richiama DDX** richiama l&#39;API del servizio Assembler `Invoke`, che è possibile utilizzare per assemblare o disassemblare documenti, aggiungere una filigrana a un PDF e così via.

1. Trascina il passaggio del flusso di lavoro **[!UICONTROL Richiama DDX]** nella scheda Forms Workflow in Sidekick.
1. Fai doppio clic sul passaggio del flusso di lavoro aggiunto per modificare il componente.
1. Nella finestra di dialogo Modifica componente configurare documenti di input, opzioni di ambiente e documenti di output e fare clic su **[!UICONTROL OK]**.

#### Documenti di input {#input-documents}

Il flusso di lavoro Richiama DDX richiede i seguenti documenti di input:

* **DDX**: è un input obbligatorio per il passaggio del flusso di lavoro Richiama DDX e può essere specificato selezionando una delle seguenti opzioni dal menu a discesa dell&#39;input DDX.

   * *Relativo al payload*: il file di input DDX è relativo alla cartella di payload per l&#39;elemento del flusso di lavoro.
   * *Usa payload*: il payload per l&#39;elemento del flusso di lavoro viene utilizzato come documento DDX di input.
   * *Percorso assoluto*: il percorso assoluto del documento DDX nell&#39;archivio CRX.

* **Crea mappa da PayLoad**: se selezionata, tutti i documenti nella cartella del payload vengono aggiunti alla mappa del documento di input per l&#39;API `invoke` nell&#39;Assembler. Il nome del nodo di ciascun documento viene utilizzato come chiave nella mappa.

* **Mappa documento di input**: specifica la mappa del documento di input. È possibile aggiungere un numero qualsiasi di voci, in cui ogni voce specifica la chiave del documento nella mappa e l&#39;origine del documento.

#### Opzioni di ambiente {#environment-options}

La scheda Opzioni ambiente consente di impostare varie opzioni di elaborazione per l’API di richiamo.

* *Livello log processi*: specifica il livello di log per i log di elaborazione.
* *Solo convalida*: verifica la validità del DDX di input.

* *Non riuscito in caso di errore*: specifica se la chiamata al servizio Assembler deve non riuscire in caso di errore. Il valore predefinito è False.

#### Documenti di output {#output-documents}

A seconda del DDX di input, l’API di richiamo può produrre più documenti di output. La scheda Documenti di output consente di selezionare la posizione in cui salvare il documento di output.

1. *Salva output nel payload*: salva i documenti di output nella cartella del payload o sovrascrive il payload, se il payload è un file.
1. *Mappa documento di output*: consente di specificare esplicitamente dove salvare ogni documento di output aggiungendo una voce per documento di output. Ogni voce specifica il documento e la posizione in cui salvarlo. Un documento di output può sovrascrivere il payload o salvarlo nella cartella del payload. È utile quando sono presenti più documenti di output.

1. *Registro processi*: specifica dove salvare il documento del registro processi, utile per la risoluzione dei problemi.

### Converti in flusso di lavoro di PDF/A {#convert-to-pdf-a-workflow}

Il passaggio del flusso di lavoro Converti in PDF/A richiama l&#39;API del servizio Assembler `toPDFA`. Viene utilizzato per convertire i documenti PDF in documenti conformi a PDF/A.

1. Trascina il passaggio del flusso di lavoro **[!UICONTROL ConvertToPDFA]** nella scheda Forms Workflow in Sidekick.

1. Fai doppio clic sul passaggio del flusso di lavoro aggiunto per modificare il componente.
1. Nella finestra di dialogo Modifica componente configurare documenti di input, opzioni di conversione e documenti di output e fare clic su **[!UICONTROL OK]**.

#### Documenti di input {#input-documents-1}

Specificare l&#39;origine del documento da convertire in un documento conforme a PDF/A in uno dei modi seguenti.

* *Relativo al payload*: il documento di input è relativo alla cartella del payload per l&#39;elemento del flusso di lavoro.
* *Usa payload*: il payload per l&#39;elemento del flusso di lavoro viene utilizzato come documento di input.
* *Percorso assoluto*: il percorso assoluto del documento di input nell&#39;archivio CRX.

#### Opzioni di conversione {#conversion-options}

Le opzioni di conversione consentono di specificare le opzioni che modificano il processo di conversione PDF/A.

* *Conformità* : specifica lo standard PDF/A a cui il PDF/A di output deve conformarsi.
* *Livello risultati* : specifica il livello di registro da utilizzare per i registri di conversione PDF/A.
* *Firme*: specifica la modalità di elaborazione delle firme nel documento di input durante la conversione.
* *Spazio colore*: specifica lo spazio colore predefinito da utilizzare per il documento PDF/A di output.
* *Verifica* conversione: specifica se il documento PDF/A convertito deve essere verificato per la conformità PDF/A dopo la conversione.
* *Livello log processi*: specifica il livello di log da utilizzare per l&#39;elaborazione dei log.

* *Schema di estensione dei metadati* : specifica il percorso dello schema di estensione dei metadati da utilizzare per le proprietà XMP nei metadati del documento PDF.

#### Documenti di output {#output-documents-1}

La scheda Documenti di output consente di specificare la destinazione dei documenti di output

* *Documento PDFA*: specifica il percorso in cui viene salvato il documento PDF/A convertito. Può sovrascrivere il documento di payload o salvarlo nella cartella di payload.
* *Registro conversione*: specifica il percorso in cui vengono salvati i registri di conversione. Può sovrascrivere il documento di payload o essere salvato nella cartella di payload.

## Moduli {#forms}

Il flusso di lavoro Modulo di rendering PDF è un wrapper intorno all&#39;API di servizio Forms `renderPDFForm` per la creazione di un modulo di PDF utilizzando un modello XDP e un XML dati.

### Flusso di lavoro di Rendering modulo PDF {#render-pdf-form-workflow}

1. Trascina il passaggio del flusso di lavoro Modulo di Rendering PDF nella scheda Forms Workflow in Sidekick.
1. Fai doppio clic sul passaggio del flusso di lavoro aggiunto per modificare il componente.
1. Nella finestra di dialogo Modifica componente configurare documenti di input, documenti di output e parametri aggiuntivi e fare clic su **[!UICONTROL OK]**.

#### Documenti di input {#input-documents-2}

* *File modello*: specifica il percorso del modello XDP. È un campo obbligatorio.

* *Documento dati*: specifica il percorso dell&#39;XML dati da unire al modello.

#### Documenti di output {#output-documents-2}

* *Documento di output*: - Specifica il nome del modulo PDF generato.

#### Parametri aggiuntivi {#additional-parameters}

* *Directory principale contenuto*: specifica il percorso della cartella nell&#39;archivio in cui sono archiviati i frammenti o le immagini utilizzati nel modello XDP di input.
* *URL di invio*: specifica l&#39;URL di invio predefinito per il modulo PDF generato.
* *Impostazioni locali*: specifica le impostazioni locali predefinite per il modulo PDF generato.
* *Acrobat versione*: specifica la versione di Acrobat di destinazione per il modulo PDF generato.
* *PDF con tag*: specifica se rendere accessibile il PDF generato.
* *Documento XCI*: specifica il percorso del file XCI.

## Output {#output}

Il flusso di lavoro di Generate Non Interactive PDF è un wrapper intorno all&#39;API del servizio di output `generatePDFOutput`. Viene utilizzato per generare documenti PDF non interattivi da un modello XDP e dati xml.

### Genera flusso di lavoro di output PDF non interattivo   {#generate-non-interactive-pdf-output-workflow-nbsp}

1. Trascina il flusso di lavoro Genera output PDF non interattivo nella scheda Forms Workflow in Sidekick.
1. Fai doppio clic sul passaggio del flusso di lavoro aggiunto per modificare il componente.
1. Nella finestra di dialogo Modifica componente configurare documenti di input, documenti di output e parametri aggiuntivi e fare clic su **[!UICONTROL OK]**.

#### Documenti di input {#input-documents-3}

* *File modello*: specifica il percorso del modello XDP. È un campo obbligatorio.

* *Documento dati*: specifica il percorso dell&#39;XML dati da unire al modello.

#### Documento di output {#output-document}

*Documento di output*: specifica il nome del modulo PDF generato.

#### Parametri aggiuntivi {#additional-parameters-1}

* *Directory principale contenuto*: specifica il percorso della cartella nell&#39;archivio in cui sono archiviati i frammenti o le immagini utilizzati nel modello XDP di input.
* *Impostazioni locali*: specifica le impostazioni locali predefinite per il modulo PDF generato.
* *Acrobat versione*: specifica la versione di Acrobat di destinazione per il modulo PDF generato.
* Linearized PDF: specifica se ottimizzare il PDF generato per la visualizzazione Web.
* *PDF con tag*: specifica se rendere accessibile il PDF generato.
* *Documento XCI*: specifica il percorso del file XCI.
