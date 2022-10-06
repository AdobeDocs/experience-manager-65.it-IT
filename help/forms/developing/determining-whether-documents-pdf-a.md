---
title: Determinare Se I Documenti Sono Conformi A PDF/A
seo-title: Determining Whether Documents Are PDF/A-Compliant
description: Utilizza il servizio Assembler per determinare se un documento PDF è conforme a PDF/A utilizzando l’API Java e l’API Web Service.
seo-description: Use the Assembler service to determine if a PDF document is PDF/A-compliant using the Java API and Web Service API.
uuid: 4e9d8c8f-2153-411b-9c4b-2d14b3c8f4bb
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: c429d6e1-7847-43c8-bf75-cb0078dbb9d5
role: Developer
exl-id: 096fd2ac-616f-484a-b093-9d98b2f87093
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2082'
ht-degree: 0%

---

# Determinare Se I Documenti Sono Conformi A PDF/A {#determining-whether-documents-are-pdf-a-compliant}

È possibile determinare se un documento PDF è conforme a PDF/A utilizzando il servizio Assembler. Un documento PDF/A esiste come formato di archiviazione per la conservazione a lungo termine del contenuto del documento. I font vengono incorporati nel documento e il file non è compresso. Di conseguenza, un documento PDF/A è generalmente più grande di un documento PDF standard. Inoltre, un documento PDF/A non contiene contenuto audio e video.

La specifica PDF/A-1 è costituita da due livelli di conformità, ovvero A e B. La differenza principale tra i due livelli è rappresentata dal supporto della struttura logica (accessibilità), che non è necessario per il livello di conformità B. Indipendentemente dal livello di conformità, PDF/A-1 determina che tutti i font sono incorporati nel documento PDF/A generato. Al momento, la convalida (e la conversione) supporta solo PDF/A-1b.

Ai fini di questa discussione, si supponga che venga utilizzato il seguente documento DDX.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
         <DocumentInformation source="Loan.pdf" result="Loan_result.xml">
         <PDFAValidation compliance="PDF/A-1b" resultLevel="Detailed"                       ignoreUnusedResources="true" allowCertificationSignatures="true" />
     </DocumentInformation>
 </DDX>
