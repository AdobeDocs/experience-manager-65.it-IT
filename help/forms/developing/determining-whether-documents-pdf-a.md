---
title: Determinazione Della Conformità Dei Documenti Con PDF/A
seo-title: Determinazione Della Conformità Dei Documenti Con PDF/A
description: 'null'
seo-description: 'null'
uuid: 4e9d8c8f-2153-411b-9c4b-2d14b3c8f4bb
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: c429d6e1-7847-43c8-bf75-cb0078dbb9d5
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '2069'
ht-degree: 0%

---


# Determinazione Della Conformità Dei Documenti Con PDF/A {#determining-whether-documents-are-pdf-a-compliant}

È possibile determinare se un documento PDF è conforme allo standard PDF/A utilizzando il servizio Assembler. Un documento PDF/A esiste come formato di archiviazione per la conservazione a lungo termine del contenuto del documento. I font vengono incorporati nel documento e il file non viene compresso. Di conseguenza, un documento PDF/A è generalmente più grande di un documento PDF standard. Inoltre, un documento PDF/A non contiene contenuto audio e video.

La specifica PDF/A-1 è costituita da due livelli di conformità, ossia A e B. La differenza principale tra i due livelli è rappresentata dal supporto della struttura logica (accessibilità), che non è richiesto per il livello di conformità B. Indipendentemente dal livello di conformità, PDF/A-1 stabilisce che tutti i font sono incorporati nel documento PDF/A generato. Al momento, è supportato solo PDF/A-1b per la convalida (e la conversione).

Ai fini di questa discussione, si supponga di utilizzare il seguente documento DDX.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
         <DocumentInformation source="Loan.pdf" result="Loan_result.xml">
         <PDFAValidation compliance="PDF/A-1b" resultLevel="Detailed"                       ignoreUnusedResources="true" allowCertificationSignatures="true" />
     </DocumentInformation>
 </DDX>
```

In questo documento DDX, l&#39; `DocumentInformation` elemento indica al servizio Assembler di restituire informazioni sul documento PDF di input. All&#39;interno dell&#39; `DocumentInformation` elemento, l&#39; `PDFAValidation` elemento indica al servizio Assembler se il documento PDF di input è conforme allo standard PDF/A.

Il servizio Assembler restituisce informazioni che specificano se il documento PDF di input è conforme allo standard PDF/A in un documento XML contenente un `PDFAConformance` elemento. Se il documento PDF di input è conforme allo standard PDF/A, il valore dell&#39; `PDFAConformance` attributo dell&#39; `isCompliant` elemento è `true`. Se il documento PDF non è conforme allo standard PDF/A, il valore dell&#39; `PDFAConformance` attributo dell&#39; `isCompliant` elemento è `false`.

>[!NOTE]
>
>Poiché il documento DDX specificato in questa sezione contiene un `DocumentInformation` elemento, il servizio Assembler restituisce dati XML anziché un documento PDF. In altre parole, il servizio Assembler non assembla né smonta un documento PDF; restituisce informazioni sul documento PDF di input all&#39;interno di un documento XML.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Assembler, vedere Riferimento [servizi per i AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Per ulteriori informazioni su un documento DDX, vedere Servizio [Assembler e Riferimento](https://www.adobe.com/go/learn_aemforms_ddx_63)DDX.

## Riepilogo dei passaggi {#summary-of-steps}

Per determinare se un documento PDF è conforme allo standard PDF/A, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un client Assembler PDF.
1. Fare riferimento a un documento DDX esistente.
1. Fare riferimento a un documento PDF utilizzato per determinare la conformità PDF/A.
1. Impostare le opzioni di esecuzione.
1. Recuperare informazioni sul documento PDF.
1. Salvare il documento XML restituito.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, accertatevi di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (richiesto se i AEM Forms sono distribuiti su JBoss)
* jbossall-client.jar (richiesto se i AEM Forms sono distribuiti su JBoss)

se i AEM Forms sono distribuiti su un server applicazione J2EE supportato diverso da JBoss, è necessario sostituire i file adobe-utilities.jar e jbossall-client.jar con file JAR specifici del server applicazione J2EE in cui sono distribuiti i AEM Forms. Per informazioni sulla posizione di tutti i file JAR AEM Forms, vedere [Inclusione di file](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)libreria Java AEM Forms.

**Creare un client Assembler PDF**

Prima di eseguire un&#39;operazione Assembler a livello di programmazione, è necessario creare un client di servizio Assembler.

**Riferimento a un documento DDX esistente**

Per eseguire un&#39;operazione del servizio Assembler, è necessario fare riferimento a un documento DDX. Per determinare se un documento PDF di input è conforme allo standard PDF/A, assicurarsi che il documento DDX contenga l&#39; `PDFAValidation` elemento all&#39;interno di un `DocumentInformation` elemento. L&#39; `PDFAValidation` elemento indica al servizio Assembler di restituire un documento XML che specifica se il documento PDF di input è conforme allo standard PDF/A.

**Riferimento a un documento PDF utilizzato per determinare la conformità PDF/A**

Per determinare se il documento PDF è conforme allo standard PDF/A, è necessario fare riferimento a un documento PDF e passarlo al servizio Assembler.

**Impostazione delle opzioni di esecuzione**

È possibile impostare opzioni di esecuzione che controllano il comportamento del servizio Assembler mentre esegue un processo. Ad esempio, potete impostare un&#39;opzione che indichi al servizio Assembler di continuare l&#39;elaborazione di un processo in caso di errore. Per informazioni sulle opzioni di esecuzione che è possibile impostare, vedere il riferimento alla `AssemblerOptionSpec` classe in Riferimento API per [AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Recupero di informazioni sul documento PDF**

Dopo aver creato il client del servizio Assembler, fatto riferimento al documento DDX, fatto riferimento a un documento PDF interattivo e impostato le opzioni di esecuzione, è possibile richiamare l&#39; `invokeDDX` operazione. Poiché il documento DDX contiene l&#39; `DocumentInformation` elemento, il servizio Assembler restituisce dati XML invece di un documento PDF.

**Salvare il documento XML restituito**

Il documento XML restituito dal servizio Assembler specifica se il documento PDF di input è conforme allo standard PDF/A. Ad esempio, se il documento PDF di input non è conforme allo standard PDF/A, il servizio Assembler restituisce un documento XML contenente il seguente elemento:

```xml
 <PDFAConformance isCompliant="false" compliance="PDF/A-1b" resultLevel="Detailed" ignoreUnusedResources="true" allowCertificationSignatures="true">
