---
title: Conversione tra formati di file e PDF
seo-title: Converting Between File Formats and PDF
description: Utilizza il servizio Generate PDF per convertire i formati di file nativi in PDF. Il servizio Generate PDF converte inoltre PDF in altri formati di file e ottimizza le dimensioni dei documenti PDF.
seo-description: Use the Generate PDF service to convert native file formats to PDF. Generate PDF service also converts PDF to other file formats and optimizes the size of PDF documents.
uuid: f72ad603-c996-4d48-9bfc-bed7bf776af6
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 180cac3f-6378-42bc-9a47-60f9f08a7103
role: Developer
exl-id: 10535740-e3c2-4347-a88f-86706ad699b4
source-git-commit: 0c7dba43dad8608b4a5de271e1e44942c950fb16
workflow-type: tm+mt
source-wordcount: '7850'
ht-degree: 0%

---

# Conversione tra formati di file e PDF {#converting-between-file-formatsand-pdf}

**Gli esempi e gli esempi contenuti in questo documento sono solo per l’ambiente AEM Forms su JEE.**

**Informazioni sul servizio Genera PDF**

Il servizio Generate PDF converte i formati di file nativi in PDF. Converte inoltre PDF in altri formati di file e ottimizza le dimensioni dei documenti PDF.

Il servizio Generate PDF utilizza applicazioni native per convertire in PDF i seguenti formati di file. Salvo diversa indicazione, sono supportate solo le versioni in tedesco, francese, inglese e giapponese di queste applicazioni. *Solo Windows* indica il supporto solo per Windows Server® 2003 e Windows Server 2008.

* Microsoft Office 2003 e 2007 per convertire DOC, DOCX, RTF, TXT, XLS, XLSX, PPT, PPTX, VSD, MPP, MPPX, XPS e PUB (solo Windows)

>[!NOTE]
>
>Per convertire il formato Microsoft XPS in PDF è necessario Acrobat® 9.2 o versione successiva.

* Autodesk AutoCAD 2005, 2006, 2007, 2008 e 2009 per convertire DWF, DWG e DXW (solo in lingua inglese)
* Corel WordPerfect 12 e X4 per convertire WPD, QPW, SHW (solo in inglese)
* OpenOffice 2.0, 2.4, 3.0.1 e 3.1 per convertire ODT, ODS, ODP, ODG, ODF, SXW, SXI, SXC, SXD, DOC, DOCX, RTF, TXT, XLS, XLSX, PPT, PPTX, VSD, MPP, MPPX e PUB

>[!NOTE]
>
>Il servizio Generate PDF non supporta le versioni a 64 bit di OpenOffice.

* Adobe Photoshop® CS2 per convertire PSD (solo Windows)

>[!NOTE]
>
>Photoshop CS3 e CS4 non sono supportati perché non supportano Windows Server 2003 o Windows Server 2008.

