---
title: Creazione dinamica di documenti DDX
seo-title: Dynamically Creating DDX Documents
description: Crea un documento DDX in modo dinamico utilizzando l’API Java e l’API Web Service. La creazione dinamica di un documento DDX consente di utilizzare i valori nel documento DDX ottenuti durante l'esecuzione.
seo-description: Create a DDX document dynamically using the Java API and Web Service API. Dynamically creating a DDX document enables you to use values in the DDX document that are obtained during run-time.
uuid: b73e8069-6c9f-4517-a0ae-f3d503191d2d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 2ad227de-68a8-446f-8c4f-a33a6f95bec8
role: Developer
exl-id: b3c19c82-e26f-4dc8-b846-6aec705cee08
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2163'
ht-degree: 0%

---

# Creazione dinamica di documenti DDX {#dynamically-creating-ddx-documents}

**Esempi ed esempi in questo documento sono solo per AEM Forms in ambiente JEE.**

È possibile creare in modo dinamico un documento DDX che può essere utilizzato per eseguire un&#39;operazione Assembler. La creazione dinamica di un documento DDX consente di utilizzare i valori nel documento DDX ottenuti durante l&#39;esecuzione. Per creare in modo dinamico un documento DDX, utilizzare le classi che appartengono al linguaggio di programmazione utilizzato. Ad esempio, se stai sviluppando l&#39;applicazione client utilizzando Java, utilizza le classi che appartengono al `org.w3c.dom.*`pacchetto. Allo stesso modo, se utilizzi Microsoft .NET, utilizza le classi che appartengono a `System.Xml` spazio dei nomi.

Prima di passare il documento DDX al servizio Assembler, convertire il codice XML da un `org.w3c.dom.Document` istanza a un `com.adobe.idp.Document` istanza. Se si utilizzano servizi Web, convertire l&#39;XML dal tipo di dati utilizzato per creare l&#39;XML (ad esempio, `XmlDocument`) a `BLOB` istanza.

Per questa discussione, si supponga che il seguente documento DDX venga creato in modo dinamico.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
      <PDFsFromBookmarks prefix="stmt">
     <PDF source="AssemblerResultPDF.pdf"/>
 </PDFsFromBookmarks>
 </DDX>