```

All&#39;interno di questo documento DDX, il `DocumentInformation` indica al servizio Assembler di restituire informazioni sul documento di input PDF. All&#39;interno di `DocumentInformation` l&#39;elemento `PDFAValidation` indica al servizio Assembler se il documento di input PDF è conforme a PDF/A.

Il servizio Assembler restituisce informazioni che specificano se il documento di input PDF è conforme a PDF/A all&#39;interno di un documento XML contenente un `PDFAConformance` elemento. Se il documento PDF di input è conforme a PDF/A, il valore della `PDFAConformance` dell’elemento `isCompliant` attributo `true`. Se il documento PDF non è conforme a PDF/A, il valore della `PDFAConformance` dell’elemento `isCompliant` attributo `false`.

>[!NOTE]
>
>Perché il documento DDX specificato in questa sezione contiene un `DocumentInformation` Il servizio Assembler restituisce i dati XML anziché un documento PDF. In altre parole, il servizio Assembler non assembla o smonta un documento PDF; restituisce informazioni sul documento di input PDF all&#39;interno di un documento XML.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Assembler, vedere [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Per ulteriori informazioni su un documento DDX, consulta [Servizio di assemblaggio e riferimento DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Riepilogo dei passaggi {#summary-of-steps}

Per determinare se un documento PDF è conforme a PDF/A, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Creare un client PDF Assembler.
1. Fai riferimento a un documento DDX esistente.
1. Fare riferimento a un documento PDF utilizzato per determinare la conformità di PDF/A.
1. Impostare le opzioni di esecuzione.
1. Recupera informazioni sul documento PDF.
1. Salvare il documento XML restituito.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso della classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è distribuito su JBoss)
* jbossall-client.jar (richiesto se AEM Forms è distribuito su JBoss)

se AEM Forms è implementato su un server applicazioni J2EE supportato diverso da JBoss, è necessario sostituire i file adobe-utilities.jar e jbossall-client.jar con file JAR specifici per il server applicazioni J2EE in cui è implementato AEM Forms. Per informazioni sulla posizione di tutti i file JAR di AEM Forms, vedi [Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un client PDF Assembler**

Prima di poter eseguire un&#39;operazione Assembler a livello di programmazione, è necessario creare un client di servizio Assembler.

**Riferimento a un documento DDX esistente**

Per eseguire un&#39;operazione del servizio Assembler, è necessario fare riferimento a un documento DDX. Per determinare se un documento di input PDF è conforme a PDF/A, assicurati che il documento DDX contenga `PDFAValidation` elemento all’interno di un `DocumentInformation` elemento. La `PDFAValidation` indica al servizio Assembler di restituire un documento XML che specifica se il documento di input PDF è conforme a PDF/A.

**Riferimento a un documento PDF utilizzato per determinare la conformità di PDF/A**

Per determinare se il documento PDF è conforme a PDF/A, è necessario fare riferimento a un documento PDF e passarlo al servizio Assembler.

**Impostare le opzioni di esecuzione**

È possibile impostare le opzioni di esecuzione che controllano il comportamento del servizio Assembler mentre esegue un processo. Ad esempio, è possibile impostare un&#39;opzione che indica al servizio Assembler di continuare l&#39;elaborazione di un processo in caso di errore. Per informazioni sulle opzioni di esecuzione che è possibile impostare, vedere la `AssemblerOptionSpec` riferimento di classe in [Riferimento API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Recupera informazioni sul documento PDF**

Dopo aver creato il client di servizio Assembler, fare riferimento al documento DDX, fare riferimento a un documento PDF interattivo e impostare le opzioni di esecuzione, è possibile richiamare `invokeDDX` funzionamento. Poiché il documento DDX contiene `DocumentInformation` Il servizio Assembler restituisce i dati XML anziché un documento PDF.

**Salvare il documento XML restituito**

Il documento XML restituito dal servizio Assembler specifica se il documento di input PDF è conforme a PDF/A. Ad esempio, se il documento di input PDF non è conforme a PDF/A, il servizio Assembler restituisce un documento XML contenente il seguente elemento:

```xml
 <PDFAConformance isCompliant="false" compliance="PDF/A-1b" resultLevel="Detailed" ignoreUnusedResources="true" allowCertificationSignatures="true">
