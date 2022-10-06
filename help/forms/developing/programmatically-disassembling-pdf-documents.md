---
title: Smontaggio programmatico dei documenti PDF
seo-title: Programmatically Disassembling PDF Documents
description: Utilizza il servizio Assembler per smontare un singolo documento PDF in più documenti PDF utilizzando l’API Java e l’API Web Service.
seo-description: Use the Assembler service to disassemble a single PDF document into multiple PDF documents using the Java API and the Web Service API.
uuid: d71cc044-e948-4b7a-b598-b041723b69e9
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 8e38a597-5d22-4d83-95fe-4494fb04e4a3
role: Developer
exl-id: c5e712e0-5c3f-48cd-91cf-fd347222a6b2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1761'
ht-degree: 0%

---

# Smontaggio programmatico dei documenti PDF {#programmatically-disassembling-pdf-documents}

**Esempi ed esempi in questo documento sono solo per AEM Forms in ambiente JEE.**

È possibile smontare un documento PDF trasmettendolo al servizio Assembler. In genere, questa attività è utile quando il documento PDF è stato creato originariamente da molti documenti, ad esempio una raccolta di istruzioni. Nell&#39;illustrazione seguente, DocA è suddiviso in più documenti risultanti, dove il primo segnalibro di livello 1 in una pagina identifica l&#39;inizio di un nuovo documento risultante.

![pd_pd_pdfsfrombookmarks](assets/pd_pd_pdfsfrombookmarks.png)

Per smontare un documento PDF, assicurati che il `PDFsFromBookmarks` si trova nel documento DDX. La `PDFsFromBookmarks` element è un elemento risultante e può essere solo un elemento figlio del `DDX` elemento. Non ha un `result` perché può generare più documenti.

La `PDFsFromBookmarks` causa la generazione di un singolo documento per ogni segnalibro di livello 1 nel documento di origine.

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
>Prima di leggere questa sezione, è consigliabile acquisire familiarità con l’assemblaggio dei documenti PDF utilizzando il servizio Assembler. (Vedi [Assemblaggio di documenti PDF a livello di programmazione](/help/forms/developing/programmatically-assembling-pdf-documents.md).)

