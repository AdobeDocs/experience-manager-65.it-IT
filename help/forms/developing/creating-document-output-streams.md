---
title: Creazione di flussi di output dei documenti
seo-title: Creazione di flussi di output dei documenti
description: 'null'
seo-description: 'null'
uuid: 80c28efa-35ce-4073-9ca6-2d93bcd67fdd
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: de527d50-991b-4ca3-a8ac-44d5cab988e9
translation-type: tm+mt
source-git-commit: 7cbe3e94eddb81925072f68388649befbb027e6d

---


# Creazione di flussi di output dei documenti {#creating-document-output-streams}

**Informazioni su Output Service**

Il servizio Output consente di inviare i documenti in formato PDF (inclusi i documenti PDF/A), PostScript, PCL (Printer Control Language) e nei seguenti formati di etichetta:

* Zebra - ZPL
* Intermec - IPL
* Datamax - DPL
* TecToshiba - TPCL

Utilizzando il servizio Output, è possibile unire i dati del modulo XML a una struttura del modulo e inviare il documento a una stampante o a un file di rete.

Esistono due modi in cui è possibile trasmettere una struttura del modulo (un file XDP) al servizio Output. È possibile trasmettere al servizio Output un&#39; `com.adobe.idp.Document` istanza contenente una struttura del modulo. In alternativa, è possibile trasmettere un valore URI che specifica la posizione della struttura del modulo. Entrambi questi modi sono descritti nella *programmazione con i moduli* AEM.

>[!NOTE]
>
>Il servizio Output non supporta i documenti Acrobat PDF contenenti script specifici dell&#39;oggetto applicativo. Non viene eseguito il rendering dei documenti PDF di Acrobat contenenti script specifici dell&#39;oggetto applicativo.

Nelle sezioni seguenti viene illustrato come trasmettere una struttura del modulo al servizio Output utilizzando un valore URI:

* [Creazione di documenti PDF](creating-document-output-streams.md#creating-pdf-documents)
* [Creazione di documenti PDF/A](creating-document-output-streams.md#creating-pdf-a-documents)

Nelle sezioni seguenti viene illustrato come trasmettere una struttura del modulo all&#39;interno di un&#39; `com.adobe.idp.Document` istanza:

* [Invio di documenti in Content Services (obsoleto) al servizio di output](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)
* [Creazione di documenti PDF tramite frammenti](creating-document-output-streams.md#creating-pdf-documents-using-fragments)

Quando si decide quale tecnica utilizzare, occorre considerare se la struttura del modulo viene ottenuta da un altro servizio AEM Forms e quindi trasmetterla in un’ `com.adobe.idp.Document` istanza. Le sezioni *Trasmissione di documenti al servizio* di output e *Creazione di documenti PDF tramite frammenti* mostrano come ottenere una struttura del modulo da un altro servizio AEM Forms. La prima sezione recupera la struttura del modulo da Content Services (obsoleto). La seconda sezione recupera la struttura del modulo dal servizio Assembler.

Se si ottiene la struttura del modulo da una posizione fissa, ad esempio il file system, è possibile utilizzare una delle due tecniche. In altre parole, è possibile specificare il valore URI per un file XDP o utilizzare un&#39; `com.adobe.idp.Document` istanza.

Per passare un valore URI che specifica la posizione della struttura del modulo durante la creazione di un documento PDF, utilizzare il `generatePDFOutput` metodo . Analogamente, per passare un&#39; `com.adobe.idp.Document` istanza al servizio Output durante la creazione di un documento PDF, utilizzare il `generatePDFOutput2` metodo .

Quando si invia un flusso di output a una stampante di rete, è possibile utilizzare anche una delle due tecniche. Per inviare un flusso di output a una stampante passando un&#39; `com.adobe.idp.Document` istanza che contiene una struttura del modulo, utilizzare il `sendToPrinter2`metodo. Per inviare un flusso di output a una stampante passando un valore URI, utilizzare il `sendToPrinter`metodo . La sezione *Invio di flussi di stampa alle stampanti* utilizza questo `sendToPrinter` metodo.

È possibile eseguire le operazioni seguenti utilizzando il servizio Output:

* [Creazione di documenti PDF](creating-document-output-streams.md#creating-pdf-documents)
* [Creazione di documenti PDF/A](creating-document-output-streams.md#creating-pdf-a-documents)
* [Invio di documenti in Content Services (obsoleto) al servizio di output](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)
* [Creazione di documenti PDF tramite frammenti](creating-document-output-streams.md#creating-pdf-documents-using-fragments)
* [Stampa su file](creating-document-output-streams.md#printing-to-files)
* [Invio di flussi di stampa alle stampanti](creating-document-output-streams.md#sending-print-streams-to-printers)
* [Creazione di più file di output](creating-document-output-streams.md#creating-multiple-output-files)
* [Creazione di regole di ricerca](creating-document-output-streams.md#creating-search-rules)
* [Conversione dei documenti PDF](creating-document-output-streams.md#flattening-pdf-documents)

   ***Nota **: Per ulteriori informazioni sul servizio Output, consultate Riferimento[servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).*

## Creazione di documenti PDF {#creating-pdf-documents}

È possibile utilizzare il servizio Output per creare un documento PDF basato su una struttura del modulo e sui dati del modulo XML forniti dall&#39;utente. Il documento PDF creato dal servizio Output non è un documento PDF interattivo; un utente non può immettere o modificare i dati del modulo.

Se si desidera creare un documento PDF destinato all&#39;archiviazione a lungo termine, è consigliabile creare un documento PDF/A. (Vedere [Creazione di documenti](creating-document-output-streams.md#creating-pdf-a-documents)PDF/A.)

Per creare un modulo PDF interattivo che consenta all&#39;utente di immettere i dati, utilizzare il servizio Moduli. (Vedere [Rendering di moduli](/help/forms/developing/rendering-forms.md#rendering-interactive-pdf-forms)PDF interattivi.)

>[!NOTE]
>
> Per ulteriori informazioni sul servizio Output, consultate Riferimento [servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary-of-steps}

Per creare un documento PDF, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un oggetto Client di output.
1. Fare riferimento a un&#39;origine dati XML.
1. Impostare le opzioni di esecuzione PDF.
1. Impostare le opzioni di esecuzione del rendering.
1. Generare un documento PDF.
1. Recuperare i risultati dell&#39;operazione.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate servizi Web, accertatevi di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è distribuito su JBoss)
* jbossall-client.jar (richiesto se AEM Forms è distribuito su JBoss)

se AEM Forms è distribuito su un server applicazione J2EE supportato che non sia JBoss, dovrete sostituire i file adobe-utilities.jar e jbossall-client.jar con file JAR specifici del server applicazione J2EE su cui è distribuito AEM Forms.

**Creare un oggetto Client di output**

Prima di eseguire un&#39;operazione del servizio Output a livello di programmazione, è necessario creare un oggetto client del servizio Output. Se utilizzate l&#39;API Java, create un `OutputClient` oggetto. Se si utilizza l&#39;API del servizio Web Output, creare un `OutputServiceService` oggetto.

**Riferimento a un&#39;origine dati XML**

Per unire i dati alla struttura del modulo, è necessario fare riferimento a un&#39;origine dati XML che contiene i dati. Per ogni campo del modulo che si intende compilare con i dati deve esistere un elemento XML. Il nome dell&#39;elemento XML deve corrispondere al nome del campo. Un elemento XML viene ignorato se non corrisponde a un campo modulo o se il nome dell&#39;elemento XML non corrisponde al nome del campo. Se vengono specificati tutti gli elementi XML, non è necessario stabilire una corrispondenza con l&#39;ordine di visualizzazione degli elementi XML.

Considerare il seguente modulo di richiesta di prestito.

![cp_cp_loanformdata](assets/cp_cp_loanformdata.png)

Per unire i dati alla struttura del modulo, è necessario creare un&#39;origine dati XML corrispondente al modulo. Il codice XML seguente rappresenta un&#39;origine dati XML XDP che corrisponde al modulo di esempio per l&#39;applicazione ipoteca.

```as3
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

**Impostazione delle opzioni di esecuzione PDF**

Impostare l&#39;opzione URI del file al momento della creazione di un documento PDF. Questa opzione specifica il nome e la posizione del file PDF generato dal servizio Output.

>[!NOTE]
>
>Anziché impostare l&#39;opzione di runtime URI del file, è possibile recuperare il documento PDF a livello di programmazione dal tipo di dati complesso restituito dal servizio Output. Tuttavia, impostando l&#39;opzione di runtime URI del file, non è necessario creare una logica applicativa che recuperi il documento PDF a livello di programmazione.

**Impostazione delle opzioni di esecuzione del rendering**

È possibile impostare le opzioni di esecuzione del rendering al momento della creazione di un documento PDF. Sebbene queste opzioni non siano richieste (a differenza delle opzioni PDF in fase di esecuzione richieste), è possibile eseguire attività quali migliorare le prestazioni del servizio Output. Ad esempio, è possibile memorizzare nella cache la struttura del modulo utilizzata dal servizio Output per migliorarne le prestazioni.

Se si utilizza un modulo Acrobat con tag come input, non è possibile utilizzare Java del servizio Output o API del servizio Web per disattivare l&#39;impostazione dei tag. Se si tenta di impostare questa opzione a livello di programmazione, al documento PDF risultante viene ancora applicato un tag. `false`

>[!NOTE]
>
>Se non specificate le opzioni di esecuzione del rendering, vengono utilizzati i valori predefiniti. Per informazioni sul rendering delle opzioni di esecuzione, vedere il riferimento alla `RenderOptionsSpec` classe. Consultate Riferimento [API per](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)AEM Forms.

**Generazione di un documento PDF**

Dopo aver fatto riferimento a un&#39;origine dati XML valida che contiene i dati del modulo e aver impostato le opzioni di esecuzione, è possibile richiamare il servizio Output, generando così un documento PDF.

Durante la generazione di un documento PDF, è possibile specificare i valori URI richiesti dal servizio Output per creare un documento PDF. Una struttura del modulo può essere memorizzata in percorsi quali il file system del server o come parte di un&#39;applicazione AEM Forms. Per fare riferimento a una struttura del modulo (o ad altre risorse, come un file di immagine) esistente all&#39;interno di un&#39;applicazione Forms, utilizzare il valore URI radice del contenuto `repository:///`. Ad esempio, tenere in considerazione la seguente struttura del modulo denominata *Loan.xdp* , disponibile all&#39;interno di un&#39;applicazione Forms denominata *Applications/FormsApplication*:

![cp_cp_formrepository](assets/cp_cp_formrepository.png)

Per accedere al file Loan.xdp illustrato nell&#39;illustrazione precedente, specificate `repository:///Applications/FormsApplication/1.0/FormsFolder/` come terzo parametro passato al `OutputClient` metodo dell&#39;oggetto `generatePDFOutput` . Specificare il nome del modulo (*Loan.xdp*) come secondo parametro passato al metodo dell&#39; `OutputClient` oggetto `generatePDFOutput` .

Se il file XDP contiene immagini (o altre risorse come i frammenti), posizionare le risorse nella stessa cartella dell&#39;applicazione del file XDP. AEM Forms utilizza l’URI della directory principale del contenuto come percorso di base per risolvere i riferimenti alle immagini. Ad esempio, se il file Loan.xdp contiene un&#39;immagine, accertatevi di inserire l&#39;immagine in `Applications/FormsApplication/1.0/FormsFolder/`.

>[!NOTE]
>
>È possibile fare riferimento all&#39;URI di un&#39;applicazione Forms quando si richiamano i `OutputClient` metodi `generatePDFOutput` o `generatePrintedOutput` gli oggetti.

>[!NOTE]
>
>Per visualizzare un avvio rapido completo che crea un documento PDF facendo riferimento a un file XDP presente in un&#39;applicazione Forms, vedere Avvio [rapido (modalità EJB): Creazione di un documento PDF basato su un file XDP dell&#39;applicazione mediante l&#39;API](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-an-application-xdp-file-using-the-java-api)Java.

**Recuperare i risultati dell&#39;operazione**

Dopo che il servizio Output ha eseguito un&#39;operazione, restituisce vari elementi di dati, ad esempio dati XML di stato, che specificano se l&#39;operazione ha avuto esito positivo.

**Consulta anche**

[Creare un documento PDF utilizzando l&#39;API Java](creating-document-output-streams.md#create-a-pdf-document-using-the-java-api)

[Creazione di un documento PDF tramite l&#39;API del servizio Web](creating-document-output-streams.md#create-a-pdf-document-using-the-web-service-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API di Output Service](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Creare un documento PDF utilizzando l&#39;API Java {#create-a-pdf-document-using-the-java-api}

Creare un documento PDF utilizzando l&#39;API di output (Java):

1. Includere i file di progetto.

   Includete file JAR client, ad esempio adobe-output-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto Client di output.

   * Creare un `ServiceClientFactory` oggetto che contenga proprietà di connessione.
   * Creare un `OutputClient` oggetto utilizzando il relativo costruttore e passando l&#39; `ServiceClientFactory` oggetto.

1. Fare riferimento a un&#39;origine dati XML.

   * Creare un `java.io.FileInputStream` oggetto che rappresenta l&#39;origine dati XML utilizzata per compilare il documento PDF utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del file XML.
   * Creare un `com.adobe.idp.Document` oggetto utilizzando il relativo costruttore. Passate l&#39; `java.io.FileInputStream` oggetto.

1. Impostare le opzioni di esecuzione PDF.

   * Creare un `PDFOutputOptionsSpec` oggetto utilizzando il relativo costruttore.
   * Impostare l&#39;opzione URI del file richiamando il `PDFOutputOptionsSpec` metodo dell&#39; `setFileURI` oggetto. Passa un valore di stringa che specifica la posizione del file PDF generato dal servizio Output. L&#39;opzione URI file è relativa al server applicazione J2EE in cui è installato AEM Forms, non al computer client.

1. Impostare le opzioni di esecuzione del rendering.

   * Creare un `RenderOptionsSpec` oggetto utilizzando il relativo costruttore.
   * Memorizzare nella cache la struttura del modulo per migliorare le prestazioni del servizio Output richiamando l&#39; `RenderOptionsSpec` oggetto `setCacheEnabled` e passando `true`.
   >[!NOTE]
   >
   >Non è possibile impostare la versione del documento PDF utilizzando il metodo dell&#39; `RenderOptionsSpec` oggetto `setPdfVersion` se il documento di input è un modulo Acrobat (un modulo creato in Acrobat) o un documento XFA firmato o certificato. Il documento PDF di output conserva la versione PDF originale. Analogamente, non è possibile impostare l&#39;opzione Adobe PDF con tag richiamando il metodo dell&#39; `RenderOptionsSpec` oggetto `setTaggedPDF` se il documento di input è un modulo Acrobat o un documento XFA firmato o certificato.

   >[!NOTE]
   >
   >Non è possibile impostare l&#39;opzione PDF linearizzato utilizzando il metodo dell&#39; `RenderOptionsSpec` oggetto `setLinearizedPDF` se il documento PDF di input è certificato o firmato digitalmente. (Vedere Firma [digitale di documenti](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)*PDF.)*

1. Generare un documento PDF.

   Creare un documento PDF richiamando il metodo dell&#39; `OutputClient` oggetto `generatePDFOutput` e passando i seguenti valori:

   * Un valore `TransformationFormat` di enumerazione. Per generare un documento PDF, specificare `TransformationFormat.PDF`.
   * Una stringa che specifica il nome della struttura del modulo.
   * Una stringa che specifica il livello principale del contenuto in cui si trova la struttura del modulo.
   * Un `PDFOutputOptionsSpec` oggetto che contiene opzioni di esecuzione PDF.
   * Un `RenderOptionsSpec` oggetto che contiene opzioni di esecuzione del rendering.
   * L&#39; `com.adobe.idp.Document` oggetto che contiene l&#39;origine dati XML contenente i dati da unire alla struttura del modulo.
   Il `generatePDFOutput` metodo restituisce un `OutputResult` oggetto che contiene i risultati dell&#39;operazione.

   >[!NOTE]
   >
   >Durante la generazione di un documento PDF richiamando il `generatePDFOutput` metodo, tenere presente che non è possibile unire i dati a un modulo PDF XFA firmato o certificato. (Vedere Firma [digitale e certificazione dei documenti](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-and-certifying-documents)*.)*

   >[!NOTE]
   >
   >Il metodo `OutputResult` dell&#39; `getRecordLevelMetaDataList` oggetto restituisce `null`*.*

   >[!NOTE]
   >
   >È inoltre possibile creare un documento PDF richiamando il `OutputClient` metodo dell&#39; `generatePDFOutput2` . (Vedere [Trasmissione di documenti in Content Services (obsoleto) al servizio](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)*di output.)*

1. Recuperare i risultati dell&#39;operazione.

   * Recuperare un `com.adobe.idp.Document` oggetto che rappresenti lo stato dell&#39; `generatePDFOutput` operazione richiamando il metodo dell&#39; `OutputResult` oggetto `getStatusDoc` . Questo metodo restituisce dati XML di stato che specificano se l&#39;operazione ha avuto esito positivo.
   * Creare un `java.io.File` oggetto che contenga i risultati dell&#39;operazione. Accertatevi che l’estensione del nome del file sia .xml.
   * Richiamare il metodo dell&#39; `com.adobe.idp.Document` oggetto `copyToFile` per copiare il contenuto dell&#39; `com.adobe.idp.Document` oggetto nel file (assicurarsi di utilizzare l&#39; `com.adobe.idp.Document` oggetto restituito dal `getStatusDoc` metodo).
   Sebbene il servizio Output scriva il documento PDF nella posizione specificata dall&#39;argomento passato al `PDFOutputOptionsSpec` metodo dell&#39; `setFileURI` oggetto, è possibile recuperare il documento PDF/A a livello di programmazione richiamando il metodo dell&#39; `OutputResult` oggetto `getGeneratedDoc` .

**Consulta anche**

[Riepilogo dei passaggi](creating-document-output-streams.md#summary-of-steps)

[Avvio rapido (modalità EJB): Creazione di un documento PDF tramite l&#39;API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-using-the-java-api)

[Avvio rapido (modalità SOAP): Creazione di un documento PDF tramite l&#39;API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-using-the-java-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Creazione di un documento PDF tramite l&#39;API del servizio Web {#create-a-pdf-document-using-the-web-service-api}

Creare un documento PDF utilizzando l&#39;API di Output (servizio Web):

1. Includere i file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituire `localhost` con l&#39;indirizzo IP del server in cui è installato AEM Forms.

1. Creare un oggetto Client di output.

   * Creare un `OutputServiceClient` oggetto utilizzando il relativo costruttore predefinito.
   * Creare un `OutputServiceClient.Endpoint.Address` oggetto utilizzando il `System.ServiceModel.EndpointAddress` costruttore. Passa un valore di stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/OutputService?blob=mtom`.) Non è necessario utilizzare l&#39; `lc_version` attributo. Questo attributo viene utilizzato quando create un riferimento a un servizio. Tuttavia, specificate `?blob=mtom` per utilizzare MTOM.
   * Creare un `System.ServiceModel.BasicHttpBinding` oggetto ottenendo il valore del `OutputServiceClient.Endpoint.Binding` campo. Inserite il valore restituito in `BasicHttpBinding`.
   * Impostare il campo `System.ServiceModel.BasicHttpBinding` dell&#39; `MessageEncoding` oggetto su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilitate l&#39;autenticazione HTTP di base eseguendo le seguenti operazioni:

      * Assegnare il nome utente dei moduli AEM al campo `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `OutputServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Fare riferimento a un&#39;origine dati XML.

   * Creare un `BLOB` oggetto utilizzando il relativo costruttore. L&#39; `BLOB` oggetto viene utilizzato per memorizzare i dati XML che verranno uniti al documento PDF.
   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file XML contenente i dati del modulo.
   * Creare un array di byte che memorizza il contenuto dell&#39; `System.IO.FileStream` oggetto. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà dell&#39; `System.IO.FileStream` oggetto `Length` .
   * Compilare l&#39;array di byte con i dati del flusso richiamando il `System.IO.FileStream` `Read` metodo dell&#39;oggetto e passando l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39; `BLOB` oggetto assegnandone `MTOM` il campo con il contenuto dell&#39;array di byte.

1. Impostazione delle opzioni di esecuzione PDF

   * Creare un `PDFOutputOptionsSpec` oggetto utilizzando il relativo costruttore.
   * Impostare l&#39;opzione URI del file assegnando un valore di stringa che specifica la posizione del file PDF generato dal servizio Output al membro `PDFOutputOptionsSpec` dati dell&#39; `fileURI` oggetto. L&#39;opzione URI file è relativa al server applicazione J2EE in cui è installato AEM Forms, non al computer client.

1. Impostare le opzioni di esecuzione del rendering.

   * Creare un `RenderOptionsSpec` oggetto utilizzando il relativo costruttore.
   * Memorizzare nella cache la struttura del modulo per migliorare le prestazioni del servizio Output assegnando il valore `true` al membro `RenderOptionsSpec` dati dell&#39; `cacheEnabled` oggetto.
   >[!NOTE]
   >
   >Non è possibile impostare la versione del documento PDF utilizzando il metodo dell&#39; `RenderOptionsSpec` oggetto `setPdfVersion` se il documento di input è un modulo Acrobat (un modulo creato in Acrobat) o un documento XFA firmato o certificato. Il documento PDF di output conserva la versione PDF originale. Allo stesso modo, non è possibile impostare l&#39;opzione Adobe PDF con tag richiamando il metodo dell&#39; `RenderOptionsSpec` oggetto `setTaggedPDF`* se il documento di input è un modulo Acrobat o un documento XFA firmato o certificato.*

   >[!NOTE]
   >
   >Non è possibile impostare l&#39;opzione PDF linearizzato utilizzando il membro dell&#39; `RenderOptionsSpec` oggetto `linearizedPDF` se il documento PDF di input è certificato o firmato digitalmente. (Vedere Firma [digitale di documenti](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)*PDF.)*

1. Generare un documento PDF.

   Creare un documento PDF richiamando il `OutputServiceService` `generatePDFOutput`metodo dell&#39;oggetto e passando i seguenti valori:

   * Un valore `TransformationFormat` di enumerazione. Per generare un documento PDF, specificare `TransformationFormat.PDF`.
   * Una stringa che specifica il nome della struttura del modulo.
   * Una stringa che specifica il livello principale del contenuto in cui si trova la struttura del modulo.
   * Un `PDFOutputOptionsSpec` oggetto che contiene opzioni di esecuzione PDF.
   * Un `RenderOptionsSpec` oggetto che contiene opzioni di esecuzione del rendering.
   * L&#39; `BLOB` oggetto che contiene l&#39;origine dati XML contenente i dati da unire alla struttura del modulo.
   * Un `BLOB` oggetto popolato dal `generatePDFOutput` metodo. Il `generatePDFOutput` metodo popola l&#39;oggetto con i metadati generati che descrivono il documento. (Questo valore di parametro è richiesto solo per la chiamata al servizio Web).
   * Un `BLOB` oggetto popolato dal `generatePDFOutput` metodo. Il `generatePDFOutput` metodo popola l&#39;oggetto con i dati dei risultati. (Questo valore di parametro è richiesto solo per la chiamata al servizio Web).
   * Un `OutputResult` oggetto che contiene i risultati dell&#39;operazione. (Questo valore di parametro è richiesto solo per la chiamata al servizio Web).
   >[!NOTE]
   >
   >Durante la generazione di un documento PDF richiamando il `generatePDFOutput` metodo, tenere presente che non è possibile unire i dati a un modulo PDF XFA firmato o certificato. (Vedere Firma [digitale e certificazione dei documenti](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-and-certifying-documents)*.)*

   >[!NOTE]
   >
   >È inoltre possibile creare un documento PDF richiamando il `OutputClient` metodo dell&#39; `generatePDFOutput2` . (Vedere [Trasmissione di documenti in Content Services (obsoleto) al servizio](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)*di output.)*

1. Recuperare i risultati dell&#39;operazione.

   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore di stringa che rappresenta un percorso di file XML contenente i dati dei risultati. Accertatevi che l’estensione del nome del file sia .xml.
   * Creare un array di byte che memorizza il contenuto dei dati dell&#39; `BLOB` oggetto compilato con i dati dei risultati dal `OutputServiceService` metodo dell&#39; `generatePDFOutput` oggetto (ottavo parametro). Compilare l&#39;array di byte ottenendo il valore dell&#39; `BLOB` oggetto `MTOM` `field`.
   * Creare un `System.IO.BinaryWriter` oggetto richiamando il relativo costruttore e passando l&#39; `System.IO.FileStream` oggetto.
   * Scrivere il contenuto dell&#39;array di byte nel file XML richiamando il metodo dell&#39; `System.IO.BinaryWriter` oggetto `Write` e passando l&#39;array di byte.
   Consulta anche

   [Riepilogo dei passaggi](creating-document-output-streams.md#summary-of-steps)

   [Attivazione di moduli AEM tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

   [Richiamo di moduli AEM con SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

   >[!NOTE]
   >
   >Il metodo `OutputServiceService` dell&#39; `generateOutput` oggetto è obsoleto.

## Creazione di documenti PDF/A {#creating-pdf-a-documents}

È possibile utilizzare il servizio Output per creare un documento PDF/A. Poiché PDF/A è un formato di archiviazione per la conservazione a lungo termine del contenuto del documento, tutti i font vengono incorporati e il file non viene compresso. Di conseguenza, un documento PDF/A è generalmente più grande di un documento PDF standard. Inoltre, un documento PDF/A non contiene contenuto audio e video. Come per altre attività del servizio Output, è possibile creare un documento PDF/A mediante la creazione di una struttura del modulo e di dati da unire a una struttura del modulo.

La specifica PDF/A-1 è costituita da due livelli di conformità, ovvero a e b. La differenza principale tra i due è relativa al supporto della struttura logica (accessibilità), che non è richiesto per il livello di conformità b. Indipendentemente dal livello di conformità, PDF/A-1 specifica che tutti i font sono incorporati nel documento PDF/A generato.

Sebbene PDF/A sia lo standard per l&#39;archiviazione di documenti PDF, non è obbligatorio utilizzare i PDF/A per l&#39;archiviazione se un documento PDF standard soddisfa le esigenze aziendali. Lo scopo dello standard PDF/A è quello di stabilire un file PDF che possa essere memorizzato per un lungo periodo di tempo e soddisfare i requisiti di conservazione dei documenti. Ad esempio, un URL non può essere incorporato in un PDF/A perché nel tempo l’URL potrebbe diventare non valido.

L&#39;organizzazione deve valutare le proprie esigenze, il tempo di conservazione del documento, le dimensioni del file e determinare la propria strategia di archiviazione. È possibile determinare a livello di programmazione se un documento PDF è conforme allo standard PDF/A utilizzando il servizio DocConverter. (Vedere Determinazione [programmatica della conformità](/help/forms/developing/pdf-a-documents.md#programmatically-determining-pdf-a-compliancy)PDF/A.)

Un documento PDF/A deve utilizzare il font specificato nella struttura del modulo e i font non possono essere sostituiti. Di conseguenza, se un font che si trova all&#39;interno di un documento PDF non è disponibile nel sistema operativo host (OS), si verifica un&#39;eccezione.

Quando un documento PDF/A viene aperto in Acrobat, viene visualizzato un messaggio che conferma che il documento è un documento PDF/A, come illustrato nell&#39;illustrazione seguente.

![cp_cp_pdfamessage](assets/cp_cp_pdfamessage.png)

>[!NOTE]
>
>Nel sito Web AIIM è disponibile una sezione relativa alle domande frequenti in formato PDF/A accessibile da [https://www.aiim.org/documents/standards/19005-1_FAQ.pdf](https://www.aiim.org/documents/standards/19005-1_FAQ.pdf).

>[!NOTE]
>
> Per ulteriori informazioni sul servizio Output, consultate Riferimento [servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-1}

Per creare un documento PDF/A, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un oggetto Client di output.
1. Fare riferimento a un&#39;origine dati XML.
1. Impostare le opzioni di esecuzione PDF/A.
1. Impostare le opzioni di esecuzione del rendering.
1. Generare un documento PDF/A.
1. Recuperare i risultati dell&#39;operazione.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione personalizzata utilizzando Java, includete i file JAR necessari. Se utilizzate servizi Web, accertatevi di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è distribuito su JBoss)
* jbossall-client.jar (richiesto se AEM Forms è distribuito su JBoss)

se AEM Forms è distribuito su un server applicazione J2EE supportato che non sia JBoss, dovrete sostituire i file adobe-utilities.jar e jbossall-client.jar con file JAR specifici del server applicazione J2EE su cui è distribuito AEM Forms.

**Creare un oggetto Client di output**

Prima di eseguire un&#39;operazione del servizio Output a livello di programmazione, è necessario creare un oggetto client del servizio Output. Se utilizzate l&#39;API Java, create un `OutputClient` oggetto. Se si utilizza l&#39;API del servizio Web Output, creare un `OutputServiceService` oggetto.

**Riferimento a un&#39;origine dati XML**

Per unire i dati alla struttura del modulo, è necessario fare riferimento a un&#39;origine dati XML che contiene i dati. Per ogni campo del modulo che si desidera compilare con i dati deve esistere un elemento XML. Il nome dell&#39;elemento XML deve corrispondere al nome del campo. Un elemento XML viene ignorato se non corrisponde a un campo modulo o se il nome dell&#39;elemento XML non corrisponde al nome del campo. Se vengono specificati tutti gli elementi XML, non è necessario stabilire una corrispondenza con l&#39;ordine di visualizzazione degli elementi XML.

**Impostazione delle opzioni di esecuzione PDF/A**

È possibile impostare l&#39;opzione URI del file al momento della creazione di un documento PDF/A. L&#39;URI è relativo al server applicazione J2EE in cui è installato AEM Forms. Ovvero, se impostate C:\Adobe, il file viene scritto nella cartella sul server, non sul computer client. L&#39;URI specifica il nome e la posizione del file PDF/A generato dal servizio Output.

**Impostazione delle opzioni di esecuzione del rendering**

È possibile impostare le opzioni di esecuzione del rendering durante la creazione di documenti PDF/A. È possibile impostare due opzioni relative ai file PDF/A: `PDFAConformance` e `PDFARevisionNumber` . Il `PDFAConformance` valore si riferisce al modo in cui un documento PDF rispetta i requisiti che specificano il modo in cui vengono conservati i documenti elettronici a lungo termine. I valori validi per questa opzione sono `A` e `B`. Per informazioni sul livello a e sulla conformità b, vedere la specifica ISO PDF/A-1 denominata *ISO 19005-1 Document Management*.

Il `PDFARevisionNumber` valore si riferisce al numero di revisione di un documento PDF/A. Per informazioni sul numero di revisione di un documento PDF/A, vedere la specifica ISO PDF/A-1 denominata *ISO 19005-1 Document Management*.

>[!NOTE]
>
>Non è possibile impostare l&#39;opzione Adobe PDF con tag su quando si crea un documento PDF/A 1A. `false` PDF/A 1A sarà sempre un documento PDF con tag. Inoltre, non è possibile impostare l&#39;opzione Adobe PDF con tag su quando si crea un documento PDF/A 1B. `true` PDF/A 1B sarà sempre un documento PDF senza tag.

**Genera un documento PDF/A**

Dopo aver fatto riferimento a un&#39;origine dati XML valida che contiene i dati del modulo e aver impostato le opzioni di esecuzione, è possibile richiamare il servizio Output generando un documento PDF/A.

**Recuperare i risultati dell&#39;operazione**

Dopo che il servizio Output ha eseguito un&#39;operazione, restituisce vari elementi di dati, ad esempio dati XML, che specificano se l&#39;operazione ha avuto esito positivo.

**Consulta anche**

[Creare un documento PDF/A utilizzando l&#39;API Java](creating-document-output-streams.md#create-a-pdf-a-document-using-the-java-api)

[Creare un documento PDF/A utilizzando l&#39;API del servizio Web](creating-document-output-streams.md#create-a-pdf-a-document-using-the-web-service-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API di Output Service](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Creare un documento PDF/A utilizzando l&#39;API Java {#create-a-pdf-a-document-using-the-java-api}

Creare un documento PDF/A utilizzando l&#39;API di output (Java):

1. Includere i file di progetto.

   Includete file JAR client, ad esempio adobe-output-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto Client di output.

   * Creare un `ServiceClientFactory` oggetto che contenga proprietà di connessione.
   * Creare un `OutputClient` oggetto utilizzando il relativo costruttore e passando l&#39; `ServiceClientFactory` oggetto.

1. Fare riferimento a un&#39;origine dati XML.

   * Creare un `java.io.FileInputStream` oggetto che rappresenta l&#39;origine dati XML utilizzata per compilare il documento PDF/A utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del file XML.
   * Creare un `com.adobe.idp.Document` oggetto utilizzando il relativo costruttore e passando l&#39; `java.io.FileInputStream` oggetto.

1. Impostare le opzioni di esecuzione PDF/A.

   * Creare un `PDFOutputOptionsSpec` oggetto utilizzando il relativo costruttore.
   * Impostare l&#39;opzione URI del file richiamando il `PDFOutputOptionsSpec` metodo dell&#39; `setFileURI` oggetto. Passa un valore di stringa che specifica la posizione del file PDF generato dal servizio Output. L&#39;opzione URI file è relativa al server applicazione J2EE in cui è installato AEM Forms, non al computer client.

1. Impostare le opzioni di esecuzione del rendering.

   * Creare un `RenderOptionsSpec` oggetto utilizzando il relativo costruttore.
   * Impostare il `PDFAConformance` valore richiamando il `RenderOptionsSpec` metodo dell&#39; `setPDFAConformance` oggetto e passando un valore `PDFAConformance` enum che specifica il livello di conformità. Ad esempio, per specificare il livello di conformità A, passare `PDFAConformance.A`.
   * Impostare il `PDFARevisionNumber` valore richiamando il `RenderOptionsSpec` metodo dell&#39; `setPDFARevisionNumber` oggetto e passando `PDFARevisionNumber.Revision_1`.
   >[!NOTE]
   >
   >La versione PDF di un documento PDF/A è 1.4 indipendentemente dal valore specificato per il `RenderOptionsSpec` metodo dell&#39; `setPdfVersion`*oggetto.*

1. Generare un documento PDF/A.

   Creare un documento PDF/A richiamando il metodo dell&#39; `OutputClient` oggetto `generatePDFOutput` e passando i seguenti valori:

   * Un valore `TransformationFormat` di enumerazione. Per generare un documento PDF/A, specificare `TransformationFormat.PDFA`.
   * Una stringa che specifica il nome della struttura del modulo.
   * Una stringa che specifica il livello principale del contenuto in cui si trova la struttura del modulo.
   * Un `PDFOutputOptionsSpec` oggetto che contiene opzioni di esecuzione PDF.
   * Un `RenderOptionsSpec` oggetto che contiene opzioni di esecuzione del rendering.
   * L&#39; `com.adobe.idp.Document` oggetto che contiene l&#39;origine dati XML contenente i dati da unire alla struttura del modulo.
   Il `generatePDFOutput` metodo restituisce un `OutputResult` oggetto che contiene i risultati dell&#39;operazione.

   >[!NOTE]
   >
   >Il metodo `OutputResult` dell&#39; `getRecordLevelMetaDataList` oggetto restituisce `null`.

   >[!NOTE]
   >
   >È inoltre possibile creare un documento PDF/A richiamando il metodo `OutputClient` 2 dell&#39; `generatePDFOutput`oggetto. (Vedere [Trasmissione di documenti in Content Services (obsoleto) al servizio](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)di output.)

1. Recuperare i risultati dell&#39;operazione.

   * Creare un `com.adobe.idp.Document` oggetto che rappresenti lo stato del `generatePDFOutput` metodo richiamando il metodo dell&#39; `OutputResult` oggetto `getStatusDoc` .
   * Creare un `java.io.File` oggetto che conterrà i risultati dell&#39;operazione. Accertatevi che l’estensione del nome del file sia .xml.
   * Richiamare il metodo dell&#39; `com.adobe.idp.Document` oggetto `copyToFile` per copiare il contenuto dell&#39; `com.adobe.idp.Document` oggetto nel file (assicurarsi di utilizzare l&#39; `com.adobe.idp.Document` oggetto restituito dal `getStatusDoc` metodo).
   >[!NOTE]
   >
   >Sebbene il servizio Output scriva il documento PDF/A nella posizione specificata dall&#39;argomento passato al `PDFOutputOptionsSpec` metodo dell&#39; `setFileURI` oggetto, è possibile recuperare il documento PDF/A a livello di programmazione richiamando il metodo dell&#39; `OutputResult` oggetto `getGeneratedDoc` .

**Consulta anche**

[Riepilogo dei passaggi](creating-document-output-streams.md#summary-of-steps)

[Avvio rapido (modalità SOAP): Creazione di un documento PDF/A tramite l&#39;API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-a-document-using-the-java-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)di connessione.

### Creare un documento PDF/A utilizzando l&#39;API del servizio Web {#create-a-pdf-a-document-using-the-web-service-api}

Creare un documento PDF/A utilizzando l&#39;API di Output (servizio Web):

1. Includere i file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituire `localhost` con l&#39;indirizzo IP del server in cui è installato AEM Forms.

1. Creare un oggetto Client di output.

   * Creare un `OutputServiceClient` oggetto utilizzando il relativo costruttore predefinito.
   * Creare un `OutputServiceClient.Endpoint.Address` oggetto utilizzando il `System.ServiceModel.EndpointAddress` costruttore. Passa un valore di stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/OutputService?blob=mtom`.) Non è necessario utilizzare l&#39; `lc_version` attributo. Questo attributo viene utilizzato quando create un riferimento a un servizio. Tuttavia, specificate `?blob=mtom` per utilizzare MTOM.
   * Creare un `System.ServiceModel.BasicHttpBinding` oggetto ottenendo il valore del `OutputServiceClient.Endpoint.Binding` campo. Inserite il valore restituito in `BasicHttpBinding`.
   * Impostare il campo `System.ServiceModel.BasicHttpBinding` dell&#39; `MessageEncoding` oggetto su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilitate l&#39;autenticazione HTTP di base eseguendo le seguenti operazioni:

      * Assegnare il nome utente dei moduli AEM al campo `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `OutputServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Fare riferimento a un&#39;origine dati XML.

   * Creare un `BLOB` oggetto utilizzando il relativo costruttore. L&#39; `BLOB` oggetto viene utilizzato per memorizzare i dati che verranno uniti al documento PDF/A.
   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF da cifrare e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto dell&#39; `System.IO.FileStream` oggetto. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà dell&#39; `System.IO.FileStream` oggetto `Length` .
   * Compilare l&#39;array di byte con i dati del flusso richiamando il `System.IO.FileStream` `Read` metodo dell&#39;oggetto e passando l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39; `BLOB` oggetto assegnando il relativo `MTOM` campo con il contenuto dell&#39;array di byte.

1. Impostare le opzioni di esecuzione PDF/A.

   * Creare un `PDFOutputOptionsSpec` oggetto utilizzando il relativo costruttore.
   * Impostare l&#39;opzione URI del file assegnando un valore di stringa che specifica la posizione del file PDF generato dal servizio Output al membro `PDFOutputOptionsSpec` dati dell&#39; `fileURI` oggetto. L&#39;opzione URI file è relativa al server applicazione J2EE in cui è installato AEM Forms, non al computer client

1. Impostare le opzioni di esecuzione del rendering.

   * Creare un `RenderOptionsSpec` oggetto utilizzando il relativo costruttore.
   * Impostare il `PDFAConformance` valore assegnando un valore `PDFAConformance` enum al membro dati dell&#39; `RenderOptionsSpec` oggetto `PDFAConformance` . Ad esempio, per specificare il livello di conformità A, assegnare `PDFAConformance.A` a questo membro dati.
   * Impostare il `PDFARevisionNumber` valore assegnando un valore `PDFARevisionNumber` enum al membro dati dell&#39; `RenderOptionsSpec` oggetto `PDFARevisionNumber` . Assegna `PDFARevisionNumber.Revision_1` a questo membro dati.
   >[!NOTE]
   >
   >La versione PDF di un documento PDF/A è 1.4 indipendentemente dal valore specificato.

1. Generare un documento PDF/A.

   Creare un documento PDF richiamando il `OutputServiceService` `generatePDFOutput`metodo dell&#39;oggetto e passando i seguenti valori:

   * Un valore di enumerazione TransformationFormat. Per generare un documento PDF, specificare `TransformationFormat.PDFA`.
   * Una stringa che specifica il nome della struttura del modulo.
   * Una stringa che specifica il livello principale del contenuto in cui si trova la struttura del modulo.
   * Un `PDFOutputOptionsSpec` oggetto che contiene opzioni di esecuzione PDF.
   * Un `RenderOptionsSpec` oggetto che contiene opzioni di esecuzione del rendering.
   * L&#39; `BLOB` oggetto che contiene l&#39;origine dati XML contenente i dati da unire alla struttura del modulo.
   * Un `BLOB` oggetto popolato dal `generatePDFOutput` metodo. Il `generatePDFOutput` metodo popola l&#39;oggetto con i metadati generati che descrivono il documento. Questo valore di parametro è richiesto solo per la chiamata al servizio Web.
   * Un `BLOB` oggetto popolato dal `generatePDFOutput` metodo. Il `generatePDFOutput` metodo popola l&#39;oggetto con i dati dei risultati. Questo valore di parametro è richiesto solo per la chiamata al servizio Web.
   * Un `OutputResult` oggetto che contiene i risultati dell&#39;operazione. Questo valore di parametro è richiesto solo per la chiamata al servizio Web.
   >[!NOTE]
   >
   >È inoltre possibile creare un documento PDF/A richiamando il metodo `OutputClient` 2 dell&#39; `generatePDFOutput`oggetto. (Vedere [Trasmissione di documenti in Content Services (obsoleto) al servizio](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)di output.)

1. Recuperare i risultati dell&#39;operazione.

   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore di stringa che rappresenta un percorso di file XML contenente i dati dei risultati. Accertatevi che l’estensione del nome del file sia .xml.
   * Creare un array di byte che memorizza il contenuto dei dati dell&#39; `BLOB` oggetto compilato con i dati dei risultati dal `OutputServiceService` metodo dell&#39; `generatePDFOutput` oggetto (ottavo parametro). Compilare l&#39;array di byte ottenendo il valore del campo dell&#39; `BLOB` oggetto `MTOM` .
   * Creare un `System.IO.BinaryWriter` oggetto richiamando il relativo costruttore e passando l&#39; `System.IO.FileStream` oggetto.
   * Scrivere il contenuto dell&#39;array di byte nel file XML richiamando il metodo dell&#39; `System.IO.BinaryWriter` oggetto `Write` e passando l&#39;array di byte.

**Consulta anche**

[Riepilogo dei passaggi](creating-document-output-streams.md#summary-of-steps)

[Attivazione di moduli AEM tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamo di moduli AEM con SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Invio di documenti in Content Services (obsoleto) al servizio di output {#passing-documents-located-in-content-services-deprecated-to-the-output-service}

Il servizio Output esegue il rendering di un modulo PDF non interattivo basato su una struttura del modulo generalmente salvata come file XDP e creata in Designer. È possibile trasmettere al servizio Output un oggetto `com.adobe.idp.Document` che contiene la struttura del modulo. Il servizio Output esegue quindi il rendering della struttura del modulo situata nell&#39; `com.adobe.idp.Document` oggetto.

Il vantaggio di passare un `com.adobe.idp.Document` oggetto al servizio Output è rappresentato dal fatto che altre operazioni del servizio AEM Forms restituiscono un&#39; `com.adobe.idp.Document` istanza. In altre parole, potete ottenere un’ `com.adobe.idp.Document` istanza da un’altra operazione del servizio ed eseguirne il rendering. Ad esempio, si supponga che un file XDP sia memorizzato in un nodo Content Services (obsoleto) denominato `/Company Home/Form Designs`, come illustrato nell&#39;illustrazione seguente.

È possibile recuperare Loan.xdp da Content Services (obsoleto) a livello di programmazione e passare il file XDP al servizio Output all&#39;interno di un `com.adobe.idp.Document` oggetto.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Forms, consultate Riferimento [servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-2}

Per passare un documento ottenuto da Content Services (obsoleto) al servizio Output, eseguire le operazioni seguenti:

1. Includere i file di progetto.
1. Creare un oggetto Output e un oggetto Document Management Client API.
1. Recuperare la struttura del modulo da Content Services (obsoleto).
1. Eseguire il rendering del modulo PDF non interattivo.
1. Eseguire un&#39;azione con il flusso di dati.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, includete i file proxy.

**Creare un oggetto Output e un oggetto API client Document Management**

Prima di eseguire un&#39;operazione API del servizio Output a livello di programmazione, creare un oggetto API Client Output. Inoltre, poiché questo flusso di lavoro recupera un file XDP da Content Services (obsoleto), create un oggetto API Document Management.

**Recuperare la struttura del modulo da Content Services (obsoleto)**

Recuperate il file XDP da Content Services (obsoleto) utilizzando l&#39;API Java o del servizio Web. Il file XDP viene restituito all&#39;interno di un&#39; `com.adobe.idp.Document` istanza (o di un&#39; `BLOB` istanza se si utilizzano i servizi Web). È quindi possibile passare l&#39; `com.adobe.idp.Document` istanza al servizio Output.

**Rendering del modulo PDF non interattivo**

Per eseguire il rendering di un modulo non interattivo, passare l&#39; `com.adobe.idp.Document` istanza restituita da Content Services (obsoleto) al servizio Output.

>[!NOTE]
>
>Due nuovi metodi denominati `generatePDFOutput2`e g `eneratePrintedOutput2`accettano un `com.adobe.idp.Document` oggetto contenente una struttura del modulo. È inoltre possibile trasmettere al servizio Output una struttura del modulo `com.adobe.idp.Document`contenente la struttura del modulo durante l&#39;invio di un flusso di stampa a una stampante di rete.

**Eseguire un&#39;azione con il flusso di dati del modulo**

È possibile salvare il modulo non interattivo come file PDF. Il modulo può essere visualizzato in Adobe Reader o Acrobat.

**Consulta anche**

[Trasmettere i documenti al servizio di output mediante l&#39;API Java](creating-document-output-streams.md#pass-documents-to-the-output-service-using-the-java-api)

[Trasmettere i documenti al servizio di output mediante l&#39;API del servizio Web](creating-document-output-streams.md#pass-documents-to-the-output-service-using-the-web-service-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API di Output Service](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

[Creazione di documenti PDF tramite frammenti](creating-document-output-streams.md#creating-pdf-documents-using-fragments)

### Trasmettere i documenti al servizio di output mediante l&#39;API Java {#pass-documents-to-the-output-service-using-the-java-api}

Trasferite un documento recuperato da Content Services (obsoleto) utilizzando il servizio di output e Content Services (obsoleto) API (Java):

1. Includere i file di progetto.

   Includete file JAR client, ad esempio adobe-output-client.jar e adobe-contentservices-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto Output e un oggetto Document Management Client API.

   * Creare un `ServiceClientFactory` oggetto che contenga proprietà di connessione. (Vedere [Impostazione delle proprietà](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)di connessione.)
   * Creare un `OutputClient` oggetto utilizzando il relativo costruttore e passando l&#39; `ServiceClientFactory` oggetto.
   * Creare un `DocumentManagementServiceClientImpl` oggetto utilizzando il relativo costruttore e passando l&#39; `ServiceClientFactory` oggetto.

1. Recuperare la struttura del modulo da Content Services (obsoleto).

   Richiama il metodo dell’ `DocumentManagementServiceClientImpl` oggetto `retrieveContent` e passa i seguenti valori:

   * Valore stringa che specifica lo store in cui viene aggiunto il contenuto. Lo store predefinito è `SpacesStore`. Questo valore è un parametro obbligatorio.
   * Un valore di stringa che specifica il percorso completo del contenuto da recuperare (ad esempio, `/Company Home/Form Designs/Loan.xdp`). Questo valore è un parametro obbligatorio.
   * Un valore di stringa che specifica la versione. Questo valore è un parametro facoltativo e potete trasmettere una stringa vuota. In questa situazione, viene recuperata la versione più recente.
   Il `retrieveContent` metodo restituisce un `CRCResult` oggetto che contiene il file XDP. Recuperare un&#39; `com.adobe.idp.Document` istanza richiamando il `CRCResult` metodo dell&#39; `getDocument` oggetto.

1. Eseguire il rendering del modulo PDF non interattivo.

   Richiama il metodo dell’ `OutputClient` oggetto `generatePDFOutput2` e passa i seguenti valori:

   * Un valore `TransformationFormat` di enumerazione. Per generare un documento PDF, specificare `TransformationFormat.PDF`.
   * Una stringa che specifica la radice del contenuto in cui si trovano le risorse aggiuntive, come le immagini.
   * Un `com.adobe.idp.Document` oggetto che rappresenta la struttura del modulo (utilizzare l&#39;istanza restituita dal `CRCResult` metodo dell&#39;oggetto `getDocument` ).
   * Un `PDFOutputOptionsSpec` oggetto che contiene opzioni di esecuzione PDF.
   * Un `RenderOptionsSpec` oggetto che contiene opzioni di esecuzione del rendering.
   * L&#39; `com.adobe.idp.Document` oggetto che contiene l&#39;origine dati XML contenente i dati da unire alla struttura del modulo.
   Il `generatePDFOutput2` metodo restituisce un `OutputResult` oggetto che contiene i risultati dell&#39;operazione.

1. Eseguire un&#39;azione con il flusso di dati del modulo.

   * Recuperare un `com.adobe.idp.Document` oggetto che rappresenta il modulo non interattivo richiamando il `OutputResult` metodo dell&#39;oggetto `getGeneratedDoc` .
   * Creare un `java.io.File` oggetto che contenga i risultati dell&#39;operazione. Accertatevi che l’estensione del nome file sia .pdf.
   * Richiamare il metodo dell&#39; `com.adobe.idp.Document` oggetto `copyToFile` per copiare il contenuto dell&#39; `com.adobe.idp.Document` oggetto nel file (assicurarsi di utilizzare l&#39; `com.adobe.idp.Document` oggetto restituito dal `getGeneratedDoc` metodo).

**Consulta anche**

[Riepilogo dei passaggi](creating-document-output-streams.md#summary-of-steps)

[Avvio rapido (modalità EJB): Trasmissione di documenti al servizio di output tramite l&#39;API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-documents-to-the-output-service-using-the-java-api)

[Avvio rapido (modalità SOAP): Trasmissione di documenti al servizio di output tramite l&#39;API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-documents-to-the-output-service-using-the-java-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Trasmettere i documenti al servizio di output mediante l&#39;API del servizio Web {#pass-documents-to-the-output-service-using-the-web-service-api}

Trasferite un documento recuperato da Content Services (obsoleto) utilizzando il servizio di output e Content Services (obsoleto) API (servizio Web):

1. Includere i file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Poiché questa applicazione client richiama due servizi AEM Forms, create due riferimenti al servizio. Utilizzare la seguente definizione WSDL per il riferimento al servizio associato al servizio Output: `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   Utilizzate la seguente definizione WSDL per il riferimento al servizio associato al servizio Document Management: `http://localhost:8080/soap/services/DocumentManagementService?WSDL&lc_version=9.0.1`.

   Poiché il tipo di `BLOB` dati è comune a entrambi i riferimenti di servizio, è necessario qualificare completamente il tipo di `BLOB` dati quando viene utilizzato. Nella procedura di avvio rapido del servizio Web corrispondente, tutte `BLOB` le istanze sono completamente qualificate.

   >[!NOTE]
   >
   >Sostituire `localhost` con l&#39;indirizzo IP del server in cui è installato AEM Forms.

1. Creare un oggetto Output e un oggetto Document Management Client API.

   * Creare un `OutputServiceClient` oggetto utilizzando il relativo costruttore predefinito.
   * Creare un `OutputServiceClient.Endpoint.Address` oggetto utilizzando il `System.ServiceModel.EndpointAddress` costruttore. Trasmettere un valore di stringa che specifica il WSDL al servizio Forms (ad esempio, `http://localhost:8080/soap/services/OutputService?blob=mtom`). Non è necessario utilizzare l&#39; `lc_version` attributo. Questo attributo viene utilizzato quando create un riferimento a un servizio.
   * Creare un `System.ServiceModel.BasicHttpBinding` oggetto ottenendo il valore del `OutputServiceClient.Endpoint.Binding` campo. Inserite il valore restituito in `BasicHttpBinding`.
   * Impostare il campo `System.ServiceModel.BasicHttpBinding` dell&#39; `MessageEncoding` oggetto su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilitate l&#39;autenticazione HTTP di base eseguendo le seguenti operazioni:

      * Assegnare il nome utente dei moduli AEM al campo `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `OutputServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.
   >[!NOTE]
   >
   >Ripetete questi passaggi per il client di `DocumentManagementServiceClient`servizio.

1. Recuperare la struttura del modulo da Content Services (obsoleto).

   Recuperare il contenuto richiamando il metodo dell&#39; `DocumentManagementServiceClient` oggetto `retrieveContent` e passando i seguenti valori:

   * Valore stringa che specifica lo store in cui viene aggiunto il contenuto. Lo store predefinito è `SpacesStore`. Questo valore è un parametro obbligatorio.
   * Un valore di stringa che specifica il percorso completo del contenuto da recuperare (ad esempio, `/Company Home/Form Designs/Loan.xdp`). Questo valore è un parametro obbligatorio.
   * Un valore di stringa che specifica la versione. Questo valore è un parametro facoltativo e potete trasmettere una stringa vuota. In questa situazione, viene recuperata la versione più recente.
   * Un parametro di output della stringa che memorizza il valore del collegamento di ricerca.
   * Un parametro di `BLOB` output che memorizza il contenuto. Potete usare questo parametro di output per recuperare il contenuto.
   * Un parametro `ServiceReference1.MyMapOf_xsd_string_To_xsd_anyType` di output che memorizza gli attributi di contenuto.
   * Un parametro `CRCResult` di output. Invece di utilizzare questo oggetto, potete utilizzare il parametro `BLOB` output per recuperare il contenuto.

1. Eseguire il rendering del modulo PDF non interattivo.

   Richiama il metodo dell’ `OutputServiceClient` oggetto `generatePDFOutput2` e passa i seguenti valori:

   * Un valore `TransformationFormat` di enumerazione. Per generare un documento PDF, specificare `TransformationFormat.PDF`.
   * Una stringa che specifica la radice del contenuto in cui si trovano le risorse aggiuntive, come le immagini.
   * Un oggetto `BLOB` che rappresenta la struttura del modulo (utilizzare l&#39; `BLOB` istanza restituita da Content Services (obsoleto)).
   * Un `PDFOutputOptionsSpec` oggetto che contiene opzioni di esecuzione PDF.
   * Un `RenderOptionsSpec` oggetto che contiene opzioni di esecuzione del rendering.
   * L&#39; `BLOB` oggetto che contiene l&#39;origine dati XML contenente i dati da unire alla struttura del modulo.
   * Un oggetto di output `BLOB` compilato dal `generatePDFOutput2` metodo. Il `generatePDFOutput2` metodo popola l&#39;oggetto con i metadati generati che descrivono il documento. (Questo valore di parametro è richiesto solo per la chiamata al servizio Web).
   * Un `OutputResult` oggetto di output che contiene i risultati dell&#39;operazione. (Questo valore di parametro è richiesto solo per la chiamata al servizio Web).
   Il `generatePDFOutput2` metodo restituisce un `BLOB` oggetto che contiene il modulo PDF non interattivo.

1. Eseguire un&#39;azione con il flusso di dati del modulo.

   * Creare un `System.IO.FileStream` oggetto richiamandone il costruttore. Passare un valore di stringa che rappresenta la posizione del file del documento PDF interattivo e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto dell&#39; `BLOB` oggetto recuperato dal `generatePDFOutput2` metodo. Compilare l&#39;array di byte ottenendo il valore del membro `BLOB` dati dell&#39; `MTOM` oggetto.
   * Creare un `System.IO.BinaryWriter` oggetto richiamando il relativo costruttore e passando l&#39; `System.IO.FileStream` oggetto.
   * Scrivere il contenuto dell&#39;array di byte in un file PDF richiamando il metodo dell&#39; `System.IO.BinaryWriter` oggetto `Write` e passando l&#39;array di byte.

**Consulta anche**

[Riepilogo dei passaggi](creating-document-output-streams.md#summary-of-steps)

[Attivazione di moduli AEM tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## Trasmissione di documenti situati nell&#39;archivio al servizio di output {#passing-documents-located-in-the-repository-to-the-output-service}

Il servizio Output esegue il rendering di un modulo PDF non interattivo basato su una struttura del modulo generalmente salvata come file XDP e creata in Designer. È possibile trasmettere al servizio Output un oggetto `com.adobe.idp.Document` che contiene la struttura del modulo. Il servizio Output esegue quindi il rendering della struttura del modulo situata nell&#39; `com.adobe.idp.Document` oggetto.

Il vantaggio di passare un `com.adobe.idp.Document` oggetto al servizio Output è rappresentato dal fatto che altre operazioni del servizio AEM Forms restituiscono un&#39; `com.adobe.idp.Document` istanza. In altre parole, potete ottenere un’ `com.adobe.idp.Document` istanza da un’altra operazione del servizio ed eseguirne il rendering. Ad esempio, si supponga che un file XDP sia memorizzato nell&#39;archivio di AEM Forms, come illustrato nell&#39;illustrazione seguente.

![pd_pd_formrepository](assets/pd_pd_formrepository.png)

La cartella *FormsFolder* è un percorso definito dall&#39;utente nell&#39;archivio di AEM Forms (questo è un esempio e non esiste per impostazione predefinita). In questo esempio, in questa cartella si trova una struttura del modulo denominata Loan.xdp. Oltre alla struttura del modulo, in questa posizione è possibile memorizzare altre risorse del modulo, come le immagini. Il percorso di una risorsa situata nell&#39;archivio di AEM Forms è:

`Applications/Application-name/Application-version/Folder.../Filename`

È possibile recuperare Loan.xdp a livello di programmazione dall&#39;archivio di AEM Forms e passarlo al servizio Output all&#39;interno di un `com.adobe.idp.Document` oggetto.

È possibile creare un PDF basato su un file XDP presente nella directory archivio in uno dei due modi disponibili. È possibile passare la posizione XDP tramite riferimento oppure recuperare l&#39;XDP dal repository a livello di programmazione e passarlo al servizio Output all&#39;interno di un file XDP.

[Avvio rapido (modalità EJB): La creazione di un documento PDF basato su un file XDP dell&#39;applicazione mediante l&#39;API](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-an-application-xdp-file-using-the-java-api) Java (mostra come passare la posizione del file XDP per riferimento).

[Avvio rapido (modalità EJB): Trasmissione di un documento che si trova nell&#39;archivio AEM Forms al servizio Output tramite l&#39;API](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-a-document-located-in-the-repository-to-the-output-service-using-the-java-api) Java (mostra come recuperare il file XDP dall&#39;archivio dei moduli AEM a livello di programmazione e trasmetterlo al servizio Output all&#39;interno di un&#39; `com.adobe.idp.Document` istanza). (Questa sezione descrive come eseguire questa attività)

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Forms, consultate Riferimento [servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-3}

Per trasmettere al servizio Output un documento ottenuto dall&#39;archivio di AEM Forms, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un oggetto Output e un oggetto Document Management Client API.
1. Recuperare la struttura del modulo dall&#39;archivio di AEM Forms.
1. Eseguire il rendering del modulo PDF non interattivo.
1. Eseguire un&#39;azione con il flusso di dati.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, includete i file proxy.

**Creare un oggetto Output e un oggetto API client Document Management**

Prima di eseguire un&#39;operazione API del servizio Output a livello di programmazione, creare un oggetto API Client Output. Inoltre, poiché questo flusso di lavoro recupera un file XDP da Content Services (obsoleto), create un oggetto API Document Management.

**Recuperare la struttura del modulo dall&#39;archivio moduli di AEM**

Recuperare il file XDP dall&#39;archivio dei moduli AEM utilizzando l&#39;API Repository. (Vedere Risorse [di](/help/forms/developing/aem-forms-repository.md#reading-resources)lettura.)

Il file XDP viene restituito all&#39;interno di un&#39; `com.adobe.idp.Document` istanza (o di un&#39; `BLOB` istanza se si utilizzano i servizi Web). È quindi possibile passare l&#39; `com.adobe.idp.Document` istanza al servizio Output.

**Rendering del modulo PDF non interattivo**

Per eseguire il rendering di un modulo non interattivo, passare l&#39; `com.adobe.idp.Document` istanza restituita utilizzando l&#39;API Repository di AEM Forms.

>[!NOTE]
>
>Due nuovi metodi denominati `generatePDFOutput2`e `generatePrintedOutput2`accettano un `com.adobe.idp.Document`oggetto contenente una struttura del modulo. È inoltre possibile trasmettere al servizio Output una struttura del modulo `com.adobe.idp.Document` contenente la struttura del modulo durante l&#39;invio di un flusso di stampa a una stampante di rete.

**Eseguire un&#39;azione con il flusso di dati del modulo**

È possibile salvare il modulo non interattivo come file PDF. Il modulo può essere visualizzato in Adobe Reader o Acrobat.

**Consulta anche**

[Trasmettere al servizio di output i documenti che si trovano nell&#39;archivio tramite l&#39;API Java](creating-document-output-streams.md#pass-documents-located-in-the-repository-to-the-output-service-using-the-java-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API di Output Service](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

ResourceRepositoryClient

### Trasmettere al servizio di output i documenti che si trovano nell&#39;archivio tramite l&#39;API Java {#pass-documents-located-in-the-repository-to-the-output-service-using-the-java-api}

Trasmettere un documento recuperato dall&#39;archivio utilizzando il servizio Output e l&#39;API Repository (Java):

1. Includere i file di progetto.

   Includete file JAR client, come adobe-output-client.jar e adobe-repository-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto Output e un oggetto Document Management Client API.

   * Creare un `ServiceClientFactory` oggetto che contenga proprietà di connessione. (Vedere [Impostazione delle proprietà](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)di connessione.)
   * Creare un `OutputClient` oggetto utilizzando il relativo costruttore e passando l&#39; `ServiceClientFactory` oggetto.
   * Creare un `DocumentManagementServiceClientImpl` oggetto utilizzando il relativo costruttore e passando l&#39; `ServiceClientFactory` oggetto.

1. Recuperare la struttura del modulo dall&#39;archivio moduli di AEM.

   Richiamare il metodo dell&#39; `ResourceRepositoryClient` oggetto `readResourceContent` e passare un valore di stringa che specifica la posizione URI del file XDP. Esempio, `/Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`. Questo valore è obbligatorio. Questo metodo restituisce un&#39; `com.adobe.idp.Document` istanza che rappresenta il file XDP.

1. Eseguire il rendering del modulo PDF non interattivo.

   Richiama il metodo dell’ `OutputClient` oggetto `generatePDFOutput2` e passa i seguenti valori:

   * Un valore `TransformationFormat` di enumerazione. Per generare un documento PDF, specificare `TransformationFormat.PDF`.
   * Una stringa che specifica la radice del contenuto in cui si trovano le risorse aggiuntive, come le immagini. Esempio, `repository:///Applications/FormsApplication/1.0/FormsFolder/`.
   * Un `com.adobe.idp.Document` oggetto che rappresenta la struttura del modulo (utilizzare l&#39;istanza restituita dal `ResourceRepositoryClient` metodo dell&#39;oggetto `readResourceContent` ).
   * Un `PDFOutputOptionsSpec` oggetto che contiene opzioni di esecuzione PDF.
   * Un `RenderOptionsSpec` oggetto che contiene opzioni di esecuzione del rendering.
   * L&#39; `com.adobe.idp.Document` oggetto che contiene l&#39;origine dati XML contenente i dati da unire alla struttura del modulo.
   Il `generatePDFOutput2` metodo restituisce un `OutputResult` oggetto che contiene i risultati dell&#39;operazione.

1. Eseguire un&#39;azione con il flusso di dati del modulo.

   * Recuperare un `com.adobe.idp.Document` oggetto che rappresenta il modulo non interattivo richiamando il `OutputResult` metodo dell&#39;oggetto `getGeneratedDoc` .
   * Creare un `java.io.File` oggetto che contenga i risultati dell&#39;operazione. Accertatevi che l’estensione del nome file sia .pdf.
   * Richiamare il metodo dell&#39; `com.adobe.idp.Document` oggetto `copyToFile` per copiare il contenuto dell&#39; `com.adobe.idp.Document` oggetto nel file (assicurarsi di utilizzare l&#39; `com.adobe.idp.Document` oggetto restituito dal `getGeneratedDoc` metodo).

**Consulta anche**

[Riepilogo dei passaggi](creating-document-output-streams.md#summary-of-steps)

[Avvio rapido (modalità EJB): Trasmissione di un documento situato nell&#39;archivio moduli AEM al servizio Output tramite l&#39;API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-a-document-located-in-the-repository-to-the-output-service-using-the-java-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Creazione di documenti PDF tramite frammenti {#creating-pdf-documents-using-fragments}

È possibile utilizzare i servizi Output e Assembler per creare un flusso di output, ad esempio un documento PDF, basato su frammenti. Il servizio Assembler assembla un documento XDP basato su frammenti presenti in più file XDP. Il documento XDP assemblato viene passato al servizio Output, che crea un documento PDF. Anche se questo flusso di lavoro mostra un documento PDF generato, il servizio Output può generare altri tipi di output, come ZPL, per questo flusso di lavoro. Un documento PDF è utilizzato solo a scopo di discussione.

L&#39;illustrazione seguente mostra questo flusso di lavoro.

![cp_cp_outputassembleframmenti](assets/cp_cp_outputassemblefragments.png)

Prima di leggere *Creazione di documenti PDF utilizzando i frammenti*, è consigliabile acquisire familiarità con l&#39;uso del servizio Assembler per assemblare più documenti XDP. (Vedere [Assemblaggio Di Più Frammenti](/help/forms/developing/assembling-pdf-documents.md#assembling-multiple-xdp-fragments)XDP.)

>[!NOTE]
>
>È inoltre possibile trasmettere una struttura del modulo assemblata dal servizio Assembler al servizio Forms anziché al servizio Output. La differenza principale tra il servizio Output e il servizio Forms è che il servizio Forms genera documenti PDF interattivi e il servizio Output genera documenti PDF non interattivi. Inoltre, il servizio Forms non è in grado di generare flussi di output basati sulla stampante come ZPL.

>[!NOTE]
>
> Per ulteriori informazioni sul servizio Output, consultate Riferimento [servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-4}

Per creare un documento PDF basato sui frammenti, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un oggetto Client di Output e Assembler.
1. Utilizzare il servizio Assembler per generare la struttura del modulo.
1. Utilizzare il servizio Output per generare il documento PDF.
1. Salvare il documento PDF come file PDF.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate servizi Web, accertatevi di includere i file proxy.

**Creare un oggetto Client di Output e Assembler**

Prima di eseguire un&#39;operazione API del servizio Output a livello di programmazione, creare un oggetto API Client Output. Inoltre, poiché questo flusso di lavoro richiama il servizio Assembler per creare la struttura del modulo, creare un oggetto API Client Assembler.

**Utilizzare il servizio Assembler per generare la struttura del modulo**

Utilizzare il servizio Assembler per generare la struttura del modulo utilizzando i frammenti. Il servizio Assembler restituisce un&#39; `com.adobe.idp.Document` istanza che contiene la struttura del modulo.

**Utilizzare il servizio Output per generare il documento PDF**

È possibile utilizzare il servizio Output per generare un documento PDF utilizzando la struttura del modulo creata dal servizio Assembler. Passare l&#39; `com.adobe.idp.Document` istanza restituita dal servizio Assembler al servizio Output.

**Salvare il documento PDF come file PDF**

Dopo che il servizio Output ha generato un documento PDF, è possibile salvarlo come file PDF.

**Consulta anche**

[Creazione di un documento PDF basato su frammenti tramite l&#39;API Java](creating-document-output-streams.md#create-a-pdf-document-based-on-fragments-using-the-java-api)

[Creazione di un documento PDF basato su frammenti tramite l&#39;API del servizio Web](creating-document-output-streams.md#create-a-pdf-document-based-on-fragments-using-the-web-service-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API di Output Service](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

[Assemblare Più Frammenti XDP](/help/forms/developing/assembling-pdf-documents.md#assembling-multiple-xdp-fragments)

[Creazione di documenti PDF](creating-document-output-streams.md#creating-pdf-documents)

### Creazione di un documento PDF basato su frammenti tramite l&#39;API Java {#create-a-pdf-document-based-on-fragments-using-the-java-api}

Creare un documento PDF basato sui frammenti utilizzando l&#39;API di Output Service e l&#39;API di Assembler Service (Java):

1. Includere i file di progetto.

   Includete file JAR client, ad esempio adobe-output-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto Client di Output e Assembler.

   * Creare un `ServiceClientFactory` oggetto che contenga proprietà di connessione.
   * Creare un `OutputClient` oggetto utilizzando il relativo costruttore e passando l&#39; `ServiceClientFactory` oggetto.
   * Creare un `AssemblerServiceClient` oggetto utilizzando il relativo costruttore e passando l&#39; `ServiceClientFactory` oggetto.

1. Utilizzare il servizio Assembler per generare la struttura del modulo.

   Richiamare il metodo dell&#39; `AssemblerServiceClient` oggetto `invokeDDX` e trasmettere i seguenti valori obbligatori:

   * Un `com.adobe.idp.Document` oggetto che rappresenta il documento DDX da utilizzare.
   * Un `java.util.Map` oggetto che contiene i file XDP di input.
   * Un `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` oggetto che specifica le opzioni di esecuzione, incluso il font predefinito e il livello di registro del processo.
   Il `invokeDDX` metodo restituisce un `com.adobe.livecycle.assembler.client.AssemblerResult` oggetto che contiene il documento XDP assemblato. Per recuperare il documento XDP assemblato, eseguire le operazioni seguenti:

   * Richiama il metodo dell’ `AssemblerResult` oggetto `getDocuments` . Questo metodo restituisce un `java.util.Map` oggetto.
   * Iterare l&#39; `java.util.Map` oggetto fino a individuare l&#39; `com.adobe.idp.Document` oggetto risultante.
   * Richiamare il metodo dell&#39; `com.adobe.idp.Document` oggetto `copyToFile` per estrarre il documento XDP assemblato.


1. Utilizzare il servizio Output per generare il documento PDF.

   Richiama il metodo dell’ `OutputClient` oggetto `generatePDFOutput2` e passa i seguenti valori:

   * Un valore `TransformationFormat` di enumerazione. Per generare un documento PDF, specificare `TransformationFormat.PDF`
   * Una stringa che specifica la radice del contenuto in cui si trovano le risorse aggiuntive, come le immagini
   * Un `com.adobe.idp.Document` oggetto che rappresenta la struttura del modulo (utilizzare l&#39;istanza restituita dal servizio Assembler)
   * Un `PDFOutputOptionsSpec` oggetto che contiene le opzioni di esecuzione PDF
   * Un oggetto `RenderOptionsSpec` che contiene le opzioni di esecuzione del rendering
   * L&#39; `com.adobe.idp.Document` oggetto che contiene l&#39;origine dati XML contenente i dati da unire alla struttura del modulo
   Il `generatePDFOutput2` metodo restituisce un `OutputResult` oggetto che contiene i risultati dell&#39;operazione

1. Salvare il documento PDF come file PDF.

   * Recuperare un `com.adobe.idp.Document` oggetto che rappresenta il documento PDF richiamando il `OutputResult` metodo dell&#39; `getGeneratedDoc` oggetto.
   * Creare un `java.io.File` oggetto che contenga i risultati dell&#39;operazione. Accertatevi che l’estensione del nome file sia .pdf.
   * Richiamare il metodo dell&#39; `com.adobe.idp.Document` oggetto `copyToFile` per copiare il contenuto dell&#39; `com.adobe.idp.Document` oggetto nel file. Assicurarsi di utilizzare l&#39; `com.adobe.idp.Document` oggetto restituito dal `getGeneratedDoc` metodo.

**Consulta anche**

[Riepilogo dei passaggi](creating-document-output-streams.md#summary-of-steps)

[Avvio rapido (modalità EJB): Creazione di un documento PDF basato su frammenti tramite l&#39;API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-fragments-using-the-java-api)

[Avvio rapido (modalità SOAP): Creazione di un documento PDF basato su frammenti tramite l&#39;API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-fragments-using-the-java-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)di connessione.

### Creazione di un documento PDF basato su frammenti tramite l&#39;API del servizio Web {#create-a-pdf-document-based-on-fragments-using-the-web-service-api}

Creare un documento PDF basato sui frammenti utilizzando l&#39;API di Output Service e l&#39;API di Assembler Service (servizio Web):

1. Includere i file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Utilizzare la seguente definizione WSDL per il riferimento al servizio associato al servizio Output:

   ```as3
    http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1.
   ```

   Utilizzate la seguente definizione WSDL per il riferimento al servizio associato al servizio Assembler:

   ```as3
    http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1.
   ```

   Poiché il tipo di `BLOB` dati è comune a entrambi i riferimenti di servizio, è necessario qualificare completamente il tipo di `BLOB` dati quando viene utilizzato. Nella procedura di avvio rapido del servizio Web corrispondente, tutte `BLOB` le istanze sono completamente qualificate.

   >[!NOTE]
   >
   >Sostituire `localhost` con l&#39;indirizzo IP del server in cui è installato AEM Forms.

1. Creare un oggetto Client di Output e Assembler.

   * Creare un `OutputServiceClient` oggetto utilizzando il relativo costruttore predefinito.
   * Creare un `OutputServiceClient.Endpoint.Address` oggetto utilizzando il `System.ServiceModel.EndpointAddress` costruttore. Passa un valore di stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/OutputService?blob=mtom`.) Non è necessario utilizzare l&#39; `lc_version` attributo. Questo attributo viene utilizzato quando create un riferimento a un servizio. Tuttavia, specificate `?blob=mtom` per utilizzare MTOM.
   * Creare un `System.ServiceModel.BasicHttpBinding` oggetto ottenendo il valore del `OutputServiceClient.Endpoint.Binding` campo. Inserite il valore restituito in `BasicHttpBinding`.
   * Impostare il campo `System.ServiceModel.BasicHttpBinding` dell&#39; `MessageEncoding` oggetto su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilitate l&#39;autenticazione HTTP di base eseguendo le seguenti operazioni:

      * Assegnare il nome utente dei moduli AEM al `OutputServiceClient.ClientCredentials.UserName.UserName`campo.
      * Assegnare il valore della password corrispondente al `OutputServiceClient.ClientCredentials.UserName.Password`campo.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al `BasicHttpBindingSecurity.Transport.ClientCredentialType`campo.
   * Assegnare il valore `BasicHttpSecurityMode.TransportCredentialOnly` costante al `BasicHttpBindingSecurity.Security.Mode`campo.
   >[!NOTE]
   >
   >Ripetere i passaggi indicati per l&#39; `AssemblerServiceClient`oggetto.

1. Utilizzare il servizio Assembler per generare la struttura del modulo.

   Richiama il metodo dell’ `AssemblerServiceClient` oggetto `invokeDDX` e passa i seguenti valori:

   * Un `BLOB` oggetto che rappresenta il documento DDX
   * L&#39; `MyMapOf_xsd_string_To_xsd_anyType` oggetto che contiene i file richiesti
   * Un oggetto `AssemblerOptionSpec` che specifica le opzioni di esecuzione
   Il `invokeDDX` metodo restituisce un `AssemblerResult` oggetto che contiene i risultati del processo ed eventuali eccezioni. Per ottenere il documento XDP appena creato, effettuare le seguenti operazioni:

   * Accedere al campo `AssemblerResult` dell&#39; `documents` oggetto, ovvero un `Map` oggetto che contiene i documenti PDF risultanti.
   * Scorrere l&#39; `Map` oggetto per recuperare la struttura del modulo assemblato. Inserite il membro della matrice `value` in un `BLOB`. Passa questa `BLOB` istanza al servizio Output.


1. Utilizzare il servizio Output per generare il documento PDF.

   Richiama il metodo dell’ `OutputServiceClient` oggetto `generatePDFOutput2` e passa i seguenti valori:

   * Un valore `TransformationFormat` di enumerazione. Per generare un documento PDF, specificare `TransformationFormat.PDF`.
   * Una stringa che specifica la radice del contenuto in cui si trovano le risorse aggiuntive, come le immagini.
   * Un `BLOB` oggetto che rappresenta la struttura del modulo (utilizzare l&#39; `BLOB` istanza restituita dal servizio Assembler).
   * Un `PDFOutputOptionsSpec` oggetto che contiene opzioni di esecuzione PDF.
   * Un `RenderOptionsSpec` oggetto che contiene opzioni di esecuzione del rendering.
   * L&#39; `BLOB` oggetto che contiene l&#39;origine dati XML contenente i dati da unire alla struttura del modulo.
   * Un `BLOB` oggetto di output compilato dal `generatePDFOutput2` metodo. Il `generatePDFOutput2` metodo popola l&#39;oggetto con i metadati generati che descrivono il documento. (Questo valore di parametro è richiesto solo per la chiamata al servizio Web).
   * Un `OutputResult` oggetto di output che contiene i risultati dell&#39;operazione. (Questo valore di parametro è richiesto solo per la chiamata al servizio Web).
   Il `generatePDFOutput2` metodo restituisce un `BLOB` oggetto che contiene il modulo PDF non interattivo.

1. Salvare il documento PDF come file PDF.

   * Creare un `System.IO.FileStream` oggetto richiamandone il costruttore. Passare un valore di stringa che rappresenta la posizione del file del documento PDF interattivo e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto dell&#39; `BLOB` oggetto recuperato dal `generatePDFOutput2` metodo. Compilare l&#39;array di byte ottenendo il valore del membro `BLOB` dati dell&#39; `MTOM` oggetto.
   * Creare un `System.IO.BinaryWriter` oggetto richiamando il relativo costruttore e passando l&#39; `System.IO.FileStream` oggetto.
   * Scrivere il contenuto dell&#39;array di byte in un file PDF richiamando il metodo dell&#39; `System.IO.BinaryWriter` oggetto `Write` e passando l&#39;array di byte.

**Consulta anche**

[Riepilogo dei passaggi](creating-document-output-streams.md#summary-of-steps)

[Attivazione di moduli AEM tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## Stampa su file {#printing-to-files}

È possibile utilizzare il servizio Output per stampare su un file flussi quali PostScript, PCL (Printer Control Language) o i seguenti formati di etichetta:

* Zebra - ZPL
* Intermec - IPL
* Datamax - DPL
* TecToshiba - TPCL

Il servizio Output consente di unire i dati XML a una struttura del modulo e di stampare il modulo su un file. L&#39;illustrazione seguente mostra il servizio Output che crea file laser ed etichette.

>[!NOTE]
>
>Per informazioni sull&#39;invio di flussi di stampa alle stampanti, vedere [Invio di flussi di stampa alle stampanti](creating-document-output-streams.md#sending-print-streams-to-printers).

>[!NOTE]
>
> Per ulteriori informazioni sul servizio Output, consultate Riferimento [servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-5}

Per stampare un file, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un oggetto Client di output.
1. Fare riferimento a un&#39;origine dati XML.
1. Impostare le opzioni di esecuzione della stampa necessarie per stampare su un file.
1. Stampare il flusso di stampa su un file.
1. Recuperare i risultati dell&#39;operazione.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate servizi Web, accertatevi di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è distribuito su JBoss)
* jbossall-client.jar (richiesto se AEM Forms è distribuito su JBoss)

se AEM Forms è distribuito su un server applicazione J2EE supportato che non sia JBoss, dovrete sostituire i file adobe-utilities.jar e jbossall-client.jar con file JAR specifici del server applicazione J2EE su cui è distribuito AEM Forms. (consultate [Inclusione di file](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)libreria Java AEM Forms).

**Creare un oggetto Client di output**

Prima di eseguire un&#39;operazione del servizio Output a livello di programmazione, è necessario creare un oggetto client del servizio Output. Se utilizzate l&#39;API Java, create un `OutputClient` oggetto. Se si utilizza l&#39;API del servizio Web Output, creare un `OutputServiceService` oggetto.

**Riferimento a un&#39;origine dati XML**

Per stampare un documento contenente dati, è necessario fare riferimento a un&#39;origine dati XML che contiene elementi XML per ogni campo del modulo che si desidera compilare con i dati. Il nome dell&#39;elemento XML deve corrispondere al nome del campo. Un elemento XML viene ignorato se non corrisponde a un campo modulo o se il nome dell&#39;elemento XML non corrisponde al nome del campo. Se vengono specificati tutti gli elementi XML, non è necessario stabilire una corrispondenza con l&#39;ordine di visualizzazione degli elementi XML.

**Impostazione delle opzioni di esecuzione della stampa necessarie per stampare su un file**

Per stampare su un file, è necessario impostare l&#39;opzione di esecuzione URI del file specificando la posizione e il nome del file su cui viene stampato il servizio Output. Ad esempio, per indicare al servizio Output di stampare un file PostScript denominato *MortgageForm.ps* su C:\Adobe, specificare C:\Adobe\MortgageForm.ps.

>[!NOTE]
>
>È possibile definire opzioni di runtime facoltative. Per informazioni su tutte le opzioni che è possibile impostare, consultate il riferimento alla `PrintedOutputOptionsSpec` classe nella Guida di riferimento [delle API per](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)AEM Forms.

**Stampare il flusso di stampa su un file**

Dopo aver fatto riferimento a un&#39;origine dati XML valida che contiene i dati del modulo e aver impostato le opzioni di esecuzione della stampa, è possibile richiamare il servizio Output, che causa la stampa di un file.

**Recuperare i risultati dell&#39;operazione**

Dopo l&#39;esecuzione di un&#39;operazione, il servizio Output restituisce vari elementi di dati, ad esempio dati XML, che specificano se l&#39;operazione ha avuto esito positivo.

**Consulta anche**

[Stampa su file tramite l&#39;API Java](creating-document-output-streams.md#print-to-files-using-the-java-api)

[Stampa su file tramite l&#39;API del servizio Web](creating-document-output-streams.md#print-to-files-using-the-web-service-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API di Output Service](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Stampa su file tramite l&#39;API Java {#print-to-files-using-the-java-api}

Stampa su un file tramite l&#39;API di Output (Java):

1. Includere i file di progetto.

   Includete file JAR client, ad esempio adobe-output-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto Client di output.

   * Creare un `ServiceClientFactory` oggetto che contenga proprietà di connessione.
   * Creare un `OutputClient` oggetto utilizzando il relativo costruttore e passando l&#39; `ServiceClientFactory` oggetto.

1. Fare riferimento a un&#39;origine dati XML.

   * Creare un `java.io.FileInputStream` oggetto che rappresenta l&#39;origine dati XML utilizzata per compilare il documento utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del file XML.
   * Creare un `com.adobe.idp.Document` oggetto utilizzando il relativo costruttore e passando l&#39; `java.io.FileInputStream` oggetto.

1. Impostare le opzioni di esecuzione della stampa necessarie per stampare su un file.

   * Creare un `PrintedOutputOptionsSpec` oggetto utilizzando il relativo costruttore.
   * Specificare il file richiamando il metodo dell&#39;oggetto PrintedOutputOptionsSpec `setFileURI` e passando un valore di stringa che rappresenta il nome e la posizione del file. Ad esempio, se si desidera che il servizio Output venga stampato su un file PostScript denominato MortgageForm.ps che si trova in C:\Adobe, specificare C:\\Adobe\MortgageForm.ps.
   * Specificare il numero di copie da stampare richiamando il metodo dell&#39; `PrintedOutputOptionsSpec` oggetto `setCopies` e passando un valore intero che rappresenta il numero di copie.

1. Stampare il flusso di stampa su un file.

   Per stampare su un file, richiamare il metodo dell&#39; `OutputClient` oggetto `generatePrintedOutput` e passare i seguenti valori:

   * Un valore di `PrintFormat` enumerazione che specifica il formato del flusso di stampa da creare. Ad esempio, per creare un flusso di stampa PostScript, passare `PrintFormat.PostScript`.
   * Una stringa che specifica il nome della struttura del modulo.
   * Una stringa che specifica la posizione dei relativi file collaterali, ad esempio i file immagine.
   * Una stringa che specifica la posizione del file XDC da utilizzare (è possibile passare `null` se si specifica il file XDC da utilizzare utilizzando l&#39; `PrintedOutputOptionsSpec` oggetto).
   * L&#39; `PrintedOutputOptionsSpec` oggetto che contiene le opzioni di esecuzione necessarie per la stampa su un file.
   * L&#39; `com.adobe.idp.Document` oggetto che contiene l&#39;origine dati XML contenente i dati del modulo.
   Il `generatePrintedOutput` metodo restituisce un `OutputResult` oggetto che contiene i risultati dell&#39;operazione.

   >[!NOTE]
   >
   >Il metodo `OutputResult` dell&#39; `getRecordLevelMetaDataList` oggetto restituisce `null`.

1. Recuperare i risultati dell&#39;operazione.

   * Creare un oggetto `com.adobe.idp.Document` che rappresenti lo stato del `generatePrintedOutput` metodo richiamando il metodo dell&#39; `OutputResult` oggetto `getStatusDoc` (l&#39; `OutputResult` oggetto è stato restituito dal `generatePrintedOutput` metodo).
   * Creare un `java.io.File` oggetto che conterrà i risultati dell&#39;operazione. Assicurarsi che l&#39;estensione del file sia XML.
   * Richiamare il metodo dell&#39; `com.adobe.idp.Document` oggetto `copyToFile` per copiare il contenuto dell&#39; `com.adobe.idp.Document` oggetto nel file (assicurarsi di utilizzare l&#39; `com.adobe.idp.Document` oggetto restituito dal `getStatusDoc` metodo).

**Consulta anche**

[Riepilogo dei passaggi](creating-document-output-streams.md#summary-of-steps)

[Avvio rapido (modalità SOAP): Stampa su un file tramite l&#39;API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-printing-to-a-file-using-the-java-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)di connessione.

### Stampa su file tramite l&#39;API del servizio Web {#print-to-files-using-the-web-service-api}

Stampa su un file tramite l&#39;API di Output (servizio Web):

1. Includere i file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituire `localhost` con l&#39;indirizzo IP del server in cui è installato AEM Forms.

1. Creare un oggetto Client di output.

   * Creare un `OutputServiceClient` oggetto utilizzando il relativo costruttore predefinito.
   * Creare un `OutputServiceClient.Endpoint.Address` oggetto utilizzando il `System.ServiceModel.EndpointAddress` costruttore. Passa un valore di stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/OutputService?blob=mtom`.) Non è necessario utilizzare l&#39; `lc_version` attributo. Questo attributo viene utilizzato quando create un riferimento a un servizio. Tuttavia, specificate `?blob=mtom` per utilizzare MTOM.
   * Creare un `System.ServiceModel.BasicHttpBinding` oggetto ottenendo il valore del `OutputServiceClient.Endpoint.Binding` campo. Inserite il valore restituito in `BasicHttpBinding`.
   * Impostare il campo `System.ServiceModel.BasicHttpBinding` dell&#39; `MessageEncoding` oggetto su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilitate l&#39;autenticazione HTTP di base eseguendo le seguenti operazioni:

      * Assegnare il nome utente dei moduli AEM al campo `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `OutputServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Fare riferimento a un&#39;origine dati XML.

   * Creare un `BLOB` oggetto utilizzando il relativo costruttore. L&#39; `BLOB` oggetto viene utilizzato per memorizzare i dati del modulo.
   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore di stringa che specifica la posizione del file XML che contiene i dati del modulo.
   * Creare un array di byte che memorizza il contenuto dell&#39; `System.IO.FileStream` oggetto. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà dell&#39; `System.IO.FileStream` oggetto `Length` .
   * Compilare l&#39;array di byte con i dati del flusso richiamando il `System.IO.FileStream` `Read` metodo dell&#39;oggetto e passando l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39; `BLOB` oggetto assegnandone `binaryData` la proprietà con il contenuto dell&#39;array di byte.

1. Impostare le opzioni di esecuzione della stampa necessarie per stampare su un file.

   * Creare un `PrintedOutputOptionsSpec` oggetto utilizzando il relativo costruttore.
   * Specificare il file assegnando un valore di stringa che rappresenta la posizione e il nome del file al membro `PrintedOutputOptionsSpec` dati `fileURI` dell&#39;oggetto. Ad esempio, se si desidera che il servizio Output venga stampato su un file PostScript denominato *MortgageForm.ps* che si trova in C:\Adobe, specificare C:\\Adobe\MortgageForm.ps.
   * Specificare il numero di copie da stampare assegnando un valore intero che rappresenta il numero di copie ai membri `PrintedOutputOptionsSpec` dati `copies` dell&#39;oggetto.

1. Stampare il flusso di stampa su un file.

   Per stampare su un file, richiamare il metodo dell&#39; `OutputServiceService` oggetto `generatePrintedOutput` e passare i seguenti valori:

   * Un valore di `PrintFormat` enumerazione che specifica il formato del flusso di stampa da creare. Ad esempio, per creare un flusso di stampa PostScript, passare `PrintFormat.PostScript`.
   * Una stringa che specifica il nome della struttura del modulo.
   * Una stringa che specifica la posizione dei relativi file collaterali, ad esempio i file immagine.
   * Una stringa che specifica la posizione del file XDC da utilizzare (è possibile passare `null` se si specifica il file XDC da utilizzare utilizzando l&#39; `PrintedOutputOptionsSpec` oggetto).
   * L&#39; `PrintedOutputOptionsSpec` oggetto che contiene le opzioni di esecuzione della stampa necessarie per stampare su un file.
   * L&#39; `BLOB` oggetto che contiene l&#39;origine dati XML contenente i dati del modulo.
   * Un `BLOB` oggetto popolato dal `generatePDFOutput` metodo. Il `generatePDFOutput` metodo popola l&#39;oggetto con i metadati generati che descrivono il documento. Questo valore di parametro è richiesto solo per la chiamata al servizio Web.
   * Un `BLOB` oggetto popolato dal `generatePDFOutput` metodo. Il `generatePDFOutput` metodo popola l&#39;oggetto con i dati dei risultati. Questo valore di parametro è richiesto solo per la chiamata al servizio Web.
   * Un `OutputResult` oggetto che contiene i risultati dell&#39;operazione. Questo valore di parametro è richiesto solo per la chiamata al servizio Web.

1. Recuperare i risultati dell&#39;operazione.

   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore di stringa che rappresenta un percorso di file XML contenente i dati dei risultati. Assicurarsi che l&#39;estensione del file sia XML.
   * Creare un array di byte che memorizza il contenuto dei dati dell&#39; `BLOB` oggetto compilato con i dati dei risultati dal `OutputServiceService` metodo dell&#39; `generatePDFOutput` oggetto (ottavo parametro). Compilare l&#39;array di byte ottenendo il valore del membro `BLOB` dati dell&#39; `MTOM` oggetto.
   * Creare un `System.IO.BinaryWriter` oggetto richiamando il relativo costruttore e passando l&#39; `System.IO.FileStream` oggetto.
   * Scrivere il contenuto dell&#39;array di byte nel file XML richiamando il metodo dell&#39; `System.IO.BinaryWriter` oggetto `Write` e passando l&#39;array di byte.

**Consulta anche**

[Riepilogo dei passaggi](creating-document-output-streams.md#summary-of-steps)

[Attivazione di moduli AEM tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamo di moduli AEM con SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Invio di flussi di stampa alle stampanti {#sending-print-streams-to-printers}

È possibile utilizzare il servizio Output per inviare flussi di stampa come PostScript, PCL (Printer Control Language) o i seguenti formati di etichetta alle stampanti di rete:

* Zebra - ZPL
* Intermec - IPL
* Datamax - DPL
* TecToshiba - TPCL

Utilizzando il servizio Output, è possibile unire i dati XML a una struttura del modulo e generare il modulo come flusso di stampa. Ad esempio, è possibile creare un flusso di stampa PostScript e inviarlo a una stampante di rete. Nell&#39;illustrazione seguente è illustrato il servizio Output che invia flussi di stampa alle stampanti di rete.

>[!NOTE]
>
>Per dimostrare come inviare un flusso di stampa a una stampante di rete, in questa sezione viene inviato un flusso di stampa PostScript a una stampante di rete utilizzando il protocollo della stampante SharedPrinter.

>[!NOTE]
>
> Per ulteriori informazioni sul servizio Output, consultate Riferimento [servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-6}

Per inviare un flusso di stampa a una stampante di rete, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un oggetto Client di output.
1. Fare riferimento a un&#39;origine dati XML.
1. Impostazione delle opzioni di esecuzione della stampa
1. Recuperare un documento da stampare.
1. Inviare il documento a una stampante di rete.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate servizi Web, accertatevi di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è distribuito su JBoss)
* jbossall-client.jar (richiesto se AEM Forms è distribuito su JBoss)

se AEM Forms è distribuito su un server applicazione J2EE supportato che non sia JBoss, dovrete sostituire i file adobe-utilities.jar e jbossall-client.jar con file JAR specifici del server applicazione J2EE su cui è distribuito AEM Forms.

**Creare un oggetto Client di output**

Prima di eseguire un&#39;operazione del servizio Output a livello di programmazione, creare un oggetto client del servizio Output. Se utilizzate l&#39;API Java, create un `OutputClient` oggetto. Se si utilizza l&#39;API del servizio Web Output, creare un `OutputServiceClient` oggetto.

**Riferimento a un&#39;origine dati XML**

Per stampare un documento contenente dati, è necessario fare riferimento a un&#39;origine dati XML che contiene elementi XML per ogni campo del modulo che si desidera compilare con i dati. Il nome dell&#39;elemento XML deve corrispondere al nome del campo. Un elemento XML viene ignorato se non corrisponde a un campo modulo o se il nome dell&#39;elemento XML non corrisponde al nome del campo. Se vengono specificati tutti gli elementi XML, non è necessario stabilire una corrispondenza con l&#39;ordine di visualizzazione degli elementi XML.

**Impostazione delle opzioni di esecuzione della stampa**

È possibile impostare le opzioni di esecuzione quando si invia un flusso di stampa a una stampante, comprese le seguenti opzioni:

* **Copie**: Specifica il numero di copie da inviare alla stampante. Il valore predefinito è 1.
* **Anello**: Quando si utilizza uno stapler, viene impostata un&#39;opzione XCI. Questa opzione può essere specificata nel modello di configurazione dall&#39;elemento di base e viene utilizzata solo per le stampanti PS e PCL.
* **OutputJog**: L&#39;opzione XCI viene impostata quando le pagine di output devono essere bloccate (fisicamente spostate nel vassoio di output). Questa opzione è disponibile solo per le stampanti PS e PCL.
* **OutputBin**: Valore XCI utilizzato per consentire al driver di stampa di selezionare il bin di output appropriato.

>[!NOTE]
>
>Per informazioni su tutte le opzioni di esecuzione che è possibile impostare, vedere il riferimento alla `PrintedOutputOptionsSpec` classe.

**Recupero di un documento da stampare**

Recuperare un flusso di stampa da inviare a una stampante. Ad esempio, è possibile recuperare un file PostScript e inviarlo a una stampante.

È possibile scegliere di inviare un file PDF se la stampante lo supporta. Tuttavia, l&#39;invio di un documento PDF a una stampante potrebbe causare un problema a causa del quale ogni produttore della stampante ha implementato in modo diverso l&#39;interprete PDF. Alcuni produttori di stampa utilizzano l&#39;interpretazione Adobe PDF, ma dipende dalla stampante. Altre stampanti dispongono di un interprete PDF specifico. Di conseguenza, i risultati della stampa possono variare.

Un altro limite all&#39;invio di un documento PDF a una stampante è rappresentato dal fatto che viene stampato; non può accedere a duplex, selezione del vassoio carta e fascicolazione, ad eccezione delle impostazioni della stampante.

Per recuperare un documento da stampare, utilizzare il `generatePrintedOutput` metodo. La tabella seguente specifica i tipi di contenuto impostati per un dato flusso di stampa quando si utilizza il `generatePrintedOutput` metodo.

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
   <td><p>Crea un flusso di output xdpl203.xdc predefinito o personalizzato per impostazione predefinita.</p></td>
  </tr>
  <tr>
   <td><p>DPL300DPI </p></td>
   <td><p>Crea un flusso di output DPL 300 DPI.</p></td>
  </tr>
  <tr>
   <td><p>DPL406DPI </p></td>
   <td><p>Crea un flusso di output DPL 400 DPI.</p></td>
  </tr>
  <tr>
   <td><p>DPL600DPI </p></td>
   <td><p>Crea un flusso di output DPL 600 DPI.</p></td>
  </tr>
  <tr>
   <td><p>GenericColorPCL </p></td>
   <td><p>Crea un flusso di output PCL (5c) a colori generico.</p></td>
  </tr>
  <tr>
   <td><p>GenericPSLevel3 </p></td>
   <td><p>Crea un flusso di output PostScript di livello 3 generico.</p></td>
  </tr>
  <tr>
   <td><p>IPL </p></td>
   <td><p>Crea un flusso di output IPL personalizzato.</p></td>
  </tr>
  <tr>
   <td><p>IPL300DPI </p></td>
   <td><p>Crea un flusso di output IPL 300 DPI.</p></td>
  </tr>
  <tr>
   <td><p>IPL400DPI </p></td>
   <td><p>Crea un flusso di output IPL 400 DPI.</p></td>
  </tr>
  <tr>
   <td><p>PCL </p></td>
   <td><p>Crea un flusso di output PCL (5e) monocromatico generico.</p></td>
  </tr>
  <tr>
   <td><p>PostScript </p></td>
   <td><p>Crea un flusso di output PostScript di livello 2 generico.</p></td>
  </tr>
  <tr>
   <td><p>TPCL </p></td>
   <td><p>Crea un flusso di output TPCL personalizzato.</p></td>
  </tr>
  <tr>
   <td><p>TPCL305DPI </p></td>
   <td><p>Crea un flusso di output TPCL 305 DPI.</p></td>
  </tr>
  <tr>
   <td><p>TPCL600DPI </p></td>
   <td><p>Crea un flusso di output TPCL 600 DPI.</p></td>
  </tr>
  <tr>
   <td><p>ZPL </p></td>
   <td><p>Crea un flusso di output ZPL 203 DPI.</p></td>
  </tr>
  <tr>
   <td><p>ZPL300DPI </p></td>
   <td><p>Crea un flusso di output ZPL 300 DPI.</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>È inoltre possibile inviare un flusso di stampa a una stampante utilizzando il `generatePrintedOutput2` metodo . Tuttavia, gli avvii rapidi associati alla sezione Invio di flussi di stampa alle stampanti utilizzano il `generatePrintedOutput` metodo.

**Inviare il flusso di stampa a una stampante di rete**

Dopo aver recuperato un documento da stampare, è possibile richiamare il servizio Output, che causa l&#39;invio di un flusso di stampa a una stampante di rete. Per individuare correttamente la stampante, è necessario specificare sia il server di stampa che il nome della stampante. È inoltre necessario specificare il protocollo di stampa.

>[!NOTE]
>
>Se sul server dei moduli è installato PDFG e il server viene eseguito su Windows Server 2008, non è possibile utilizzare la proprietà SharedPrinter. In questa situazione, utilizzare un protocollo di stampa diverso.

>[!NOTE]
>
>Se si utilizza una stampante di rete e il meccanismo di accesso è SharedPrinter, è necessario specificare il percorso di rete completo della stampante.Inviare un flusso di stampa a una stampante di rete utilizzando l&#39;API Java

Inviare un flusso di stampa a una stampante di rete utilizzando l&#39;API Output (Java):

1. Includere i file di progetto.

   Includete file JAR client, ad esempio adobe-output-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto Client di output

   * Creare un `ServiceClientFactory` oggetto che contenga proprietà di connessione.
   * Creare un `OutputClient` oggetto utilizzando il relativo costruttore e passando l&#39; `ServiceClientFactory` oggetto.

1. Riferimento a un&#39;origine dati XML

   * Creare un `java.io.FileInputStream` oggetto che rappresenta l&#39;origine dati XML utilizzata per compilare il documento utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del file XML.
   * Creare un `com.adobe.idp.Document` oggetto utilizzando il relativo costruttore e passando l&#39; `java.io.FileInputStream` oggetto.

1. Impostazione delle opzioni di esecuzione della stampa

   Creare un `PrintedOutputOptionsSpec` oggetto che rappresenti le opzioni di esecuzione della stampa. Ad esempio, è possibile specificare il numero di copie da stampare richiamando il `PrintedOutputOptionsSpec` metodo dell&#39;oggetto `setCopies` .

   >[!NOTE]
   >
   >Non è possibile impostare il valore dell&#39;impaginazione utilizzando il metodo dell&#39; `PrintedOutputOptionsSpec` oggetto `setPagination` se si sta generando un flusso di stampa ZPL. Analogamente, non è possibile impostare le seguenti opzioni per un flusso di stampa ZPL: OutputJog, PageOffset e Staple. Il `setPagination` metodo non è valido per la generazione PostScript. È valido solo per la generazione PCL.

1. Recupero di un documento da stampare

   * Recuperare un documento da stampare richiamando il metodo dell&#39; `OutputClient` oggetto `generatePrintedOutput` e passando i seguenti valori:

      * Un valore di `PrintFormat` enumerazione che specifica il flusso di stampa. Ad esempio, per creare un flusso di stampa PostScript, passare `PrintFormat.PostScript`.
      * Una stringa che specifica il nome della struttura del modulo.
      * Una stringa che specifica la posizione dei relativi file collaterali, ad esempio i file immagine.
      * Una stringa che specifica la posizione del file XDC da utilizzare.
      * L&#39; `PrintedOutputOptionsSpec` oggetto che contiene le opzioni di esecuzione necessarie per la stampa su un file.
      * L&#39; `com.adobe.idp.Document` oggetto che rappresenta l&#39;origine dati XML contenente i dati del modulo da unire alla struttura del modulo.
      Questo metodo restituisce un `OutputResult` oggetto che contiene i risultati dell&#39;operazione.

   * Creare un `com.adobe.idp.Document` oggetto da inviare alla stampante richiamando il `OutputResult` metodo ‘s `getGeneratedDoc` . Questo metodo restituisce un `com.adobe.idp.Document` oggetto.


1. Inviare il flusso di stampa a una stampante di rete

   Inviare il flusso di stampa a una stampante di rete richiamando il metodo dell&#39; `OutputClient` oggetto `sendToPrinter` e passando i seguenti valori:

   * Un `com.adobe.idp.Document` oggetto che rappresenta il flusso di stampa da inviare alla stampante.
   * Un valore di `PrinterProtocol` enumerazione che specifica il protocollo della stampante da utilizzare. Ad esempio, per specificare il protocollo SharedPrinter, passare `PrinterProtocol.SharedPrinter`.
   * Una stringa che specifica il nome del server di stampa. Ad esempio, se il nome del server di stampa è PrintServer1, passare `\\\PrintSever1`.
   * Valore stringa che specifica il nome della stampante. Ad esempio, se il nome della stampante è Printer1, passare `\\\PrintSever1\Printer1`.
   >[!NOTE]
   >
   >Il `sendToPrinter` metodo è stato aggiunto all’API di AEM Forms nella versione 8.2.1.

### Inviare un flusso di stampa a una stampante utilizzando l&#39;API del servizio Web {#send-a-print-stream-to-a-printer-using-the-web-service-api}

Inviare un flusso di stampa a una stampante di rete utilizzando l&#39;API Output (servizio Web):

1. Includere i file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituire `localhost` con l&#39;indirizzo IP del server in cui è installato AEM Forms.

1. Creare un oggetto Client di output.

   * Creare un `OutputServiceClient` oggetto utilizzando il relativo costruttore predefinito.
   * Creare un `OutputServiceClient.Endpoint.Address` oggetto utilizzando il `System.ServiceModel.EndpointAddress` costruttore. Passa un valore di stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/OutputService?blob=mtom`.) Non è necessario utilizzare l&#39; `lc_version` attributo. Questo attributo viene utilizzato quando create un riferimento a un servizio. Tuttavia, specificate `?blob=mtom` per utilizzare MTOM.
   * Creare un `System.ServiceModel.BasicHttpBinding` oggetto ottenendo il valore del `OutputServiceClient.Endpoint.Binding` campo. Inserite il valore restituito in `BasicHttpBinding`.
   * Impostare il campo `System.ServiceModel.BasicHttpBinding` dell&#39; `MessageEncoding` oggetto su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilitate l&#39;autenticazione HTTP di base eseguendo le seguenti operazioni:

      * Assegnare il nome utente dei moduli AEM al campo `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `OutputServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Fare riferimento a un&#39;origine dati XML.

   * Creare un `BLOB` oggetto utilizzando il relativo costruttore. L&#39; `BLOB` oggetto viene utilizzato per memorizzare i dati del modulo.
   * Creare un `System.IO.FileStream` oggetto richiamandone il costruttore. Passa un valore di stringa che specifica la posizione del file XML contenente i dati del modulo.
   * Creare un array di byte che memorizza il contenuto dell&#39; `System.IO.FileStream` oggetto. Determinare la lunghezza dell&#39;array di byte ottenendo la `System.IO.FileStream` proprietà dell&#39; `Length` oggetto.
   * Compilare l&#39;array di byte con i dati del flusso richiamando il `System.IO.FileStream` `Read` metodo dell&#39;oggetto e passando l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39; `BLOB` oggetto assegnandone `MTOM` il campo con il contenuto dell&#39;array di byte.

1. Impostare le opzioni di esecuzione della stampa.

   Creare un `PrintedOutputOptionsSpec` oggetto utilizzando il relativo costruttore. Ad esempio, è possibile specificare il numero di copie da stampare assegnando un valore intero che rappresenta il numero di copie al membro `PrintedOutputOptionsSpec` dati dell&#39; `copies` oggetto.

   >[!NOTE]
   >
   >Non è possibile impostare il valore di impaginazione utilizzando il membro dati dell&#39; `PrintedOutputOptionsSpec` oggetto `pagination` se si sta generando un flusso di stampa ZPL. Analogamente, non è possibile impostare le seguenti opzioni per un flusso di stampa ZPL: OutputJog, PageOffset e Staple. Il membro `pagination` dati non è valido per la generazione PostScript. È valido solo per la generazione PCL.

1. Recuperare un documento da stampare.

   * Recuperare un documento da stampare richiamando il metodo dell&#39; `OutputServiceService` oggetto `generatePrintedOutput` e passando i seguenti valori:

      * Un valore di `PrintFormat` enumerazione che specifica il flusso di stampa. Ad esempio, per creare un flusso di stampa PostScript, passare `PrintFormat.PostScript`.
      * Una stringa che specifica il nome della struttura del modulo.
      * Una stringa che specifica la posizione dei relativi file collaterali, ad esempio i file immagine.
      * Una stringa che specifica la posizione del file XDC da utilizzare.
      * L&#39; `PrintedOutputOptionsSpec` oggetto che contiene le opzioni di esecuzione della stampa utilizzate per inviare un flusso di stampa a una stampante di rete.
      * L&#39; `BLOB` oggetto che contiene l&#39;origine dati XML contenente i dati del modulo.
      * Un `BLOB` oggetto popolato dal `generatePrintedOutput` metodo. Il `generatePrintedOutput` metodo popola l&#39;oggetto con i metadati generati che descrivono il documento. Questo valore di parametro è richiesto solo per la chiamata al servizio Web.
      * Un `BLOB` oggetto popolato dal `generatePrintedOutput` metodo. Il `generatePrintedOutput` metodo popola l&#39;oggetto con i dati dei risultati. Questo valore di parametro è richiesto solo per la chiamata al servizio Web.
      * Un `OutputResult` oggetto che contiene i risultati dell&#39;operazione. Questo valore di parametro è richiesto solo per la chiamata al servizio Web.
   * Creare un `BLOB` oggetto da inviare alla stampante ottenendo il valore del `OutputResult` metodo ‘s `generatedDoc` . Questo metodo restituisce un `BLOB` oggetto che contiene i dati PostScript restituiti dal `generatePrintedOutput` metodo.


1. Inviare il flusso di stampa a una stampante di rete.

   Inviare il flusso di stampa a una stampante di rete richiamando il metodo dell&#39; `OutputClient` oggetto `sendToPrinter` e passando i seguenti valori:

   * Un `BLOB` oggetto che rappresenta il flusso di stampa da inviare alla stampante.
   * Un valore di `PrinterProtocol` enumerazione che specifica il protocollo della stampante da utilizzare. Ad esempio, per specificare il protocollo SharedPrinter, passare `PrinterProtocol.SharedPrinter`.
   * Un `bool` valore che specifica se utilizzare il valore del parametro precedente. Passa il valore `true`. Questo valore di parametro è richiesto solo per la chiamata al servizio Web.
   * Una stringa che specifica il nome del server di stampa. Ad esempio, se il nome del server di stampa è PrintServer1, passare `\\\PrintSever1`.
   * Valore stringa che specifica il nome della stampante. Ad esempio, se il nome della stampante è Printer1, passare `\\\PrintSever1\Printer1`.
   >[!NOTE]
   >
   >Il `sendToPrinter` metodo è stato aggiunto all’API di AEM Forms nella versione 8.2.1.

## Creazione di più file di output {#creating-multiple-output-files}

Il servizio Output può creare documenti separati per ciascun record all&#39;interno di un&#39;origine dati XML o di un singolo file contenente tutti i record (questa funzionalità è l&#39;impostazione predefinita). Ad esempio, si supponga che dieci record si trovino all&#39;interno di un&#39;origine dati XML e si informi il servizio Output di creare documenti PDF separati (o altri tipi di output) per ciascun record utilizzando l&#39;API Output Service. Di conseguenza, il servizio Output genera dieci documenti PDF. Anziché creare documenti, è possibile inviare più flussi di stampa a una stampante.

Nell&#39;illustrazione seguente è illustrato anche il servizio Output che elabora un file di dati XML contenente più record. Si supponga tuttavia di richiedere al servizio Output di creare un singolo documento PDF contenente tutti i record di dati. In questa situazione, il servizio Output genera un documento che contiene tutti i record.

Nell&#39;illustrazione seguente è illustrato il servizio Output che elabora un file di dati XML contenente più record. Si supponga di indicare al servizio Output di creare un documento PDF separato per ciascun record di dati. In questa situazione, il servizio Output genera un documento PDF separato per ciascun record di dati.

![cm_outputbatchmany](assets/cm_outputbatchmany.png)

I seguenti dati XML mostrano un esempio di un file di dati contenente tre record di dati.

```as3
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

Tenere presente che l&#39;elemento XML che avvia e termina ogni record di dati è `LoanRecord`. A questo elemento XML fa riferimento la logica dell&#39;applicazione che genera più file.

>[!NOTE]
>
> Per ulteriori informazioni sul servizio Output, consultate Riferimento [servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-7}

Per creare più file PDF basati su un&#39;origine dati XML, procedere come segue:

1. Includere i file di progetto.
1. Creare un oggetto Client di output.
1. Fare riferimento a un&#39;origine dati XML.
1. Impostare le opzioni di esecuzione PDF.
1. Impostare le opzioni di esecuzione del rendering.
1. Generare più file PDF.
1. Recuperare i risultati dell&#39;operazione.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate servizi Web, accertatevi di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è distribuito su JBoss)
* jbossall-client.jar (richiesto se AEM Forms è distribuito su JBoss)

se AEM Forms è distribuito su un server applicazione J2EE supportato che non sia JBoss, dovrete sostituire i file adobe-utilities.jar e jbossall-client.jar con file JAR specifici del server applicazione J2EE su cui è distribuito AEM Forms.

**Creare un oggetto Client di output**

Prima di eseguire un&#39;operazione del servizio Output a livello di programmazione, è necessario creare un oggetto client del servizio Output. Se utilizzate l&#39;API Java, create un `OutputClient` oggetto. Se si utilizza l&#39;API del servizio Web Output, creare un `OutputServiceService` oggetto.

**Riferimento a un&#39;origine dati XML**

Fare riferimento a un&#39;origine dati XML che contiene più record. Per separare i record di dati è necessario utilizzare un elemento XML. Ad esempio, nell&#39;origine dati XML di esempio visualizzata in precedenza in questa sezione, l&#39;elemento XML che separa i record di dati è denominato `LoanRecord`.

Per ogni campo del modulo che si desidera compilare con i dati deve esistere un elemento XML. Il nome dell&#39;elemento XML deve corrispondere al nome del campo. Un elemento XML viene ignorato se non corrisponde a un campo modulo o se il nome dell&#39;elemento XML non corrisponde al nome del campo. Se vengono specificati tutti gli elementi XML, non è necessario stabilire una corrispondenza con l&#39;ordine di visualizzazione degli elementi XML.

**Impostazione delle opzioni di esecuzione PDF**

Per creare correttamente più file basati su un&#39;origine dati XML, è necessario impostare le seguenti opzioni di esecuzione per il servizio Output:

* **Molti file**: Specifica se il servizio Output crea uno o più documenti. Potete specificare true o false. Per creare un documento separato per ciascun record di dati nell&#39;origine dati XML, specificare true.
* **URI** file: Specifica la posizione dei file generati dal servizio Output. Ad esempio, si supponga di specificare C:\\Adobe\forms\Loan.pdf. In questa situazione, il servizio Output crea un file denominato Loan.pdf e inserisce il file nella cartella C:\\Adobe\forms folder. In presenza di più file, i nomi dei file sono Loan0001.pdf, Loan0002.pdf, Loan0003.pdf e così via. Se specificate un percorso di file, i file vengono inseriti sul server, non sul computer client.
* **Nome** record: Specifica il nome dell&#39;elemento XML nell&#39;origine dati che separa i record di dati. Ad esempio, nell&#39;origine dati XML di esempio visualizzata in precedenza in questa sezione, viene chiamato l&#39;elemento XML che separa i record di dati `LoanRecord`. Anziché impostare l&#39;opzione di runtime Nome record, potete impostare il livello di record assegnandogli un valore numerico che indica il livello di elemento che contiene i record di dati. Tuttavia, potete impostare solo il Nome record o il Livello record. Non è possibile impostare entrambi i valori.

**Impostazione delle opzioni di esecuzione del rendering**

Potete impostare le opzioni di esecuzione del rendering durante la creazione di più file. Sebbene queste opzioni non siano richieste (a differenza delle opzioni di esecuzione dell&#39;output, che sono richieste), è possibile eseguire attività quali migliorare le prestazioni del servizio Output. Ad esempio, è possibile memorizzare nella cache la struttura del modulo utilizzata dal servizio Output per migliorare le prestazioni.

Quando il servizio Output elabora i record batch, legge i dati che contengono più record in modo incrementale. In altre parole, il servizio Output legge i dati in memoria e rilascia i dati durante l&#39;elaborazione del batch di record. Il servizio Output carica i dati in modo incrementale quando è impostata una delle due opzioni di esecuzione. Se si imposta l&#39;opzione di runtime Nome record, il servizio Output legge i dati in modo incrementale. Analogamente, se si imposta l&#39;opzione di esecuzione del livello di record su 2 o superiore, il servizio Output legge i dati in modo incrementale.

È possibile controllare se il servizio Output esegue il caricamento incrementale utilizzando il `PDFOutputOptionsSpec` metodo dell&#39; `PrintedOutputOptionSpec` oggetto o `setLazyLoading` . È possibile passare il valore `false` a questo metodo che disattiva il caricamento incrementale.

**Generare più file PDF**

Dopo aver fatto riferimento a un&#39;origine dati XML valida che contiene più record di dati e aver impostato le opzioni di esecuzione, è possibile richiamare il servizio Output, generando così più file. Quando si generano più record, il metodo dell&#39; `OutputResult` oggetto `getGeneratedDoc` restituisce `null`.

**Recuperare i risultati dell&#39;operazione**

Dopo che il servizio Output ha eseguito un&#39;operazione, restituisce dati XML che specificano se l&#39;operazione ha avuto esito positivo. Il seguente codice XML viene restituito dal servizio Output. In questa situazione, il servizio Output ha generato 42 documenti.

```as3
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

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API di Output Service](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Creare più file PDF utilizzando l&#39;API Java {#create-multiple-pdf-files-using-the-java-api}

Creare più file PDF utilizzando l&#39;API di output (Java):

1. Includi file di progetto&quot;

   Includete file JAR client, ad esempio adobe-output-client.jar, nel percorso di classe del progetto Java. .

1. Creare un oggetto Client di output

   * Creare un `ServiceClientFactory` oggetto che contenga proprietà di connessione.
   * Creare un `OutputClient` oggetto utilizzando il relativo costruttore e passando l&#39; `ServiceClientFactory` oggetto.

1. Riferimento a un&#39;origine dati XML

   * Creare un `java.io.FileInputStream` oggetto che rappresenta l&#39;origine dati XML che contiene più record utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del file XML.
   * Creare un `com.adobe.idp.Document` oggetto utilizzando il relativo costruttore e passando l&#39; `java.io.FileInputStream` oggetto.

1. Impostazione delle opzioni di esecuzione PDF

   * Creare un `PDFOutputOptionsSpec` oggetto utilizzando il relativo costruttore.
   * Impostare l&#39;opzione Molti file richiamando il `PDFOutputOptionsSpec` metodo dell&#39; `setGenerateManyFiles` oggetto. Ad esempio, passare il valore `true` per indicare al servizio Output di creare un file PDF separato per ciascun record nell&#39;origine dati XML. (Se si passa `false`il servizio Output genera un singolo documento PDF contenente tutti i record).
   * Impostare l&#39;opzione URI del file richiamando il metodo dell&#39; `PDFOutputOptionsSpec` oggetto `setFileUri` e passando un valore di stringa che specifica la posizione dei file generati dal servizio Output. L&#39;opzione URI file è relativa al server applicazione J2EE in cui è installato AEM Forms, non al computer client.
   * Impostare l&#39;opzione Nome record richiamando il metodo dell&#39; `OutputOptionsSpec` oggetto `setRecordName` e passando un valore di stringa che specifica il nome dell&#39;elemento XML nell&#39;origine dati che separa i record di dati. Ad esempio, si consideri l&#39;origine dati XML visualizzata in precedenza in questa sezione. Il nome dell&#39;elemento XML che separa i record di dati è LoanRecord).

1. Impostazione delle opzioni di esecuzione del rendering

   * Creare un `RenderOptionsSpec` oggetto utilizzando il relativo costruttore.
   * Memorizzare nella cache la struttura del modulo per migliorare le prestazioni del servizio Output richiamando l&#39; `RenderOptionsSpec` oggetto `setCacheEnabled` e passando un `Boolean` valore di `true`.

1. Generare più file PDF

   Generare più file PDF richiamando il metodo dell&#39; `OutputClient` oggetto `generatePDFOutput` e passando i seguenti valori:

   * Un valore `TransformationFormat` enum. Per generare un documento PDF, specificare `TransformationFormat.PDF`.
   * Una stringa che specifica il nome della struttura del modulo.
   * Una stringa che specifica il livello principale del contenuto in cui si trova la struttura del modulo.
   * Un `PDFOutputOptionsSpec` oggetto che contiene opzioni di esecuzione PDF.
   * Un `RenderOptionsSpec` oggetto che contiene opzioni di esecuzione del rendering.
   * L&#39; `com.adobe.idp.Document` oggetto che contiene l&#39;origine dati XML contenente i dati da unire alla struttura del modulo.
   Il `generatePDFOutput` metodo restituisce un `OutputResult` oggetto che contiene i risultati dell&#39;operazione.

1. Recuperare i risultati dell&#39;operazione

   * Creare un `java.io.File` oggetto che rappresenta un file XML che conterrà i risultati del `generatePDFOutput` metodo. Accertatevi che l’estensione del nome del file sia .xml.
   * Richiamare il metodo dell&#39; `com.adobe.idp.Document` oggetto `copyToFile` per copiare il contenuto dell&#39; `com.adobe.idp.Document` oggetto nel file (assicurarsi di utilizzare l&#39; `com.adobe.idp.Document` oggetto restituito dal `applyUsageRights` metodo).

**Consulta anche**

[Riepilogo dei passaggi](creating-document-output-streams.md#summary-of-steps)

[Avvio rapido (modalità EJB): Creazione di più file PDF tramite l&#39;API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-multiple-pdf-files-using-the-java-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Creazione di più file PDF tramite l&#39;API del servizio Web {#create-multiple-pdf-files-using-the-web-service-api}

Creare più file PDF utilizzando l&#39;API di Output (servizio Web):

1. Includere i file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituire `localhost` con l&#39;indirizzo IP del server in cui è installato AEM Forms.

1. Creare un oggetto Client di output.

   * Creare un `OutputServiceClient` oggetto utilizzando il relativo costruttore predefinito.
   * Creare un `OutputServiceClient.Endpoint.Address` oggetto utilizzando il `System.ServiceModel.EndpointAddress` costruttore. Passa un valore di stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/OutputService?blob=mtom`.) Non è necessario utilizzare l&#39; `lc_version` attributo. Questo attributo viene utilizzato quando create un riferimento a un servizio. Tuttavia, specificate `?blob=mtom` per utilizzare MTOM.
   * Creare un `System.ServiceModel.BasicHttpBinding` oggetto ottenendo il valore del `OutputServiceClient.Endpoint.Binding` campo. Inserite il valore restituito in `BasicHttpBinding`.
   * Impostare il campo `System.ServiceModel.BasicHttpBinding` dell&#39; `MessageEncoding` oggetto su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilitate l&#39;autenticazione HTTP di base eseguendo le seguenti operazioni:

      * Assegnare il nome utente dei moduli AEM al campo `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `OutputServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Fare riferimento a un&#39;origine dati XML.

   * Creare un `BLOB` oggetto utilizzando il relativo costruttore. L&#39; `BLOB` oggetto viene utilizzato per memorizzare i dati del modulo che contengono più record.
   * Creare un `System.IO.FileStream` oggetto richiamandone il costruttore. Passa un valore di stringa che rappresenta la posizione del file XML contenente più record.
   * Creare un array di byte che memorizza il contenuto dell&#39; `System.IO.FileStream` oggetto. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà dell&#39; `System.IO.FileStream` oggetto `Length` .
   * Compilare l&#39;array di byte con i dati del flusso richiamando il `System.IO.FileStream` `Read` metodo dell&#39;oggetto e passando l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39; `BLOB` oggetto assegnandone `MTOM` il campo con il contenuto dell&#39;array di byte.

1. Impostare le opzioni di esecuzione PDF.

   * Creare un `PDFOutputOptionsSpec` oggetto utilizzando il relativo costruttore.
   * Impostare l&#39;opzione Molti file assegnando un valore booleano al membro dati dell&#39; `OutputOptionsSpec` oggetto `generateManyFiles` . Ad esempio, assegnare il valore `true` a questo membro dati per indicare al servizio Output di creare un file PDF separato per ciascun record nell&#39;origine dati XML. (Se si assegna `false` a questo membro dati, il servizio Output genera un singolo PDF contenente tutti i record).
   * Impostare l&#39;opzione URI del file assegnando un valore di stringa che specifica la posizione dei file generati dal servizio Output al membro `OutputOptionsSpec` dati dell&#39;oggetto `fileURI` . L&#39;opzione URI file è relativa al server applicazione J2EE in cui è installato AEM Forms, non al computer client.
   * Impostare l&#39;opzione del nome del record assegnando un valore stringa che specifica il nome dell&#39;elemento XML nell&#39;origine dati che separa i record di dati dal membro `OutputOptionsSpec` dati dell&#39; `recordName` oggetto.
   * Impostare l&#39;opzione copie assegnando un valore intero che specifica il numero di copie generate dal servizio Output al membro dati dell&#39; `OutputOptionsSpec` oggetto `copies` .

1. Impostare le opzioni di esecuzione del rendering.

   * Creare un `RenderOptionsSpec` oggetto utilizzando il relativo costruttore.
   * Memorizzare nella cache la struttura del modulo per migliorare le prestazioni del servizio Output assegnando il valore `true` al membro `RenderOptionsSpec` dati dell&#39; `cacheEnabled` oggetto.

1. Generare più file PDF.

   Per creare più file PDF, richiamare il `OutputServiceService` `generatePDFOutput`metodo dell&#39;oggetto e passare i seguenti valori:

   * Un valore enum TransformationFormat. Per generare un documento PDF, specificare `TransformationFormat.PDF`.
   * Una stringa che specifica il nome della struttura del modulo.
   * Una stringa che specifica il livello principale del contenuto in cui si trova la struttura del modulo.
   * Un `PDFOutputOptionsSpec` oggetto che contiene opzioni di esecuzione PDF.
   * Un `RenderOptionsSpec` oggetto che contiene opzioni di esecuzione del rendering.
   * L&#39; `BLOB` oggetto che contiene l&#39;origine dati XML contenente i dati da unire alla struttura del modulo.
   * Un `BLOB` oggetto popolato dal `generatePDFOutput` metodo. Il `generatePDFOutput` metodo popola l&#39;oggetto con i metadati generati che descrivono il documento.
   * Un `BLOB` oggetto popolato dal `generatePDFOutput` metodo. Il `generatePDFOutput` metodo popola l&#39;oggetto con i dati dei risultati.
   * Un `OutputResult` oggetto che contiene i risultati dell&#39;operazione.

1. Recuperare i risultati dell&#39;operazione

   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore di stringa che rappresenta un percorso di file XML contenente i dati dei risultati. Accertatevi che l’estensione del nome del file sia .xml.
   * Creare un array di byte che memorizza il contenuto dei dati dell&#39; `BLOB` oggetto compilato con i dati dei risultati dal `OutputServiceService` metodo dell&#39; `generatePDFOutput` oggetto (ottavo parametro). Compilare l&#39;array di byte ottenendo il valore del membro `BLOB` dati dell&#39; `binaryData` oggetto.
   * Creare un `System.IO.BinaryWriter` oggetto richiamando il relativo costruttore e passando l&#39; `System.IO.FileStream` oggetto.
   * Scrivere il contenuto dell&#39;array di byte nel file XML richiamando il metodo dell&#39; `System.IO.BinaryWriter` oggetto `Write` e passando l&#39;array di byte.

**Consulta anche**

[Riepilogo dei passaggi](creating-document-output-streams.md#summary-of-steps)

[Attivazione di moduli AEM tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamo di moduli AEM con SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Creazione di regole di ricerca {#creating-search-rules}

È possibile creare regole di ricerca che determinano l&#39;esame dei dati di input da parte del servizio Output e l&#39;utilizzo di strutture del modulo diverse in base al contenuto dei dati per generare l&#39;output. Ad esempio, se il *mutuo* di testo si trova all&#39;interno dei dati di input, il servizio Output può utilizzare una struttura del modulo denominata Mortgage.xdp. Allo stesso modo, se l&#39; *automobile* di testo si trova nei dati di input, il servizio Output può utilizzare una struttura del modulo salvata come AutomobileLoan.xdp. Anche se il servizio Output può generare tipi di output diversi, questa sezione presuppone che il servizio Output generi un file PDF. Nel diagramma seguente è illustrato il servizio Output che genera un file PDF elaborando un file di dati XML e utilizzando una delle numerose strutture del modulo.

Inoltre, il servizio Output è in grado di generare pacchetti di documenti, in cui nel set di dati vengono forniti più record, ogni record viene associato a una struttura del modulo e un singolo documento viene generato con più strutture del modulo.

![cs_outputbatchmanyformdesigns2](assets/cs_outputbatchmanyformdesigns2.png)

>[!NOTE]
>
> Per ulteriori informazioni sul servizio Output, consultate Riferimento [servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-8}

Per indicare al servizio Output di utilizzare le regole di ricerca durante la generazione di un documento, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un oggetto Client di output.
1. Fare riferimento a un&#39;origine dati XML.
1. Definire le regole di ricerca.
1. Impostare le opzioni di esecuzione PDF.
1. Impostare le opzioni di esecuzione del rendering.
1. Generare un documento PDF.
1. Recuperare i risultati dell&#39;operazione.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se state creando un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate servizi Web, accertatevi di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è distribuito su JBoss)
* jbossall-client.jar (richiesto se AEM Forms è distribuito su JBoss)

se AEM Forms è distribuito su un server applicazione J2EE supportato che non sia JBoss, sarà necessario sostituire adobe-utilities.jar e jbossall-client.jar con file JAR specifici per il server applicazione J2EE su cui è distribuito AEM Forms.

**Creare un oggetto Client di output**

Prima di eseguire un&#39;operazione del servizio Output a livello di programmazione, è necessario creare un oggetto client del servizio Output.

**Riferimento a un&#39;origine dati XML**

Per ogni campo del modulo che si desidera compilare con i dati deve esistere un elemento XML. Il nome dell&#39;elemento XML deve corrispondere al nome del campo. Un elemento XML viene ignorato se non corrisponde a un campo modulo o se il nome dell&#39;elemento XML non corrisponde al nome del campo. Non è necessario stabilire una corrispondenza con l&#39;ordine in cui vengono visualizzati gli elementi XML, purché siano specificati tutti gli elementi XML.

**Definire le regole di ricerca**

Per definire le regole di ricerca, è necessario definire uno o più pattern di testo ricercati dai servizi Output nei dati di input. Per ciascun pattern di testo definito, è necessario specificare una struttura del modulo corrispondente utilizzata se il pattern di testo è posizionato. Se si trova un pattern di testo, il servizio Output utilizza la struttura del modulo corrispondente per generare l&#39;output. Un esempio di pattern di testo è *ipoteca*.

>[!NOTE]
>
>Se i pattern di testo non si trovano, viene utilizzato il modulo predefinito. Assicurarsi che tutte le strutture del modulo utilizzate si trovino nella directory principale del contenuto.

**Impostazione delle opzioni di esecuzione PDF**

Per consentire al servizio Output di creare correttamente un documento PDF basato su più strutture del modulo, impostare le seguenti opzioni di esecuzione PDF:

* **URI** file: Specifica il nome e la posizione del file PDF generato dal servizio Output.
* **Regole**: Specifica le regole definite dall&#39;utente.
* **LookAHead**: Specifica il numero di byte da utilizzare dall&#39;inizio del file di dati di input per la ricerca dei pattern di testo definiti. Il valore predefinito è 500 byte.

**Impostazione delle opzioni di esecuzione del rendering**

Potete impostare le opzioni di esecuzione del rendering durante la creazione di file PDF. Sebbene queste opzioni non siano richieste (a differenza delle opzioni di esecuzione PDF), è possibile eseguire attività quali migliorare le prestazioni del servizio Output. Ad esempio, è possibile memorizzare nella cache la struttura del modulo utilizzata dal servizio Output per migliorare le prestazioni.

**Generazione di un documento PDF**

Dopo aver fatto riferimento a un&#39;origine dati XML valida e aver impostato le opzioni di esecuzione, è possibile richiamare il servizio Output generando un documento PDF. Se il servizio Output individua un pattern di testo specificato nei dati di input, utilizza la struttura del modulo corrispondente. Se non viene utilizzato un pattern di testo, il servizio Output utilizza la struttura del modulo predefinita.

**Recuperare i risultati dell&#39;operazione**

Dopo che il servizio Output ha eseguito un&#39;operazione, restituisce dati XML che specificano se l&#39;operazione ha avuto esito positivo.

**Consulta anche**

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API di Output Service](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Creare regole di ricerca utilizzando l&#39;API Java {#create-search-rules-using-the-java-api}

Create le regole di ricerca utilizzando l&#39;API di output (Java):

1. Includere i file di progetto.

   Includete file JAR client, ad esempio adobe-output-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto Client di output.

   * Creare un `ServiceClientFactory` oggetto che contenga proprietà di connessione.
   * Creare un `OutputClient` oggetto utilizzando il relativo costruttore e passando l&#39; `ServiceClientFactory` oggetto.

1. Fare riferimento a un&#39;origine dati XML.

   * Creare un `java.io.FileInputStream` oggetto che rappresenta l&#39;origine dati XML utilizzata per compilare il documento PDF utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del file XML.
   * Creare un `com.adobe.idp.Document` oggetto utilizzando il relativo costruttore e passando l&#39; `java.io.FileInputStream` oggetto.

1. Definire le regole di ricerca.

   * Creare un `Rule` oggetto utilizzando il relativo costruttore.
   * Definire un pattern di testo richiamando il metodo dell&#39; `Rule` oggetto `setPattern` e passando un valore di stringa che specifica un pattern di testo.
   * Definire la struttura del modulo corrispondente richiamando il `Rule` metodo `setForm` dell&#39;oggetto. Passa un valore di stringa che specifica il nome della struttura del modulo.
   >[!NOTE]
   >
   >Per ciascun pattern di testo da definire, ripetere i tre passaggi secondari precedenti.

   * Creare un `java.util.List` oggetto utilizzando un `java.util.ArrayList` costruttore.
   * Per ogni `Rule` oggetto creato, richiamare il `java.util.List` metodo dell&#39; `add` oggetto e passare l&#39; `Rule` oggetto.


1. Impostare le opzioni di esecuzione PDF.

   * Creare un `PDFOutputOptionsSpec` oggetto utilizzando il relativo costruttore.
   * Specificare il nome e la posizione del file PDF generato dal servizio Output richiamando il `PDFOutputOptionsSpec` metodo dell&#39; `setFileURI` oggetto. Passa un valore di stringa che specifica la posizione del file PDF. L&#39;opzione URI file è relativa al server applicazione J2EE in cui è installato AEM Forms, non al computer client.
   * Impostare le regole definite richiamando il `PDFOutputOptionsSpec` metodo dell&#39; `setRules` oggetto. Passate l&#39; `java.util.List` oggetto che contiene gli `Rule` oggetti.
   * Impostare il numero di byte per la ricerca dei pattern di testo definiti richiamando il `PDFOutputOptionsSpec` metodo dell&#39; `setLookAhead` oggetto. Passa un valore intero che rappresenta i numeri di byte.

1. Impostare le opzioni di esecuzione del rendering.

   * Creare un `RenderOptionsSpec` oggetto utilizzando il relativo costruttore.
   * Memorizzare nella cache la struttura del modulo per migliorare le prestazioni del servizio Output richiamando l&#39; `RenderOptionsSpec` oggetto `setCacheEnabled` e passando `true`.

1. Generare un documento PDF.

   Generare un documento PDF basato su più strutture del modulo richiamando il metodo dell&#39; `OutputClient` oggetto `generatePDFOutput` e passando i seguenti valori:

   * Un valore `TransformationFormat` di enumerazione. Per generare un documento PDF, specificare `TransformationFormat.PDF`.
   * Una stringa che specifica il nome della struttura del modulo predefinita. ovvero la struttura del modulo utilizzata se non si trova un pattern di testo.
   * Una stringa che specifica il livello principale del contenuto in cui si trovano le strutture del modulo.
   * Un `PDFOutputOptionsSpec` oggetto che contiene opzioni di esecuzione PDF.
   * Un `RenderOptionsSpec` oggetto che contiene opzioni di esecuzione del rendering.
   * L&#39; `com.adobe.idp.Document` oggetto che contiene i dati del modulo ricercati dal servizio Output per individuare i pattern di testo definiti.
   Il `generatePDFOutput` metodo restituisce un `OutputResult` oggetto che contiene i risultati dell&#39;operazione.

1. Recuperare i risultati dell&#39;operazione.

   * Creare un `com.adobe.idp.Document` oggetto che rappresenti lo stato del `generatePDFOutput` metodo richiamando il metodo dell&#39; `OutputResult` oggetto `getStatusDoc` .
   * Creare un `java.io.File` oggetto che conterrà i risultati dell&#39;operazione. Accertatevi che l’estensione del file sia .xml.
   * Richiamare il metodo dell&#39; `com.adobe.idp.Document` oggetto `copyToFile` per copiare il contenuto dell&#39; `com.adobe.idp.Document` oggetto nel file (assicurarsi di utilizzare l&#39; `com.adobe.idp.Document` oggetto restituito dal `getStatusDoc` metodo).

**Consulta anche**

[Riepilogo dei passaggi](creating-document-output-streams.md#summary-of-steps)

[Avvio rapido (modalità EJB): Creazione di regole di ricerca tramite l&#39;API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-search-rules-using-the-java-api)

[Avvio rapido (modalità SOAP): Creazione di regole di ricerca tramite l&#39;API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-search-rules-using-the-java-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Creare regole di ricerca utilizzando l&#39;API del servizio Web {#create-search-rules-using-the-web-service-api}

Create le regole di ricerca utilizzando l&#39;API di Output (servizio Web):

1. Includere i file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituire `localhost` con l&#39;indirizzo IP del server in cui è installato AEM Forms.

1. Creare un oggetto Client di output.

   * Creare un `OutputServiceClient` oggetto utilizzando il relativo costruttore predefinito.
   * Creare un `OutputServiceClient.Endpoint.Address` oggetto utilizzando il `System.ServiceModel.EndpointAddress` costruttore. Passa un valore di stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/OutputService?blob=mtom`.) Non è necessario utilizzare l&#39; `lc_version` attributo. Questo attributo viene utilizzato quando create un riferimento a un servizio. Tuttavia, specificate `?blob=mtom` per utilizzare MTOM.
   * Creare un `System.ServiceModel.BasicHttpBinding` oggetto ottenendo il valore del `OutputServiceClient.Endpoint.Binding` campo. Inserite il valore restituito in `BasicHttpBinding`.
   * Impostare il campo `System.ServiceModel.BasicHttpBinding` dell&#39; `MessageEncoding` oggetto su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilitate l&#39;autenticazione HTTP di base eseguendo le seguenti operazioni:

      * Assegnare il nome utente dei moduli AEM al campo `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `OutputServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Fare riferimento a un&#39;origine dati XML.

   * Creare un `BLOB` oggetto utilizzando il relativo costruttore. L&#39; `BLOB` oggetto viene utilizzato per memorizzare i dati che verranno uniti al documento PDF.
   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF da cifrare e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto dell&#39; `System.IO.FileStream` oggetto. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà dell&#39; `System.IO.FileStream` oggetto `Length` .
   * Compilare l&#39;array di byte con i dati del flusso richiamando il `System.IO.FileStream` `Read` metodo dell&#39;oggetto e passando l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39; `BLOB` oggetto assegnandone `MTOM` il campo con il contenuto dell&#39;array di byte.

1. Definire le regole di ricerca.

   * Creare un `Rule` oggetto utilizzando il relativo costruttore.
   * Definire un pattern di testo assegnando un valore di stringa che specifica un pattern di testo al membro `Rule` dati `pattern` dell&#39;oggetto.
   * Definire la struttura del modulo corrispondente assegnando un valore stringa che specifica la struttura del modulo al membro `Rule` dati `form` dell&#39;oggetto.
   >[!NOTE]
   >
   >Per ciascun pattern di testo da definire, ripetere i tre passaggi secondari precedenti.

   * Creare un `MyArrayOf_xsd_anyType` oggetto che memorizza le regole.
   * Assegnare ciascun `Rule` oggetto a un elemento dell&#39; `MyArrayOf_xsd_anyType` array. Richiamare il metodo dell&#39; `MyArrayOf_xsd_anyType` oggetto `Add` per ciascun `Rule` oggetto.


1. Impostazione delle opzioni di esecuzione PDF

   * Creare un `PDFOutputOptionsSpec` oggetto utilizzando il relativo costruttore.
   * Impostare l&#39;opzione URI del file assegnando un valore di stringa che specifica la posizione del file PDF generato dal servizio Output al membro `PDFOutputOptionsSpec` dati dell&#39;oggetto `fileURI` . L&#39;opzione URI file è relativa al server applicazione J2EE in cui è installato AEM Forms, non al computer client.
   * Impostare l&#39;opzione copie assegnando un valore intero che specifica il numero di copie generate dal servizio Output al membro dati dell&#39; `PDFOutputOptionsSpec` oggetto `copies` .
   * Impostare le regole definite assegnando l&#39; `MyArrayOf_xsd_anyType` oggetto che memorizza le regole al membro `PDFOutputOptionsSpec` dati dell&#39; `rules` oggetto.
   * Impostare il numero di byte da analizzare per i pattern di testo definiti assegnando un valore intero che rappresenta i numeri di byte da analizzare al metodo di `PDFOutputOptionsSpec` dati dell&#39;oggetto `lookAhead` .

1. Impostazione delle opzioni di esecuzione del rendering

   * Creare un `RenderOptionsSpec` oggetto utilizzando il relativo costruttore.
   * Memorizzare nella cache la struttura del modulo per migliorare le prestazioni del servizio Output assegnando il valore `true` al membro `RenderOptionsSpec` dati dell&#39; `cacheEnabled` oggetto.
   >[!NOTE]
   >
   >Non è possibile impostare la versione del documento PDF utilizzando il membro dell&#39; `RenderOptionsSpec` oggetto `pdfVersion` se il documento di input è un modulo Acrobat. Nel documento PDF di output viene mantenuta la versione PDF del modulo Acrobat. Analogamente, non è possibile impostare l&#39;opzione PDF con tag utilizzando il metodo dell&#39; `RenderOptionsSpec` oggetto `taggedPDF` se il documento di input è un modulo Acrobat.

   >[!NOTE]
   >
   >Non è possibile impostare l&#39;opzione PDF linearizzato utilizzando il membro dell&#39; `RenderOptionsSpec` oggetto `linearizedPDF` se il documento PDF di input è certificato o firmato digitalmente. Per ulteriori informazioni, vedere Firma [digitale di documenti](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)PDF.

1. Generazione di un documento PDF

   Creare un documento PDF richiamando il `OutputServiceService` `generatePDFOutput`metodo dell&#39;oggetto e passando i seguenti valori:

   * Un valore `TransformationFormat` di enumerazione. Per generare un documento PDF, specificare `TransformationFormat.PDF`.
   * Una stringa che specifica il nome della struttura del modulo.
   * Una stringa che specifica il livello principale del contenuto in cui si trova la struttura del modulo.
   * Un `PDFOutputOptionsSpec` oggetto che contiene opzioni di esecuzione PDF.
   * Un `RenderOptionsSpec` oggetto che contiene opzioni di esecuzione del rendering.
   * L&#39; `BLOB` oggetto che contiene l&#39;origine dati XML contenente i dati da unire alla struttura del modulo.
   * Un `BLOB` oggetto popolato dal `generatePDFOutput` metodo. Il `generatePDFOutput` metodo popola l&#39;oggetto con i metadati generati che descrivono il documento. (Questo valore di parametro è richiesto solo per la chiamata al servizio Web).
   * Un `BLOB` oggetto popolato dal `generatePDFOutput` metodo. Il `generatePDFOutput` metodo popola l&#39;oggetto con i dati dei risultati. (Questo valore di parametro è richiesto solo per la chiamata al servizio Web).
   * Un `OutputResult` oggetto che contiene i risultati dell&#39;operazione. (Questo valore di parametro è richiesto solo per la chiamata al servizio Web).
   >[!NOTE]
   >
   >Durante la generazione di un documento PDF richiamando il `generatePDFOutput` metodo, tenere presente che non è possibile unire i dati a un modulo PDF XFA firmato, certificato o contenente diritti di utilizzo. Per informazioni sui diritti di utilizzo, vedere [Applicazione dei diritti di utilizzo ai documenti](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)PDF.

1. Recuperare i risultati dell&#39;operazione

   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore di stringa che rappresenta un percorso di file XML contenente i dati dei risultati. Assicurarsi che l&#39;estensione del file sia XML.
   * Creare un array di byte che memorizza il contenuto dei dati dell&#39; `BLOB` oggetto compilato con i dati dei risultati dal `OutputServiceService` metodo dell&#39; `generatePDFOutput` oggetto (ottavo parametro). Compilare l&#39;array di byte ottenendo il valore del membro `BLOB` dati dell&#39; `MTOM` oggetto.
   * Creare un `System.IO.BinaryWriter` oggetto richiamando il relativo costruttore e passando l&#39; `System.IO.FileStream` oggetto.
   * Scrivere il contenuto dell&#39;array di byte nel file XML richiamando il metodo dell&#39; `System.IO.BinaryWriter` oggetto `Write` e passando l&#39;array di byte.

**Consulta anche**

[Riepilogo dei passaggi](creating-document-output-streams.md#summary-of-steps)

[Attivazione di moduli AEM tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamo di moduli AEM con SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Conversione dei documenti PDF {#flattening-pdf-documents}

È possibile utilizzare il servizio Output per trasformare un documento PDF interattivo in un PDF non interattivo. Un documento PDF interattivo consente agli utenti di immettere o modificare i dati presenti nei campi del documento PDF. Il processo di trasformazione di un documento PDF interattivo in un documento PDF non interattivo è denominato *appiattimento*. Quando un documento PDF viene appiattito, un utente non può modificare i dati nei campi del documento. Uno dei motivi per appiattire un documento PDF è garantire che i dati non possano essere modificati.

È possibile appiattire i seguenti tipi di documenti PDF:

* Documenti PDF XFA interattivi
* Acrobat Forms

Se si tenta di appiattire un PDF che è un documento PDF non interattivo, si verifica un&#39;eccezione.

>[!NOTE]
>
> Per ulteriori informazioni sul servizio Output, consultate Riferimento [servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-9}

Per convertire un documento PDF interattivo in un documento PDF non interattivo, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un oggetto Client di output.
1. Recuperare un documento PDF interattivo.
1. Trasforma il documento PDF.
1. Salvare il documento PDF non interattivo come file PDF.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, accertatevi di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è distribuito su JBoss)
* jbossall-client.jar (richiesto se AEM Forms è distribuito su JBoss)

se AEM Forms è distribuito su un server applicazione J2EE supportato che non sia JBoss, dovrete sostituire i file adobe-utilities.jar e jbossall-client.jar con file JAR specifici del server applicazione J2EE su cui è distribuito AEM Forms. Per informazioni sulla posizione di tutti i file AEM Forms JAR, consultate [Inclusione dei file](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)di libreria Java AEM Forms.

**Creare un oggetto Client di output**

Prima di eseguire un&#39;operazione del servizio Output a livello di programmazione, è necessario creare un oggetto client del servizio Output. Se utilizzate l&#39;API Java, create un `OutputClient` oggetto. Se si utilizza l&#39;API del servizio Web Output, creare un `OutputServiceService` oggetto.

**Recuperare un documento PDF interattivo**

Recuperare un documento PDF interattivo da trasformare in un documento PDF non interattivo. Se si tenta di trasformare un documento PDF non interattivo, si verifica un&#39;eccezione.

**Trasformare il documento PDF**

Dopo aver recuperato un documento PDF interattivo, è possibile trasformarlo in un documento PDF non interattivo. Il servizio Output restituisce un documento PDF non interattivo.

**Salvare il documento PDF non interattivo come file PDF**

È possibile salvare il documento PDF non interattivo come file PDF.

**Consulta anche**

[Appiattire un documento PDF utilizzando l&#39;API Java](creating-document-output-streams.md#flatten-a-pdf-document-using-the-java-api)

[Appiattisci un documento PDF utilizzando l&#39;API del servizio Web](creating-document-output-streams.md#flatten-a-pdf-document-using-the-web-service-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API di Output Service](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Appiattire un documento PDF utilizzando l&#39;API Java {#flatten-a-pdf-document-using-the-java-api}

Appiattisci un documento PDF interattivo su un documento PDF non interattivo utilizzando l&#39;API di output (Java):

1. Includere i file di progetto.

   Includete file JAR client, ad esempio adobe-output-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto Client di output.

   * Creare un `ServiceClientFactory` oggetto che contenga proprietà di connessione.
   * Creare un `OutputClient` oggetto utilizzando il relativo costruttore e passando l&#39; `ServiceClientFactory` oggetto.

1. Recuperare un documento PDF interattivo.

   * Creare un `java.io.FileInputStream` oggetto che rappresenti il documento PDF interattivo da trasformare utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del file PDF interattivo.
   * Creare un `com.adobe.idp.Document` oggetto utilizzando il relativo costruttore e passando l&#39; `java.io.FileInputStream` oggetto.

1. Trasforma il documento PDF.

   Trasformare il documento PDF interattivo in un documento PDF non interattivo richiamando il metodo dell&#39; `OutputServiceService` oggetto `transformPDF` e passando i seguenti valori:

   * L&#39; `com.adobe.idp.Document` oggetto che contiene il documento PDF interattivo.
   * Un valore `TransformationFormat` enum. Per generare un documento PDF non interattivo, specificare `TransformationFormat.PDF`.
   * Un valore `PDFARevisionNumber` enum che specifica il numero di revisione. Poiché questo parametro è destinato a un documento PDF/A, è possibile specificare `null`.
   * Valore stringa che rappresenta il numero e l&#39;anno della modifica, separati da due punti. Poiché questo parametro è destinato a un documento PDF/A, è possibile specificare `null`.
   * Un valore `PDFAConformance` enum che rappresenta il livello di conformità PDF/A. Poiché questo parametro è destinato a un documento PDF/A, è possibile specificare `null`.
   Il `transformPDF` metodo restituisce un `com.adobe.idp.Document` oggetto che contiene un documento PDF non interattivo.

1. Salvare il documento PDF non interattivo come file PDF.

   * Create un `java.io.File` oggetto e accertatevi che l&#39;estensione del nome del file sia .pdf.
   * Richiamare il metodo dell&#39; `Document` oggetto `copyToFile` per copiare il contenuto dell&#39; `Document` oggetto nel file (assicurarsi di utilizzare l&#39; `Document` oggetto restituito dal `transformPDF` metodo).

**Consulta anche**

[Riepilogo dei passaggi](creating-document-output-streams.md#summary-of-steps)

[Avvio rapido (modalità EJB): Trasformazione di un documento PDF tramite l&#39;API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-transforming-a-pdf-document-using-the-java-api)

[Avvio rapido (modalità SOAP): Trasformazione di un documento PDF tramite l&#39;API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-transforming-a-pdf-document-using-the-java-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Appiattisci un documento PDF utilizzando l&#39;API del servizio Web {#flatten-a-pdf-document-using-the-web-service-api}

Appiattisci un documento PDF interattivo su un documento PDF non interattivo utilizzando l&#39;API di Output (servizio Web):

1. Includere i file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituire `localhost` con l&#39;indirizzo IP del server in cui è installato AEM Forms.

1. Creare un oggetto Client di output.

   * Creare un `OutputServiceClient` oggetto utilizzando il relativo costruttore predefinito.
   * Creare un `OutputServiceClient.Endpoint.Address` oggetto utilizzando il `System.ServiceModel.EndpointAddress` costruttore. Passa un valore di stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/OutputService?blob=mtom`.) Non è necessario utilizzare l&#39; `lc_version` attributo. Questo attributo viene utilizzato quando create un riferimento a un servizio. Tuttavia, specificate `?blob=mtom` per utilizzare MTOM.
   * Creare un `System.ServiceModel.BasicHttpBinding` oggetto ottenendo il valore del `OutputServiceClient.Endpoint.Binding` campo. Inserite il valore restituito in `BasicHttpBinding`.
   * Impostare il campo `System.ServiceModel.BasicHttpBinding` dell&#39; `MessageEncoding` oggetto su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilitate l&#39;autenticazione HTTP di base eseguendo le seguenti operazioni:

      * Assegnare il nome utente dei moduli AEM al campo `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `OutputServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recuperare un documento PDF interattivo.

   * Creare un `BLOB` oggetto utilizzando il relativo costruttore. L&#39; `BLOB` oggetto viene utilizzato per memorizzare il documento PDF interattivo.
   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF interattivo.
   * Creare un array di byte che memorizza il contenuto dell&#39; `System.IO.FileStream` oggetto. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà dell&#39; `System.IO.FileStream` oggetto `Length` .
   * Compilare l&#39;array di byte con i dati del flusso richiamando il `System.IO.FileStream` `Read` metodo dell&#39;oggetto e passando l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39; `BLOB` oggetto assegnandone `MTOM` la proprietà con il contenuto dell&#39;array di byte.

1. Trasforma il documento PDF.

   Trasformare il documento PDF interattivo in un documento PDF non interattivo richiamando il metodo dell&#39; `OutputClient` oggetto `transformPDF` e passando i seguenti valori:

   * Un `BLOB` oggetto che contiene il documento PDF interattivo.
   * Un valore `TransformationFormat` di enumerazione. Per generare un documento PDF non interattivo, specificare `TransformationFormat.PDF`.
   * Un valore `PDFARevisionNumber` enum che specifica il numero di revisione.
   * Un valore booleano che specifica se viene utilizzato il valore `PDFARevisionNumber` enum. Poiché questo parametro è destinato a un documento PDF/A, è possibile specificare `false`.
   * Valore stringa che rappresenta il numero e l&#39;anno della modifica, separati da due punti. Poiché questo parametro è destinato a un documento PDF/A, è possibile specificare `null`.
   * Un valore `PDFAConformance` enum che rappresenta il livello di conformità PDF/A.
   * Valore booleano che specifica se viene utilizzato il valore `PDFAConformance` enum. Poiché questo parametro è destinato a un documento PDF/A, è possibile specificare `false`.
   Il `transformPDF` metodo restituisce un `BLOB` oggetto che contiene un documento PDF non interattivo.

1. Salvare il documento PDF non interattivo come file PDF.

   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF non interattivo.
   * Creare un array di byte che memorizza il contenuto dei dati dell&#39; `BLOB` oggetto restituito dal `transformPDF` metodo. Compilare l&#39;array di byte ottenendo il valore del membro `BLOB` dati dell&#39; `MTOM` oggetto.
   * Creare un `System.IO.BinaryWriter` oggetto richiamando il relativo costruttore e passando l&#39; `System.IO.FileStream` oggetto.
   * Scrivere il contenuto dell&#39;array di byte in un file PDF richiamando il metodo dell&#39; `System.IO.BinaryWriter` oggetto `Write` e passando l&#39;array di byte.

**Consulta anche**

[Riepilogo dei passaggi](creating-document-output-streams.md#summary-of-steps)

[Attivazione di moduli AEM tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamo di moduli AEM con SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