```

Salvare il documento XML come file XML in modo da poter aprire il file e visualizzare i risultati.

**Consulta anche**

[Determinare se un documento è conforme allo standard PDF/A tramite l&#39;API Java](/help/forms/developing/determining-whether-documents-pdf-a.md#determine-whether-a-document-is-pdf-a-compliant-using-the-java-api)

[Determinare se un documento è conforme allo standard PDF/A utilizzando l&#39;API del servizio Web](/help/forms/developing/determining-whether-documents-pdf-a.md#determine-whether-a-document-is-pdf-a-compliant-using-the-web-service-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Assemblaggio di documenti PDF a livello di programmazione](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Determinare se un documento è conforme allo standard PDF/A tramite l&#39;API Java {#determine-whether-a-document-is-pdf-a-compliant-using-the-java-api}

Determinare se un documento PDF è conforme allo standard PDF/A utilizzando l&#39;API di Assembler Service (Java):

1. Includere i file di progetto.

   Includete file JAR client, ad esempio adobe-assembler-client.jar, nel percorso di classe del progetto Java.

1. Creare un client Assembler PDF.

   * Creare un `ServiceClientFactory` oggetto che contenga proprietà di connessione.
   * Creare un `AssemblerServiceClient` oggetto utilizzando il relativo costruttore e passando l&#39; `ServiceClientFactory` oggetto.

1. Fare riferimento a un documento DDX esistente.

   * Creare un `java.io.FileInputStream` oggetto che rappresenta il documento DDX utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del file DDX. Per determinare se il documento PDF è conforme allo standard PDF/A, assicurarsi che il documento DDX contenga l&#39; `PDFAValidation` elemento contenuto all&#39;interno di un `DocumentInformation` elemento.
   * Creare un `com.adobe.idp.Document` oggetto utilizzando il relativo costruttore e passando l&#39; `java.io.FileInputStream` oggetto.

1. Fare riferimento a un documento PDF utilizzato per determinare la conformità PDF/A.

   * Creare un `java.io.FileInputStream` oggetto utilizzando il relativo costruttore e passando la posizione di un documento PDF utilizzato per determinare la conformità PDF/A.
   * Creare un `com.adobe.idp.Document` oggetto utilizzando il relativo costruttore e passando l&#39; `java.io.FileInputStream` oggetto che contiene il documento PDF.
   * Creare un oggetto `java.util.Map` utilizzato per memorizzare il documento PDF di input utilizzando un `HashMap` costruttore.
   * Aggiungere una voce all&#39; `java.util.Map` oggetto richiamandone il `put` metodo e passando gli argomenti seguenti:

      * Un valore di stringa che rappresenta il nome della chiave. Questo valore deve corrispondere al valore dell&#39;elemento di origine specificato nel documento DDX. Ad esempio, il valore dell&#39;elemento di origine presente nel documento DDX introdotto in questa sezione è Loan.pdf.
      * Un `com.adobe.idp.Document` oggetto che contiene il documento PDF di input.

1. Impostare le opzioni di esecuzione.

   * Creare un `AssemblerOptionSpec` oggetto che memorizza le opzioni di esecuzione utilizzando il relativo costruttore.
   * Impostate le opzioni di runtime per soddisfare i requisiti aziendali richiamando un metodo che appartiene all&#39; `AssemblerOptionSpec` oggetto. Ad esempio, per indicare al servizio Assembler di continuare a elaborare un processo quando si verifica un errore, richiamare il metodo dell&#39; `AssemblerOptionSpec` oggetto `setFailOnError` e passare `false`.

1. Recuperare informazioni sul documento PDF.

   Richiamare il metodo dell&#39; `AssemblerServiceClient` oggetto `invokeDDX` e trasmettere i seguenti valori obbligatori:

   * Un `com.adobe.idp.Document` oggetto che rappresenta il documento DDX da utilizzare
   * Un `java.util.Map` oggetto che contiene il file PDF di input utilizzato per determinare la conformità PDF/A
   * Un `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` oggetto che specifica le opzioni di esecuzione

   Il `invokeDDX` metodo restituisce un `com.adobe.livecycle.assembler.client.AssemblerResult` oggetto contenente dati XML che specifica se il documento PDF di input è conforme allo standard PDF/A.

1. Salvare il documento XML restituito.

   Per ottenere dati XML che specificano se il documento PDF di input è un documento PDF/A, effettuare le seguenti operazioni:

   * Richiama il metodo dell’ `AssemblerResult` oggetto `getDocuments` . Questo restituisce un `java.util.Map` oggetto.
   * Eseguire un&#39;iterazione sull&#39; `java.util.Map` oggetto fino a individuare l&#39; `com.adobe.idp.Document` oggetto risultante.
   * Richiamare il metodo dell&#39; `com.adobe.idp.Document` oggetto `copyToFile` per estrarre il documento XML. Assicurarsi di salvare i dati XML come file XML.

**Consulta anche**

[Avvio rapido (modalità SOAP): Determinazione della conformità di un documento PDF/A tramite l&#39;API](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-determining-whether-a-document-is-pdf-a-compliant-using-the-java-api) Java (modalità SOAP)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Determinare se un documento è conforme allo standard PDF/A utilizzando l&#39;API del servizio Web {#determine-whether-a-document-is-pdf-a-compliant-using-the-web-service-api}

Determinare se un documento PDF è conforme allo standard PDF/A utilizzando l&#39;API di Assembler Service (servizio Web):

1. Includere i file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituire `localhost` con l&#39;indirizzo IP del server host AEM Forms.

1. Creare un client Assembler PDF.

   * Creare un `AssemblerServiceClient` oggetto utilizzando il relativo costruttore predefinito.
   * Creare un `AssemblerServiceClient.Endpoint.Address` oggetto utilizzando il `System.ServiceModel.EndpointAddress` costruttore. Passate un valore di stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). Non è necessario utilizzare l&#39; `lc_version` attributo. Questo attributo viene utilizzato quando create un riferimento a un servizio.
   * Creare un `System.ServiceModel.BasicHttpBinding` oggetto ottenendo il valore del `AssemblerServiceClient.Endpoint.Binding` campo. Inserite il valore restituito in `BasicHttpBinding`.
   * Impostare il campo `System.ServiceModel.BasicHttpBinding` dell&#39; `MessageEncoding` oggetto su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilitate l&#39;autenticazione HTTP di base eseguendo le seguenti operazioni:

      * Assegnare il nome utente dei moduli AEM al campo `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Fare riferimento a un documento DDX esistente.

   * Creare un `BLOB` oggetto utilizzando il relativo costruttore. L&#39; `BLOB` oggetto viene utilizzato per memorizzare il documento DDX.
   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento DDX e la modalità in cui aprire il file.
   * Creare un array di byte che memorizza il contenuto dell&#39; `System.IO.FileStream` oggetto. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà dell&#39; `System.IO.FileStream` oggetto `Length` .
   * Compilare l&#39;array di byte con i dati del flusso richiamando il `System.IO.FileStream` `Read` metodo dell&#39;oggetto e passando l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39; `BLOB` oggetto assegnandone `MTOM` il campo con il contenuto dell&#39;array di byte.

