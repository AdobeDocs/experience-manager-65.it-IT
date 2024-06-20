---
title: Determinare Se I Documenti Sono Conformi A PDF/A
description: Utilizza il servizio Assembler per determinare se un documento PDF è compatibile con PDF/A utilizzando l’API Java e l’API del servizio Web.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 096fd2ac-616f-484a-b093-9d98b2f87093
solution: Experience Manager, Experience Manager Forms
source-git-commit: 872e2de411f51b5f0b26a2ff47cb49f01313d39f
workflow-type: tm+mt
source-wordcount: '2065'
ht-degree: 2%

---

# Determinare Se I Documenti Sono Conformi A PDF/A {#determining-whether-documents-are-pdf-a-compliant}

È possibile determinare se un documento PDF è compatibile con PDF/A utilizzando il servizio Assembler. Un documento PDF/A esiste come formato di archiviazione destinato alla conservazione a lungo termine del contenuto del documento. I font vengono incorporati nel documento e il file non è compresso. Di conseguenza, un documento PDF/A è generalmente più grande di un documento PDF standard. Inoltre, un documento PDF/A non include contenuti audio e video.

La specifica PDF/A-1 è costituita da due livelli di conformità, ovvero A e B. La differenza principale tra i due livelli è il supporto della struttura logica (accessibilità), che non è richiesto per il livello di conformità B. Indipendentemente dal livello di conformità, PDF/A-1 impone che tutti i font siano incorporati all&#39;interno del documento PDF/A generato. Al momento, solo PDF/A-1b è supportato nella convalida (e nella conversione).

Ai fini della presente discussione, si supponga che venga utilizzato il seguente documento DDX.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
         <DocumentInformation source="Loan.pdf" result="Loan_result.xml">
         <PDFAValidation compliance="PDF/A-1b" resultLevel="Detailed"                       ignoreUnusedResources="true" allowCertificationSignatures="true" />
     </DocumentInformation>
 </DDX>
```

In questo documento DDX, il `DocumentInformation` indica al servizio Assembler di restituire informazioni sul documento di input PDF. All&#39;interno del `DocumentInformation` elemento, l&#39; `PDFAValidation` indica al servizio Assembler di indicare se il documento di input PDF è compatibile con PDF/A.

Il servizio Assembler restituisce informazioni che specificano se il documento PDF di input è conforme a PDF/A all&#39;interno di un documento XML che contiene un `PDFAConformance` elemento. Se il documento di input PDF è compatibile con PDF/A, il valore di `PDFAConformance` dell&#39;elemento `isCompliant` l&#39;attributo è `true`. Se il documento PDF non è conforme a PDF/A, il valore di `PDFAConformance` dell&#39;elemento `isCompliant` l&#39;attributo è `false`.

>[!NOTE]
>
>Poiché il documento DDX specificato in questa sezione contiene `DocumentInformation` , il servizio Assembler restituisce dati XML anziché un documento PDF. In altre parole, il servizio Assembler non assembla o disassembla un documento PDF, ma restituisce informazioni sul documento PDF di input all&#39;interno di un documento XML.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Assembler, vedere [Guida di riferimento dei servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Per ulteriori informazioni su un documento DDX, vedere [Servizio assemblatore e riferimento DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Riepilogo dei passaggi {#summary-of-steps}

Per determinare se un documento di PDF è compatibile con PDF/A, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Creare un client PDF Assembler.
1. Fare riferimento a un documento DDX esistente.
1. Fai riferimento a un documento PDF utilizzato per determinare la conformità di PDF/A.
1. Impostare le opzioni di runtime.
1. Recuperare informazioni sul documento PDF.
1. Salva il documento XML restituito.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso della classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è implementato su JBoss)
* jbossall-client.jar (obbligatorio se AEM Forms è distribuito su JBoss)

se AEM Forms viene distribuito su un server applicazioni J2EE supportato diverso da JBoss, è necessario sostituire i file adobe-utilities.jar e jbossall-client.jar con file JAR specifici per il server applicazioni J2EE su cui è distribuito AEM Forms. Per informazioni sulla posizione di tutti i file JAR di AEM Forms, vedi [Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un client PDF Assembler**

Prima di poter eseguire un&#39;operazione Assembler a livello di programmazione, è necessario creare un client del servizio Assembler.

**Riferimento a un documento DDX esistente**

Per eseguire un&#39;operazione del servizio Assembler, è necessario fare riferimento a un documento DDX. Per determinare se un documento PDF di input è conforme a PDF/A, verificare che il documento DDX contenga `PDFAValidation` elemento in un `DocumentInformation` elemento. Il `PDFAValidation` indica al servizio Assembler di restituire un documento XML che specifica se il documento di input PDF è conforme a PDF/A.

**Riferimento a un documento PDF utilizzato per determinare la conformità PDF/A**

È necessario fare riferimento a un documento PDF e passarlo al servizio Assembler per determinare se il documento PDF è compatibile con PDF/A.

**Impostare le opzioni di runtime**

È possibile impostare le opzioni di runtime che controllano il comportamento del servizio Assembler durante l&#39;esecuzione di un processo. È ad esempio possibile impostare un&#39;opzione che indichi al servizio Assembler di continuare l&#39;elaborazione di un processo in caso di errore. Per informazioni sulle opzioni di runtime impostabili, vedere `AssemblerOptionSpec` riferimento di classe in [Riferimento API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Recuperare informazioni sul documento PDF**

Dopo aver creato il client del servizio Assembler, aver fatto riferimento al documento DDX, aver creato un riferimento a un documento interattivo di PDF e aver impostato le opzioni di runtime, è possibile richiamare `invokeDDX` operazione. Poiché il documento DDX contiene `DocumentInformation` , il servizio Assembler restituisce dati XML anziché un documento PDF.

**Salva il documento XML restituito**

Il documento XML restituito dal servizio Assembler specifica se il documento PDF di input è compatibile con PDF/A. Se, ad esempio, il documento di input PDF non è compatibile con PDF/A, il servizio Assembler restituisce un documento XML contenente l&#39;elemento seguente:

```xml
 <PDFAConformance isCompliant="false" compliance="PDF/A-1b" resultLevel="Detailed" ignoreUnusedResources="true" allowCertificationSignatures="true">
