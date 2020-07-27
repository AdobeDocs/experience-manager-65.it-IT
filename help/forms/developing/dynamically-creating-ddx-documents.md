---
title: Creazione dinamica di documenti DDX
seo-title: Creazione dinamica di documenti DDX
description: 'null'
seo-description: 'null'
uuid: b73e8069-6c9f-4517-a0ae-f3d503191d2d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 2ad227de-68a8-446f-8c4f-a33a6f95bec8
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '2123'
ht-degree: 0%

---


# Creazione dinamica di documenti DDX {#dynamically-creating-ddx-documents}

È possibile creare in modo dinamico un documento DDX che può essere utilizzato per eseguire un&#39;operazione Assembler. La creazione dinamica di un documento DDX consente di utilizzare valori nel documento DDX ottenuti durante l&#39;esecuzione. Per creare in modo dinamico un documento DDX, utilizzare classi appartenenti al linguaggio di programmazione utilizzato. Ad esempio, se state sviluppando l&#39;applicazione client utilizzando Java, utilizzate le classi che appartengono al `org.w3c.dom.*`pacchetto. Analogamente, se si utilizza Microsoft .NET, utilizzare classi appartenenti allo `System.Xml` spazio dei nomi.

Prima di passare il documento DDX al servizio Assembler, convertire l&#39;XML da un&#39; `org.w3c.dom.Document` istanza a un&#39; `com.adobe.idp.Document` istanza. Se si utilizzano i servizi Web, convertire l&#39;XML dal tipo di dati utilizzato per creare l&#39;XML (ad esempio, `XmlDocument`) in un&#39; `BLOB` istanza.

Per questa discussione, si supponga che il seguente documento DDX venga creato in modo dinamico.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
      <PDFsFromBookmarks prefix="stmt">
     <PDF source="AssemblerResultPDF.pdf"/>
 </PDFsFromBookmarks>
 </DDX>