1. Fare riferimento a un documento PDF utilizzato per determinare la conformità PDF/A.

   * Creare un `BLOB` oggetto utilizzando il relativo costruttore. L&#39; `BLOB` oggetto viene utilizzato per memorizzare il documento PDF di input.
   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF di input e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto dell&#39; `System.IO.FileStream` oggetto. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà dell&#39; `System.IO.FileStream` oggetto `Length` .
   * Compilare l&#39;array di byte con i dati del flusso richiamando il `System.IO.FileStream` `Read` metodo dell&#39;oggetto e passando l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39; `BLOB` oggetto assegnandone `MTOM` la proprietà con il contenuto dell&#39;array di byte.
   * Create a `MyMapOf_xsd_string_To_xsd_anyType` object. Questo oggetto raccolta viene utilizzato per memorizzare il documento PDF.
   * Create a `MyMapOf_xsd_string_To_xsd_anyType_Item` object.
   * Assegnare un valore di stringa che rappresenta il nome chiave al campo dell&#39; `MyMapOf_xsd_string_To_xsd_anyType_Item` oggetto `key` . Questo valore deve corrispondere al valore dell&#39;elemento di origine PDF specificato nel documento DDX.
   * Assegnare l&#39; `BLOB` oggetto che memorizza il documento PDF nel campo dell&#39; `MyMapOf_xsd_string_To_xsd_anyType_Item` oggetto `value` .
   * Aggiungere l&#39; `MyMapOf_xsd_string_To_xsd_anyType_Item` oggetto all&#39; `MyMapOf_xsd_string_To_xsd_anyType` oggetto. Richiamare il metodo `MyMapOf_xsd_string_To_xsd_anyType` dell&#39;oggetto `Add` e passare l&#39; `MyMapOf_xsd_string_To_xsd_anyType` oggetto.

