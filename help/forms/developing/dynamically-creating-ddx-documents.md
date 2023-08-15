---
title: Creazione dinamica di documenti DDX
seo-title: Dynamically Creating DDX Documents
description: Creare un documento DDX in modo dinamico utilizzando l'API Java e l'API del servizio Web. La creazione dinamica di un documento DDX consente di utilizzare nel documento DDX i valori ottenuti durante l'esecuzione.
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
source-git-commit: 10227bcfcfd5a9b0f126fee74dce6ec7842f5e95
workflow-type: tm+mt
source-wordcount: '2163'
ht-degree: 0%

---

# Creazione dinamica di documenti DDX {#dynamically-creating-ddx-documents}

**Gli esempi e gli esempi contenuti in questo documento sono solo per l’ambiente AEM Forms su JEE.**

È possibile creare in modo dinamico un documento DDX che può essere utilizzato per eseguire un&#39;operazione Assembler. La creazione dinamica di un documento DDX consente di utilizzare nel documento DDX i valori ottenuti durante l&#39;esecuzione. Per creare in modo dinamico un documento DDX, utilizzare le classi che appartengono al linguaggio di programmazione in uso. Ad esempio, se sviluppi l’applicazione client utilizzando Java, utilizza le classi che appartengono al `org.w3c.dom.*`pacchetto. Analogamente, se si utilizza Microsoft .NET, utilizzare le classi che appartengono al `System.Xml` spazio dei nomi.

Prima di poter passare il documento DDX al servizio Assembler, convertire il codice XML da un `org.w3c.dom.Document` istanza a un `com.adobe.idp.Document` dell&#39;istanza. Se si utilizzano i servizi Web, convertire il codice XML dal tipo di dati utilizzato per creare il codice XML (ad esempio, `XmlDocument`) a un `BLOB` dell&#39;istanza.

Per questa discussione, si supponga che il seguente documento DDX venga creato in modo dinamico.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
      <PDFsFromBookmarks prefix="stmt">
     <PDF source="AssemblerResultPDF.pdf"/>
 </PDFsFromBookmarks>
 </DDX>
