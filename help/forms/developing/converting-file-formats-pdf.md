---
title: Conversione tra formati di file e PDF
seo-title: Conversione tra formati di file e PDF
description: Il servizio Genera PDF consente di convertire i formati di file nativi in PDF. Il servizio Genera PDF consente inoltre di convertire i file PDF in altri formati e di ottimizzare le dimensioni dei documenti PDF.
seo-description: Il servizio Genera PDF consente di convertire i formati di file nativi in PDF. Il servizio Genera PDF consente inoltre di convertire i file PDF in altri formati e di ottimizzare le dimensioni dei documenti PDF.
uuid: f72ad603-c996-4d48-9bfc-bed7bf776af6
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 180cac3f-6378-42bc-9a47-60f9f08a7103
translation-type: tm+mt
source-git-commit: 07889ead2ae402b5fb738ca08c7efe076ef33e44
workflow-type: tm+mt
source-wordcount: '7898'
ht-degree: 0%

---


# Conversione tra formati di file e PDF {#converting-between-file-formatsand-pdf}

**Informazioni su Generate PDF Service**

Il servizio Genera PDF converte i formati di file nativi in PDF. Consente inoltre di convertire i file PDF in altri formati e di ottimizzare le dimensioni dei documenti PDF.

Il servizio Genera PDF utilizza applicazioni native per convertire in PDF i seguenti formati di file. Salvo diversa indicazione, sono supportate solo le versioni in tedesco, francese, inglese e giapponese di queste applicazioni. *Solo Windows* indica il supporto per Windows Server® 2003 e Windows Server 2008.

* Microsoft Office 2003 e 2007 per convertire DOC, DOCX, RTF, TXT, XLS, XLSX, PPT, PPTX, VSD, MPP, MPPX, XPS e PUB (solo Windows)

>[!NOTE]
>
> Acrobat® 9.2 o versione successiva è necessario per convertire il formato Microsoft XPS in PDF.

* Autodesk AutoCAD 2005, 2006, 2007, 2008 e 2009 per convertire DWF, DWG e DXW (solo in lingua inglese)
* Corel WordPerfect 12 e X4 per convertire WPD, QPW, SHW (solo inglese)
* OpenOffice 2.0, 2.4, 3.0.1 e 3.1 per convertire ODT, ODS, ODP, ODG, ODF, ODF, SXW, SXI, SXC, SXD, DOC, DOCX, RTF, TXT, XLS, XLSX, PPT, PPTX, VSD, MPP, MPPX e PUB

>[!NOTE]
>
>Il servizio Genera PDF non supporta le versioni a 64 bit di OpenOffice.

*  Adobe Photoshop® CS2 per convertire PSD (solo Windows)

>[!NOTE]
>
>Photoshop CS3 e CS4 non sono supportati perché non supportano Windows Server 2003 o Windows Server 2008.