1. Impostare le opzioni di esecuzione.

   * Creare un `AssemblerOptionSpec` oggetto che memorizza le opzioni di esecuzione utilizzando il relativo costruttore.
   * Impostare le opzioni di runtime per soddisfare i requisiti aziendali assegnando un valore a un membro di dati che appartiene all&#39; `AssemblerOptionSpec` oggetto. Ad esempio, per indicare al servizio Assembler di continuare l&#39;elaborazione di un processo in caso di errore, assegnare `false` al membro `AssemblerOptionSpec` dati dell&#39; `failOnError` oggetto.

1. Recuperare informazioni sul documento PDF.

   Richiama il metodo dell’ `AssemblerServiceService` oggetto `invoke` e passa i seguenti valori:

   * Un `BLOB` oggetto che rappresenta il documento DDX.
   * L&#39; `MyMapOf_xsd_string_To_xsd_anyType` oggetto che contiene il documento PDF di input. Le chiavi devono corrispondere ai nomi dei file sorgente PDF e i relativi valori devono essere l&#39; `BLOB` oggetto che corrisponde al file PDF di input.
   * Un `AssemblerOptionSpec` oggetto che specifica le opzioni di esecuzione.

   Il `invoke` metodo restituisce un `AssemblerResult` oggetto contenente dati XML che specifica se il documento PDF di input è un documento PDF/A.

1. Salvare il documento XML restituito.

   Per ottenere dati XML che specificano se il documento PDF di input è un documento PDF/A, effettuare le seguenti operazioni:

   * Accedere al campo dell&#39; `AssemblerResult` oggetto `documents` , ovvero un `Map` oggetto che contiene i dati XML che specifica se il documento PDF di input è un documento PDF/A.
   * Eseguire un&#39;iterazione sull&#39; `Map` oggetto per ottenere ogni documento risultante. Quindi, proiettare il valore del membro dell&#39;array su un `BLOB`.
   * Estrarre i dati binari che rappresentano i dati XML accedendo al campo `BLOB` dell&#39;oggetto `MTOM` . Questo campo memorizza un array di byte che è possibile scrivere come file XML.

**Consulta anche**

[Chiamata di AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
