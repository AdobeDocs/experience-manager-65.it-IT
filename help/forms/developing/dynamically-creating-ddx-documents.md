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

È possibile creare in modo dinamico un documento DDX che può essere utilizzato per eseguire un&#39;operazione Assembler. La creazione dinamica di un documento DDX consente di utilizzare valori nel documento DDX ottenuti durante l&#39;esecuzione. Per creare in modo dinamico un documento DDX, utilizzare classi appartenenti al linguaggio di programmazione utilizzato. Ad esempio, se state sviluppando l&#39;applicazione client utilizzando Java, utilizzate le classi che appartengono al pacchetto `org.w3c.dom.*`. Analogamente, se si utilizza Microsoft .NET, utilizzare classi appartenenti allo spazio dei nomi `System.Xml`.

Prima di passare il documento DDX al servizio Assembler, convertire l&#39;XML da un&#39;istanza `org.w3c.dom.Document` in un&#39;istanza `com.adobe.idp.Document`. Se si utilizzano servizi Web, convertire l&#39;XML dal tipo di dati utilizzato per creare l&#39;XML (ad esempio, `XmlDocument`) in un&#39;istanza `BLOB`.

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
>Per ulteriori informazioni sul servizio Assembler, vedere [Guida di riferimento dei servizi per  AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Per ulteriori informazioni su un documento DDX, vedere [Servizio Assembler e Riferimento DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

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
* adobe-utilities.jar (richiesto se  AEM Forms è distribuito su JBoss)
* jbossall-client.jar (richiesto se  AEM Forms è distribuito su JBoss)

**Creare un client Assembler PDF**

Prima di eseguire un&#39;operazione Assembler a livello di programmazione, create un client di servizio Assembler.

**Creare il documento DDX**

Creare un documento DDX utilizzando il linguaggio di programmazione utilizzato. Per creare un documento DDX che smonti un documento PDF, assicurarsi che contenga l&#39;elemento `PDFsFromBookmarks`. Converti il tipo di dati utilizzato per creare il documento DDX in un&#39;istanza `com.adobe.idp.Document` se utilizzi l&#39;API Java. Se si utilizzano servizi Web, convertire il tipo di dati in un&#39;istanza `BLOB`.

**Conversione del documento DDX**

Un documento DDX creato utilizzando le classi `org.w3c.dom` deve essere convertito in un oggetto `com.adobe.idp.Document`. Per eseguire questa attività quando si utilizza l&#39;API Java, utilizzare le classi di trasformazione Java XML. Se si utilizzano i servizi Web, convertire il documento DDX in un oggetto `BLOB`.

**Riferimento a un documento PDF da smontare**

Per smontare un documento PDF, fare riferimento a un file PDF che rappresenta il documento PDF da smontare. Quando viene passato al servizio Assembler, viene restituito un documento PDF separato per ciascun segnalibro di livello 1 nel documento.

**Impostazione delle opzioni di esecuzione**

È possibile impostare opzioni di esecuzione che controllano il comportamento del servizio Assembler mentre esegue un processo. Ad esempio, potete impostare un&#39;opzione che indichi al servizio Assembler di continuare l&#39;elaborazione di un processo in caso di errore. Per impostare le opzioni di esecuzione, è necessario utilizzare un oggetto `AssemblerOptionSpec`.

**Smontare il documento PDF**

Smontare il documento PDF richiamando l&#39;operazione `invokeDDX`. Passa il documento DDX creato in modo dinamico. Il servizio Assembler restituisce documenti PDF smontati all&#39;interno di un oggetto raccolta.

**Salvare i documenti PDF smontati**

Tutti i documenti PDF disassemblati vengono restituiti all&#39;interno di un oggetto raccolta. Iterare l&#39;oggetto della raccolta e salvare ciascun documento PDF come file PDF.

**Consulta anche**

[Creare in modo dinamico un documento DDX utilizzando l&#39;API Java](/help/forms/developing/dynamically-creating-ddx-documents.md#dynamically-create-a-ddx-document-using-the-java-api)

[Creare in modo dinamico un documento DDX utilizzando l&#39;API del servizio Web](/help/forms/developing/dynamically-creating-ddx-documents.md#dynamically-create-a-ddx-document-using-the-web-service-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Scomposizione programmatica dei documenti PDF](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

## Creare in modo dinamico un documento DDX utilizzando l&#39;API Java {#dynamically-create-a-ddx-document-using-the-java-api}

Creare in modo dinamico un documento DDX e smontare un documento PDF utilizzando l&#39;API Assembler Service (Java):

1. Includere i file di progetto.

   Includete file JAR client, ad esempio adobe-assembler-client.jar, nel percorso di classe del progetto Java.

1. Creare un client Assembler PDF.

   * Creare un oggetto `ServiceClientFactory` che contiene le proprietà di connessione.
   * Creare un oggetto `AssemblerServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Creare il documento DDX.

   * Creare un oggetto Java `DocumentBuilderFactory` chiamando il metodo `DocumentBuilderFactory` class `newInstance`.
   * Creare un oggetto Java `DocumentBuilder` chiamando il metodo `DocumentBuilderFactory` dell&#39;oggetto `newDocumentBuilder`.
   * Chiamare il metodo `DocumentBuilder` dell&#39;oggetto `newDocument` per creare un&#39;istanza di un oggetto `org.w3c.dom.Document`.
   * Creare l&#39;elemento principale del documento DDX richiamando il metodo `org.w3c.dom.Document` dell&#39;oggetto `createElement`. Questo metodo crea un oggetto `Element` che rappresenta l&#39;elemento principale. Passate al metodo `createElement` un valore di stringa che rappresenta il nome dell&#39;elemento. Inserite il valore restituito in `Element`. Quindi, impostate un valore per l&#39;elemento secondario chiamandone il metodo `setAttribute`. Infine, aggiungete l&#39;elemento all&#39;elemento header chiamando il metodo dell&#39;elemento header `appendChild` e passate l&#39;oggetto dell&#39;elemento secondario come argomento. Le seguenti righe di codice mostrano questa logica di applicazione:
      ` Element root = (Element)document.createElement("DDX");  root.setAttribute("xmlns","https://ns.adobe.com/DDX/1.0/");  document.appendChild(root);`

   * Creare l&#39;elemento `PDFsFromBookmarks` chiamando il metodo `Document` dell&#39;oggetto `createElement`. Passate al metodo `createElement` un valore di stringa che rappresenta il nome dell&#39;elemento. Inserite il valore restituito in `Element`. Impostate un valore per l&#39;elemento `PDFsFromBookmarks` chiamandone il metodo `setAttribute`. Aggiungete l&#39;elemento `PDFsFromBookmarks` all&#39;elemento `DDX` chiamando il metodo `appendChild` dell&#39;elemento DDX. Passa l&#39;oggetto `PDFsFromBookmarks` come argomento. Le seguenti righe di codice mostrano questa logica di applicazione:

      ` Element PDFsFromBookmarks = (Element)document.createElement("PDFsFromBookmarks");  PDFsFromBookmarks.setAttribute("prefix","stmt");  root.appendChild(PDFsFromBookmarks);`

   * Create un elemento `PDF` chiamando il metodo `Document` dell&#39;oggetto `createElement`. Passate un valore di stringa che rappresenta il nome dell&#39;elemento. Inserite il valore restituito in `Element`. Impostate un valore per l&#39;elemento `PDF` chiamandone il metodo `setAttribute`. Aggiungete l&#39;elemento `PDF` all&#39;elemento `PDFsFromBookmarks` chiamando il metodo `PDFsFromBookmarks` dell&#39;elemento `appendChild`. Passa l&#39;oggetto `PDF` come argomento. Le seguenti righe di codice mostrano la logica di questa applicazione:

      ` Element PDF = (Element)document.createElement("PDF");  PDF.setAttribute("source","AssemblerResultPDF.pdf");  PDFsFromBookmarks.appendChild(PDF);`

1. Convertire il documento DDX.

   * Creare un oggetto `javax.xml.transform.Transformer` richiamando il metodo statico `javax.xml.transform.Transformer` dell&#39;oggetto `newInstance`.
   * Creare un oggetto `Transformer` richiamando il metodo `TransformerFactory` dell&#39;oggetto `newTransformer`.
   * Creare un oggetto `ByteArrayOutputStream` utilizzando il relativo costruttore.
   * Creare un oggetto `javax.xml.transform.dom.DOMSource` utilizzando il relativo costruttore. Passa l&#39;oggetto `org.w3c.dom.Document` che rappresenta il documento DDX.
   * Creare un oggetto `javax.xml.transform.dom.DOMSource` utilizzando il relativo costruttore e passando l&#39;oggetto `ByteArrayOutputStream`.
   * Compilare l&#39;oggetto Java `ByteArrayOutputStream` richiamando il metodo `javax.xml.transform.Transformer` dell&#39;oggetto `transform`. Passare gli oggetti `javax.xml.transform.dom.DOMSource` e `javax.xml.transform.stream.StreamResult`.
   * Creare un array di byte e allocare la dimensione dell&#39;oggetto `ByteArrayOutputStream` all&#39;array di byte.
   * Compilare l&#39;array di byte richiamando il metodo `toByteArray` dell&#39;oggetto `ByteArrayOutputStream`.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;array di byte.

1. Fare riferimento a un documento PDF per smontare.

   * Creare un oggetto `java.util.Map` utilizzato per memorizzare i documenti PDF di input utilizzando un costruttore `HashMap`.
   * Creare un oggetto `java.io.FileInputStream` utilizzando il relativo costruttore e passando la posizione del documento PDF da smontare.
   * Creare un oggetto `com.adobe.idp.Document`. Passare l&#39;oggetto `java.io.FileInputStream` che contiene il documento PDF da smontare.
   * Aggiungere una voce all&#39;oggetto `java.util.Map` richiamandone il metodo `put` e trasmettendo gli argomenti seguenti:

      * Un valore di stringa che rappresenta il nome della chiave. Questo valore deve corrispondere al valore dell&#39;elemento di origine PDF specificato nel documento DDX. Nel documento DDX creato in modo dinamico, il valore è `AssemblerResultPDF.pdf`.
      * Un oggetto `com.adobe.idp.Document` che contiene il documento PDF da smontare.

1. Impostare le opzioni di esecuzione.

   * Creare un oggetto `AssemblerOptionSpec` che memorizza le opzioni di esecuzione utilizzando il relativo costruttore.
   * Impostate le opzioni di runtime per soddisfare i requisiti aziendali richiamando un metodo che appartiene all&#39;oggetto `AssemblerOptionSpec`. Ad esempio, per indicare al servizio Assembler di continuare a elaborare un processo quando si verifica un errore, richiamare il metodo `AssemblerOptionSpec` dell&#39;oggetto `setFailOnError` e passare `false`.

1. Smontare il documento PDF.

   Richiamare il metodo `AssemblerServiceClient` dell&#39;oggetto `invokeDDX` e trasmettere i seguenti valori:

   * Un oggetto `com.adobe.idp.Document` che rappresenta il documento DDX creato dinamicamente
   * Un oggetto `java.util.Map` che contiene il documento PDF da smontare
   * Un oggetto `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` che specifica le opzioni di esecuzione, incluso il font predefinito e il livello di registro del processo

   Il metodo `invokeDDX` restituisce un oggetto `com.adobe.livecycle.assembler.client.AssemblerResult` che contiene i documenti PDF smontati ed eventuali eccezioni.

1. Salvare i documenti PDF smontati.

   Per ottenere i documenti PDF disassemblati, effettuare le seguenti operazioni:

   * Richiamare il metodo `AssemblerResult` dell&#39;oggetto `getDocuments`. Questo metodo restituisce un oggetto `java.util.Map`.
   * Iterate l&#39;oggetto `java.util.Map` fino a individuare l&#39;oggetto `com.adobe.idp.Document` risultante.
   * Richiamare il metodo `com.adobe.idp.Document` dell&#39;oggetto `copyToFile` per estrarre il documento PDF.

**Consulta anche**

[Avvio rapido (modalità SOAP): Creazione dinamica di un documento DDX utilizzando l&#39;API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-dynamically-creating-a-ddx-document-using-the-java-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Creare in modo dinamico un documento DDX utilizzando l&#39;API del servizio Web {#dynamically-create-a-ddx-document-using-the-web-service-api}

Creare in modo dinamico un documento DDX e smontare un documento PDF utilizzando l&#39;API Assembler Service (servizio Web):

1. Includere i file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Quando imposti un riferimento a un servizio, accertatevi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

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

1. Creare il documento DDX.

   * Creare un oggetto `System.Xml.XmlElement` utilizzando il relativo costruttore.
   * Creare l&#39;elemento principale del documento DDX richiamando il metodo `XmlElement` dell&#39;oggetto `CreateElement`. Questo metodo crea un oggetto `Element` che rappresenta l&#39;elemento principale. Passate al metodo `CreateElement` un valore di stringa che rappresenta il nome dell&#39;elemento. Impostate un valore per l&#39;elemento DDX chiamandone il metodo `SetAttribute`. Infine, aggiungere l&#39;elemento al documento DDX chiamando il metodo `XmlElement` dell&#39;oggetto `AppendChild`. Passa l&#39;oggetto DDX come argomento. Le seguenti righe di codice mostrano questa logica di applicazione:

      ` System.Xml.XmlElement root = ddx.CreateElement("DDX");  root.SetAttribute("xmlns", "https://ns.adobe.com/DDX/1.0/");  ddx.AppendChild(root);`

   * Creare l&#39;elemento `PDFsFromBookmarks` del documento DDX chiamando il metodo `XmlElement` dell&#39;oggetto `CreateElement`. Passate al metodo `CreateElement` un valore di stringa che rappresenta il nome dell&#39;elemento. Quindi, impostate un valore per l&#39;elemento chiamandone il metodo `SetAttribute`. Aggiungete l&#39;elemento `PDFsFromBookmarks` all&#39;elemento principale chiamando il metodo `DDX` dell&#39;elemento `AppendChild`. Passa l&#39;oggetto `PDFsFromBookmarks` come argomento. Le seguenti righe di codice mostrano questa logica di applicazione:

      ` XmlElement PDFsFromBookmarks = ddx.CreateElement("PDFsFromBookmarks");  PDFsFromBookmarks.SetAttribute("prefix", "stmt");  root.AppendChild(PDFsFromBookmarks);`

   * Creare l&#39;elemento `PDF` del documento DDX chiamando il metodo `XmlElement` dell&#39;oggetto `CreateElement`. Passate al metodo `CreateElement` un valore di stringa che rappresenta il nome dell&#39;elemento. Quindi, impostate un valore per l&#39;elemento secondario chiamandone il metodo `SetAttribute`. Aggiungete l&#39;elemento `PDF` all&#39;elemento `PDFsFromBookmarks` chiamando il metodo `PDFsFromBookmarks` dell&#39;elemento `AppendChild`. Passa l&#39;oggetto `PDF` come argomento. Le seguenti righe di codice mostrano la logica di questa applicazione:

      ` XmlElement PDF = ddx.CreateElement("PDF");  PDF.SetAttribute("source", "AssemblerResultPDF.pdf");  PDFsFromBookmarks.AppendChild(PDF);`

1. Convertire il documento DDX.

   * Creare un oggetto `System.IO.MemoryStream` utilizzando il relativo costruttore.
   * Compilare l&#39;oggetto `MemoryStream` con il documento DDX utilizzando l&#39;oggetto `XmlElement` che rappresenta il documento DDX. Richiamare il metodo `XmlElement` dell&#39;oggetto `Save` e passare l&#39;oggetto `MemoryStream`.
   * Creare un array di byte e compilarlo con i dati che si trovano nell&#39;oggetto `MemoryStream`. Il codice seguente mostra la logica di questa applicazione:

      ` int bufLen = Convert.ToInt32(stream.Length);  byte[] byteArray = new byte[bufLen];  stream.Position = 0;  int count = stream.Read(byteArray, 0, bufLen);`

   * Creare un oggetto `BLOB`. Assegnare l&#39;array di byte al campo `BLOB` dell&#39;oggetto `MTOM`.

1. Fare riferimento a un documento PDF per smontare.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare il documento PDF di input. Questo oggetto `BLOB` viene passato al `invokeOneDocument` come argomento.
   * Creare un oggetto `System.IO.FileStream` richiamandone il costruttore. Passa un valore di stringa che rappresenta la posizione del file del documento PDF di input e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà `System.IO.FileStream` dell&#39;oggetto `Length`.
   * Compilare l&#39;array di byte con i dati del flusso richiamando il metodo `Read` dell&#39;oggetto `System.IO.FileStream` e passando l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando alla relativa proprietà `MTOM` il contenuto dell&#39;array di byte.

1. Impostare le opzioni di esecuzione.

   * Creare un oggetto `AssemblerOptionSpec` che memorizza le opzioni di esecuzione utilizzando il relativo costruttore.
   * Impostare le opzioni di runtime per soddisfare i requisiti aziendali assegnando un valore a un membro di dati che appartiene all&#39;oggetto `AssemblerOptionSpec`. Ad esempio, per indicare al servizio Assembler di continuare l&#39;elaborazione di un processo in caso di errore, assegnare `false` al membro di dati `AssemblerOptionSpec` dell&#39;oggetto `failOnError`.

1. Smontare il documento PDF.

   Richiamare il metodo `AssemblerServiceClient` dell&#39;oggetto `invokeDDX` e trasmettere i seguenti valori:

   * Un oggetto `BLOB` che rappresenta il documento DDX creato dinamicamente
   * L&#39;array `mapItem` che contiene il documento PDF di input
   * Un oggetto `AssemblerOptionSpec` che specifica le opzioni di esecuzione

   Il metodo `invokeDDX` restituisce un oggetto `AssemblerResult` che contiene i risultati del processo ed eventuali eccezioni.

1. Salvare i documenti PDF smontati.

   Per ottenere i documenti PDF appena creati, effettuare le seguenti operazioni:

   * Accedere al campo `documents` dell&#39;oggetto `AssemblerResult`, che è un oggetto `Map` contenente i documenti PDF smontati.
   * Iterate l&#39;oggetto `Map` per ottenere ogni documento risultante. Quindi, proiettare l&#39;elemento `value` del membro della matrice su un elemento `BLOB`.
   * Estrarre i dati binari che rappresentano il documento PDF accedendo alla proprietà `BLOB` dell&#39;oggetto `MTOM`. Questo restituisce un array di byte che è possibile scrivere in un file PDF.

**Consulta anche**

[Chiamata  AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chiamata  AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
