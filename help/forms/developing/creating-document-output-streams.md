---
title: Creazione di flussi di output dei documenti
seo-title: Creating Document Output Streams
description: Utilizza il servizio Output per convertire i documenti come PDF (inclusi i documenti PDF/A), PostScript, Printer Control Language (PCL) e nei formati etichetta Zebra - ZPL, Intermec - IPL, Datamax - DPL e TecToshiba - TPCL.
seo-description: Use the Output service to convert documents as PDF (including PDF/A documents), PostScript, Printer Control Language (PCL), and Zebra - ZPL, Intermec - IPL, Datamax - DPL, and TecToshiba - TPCL label formats.
uuid: 80c28efa-35ce-4073-9ca6-2d93bcd67fdd
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: de527d50-991b-4ca3-a8ac-44d5cab988e9
role: Developer
exl-id: a521bfac-f417-4002-9c5c-8d7794d3eec7
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '19016'
ht-degree: 0%

---

# Creazione di flussi di output dei documenti  {#creating-document-output-streams}

**Esempi ed esempi in questo documento sono solo per AEM Forms in ambiente JEE.**

**Informazioni sul servizio di output**

Il servizio Output consente di inviare i documenti come PDF (inclusi i documenti PDF/A), PostScript, PCL (Printer Control Language) e i seguenti formati di etichetta:

* Zebra - ZPL
* Intermec - IPL
* Datamax - DPL
* TecToshiba - TPCL

Tramite il servizio Output è possibile unire i dati del modulo XML a una struttura del modulo e inviare il documento a una stampante o a un file di rete.

Esistono due modi per passare una struttura del modulo (un file XDP) al servizio Output. Puoi passare un `com.adobe.idp.Document` istanza che contiene una struttura del modulo per il servizio Output. In alternativa, è possibile passare un valore URI che specifica la posizione della struttura del modulo. Entrambi questi modi sono discussi in *Programmazione con moduli AEM*.

>[!NOTE]
>
>Il servizio Output non supporta i documenti PDF Acroform contenenti script specifici per oggetti applicativi. Non viene eseguito il rendering dei documenti Acroform PDF contenenti script specifici per oggetti dell&#39;applicazione.

Nelle sezioni seguenti viene illustrato come passare una struttura del modulo al servizio Output utilizzando un valore URI:

* [Creazione di documenti PDF](creating-document-output-streams.md#creating-pdf-documents)
* [Creazione di documenti PDF/A](creating-document-output-streams.md#creating-pdf-a-documents)

Nelle sezioni seguenti viene illustrato come passare una struttura del modulo all’interno di un `com.adobe.idp.Document` istanza:

* [Trasmissione di documenti situati in Content Services (obsoleto) al servizio di output](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)
* [Creazione di documenti PDF tramite frammenti](creating-document-output-streams.md#creating-pdf-documents-using-fragments)

Quando si decide quale tecnica utilizzare, occorre tenere presente che la struttura del modulo deve essere ricevuta da un altro servizio AEM Forms e quindi trasmessa all’interno di un `com.adobe.idp.Document` istanza. Entrambi i *Trasmissione di documenti al servizio di output* e *Creazione di documenti PDF tramite frammenti* Le sezioni mostrano come ottenere una struttura del modulo da un altro servizio AEM Forms. La prima sezione recupera la struttura del modulo da Content Services (obsoleto). La seconda sezione recupera la struttura del modulo dal servizio Assembler.

Se si ottiene la struttura del modulo da una posizione fissa, ad esempio il file system, è possibile utilizzare una di queste tecniche. In altre parole, è possibile specificare il valore URI in un file XDP o utilizzare un `com.adobe.idp.Document` istanza.

Per passare un valore URI che specifichi la posizione della struttura del modulo durante la creazione di un documento PDF, utilizzare la `generatePDFOutput` metodo . Allo stesso modo, per passare un `com.adobe.idp.Document` istanza al servizio Output durante la creazione di un documento PDF, utilizzare il `generatePDFOutput2` metodo .

Quando si invia un flusso di output a una stampante di rete, è inoltre possibile utilizzare una di queste tecniche. Per inviare un flusso di output a una stampante passando una `com.adobe.idp.Document` istanza che contiene una struttura del modulo, utilizzare `sendToPrinter2`metodo . Per inviare un flusso di output a una stampante passando un valore URI, utilizzare il comando `sendToPrinter`metodo . La *Invio di flussi di stampa alle stampanti* utilizza la sezione `sendToPrinter` metodo .

Puoi eseguire queste attività utilizzando il servizio Output:

* [Creazione di documenti PDF](creating-document-output-streams.md#creating-pdf-documents)
* [Creazione di documenti PDF/A](creating-document-output-streams.md#creating-pdf-a-documents)
* [Trasmissione di documenti situati in Content Services (obsoleto) al servizio di output](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)
* [Creazione di documenti PDF tramite frammenti](creating-document-output-streams.md#creating-pdf-documents-using-fragments)
* [Stampa su file](creating-document-output-streams.md#printing-to-files)
* [Invio di flussi di stampa alle stampanti](creating-document-output-streams.md#sending-print-streams-to-printers)
* [Creazione di più file di output](creating-document-output-streams.md#creating-multiple-output-files)
* [Creazione di regole di ricerca](creating-document-output-streams.md#creating-search-rules)
* [Flatting dei documenti PDF](creating-document-output-streams.md#flattening-pdf-documents)

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Output, vedi [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Creazione di documenti PDF {#creating-pdf-documents}

È possibile utilizzare il servizio Output per creare un documento PDF basato su una struttura del modulo e sui dati del modulo XML forniti. Il documento PDF creato dal servizio Output non è un documento PDF interattivo; un utente non può immettere o modificare i dati del modulo.

Per creare un documento PDF destinato all’archiviazione a lungo termine, è consigliabile creare un documento PDF/A. (Vedi [Creazione di documenti PDF/A](creating-document-output-streams.md#creating-pdf-a-documents).)

Per creare un modulo PDF interattivo che consenta all’utente di immettere i dati, utilizzare il servizio Forms. (Vedi [Rendering di PDF forms interattivi](/help/forms/developing/rendering-forms.md#rendering-interactive-pdf-forms).)

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Output, vedi [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary-of-steps}

Per creare un documento PDF, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Creare un oggetto Client di output.
1. Fare riferimento a un&#39;origine dati XML.
1. Impostare le opzioni di runtime di PDF.
1. Imposta le opzioni di esecuzione del rendering.
1. Genera un documento PDF.
1. Recupera i risultati dell’operazione.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar (obbligatorio se AEM Forms è distribuito su JBoss)
* jbossall-client.jar (obbligatorio se AEM Forms è distribuito su JBoss)

se AEM Forms è distribuito su un server applicazioni J2EE supportato che non è JBoss, sarà necessario sostituire i file adobe-utilities.jar e jbossall-client.jar con file JAR specifici per il server applicazioni J2EE in cui viene distribuito AEM Forms.

**Creare un oggetto Client di output**

Prima di poter eseguire un&#39;operazione del servizio Output a livello di programmazione, è necessario creare un oggetto client del servizio Output. Se utilizzi l’API Java, crea un `OutputClient` oggetto. Se utilizzi l’API del servizio Web Output, crea un `OutputServiceService` oggetto.

**Riferimento a un’origine dati XML**

Per unire i dati alla struttura del modulo, è necessario fare riferimento a un’origine dati XML contenente i dati. Per ogni campo del modulo che si intende compilare con i dati deve esistere un elemento XML. Il nome dell&#39;elemento XML deve corrispondere al nome del campo. Un elemento XML viene ignorato se non corrisponde a un campo modulo o se il nome dell’elemento XML non corrisponde al nome del campo. Se vengono specificati tutti gli elementi XML, non è necessario stabilire una corrispondenza con l’ordine in cui vengono visualizzati gli elementi XML.

Prendi in considerazione il seguente modulo di richiesta di prestito.

![cp_cp_loanformdata](assets/cp_cp_loanformdata.png)

Per unire i dati alla struttura del modulo, è necessario creare un’origine dati XML corrispondente al modulo. Il seguente XML rappresenta un&#39;origine dati XML XDP che corrisponde al modulo di applicazione per ipoteca di esempio.

```xml
 <?xml version="1.0" encoding="UTF-8" ?>
 - <xfa:datasets xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/">
 - <xfa:data>
 - <data>
     - <Layer>
         <closeDate>1/26/2007</closeDate>
         <lastName>Johnson</lastName>
         <firstName>Jerry</firstName>
         <mailingAddress>JJohnson@NoMailServer.com</mailingAddress>
         <city>New York</city>
         <zipCode>00501</zipCode>
         <state>NY</state>
         <dateBirth>26/08/1973</dateBirth>
         <middleInitials>D</middleInitials>
         <socialSecurityNumber>(555) 555-5555</socialSecurityNumber>
         <phoneNumber>5555550000</phoneNumber>
     </Layer>
     - <Mortgage>
         <mortgageAmount>295000.00</mortgageAmount>
         <monthlyMortgagePayment>1724.54</monthlyMortgagePayment>
         <purchasePrice>300000</purchasePrice>
         <downPayment>5000</downPayment>
         <term>25</term>
         <interestRate>5.00</interestRate>
     </Mortgage>
 </data>
 </xfa:data>
 </xfa:datasets>
```

**Impostare le opzioni di runtime di PDF**

Impostare l’opzione URI del file durante la creazione di un documento PDF. Questa opzione specifica il nome e la posizione del file PDF generato dal servizio Output.

>[!NOTE]
>
>Invece di impostare l’opzione di esecuzione URI del file, è possibile recuperare in modo programmatico il documento PDF dal tipo di dati complesso restituito dal servizio Output. Tuttavia, impostando l’opzione di esecuzione URI del file, non è necessario creare una logica applicativa che recuperi il documento PDF in modo programmatico.

**Impostare le opzioni di esecuzione del rendering**

È possibile impostare le opzioni di esecuzione del rendering durante la creazione di un documento PDF. Sebbene queste opzioni non siano necessarie (a differenza delle opzioni di runtime di PDF richieste), è possibile eseguire attività quali il miglioramento delle prestazioni del servizio Output. Ad esempio, è possibile memorizzare nella cache la struttura del modulo utilizzata dal servizio Output per migliorarne le prestazioni.

Se si utilizza un modulo Acrobat con tag come input, non è possibile utilizzare Java del servizio di output o API del servizio Web per disattivare l’impostazione con tag. Se tenti di impostare questa opzione a livello di programmazione su `false`, il risultato del documento PDF è ancora contrassegnato.

>[!NOTE]
>
>Se non si specificano le opzioni di esecuzione del rendering, vengono utilizzati i valori predefiniti. Per informazioni sulle opzioni di rendering in fase di esecuzione, consulta la sezione `RenderOptionsSpec` riferimento della classe. (Vedi [Riferimento API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)).

**Generare un documento PDF**

Dopo aver fatto riferimento a un’origine dati XML valida contenente i dati del modulo e aver impostato le opzioni di esecuzione, è possibile richiamare il servizio Output, generando un documento PDF.

Quando si genera un documento PDF, è necessario specificare i valori URI richiesti dal servizio Output per creare un documento PDF. Una struttura del modulo può essere memorizzata in posizioni quali il file system del server o come parte di un’applicazione AEM Forms. È possibile fare riferimento a una struttura del modulo (o ad altre risorse, ad esempio un file immagine) esistente nell’ambito di un’applicazione Forms utilizzando il valore URI della directory principale contenuto `repository:///`. Ad esempio, considerare la seguente struttura del modulo denominata *Loan.xdp* all&#39;interno di un&#39;applicazione Forms denominata *Applicazioni/FormsApplication*:

![cp_cp_formrepository](assets/cp_cp_formrepository.png)

Per accedere al file Loan.xdp mostrato nell&#39;illustrazione precedente, specifica `repository:///Applications/FormsApplication/1.0/FormsFolder/` come terzo parametro trasmesso al `OutputClient` dell’oggetto `generatePDFOutput` metodo . Specifica il nome del modulo (*Loan.xdp*) come secondo parametro trasmesso al `OutputClient` dell’oggetto `generatePDFOutput` metodo .

Se il file XDP contiene immagini (o altre risorse come frammenti), posiziona le risorse nella stessa cartella dell’applicazione del file XDP. AEM Forms utilizza l’URI della directory principale del contenuto come percorso di base per risolvere i riferimenti alle immagini. Ad esempio, se il file Loan.xdp contiene un&#39;immagine, accertati di inserire l&#39;immagine in `Applications/FormsApplication/1.0/FormsFolder/`.

>[!NOTE]
>
>È possibile fare riferimento a un URI di applicazione Forms quando si richiama il `OutputClient` dell’oggetto `generatePDFOutput` o `generatePrintedOutput` metodi.

>[!NOTE]
>
>Per visualizzare un avvio rapido completo che crea un documento PDF facendo riferimento a un file XDP presente in un&#39;applicazione Forms, vedi [Avvio rapido (modalità EJB): Creazione di un documento PDF basato su un file XDP dell’applicazione utilizzando l’API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-an-application-xdp-file-using-the-java-api).

**Recupera i risultati dell&#39;operazione**

Dopo l&#39;esecuzione di un&#39;operazione, il servizio Output restituisce vari elementi di dati, ad esempio dati XML di stato, che specificano se l&#39;operazione ha avuto esito positivo.

**Consulta anche**

[Creare un documento PDF utilizzando l’API Java](creating-document-output-streams.md#create-a-pdf-document-using-the-java-api)

[Creare un documento PDF utilizzando l’API del servizio Web](creating-document-output-streams.md#create-a-pdf-document-using-the-web-service-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API del servizio di output](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Creare un documento PDF utilizzando l’API Java {#create-a-pdf-document-using-the-java-api}

Creare un documento PDF utilizzando l’API di output (Java):

1. Includi file di progetto.

   Includi file JAR client, come adobe-output-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto Client di output.

   * Crea un `ServiceClientFactory` oggetto contenente le proprietà di connessione.
   * Crea un `OutputClient` utilizzando il relativo costruttore e passando `ServiceClientFactory` oggetto.

1. Fare riferimento a un&#39;origine dati XML.

   * Crea un `java.io.FileInputStream` oggetto che rappresenta l&#39;origine dati XML utilizzata per compilare il documento PDF utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del file XML.
   * Crea un `com.adobe.idp.Document` utilizzando il relativo costruttore. Passa la `java.io.FileInputStream` oggetto.

1. Impostare le opzioni di runtime di PDF.

   * Crea un `PDFOutputOptionsSpec` utilizzando il relativo costruttore.
   * Imposta l&#39;opzione URI file richiamando il `PDFOutputOptionsSpec` dell’oggetto `setFileURI` metodo . Passa un valore stringa che specifica la posizione del file PDF generato dal servizio Output. L’opzione URI file è relativa al server applicazioni J2EE che ospita AEM Forms, non al computer client.

1. Imposta le opzioni di esecuzione del rendering.

   * Crea un `RenderOptionsSpec` utilizzando il relativo costruttore.
   * Memorizza in cache la struttura del modulo per migliorare le prestazioni del servizio Output richiamando il `RenderOptionsSpec` dell’oggetto `setCacheEnabled` e di passaggio `true`.

   >[!NOTE]
   >
   >Non è possibile impostare la versione del documento di PDF utilizzando il `RenderOptionsSpec` dell’oggetto `setPdfVersion` se il documento di input è un modulo Acrobat (un modulo creato in Acrobat) o un documento XFA firmato o certificato. Il documento PDF di output conserva la versione originale di PDF. Allo stesso modo, non è possibile impostare l’opzione Adobe PDF con tag richiamando il `RenderOptionsSpec` dell’oggetto `setTaggedPDF` se il documento di input è un modulo Acrobat o un documento XFA firmato o certificato.

   >[!NOTE]
   >
   >Non è possibile impostare l’opzione linearized PDF utilizzando `RenderOptionsSpec` dell’oggetto `setLinearizedPDF` se il documento di input PDF è certificato o firmato digitalmente. (Vedi [Firma digitale di documenti PDF ](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)*.)*

1. Genera un documento PDF.

   Creare un documento PDF richiamando il `OutputClient` dell’oggetto `generatePDFOutput` e passando i seguenti valori:

   * A `TransformationFormat` valore di enumerazione. Per generare un documento PDF, specificare `TransformationFormat.PDF`.
   * Valore stringa che specifica il nome della struttura del modulo.
   * Valore stringa che specifica la directory principale del contenuto in cui si trova la struttura del modulo.
   * A `PDFOutputOptionsSpec` oggetto contenente le opzioni di runtime di PDF.
   * A `RenderOptionsSpec` oggetto contenente le opzioni di esecuzione del rendering.
   * La `com.adobe.idp.Document` oggetto contenente l’origine dati XML contenente i dati da unire alla struttura del modulo.

   La `generatePDFOutput` restituisce un `OutputResult` oggetto contenente i risultati dell&#39;operazione.

   >[!NOTE]
   >
   >Quando si genera un documento PDF richiamando il `generatePDFOutput` tenere presente che non è possibile unire dati con un modulo XFA PDF firmato o certificato. (Vedi [Firma digitale e certificazione dei documenti ](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-and-certifying-documents)*.)*

   >[!NOTE]
   >
   >La `OutputResult` dell’oggetto `getRecordLevelMetaDataList` restituisce il metodo `null`*.*

   >[!NOTE]
   >
   >È inoltre possibile creare un documento PDF richiamando il `OutputClient` dell’oggetto `generatePDFOutput2` metodo . (Vedi [Trasmissione di documenti situati in Content Services (obsoleto) al servizio di output ](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)*.)*

1. Recupera i risultati dell’operazione.

   * Recupera un `com.adobe.idp.Document` che rappresenta lo stato `generatePDFOutput` richiamando il `OutputResult` dell’oggetto `getStatusDoc` metodo . Questo metodo restituisce dati XML di stato che specificano se l&#39;operazione è riuscita.
   * Crea un `java.io.File` oggetto contenente i risultati dell&#39;operazione. Assicurati che l&#39;estensione del nome file sia .xml.
   * Richiama il `com.adobe.idp.Document` dell’oggetto `copyToFile` per copiare il contenuto del `com.adobe.idp.Document` al file (assicurati di utilizzare `com.adobe.idp.Document` oggetto restituito da `getStatusDoc` metodo).

   Anche se il servizio Output scrive il documento PDF nel percorso specificato dall&#39;argomento passato al `PDFOutputOptionsSpec` dell’oggetto `setFileURI` è possibile recuperare in modo programmatico il documento PDF/A richiamando il `OutputResult` dell’oggetto `getGeneratedDoc` metodo .

**Consulta anche**

[Riepilogo dei passaggi](creating-document-output-streams.md#summary-of-steps)

[Avvio rapido (modalità EJB): Creazione di un documento PDF tramite l’API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-using-the-java-api)

[Avvio rapido (modalità SOAP): Creazione di un documento PDF tramite l’API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Creare un documento PDF utilizzando l’API del servizio Web {#create-a-pdf-document-using-the-web-service-api}

Creare un documento PDF utilizzando l’API di output (servizio Web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurati di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l’indirizzo IP del server che ospita AEM Forms.

1. Creare un oggetto Client di output.

   * Crea un `OutputServiceClient` utilizzando il relativo costruttore predefinito.
   * Crea un `OutputServiceClient.Endpoint.Address` utilizzando `System.ServiceModel.EndpointAddress` costruttore. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/OutputService?blob=mtom`.) Non è necessario utilizzare il `lc_version` attributo. Questo attributo viene utilizzato quando si crea un riferimento a un servizio. Tuttavia, specifica `?blob=mtom` per utilizzare MTOM.
   * Crea un `System.ServiceModel.BasicHttpBinding` ottenendo il valore del `OutputServiceClient.Endpoint.Binding` campo . Imposta il valore restituito su `BasicHttpBinding`.
   * Imposta la `System.ServiceModel.BasicHttpBinding` dell’oggetto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegnare il nome utente del modulo di AEM al campo `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore della password corrispondente al campo `OutputServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Fare riferimento a un&#39;origine dati XML.

   * Crea un `BLOB` utilizzando il relativo costruttore. La `BLOB` viene utilizzato per memorizzare i dati XML che verranno uniti al documento PDF.
   * Crea un `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file XML contenente i dati del modulo.
   * Creare un array di byte che memorizza il contenuto del `System.IO.FileStream` oggetto. È possibile determinare le dimensioni dell&#39;array di byte ottenendo il `System.IO.FileStream` dell’oggetto `Length` proprietà.
   * Compilare l&#39;array di byte con i dati del flusso richiamando il `System.IO.FileStream` dell’oggetto `Read` e passare l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare `BLOB` oggetto assegnando il relativo `MTOM` con il contenuto dell&#39;array di byte.

1. Impostare le opzioni di runtime di PDF

   * Crea un `PDFOutputOptionsSpec` utilizzando il relativo costruttore.
   * Impostare l&#39;opzione URI file assegnando un valore stringa che specifica la posizione del file PDF generato dal servizio Output nel `PDFOutputOptionsSpec` dell’oggetto `fileURI` membro dati. L’opzione URI file è relativa al server applicazioni J2EE che ospita AEM Forms, non al computer client.

1. Imposta le opzioni di esecuzione del rendering.

   * Crea un `RenderOptionsSpec` utilizzando il relativo costruttore.
   * Memorizza in cache la struttura del modulo per migliorare le prestazioni del servizio Output assegnando il valore `true` al `RenderOptionsSpec` dell’oggetto `cacheEnabled` membro dati.

   >[!NOTE]
   >
   >Non è possibile impostare la versione del documento di PDF utilizzando il `RenderOptionsSpec` dell’oggetto `setPdfVersion` se il documento di input è un modulo Acrobat (un modulo creato in Acrobat) o un documento XFA firmato o certificato. Il documento PDF di output conserva la versione originale di PDF. Allo stesso modo, non è possibile impostare l’opzione Adobe PDF con tag richiamando il `RenderOptionsSpec` dell’oggetto `setTaggedPDF`* se il documento di input è un modulo Acrobat o un documento XFA firmato o certificato.*

   >[!NOTE]
   >
   >Non è possibile impostare l’opzione linearized PDF utilizzando `RenderOptionsSpec` dell’oggetto `linearizedPDF` se il documento di input PDF è certificato o firmato digitalmente. (Vedi [Firma digitale di documenti PDF ](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)*.)*

1. Genera un documento PDF.

   Creare un documento PDF richiamando il `OutputServiceService` dell’oggetto `generatePDFOutput`e passando i seguenti valori:

   * A `TransformationFormat` valore di enumerazione. Per generare un documento PDF, specificare `TransformationFormat.PDF`.
   * Valore stringa che specifica il nome della struttura del modulo.
   * Valore stringa che specifica la directory principale del contenuto in cui si trova la struttura del modulo.
   * A `PDFOutputOptionsSpec` oggetto contenente le opzioni di runtime di PDF.
   * A `RenderOptionsSpec` oggetto contenente le opzioni di esecuzione del rendering.
   * La `BLOB` oggetto contenente l’origine dati XML contenente i dati da unire alla struttura del modulo.
   * A `BLOB` oggetto popolato da `generatePDFOutput` metodo . La `generatePDFOutput` popola l&#39;oggetto con i metadati generati che descrivono il documento. (Questo valore di parametro è richiesto solo per la chiamata al servizio Web).
   * A `BLOB` oggetto popolato da `generatePDFOutput` metodo . La `generatePDFOutput` popola l&#39;oggetto con i dati dei risultati. (Questo valore di parametro è richiesto solo per la chiamata al servizio Web).
   * Un `OutputResult` oggetto contenente i risultati dell&#39;operazione. (Questo valore di parametro è richiesto solo per la chiamata al servizio Web).

   >[!NOTE]
   >
   >Quando si genera un documento PDF richiamando il `generatePDFOutput` tenere presente che non è possibile unire dati con un modulo XFA PDF firmato o certificato. (Vedi [Firma digitale e certificazione dei documenti ](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-and-certifying-documents)*.)*

   >[!NOTE]
   >
   >È inoltre possibile creare un documento PDF richiamando il `OutputClient` dell’oggetto `generatePDFOutput2` metodo . (Vedi [Trasmissione di documenti situati in Content Services (obsoleto) al servizio di output ](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)*.)*

1. Recupera i risultati dell’operazione.

   * Crea un `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta una posizione di file XML contenente i dati dei risultati. Assicurati che l&#39;estensione del nome file sia .xml.
   * Creare un array di byte che memorizza il contenuto dei dati del `BLOB` oggetto popolato con i dati dei risultati da `OutputServiceService` dell’oggetto `generatePDFOutput` (l&#39;ottavo parametro). Compilare l’array di byte ottenendo il valore del `BLOB` dell’oggetto `MTOM` `field`.
   * Crea un `System.IO.BinaryWriter` richiamando il relativo costruttore e passando `System.IO.FileStream` oggetto.
   * Scrivere il contenuto dell&#39;array di byte nel file XML richiamando il `System.IO.BinaryWriter` dell’oggetto `Write` e passare l&#39;array di byte.

   Consulta anche

[Riepilogo dei passaggi](creating-document-output-streams.md#summary-of-steps)

[Richiamo di AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamo di AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

   >[!NOTE]
   >
   >La `OutputServiceService` dell’oggetto `generateOutput` è obsoleto.

## Creazione di documenti PDF/A {#creating-pdf-a-documents}

È possibile utilizzare il servizio Output per creare un documento PDF/A. Poiché PDF/A è un formato di archiviazione per la conservazione a lungo termine del contenuto del documento, tutti i font vengono incorporati e il file non viene compresso. Di conseguenza, un documento PDF/A è generalmente più grande di un documento PDF standard. Inoltre, un documento PDF/A non contiene contenuti audio e video. Come per altre attività del servizio Output, è possibile fornire una struttura del modulo e i dati da unire a una struttura del modulo per creare un documento PDF/A.

La specifica PDF/A-1 è costituita da due livelli di conformità, ossia a e b. La differenza principale tra i due riguarda il supporto della struttura logica (accessibilità), che non è necessario per il livello di conformità b. Indipendentemente dal livello di conformità, PDF/A-1 determina che tutti i font sono incorporati nel documento PDF/A generato.

Anche se PDF/A è lo standard per l’archiviazione dei documenti PDF, non è obbligatorio utilizzare PDF/A per l’archiviazione se un documento PDF standard soddisfa le esigenze aziendali. Lo scopo dello standard PDF/A è quello di stabilire un file PDF che possa essere archiviato per un lungo periodo di tempo e che soddisfi i requisiti di conservazione dei documenti. Ad esempio, non è possibile incorporare un URL in un PDF/A perché nel tempo l’URL potrebbe non essere valido.

L&#39;organizzazione deve valutare le proprie esigenze, il periodo di tempo previsto per la conservazione del documento, le dimensioni del file e determinare la propria strategia di archiviazione. È possibile determinare a livello di programmazione se un documento PDF è conforme a PDF/A utilizzando il servizio DocConverter. (Vedi [Determinazione programmatica della conformità PDF/A](/help/forms/developing/pdf-a-documents.md#programmatically-determining-pdf-a-compliancy).)

Un documento PDF/A deve utilizzare il font specificato nella struttura del modulo e i font non possono essere sostituiti. Di conseguenza, se un font che si trova all’interno di un documento PDF non è disponibile nel sistema operativo host (OS), si verifica un’eccezione.

Quando un documento PDF/A viene aperto in Acrobat, viene visualizzato un messaggio che conferma che il documento è un documento PDF/A, come illustrato nella figura seguente.

![cp_cp_pdfamessage](assets/cp_cp_pdfamessage.png)

>[!NOTE]
>
>Il sito web AIIM dispone di una sezione FAQ PDF/A a cui puoi accedere all’indirizzo [https://www.loc.gov/preservation/digital/formats/fdd/fdd000125.shtml](https://www.loc.gov/preservation/digital/formats/fdd/fdd000125.shtml).

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Output, vedi [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_65).

### Riepilogo dei passaggi {#summary_of_steps-1}

Per creare un documento PDF/A, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Creare un oggetto Client di output.
1. Fare riferimento a un&#39;origine dati XML.
1. Impostare le opzioni di esecuzione di PDF/A.
1. Imposta le opzioni di esecuzione del rendering.
1. Genera un documento PDF/A.
1. Recupera i risultati dell’operazione.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione personalizzata utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso della classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar (obbligatorio se AEM Forms è distribuito su JBoss)
* jbossall-client.jar (obbligatorio se AEM Forms è distribuito su JBoss)

se AEM Forms è distribuito su un server applicazioni J2EE supportato che non è JBoss, sarà necessario sostituire i file adobe-utilities.jar e jbossall-client.jar con file JAR specifici per il server applicazioni J2EE in cui viene distribuito AEM Forms.

**Creare un oggetto Client di output**

Prima di poter eseguire un&#39;operazione del servizio Output a livello di programmazione, è necessario creare un oggetto client del servizio Output. Se utilizzi l’API Java, crea un `OutputClient` oggetto. Se utilizzi l’API del servizio Web Output, crea un `OutputServiceService` oggetto.

**Riferimento a un’origine dati XML**

Per unire i dati alla struttura del modulo, è necessario fare riferimento a un’origine dati XML contenente i dati. Per ogni campo del modulo che si desidera compilare con i dati deve esistere un elemento XML. Il nome dell&#39;elemento XML deve corrispondere al nome del campo. Un elemento XML viene ignorato se non corrisponde a un campo modulo o se il nome dell’elemento XML non corrisponde al nome del campo. Se vengono specificati tutti gli elementi XML, non è necessario stabilire una corrispondenza con l’ordine in cui vengono visualizzati gli elementi XML.

**Impostare le opzioni di esecuzione di PDF/A**

È possibile impostare l’opzione URI file durante la creazione di un documento PDF/A. L’URI è relativo al server applicazioni J2EE che ospita AEM Forms. In altre parole, se si imposta C:\Adobe, il file viene scritto nella cartella sul server, non nel computer client. L’URI specifica il nome e la posizione del file PDF/A generato dal servizio Output.

**Impostare le opzioni di esecuzione del rendering**

È possibile impostare le opzioni di esecuzione del rendering durante la creazione di documenti PDF/A. Le due opzioni relative a PDF/A che è possibile impostare sono le seguenti: `PDFAConformance` e `PDFARevisionNumber` valori. La `PDFAConformance` Il valore si riferisce al modo in cui un documento PDF aderisce ai requisiti che specificano il modo in cui vengono conservati i documenti elettronici a lungo termine. I valori validi per questa opzione sono `A` e `B`. Per informazioni sulla conformità ai livelli a e b, vedere la specifica ISO PDF/A-1 denominata *ISO 19005-1 Gestione dei documenti*.

La `PDFARevisionNumber` Il valore si riferisce al numero di revisione di un documento PDF/A. Per informazioni sul numero di revisione di un documento PDF/A, vedere la specifica ISO PDF/A-1 denominata *ISO 19005-1 Gestione dei documenti*.

>[!NOTE]
>
>Non è possibile impostare l’opzione Adobe PDF con tag su `false` durante la creazione di un documento PDF/A 1A. PDF/A 1A sarà sempre un documento PDF con tag. Inoltre, non è possibile impostare l’opzione Adobe PDF con tag su `true` durante la creazione di un documento PDF/A 1B. PDF/A 1B sarà sempre un documento PDF senza tag.

**Generare un documento PDF/A**

Dopo aver fatto riferimento a un’origine dati XML valida contenente i dati del modulo e aver impostato le opzioni di esecuzione, è possibile richiamare il servizio Output generando un documento PDF/A.

**Recupera i risultati dell&#39;operazione**

Dopo l&#39;esecuzione di un&#39;operazione, il servizio Output restituisce vari elementi di dati, ad esempio dati XML, che specificano se l&#39;operazione ha avuto esito positivo.

**Consulta anche**

[Creare un documento PDF/A utilizzando l’API Java](creating-document-output-streams.md#create-a-pdf-a-document-using-the-java-api)

[Creare un documento PDF/A utilizzando l’API del servizio Web](creating-document-output-streams.md#create-a-pdf-a-document-using-the-web-service-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API del servizio di output](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Creare un documento PDF/A utilizzando l’API Java {#create-a-pdf-a-document-using-the-java-api}

Crea un documento PDF/A utilizzando l’API di output (Java):

1. Includi file di progetto.

   Includi file JAR client, come adobe-output-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto Client di output.

   * Crea un `ServiceClientFactory` oggetto contenente le proprietà di connessione.
   * Crea un `OutputClient` utilizzando il relativo costruttore e passando `ServiceClientFactory` oggetto.

1. Fare riferimento a un&#39;origine dati XML.

   * Crea un `java.io.FileInputStream` oggetto che rappresenta l&#39;origine dati XML utilizzata per compilare il documento PDF/A utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del file XML.
   * Crea un `com.adobe.idp.Document` utilizzando il relativo costruttore e passando `java.io.FileInputStream` oggetto.

1. Impostare le opzioni di esecuzione di PDF/A.

   * Crea un `PDFOutputOptionsSpec` utilizzando il relativo costruttore.
   * Imposta l&#39;opzione URI file richiamando il `PDFOutputOptionsSpec` dell’oggetto `setFileURI` metodo . Passa un valore stringa che specifica la posizione del file PDF generato dal servizio Output. L’opzione URI file è relativa al server applicazioni J2EE che ospita AEM Forms, non al computer client.

1. Imposta le opzioni di esecuzione del rendering.

   * Crea un `RenderOptionsSpec` utilizzando il relativo costruttore.
   * Imposta la `PDFAConformance` richiamando il `RenderOptionsSpec` dell’oggetto `setPDFAConformance` e passare un `PDFAConformance` valore enum che specifica il livello di conformità. Ad esempio, per specificare il livello di conformità A, passare `PDFAConformance.A`.
   * Imposta la `PDFARevisionNumber` richiamando il `RenderOptionsSpec` dell’oggetto `setPDFARevisionNumber` metodo e passaggio `PDFARevisionNumber.Revision_1`.

   >[!NOTE]
   >
   >La versione PDF di un documento PDF/A è 1.4 indipendentemente dal valore specificato per il `RenderOptionsSpec` dell’oggetto `setPdfVersion`*metodo .*

1. Genera un documento PDF/A.

   Crea un documento PDF/A richiamando il `OutputClient` dell’oggetto `generatePDFOutput` e passando i seguenti valori:

   * A `TransformationFormat` valore di enumerazione. Per generare un documento PDF/A, specificare `TransformationFormat.PDFA`.
   * Valore stringa che specifica il nome della struttura del modulo.
   * Valore stringa che specifica la directory principale del contenuto in cui si trova la struttura del modulo.
   * A `PDFOutputOptionsSpec` oggetto contenente le opzioni di runtime di PDF.
   * A `RenderOptionsSpec` oggetto contenente le opzioni di esecuzione del rendering.
   * La `com.adobe.idp.Document` oggetto che contiene l’origine dati XML contenente i dati da unire alla struttura del modulo.

   La `generatePDFOutput` restituisce un `OutputResult` oggetto contenente i risultati dell&#39;operazione.

   >[!NOTE]
   >
   >La `OutputResult` dell’oggetto `getRecordLevelMetaDataList` restituisce il metodo `null`.

   >[!NOTE]
   >
   >È inoltre possibile creare un documento PDF/A richiamando il `OutputClient` dell’oggetto `generatePDFOutput`metodo 2. (Vedi [Trasmissione di documenti situati in Content Services (obsoleto) al servizio di output](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service).)

1. Recupera i risultati dell’operazione.

   * Crea un `com.adobe.idp.Document` che rappresenta lo stato `generatePDFOutput` richiamando il metodo `OutputResult` dell’oggetto `getStatusDoc` metodo .
   * Crea un `java.io.File` oggetto che conterrà i risultati dell&#39;operazione. Assicurati che l&#39;estensione del nome file sia .xml.
   * Richiama il `com.adobe.idp.Document` dell’oggetto `copyToFile` per copiare il contenuto del `com.adobe.idp.Document` al file (assicurati di utilizzare `com.adobe.idp.Document` oggetto restituito da `getStatusDoc` metodo).

   >[!NOTE]
   >
   >Anche se il servizio Output scrive il documento PDF/A nel percorso specificato dall&#39;argomento passato al `PDFOutputOptionsSpec` dell’oggetto `setFileURI` è possibile recuperare in modo programmatico il documento PDF/A richiamando il `OutputResult` dell’oggetto `getGeneratedDoc` metodo .

**Consulta anche**

[Riepilogo dei passaggi](creating-document-output-streams.md#summary-of-steps)

[Avvio rapido (modalità SOAP): Creazione di un documento PDF/A tramite l’API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-a-document-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

### Creare un documento PDF/A utilizzando l’API del servizio Web {#create-a-pdf-a-document-using-the-web-service-api}

Crea un documento PDF/A utilizzando l’API di output (servizio Web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurati di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l’indirizzo IP del server che ospita AEM Forms.

1. Creare un oggetto Client di output.

   * Crea un `OutputServiceClient` utilizzando il relativo costruttore predefinito.
   * Crea un `OutputServiceClient.Endpoint.Address` utilizzando `System.ServiceModel.EndpointAddress` costruttore. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/OutputService?blob=mtom`.) Non è necessario utilizzare il `lc_version` attributo. Questo attributo viene utilizzato quando si crea un riferimento a un servizio. Tuttavia, specifica `?blob=mtom` per utilizzare MTOM.
   * Crea un `System.ServiceModel.BasicHttpBinding` ottenendo il valore del `OutputServiceClient.Endpoint.Binding` campo . Imposta il valore restituito su `BasicHttpBinding`.
   * Imposta la `System.ServiceModel.BasicHttpBinding` dell’oggetto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegnare il nome utente del modulo di AEM al campo `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore della password corrispondente al campo `OutputServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Fare riferimento a un&#39;origine dati XML.

   * Crea un `BLOB` utilizzando il relativo costruttore. La `BLOB` viene utilizzato per memorizzare i dati che verranno uniti al documento PDF/A.
   * Crea un `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF da crittografare e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto del `System.IO.FileStream` oggetto. È possibile determinare le dimensioni dell&#39;array di byte ottenendo il `System.IO.FileStream` dell’oggetto `Length` proprietà.
   * Compilare l&#39;array di byte con i dati del flusso richiamando il `System.IO.FileStream` dell’oggetto `Read` e passare l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare `BLOB` oggetto assegnando il relativo `MTOM` con il contenuto dell&#39;array di byte.

1. Impostare le opzioni di esecuzione di PDF/A.

   * Crea un `PDFOutputOptionsSpec` utilizzando il relativo costruttore.
   * Impostare l&#39;opzione URI file assegnando un valore stringa che specifica la posizione del file PDF generato dal servizio Output nel `PDFOutputOptionsSpec` dell’oggetto `fileURI` membro dati. L&#39;opzione URI file è relativa al server applicazioni J2EE che ospita AEM Forms, non al computer client

1. Imposta le opzioni di esecuzione del rendering.

   * Crea un `RenderOptionsSpec` utilizzando il relativo costruttore.
   * Imposta la `PDFAConformance` assegnando un valore `PDFAConformance` valore enum per `RenderOptionsSpec` dell’oggetto `PDFAConformance` membro dati. Ad esempio, per specificare il livello di conformità A, assegnare `PDFAConformance.A` a questo membro dati.
   * Imposta la `PDFARevisionNumber` assegnando un valore `PDFARevisionNumber` valore enum per `RenderOptionsSpec` dell’oggetto `PDFARevisionNumber` membro dati. Assegna `PDFARevisionNumber.Revision_1` a questo membro dati.

   >[!NOTE]
   >
   >La versione PDF di un documento PDF/A è 1.4 indipendentemente dal valore specificato.

1. Genera un documento PDF/A.

   Creare un documento PDF richiamando il `OutputServiceService` dell’oggetto `generatePDFOutput`e passando i seguenti valori:

   * Un valore di enumerazione TransformationFormat. Per generare un documento PDF, specificare `TransformationFormat.PDFA`.
   * Valore stringa che specifica il nome della struttura del modulo.
   * Valore stringa che specifica la directory principale del contenuto in cui si trova la struttura del modulo.
   * A `PDFOutputOptionsSpec` oggetto contenente le opzioni di runtime di PDF.
   * A `RenderOptionsSpec` oggetto contenente le opzioni di esecuzione del rendering.
   * La `BLOB` oggetto contenente l’origine dati XML contenente i dati da unire alla struttura del modulo.
   * A `BLOB` oggetto popolato da `generatePDFOutput` metodo . La `generatePDFOutput` popola l&#39;oggetto con i metadati generati che descrivono il documento. Questo valore di parametro è necessario solo per la chiamata al servizio Web.
   * A `BLOB` oggetto popolato da `generatePDFOutput` metodo . La `generatePDFOutput` popola l&#39;oggetto con i dati dei risultati. Questo valore di parametro è necessario solo per la chiamata al servizio Web.
   * Un `OutputResult` oggetto contenente i risultati dell&#39;operazione. Questo valore di parametro è necessario solo per la chiamata al servizio Web.

   >[!NOTE]
   >
   >È inoltre possibile creare un documento PDF/A richiamando il `OutputClient` dell’oggetto `generatePDFOutput`metodo 2. (Vedi [Trasmissione di documenti situati in Content Services (obsoleto) al servizio di output](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service).)

1. Recupera i risultati dell’operazione.

   * Crea un `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta una posizione di file XML contenente i dati dei risultati. Assicurati che l&#39;estensione del nome file sia .xml.
   * Creare un array di byte che memorizza il contenuto dei dati del `BLOB` oggetto popolato con i dati dei risultati da `OutputServiceService` dell’oggetto `generatePDFOutput` (l&#39;ottavo parametro). Compilare l’array di byte ottenendo il valore del `BLOB` dell’oggetto `MTOM` campo .
   * Crea un `System.IO.BinaryWriter` richiamando il relativo costruttore e passando `System.IO.FileStream` oggetto.
   * Scrivere il contenuto dell&#39;array di byte nel file XML richiamando il `System.IO.BinaryWriter` dell’oggetto `Write` e passare l&#39;array di byte.

**Consulta anche**

[Riepilogo dei passaggi](creating-document-output-streams.md#summary-of-steps)

[Richiamo di AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamo di AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Trasmissione di documenti situati in Content Services (obsoleto) al servizio di output {#passing-documents-located-in-content-services-deprecated-to-the-output-service}

Il servizio Output esegue il rendering di un modulo PDF non interattivo basato su una struttura del modulo generalmente salvata come file XDP e creata in Designer. Puoi trasmettere un `com.adobe.idp.Document` oggetto contenente la struttura del modulo al servizio Output. Il servizio Output esegue quindi il rendering della struttura del modulo che si trova nel `com.adobe.idp.Document` oggetto.

Il vantaggio di passare un `com.adobe.idp.Document` l&#39;oggetto al servizio Output è che altre operazioni del servizio AEM Forms restituiscono un `com.adobe.idp.Document` istanza. Cioè, puoi ottenere un `com.adobe.idp.Document` istanza da un&#39;altra operazione di servizio ed esegui il rendering. Ad esempio, si supponga che un file XDP sia memorizzato in un nodo Content Services (obsoleto) denominato `/Company Home/Form Designs`, come illustrato nella figura seguente.

È possibile recuperare in modo programmatico il file Loan.xdp da Content Services (obsoleto) e passare il file XDP al servizio Output all&#39;interno di un `com.adobe.idp.Document` oggetto.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Forms, vedi [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-2}

Per passare un documento ottenuto da Content Services (obsoleto) al servizio Output, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Creare un oggetto Output e un oggetto API client di gestione documenti.
1. Recupera la struttura del modulo da Content Services (obsoleto).
1. Eseguire il rendering del modulo PDF non interattivo.
1. Esegui un&#39;azione con il flusso di dati.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, includi i file proxy.

**Creare un oggetto Output e un oggetto API client di gestione documenti**

Prima di eseguire un’operazione API del servizio di output a livello di programmazione, creare un oggetto API client di output. Inoltre, poiché questo flusso di lavoro recupera un file XDP da Content Services (obsoleto), crea un oggetto API di gestione dei documenti.

**Recupera la struttura del modulo da Content Services (obsoleto)**

Recupera il file XDP da Content Services (obsoleto) utilizzando l’API Java o del servizio Web. Il file XDP viene restituito all&#39;interno di un `com.adobe.idp.Document` istanza (o `BLOB` (se utilizzi servizi web). È quindi possibile passare il `com.adobe.idp.Document` al servizio Output.

**Rendering del modulo PDF non interattivo**

Per eseguire il rendering di un modulo non interattivo, passare la `com.adobe.idp.Document` istanza restituita da Content Services (obsoleto) al servizio Output.

>[!NOTE]
>
>Due nuovi metodi denominati `generatePDFOutput2`e g `eneratePrintedOutput2`accettare `com.adobe.idp.Document` oggetto contenente una struttura del modulo. È inoltre possibile passare un `com.adobe.idp.Document`che contiene la struttura del modulo al servizio Output quando si invia un flusso di stampa a una stampante di rete.

**Eseguire un’azione con il flusso di dati del modulo**

È possibile salvare il modulo non interattivo come file PDF. Il modulo può essere visualizzato in Adobe Reader o Acrobat.

**Consulta anche**

[Trasmettere i documenti al servizio di output utilizzando l’API Java](creating-document-output-streams.md#pass-documents-to-the-output-service-using-the-java-api)

[Trasmettere i documenti al servizio di output utilizzando l’API del servizio Web](creating-document-output-streams.md#pass-documents-to-the-output-service-using-the-web-service-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API del servizio di output](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

[Creazione di documenti PDF tramite frammenti](creating-document-output-streams.md#creating-pdf-documents-using-fragments)

### Trasmettere i documenti al servizio di output utilizzando l’API Java {#pass-documents-to-the-output-service-using-the-java-api}

Passa un documento recuperato da Content Services (obsoleto) utilizzando il servizio di output e l’API Content Services (obsoleto):

1. Includi file di progetto.

   Includi file JAR client, come adobe-output-client.jar e adobe-contentservices-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto Output e un oggetto API client di gestione documenti.

   * Crea un `ServiceClientFactory` oggetto contenente le proprietà di connessione. (Vedi [Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * Crea un `OutputClient` utilizzando il relativo costruttore e passando `ServiceClientFactory` oggetto.
   * Crea un `DocumentManagementServiceClientImpl` utilizzando il relativo costruttore e passando `ServiceClientFactory` oggetto.

1. Recupera la struttura del modulo da Content Services (obsoleto).

   Richiama il `DocumentManagementServiceClientImpl` dell’oggetto `retrieveContent` e passare i seguenti valori:

   * Valore stringa che specifica l&#39;archivio in cui viene aggiunto il contenuto. Lo store predefinito è `SpacesStore`. Questo valore è un parametro obbligatorio.
   * Valore stringa che specifica il percorso completo del contenuto da recuperare (ad esempio, `/Company Home/Form Designs/Loan.xdp`). Questo valore è un parametro obbligatorio.
   * Valore stringa che specifica la versione. Questo valore è un parametro facoltativo ed è possibile trasmettere una stringa vuota. In questa situazione, viene recuperata la versione più recente.

   La `retrieveContent` restituisce un `CRCResult` oggetto che contiene il file XDP. Recupera un `com.adobe.idp.Document` richiamando la `CRCResult` dell’oggetto `getDocument` metodo .

1. Eseguire il rendering del modulo PDF non interattivo.

   Richiama il `OutputClient` dell’oggetto `generatePDFOutput2` e passare i seguenti valori:

   * A `TransformationFormat` valore di enumerazione. Per generare un documento PDF, specificare `TransformationFormat.PDF`.
   * Valore stringa che specifica la directory principale del contenuto in cui si trovano le risorse aggiuntive, ad esempio le immagini.
   * A `com.adobe.idp.Document` oggetto che rappresenta la struttura del modulo (utilizzare l&#39;istanza restituita dal `CRCResult` dell’oggetto `getDocument` metodo).
   * A `PDFOutputOptionsSpec` oggetto contenente le opzioni di runtime di PDF.
   * A `RenderOptionsSpec` oggetto contenente le opzioni di esecuzione del rendering.
   * La `com.adobe.idp.Document` oggetto contenente l’origine dati XML contenente i dati da unire alla struttura del modulo.

   La `generatePDFOutput2` restituisce un `OutputResult` oggetto contenente i risultati dell&#39;operazione.

1. Eseguire un’azione con il flusso di dati del modulo.

   * Recupera un `com.adobe.idp.Document` oggetto che rappresenta il modulo non interattivo richiamando il `OutputResult` dell’oggetto `getGeneratedDoc` metodo .
   * Crea un `java.io.File` oggetto contenente i risultati dell&#39;operazione. Assicurati che l&#39;estensione del nome file sia .pdf.
   * Richiama il `com.adobe.idp.Document` dell’oggetto `copyToFile` per copiare il contenuto del `com.adobe.idp.Document` al file (assicurati di utilizzare `com.adobe.idp.Document` oggetto restituito da `getGeneratedDoc` metodo).

**Consulta anche**

[Riepilogo dei passaggi](creating-document-output-streams.md#summary-of-steps)

[Avvio rapido (modalità EJB): Trasmissione di documenti al servizio di output tramite l’API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-documents-to-the-output-service-using-the-java-api)

[Avvio rapido (modalità SOAP): Trasmissione di documenti al servizio di output tramite l’API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-documents-to-the-output-service-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Trasmettere i documenti al servizio di output utilizzando l’API del servizio Web {#pass-documents-to-the-output-service-using-the-web-service-api}

Passa un documento recuperato da Content Services (obsoleto) utilizzando il servizio di output e l’API Content Services (obsoleto) (servizio Web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Poiché questa applicazione client richiama due servizi AEM Forms, crea due riferimenti al servizio. Utilizzare la seguente definizione WSDL per il riferimento al servizio associato al servizio Output: `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   Utilizzare la seguente definizione WSDL per il riferimento al servizio associato al servizio Document Management: `http://localhost:8080/soap/services/DocumentManagementService?WSDL&lc_version=9.0.1`.

   Perché `BLOB` il tipo di dati è comune a entrambi i riferimenti di servizio e definisce completamente il `BLOB` tipo di dati quando viene utilizzato. All&#39;avvio rapido del servizio Web corrispondente, `BLOB` le istanze sono completamente qualificate.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l’indirizzo IP del server che ospita AEM Forms.

1. Creare un oggetto Output e un oggetto API client di gestione documenti.

   * Crea un `OutputServiceClient` utilizzando il relativo costruttore predefinito.
   * Crea un `OutputServiceClient.Endpoint.Address` utilizzando `System.ServiceModel.EndpointAddress` costruttore. Passa un valore stringa che specifica il WSDL al servizio Forms (ad esempio, `http://localhost:8080/soap/services/OutputService?blob=mtom`). Non è necessario utilizzare il `lc_version` attributo. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Crea un `System.ServiceModel.BasicHttpBinding` ottenendo il valore del `OutputServiceClient.Endpoint.Binding` campo . Imposta il valore restituito su `BasicHttpBinding`.
   * Imposta la `System.ServiceModel.BasicHttpBinding` dell’oggetto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegnare il nome utente del modulo di AEM al campo `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore della password corrispondente al campo `OutputServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

   >[!NOTE]
   >
   >Ripeti questi passaggi per `DocumentManagementServiceClient`client di servizio.

1. Recupera la struttura del modulo da Content Services (obsoleto).

   Recupera il contenuto richiamando il `DocumentManagementServiceClient` dell’oggetto `retrieveContent` e passando i seguenti valori:

   * Valore stringa che specifica l&#39;archivio in cui viene aggiunto il contenuto. Lo store predefinito è `SpacesStore`. Questo valore è un parametro obbligatorio.
   * Valore stringa che specifica il percorso completo del contenuto da recuperare (ad esempio, `/Company Home/Form Designs/Loan.xdp`). Questo valore è un parametro obbligatorio.
   * Valore stringa che specifica la versione. Questo valore è un parametro facoltativo ed è possibile trasmettere una stringa vuota. In questa situazione, viene recuperata la versione più recente.
   * Parametro di output della stringa che memorizza il valore del collegamento di ricerca.
   * A `BLOB` parametro di output che memorizza il contenuto. Puoi utilizzare questo parametro di output per recuperare il contenuto.
   * A `ServiceReference1.MyMapOf_xsd_string_To_xsd_anyType` parametro di output che memorizza gli attributi di contenuto.
   * A `CRCResult` parametro di output. Invece di utilizzare questo oggetto, è possibile utilizzare il `BLOB` parametro di output per recuperare il contenuto.

1. Eseguire il rendering del modulo PDF non interattivo.

   Richiama il `OutputServiceClient` dell’oggetto `generatePDFOutput2` e passare i seguenti valori:

   * A `TransformationFormat` valore di enumerazione. Per generare un documento PDF, specificare `TransformationFormat.PDF`.
   * Valore stringa che specifica la directory principale del contenuto in cui si trovano le risorse aggiuntive, ad esempio le immagini.
   * A `BLOB` che rappresenta la struttura del modulo (utilizzare `BLOB` istanza restituita da Content Services (obsoleto).
   * A `PDFOutputOptionsSpec` oggetto contenente le opzioni di runtime di PDF.
   * A `RenderOptionsSpec` oggetto contenente le opzioni di esecuzione del rendering.
   * La `BLOB` oggetto contenente l’origine dati XML contenente i dati da unire alla struttura del modulo.
   * Uscita `BLOB` oggetto popolato da `generatePDFOutput2` metodo . La `generatePDFOutput2` popola l&#39;oggetto con i metadati generati che descrivono il documento. (Questo valore di parametro è richiesto solo per la chiamata al servizio Web).
   * Uscita `OutputResult` oggetto contenente i risultati dell&#39;operazione. (Questo valore di parametro è richiesto solo per la chiamata al servizio Web).

   La `generatePDFOutput2` restituisce un `BLOB` che contiene il modulo PDF non interattivo.

1. Eseguire un’azione con il flusso di dati del modulo.

   * Crea un `System.IO.FileStream` richiamando il relativo costruttore. Passa un valore stringa che rappresenta la posizione del file del documento PDF interattivo e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto del `BLOB` oggetto recuperato dal `generatePDFOutput2` metodo . Compilare l’array di byte ottenendo il valore del `BLOB` dell’oggetto `MTOM` membro dati.
   * Crea un `System.IO.BinaryWriter` richiamando il relativo costruttore e passando `System.IO.FileStream` oggetto.
   * Scrivi il contenuto dell’array di byte in un file PDF richiamando il `System.IO.BinaryWriter` dell’oggetto `Write` e passare l&#39;array di byte.

**Consulta anche**

[Riepilogo dei passaggi](creating-document-output-streams.md#summary-of-steps)

[Richiamo di AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## Trasferimento dei documenti presenti nell&#39;archivio al servizio di output {#passing-documents-located-in-the-repository-to-the-output-service}

Il servizio Output esegue il rendering di un modulo PDF non interattivo basato su una struttura del modulo generalmente salvata come file XDP e creata in Designer. Puoi trasmettere un `com.adobe.idp.Document` oggetto contenente la struttura del modulo al servizio Output. Il servizio Output esegue quindi il rendering della struttura del modulo che si trova nel `com.adobe.idp.Document` oggetto.

Il vantaggio di passare un `com.adobe.idp.Document` l&#39;oggetto al servizio Output è che altre operazioni del servizio AEM Forms restituiscono un `com.adobe.idp.Document` istanza. Cioè, puoi ottenere un `com.adobe.idp.Document` istanza da un&#39;altra operazione di servizio ed esegui il rendering. Ad esempio, si supponga che un file XDP sia memorizzato nell’archivio AEM Forms, come illustrato di seguito.

![pd_pd_formrepository](assets/pd_pd_formrepository.png)

La *FormsFolder* La cartella è una posizione definita dall’utente nell’archivio AEM Forms (questa posizione è un esempio e non esiste per impostazione predefinita). In questo esempio, una struttura del modulo denominata Loan.xdp si trova in questa cartella. Oltre alla struttura del modulo, in questa posizione è possibile memorizzare altre informazioni collaterali come le immagini. Il percorso di una risorsa situata nell’archivio AEM Forms è:

`Applications/Application-name/Application-version/Folder.../Filename`

È possibile recuperare in modo programmatico il file Loan.xdp dall&#39;archivio AEM Forms e passarlo al servizio Output all&#39;interno di un `com.adobe.idp.Document` oggetto.

È possibile creare un PDF basato su un file XDP presente nell’archivio utilizzando uno dei due modi seguenti: Puoi passare la posizione XDP tramite riferimento oppure recuperare l&#39;XDP dal repository a livello di programmazione e passarlo al servizio Output all&#39;interno di un file XDP.

[Avvio rapido (modalità EJB): Creazione di un documento PDF basato su un file XDP dell’applicazione utilizzando l’API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-an-application-xdp-file-using-the-java-api) (mostra come passare la posizione del file XDP tramite riferimento).

[Avvio rapido (modalità EJB): Trasmissione di un documento situato nell’archivio AEM Forms al servizio Output tramite l’API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-a-document-located-in-the-repository-to-the-output-service-using-the-java-api) (mostra come recuperare in modo programmatico il file XDP dall’archivio AEM Forms e passarlo al servizio Output all’interno di un `com.adobe.idp.Document` (istanza). (Questa sezione illustra come eseguire questa attività)

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Forms, vedi [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-3}

Per passare un documento ottenuto dall&#39;archivio AEM Forms al servizio Output, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Creare un oggetto Output e un oggetto API client di gestione documenti.
1. Recupera la struttura del modulo dall’archivio AEM Forms.
1. Eseguire il rendering del modulo PDF non interattivo.
1. Esegui un&#39;azione con il flusso di dati.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, includi i file proxy.

**Creare un oggetto Output e un oggetto API client di gestione documenti**

Prima di eseguire un’operazione API del servizio di output a livello di programmazione, creare un oggetto API client di output. Inoltre, poiché questo flusso di lavoro recupera un file XDP da Content Services (obsoleto), crea un oggetto API di gestione dei documenti.

**Recuperare la struttura del modulo dall’archivio AEM Forms**

Recupera il file XDP dall’archivio AEM Forms utilizzando l’API Repository. (Vedi [Lettura delle risorse](/help/forms/developing/aem-forms-repository.md#reading-resources).)

Il file XDP viene restituito all&#39;interno di un `com.adobe.idp.Document` istanza (o `BLOB` (se utilizzi servizi web). È quindi possibile passare il `com.adobe.idp.Document` istanza del servizio Output.

**Rendering del modulo PDF non interattivo**

Per eseguire il rendering di un modulo non interattivo, passare la `com.adobe.idp.Document` istanza restituita utilizzando l’API del repository di AEM Forms.

>[!NOTE]
>
>Due nuovi metodi denominati `generatePDFOutput2`e `generatePrintedOutput2`accettare `com.adobe.idp.Document`oggetto contenente una struttura del modulo. È inoltre possibile passare un `com.adobe.idp.Document` che contiene la struttura del modulo al servizio Output quando si invia un flusso di stampa a una stampante di rete.

**Eseguire un’azione con il flusso di dati del modulo**

È possibile salvare il modulo non interattivo come file PDF. Il modulo può essere visualizzato in Adobe Reader o Acrobat.

**Consulta anche**

[Trasmettere al servizio di output i documenti presenti nell’archivio utilizzando l’API Java](creating-document-output-streams.md#pass-documents-located-in-the-repository-to-the-output-service-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API del servizio di output](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

ResourceRepositoryClient

### Trasmettere al servizio di output i documenti presenti nell’archivio utilizzando l’API Java {#pass-documents-located-in-the-repository-to-the-output-service-using-the-java-api}

Passa un documento recuperato dall’archivio utilizzando il servizio di output e l’API dell’archivio (Java):

1. Includi file di progetto.

   Includi file JAR client, come adobe-output-client.jar e adobe-repository-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto Output e un oggetto API client di gestione documenti.

   * Crea un `ServiceClientFactory` oggetto contenente le proprietà di connessione. (Vedi [Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * Crea un `OutputClient` utilizzando il relativo costruttore e passando `ServiceClientFactory` oggetto.
   * Crea un `DocumentManagementServiceClientImpl` utilizzando il relativo costruttore e passando `ServiceClientFactory` oggetto.

1. Recupera la struttura del modulo dall’archivio AEM Forms.

   Richiama il `ResourceRepositoryClient` dell’oggetto `readResourceContent` e passare un valore stringa che specifica la posizione URI nel file XDP. Esempio: `/Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`. Questo valore è obbligatorio. Questo metodo restituisce un `com.adobe.idp.Document` istanza che rappresenta il file XDP.

1. Eseguire il rendering del modulo PDF non interattivo.

   Richiama il `OutputClient` dell’oggetto `generatePDFOutput2` e passare i seguenti valori:

   * A `TransformationFormat` valore di enumerazione. Per generare un documento PDF, specificare `TransformationFormat.PDF`.
   * Valore stringa che specifica la directory principale del contenuto in cui si trovano le risorse aggiuntive, ad esempio le immagini. Esempio: `repository:///Applications/FormsApplication/1.0/FormsFolder/`.
   * A `com.adobe.idp.Document` oggetto che rappresenta la struttura del modulo (utilizzare l&#39;istanza restituita dal `ResourceRepositoryClient` dell’oggetto `readResourceContent` metodo).
   * A `PDFOutputOptionsSpec` oggetto contenente le opzioni di runtime di PDF.
   * A `RenderOptionsSpec` oggetto contenente le opzioni di esecuzione del rendering.
   * La `com.adobe.idp.Document` oggetto contenente l’origine dati XML contenente i dati da unire alla struttura del modulo.

   La `generatePDFOutput2` restituisce un `OutputResult` oggetto contenente i risultati dell&#39;operazione.

1. Eseguire un’azione con il flusso di dati del modulo.

   * Recupera un `com.adobe.idp.Document` oggetto che rappresenta il modulo non interattivo richiamando il `OutputResult` dell’oggetto `getGeneratedDoc` metodo .
   * Crea un `java.io.File` oggetto contenente i risultati dell&#39;operazione. Assicurati che l&#39;estensione del nome file sia .pdf.
   * Richiama il `com.adobe.idp.Document` dell’oggetto `copyToFile` per copiare il contenuto del `com.adobe.idp.Document` al file (assicurati di utilizzare `com.adobe.idp.Document` oggetto restituito da `getGeneratedDoc` metodo).

**Consulta anche**

[Riepilogo dei passaggi](creating-document-output-streams.md#summary-of-steps)

[Avvio rapido (modalità EJB): Trasmissione di un documento situato nell’archivio AEM Forms al servizio Output tramite l’API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-a-document-located-in-the-repository-to-the-output-service-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Creazione di documenti PDF tramite frammenti {#creating-pdf-documents-using-fragments}

È possibile utilizzare i servizi Output e Assembler per creare un flusso di output, ad esempio un documento PDF, basato sui frammenti. Il servizio Assembler assembla un documento XDP basato su frammenti che si trovano in più file XDP. Il documento XDP assemblato viene passato al servizio Output, che crea un documento PDF. Anche se questo flusso di lavoro mostra un documento PDF in fase di generazione, il servizio Output può generare altri tipi di output, ad esempio ZPL, per questo flusso di lavoro. Un documento PDF viene utilizzato solo a scopo di discussione.

L’illustrazione seguente mostra questo flusso di lavoro.

![cp_cp_outputassemblefragments](assets/cp_cp_outputassemblefragments.png)

Prima della lettura *Creazione di documenti PDF tramite frammenti*, si consiglia di acquisire familiarità con l&#39;utilizzo del servizio Assembler per assemblare più documenti XDP. (Vedi [Assemblaggio di più frammenti XDP](/help/forms/developing/assembling-pdf-documents.md#assembling-multiple-xdp-fragments).)

>[!NOTE]
>
>È inoltre possibile passare una struttura del modulo assemblata dal servizio Assembler al servizio Forms anziché al servizio Output. La differenza principale tra il servizio Output e il servizio Forms è che il servizio Forms genera documenti PDF interattivi e il servizio Output produce documenti PDF non interattivi. Inoltre, il servizio Forms non può generare flussi di output basati su stampante come ZPL.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Output, vedi [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-4}

Per creare un documento PDF basato sui frammenti, procedere come segue:

1. Includi file di progetto.
1. Creare un oggetto client Output e Assembler.
1. Utilizzare il servizio Assembler per generare la struttura del modulo.
1. Utilizzare il servizio Output per generare il documento PDF.
1. Salvare il documento PDF come file PDF.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

**Creare un oggetto client Output e Assembler**

Prima di eseguire un’operazione API del servizio Output a livello di programmazione, creare un oggetto API client di output. Inoltre, poiché questo flusso di lavoro richiama il servizio Assembler per creare la struttura del modulo, creare un oggetto API client Assembler.

**Utilizzare il servizio Assembler per generare la struttura del modulo**

Utilizzare il servizio Assembler per generare la struttura del modulo utilizzando i frammenti. Il servizio Assembler restituisce un `com.adobe.idp.Document` istanza che contiene la struttura del modulo.

**Utilizzare il servizio Output per generare il documento PDF**

È possibile utilizzare il servizio Output per generare un documento PDF utilizzando la struttura del modulo creata dal servizio Assembler. Passa la `com.adobe.idp.Document` istanza restituita dal servizio Assembler al servizio Output.

**Salvare il documento PDF come file PDF**

Dopo la generazione di un documento PDF da parte del servizio Output, è possibile salvarlo come file PDF.

**Consulta anche**

[Creare un documento PDF basato sui frammenti utilizzando l’API Java](creating-document-output-streams.md#create-a-pdf-document-based-on-fragments-using-the-java-api)

[Creare un documento PDF basato sui frammenti utilizzando l’API del servizio Web](creating-document-output-streams.md#create-a-pdf-document-based-on-fragments-using-the-web-service-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API del servizio di output](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

[Assemblaggio di più frammenti XDP](/help/forms/developing/assembling-pdf-documents.md#assembling-multiple-xdp-fragments)

[Creazione di documenti PDF](creating-document-output-streams.md#creating-pdf-documents)

### Creare un documento PDF basato sui frammenti utilizzando l’API Java {#create-a-pdf-document-based-on-fragments-using-the-java-api}

Crea un documento PDF basato sui frammenti utilizzando l’API del servizio di output e l’API del servizio Assembler (Java):

1. Includi file di progetto.

   Includi file JAR client, come adobe-output-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto client Output e Assembler.

   * Crea un `ServiceClientFactory` oggetto contenente le proprietà di connessione.
   * Crea un `OutputClient` utilizzando il relativo costruttore e passando `ServiceClientFactory` oggetto.
   * Crea un `AssemblerServiceClient` utilizzando il relativo costruttore e passando `ServiceClientFactory` oggetto.

1. Utilizzare il servizio Assembler per generare la struttura del modulo.

   Richiama il `AssemblerServiceClient` dell’oggetto `invokeDDX` e trasmettere i seguenti valori richiesti:

   * A `com.adobe.idp.Document` oggetto che rappresenta il documento DDX da utilizzare.
   * A `java.util.Map` oggetto che contiene i file XDP di input.
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` oggetto che specifica le opzioni di esecuzione, incluso il carattere predefinito e il livello del registro di lavoro.

   La `invokeDDX` restituisce un `com.adobe.livecycle.assembler.client.AssemblerResult` oggetto contenente il documento XDP assemblato. Per recuperare il documento XDP assemblato, eseguire le operazioni seguenti:

   * Richiama il `AssemblerResult` dell’oggetto `getDocuments` metodo . Questo metodo restituisce un `java.util.Map` oggetto.
   * Itera attraverso il `java.util.Map` finché non trovi il risultato `com.adobe.idp.Document` oggetto.
   * Richiama il `com.adobe.idp.Document` dell’oggetto `copyToFile` metodo per estrarre il documento XDP assemblato.


1. Utilizzare il servizio Output per generare il documento PDF.

   Richiama il `OutputClient` dell’oggetto `generatePDFOutput2` e passare i seguenti valori:

   * A `TransformationFormat` valore di enumerazione. Per generare un documento PDF, specificare `TransformationFormat.PDF`
   * Valore stringa che specifica la directory principale del contenuto in cui si trovano le risorse aggiuntive, ad esempio le immagini.
   * A `com.adobe.idp.Document` oggetto che rappresenta la struttura del modulo (utilizzare l&#39;istanza restituita dal servizio Assembler)
   * A `PDFOutputOptionsSpec` oggetto contenente le opzioni di esecuzione di PDF
   * A `RenderOptionsSpec` oggetto contenente le opzioni di esecuzione del rendering
   * La `com.adobe.idp.Document` oggetto contenente l’origine dati XML contenente i dati da unire alla struttura del modulo

   La `generatePDFOutput2` restituisce un `OutputResult` oggetto contenente i risultati dell&#39;operazione

1. Salvare il documento PDF come file PDF.

   * Recupera un `com.adobe.idp.Document` oggetto che rappresenta il documento PDF richiamando il `OutputResult` dell’oggetto `getGeneratedDoc` metodo .
   * Crea un `java.io.File` oggetto contenente i risultati dell&#39;operazione. Assicurati che l&#39;estensione del nome del file sia .pdf.
   * Richiama il `com.adobe.idp.Document` dell’oggetto `copyToFile` per copiare il contenuto del `com.adobe.idp.Document` al file. (Assicurati di utilizzare il `com.adobe.idp.Document` oggetto che `getGeneratedDoc` restituito.).

**Consulta anche**

[Riepilogo dei passaggi](creating-document-output-streams.md#summary-of-steps)

[Avvio rapido (modalità EJB): Creazione di un documento PDF basato su frammenti tramite l’API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-fragments-using-the-java-api)

[Avvio rapido (modalità SOAP): Creazione di un documento PDF basato su frammenti tramite l’API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-fragments-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

### Creare un documento PDF basato sui frammenti utilizzando l’API del servizio Web {#create-a-pdf-document-based-on-fragments-using-the-web-service-api}

Crea un documento PDF basato sui frammenti utilizzando l’API del servizio di output e l’API del servizio Assembler (servizio Web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Utilizzare la seguente definizione WSDL per il riferimento al servizio associato al servizio Output:

   ```java
    http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1.
   ```

   Utilizzare la seguente definizione WSDL per il riferimento al servizio associato al servizio Assembler:

   ```java
    http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1.
   ```

   Perché `BLOB` il tipo di dati è comune a entrambi i riferimenti di servizio e definisce completamente il `BLOB` tipo di dati quando viene utilizzato. All&#39;avvio rapido del servizio Web corrispondente, `BLOB` le istanze sono completamente qualificate.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l’indirizzo IP del server che ospita AEM Forms.

1. Creare un oggetto client Output e Assembler.

   * Crea un `OutputServiceClient` utilizzando il relativo costruttore predefinito.
   * Crea un `OutputServiceClient.Endpoint.Address` utilizzando `System.ServiceModel.EndpointAddress` costruttore. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/OutputService?blob=mtom`.) Non è necessario utilizzare il `lc_version` attributo. Questo attributo viene utilizzato quando si crea un riferimento a un servizio. Tuttavia, specifica `?blob=mtom` per utilizzare MTOM.
   * Crea un `System.ServiceModel.BasicHttpBinding` ottenendo il valore del `OutputServiceClient.Endpoint.Binding` campo . Imposta il valore restituito su `BasicHttpBinding`.
   * Imposta la `System.ServiceModel.BasicHttpBinding` dell’oggetto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegnare il nome utente dei moduli di AEM al `OutputServiceClient.ClientCredentials.UserName.UserName`campo .
      * Assegna il valore della password corrispondente al `OutputServiceClient.ClientCredentials.UserName.Password`campo .
      * Assegna il valore costante `HttpClientCredentialType.Basic` al `BasicHttpBindingSecurity.Transport.ClientCredentialType`campo .
   * Assegna `BasicHttpSecurityMode.TransportCredentialOnly` valore costante nel `BasicHttpBindingSecurity.Security.Mode`campo .

   >[!NOTE]
   >
   >Ripeti questi passaggi per `AssemblerServiceClient`oggetto.

1. Utilizzare il servizio Assembler per generare la struttura del modulo.

   Richiama il `AssemblerServiceClient` dell’oggetto `invokeDDX` e passare i seguenti valori:

   * A `BLOB` oggetto che rappresenta il documento DDX
   * La `MyMapOf_xsd_string_To_xsd_anyType` oggetto contenente i file richiesti
   * Un `AssemblerOptionSpec` oggetto che specifica le opzioni di esecuzione

   La `invokeDDX` restituisce un `AssemblerResult` oggetto contenente i risultati del processo ed eventuali eccezioni. Per ottenere il documento XDP appena creato, esegui le seguenti operazioni:

   * Accedere al `AssemblerResult` dell’oggetto `documents` un campo `Map` oggetto contenente i documenti PDF risultanti.
   * Itera attraverso il `Map` oggetto per recuperare la struttura del modulo assemblato. Cast del membro della matrice `value` a `BLOB`. Passa questo `BLOB` al servizio Output.


1. Utilizzare il servizio Output per generare il documento PDF.

   Richiama il `OutputServiceClient` dell’oggetto `generatePDFOutput2` e passare i seguenti valori:

   * A `TransformationFormat` valore di enumerazione. Per generare un documento PDF, specificare `TransformationFormat.PDF`.
   * Valore stringa che specifica la directory principale del contenuto in cui si trovano le risorse aggiuntive, ad esempio le immagini.
   * A `BLOB` che rappresenta la struttura del modulo (utilizzare `BLOB` istanza restituita dal servizio Assembler).
   * A `PDFOutputOptionsSpec` oggetto contenente le opzioni di runtime di PDF.
   * A `RenderOptionsSpec` oggetto contenente le opzioni di esecuzione del rendering.
   * La `BLOB` oggetto contenente l’origine dati XML contenente i dati da unire alla struttura del modulo.
   * Uscita `BLOB` oggetto che `generatePDFOutput2` viene compilato. La `generatePDFOutput2` popola l&#39;oggetto con i metadati generati che descrivono il documento. (Questo valore di parametro è richiesto solo per la chiamata al servizio Web).
   * Uscita `OutputResult` oggetto contenente i risultati dell&#39;operazione. (Questo valore di parametro è richiesto solo per la chiamata al servizio Web).

   La `generatePDFOutput2` restituisce un `BLOB` che contiene il modulo PDF non interattivo.

1. Salvare il documento PDF come file PDF.

   * Crea un `System.IO.FileStream` richiamando il relativo costruttore. Passa un valore stringa che rappresenta la posizione del file del documento PDF interattivo e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto del `BLOB` oggetto recuperato dal `generatePDFOutput2` metodo . Compilare l’array di byte ottenendo il valore del `BLOB` dell’oggetto `MTOM` membro dati.
   * Crea un `System.IO.BinaryWriter` richiamando il relativo costruttore e passando `System.IO.FileStream` oggetto.
   * Scrivi il contenuto dell’array di byte in un file PDF richiamando il `System.IO.BinaryWriter` dell’oggetto `Write` e passare l&#39;array di byte.

**Consulta anche**

[Riepilogo dei passaggi](creating-document-output-streams.md#summary-of-steps)

[Richiamo di AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## Stampa su file {#printing-to-files}

È possibile utilizzare il servizio Output per stampare su un file flussi quali PostScript, PCL (Printer Control Language) o i seguenti formati di etichetta:

* Zebra - ZPL
* Intermec - IPL
* Datamax - DPL
* TecToshiba - TPCL

Utilizzando il servizio Output, è possibile unire i dati XML con una struttura del modulo e stampare il modulo in un file. L&#39;illustrazione seguente mostra il servizio Output che crea file laser ed etichette.

>[!NOTE]
>
>Per informazioni sull&#39;invio di flussi di stampa alle stampanti, vedere [Invio di flussi di stampa alle stampanti](creating-document-output-streams.md#sending-print-streams-to-printers).

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Output, vedi [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-5}

Per stampare su un file, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Creare un oggetto Client di output.
1. Fare riferimento a un&#39;origine dati XML.
1. Impostare le opzioni di esecuzione della stampa necessarie per stampare su un file.
1. Stampa il flusso di stampa su un file.
1. Recupera i risultati dell’operazione.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso della classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è distribuito su JBoss)
* jbossall-client.jar (richiesto se AEM Forms è distribuito su JBoss)

se AEM Forms è distribuito su un server applicazioni J2EE supportato che non è JBoss, sarà necessario sostituire i file adobe-utilities.jar e jbossall-client.jar con file JAR specifici per il server applicazioni J2EE in cui viene distribuito AEM Forms. (Vedi [Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).)

**Creare un oggetto Client di output**

Prima di poter eseguire un&#39;operazione del servizio Output a livello di programmazione, è necessario creare un oggetto client del servizio Output. Se utilizzi l’API Java, crea un `OutputClient` oggetto. Se utilizzi l’API del servizio Web Output, crea un `OutputServiceService` oggetto.

**Riferimento a un’origine dati XML**

Per stampare un documento contenente dati, è necessario fare riferimento a un&#39;origine dati XML contenente elementi XML per ogni campo del modulo che si desidera compilare con i dati. Il nome dell&#39;elemento XML deve corrispondere al nome del campo. Un elemento XML viene ignorato se non corrisponde a un campo modulo o se il nome dell’elemento XML non corrisponde al nome del campo. Se vengono specificati tutti gli elementi XML, non è necessario stabilire una corrispondenza con l’ordine in cui vengono visualizzati gli elementi XML.

**Impostare le opzioni di esecuzione della stampa necessarie per stampare su un file**

Per stampare su un file, è necessario impostare l&#39;opzione File URI di esecuzione specificando la posizione e il nome del file su cui viene stampato il servizio Output. Ad esempio, per richiedere al servizio Output di stampare un file PostScript denominato *MutuiForm.ps* a C:\Adobe, specifica C:\Adobe\MortgageForm.ps.

>[!NOTE]
>
>È possibile definire opzioni di runtime facoltative. Per informazioni su tutte le opzioni che è possibile impostare, consulta la sezione `PrintedOutputOptionsSpec` riferimento di classe in [Riferimento API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Stampa il flusso di stampa su un file**

Dopo aver fatto riferimento a un&#39;origine dati XML valida contenente i dati del modulo e aver impostato le opzioni di esecuzione della stampa, è possibile richiamare il servizio Output, che lo causa nella stampa di un file.

**Recupera i risultati dell&#39;operazione**

Dopo l&#39;esecuzione di un&#39;operazione, il servizio Output restituisce vari elementi di dati, ad esempio dati XML, che specificano se l&#39;operazione ha avuto esito positivo.

**Consulta anche**

[Stampa su file utilizzando l’API Java](creating-document-output-streams.md#print-to-files-using-the-java-api)

[Stampa su file tramite l’API del servizio Web](creating-document-output-streams.md#print-to-files-using-the-web-service-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API del servizio di output](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Stampa su file utilizzando l’API Java {#print-to-files-using-the-java-api}

Stampa su un file utilizzando l’API di output (Java):

1. Includi file di progetto.

   Includi file JAR client, come adobe-output-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto Client di output.

   * Crea un `ServiceClientFactory` oggetto contenente le proprietà di connessione.
   * Crea un `OutputClient` utilizzando il relativo costruttore e passando `ServiceClientFactory` oggetto.

1. Fare riferimento a un&#39;origine dati XML.

   * Crea un `java.io.FileInputStream` oggetto che rappresenta l&#39;origine dati XML utilizzata per compilare il documento utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del file XML.
   * Crea un `com.adobe.idp.Document` utilizzando il relativo costruttore e passando `java.io.FileInputStream` oggetto.

1. Impostare le opzioni di esecuzione della stampa necessarie per stampare su un file.

   * Crea un `PrintedOutputOptionsSpec` utilizzando il relativo costruttore.
   * Specificare il file richiamando l&#39;oggetto PraintOutputOptionsSpec `setFileURI` e passare un valore stringa che rappresenta il nome e la posizione del file. Ad esempio, se si desidera che il servizio Output venga stampato in un file PostScript denominato MortagelForm.ps situato in C:\Adobe, specificare C:\\Adobe\MortgageForm.ps.
   * Specificare il numero di copie da stampare richiamando il `PrintedOutputOptionsSpec` dell’oggetto `setCopies` e passare un valore intero che rappresenta il numero di copie.

1. Stampa il flusso di stampa su un file.

   Stampa su un file richiamando il `OutputClient` dell’oggetto `generatePrintedOutput` e passando i seguenti valori:

   * A `PrintFormat` valore di enumerazione che specifica il formato del flusso di stampa da creare. Ad esempio, per creare un flusso di stampa PostScript, passare `PrintFormat.PostScript`.
   * Valore stringa che specifica il nome della struttura del modulo.
   * Valore stringa che specifica la posizione dei relativi file collaterali, ad esempio i file immagine.
   * Valore stringa che specifica la posizione del file XDC da utilizzare (è possibile passare `null` se è stato specificato il file XDC da utilizzare utilizzando `PrintedOutputOptionsSpec` oggetto).
   * La `PrintedOutputOptionsSpec` oggetto contenente le opzioni di esecuzione necessarie per la stampa in un file.
   * La `com.adobe.idp.Document` oggetto che contiene l&#39;origine dati XML contenente i dati del modulo.

   La `generatePrintedOutput` restituisce un `OutputResult` oggetto contenente i risultati dell&#39;operazione.

   >[!NOTE]
   >
   >La `OutputResult` dell’oggetto `getRecordLevelMetaDataList` restituisce il metodo `null`.

1. Recupera i risultati dell’operazione.

   * Crea un `com.adobe.idp.Document` che rappresenta lo stato `generatePrintedOutput` richiamando il metodo `OutputResult` dell’oggetto `getStatusDoc` il metodo `OutputResult` è stato restituito dall&#39;oggetto `generatePrintedOutput` metodo).
   * Crea un `java.io.File` oggetto che conterrà i risultati dell&#39;operazione. Assicurati che l&#39;estensione del file sia XML.
   * Richiama il `com.adobe.idp.Document` dell’oggetto `copyToFile` per copiare il contenuto del `com.adobe.idp.Document` al file (assicurati di utilizzare `com.adobe.idp.Document` oggetto restituito da `getStatusDoc` metodo).

**Consulta anche**

[Riepilogo dei passaggi](creating-document-output-streams.md#summary-of-steps)

[Avvio rapido (modalità SOAP): Stampa su un file tramite l’API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-printing-to-a-file-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

### Stampa su file tramite l’API del servizio Web {#print-to-files-using-the-web-service-api}

Stampa su un file utilizzando l’API di output (servizio Web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurati di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l’indirizzo IP del server che ospita AEM Forms.

1. Creare un oggetto Client di output.

   * Crea un `OutputServiceClient` utilizzando il relativo costruttore predefinito.
   * Crea un `OutputServiceClient.Endpoint.Address` utilizzando `System.ServiceModel.EndpointAddress` costruttore. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/OutputService?blob=mtom`.) Non è necessario utilizzare il `lc_version` attributo. Questo attributo viene utilizzato quando si crea un riferimento a un servizio. Tuttavia, specifica `?blob=mtom` per utilizzare MTOM.
   * Crea un `System.ServiceModel.BasicHttpBinding` ottenendo il valore del `OutputServiceClient.Endpoint.Binding` campo . Imposta il valore restituito su `BasicHttpBinding`.
   * Imposta la `System.ServiceModel.BasicHttpBinding` dell’oggetto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegnare il nome utente del modulo di AEM al campo `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore della password corrispondente al campo `OutputServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Fare riferimento a un&#39;origine dati XML.

   * Crea un `BLOB` utilizzando il relativo costruttore. La `BLOB` viene utilizzato per memorizzare i dati del modulo.
   * Crea un `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che specifica la posizione del file XML contenente i dati del modulo.
   * Creare un array di byte che memorizza il contenuto del `System.IO.FileStream` oggetto. È possibile determinare le dimensioni dell&#39;array di byte ottenendo il `System.IO.FileStream` dell’oggetto `Length` proprietà.
   * Compilare l&#39;array di byte con i dati del flusso richiamando il `System.IO.FileStream` dell’oggetto `Read` e passare l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare `BLOB` oggetto assegnando il relativo `binaryData` con il contenuto dell&#39;array di byte.

1. Impostare le opzioni di esecuzione della stampa necessarie per stampare su un file.

   * Crea un `PrintedOutputOptionsSpec` utilizzando il relativo costruttore.
   * Specificare il file assegnando un valore stringa che rappresenta la posizione e il nome del file al `PrintedOutputOptionsSpec` dell’oggetto `fileURI` membro dati. Ad esempio, se si desidera che il servizio Output venga stampato in un file PostScript denominato *MutuiForm.ps* situato in C:\Adobe, specifica C:\\Adobe\MortgageForm.ps.
   * Specificare il numero di copie da stampare assegnando un valore intero che rappresenta il numero di copie nel `PrintedOutputOptionsSpec` dell’oggetto `copies` membri dati.

1. Stampa il flusso di stampa su un file.

   Stampa su un file richiamando il `OutputServiceService` dell’oggetto `generatePrintedOutput` e passando i seguenti valori:

   * A `PrintFormat` valore di enumerazione che specifica il formato del flusso di stampa da creare. Ad esempio, per creare un flusso di stampa PostScript, passare `PrintFormat.PostScript`.
   * Valore stringa che specifica il nome della struttura del modulo.
   * Valore stringa che specifica la posizione dei relativi file collaterali, ad esempio i file immagine.
   * Valore stringa che specifica la posizione del file XDC da utilizzare (è possibile passare `null` se è stato specificato il file XDC da utilizzare utilizzando `PrintedOutputOptionsSpec` oggetto).
   * La `PrintedOutputOptionsSpec` oggetto contenente le opzioni di esecuzione della stampa necessarie per la stampa su un file.
   * La `BLOB` oggetto contenente l&#39;origine dati XML contenente i dati del modulo.
   * A `BLOB` oggetto popolato da `generatePDFOutput` metodo . La `generatePDFOutput` popola l&#39;oggetto con i metadati generati che descrivono il documento. Questo valore di parametro è necessario solo per la chiamata al servizio Web.
   * A `BLOB` oggetto popolato da `generatePDFOutput` metodo . La `generatePDFOutput` popola l&#39;oggetto con i dati dei risultati. Questo valore di parametro è necessario solo per la chiamata al servizio Web.
   * Un `OutputResult` oggetto contenente i risultati dell&#39;operazione. Questo valore di parametro è necessario solo per la chiamata al servizio Web.

1. Recupera i risultati dell’operazione.

   * Crea un `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta una posizione di file XML contenente i dati dei risultati. Assicurati che l&#39;estensione del file sia XML.
   * Creare un array di byte che memorizza il contenuto dei dati del `BLOB` oggetto popolato con i dati dei risultati da `OutputServiceService` dell’oggetto `generatePDFOutput` (l&#39;ottavo parametro). Compilare l’array di byte ottenendo il valore del `BLOB` dell’oggetto `MTOM` membro dati.
   * Crea un `System.IO.BinaryWriter` richiamando il relativo costruttore e passando `System.IO.FileStream` oggetto.
   * Scrivere il contenuto dell&#39;array di byte nel file XML richiamando il `System.IO.BinaryWriter` dell’oggetto `Write` e passare l&#39;array di byte.

**Consulta anche**

[Riepilogo dei passaggi](creating-document-output-streams.md#summary-of-steps)

[Richiamo di AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamo di AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Invio di flussi di stampa alle stampanti {#sending-print-streams-to-printers}

È possibile utilizzare il servizio Output per inviare flussi di stampa quali PostScript, PCL (Printer Control Language) o i seguenti formati di etichetta alle stampanti di rete:

* Zebra - ZPL
* Intermec - IPL
* Datamax - DPL
* TecToshiba - TPCL

Utilizzando il servizio Output, è possibile unire i dati XML con una struttura del modulo e generare il modulo come flusso di stampa. Ad esempio, è possibile creare un flusso di stampa PostScript e inviarlo a una stampante di rete. Nell&#39;illustrazione seguente viene illustrato l&#39;invio di flussi di stampa da parte del servizio Output a stampanti di rete.

>[!NOTE]
>
>Per dimostrare come inviare un flusso di stampa a una stampante di rete, questa sezione invia un flusso di stampa PostScript a una stampante di rete utilizzando il protocollo della stampante SharedPrinter.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Output, vedi [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-6}

Per inviare un flusso di stampa a una stampante di rete, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Creare un oggetto Client di output.
1. Fare riferimento a un&#39;origine dati XML.
1. Impostare le opzioni di esecuzione della stampa
1. Recupera un documento da stampare.
1. Inviare il documento a una stampante di rete.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso della classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar (obbligatorio se AEM Forms è distribuito su JBoss)
* jbossall-client.jar (obbligatorio se AEM Forms è distribuito su JBoss)

se AEM Forms è distribuito su un server applicazioni J2EE supportato che non è JBoss, sarà necessario sostituire i file adobe-utilities.jar e jbossall-client.jar con file JAR specifici per il server applicazioni J2EE in cui viene distribuito AEM Forms.

**Creare un oggetto Client di output**

Prima di eseguire un&#39;operazione del servizio Output a livello di programmazione, creare un oggetto client del servizio Output. Se utilizzi l’API Java, crea un `OutputClient` oggetto. Se utilizzi l’API del servizio Web Output, crea un `OutputServiceClient` oggetto.

**Riferimento a un’origine dati XML**

Per stampare un documento contenente dati, è necessario fare riferimento a un&#39;origine dati XML contenente elementi XML per ogni campo del modulo che si desidera compilare con i dati. Il nome dell&#39;elemento XML deve corrispondere al nome del campo. Un elemento XML viene ignorato se non corrisponde a un campo modulo o se il nome dell’elemento XML non corrisponde al nome del campo. Se vengono specificati tutti gli elementi XML, non è necessario stabilire una corrispondenza con l’ordine in cui vengono visualizzati gli elementi XML.

**Impostare le opzioni di esecuzione della stampa**

È possibile impostare le opzioni di esecuzione durante l&#39;invio di un flusso di stampa a una stampante, incluse le seguenti opzioni:

* **Copie**: Specifica il numero di copie da inviare alla stampante. Il valore predefinito è 1.
* **graffetta**: Quando si utilizza un ripiano, viene impostata un&#39;opzione XCI. Questa opzione può essere specificata nel modello di configurazione dall&#39;elemento di base e viene utilizzata solo per stampanti PS e PCL.
* **OutputJog**: L&#39;opzione XCI viene impostata quando le pagine di output devono essere sottoposte a jogging (fisicamente spostate nella barra di uscita). Questa opzione è disponibile solo per stampanti PS e PCL.
* **OutputBin**: Valore XCI utilizzato per consentire al driver di stampa di selezionare il bin di output appropriato.

>[!NOTE]
>
>Per informazioni su tutte le opzioni di esecuzione che è possibile impostare, vedere la `PrintedOutputOptionsSpec` riferimento della classe.

**Recupera un documento da stampare**

Recupera un flusso di stampa da inviare a una stampante. Ad esempio, è possibile recuperare un file PostScript e inviarlo a una stampante.

Se la stampante supporta PDF, è possibile scegliere di inviare un file PDF. Tuttavia, un problema relativo all&#39;invio di un documento PDF a una stampante è rappresentato dal fatto che ogni produttore della stampante ha implementato in modo diverso l&#39;interprete PDF. Alcuni produttori di stampa utilizzano l&#39;interpretazione Adobe PDF, ma dipende dalla stampante. Altre stampanti hanno un proprio interprete PDF. Di conseguenza, i risultati della stampa possono variare.

Un&#39;altra limitazione dell&#39;invio di un documento PDF a una stampante è la stampa; non può accedere a duplex, selezione del vassoio della carta e cucitura, ad eccezione delle impostazioni sulla stampante.

Per recuperare un documento da stampare, utilizzare la `generatePrintedOutput` metodo . La tabella seguente specifica i tipi di contenuto impostati per un dato flusso di stampa quando si utilizza il `generatePrintedOutput` metodo .

<table>
 <thead>
  <tr>
   <th><p>Formato di stampa </p></th>
   <th><p>Descrizione</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>DPL </p></td>
   <td><p>Crea un flusso di output xdc dpl203.xdc predefinito o personalizzato.</p></td>
  </tr>
  <tr>
   <td><p>DPL 300 DPI </p></td>
   <td><p>Crea un flusso di output DPL 300 DPI.</p></td>
  </tr>
  <tr>
   <td><p>DPL 406 DPI </p></td>
   <td><p>Crea un flusso di uscita DPL 400 DPI.</p></td>
  </tr>
  <tr>
   <td><p>DPL 600 DPI </p></td>
   <td><p>Crea un flusso di output DPL 600 DPI.</p></td>
  </tr>
  <tr>
   <td><p>GenericColorPCL </p></td>
   <td><p>Crea un flusso di output generico di colore PCL (5c).</p></td>
  </tr>
  <tr>
   <td><p>GenericPSLevel3 </p></td>
   <td><p>Crea un flusso di output generico PostScript di livello 3.</p></td>
  </tr>
  <tr>
   <td><p>IPL </p></td>
   <td><p>Crea un flusso di output IPL personalizzato.</p></td>
  </tr>
  <tr>
   <td><p>IPL 300 DPI </p></td>
   <td><p>Crea un flusso di uscita IPL 300 DPI.</p></td>
  </tr>
  <tr>
   <td><p>IPL 400 DPI </p></td>
   <td><p>Crea un flusso di uscita IPL 400 DPI.</p></td>
  </tr>
  <tr>
   <td><p>PCL </p></td>
   <td><p>Crea un flusso di output generico PCL monocromatico (5e).</p></td>
  </tr>
  <tr>
   <td><p>PostScript </p></td>
   <td><p>Crea un flusso di output generico di livello 2 di PostScript.</p></td>
  </tr>
  <tr>
   <td><p>TPCL </p></td>
   <td><p>Crea un flusso di output TPCL personalizzato.</p></td>
  </tr>
  <tr>
   <td><p>TPCL 305 DPI </p></td>
   <td><p>Crea un flusso di output TPCL 305 DPI.</p></td>
  </tr>
  <tr>
   <td><p>TPCL 600 DPI </p></td>
   <td><p>Crea un flusso di output TPCL 600 DPI.</p></td>
  </tr>
  <tr>
   <td><p>ZPL </p></td>
   <td><p>Crea un flusso di output ZPL 203 DPI.</p></td>
  </tr>
  <tr>
   <td><p>ZPL 300 DPI </p></td>
   <td><p>Crea un flusso di output ZPL 300 DPI.</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>È inoltre possibile inviare un flusso di stampa a una stampante utilizzando `generatePrintedOutput2` metodo . Tuttavia, gli avvii rapidi associati alla sezione Invio di flussi di stampa a stampanti utilizzano la `generatePrintedOutput` metodo .

**Inviare il flusso di stampa a una stampante di rete**

Dopo aver recuperato un documento da stampare, è possibile richiamare il servizio Output, che lo fa inviare un flusso di stampa a una stampante di rete. Affinché il servizio Output possa individuare correttamente la stampante, è necessario specificare sia il server di stampa che il nome della stampante. Inoltre, è necessario specificare anche il protocollo di stampa.

>[!NOTE]
>
>Se sul server dei moduli è installato PDFG e il server viene eseguito su Windows Server 2008, non è possibile utilizzare la proprietà SharedPrinter. In questa situazione, utilizzare un protocollo di stampa diverso.

>[!NOTE]
>
>Se si utilizza una stampante di rete e il meccanismo di accesso è SharedPrinter, è necessario specificare il percorso di rete completo della stampante.Inviare un flusso di stampa a una stampante di rete utilizzando l&#39;API Java

Inviare un flusso di stampa a una stampante di rete utilizzando l&#39;API di output (Java):

1. Includi file di progetto.

   Includi file JAR client, come adobe-output-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto Client di output

   * Crea un `ServiceClientFactory` oggetto contenente le proprietà di connessione.
   * Crea un `OutputClient` utilizzando il relativo costruttore e passando `ServiceClientFactory` oggetto.

1. Riferimento a un’origine dati XML

   * Crea un `java.io.FileInputStream` oggetto che rappresenta l&#39;origine dati XML utilizzata per compilare il documento utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del file XML.
   * Crea un `com.adobe.idp.Document` utilizzando il relativo costruttore e passando `java.io.FileInputStream` oggetto.

1. Impostare le opzioni di esecuzione della stampa

   Crea un `PrintedOutputOptionsSpec` oggetto che rappresenta le opzioni di esecuzione della stampa. Ad esempio, è possibile specificare il numero di copie da stampare richiamando il `PrintedOutputOptionsSpec` dell’oggetto `setCopies` metodo .

   >[!NOTE]
   >
   >Non è possibile impostare il valore di impaginazione utilizzando la variabile `PrintedOutputOptionsSpec` dell’oggetto `setPagination` se si sta generando un flusso di stampa ZPL. Allo stesso modo, non è possibile impostare le seguenti opzioni per un flusso di stampa ZPL: OutputJog, PageOffset e Staple. La `setPagination` metodo non valido per la generazione PostScript. È valido solo per la generazione PCL.

1. Recupera un documento da stampare

   * Recupera un documento da stampare richiamando il `OutputClient` dell’oggetto `generatePrintedOutput` e passando i seguenti valori:

      * A `PrintFormat` valore di enumerazione che specifica il flusso di stampa. Ad esempio, per creare un flusso di stampa PostScript, passare `PrintFormat.PostScript`.
      * Valore stringa che specifica il nome della struttura del modulo.
      * Valore stringa che specifica la posizione dei relativi file collaterali, ad esempio i file di immagine.
      * Valore stringa che specifica la posizione del file XDC da utilizzare.
      * La `PrintedOutputOptionsSpec` oggetto contenente le opzioni di esecuzione necessarie per la stampa in un file.
      * La `com.adobe.idp.Document` oggetto che rappresenta l’origine dati XML contenente i dati del modulo da unire alla struttura del modulo.

      Questo metodo restituisce un `OutputResult` oggetto contenente i risultati dell&#39;operazione.

   * Crea un `com.adobe.idp.Document` oggetto da inviare alla stampante richiamando il `OutputResult` oggetto ‘s `getGeneratedDoc` metodo . Questo metodo restituisce un `com.adobe.idp.Document` oggetto.


1. Inviare il flusso di stampa a una stampante di rete

   Inviare il flusso di stampa a una stampante di rete richiamando il `OutputClient` dell’oggetto `sendToPrinter` e passando i seguenti valori:

   * A `com.adobe.idp.Document` oggetto che rappresenta il flusso di stampa da inviare alla stampante.
   * A `PrinterProtocol` valore di enumerazione che specifica il protocollo della stampante da utilizzare. Ad esempio, per specificare il protocollo SharedPrinter, passare `PrinterProtocol.SharedPrinter`.
   * Valore stringa che specifica il nome del server di stampa. Ad esempio, supponendo che il nome del server di stampa sia PrintServer1, passare `\\\PrintSever1`.
   * Valore stringa che specifica il nome della stampante. Ad esempio, supponendo che il nome della stampante sia Printer1, passare `\\\PrintSever1\Printer1`.

   >[!NOTE]
   >
   >La `sendToPrinter` è stato aggiunto all’API AEM Forms nella versione 8.2.1.

### Inviare un flusso di stampa a una stampante utilizzando l’API del servizio Web {#send-a-print-stream-to-a-printer-using-the-web-service-api}

Inviare un flusso di stampa a una stampante di rete utilizzando l&#39;API di output (servizio Web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurati di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l’indirizzo IP del server che ospita AEM Forms.

1. Creare un oggetto Client di output.

   * Crea un `OutputServiceClient` utilizzando il relativo costruttore predefinito.
   * Crea un `OutputServiceClient.Endpoint.Address` utilizzando `System.ServiceModel.EndpointAddress` costruttore. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/OutputService?blob=mtom`.) Non è necessario utilizzare il `lc_version` attributo. Questo attributo viene utilizzato quando si crea un riferimento a un servizio. Tuttavia, specifica `?blob=mtom` per utilizzare MTOM.
   * Crea un `System.ServiceModel.BasicHttpBinding` ottenendo il valore del `OutputServiceClient.Endpoint.Binding` campo . Imposta il valore restituito su `BasicHttpBinding`.
   * Imposta la `System.ServiceModel.BasicHttpBinding` dell’oggetto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegnare il nome utente del modulo di AEM al campo `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore della password corrispondente al campo `OutputServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Fare riferimento a un&#39;origine dati XML.

   * Crea un `BLOB` utilizzando il relativo costruttore. La `BLOB` viene utilizzato per memorizzare i dati del modulo.
   * Crea un `System.IO.FileStream` richiamando il relativo costruttore. Passare un valore di stringa che specifica la posizione del file XML contenente i dati del modulo.
   * Creare un array di byte che memorizza il contenuto del `System.IO.FileStream` oggetto. Determina la lunghezza della matrice dei byte ottenendo il `System.IO.FileStream` dell’oggetto `Length` proprietà.
   * Compilare l&#39;array di byte con i dati del flusso richiamando il `System.IO.FileStream` dell’oggetto `Read` e passare l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare `BLOB` oggetto assegnando il relativo `MTOM` con il contenuto dell&#39;array di byte.

1. Impostare le opzioni di esecuzione della stampa.

   Crea un `PrintedOutputOptionsSpec` utilizzando il relativo costruttore. Ad esempio, è possibile specificare il numero di copie da stampare assegnando un valore intero che rappresenta il numero di copie da stampare `PrintedOutputOptionsSpec` dell’oggetto `copies` membro dati.

   >[!NOTE]
   >
   >Non è possibile impostare il valore di impaginazione utilizzando la variabile `PrintedOutputOptionsSpec` dell’oggetto `pagination` membro dati se si sta generando un flusso di stampa ZPL. Allo stesso modo, non è possibile impostare le seguenti opzioni per un flusso di stampa ZPL: OutputJog, PageOffset e Staple. La `pagination` membro dati non valido per la generazione PostScript. È valido solo per la generazione PCL.

1. Recupera un documento da stampare.

   * Recupera un documento da stampare richiamando il `OutputServiceService` dell’oggetto `generatePrintedOutput` e passando i seguenti valori:

      * A `PrintFormat` valore di enumerazione che specifica il flusso di stampa. Ad esempio, per creare un flusso di stampa PostScript, passare `PrintFormat.PostScript`.
      * Valore stringa che specifica il nome della struttura del modulo.
      * Valore stringa che specifica la posizione dei relativi file collaterali, ad esempio i file di immagine.
      * Valore stringa che specifica la posizione del file XDC da utilizzare.
      * La `PrintedOutputOptionsSpec` oggetto contenente le opzioni di esecuzione della stampa utilizzate per l&#39;invio di un flusso di stampa a una stampante di rete.
      * La `BLOB` oggetto contenente l&#39;origine dati XML contenente i dati del modulo.
      * A `BLOB` oggetto popolato da `generatePrintedOutput` metodo . La `generatePrintedOutput` popola l&#39;oggetto con i metadati generati che descrivono il documento. Questo valore di parametro è necessario solo per la chiamata al servizio Web.
      * A `BLOB` oggetto popolato da `generatePrintedOutput` metodo . La `generatePrintedOutput` popola l&#39;oggetto con i dati dei risultati. Questo valore di parametro è necessario solo per la chiamata al servizio Web.
      * Un `OutputResult` oggetto contenente i risultati dell&#39;operazione. Questo valore di parametro è necessario solo per la chiamata al servizio Web.
   * Crea un `BLOB` oggetto da inviare alla stampante ottenendo il valore del `OutputResult` oggetto ‘s `generatedDoc` metodo . Questo metodo restituisce un `BLOB` oggetto contenente i dati PostScript restituiti da `generatePrintedOutput` metodo .


1. Inviare il flusso di stampa a una stampante di rete.

   Inviare il flusso di stampa a una stampante di rete richiamando il `OutputClient` dell’oggetto `sendToPrinter` e passando i seguenti valori:

   * A `BLOB` oggetto che rappresenta il flusso di stampa da inviare alla stampante.
   * A `PrinterProtocol` valore di enumerazione che specifica il protocollo della stampante da utilizzare. Ad esempio, per specificare il protocollo SharedPrinter, passare `PrinterProtocol.SharedPrinter`.
   * A `bool` che specifica se utilizzare il valore del parametro precedente. Passa il valore `true`. Questo valore di parametro è necessario solo per la chiamata al servizio Web.
   * Valore stringa che specifica il nome del server di stampa. Ad esempio, supponendo che il nome del server di stampa sia PrintServer1, passare `\\\PrintSever1`.
   * Valore stringa che specifica il nome della stampante. Ad esempio, supponendo che il nome della stampante sia Printer1, passare `\\\PrintSever1\Printer1`.

   >[!NOTE]
   >
   >La `sendToPrinter` è stato aggiunto all’API AEM Forms nella versione 8.2.1.

## Creazione di più file di output {#creating-multiple-output-files}

Il servizio Output può creare documenti separati per ogni record all&#39;interno di un&#39;origine dati XML o di un singolo file contenente tutti i record (questa funzionalità è l&#39;impostazione predefinita). Ad esempio, si supponga che dieci record si trovino all&#39;interno di un&#39;origine dati XML e si istruisce il servizio Output di creare documenti PDF separati (o altri tipi di output) per ciascun record utilizzando l&#39;API del servizio di output. Di conseguenza, il servizio Output genera dieci documenti PDF. Invece di creare documenti, è possibile inviare più flussi di stampa a una stampante.

L&#39;illustrazione seguente mostra anche il servizio Output che elabora un file di dati XML contenente più record. Tuttavia, si supponga di istruire il servizio Output per creare un singolo documento PDF contenente tutti i record di dati. In questa situazione, il servizio Output genera un documento contenente tutti i record.

Nell&#39;illustrazione seguente viene illustrato il servizio Output che elabora un file di dati XML contenente più record. Si supponga di istruire il servizio Output per creare un documento PDF separato per ogni record di dati. In questa situazione, il servizio Output genera un documento PDF separato per ogni record di dati.

![cm_outputbatchmany](assets/cm_outputbatchmany.png)

I seguenti dati XML mostrano un esempio di file di dati che contiene tre record di dati.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <batch>
 <LoanRecord>
     <mortgageAmount>500000</mortgageAmount>
     <lastName>Blue</lastName>
     <firstName>Tony</firstName>
     <SSN>555666777</SSN>
     <PositionTitle>Product Manager</PositionTitle>
     <Address>555 No Where Dr</Address>
     <City>New York</City>
     <StateProv>New York</StateProv>
     <ZipCode>51256</ZipCode>
     <Email>TBlue@NoMailServer.com</Email>
     <PhoneNum>555-7418</PhoneNum>
     <FaxNum>555-9981</FaxNum>
     <Description>Buy a home</Description>
 </LoanRecord>
 <LoanRecord>
     <mortgageAmount>300000</mortgageAmount>
     <lastName>White</lastName>
     <firstName>Sam</firstName>
     <SSN>555666222</SSN>
     <PositionTitle>Program Manager</PositionTitle>
     <Address>557 No Where Dr</Address>
     <City>New York</City>
     <StateProv>New York</StateProv>
     <ZipCode>51256</ZipCode>
     <Email>SWhite@NoMailServer.com</Email>
     <PhoneNum>555-7445</PhoneNum>
     <FaxNum>555-9986</FaxNum>
     <Description>Buy a home</Description>
 </LoanRecord>
 <LoanRecord>
     <mortgageAmount>700000</mortgageAmount>
     <lastName>Green</lastName>
     <firstName>Steve</firstName>
     <SSN>55566688</SSN>
     <PositionTitle>Project Manager</PositionTitle>
     <Address>445 No Where Dr</Address>
     <City>New York</City>
     <StateProv>New York</StateProv>
     <ZipCode>51256</ZipCode>
     <Email>SGreeb@NoMailServer.com</Email>
     <PhoneNum>555-2211</PhoneNum>
     <FaxNum>555-2221</FaxNum>
     <Description>Buy a home</Description>
 </LoanRecord>
 </batch>
```

L’elemento XML che avvia e termina ogni record di dati è `LoanRecord`. A questo elemento XML viene fatto riferimento dalla logica dell&#39;applicazione che genera più file.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Output, vedi [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-7}

Per creare più file PDF basati su un’origine dati XML, effettua le seguenti operazioni:

1. Includi file di progetto.
1. Creare un oggetto Client di output.
1. Fare riferimento a un&#39;origine dati XML.
1. Impostare le opzioni di runtime di PDF.
1. Imposta le opzioni di esecuzione del rendering.
1. Generare più file PDF.
1. Recupera i risultati dell’operazione.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso della classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è distribuito su JBoss)
* jbossall-client.jar (richiesto se AEM Forms è distribuito su JBoss)

se AEM Forms è distribuito su un server applicazioni J2EE supportato che non è JBoss, sarà necessario sostituire i file adobe-utilities.jar e jbossall-client.jar con file JAR specifici per il server applicazioni J2EE in cui viene distribuito AEM Forms.

**Creare un oggetto Client di output**

Prima di poter eseguire un&#39;operazione del servizio Output a livello di programmazione, è necessario creare un oggetto client del servizio Output. Se utilizzi l’API Java, crea un `OutputClient` oggetto. Se utilizzi l’API del servizio Web Output, crea un `OutputServiceService` oggetto.

**Riferimento a un’origine dati XML**

Fare riferimento a un&#39;origine dati XML contenente più record. Per separare i record di dati è necessario utilizzare un elemento XML. Ad esempio, nell’origine dati XML di esempio mostrata in precedenza in questa sezione, l’elemento XML che separa i record di dati viene denominato `LoanRecord`.

Per ogni campo del modulo che si desidera compilare con i dati deve esistere un elemento XML. Il nome dell&#39;elemento XML deve corrispondere al nome del campo. Un elemento XML viene ignorato se non corrisponde a un campo modulo o se il nome dell’elemento XML non corrisponde al nome del campo. Se vengono specificati tutti gli elementi XML, non è necessario stabilire una corrispondenza con l’ordine in cui vengono visualizzati gli elementi XML.

**Impostare le opzioni di runtime di PDF**

Per creare correttamente più file in base a un&#39;origine dati XML, è necessario impostare le seguenti opzioni di esecuzione per il servizio Output:

* **Molti file**: Specifica se il servizio Output crea uno o più documenti. È possibile specificare true o false. Per creare un documento separato per ogni record di dati nell&#39;origine dati XML, specificare true.
* **URI file**: Specifica la posizione dei file generati dal servizio Output. Ad esempio, si supponga di specificare C:\\Adobe\forms\Loan.pdf. In questa situazione, il servizio Output crea un file denominato Loan.pdf e inserisce il file nella cartella C:\\Adobe\forms folder. In presenza di più file, i nomi dei file sono Loan0001.pdf, Loan002.pdf, Loan0003.pdf e così via. Se si specifica un percorso di file, i file vengono inseriti sul server, non sul computer client.
* **Nome record**: Specifica il nome dell&#39;elemento XML nell&#39;origine dati che separa i record di dati. Ad esempio, nell’origine dati XML di esempio mostrata in precedenza in questa sezione, viene chiamato l’elemento XML che separa i record di dati `LoanRecord`. Anziché impostare l’opzione di esecuzione Nome record, è possibile impostare il livello di record assegnandogli un valore numerico che indica il livello di elemento contenente i record di dati. Tuttavia, è possibile impostare solo il Nome record o il Livello record. Non è possibile impostare entrambi i valori.)

**Impostare le opzioni di esecuzione del rendering**

È possibile impostare le opzioni di esecuzione del rendering durante la creazione di più file. Sebbene queste opzioni non siano necessarie (a differenza delle opzioni di esecuzione dell&#39;output, che sono necessarie), è possibile eseguire attività quali il miglioramento delle prestazioni del servizio Output. Ad esempio, è possibile memorizzare nella cache la struttura del modulo utilizzata dal servizio Output per migliorare le prestazioni.

Quando il servizio Output elabora i record batch, legge i dati che contengono più record in modo incrementale. In altre parole, il servizio Output legge i dati in memoria e rilascia i dati durante l&#39;elaborazione del batch di record. Il servizio Output carica i dati in modo incrementale quando è impostata una delle due opzioni di runtime. Se si imposta l&#39;opzione di esecuzione Nome record, il servizio Output legge i dati in modo incrementale. Allo stesso modo, se si imposta l&#39;opzione di esecuzione a livello di record su 2 o superiore, il servizio di output legge i dati in modo incrementale.

È possibile controllare se il servizio di output esegue il caricamento incrementale utilizzando il `PDFOutputOptionsSpec` o `PrintedOutputOptionSpec` dell’oggetto `setLazyLoading` metodo . Puoi trasmettere il valore `false` a questo metodo che disattiva il caricamento incrementale.

**Generare più file PDF**

Dopo aver fatto riferimento a un&#39;origine dati XML valida contenente più record di dati e aver impostato le opzioni di esecuzione, è possibile richiamare il servizio Output, che ne determina la generazione di più file. Quando si generano più record, il `OutputResult` dell’oggetto `getGeneratedDoc` restituisce il metodo `null`.

**Recupera i risultati dell&#39;operazione**

Dopo aver eseguito un&#39;operazione, il servizio Output restituisce dati XML che specificano se l&#39;operazione è riuscita. Il seguente XML viene restituito dal servizio Output. In questa situazione, il servizio di output ha generato 42 documenti.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <printResult>
 <status>0</status>
 <requestId>4ad85f9e2</requestId>
 <context/>
 <messages>
 <message>Printed all 42 records successfully.</message>
 </messages>
 <printSpec>
 <input>
 <validated>true</validated>
 <dataFile recordIdField="" recordLevel="0" recordName="LoanRecord"/>
 <sniffRules lookAhead="300"/>
 <formDesign>Loan.xdp</formDesign>
 <contentRoot>C:\Adobe</contentRoot>
 <metadata-spec record="false"/>
 </input>
 <output>
 <format>PDF</format>
 <fileURI>C:\Adobe\forms\Loan.pdf</fileURI>
 <optionString>cacheenabled=true&padebug=false&linearpdf=false&pdfarevisionnumber=1&pdfaconformance=A&taggedpdf=false&TransactionTimeOut=180</optionString>
 <waitForResponse>true</waitForResponse>
 <outputStream>multiple</outputStream>
 </output>
 </printSpec>
 </printResult>
```

**Consulta anche**

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API del servizio di output](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Creare più file PDF utilizzando l’API Java {#create-multiple-pdf-files-using-the-java-api}

Creare più file PDF utilizzando l’API di output (Java):

1. Includi file di progetto&quot;

   Includi file JAR client, come adobe-output-client.jar, nel percorso di classe del progetto Java. .

1. Creare un oggetto Client di output

   * Crea un `ServiceClientFactory` oggetto contenente le proprietà di connessione.
   * Crea un `OutputClient` utilizzando il relativo costruttore e passando `ServiceClientFactory` oggetto.

1. Riferimento a un’origine dati XML

   * Crea un `java.io.FileInputStream` oggetto che rappresenta l&#39;origine dati XML contenente più record utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del file XML.
   * Crea un `com.adobe.idp.Document` utilizzando il relativo costruttore e passando `java.io.FileInputStream` oggetto.

1. Impostare le opzioni di runtime di PDF

   * Crea un `PDFOutputOptionsSpec` utilizzando il relativo costruttore.
   * Imposta l&#39;opzione Molti file richiamando il `PDFOutputOptionsSpec` dell’oggetto `setGenerateManyFiles` metodo . Ad esempio, passa il valore `true` istruzioni al servizio Output di creare un file PDF separato per ogni record nell&#39;origine dati XML. (Se passi `false`, il servizio Output genera un singolo documento PDF contenente tutti i record.
   * Imposta l&#39;opzione URI file richiamando il `PDFOutputOptionsSpec` dell’oggetto `setFileUri` e passare un valore stringa che specifica la posizione dei file generati dal servizio Output. L’opzione URI file è relativa al server applicazioni J2EE che ospita AEM Forms, non al computer client.
   * Imposta l’opzione Nome record richiamando la `OutputOptionsSpec` dell’oggetto `setRecordName` e passare un valore stringa che specifica il nome dell&#39;elemento XML nell&#39;origine dati che separa i record di dati. Ad esempio, considerare l&#39;origine dati XML mostrata in precedenza in questa sezione. Il nome dell&#39;elemento XML che separa i record di dati è LoanRecord).

1. Impostare le opzioni di esecuzione del rendering

   * Crea un `RenderOptionsSpec` utilizzando il relativo costruttore.
   * Memorizza in cache la struttura del modulo per migliorare le prestazioni del servizio Output richiamando il `RenderOptionsSpec` dell’oggetto `setCacheEnabled` e passando un `Boolean` valore `true`.

1. Generare più file PDF

   Generare più file PDF richiamando il `OutputClient` dell’oggetto `generatePDFOutput` e passando i seguenti valori:

   * A `TransformationFormat` valore enum. Per generare un documento PDF, specificare `TransformationFormat.PDF`.
   * Valore stringa che specifica il nome della struttura del modulo.
   * Valore stringa che specifica la directory principale del contenuto in cui si trova la struttura del modulo.
   * A `PDFOutputOptionsSpec` oggetto contenente le opzioni di runtime di PDF.
   * A `RenderOptionsSpec` oggetto contenente le opzioni di esecuzione del rendering.
   * La `com.adobe.idp.Document` oggetto contenente l’origine dati XML contenente i dati da unire alla struttura del modulo.

   La `generatePDFOutput` restituisce un `OutputResult` oggetto contenente i risultati dell&#39;operazione.

1. Recupera i risultati dell&#39;operazione

   * Crea un `java.io.File` oggetto che rappresenta un file XML che conterrà i risultati del `generatePDFOutput` metodo . Assicurati che l&#39;estensione del nome file sia .xml.
   * Richiama il `com.adobe.idp.Document` dell’oggetto `copyToFile` per copiare il contenuto del `com.adobe.idp.Document` al file (assicurati di utilizzare `com.adobe.idp.Document` oggetto restituito da `applyUsageRights` metodo).

**Consulta anche**

[Riepilogo dei passaggi](creating-document-output-streams.md#summary-of-steps)

[Avvio rapido (modalità EJB): Creazione di più file PDF tramite l’API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-multiple-pdf-files-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Creare più file PDF utilizzando l’API del servizio Web {#create-multiple-pdf-files-using-the-web-service-api}

Creare più file PDF utilizzando l’API di output (servizio Web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurati di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l’indirizzo IP del server che ospita AEM Forms.

1. Creare un oggetto Client di output.

   * Crea un `OutputServiceClient` utilizzando il relativo costruttore predefinito.
   * Crea un `OutputServiceClient.Endpoint.Address` utilizzando `System.ServiceModel.EndpointAddress` costruttore. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/OutputService?blob=mtom`.) Non è necessario utilizzare il `lc_version` attributo. Questo attributo viene utilizzato quando si crea un riferimento a un servizio. Tuttavia, specifica `?blob=mtom` per utilizzare MTOM.
   * Crea un `System.ServiceModel.BasicHttpBinding` ottenendo il valore del `OutputServiceClient.Endpoint.Binding` campo . Imposta il valore restituito su `BasicHttpBinding`.
   * Imposta la `System.ServiceModel.BasicHttpBinding` dell’oggetto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegnare il nome utente del modulo di AEM al campo `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore della password corrispondente al campo `OutputServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Fare riferimento a un&#39;origine dati XML.

   * Crea un `BLOB` utilizzando il relativo costruttore. La `BLOB` viene utilizzato per memorizzare i dati del modulo contenenti più record.
   * Crea un `System.IO.FileStream` richiamando il relativo costruttore. Passare un valore di stringa che rappresenta la posizione del file XML contenente più record.
   * Creare un array di byte che memorizza il contenuto del `System.IO.FileStream` oggetto. È possibile determinare le dimensioni dell&#39;array di byte ottenendo il `System.IO.FileStream` dell’oggetto `Length` proprietà.
   * Compilare l&#39;array di byte con i dati del flusso richiamando il `System.IO.FileStream` dell’oggetto `Read` e passare l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare `BLOB` oggetto assegnando il relativo `MTOM` con il contenuto dell&#39;array di byte.

1. Impostare le opzioni di runtime di PDF.

   * Crea un `PDFOutputOptionsSpec` utilizzando il relativo costruttore.
   * Imposta l’opzione Molti file assegnando un valore booleano al `OutputOptionsSpec` dell’oggetto `generateManyFiles` membro dati. Ad esempio, assegna il valore `true` a questo membro dati per istruire il servizio Output di creare un file PDF separato per ogni record nell&#39;origine dati XML. (Se si assegna `false` a questo membro dati, il servizio Output genera un singolo PDF che contiene tutti i record.
   * Impostare l&#39;opzione URI del file assegnando un valore stringa che specifica la posizione dei file generati dal servizio Output nel `OutputOptionsSpec` dell’oggetto `fileURI` membro dati. L’opzione URI file è relativa al server applicazioni J2EE che ospita AEM Forms, non al computer client.
   * Impostare l&#39;opzione nome record assegnando un valore stringa che specifica il nome dell&#39;elemento XML nell&#39;origine dati che separa i record di dati dalla `OutputOptionsSpec` dell’oggetto `recordName` membro dati.
   * Impostare l&#39;opzione copie assegnando un valore intero che specifica il numero di copie generate dal servizio Output al `OutputOptionsSpec` dell’oggetto `copies` membro dati.

1. Imposta le opzioni di esecuzione del rendering.

   * Crea un `RenderOptionsSpec` utilizzando il relativo costruttore.
   * Memorizza in cache la struttura del modulo per migliorare le prestazioni del servizio Output assegnando il valore `true` al `RenderOptionsSpec` dell’oggetto `cacheEnabled` membro dati.

1. Generare più file PDF.

   Creazione di più file PDF richiamando il `OutputServiceService` dell’oggetto `generatePDFOutput`e passando i seguenti valori:

   * Valore enum di TransformationFormat. Per generare un documento PDF, specificare `TransformationFormat.PDF`.
   * Valore stringa che specifica il nome della struttura del modulo.
   * Valore stringa che specifica la directory principale del contenuto in cui si trova la struttura del modulo.
   * A `PDFOutputOptionsSpec` oggetto contenente le opzioni di runtime di PDF.
   * A `RenderOptionsSpec` oggetto contenente le opzioni di esecuzione del rendering.
   * La `BLOB` oggetto contenente l’origine dati XML contenente i dati da unire alla struttura del modulo.
   * A `BLOB` oggetto popolato da `generatePDFOutput` metodo . La `generatePDFOutput` popola l&#39;oggetto con i metadati generati che descrivono il documento.
   * A `BLOB` oggetto popolato da `generatePDFOutput` metodo . La `generatePDFOutput` popola l&#39;oggetto con i dati dei risultati.
   * Un `OutputResult` oggetto contenente i risultati dell&#39;operazione.

1. Recupera i risultati dell&#39;operazione

   * Crea un `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta una posizione di file XML contenente i dati dei risultati. Assicurati che l&#39;estensione del nome file sia .xml.
   * Creare un array di byte che memorizza il contenuto dei dati del `BLOB` oggetto popolato con i dati dei risultati da `OutputServiceService` dell’oggetto `generatePDFOutput` (l&#39;ottavo parametro). Compilare l’array di byte ottenendo il valore del `BLOB` dell’oggetto `binaryData` membro dati.
   * Crea un `System.IO.BinaryWriter` richiamando il relativo costruttore e passando `System.IO.FileStream` oggetto.
   * Scrivere il contenuto dell&#39;array di byte nel file XML richiamando il `System.IO.BinaryWriter` dell’oggetto `Write` e passare l&#39;array di byte.

**Consulta anche**

[Riepilogo dei passaggi](creating-document-output-streams.md#summary-of-steps)

[Richiamo di AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamo di AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Creazione di regole di ricerca {#creating-search-rules}

È possibile creare regole di ricerca che consentono al servizio Output di esaminare i dati di input e utilizzare strutture del modulo diverse in base al contenuto dei dati per generare l’output. Ad esempio, se il testo *mutuo* si trova all&#39;interno dei dati di input, quindi il servizio Output può utilizzare una struttura del modulo denominata Mortgage.xdp. Analogamente, se il testo *automobile* si trova nei dati di input, quindi il servizio Output può utilizzare una struttura del modulo salvata come AutomobileLoan.xdp. Sebbene il servizio Output possa generare diversi tipi di output, questa sezione presuppone che il servizio Output generi un file PDF. Il diagramma seguente mostra il servizio Output che genera un file PDF elaborando un file di dati XML e utilizzando una delle numerose strutture del modulo.

Inoltre, il servizio Output è in grado di generare pacchetti di documenti, in cui vengono forniti più record nel set di dati e ogni record viene associato a una struttura del modulo e viene generato un singolo documento composto da più strutture del modulo.

![cs_outputbatchmanyformdesigns2](assets/cs_outputbatchmanyformdesigns2.png)

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Output, vedi [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-8}

Per indicare al servizio di output di utilizzare le regole di ricerca durante la generazione di un documento, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Creare un oggetto Client di output.
1. Fare riferimento a un&#39;origine dati XML.
1. Definisci le regole di ricerca.
1. Impostare le opzioni di runtime di PDF.
1. Imposta le opzioni di esecuzione del rendering.
1. Genera un documento PDF.
1. Recupera i risultati dell’operazione.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar (obbligatorio se AEM Forms è distribuito su JBoss)
* jbossall-client.jar (obbligatorio se AEM Forms è distribuito su JBoss)

se AEM Forms è implementato su un server applicazioni J2EE supportato che non è JBoss, sarà necessario sostituire adobe-utilities.jar e jbossall-client.jar con file JAR specifici per il server applicazioni J2EE in cui viene distribuito AEM Forms.

**Creare un oggetto Client di output**

Prima di poter eseguire un&#39;operazione del servizio Output a livello di programmazione, è necessario creare un oggetto client del servizio Output.

**Riferimento a un’origine dati XML**

Per ogni campo del modulo che si desidera compilare con i dati deve esistere un elemento XML. Il nome dell&#39;elemento XML deve corrispondere al nome del campo. Un elemento XML viene ignorato se non corrisponde a un campo modulo o se il nome dell’elemento XML non corrisponde al nome del campo. Non è necessario stabilire una corrispondenza con l&#39;ordine di visualizzazione degli elementi XML, purché siano specificati tutti gli elementi XML.

**Definire le regole di ricerca**

Per definire le regole di ricerca, è necessario definire uno o più pattern di testo ricercati dai servizi di output nei dati di input. Per ogni pattern di testo definito, specificare una struttura del modulo corrispondente da utilizzare se il pattern di testo è posizionato. Se si trova un pattern di testo, il servizio Output utilizza la struttura del modulo corrispondente per generare l’output. Un esempio di pattern di testo è *mutuo*.

>[!NOTE]
>
>Se i pattern di testo non si trovano, viene utilizzato il modulo predefinito. Assicurarsi che tutte le strutture del modulo utilizzate si trovino nella directory principale del contenuto.

**Impostare le opzioni di runtime di PDF**

Impostare le seguenti opzioni di esecuzione di PDF affinché il servizio Output possa creare correttamente un documento PDF basato su più strutture del modulo:

* **URI file**: Specifica il nome e la posizione del file PDF generato dal servizio Output.
* **Regole**: Specifica le regole definite.
* **LookAHead**: Specifica il numero di byte da utilizzare dall&#39;inizio del file di dati di input per la ricerca dei pattern di testo definiti. Il valore predefinito è 500 byte.

**Impostare le opzioni di esecuzione del rendering**

È possibile impostare le opzioni di esecuzione del rendering durante la creazione di file PDF. Sebbene queste opzioni non siano necessarie (a differenza delle opzioni di runtime di PDF), è possibile eseguire attività quali il miglioramento delle prestazioni del servizio Output. Ad esempio, è possibile memorizzare nella cache la struttura del modulo utilizzata dal servizio Output per migliorare le prestazioni.

**Generare un documento PDF**

Dopo aver fatto riferimento a un&#39;origine dati XML valida e aver impostato le opzioni di esecuzione, è possibile richiamare il servizio Output generando un documento PDF. Se il servizio Output individua un pattern di testo specificato nei dati di input, utilizza la struttura del modulo corrispondente. Se non si utilizza un pattern di testo, il servizio Output utilizza la struttura del modulo predefinita.

**Recupera i risultati dell&#39;operazione**

Dopo aver eseguito un&#39;operazione, il servizio Output restituisce dati XML che specificano se l&#39;operazione è riuscita.

**Consulta anche**

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API del servizio di output](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Creare regole di ricerca utilizzando l’API Java {#create-search-rules-using-the-java-api}

Creare regole di ricerca utilizzando l’API di output (Java):

1. Includi file di progetto.

   Includi file JAR client, come adobe-output-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto Client di output.

   * Crea un `ServiceClientFactory` oggetto contenente le proprietà di connessione.
   * Crea un `OutputClient` utilizzando il relativo costruttore e passando `ServiceClientFactory` oggetto.

1. Fare riferimento a un&#39;origine dati XML.

   * Crea un `java.io.FileInputStream` oggetto che rappresenta l&#39;origine dati XML utilizzata per compilare il documento PDF utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del file XML.
   * Crea un `com.adobe.idp.Document` utilizzando il relativo costruttore e passando `java.io.FileInputStream` oggetto.

1. Definisci le regole di ricerca.

   * Crea un `Rule` utilizzando il relativo costruttore.
   * Definire un pattern di testo richiamando il `Rule` dell’oggetto `setPattern` e passare un valore stringa che specifica un pattern di testo.
   * Definire la struttura del modulo corrispondente richiamando il `Rule` dell’oggetto `setForm` metodo . Passa un valore stringa che specifica il nome della struttura del modulo.

   >[!NOTE]
   >
   >Per ogni pattern di testo da definire, ripetere i tre passaggi secondari precedenti.

   * Crea un `java.util.List` utilizzando un `java.util.ArrayList` costruttore.
   * Per ogni `Rule` oggetto creato, richiamare `java.util.List` dell’oggetto `add` e passare il `Rule` oggetto.


1. Impostare le opzioni di runtime di PDF.

   * Crea un `PDFOutputOptionsSpec` utilizzando il relativo costruttore.
   * Specifica il nome e la posizione del file PDF generato dal servizio Output richiamando il `PDFOutputOptionsSpec` dell’oggetto `setFileURI` metodo . Passa un valore stringa che specifica la posizione del file PDF. L’opzione URI file è relativa al server applicazioni J2EE che ospita AEM Forms, non al computer client.
   * Imposta le regole definite richiamando il `PDFOutputOptionsSpec` dell’oggetto `setRules` metodo . Passa la `java.util.List` oggetto che contiene `Rule` oggetti.
   * Impostare il numero di byte da analizzare per i pattern di testo definiti richiamando il `PDFOutputOptionsSpec` dell’oggetto `setLookAhead` metodo . Passa un valore intero che rappresenta i numeri di byte.

1. Imposta le opzioni di esecuzione del rendering.

   * Crea un `RenderOptionsSpec` utilizzando il relativo costruttore.
   * Memorizza in cache la struttura del modulo per migliorare le prestazioni del servizio Output richiamando il `RenderOptionsSpec` dell’oggetto `setCacheEnabled` e di passaggio `true`.

1. Genera un documento PDF.

   Generare un documento PDF basato su più strutture del modulo richiamando il `OutputClient` dell’oggetto `generatePDFOutput` e passando i seguenti valori:

   * A `TransformationFormat` valore di enumerazione. Per generare un documento PDF, specificare `TransformationFormat.PDF`.
   * Valore stringa che specifica il nome della struttura del modulo predefinita. In altre parole, la struttura del modulo utilizzata se non si trova un pattern di testo.
   * Valore stringa che specifica la directory principale del contenuto in cui si trovano le strutture del modulo.
   * A `PDFOutputOptionsSpec` oggetto contenente le opzioni di runtime di PDF.
   * A `RenderOptionsSpec` oggetto contenente le opzioni di esecuzione del rendering.
   * La `com.adobe.idp.Document` oggetto che contiene i dati del modulo ricercati dal servizio Output per individuare i pattern di testo definiti.

   La `generatePDFOutput` restituisce un `OutputResult` oggetto contenente i risultati dell&#39;operazione.

1. Recupera i risultati dell’operazione.

   * Crea un `com.adobe.idp.Document` che rappresenta lo stato `generatePDFOutput` richiamando il metodo `OutputResult` dell’oggetto `getStatusDoc` metodo .
   * Crea un `java.io.File` oggetto che conterrà i risultati dell&#39;operazione. Assicurati che l&#39;estensione del file sia .xml.
   * Richiama il `com.adobe.idp.Document` dell’oggetto `copyToFile` per copiare il contenuto del `com.adobe.idp.Document` al file (assicurati di utilizzare `com.adobe.idp.Document` oggetto restituito da `getStatusDoc` metodo).

**Consulta anche**

[Riepilogo dei passaggi](creating-document-output-streams.md#summary-of-steps)

[Avvio rapido (modalità EJB): Creazione di regole di ricerca tramite l’API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-search-rules-using-the-java-api)

[Avvio rapido (modalità SOAP): Creazione di regole di ricerca tramite l’API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-search-rules-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Creare regole di ricerca utilizzando l’API del servizio Web {#create-search-rules-using-the-web-service-api}

Crea le regole di ricerca utilizzando l’API di output (servizio Web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurati di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l’indirizzo IP del server che ospita AEM Forms.

1. Creare un oggetto Client di output.

   * Crea un `OutputServiceClient` utilizzando il relativo costruttore predefinito.
   * Crea un `OutputServiceClient.Endpoint.Address` utilizzando `System.ServiceModel.EndpointAddress` costruttore. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/OutputService?blob=mtom`.) Non è necessario utilizzare il `lc_version` attributo. Questo attributo viene utilizzato quando si crea un riferimento a un servizio. Tuttavia, specifica `?blob=mtom` per utilizzare MTOM.
   * Crea un `System.ServiceModel.BasicHttpBinding` ottenendo il valore del `OutputServiceClient.Endpoint.Binding` campo . Imposta il valore restituito su `BasicHttpBinding`.
   * Imposta la `System.ServiceModel.BasicHttpBinding` dell’oggetto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegnare il nome utente del modulo di AEM al campo `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore della password corrispondente al campo `OutputServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Fare riferimento a un&#39;origine dati XML.

   * Crea un `BLOB` utilizzando il relativo costruttore. La `BLOB` viene utilizzato per memorizzare i dati che verranno uniti al documento PDF.
   * Crea un `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF da crittografare e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto del `System.IO.FileStream` oggetto. È possibile determinare le dimensioni dell&#39;array di byte ottenendo il `System.IO.FileStream` dell’oggetto `Length` proprietà.
   * Compilare l&#39;array di byte con i dati del flusso richiamando il `System.IO.FileStream` dell’oggetto `Read` e passare l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare `BLOB` oggetto assegnando il relativo `MTOM` con il contenuto dell&#39;array di byte.

1. Definisci le regole di ricerca.

   * Crea un `Rule` utilizzando il relativo costruttore.
   * Definire un pattern di testo assegnando un valore di stringa che specifica un pattern di testo `Rule` dell’oggetto `pattern` membro dati.
   * Definire la struttura del modulo corrispondente assegnando un valore stringa che specifica la struttura del modulo `Rule` dell’oggetto `form` membro dati.

   >[!NOTE]
   >
   >Per ogni pattern di testo da definire, ripetere i tre passaggi secondari precedenti.

   * Crea un `MyArrayOf_xsd_anyType` oggetto che memorizza le regole.
   * Assegna ogni `Rule` a un elemento del `MyArrayOf_xsd_anyType` array. Richiama il `MyArrayOf_xsd_anyType` dell’oggetto `Add` metodo per `Rule` oggetto.


1. Impostare le opzioni di runtime di PDF

   * Crea un `PDFOutputOptionsSpec` utilizzando il relativo costruttore.
   * Impostare l&#39;opzione URI del file assegnando un valore stringa che specifica la posizione del file PDF generato dal servizio Output nel `PDFOutputOptionsSpec` dell’oggetto `fileURI` membro dati. L’opzione URI file è relativa al server applicazioni J2EE che ospita AEM Forms, non al computer client.
   * Impostare l&#39;opzione copie assegnando un valore intero che specifica il numero di copie generate dal servizio Output al `PDFOutputOptionsSpec` dell’oggetto `copies` membro dati.
   * Imposta le regole definite assegnando il `MyArrayOf_xsd_anyType` oggetto che memorizza le regole nel `PDFOutputOptionsSpec` dell’oggetto `rules` membro dati.
   * Impostare il numero di byte da analizzare per i pattern di testo definiti assegnando un valore intero che rappresenta i numeri di byte da analizzare al `PDFOutputOptionsSpec` dell’oggetto `lookAhead` metodo data.

1. Impostare le opzioni di esecuzione del rendering

   * Crea un `RenderOptionsSpec` utilizzando il relativo costruttore.
   * Memorizza in cache la struttura del modulo per migliorare le prestazioni del servizio Output assegnando il valore `true` al `RenderOptionsSpec` dell’oggetto `cacheEnabled` membro dati.

   >[!NOTE]
   >
   >Non è possibile impostare la versione del documento di PDF utilizzando il `RenderOptionsSpec` dell’oggetto `pdfVersion` membro se il documento di input è un modulo Acrobat. Nel documento di output PDF viene mantenuta la versione PDF del modulo Acrobat. Allo stesso modo, non è possibile impostare l’opzione PDF con tag utilizzando `RenderOptionsSpec` dell’oggetto `taggedPDF` se il documento di input è un modulo Acrobat.

   >[!NOTE]
   >
   >Non è possibile impostare l’opzione linearized PDF utilizzando `RenderOptionsSpec` dell’oggetto `linearizedPDF` se il documento di input PDF è certificato o firmato digitalmente. Per informazioni, consulta [Firma digitale di documenti PDF](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents).

1. Generare un documento PDF

   Creare un documento PDF richiamando il `OutputServiceService` dell’oggetto `generatePDFOutput`e passando i seguenti valori:

   * A `TransformationFormat` valore di enumerazione. Per generare un documento PDF, specificare `TransformationFormat.PDF`.
   * Valore stringa che specifica il nome della struttura del modulo.
   * Valore stringa che specifica la directory principale del contenuto in cui si trova la struttura del modulo.
   * A `PDFOutputOptionsSpec` oggetto contenente le opzioni di runtime di PDF.
   * A `RenderOptionsSpec` oggetto contenente le opzioni di esecuzione del rendering.
   * La `BLOB` oggetto contenente l’origine dati XML contenente i dati da unire alla struttura del modulo.
   * A `BLOB` oggetto popolato da `generatePDFOutput` metodo . La `generatePDFOutput` popola l&#39;oggetto con i metadati generati che descrivono il documento. (Questo valore di parametro è richiesto solo per la chiamata al servizio Web).
   * A `BLOB` oggetto popolato da `generatePDFOutput` metodo . La `generatePDFOutput` popola l&#39;oggetto con i dati dei risultati. (Questo valore di parametro è richiesto solo per la chiamata al servizio Web).
   * Un `OutputResult` oggetto contenente i risultati dell&#39;operazione. (Questo valore di parametro è richiesto solo per la chiamata al servizio Web).

   >[!NOTE]
   >
   >Quando si genera un documento PDF richiamando il `generatePDFOutput` metodo : non è possibile unire dati con un modulo XFA PDF firmato, certificato o contenente diritti di utilizzo. Per informazioni sui diritti di utilizzo, vedi [Applicazione dei diritti di utilizzo ai documenti PDF](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents).

1. Recupera i risultati dell&#39;operazione

   * Crea un `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta una posizione di file XML contenente i dati dei risultati. Assicurati che l&#39;estensione del file sia XML.
   * Creare un array di byte che memorizza il contenuto dei dati del `BLOB` oggetto popolato con i dati dei risultati da `OutputServiceService` dell’oggetto `generatePDFOutput` (l&#39;ottavo parametro). Compilare l’array di byte ottenendo il valore del `BLOB` dell’oggetto `MTOM` membro dati.
   * Crea un `System.IO.BinaryWriter` richiamando il relativo costruttore e passando `System.IO.FileStream` oggetto.
   * Scrivere il contenuto dell&#39;array di byte nel file XML richiamando il `System.IO.BinaryWriter` dell’oggetto `Write` e passare l&#39;array di byte.

**Consulta anche**

[Riepilogo dei passaggi](creating-document-output-streams.md#summary-of-steps)

[Richiamo di AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamo di AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Flatting dei documenti PDF {#flattening-pdf-documents}

È possibile utilizzare il servizio Output per trasformare un documento PDF interattivo in un PDF non interattivo. Un documento PDF interattivo consente agli utenti di immettere o modificare i dati presenti nei campi del documento di PDF. Il processo di trasformazione di un documento PDF interattivo in un documento PDF non interattivo è denominato *appiattimento*. Quando un documento PDF viene appiattito, un utente non può modificare i dati nei campi del documento. Un motivo per appiattire un documento di PDF è garantire che i dati non possano essere modificati.

È possibile appiattire i seguenti tipi di documenti PDF:

* Documenti XFA PDF interattivi
* Acrobat Forms

Il tentativo di appiattire un PDF che è un documento di PDF non interattivo causa un&#39;eccezione.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Output, vedi [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-9}

Per appiattire un documento PDF interattivo a un documento PDF non interattivo, procedere come segue:

1. Includi file di progetto.
1. Creare un oggetto Client di output.
1. Recupera un documento PDF interattivo.
1. Trasforma il documento PDF.
1. Salvare il documento PDF non interattivo come file PDF.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso della classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è distribuito su JBoss)
* jbossall-client.jar (richiesto se AEM Forms è distribuito su JBoss)

se AEM Forms è distribuito su un server applicazioni J2EE supportato che non è JBoss, sarà necessario sostituire i file adobe-utilities.jar e jbossall-client.jar con file JAR specifici per il server applicazioni J2EE in cui viene distribuito AEM Forms. Per informazioni sulla posizione di tutti i file JAR di AEM Forms, vedi [Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un oggetto Client di output**

Prima di poter eseguire un&#39;operazione del servizio Output a livello di programmazione, è necessario creare un oggetto client del servizio Output. Se utilizzi l’API Java, crea un `OutputClient` oggetto. Se utilizzi l’API del servizio Web Output, crea un `OutputServiceService` oggetto.

**Recuperare un documento PDF interattivo**

Recuperare un documento PDF interattivo da trasformare in un documento PDF non interattivo. Il tentativo di trasformare un documento PDF non interattivo causa un&#39;eccezione.

**Trasforma il documento PDF**

Dopo aver recuperato un documento PDF interattivo, è possibile trasformarlo in un documento PDF non interattivo. Il servizio Output restituisce un documento PDF non interattivo.

**Salvare il documento PDF non interattivo come file PDF**

È possibile salvare il documento PDF non interattivo come file PDF.

**Consulta anche**

[Appiattire un documento PDF utilizzando l’API Java](creating-document-output-streams.md#flatten-a-pdf-document-using-the-java-api)

[Appiattire un documento PDF utilizzando l’API del servizio Web](creating-document-output-streams.md#flatten-a-pdf-document-using-the-web-service-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API del servizio di output](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Appiattire un documento PDF utilizzando l’API Java {#flatten-a-pdf-document-using-the-java-api}

Appiattisci un documento PDF interattivo a un documento PDF non interattivo utilizzando l’API di output (Java):

1. Includi file di progetto.

   Includi file JAR client, come adobe-output-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto Client di output.

   * Crea un `ServiceClientFactory` oggetto contenente le proprietà di connessione.
   * Crea un `OutputClient` utilizzando il relativo costruttore e passando `ServiceClientFactory` oggetto.

1. Recupera un documento PDF interattivo.

   * Crea un `java.io.FileInputStream` oggetto che rappresenta il documento PDF interattivo da trasformare utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del file PDF interattivo.
   * Crea un `com.adobe.idp.Document` utilizzando il relativo costruttore e passando `java.io.FileInputStream` oggetto.

1. Trasforma il documento PDF.

   Trasforma il documento PDF interattivo in un documento PDF non interattivo richiamando il `OutputServiceService` dell’oggetto `transformPDF` e passando i seguenti valori:

   * La `com.adobe.idp.Document` oggetto contenente il documento interattivo di PDF.
   * A `TransformationFormat` valore enum. Per generare un documento PDF non interattivo, specificare `TransformationFormat.PDF`.
   * A `PDFARevisionNumber` valore enum che specifica il numero di revisione. Poiché questo parametro è destinato a un documento PDF/A, è possibile specificare `null`.
   * Valore stringa che rappresenta il numero e l&#39;anno della modifica, separati da due punti. Poiché questo parametro è destinato a un documento PDF/A, è possibile specificare `null`.
   * A `PDFAConformance` valore enum che rappresenta il livello di conformità PDF/A. Poiché questo parametro è destinato a un documento PDF/A, è possibile specificare `null`.

   La `transformPDF` restituisce un `com.adobe.idp.Document` oggetto contenente un documento PDF non interattivo.

1. Salvare il documento PDF non interattivo come file PDF.

   * Crea un `java.io.File` e assicurati che l&#39;estensione del nome del file sia .pdf.
   * Richiama il `Document` dell’oggetto `copyToFile` per copiare il contenuto del `Document` al file (assicurati di utilizzare `Document` oggetto restituito da `transformPDF` metodo).

**Consulta anche**

[Riepilogo dei passaggi](creating-document-output-streams.md#summary-of-steps)

[Avvio rapido (modalità EJB): Trasformazione di un documento PDF tramite l’API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-transforming-a-pdf-document-using-the-java-api)

[Avvio rapido (modalità SOAP): Trasformazione di un documento PDF tramite l’API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-transforming-a-pdf-document-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Appiattire un documento PDF utilizzando l’API del servizio Web {#flatten-a-pdf-document-using-the-web-service-api}

Appiattisci un documento PDF interattivo a un documento PDF non interattivo utilizzando l’API di output (servizio Web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurati di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l’indirizzo IP del server che ospita AEM Forms.

1. Creare un oggetto Client di output.

   * Crea un `OutputServiceClient` utilizzando il relativo costruttore predefinito.
   * Crea un `OutputServiceClient.Endpoint.Address` utilizzando `System.ServiceModel.EndpointAddress` costruttore. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/OutputService?blob=mtom`.) Non è necessario utilizzare il `lc_version` attributo. Questo attributo viene utilizzato quando si crea un riferimento a un servizio. Tuttavia, specifica `?blob=mtom` per utilizzare MTOM.
   * Crea un `System.ServiceModel.BasicHttpBinding` ottenendo il valore del `OutputServiceClient.Endpoint.Binding` campo . Imposta il valore restituito su `BasicHttpBinding`.
   * Imposta la `System.ServiceModel.BasicHttpBinding` dell’oggetto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegnare il nome utente del modulo di AEM al campo `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore della password corrispondente al campo `OutputServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recupera un documento PDF interattivo.

   * Crea un `BLOB` utilizzando il relativo costruttore. La `BLOB` viene utilizzato per memorizzare il documento interattivo di PDF.
   * Crea un `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento interattivo di PDF.
   * Creare un array di byte che memorizza il contenuto del `System.IO.FileStream` oggetto. È possibile determinare le dimensioni dell&#39;array di byte ottenendo il `System.IO.FileStream` dell’oggetto `Length` proprietà.
   * Compilare l&#39;array di byte con i dati del flusso richiamando il `System.IO.FileStream` dell’oggetto `Read` e passare l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare `BLOB` oggetto assegnando il relativo `MTOM` con il contenuto dell&#39;array di byte.

1. Trasforma il documento PDF.

   Trasforma il documento PDF interattivo in un documento PDF non interattivo richiamando il `OutputClient` dell’oggetto `transformPDF` e passando i seguenti valori:

   * A `BLOB` oggetto contenente il documento interattivo di PDF.
   * A `TransformationFormat` valore di enumerazione. Per generare un documento PDF non interattivo, specificare `TransformationFormat.PDF`.
   * A `PDFARevisionNumber` valore enum che specifica il numero di revisione.
   * Un valore booleano che specifica se la variabile `PDFARevisionNumber` viene utilizzato il valore enum. Poiché questo parametro è destinato a un documento PDF/A, è possibile specificare `false`.
   * Valore stringa che rappresenta il numero e l&#39;anno della modifica, separati da due punti. Poiché questo parametro è destinato a un documento PDF/A, è possibile specificare `null`.
   * A `PDFAConformance` valore enum che rappresenta il livello di conformità PDF/A.
   * Valore booleano che specifica se la variabile `PDFAConformance` viene utilizzato il valore enum. Poiché questo parametro è destinato a un documento PDF/A, è possibile specificare `false`.

   La `transformPDF` restituisce un `BLOB` oggetto contenente un documento PDF non interattivo.

1. Salvare il documento PDF non interattivo come file PDF.

   * Crea un `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF non interattivo.
   * Creare un array di byte che memorizza il contenuto dei dati del `BLOB` oggetto restituito da `transformPDF` metodo . Compilare l’array di byte ottenendo il valore del `BLOB` dell’oggetto `MTOM` membro dati.
   * Crea un `System.IO.BinaryWriter` richiamando il relativo costruttore e passando `System.IO.FileStream` oggetto.
   * Scrivi il contenuto dell’array di byte in un file PDF richiamando il `System.IO.BinaryWriter` dell’oggetto `Write` e passare l&#39;array di byte.

**Consulta anche**

[Riepilogo dei passaggi](creating-document-output-streams.md#summary-of-steps)

[Richiamo di AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamo di AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