*  Adobe FrameMaker® 7.2 e 8 per convertire FM (solo Windows)
*  PageMaker di Adobe® 7.0 per convertire PMD, PM6, P65 e PM (solo Windows)
* Formati nativi supportati da applicazioni di terze parti (richiede lo sviluppo di file di configurazione specifici per l&#39;applicazione) (solo Windows)

Il servizio Genera PDF converte in PDF i seguenti formati di file basati su standard.

* Formati video: SWF, FLV (solo Windows)
* Formati immagine: JPEG, JPG, JP2, J2Kí, JPC, J2C, GIF, BMP, TIFF, TIF, PNG, JPF
* HTML (Windows, Sun™ Solaris™ e Linux®)

Il servizio Genera PDF converte i PDF nei seguenti formati di file (solo Windows):

* Encapsulated PostScript (EPS)
* HTML3.2
* HTML 4.01 con CSS 1.0
* DOC (formato Microsoft Word)
* RTF
* Testo (accessibile e semplice)
* XML
* PDF/A-1a che utilizza solo lo spazio colore DeviceRGB
* PDF/A-1b che utilizza solo lo spazio colore DeviceRGB

Il servizio Genera PDF richiede l&#39;esecuzione delle seguenti attività amministrative:

* Installazione delle applicazioni native necessarie nel computer in cui è installato  AEM Forms
* Installare  Adobe Acrobat Professional o  Acrobat Pro Extended 9.2 sul computer in cui è installato  AEM Forms
* Eseguire operazioni di configurazione post-installazione

Tali attività sono descritte in Installazione e distribuzione di moduli AEM tramite chiavi in mano JBoss.

È possibile eseguire le seguenti attività utilizzando il servizio Genera PDF:

* Conversione da formati di file nativi a PDF.
* Convertire documenti HTML in documenti PDF.
* Convertire i documenti PDF in formati di file.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Genera PDF, vedere [Guida di riferimento dei servizi per  AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Conversione di documenti Word in documenti PDF {#converting-word-documents-to-pdf-documents}

Questa sezione descrive come utilizzare l&#39;API Generate PDF per convertire in modo programmatico un documento di Microsoft Word in un documento PDF.

>[!NOTE]
>
>Per ulteriori informazioni sui formati di file aggiuntivi, vedere [Aggiunta del supporto per formati di file nativi aggiuntivi](converting-file-formats-pdf.md#adding-support-for-additional-native-file-formats).

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Genera PDF, vedere [Guida di riferimento dei servizi per  AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary-of-steps}

Per convertire un documento di Microsoft Word in un documento PDF, eseguire le operazioni seguenti:

1. Includere i file di progetto.
1. Creare un client Generate PDF.
1. Recuperare il file da convertire in un documento PDF.
1. Convertire il file in un documento PDF.
1. Recuperate i risultati.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, accertatevi di includere i file proxy.

**Creazione di un client PDF**

Prima di eseguire un&#39;operazione Genera PDF a livello di programmazione, creare un client di servizi Genera PDF. Se utilizzate l&#39;API Java, create un oggetto `GeneratePdfServiceClient`. Se utilizzate l&#39;API del servizio Web, create un oggetto `GeneratePDFServiceService`.

**Recuperare il file da convertire in un documento PDF**

Recuperare il documento di Microsoft Word per la conversione in documento PDF.

**Conversione del file in un documento PDF**

Dopo aver creato il client del servizio Genera PDF, è possibile richiamare il metodo `createPDF2`. Questo metodo richiede informazioni sul documento da convertire, inclusa l’estensione del file.

**Recuperare i risultati**

Dopo aver convertito il file in un documento PDF, è possibile recuperare i risultati. Ad esempio, dopo aver convertito un file Word in un documento PDF, è possibile recuperare e salvare il documento PDF.

**Consulta anche**

[Conversione di documenti Word in documenti PDF tramite l&#39;API Java](converting-file-formats-pdf.md#convert-word-documents-to-pdf-documents-using-the-java-api)

[Conversione di documenti Word in documenti PDF tramite l&#39;API del servizio Web](converting-file-formats-pdf.md#convert-word-documents-to-pdf-documents-using-the-web-service-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Generazione rapida API servizio PDF](/help/forms/developing/generate-pdf-service-java-api.md#generate-pdf-service-java-api-quick-start-soap)

### Conversione di documenti Word in documenti PDF tramite l&#39;API Java {#convert-word-documents-to-pdf-documents-using-the-java-api}

Convertire un documento di Microsoft Word in un documento PDF utilizzando l&#39;API Generate PDF (Java):

1. Includere i file di progetto.

   Includete file JAR client, ad esempio adobe-generatepdf-client.jar, nel percorso di classe del progetto Java.

1. Creare un client Generate PDF.

   * Creare un oggetto `ServiceClientFactory` che contiene le proprietà di connessione.
   * Creare un oggetto `GeneratePdfServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Recuperare il file da convertire in un documento PDF.

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il file Word da convertire utilizzando il relativo costruttore. Passa un valore di stringa che specifica la posizione del file.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Convertire il file in un documento PDF.

   Per convertire il file in un documento PDF, richiamare il metodo `GeneratePdfServiceClient` dell&#39;oggetto &lt;a1/> e passare i valori seguenti:`createPDF2`

   * Un oggetto `com.adobe.idp.Document` che rappresenta il file da convertire.
   * Un oggetto `java.lang.String` che contiene l&#39;estensione del file.
   * Un oggetto `java.lang.String` che contiene le impostazioni del tipo di file da utilizzare nella conversione. Le impostazioni relative ai tipi di file forniscono le impostazioni di conversione per diversi tipi di file, ad esempio .doc o .xls.
   * Un oggetto `java.lang.String` che contiene il nome delle impostazioni PDF da utilizzare. Ad esempio, è possibile specificare `Standard`.
   * Un oggetto `java.lang.String` che contiene il nome delle impostazioni di protezione da utilizzare.
   * Un oggetto `com.adobe.idp.Document` facoltativo che contiene le impostazioni da applicare durante la generazione del documento PDF.
   * Un oggetto `com.adobe.idp.Document` facoltativo che contiene le informazioni sui metadati da applicare al documento PDF.

   Il metodo `createPDF2` restituisce un oggetto `CreatePDFResult` che contiene il nuovo documento PDF e le informazioni di registro. Il file di registro in genere contiene messaggi di errore o di avviso generati dalla richiesta di conversione.

1. Recuperate i risultati.

   Per ottenere il documento PDF, effettuare le seguenti operazioni:

   * Richiamare il metodo `CreatePDFResult` dell&#39;oggetto `getCreatedDocument`, che restituisce un oggetto `com.adobe.idp.Document`.
   * Richiamare il metodo `com.adobe.idp.Document` dell&#39;oggetto `copyToFile` per estrarre il documento PDF dall&#39;oggetto creato nel passaggio precedente.

   Se avete utilizzato il metodo `createPDF2` per ottenere il documento di registro (non applicabile alle conversioni HTML), effettuate le seguenti operazioni:

   * Richiamare il metodo `CreatePDFResult` dell&#39;oggetto `getLogDocument`. Questo restituisce un oggetto `com.adobe.idp.Document`.
   * Richiamare il metodo `com.adobe.idp.Document` dell&#39;oggetto `copyToFile` per estrarre il documento di registro.


**Consulta anche**

[Riepilogo dei passaggi](converting-file-formats-pdf.md#summary-of-steps)

[Avvio rapido (modalità SOAP): Conversione di un documento di Microsoft Word in un documento PDF tramite l&#39;API Java](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-a-microsoft-word-document-to-a-pdf-document-using-the-java-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Conversione di documenti Word in documenti PDF tramite l&#39;API del servizio Web {#convert-word-documents-to-pdf-documents-using-the-web-service-api}

Convertire un documento di Microsoft Word in un documento PDF utilizzando l&#39;API Generate PDF (servizio Web):

1. Includere i file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/GeneratePDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituire `localhost` con l&#39;indirizzo IP del server che ospita  AEM Forms.

1. Creare un client Generate PDF.

   * Creare un oggetto `GeneratePDFServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `GeneratePDFServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passate un valore di stringa che specifica il WSDL al servizio AEM Forms  (ad esempio, `http://localhost:8080/soap/services/GeneratePDFService?blob=mtom`). Non è necessario utilizzare l&#39;attributo `lc_version`. Tuttavia, specificate `?blob=mtom`.
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `GeneratePDFServiceClient.Endpoint.Binding`. Inserite il valore restituito in `BasicHttpBinding`.
   * Impostare il campo `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto `MessageEncoding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilitate l&#39;autenticazione HTTP di base eseguendo le seguenti operazioni:

      * Assegnare il nome utente del modulo AEM al campo `GeneratePDFServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `GeneratePDFServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recuperare il file da convertire in un documento PDF.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare il file da convertire in documento PDF.
   * Creare un oggetto `System.IO.FileStream` richiamandone il costruttore. Passa un valore di stringa che rappresenta la posizione del file da convertire e la modalità in cui aprire il file.
   * Creare un array di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà `System.IO.FileStream` dell&#39;oggetto `Length`.
   * Compilare l&#39;array di byte con i dati del flusso richiamando il metodo `Read` dell&#39;oggetto `System.IO.FileStream` e passando l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando alla relativa proprietà `MTOM` il contenuto dell&#39;array di byte.

1. Convertire il file in un documento PDF.

   Per convertire il file in un documento PDF, richiamare il metodo `GeneratePDFServiceService` dell&#39;oggetto &lt;a1/> e passare i valori seguenti:`CreatePDF2`

   * Un oggetto `BLOB` che rappresenta il file da convertire.
   * Una stringa che contiene l&#39;estensione del file.
   * Un oggetto `java.lang.String` che contiene le impostazioni del tipo di file da utilizzare nella conversione. Le impostazioni relative ai tipi di file forniscono le impostazioni di conversione per diversi tipi di file, ad esempio .doc o .xls.
   * Un oggetto stringa che contiene le impostazioni PDF da utilizzare. È possibile specificare `Standard`.
   * Un oggetto stringa che contiene le impostazioni di protezione da utilizzare. È possibile specificare `No Security`.
   * Un oggetto `BLOB` facoltativo che contiene le impostazioni da applicare durante la generazione del documento PDF.
   * Un oggetto `BLOB` facoltativo che contiene le informazioni sui metadati da applicare al documento PDF.
   * Un parametro di output di tipo `BLOB` compilato dal metodo `CreatePDF2`. Il metodo `CreatePDF2` compila l&#39;oggetto con il documento convertito. (Questo valore di parametro è richiesto solo per la chiamata al servizio Web).
   * Un parametro di output di tipo `BLOB` compilato dal metodo `CreatePDF2`. Il metodo `CreatePDF2` compila l&#39;oggetto con il documento di registro. (Questo valore di parametro è richiesto solo per la chiamata al servizio Web).

1. Recuperate i risultati.

   * Recuperare il documento PDF convertito assegnando il campo `MTOM` dell&#39;oggetto `BLOB` a un array di byte. L&#39;array di byte rappresenta il documento PDF convertito. Assicurarsi di utilizzare l&#39;oggetto `BLOB` utilizzato come parametro di output per il metodo `createPDF2`.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF convertito.
   * Creare un oggetto `System.IO.BinaryWriter` richiamandone il costruttore e passando l&#39;oggetto `System.IO.FileStream`.
   * Scrivere il contenuto dell&#39;array di byte in un file PDF richiamando il metodo `System.IO.BinaryWriter` dell&#39;oggetto `Write` e passando l&#39;array di byte.

**Consulta anche**

[Riepilogo dei passaggi](converting-file-formats-pdf.md#summary-of-steps)

[Chiamata  AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chiamata  AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Conversione di documenti HTML in documenti PDF {#converting-html-documents-to-pdf-documents}

Questa sezione descrive come utilizzare l&#39;API Generate PDF per convertire in modo programmatico i documenti HTML in documenti PDF.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Genera PDF, vedere [Guida di riferimento dei servizi per  AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-1}

Per convertire un documento HTML in un documento PDF, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un client Generate PDF.
1. Recuperate il contenuto HTML da convertire in un documento PDF.
1. Convertite il contenuto HTML in un documento PDF.
1. Recuperate i risultati.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, accertatevi di includere i file proxy.

**Creazione di un client PDF**

Prima di eseguire un&#39;operazione Genera PDF a livello di programmazione, è necessario creare un client di servizi Genera PDF. Se utilizzate l&#39;API Java, create un oggetto `GeneratePdfServiceClient`. Se utilizzate l&#39;API del servizio Web, create un `GeneratePDFServiceService`.

**Recuperare il contenuto HTML da convertire in un documento PDF**

Fate riferimento al contenuto HTML da convertire in un documento PDF. Potete fare riferimento al contenuto HTML, ad esempio un file HTML o un contenuto HTML accessibile tramite un URL.

**Conversione del contenuto HTML in un documento PDF**

Dopo aver creato il client di servizi, potete richiamare l’operazione di creazione PDF appropriata. Questa operazione richiede informazioni sul documento da convertire, compreso il percorso del documento di destinazione.

**Recuperare i risultati**

Dopo aver convertito il contenuto HTML in un documento PDF, è possibile recuperare i risultati e salvare il documento PDF.

**Consulta anche**

[Convertire il contenuto HTML in un documento PDF utilizzando l&#39;API Java](converting-file-formats-pdf.md#convert-html-content-to-a-pdf-document-using-the-java-api)

[Conversione di contenuto HTML in un documento PDF tramite l&#39;API del servizio Web](converting-file-formats-pdf.md#convert-html-content-to-a-pdf-document-using-the-web-service-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Generazione rapida API servizio PDF](/help/forms/developing/generate-pdf-service-java-api.md#generate-pdf-service-java-api-quick-start-soap)

### Convertire il contenuto HTML in un documento PDF utilizzando l&#39;API Java {#convert-html-content-to-a-pdf-document-using-the-java-api}

Convertire un documento HTML in un documento PDF utilizzando l&#39;API Generate PDF (Java):

1. Includere i file di progetto.

   Includete file JAR client, ad esempio adobe-generatepdf-client.jar, nel percorso di classe del progetto Java.

1. Creare un client Generate PDF.

   Creare un oggetto `GeneratePdfServiceClient` utilizzando il relativo costruttore e passando un oggetto `ServiceClientFactory` che contiene proprietà di connessione.

1. Recuperate il contenuto HTML da convertire in un documento PDF.

   Recuperate il contenuto HTML creando una variabile stringa e assegnando un URL che punta al contenuto HTML.

1. Convertite il contenuto HTML in un documento PDF.

   Richiamare il metodo `GeneratePdfServiceClient` dell&#39;oggetto `htmlToPDF2` e trasmettere i seguenti valori:

   * Un oggetto `java.lang.String` che contiene l&#39;URL del file HTML da convertire.
   * Un oggetto `java.lang.String` che contiene le impostazioni del tipo di file da utilizzare nella conversione. Le impostazioni del tipo di file possono includere livelli di ragionamento.
   * Un oggetto `java.lang.String` che contiene il nome delle impostazioni di protezione da utilizzare.
   * Un oggetto `com.adobe.idp.Document` facoltativo che contiene le impostazioni da applicare durante la generazione del documento PDF. Se queste informazioni non vengono fornite, le impostazioni vengono scelte automaticamente in base ai tre parametri precedenti.
   * Un oggetto `com.adobe.idp.Document` facoltativo che contiene le informazioni sui metadati da applicare al documento PDF.

1. Recuperate i risultati.

   Il metodo `htmlToPDF2` restituisce un oggetto `HtmlToPdfResult` che contiene il nuovo documento PDF generato. Per ottenere il documento PDF appena creato, effettuare le seguenti operazioni:

   * Richiamare il metodo `HtmlToPdfResult` dell&#39;oggetto `getCreatedDocument`. Questo restituisce un oggetto `com.adobe.idp.Document`.
   * Richiamare il metodo `com.adobe.idp.Document` dell&#39;oggetto `copyToFile` per estrarre il documento PDF dall&#39;oggetto creato nel passaggio precedente.

**Consulta anche**

[Conversione di documenti HTML in documenti PDF](converting-file-formats-pdf.md#converting-html-documents-to-pdf-documents)

[Avvio rapido (modalità SOAP): Conversione del contenuto HTML in un documento PDF tramite l&#39;API Java](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-html-content-to-a-pdf-document-using-the-java-api)

[Avvio rapido (modalità SOAP): Conversione del contenuto HTML in un documento PDF tramite l&#39;API Java](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-html-content-to-a-pdf-document-using-the-java-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Convertire il contenuto HTML in un documento PDF utilizzando l&#39;API del servizio Web {#convert-html-content-to-a-pdf-document-using-the-web-service-api}

Convertire il contenuto HTML in un documento PDF utilizzando l&#39;API Generate PDF (servizio Web):

1. Includere i file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/GeneratePDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituire `localhost` con l&#39;indirizzo IP del server che ospita  AEM Forms.

1. Creare un client Generate PDF.

   * Creare un oggetto `GeneratePDFServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `GeneratePDFServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passate un valore di stringa che specifica il WSDL al servizio AEM Forms  (ad esempio, `http://localhost:8080/soap/services/GeneratePDFService?blob=mtom`). Non è necessario utilizzare l&#39;attributo `lc_version`. Tuttavia, specificate `?blob=mtom`.
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `GeneratePDFServiceClient.Endpoint.Binding`. Inserite il valore restituito in `BasicHttpBinding`.
   * Impostare il campo `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto `MessageEncoding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilitate l&#39;autenticazione HTTP di base eseguendo le seguenti operazioni:

      * Assegnare il nome utente del modulo AEM al campo `GeneratePDFServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `GeneratePDFServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recuperate il contenuto HTML da convertire in un documento PDF.

   Recuperate il contenuto HTML creando una variabile stringa e assegnando un URL che punta al contenuto HTML.

1. Convertite il contenuto HTML in un documento PDF.

   Convertite il contenuto HTML in un documento PDF richiamando il metodo `GeneratePDFServiceService` dell&#39;oggetto &lt;a1/> e passando i seguenti valori:`HtmlToPDF2`

   * Una stringa che contiene il contenuto HTML da convertire.
   * Un oggetto `java.lang.String` che contiene le impostazioni del tipo di file da utilizzare nella conversione.
   * Un oggetto stringa che contiene le impostazioni di protezione da utilizzare.
   * Un oggetto `BLOB` facoltativo che contiene le impostazioni da applicare durante la generazione del documento PDF.
   * Un oggetto `BLOB` facoltativo che contiene le informazioni sui metadati da applicare al documento PDF.
   * Un parametro di output di tipo `BLOB` compilato dal metodo `CreatePDF2`. Il metodo `CreatePDF2` compila l&#39;oggetto con il documento convertito. (Questo valore di parametro è richiesto solo per la chiamata al servizio Web).

1. Recuperate i risultati.

   * Recuperare il documento PDF convertito assegnando il campo `MTOM` dell&#39;oggetto `BLOB` a un array di byte. L&#39;array di byte rappresenta il documento PDF convertito. Assicurarsi di utilizzare l&#39;oggetto `BLOB` utilizzato come parametro di output per il metodo `HtmlToPDF2`.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF convertito.
   * Creare un oggetto `System.IO.BinaryWriter` richiamandone il costruttore e passando l&#39;oggetto `System.IO.FileStream`.
   * Scrivere il contenuto dell&#39;array di byte in un file PDF richiamando il metodo `System.IO.BinaryWriter` dell&#39;oggetto `Write` e passando l&#39;array di byte.

**Consulta anche**

[Conversione di documenti HTML in documenti PDF](converting-file-formats-pdf.md#converting-html-documents-to-pdf-documents)

[Chiamata  AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chiamata  AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Conversione di documenti PDF in formati non immagine {#converting-pdf-documents-to-non-image-formats}

Questa sezione descrive come utilizzare l&#39;API Java Generate PDF e l&#39;API del servizio Web per convertire un documento PDF in un file RTF a livello di programmazione, che è un esempio di formato non immagine. Altri formati non immagine includono HTML, testo, DOC ed EPS. Durante la conversione di un documento PDF in formato RTF, assicurarsi che il documento PDF non contenga elementi del modulo, ad esempio un pulsante di invio. Gli elementi del modulo non vengono convertiti.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Genera PDF, vedere [Guida di riferimento dei servizi per  AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-2}

Per convertire un documento PDF in uno dei tipi supportati, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un client Generate PDF.
1. Recuperare il documento PDF da convertire.
1. Convertire il documento PDF.
1. Salvate il file convertito.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, accertatevi di includere i file proxy.

**Creazione di un client PDF**

Prima di eseguire un&#39;operazione Genera PDF a livello di programmazione, è necessario creare un client di servizi Genera PDF. Se utilizzate l&#39;API Java, create un oggetto `GeneratePdfServiceClient`. Se utilizzate l&#39;API del servizio Web, create un oggetto `GeneratePDFServiceService`.

**Recuperare il documento PDF da convertire**

Recuperare il documento PDF per la conversione in un formato non immagine.

**Conversione del documento PDF**

Dopo aver creato il client del servizio, potete richiamare l’operazione di esportazione PDF. Questa operazione richiede informazioni sul documento da convertire, compreso il percorso del documento di destinazione.

**Salvare il file convertito**

Salvate il file convertito. Ad esempio, se convertite un documento PDF in un file RTF, salvate il documento convertito in un file RTF.

**Consulta anche**

[Conversione di un documento PDF in un file RTF mediante l&#39;API Java](converting-file-formats-pdf.md#convert-a-pdf-document-to-a-rtf-file-using-the-java-api)

[Conversione di un documento PDF in un file RTF tramite l&#39;API del servizio Web](converting-file-formats-pdf.md#convert-a-pdf-document-to-a-rtf-file-using-the-web-service-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Generazione rapida API servizio PDF](/help/forms/developing/generate-pdf-service-java-api.md#generate-pdf-service-java-api-quick-start-soap)

### Convertire un documento PDF in un file RTF utilizzando l&#39;API Java {#convert-a-pdf-document-to-a-rtf-file-using-the-java-api}

Convertire un documento PDF in un file RTF utilizzando l&#39;API Generate PDF (Java):

1. Includere i file di progetto.

   Includete file JAR client, ad esempio adobe-generatepdf-client.jar, nel percorso di classe del progetto Java.

1. Creare un client Generate PDF.

   Creare un oggetto `GeneratePdfServiceClient` utilizzando il relativo costruttore e passando un oggetto `ServiceClientFactory` che contiene proprietà di connessione.

1. Recuperare il documento PDF da convertire.

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento PDF da convertire utilizzando il relativo costruttore. Passa un valore di stringa che specifica la posizione del documento PDF.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Convertire il documento PDF.

   Richiamare il metodo `GeneratePdfServiceClient` dell&#39;oggetto `exportPDF2` e trasmettere i seguenti valori:

   * Un oggetto `com.adobe.idp.Document` che rappresenta il file PDF da convertire.
   * Un oggetto `java.lang.String` che contiene il nome del file da convertire.
   * Un oggetto `java.lang.String` che contiene il nome delle impostazioni Adobe PDF .
   * Un oggetto `ConvertPDFFormatType` che specifica il tipo di file di destinazione per la conversione.
   * Un oggetto `com.adobe.idp.Document` facoltativo che contiene le impostazioni da applicare durante la generazione del documento PDF.

   Il metodo `exportPDF2` restituisce un oggetto `ExportPDFResult` che contiene il file convertito.

1. Convertire il documento PDF.

   Per ottenere il file appena creato, effettuate le seguenti operazioni:

   * Richiamare il metodo `ExportPDFResult` dell&#39;oggetto `getConvertedDocument`. Questo restituisce un oggetto `com.adobe.idp.Document`.
   * Richiamare il metodo `com.adobe.idp.Document` dell&#39;oggetto `copyToFile` per estrarre il nuovo documento.

**Consulta anche**

[Riepilogo dei passaggi](converting-file-formats-pdf.md#summary-of-steps)

[Avvio rapido (modalità SOAP): Conversione del contenuto HTML in un documento PDF tramite l&#39;API Java](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-html-content-to-a-pdf-document-using-the-java-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Convertire un documento PDF in un file RTF utilizzando l&#39;API del servizio Web {#convert-a-pdf-document-to-a-rtf-file-using-the-web-service-api}

Convertire un documento PDF in un file RTF utilizzando l&#39;API Generate PDF (servizio Web):

1. Includere i file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/GeneratePDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituire `localhost` con l&#39;indirizzo IP del server che ospita  AEM Forms.

1. Creare un client Generate PDf.

   * Creare un oggetto `GeneratePDFServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `GeneratePDFServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passate un valore di stringa che specifica il WSDL al servizio AEM Forms  (ad esempio, `http://localhost:8080/soap/services/GeneratePDFService?blob=mtom`). Non è necessario utilizzare l&#39;attributo `lc_version`. Tuttavia, specificate `?blob=mtom`.
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `GeneratePDFServiceClient.Endpoint.Binding`. Inserite il valore restituito in `BasicHttpBinding`.
   * Impostare il campo `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto `MessageEncoding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilitate l&#39;autenticazione HTTP di base eseguendo le seguenti operazioni:

      * Assegnare il nome utente del modulo AEM al campo `GeneratePDFServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `GeneratePDFServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recuperare il documento PDF da convertire.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare un documento PDF convertito.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà `System.IO.FileStream` dell&#39;oggetto `Length`.
   * Compilare l&#39;array di byte con i dati del flusso richiamando il metodo `Read` dell&#39;oggetto `System.IO.FileStream` e passando l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando alla relativa proprietà `MTOM` il contenuto dell&#39;array di byte.

1. Convertire il documento PDF.

   Richiamare il metodo `GeneratePDFServiceServiceWse` dell&#39;oggetto `ExportPDF2` e trasmettere i seguenti valori:

   * Un oggetto `BLOB` che rappresenta il file PDF da convertire.
   * Una stringa che contiene il nome del percorso del file da convertire.
   * Un oggetto `java.lang.String` che specifica la posizione del file.
   * Un oggetto stringa che specifica il tipo di file di destinazione per la conversione. Specifica `RTF`.
   * Un oggetto `BLOB` facoltativo che contiene le impostazioni da applicare durante la generazione del documento PDF.
   * Un parametro di output di tipo `BLOB` compilato dal metodo `ExportPDF2`. Il metodo `ExportPDF2` compila l&#39;oggetto con il documento convertito. (Questo valore di parametro è richiesto solo per la chiamata al servizio Web).

1. Salvate il file convertito.

   * Recuperare il documento RTF convertito assegnando il campo `MTOM` dell&#39;oggetto `BLOB` a un array di byte. L&#39;array di byte rappresenta il documento RTF convertito. Assicurarsi di utilizzare l&#39;oggetto `BLOB` utilizzato come parametro di output per il metodo `ExportPDF2`.
   * Creare un oggetto `System.IO.FileStream` richiamandone il costruttore. Passa un valore di stringa che rappresenta la posizione del file RTF.
   * Creare un oggetto `System.IO.BinaryWriter` richiamandone il costruttore e passando l&#39;oggetto `System.IO.FileStream`.
   * Scrivere il contenuto dell&#39;array di byte in un file RTF richiamando il metodo `System.IO.BinaryWriter` dell&#39;oggetto `Write` e passando l&#39;array di byte.

**Consulta anche**

[Riepilogo dei passaggi](converting-file-formats-pdf.md#summary-of-steps)

[Chiamata  AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chiamata  AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Aggiunta del supporto per formati di file nativi aggiuntivi {#adding-support-for-additional-native-file-formats}

In questa sezione viene illustrato come aggiungere il supporto per ulteriori formati di file nativi. Fornisce una panoramica delle interazioni tra il servizio Genera PDF e le applicazioni native utilizzate da questo servizio per convertire i formati di file nativi in PDF.

Questa sezione spiega anche quanto segue:

* Come modificare la risposta fornita dal servizio Genera PDF alle applicazioni native che il prodotto utilizza già per convertire i formati di file nativi in PDF
* Interazioni tra il servizio Genera PDF, il componente Generate PDF service Application Monitor (AppMon) e le applicazioni native, come Microsoft Word
* I ruoli che le grammatiche XML svolgono in tali interazioni

### Interazioni dei componenti {#component-interactions}

Il servizio Genera PDF converte i formati di file nativi richiamando l&#39;applicazione associata al formato di file e interagendo con l&#39;applicazione per stampare il documento utilizzando la stampante predefinita. La stampante predefinita deve essere impostata come stampante  Adobe PDF.

Questa illustrazione mostra i componenti e i driver coinvolti nel supporto nativo delle applicazioni. Inoltre, menziona le grammatiche XML che influenzano le interazioni.

Interazioni dei componenti per la conversione dei file nativi

Questo documento utilizza il termine *applicazione nativa* per indicare l&#39;applicazione utilizzata per produrre un formato di file nativo, ad esempio Microsoft Word.

** AppMonis un componente Enterprise che interagisce con un&#39;applicazione nativa nello stesso modo in cui un utente naviga nelle finestre di dialogo presentate da tale applicazione. Le grammatiche XML utilizzate da AppMon per indicare a un&#39;applicazione, come Microsoft Word, di aprire e stampare un file richiedono le seguenti attività sequenziali:

1. Per aprire il file, selezionare File > Apri
1. Assicurarsi che venga visualizzata la finestra di dialogo Apri; in caso contrario, gestione dell&#39;errore
1. Specificare il nome del file nel campo Nome file e fare clic sul pulsante Apri
1. Verificare che il file venga aperto
1. Aprire la finestra di dialogo Stampa selezionando File > Stampa
1. Verificare che venga visualizzata la finestra di dialogo Stampa

AppMon utilizza le API Win32 standard per interagire con le applicazioni di terze parti al fine di trasferire eventi dell&#39;interfaccia utente quali tasti e clic del mouse, il che è utile per controllare queste applicazioni e generare file PDF da esse.

A causa di un limite con queste API Win32, AppMon non è in grado di inviare questi eventi dell&#39;interfaccia utente ad alcuni tipi specifici di finestre, come barre di menu mobili (trovate in alcune applicazioni come TextPad), e certi tipi di finestre di dialogo il cui contenuto non può essere recuperato utilizzando le API Win32.

È facile identificare visivamente una barra di menu mobile; tuttavia, potrebbe non essere possibile identificare i tipi speciali di dialoghi solo attraverso l&#39;ispezione visiva. È necessario un&#39;applicazione di terze parti come Microsoft Spy++ (parte dell&#39;ambiente di sviluppo di Microsoft Visual C++) o il relativo WinID equivalente (che può essere scaricato gratuitamente da [https://www.dennisbabkin.com/php/download.php?what=WinID](https://www.dennisbabkin.com/php/download.php?what=WinID)) per esaminare una finestra di dialogo per determinare se AppMon possa interagire con esso utilizzando le API Win32 standard.

Se WinID è in grado di estrarre il contenuto della finestra di dialogo come il testo, le finestre secondarie, l’ID della classe della finestra e così via, AppMon sarà in grado di fare lo stesso.

In questa tabella sono elencati i tipi di informazioni utilizzati per la stampa dei formati di file nativi.

<table>
 <thead>
  <tr>
   <th><p>Tipo di informazione</p></th>
   <th><p>Descrizione</p></th>
   <th><p>Modifica/creazione di voci correlate a file nativi </p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>Impostazioni amministrative </p></td>
   <td><p>Include le impostazioni PDF, le impostazioni di protezione e il tipo di file. </p><p>Le impostazioni del tipo di file associano le estensioni del nome di file alle applicazioni native corrispondenti. Le impostazioni del tipo di file specificano anche le impostazioni dell'applicazione nativa utilizzate per stampare i file nativi. </p></td>
   <td><p>Per modificare le impostazioni per un'applicazione nativa già supportata, l'amministratore di sistema imposta le impostazioni Tipo file nella console di amministrazione. </p><p>Per aggiungere il supporto per un nuovo formato di file nativo, è necessario modificare manualmente il file. (Vedere <a href="converting-file-formats-pdf.md#adding-or-modifying-support-for-a-native-file-format">Aggiunta o modifica del supporto per un formato di file nativo</a>.) </p></td>
  </tr>
  <tr>
   <td><p>Script </p></td>
   <td><p>Specifica le interazioni tra il servizio Genera PDF e un'applicazione nativa. Tali interazioni di solito indirizzano l'applicazione a stampare un file sul driver Adobe PDF . </p><p>Lo script contiene istruzioni che indirizzano l'applicazione nativa all'apertura di finestre di dialogo specifiche e che forniscono risposte specifiche ai campi e ai pulsanti di tali finestre di dialogo. </p></td>
   <td><p>Il servizio Genera PDF include file di script per tutte le applicazioni native supportate. Potete modificare questi file utilizzando un'applicazione di modifica XML.</p><p>Per aggiungere il supporto per una nuova applicazione nativa, è necessario creare un nuovo file di script. (Vedere <a href="converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application">Creazione o modifica di un file XML di dialogo aggiuntivo per un'applicazione nativa</a>.) </p></td>
  </tr>
  <tr>
   <td><p>Istruzioni generali della finestra di dialogo </p></td>
   <td><p>Specifica come rispondere alle finestre di dialogo comuni a più applicazioni. Tali finestre di dialogo sono generate da sistemi operativi, applicazioni helper (come PDFMaker) e driver. </p><p>Il file che contiene queste informazioni è appmon.global.en_US.xml.</p></td>
   <td><p>Non modificate questo file. </p></td>
  </tr>
  <tr>
   <td><p>Istruzioni per la finestra di dialogo specifica per l'applicazione</p></td>
   <td><p>Specifica come rispondere alle finestre di dialogo specifiche dell'applicazione. </p><p>Il file che contiene queste informazioni è appmon.<i>`[nomeapp]`</i>.dialog.<i>`[locale]`</i>.xml (ad esempio, appmon.word.en_US.xml).</p></td>
   <td><p>Non modificate questo file. </p><p>Per aggiungere le istruzioni della finestra di dialogo per una nuova applicazione nativa, vedere <a href="converting-file-formats-pdf.md#creating_or_modifying_an_additional_dialog_xml_file_for_a_native_application">Creazione o modifica di un file XML di dialogo aggiuntivo per un'applicazione nativa</a>.</p></td>
  </tr>
  <tr>
   <td><p>Istruzioni aggiuntive per la finestra di dialogo specifica per l’applicazione </p></td>
   <td><p>Specifica sostituzioni e aggiunte alle istruzioni della finestra di dialogo specifica per l’applicazione. La sezione presenta un esempio di tali informazioni. </p><p>Il file che contiene queste informazioni è appmon.<i>`[nomeapp]`</i>.add.<i>`[locale]`</i>.xml. Un esempio è appmon.addizione.en_US.xml.</p></td>
   <td><p>I file di questo tipo possono essere creati e modificati utilizzando un'applicazione di modifica XML. (Vedere <a href="converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application">Creazione o modifica di un file XML di dialogo aggiuntivo per un'applicazione nativa</a>.) </p><p><strong>Importante</strong>: È necessario creare ulteriori istruzioni per la finestra di dialogo specifiche per l'applicazione per ogni applicazione nativa supportata dal server. </p></td>
  </tr>
 </tbody>
</table>

### Informazioni sullo script e sui file XML della finestra di dialogo {#about-the-script-and-dialog-xml-files}

I file XML di script indirizzano il servizio Genera PDF per spostarsi tra le finestre di dialogo dell&#39;applicazione nello stesso modo in cui l&#39;utente naviga attraverso le finestre di dialogo dell&#39;applicazione. I file XML di script inoltre indirizzano il servizio Genera PDF per rispondere alle finestre di dialogo eseguendo azioni quali la pressione dei pulsanti, la selezione o la deselezione delle caselle di controllo o la selezione delle voci di menu.

Al contrario, i file XML di dialogo rispondono semplicemente a finestre di dialogo con gli stessi tipi di azioni utilizzate nei file XML di script.

#### Terminologia della finestra di dialogo e dell&#39;elemento finestra {#dialog-box-and-window-element-terminology}

In questa sezione e nella sezione successiva viene utilizzata una terminologia diversa per le finestre di dialogo e per i componenti che contengono, a seconda della prospettiva descritta. I componenti della finestra di dialogo sono elementi quali pulsanti, campi e caselle combinate.

Quando questa sezione e la sezione successiva descrivono le finestre di dialogo e i relativi componenti dal punto di vista di un utente, vengono utilizzati termini quali *finestra di dialogo*, *pulsante*, *campo* e *casella combinata*.

Quando questa sezione e la sezione successiva descrivono le finestre di dialogo e i relativi componenti dal punto di vista della loro rappresentazione interna, viene utilizzato il termine *elemento finestra*. La rappresentazione interna degli elementi finestra è una gerarchia, in cui ogni istanza di elemento finestra è identificata dalle etichette. L&#39;istanza dell&#39;elemento window descrive inoltre le sue caratteristiche fisiche e il suo comportamento.

Dal punto di vista dell&#39;utente, le finestre di dialogo e i relativi componenti mostrano comportamenti diversi, dove alcuni elementi delle finestre di dialogo vengono nascosti fino all&#39;attivazione. Dal punto di vista della rappresentazione interna, non esiste alcun problema di comportamento. Ad esempio, la rappresentazione interna di una finestra di dialogo ha un aspetto simile a quello dei componenti che contiene, ad eccezione del fatto che i componenti sono nidificati all&#39;interno della finestra di dialogo.

Questa sezione descrive gli elementi XML che forniscono istruzioni ad AppMon. Questi elementi hanno nomi quali l&#39;elemento `dialog` e l&#39;elemento `window`. In questo documento viene utilizzato un font monospazio per distinguere gli elementi XML. L&#39;elemento `dialog` identifica una finestra di dialogo che consente la visualizzazione intenzionale o non intenzionale di un file di script XML. L&#39;elemento `window` identifica un elemento finestra (finestra di dialogo o componenti di una finestra di dialogo).

#### Gerarchia {#hierarchy}

Questo diagramma mostra la gerarchia di script e finestra di dialogo XML. Un file XML di script è conforme allo schema script.xsd, che include (in senso XML) lo schema window.xsd. Analogamente, un file XML della finestra di dialogo è conforme allo schema dialogs.xsd, che include anche lo schema window.xsd.

![as_as_xml_hierarchy](assets/as_as_xml_hierarchy.png)

Gerarchia dello script e della finestra di dialogo XML

#### Script di file XML {#script-xml-files}

Un *file XML di script* specifica una serie di passaggi che indirizzano l&#39;applicazione nativa a spostarsi su alcuni elementi della finestra e quindi a fornire le risposte a tali elementi. La maggior parte delle risposte è costituita da testo o tasti che corrispondono all&#39;input che un utente immette a un campo, a una casella combinata o a un pulsante nella finestra di dialogo corrispondente.

Il supporto del servizio Genera PDF per i file XML di script ha lo scopo di indirizzare un&#39;applicazione nativa alla stampa di un file nativo. Tuttavia, i file XML di script possono essere utilizzati per eseguire qualsiasi attività che un utente può eseguire quando interagisce con le finestre di dialogo dell&#39;applicazione nativa.

I passaggi contenuti in un file XML di script vengono eseguiti in ordine, senza possibilità di branching. L&#39;unico test condizionale supportato è per timeout/tentativi, che causa la chiusura di uno script se un passaggio non viene completato correttamente entro un periodo di tempo specifico e dopo un numero specifico di tentativi.

Oltre alla sequenza dei passaggi, le istruzioni all&#39;interno di un passaggio vengono anche eseguite in ordine. È necessario assicurarsi che i passaggi e le istruzioni riflettano l&#39;ordine in cui un utente eseguirebbe gli stessi passaggi.

Ciascun passaggio in un file XML di script identifica l&#39;elemento window che deve essere visualizzato se le istruzioni del passaggio vengono eseguite correttamente. Se durante l&#39;esecuzione di un passaggio di script viene visualizzata una finestra di dialogo imprevista, il servizio Genera PDF effettua la ricerca nei file XML della finestra di dialogo come descritto nella sezione successiva.

#### File XML di dialogo {#dialog-xml-files}

L&#39;esecuzione di applicazioni native visualizza diverse finestre di dialogo, che vengono visualizzate indipendentemente dal fatto che le applicazioni native siano in modalità visibile o invisibile. Le finestre di dialogo possono essere generate dal sistema operativo o dall&#39;applicazione stessa. Quando le applicazioni native sono in esecuzione sotto il controllo del servizio Genera PDF, le finestre di dialogo del sistema e dell&#39;applicazione nativa vengono visualizzate in una finestra invisibile.

Un *file XML della finestra di dialogo* specifica in che modo il servizio Genera PDF risponde alle finestre di dialogo del sistema o dell&#39;applicazione nativa. I file XML della finestra di dialogo consentono al servizio Genera PDF di rispondere alle finestre di dialogo non visualizzate in modo da facilitare il processo di conversione.

Quando nel sistema o nell&#39;applicazione nativa viene visualizzata una finestra di dialogo non gestita dal file XML di script attualmente in esecuzione, il servizio Genera PDF esegue la ricerca nei file XML della finestra di dialogo in questo ordine, arrestandosi quando viene rilevata una corrispondenza:

* appmon.`[appname]`.Additional.`[locale]`.xml
* appmon.`[appname]`.`[locale]`.xml (non modificate questo file).
* appmon.global.`[locale]`.xml (non modificate questo file).

Se il servizio Genera PDF trova una corrispondenza per la finestra di dialogo, la ignora inviando la tastiera o altre azioni specificate per la finestra di dialogo. Se nelle istruzioni della finestra di dialogo viene specificato un messaggio di interruzione, il servizio Genera PDF interrompe il processo in esecuzione e genera un messaggio di errore. Tale messaggio di interruzione viene specificato nell&#39;elemento `abortMessage` della grammatica XML dello script.

Se il servizio Genera PDF rileva una finestra di dialogo non descritta in nessuno dei file elencati in precedenza, il servizio Genera PDF incorpora la didascalia della finestra di dialogo nella voce del file di registro. Il processo attualmente in esecuzione alla fine si interrompe. Potete quindi utilizzare le informazioni contenute nel file di registro per comporre nuove istruzioni nel file XML della finestra di dialogo aggiuntivo per l&#39;applicazione nativa.

### Aggiunta o modifica del supporto per un formato di file nativo {#adding-or-modifying-support-for-a-native-file-format}

Questa sezione descrive le attività da eseguire per supportare altri formati di file nativi o per modificare il supporto per un formato di file nativo già supportato.

Prima di poter aggiungere o modificare il supporto, è necessario completare le seguenti attività.

#### Scelta di uno strumento per identificare gli elementi della finestra {#choosing-a-tool-for-identifying-window-elements}

I file XML di finestra di dialogo e script richiedono l&#39;identificazione dell&#39;elemento finestra (finestra di dialogo, campo o altro componente di dialogo) a cui l&#39;elemento script o finestra di dialogo risponde. Ad esempio, dopo che uno script richiama un menu per un&#39;applicazione nativa, lo script deve identificare l&#39;elemento finestra del menu a cui applicare i tasti o un&#39;azione.

È possibile identificare facilmente una finestra di dialogo mediante la didascalia visualizzata nella barra del titolo. Tuttavia, è necessario utilizzare uno strumento come Microsoft Spy++ per identificare gli elementi della finestra di livello inferiore. Gli elementi della finestra di livello inferiore possono essere identificati attraverso una serie di attributi, che non sono ovvi. Inoltre, ogni applicazione nativa può identificare in modo diverso il proprio elemento finestra. Di conseguenza, esistono diversi modi per identificare un elemento finestra. Di seguito è riportato l&#39;ordine consigliato per l&#39;identificazione dell&#39;elemento finestra:

1. Didascalia se è univoca
1. ID controllo, che può essere univoco o meno per una determinata finestra di dialogo
1. Nome della classe, che può essere univoco o meno

Per identificare una finestra è possibile utilizzare uno o una combinazione di questi tre attributi.

Se gli attributi non identificano una didascalia, è possibile identificare un elemento finestra utilizzando il relativo indice rispetto al relativo elemento padre. Un elemento *index* specifica la posizione dell&#39;elemento finestra rispetto agli elementi della finestra di pari livello. Spesso, gli indici sono l&#39;unico modo per identificare le caselle combinate.

Tenete presenti i seguenti problemi:

* Microsoft Spy++ visualizza le didascalie utilizzando una e commerciale (&amp;) per identificare il tasto di scelta rapida della didascalia. Ad esempio, Spy++ mostra la didascalia di una finestra di dialogo Stampa come `Pri&nt`, che indica che il tasto di scelta rapida è *n*. I titoli dei sottotitoli nei file XML di script e di dialogo devono omettere le commerciale.
* Alcune didascalie includono le interruzioni di riga. il servizio Genera PDF non è in grado di identificare le interruzioni di riga. Se una didascalia include un&#39;interruzione di riga, includete una porzione sufficiente della didascalia per distinguerla dalle altre voci di menu, quindi utilizzate le espressioni regolari per la parte omessa. Un esempio è ( `^Long caption title$`). (Vedere [Uso di espressioni regolari negli attributi della didascalia](converting-file-formats-pdf.md#using-regular-expressions-in-caption-attributes).)
* Utilizzare entità carattere (o sequenze di escape) per caratteri XML riservati. Ad esempio, utilizzare `&` per le e commerciale, `<` e `>` per i simboli minore e maggiore di, `&apos;` per gli apostrofi e `&quot;` per le virgolette.

Se intendete lavorare su file di dialogo o script XML, installate l&#39;applicazione Microsoft Spy++.

#### Estrazione del pacchetto dei file di finestra di dialogo e script {#unpackaging-the-dialog-and-script-files}

I file di dialogo e script risiedono nel file appmondata.jar. Per poter modificare uno di questi file o aggiungere nuovi file di script o di dialogo, è necessario rimuovere il pacchetto dal file JAR. Ad esempio, si supponga di voler aggiungere il supporto per l&#39;applicazione EditPlus. Potete creare due file XML denominati appmon.editplus.script.en_US.xml e appmon.editplus.script.add.en_US.xml. Questi script XML devono essere aggiunti al file adobe-appmondata.jar in due posizioni, come specificato di seguito:

* adobe-livecycle-native-jboss-x86_win32.ear > adobe-Native2PDFSvc.war\WEB-INF\lib > adobe-native.jar > Native2PDFSvc-native.jar\bin > adobe-appmondata.jar\com\adobe\appmon. Il file adobe-livecycle-native-jboss-x86_win32.ear si trova nella cartella di esportazione in `[AEM forms install directory]\configurationManager`. (se  AEM Forms è distribuito su un altro server applicazioni J2EE, sostituite il file adobe-livecycle-native-jboss-x86_win32.ear con il file EAR corrispondente al server applicazioni J2EE).
* adobe-generatepdf-dsc.jar > adobe-appmondata.jar\com\adobe\appmon (il file adobe-appmondata.jar si trova nel file adobe-generatepdf-dsc.jar). Il file adobe-generatepdf-dsc.jar si trova nella cartella `[AEM forms install directory]\deploy`.

Dopo aver aggiunto questi file XML al file adobe-appmondata.jar, è necessario ridistribuire il componente GeneratePDF. Per aggiungere file di dialogo e script XML al file adobe-appmondata.jar, eseguire le operazioni seguenti:

1. Utilizzando uno strumento come WinZip o WinRAR, aprite il file adobe-livecycle-native-jboss-x86_win32.earfile > adobe-Native2PDFSvc.war\WEB-INF\lib > adobe-native.jar > Native2PDFSvc-native.jar\bin > adobe-appmondata.jar.
1. Aggiungete la finestra di dialogo e i file XML di script al file appmondata.jar o modificate i file XML esistenti in questo file. (Vedere [Creazione o modifica di un file XML di script per un&#39;applicazione nativa](converting-file-formats-pdf.md#creating-or-modifying-a-script-xml-file-for-a-native-application)e [Creazione o modifica di un file XML di dialogo aggiuntivo per un&#39;applicazione nativa](converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application).)
1. Utilizzando uno strumento come WinZip o WinRAR, apri adobe-generatepdf-dsc.jar > adobe-appmondata.jar.
1. Aggiungete la finestra di dialogo e i file XML di script al file appmondata.jar o modificate i file XML esistenti in questo file. (Vedere [Creazione o modifica di un file XML di script per un&#39;applicazione nativa](converting-file-formats-pdf.md#creating-or-modifying-a-script-xml-file-for-a-native-application)e [Creazione o modifica di un file XML di dialogo aggiuntivo per un&#39;applicazione nativa](converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application).) Dopo aver aggiunto i file XML al file adobe-appmondata.jar, inserite il nuovo file adobe-appmondata.jar nel file adobe-generatepdf-dsc.jar.
1. Se è stato aggiunto il supporto per un formato di file nativo aggiuntivo, creare una variabile di ambiente di sistema che fornisca il percorso dell&#39;applicazione (vedere [Creazione di una variabile di ambiente per individuare l&#39;applicazione nativa](converting-file-formats-pdf.md#creating-an-environment-variable-to-locate-the-native-application)).

**Per ridistribuire il componente GeneratePDF**

1. Accedere a Workbench.
1. Selezionare **Finestra** > **Mostra viste** > **Componenti**. Questa azione consente di aggiungere la visualizzazione Componenti a Workbench.
1. Fare clic con il pulsante destro del mouse sul componente GeneratePDF, quindi selezionare **Interrompi componente**.
1. Quando il componente è interrotto, fare clic con il pulsante destro del mouse e selezionare Disinstalla componente per rimuoverlo.
1. Fare clic con il pulsante destro del mouse sull&#39;icona **Componenti** e selezionare **Installa componente**.
1. Individuate e selezionate il file adobe-generatepdf-dsc.jar modificato, quindi fate clic su Apri. Accanto al componente GeneratePDF viene visualizzato un quadrato rosso.
1. Espandere il componente GeneratePDF, selezionare Service Descriptor, quindi fare clic con il pulsante destro del mouse su GeneratePDFService e selezionare Activate Service.
1. Nella finestra di dialogo di configurazione visualizzata, immettete i valori di configurazione applicabili. Se lasciate vuoti questi valori, vengono utilizzati i valori di configurazione predefiniti.
1. Fare clic con il pulsante destro del mouse su GeneratePDF e selezionare Avvia componente.
1. Espandi servizi attivi. Se è in esecuzione, accanto al nome del servizio viene visualizzata una freccia verde. In caso contrario, il servizio è in stato di arresto.
1. Se il servizio è in stato di arresto, fare clic con il pulsante destro del mouse sul nome del servizio e selezionare Avvia servizio.

### Creazione o modifica di un file XML di script per un&#39;applicazione nativa {#creating-or-modifying-a-script-xml-file-for-a-native-application}

Se si desidera indirizzare i file a una nuova applicazione nativa, è necessario creare un file XML di script per tale applicazione. Per modificare il modo in cui il servizio Genera PDF interagisce con un&#39;applicazione nativa già supportata, è necessario modificare lo script per tale applicazione.

Lo script contiene istruzioni che si spostano tra gli elementi della finestra dell&#39;applicazione nativa e forniscono risposte specifiche a tali elementi. Il file che contiene queste informazioni è `appmon.`[nomeapp]&quot;`.script.`[locale]`.xml`. Un esempio è appmon.blocco note.script.en_US.xml.

#### Identificazione dei passaggi che lo script deve eseguire {#identifying-steps-the-script-must-execute}

Utilizzando l&#39;applicazione nativa, determinare gli elementi della finestra da esplorare e ogni risposta da eseguire per stampare il documento. Osservate le finestre di dialogo risultanti da qualsiasi risposta. La procedura sarà simile alla seguente:

1. Selezionare File > Apri.
1. Specificate il percorso e fate clic su Apri.
1. Selezionare File > Stampa nella barra dei menu.
1. Specificare le proprietà richieste per la stampante.
1. Selezionare Stampa e attendere che venga visualizzata la finestra di dialogo Salva con nome. La finestra di dialogo Salva con nome è necessaria affinché il servizio Genera PDF specifichi la destinazione del file PDF.

#### Identificazione delle finestre di dialogo specificate negli attributi della didascalia {#identifying-the-dialogs-specified-in-caption-attributes}

Utilizzate Microsoft Spy++ per ottenere le identità delle proprietà degli elementi finestra nell&#39;applicazione nativa. Per scrivere gli script è necessario disporre di queste identità.

#### Utilizzo di espressioni regolari negli attributi della didascalia {#using-regular-expressions-in-caption-attributes}

È possibile utilizzare espressioni regolari nelle specifiche delle didascalie. Il servizio Genera PDF utilizza la classe `java.util.regex.Matcher` per supportare le espressioni regolari. Tale utilità supporta le espressioni regolari descritte in `java.util.regex.Pattern`. (visitare il sito Web Java all&#39;indirizzo [https://java.sun.com/j2se/1.4.2/docs/api/java/util/regex/Pattern.html](https://java.sun.com/j2se/1.4.2/docs/api/java/util/regex/Pattern.html).)

**Espressione regolare che contiene il nome del file preceduto dal Blocco note nel banner del Blocco note**

```xml
 <!-- The regular expression ".*Notepad" means any number of non-terminating characters followed by Notepad. -->
 <step>
     <expectedWindow>
         <window caption=".*Notepad"/>
     </expectedWindow>
 </step>
```

**Espressione regolare che differenzia Stampa da Impostazione stampa**

```xml
 <!-- This regular expression differentiates the Print dialog box from the Print Setup dialog box. The "^" specifies the beginning of the line, and the "$" specifies the end of the line. -->
 <windowList>
     <window controlID="0x01" caption="^Print$" action="press"/>
 </windowList>
```

#### Ordinamento degli elementi windowList e windowList {#ordering-the-window-and-windowlist-elements}

È necessario ordinare gli elementi `window` e `windowList` come segue:

* Quando più elementi `window` appaiono come elementi secondari in un elemento `windowList` o `dialog`, ordinate questi elementi `window` in ordine decrescente, con le lunghezze dei nomi `caption` che indicano la posizione nell&#39;ordine.
* Quando più elementi `windowList` appaiono in un elemento `window`, ordinate gli elementi `windowList` in ordine decrescente, con le lunghezze degli attributi `caption` del primo elemento `indexes/` che indicano la posizione nell&#39;ordine.

**Ordinamento degli elementi della finestra in un file di dialogo**

```xml
 <!-- The caption attribute in the following window element is 40 characters long. It is the longest caption in this example, so its parent window element appears before the others. -->
 <window caption="Unexpected Failure in DebugActiveProcess">
     <…>
 </window>

 <!-- Caption length is 33 characters. -->
 <window caption="Adobe Acrobat - License Agreement">
     <…>
 </window>

 <!-- Caption length is 33 characters. -->
 <window caption="Microsoft Visual.*Runtime Library">
     <…>
 </window>

 <!-- The caption attribute in the following window element is 28 characters long. It is the shortest caption in this example, so its parent window element appears after the others. -->
 <window caption="Adobe Acrobat - Registration">
     <…>
 </window>
```

**Ordinamento degli elementi della finestra all&#39;interno di un elemento windowList**

```xml
 <!-- The caption attribute in the following indexes element is 56 characters long. It is the longest caption in this example, so its parent window element appears before the others. -->
 <windowList>
     <window caption="Can&apos;t exit design mode because.* cannot be created"/>
     <window className="Button" caption="OK" action="press"/>
 </windowList>
 <windowList>
     <window caption="Do you want to continue loading the project?"/>
     <window className="Button" caption="No" action="press"/>
 </windowList>
 <windowList>
     <window caption="The macros in this project are disabled"/>
     <window className="Button" caption="OK" action="press"/>
 </windowList>
```

### Creazione o modifica di un file XML di finestra di dialogo aggiuntivo per un&#39;applicazione nativa {#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application}

Se si crea uno script per un&#39;applicazione nativa non supportata in precedenza, è necessario creare anche un file XML di dialogo aggiuntivo per tale applicazione. Ogni applicazione nativa utilizzata da AppMon deve avere un solo file XML di dialogo aggiuntivo. Il file XML della finestra di dialogo aggiuntivo è richiesto anche se non sono previste finestre di dialogo non richieste. La finestra di dialogo aggiuntiva deve contenere almeno un elemento `window`, anche se tale elemento `window` è semplicemente un segnaposto.

>[!NOTE]
>
>In questo contesto, il termine aggiuntivo indica il contenuto del file `appmon.[applicationname].addition.[locale]`.xml`. Tale file specifica sostituzioni e aggiunte al file XML della finestra di dialogo.

È inoltre possibile modificare il file XML della finestra di dialogo aggiuntivo per un&#39;applicazione nativa per i seguenti scopi:

* Per ignorare il file XML della finestra di dialogo per un&#39;applicazione con una risposta diversa
* Aggiunta di una risposta a una finestra di dialogo non indirizzata nel file XML della finestra di dialogo per l&#39;applicazione

Il nome del file che identifica un file DialogXML aggiuntivo è `appmon.[appname].addition.[locale].xml`. Un esempio è appmon.excel.addizione.en_US.xml.

Il nome del file XML della finestra di dialogo aggiuntiva deve utilizzare il formato `appmon.[applicationname].addition.[locale].xml`, dove *applicationname* deve corrispondere esattamente al nome dell&#39;applicazione utilizzato nel file di configurazione XML e nello script.

>[!NOTE]
>
>Nessuna delle applicazioni generiche specificate nel file di configurazione native2pdfconfig.xml dispone di un file XML della finestra di dialogo principale. La sezione [Aggiunta o modifica del supporto per un formato di file nativo](converting-file-formats-pdf.md#adding-or-modifying-support-for-a-native-file-format) descrive tali specifiche.

È necessario ordinare gli elementi `windowList` che vengono visualizzati come elementi secondari in un elemento `window`. (Vedere [Ordinamento degli elementi window e windowList](converting-file-formats-pdf.md#ordering-the-window-and-windowlist-elements).)

### Modifica del file XML della finestra di dialogo generale {#modifying-the-general-dialog-xml-file}

È possibile modificare il file XML della finestra di dialogo generale per rispondere alle finestre di dialogo generate dal sistema o per rispondere alle finestre di dialogo comuni a più applicazioni.

#### Aggiunta di una voce del tipo di file nel file di configurazione XML {#adding-a-filetype-entry-in-the-xml-configuration-file}

In questa procedura viene illustrato come aggiornare il file di configurazione del servizio Genera PDF per associare tipi di file alle applicazioni native. Per aggiornare questo file di configurazione, è necessario utilizzare la console di amministrazione per esportare i dati di configurazione in un file. Il nome file predefinito per i dati di configurazione è nativo2pdfconfig.xml.

**Aggiornamento del file di configurazione del servizio Genera PDF**

1. Selezionare **Home** > **Services** > **Adobe PDF Generator** > **File di configurazione**, quindi selezionare **Esporta configurazione**.
1. Modificate l&#39;elemento `filetype-settings` nel file nativo2pdfconfig.xml, in base alle esigenze.
1. Selezionare **Home** > **Services** > **Adobe PDF Generator** >**File di configurazione**, quindi selezionare **Importa configurazione**. I dati di configurazione vengono importati nel servizio Genera PDF, sostituendo le impostazioni precedenti.

>[!NOTE]
>
>Il nome dell&#39;applicazione è specificato come valore dell&#39;attributo `GenericApp` dell&#39;elemento `name`. Questo valore deve corrispondere esattamente al nome corrispondente specificato nello script sviluppato per quell&#39;applicazione. Analogamente, l&#39;attributo `GenericApp` dell&#39;elemento `displayName` deve corrispondere esattamente alla didascalia della finestra `expectedWindow` dello script corrispondente. Tale equivalenza viene valutata dopo la risoluzione di eventuali espressioni regolari visualizzate negli attributi `displayName` o `caption`.

In questo esempio, i dati di configurazione predefiniti forniti con il servizio Genera PDF sono stati modificati per specificare che Notepad (non Microsoft Word) deve essere utilizzato per elaborare i file con l&#39;estensione .txt. Prima di questa modifica, Microsoft Word veniva specificato come applicazione nativa che avrebbe dovuto elaborare tali file.

**Modifiche per reindirizzare i file di testo a Notepad (native2pdfconfig.xml)**

```xml
 <filetype-settings>

 <!-- Some native app file types were omitted for brevity. -->
 <!-- The following GenericApp element specifies Notepad as the native application that should be used to process files that have a txt file name extension. -->
             <GenericApp
                 extensions="txt"
                 name="Notepad" displayName=".*Notepad"/>
             <GenericApp
                 extensions="wpd"
                 name="WordPerfect" displayName="Corel WordPerfect"/>
             <GenericApp extensions="pmd,pm6,p65,pm"
                 name="PageMaker" displayName="Adobe PageMaker"/>
             <GenericApp extensions="fm"
                 name="FrameMaker" displayName="Adobe FrameMaker"/>
             <GenericApp extensions="psd"
                 name="Photoshop" displayName="Adobe Photoshop"/>
         </settings>
     </filetype-settings>
```

#### Creazione di una variabile di ambiente per individuare l&#39;applicazione nativa {#creating-an-environment-variable-to-locate-the-native-application}

Create una variabile di ambiente che specifica la posizione dell&#39;applicazione nativa eseguibile. La variabile deve utilizzare il formato `[applicationname]_PATH`, dove *applicationname* deve corrispondere esattamente al nome dell&#39;applicazione utilizzato nel file di configurazione XML e nello script, e dove il percorso contiene il percorso dell&#39;eseguibile tra virgolette doppie. Un esempio di tale variabile di ambiente è `Photoshop_PATH`.

Dopo aver creato la nuova variabile di ambiente, è necessario riavviare il server in cui è distribuito il servizio Genera PDF.

**Creare una variabile di sistema nell&#39;ambiente Windows XP**

1. Selezionare **Pannello di controllo Campaign > System**.
1. Nella finestra di dialogo Proprietà sistema, fare clic sulla scheda **Avanzate**, quindi fare clic su **Variabili di ambiente**.
1. In Variabili di sistema nella finestra di dialogo Variabili di ambiente, fare clic su **Nuovo**.
1. Nella finestra di dialogo Nuova variabile di sistema, digitare un nome che utilizza il formato `[applicationname]_PATH` nella casella **Nome variabile**.
1. Nella casella **Valore variabile** digitare il percorso completo e il nome del file eseguibile dell&#39;applicazione, quindi fare clic su **OK**. Ad esempio, digitare: `c:\windows\Notepad.exe`
1. Nella finestra di dialogo Variabili di ambiente, fare clic su **OK**.

**Creare una variabile di sistema dalla riga di comando**

1. Nella finestra della riga di comando, digitare la definizione della variabile utilizzando il seguente formato:

   ```shell
            [applicationname]_PATH=[Full path name]
   ```

   Ad esempio, digitare: `NotePad_PATH=C:\WINDOWS\NOTEPAD.EXE`

1. Avviate un nuovo prompt della riga di comando affinché la variabile di sistema abbia effetto.

#### File XML {#xml-files}

 AEM Forms include file XML di esempio che causano l&#39;utilizzo di Notepad da parte del servizio Genera PDF per l&#39;elaborazione di file con estensione .txt. Questo codice è incluso in questa sezione. Inoltre, è necessario apportare le altre modifiche descritte in questa sezione.

#### File XML della finestra di dialogo aggiuntivo {#additional-dialog-xml-file}

Questo esempio contiene le finestre di dialogo aggiuntive per l&#39;applicazione Notepad. Queste finestre di dialogo possono essere aggiunte a quelle specificate dal servizio Genera PDF.

**Finestra di dialogo Blocco note(appmon.blocco note.addizione.en_US.xml)**

```xml
 <dialogs app="Notepad" locale="en_US" version="7.0" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="dialogs.xsd">
     <window caption="Caption Title">
         <windowList>
             <window className="Button" caption="OK" action="press"/>
         </windowList>
     </window>
 </dialogs>
```

#### File XML di script {#script-xml-file}

Questo esempio specifica in che modo il servizio Genera PDF deve interagire con Notepad per stampare i file utilizzando la stampante Adobe PDF .

**File XML di script Notepad (appmon.blocco note.script.en_US.xml)**

```xml
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<!--
*
* ADOBE CONFIDENTIAL
* ___________________
* Copyright 2004 - 2005 Adobe Systems Incorporated
* All Rights Reserved.
*
* NOTICE:  All information contained herein is, and remains
* the property of Adobe Systems Incorporated and its suppliers,
* if any.  The intellectual and technical concepts contained
* herein are proprietary to Adobe Systems Incorporated and its
* suppliers and may be covered by U.S. and Foreign Patents,
* patents in process, and are protected by trade secret or copyright law.
* Dissemination of this information or reproduction of this material
* is strictly forbidden unless prior written permission is obtained
* from Adobe Systems Incorporated.
*-->

<!-- This file automates printing of text files via notepad to Adobe PDF printer. In order to see the complete hierarchy we recommend using the Microsoft Spy++ which details the properties of windows necessary to write scripts. In this sample there are total of eight steps-->

<application name="Notepad" version="9.0" locale="en_US" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="scripts.xsd">

    <!-- In this step we wait for the application window to appear -->
    <step>
        <expectedWindow>
            <window caption=".*Notepad"/>
        </expectedWindow>
    </step>

    <!-- In this step, we acquire the application window and send File->Open menu bar, menu item commands and the expectation is the windows Open dialog-->
    <step>
        <acquiredWindow>
            <window caption=".*Notepad">
                <virtualInput>
                    <menuBar>
                        <selection>
                            <name>File</name>
                        </selection>
                        <selection>
                            <name>Open...</name>
                        </selection>
                    </menuBar>
                </virtualInput>
            </window>
        </acquiredWindow>
        <expectedWindow>
            <window caption="Open"/>
        </expectedWindow>
    </step>

    <!-- In this step, we acquire the Open window and then select the 'Edit' widget and input the source path followed by clicking on the 'Open' button . The expectation of this 'action' is that the Open dialog will disappear -->
    <step>
        <acquiredWindow>
            <window caption="Open">
                <windowList>
                    <window className="ComboBoxEx32">
                        <windowList>
                            <window className="ComboBox">
                                <windowList>
                                <window className="Edit" action="inputSourcePath"/>
                                </windowList>
                            </window>
                        </windowList>
                    </window>
                </windowList>
                <windowList>
                    <window className="Button" caption="Open" action="press"/>
                </windowList>
            </window>
        </acquiredWindow>
        <expectedWindow>
            <window caption="Open" action="disappear"/>
        </expectedWindow>
        <pause value="30"/>
    </step>

    <!-- In this step, we acquire the application window and send File->Print menu bar, menu item commands and the expectation is the windows Print dialog-->
    <step>
        <acquiredWindow>
            <window caption=".*Notepad">
                <virtualInput>
                    <menuBar>
                        <selection>
                            <name>File</name>
                        </selection>
                        <selection>
                            <name>Print...</name>
                        </selection>
                    </menuBar>
                </virtualInput>
            </window>
        </acquiredWindow>
        <expectedWindow>
            <window caption="Print">
        </window>
        </expectedWindow>
    </step>

    <!-- In this step, we acquire the Print dialog and click on the 'Preferences' button and the expected window in this case is the dialog with the caption '"Printing Preferences' -->
    <step>
        <acquiredWindow>
            <window caption="Print">
                <windowList>
                    <window caption="General">
                        <windowList>
                            <window className="Button" caption="Preferences" action="press"/>
                        </windowList>
                    </window>
                </windowList>
            </window>
        </acquiredWindow>
        <expectedWindow>
            <window caption="Printing Preferences"/>
        </expectedWindow>
    </step>

    <!-- In this step, we acquire the dialog "Printing Preferences' and select the combo box which is the 10th child of window with caption '"Adobe PDF Settings' and select the first index. (Note: All indeces start with 0.) Besides this we uncheck the box which  has the caption '"View Adobe PDF results' and we click on the button OK. The expectation is that 'Printing Preferences' dialog disappears. -->
    <step>
        <acquiredWindow>
            <window caption="Printing Preferences">
                <windowList>
                    <window caption="Adobe PDF Settings">
                        <windowList>
                            <window className="Button" caption="View Adobe PDF results" action="uncheck"/>
                        </windowList>
                        <windowList>
                            <window className="Button" caption="Ask to Replace existing PDF file" action="uncheck"/>
                        </windowList>
                    </window>
                </windowList>
                <windowList>
                    <window className="Button" caption="OK" action="press"/>
                </windowList>
            </window>
        </acquiredWindow>
        <expectedWindow>
            <window caption="Printing Preferences" action="disappear"/>
        </expectedWindow>
    </step>

    <!-- In this step, we acquire the 'Print' dialog and click on the Print button. The expectation is that the dialog with caption 'Print' disappears. In this case we use the regular expression '^Print$' for specifying the caption given there could be multiple dialogs with caption that includes the word Print. -->
    <step>
        <acquiredWindow>
            <window caption="Print">
                <windowList>
                    <window caption="General"/>
                    <window className="Button" caption="^Print$" action="press"/>
                </windowList>
            </window>
        </acquiredWindow>
        <expectedWindow>
            <window caption="Print" action="disappear"/>
        </expectedWindow>
    </step>
    <step>
        <expectedWindow>
            <window caption="Save PDF File As"/>
        </expectedWindow>
    </step>
    <!-- Finally in this step, we acquire the dialog with caption "Save PDF File As" and in the Edit widget type the destination path for the output PDF file and click on the Save button. The expectation is that the dialog disappears-->
    <step>
        <acquiredWindow>
            <window caption="Save PDF File As">
                <windowList>
                    <window className="Edit" action="inputDestinationPath"/>
                </windowList>
                <windowList>
                    <window className="Button" caption="Save" action="press"/>
                </windowList>
            </window>
        </acquiredWindow>
        <expectedWindow>
            <window caption="Save PDF File As" action="disappear"/>
        </expectedWindow>
    </step>

    <!-- We can always set a retry count or a maximum time for a step. In case we surpass these limitations, PDF Generator generates this abort message and terminates processing. -->
    <abortMessage msg="15078"/>
</application>
```