>[!NOTE]
>
>Quando si passa un singolo documento PDF al servizio Assembler e si recupera un singolo documento, è possibile richiamare `invokeOneDocument` funzionamento. Tuttavia, per smontare un documento PDF, utilizzare il `invokeDDX` poiché, sebbene un documento di input PDF venga passato al servizio Assembler, il servizio Assembler restituisce un oggetto raccolta contenente uno o più documenti.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Assembler, vedere [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Per ulteriori informazioni su un documento DDX, consulta [Servizio di assemblaggio e riferimento DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Riepilogo dei passaggi {#summary-of-steps}

Per smontare un documento PDF, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Creare un client PDF Assembler.
1. Fai riferimento a un documento DDX esistente.
1. Fare riferimento a un documento PDF per smontare.
1. Impostare le opzioni di esecuzione.
1. Smontare il documento PDF.
1. Salvare i documenti PDF smontati.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso della classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è distribuito su JBoss)
* jbossall-client.jar (richiesto se AEM Forms è distribuito su JBoss)

se AEM Forms è implementato su un server applicazioni J2EE supportato che non è JBoss, devi sostituire adobe-utilities.jar e jbossall-client.jar con file JAR specifici per il server applicazioni J2EE in cui viene distribuito AEM Forms.

**Creare un client PDF Assembler**

Prima di poter eseguire un&#39;operazione Assembler a livello di programmazione, è necessario creare un client di servizio Assembler.

**Riferimento a un documento DDX esistente**

Per smontare un documento PDF è necessario fare riferimento a un documento DDX. Questo documento DDX deve contenere `PDFsFromBookmarks` elemento.

**Fare riferimento a un documento PDF per la scomposizione**

Per smontare un documento PDF, fare riferimento a un file PDF che rappresenta il documento PDF da smontare. Quando viene passato al servizio Assembler, viene restituito un documento PDF separato per ogni segnalibro di livello 1 nel documento.

**Impostare le opzioni di esecuzione**

È possibile impostare le opzioni di esecuzione che controllano il comportamento del servizio Assembler mentre esegue un processo. Ad esempio, è possibile impostare un&#39;opzione che indica al servizio Assembler di continuare l&#39;elaborazione di un processo in caso di errore.

**Smontare il documento PDF**

Dopo aver creato il client di servizio Assembler, fare riferimento al documento DDX, fare riferimento a un documento PDF per smontare e impostare le opzioni di esecuzione, è possibile smontare un documento PDF richiamando il `invokeDDX` metodo . Se il documento DDX contiene istruzioni per smontare il documento PDF, il servizio Assembler restituisce documenti PDF smontati all&#39;interno di un oggetto di raccolta.

**Salvare i documenti PDF smontati**

Tutti i documenti PDF smontati vengono restituiti all&#39;interno di un oggetto raccolta. Iterare l’oggetto raccolta e salvare ogni documento PDF come file PDF.

**Consulta anche**

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Assemblaggio di documenti PDF a livello di programmazione](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Smontare un documento PDF utilizzando l’API Java {#disassemble-a-pdf-document-using-the-java-api}

Smontare un documento PDF utilizzando l’API del servizio Assembler (Java):

1. Includi file di progetto.

   Includi file JAR client, come adobe-assembler-client.jar, nel percorso di classe del progetto Java.

1. Creare un client PDF Assembler.

   * Crea un `ServiceClientFactory` oggetto contenente le proprietà di connessione.
   * Crea un `AssemblerServiceClient` utilizzando il relativo costruttore e passando `ServiceClientFactory` oggetto.

1. Fai riferimento a un documento DDX esistente.

   * Crea un `java.io.FileInputStream` oggetto che rappresenta il documento DDX utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del file DDX.
   * Crea un `com.adobe.idp.Document` utilizzando il relativo costruttore e passando `java.io.FileInputStream` oggetto.

1. Fare riferimento a un documento PDF per smontare.

   * Crea un `java.util.Map` oggetto utilizzato per memorizzare i documenti PDF di input utilizzando un `HashMap` costruttore.
   * Crea un `java.io.FileInputStream` utilizzando il relativo costruttore e passando la posizione del documento PDF da smontare.
   * Crea un `com.adobe.idp.Document` e passare `java.io.FileInputStream` oggetto contenente il documento PDF da smontare.
   * Aggiungi una voce al `java.util.Map` richiamandone l&#39;oggetto `put` e passare gli argomenti seguenti:

      * Valore stringa che rappresenta il nome della chiave. Questo valore deve corrispondere al valore dell&#39;elemento di origine PDF specificato nel documento DDX.
      * A `com.adobe.idp.Document` oggetto contenente il documento PDF da smontare.

1. Impostare le opzioni di esecuzione.

   * Crea un `AssemblerOptionSpec` oggetto che memorizza le opzioni di esecuzione utilizzando il relativo costruttore.
   * Impostare le opzioni di esecuzione per soddisfare i requisiti aziendali richiamando un metodo che appartiene al `AssemblerOptionSpec` oggetto. Ad esempio, per dare istruzioni al servizio Assembler di continuare a elaborare un processo quando si verifica un errore, richiama il `AssemblerOptionSpec` dell’oggetto `setFailOnError` metodo e passaggio `false`.

1. Smontare il documento PDF.

   Richiama il `AssemblerServiceClient` dell’oggetto `invokeDDX` e trasmettere i seguenti valori richiesti:

   * A `com.adobe.idp.Document` oggetto che rappresenta il documento DDX da utilizzare
   * A `java.util.Map` oggetto contenente il documento PDF da smontare
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` oggetto che specifica le opzioni di esecuzione, incluso il carattere predefinito e il livello del registro di lavoro

   La `invokeDDX` restituisce un `com.adobe.livecycle.assembler.client.AssemblerResult` oggetto che contiene i documenti PDF smontati ed eventuali eccezioni.

1. Salvare i documenti PDF smontati.

   Per ottenere i documenti PDF smontati, eseguire le operazioni seguenti:

   * Richiama il `AssemblerResult` dell’oggetto `getDocuments` metodo . Questo restituisce un `java.util.Map` oggetto.
   * Itera attraverso il `java.util.Map` finché non trovi il risultato `com.adobe.idp.Document` oggetto.
   * Richiama il `com.adobe.idp.Document` dell’oggetto `copyToFile` per estrarre il documento PDF.

**Consulta anche**

[Smontaggio programmatico dei documenti PDF](#programmatically-disassembling-pdf-documents)

[Avvio rapido (modalità SOAP): Smontaggio di un documento PDF tramite l’API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-disassembling-a-pdf-document-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Smontare un documento PDF utilizzando l’API del servizio Web {#disassemble-a-pdf-document-using-the-web-service-api}

Smontare un documento PDF utilizzando l&#39;API del servizio Assembler (servizio Web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Quando imposti un riferimento a un servizio, assicurati di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l’indirizzo IP del server che ospita AEM Forms.

1. Creare un client PDF Assembler.

   * Crea un `AssemblerServiceClient` utilizzando il relativo costruttore predefinito.
   * Crea un `AssemblerServiceClient.Endpoint.Address` utilizzando `System.ServiceModel.EndpointAddress` costruttore. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). Non è necessario utilizzare il `lc_version` attributo. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.
   * Crea un `System.ServiceModel.BasicHttpBinding` ottenendo il valore del `AssemblerServiceClient.Endpoint.Binding` campo . Imposta il valore restituito su `BasicHttpBinding`.
   * Imposta la `System.ServiceModel.BasicHttpBinding` dell’oggetto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegnare il nome utente del modulo di AEM al campo `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore della password corrispondente al campo `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Fai riferimento a un documento DDX esistente.

   * Crea un `BLOB` utilizzando il relativo costruttore. La `BLOB` viene utilizzato per memorizzare il documento DDX.
   * Crea un `System.IO.FileStream` richiamando il relativo costruttore. Passa un valore stringa che rappresenta la posizione del file del documento DDX e la modalità in cui aprire il file.
   * Creare un array di byte che memorizza il contenuto del `System.IO.FileStream` oggetto. È possibile determinare le dimensioni dell&#39;array di byte ottenendo il `System.IO.FileStream` dell’oggetto `Length` proprietà.
   * Compilare l&#39;array di byte con i dati del flusso richiamando il `System.IO.FileStream` dell’oggetto `Read` e passare l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare `BLOB` oggetto assegnando il relativo `MTOM` con il contenuto dell&#39;array di byte.

1. Fare riferimento a un documento PDF per smontare.

   * Crea un `BLOB` utilizzando il relativo costruttore. La `BLOB` viene utilizzato per memorizzare il documento di input PDF. Questo `BLOB` viene passato all&#39;oggetto `invokeOneDocument` come argomento.
   * Crea un `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento di input PDF e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto del `System.IO.FileStream` oggetto. È possibile determinare le dimensioni dell&#39;array di byte ottenendo il `System.IO.FileStream` dell’oggetto `Length` proprietà.
   * Compilare l&#39;array di byte con i dati del flusso richiamando il `System.IO.FileStream` dell’oggetto `Read` e passare l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare `BLOB` oggetto assegnando il relativo `MTOM` il contenuto dell&#39;array di byte.
   * Crea un `MyMapOf_xsd_string_To_xsd_anyType` oggetto. Questo oggetto raccolta viene utilizzato per memorizzare PDF da smontare.
   * Crea un `MyMapOf_xsd_string_To_xsd_anyType_Item` oggetto.
   * Assegna un valore stringa che rappresenta il nome della chiave al `MyMapOf_xsd_string_To_xsd_anyType_Item` dell’oggetto `key` campo . Questo valore deve corrispondere al valore dell&#39;elemento di origine PDF specificato nel documento DDX.
   * Assegna `BLOB` oggetto che memorizza il documento PDF nella `MyMapOf_xsd_string_To_xsd_anyType_Item` dell’oggetto `value` campo .
   * Aggiungi il `MyMapOf_xsd_string_To_xsd_anyType_Item` dell&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType` oggetto. Richiama il `MyMapOf_xsd_string_To_xsd_anyType` oggetto&quot; `Add` e passare il `MyMapOf_xsd_string_To_xsd_anyType` oggetto.

1. Impostare le opzioni di esecuzione.

   * Crea un `AssemblerOptionSpec` oggetto che memorizza le opzioni di esecuzione utilizzando il relativo costruttore.
   * Impostare le opzioni di esecuzione per soddisfare i requisiti aziendali assegnando un valore a un membro dati che appartiene al `AssemblerOptionSpec` oggetto. Ad esempio, per dare istruzioni al servizio Assembler di continuare a elaborare un processo quando si verifica un errore, assegnare `false` al `AssemblerOptionSpec` dell’oggetto `failOnError` campo .

1. Smontare il documento PDF.

   Richiama il `AssemblerServiceClient` dell’oggetto `invokeDDX` e passare i seguenti valori:

   * A `BLOB` oggetto che rappresenta il documento DDX che smonta il documento PDF
   * La `MyMapOf_xsd_string_To_xsd_anyType` oggetto contenente il documento PDF da smontare
   * Un `AssemblerOptionSpec` oggetto che specifica le opzioni di esecuzione

   La `invokeDDX` restituisce un `AssemblerResult` oggetto contenente i risultati del processo ed eventuali eccezioni.

1. Salvare i documenti PDF smontati.

   Per ottenere i documenti PDF appena creati, eseguire le operazioni seguenti:

   * Accedere al `AssemblerResult` dell’oggetto `documents` un campo `Map` oggetto contenente i documenti PDF smontati.
   * Itera attraverso il `Map` per ottenere ogni documento risultante. Quindi, eseguire il cast del membro dell&#39;array `value` a `BLOB`.
   * Estrarre i dati binari che rappresentano il documento PDF accedendo ai relativi `BLOB` dell’oggetto `MTOM` proprietà. Restituisce una matrice di byte che è possibile scrivere in un file PDF.

**Consulta anche**

[Smontaggio programmatico dei documenti PDF](#programmatically-disassembling-pdf-documents)

[Richiamo di AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