```

Questo documento DDX disassembla un documento PDF. È consigliabile avere familiarità con lo smontaggio dei documenti PDF.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Assembler, vedere [Guida di riferimento dei servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Per ulteriori informazioni su un documento DDX, vedere [Servizio assemblatore e riferimento DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Riepilogo dei passaggi {#summary-of-steps}

Per disassemblare un documento PDF utilizzando un documento DDX creato in modo dinamico, effettuare le seguenti operazioni:

1. Includi file di progetto.
1. Creare un client PDF Assembler.
1. Creare il documento DDX.
1. Converte il documento DDX.
1. Impostare le opzioni di runtime.
1. Disassemblare il documento PDF.
1. Salvare i documenti PDF disassemblati.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso della classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è implementato su JBoss)
* jbossall-client.jar (obbligatorio se AEM Forms è distribuito su JBoss)

**Creare un client PDF Assembler**

Prima di eseguire un&#39;operazione Assembler a livello di programmazione, creare un client del servizio Assembler.

**Creare il documento DDX**

Creare un documento DDX utilizzando il linguaggio di programmazione in uso. Per creare un documento DDX che disassembli un documento PDF, assicurarsi che contenga `PDFsFromBookmarks` elemento. Converte il tipo di dati utilizzato per creare il documento DDX in un `com.adobe.idp.Document` se utilizzi l’API Java. Se si utilizzano i servizi Web, convertire il tipo di dati in `BLOB` dell&#39;istanza.

**Convertire il documento DDX**

Documento DDX creato utilizzando `org.w3c.dom` le classi devono essere convertite in `com.adobe.idp.Document` oggetto. Per eseguire questa attività quando si utilizza l’API Java, utilizza le classi di trasformazione Java XML. Se si utilizzano i servizi Web, convertire il documento DDX in `BLOB` oggetto.

**Riferimento a un documento PDF da disassemblare**

Per disassemblare un documento PDF, fare riferimento a un file PDF che rappresenta il documento PDF da disassemblare. Quando viene passato al servizio Assembler, viene restituito un documento PDF separato per ogni segnalibro di livello 1 del documento.

**Impostare le opzioni di runtime**

È possibile impostare le opzioni di runtime che controllano il comportamento del servizio Assembler durante l&#39;esecuzione di un processo. È ad esempio possibile impostare un&#39;opzione che indichi al servizio Assembler di continuare l&#39;elaborazione di un processo in caso di errore. Per impostare le opzioni di run-time, utilizzare un `AssemblerOptionSpec` oggetto.

**Disassemblare il documento PDF**

Disassemblare il documento PDF richiamando `invokeDDX` operazione. Passa il documento DDX creato in modo dinamico. Il servizio Assembler restituisce documenti PDF disassemblati all&#39;interno di un oggetto insieme.

**Salvare i documenti PDF disassemblati**

Tutti i documenti PDF disassemblati vengono restituiti all&#39;interno di un insieme. Scorrere l&#39;oggetto insieme e salvare ogni documento PDF come file PDF.

**Consulta anche**

[Creare in modo dinamico un documento DDX utilizzando l’API Java](/help/forms/developing/dynamically-creating-ddx-documents.md#dynamically-create-a-ddx-document-using-the-java-api)

[Creare in modo dinamico un documento DDX utilizzando l’API del servizio web](/help/forms/developing/dynamically-creating-ddx-documents.md#dynamically-create-a-ddx-document-using-the-web-service-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Disassemblaggio di documenti PDF a livello di programmazione](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

## Creare in modo dinamico un documento DDX utilizzando l’API Java {#dynamically-create-a-ddx-document-using-the-java-api}

Creare in modo dinamico un documento DDX e disassemblare un documento PDF utilizzando l&#39;API del servizio Assembler (Java):

1. Includi file di progetto.

   Includi i file JAR client, come adobe-assembler-client.jar, nel percorso di classe del progetto Java.

1. Creare un client PDF Assembler.

   * Creare un `ServiceClientFactory` oggetto che contiene proprietà di connessione.
   * Creare un `AssemblerServiceClient` mediante il costruttore e passando il `ServiceClientFactory` oggetto.

1. Creare il documento DDX.

   * Creare un Java `DocumentBuilderFactory` oggetto chiamando il `DocumentBuilderFactory` class&#39; `newInstance` metodo.
   * Creare un Java `DocumentBuilder` oggetto chiamando il `DocumentBuilderFactory` dell&#39;oggetto `newDocumentBuilder` metodo.
   * Chiama il `DocumentBuilder` dell&#39;oggetto `newDocument` metodo per creare un&#39;istanza di `org.w3c.dom.Document` oggetto.
   * Creare l&#39;elemento radice del documento DDX richiamando `org.w3c.dom.Document` dell&#39;oggetto `createElement` metodo. Questo metodo crea un `Element` oggetto che rappresenta l&#39;elemento principale. Passa un valore stringa che rappresenta il nome dell’elemento al `createElement` metodo. Invia il valore restituito a `Element`. Quindi, imposta un valore per l’elemento figlio chiamando il relativo `setAttribute` metodo. Infine, aggiungi l’elemento all’elemento header chiamando l’ `appendChild` e passare l&#39;oggetto elemento figlio come argomento. Le seguenti righe di codice mostrano questa logica dell’applicazione:
     ` Element root = (Element)document.createElement("DDX");  root.setAttribute("xmlns","https://ns.adobe.com/DDX/1.0/");  document.appendChild(root);`

   * Creare `PDFsFromBookmarks` chiamando l&#39; `Document` dell&#39;oggetto `createElement` metodo. Passa un valore stringa che rappresenta il nome dell’elemento al `createElement` metodo. Invia il valore restituito a `Element`. Imposta un valore per `PDFsFromBookmarks` elemento chiamando il relativo `setAttribute` metodo. Aggiungi `PDFsFromBookmarks` elemento al `DDX` chiamando l&#39;elemento DDX `appendChild` metodo. Passa il `PDFsFromBookmarks` come argomento. Le seguenti righe di codice mostrano questa logica dell’applicazione:

     ` Element PDFsFromBookmarks = (Element)document.createElement("PDFsFromBookmarks");  PDFsFromBookmarks.setAttribute("prefix","stmt");  root.appendChild(PDFsFromBookmarks);`

   * Creare un `PDF` chiamando l&#39; `Document` dell&#39;oggetto `createElement` metodo. Passa un valore stringa che rappresenta il nome dell’elemento. Invia il valore restituito a `Element`. Imposta un valore per `PDF` elemento chiamando il relativo `setAttribute` metodo. Aggiungi `PDF` elemento al `PDFsFromBookmarks` chiamando l&#39; `PDFsFromBookmarks` dell&#39;elemento `appendChild` metodo. Passa il `PDF` come argomento. Le seguenti righe di codice mostrano questa logica dell’applicazione:

     ` Element PDF = (Element)document.createElement("PDF");  PDF.setAttribute("source","AssemblerResultPDF.pdf");  PDFsFromBookmarks.appendChild(PDF);`

1. Converte il documento DDX.

   * Creare un `javax.xml.transform.Transformer` oggetto richiamando il `javax.xml.transform.Transformer` statico dell&#39;oggetto `newInstance` metodo.
   * Creare un `Transformer` oggetto richiamando il `TransformerFactory` dell&#39;oggetto `newTransformer` metodo.
   * Creare un `ByteArrayOutputStream` mediante il costruttore.
   * Creare un `javax.xml.transform.dom.DOMSource` mediante il costruttore. Passa il `org.w3c.dom.Document` oggetto che rappresenta il documento DDX.
   * Creare un `javax.xml.transform.dom.DOMSource` mediante il costruttore e passando il `ByteArrayOutputStream` oggetto.
   * Popolare Java `ByteArrayOutputStream` oggetto richiamando il `javax.xml.transform.Transformer` dell&#39;oggetto `transform` metodo. Passa il `javax.xml.transform.dom.DOMSource` e `javax.xml.transform.stream.StreamResult` oggetti.
   * Creare una matrice di byte e allocare le dimensioni della `ByteArrayOutputStream` alla matrice di byte.
   * Popolare la matrice di byte richiamando `ByteArrayOutputStream` dell&#39;oggetto `toByteArray` metodo.
   * Creare un `com.adobe.idp.Document` mediante il costruttore e passando la matrice di byte.

1. Fare riferimento a un documento PDF da disassemblare.

   * Creare un `java.util.Map` oggetto utilizzato per memorizzare i documenti di input PDF utilizzando un `HashMap` costruttore.
   * Creare un `java.io.FileInputStream` mediante il costruttore e passando la posizione del documento PDF da disassemblare.
   * Creare un `com.adobe.idp.Document` oggetto. Passa il `java.io.FileInputStream` oggetto che contiene il documento PDF da disassemblare.
   * Aggiungi una voce al `java.util.Map` oggetto richiamando il relativo `put` e fornendo i seguenti argomenti:

      * Valore stringa che rappresenta il nome della chiave. Questo valore deve corrispondere al valore dell&#39;elemento di origine PDF specificato nel documento DDX. Nel documento DDX creato in modo dinamico, il valore è `AssemblerResultPDF.pdf`.)
      * A `com.adobe.idp.Document` oggetto che contiene il documento PDF da disassemblare.

1. Impostare le opzioni di runtime.

   * Creare un `AssemblerOptionSpec` oggetto che memorizza le opzioni di runtime mediante il relativo costruttore.
   * Impostare le opzioni di runtime per soddisfare i requisiti aziendali richiamando un metodo che appartiene al `AssemblerOptionSpec` oggetto. Ad esempio, per indicare al servizio Assembler di continuare l&#39;elaborazione di un processo quando si verifica un errore, richiamare `AssemblerOptionSpec` dell&#39;oggetto `setFailOnError` metodo e passaggio `false`.

1. Disassemblare il documento PDF.

   Richiama `AssemblerServiceClient` dell&#39;oggetto `invokeDDX` e trasmettere i seguenti valori:

   * A `com.adobe.idp.Document` oggetto che rappresenta il documento DDX creato in modo dinamico
   * A `java.util.Map` oggetto che contiene il documento PDF da disassemblare
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` oggetto che specifica le opzioni di runtime, inclusi il tipo di carattere predefinito e il livello di registro del processo

   Il `invokeDDX` il metodo restituisce un `com.adobe.livecycle.assembler.client.AssemblerResult` oggetto contenente i documenti PDF disassemblati ed eventuali eccezioni.

