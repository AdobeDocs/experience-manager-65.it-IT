---
title: Creazione dinamica di documenti DDX
seo-title: Creazione dinamica di documenti DDX
description: Crea un documento DDX in modo dinamico utilizzando l’API Java e l’API Web Service. La creazione dinamica di un documento DDX consente di utilizzare i valori nel documento DDX ottenuti durante l'esecuzione.
seo-description: Crea un documento DDX in modo dinamico utilizzando l’API Java e l’API Web Service. La creazione dinamica di un documento DDX consente di utilizzare i valori nel documento DDX ottenuti durante l'esecuzione.
uuid: b73e8069-6c9f-4517-a0ae-f3d503191d2d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 2ad227de-68a8-446f-8c4f-a33a6f95bec8
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2200'
ht-degree: 0%

---


# Creazione dinamica di documenti DDX {#dynamically-creating-ddx-documents}

**Esempi ed esempi in questo documento sono solo per AEM Forms in ambiente JEE.**

È possibile creare in modo dinamico un documento DDX che può essere utilizzato per eseguire un&#39;operazione Assembler. La creazione dinamica di un documento DDX consente di utilizzare i valori nel documento DDX ottenuti durante l&#39;esecuzione. Per creare in modo dinamico un documento DDX, utilizzare le classi che appartengono al linguaggio di programmazione utilizzato. Ad esempio, se stai sviluppando l’applicazione client utilizzando Java, utilizza le classi che appartengono al pacchetto `org.w3c.dom.*`. Analogamente, se si utilizza Microsoft .NET, utilizzare le classi che appartengono allo spazio dei nomi `System.Xml`.

Prima di passare il documento DDX al servizio Assembler, convertire l&#39;XML da un&#39;istanza `org.w3c.dom.Document` a un&#39;istanza `com.adobe.idp.Document`. Se utilizzi servizi web, converti l’XML dal tipo di dati utilizzato per creare l’XML (ad esempio, `XmlDocument`) in un’istanza `BLOB`.

Per questa discussione, si supponga che il seguente documento DDX venga creato in modo dinamico.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
      <PDFsFromBookmarks prefix="stmt">
     <PDF source="AssemblerResultPDF.pdf"/>
 </PDFsFromBookmarks>
 </DDX>
