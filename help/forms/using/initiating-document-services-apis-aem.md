---
title: Avviare le API di Document Services dal flusso di lavoro AEM
seo-title: Initiate Document Services APIs from AEM Workflow
description: Scopri come richiamare AEM Document Services su DDX o gli input forniti. Vedere anche come convertire PDF in PDF/A
seo-description: Learn how to invoke AEM Document services on DDX or supplied inputs. Also see hwo to convert PDF to PDF/A
uuid: aacec2df-1ad6-4ff2-a99d-ef206efcdc09
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: 8b85bdc7-3864-49c9-81b0-cf15b8e986d9
exl-id: 123087a2-9d09-4579-9185-2ccd7d25bf8d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1171'
ht-degree: 0%

---

# Avviare le API di Document Services dal flusso di lavoro AEM  {#initiate-document-services-apis-from-aem-workflow}

## Assemblatore {#assembler}

AEM Forms fornisce flussi di lavoro personalizzati per richiamare le seguenti API del servizio Assembler:

* **invocare**: Richiama le operazioni specificate in DDX in ingresso sugli input forniti.
* **toPDFA**: Converte il documento di input PDF in documento PDF/A.

### Richiama del flusso di lavoro DDX {#invoke-ddx-workflow}

La **Richiama DDX** richiama il `Invoke` API del servizio Assembler, che consente di assemblare o smontare documenti, aggiungere filigrane a un PDF e così via.

1. Trascina **[!UICONTROL Richiama DDX]** passaggio del flusso di lavoro nella scheda Forms Workflow della barra laterale.
1. Fai doppio clic sul passaggio del flusso di lavoro aggiunto per modificare il componente.
1. Nella finestra di dialogo Modifica componente configurare documenti di input, opzioni dell’ambiente e documenti di output e fare clic su **[!UICONTROL OK]**.

#### Documenti di input {#input-documents}

Il flusso di lavoro Richiama DDX richiede i seguenti documenti di input:

* **DDX**: È un input obbligatorio per il passaggio del flusso di lavoro Invoke DDX e può essere specificato selezionando una delle seguenti opzioni dal menu a discesa di input DDX.

   * *Relativo Al Payload*: Il file di input DDX è relativo alla cartella payload per l’elemento del flusso di lavoro.
   * *Usa payload*: Il payload per l’elemento del flusso di lavoro viene utilizzato come documento DDX di input.
   * *Percorso assoluto*: Percorso assoluto del documento DDX nell&#39;archivio CRX.

* **Crea mappa da PayLoad**: Quando è selezionata questa opzione, tutti i documenti contenuti nella cartella payload vengono aggiunti alla mappa del documento di input per la `invoke` API in Assembler. Il nome del nodo di ciascun documento viene utilizzato come chiave nella mappa.

* **Mappa del documento di input**: Specifica la mappa del documento di input. È possibile aggiungere un numero qualsiasi di voci, in cui ogni voce specifica la chiave del documento nella mappa e l&#39;origine del documento.

#### Opzioni di ambiente {#environment-options}

La scheda Opzioni ambiente consente di impostare diverse opzioni di elaborazione per l’API di chiamata.

* *Livello registro processi*: Specifica il livello di registro per i registri di elaborazione.
* *Convalida solo*: Controlla la validità dell&#39;input DDX.

* *Errore*: Specifica se la chiamata al servizio Assembler deve non riuscire in caso di errore. Il valore predefinito è False.

#### Documenti di output {#output-documents}

A seconda dell’DDX di input, l’API di chiamata può produrre più documenti di output. La scheda Documenti di output consente di selezionare la posizione in cui salvare il documento di output.

1. *Salva output nel payload*: Salva i documenti di output sotto la cartella payload o sovrascrive il payload, se il payload è un file.
1. *Mappa del documento di output*: Consente di specificare in modo esplicito dove salvare ogni documento di output aggiungendo una voce per documento di output. Ogni voce specifica il documento e la posizione in cui salvarlo. Un documento di output può sovrascrivere il payload o salvarlo nella cartella payload. È utile quando sono presenti più documenti di output.

1. *Registro processi*: Specifica la posizione in cui salvare il documento del registro di lavoro, utile per la risoluzione degli errori.

### Flusso di lavoro Converti in PDF/A {#convert-to-pdf-a-workflow}

Il passaggio del flusso di lavoro Converti in PDF/A richiama l’ `toPDFA` API del servizio Assembler. Viene utilizzato per convertire i documenti PDF in documenti conformi a PDF/A.

1. Trascina **[!UICONTROL ConvertToPDFA]** passaggio del flusso di lavoro nella scheda Forms Workflow della barra laterale.

1. Fai doppio clic sul passaggio del flusso di lavoro aggiunto per modificare il componente.
1. Nella finestra di dialogo Modifica componente, configura documenti di input, opzioni di conversione e documenti di output e fai clic su **[!UICONTROL OK]**.

#### Documenti di input {#input-documents-1}

Specificare l&#39;origine del documento da convertire in un documento conforme a PDF/A in uno dei seguenti modi.