1. Salvare i documenti PDF disassemblati.

   Per ottenere i documenti PDF disassemblati, effettuare le seguenti operazioni:

   * Richiama `AssemblerResult` dell&#39;oggetto `getDocuments` metodo. Questo metodo restituisce un `java.util.Map` oggetto.
   * Effettua iterazione attraverso `java.util.Map` finché non viene individuato il risultato `com.adobe.idp.Document` oggetto.
   * Richiama `com.adobe.idp.Document` dell&#39;oggetto `copyToFile` per estrarre il documento PDF.

**Consulta anche**

[Quick Start (modalità SOAP): creazione dinamica di un documento DDX utilizzando l’API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-dynamically-creating-a-ddx-document-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Creare in modo dinamico un documento DDX utilizzando l’API del servizio web {#dynamically-create-a-ddx-document-using-the-web-service-api}

Creare in modo dinamico un documento DDX e disassemblare un documento PDF utilizzando l&#39;API del servizio Assembler (servizio Web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL durante l&#39;impostazione di un riferimento al servizio: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l’indirizzo IP del server che ospita AEM Forms.

1. Creare un client PDF Assembler.

   * Creare un `AssemblerServiceClient` utilizzando il costruttore predefinito.
   * Creare un `AssemblerServiceClient.Endpoint.Address` oggetto utilizzando `System.ServiceModel.EndpointAddress` costruttore. Passa un valore stringa che specifica il file WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). Non è necessario utilizzare il `lc_version` attributo. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.
   * Creare un `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto ottenendo il valore del `AssemblerServiceClient.Endpoint.Binding` campo. Invia il valore restituito a `BasicHttpBinding`.
   * Imposta il `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegna al campo il nome utente dei moduli AEM `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore password corrispondente al campo `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Creare il documento DDX.

   * Creare un `System.Xml.XmlElement` mediante il costruttore.
   * Creare l&#39;elemento radice del documento DDX richiamando `XmlElement` dell&#39;oggetto `CreateElement` metodo. Questo metodo crea un `Element` oggetto che rappresenta l&#39;elemento principale. Passa un valore stringa che rappresenta il nome dell’elemento al `CreateElement` metodo. Imposta un valore per l&#39;elemento DDX chiamando il relativo `SetAttribute` metodo. Infine, aggiungere l&#39;elemento al documento DDX chiamando `XmlElement` dell&#39;oggetto `AppendChild` metodo. Passa l&#39;oggetto DDX come argomento. Le seguenti righe di codice mostrano questa logica dell’applicazione:

     ` System.Xml.XmlElement root = ddx.CreateElement("DDX");  root.SetAttribute("xmlns", "https://ns.adobe.com/DDX/1.0/");  ddx.AppendChild(root);`

   * Crea il documento DDX `PDFsFromBookmarks` chiamando l&#39; `XmlElement` dell&#39;oggetto `CreateElement` metodo. Passa un valore stringa che rappresenta il nome dell’elemento al `CreateElement` metodo. Quindi, imposta un valore per l’elemento chiamando il relativo `SetAttribute` metodo. Aggiungi `PDFsFromBookmarks` all&#39;elemento principale chiamando il `DDX` dell&#39;elemento `AppendChild` metodo. Passa il `PDFsFromBookmarks` come argomento. Le seguenti righe di codice mostrano questa logica dell’applicazione:

     ` XmlElement PDFsFromBookmarks = ddx.CreateElement("PDFsFromBookmarks");  PDFsFromBookmarks.SetAttribute("prefix", "stmt");  root.AppendChild(PDFsFromBookmarks);`

   * Crea il documento DDX `PDF` chiamando l&#39; `XmlElement` dell&#39;oggetto `CreateElement` metodo. Passa un valore stringa che rappresenta il nome dell’elemento al `CreateElement` metodo. Quindi, imposta un valore per l’elemento figlio chiamando il relativo `SetAttribute` metodo. Aggiungi `PDF` elemento al `PDFsFromBookmarks` chiamando l&#39; `PDFsFromBookmarks` dell&#39;elemento `AppendChild` metodo. Passa il `PDF` come argomento. Le seguenti righe di codice mostrano questa logica dell’applicazione:

     ` XmlElement PDF = ddx.CreateElement("PDF");  PDF.SetAttribute("source", "AssemblerResultPDF.pdf");  PDFsFromBookmarks.AppendChild(PDF);`

1. Converte il documento DDX.

   * Creare un `System.IO.MemoryStream` mediante il costruttore.
   * Popolare il `MemoryStream` con il documento DDX utilizzando `XmlElement` oggetto che rappresenta il documento DDX. Richiama `XmlElement` dell&#39;oggetto `Save` e trasmettere il `MemoryStream` oggetto.
   * Creare una matrice di byte e popolarla con i dati presenti nella `MemoryStream` oggetto. Il codice seguente mostra questa logica dell’applicazione:

     ` int bufLen = Convert.ToInt32(stream.Length);  byte[] byteArray = new byte[bufLen];  stream.Position = 0;  int count = stream.Read(byteArray, 0, bufLen);`

   * Creare un `BLOB` oggetto. Assegnare la matrice di byte al `BLOB` dell&#39;oggetto `MTOM` campo.

1. Fare riferimento a un documento PDF da disassemblare.

   * Creare un `BLOB` mediante il costruttore. Il `BLOB` L&#39;oggetto viene utilizzato per memorizzare il documento di input PDF. Questo `BLOB` l&#39;oggetto viene passato al `invokeOneDocument` come argomento.
   * Creare un `System.IO.FileStream` richiamando il relativo costruttore. Passa un valore stringa che rappresenta la posizione del file del documento PDF di input e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto della `System.IO.FileStream` oggetto. È possibile determinare le dimensioni della matrice di byte ottenendo `System.IO.FileStream` dell&#39;oggetto `Length` proprietà.
   * Compilare la matrice di byte con i dati di flusso richiamando `System.IO.FileStream` dell&#39;oggetto `Read` e passando la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare il `BLOB` oggetto assegnando il relativo `MTOM` proprietà il contenuto della matrice di byte.

1. Impostare le opzioni di runtime.

   * Creare un `AssemblerOptionSpec` oggetto che memorizza le opzioni di runtime mediante il relativo costruttore.
   * Impostare le opzioni di runtime per soddisfare i requisiti aziendali assegnando un valore a un membro dati che appartiene al `AssemblerOptionSpec` oggetto. Ad esempio, per indicare al servizio Assembler di continuare l&#39;elaborazione di un processo quando si verifica un errore, assegnare `false` al `AssemblerOptionSpec` dell&#39;oggetto `failOnError` membro dati.

1. Disassemblare il documento PDF.

   Richiama `AssemblerServiceClient` dell&#39;oggetto `invokeDDX` e trasmettere i seguenti valori:

   * A `BLOB` oggetto che rappresenta il documento DDX creato in modo dinamico
   * Il `mapItem` array contenente il documento di input PDF
   * Un `AssemblerOptionSpec` oggetto che specifica le opzioni di runtime

   Il `invokeDDX` il metodo restituisce un `AssemblerResult` oggetto contenente i risultati del processo ed eventuali eccezioni verificatesi.

1. Salvare i documenti PDF disassemblati.

   Per ottenere i documenti di PDF appena creati, effettuare le seguenti operazioni:

   * Accedere a `AssemblerResult` dell&#39;oggetto `documents` campo, che è un `Map` oggetto contenente i documenti PDF disassemblati.
   * Effettua iterazione attraverso `Map` per ottenere ogni documento risultante. Quindi, esegui il cast del membro di array `value` a un `BLOB`.
   * Estrarre i dati binari che rappresentano il documento PDF accedendo al relativo `BLOB` dell&#39;oggetto `MTOM` proprietà. Restituisce una matrice di byte che è possibile scrivere in un file PDF.

**Consulta anche**

[Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamare AEM Forms con SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