```

Salvare il documento XML come file XML in modo da poter aprire il file e visualizzare i risultati.

**Consulta anche**

[Determinare se un documento è conforme a PDF/A utilizzando l’API Java](/help/forms/developing/determining-whether-documents-pdf-a.md#determine-whether-a-document-is-pdf-a-compliant-using-the-java-api)

[Determinare se un documento è conforme a PDF/A utilizzando l’API del servizio Web](/help/forms/developing/determining-whether-documents-pdf-a.md#determine-whether-a-document-is-pdf-a-compliant-using-the-web-service-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Assemblaggio di documenti PDF a livello di programmazione](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Determinare se un documento è conforme a PDF/A utilizzando l’API Java {#determine-whether-a-document-is-pdf-a-compliant-using-the-java-api}

Determinare se un documento PDF è conforme a PDF/A utilizzando l’API del servizio Assembler (Java):

1. Includi file di progetto.

   Includi file JAR client, come adobe-assembler-client.jar, nel percorso di classe del progetto Java.

1. Creare un client PDF Assembler.

   * Crea un `ServiceClientFactory` oggetto contenente le proprietà di connessione.
   * Crea un `AssemblerServiceClient` utilizzando il relativo costruttore e passando `ServiceClientFactory` oggetto.

1. Fai riferimento a un documento DDX esistente.

   * Crea un `java.io.FileInputStream` oggetto che rappresenta il documento DDX utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del file DDX. Per determinare se il documento PDF è conforme a PDF/A, assicurati che il documento DDX contenga `PDFAValidation` elemento contenuto in un `DocumentInformation` elemento.
   * Crea un `com.adobe.idp.Document` utilizzando il relativo costruttore e passando `java.io.FileInputStream` oggetto.

1. Fare riferimento a un documento PDF utilizzato per determinare la conformità di PDF/A.

   * Crea un `java.io.FileInputStream` utilizzando il relativo costruttore e passando la posizione di un documento PDF utilizzato per determinare la conformità di PDF/A.
   * Crea un `com.adobe.idp.Document` utilizzando il relativo costruttore e passando `java.io.FileInputStream` oggetto contenente il documento PDF.
   * Crea un `java.util.Map` oggetto utilizzato per memorizzare il documento di input PDF utilizzando un `HashMap` costruttore.
   * Aggiungi una voce al `java.util.Map` richiamandone l&#39;oggetto `put` e passare gli argomenti seguenti:

      * Valore stringa che rappresenta il nome della chiave. Questo valore deve corrispondere al valore dell&#39;elemento di origine specificato nel documento DDX. Ad esempio, il valore dell&#39;elemento di origine situato nel documento DDX introdotto in questa sezione è Loan.pdf.
      * A `com.adobe.idp.Document` oggetto contenente il documento di input PDF.

1. Impostare le opzioni di esecuzione.

   * Crea un `AssemblerOptionSpec` oggetto che memorizza le opzioni di esecuzione utilizzando il relativo costruttore.
   * Impostare le opzioni di esecuzione per soddisfare i requisiti aziendali richiamando un metodo che appartiene al `AssemblerOptionSpec` oggetto. Ad esempio, per dare istruzioni al servizio Assembler di continuare a elaborare un processo quando si verifica un errore, richiama il `AssemblerOptionSpec` dell’oggetto `setFailOnError` metodo e passaggio `false`.

1. Recupera informazioni sul documento PDF.

   Richiama il `AssemblerServiceClient` dell’oggetto `invokeDDX` e trasmettere i seguenti valori richiesti:

   * A `com.adobe.idp.Document` oggetto che rappresenta il documento DDX da utilizzare
   * A `java.util.Map` oggetto contenente il file PDF di input utilizzato per determinare la conformità di PDF/A
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` oggetto che specifica le opzioni di esecuzione

   La `invokeDDX` restituisce un `com.adobe.livecycle.assembler.client.AssemblerResult` oggetto contenente dati XML che specifica se il documento di input PDF è conforme a PDF/A.

1. Salvare il documento XML restituito.

   Per ottenere i dati XML che specificano se il documento di input PDF è un documento PDF/A, eseguire le operazioni seguenti:

   * Richiama il `AssemblerResult` dell’oggetto `getDocuments` metodo . Questo restituisce un `java.util.Map` oggetto.
   * Itera attraverso il `java.util.Map` finché non trovi il risultato `com.adobe.idp.Document` oggetto.
   * Richiama il `com.adobe.idp.Document` dell’oggetto `copyToFile` per estrarre il documento XML. Assicurarsi di salvare i dati XML come file XML.

**Consulta anche**