* *Relativo Al Payload*: Il documento di input è relativo alla cartella payload per l’elemento del flusso di lavoro.
* *Usa payload*: Il payload per l’elemento del flusso di lavoro viene utilizzato come documento di input.
* *Percorso assoluto*: Percorso assoluto del documento di input nell’archivio CRX.

#### Opzioni di conversione {#conversion-options}

Le opzioni di conversione consentono di specificare le opzioni che modificano il processo di conversione di PDF/A.

* *Conformità* : Specifica lo standard PDF/A a cui deve conformarsi l&#39;output PDF/A.
* *Livello dei risultati* : Specifica il livello di registro da utilizzare per i registri di conversione di PDF/A.
* *Firme* : Specifica la modalità di elaborazione delle firme nel documento di input durante la conversione.
* *Spazio colore* : Specifica lo spazio colore predefinito da utilizzare per il documento PDF/A di output.
* *Verifica* Conversione: Specifica se il documento PDF/A convertito deve essere verificato per la conformità di PDF/A dopo la conversione.
* *Livello registro processi* : Specifica il livello di registro da utilizzare per l’elaborazione dei registri.

* *Schema di estensione metadati* : Specifica il percorso dello schema di estensione dei metadati da utilizzare per le proprietà XMP nei metadati del documento di PDF.

#### Documenti di output {#output-documents-1}

La scheda Documenti di output consente di specificare la destinazione dei documenti di output

* *Documento PDFA*: Specifica il percorso in cui viene salvato il documento PDF/A convertito. Può sovrascrivere il documento di payload o salvarlo nella cartella di payload.
* *Registro di conversione*: Specifica il percorso in cui vengono salvati i registri di conversione. Può sovrascrivere il documento di payload o può essere salvato nella cartella di payload.

## Forms {#forms}

Il flusso di lavoro Render PDF Form è un wrapper per `renderPDFForm` API del servizio Forms per creare un modulo PDF utilizzando un modello XDP e un data xml.

### Flusso di lavoro del modulo PDF di rendering {#render-pdf-form-workflow}

1. Trascina il passaggio del flusso di lavoro Rendering modulo PDF nella scheda Forms Workflow nella barra laterale.
1. Fai doppio clic sul passaggio del flusso di lavoro aggiunto per modificare il componente.
1. Nella finestra di dialogo Modifica componente, configura documenti di input, documenti di output e parametri aggiuntivi e fai clic su **[!UICONTROL OK]**.

#### Documenti di input {#input-documents-2}

* *File modello*: Specifica la posizione del modello XDP. È un campo obbligatorio.

* *Documento dati*: Specifica la posizione del file xml di dati da unire al modello.

#### Documenti di output {#output-documents-2}

* *Documento di output*: - Specifica il nome del modulo PDF generato.

#### Parametri aggiuntivi {#additional-parameters}

* *Directory principale dei contenuti*: Specifica il percorso della cartella nell&#39;archivio in cui sono archiviati i frammenti o le immagini utilizzati nel modello XDP di input.
* *Invia Url*: Specifica l’URL di invio predefinito per il modulo PDF generato.
* *Impostazioni internazionali*: Specifica le impostazioni internazionali predefinite per il modulo PDF generato.
* *Versione Acrobat*: Specifica la versione Acrobat di destinazione per il modulo PDF generato.
* *PDF con tag*: Specifica se rendere accessibile il PDF generato.
* *Documento XCI*: Specifica il percorso del file XCI.

## Output {#output}

Il flusso di lavoro Generate Non Interactive PDF è un wrapper per `generatePDFOutput` API del servizio di output. Viene utilizzato per generare documenti PDF non interattivi dal modello XDP e dai dati xml.

### Genera flusso di lavoro Output PDF non interattivo   {#generate-non-interactive-pdf-output-workflow-nbsp}

1. Trascina il flusso di lavoro Genera output PDF non interattivo nella scheda Forms Workflow nella barra laterale.
1. Fai doppio clic sul passaggio del flusso di lavoro aggiunto per modificare il componente.
1. Nella finestra di dialogo Modifica componente, configura documenti di input, documenti di output e parametri aggiuntivi e fai clic su **[!UICONTROL OK]**.

#### Documenti di input {#input-documents-3}

* *File modello*: Specifica la posizione del modello XDP. È un campo obbligatorio.

* *Documento dati*: Specifica la posizione del file xml di dati da unire al modello.

#### Documento di output {#output-document}

*Documento di output*: Specifica il nome del modulo PDF generato.

#### Parametri aggiuntivi {#additional-parameters-1}

* *Directory principale dei contenuti*: Specifica il percorso della cartella nell&#39;archivio in cui sono archiviati i frammenti o le immagini utilizzati nel modello XDP di input.
* *Impostazioni internazionali*: Specifica le impostazioni internazionali predefinite per il modulo PDF generato.
* *Versione Acrobat*: Specifica la versione Acrobat di destinazione per il modulo PDF generato.
* PDF lineare: Specifica se ottimizzare il PDF generato per la visualizzazione Web.
* *PDF con tag*: Specifica se rendere accessibile il PDF generato.
* *Documento XCI*: Specifica il percorso del file XCI.