```

Questo documento DDX smonta un documento PDF. Si consiglia di avere familiarità con la disassemblaggio dei documenti PDF.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Assembler, vedere [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Per ulteriori informazioni su un documento DDX, consulta [Servizio di assemblaggio e riferimento DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Riepilogo dei passaggi {#summary-of-steps}

Per smontare un documento PDF utilizzando un documento DDX creato in modo dinamico, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Creare un client PDF Assembler.
1. Crea il documento DDX.
1. Convertire il documento DDX.
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

**Creare un client PDF Assembler**

Prima di eseguire un&#39;operazione Assembler a livello di programmazione, creare un client di servizio Assembler.

**Creare il documento DDX**

Creare un documento DDX utilizzando il linguaggio di programmazione utilizzato. Per creare un documento DDX che smonti un documento PDF, assicurati che contenga `PDFsFromBookmarks` elemento. Convertire il tipo di dati utilizzato per creare il documento DDX in un `com.adobe.idp.Document` Se utilizzi l’API Java. Se utilizzi servizi web, converti il tipo di dati in un `BLOB` istanza.

**Conversione del documento DDX**

Documento DDX creato utilizzando `org.w3c.dom` le classi devono essere convertite in un `com.adobe.idp.Document` oggetto. Per eseguire questa attività quando si utilizza l&#39;API Java, utilizzare le classi di trasformazione Java XML. Se utilizzi servizi web, converti il documento DDX in un `BLOB` oggetto.

**Fare riferimento a un documento PDF per la scomposizione**

Per smontare un documento PDF, fare riferimento a un file PDF che rappresenta il documento PDF da smontare. Quando viene passato al servizio Assembler, viene restituito un documento PDF separato per ogni segnalibro di livello 1 nel documento.

**Impostare le opzioni di esecuzione**

È possibile impostare le opzioni di esecuzione che controllano il comportamento del servizio Assembler mentre esegue un processo. Ad esempio, è possibile impostare un&#39;opzione che indica al servizio Assembler di continuare l&#39;elaborazione di un processo in caso di errore. Per impostare le opzioni di esecuzione, utilizza un `AssemblerOptionSpec` oggetto.

**Smontare il documento PDF**

Smontare il documento PDF richiamando il `invokeDDX` funzionamento. Passa il documento DDX creato in modo dinamico. Il servizio Assembler restituisce documenti PDF smontati all&#39;interno di un oggetto raccolta.

**Salvare i documenti PDF smontati**

Tutti i documenti PDF smontati vengono restituiti all&#39;interno di un oggetto raccolta. Iterare l’oggetto raccolta e salvare ogni documento PDF come file PDF.

**Consulta anche**

[Creare in modo dinamico un documento DDX utilizzando l’API Java](/help/forms/developing/dynamically-creating-ddx-documents.md#dynamically-create-a-ddx-document-using-the-java-api)

[Creare in modo dinamico un documento DDX utilizzando l’API del servizio Web](/help/forms/developing/dynamically-creating-ddx-documents.md#dynamically-create-a-ddx-document-using-the-web-service-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Smontaggio programmatico dei documenti PDF](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

## Creare in modo dinamico un documento DDX utilizzando l’API Java {#dynamically-create-a-ddx-document-using-the-java-api}

Creare in modo dinamico un documento DDX e smontare un documento PDF utilizzando l&#39;API del servizio Assembler (Java):

1. Includi file di progetto.

   Includi file JAR client, come adobe-assembler-client.jar, nel percorso di classe del progetto Java.

1. Creare un client PDF Assembler.

   * Crea un `ServiceClientFactory` oggetto contenente le proprietà di connessione.
   * Crea un `AssemblerServiceClient` utilizzando il relativo costruttore e passando `ServiceClientFactory` oggetto.

1. Crea il documento DDX.

   * Creare un Java `DocumentBuilderFactory` chiamando `DocumentBuilderFactory` classe&quot; `newInstance` metodo .
   * Creare un Java `DocumentBuilder` chiamando `DocumentBuilderFactory` dell’oggetto `newDocumentBuilder` metodo .
   * Chiama il `DocumentBuilder` dell’oggetto `newDocument` per creare un&#39;istanza di un `org.w3c.dom.Document` oggetto.
   * Crea l&#39;elemento principale del documento DDX richiamando il `org.w3c.dom.Document` dell’oggetto `createElement` metodo . Questo metodo crea un `Element` oggetto che rappresenta l&#39;elemento principale. Passa un valore stringa che rappresenta il nome dell&#39;elemento al `createElement` metodo . Imposta il valore restituito su `Element`. Quindi, imposta un valore per l’elemento figlio chiamando il relativo `setAttribute` metodo . Infine, aggiungi l’elemento all’elemento header chiamando l’elemento header `appendChild` e passare l&#39;oggetto elemento figlio come argomento. Le seguenti righe di codice mostrano questa logica di applicazione:
      ` Element root = (Element)document.createElement("DDX");  root.setAttribute("xmlns","https://ns.adobe.com/DDX/1.0/");  document.appendChild(root);`

   * Crea il `PDFsFromBookmarks` chiamando `Document` dell’oggetto `createElement` metodo . Passa un valore stringa che rappresenta il nome dell&#39;elemento al `createElement` metodo . Imposta il valore restituito su `Element`. Imposta un valore per `PDFsFromBookmarks` elemento chiamando il relativo `setAttribute` metodo . Aggiungi `PDFsFromBookmarks` dell&#39;elemento `DDX` chiamando l’elemento DDX `appendChild` metodo . Passa la `PDFsFromBookmarks` oggetto elemento come argomento. Le seguenti righe di codice mostrano questa logica di applicazione:

      ` Element PDFsFromBookmarks = (Element)document.createElement("PDFsFromBookmarks");  PDFsFromBookmarks.setAttribute("prefix","stmt");  root.appendChild(PDFsFromBookmarks);`

   * Crea un `PDF` chiamando `Document` dell’oggetto `createElement` metodo . Passa un valore stringa che rappresenta il nome dell&#39;elemento. Imposta il valore restituito su `Element`. Imposta un valore per `PDF` elemento chiamando il relativo `setAttribute` metodo . Aggiungi `PDF` dell&#39;elemento `PDFsFromBookmarks` chiamando `PDFsFromBookmarks` dell’elemento `appendChild` metodo . Passa la `PDF` oggetto elemento come argomento. Le seguenti righe di codice mostrano questa logica di applicazione:

      ` Element PDF = (Element)document.createElement("PDF");  PDF.setAttribute("source","AssemblerResultPDF.pdf");  PDFsFromBookmarks.appendChild(PDF);`

1. Convertire il documento DDX.

   * Crea un `javax.xml.transform.Transformer` richiamando l&#39;oggetto `javax.xml.transform.Transformer` statico dell’oggetto `newInstance` metodo .
   * Crea un `Transformer` richiamando l&#39;oggetto `TransformerFactory` dell’oggetto `newTransformer` metodo .
   * Crea un `ByteArrayOutputStream` utilizzando il relativo costruttore.
   * Crea un `javax.xml.transform.dom.DOMSource` utilizzando il relativo costruttore. Passa la `org.w3c.dom.Document` oggetto che rappresenta il documento DDX.
   * Crea un `javax.xml.transform.dom.DOMSource` utilizzando il relativo costruttore e passando `ByteArrayOutputStream` oggetto.
   * Popolare Java `ByteArrayOutputStream` richiamando l&#39;oggetto `javax.xml.transform.Transformer` dell’oggetto `transform` metodo . Passa la `javax.xml.transform.dom.DOMSource` e `javax.xml.transform.stream.StreamResult` oggetti.
   * Creare un array di byte e allocare le dimensioni del `ByteArrayOutputStream` all&#39;array di byte.
   * Compilare l’array di byte richiamando il `ByteArrayOutputStream` dell’oggetto `toByteArray` metodo .
   * Crea un `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;array di byte.

