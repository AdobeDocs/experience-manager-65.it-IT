---
title: Utilizzo dei documenti PDF/A
seo-title: Utilizzo dei documenti PDF/A
description: Il servizio DocConverter consente di determinare se un documento PDF è un documento PDF/A e di convertire i documenti PDF in documenti PDF/A.
seo-description: Il servizio DocConverter consente di determinare se un documento PDF è un documento PDF/A e di convertire i documenti PDF in documenti PDF/A.
uuid: c258d253-068a-4412-955a-21d8a4792d6f
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 1e6cc554-aef1-463c-906b-634b80a27917
translation-type: tm+mt
source-git-commit: 07889ead2ae402b5fb738ca08c7efe076ef33e44
workflow-type: tm+mt
source-wordcount: '2386'
ht-degree: 0%

---


# Utilizzo di documenti PDF/A {#working-with-pdf-a-documents}

**Informazioni sul servizio DocConverter**

Il servizio DocConverter può convertire documenti PDF in documenti PDA/A. È possibile eseguire le seguenti attività con il seguente servizio:

* Convertire i documenti PDF in documenti PDF/A. (Vedere [Conversione di documenti in documenti PDF/A](pdf-a-documents.md#converting-documents-to-pdf-a-documents).)
* Determinare se i documenti PDF sono documenti PDF/A. (Vedere [Determinazione programmatica della conformità PDF/A](pdf-a-documents.md#programmatically-determining-pdf-a-compliancy).)

>[!NOTE]
>
>Per ulteriori informazioni sul servizio DocConverter, vedere [Guida di riferimento dei servizi per  AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Conversione di documenti in documenti PDF/A {#converting-documents-to-pdf-a-documents}

È possibile utilizzare il servizio DocConverter per convertire un documento PDF in un documento PDF/A. Poiché PDF/A è un formato di archiviazione per la conservazione a lungo termine del contenuto del documento, tutti i font vengono incorporati e il file non viene compresso. Di conseguenza, un documento PDF/A è generalmente più grande di un documento PDF standard. Inoltre, un documento PDF/A non contiene contenuto audio e video. Prima di convertire un documento PDF in un documento PDF/A, accertarsi che il documento PDF non sia un documento PDF/A.

La specifica PDF/A-1 è costituita da due livelli di conformità, ossia A e B. La differenza principale tra i due è relativa al supporto della struttura logica (accessibilità), che non è richiesto per il livello di conformità B. Indipendentemente dal livello di conformità, PDF/A-1 stabilisce che tutti i font sono incorporati nel documento PDF/A generato. Al momento, è supportato solo PDF/A-1b per la convalida (e la conversione).

Sebbene PDF/A sia lo standard per l&#39;archiviazione di documenti PDF, non è obbligatorio utilizzare i PDF/A per l&#39;archiviazione se un documento PDF standard soddisfa i requisiti aziendali. Lo scopo dello standard PDF/A è quello di creare un file PDF adatto per l&#39;archiviazione a lungo termine e per la conservazione dei documenti.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio DocConverter, vedere [Guida di riferimento dei servizi per  AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary-of-steps}

Per convertire un documento PDF in documento PDF/A, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un client DocConvert
1. Fare riferimento a un documento PDF per la conversione in documento PDF/A.
1. Impostate le informazioni di tracciamento.
1. Convertite il documento.
1. Salvare il documento PDF/A.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, accertatevi di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-docconverter-client.jar
* adobe-utilities.jar (richiesto se  AEM Forms è distribuito sul server applicazioni JBoss)
* jbossall-client.jar (richiesto se  AEM Forms è distribuito sul server applicazioni JBoss)

Per informazioni sulla posizione di questi file JAR, vedere [Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un client DocConvert**

Prima di eseguire un&#39;operazione DocConverter a livello di programmazione, è necessario creare un client DocConverter. Se utilizzate l&#39;API Java, create un oggetto `DocConverterServiceClient`. Se utilizzate l&#39;API del servizio Web DocConverter, create un oggetto `DocConverterServiceService`.

**Riferimento a un documento PDF da convertire in documento PDF/A**

Recuperare un documento PDF da convertire in documento PDF/A. Se si tenta di convertire un documento PDF, ad esempio un modulo Acrobat , in un documento PDF/A, si verificherà un&#39;eccezione.

**Impostazione delle informazioni di tracciamento**

È possibile impostare un&#39;opzione di esecuzione che determina la quantità di informazioni tracciate durante il processo di conversione. In altre parole, è possibile impostare nove livelli diversi per specificare quante informazioni il servizio DocConverter tiene traccia quando converte un documento PDF in un documento PDF/A.

**Conversione del documento**

Dopo aver creato il client del servizio DocConverter, fare riferimento al documento PDF per convertire e impostare l&#39;opzione di esecuzione che specifica il numero di informazioni da tenere traccia, è possibile convertire il documento PDF in un documento PDF/A.

**Salvare il documento PDF/A**

È possibile salvare il documento PDF/A come file PDF.

**Consulta anche**

[Conversione di documenti in documenti PDF/A tramite l&#39;API Java](pdf-a-documents.md#convert-documents-to-pdf-a-documents-using-the-java-api)

[Conversione di documenti in documenti PDF/A tramite l&#39;API del servizio Web](pdf-a-documents.md#convert-documents-to-pdf-a-documents-using-the-web-service-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Determinazione programmatica della conformità PDF/A](pdf-a-documents.md#programmatically-determining-pdf-a-compliancy)

### Convertire i documenti in documenti PDF/A utilizzando l&#39;API Java {#convert-documents-to-pdf-a-documents-using-the-java-api}

Convertire un documento PDF in un documento PDF/A utilizzando l&#39;API Java:

1. Includi file di progetto

   Includete file JAR client, ad esempio adobe-docconverter-client.jar, nel percorso di classe del progetto Java.

1. Creare un client DocConvert

   * Creare un oggetto `ServiceClientFactory` che contiene le proprietà di connessione.
   * Creare un oggetto `DocConverterServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Riferimento a un documento PDF da convertire in documento PDF/A

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento PDF da convertire utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del file PDF.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Impostazione delle informazioni di tracciamento

   * Creare un oggetto `PDFAConversionOptionSpec` utilizzando il relativo costruttore.
   * Impostare il livello di tracciamento delle informazioni richiamando il metodo `setLogLevel` dell&#39;oggetto `PDFAConversionOptionSpec` e passando un valore di stringa che specifica il livello di tracciamento. Ad esempio, passare il valore `FINE`. Per informazioni sui diversi valori, vedete il metodo `setLogLevel` in [ Guida di riferimento delle API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. Conversione del documento

   Convertire il documento PDF in un documento PDF/A richiamando il metodo `DocConverterServiceClient` dell&#39;oggetto &lt;a1/> e passando i valori seguenti:`toPDFA`

   * L&#39;oggetto `com.adobe.idp.Document` che contiene il documento PDF da convertire
   * L&#39;oggetto `PDFAConversionOptionSpec` che specifica le informazioni di tracciamento

   Il metodo `toPDFA` restituisce un oggetto `PDFAConversionResult` che contiene il documento PDF/A.

1. Salvare il documento PDF/A

   * Recuperare il documento PDF/A richiamando il metodo `PDFAConversionResult` dell&#39;oggetto `getPDFA`. Questo metodo restituisce un oggetto `com.adobe.idp.Document` che rappresenta il documento PDF/A.
   * Creare un oggetto `java.io.File` che rappresenti il file PDF/A. Accertatevi che l’estensione del nome file sia .pdf.
   * Compilare il file con dati PDF/A richiamando il metodo `com.adobe.idp.Document` dell&#39;oggetto `copyToFile` e passando l&#39;oggetto &lt;a2/>.`java.io.File`

**Consulta anche**

[Utilizzo dei documenti PDF/A](pdf-a-documents.md#working-with-pdf-a-documents)

[Avvio rapido (modalità SOAP): Conversione di un documento in un documento PDF/A mediante l&#39;API Java](/help/forms/developing/docconverter-service-java-api-quick.md#quick-start-soap-mode-converting-a-document-to-a-pdf-a-document-using-the-java-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Convertire i documenti in documenti PDF/A utilizzando l&#39;API del servizio Web {#convert-documents-to-pdf-a-documents-using-the-web-service-api}

Convertire un documento PDF in un documento PDF/A utilizzando l&#39;API DocConverter (servizio Web):

1. Includi file di progetto

   * Creare un assembly client Microsoft .NET che utilizzi il WSDL DocConverter.
   * Fare riferimento all&#39;assembly client Microsoft .NET.

1. Creare un client DocConvert

   * Utilizzando l&#39;assembly client Microsoft .NET, creare un oggetto `DocConverterServiceService` richiamando il relativo costruttore predefinito.
   * Impostare il membro di dati `DocConverterServiceService` dell&#39;oggetto `Credentials` con un valore `System.Net.NetworkCredential` che specifica il nome utente e il valore della password.

1. Riferimento a un documento PDF da convertire in documento PDF/A

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare il documento PDF convertito in documento PDF/A.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà `System.IO.FileStream` dell&#39;oggetto `Length`.
   * Compilare l&#39;array di byte con i dati del flusso richiamando il metodo `Read` dell&#39;oggetto `System.IO.FileStream` e passando l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnandone la proprietà `binaryData` con il contenuto dell&#39;array di byte.

1. Impostazione delle informazioni di tracciamento

   * Creare un oggetto `PDFAConversionOptionSpec` utilizzando il relativo costruttore.
   * Impostare il livello di tracciamento delle informazioni assegnando un valore che specifica il livello di tracciamento al membro di dati `PDFAConversionOptionSpec` dell&#39;oggetto `logLevel`. Ad esempio, assegnare il valore `FINE` a questo membro dati.

1. Conversione del documento

   Convertire il documento PDF in un documento PDF/A richiamando il metodo `DocConverterServiceService` dell&#39;oggetto &lt;a1/> e passando i valori seguenti:`toPDFA`

   * L&#39;oggetto `BLOB` che contiene il documento PDF da convertire
   * L&#39;oggetto `PDFAConversionOptionSpec` che specifica le informazioni di tracciamento

   Il metodo `toPDFA` restituisce un oggetto `PDFAConversionResult` che contiene il documento PDF/A.

1. Salvare il documento PDF/A

   * Creare un oggetto `BLOB` che memorizza il documento PDF/A ottenendo il valore del membro di dati `PDFAConversionResult` dell&#39;oggetto `PDFADocument`.
   * Creare un array di byte che memorizza il contenuto dell&#39;oggetto `BLOB` restituito utilizzando l&#39;oggetto `PDFAConversionResult`. Compilare l&#39;array di byte ottenendo il valore del membro di dati `BLOB` dell&#39;oggetto `binaryData`.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file nel documento PDF/A.
   * Creare un oggetto `System.IO.BinaryWriter` richiamandone il costruttore e passando l&#39;oggetto `System.IO.FileStream`.
   * Scrivere il contenuto dell&#39;array di byte in un file PDF richiamando il metodo `System.IO.BinaryWriter` dell&#39;oggetto `Write` e passando l&#39;array di byte.

**Consulta anche**

[Utilizzo dei documenti PDF/A](pdf-a-documents.md#working-with-pdf-a-documents)

[Richiamo  AEM Forms con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Creazione di un assembly client .NET che utilizza la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Determinazione programmatica della conformità PDF/A {#programmatically-determining-pdf-a-compliancy}

È possibile utilizzare il servizio DocConverter per determinare se un documento PDF è conforme allo standard PDF/A. Per informazioni su un documento PDF/A e su come convertire un documento PDF in documento PDF/A, vedere [Conversione di documenti in documenti PDF/A](pdf-a-documents.md#converting-documents-to-pdf-a-documents).

>[!NOTE]
>
>Per ulteriori informazioni sul servizio DocConverter, vedere [Guida di riferimento dei servizi per  AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-1}

Per determinare la conformità PDF/A, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un client DocConvert
1. Fare riferimento a un documento PDF utilizzato per determinare la conformità PDF/A.
1. Impostare le opzioni di esecuzione.
1. Recuperare informazioni sul documento PDF.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, accertatevi di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-docconverter-client.jar
* adobe-utilities.jar (richiesto se  AEM Forms è distribuito sul server applicazioni JBoss)
* jbossall-client.jar (richiesto se  AEM Forms è distribuito sul server applicazioni JBoss)

Per informazioni sulla posizione di questi file JAR, vedere [Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un client DocConvert**

Prima di eseguire un&#39;operazione DocConverter a livello di programmazione, è necessario creare un client DocConverter. Se utilizzate l&#39;API Java, create un oggetto `DocConverterServiceClient`. Se utilizzate l&#39;API del servizio Web DocConverter, create un oggetto `DocConverterServiceService`.

**Riferimento a un documento PDF utilizzato per determinare la conformità PDF/A**

Per determinare se il documento PDF è conforme allo standard PDF/A, è necessario fare riferimento a un documento PDF e passarlo al servizio DocConverter.

**Impostazione delle opzioni di esecuzione**

È possibile impostare un&#39;opzione di esecuzione che determina la quantità di informazioni tracciate durante il processo di conversione. In altre parole, è possibile impostare nove livelli diversi per specificare quante informazioni il servizio DocConverter tiene traccia quando converte un documento PDF in un documento PDF/A.

**Recupero di informazioni sul documento PDF**

Dopo aver creato il client del servizio DocConverter, fare riferimento al documento PDF e impostare le opzioni di esecuzione, è possibile determinare se il documento PDF è conforme allo standard PDF/A.

**Consulta anche**

[Determinare la conformità PDF/A tramite l&#39;API Java](pdf-a-documents.md#determine-pdf-a-compliancy-using-the-java-api)

[Determinazione della conformità PDF/A tramite l&#39;API del servizio Web](pdf-a-documents.md#determine-pdf-a-compliancy-using-the-web-service-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Determinare la conformità PDF/A utilizzando l&#39;API Java {#determine-pdf-a-compliancy-using-the-java-api}

Determinare la conformità PDF/A utilizzando l&#39;API Java:

1. Includi file di progetto

   Includete file JAR client, ad esempio adobe-docconverter-client.jar, nel percorso di classe del progetto Java.

1. Creare un client DocConvert

   * Creare un oggetto `ServiceClientFactory` che contiene le proprietà di connessione.
   * Creare un oggetto `DocConverterServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Riferimento a un documento PDF utilizzato per determinare la conformità PDF/A

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento PDF da convertire utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del file PDF.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Impostazione delle opzioni di esecuzione

   * Creare un oggetto `PDFAValidationOptionSpec` utilizzando il relativo costruttore.
   * Impostare il livello di conformità richiamando il metodo `PDFAValidationOptionSpec` dell&#39;oggetto `setCompliance` e passando `PDFAValidationOptionSpec.Compliance.PDFA_1B`.
   * Impostare il livello di tracciamento delle informazioni richiamando il metodo `setLogLevel` dell&#39;oggetto `PDFAValidationOptionSpec` e passando un valore di stringa che specifica il livello di tracciamento. Ad esempio, passare il valore `FINE`. Per informazioni sui diversi valori, vedete il metodo `setLogLevel` in [ Guida di riferimento delle API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. Recupero di informazioni sul documento PDF

   Determinare la conformità PDF/A richiamando il metodo `DocConverterServiceClient` dell&#39;oggetto &lt;a1/> e passando i valori seguenti:`isPDFA`

   * L&#39;oggetto `com.adobe.idp.Document` che contiene il documento PDF.
   * L&#39;oggetto `PDFAValidationOptionSpec` che specifica le opzioni di esecuzione.

   Il metodo `isPDFA` restituisce un oggetto `PDFAValidationResult` che contiene i risultati dell&#39;operazione.

**Consulta anche**

[Utilizzo dei documenti PDF/A](pdf-a-documents.md#working-with-pdf-a-documents)

[Avvio rapido (modalità SOAP): Determinazione della conformità PDF/A tramite l&#39;API Java](/help/forms/developing/docconverter-service-java-api-quick.md#quick-start-soap-mode-determining-pdf-a-compliancy-using-the-java-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Determinare la conformità PDF/A utilizzando l&#39;API del servizio Web {#determine-pdf-a-compliancy-using-the-web-service-api}

Determinare la conformità PDF/A utilizzando l&#39;API del servizio Web:

1. Includi file di progetto

   * Creare un assembly client Microsoft .NET che utilizzi il WSDL DocConverter.
   * Fare riferimento all&#39;assembly client Microsoft .NET.

1. Creare un client DocConvert

   * Utilizzando l&#39;assembly client Microsoft .NET, creare un oggetto `DocConverterServiceService` richiamando il relativo costruttore predefinito.
   * Impostare il membro di dati `DocConverterServiceService` dell&#39;oggetto `Credentials` con un valore `System.Net.NetworkCredential` che specifica il nome utente e il valore della password.

1. Riferimento a un documento PDF utilizzato per determinare la conformità PDF/A

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare il documento PDF convertito in documento PDF/A.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà `System.IO.FileStream` dell&#39;oggetto `Length`.
   * Compilare l&#39;array di byte con i dati del flusso richiamando il metodo `Read` dell&#39;oggetto `System.IO.FileStream` e passando l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnandone la proprietà `binaryData` con il contenuto dell&#39;array di byte.

1. Impostazione delle opzioni di esecuzione

   * Creare un oggetto `PDFAValidationOptionSpec` utilizzando il relativo costruttore.
   * Impostare il livello di conformità assegnando al membro di dati `PDFAValidationOptionSpec` dell&#39;oggetto `compliance` il valore &lt;a2/>.`PDFAConversionOptionSpec_Compliance.PDFA_1B`
   * Impostare il livello di tracciamento delle informazioni assegnando il membro di dati `PDFAValidationOptionSpec` dell&#39;oggetto con il valore `resultLevel`.`PDFAValidationOptionSpec_ResultLevel.DETAILED`

1. Recupero di informazioni sul documento PDF

   Determinare la conformità PDF/A richiamando il metodo `DocConverterServiceService` dell&#39;oggetto &lt;a1/> e passando i valori seguenti:`isPDFA`

   * L&#39;oggetto `BLOB` che contiene il documento PDF.
   * L&#39;oggetto `PDFAValidationOptionSpec` che contiene le opzioni di esecuzione.

   Il metodo `isPDFA` restituisce un oggetto `PDFAValidationResult` che contiene i risultati dell&#39;operazione.

**Consulta anche**

[Utilizzo dei documenti PDF/A](pdf-a-documents.md#working-with-pdf-a-documents)

[Richiamo  AEM Forms con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Creazione di un assembly client .NET che utilizza la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)