* Adobe FrameMaker® 7.2 e 8 per convertire FM (solo Windows)
* PageMaker di Adobe ® 7.0 per convertire PMD, PM6, P65 e PM (solo Windows)
* Formati nativi supportati da applicazioni di terze parti (richiede lo sviluppo di file di installazione specifici per l&#39;applicazione) (solo Windows)

Il servizio Generate PDF converte in PDF i seguenti formati di file basati su standard.

* Formati video: SWF, FLV (solo Windows)
* Formati di immagini: JPEG, JPG, JP2, J2Kí, JPC, J2C, GIF, BMP, TIFF, TIF, PNG, JPF
* HTML (Windows, Sun™ Solaris™ e Linux®)

Il servizio Generate PDF converte PDF nei seguenti formati di file (solo Windows):

* PostScript incapsulato (EPS)
* HTML3.2
* HTML 4.01 con CSS 1.0
* DOC (formato Microsoft Word)
* RTF
* Testo (sia accessibile che normale)
* XML
* PDF/A-1a che utilizza solo lo spazio colore DeviceRGB
* PDF/A-1b che utilizza solo lo spazio colore DeviceRGB

Il servizio Genera PDF richiede l&#39;esecuzione dei seguenti task amministrativi:

* Installare le applicazioni native richieste nel computer che ospita AEM Forms
* Installare Adobe Acrobat Professional o Acrobat Pro Extended 9.2 sul computer che ospita AEM Forms
* Eseguire attività di installazione successive all&#39;installazione

Queste attività sono descritte in Installazione e distribuzione di moduli AEM tramite JBoss Turnkey.

Puoi eseguire queste attività utilizzando il servizio Genera PDF:

* Converti da formati di file nativi a PDF.
* Convertire documenti HTML in documenti PDF.
* Convertire documenti PDF in formati di file.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Generate PDF, consulta [Guida di riferimento dei servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Conversione di documenti Word in documenti PDF {#converting-word-documents-to-pdf-documents}

In questa sezione viene descritto come utilizzare l&#39;API Generate PDF per convertire in modo programmatico un documento di Microsoft Word in un documento di PDF.

>[!NOTE]
>
>Per ulteriori informazioni sui formati di file aggiuntivi, vedere [Aggiunta del supporto per formati di file nativi aggiuntivi](converting-file-formats-pdf.md#adding-support-for-additional-native-file-formats).

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Generate PDF, consulta [Guida di riferimento dei servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary-of-steps}

Per convertire un documento di Microsoft Word in un documento di PDF, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Crea un client Generate PDF.
1. Recuperare il file da convertire in un documento PDF.
1. Converte il file in un documento PDF.
1. Recupera i risultati.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

**Creare un client Generate PDF**

Prima di poter eseguire un&#39;operazione di generazione di PDF a livello di programmazione, creare un client di generazione di servizi di PDF. Se utilizzi l’API Java, crea un’ `GeneratePdfServiceClient` oggetto. Se utilizzi l’API del servizio web, crea un’ `GeneratePDFServiceService` oggetto.

**Recuperare il file da convertire in un documento PDF**

Recuperare il documento di Microsoft Word per convertirlo in un documento di PDF.

**Convertire il file in un documento PDF**

Dopo aver creato il client del servizio Generate PDF, è possibile richiamare `createPDF2` metodo. Questo metodo richiede informazioni sul documento da convertire, inclusa l&#39;estensione del file.

**Recuperare i risultati**

Dopo aver convertito il file in un documento PDF, è possibile recuperare i risultati. Dopo aver convertito un file di Word in un documento di PDF, ad esempio, è possibile recuperare e salvare il documento di PDF.

**Consulta anche**

[Convertire documenti Word in documenti PDF utilizzando l’API Java](converting-file-formats-pdf.md#convert-word-documents-to-pdf-documents-using-the-java-api)

[Convertire documenti di Word in documenti di PDF utilizzando l’API del servizio web](converting-file-formats-pdf.md#convert-word-documents-to-pdf-documents-using-the-web-service-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido di Generate PDF Service API](/help/forms/developing/generate-pdf-service-java-api.md#generate-pdf-service-java-api-quick-start-soap)

### Convertire documenti Word in documenti PDF utilizzando l’API Java {#convert-word-documents-to-pdf-documents-using-the-java-api}

Convertire un documento di Microsoft Word in un documento di PDF utilizzando l&#39;API Genera PDF (Java):

1. Includi file di progetto.

   Includi i file JAR client, ad esempio adobe-generatepdf-client.jar, nel percorso di classe del progetto Java.

1. Crea un client Generate PDF.

   * Creare un `ServiceClientFactory` oggetto che contiene proprietà di connessione.
   * Creare un `GeneratePdfServiceClient` mediante il costruttore e passando il `ServiceClientFactory` oggetto.

1. Recuperare il file da convertire in un documento PDF.

   * Creare un `java.io.FileInputStream` oggetto che rappresenta il file Word da convertire utilizzando il relativo costruttore. Passa un valore stringa che specifica la posizione del file.
   * Creare un `com.adobe.idp.Document` mediante il costruttore e passando il `java.io.FileInputStream` oggetto.

1. Converte il file in un documento PDF.

   Convertire il file in un documento PDF richiamando `GeneratePdfServiceClient` dell&#39;oggetto `createPDF2` e fornendo i seguenti valori:

   * A `com.adobe.idp.Document` oggetto che rappresenta il file da convertire.
   * A `java.lang.String` oggetto che contiene l&#39;estensione del file.
   * A `java.lang.String` oggetto contenente le impostazioni del tipo di file da utilizzare nella conversione. Le impostazioni del tipo di file forniscono impostazioni di conversione per diversi tipi di file, ad esempio doc o xls.
   * A `java.lang.String` oggetto contenente il nome delle impostazioni PDF da utilizzare. Ad esempio, puoi specificare `Standard`.
   * A `java.lang.String` oggetto contenente il nome delle impostazioni di protezione da utilizzare.
   * Un&#39;opzione `com.adobe.idp.Document` oggetto contenente le impostazioni da applicare durante la generazione del documento PDF.
   * Un&#39;opzione `com.adobe.idp.Document` oggetto contenente informazioni sui metadati da applicare al documento PDF.

   Il `createPDF2` il metodo restituisce un `CreatePDFResult` oggetto contenente il nuovo documento PDF e informazioni di registro. Il file di registro contiene in genere messaggi di errore o di avviso generati dalla richiesta di conversione.

1. Recupera i risultati.

   Per ottenere il documento PDF, effettuare le seguenti operazioni:

   * Richiama `CreatePDFResult` dell&#39;oggetto `getCreatedDocument` , che restituisce un `com.adobe.idp.Document` oggetto.
   * Richiama `com.adobe.idp.Document` dell&#39;oggetto `copyToFile` metodo per estrarre il documento PDF dall&#39;oggetto creato nel passaggio precedente.

   Se è stato utilizzato il `createPDF2` per ottenere il documento di registro (non applicabile alle conversioni HTML), eseguire le operazioni seguenti:

   * Richiama `CreatePDFResult` dell&#39;oggetto `getLogDocument` metodo. Questo restituisce un `com.adobe.idp.Document` oggetto.
   * Richiama `com.adobe.idp.Document` dell&#39;oggetto `copyToFile` per estrarre il documento di log.


**Consulta anche**

[Riepilogo dei passaggi](converting-file-formats-pdf.md#summary-of-steps)

[Guida rapida (modalità SOAP): conversione di un documento Microsoft Word in un documento PDF tramite l’API Java](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-a-microsoft-word-document-to-a-pdf-document-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Convertire documenti di Word in documenti di PDF utilizzando l’API del servizio web {#convert-word-documents-to-pdf-documents-using-the-web-service-api}

Convertire un documento di Microsoft Word in un documento di PDF utilizzando l’API Genera PDF (servizio web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/GeneratePDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l’indirizzo IP del server che ospita AEM Forms.

1. Crea un client Generate PDF.

   * Creare un `GeneratePDFServiceClient` utilizzando il costruttore predefinito.
   * Creare un `GeneratePDFServiceClient.Endpoint.Address` oggetto utilizzando `System.ServiceModel.EndpointAddress` costruttore. Passa un valore stringa che specifica il file WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/GeneratePDFService?blob=mtom`.) Non è necessario utilizzare il `lc_version` attributo. Tuttavia, specifica `?blob=mtom`.
   * Creare un `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto ottenendo il valore del `GeneratePDFServiceClient.Endpoint.Binding` campo. Invia il valore restituito a `BasicHttpBinding`.
   * Imposta il `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegna al campo il nome utente dei moduli AEM `GeneratePDFServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore password corrispondente al campo `GeneratePDFServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recuperare il file da convertire in un documento PDF.

   * Creare un `BLOB` mediante il costruttore. Il `BLOB` L&#39;oggetto viene utilizzato per memorizzare il file che si desidera convertire in un documento PDF.
   * Creare un `System.IO.FileStream` richiamando il relativo costruttore. Passa un valore stringa che rappresenta la posizione del file da convertire e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto della `System.IO.FileStream` oggetto. È possibile determinare le dimensioni della matrice di byte ottenendo `System.IO.FileStream` dell&#39;oggetto `Length` proprietà.
   * Compilare la matrice di byte con i dati di flusso richiamando `System.IO.FileStream` dell&#39;oggetto `Read` e passando la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare il `BLOB` oggetto assegnando al relativo `MTOM` proprietà il contenuto della matrice di byte.

1. Converte il file in un documento PDF.

   Convertire il file in un documento PDF richiamando `GeneratePDFServiceService` dell&#39;oggetto `CreatePDF2` e fornendo i seguenti valori:

   * A `BLOB` oggetto che rappresenta il file da convertire.
   * Stringa che contiene l’estensione del file.
   * A `java.lang.String` oggetto contenente le impostazioni del tipo di file da utilizzare nella conversione. Le impostazioni del tipo di file forniscono impostazioni di conversione per diversi tipi di file, ad esempio doc o xls.
   * Oggetto stringa contenente le impostazioni PDF da utilizzare. È possibile specificare `Standard`.
   * Oggetto stringa contenente le impostazioni di protezione da utilizzare. È possibile specificare `No Security`.
   * Un&#39;opzione `BLOB` oggetto contenente le impostazioni da applicare durante la generazione del documento PDF.
   * Un&#39;opzione `BLOB` oggetto contenente informazioni sui metadati da applicare al documento PDF.
   * Un parametro di output di tipo `BLOB` che viene compilato da `CreatePDF2` metodo. Il `CreatePDF2` Il metodo compila questo oggetto con il documento convertito. (Questo valore di parametro è richiesto solo per la chiamata del servizio Web).
   * Un parametro di output di tipo `BLOB` che viene compilato da `CreatePDF2` metodo. Il `CreatePDF2` il metodo compila questo oggetto con il documento di log. (Questo valore di parametro è richiesto solo per la chiamata del servizio Web).

1. Recupera i risultati.

   * Recuperare il documento PDF convertito assegnando il `BLOB` dell&#39;oggetto `MTOM` a una matrice di byte. La matrice di byte rappresenta il documento PDF convertito. Assicurati di utilizzare `BLOB` oggetto utilizzato come parametro di output per `createPDF2` metodo.
   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore stringa che rappresenta la posizione del file del documento PDF convertito.
   * Creare un `System.IO.BinaryWriter` oggetto richiamando il relativo costruttore e passando il `System.IO.FileStream` oggetto.
   * Scrivere il contenuto della matrice di byte in un file PDF richiamando `System.IO.BinaryWriter` dell&#39;oggetto `Write` e passando la matrice di byte.

**Consulta anche**

[Riepilogo dei passaggi](converting-file-formats-pdf.md#summary-of-steps)

[Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamare AEM Forms con SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Conversione di documenti HTML in documenti PDF {#converting-html-documents-to-pdf-documents}

Questa sezione descrive come utilizzare l’API Generate PDF per convertire in modo programmatico i documenti HTML in documenti PDF.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Generate PDF, consulta [Guida di riferimento dei servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-1}

Per convertire un documento HTML in un documento PDF, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Crea un client Generate PDF.
1. Recupera il contenuto HTML per convertirlo in un documento PDF.
1. Convertire il contenuto di HTML in un documento di PDF.
1. Recupera i risultati.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

**Creare un client Generate PDF**

Prima di poter eseguire un&#39;operazione di generazione di PDF a livello di programmazione, è necessario creare un client del servizio Generate PDF. Se utilizzi l’API Java, crea un’ `GeneratePdfServiceClient` oggetto. Se utilizzi l’API del servizio web, crea un’ `GeneratePDFServiceService`.

**Recuperare il contenuto HTML per la conversione in un documento PDF**

Fare riferimento al contenuto di HTML che si desidera convertire in un documento di PDF. Puoi fare riferimento a contenuto HTML, ad esempio un file HTML o a contenuto HTML, accessibile tramite un URL.

**Convertire il contenuto di HTML in un documento di PDF**

Dopo aver creato il client del servizio, è possibile richiamare l&#39;operazione di creazione PDF appropriata. Questa operazione richiede informazioni sul documento da convertire, incluso il percorso del documento di destinazione.

**Recuperare i risultati**

Dopo aver convertito il contenuto HTML in un documento PDF, puoi recuperare i risultati e salvare il documento PDF.

**Consulta anche**

[Convertire contenuti HTML in un documento PDF utilizzando l’API Java](converting-file-formats-pdf.md#convert-html-content-to-a-pdf-document-using-the-java-api)

[Convertire contenuti HTML in un documento PDF utilizzando l’API del servizio web](converting-file-formats-pdf.md#convert-html-content-to-a-pdf-document-using-the-web-service-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido di Generate PDF Service API](/help/forms/developing/generate-pdf-service-java-api.md#generate-pdf-service-java-api-quick-start-soap)

### Convertire contenuti HTML in un documento PDF utilizzando l’API Java {#convert-html-content-to-a-pdf-document-using-the-java-api}

Converti un documento HTML in un documento PDF utilizzando l’API Genera PDF (Java):

1. Includi file di progetto.

   Includi i file JAR client, ad esempio adobe-generatepdf-client.jar, nel percorso di classe del progetto Java.

1. Crea un client Generate PDF.

   Creare un `GeneratePdfServiceClient` oggetto utilizzando il relativo costruttore e passando un `ServiceClientFactory` oggetto che contiene proprietà di connessione.

1. Recupera il contenuto HTML per convertirlo in un documento PDF.

   Recupera il contenuto HTML creando una variabile stringa e assegnando un URL che punti al contenuto HTML.

1. Convertire il contenuto di HTML in un documento di PDF.

   Richiama `GeneratePdfServiceClient` dell&#39;oggetto `htmlToPDF2` e trasmettere i seguenti valori:

   * A `java.lang.String` oggetto che contiene l&#39;URL del file HTML da convertire.
   * A `java.lang.String` oggetto contenente le impostazioni del tipo di file da utilizzare nella conversione. Le impostazioni del tipo di file possono includere livelli di spider.
   * A `java.lang.String` oggetto contenente il nome delle impostazioni di protezione da utilizzare.
   * Un&#39;opzione `com.adobe.idp.Document` oggetto contenente le impostazioni da applicare durante la generazione del documento PDF. Se queste informazioni non vengono fornite, le impostazioni vengono scelte automaticamente in base ai tre parametri precedenti.
   * Un&#39;opzione `com.adobe.idp.Document` oggetto contenente informazioni sui metadati da applicare al documento PDF.

1. Recupera i risultati.

   Il `htmlToPDF2` il metodo restituisce un `HtmlToPdfResult` oggetto contenente il nuovo documento PDF generato. Per ottenere il documento di PDF appena creato, effettuare le seguenti operazioni:

   * Richiama `HtmlToPdfResult` dell&#39;oggetto `getCreatedDocument` metodo. Questo restituisce un `com.adobe.idp.Document` oggetto.
   * Richiama `com.adobe.idp.Document` dell&#39;oggetto `copyToFile` metodo per estrarre il documento PDF dall&#39;oggetto creato nel passaggio precedente.

**Consulta anche**

[Conversione di documenti HTML in documenti PDF](converting-file-formats-pdf.md#converting-html-documents-to-pdf-documents)

[Guida rapida (modalità SOAP): conversione di contenuti HTML in documenti PDF tramite l’API Java](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-html-content-to-a-pdf-document-using-the-java-api)

[Guida rapida (modalità SOAP): conversione di contenuti HTML in documenti PDF tramite l’API Java](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-html-content-to-a-pdf-document-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Convertire contenuti HTML in un documento PDF utilizzando l’API del servizio web {#convert-html-content-to-a-pdf-document-using-the-web-service-api}

Converti il contenuto di HTML in un documento di PDF utilizzando Genera API PDF (servizio web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/GeneratePDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l’indirizzo IP del server che ospita AEM Forms.

1. Crea un client Generate PDF.

   * Creare un `GeneratePDFServiceClient` utilizzando il costruttore predefinito.
   * Creare un `GeneratePDFServiceClient.Endpoint.Address` oggetto utilizzando `System.ServiceModel.EndpointAddress` costruttore. Passa un valore stringa che specifica il file WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/GeneratePDFService?blob=mtom`.) Non è necessario utilizzare il `lc_version` attributo. Tuttavia, specifica `?blob=mtom`.
   * Creare un `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto ottenendo il valore del `GeneratePDFServiceClient.Endpoint.Binding` campo. Invia il valore restituito a `BasicHttpBinding`.
   * Imposta il `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegna al campo il nome utente dei moduli AEM `GeneratePDFServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore password corrispondente al campo `GeneratePDFServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recupera il contenuto HTML per convertirlo in un documento PDF.

   Recupera il contenuto HTML creando una variabile stringa e assegnando un URL che punti al contenuto HTML.

1. Convertire il contenuto di HTML in un documento di PDF.

   Convertire il contenuto di HTML in un documento di PDF richiamando `GeneratePDFServiceService` dell&#39;oggetto `HtmlToPDF2` e trasmettere i seguenti valori:

   * Stringa contenente il contenuto HTML da convertire.
   * A `java.lang.String` oggetto contenente le impostazioni del tipo di file da utilizzare nella conversione.
   * Oggetto stringa contenente le impostazioni di protezione da utilizzare.
   * Un&#39;opzione `BLOB` oggetto contenente le impostazioni da applicare durante la generazione del documento PDF.
   * Un&#39;opzione `BLOB` oggetto contenente informazioni sui metadati da applicare al documento PDF.
   * Un parametro di output di tipo `BLOB` che viene compilato da `CreatePDF2` metodo. Il `CreatePDF2` Il metodo compila questo oggetto con il documento convertito. (Questo valore di parametro è richiesto solo per la chiamata del servizio Web).

1. Recupera i risultati.

   * Recuperare il documento PDF convertito assegnando il `BLOB` dell&#39;oggetto `MTOM` a una matrice di byte. La matrice di byte rappresenta il documento PDF convertito. Assicurati di utilizzare `BLOB` oggetto utilizzato come parametro di output per `HtmlToPDF2` metodo.
   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore stringa che rappresenta la posizione del file del documento PDF convertito.
   * Creare un `System.IO.BinaryWriter` oggetto richiamando il relativo costruttore e passando il `System.IO.FileStream` oggetto.
   * Scrivere il contenuto della matrice di byte in un file PDF richiamando `System.IO.BinaryWriter` dell&#39;oggetto `Write` e passando la matrice di byte.

**Consulta anche**

[Conversione di documenti HTML in documenti PDF](converting-file-formats-pdf.md#converting-html-documents-to-pdf-documents)

[Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamare AEM Forms con SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Conversione di documenti PDF in formati non immagine {#converting-pdf-documents-to-non-image-formats}

In questa sezione viene descritto come utilizzare l&#39;API di generazione Java PDF e l&#39;API di servizio Web per convertire in modo programmatico un documento PDF in un file RTF, ad esempio un formato non immagine. Altri formati non di immagine includono HTML, testo, DOC e EPS. Quando converti un documento PDF in RTF, accertati che il documento PDF non contenga elementi modulo, ad esempio un pulsante di invio. Gli elementi modulo non vengono convertiti.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Generate PDF, consulta [Guida di riferimento dei servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-2}

Per convertire un documento PDF in uno qualsiasi dei tipi supportati, effettuare le seguenti operazioni:

1. Includi file di progetto.
1. Crea un client Generate PDF.
1. Recuperare il documento PDF da convertire.
1. Convertire il documento PDF.
1. Salva il file convertito.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

**Creare un client Generate PDF**

Prima di poter eseguire un&#39;operazione di generazione di PDF a livello di programmazione, è necessario creare un client del servizio Generate PDF. Se utilizzi l’API Java, crea un’ `GeneratePdfServiceClient` oggetto. Se utilizzi l’API del servizio web, crea un’ `GeneratePDFServiceService` oggetto.

**Recupera il documento PDF da convertire**

Recuperate il documento PDF per convertirlo in un formato non immagine.

**Convertire il documento PDF**

Dopo aver creato il client del servizio, è possibile richiamare l&#39;operazione di esportazione PDF. Questa operazione richiede informazioni sul documento da convertire, incluso il percorso del documento di destinazione.

**Salva il file convertito**

Salva il file convertito. Se ad esempio si converte un documento PDF in un file RTF, salvare il documento convertito in un file RTF.

**Consulta anche**

[Convertire un documento PDF in un file RTF utilizzando l’API Java](converting-file-formats-pdf.md#convert-a-pdf-document-to-a-rtf-file-using-the-java-api)

[Convertire un documento PDF in un file RTF utilizzando l’API del servizio web](converting-file-formats-pdf.md#convert-a-pdf-document-to-a-rtf-file-using-the-web-service-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido di Generate PDF Service API](/help/forms/developing/generate-pdf-service-java-api.md#generate-pdf-service-java-api-quick-start-soap)

### Convertire un documento PDF in un file RTF utilizzando l’API Java {#convert-a-pdf-document-to-a-rtf-file-using-the-java-api}

Convertire un documento PDF in un file RTF utilizzando l&#39;API Generate PDF (Java):

1. Includi file di progetto.

   Includi i file JAR client, ad esempio adobe-generatepdf-client.jar, nel percorso di classe del progetto Java.

1. Crea un client Generate PDF.

   Creare un `GeneratePdfServiceClient` oggetto utilizzando il relativo costruttore e passando un `ServiceClientFactory` oggetto che contiene proprietà di connessione.

1. Recuperare il documento PDF da convertire.

   * Creare un `java.io.FileInputStream` oggetto che rappresenta il documento PDF da convertire utilizzando il relativo costruttore. Passa un valore stringa che specifica la posizione del documento PDF.
   * Creare un `com.adobe.idp.Document` mediante il costruttore e passando il `java.io.FileInputStream` oggetto.

1. Convertire il documento PDF.

   Richiama `GeneratePdfServiceClient` dell&#39;oggetto `exportPDF2` e trasmettere i seguenti valori:

   * A `com.adobe.idp.Document` oggetto che rappresenta il file PDF da convertire.
   * A `java.lang.String` oggetto contenente il nome del file da convertire.
   * A `java.lang.String` oggetto contenente il nome delle impostazioni di Adobe PDF.
   * A `ConvertPDFFormatType` oggetto che specifica il tipo di file di destinazione per la conversione.
   * Un&#39;opzione `com.adobe.idp.Document` oggetto contenente le impostazioni da applicare durante la generazione del documento PDF.

   Il `exportPDF2` il metodo restituisce un `ExportPDFResult` oggetto contenente il file convertito.

1. Convertire il documento PDF.

   Per ottenere il file appena creato, effettuare le seguenti operazioni:

   * Richiama `ExportPDFResult` dell&#39;oggetto `getConvertedDocument` metodo. Questo restituisce un `com.adobe.idp.Document` oggetto.
   * Richiama `com.adobe.idp.Document` dell&#39;oggetto `copyToFile` per estrarre il nuovo documento.

**Consulta anche**

[Riepilogo dei passaggi](converting-file-formats-pdf.md#summary-of-steps)

[Guida rapida (modalità SOAP): conversione di contenuti HTML in documenti PDF tramite l’API Java](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-html-content-to-a-pdf-document-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Convertire un documento PDF in un file RTF utilizzando l’API del servizio web {#convert-a-pdf-document-to-a-rtf-file-using-the-web-service-api}

Converti un documento PDF in un file RTF utilizzando l’API Genera PDF (servizio web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/GeneratePDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l’indirizzo IP del server che ospita AEM Forms.

1. Creare un client Generate PDf.

   * Creare un `GeneratePDFServiceClient` utilizzando il costruttore predefinito.
   * Creare un `GeneratePDFServiceClient.Endpoint.Address` oggetto utilizzando `System.ServiceModel.EndpointAddress` costruttore. Passa un valore stringa che specifica il file WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/GeneratePDFService?blob=mtom`.) Non è necessario utilizzare il `lc_version` attributo. Tuttavia, specifica `?blob=mtom`.
   * Creare un `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto ottenendo il valore del `GeneratePDFServiceClient.Endpoint.Binding` campo. Invia il valore restituito a `BasicHttpBinding`.
   * Imposta il `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegna al campo il nome utente dei moduli AEM `GeneratePDFServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore password corrispondente al campo `GeneratePDFServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recuperare il documento PDF da convertire.

   * Creare un `BLOB` mediante il costruttore. Il `BLOB` L&#39;oggetto viene utilizzato per memorizzare un documento PDF convertito.
   * Creare un `System.IO.FileStream` dell&#39;oggetto richiamando il relativo costruttore e passando un valore stringa che rappresenta la posizione del file del documento PDF e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto della `System.IO.FileStream` oggetto. È possibile determinare le dimensioni della matrice di byte ottenendo `System.IO.FileStream` dell&#39;oggetto `Length` proprietà.
   * Compilare la matrice di byte con i dati di flusso richiamando `System.IO.FileStream` dell&#39;oggetto `Read` e passando la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare il `BLOB` oggetto assegnando al relativo `MTOM` proprietà il contenuto della matrice di byte.

1. Convertire il documento PDF.

   Richiama `GeneratePDFServiceServiceWse` dell&#39;oggetto `ExportPDF2` e trasmettere i seguenti valori:

   * A `BLOB` oggetto che rappresenta il file PDF da convertire.
   * Stringa che contiene il percorso del file da convertire.
   * A `java.lang.String` oggetto che specifica la posizione del file.
   * Oggetto string che specifica il tipo di file di destinazione per la conversione. Specifica `RTF`.
   * Un&#39;opzione `BLOB` oggetto contenente le impostazioni da applicare durante la generazione del documento PDF.
   * Un parametro di output di tipo `BLOB` che viene compilato da `ExportPDF2` metodo. Il `ExportPDF2` Il metodo compila questo oggetto con il documento convertito. (Questo valore di parametro è richiesto solo per la chiamata del servizio Web).

1. Salva il file convertito.

   * Recuperare il documento RTF convertito assegnando il `BLOB` dell&#39;oggetto `MTOM` a una matrice di byte. La matrice di byte rappresenta il documento RTF convertito. Assicurati di utilizzare `BLOB` oggetto utilizzato come parametro di output per `ExportPDF2` metodo.
   * Creare un `System.IO.FileStream` richiamando il relativo costruttore. Passa un valore stringa che rappresenta la posizione del file RTF.
   * Creare un `System.IO.BinaryWriter` oggetto richiamando il relativo costruttore e passando il `System.IO.FileStream` oggetto.
   * Scrivere il contenuto della matrice di byte in un file RTF richiamando `System.IO.BinaryWriter` dell&#39;oggetto `Write` e passando la matrice di byte.

**Consulta anche**

[Riepilogo dei passaggi](converting-file-formats-pdf.md#summary-of-steps)

[Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamare AEM Forms con SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Aggiunta del supporto per formati di file nativi aggiuntivi {#adding-support-for-additional-native-file-formats}

Questa sezione spiega come aggiungere il supporto per ulteriori formati di file nativi. Fornisce una panoramica delle interazioni tra il servizio Generate PDF e le applicazioni native utilizzate da questo servizio per convertire i formati di file nativi in PDF.

Questa sezione spiega anche quanto segue:

* Come modificare la risposta fornita dal servizio Generate PDF alle applicazioni native già utilizzate da questo prodotto per convertire i formati di file nativi in PDF
* Interazioni tra il servizio Generate PDF, il componente Generate PDF Service Application Monitor (AppMon) e le applicazioni native, ad esempio Microsoft Word
* Ruoli svolti dalle grammatiche XML in tali interazioni

### Interazioni dei componenti {#component-interactions}

Il servizio Generate PDF converte i formati di file nativi richiamando l&#39;applicazione associata al formato di file e interagendo con l&#39;applicazione per stampare il documento utilizzando la stampante predefinita. La stampante predefinita deve essere impostata come stampante Adobe PDF.

Questa illustrazione mostra i componenti e i driver coinvolti nel supporto nativo delle applicazioni. Vengono inoltre menzionate le grammatiche XML che influenzano le interazioni.

Interazioni dei componenti per la conversione di file nativi

Questo documento utilizza il termine *applicazione nativa* per indicare l&#39;applicazione utilizzata per produrre un formato di file nativo, ad esempio Microsoft Word.

*AppMon* è un componente enterprise che interagisce con un’applicazione nativa nello stesso modo in cui un utente naviga attraverso le finestre di dialogo presentate da tale applicazione. Le grammatiche XML utilizzate da AppMon per istruire un&#39;applicazione, ad esempio Microsoft Word, ad aprire e stampare un file implicano le seguenti attività sequenziali:

1. Aprire il file selezionando File > Apri
1. Verificare che venga visualizzata la finestra di dialogo Apri; in caso contrario, gestire l&#39;errore
1. Specificare il nome del file nel campo Nome file, quindi fare clic sul pulsante Apri
1. Verifica dell&#39;effettiva apertura del file
1. Aprire la finestra di dialogo Stampa selezionando File > Stampa
1. Assicurarsi che venga visualizzata la finestra di dialogo Stampa

AppMon utilizza le API Win32 standard per interagire con applicazioni di terze parti al fine di trasferire eventi dell’interfaccia utente come colpi di tasto e clic del mouse, utili per controllare queste applicazioni per produrre file PDF da esse.

A causa di una limitazione con queste API Win32, AppMon non è in grado di inviare questi eventi dell&#39;interfaccia utente ad alcuni tipi specifici di finestre, come le barre dei menu mobili (presenti in alcune applicazioni come TextPad) e alcuni tipi di finestre di dialogo il cui contenuto non può essere recuperato utilizzando le API Win32.

È facile identificare visivamente una barra dei menu mobile; tuttavia, potrebbe non essere possibile identificare i tipi speciali di finestre di dialogo solo tramite ispezione visiva. È necessaria un&#39;applicazione di terze parti come Microsoft Spy++ (parte dell&#39;ambiente di sviluppo Microsoft Visual C++) o il relativo WinID equivalente (scaricabile gratuitamente da [https://www.dennisbabkin.com/php/download.php?what=WinID](https://www.dennisbabkin.com/php/download.php?what=WinID)) per esaminare una finestra di dialogo per determinare se AppMon sarebbe in grado di interagire con essa utilizzando API Win32 standard.

Se WinID è in grado di estrarre il contenuto della finestra di dialogo, ad esempio il testo, le finestre secondarie, l&#39;ID della classe della finestra e così via, AppMon sarà in grado di fare lo stesso.

In questa tabella sono elencati i tipi di informazioni utilizzati per la stampa dei formati di file nativi.

<table>
 <thead>
  <tr>
   <th><p>Tipo di informazioni</p></th>
   <th><p>Descrizione</p></th>
   <th><p>Modifica/creazione di voci correlate a file nativi </p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>Impostazioni amministrative </p></td>
   <td><p>Include le impostazioni di PDF, di protezione e di tipo di file. </p><p>Le impostazioni del tipo di file associano le estensioni dei nomi di file alle applicazioni native corrispondenti. Le impostazioni del tipo di file specificano inoltre le impostazioni dell'applicazione nativa utilizzate per stampare i file nativi. </p></td>
   <td><p>Per modificare le impostazioni per un'applicazione nativa già supportata, l'amministratore di sistema imposta le impostazioni del tipo di file nella console di amministrazione. </p><p>Per aggiungere il supporto per un nuovo formato di file nativo, è necessario modificare manualmente il file. (vedere <a href="converting-file-formats-pdf.md#adding-or-modifying-support-for-a-native-file-format">Aggiunta o modifica del supporto per un formato di file nativo</a>.) </p></td>
  </tr>
  <tr>
   <td><p>Script </p></td>
   <td><p>Specifica le interazioni tra il servizio Generate PDF e un'applicazione nativa. Tali interazioni in genere indirizzano l’applicazione a stampare un file sul driver di Adobe PDF. </p><p>Lo script contiene istruzioni che indirizzano l'applicazione nativa ad aprire finestre di dialogo specifiche e che forniscono risposte specifiche ai campi e ai pulsanti presenti in tali finestre di dialogo. </p></td>
   <td><p>Il servizio Generate PDF include file di script per tutte le applicazioni native supportate. È possibile modificare questi file utilizzando un'applicazione di modifica XML.</p><p>Per aggiungere il supporto per una nuova applicazione nativa, è necessario creare un nuovo file di script. (vedere <a href="converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application">Creazione o modifica di un ulteriore file XML di finestra di dialogo per un'applicazione nativa</a>.) </p></td>
  </tr>
  <tr>
   <td><p>Istruzioni generiche della finestra di dialogo </p></td>
   <td><p>Specifica come rispondere alle finestre di dialogo comuni a più applicazioni. Tali finestre di dialogo sono generate da sistemi operativi, applicazioni di supporto (come PDFMaker) e driver. </p><p>Il file che contiene queste informazioni è appmon.global.en_US.xml.</p></td>
   <td><p>Non modificare questo file. </p></td>
  </tr>
  <tr>
   <td><p>Istruzioni della finestra di dialogo specifiche dell'applicazione</p></td>
   <td><p>Specifica come rispondere alle finestre di dialogo specifiche dell'applicazione. </p><p>Il file che contiene queste informazioni è valido.<i>`[appname]`</i>.dialogo.<i>`[locale]`</i>.xml (ad esempio appmon.word.en_US.xml).</p></td>
   <td><p>Non modificare questo file. </p><p>Per aggiungere istruzioni di dialogo per una nuova applicazione nativa, vedere <a href="converting-file-formats-pdf.md#creating_or_modifying_an_additional_dialog_xml_file_for_a_native_application">Creazione o modifica di un ulteriore file XML di finestra di dialogo per un'applicazione nativa</a>.</p></td>
  </tr>
  <tr>
   <td><p>Istruzioni aggiuntive della finestra di dialogo specifiche per l'applicazione </p></td>
   <td><p>Specifica le sostituzioni e le aggiunte alle istruzioni della finestra di dialogo specifiche dell'applicazione. La sezione presenta un esempio di tali informazioni. </p><p>Il file che contiene queste informazioni è valido.<i>`[appname]`</i>.aggiunta.<i>`[locale]`</i>.xml. Un esempio è appmon.add.en_US.xml.</p></td>
   <td><p>È possibile creare e modificare file di questo tipo utilizzando un'applicazione di modifica XML. (vedere <a href="converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application">Creazione o modifica di un ulteriore file XML di finestra di dialogo per un'applicazione nativa</a>.) </p><p><strong>Importante</strong>: è necessario creare istruzioni aggiuntive della finestra di dialogo specifiche per l'applicazione per ogni applicazione nativa supportata dal server. </p></td>
  </tr>
 </tbody>
</table>

### Informazioni sui file XML dello script e della finestra di dialogo {#about-the-script-and-dialog-xml-files}

I file XML di script indirizzano il servizio Generate PDF a spostarsi tra le finestre di dialogo dell&#39;applicazione nello stesso modo in cui l&#39;utente passa attraverso le finestre di dialogo dell&#39;applicazione. I file XML di script indicano inoltre al servizio Generate PDF di rispondere alle finestre di dialogo eseguendo azioni quali la pressione dei pulsanti, la selezione o deselezione delle caselle di controllo o la selezione delle voci di menu.

Al contrario, i file XML delle finestre di dialogo rispondono semplicemente alle finestre di dialogo con gli stessi tipi di azioni utilizzate nei file XML degli script.

#### Terminologia della finestra di dialogo e degli elementi della finestra {#dialog-box-and-window-element-terminology}

Questa sezione e quella successiva utilizzano una terminologia diversa per le finestre di dialogo e per i componenti in esse contenuti, a seconda della prospettiva descritta. I componenti della finestra di dialogo sono elementi quali pulsanti, campi e caselle combinate.

Quando questa sezione e quella successiva descrivono le finestre di dialogo e i relativi componenti dal punto di vista di un utente, termini quali *finestra di dialogo*, *pulsante*, *campo*, e *casella combinata* vengono utilizzati.

Quando questa sezione e quella successiva descrivono le finestre di dialogo e i relativi componenti dal punto di vista della rappresentazione interna, il termine *elemento finestra* viene utilizzato. La rappresentazione interna degli elementi di finestra è una gerarchia, in cui ogni istanza di elemento di finestra è identificata da etichette. L&#39;istanza dell&#39;elemento window ne descrive anche le caratteristiche fisiche e il comportamento.

Dal punto di vista di un utente, le finestre di dialogo e i relativi componenti mostrano comportamenti diversi, in cui alcuni elementi della finestra di dialogo vengono nascosti fino all&#39;attivazione. Dal punto di vista della rappresentazione interna, non esiste un tale problema di comportamento. Ad esempio, la rappresentazione interna di una finestra di dialogo è simile a quella dei componenti in essa contenuti, con l&#39;eccezione che i componenti sono nidificati all&#39;interno della finestra di dialogo.

Questa sezione descrive gli elementi XML che forniscono istruzioni ad AppMon. Questi elementi hanno nomi come `dialog` e `window` elemento. In questo documento viene utilizzato un carattere a spaziatura fissa per distinguere gli elementi XML. Il `dialog` L&#39;elemento identifica una finestra di dialogo che un file di script XML può causare, intenzionalmente o meno. Il `window` L&#39;elemento identifica un elemento finestra (finestra di dialogo o i componenti di una finestra di dialogo).

#### Gerarchia {#hierarchy}

In questo diagramma viene illustrata la gerarchia di script e finestra di dialogo XML. Un file XML di script è conforme allo schema script.xsd, che include (nel senso XML) lo schema window.xsd. Analogamente, un file XML della finestra di dialogo è conforme allo schema dialogs.xsd, che include anche lo schema window.xsd.

![as_as_xml_hierarchy](assets/as_as_xml_hierarchy.png)

Gerarchia di script e finestra di dialogo XML

#### File XML di script {#script-xml-files}

A *file XML script* specifica una serie di passaggi che indirizzano l&#39;applicazione nativa a passare a determinati elementi della finestra e quindi a fornire le risposte a tali elementi. La maggior parte delle risposte è costituita da testo o sequenze di tasti corrispondenti all&#39;input che l&#39;utente fornirebbe a un campo, una casella combinata o un pulsante nella finestra di dialogo corrispondente.

Lo scopo del supporto del servizio Generate PDF per i file XML di script è quello di indirizzare un’applicazione nativa a stampare un file nativo. Tuttavia, i file XML di script possono essere utilizzati per eseguire qualsiasi operazione che un utente può eseguire quando interagisce con le finestre di dialogo dell&#39;applicazione nativa.

I passaggi in un file XML di script vengono eseguiti in ordine, senza alcuna opportunità di diramazione. L’unico test condizionale supportato è timeout/nuovo tentativo, che causa la chiusura di uno script se un passaggio non viene completato correttamente entro un periodo di tempo specifico e dopo un numero specifico di tentativi.

Oltre che sequenziali, le istruzioni di un passaggio vengono eseguite in ordine. È necessario assicurarsi che i passaggi e le istruzioni riflettano l’ordine in cui un utente eseguirebbe gli stessi passaggi.

Ogni passaggio in un file XML di script identifica l&#39;elemento della finestra che dovrebbe essere visualizzato se le istruzioni del passaggio vengono eseguite correttamente. Se durante l&#39;esecuzione di un passaggio di script viene visualizzata una finestra di dialogo imprevista, il servizio Generate PDF esegue la ricerca nei file XML della finestra di dialogo come descritto nella sezione successiva.

#### File XML finestra di dialogo {#dialog-xml-files}

L&#39;esecuzione di applicazioni native visualizza diverse finestre di dialogo, che vengono visualizzate indipendentemente dal fatto che le applicazioni native siano in modalità visibile o invisibile. Le finestre di dialogo possono essere generate dal sistema operativo o dall&#39;applicazione stessa. Quando le applicazioni native vengono eseguite sotto il controllo del servizio Genera PDF, le finestre di dialogo del sistema e dell&#39;applicazione nativa vengono visualizzate in una finestra invisibile.

A *finestra di dialogo File XML* specifica la modalità di risposta del servizio Generate PDF alle finestre di dialogo di sistema o dell&#39;applicazione nativa. I file XML delle finestre di dialogo consentono al servizio Generate PDF di rispondere alle finestre di dialogo non visualizzate in modo da facilitare il processo di conversione.

Quando il sistema o l&#39;applicazione nativa visualizza una finestra di dialogo non gestita dal file XML di script in esecuzione, il servizio Generate PDF esegue la ricerca nei file XML di dialogo in questo ordine, interrompendo la ricerca quando viene trovata una corrispondenza:

* appmon.`[appname]`.aggiuntivo.`[locale]`.xml
* appmon.`[appname]`.`[locale]`.xml (non modificare il file).
* appmon.global.`[locale]`.xml (non modificare il file).

Se il servizio Generate PDF trova una corrispondenza per la finestra di dialogo, la ignora inviando la sequenza di tasti o un&#39;altra azione specificata per la finestra di dialogo. Se nelle istruzioni della finestra di dialogo viene specificato un messaggio di interruzione, il servizio Generate PDF interrompe il processo in esecuzione e genera un messaggio di errore. Tale messaggio di interruzione verrebbe specificato nel `abortMessage` nella grammatica XML dello script.

Se il servizio Generate PDF rileva una finestra di dialogo non descritta in nessuno dei file elencati in precedenza, il servizio Generate PDF incorpora la didascalia della finestra di dialogo nella voce del file di log. Alla fine il processo in esecuzione si interrompe. È quindi possibile utilizzare le informazioni contenute nel file di log per comporre nuove istruzioni nel file XML della finestra di dialogo aggiuntiva per l&#39;applicazione nativa.

### Aggiunta o modifica del supporto per un formato di file nativo {#adding-or-modifying-support-for-a-native-file-format}

In questa sezione vengono descritte le attività da eseguire per supportare altri formati di file nativi o per modificare il supporto di un formato di file nativo già supportato.

Prima di aggiungere o modificare il supporto, è necessario completare le attività seguenti.

#### Scelta di uno strumento per identificare gli elementi della finestra {#choosing-a-tool-for-identifying-window-elements}

I file XML di dialogo e di script richiedono l&#39;identificazione dell&#39;elemento finestra (finestra di dialogo, campo o altro componente finestra di dialogo) al quale risponde la finestra di dialogo o l&#39;elemento script. Ad esempio, dopo che uno script richiama un menu per un&#39;applicazione nativa, lo script deve identificare l&#39;elemento finestra del menu a cui devono essere applicate le pressioni dei tasti o un&#39;azione.

È possibile identificare facilmente una finestra di dialogo in base alla didascalia visualizzata nella barra del titolo. Tuttavia, devi utilizzare uno strumento come Microsoft Spy++ per identificare gli elementi della finestra di livello inferiore. Gli elementi della finestra di livello inferiore possono essere identificati tramite una varietà di attributi, che non sono evidenti. Inoltre, ogni applicazione nativa può identificare il proprio elemento finestra in modo diverso. Di conseguenza, esistono diversi modi per identificare un elemento della finestra. Di seguito è riportato l’ordine suggerito per considerare l’identificazione degli elementi finestra:

1. Didascalia stessa se è univoca
1. ID di controllo, che può essere o meno univoco per una determinata finestra di dialogo
1. Nome della classe, che può essere o meno univoco

Per identificare una finestra è possibile utilizzare uno o una combinazione di questi tre attributi.

Se gli attributi non identificano una didascalia, è possibile identificare un elemento finestra utilizzando il relativo indice rispetto al relativo elemento padre. Un *index* specifica la posizione dell&#39;elemento window rispetto agli elementi della finestra di pari livello. Spesso, gli indici sono l’unico modo per identificare le caselle combinate.

Presta attenzione a questi problemi:

* Microsoft Spy++ visualizza i sottotitoli utilizzando una e commerciale (&amp;) per identificare il tasto di scelta rapida della didascalia. Ad esempio, Spy++ mostra la didascalia di una finestra di dialogo Stampa come `Pri&nt`, che indica che la scelta rapida è *n*. I titoli dei sottotitoli nei file XML di script e di dialogo devono omettere la e commerciale.
* Alcuni sottotitoli includono interruzioni di riga. il servizio Generate PDF non è in grado di identificare le interruzioni di riga. Se una didascalia include un&#39;interruzione di riga, includerne una quantità sufficiente per differenziarla dalle altre voci di menu e quindi utilizzare espressioni regolari per la parte omessa. Un esempio è ( `^Long caption title$`). (vedere [Utilizzo di espressioni regolari negli attributi delle didascalie](converting-file-formats-pdf.md#using-regular-expressions-in-caption-attributes).)
* Utilizzare le entità carattere (dette anche sequenze di escape) per i caratteri XML riservati. Ad esempio, utilizza `&` e commerciale, `<` e `>` per simboli minori e maggiori di, `&apos;` per gli apostrofi, e `&quot;` tra virgolette.

Se si prevede di lavorare su file XML di dialogo o script, è necessario installare l&#39;applicazione Microsoft Spy++.

#### Decompressione dei file di dialogo e di script {#unpackaging-the-dialog-and-script-files}

I file di dialogo e script risiedono nel file appmondata.jar. Prima di poter modificare uno di questi file o aggiungere nuovi file script o di dialogo, è necessario decomprimere il file JAR. Si supponga, ad esempio, di voler aggiungere il supporto per l&#39;applicazione EditPlus. Vengono creati due file XML, denominati appmon.editplus.script.en_US.xml e appmon.editplus.script.add.en_US.xml. Questi script XML devono essere aggiunti al file adobe-appmondata.jar in due posizioni, come specificato di seguito:

* adobe-livecycle-native-jboss-x86_win32.ear > adobe-Native2PDFSvc.war\WEB-INF\lib > adobe-native.jar > Native2PDFSvc-native.jar\bin > adobe-appmondata.jar\com\adobe\appmon. Il file adobe-livecycle-native-jboss-x86_win32.ear si trova nella cartella di esportazione all&#39;indirizzo `[AEM forms install directory]\configurationManager`. Se AEM Forms viene distribuito su un altro server applicazioni J2EE, sostituire il file adobe-livecycle-native-jboss-x86_win32.ear con il file EAR corrispondente al server applicazioni J2EE.
* adobe-generatepdf-dsc.jar > adobe-appmondata.jar\com\adobe\appmon (il file adobe-appmondata.jar si trova all’interno del file adobe-generatepdf-dsc.jar). Il file adobe-generatepdf-dsc.jar si trova in `[AEM forms install directory]\deploy` cartella.

Dopo aver aggiunto questi file XML al file adobe-appmondata.jar, è necessario ridistribuire il componente GeneratePDF. Per aggiungere file di dialogo e script XML al file adobe-appmondata.jar, eseguire le operazioni seguenti:

1. Utilizzando uno strumento come WinZip o WinRAR, apri il file adobe-livecycle-native-jboss-x86_win32.earfile > adobe-Native2PDFSvc.war\WEB-INF\lib > adobe-native.jar > Native2PDFSvc-native.jar\bin > adobe-appmondata.jar.
1. Aggiungi i file XML di dialogo e script al file appmondata.jar o modifica i file XML esistenti in questo file. (vedere [Creazione o modifica di un file XML di script per un&#39;applicazione nativa](converting-file-formats-pdf.md#creating-or-modifying-a-script-xml-file-for-a-native-application)e [Creazione o modifica di un ulteriore file XML di finestra di dialogo per un&#39;applicazione nativa](converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application).)
1. Utilizzando uno strumento come WinZip o WinRAR, apri adobe-generatepdf-dsc.jar > adobe-appmondata.jar.
1. Aggiungi i file XML di dialogo e script al file appmondata.jar o modifica i file XML esistenti in questo file. (vedere [Creazione o modifica di un file XML di script per un&#39;applicazione nativa](converting-file-formats-pdf.md#creating-or-modifying-a-script-xml-file-for-a-native-application)e [Creazione o modifica di un ulteriore file XML di finestra di dialogo per un&#39;applicazione nativa](converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application).) Dopo aver aggiunto i file XML al file adobe-appmondata.jar, inserire il nuovo file adobe-appmondata.jar nel file adobe-generatepdf-dsc.jar.
1. Se è stato aggiunto il supporto per un formato di file nativo aggiuntivo, creare una variabile di ambiente di sistema che fornisca il percorso dell&#39;applicazione (vedere [Creazione di una variabile di ambiente per individuare l&#39;applicazione nativa](converting-file-formats-pdf.md#creating-an-environment-variable-to-locate-the-native-application).)

**Per ridistribuire il componente GeneratePDF**

1. Accedi a Workbench.
1. Seleziona **Finestra** > **Mostra visualizzazioni** > **Componenti**. Questa azione aggiunge la vista Componenti a Workbench.
1. Fai clic con il pulsante destro del mouse sul componente Genera PDF, quindi seleziona **Interrompi componente**.
1. Una volta arrestato il componente, fare clic con il pulsante destro del mouse e selezionare Disinstalla componente per rimuoverlo.
1. Fare clic con il pulsante destro del mouse **Componenti** e seleziona **Installa componente**.
1. Individua e seleziona il file adobe-generatepdf-dsc.jar modificato e fai clic su Apri. Accanto al componente GeneratePDF viene visualizzato un quadratino rosso.
1. Espandere il componente GeneratePDF, selezionare Service Descriptors, quindi fare clic con il pulsante destro del mouse su GeneratePDFService e selezionare Activate Service.
1. Nella finestra di dialogo di configurazione visualizzata, immettete i valori di configurazione applicabili. Se non si specifica alcun valore, vengono utilizzati i valori di configurazione predefiniti.
1. Fai clic con il pulsante destro del mouse su Genera PDF e seleziona Avvia componente.
1. Espandere Servizi attivi. Accanto al nome del servizio, se in esecuzione, viene visualizzata una freccia verde. In caso contrario, il servizio è in stato di arresto.
1. Se il servizio è in stato di arresto, fare clic con il pulsante destro del mouse sul nome del servizio e selezionare Avvia servizio.

### Creazione o modifica di un file XML di script per un&#39;applicazione nativa {#creating-or-modifying-a-script-xml-file-for-a-native-application}

Se si desidera indirizzare i file a una nuova applicazione nativa, è necessario creare un file XML di script per tale applicazione. Se si desidera modificare il modo in cui il servizio Generate PDF interagisce con un&#39;applicazione nativa già supportata, è necessario modificare lo script per tale applicazione.

Lo script contiene istruzioni che consentono di spostarsi tra gli elementi della finestra dell’applicazione nativa e che forniscono risposte specifiche a tali elementi. Il file che contiene queste informazioni è `appmon.`[appname]&quot; `.script.`[lingua]`.xml`. Un esempio è appmon.notepad.script.en_US.xml.

#### Identificazione dei passaggi che lo script deve eseguire {#identifying-steps-the-script-must-execute}

Utilizzando l&#39;applicazione nativa, determinare gli elementi della finestra che è necessario esplorare e ogni risposta da eseguire per stampare il documento. Osserva le finestre di dialogo risultanti da qualsiasi risposta. I passaggi saranno simili ai seguenti:

1. Selezionate File > Apri (Open).
1. Specificare il percorso e fare clic su Apri.
1. Selezionare File > Stampa sulla barra dei menu.
1. Specificare le proprietà richieste per la stampante.
1. Selezionare Stampa e attendere la visualizzazione della finestra di dialogo Salva con nome. La finestra di dialogo Salva con nome è necessaria affinché il servizio Genera PDF specifichi la destinazione del file PDF.

#### Identificazione delle finestre di dialogo specificate negli attributi dei sottotitoli {#identifying-the-dialogs-specified-in-caption-attributes}

Utilizza Microsoft Spy++ per ottenere le identità delle proprietà degli elementi finestra nell’applicazione nativa. Per scrivere gli script è necessario disporre di queste identità.

#### Utilizzo di espressioni regolari negli attributi delle didascalie {#using-regular-expressions-in-caption-attributes}

È possibile utilizzare espressioni regolari nelle specifiche dei sottotitoli. Il servizio Generate PDF utilizza `java.util.regex.Matcher` classe per supportare espressioni regolari. Tale utility supporta le espressioni regolari descritte in `java.util.regex.Pattern`.

**Espressione regolare che include il nome file aggiunto al Blocco note nel banner Blocco note**

```xml
 <!-- The regular expression ".*Notepad" means any number of non-terminating characters followed by Notepad. -->
 <step>
     <expectedWindow>
         <window caption=".*Notepad"/>
     </expectedWindow>
 </step>
```

**Espressione regolare che differenzia Stampa da Imposta stampante**

```xml
 <!-- This regular expression differentiates the Print dialog box from the Print Setup dialog box. The "^" specifies the beginning of the line, and the "$" specifies the end of the line. -->
 <windowList>
     <window controlID="0x01" caption="^Print$" action="press"/>
 </windowList>
```

#### Ordinamento degli elementi window e windowList {#ordering-the-window-and-windowlist-elements}

Devi ordinare `window` e `windowList` elementi come segue:

* Quando più `window` Gli elementi vengono visualizzati come elementi figlio in un `windowList` o `dialog` elemento, ordina quelli `window` elementi in ordine decrescente, con le lunghezze `caption` nomi che indicano la posizione nell’ordine.
* Quando più `windowList` Gli elementi vengono visualizzati in un `window` elemento, ordina quelli `windowList` elementi in ordine decrescente, con le lunghezze `caption` attributi del primo `indexes/`elemento che indica la posizione nell’ordine.

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

**Ordinamento di elementi della finestra all&#39;interno di un elemento windowList**

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

### Creazione o modifica di un ulteriore file XML di finestra di dialogo per un&#39;applicazione nativa {#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application}

Se si crea uno script per un&#39;applicazione nativa non supportata in precedenza, è necessario creare anche un ulteriore file XML di finestra di dialogo per tale applicazione. Ogni applicazione nativa utilizzata da AppMon deve disporre di un solo file XML di dialogo aggiuntivo. Il file XML della finestra di dialogo aggiuntiva è necessario anche se non sono previste finestre di dialogo non richieste. La finestra di dialogo aggiuntiva deve contenere almeno un `window` , anche se `window` è semplicemente un segnaposto.

>[!NOTE]
>
>In questo contesto, il termine supplementare indica il contenuto `appmon.[applicationname].addition.[locale].xml` file. Tale file specifica sostituzioni e aggiunte al file XML della finestra di dialogo.

È inoltre possibile modificare il file XML della finestra di dialogo aggiuntiva per un&#39;applicazione nativa per i seguenti scopi:

* Per ignorare il file XML della finestra di dialogo per un&#39;applicazione con una risposta diversa
* Per aggiungere una risposta a una finestra di dialogo non gestita nel file XML della finestra di dialogo per l&#39;applicazione

Il nome del file che identifica un ulteriore file dialogXML è `appmon.[appname].addition.[locale].xml`. Un esempio è appmon.excel.add.en_US.xml.

Il nome del file XML della finestra di dialogo aggiuntiva deve utilizzare il formato `appmon.[applicationname].addition.[locale].xml`, dove *applicationname* deve corrispondere esattamente al nome applicazione utilizzato nel file di configurazione XML e nello script.

>[!NOTE]
>
>Nessuna delle applicazioni generiche specificate nel file di configurazione native2pdfconfig.xml dispone di un file XML di dialogo primario. La sezione [Aggiunta o modifica del supporto per un formato di file nativo](converting-file-formats-pdf.md#adding-or-modifying-support-for-a-native-file-format) descrive tali specifiche.

Devi ordinare `windowList` elementi visualizzati come elementi figlio in un `window` elemento. (vedere [Ordinamento degli elementi window e windowList](converting-file-formats-pdf.md#ordering-the-window-and-windowlist-elements).)

### Modifica del file XML della finestra di dialogo generale {#modifying-the-general-dialog-xml-file}

È possibile modificare il file XML della finestra di dialogo generale per rispondere alle finestre di dialogo generate dal sistema o per rispondere a finestre di dialogo comuni a più applicazioni.

#### Aggiunta di una voce di tipo file nel file di configurazione XML {#adding-a-filetype-entry-in-the-xml-configuration-file}

In questa procedura viene illustrato come aggiornare il file di configurazione del servizio Generate PDF per associare i tipi di file alle applicazioni native. Per aggiornare questo file di configurazione, è necessario utilizzare la console di amministrazione per esportare i dati di configurazione in un file. Il nome file predefinito per i dati di configurazione è native2pdfconfig.xml.

**Aggiornare il file di configurazione del servizio Generate PDF**

1. Seleziona **Home** > **Servizi** > **Adobe PDF Generator** > **File di configurazione**, quindi selezionare **Esporta configurazione**.
1. Modifica il `filetype-settings` nel file native2pdfconfig.xml, in base alle esigenze.
1. Seleziona **Home** > **Servizi** > **Adobe PDF Generator** >**File di configurazione**, quindi selezionare **Importa configurazione**. I dati di configurazione vengono importati nel servizio Genera PDF, sostituendo le impostazioni precedenti.

>[!NOTE]
>
>Il nome dell’applicazione viene specificato come valore del `GenericApp` dell&#39;elemento `name` attributo. Questo valore deve corrispondere esattamente al nome corrispondente specificato nello script sviluppato per l’applicazione. Analogamente, il `GenericApp` dell&#39;elemento `displayName` deve corrispondere esattamente a quello dello script corrispondente `expectedWindow` didascalia della finestra. Tale equivalenza viene valutata dopo la risoluzione delle espressioni regolari visualizzate nel `displayName` o `caption` attributi.

In questo esempio, i dati di configurazione predefiniti forniti con il servizio Generate PDF sono stati modificati per specificare che Notepad (non Microsoft Word) deve essere utilizzato per elaborare i file con estensione .txt. Prima di questa modifica, Microsoft Word era stato specificato come applicazione nativa che avrebbe dovuto elaborare tali file.

**Modifiche per indirizzare i file di testo al Blocco note (native2pdfconfig.xml)**

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

Creare una variabile di ambiente che specifichi la posizione dell&#39;eseguibile nativo dell&#39;applicazione. La variabile deve utilizzare il formato `[applicationname]_PATH`, dove *applicationname* deve corrispondere esattamente al nome dell&#39;applicazione utilizzato nel file di configurazione XML e nello script e dove il percorso contiene il percorso dell&#39;eseguibile tra virgolette doppie. Un esempio di tale variabile di ambiente è `Photoshop_PATH`.

Dopo aver creato la nuova variabile di ambiente, è necessario riavviare il server in cui è distribuito il servizio Generate PDF.

**Creare una variabile di sistema nell&#39;ambiente Windows XP**

1. Seleziona **Pannello di controllo Campaign > Sistema**.
1. Nella finestra di dialogo Proprietà di sistema fare clic su **Avanzate** e quindi fare clic su **Variabili di ambiente**.
1. In Variabili di sistema (System Variables) nella finestra di dialogo Variabili di ambiente (Environment Variables), fate clic su **Nuovo**.
1. Nella finestra di dialogo Nuova variabile di sistema, nel **Nome variabile** digitare un nome che utilizzi il formato `[applicationname]_PATH`.
1. In **Valore variabile** digitare il percorso completo e il nome file del file eseguibile dell&#39;applicazione e quindi fare clic su **OK**. Ad esempio, digita: `c:\windows\Notepad.exe`
1. Nella finestra di dialogo Variabili di ambiente, fate clic su **OK**.

**Creare una variabile di sistema dalla riga di comando**

1. In una finestra della riga di comando, digitare la definizione della variabile utilizzando il seguente formato:

   ```shell
            [applicationname]_PATH=[Full path name]
   ```

   Ad esempio, digita: `NotePad_PATH=C:\WINDOWS\NOTEPAD.EXE`

1. Avvia un nuovo prompt della riga di comando per rendere effettiva la variabile di sistema.

#### File XML {#xml-files}

AEM Forms include file XML di esempio che fanno sì che il servizio Generate PDF utilizzi il Blocco note per elaborare qualsiasi file con estensione .txt. Questo codice è incluso in questa sezione. È inoltre necessario apportare le altre modifiche descritte in questa sezione.

#### File XML della finestra di dialogo aggiuntivo {#additional-dialog-xml-file}

In questo esempio sono contenute le finestre di dialogo aggiuntive per l&#39;applicazione Blocco note. Queste finestre di dialogo possono essere aggiuntive a quelle specificate dal servizio Genera PDF.

**Finestre di dialogo Blocco note(appmon.notepad.add.en_US.xml)**

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

In questo esempio viene specificato il modo in cui il servizio Generate PDF interagisce con il Blocco note per stampare i file utilizzando la stampante Adobe PDF.

**File XML di script del Blocco note (appmon.notepad.script.en_US.xml)**

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