[Avvio rapido (modalità SOAP): Determinare se un documento è conforme a PDF/A utilizzando l’API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-determining-whether-a-document-is-pdf-a-compliant-using-the-java-api) (modalità SOAP)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Determinare se un documento è conforme a PDF/A utilizzando l’API del servizio Web {#determine-whether-a-document-is-pdf-a-compliant-using-the-web-service-api}

Determinare se un documento PDF è conforme a PDF/A utilizzando l&#39;API del servizio Assembler (servizio Web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurati di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l’indirizzo IP del server che ospita AEM Forms.

1. Creare un client PDF Assembler.

   * Crea un `AssemblerServiceClient` utilizzando il relativo costruttore predefinito.
   * Crea un `AssemblerServiceClient.Endpoint.Address` utilizzando `System.ServiceModel.EndpointAddress` costruttore. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). Non è necessario utilizzare il `lc_version` attributo. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Crea un `System.ServiceModel.BasicHttpBinding` ottenendo il valore del `AssemblerServiceClient.Endpoint.Binding` campo . Imposta il valore restituito su `BasicHttpBinding`.
   * Imposta la `System.ServiceModel.BasicHttpBinding` dell’oggetto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegnare il nome utente del modulo di AEM al campo `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore della password corrispondente al campo `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Fai riferimento a un documento DDX esistente.

   * Crea un `BLOB` utilizzando il relativo costruttore. La `BLOB` viene utilizzato per memorizzare il documento DDX.
   * Crea un `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento DDX e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto del `System.IO.FileStream` oggetto. È possibile determinare le dimensioni dell&#39;array di byte ottenendo il `System.IO.FileStream` dell’oggetto `Length` proprietà.
   * Compilare l&#39;array di byte con i dati del flusso richiamando il `System.IO.FileStream` dell’oggetto `Read` e passare l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare `BLOB` oggetto assegnando il relativo `MTOM` con il contenuto dell&#39;array di byte.

1. Fare riferimento a un documento PDF utilizzato per determinare la conformità di PDF/A.

   * Crea un `BLOB` utilizzando il relativo costruttore. La `BLOB` viene utilizzato per memorizzare il documento di input PDF.
   * Crea un `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento di input PDF e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto del `System.IO.FileStream` oggetto. È possibile determinare le dimensioni dell&#39;array di byte ottenendo il `System.IO.FileStream` dell’oggetto `Length` proprietà.
   * Compilare l&#39;array di byte con i dati del flusso richiamando il `System.IO.FileStream` dell’oggetto `Read` e passare l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare `BLOB` oggetto assegnando il relativo `MTOM` con il contenuto dell&#39;array di byte.
   * Crea un `MyMapOf_xsd_string_To_xsd_anyType` oggetto. Questo oggetto raccolta viene utilizzato per memorizzare il documento PDF.
   * Crea un `MyMapOf_xsd_string_To_xsd_anyType_Item` oggetto.
   * Assegna un valore stringa che rappresenta il nome della chiave al `MyMapOf_xsd_string_To_xsd_anyType_Item` dell&#39;oggetto `key` campo . Questo valore deve corrispondere al valore dell&#39;elemento di origine PDF specificato nel documento DDX.
   * Assegna `BLOB` oggetto che memorizza il documento PDF nella `MyMapOf_xsd_string_To_xsd_anyType_Item` dell&#39;oggetto `value` campo .
   * Aggiungi il `MyMapOf_xsd_string_To_xsd_anyType_Item` dell&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType` oggetto. Richiama il `MyMapOf_xsd_string_To_xsd_anyType` object&#39; `Add` e passare il `MyMapOf_xsd_string_To_xsd_anyType` oggetto.

1. Impostare le opzioni di esecuzione.

   * Crea un `AssemblerOptionSpec` oggetto che memorizza le opzioni di esecuzione utilizzando il relativo costruttore.
   * Impostare le opzioni di esecuzione per soddisfare i requisiti aziendali assegnando un valore a un membro dati che appartiene al `AssemblerOptionSpec` oggetto. Ad esempio, per dare istruzioni al servizio Assembler di continuare a elaborare un processo quando si verifica un errore, assegnare `false` al `AssemblerOptionSpec` dell’oggetto `failOnError` membro dati.

1. Recupera informazioni sul documento PDF.

   Richiama il `AssemblerServiceService` dell’oggetto `invoke` e passare i seguenti valori:

   * A `BLOB` oggetto che rappresenta il documento DDX.
   * La `MyMapOf_xsd_string_To_xsd_anyType` oggetto contenente il documento di input PDF. Le chiavi devono corrispondere ai nomi dei file di origine di PDF e i relativi valori devono essere `BLOB` che corrisponde al file di input PDF.
   * Un `AssemblerOptionSpec` oggetto che specifica le opzioni di esecuzione.

   La `invoke` restituisce un `AssemblerResult` oggetto contenente dati XML che specifica se il documento di input PDF è un documento PDF/A.

1. Salvare il documento XML restituito.

   Per ottenere i dati XML che specificano se il documento di input PDF è un documento PDF/A, eseguire le operazioni seguenti:

   * Accedere al `AssemblerResult` dell&#39;oggetto `documents` un campo `Map` oggetto che contiene i dati XML che specifica se il documento di input PDF è un documento PDF/A.
   * Itera attraverso il `Map` per ottenere ogni documento risultante. Quindi, eseguire il cast del valore del membro dell&#39;array su un `BLOB`.
   * Estrarre i dati binari che rappresentano i dati XML accedendo ai relativi `BLOB` dell&#39;oggetto `MTOM` campo . Questo campo memorizza una matrice di byte che è possibile scrivere come file XML.

**Consulta anche**

[Richiamo di AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