```

Questo documento DDX smonta un documento PDF. Si consiglia di avere familiarità con la scomposizione dei documenti PDF.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Assembler, vedere [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Per ulteriori informazioni su un documento DDX, vedere [Servizio Assembler e Riferimento DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Riepilogo dei passaggi {#summary-of-steps}

Per smontare un documento PDF utilizzando un documento DDX creato in modo dinamico, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Creare un client Assembler PDF.
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

**Creare un client Assembler PDF**

Prima di eseguire un&#39;operazione Assembler a livello di programmazione, creare un client di servizio Assembler.

**Creare il documento DDX**

Creare un documento DDX utilizzando il linguaggio di programmazione utilizzato. Per creare un documento DDX che smonti un documento PDF, assicurati che contenga l&#39;elemento `PDFsFromBookmarks` . Converti il tipo di dati utilizzato per creare il documento DDX in un&#39;istanza `com.adobe.idp.Document` se utilizzi l&#39;API Java. Se utilizzi servizi web, converti il tipo di dati in un’istanza `BLOB`.

**Conversione del documento DDX**

Un documento DDX creato utilizzando le classi `org.w3c.dom` deve essere convertito in un oggetto `com.adobe.idp.Document`. Per eseguire questa attività quando si utilizza l&#39;API Java, utilizzare le classi di trasformazione Java XML. Se utilizzi servizi Web, converti il documento DDX in un oggetto `BLOB`.

**Riferimento a un documento PDF da smontare**

Per smontare un documento PDF, fare riferimento a un file PDF che rappresenta il documento PDF da smontare. Quando viene passato al servizio Assembler, viene restituito un documento PDF separato per ogni segnalibro di livello 1 nel documento.

**Impostare le opzioni di esecuzione**

È possibile impostare le opzioni di esecuzione che controllano il comportamento del servizio Assembler mentre esegue un processo. Ad esempio, è possibile impostare un&#39;opzione che indica al servizio Assembler di continuare l&#39;elaborazione di un processo in caso di errore. Per impostare le opzioni di esecuzione, utilizzare un oggetto `AssemblerOptionSpec`.

**Smontare il documento PDF**

Smontare il documento PDF richiamando l&#39;operazione `invokeDDX`. Passa il documento DDX creato in modo dinamico. Il servizio Assembler restituisce documenti PDF smontati all&#39;interno di un oggetto raccolta.

**Salvare i documenti PDF smontati**

Tutti i documenti PDF smontati vengono restituiti all&#39;interno di un oggetto raccolta. Iterare l&#39;oggetto raccolta e salvare ogni documento PDF come file PDF.

**Consulta anche**

[Creare in modo dinamico un documento DDX utilizzando l’API Java](/help/forms/developing/dynamically-creating-ddx-documents.md#dynamically-create-a-ddx-document-using-the-java-api)

[Creare in modo dinamico un documento DDX utilizzando l’API del servizio Web](/help/forms/developing/dynamically-creating-ddx-documents.md#dynamically-create-a-ddx-document-using-the-web-service-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Smontaggio programmatico dei documenti PDF](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

## Creare in modo dinamico un documento DDX utilizzando l&#39;API Java {#dynamically-create-a-ddx-document-using-the-java-api}

Creare in modo dinamico un documento DDX e smontare un documento PDF utilizzando l&#39;API del servizio Assembler (Java):

1. Includi file di progetto.

   Includi file JAR client, come adobe-assembler-client.jar, nel percorso di classe del progetto Java.

1. Creare un client Assembler PDF.

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `AssemblerServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Crea il documento DDX.

   * Crea un oggetto Java `DocumentBuilderFactory` chiamando il metodo `DocumentBuilderFactory` class’ `newInstance` .
   * Crea un oggetto Java `DocumentBuilder` chiamando il metodo `DocumentBuilderFactory` dell&#39;oggetto `newDocumentBuilder` .
   * Chiama il metodo `newDocument` dell&#39;oggetto `DocumentBuilder` per creare un&#39;istanza di un oggetto `org.w3c.dom.Document`.
   * Creare l&#39;elemento principale del documento DDX richiamando il metodo `org.w3c.dom.Document` dell&#39;oggetto `createElement`. Questo metodo crea un oggetto `Element` che rappresenta l&#39;elemento principale. Passa al metodo `createElement` un valore stringa che rappresenta il nome dell&#39;elemento. Imposta il valore restituito su `Element`. Quindi, imposta un valore per l’elemento figlio chiamandone il metodo `setAttribute` . Infine, aggiungi l’elemento all’elemento header chiamando il metodo `appendChild` dell’elemento header e passa l’oggetto elemento figlio come argomento. Le seguenti righe di codice mostrano questa logica di applicazione:
      ` Element root = (Element)document.createElement("DDX");  root.setAttribute("xmlns","https://ns.adobe.com/DDX/1.0/");  document.appendChild(root);`

   * Crea l’elemento `PDFsFromBookmarks` chiamando il metodo `Document` dell’oggetto `createElement` . Passa al metodo `createElement` un valore stringa che rappresenta il nome dell&#39;elemento. Imposta il valore restituito su `Element`. Imposta un valore per l&#39;elemento `PDFsFromBookmarks` chiamandone il metodo `setAttribute` . Aggiungi l’elemento `PDFsFromBookmarks` all’elemento `DDX` chiamando il metodo `appendChild` dell’elemento DDX. Passa l’oggetto elemento `PDFsFromBookmarks` come argomento. Le seguenti righe di codice mostrano questa logica di applicazione:

      ` Element PDFsFromBookmarks = (Element)document.createElement("PDFsFromBookmarks");  PDFsFromBookmarks.setAttribute("prefix","stmt");  root.appendChild(PDFsFromBookmarks);`

   * Crea un elemento `PDF` chiamando il metodo `Document` dell&#39;oggetto `createElement` . Passa un valore stringa che rappresenta il nome dell&#39;elemento. Imposta il valore restituito su `Element`. Imposta un valore per l&#39;elemento `PDF` chiamandone il metodo `setAttribute` . Aggiungi l’elemento `PDF` all’elemento `PDFsFromBookmarks` chiamando il metodo `PDFsFromBookmarks` dell’elemento `appendChild` . Passa l’oggetto elemento `PDF` come argomento. Le seguenti righe di codice mostrano questa logica di applicazione:

      ` Element PDF = (Element)document.createElement("PDF");  PDF.setAttribute("source","AssemblerResultPDF.pdf");  PDFsFromBookmarks.appendChild(PDF);`

