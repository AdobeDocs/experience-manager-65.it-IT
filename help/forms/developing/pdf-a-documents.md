---
title: Utilizzo dei documenti di PDF/A
seo-title: Working with PDF/A Documents
description: Utilizzare il servizio DocConverter per determinare se un documento PDF è un documento PDF/A e convertire i documenti PDF in documenti PDF/A.
seo-description: Use the  DocConverter service to determine if a PDF document is a PDF/A document and convert PDF documents to PDF/A documents.
uuid: c258d253-068a-4412-955a-21d8a4792d6f
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 1e6cc554-aef1-463c-906b-634b80a27917
role: Developer
exl-id: 966c3554-25df-4467-866e-11c43cc15b58
source-git-commit: 1807919078996b1cf1cbd1f2d90c3b14cb660e2c
workflow-type: tm+mt
source-wordcount: '2356'
ht-degree: 1%

---

# Utilizzo dei documenti di PDF/A {#working-with-pdf-a-documents}

**Informazioni sul servizio DocConverter**

Il servizio DocConverter può convertire i documenti PDF in documenti PDA/A. Puoi eseguire queste attività utilizzando questo servizio:

* Convertire documenti PDF in documenti PDF/A. (vedere [Conversione di documenti in documenti PDF/A](pdf-a-documents.md#converting-documents-to-pdf-a-documents).)
* Determina se i documenti PDF sono documenti PDF/A. (vedere [Determinazione a livello di programmazione della conformità di PDF/A](pdf-a-documents.md#programmatically-determining-pdf-a-compliancy).)

>[!NOTE]
>
>Per ulteriori informazioni sul servizio DocConverter, vedere [Guida di riferimento dei servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Conversione di documenti in documenti PDF/A {#converting-documents-to-pdf-a-documents}

È possibile utilizzare il servizio DocConverter per convertire un documento PDF in un documento PDF/A. Poiché PDF/A è un formato di archiviazione per la conservazione a lungo termine del contenuto del documento, tutti i font sono incorporati e il file non è compresso. Di conseguenza, un documento PDF/A è generalmente più grande di un documento PDF standard. Inoltre, un documento PDF/A non include contenuti audio e video. Prima di convertire un documento PDF in un documento PDF/A, accertatevi che il documento PDF non sia un documento PDF/A.

La specifica PDF/A-1 è costituita da due livelli di conformità, ovvero A e B. La differenza principale tra i due è relativa al supporto della struttura logica (accessibilità), che non è richiesto per il livello di conformità B. Indipendentemente dal livello di conformità, PDF/A-1 impone che tutti i font siano incorporati all&#39;interno del documento PDF/A generato. Al momento, solo PDF/A-1b è supportato nella convalida (e nella conversione).

Sebbene PDF/A sia lo standard per l’archiviazione dei documenti PDF PDF, non è obbligatorio utilizzarlo per l’archiviazione se un documento PDF standard soddisfa i requisiti aziendali. Lo scopo dello standard PDF/A è quello di stabilire un file PDF per esigenze di archiviazione a lungo termine e conservazione dei documenti.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio DocConverter, vedere [Guida di riferimento dei servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary-of-steps}

Per convertire un documento PDF in un documento PDF/A, effettuare le seguenti operazioni:

1. Includi file di progetto.
1. Creare un client DocConvert
1. Fare riferimento a un documento PDF da convertire in un documento PDF/A.
1. Imposta le informazioni di tracciamento.
1. Convertire il documento.
1. Salvare il documento PDF/A.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso della classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-docconverter-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è distribuito sul server applicazioni JBoss)
* jbossall-client.jar (richiesto se AEM Forms è distribuito sul server applicazioni JBoss)

Per informazioni sulla posizione di questi file JAR, vedi [Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un client DocConvert**

Prima di poter eseguire un&#39;operazione DocConverter a livello di programmazione, è necessario creare un client DocConverter. Se utilizzi l’API Java, crea un’ `DocConverterServiceClient` oggetto. Se utilizzi l’API del servizio web DocConverter, crea un’ `DocConverterServiceService` oggetto.

**Fare riferimento a un documento PDF da convertire in un documento PDF/A**

Recuperare un documento PDF per convertirlo in un documento PDF/A. Se si tenta di convertire un documento PDF, ad esempio un modulo Acrobat, in un documento PDF/A, verrà generata un&#39;eccezione.

**Impostare le informazioni di tracciamento**

È possibile impostare un&#39;opzione di run-time che determina la quantità di informazioni tracciate durante il processo di conversione. In altre parole, è possibile impostare nove livelli diversi che specificano la quantità di informazioni che il servizio DocConverter tiene traccia quando converte un documento PDF in un documento PDF/A.

**Converti il documento**

Dopo aver creato il client del servizio DocConverter, fare riferimento al documento PDF per la conversione e impostare l&#39;opzione di runtime che specifica la quantità di informazioni tracciate, è possibile convertire il documento PDF in un documento PDF/A.

**Salvare il documento PDF/A**

È possibile salvare il documento PDF/A come file PDF.

**Consulta anche**

[Conversione di documenti in documenti PDF/A tramite API Java](pdf-a-documents.md#convert-documents-to-pdf-a-documents-using-the-java-api)

[Conversione di documenti in documenti PDF/A tramite l’API del servizio web](pdf-a-documents.md#convert-documents-to-pdf-a-documents-using-the-web-service-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Determinazione a livello di programmazione della conformità di PDF/A](pdf-a-documents.md#programmatically-determining-pdf-a-compliancy)

### Conversione di documenti in documenti PDF/A tramite API Java {#convert-documents-to-pdf-a-documents-using-the-java-api}

Convertire un documento PDF in un documento PDF/A utilizzando l’API Java:

1. Includi file di progetto

   Includi i file JAR client, come adobe-docconverter-client.jar, nel percorso di classe del progetto Java.

1. Creare un client DocConvert

   * Creare un `ServiceClientFactory` oggetto che contiene proprietà di connessione.
   * Creare un `DocConverterServiceClient` mediante il costruttore e passando il `ServiceClientFactory` oggetto.

1. Fare riferimento a un documento PDF da convertire in un documento PDF/A

   * Creare un `java.io.FileInputStream` oggetto che rappresenta il documento PDF da convertire utilizzando il relativo costruttore e passando un valore stringa che specifica la posizione del file PDF.
   * Creare un `com.adobe.idp.Document` mediante il costruttore e passando il `java.io.FileInputStream` oggetto.

1. Impostare le informazioni di tracciamento

   * Creare un `PDFAConversionOptionSpec` mediante il costruttore.
   * Imposta il livello di tracciamento delle informazioni richiamando `PDFAConversionOptionSpec` dell&#39;oggetto `setLogLevel` e passando un valore stringa che specifica il livello di tracciamento. Ad esempio, passa il valore `FINE`. Per informazioni sui diversi valori, vedere `setLogLevel` metodo in [Riferimento API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. Converti il documento

   Convertire il documento PDF in un documento PDF/A richiamando il `DocConverterServiceClient` dell&#39;oggetto `toPDFA` e fornendo i seguenti valori:

   * Il `com.adobe.idp.Document` oggetto contenente il documento PDF da convertire
   * Il `PDFAConversionOptionSpec` oggetto che specifica le informazioni di tracciamento

   Il `toPDFA` il metodo restituisce un `PDFAConversionResult` oggetto che contiene il documento PDF/A.

1. Salvare il documento PDF/A

   * Recupera il documento PDF/A richiamando il `PDFAConversionResult` dell&#39;oggetto `getPDFA` metodo. Questo metodo restituisce un `com.adobe.idp.Document` oggetto che rappresenta il documento PDF/A.
   * Creare un `java.io.File` oggetto che rappresenta il file PDF/A. Assicurati che l’estensione del nome file sia .pdf.
   * Popola il file con i dati di PDF/A richiamando il `com.adobe.idp.Document` dell&#39;oggetto `copyToFile` e passando il `java.io.File` oggetto.

**Consulta anche**

[Utilizzo dei documenti di PDF/A](pdf-a-documents.md#working-with-pdf-a-documents)

[Guida rapida (modalità SOAP): conversione di un documento in un documento PDF/A tramite l’API Java](/help/forms/developing/docconverter-service-java-api-quick.md#quick-start-soap-mode-converting-a-document-to-a-pdf-a-document-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Conversione di documenti in documenti PDF/A tramite l’API del servizio web {#convert-documents-to-pdf-a-documents-using-the-web-service-api}

Converti un documento PDF in un documento PDF/A utilizzando l’API DocConverter (servizio web):

1. Includi file di progetto

   * Creare un assembly client Microsoft .NET che utilizza il WSDL DocConverter.
   * Fare riferimento all&#39;assembly client Microsoft .NET.

1. Creare un client DocConvert

   * Utilizzando l&#39;assembly client Microsoft .NET, creare un `DocConverterServiceService` richiamando il relativo costruttore predefinito.
   * Imposta il `DocConverterServiceService` dell&#39;oggetto `Credentials` membro dati con un `System.Net.NetworkCredential` valore che specifica il nome utente e la password.

1. Fare riferimento a un documento PDF da convertire in un documento PDF/A

   * Creare un `BLOB` mediante il costruttore. Il `BLOB` L&#39;oggetto viene utilizzato per memorizzare il documento PDF convertito in un documento PDF/A.
   * Creare un `System.IO.FileStream` richiamando il relativo costruttore e passando un valore stringa che rappresenta la posizione del file del documento PDF e la modalità di apertura del file in.
   * Creare una matrice di byte che memorizza il contenuto della `System.IO.FileStream` oggetto. È possibile determinare le dimensioni della matrice di byte ottenendo `System.IO.FileStream` dell&#39;oggetto `Length` proprietà.
   * Compilare la matrice di byte con i dati di flusso richiamando `System.IO.FileStream` dell&#39;oggetto `Read` e passando la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare il `BLOB` oggetto assegnando il relativo `binaryData` con il contenuto della matrice di byte.

1. Impostare le informazioni di tracciamento

   * Creare un `PDFAConversionOptionSpec` mediante il costruttore.
   * Imposta il livello di tracciamento delle informazioni assegnando un valore che specifica il livello di tracciamento al `PDFAConversionOptionSpec` dell&#39;oggetto `logLevel` membro dati. Ad esempio, assegna il valore `FINE` a questo membro dati.

1. Converti il documento

   Convertire il documento PDF in un documento PDF/A richiamando il `DocConverterServiceService` dell&#39;oggetto `toPDFA` e fornendo i seguenti valori:

   * Il `BLOB` oggetto contenente il documento PDF da convertire
   * Il `PDFAConversionOptionSpec` oggetto che specifica le informazioni di tracciamento

   Il `toPDFA` il metodo restituisce un `PDFAConversionResult` oggetto che contiene il documento PDF/A.

1. Salvare il documento PDF/A

   * Creare un `BLOB` oggetto che memorizza il documento PDF/A ottenendo il valore del `PDFAConversionResult` dell&#39;oggetto `PDFADocument` membro dati.
   * Creare una matrice di byte che memorizza il contenuto della `BLOB` oggetto restituito utilizzando `PDFAConversionResult` oggetto. Popolare la matrice di byte ottenendo il valore della `BLOB` dell&#39;oggetto `binaryData` membro dati.
   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore stringa che rappresenta la posizione del file del documento PDF/A.
   * Creare un `System.IO.BinaryWriter` oggetto richiamando il relativo costruttore e passando il `System.IO.FileStream` oggetto.
   * Scrivere il contenuto della matrice di byte in un file PDF richiamando `System.IO.BinaryWriter` dell&#39;oggetto `Write` e passando la matrice di byte.

**Consulta anche**

[Utilizzo dei documenti di PDF/A](pdf-a-documents.md#working-with-pdf-a-documents)

[Richiamare AEM Forms utilizzando la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Creazione di un assembly client .NET che utilizza la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Determinazione a livello di programmazione della conformità di PDF/A {#programmatically-determining-pdf-a-compliancy}

È possibile utilizzare il servizio DocConverter per determinare se un documento PDF è conforme a PDF/A. Per informazioni su un documento PDF/A e su come convertire un documento PDF in un documento PDF/A, consulta [Conversione di documenti in documenti PDF/A](pdf-a-documents.md#converting-documents-to-pdf-a-documents).

>[!NOTE]
>
>Per ulteriori informazioni sul servizio DocConverter, vedere [Guida di riferimento dei servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-1}

Per determinare la conformità di PDF/A, effettuare le seguenti operazioni:

1. Includi file di progetto.
1. Creare un client DocConvert
1. Fai riferimento a un documento PDF utilizzato per determinare la conformità di PDF/A.
1. Impostare le opzioni di runtime.
1. Recuperare informazioni sul documento PDF.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso della classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-docconverter-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è distribuito sul server applicazioni JBoss)
* jbossall-client.jar (richiesto se AEM Forms è distribuito sul server applicazioni JBoss)

Per informazioni sulla posizione di questi file JAR, vedi [Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un client DocConvert**

Prima di poter eseguire un&#39;operazione DocConverter a livello di programmazione, è necessario creare un client DocConverter. Se utilizzi l’API Java, crea un’ `DocConverterServiceClient` oggetto. Se utilizzi l’API del servizio web DocConverter, crea un’ `DocConverterServiceService` oggetto.

**Riferimento a un documento PDF utilizzato per determinare la conformità PDF/A**

È necessario fare riferimento a un documento PDF e passarlo al servizio DocConverter per determinare se il documento PDF è compatibile con PDF/A.

**Impostare le opzioni di runtime**

È possibile impostare un&#39;opzione di run-time che determina la quantità di informazioni tracciate durante il processo di conversione. In altre parole, è possibile impostare nove diversi livelli che specificano la quantità di informazioni che il servizio DocConverter tiene traccia quando converte un documento PDF in un documento PDF/A.

**Recuperare informazioni sul documento PDF**

Dopo aver creato il client del servizio DocConverter, aver creato un riferimento al documento PDF e aver impostato le opzioni di runtime, è possibile determinare se il documento PDF è compatibile con PDF/A.

**Consulta anche**

[Determinare la conformità PDF/A utilizzando l’API Java](pdf-a-documents.md#determine-pdf-a-compliancy-using-the-java-api)

[Determinare la conformità PDF/A utilizzando l’API del servizio web](pdf-a-documents.md#determine-pdf-a-compliancy-using-the-web-service-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Determinare la conformità PDF/A utilizzando l’API Java {#determine-pdf-a-compliancy-using-the-java-api}

Determinare la conformità di PDF/A utilizzando l’API Java:

1. Includi file di progetto

   Includi i file JAR client, come adobe-docconverter-client.jar, nel percorso di classe del progetto Java.

1. Creare un client DocConvert

   * Creare un `ServiceClientFactory` oggetto che contiene proprietà di connessione.
   * Creare un `DocConverterServiceClient` mediante il costruttore e passando il `ServiceClientFactory` oggetto.

1. Riferimento a un documento PDF utilizzato per determinare la conformità PDF/A

   * Creare un `java.io.FileInputStream` oggetto che rappresenta il documento PDF da convertire utilizzando il relativo costruttore e passando un valore stringa che specifica la posizione del file PDF.
   * Creare un `com.adobe.idp.Document` mediante il costruttore e passando il `java.io.FileInputStream` oggetto.

1. Impostare le opzioni di runtime

   * Creare un `PDFAValidationOptionSpec` mediante il costruttore.
   * Impostare il livello di conformità richiamando `PDFAValidationOptionSpec` dell&#39;oggetto `setCompliance` metodo e passaggio `PDFAValidationOptionSpec.Compliance.PDFA_1B`.
   * Imposta il livello di tracciamento delle informazioni richiamando `PDFAValidationOptionSpec` dell&#39;oggetto `setLogLevel` e passando un valore stringa che specifica il livello di tracciamento. Ad esempio, passa il valore `FINE`. Per informazioni sui diversi valori, vedere `setLogLevel` metodo in [Riferimento API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. Recuperare informazioni sul documento PDF

   Determinare la conformità PDF/A richiamando `DocConverterServiceClient` dell&#39;oggetto `isPDFA` e fornendo i seguenti valori:

   * Il `com.adobe.idp.Document` oggetto che contiene il documento PDF.
   * Il `PDFAValidationOptionSpec` oggetto che specifica le opzioni di runtime.

   Il `isPDFA` il metodo restituisce un `PDFAValidationResult` oggetto che contiene i risultati dell&#39;operazione.

**Consulta anche**

[Utilizzo dei documenti di PDF/A](pdf-a-documents.md#working-with-pdf-a-documents)

[Quick Start (modalità SOAP): determinazione della conformità PDF/A tramite l’API Java](/help/forms/developing/docconverter-service-java-api-quick.md#quick-start-soap-mode-determining-pdf-a-compliancy-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Determinare la conformità PDF/A utilizzando l’API del servizio web {#determine-pdf-a-compliancy-using-the-web-service-api}

Determinare la conformità di PDF/A utilizzando l’API del servizio web:

1. Includi file di progetto

   * Creare un assembly client Microsoft .NET che utilizza il WSDL DocConverter.
   * Fare riferimento all&#39;assembly client Microsoft .NET.

1. Creare un client DocConvert

   * Utilizzando l&#39;assembly client Microsoft .NET, creare un `DocConverterServiceService` richiamando il relativo costruttore predefinito.
   * Imposta il `DocConverterServiceService` dell&#39;oggetto `Credentials` membro dati con un `System.Net.NetworkCredential` valore che specifica il nome utente e la password.

1. Riferimento a un documento PDF utilizzato per determinare la conformità PDF/A

   * Creare un `BLOB` mediante il costruttore. Il `BLOB` L&#39;oggetto viene utilizzato per memorizzare il documento PDF convertito in un documento PDF/A.
   * Creare un `System.IO.FileStream` richiamando il relativo costruttore e passando un valore stringa che rappresenta la posizione del file del documento PDF e la modalità di apertura del file in.
   * Creare una matrice di byte che memorizza il contenuto della `System.IO.FileStream` oggetto. È possibile determinare le dimensioni della matrice di byte ottenendo `System.IO.FileStream` dell&#39;oggetto `Length` proprietà.
   * Compilare la matrice di byte con i dati di flusso richiamando `System.IO.FileStream` dell&#39;oggetto `Read` e passando la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare il `BLOB` oggetto assegnando il relativo `binaryData` con il contenuto della matrice di byte.

1. Impostare le opzioni di runtime

   * Creare un `PDFAValidationOptionSpec` mediante il costruttore.
   * Impostare il livello di conformità assegnando `PDFAValidationOptionSpec` dell&#39;oggetto `compliance` membro dati con il valore `PDFAConversionOptionSpec_Compliance.PDFA_1B`.
   * Imposta il livello di tracciamento delle informazioni assegnando `PDFAValidationOptionSpec` dell&#39;oggetto `resultLevel` membro dati con il valore `PDFAValidationOptionSpec_ResultLevel.DETAILED`.

1. Recuperare informazioni sul documento PDF

   Determinare la conformità PDF/A richiamando `DocConverterServiceService` dell&#39;oggetto `isPDFA` e fornendo i seguenti valori:

   * Il `BLOB` oggetto che contiene il documento PDF.
   * Il `PDFAValidationOptionSpec` oggetto contenente opzioni di runtime.

   Il `isPDFA` il metodo restituisce un `PDFAValidationResult` oggetto che contiene i risultati dell&#39;operazione.

**Consulta anche**

[Utilizzo dei documenti di PDF/A](pdf-a-documents.md#working-with-pdf-a-documents)

[Richiamare AEM Forms utilizzando la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Creazione di un assembly client .NET che utilizza la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)