```

Salvare il documento XML come file XML in modo da poter aprire il file e visualizzare i risultati.

**Consulta anche**

[Determinare se un documento è conforme a PDF/A utilizzando l’API Java](/help/forms/developing/determining-whether-documents-pdf-a.md#determine-whether-a-document-is-pdf-a-compliant-using-the-java-api)

[Determinare se un documento è conforme a PDF/A utilizzando l’API del servizio web](/help/forms/developing/determining-whether-documents-pdf-a.md#determine-whether-a-document-is-pdf-a-compliant-using-the-web-service-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Assemblaggio di documenti PDF a livello di programmazione](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Determinare se un documento è conforme a PDF/A utilizzando l’API Java {#determine-whether-a-document-is-pdf-a-compliant-using-the-java-api}

Determinare se un documento PDF è conforme a PDF/A utilizzando l&#39;API del servizio Assembler (Java):

1. Includi file di progetto.

   Includi i file JAR client, come adobe-assembler-client.jar, nel percorso di classe del progetto Java.

1. Creare un client PDF Assembler.

   * Creare un `ServiceClientFactory` oggetto che contiene proprietà di connessione.
   * Creare un `AssemblerServiceClient` mediante il costruttore e passando il `ServiceClientFactory` oggetto.

1. Fare riferimento a un documento DDX esistente.

   * Creare un `java.io.FileInputStream` oggetto che rappresenta il documento DDX utilizzando il relativo costruttore e passando un valore stringa che specifica la posizione del file DDX. Per determinare se il documento PDF è compatibile con PDF/A, verificare che il documento DDX contenga `PDFAValidation` elemento contenuto in un elemento `DocumentInformation` elemento.
   * Creare un `com.adobe.idp.Document` mediante il costruttore e passando il `java.io.FileInputStream` oggetto.

1. Fai riferimento a un documento PDF utilizzato per determinare la conformità di PDF/A.

   * Creare un `java.io.FileInputStream` mediante il costruttore e passando la posizione di un documento PDF utilizzato per determinare la conformità PDF/A.
   * Creare un `com.adobe.idp.Document` mediante il costruttore e passando il `java.io.FileInputStream` oggetto che contiene il documento PDF.
   * Creare un `java.util.Map` oggetto utilizzato per memorizzare il documento di input PDF utilizzando un `HashMap` costruttore.
   * Aggiungi una voce al `java.util.Map` oggetto richiamando il relativo `put` e fornendo i seguenti argomenti:

      * Valore stringa che rappresenta il nome della chiave. Questo valore deve corrispondere al valore dell&#39;elemento di origine specificato nel documento DDX. Ad esempio, il valore dell&#39;elemento di origine nel documento DDX introdotto in questa sezione è Loan.pdf.
      * A `com.adobe.idp.Document` oggetto che contiene il documento di input PDF.

1. Impostare le opzioni di runtime.

   * Creare un `AssemblerOptionSpec` oggetto che memorizza le opzioni di runtime mediante il relativo costruttore.
   * Impostare le opzioni di runtime per soddisfare i requisiti aziendali richiamando un metodo che appartiene al `AssemblerOptionSpec` oggetto. Ad esempio, per indicare al servizio Assembler di continuare l&#39;elaborazione di un processo quando si verifica un errore, richiamare `AssemblerOptionSpec` dell&#39;oggetto `setFailOnError` metodo e passaggio `false`.

1. Recuperare informazioni sul documento PDF.

   Richiama `AssemblerServiceClient` dell&#39;oggetto `invokeDDX` e trasmettere i seguenti valori richiesti:

   * A `com.adobe.idp.Document` oggetto che rappresenta il documento DDX da utilizzare
   * A `java.util.Map` oggetto contenente il file PDF di input utilizzato per determinare la conformità di PDF/A
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` oggetto che specifica le opzioni di runtime

   Il `invokeDDX` il metodo restituisce un `com.adobe.livecycle.assembler.client.AssemblerResult` oggetto che contiene dati XML che specifica se il documento di input PDF è compatibile con PDF/A.