1. Convertire il documento DDX.

   * Creare un oggetto `javax.xml.transform.Transformer` richiamando il metodo statico `javax.xml.transform.Transformer` dell&#39;oggetto `newInstance`.
   * Creare un oggetto `Transformer` richiamando il metodo `TransformerFactory` dell&#39;oggetto `newTransformer`.
   * Creare un oggetto `ByteArrayOutputStream` utilizzando il relativo costruttore.
   * Creare un oggetto `javax.xml.transform.dom.DOMSource` utilizzando il relativo costruttore. Passa l&#39;oggetto `org.w3c.dom.Document` che rappresenta il documento DDX.
   * Creare un oggetto `javax.xml.transform.dom.DOMSource` utilizzando il relativo costruttore e passando l&#39;oggetto `ByteArrayOutputStream`.
   * Compilare l&#39;oggetto Java `ByteArrayOutputStream` richiamando il metodo `javax.xml.transform.Transformer` dell&#39;oggetto `transform`. Passa gli oggetti `javax.xml.transform.dom.DOMSource` e `javax.xml.transform.stream.StreamResult` .
   * Creare una matrice di byte e allocare la dimensione dell&#39;oggetto `ByteArrayOutputStream` all&#39;array di byte.
   * Compilare la matrice dei byte richiamando il metodo `toByteArray` dell&#39;oggetto `ByteArrayOutputStream`.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando la matrice dei byte.

1. Fare riferimento a un documento PDF per smontare.

   * Creare un oggetto `java.util.Map` utilizzato per memorizzare i documenti PDF di input utilizzando un costruttore `HashMap`.
   * Creare un oggetto `java.io.FileInputStream` utilizzando il relativo costruttore e passando la posizione del documento PDF da smontare.
   * Creare un oggetto `com.adobe.idp.Document`. Passa l&#39;oggetto `java.io.FileInputStream` che contiene il documento PDF da smontare.
   * Aggiungere una voce all&#39;oggetto `java.util.Map` richiamando il relativo metodo `put` e passando i seguenti argomenti:

      * Valore stringa che rappresenta il nome della chiave. Questo valore deve corrispondere al valore dell&#39;elemento di origine PDF specificato nel documento DDX. Nel documento DDX creato in modo dinamico, il valore è `AssemblerResultPDF.pdf`.
      * Un oggetto `com.adobe.idp.Document` contenente il documento PDF da smontare.

1. Impostare le opzioni di esecuzione.

   * Creare un oggetto `AssemblerOptionSpec` che memorizza le opzioni di esecuzione utilizzando il relativo costruttore.
   * Impostare le opzioni di esecuzione per soddisfare i requisiti aziendali richiamando un metodo appartenente all&#39;oggetto `AssemblerOptionSpec`. Ad esempio, per dare istruzioni al servizio Assembler di continuare a elaborare un processo quando si verifica un errore, richiamare il metodo `setFailOnError` dell&#39;oggetto `AssemblerOptionSpec` e passare `false`.

