---
title: Creazione dinamica di documenti DDX
description: Creare un documento DDX in modo dinamico utilizzando l'API Java e l'API del servizio Web. La creazione dinamica di un documento DDX consente di utilizzare nel documento DDX i valori ottenuti durante l'esecuzione.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: b3c19c82-e26f-4dc8-b846-6aec705cee08
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '2153'
ht-degree: 0%

---

# Creazione dinamica di documenti DDX {#dynamically-creating-ddx-documents}

**Gli esempi e gli esempi contenuti in questo documento sono solo per AEM Forms in ambiente JEE.**

È possibile creare in modo dinamico un documento DDX che può essere utilizzato per eseguire un&#39;operazione Assembler. La creazione dinamica di un documento DDX consente di utilizzare nel documento DDX i valori ottenuti durante l&#39;esecuzione. Per creare in modo dinamico un documento DDX, utilizzare le classi che appartengono al linguaggio di programmazione in uso. Se ad esempio si sviluppa l&#39;applicazione client utilizzando Java, utilizzare le classi che appartengono al pacchetto `org.w3c.dom.*`. Analogamente, se si utilizza Microsoft .NET, utilizzare le classi che appartengono allo spazio dei nomi `System.Xml`.

Prima di passare il documento DDX al servizio Assembler, convertire l&#39;XML da un&#39;istanza `org.w3c.dom.Document` a un&#39;istanza `com.adobe.idp.Document`. Se si utilizzano i servizi Web, convertire l&#39;XML dal tipo di dati utilizzato per creare l&#39;XML (ad esempio, `XmlDocument`) in un&#39;istanza `BLOB`.

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
>Per ulteriori informazioni sul servizio Assembler, vedere [Riferimento ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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

**Creare un client Assembler PDF**

Prima di eseguire un&#39;operazione Assembler a livello di programmazione, creare un client del servizio Assembler.

**Crea il documento DDX**

Creare un documento DDX utilizzando il linguaggio di programmazione in uso. Per creare un documento DDX che disassembla un documento PDF, verificare che contenga l&#39;elemento `PDFsFromBookmarks`. Se si utilizza l&#39;API Java, convertire il tipo di dati utilizzato per creare il documento DDX in un&#39;istanza `com.adobe.idp.Document`. Se si utilizzano servizi Web, convertire il tipo di dati in un&#39;istanza `BLOB`.

**Convertire il documento DDX**

Un documento DDX creato utilizzando le classi `org.w3c.dom` deve essere convertito in un oggetto `com.adobe.idp.Document`. Per eseguire questa attività quando si utilizza l’API Java, utilizza le classi di trasformazione Java XML. Se si utilizzano i servizi Web, convertire il documento DDX in un oggetto `BLOB`.

**Riferimento a un documento PDF da disassemblare**

Per disassemblare un documento PDF, fare riferimento a un file PDF che rappresenta il documento PDF da disassemblare. Quando viene passato al servizio Assembler, viene restituito un documento PDF separato per ogni segnalibro di livello 1 del documento.

**Impostare le opzioni di runtime**

È possibile impostare le opzioni di runtime che controllano il comportamento del servizio Assembler durante l&#39;esecuzione di un processo. È ad esempio possibile impostare un&#39;opzione che indichi al servizio Assembler di continuare l&#39;elaborazione di un processo in caso di errore. Per impostare le opzioni di runtime, utilizzare un oggetto `AssemblerOptionSpec`.

**Disassemblare il documento PDF**

Disassemblare il documento PDF richiamando l&#39;operazione `invokeDDX`. Passa il documento DDX creato in modo dinamico. Il servizio Assembler restituisce documenti PDF disassemblati all&#39;interno di un oggetto insieme.

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

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `AssemblerServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Creare il documento DDX.

   * Creare un oggetto Java `DocumentBuilderFactory` chiamando il metodo `newInstance` della classe `DocumentBuilderFactory`.
   * Creare un oggetto Java `DocumentBuilder` chiamando il metodo `newDocumentBuilder` dell&#39;oggetto `DocumentBuilderFactory`.
   * Chiamare il metodo `newDocument` dell&#39;oggetto `DocumentBuilder` per creare un&#39;istanza di un oggetto `org.w3c.dom.Document`.
   * Creare l&#39;elemento radice del documento DDX richiamando il metodo `createElement` dell&#39;oggetto `org.w3c.dom.Document`. Questo metodo crea un oggetto `Element` che rappresenta l&#39;elemento radice. Passa un valore stringa che rappresenta il nome dell&#39;elemento al metodo `createElement`. Eseguire il cast del valore restituito in `Element`. Impostare quindi un valore per l&#39;elemento figlio chiamando il relativo metodo `setAttribute`. Infine, accodare l&#39;elemento all&#39;elemento header chiamando il metodo `appendChild` dell&#39;elemento header e passare l&#39;oggetto elemento figlio come argomento. Le seguenti righe di codice mostrano questa logica dell’applicazione:
     ` Element root = (Element)document.createElement("DDX");  root.setAttribute("xmlns","https://ns.adobe.com/DDX/1.0/");  document.appendChild(root);`

   * Creare l&#39;elemento `PDFsFromBookmarks` chiamando il metodo `createElement` dell&#39;oggetto `Document`. Passa un valore stringa che rappresenta il nome dell&#39;elemento al metodo `createElement`. Eseguire il cast del valore restituito in `Element`. Impostare un valore per l&#39;elemento `PDFsFromBookmarks` chiamando il relativo metodo `setAttribute`. Aggiungere l&#39;elemento `PDFsFromBookmarks` all&#39;elemento `DDX` chiamando il metodo `appendChild` dell&#39;elemento DDX. Passa l&#39;oggetto elemento `PDFsFromBookmarks` come argomento. Le seguenti righe di codice mostrano questa logica dell’applicazione:

     ` Element PDFsFromBookmarks = (Element)document.createElement("PDFsFromBookmarks");  PDFsFromBookmarks.setAttribute("prefix","stmt");  root.appendChild(PDFsFromBookmarks);`

   * Creare un elemento `PDF` chiamando il metodo `createElement` dell&#39;oggetto `Document`. Passa un valore stringa che rappresenta il nome dell’elemento. Eseguire il cast del valore restituito in `Element`. Impostare un valore per l&#39;elemento `PDF` chiamando il relativo metodo `setAttribute`. Aggiungere l&#39;elemento `PDF` all&#39;elemento `PDFsFromBookmarks` chiamando il metodo `appendChild` dell&#39;elemento `PDFsFromBookmarks`. Passa l&#39;oggetto elemento `PDF` come argomento. Le seguenti righe di codice mostrano questa logica dell’applicazione:

     ` Element PDF = (Element)document.createElement("PDF");  PDF.setAttribute("source","AssemblerResultPDF.pdf");  PDFsFromBookmarks.appendChild(PDF);`

1. Converte il documento DDX.

   * Creare un oggetto `javax.xml.transform.Transformer` richiamando il metodo `newInstance` statico dell&#39;oggetto `javax.xml.transform.Transformer`.
   * Creare un oggetto `Transformer` richiamando il metodo `newTransformer` dell&#39;oggetto `TransformerFactory`.
   * Creare un oggetto `ByteArrayOutputStream` utilizzando il relativo costruttore.
   * Creare un oggetto `javax.xml.transform.dom.DOMSource` utilizzando il relativo costruttore. Passa l&#39;oggetto `org.w3c.dom.Document` che rappresenta il documento DDX.
   * Creare un oggetto `javax.xml.transform.dom.DOMSource` utilizzando il relativo costruttore e passando l&#39;oggetto `ByteArrayOutputStream`.
   * Compilare l&#39;oggetto Java `ByteArrayOutputStream` richiamando il metodo `transform` dell&#39;oggetto `javax.xml.transform.Transformer`. Passa gli oggetti `javax.xml.transform.dom.DOMSource` e `javax.xml.transform.stream.StreamResult`.
   * Creare una matrice di byte e allocare le dimensioni dell&#39;oggetto `ByteArrayOutputStream` alla matrice di byte.
   * Compilare la matrice di byte richiamando il metodo `toByteArray` dell&#39;oggetto `ByteArrayOutputStream`.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando la matrice di byte.

1. Fare riferimento a un documento PDF da disassemblare.

   * Creare un oggetto `java.util.Map` utilizzato per memorizzare i documenti di input PDF utilizzando un costruttore `HashMap`.
   * Creare un oggetto `java.io.FileInputStream` utilizzando il relativo costruttore e passando la posizione del documento PDF da disassemblare.
   * Creare un oggetto `com.adobe.idp.Document`. Passa l&#39;oggetto `java.io.FileInputStream` che contiene il documento PDF da disassemblare.
   * Aggiungere una voce all&#39;oggetto `java.util.Map` richiamando il relativo metodo `put` e passando i seguenti argomenti:

      * Valore stringa che rappresenta il nome della chiave. Questo valore deve corrispondere al valore dell&#39;elemento di origine PDF specificato nel documento DDX. Nel documento DDX creato in modo dinamico, il valore è `AssemblerResultPDF.pdf`.
      * Oggetto `com.adobe.idp.Document` contenente il documento PDF da disassemblare.

1. Impostare le opzioni di runtime.

   * Creare un oggetto `AssemblerOptionSpec` che memorizza le opzioni di runtime utilizzando il relativo costruttore.
   * Impostare le opzioni di runtime per soddisfare i requisiti aziendali richiamando un metodo che appartiene all&#39;oggetto `AssemblerOptionSpec`. Ad esempio, per indicare al servizio Assembler di continuare a elaborare un processo quando si verifica un errore, richiamare il metodo `setFailOnError` dell&#39;oggetto `AssemblerOptionSpec` e passare `false`.

1. Disassemblare il documento PDF.

   Richiama il metodo `invokeDDX` dell&#39;oggetto `AssemblerServiceClient` e passa i seguenti valori:

   * Oggetto `com.adobe.idp.Document` che rappresenta il documento DDX creato in modo dinamico
   * Oggetto `java.util.Map` contenente il documento PDF da disassemblare
   * Oggetto `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` che specifica le opzioni di runtime, inclusi il tipo di carattere predefinito e il livello del log del processo

   Il metodo `invokeDDX` restituisce un oggetto `com.adobe.livecycle.assembler.client.AssemblerResult` contenente i documenti PDF disassemblati ed eventuali eccezioni.

1. Salvare i documenti PDF disassemblati.

   Per ottenere i documenti PDF disassemblati, effettuare le seguenti operazioni:

   * Richiama il metodo `getDocuments` dell&#39;oggetto `AssemblerResult`. Questo metodo restituisce un oggetto `java.util.Map`.
   * Scorrere l&#39;oggetto `java.util.Map` fino a trovare l&#39;oggetto `com.adobe.idp.Document` risultante.
   * Richiama il metodo `copyToFile` dell&#39;oggetto `com.adobe.idp.Document` per estrarre il documento PDF.

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
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Creare un client PDF Assembler.

   * Creare un oggetto `AssemblerServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `AssemblerServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). Non è necessario utilizzare l&#39;attributo `lc_version`. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `AssemblerServiceClient.Endpoint.Binding`. Eseguire il cast del valore restituito in `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegnare il nome utente dei moduli AEM al campo `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Creare il documento DDX.

   * Creare un oggetto `System.Xml.XmlElement` utilizzando il relativo costruttore.
   * Creare l&#39;elemento radice del documento DDX richiamando il metodo `CreateElement` dell&#39;oggetto `XmlElement`. Questo metodo crea un oggetto `Element` che rappresenta l&#39;elemento radice. Passa un valore stringa che rappresenta il nome dell&#39;elemento al metodo `CreateElement`. Impostare un valore per l&#39;elemento DDX chiamando il relativo metodo `SetAttribute`. Aggiungere infine l&#39;elemento al documento DDX chiamando il metodo `AppendChild` dell&#39;oggetto `XmlElement`. Passa l&#39;oggetto DDX come argomento. Le seguenti righe di codice mostrano questa logica dell’applicazione:

     ` System.Xml.XmlElement root = ddx.CreateElement("DDX");  root.SetAttribute("xmlns", "https://ns.adobe.com/DDX/1.0/");  ddx.AppendChild(root);`

   * Creare l&#39;elemento `PDFsFromBookmarks` del documento DDX chiamando il metodo `CreateElement` dell&#39;oggetto `XmlElement`. Passa un valore stringa che rappresenta il nome dell&#39;elemento al metodo `CreateElement`. Quindi, impostare un valore per l&#39;elemento chiamando il relativo metodo `SetAttribute`. Aggiungere l&#39;elemento `PDFsFromBookmarks` all&#39;elemento radice chiamando il metodo `AppendChild` dell&#39;elemento `DDX`. Passa l&#39;oggetto elemento `PDFsFromBookmarks` come argomento. Le seguenti righe di codice mostrano questa logica dell’applicazione:

     ` XmlElement PDFsFromBookmarks = ddx.CreateElement("PDFsFromBookmarks");  PDFsFromBookmarks.SetAttribute("prefix", "stmt");  root.AppendChild(PDFsFromBookmarks);`

   * Creare l&#39;elemento `PDF` del documento DDX chiamando il metodo `CreateElement` dell&#39;oggetto `XmlElement`. Passa un valore stringa che rappresenta il nome dell&#39;elemento al metodo `CreateElement`. Impostare quindi un valore per l&#39;elemento figlio chiamando il relativo metodo `SetAttribute`. Aggiungere l&#39;elemento `PDF` all&#39;elemento `PDFsFromBookmarks` chiamando il metodo `AppendChild` dell&#39;elemento `PDFsFromBookmarks`. Passa l&#39;oggetto elemento `PDF` come argomento. Le seguenti righe di codice mostrano questa logica dell’applicazione:

     ` XmlElement PDF = ddx.CreateElement("PDF");  PDF.SetAttribute("source", "AssemblerResultPDF.pdf");  PDFsFromBookmarks.AppendChild(PDF);`

1. Converte il documento DDX.

   * Creare un oggetto `System.IO.MemoryStream` utilizzando il relativo costruttore.
   * Compilare l&#39;oggetto `MemoryStream` con il documento DDX utilizzando l&#39;oggetto `XmlElement` che rappresenta il documento DDX. Richiama il metodo `Save` dell&#39;oggetto `XmlElement` e passa l&#39;oggetto `MemoryStream`.
   * Creare una matrice di byte e popolarla con i dati nell&#39;oggetto `MemoryStream`. Il codice seguente mostra questa logica dell’applicazione:

     ` int bufLen = Convert.ToInt32(stream.Length);  byte[] byteArray = new byte[bufLen];  stream.Position = 0;  int count = stream.Read(byteArray, 0, bufLen);`

   * Creare un oggetto `BLOB`. Assegnare la matrice di byte al campo `MTOM` dell&#39;oggetto `BLOB`.

1. Fare riferimento a un documento PDF da disassemblare.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare il documento PDF di input. Questo oggetto `BLOB` è passato a `invokeOneDocument` come argomento.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore. Passa un valore stringa che rappresenta la posizione del file del documento PDF di input e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni della matrice di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare la matrice di byte con i dati di flusso richiamando il metodo `Read` dell&#39;oggetto `System.IO.FileStream` e passando la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando alla relativa proprietà `MTOM` il contenuto della matrice di byte.

1. Impostare le opzioni di runtime.

   * Creare un oggetto `AssemblerOptionSpec` che memorizza le opzioni di runtime utilizzando il relativo costruttore.
   * Impostare le opzioni di runtime per soddisfare i requisiti aziendali assegnando un valore a un membro dati che appartiene all&#39;oggetto `AssemblerOptionSpec`. Ad esempio, per indicare al servizio Assembler di continuare a elaborare un processo quando si verifica un errore, assegnare `false` al membro dati `failOnError` dell&#39;oggetto `AssemblerOptionSpec`.

1. Disassemblare il documento PDF.

   Richiama il metodo `invokeDDX` dell&#39;oggetto `AssemblerServiceClient` e passa i seguenti valori:

   * Oggetto `BLOB` che rappresenta il documento DDX creato in modo dinamico
   * Array `mapItem` contenente il documento PDF di input
   * Oggetto `AssemblerOptionSpec` che specifica le opzioni di runtime

   Il metodo `invokeDDX` restituisce un oggetto `AssemblerResult` contenente i risultati del processo ed eventuali eccezioni.

1. Salvare i documenti PDF disassemblati.

   Per ottenere i documenti di PDF appena creati, effettuare le seguenti operazioni:

   * Accedere al campo `documents` dell&#39;oggetto `AssemblerResult`, che è un oggetto `Map` contenente i documenti PDF disassemblati.
   * Scorrere l&#39;oggetto `Map` per ottenere ogni documento risultante. Quindi, eseguire il cast di `value` del membro dell&#39;array in un `BLOB`.
   * Estrarre i dati binari che rappresentano il documento PDF accedendo alla proprietà `MTOM` dell&#39;oggetto `BLOB`. Restituisce una matrice di byte che è possibile scrivere in un file PDF.

**Consulta anche**

[Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamare AEM Forms con SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
