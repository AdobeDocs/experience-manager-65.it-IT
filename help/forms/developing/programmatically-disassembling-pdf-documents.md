---
title: Scomposizione programmatica dei documenti PDF
seo-title: Scomposizione programmatica dei documenti PDF
description: 'null'
seo-description: 'null'
uuid: d71cc044-e948-4b7a-b598-b041723b69e9
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 8e38a597-5d22-4d83-95fe-4494fb04e4a3
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '1730'
ht-degree: 0%

---


# Scomposizione programmatica dei documenti PDF {#programmatically-disassembling-pdf-documents}

È possibile smontare un documento PDF trasferendolo al servizio Assembler. In genere, questa attività è utile quando il documento PDF è stato creato originariamente da molti documenti, ad esempio una raccolta di istruzioni. Nell&#39;illustrazione seguente, DocA è diviso in più documenti risultanti, dove il segnalibro di primo livello 1 in una pagina identifica l&#39;inizio di un nuovo documento risultante.

![pd_pd_pdfsfrombookmarks](assets/pd_pd_pdfsfrombookmarks.png)

Per smontare un documento PDF, assicurarsi che l&#39; `PDFsFromBookmarks` elemento si trovi nel documento DDX. L&#39; `PDFsFromBookmarks` elemento è un elemento risultante e può essere solo un elemento secondario dell&#39; `DDX` elemento. Non ha un `result` attributo perché può generare più documenti.

L&#39; `PDFsFromBookmarks` elemento determina la generazione di un singolo documento per ciascun segnalibro di livello 1 nel documento di origine.

Ai fini di questa discussione, si supponga di utilizzare il seguente documento DDX.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
      <PDFsFromBookmarks prefix="stmt">
     <PDF source="AssemblerResultPDF.pdf"/>
 </PDFsFromBookmarks>
 </DDX>