1. Smontare il documento PDF.

   Richiama il metodo `invokeDDX` dell&#39;oggetto `AssemblerServiceClient` e passa i seguenti valori:

   * Un oggetto `com.adobe.idp.Document` che rappresenta il documento DDX creato dinamicamente
   * Un oggetto `java.util.Map` che contiene il documento PDF da smontare
   * Un oggetto `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` che specifica le opzioni di esecuzione, incluso il font predefinito e il livello di log del processo

   Il metodo `invokeDDX` restituisce un oggetto `com.adobe.livecycle.assembler.client.AssemblerResult` contenente i documenti PDF smontati ed eventuali eccezioni.

1. Salvare i documenti PDF smontati.

   Per ottenere i documenti PDF smontati, eseguire le operazioni seguenti:

   * Richiama il metodo `getDocuments` dell&#39;oggetto `AssemblerResult`. Questo metodo restituisce un oggetto `java.util.Map`.
   * Iterare l&#39;oggetto `java.util.Map` fino a trovare l&#39;oggetto `com.adobe.idp.Document` risultante.
   * Richiamare il metodo `copyToFile` dell&#39;oggetto `com.adobe.idp.Document` per estrarre il documento PDF.

**Consulta anche**

[Avvio rapido (modalità SOAP): Creazione dinamica di un documento DDX utilizzando l’API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-dynamically-creating-a-ddx-document-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Creare in modo dinamico un documento DDX utilizzando l&#39;API del servizio Web {#dynamically-create-a-ddx-document-using-the-web-service-api}

Creare in modo dinamico un documento DDX e smontare un documento PDF utilizzando l&#39;API del servizio Assembler (servizio Web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Quando imposti un riferimento a un servizio, assicurati di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Creare un client Assembler PDF.

   * Creare un oggetto `AssemblerServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `AssemblerServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). Non è necessario utilizzare l&#39;attributo `lc_version` . Questo attributo viene utilizzato quando si crea un riferimento a un servizio.
   * Crea un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `AssemblerServiceClient.Endpoint.Binding` . Imposta il valore restituito su `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegna il nome utente del modulo di AEM al campo `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore della password corrispondente al campo `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Crea il documento DDX.

   * Creare un oggetto `System.Xml.XmlElement` utilizzando il relativo costruttore.
   * Creare l&#39;elemento principale del documento DDX richiamando il metodo `XmlElement` dell&#39;oggetto `CreateElement`. Questo metodo crea un oggetto `Element` che rappresenta l&#39;elemento principale. Passa al metodo `CreateElement` un valore stringa che rappresenta il nome dell&#39;elemento. Imposta un valore per l&#39;elemento DDX chiamandone il metodo `SetAttribute` . Infine, aggiungi l’elemento al documento DDX chiamando il metodo `XmlElement` dell’oggetto `AppendChild` . Passa l&#39;oggetto DDX come argomento. Le seguenti righe di codice mostrano questa logica di applicazione:

      ` System.Xml.XmlElement root = ddx.CreateElement("DDX");  root.SetAttribute("xmlns", "https://ns.adobe.com/DDX/1.0/");  ddx.AppendChild(root);`

   * Crea l&#39;elemento `PDFsFromBookmarks` del documento DDX chiamando il metodo `XmlElement` dell&#39;oggetto `CreateElement`. Passa al metodo `CreateElement` un valore stringa che rappresenta il nome dell&#39;elemento. Quindi, imposta un valore per l&#39;elemento chiamandone il metodo `SetAttribute` . Aggiungi l’elemento `PDFsFromBookmarks` all’elemento principale chiamando il metodo `DDX` dell’elemento `AppendChild` . Passa l’oggetto elemento `PDFsFromBookmarks` come argomento. Le seguenti righe di codice mostrano questa logica di applicazione:

      ` XmlElement PDFsFromBookmarks = ddx.CreateElement("PDFsFromBookmarks");  PDFsFromBookmarks.SetAttribute("prefix", "stmt");  root.AppendChild(PDFsFromBookmarks);`

   * Crea l&#39;elemento `PDF` del documento DDX chiamando il metodo `XmlElement` dell&#39;oggetto `CreateElement`. Passa al metodo `CreateElement` un valore stringa che rappresenta il nome dell&#39;elemento. Quindi, imposta un valore per l’elemento figlio chiamandone il metodo `SetAttribute` . Aggiungi l’elemento `PDF` all’elemento `PDFsFromBookmarks` chiamando il metodo `PDFsFromBookmarks` dell’elemento `AppendChild` . Passa l’oggetto elemento `PDF` come argomento. Le seguenti righe di codice mostrano questa logica di applicazione:

      ` XmlElement PDF = ddx.CreateElement("PDF");  PDF.SetAttribute("source", "AssemblerResultPDF.pdf");  PDFsFromBookmarks.AppendChild(PDF);`

1. Convertire il documento DDX.

   * Creare un oggetto `System.IO.MemoryStream` utilizzando il relativo costruttore.
   * Compilare l&#39;oggetto `MemoryStream` con il documento DDX utilizzando l&#39;oggetto `XmlElement` che rappresenta il documento DDX. Richiamare il metodo `Save` dell&#39;oggetto `XmlElement` e passare l&#39;oggetto `MemoryStream`.
   * Creare una matrice di byte e compilarla con dati che si trovano nell&#39;oggetto `MemoryStream`. Il codice seguente mostra questa logica di applicazione:

      ` int bufLen = Convert.ToInt32(stream.Length);  byte[] byteArray = new byte[bufLen];  stream.Position = 0;  int count = stream.Read(byteArray, 0, bufLen);`

   * Creare un oggetto `BLOB`. Assegnare l’array di byte al campo `MTOM` dell’oggetto `BLOB`.

1. Fare riferimento a un documento PDF per smontare.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare il documento PDF di input. Questo oggetto `BLOB` viene passato a `invokeOneDocument` come argomento.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore. Passa un valore stringa che rappresenta la posizione del file del documento PDF di input e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni dell&#39;array di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare l’array di byte con i dati del flusso richiamando il metodo `Read` dell’oggetto `System.IO.FileStream` e passando l’array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando alla relativa proprietà `MTOM` il contenuto dell&#39;array di byte.

1. Impostare le opzioni di esecuzione.

   * Creare un oggetto `AssemblerOptionSpec` che memorizza le opzioni di esecuzione utilizzando il relativo costruttore.
   * Impostare le opzioni di esecuzione per soddisfare i requisiti aziendali assegnando un valore a un membro dati appartenente all&#39;oggetto `AssemblerOptionSpec`. Ad esempio, per dare istruzioni al servizio Assembler di continuare a elaborare un processo in caso di errore, assegna `false` al membro dati `AssemblerOptionSpec` dell&#39;oggetto `failOnError`.

1. Smontare il documento PDF.

   Richiama il metodo `invokeDDX` dell&#39;oggetto `AssemblerServiceClient` e passa i seguenti valori:

   * Un oggetto `BLOB` che rappresenta il documento DDX creato dinamicamente
   * Array `mapItem` contenente il documento PDF di input
   * Un oggetto `AssemblerOptionSpec` che specifica le opzioni di esecuzione

   Il metodo `invokeDDX` restituisce un oggetto `AssemblerResult` contenente i risultati del processo ed eventuali eccezioni.

1. Salvare i documenti PDF smontati.

   Per ottenere i documenti PDF appena creati, eseguire le operazioni seguenti:

   * Accedere al campo `documents` dell&#39;oggetto `AssemblerResult`, che è un oggetto `Map` che contiene i documenti PDF smontati.
   * Iterare attraverso l&#39;oggetto `Map` per ottenere ogni documento risultante. Quindi, eseguire il cast di `value` del membro della matrice su un `BLOB`.
   * Estrarre i dati binari che rappresentano il documento PDF accedendo alla proprietà `MTOM` dell’oggetto `BLOB` corrispondente. Restituisce una matrice di byte che è possibile scrivere in un file PDF.

**Consulta anche**

[Richiamo di AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamo di AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
