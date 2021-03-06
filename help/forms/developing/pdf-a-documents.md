---
title: Utilizzo dei documenti PDF/A
seo-title: Utilizzo dei documenti PDF/A
description: Utilizzare il servizio DocConverter per determinare se un documento PDF è un documento PDF/A e convertire i documenti PDF in documenti PDF/A.
seo-description: Utilizzare il servizio DocConverter per determinare se un documento PDF è un documento PDF/A e convertire i documenti PDF in documenti PDF/A.
uuid: c258d253-068a-4412-955a-21d8a4792d6f
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 1e6cc554-aef1-463c-906b-634b80a27917
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2387'
ht-degree: 0%

---


# Utilizzo dei documenti PDF/A {#working-with-pdf-a-documents}

**Informazioni sul servizio DocConverter**

Il servizio DocConverter può convertire i documenti PDF in documenti PDA/A. Puoi eseguire queste attività utilizzando questo servizio:

* Conversione di documenti PDF in documenti PDF/A. (Vedere [Conversione di documenti in documenti PDF/A](pdf-a-documents.md#converting-documents-to-pdf-a-documents).)
* Determinare se i documenti PDF sono documenti PDF/A. (Consultare [Determinazione programmatica della conformità PDF/A](pdf-a-documents.md#programmatically-determining-pdf-a-compliancy).)

>[!NOTE]
>
>Per ulteriori informazioni sul servizio DocConverter, vedere [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Conversione di documenti in documenti PDF/A {#converting-documents-to-pdf-a-documents}

È possibile utilizzare il servizio DocConverter per convertire un documento PDF in un documento PDF/A. Poiché PDF/A è un formato di archiviazione per la conservazione a lungo termine del contenuto del documento, tutti i font vengono incorporati e il file non viene compresso. Di conseguenza, un documento PDF/A è generalmente più grande di un documento PDF standard. Inoltre, un documento PDF/A non contiene contenuto audio e video. Prima di convertire un documento PDF in un documento PDF/A, assicurarsi che il documento PDF non sia un documento PDF/A.

La specifica PDF/A-1 è costituita da due livelli di conformità, ovvero A e B. La differenza principale tra i due è relativa al supporto della struttura logica (accessibilità), che non è necessario per il livello di conformità B. A prescindere dal livello di conformità, PDF/A-1 determina che tutti i font sono incorporati nel documento PDF/A generato. Al momento, la convalida (e la conversione) supporta solo PDF/A-1b.

Sebbene PDF/A sia lo standard per l’archiviazione di documenti PDF, non è obbligatorio utilizzare PDF/A per l’archiviazione se un documento PDF standard soddisfa i requisiti aziendali. Lo scopo dello standard PDF/A è quello di stabilire un file PDF destinato alle esigenze di archiviazione e conservazione a lungo termine dei documenti.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio DocConverter, vedere [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary-of-steps}

Per convertire un documento PDF in un documento PDF/A, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Creare un client DocConvert
1. Fare riferimento a un documento PDF per la conversione in documento PDF/A.
1. Imposta le informazioni di tracciamento.
1. Converti il documento.
1. Salvare il documento PDF/A.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso della classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-docconverter-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è distribuito su JBoss Application Server)
* jbossall-client.jar (richiesto se AEM Forms è distribuito su JBoss Application Server)

Per informazioni sulla posizione di questi file JAR, consulta [Inclusione dei file della libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un client DocConvert**

Prima di eseguire un&#39;operazione DocConverter a livello di programmazione, è necessario creare un client DocConverter. Se utilizzi l’API Java, crea un oggetto `DocConverterServiceClient`. Se utilizzi l&#39;API del servizio Web DocConverter, crea un oggetto `DocConverterServiceService`.

**Fare riferimento a un documento PDF per la conversione in documento PDF/A**

Recupera un documento PDF da convertire in un documento PDF/A. Se si tenta di convertire un documento PDF, ad esempio un modulo Acrobat, in un documento PDF/A, verrà generata un&#39;eccezione.

**Impostare le informazioni di tracciamento**

Puoi impostare un’opzione di esecuzione che determina la quantità di informazioni tracciate durante il processo di conversione. In altre parole, è possibile impostare nove livelli diversi per specificare la quantità di informazioni che il servizio DocConverter tiene traccia quando converte un documento PDF in un documento PDF/A.

**Conversione del documento**

Dopo aver creato il client di servizio DocConverter, fare riferimento al documento PDF per convertire e impostare l&#39;opzione di esecuzione che specifica la quantità di informazioni da tenere traccia, è possibile convertire il documento PDF in un documento PDF/A.

**Salvare il documento PDF/A**

È possibile salvare il documento PDF/A come file PDF.

**Consulta anche**

[Conversione di documenti in documenti PDF/A tramite API Java](pdf-a-documents.md#convert-documents-to-pdf-a-documents-using-the-java-api)

[Conversione di documenti in documenti PDF/A tramite API del servizio Web](pdf-a-documents.md#convert-documents-to-pdf-a-documents-using-the-web-service-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Determinazione programmatica della conformità PDF/A](pdf-a-documents.md#programmatically-determining-pdf-a-compliancy)

### Convertire documenti in documenti PDF/A utilizzando l&#39;API Java {#convert-documents-to-pdf-a-documents-using-the-java-api}

Convertire un documento PDF in un documento PDF/A utilizzando l’API Java:

1. Includi file di progetto

   Includi file JAR client, come adobe-docconverter-client.jar, nel percorso di classe del progetto Java.

1. Creare un client DocConvert

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `DocConverterServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Fare riferimento a un documento PDF per la conversione in documento PDF/A

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento PDF da convertire utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del file PDF.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Impostare le informazioni di tracciamento

   * Creare un oggetto `PDFAConversionOptionSpec` utilizzando il relativo costruttore.
   * Impostare il livello di tracciamento delle informazioni richiamando il metodo `setLogLevel` dell&#39;oggetto `PDFAConversionOptionSpec` e passando un valore di stringa che specifica il livello di tracciamento. Ad esempio, passare il valore `FINE`. Per informazioni sui diversi valori, vedi il metodo `setLogLevel` in [Riferimento API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. Conversione del documento

   Convertire il documento PDF in un documento PDF/A richiamando il metodo `toPDFA` dell’oggetto `DocConverterServiceClient` e passando i seguenti valori:

   * L&#39;oggetto `com.adobe.idp.Document` che contiene il documento PDF da convertire
   * Oggetto `PDFAConversionOptionSpec` che specifica le informazioni di tracciamento

   Il metodo `toPDFA` restituisce un oggetto `PDFAConversionResult` contenente il documento PDF/A.

1. Salvare il documento PDF/A

   * Recupera il documento PDF/A richiamando il metodo `getPDFA` dell’oggetto `PDFAConversionResult`. Questo metodo restituisce un oggetto `com.adobe.idp.Document` che rappresenta il documento PDF/A.
   * Creare un oggetto `java.io.File` che rappresenta il file PDF/A. Assicurati che l&#39;estensione del nome file sia .pdf.
   * Compilare il file con i dati PDF/A richiamando il metodo `copyToFile` dell’oggetto `java.io.File` e passando l’oggetto `com.adobe.idp.Document`.

**Consulta anche**

[Utilizzo dei documenti PDF/A](pdf-a-documents.md#working-with-pdf-a-documents)

[Avvio rapido (modalità SOAP): Conversione di un documento in un documento PDF/A tramite l’API Java](/help/forms/developing/docconverter-service-java-api-quick.md#quick-start-soap-mode-converting-a-document-to-a-pdf-a-document-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Convertire documenti in documenti PDF/A utilizzando l&#39;API del servizio Web {#convert-documents-to-pdf-a-documents-using-the-web-service-api}

Convertire un documento PDF in un documento PDF/A utilizzando l&#39;API DocConverter (servizio Web):

1. Includi file di progetto

   * Creare un assembly client Microsoft .NET che utilizzi la WSDL DocConverter.
   * Fare riferimento all&#39;assembly client Microsoft .NET.

1. Creare un client DocConvert

   * Utilizzando l&#39;assembly client Microsoft .NET, creare un oggetto `DocConverterServiceService` richiamando il relativo costruttore predefinito.
   * Impostare il membro dati `Credentials` dell&#39;oggetto `DocConverterServiceService` con un valore `System.Net.NetworkCredential` che specifica il nome utente e il valore della password.

1. Fare riferimento a un documento PDF per la conversione in documento PDF/A

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L’oggetto `BLOB` viene utilizzato per memorizzare il documento PDF convertito in documento PDF/A.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni dell&#39;array di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare l’array di byte con i dati del flusso richiamando il metodo `Read` dell’oggetto `System.IO.FileStream` e passando l’array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando la relativa proprietà `binaryData` con il contenuto dell&#39;array di byte.

1. Impostare le informazioni di tracciamento

   * Creare un oggetto `PDFAConversionOptionSpec` utilizzando il relativo costruttore.
   * Imposta il livello di tracciamento delle informazioni assegnando un valore che specifica il livello di tracciamento al membro dati `logLevel` dell&#39;oggetto `PDFAConversionOptionSpec`. Ad esempio, assegnare il valore `FINE` a questo membro dati.

1. Conversione del documento

   Convertire il documento PDF in un documento PDF/A richiamando il metodo `toPDFA` dell’oggetto `DocConverterServiceService` e passando i seguenti valori:

   * L&#39;oggetto `BLOB` che contiene il documento PDF da convertire
   * Oggetto `PDFAConversionOptionSpec` che specifica le informazioni di tracciamento

   Il metodo `toPDFA` restituisce un oggetto `PDFAConversionResult` contenente il documento PDF/A.

1. Salvare il documento PDF/A

   * Creare un oggetto `BLOB` che memorizza il documento PDF/A ottenendo il valore del membro dati `PDFAConversionResult` dell&#39;oggetto `PDFADocument`.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `BLOB` restituito utilizzando l&#39;oggetto `PDFAConversionResult`. Compilare l&#39;array di byte ottenendo il valore del membro dati `BLOB` dell&#39;oggetto `binaryData`.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF/A.
   * Creare un oggetto `System.IO.BinaryWriter` richiamandone il costruttore e passando l&#39;oggetto `System.IO.FileStream`.
   * Scrivi il contenuto dell’array di byte in un file PDF richiamando il metodo `Write` dell’oggetto `System.IO.BinaryWriter` e passando l’array di byte.

**Consulta anche**

[Utilizzo dei documenti PDF/A](pdf-a-documents.md#working-with-pdf-a-documents)

[Richiamo di AEM Forms con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Creazione di un assembly client .NET che utilizza la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Determinazione programmatica della conformità PDF/A {#programmatically-determining-pdf-a-compliancy}

È possibile utilizzare il servizio DocConverter per determinare se un documento PDF è compatibile con PDF/A. Per informazioni su un documento PDF/A e su come convertire un documento PDF in un documento PDF/A, vedere [Conversione di documenti in documenti PDF/A](pdf-a-documents.md#converting-documents-to-pdf-a-documents).

>[!NOTE]
>
>Per ulteriori informazioni sul servizio DocConverter, vedere [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-1}

Per determinare la conformità PDF/A, effettua le seguenti operazioni:

1. Includi file di progetto.
1. Creare un client DocConvert
1. Fare riferimento a un documento PDF utilizzato per determinare la conformità PDF/A.
1. Impostare le opzioni di esecuzione.
1. Recupera informazioni sul documento PDF.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso della classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-docconverter-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è distribuito su JBoss Application Server)
* jbossall-client.jar (richiesto se AEM Forms è distribuito su JBoss Application Server)

Per informazioni sulla posizione di questi file JAR, consulta [Inclusione dei file della libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un client DocConvert**

Prima di eseguire un&#39;operazione DocConverter a livello di programmazione, è necessario creare un client DocConverter. Se utilizzi l’API Java, crea un oggetto `DocConverterServiceClient`. Se utilizzi l&#39;API del servizio Web DocConverter, crea un oggetto `DocConverterServiceService`.

**Riferimento a un documento PDF utilizzato per determinare la conformità PDF/A**

Per determinare se il documento PDF è conforme a PDF/A, è necessario fare riferimento a un documento PDF e passarlo al servizio DocConverter.

**Impostare le opzioni di esecuzione**

Puoi impostare un’opzione di esecuzione che determina la quantità di informazioni tracciate durante il processo di conversione. In altre parole, è possibile impostare nove livelli diversi per specificare la quantità di informazioni che il servizio DocConverter tiene traccia quando converte un documento PDF in un documento PDF/A.

**Recupera informazioni sul documento PDF**

Dopo aver creato il client di servizio DocConverter, fare riferimento al documento PDF e impostare le opzioni di esecuzione, è possibile determinare se il documento PDF è un documento conforme a PDF/A.

**Consulta anche**

[Determinare la conformità PDF/A utilizzando l’API Java](pdf-a-documents.md#determine-pdf-a-compliancy-using-the-java-api)

[Determinare la conformità PDF/A utilizzando l’API del servizio Web](pdf-a-documents.md#determine-pdf-a-compliancy-using-the-web-service-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Determinare la conformità PDF/A utilizzando l’API Java {#determine-pdf-a-compliancy-using-the-java-api}

Determina la conformità PDF/A utilizzando l’API Java:

1. Includi file di progetto

   Includi file JAR client, come adobe-docconverter-client.jar, nel percorso di classe del progetto Java.

1. Creare un client DocConvert

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `DocConverterServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Riferimento a un documento PDF utilizzato per determinare la conformità PDF/A

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento PDF da convertire utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del file PDF.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Impostare le opzioni di esecuzione

   * Creare un oggetto `PDFAValidationOptionSpec` utilizzando il relativo costruttore.
   * Impostare il livello di conformità richiamando il metodo `setCompliance` dell&#39;oggetto `PDFAValidationOptionSpec` e passando `PDFAValidationOptionSpec.Compliance.PDFA_1B`.
   * Impostare il livello di tracciamento delle informazioni richiamando il metodo `setLogLevel` dell&#39;oggetto `PDFAValidationOptionSpec` e passando un valore di stringa che specifica il livello di tracciamento. Ad esempio, passare il valore `FINE`. Per informazioni sui diversi valori, vedi il metodo `setLogLevel` in [Riferimento API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. Recupera informazioni sul documento PDF

   Determina la conformità PDF/A richiamando il metodo `isPDFA` dell’oggetto `DocConverterServiceClient` e passando i seguenti valori:

   * L&#39;oggetto `com.adobe.idp.Document` che contiene il documento PDF.
   * L&#39;oggetto `PDFAValidationOptionSpec` che specifica le opzioni di esecuzione.

   Il metodo `isPDFA` restituisce un oggetto `PDFAValidationResult` contenente i risultati di questa operazione.

**Consulta anche**

[Utilizzo dei documenti PDF/A](pdf-a-documents.md#working-with-pdf-a-documents)

[Avvio rapido (modalità SOAP): Determinazione della conformità PDF/A tramite l’API Java](/help/forms/developing/docconverter-service-java-api-quick.md#quick-start-soap-mode-determining-pdf-a-compliancy-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Determinare la conformità PDF/A utilizzando l&#39;API del servizio Web {#determine-pdf-a-compliancy-using-the-web-service-api}

Determina la conformità PDF/A utilizzando l’API del servizio Web:

1. Includi file di progetto

   * Creare un assembly client Microsoft .NET che utilizzi la WSDL DocConverter.
   * Fare riferimento all&#39;assembly client Microsoft .NET.

1. Creare un client DocConvert

   * Utilizzando l&#39;assembly client Microsoft .NET, creare un oggetto `DocConverterServiceService` richiamando il relativo costruttore predefinito.
   * Impostare il membro dati `Credentials` dell&#39;oggetto `DocConverterServiceService` con un valore `System.Net.NetworkCredential` che specifica il nome utente e il valore della password.

1. Riferimento a un documento PDF utilizzato per determinare la conformità PDF/A

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L’oggetto `BLOB` viene utilizzato per memorizzare il documento PDF convertito in documento PDF/A.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni dell&#39;array di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare l’array di byte con i dati del flusso richiamando il metodo `Read` dell’oggetto `System.IO.FileStream` e passando l’array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando la relativa proprietà `binaryData` con il contenuto dell&#39;array di byte.

1. Impostare le opzioni di esecuzione

   * Creare un oggetto `PDFAValidationOptionSpec` utilizzando il relativo costruttore.
   * Imposta il livello di conformità assegnando al membro dati `compliance` dell&#39;oggetto `PDFAValidationOptionSpec` il valore `PDFAConversionOptionSpec_Compliance.PDFA_1B`.
   * Imposta il livello di tracciamento delle informazioni assegnando il membro dati `resultLevel` dell&#39;oggetto `PDFAValidationOptionSpec_ResultLevel.DETAILED` con il valore `PDFAValidationOptionSpec`.

1. Recupera informazioni sul documento PDF

   Determina la conformità PDF/A richiamando il metodo `isPDFA` dell’oggetto `DocConverterServiceService` e passando i seguenti valori:

   * L&#39;oggetto `BLOB` che contiene il documento PDF.
   * L&#39;oggetto `PDFAValidationOptionSpec` che contiene opzioni di esecuzione.

   Il metodo `isPDFA` restituisce un oggetto `PDFAValidationResult` contenente i risultati di questa operazione.

**Consulta anche**

[Utilizzo dei documenti PDF/A](pdf-a-documents.md#working-with-pdf-a-documents)

[Richiamo di AEM Forms con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Creazione di un assembly client .NET che utilizza la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)