1. Salva il documento XML restituito.

   Per ottenere dati XML che specificano se il documento PDF di input è un documento PDF/A, effettuare le seguenti operazioni:

   * Richiama `AssemblerResult` dell&#39;oggetto `getDocuments` metodo. Questo restituisce un `java.util.Map` oggetto.
   * Effettua iterazione attraverso `java.util.Map` finché non viene individuato il risultato `com.adobe.idp.Document` oggetto.
   * Richiama `com.adobe.idp.Document` dell&#39;oggetto `copyToFile` per estrarre il documento XML. Assicurarsi di salvare i dati XML come file XML.

**Consulta anche**

[Guida rapida (modalità SOAP): determinare se un documento è conforme a PDF/A utilizzando l’API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-determining-whether-a-document-is-pdf-a-compliant-using-the-java-api) (modalità SOAP)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Determinare se un documento è conforme a PDF/A utilizzando l’API del servizio web {#determine-whether-a-document-is-pdf-a-compliant-using-the-web-service-api}

Determina se un documento PDF è conforme a PDF/A utilizzando l’API del servizio Assembler (servizio web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l’indirizzo IP del server che ospita AEM Forms.

1. Creare un client PDF Assembler.

   * Creare un `AssemblerServiceClient` utilizzando il costruttore predefinito.
   * Creare un `AssemblerServiceClient.Endpoint.Address` oggetto utilizzando `System.ServiceModel.EndpointAddress` costruttore. Passa un valore stringa che specifica il file WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). Non è necessario utilizzare il `lc_version` attributo. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Creare un `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto ottenendo il valore del `AssemblerServiceClient.Endpoint.Binding` campo. Invia il valore restituito a `BasicHttpBinding`.
   * Imposta il `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegna al campo il nome utente dei moduli AEM `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore password corrispondente al campo `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Fare riferimento a un documento DDX esistente.

   * Creare un `BLOB` mediante il costruttore. Il `BLOB` viene utilizzato per memorizzare il documento DDX.
   * Creare un `System.IO.FileStream` richiamando il relativo costruttore e passando un valore stringa che rappresenta la posizione del file del documento DDX e la modalità di apertura del file in.
   * Creare una matrice di byte che memorizza il contenuto della `System.IO.FileStream` oggetto. È possibile determinare le dimensioni della matrice di byte ottenendo `System.IO.FileStream` dell&#39;oggetto `Length` proprietà.
   * Compilare la matrice di byte con i dati di flusso richiamando `System.IO.FileStream` dell&#39;oggetto `Read` e passando la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare il `BLOB` oggetto assegnando il relativo `MTOM` con il contenuto della matrice di byte.

1. Fai riferimento a un documento PDF utilizzato per determinare la conformità di PDF/A.

   * Creare un `BLOB` mediante il costruttore. Il `BLOB` L&#39;oggetto viene utilizzato per memorizzare il documento di input PDF.
   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore stringa che rappresenta la posizione del file del documento di input PDF e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto della `System.IO.FileStream` oggetto. È possibile determinare le dimensioni della matrice di byte ottenendo `System.IO.FileStream` dell&#39;oggetto `Length` proprietà.
   * Compilare la matrice di byte con i dati di flusso richiamando `System.IO.FileStream` dell&#39;oggetto `Read` e passando la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare il `BLOB` oggetto assegnando il relativo `MTOM` con il contenuto della matrice di byte.
   * Creare un `MyMapOf_xsd_string_To_xsd_anyType` oggetto. Questo oggetto insieme viene utilizzato per memorizzare il documento PDF.
   * Creare un `MyMapOf_xsd_string_To_xsd_anyType_Item` oggetto.
   * Assegna un valore stringa che rappresenta il nome della chiave al `MyMapOf_xsd_string_To_xsd_anyType_Item` dell&#39;oggetto `key` campo. Questo valore deve corrispondere al valore dell&#39;elemento di origine PDF specificato nel documento DDX.
   * Assegna la `BLOB` oggetto che memorizza il documento PDF in `MyMapOf_xsd_string_To_xsd_anyType_Item` dell&#39;oggetto `value` campo.
   * Aggiungi il `MyMapOf_xsd_string_To_xsd_anyType_Item` oggetto al `MyMapOf_xsd_string_To_xsd_anyType` oggetto. Richiama `MyMapOf_xsd_string_To_xsd_anyType` oggetto&#39; `Add` e trasmettere il `MyMapOf_xsd_string_To_xsd_anyType` oggetto.

1. Impostare le opzioni di runtime.

   * Creare un `AssemblerOptionSpec` oggetto che memorizza le opzioni di runtime mediante il relativo costruttore.
   * Impostare le opzioni di runtime per soddisfare i requisiti aziendali assegnando un valore a un membro dati che appartiene al `AssemblerOptionSpec` oggetto. Ad esempio, per indicare al servizio Assembler di continuare l&#39;elaborazione di un processo quando si verifica un errore, assegnare `false` al `AssemblerOptionSpec` dell&#39;oggetto `failOnError` membro dati.

1. Recuperare informazioni sul documento PDF.

   Richiama `AssemblerServiceService` dell&#39;oggetto `invoke` e trasmettere i seguenti valori:

   * A `BLOB` oggetto che rappresenta il documento DDX.
   * Il `MyMapOf_xsd_string_To_xsd_anyType` oggetto che contiene il documento di input PDF. Le chiavi devono corrispondere ai nomi dei file di origine di PDF e i relativi valori devono essere `BLOB` oggetto che corrisponde al file PDF di input.
   * Un `AssemblerOptionSpec` oggetto che specifica le opzioni di runtime.

   Il `invoke` il metodo restituisce un `AssemblerResult` oggetto che contiene dati XML che specifica se il documento PDF di input è un documento PDF/A.

1. Salva il documento XML restituito.

   Per ottenere dati XML che specificano se il documento PDF di input è un documento PDF/A, effettuare le seguenti operazioni:

   * Accedere a `AssemblerResult` dell&#39;oggetto `documents` campo, che è un `Map` oggetto contenente i dati XML che specifica se il documento PDF di input è un documento PDF/A.
   * Effettua iterazione attraverso `Map` per ottenere ogni documento risultante. Quindi, esegui il cast del valore del membro dell’array su un `BLOB`.
   * Estrarre i dati binari che rappresentano i dati XML accedendo ai relativi `BLOB` dell&#39;oggetto `MTOM` campo. In questo campo viene memorizzata una matrice di byte che è possibile scrivere come file XML.

**Consulta anche**

[Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
