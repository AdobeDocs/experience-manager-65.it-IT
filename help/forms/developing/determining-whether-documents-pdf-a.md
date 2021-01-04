---
title: Determinazione Della Conformità Dei Documenti Con PDF/A
seo-title: Determinazione Della Conformità Dei Documenti Con PDF/A
description: Utilizzate il servizio Assembler per determinare se un documento PDF è conforme allo standard PDF/A tramite l'API Java e l'API del servizio Web.
seo-description: Utilizzate il servizio Assembler per determinare se un documento PDF è conforme allo standard PDF/A tramite l'API Java e l'API del servizio Web.
uuid: 4e9d8c8f-2153-411b-9c4b-2d14b3c8f4bb
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: c429d6e1-7847-43c8-bf75-cb0078dbb9d5
translation-type: tm+mt
source-git-commit: 07889ead2ae402b5fb738ca08c7efe076ef33e44
workflow-type: tm+mt
source-wordcount: '2109'
ht-degree: 0%

---


# Determinare se i documenti sono conformi allo standard PDF/A {#determining-whether-documents-are-pdf-a-compliant}

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

In questo documento DDX, l&#39;elemento `DocumentInformation` indica al servizio Assembler di restituire informazioni sul documento PDF di input. All&#39;interno dell&#39;elemento `DocumentInformation`, l&#39;elemento `PDFAValidation` indica al servizio Assembler se il documento PDF di input è conforme allo standard PDF/A.

Il servizio Assembler restituisce informazioni che specificano se il documento PDF di input è conforme allo standard PDF/A in un documento XML contenente un elemento `PDFAConformance`. Se il documento PDF di input è conforme allo standard PDF/A, il valore dell&#39;attributo `PDFAConformance` dell&#39;elemento `isCompliant` è &lt;a2/>. `true` Se il documento PDF non è conforme allo standard PDF/A, il valore dell&#39;attributo `PDFAConformance` dell&#39;elemento `isCompliant` è &lt;a2/>.`false`

>[!NOTE]
>
>Poiché il documento DDX specificato in questa sezione contiene un elemento `DocumentInformation`, il servizio Assembler restituisce dati XML invece di un documento PDF. In altre parole, il servizio Assembler non assembla né smonta un documento PDF; restituisce informazioni sul documento PDF di input all&#39;interno di un documento XML.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Assembler, vedere [Guida di riferimento dei servizi per  AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Per ulteriori informazioni su un documento DDX, vedere [Servizio Assembler e Riferimento DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

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
* adobe-utilities.jar (richiesto se  AEM Forms è distribuito su JBoss)
* jbossall-client.jar (richiesto se  AEM Forms è distribuito su JBoss)