```

>[!NOTE]
>
>Prima di leggere questa sezione, è consigliabile avere familiarità con l&#39;assemblaggio dei documenti PDF tramite il servizio Assembler. (Vedere Assemblaggio [di documenti](/help/forms/developing/programmatically-assembling-pdf-documents.md)PDF a livello di programmazione.)

>[!NOTE]
>
>Quando si passa un singolo documento PDF al servizio Assembler e si ritorna a un singolo documento, è possibile richiamare l&#39; `invokeOneDocument` operazione. Tuttavia, per smontare un documento PDF, utilizzare l&#39; `invokeDDX` operazione perché, sebbene un documento PDF di input venga passato al servizio Assembler, il servizio Assembler restituisce un oggetto raccolta contenente uno o più documenti.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Assembler, vedere Riferimento [servizi per i AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Per ulteriori informazioni su un documento DDX, vedere Servizio [Assembler e Riferimento](https://www.adobe.com/go/learn_aemforms_ddx_63)DDX.

## Riepilogo dei passaggi {#summary-of-steps}

Per smontare un documento PDF, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un client Assembler PDF.
1. Fare riferimento a un documento DDX esistente.
1. Fare riferimento a un documento PDF per smontare.
1. Impostare le opzioni di esecuzione.
1. Smontare il documento PDF.
1. Salvare i documenti PDF smontati.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, accertatevi di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (richiesto se i AEM Forms sono distribuiti su JBoss)
* jbossall-client.jar (richiesto se i AEM Forms sono distribuiti su JBoss)

se i AEM Forms sono distribuiti su un server applicazione J2EE supportato che non è JBoss, è necessario sostituire adobe-utilities.jar e jbossall-client.jar con file JAR specifici del server applicazione J2EE in cui sono distribuiti i AEM Forms.

**Creare un client Assembler PDF**

Prima di eseguire un&#39;operazione Assembler a livello di programmazione, è necessario creare un client di servizio Assembler.

**Riferimento a un documento DDX esistente**

Per smontare un documento PDF è necessario fare riferimento a un documento DDX. Questo documento DDX deve contenere l&#39; `PDFsFromBookmarks` elemento .

**Riferimento a un documento PDF da smontare**

Per smontare un documento PDF, fare riferimento a un file PDF che rappresenta il documento PDF da smontare. Quando viene passato al servizio Assembler, viene restituito un documento PDF separato per ciascun segnalibro di livello 1 nel documento.

**Impostazione delle opzioni di esecuzione**

È possibile impostare opzioni di esecuzione che controllano il comportamento del servizio Assembler mentre esegue un processo. Ad esempio, potete impostare un&#39;opzione che indichi al servizio Assembler di continuare l&#39;elaborazione di un processo in caso di errore.

**Smontare il documento PDF**

Dopo aver creato il client del servizio Assembler, fare riferimento al documento DDX, fare riferimento a un documento PDF per smontare e impostare le opzioni di esecuzione, è possibile smontare un documento PDF richiamando il `invokeDDX` metodo. Se il documento DDX contiene istruzioni per smontare il documento PDF, il servizio Assembler restituisce documenti PDF smontati all&#39;interno di un oggetto raccolta.

**Salvare i documenti PDF smontati**

Tutti i documenti PDF disassemblati vengono restituiti all&#39;interno di un oggetto raccolta. Iterare l&#39;oggetto della raccolta e salvare ciascun documento PDF come file PDF.

**Consulta anche**

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Assemblaggio di documenti PDF a livello di programmazione](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Smontare un documento PDF utilizzando l&#39;API Java {#disassemble-a-pdf-document-using-the-java-api}

Smontare un documento PDF utilizzando l&#39;API Assembler Service (Java):

1. Includere i file di progetto.

   Includete file JAR client, ad esempio adobe-assembler-client.jar, nel percorso di classe del progetto Java.

1. Creare un client Assembler PDF.

   * Creare un `ServiceClientFactory` oggetto che contenga proprietà di connessione.
   * Creare un `AssemblerServiceClient` oggetto utilizzando il relativo costruttore e passando l&#39; `ServiceClientFactory` oggetto.

1. Fare riferimento a un documento DDX esistente.

   * Creare un `java.io.FileInputStream` oggetto che rappresenta il documento DDX utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del file DDX.
   * Creare un `com.adobe.idp.Document` oggetto utilizzando il relativo costruttore e passando l&#39; `java.io.FileInputStream` oggetto.

1. Fare riferimento a un documento PDF per smontare.

   * Creare un oggetto `java.util.Map` utilizzato per memorizzare i documenti PDF di input utilizzando un `HashMap` costruttore.
   * Creare un `java.io.FileInputStream` oggetto utilizzando il relativo costruttore e passare la posizione del documento PDF da smontare.
   * Creare un `com.adobe.idp.Document` oggetto e passare l&#39; `java.io.FileInputStream` oggetto che contiene il documento PDF da smontare.
   * Aggiungere una voce all&#39; `java.util.Map` oggetto richiamandone il `put` metodo e passando gli argomenti seguenti:

      * Un valore di stringa che rappresenta il nome della chiave. Questo valore deve corrispondere al valore dell&#39;elemento di origine PDF specificato nel documento DDX.
      * Un `com.adobe.idp.Document` oggetto che contiene il documento PDF da smontare.

1. Impostare le opzioni di esecuzione.

   * Creare un `AssemblerOptionSpec` oggetto che memorizza le opzioni di esecuzione utilizzando il relativo costruttore.
   * Impostate le opzioni di runtime per soddisfare i requisiti aziendali richiamando un metodo che appartiene all&#39; `AssemblerOptionSpec` oggetto. Ad esempio, per indicare al servizio Assembler di continuare a elaborare un processo quando si verifica un errore, richiamare il metodo dell&#39; `AssemblerOptionSpec` oggetto `setFailOnError` e passare `false`.

1. Smontare il documento PDF.

   Richiamare il metodo dell&#39; `AssemblerServiceClient` oggetto `invokeDDX` e trasmettere i seguenti valori obbligatori:

   * Un `com.adobe.idp.Document` oggetto che rappresenta il documento DDX da utilizzare
   * Un `java.util.Map` oggetto che contiene il documento PDF da smontare
   * Un `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` oggetto che specifica le opzioni di esecuzione, incluso il font predefinito e il livello di registro del processo

   Il `invokeDDX` metodo restituisce un `com.adobe.livecycle.assembler.client.AssemblerResult` oggetto che contiene i documenti PDF disassemblati ed eventuali eccezioni.

1. Salvare i documenti PDF smontati.

   Per ottenere i documenti PDF disassemblati, effettuare le seguenti operazioni:

   * Richiama il metodo dell’ `AssemblerResult` oggetto `getDocuments` . Questo restituisce un `java.util.Map` oggetto.
   * Eseguire un&#39;iterazione sull&#39; `java.util.Map` oggetto fino a individuare l&#39; `com.adobe.idp.Document` oggetto risultante.
   * Richiamare il metodo dell&#39; `com.adobe.idp.Document` oggetto `copyToFile` per estrarre il documento PDF.

**Consulta anche**

[Scomposizione programmatica dei documenti PDF](#programmatically-disassembling-pdf-documents)

[Avvio rapido (modalità SOAP): Smontaggio di un documento PDF mediante l&#39;API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-disassembling-a-pdf-document-using-the-java-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Smontare un documento PDF utilizzando l&#39;API del servizio Web {#disassemble-a-pdf-document-using-the-web-service-api}

Smontare un documento PDF utilizzando l&#39;API Assembler Service (servizio Web):

1. Includere i file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Quando imposti un riferimento a un servizio, accertatevi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

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
   * Creare un `System.IO.FileStream` oggetto richiamandone il costruttore. Passa un valore di stringa che rappresenta la posizione del file del documento DDX e la modalità in cui aprire il file.
   * Creare un array di byte che memorizza il contenuto dell&#39; `System.IO.FileStream` oggetto. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà dell&#39; `System.IO.FileStream` oggetto `Length` .
   * Compilare l&#39;array di byte con i dati del flusso richiamando il `System.IO.FileStream` `Read` metodo dell&#39;oggetto e passando l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39; `BLOB` oggetto assegnandone `MTOM` la proprietà con il contenuto dell&#39;array di byte.

1. Fare riferimento a un documento PDF per smontare.

   * Creare un `BLOB` oggetto utilizzando il relativo costruttore. L&#39; `BLOB` oggetto viene utilizzato per memorizzare il documento PDF di input. Questo `BLOB` oggetto viene passato all&#39;oggetto `invokeOneDocument` come argomento.
   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF di input e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto dell&#39; `System.IO.FileStream` oggetto. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà dell&#39; `System.IO.FileStream` oggetto `Length` .
   * Compilare l&#39;array di byte con i dati del flusso richiamando il `System.IO.FileStream` `Read` metodo dell&#39;oggetto e passando l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39; `BLOB` oggetto assegnando al relativo `MTOM` campo il contenuto dell&#39;array di byte.
   * Create a `MyMapOf_xsd_string_To_xsd_anyType` object. Questo oggetto raccolta viene utilizzato per memorizzare il PDF per la scomposizione.
   * Create a `MyMapOf_xsd_string_To_xsd_anyType_Item` object.
   * Assegnare un valore di stringa che rappresenta il nome chiave al campo dell&#39; `MyMapOf_xsd_string_To_xsd_anyType_Item` oggetto `key` . Questo valore deve corrispondere al valore dell&#39;elemento di origine PDF specificato nel documento DDX.
   * Assegnare l&#39; `BLOB` oggetto che memorizza il documento PDF nel campo dell&#39; `MyMapOf_xsd_string_To_xsd_anyType_Item` oggetto `value` .
   * Aggiungere l&#39; `MyMapOf_xsd_string_To_xsd_anyType_Item` oggetto all&#39; `MyMapOf_xsd_string_To_xsd_anyType` oggetto. Richiamare il metodo dell’ `MyMapOf_xsd_string_To_xsd_anyType` oggetto `Add` e passare l’ `MyMapOf_xsd_string_To_xsd_anyType` oggetto.

1. Impostare le opzioni di esecuzione.

   * Creare un `AssemblerOptionSpec` oggetto che memorizza le opzioni di esecuzione utilizzando il relativo costruttore.
   * Impostare le opzioni di runtime per soddisfare i requisiti aziendali assegnando un valore a un membro di dati che appartiene all&#39; `AssemblerOptionSpec` oggetto. Ad esempio, per indicare al servizio Assembler di continuare l&#39;elaborazione di un processo in caso di errore, assegnare `false` al campo dell&#39; `AssemblerOptionSpec` oggetto `failOnError` .

1. Smontare il documento PDF.

   Richiama il metodo dell’ `AssemblerServiceClient` oggetto `invokeDDX` e passa i seguenti valori:

   * Un `BLOB` oggetto che rappresenta il documento DDX che smonta il documento PDF
   * L&#39; `MyMapOf_xsd_string_To_xsd_anyType` oggetto che contiene il documento PDF da smontare
   * Un oggetto `AssemblerOptionSpec` che specifica le opzioni di esecuzione

   Il `invokeDDX` metodo restituisce un `AssemblerResult` oggetto che contiene i risultati del processo ed eventuali eccezioni.

1. Salvare i documenti PDF smontati.

   Per ottenere i documenti PDF appena creati, effettuare le seguenti operazioni:

   * Accedere al campo dell&#39; `AssemblerResult` oggetto `documents` , ovvero un `Map` oggetto che contiene i documenti PDF smontati.
   * Eseguire un&#39;iterazione sull&#39; `Map` oggetto per ottenere ogni documento risultante. Quindi, inserite il membro dell&#39;array `value` in un `BLOB`.
   * Estrarre i dati binari che rappresentano il documento PDF accedendo alla `BLOB` proprietà dell&#39; `MTOM` oggetto. Questo restituisce un array di byte che è possibile scrivere in un file PDF.

**Consulta anche**

[Scomposizione programmatica dei documenti PDF](#programmatically-disassembling-pdf-documents)

[Chiamata di AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
