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
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
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

In questo documento DDX, l&#39;elemento `DocumentInformation` indica al servizio Assembler di restituire informazioni sul documento PDF di input. All&#39;interno dell&#39;elemento `DocumentInformation`, l&#39;elemento `PDFAValidation` indica al servizio Assembler di indicare se il documento PDF di input è conforme a PDF/A.

Il servizio Assembler restituisce informazioni che specificano se il documento PDF di input è conforme a PDF/A all&#39;interno di un documento XML che contiene un elemento `PDFAConformance`. Se il documento PDF di input è compatibile con PDF/A, il valore dell&#39;attributo `isCompliant` dell&#39;elemento `PDFAConformance` è `true`. Se il documento PDF non è conforme a PDF/A, il valore dell&#39;attributo `isCompliant` dell&#39;elemento `PDFAConformance` è `false`.

>[!NOTE]
>
>Poiché il documento DDX specificato in questa sezione contiene un elemento `DocumentInformation`, il servizio Assembler restituisce dati XML anziché un documento PDF. In altre parole, il servizio Assembler non assembla o disassembla un documento PDF, ma restituisce informazioni sul documento PDF di input all&#39;interno di un documento XML.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Assembler, vedere [Riferimento ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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

se AEM Forms viene distribuito su un server applicazioni J2EE supportato diverso da JBoss, è necessario sostituire i file adobe-utilities.jar e jbossall-client.jar con file JAR specifici per il server applicazioni J2EE su cui è distribuito AEM Forms. Per informazioni sulla posizione di tutti i file JAR di AEM Forms, vedi [Inclusi i file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un client Assembler PDF**

Prima di poter eseguire un&#39;operazione Assembler a livello di programmazione, è necessario creare un client del servizio Assembler.

**Riferimento a un documento DDX esistente**

Per eseguire un&#39;operazione del servizio Assembler, è necessario fare riferimento a un documento DDX. Per determinare se un documento PDF di input è compatibile con PDF/A, verificare che il documento DDX contenga l&#39;elemento `PDFAValidation` all&#39;interno di un elemento `DocumentInformation`. L&#39;elemento `PDFAValidation` indica al servizio Assembler di restituire un documento XML che specifica se il documento PDF di input è conforme a PDF/A.

**Fai riferimento a un documento PDF utilizzato per determinare la conformità di PDF/A**

È necessario fare riferimento a un documento PDF e passarlo al servizio Assembler per determinare se il documento PDF è compatibile con PDF/A.

**Impostare le opzioni di runtime**

È possibile impostare le opzioni di runtime che controllano il comportamento del servizio Assembler durante l&#39;esecuzione di un processo. È ad esempio possibile impostare un&#39;opzione che indichi al servizio Assembler di continuare l&#39;elaborazione di un processo in caso di errore. Per informazioni sulle opzioni di runtime che è possibile impostare, vedere il riferimento alla classe `AssemblerOptionSpec` in [Riferimento API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Recupera informazioni sul documento PDF**

Dopo aver creato il client del servizio Assembler, aver fatto riferimento al documento DDX, aver fatto riferimento a un documento interattivo di PDF e aver impostato le opzioni di runtime, è possibile richiamare l&#39;operazione `invokeDDX`. Poiché il documento DDX contiene l&#39;elemento `DocumentInformation`, il servizio Assembler restituisce dati XML anziché un documento PDF.

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

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `AssemblerServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Fare riferimento a un documento DDX esistente.

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento DDX utilizzando il relativo costruttore e passando un valore stringa che specifica la posizione del file DDX. Per determinare se il documento PDF è conforme a PDF/A, verificare che il documento DDX contenga l&#39;elemento `PDFAValidation` contenuto in un elemento `DocumentInformation`.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Fai riferimento a un documento PDF utilizzato per determinare la conformità di PDF/A.

   * Creare un oggetto `java.io.FileInputStream` utilizzando il relativo costruttore e passando il percorso di un documento PDF utilizzato per determinare la conformità PDF/A.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream` che contiene il documento PDF.
   * Creare un oggetto `java.util.Map` utilizzato per memorizzare il documento di input PDF utilizzando un costruttore `HashMap`.
   * Aggiungere una voce all&#39;oggetto `java.util.Map` richiamando il relativo metodo `put` e passando i seguenti argomenti:

      * Valore stringa che rappresenta il nome della chiave. Questo valore deve corrispondere al valore dell&#39;elemento di origine specificato nel documento DDX. Ad esempio, il valore dell&#39;elemento di origine nel documento DDX introdotto in questa sezione è Loan.pdf.
      * Oggetto `com.adobe.idp.Document` contenente il documento PDF di input.

1. Impostare le opzioni di runtime.

   * Creare un oggetto `AssemblerOptionSpec` che memorizza le opzioni di runtime utilizzando il relativo costruttore.
   * Impostare le opzioni di runtime per soddisfare i requisiti aziendali richiamando un metodo che appartiene all&#39;oggetto `AssemblerOptionSpec`. Ad esempio, per indicare al servizio Assembler di continuare a elaborare un processo quando si verifica un errore, richiamare il metodo `setFailOnError` dell&#39;oggetto `AssemblerOptionSpec` e passare `false`.

1. Recuperare informazioni sul documento PDF.

   Richiama il metodo `invokeDDX` dell&#39;oggetto `AssemblerServiceClient` e passa i seguenti valori richiesti:

   * Oggetto `com.adobe.idp.Document` che rappresenta il documento DDX da utilizzare
   * Oggetto `java.util.Map` contenente il file PDF di input utilizzato per determinare la conformità di PDF/A
   * Oggetto `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` che specifica le opzioni di runtime

   Il metodo `invokeDDX` restituisce un oggetto `com.adobe.livecycle.assembler.client.AssemblerResult` che contiene dati XML che specifica se il documento PDF di input è conforme a PDF/A.

1. Salva il documento XML restituito.

   Per ottenere dati XML che specificano se il documento PDF di input è un documento PDF/A, effettuare le seguenti operazioni:

   * Richiama il metodo `getDocuments` dell&#39;oggetto `AssemblerResult`. Restituisce un oggetto `java.util.Map`.
   * Scorrere l&#39;oggetto `java.util.Map` fino a trovare l&#39;oggetto `com.adobe.idp.Document` risultante.
   * Richiama il metodo `copyToFile` dell&#39;oggetto `com.adobe.idp.Document` per estrarre il documento XML. Assicurarsi di salvare i dati XML come file XML.

**Consulta anche**

[Guida rapida (modalità SOAP): verifica della conformità di un documento a PDF/A tramite l&#39;API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-determining-whether-a-document-is-pdf-a-compliant-using-the-java-api) (modalità SOAP)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Determinare se un documento è conforme a PDF/A utilizzando l’API del servizio web {#determine-whether-a-document-is-pdf-a-compliant-using-the-web-service-api}

Determina se un documento PDF è conforme a PDF/A utilizzando l’API del servizio Assembler (servizio web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Creare un client PDF Assembler.

   * Creare un oggetto `AssemblerServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `AssemblerServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). Non è necessario utilizzare l&#39;attributo `lc_version`. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `AssemblerServiceClient.Endpoint.Binding`. Eseguire il cast del valore restituito in `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegnare il nome utente dei moduli AEM al campo `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Fare riferimento a un documento DDX esistente.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per archiviare il documento DDX.
   * Creare un oggetto `System.IO.FileStream` richiamandone il costruttore e passando un valore stringa che rappresenta la posizione del file del documento DDX e la modalità di apertura del file in.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni della matrice di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare la matrice di byte con i dati di flusso richiamando il metodo `Read` dell&#39;oggetto `System.IO.FileStream` e passando la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando il relativo campo `MTOM` al contenuto della matrice di byte.

1. Fai riferimento a un documento PDF utilizzato per determinare la conformità di PDF/A.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare il documento PDF di input.
   * Creare un oggetto `System.IO.FileStream` richiamandone il costruttore e passando un valore stringa che rappresenta la posizione del file del documento PDF di input e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni della matrice di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare la matrice di byte con i dati di flusso richiamando il metodo `Read` dell&#39;oggetto `System.IO.FileStream` e passando la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando la relativa proprietà `MTOM` al contenuto della matrice di byte.
   * Creare un oggetto `MyMapOf_xsd_string_To_xsd_anyType`. Questo oggetto insieme viene utilizzato per memorizzare il documento PDF.
   * Creare un oggetto `MyMapOf_xsd_string_To_xsd_anyType_Item`.
   * Assegnare un valore stringa che rappresenta il nome chiave al campo `key` dell&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType_Item`. Questo valore deve corrispondere al valore dell&#39;elemento di origine PDF specificato nel documento DDX.
   * Assegnare l&#39;oggetto `BLOB` che memorizza il documento PDF al campo `value` dell&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType_Item`.
   * Aggiungere l&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType_Item` all&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType`. Richiama il metodo `Add` dell&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType` e passa l&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType`.

1. Impostare le opzioni di runtime.

   * Creare un oggetto `AssemblerOptionSpec` che memorizza le opzioni di runtime utilizzando il relativo costruttore.
   * Impostare le opzioni di runtime per soddisfare i requisiti aziendali assegnando un valore a un membro dati che appartiene all&#39;oggetto `AssemblerOptionSpec`. Ad esempio, per indicare al servizio Assembler di continuare a elaborare un processo quando si verifica un errore, assegnare `false` al membro dati `failOnError` dell&#39;oggetto `AssemblerOptionSpec`.

1. Recuperare informazioni sul documento PDF.

   Richiama il metodo `invoke` dell&#39;oggetto `AssemblerServiceService` e passa i seguenti valori:

   * Oggetto `BLOB` che rappresenta il documento DDX.
   * L&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType` che contiene il documento PDF di input. Le chiavi devono corrispondere ai nomi dei file di origine di PDF e i relativi valori devono essere l&#39;oggetto `BLOB` che corrisponde al file di PDF di input.
   * Oggetto `AssemblerOptionSpec` che specifica le opzioni di runtime.

   Il metodo `invoke` restituisce un oggetto `AssemblerResult` che contiene dati XML che specifica se il documento PDF di input è un documento PDF/A.

1. Salva il documento XML restituito.

   Per ottenere dati XML che specificano se il documento PDF di input è un documento PDF/A, effettuare le seguenti operazioni:

   * Accedere al campo `documents` dell&#39;oggetto `AssemblerResult`, che è un oggetto `Map` contenente i dati XML che specifica se il documento PDF di input è un documento PDF/A.
   * Scorrere l&#39;oggetto `Map` per ottenere ogni documento risultante. Quindi, eseguire il cast del valore del membro dell&#39;array a `BLOB`.
   * Estrarre i dati binari che rappresentano i dati XML accedendo al campo `MTOM` dell&#39;oggetto `BLOB`. In questo campo viene memorizzata una matrice di byte che è possibile scrivere come file XML.

**Consulta anche**

[Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