```

Questo documento DDX smonta un documento PDF. È consigliabile avere familiarità con la scomposizione dei documenti PDF.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Assembler, vedere Riferimento [servizi per i AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Per ulteriori informazioni su un documento DDX, vedere Servizio [Assembler e Riferimento](https://www.adobe.com/go/learn_aemforms_ddx_63)DDX.

## Riepilogo dei passaggi {#summary-of-steps}

Per smontare un documento PDF utilizzando un documento DDX creato in modo dinamico, eseguire le operazioni seguenti:

1. Includere i file di progetto.
1. Creare un client Assembler PDF.
1. Creare il documento DDX.
1. Convertire il documento DDX.
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

**Creare un client Assembler PDF**

Prima di eseguire un&#39;operazione Assembler a livello di programmazione, create un client di servizio Assembler.

**Creare il documento DDX**

Creare un documento DDX utilizzando il linguaggio di programmazione utilizzato. Per creare un documento DDX che smonti un documento PDF, assicurarsi che contenga l&#39; `PDFsFromBookmarks` elemento. Convertire il tipo di dati utilizzato per creare il documento DDX in un&#39; `com.adobe.idp.Document` istanza se si utilizza l&#39;API Java. Se si utilizzano i servizi Web, convertire il tipo di dati in un&#39; `BLOB` istanza.

**Conversione del documento DDX**

Un documento DDX creato utilizzando `org.w3c.dom` le classi deve essere convertito in un `com.adobe.idp.Document` oggetto. Per eseguire questa attività quando si utilizza l&#39;API Java, utilizzare le classi di trasformazione Java XML. Se si utilizzano i servizi Web, convertire il documento DDX in un `BLOB` oggetto.

**Riferimento a un documento PDF da smontare**

Per smontare un documento PDF, fare riferimento a un file PDF che rappresenta il documento PDF da smontare. Quando viene passato al servizio Assembler, viene restituito un documento PDF separato per ciascun segnalibro di livello 1 nel documento.

**Impostazione delle opzioni di esecuzione**

È possibile impostare opzioni di esecuzione che controllano il comportamento del servizio Assembler mentre esegue un processo. Ad esempio, potete impostare un&#39;opzione che indichi al servizio Assembler di continuare l&#39;elaborazione di un processo in caso di errore. Per impostare le opzioni di esecuzione, è necessario utilizzare un `AssemblerOptionSpec` oggetto.

**Smontare il documento PDF**

Smontare il documento PDF richiamando l&#39; `invokeDDX` operazione. Passa il documento DDX creato in modo dinamico. Il servizio Assembler restituisce documenti PDF smontati all&#39;interno di un oggetto raccolta.

**Salvare i documenti PDF smontati**

Tutti i documenti PDF disassemblati vengono restituiti all&#39;interno di un oggetto raccolta. Iterare l&#39;oggetto della raccolta e salvare ciascun documento PDF come file PDF.

**Consulta anche**

[Creare in modo dinamico un documento DDX utilizzando l&#39;API Java](/help/forms/developing/dynamically-creating-ddx-documents.md#dynamically-create-a-ddx-document-using-the-java-api)

[Creare in modo dinamico un documento DDX utilizzando l&#39;API del servizio Web](/help/forms/developing/dynamically-creating-ddx-documents.md#dynamically-create-a-ddx-document-using-the-web-service-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Scomposizione programmatica dei documenti PDF](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

## Creare in modo dinamico un documento DDX utilizzando l&#39;API Java {#dynamically-create-a-ddx-document-using-the-java-api}

Creare in modo dinamico un documento DDX e smontare un documento PDF utilizzando l&#39;API Assembler Service (Java):

1. Includere i file di progetto.

   Includete file JAR client, ad esempio adobe-assembler-client.jar, nel percorso di classe del progetto Java.

1. Creare un client Assembler PDF.

   * Creare un `ServiceClientFactory` oggetto che contenga proprietà di connessione.
   * Creare un `AssemblerServiceClient` oggetto utilizzando il relativo costruttore e passando l&#39; `ServiceClientFactory` oggetto.

1. Creare il documento DDX.

   * Creare un oggetto Java `DocumentBuilderFactory` chiamando il metodo della `DocumentBuilderFactory` classe `newInstance` .
   * Creare un oggetto Java `DocumentBuilder` chiamando il `DocumentBuilderFactory` metodo dell&#39; `newDocumentBuilder` oggetto.
   * Chiamare il metodo dell&#39; `DocumentBuilder` oggetto `newDocument` per creare un&#39;istanza di un `org.w3c.dom.Document` oggetto.
   * Creare l&#39;elemento principale del documento DDX richiamando il `org.w3c.dom.Document` metodo dell&#39; `createElement` oggetto. Questo metodo crea un `Element` oggetto che rappresenta l&#39;elemento principale. Passate al `createElement` metodo un valore di stringa che rappresenta il nome dell&#39;elemento. Inserite il valore restituito in `Element`. Quindi, impostate un valore per l’elemento secondario chiamandone il `setAttribute` metodo. Infine, aggiungete l’elemento all’elemento header chiamando il metodo dell’elemento header e passate l’oggetto element secondario come argomento. `appendChild` Le seguenti righe di codice mostrano questa logica di applicazione:
      ` Element root = (Element)document.createElement("DDX");  root.setAttribute("xmlns","https://ns.adobe.com/DDX/1.0/");  document.appendChild(root);`

   * Create l&#39; `PDFsFromBookmarks` elemento chiamando il metodo dell&#39; `Document` oggetto `createElement` . Passate al `createElement` metodo un valore di stringa che rappresenta il nome dell&#39;elemento. Inserite il valore restituito in `Element`. Impostate un valore per l&#39; `PDFsFromBookmarks` elemento chiamandone il `setAttribute` metodo. Aggiungete l&#39; `PDFsFromBookmarks` elemento all&#39; `DDX` elemento chiamando il `appendChild` metodo dell&#39;elemento DDX. Passate l&#39;oggetto `PDFsFromBookmarks` element come argomento. Le seguenti righe di codice mostrano questa logica di applicazione:

      ` Element PDFsFromBookmarks = (Element)document.createElement("PDFsFromBookmarks");  PDFsFromBookmarks.setAttribute("prefix","stmt");  root.appendChild(PDFsFromBookmarks);`

   * Create un `PDF` elemento chiamando il metodo dell&#39; `Document` oggetto `createElement` . Passate un valore di stringa che rappresenta il nome dell&#39;elemento. Inserite il valore restituito in `Element`. Impostate un valore per l&#39; `PDF` elemento chiamandone il `setAttribute` metodo. Aggiungete l&#39; `PDF` elemento all&#39; `PDFsFromBookmarks` elemento chiamando il metodo dell&#39; `PDFsFromBookmarks` elemento `appendChild` . Passate l&#39;oggetto `PDF` element come argomento. Le seguenti righe di codice mostrano la logica di questa applicazione:

      ` Element PDF = (Element)document.createElement("PDF");  PDF.setAttribute("source","AssemblerResultPDF.pdf");  PDFsFromBookmarks.appendChild(PDF);`

1. Convertire il documento DDX.

   * Creare un `javax.xml.transform.Transformer` oggetto richiamando il `javax.xml.transform.Transformer` metodo statico dell&#39;oggetto `newInstance` .
   * Creare un `Transformer` oggetto richiamando il `TransformerFactory` metodo dell&#39; `newTransformer` oggetto.
   * Creare un `ByteArrayOutputStream` oggetto utilizzando il relativo costruttore.
   * Creare un `javax.xml.transform.dom.DOMSource` oggetto utilizzando il relativo costruttore. Passa l&#39; `org.w3c.dom.Document` oggetto che rappresenta il documento DDX.
   * Creare un `javax.xml.transform.dom.DOMSource` oggetto utilizzando il relativo costruttore e passando l&#39; `ByteArrayOutputStream` oggetto.
   * Compilare l&#39;oggetto Java `ByteArrayOutputStream` richiamando il `javax.xml.transform.Transformer` metodo dell&#39; `transform` oggetto. Passate gli `javax.xml.transform.dom.DOMSource` oggetti e gli `javax.xml.transform.stream.StreamResult` oggetti.
   * Creare un array di byte e allocare la dimensione dell&#39; `ByteArrayOutputStream` oggetto all&#39;array di byte.
   * Compilare l&#39;array di byte richiamando il metodo dell&#39; `ByteArrayOutputStream` oggetto `toByteArray` .
   * Creare un `com.adobe.idp.Document` oggetto utilizzando il relativo costruttore e passando l&#39;array di byte.

1. Fare riferimento a un documento PDF per smontare.

   * Creare un oggetto `java.util.Map` utilizzato per memorizzare i documenti PDF di input utilizzando un `HashMap` costruttore.
   * Creare un `java.io.FileInputStream` oggetto utilizzando il relativo costruttore e passare la posizione del documento PDF da smontare.
   * Create a `com.adobe.idp.Document` object. Trasmettere l&#39; `java.io.FileInputStream` oggetto che contiene il documento PDF per smontare.
   * Aggiungere una voce all&#39; `java.util.Map` oggetto richiamandone il `put` metodo e passando gli argomenti seguenti:

      * Un valore di stringa che rappresenta il nome della chiave. Questo valore deve corrispondere al valore dell&#39;elemento di origine PDF specificato nel documento DDX. Nel documento DDX creato in modo dinamico, il valore è `AssemblerResultPDF.pdf`.
      * Un `com.adobe.idp.Document` oggetto che contiene il documento PDF da smontare.

1. Impostare le opzioni di esecuzione.

   * Creare un `AssemblerOptionSpec` oggetto che memorizza le opzioni di esecuzione utilizzando il relativo costruttore.
   * Impostate le opzioni di runtime per soddisfare i requisiti aziendali richiamando un metodo che appartiene all&#39; `AssemblerOptionSpec` oggetto. Ad esempio, per indicare al servizio Assembler di continuare a elaborare un processo quando si verifica un errore, richiamare il metodo dell&#39; `AssemblerOptionSpec` oggetto `setFailOnError` e passare `false`.

1. Smontare il documento PDF.

   Richiama il metodo dell’ `AssemblerServiceClient` oggetto `invokeDDX` e passa i seguenti valori:

   * Un `com.adobe.idp.Document` oggetto che rappresenta il documento DDX creato dinamicamente
   * Un `java.util.Map` oggetto che contiene il documento PDF da smontare
   * Un `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` oggetto che specifica le opzioni di esecuzione, incluso il font predefinito e il livello di registro del processo

   Il `invokeDDX` metodo restituisce un `com.adobe.livecycle.assembler.client.AssemblerResult` oggetto che contiene i documenti PDF disassemblati ed eventuali eccezioni.

1. Salvare i documenti PDF smontati.

   Per ottenere i documenti PDF disassemblati, effettuare le seguenti operazioni:

   * Richiama il metodo dell’ `AssemblerResult` oggetto `getDocuments` . Questo metodo restituisce un `java.util.Map` oggetto.
   * Eseguire un&#39;iterazione sull&#39; `java.util.Map` oggetto fino a individuare l&#39; `com.adobe.idp.Document` oggetto risultante.
   * Richiamare il metodo dell&#39; `com.adobe.idp.Document` oggetto `copyToFile` per estrarre il documento PDF.

**Consulta anche**

[Avvio rapido (modalità SOAP): Creazione dinamica di un documento DDX utilizzando l&#39;API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-dynamically-creating-a-ddx-document-using-the-java-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Creare in modo dinamico un documento DDX utilizzando l&#39;API del servizio Web {#dynamically-create-a-ddx-document-using-the-web-service-api}

Creare in modo dinamico un documento DDX e smontare un documento PDF utilizzando l&#39;API Assembler Service (servizio Web):

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

1. Creare il documento DDX.

   * Creare un `System.Xml.XmlElement` oggetto utilizzando il relativo costruttore.
   * Creare l&#39;elemento principale del documento DDX richiamando il `XmlElement` metodo dell&#39; `CreateElement` oggetto. Questo metodo crea un `Element` oggetto che rappresenta l&#39;elemento principale. Passate al `CreateElement` metodo un valore di stringa che rappresenta il nome dell&#39;elemento. Impostate un valore per l&#39;elemento DDX chiamandone il `SetAttribute` metodo. Infine, aggiungere l&#39;elemento al documento DDX chiamando il `XmlElement` metodo dell&#39;oggetto `AppendChild` . Passa l&#39;oggetto DDX come argomento. Le seguenti righe di codice mostrano questa logica di applicazione:

      ` System.Xml.XmlElement root = ddx.CreateElement("DDX");  root.SetAttribute("xmlns", "https://ns.adobe.com/DDX/1.0/");  ddx.AppendChild(root);`

   * Creare l&#39; `PDFsFromBookmarks` elemento del documento DDX chiamando il `XmlElement` metodo dell&#39; `CreateElement` oggetto. Passate al `CreateElement` metodo un valore di stringa che rappresenta il nome dell&#39;elemento. Quindi, impostate un valore per l&#39;elemento chiamandone il `SetAttribute` metodo. Aggiungete l&#39; `PDFsFromBookmarks` elemento all&#39;elemento principale chiamando il metodo dell&#39; `DDX` elemento `AppendChild` . Passate l&#39;oggetto `PDFsFromBookmarks` element come argomento. Le seguenti righe di codice mostrano questa logica di applicazione:

      ` XmlElement PDFsFromBookmarks = ddx.CreateElement("PDFsFromBookmarks");  PDFsFromBookmarks.SetAttribute("prefix", "stmt");  root.AppendChild(PDFsFromBookmarks);`

   * Creare l&#39; `PDF` elemento del documento DDX chiamando il `XmlElement` metodo dell&#39; `CreateElement` oggetto. Passate al `CreateElement` metodo un valore di stringa che rappresenta il nome dell&#39;elemento. Quindi, impostate un valore per l’elemento secondario chiamandone il `SetAttribute` metodo. Aggiungete l&#39; `PDF` elemento all&#39; `PDFsFromBookmarks` elemento chiamando il metodo dell&#39; `PDFsFromBookmarks` elemento `AppendChild` . Passate l&#39;oggetto `PDF` element come argomento. Le seguenti righe di codice mostrano la logica di questa applicazione:

      ` XmlElement PDF = ddx.CreateElement("PDF");  PDF.SetAttribute("source", "AssemblerResultPDF.pdf");  PDFsFromBookmarks.AppendChild(PDF);`

1. Convertire il documento DDX.

   * Creare un `System.IO.MemoryStream` oggetto utilizzando il relativo costruttore.
   * Compilare l&#39; `MemoryStream` oggetto con il documento DDX utilizzando l&#39; `XmlElement` oggetto che rappresenta il documento DDX. Richiamare il metodo dell&#39; `XmlElement` oggetto `Save` e passare l&#39; `MemoryStream` oggetto.
   * Creare un array di byte e compilarlo con i dati che si trovano nell&#39; `MemoryStream` oggetto. Il codice seguente mostra la logica di questa applicazione:

      ` int bufLen = Convert.ToInt32(stream.Length);  byte[] byteArray = new byte[bufLen];  stream.Position = 0;  int count = stream.Read(byteArray, 0, bufLen);`

   * Create a `BLOB` object. Assegnare l&#39;array di byte al campo dell&#39; `BLOB` oggetto `MTOM` .

1. Fare riferimento a un documento PDF per smontare.

   * Creare un `BLOB` oggetto utilizzando il relativo costruttore. L&#39; `BLOB` oggetto viene utilizzato per memorizzare il documento PDF di input. Questo `BLOB` oggetto viene passato all&#39;oggetto `invokeOneDocument` come argomento.
   * Creare un `System.IO.FileStream` oggetto richiamandone il costruttore. Passa un valore di stringa che rappresenta la posizione del file del documento PDF di input e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto dell&#39; `System.IO.FileStream` oggetto. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà dell&#39; `System.IO.FileStream` oggetto `Length` .
   * Compilare l&#39;array di byte con i dati del flusso richiamando il `System.IO.FileStream` `Read` metodo dell&#39;oggetto e passando l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39; `BLOB` oggetto assegnando alla `MTOM` proprietà il contenuto dell&#39;array di byte.

1. Impostare le opzioni di esecuzione.

   * Creare un `AssemblerOptionSpec` oggetto che memorizza le opzioni di esecuzione utilizzando il relativo costruttore.
   * Impostare le opzioni di runtime per soddisfare i requisiti aziendali assegnando un valore a un membro di dati che appartiene all&#39; `AssemblerOptionSpec` oggetto. Ad esempio, per indicare al servizio Assembler di continuare l&#39;elaborazione di un processo in caso di errore, assegnare `false` al membro `AssemblerOptionSpec` dati dell&#39; `failOnError` oggetto.

1. Smontare il documento PDF.

   Richiama il metodo dell’ `AssemblerServiceClient` oggetto `invokeDDX` e passa i seguenti valori:

   * Un `BLOB` oggetto che rappresenta il documento DDX creato dinamicamente
   * L&#39; `mapItem` array che contiene il documento PDF di input
   * Un oggetto `AssemblerOptionSpec` che specifica le opzioni di esecuzione

   Il `invokeDDX` metodo restituisce un `AssemblerResult` oggetto che contiene i risultati del processo ed eventuali eccezioni.

1. Salvare i documenti PDF smontati.

   Per ottenere i documenti PDF appena creati, effettuare le seguenti operazioni:

   * Accedere al campo dell&#39; `AssemblerResult` oggetto `documents` , ovvero un `Map` oggetto che contiene i documenti PDF smontati.
   * Eseguire un&#39;iterazione sull&#39; `Map` oggetto per ottenere ogni documento risultante. Quindi, inserite il membro dell&#39;array `value` in un `BLOB`.
   * Estrarre i dati binari che rappresentano il documento PDF accedendo alla `BLOB` proprietà dell&#39; `MTOM` oggetto. Questo restituisce un array di byte che è possibile scrivere in un file PDF.

**Consulta anche**

[Chiamata di AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chiamata di AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