1. Fare riferimento a un documento PDF per smontare.

   * Crea un `java.util.Map` oggetto utilizzato per memorizzare i documenti PDF di input utilizzando un `HashMap` costruttore.
   * Crea un `java.io.FileInputStream` utilizzando il relativo costruttore e passando la posizione del documento PDF da smontare.
   * Crea un `com.adobe.idp.Document` oggetto. Passa la `java.io.FileInputStream` oggetto contenente il documento PDF da smontare.
   * Aggiungi una voce al `java.util.Map` richiamandone l&#39;oggetto `put` e passare gli argomenti seguenti:

      * Valore stringa che rappresenta il nome della chiave. Questo valore deve corrispondere al valore dell&#39;elemento di origine PDF specificato nel documento DDX. Nel documento DDX creato in modo dinamico, il valore è `AssemblerResultPDF.pdf`.)
      * A `com.adobe.idp.Document` oggetto contenente il documento PDF da smontare.

1. Impostare le opzioni di esecuzione.

   * Crea un `AssemblerOptionSpec` oggetto che memorizza le opzioni di esecuzione utilizzando il relativo costruttore.
   * Impostare le opzioni di esecuzione per soddisfare i requisiti aziendali richiamando un metodo che appartiene al `AssemblerOptionSpec` oggetto. Ad esempio, per dare istruzioni al servizio Assembler di continuare a elaborare un processo quando si verifica un errore, richiama il `AssemblerOptionSpec` dell’oggetto `setFailOnError` metodo e passaggio `false`.