se  AEM Forms è distribuito su un server applicazione J2EE supportato diverso da JBoss, è necessario sostituire i file adobe-utilities.jar e jbossall-client.jar con file JAR specifici del server applicazione J2EE in cui  AEM Forms è distribuito. Per informazioni sulla posizione di tutti  file AEM Forms JAR, vedere [Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un client Assembler PDF**

Prima di eseguire un&#39;operazione Assembler a livello di programmazione, è necessario creare un client di servizio Assembler.

**Riferimento a un documento DDX esistente**

Per eseguire un&#39;operazione del servizio Assembler, è necessario fare riferimento a un documento DDX. Per determinare se un documento PDF di input è conforme allo standard PDF/A, assicurarsi che il documento DDX contenga l&#39;elemento `PDFAValidation` all&#39;interno di un elemento `DocumentInformation`. L&#39;elemento `PDFAValidation` indica al servizio Assembler di restituire un documento XML che specifica se il documento PDF di input è conforme allo standard PDF/A.

**Riferimento a un documento PDF utilizzato per determinare la conformità PDF/A**

Per determinare se il documento PDF è conforme allo standard PDF/A, è necessario fare riferimento a un documento PDF e passarlo al servizio Assembler.

**Impostazione delle opzioni di esecuzione**

È possibile impostare opzioni di esecuzione che controllano il comportamento del servizio Assembler mentre esegue un processo. Ad esempio, potete impostare un&#39;opzione che indichi al servizio Assembler di continuare l&#39;elaborazione di un processo in caso di errore. Per informazioni sulle opzioni di esecuzione che è possibile impostare, vedere il riferimento alla classe `AssemblerOptionSpec` in [ Guida di riferimento delle API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Recupero di informazioni sul documento PDF**

Dopo aver creato il client del servizio Assembler, fatto riferimento al documento DDX, fatto riferimento a un documento PDF interattivo e impostato le opzioni di esecuzione, è possibile richiamare l&#39;operazione `invokeDDX`. Poiché il documento DDX contiene l&#39;elemento `DocumentInformation`, il servizio Assembler restituisce dati XML anziché un documento PDF.

**Salvare il documento XML restituito**

Il documento XML restituito dal servizio Assembler specifica se il documento PDF di input è conforme allo standard PDF/A. Ad esempio, se il documento PDF di input non è conforme allo standard PDF/A, il servizio Assembler restituisce un documento XML contenente il seguente elemento:

```xml
 <PDFAConformance isCompliant="false" compliance="PDF/A-1b" resultLevel="Detailed" ignoreUnusedResources="true" allowCertificationSignatures="true">
```

Salvare il documento XML come file XML in modo da poter aprire il file e visualizzare i risultati.

**Consulta anche**

[Determinare se un documento è conforme allo standard PDF/A tramite l&#39;API Java](/help/forms/developing/determining-whether-documents-pdf-a.md#determine-whether-a-document-is-pdf-a-compliant-using-the-java-api)

[Determinare se un documento è conforme allo standard PDF/A utilizzando l&#39;API del servizio Web](/help/forms/developing/determining-whether-documents-pdf-a.md#determine-whether-a-document-is-pdf-a-compliant-using-the-web-service-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Assemblaggio di documenti PDF a livello di programmazione](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Determinare se un documento è conforme allo standard PDF/A utilizzando l&#39;API Java {#determine-whether-a-document-is-pdf-a-compliant-using-the-java-api}

Determinare se un documento PDF è conforme allo standard PDF/A utilizzando l&#39;API di Assembler Service (Java):

1. Includere i file di progetto.

   Includete file JAR client, ad esempio adobe-assembler-client.jar, nel percorso di classe del progetto Java.

1. Creare un client Assembler PDF.

   * Creare un oggetto `ServiceClientFactory` che contiene le proprietà di connessione.
   * Creare un oggetto `AssemblerServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Fare riferimento a un documento DDX esistente.

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento DDX utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del file DDX. Per determinare se il documento PDF è conforme allo standard PDF/A, assicurarsi che il documento DDX contenga l&#39;elemento `PDFAValidation` contenuto all&#39;interno di un elemento `DocumentInformation`.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Fare riferimento a un documento PDF utilizzato per determinare la conformità PDF/A.

   * Creare un oggetto `java.io.FileInputStream` utilizzando il relativo costruttore e passando la posizione di un documento PDF utilizzata per determinare la conformità PDF/A.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream` che contiene il documento PDF.
   * Creare un oggetto `java.util.Map` utilizzato per memorizzare il documento PDF di input utilizzando un costruttore `HashMap`.
   * Aggiungere una voce all&#39;oggetto `java.util.Map` richiamandone il metodo `put` e trasmettendo gli argomenti seguenti:

      * Un valore di stringa che rappresenta il nome della chiave. Questo valore deve corrispondere al valore dell&#39;elemento di origine specificato nel documento DDX. Ad esempio, il valore dell&#39;elemento di origine presente nel documento DDX introdotto in questa sezione è Loan.pdf.
      * Un oggetto `com.adobe.idp.Document` che contiene il documento PDF di input.

1. Impostare le opzioni di esecuzione.

   * Creare un oggetto `AssemblerOptionSpec` che memorizza le opzioni di esecuzione utilizzando il relativo costruttore.
   * Impostate le opzioni di runtime per soddisfare i requisiti aziendali richiamando un metodo che appartiene all&#39;oggetto `AssemblerOptionSpec`. Ad esempio, per indicare al servizio Assembler di continuare a elaborare un processo quando si verifica un errore, richiamare il metodo `AssemblerOptionSpec` dell&#39;oggetto `setFailOnError` e passare `false`.

1. Recuperare informazioni sul documento PDF.

   Richiamare il metodo `AssemblerServiceClient` dell&#39;oggetto `invokeDDX` e trasmettere i seguenti valori obbligatori:

   * Un oggetto `com.adobe.idp.Document` che rappresenta il documento DDX da utilizzare
   * Un oggetto `java.util.Map` contenente il file PDF di input utilizzato per determinare la conformità PDF/A
   * Un oggetto `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` che specifica le opzioni di esecuzione

   Il metodo `invokeDDX` restituisce un oggetto `com.adobe.livecycle.assembler.client.AssemblerResult` contenente dati XML che specifica se il documento PDF di input è conforme allo standard PDF/A.

1. Salvare il documento XML restituito.

   Per ottenere dati XML che specificano se il documento PDF di input è un documento PDF/A, effettuare le seguenti operazioni:

   * Richiamare il metodo `AssemblerResult` dell&#39;oggetto `getDocuments`. Questo restituisce un oggetto `java.util.Map`.
   * Iterate l&#39;oggetto `java.util.Map` fino a individuare l&#39;oggetto `com.adobe.idp.Document` risultante.
   * Richiamare il metodo `com.adobe.idp.Document` dell&#39;oggetto `copyToFile` per estrarre il documento XML. Assicurarsi di salvare i dati XML come file XML.

**Consulta anche**

[Avvio rapido (modalità SOAP): Determinazione della conformità di un documento PDF/A tramite l&#39;API](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-determining-whether-a-document-is-pdf-a-compliant-using-the-java-api)  Java (modalità SOAP)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Determinare se un documento è conforme allo standard PDF/A utilizzando l&#39;API del servizio Web {#determine-whether-a-document-is-pdf-a-compliant-using-the-web-service-api}

Determinare se un documento PDF è conforme allo standard PDF/A utilizzando l&#39;API di Assembler Service (servizio Web):

1. Includere i file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituire `localhost` con l&#39;indirizzo IP del server che ospita  AEM Forms.

1. Creare un client Assembler PDF.

   * Creare un oggetto `AssemblerServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `AssemblerServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passate un valore di stringa che specifica il WSDL al servizio AEM Forms  (ad esempio, `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). Non è necessario utilizzare l&#39;attributo `lc_version`. Questo attributo viene utilizzato quando create un riferimento a un servizio.
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `AssemblerServiceClient.Endpoint.Binding`. Inserite il valore restituito in `BasicHttpBinding`.
   * Impostare il campo `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto `MessageEncoding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilitate l&#39;autenticazione HTTP di base eseguendo le seguenti operazioni:

      * Assegnare il nome utente del modulo AEM al campo `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Fare riferimento a un documento DDX esistente.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare il documento DDX.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento DDX e la modalità in cui aprire il file.
   * Creare un array di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà `System.IO.FileStream` dell&#39;oggetto `Length`.
   * Compilare l&#39;array di byte con i dati del flusso richiamando il metodo `Read` dell&#39;oggetto `System.IO.FileStream` e passando l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando il relativo campo `MTOM` con il contenuto dell&#39;array di byte.

1. Fare riferimento a un documento PDF utilizzato per determinare la conformità PDF/A.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare il documento PDF di input.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF di input e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà `System.IO.FileStream` dell&#39;oggetto `Length`.
   * Compilare l&#39;array di byte con i dati del flusso richiamando il metodo `Read` dell&#39;oggetto `System.IO.FileStream` e passando l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnandone la proprietà `MTOM` con il contenuto dell&#39;array di byte.
   * Creare un oggetto `MyMapOf_xsd_string_To_xsd_anyType`. Questo oggetto raccolta viene utilizzato per memorizzare il documento PDF.
   * Creare un oggetto `MyMapOf_xsd_string_To_xsd_anyType_Item`.
   * Assegnare un valore di stringa che rappresenta il nome chiave al campo `MyMapOf_xsd_string_To_xsd_anyType_Item` dell&#39;oggetto `key`. Questo valore deve corrispondere al valore dell&#39;elemento di origine PDF specificato nel documento DDX.
   * Assegnare l&#39;oggetto `BLOB` che memorizza il documento PDF nel campo `MyMapOf_xsd_string_To_xsd_anyType_Item` dell&#39;oggetto `value`.
   * Aggiungere l&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType_Item` all&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType`. Richiamare il metodo `MyMapOf_xsd_string_To_xsd_anyType` object&#39; `Add` e passare l&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType`.

1. Impostare le opzioni di esecuzione.

   * Creare un oggetto `AssemblerOptionSpec` che memorizza le opzioni di esecuzione utilizzando il relativo costruttore.
   * Impostare le opzioni di runtime per soddisfare i requisiti aziendali assegnando un valore a un membro di dati che appartiene all&#39;oggetto `AssemblerOptionSpec`. Ad esempio, per indicare al servizio Assembler di continuare l&#39;elaborazione di un processo in caso di errore, assegnare `false` al membro di dati `AssemblerOptionSpec` dell&#39;oggetto `failOnError`.

1. Recuperare informazioni sul documento PDF.

   Richiamare il metodo `AssemblerServiceService` dell&#39;oggetto `invoke` e trasmettere i seguenti valori:

   * Un oggetto `BLOB` che rappresenta il documento DDX.
   * L&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType` che contiene il documento PDF di input. Le chiavi devono corrispondere ai nomi dei file sorgente PDF e i relativi valori devono essere l&#39;oggetto `BLOB` che corrisponde al file PDF di input.
   * Un oggetto `AssemblerOptionSpec` che specifica le opzioni di esecuzione.

   Il metodo `invoke` restituisce un oggetto `AssemblerResult` contenente dati XML che specifica se il documento PDF di input è un documento PDF/A.

1. Salvare il documento XML restituito.

   Per ottenere dati XML che specificano se il documento PDF di input è un documento PDF/A, effettuare le seguenti operazioni:

   * Accedere al campo `documents` dell&#39;oggetto `AssemblerResult`, che è un oggetto `Map` contenente i dati XML che specifica se il documento PDF di input è un documento PDF/A.
   * Iterate l&#39;oggetto `Map` per ottenere ogni documento risultante. Quindi, inserire il valore del membro della matrice in un elemento `BLOB`.
   * Estrarre i dati binari che rappresentano i dati XML accedendo al relativo campo `BLOB` dell&#39;oggetto `MTOM`. Questo campo memorizza un array di byte che è possibile scrivere come file XML.

**Consulta anche**

[Chiamata  AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