1. Smontare il documento PDF.

   Richiama il `AssemblerServiceClient` dell’oggetto `invokeDDX` e passare i seguenti valori:

   * A `com.adobe.idp.Document` oggetto che rappresenta il documento DDX creato dinamicamente
   * A `java.util.Map` oggetto contenente il documento PDF da smontare
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` oggetto che specifica le opzioni di esecuzione, incluso il carattere predefinito e il livello del registro di lavoro

   La `invokeDDX` restituisce un `com.adobe.livecycle.assembler.client.AssemblerResult` oggetto che contiene i documenti PDF smontati ed eventuali eccezioni.

1. Salvare i documenti PDF smontati.

   Per ottenere i documenti PDF smontati, eseguire le operazioni seguenti:

   * Richiama il `AssemblerResult` dell’oggetto `getDocuments` metodo . Questo metodo restituisce un `java.util.Map` oggetto.
   * Itera attraverso il `java.util.Map` finché non trovi il risultato `com.adobe.idp.Document` oggetto.
   * Richiama il `com.adobe.idp.Document` dell’oggetto `copyToFile` per estrarre il documento PDF.

**Consulta anche**

[Avvio rapido (modalità SOAP): Creazione dinamica di un documento DDX utilizzando l’API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-dynamically-creating-a-ddx-document-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Creare in modo dinamico un documento DDX utilizzando l’API del servizio Web {#dynamically-create-a-ddx-document-using-the-web-service-api}

Creare in modo dinamico un documento DDX e smontare un documento PDF utilizzando l&#39;API del servizio Assembler (servizio Web):

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

1. Crea il documento DDX.

   * Crea un `System.Xml.XmlElement` utilizzando il relativo costruttore.
   * Crea l&#39;elemento principale del documento DDX richiamando il `XmlElement` dell’oggetto `CreateElement` metodo . Questo metodo crea un `Element` oggetto che rappresenta l&#39;elemento principale. Passa un valore stringa che rappresenta il nome dell&#39;elemento al `CreateElement` metodo . Imposta un valore per l&#39;elemento DDX chiamandone l&#39;elemento `SetAttribute` metodo . Infine, aggiungi l’elemento al documento DDX chiamando il `XmlElement` dell’oggetto `AppendChild` metodo . Passa l&#39;oggetto DDX come argomento. Le seguenti righe di codice mostrano questa logica di applicazione:

      ` System.Xml.XmlElement root = ddx.CreateElement("DDX");  root.SetAttribute("xmlns", "https://ns.adobe.com/DDX/1.0/");  ddx.AppendChild(root);`

   * Creare il documento DDX `PDFsFromBookmarks` chiamando `XmlElement` dell’oggetto `CreateElement` metodo . Passa un valore stringa che rappresenta il nome dell&#39;elemento al `CreateElement` metodo . Quindi, imposta un valore per l’elemento chiamando il relativo `SetAttribute` metodo . Aggiungi `PDFsFromBookmarks` all&#39;elemento principale chiamando il `DDX` dell’elemento `AppendChild` metodo . Passa la `PDFsFromBookmarks` oggetto elemento come argomento. Le seguenti righe di codice mostrano questa logica di applicazione:

      ` XmlElement PDFsFromBookmarks = ddx.CreateElement("PDFsFromBookmarks");  PDFsFromBookmarks.SetAttribute("prefix", "stmt");  root.AppendChild(PDFsFromBookmarks);`

   * Creare il documento DDX `PDF` chiamando `XmlElement` dell’oggetto `CreateElement` metodo . Passa un valore stringa che rappresenta il nome dell&#39;elemento al `CreateElement` metodo . Quindi, imposta un valore per l’elemento figlio chiamando il relativo `SetAttribute` metodo . Aggiungi `PDF` dell&#39;elemento `PDFsFromBookmarks` chiamando `PDFsFromBookmarks` dell’elemento `AppendChild` metodo . Passa la `PDF` oggetto elemento come argomento. Le seguenti righe di codice mostrano questa logica di applicazione:

      ` XmlElement PDF = ddx.CreateElement("PDF");  PDF.SetAttribute("source", "AssemblerResultPDF.pdf");  PDFsFromBookmarks.AppendChild(PDF);`

1. Convertire il documento DDX.

   * Crea un `System.IO.MemoryStream` utilizzando il relativo costruttore.
   * Popolare `MemoryStream` oggetto con il documento DDX utilizzando `XmlElement` oggetto che rappresenta il documento DDX. Richiama il `XmlElement` dell’oggetto `Save` e passare il `MemoryStream` oggetto.
   * Crea un array di byte e popolalo con i dati che si trovano nel `MemoryStream` oggetto. Il codice seguente mostra questa logica di applicazione:

      ` int bufLen = Convert.ToInt32(stream.Length);  byte[] byteArray = new byte[bufLen];  stream.Position = 0;  int count = stream.Read(byteArray, 0, bufLen);`

   * Crea un `BLOB` oggetto. Assegna l&#39;array di byte al `BLOB` dell’oggetto `MTOM` campo .

1. Fare riferimento a un documento PDF per smontare.

   * Crea un `BLOB` utilizzando il relativo costruttore. La `BLOB` viene utilizzato per memorizzare il documento di input PDF. Questo `BLOB` viene passato all&#39;oggetto `invokeOneDocument` come argomento.
   * Crea un `System.IO.FileStream` richiamando il relativo costruttore. Passa un valore stringa che rappresenta la posizione del file del documento PDF di input e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto del `System.IO.FileStream` oggetto. È possibile determinare le dimensioni dell&#39;array di byte ottenendo il `System.IO.FileStream` dell’oggetto `Length` proprietà.
   * Compilare l&#39;array di byte con i dati del flusso richiamando il `System.IO.FileStream` dell’oggetto `Read` e passare l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare `BLOB` oggetto assegnando il relativo `MTOM` proprietà il contenuto dell&#39;array di byte.

1. Impostare le opzioni di esecuzione.

   * Crea un `AssemblerOptionSpec` oggetto che memorizza le opzioni di esecuzione utilizzando il relativo costruttore.
   * Impostare le opzioni di esecuzione per soddisfare i requisiti aziendali assegnando un valore a un membro dati che appartiene al `AssemblerOptionSpec` oggetto. Ad esempio, per dare istruzioni al servizio Assembler di continuare a elaborare un processo quando si verifica un errore, assegnare `false` al `AssemblerOptionSpec` dell’oggetto `failOnError` membro dati.

1. Smontare il documento PDF.

   Richiama il `AssemblerServiceClient` dell’oggetto `invokeDDX` e passare i seguenti valori:

   * A `BLOB` oggetto che rappresenta il documento DDX creato dinamicamente
   * La `mapItem` array contenente il documento PDF di input
   * Un `AssemblerOptionSpec` oggetto che specifica le opzioni di esecuzione

   La `invokeDDX` restituisce un `AssemblerResult` oggetto contenente i risultati del processo ed eventuali eccezioni.

1. Salvare i documenti PDF smontati.

   Per ottenere i documenti PDF appena creati, eseguire le operazioni seguenti:

   * Accedere al `AssemblerResult` dell’oggetto `documents` un campo `Map` oggetto contenente i documenti PDF smontati.
   * Itera attraverso il `Map` per ottenere ogni documento risultante. Quindi, eseguire il cast del membro dell&#39;array `value` a `BLOB`.
   * Estrarre i dati binari che rappresentano il documento PDF accedendo ai relativi `BLOB` dell’oggetto `MTOM` proprietà. Restituisce una matrice di byte che è possibile scrivere in un file PDF.

**Consulta anche**

[Richiamo di AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamo di AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
