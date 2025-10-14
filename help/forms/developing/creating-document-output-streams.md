---
title: Creazione di flussi di output dei documenti
description: Utilizzare il servizio Output per convertire i documenti come formati PDF (inclusi i documenti PDF/A), PostScript, Printer Control Language (PCL) e Zebra - ZPL, Intermec - IPL, Datamax - DPL e TecToshiba - TPCL.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: a521bfac-f417-4002-9c5c-8d7794d3eec7
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '18860'
ht-degree: 0%

---

# Creazione di flussi di output dei documenti  {#creating-document-output-streams}

**Gli esempi e gli esempi contenuti in questo documento sono solo per AEM Forms in ambiente JEE.**

**Informazioni sul servizio di output**

Il servizio Output consente di eseguire l&#39;output di documenti come PDF (inclusi documenti PDF/A), PostScript, Printer Control Language (PCL) e nei seguenti formati di etichetta:

* Zebra - ZPL
* Intermec - IPL
* Datamax - DPL
* TecToshiba - TPCL

Tramite il servizio di output è possibile unire i dati del modulo XML con la struttura di un modulo e inviare il documento a una stampante o a un file di rete.

Esistono due modi per passare una progettazione di un modulo (un file XDP) al servizio di output. È possibile passare un&#39;istanza `com.adobe.idp.Document` contenente una struttura di modulo al servizio di output. In alternativa, è possibile passare un valore URI che specifichi la posizione della struttura del modulo. Entrambi questi modi sono trattati in *Programmazione con moduli AEM*.

>[!NOTE]
>
>Il servizio di output non supporta i documenti Acroform PDF che contengono script specifici per oggetti applicativi. I documenti Acroform PDF che contengono script specifici di oggetti applicativi non vengono sottoposti a rendering.

Nelle sezioni seguenti viene illustrato come passare una progettazione di modulo al servizio di output utilizzando un valore URI:

* [Creazione di documenti PDF](creating-document-output-streams.md#creating-pdf-documents)
* [Creazione di documenti PDF/A](creating-document-output-streams.md#creating-pdf-a-documents)

Nelle sezioni seguenti viene illustrato come passare una struttura di modulo all&#39;interno di un&#39;istanza `com.adobe.idp.Document`:

* [Passaggio di documenti in Content Services (obsoleto) al servizio di output](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)
* [Creazione di documenti PDF tramite frammenti](creating-document-output-streams.md#creating-pdf-documents-using-fragments)

Per decidere quale tecnica utilizzare, è importante considerare se si sta ottenendo la progettazione del modulo da un altro servizio AEM Forms, quindi trasmetterla all&#39;interno di un&#39;istanza `com.adobe.idp.Document`. Entrambe le sezioni *Passaggio dei documenti al servizio di output* e *Creazione di documenti PDF mediante frammenti* mostrano come ottenere una struttura di modulo da un altro servizio AEM Forms. La prima sezione recupera la progettazione del modulo da Content Services (obsoleto). La seconda sezione recupera la progettazione del modulo dal servizio Assembler.

Se la progettazione del modulo viene ottenuta da una posizione fissa, ad esempio il file system, è possibile utilizzare entrambe le tecniche. In altre parole, è possibile specificare il valore URI in un file XDP o utilizzare un&#39;istanza `com.adobe.idp.Document`.

Per passare un valore URI che specifichi la posizione della struttura del modulo durante la creazione di un documento PDF, utilizzare il metodo `generatePDFOutput`. Allo stesso modo, per passare un&#39;istanza `com.adobe.idp.Document` al servizio di output durante la creazione di un documento PDF, utilizzare il metodo `generatePDFOutput2`.

Quando si invia un flusso di output a una stampante di rete, è anche possibile utilizzare una delle due tecniche. Per inviare un flusso di output a una stampante passando un&#39;istanza `com.adobe.idp.Document` contenente una struttura di modulo, utilizzare il metodo `sendToPrinter2`. Per inviare un flusso di output a una stampante passando un valore URI, utilizzare il metodo `sendToPrinter`. La sezione *Invio di flussi di stampa alle stampanti* utilizza il metodo `sendToPrinter`.

Puoi eseguire queste attività utilizzando il servizio di output:

* [Creazione di documenti PDF](creating-document-output-streams.md#creating-pdf-documents)
* [Creazione di documenti PDF/A](creating-document-output-streams.md#creating-pdf-a-documents)
* [Passaggio di documenti in Content Services (obsoleto) al servizio di output](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)
* [Creazione di documenti PDF tramite frammenti](creating-document-output-streams.md#creating-pdf-documents-using-fragments)
* [Stampa su file](creating-document-output-streams.md#printing-to-files)
* [Invio di flussi di stampa alle stampanti](creating-document-output-streams.md#sending-print-streams-to-printers)
* [Creazione di più file di output](creating-document-output-streams.md#creating-multiple-output-files)
* [Creazione di regole di ricerca](creating-document-output-streams.md#creating-search-rules)
* [Appiattimento documenti PDF](creating-document-output-streams.md#flattening-pdf-documents)

>[!NOTE]
>
>Per ulteriori informazioni sul servizio di output, vedere [Riferimento ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Creazione di documenti PDF {#creating-pdf-documents}

È possibile utilizzare il servizio Output per creare un documento PDF basato sulla struttura di un modulo e sui dati del modulo XML forniti. Il documento PDF creato dal servizio di output non è un documento PDF interattivo. L&#39;utente non può immettere o modificare i dati del modulo.

Se desideri creare un documento PDF per l’archiviazione a lungo termine, ti consigliamo di creare un documento PDF/A. (Vedi [Creazione di documenti PDF/A](creating-document-output-streams.md#creating-pdf-a-documents).)

Per creare un modulo PDF interattivo che consenta a un utente di immettere dati, utilizza il servizio Forms. (Vedi [Rendering dei PDF forms interattivi](/help/forms/developing/rendering-forms.md#rendering-interactive-pdf-forms).)

>[!NOTE]
>
>Per ulteriori informazioni sul servizio di output, vedere [Riferimento ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary-of-steps}

Per creare un documento PDF, effettuare le seguenti operazioni:

1. Includi file di progetto.
1. Creare un oggetto client di output.
1. Fare riferimento a un&#39;origine dati XML.
1. Impostare le opzioni di runtime di PDF.
1. Impostate le opzioni di runtime per il rendering.
1. Genera un documento PDF.
1. Recuperate i risultati dell&#39;operazione.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è implementato su JBoss)
* jbossall-client.jar (obbligatorio se AEM Forms è distribuito su JBoss)

se AEM Forms viene distribuito su un server applicazioni J2EE supportato che non è JBoss, è necessario sostituire i file adobe-utilities.jar e jbossall-client.jar con file JAR specifici per il server applicazioni J2EE in cui viene distribuito AEM Forms.

**Crea un oggetto client di output**

Prima di poter eseguire un&#39;operazione del servizio di output a livello di programmazione, è necessario creare un oggetto client del servizio di output. Se si utilizza l&#39;API Java, creare un oggetto `OutputClient`. Se si utilizza l&#39;API del servizio Web di output, creare un oggetto `OutputServiceService`.

**Riferimento a un&#39;origine dati XML**

Per unire i dati con la struttura del modulo, è necessario fare riferimento a un&#39;origine dati XML che contiene dati. Un elemento XML deve esistere per ogni campo modulo che si intende compilare con i dati. Il nome dell&#39;elemento XML deve corrispondere al nome del campo. Un elemento XML viene ignorato se non corrisponde a un campo modulo o se il nome dell&#39;elemento XML non corrisponde al nome del campo. Se vengono specificati tutti gli elementi XML, non è necessario che l&#39;ordine di visualizzazione degli elementi XML corrisponda a quello specificato.

Prendi in considerazione il seguente esempio di modulo di richiesta di prestito.

![cp_cp_loanformdata](assets/cp_cp_loanformdata.png)

Per unire i dati in questa struttura di modulo, è necessario creare un&#39;origine dati XML corrispondente al modulo. Il codice XML seguente rappresenta un&#39;origine dati XML XDP che corrisponde al modulo di applicazione ipotecaria di esempio.

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

**Imposta opzioni runtime di PDF**

Impostare l&#39;opzione URI file durante la creazione di un documento PDF. Questa opzione specifica il nome e la posizione del file PDF generato dal servizio di output.

>[!NOTE]
>
>Invece di impostare l&#39;opzione di runtime URI del file, è possibile recuperare in modo programmatico il documento PDF dal tipo di dati complesso restituito dal servizio di output. Tuttavia, impostando l&#39;opzione di runtime URI del file, non è necessario creare una logica dell&#39;applicazione che recuperi il documento PDF a livello di programmazione.

**Impostare le opzioni di runtime di rendering**

È possibile impostare le opzioni di rendering in fase di esecuzione durante la creazione di un documento PDF. Anche se queste opzioni non sono obbligatorie (a differenza delle opzioni di runtime di PDF necessarie), è possibile eseguire attività quali il miglioramento delle prestazioni del servizio di output. È ad esempio possibile memorizzare in cache la struttura del modulo utilizzata dal servizio di output per migliorarne le prestazioni.

Se come input si utilizza un modulo Acrobat con tag, non è possibile utilizzare l’API del servizio di output Java o del servizio web per disattivare l’impostazione dei tag. Se si tenta di impostare questa opzione su `false` a livello di programmazione, il documento PDF risultante verrà comunque contrassegnato.

>[!NOTE]
>
>Se non specificate le opzioni di rendering in fase di esecuzione, vengono utilizzati i valori predefiniti. Per informazioni sul rendering delle opzioni di runtime, vedere il riferimento alla classe `RenderOptionsSpec`. (Vedi [Riferimento API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)).

**Generare un documento PDF**

Dopo aver fatto riferimento a un&#39;origine dati XML valida contenente dati del modulo e aver impostato le opzioni di runtime, è possibile richiamare il servizio di output, che genera un documento PDF.

Durante la generazione di un documento PDF, è possibile specificare i valori URI richiesti dal servizio di output per la creazione di un documento PDF. La progettazione di un modulo può essere archiviata in posizioni quali il file system del server o come parte di un&#39;applicazione AEM Forms. È possibile fare riferimento a una struttura del modulo (o ad altre risorse, ad esempio un file di immagine) esistente come parte di un&#39;applicazione Forms utilizzando il valore URI radice del contenuto `repository:///`. Si consideri ad esempio il seguente design di modulo denominato *Loan.xdp* che si trova all&#39;interno di un&#39;applicazione Forms denominata *Applications/FormsApplication*:

![cp_cp_formrepository](assets/cp_cp_formrepository.png)

Per accedere al file Loan.xdp illustrato nella figura precedente, specificare `repository:///Applications/FormsApplication/1.0/FormsFolder/` come terzo parametro passato al metodo `generatePDFOutput` dell&#39;oggetto `OutputClient`. Specificare il nome del modulo (*Loan.xdp*) come secondo parametro passato al metodo `generatePDFOutput` dell&#39;oggetto `OutputClient`.

Se il file XDP contiene immagini (o altre risorse, ad esempio frammenti), posiziona le risorse nella stessa cartella dell’applicazione del file XDP. AEM Forms utilizza l’URI della directory principale dei contenuti come percorso di base per risolvere i riferimenti alle immagini. Se ad esempio il file Loan.xdp contiene un&#39;immagine, assicurarsi di inserirla in `Applications/FormsApplication/1.0/FormsFolder/`.

>[!NOTE]
>
>È possibile fare riferimento all&#39;URI di un&#39;applicazione Forms quando si richiamano i metodi `generatePDFOutput` o `generatePrintedOutput` dell&#39;oggetto `OutputClient`.

>[!NOTE]
>
>Per visualizzare un avvio rapido completo che crea un documento PDF facendo riferimento a un XDP in un&#39;applicazione Forms, vedere [Avvio rapido (modalità EJB): creazione di un documento PDF basato su un file XDP dell&#39;applicazione mediante l&#39;API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-an-application-xdp-file-using-the-java-api).

**Recupera i risultati dell&#39;operazione**

Dopo aver eseguito un&#39;operazione, il servizio di output restituisce vari elementi di dati, ad esempio dati XML di stato, che specificano se l&#39;operazione è stata eseguita correttamente.

**Consulta anche**

[Creare un documento PDF utilizzando l’API Java](creating-document-output-streams.md#create-a-pdf-document-using-the-java-api)

[Creare un documento PDF utilizzando l’API del servizio web](creating-document-output-streams.md#create-a-pdf-document-using-the-web-service-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API servizio di output](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Creare un documento PDF utilizzando l’API Java {#create-a-pdf-document-using-the-java-api}

Crea un documento PDF utilizzando l’API di output (Java):

1. Includi file di progetto.

   Includi i file JAR client, come adobe-output-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto client di output.

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `OutputClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Fare riferimento a un&#39;origine dati XML.

   * Creare un oggetto `java.io.FileInputStream` che rappresenta l&#39;origine dati XML utilizzata per popolare il documento PDF utilizzando il relativo costruttore e passando un valore stringa che specifica la posizione del file XML.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore. Passa l&#39;oggetto `java.io.FileInputStream`.

1. Impostare le opzioni di runtime di PDF.

   * Creare un oggetto `PDFOutputOptionsSpec` utilizzando il relativo costruttore.
   * Impostare l&#39;opzione URI file richiamando il metodo `setFileURI` dell&#39;oggetto `PDFOutputOptionsSpec`. Passa un valore stringa che specifica la posizione del file PDF generato dal servizio di output. L&#39;opzione URI file è relativa al server applicazioni J2EE che ospita AEM Forms, non al computer client.

1. Impostate le opzioni di runtime per il rendering.

   * Creare un oggetto `RenderOptionsSpec` utilizzando il relativo costruttore.
   * Memorizza nella cache la struttura del modulo per migliorare le prestazioni del servizio di output richiamando `setCacheEnabled` dell&#39;oggetto `RenderOptionsSpec` e passando `true`.

   >[!NOTE]
   >
   >Impossibile impostare la versione del documento PDF utilizzando il metodo `setPdfVersion` dell&#39;oggetto `RenderOptionsSpec` se il documento di input è un modulo di Acrobat (un modulo creato in Acrobat) o un documento XFA firmato o certificato. Il documento PDF di output conserva la versione originale di PDF. Analogamente, non è possibile impostare l&#39;opzione Adobe PDF con tag richiamando il metodo `setTaggedPDF` dell&#39;oggetto `RenderOptionsSpec` se il documento di input è un modulo Acrobat o un documento XFA firmato o certificato.

   >[!NOTE]
   >
   >Impossibile impostare l&#39;opzione PDF linearizzato utilizzando il metodo `setLinearizedPDF` dell&#39;oggetto `RenderOptionsSpec` se il documento PDF di input è certificato o firmato digitalmente. (Vedi [Documenti Di PDF Con Firma Digitale &#x200B;](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)*.)*

1. Genera un documento PDF.

   Creare un documento PDF richiamando il metodo `generatePDFOutput` dell&#39;oggetto `OutputClient` e passando i valori seguenti:

   * Valore di enumerazione `TransformationFormat`. Per generare un documento PDF, specificare `TransformationFormat.PDF`.
   * Valore stringa che specifica il nome della struttura del modulo.
   * Valore stringa che specifica la directory principale del contenuto in cui si trova la struttura del modulo.
   * Oggetto `PDFOutputOptionsSpec` contenente le opzioni di runtime di PDF.
   * Oggetto `RenderOptionsSpec` contenente le opzioni di rendering in fase di esecuzione.
   * Oggetto `com.adobe.idp.Document` contenente l&#39;origine dati XML contenente i dati da unire con la struttura del modulo.

   Il metodo `generatePDFOutput` restituisce un oggetto `OutputResult` contenente i risultati dell&#39;operazione.

   >[!NOTE]
   >
   >Quando si genera un documento PDF richiamando il metodo `generatePDFOutput`, non è possibile unire i dati con un modulo PDF XFA firmato o certificato. (Vedi [Documenti di firma digitale e certificazione &#x200B;](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-and-certifying-documents)*.)*

   >[!NOTE]
   >
   >Il metodo `getRecordLevelMetaDataList` dell&#39;oggetto `OutputResult` restituisce `null`*.*

   >[!NOTE]
   >
   >È inoltre possibile creare un documento PDF richiamando il metodo `generatePDFOutput2` dell&#39;oggetto `OutputClient`. (Vedi [Passaggio dei documenti in Content Services (obsoleto) al servizio di output &#x200B;](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)*.)*

1. Recuperate i risultati dell&#39;operazione.

   * Recuperare un oggetto `com.adobe.idp.Document` che rappresenta lo stato dell&#39;operazione `generatePDFOutput` richiamando il metodo `getStatusDoc` dell&#39;oggetto `OutputResult`. Questo metodo restituisce dati XML di stato che specificano se l&#39;operazione è stata eseguita correttamente.
   * Creare un oggetto `java.io.File` contenente i risultati dell&#39;operazione. Verificare che l&#39;estensione del nome file sia .xml.
   * Richiamare il metodo `copyToFile` dell&#39;oggetto `com.adobe.idp.Document` per copiare il contenuto dell&#39;oggetto `com.adobe.idp.Document` nel file (assicurarsi di utilizzare l&#39;oggetto `com.adobe.idp.Document` restituito dal metodo `getStatusDoc`).

   Sebbene il servizio di output scriva il documento PDF nella posizione specificata dall&#39;argomento passato al metodo `setFileURI` dell&#39;oggetto `PDFOutputOptionsSpec`, è possibile recuperare in modo programmatico il documento PDF/A richiamando il metodo `getGeneratedDoc` dell&#39;oggetto `OutputResult`.

**Consulta anche**

[Riepilogo dei passaggi](creating-document-output-streams.md#summary-of-steps)

[Guida rapida (modalità EJB): creazione di un documento PDF tramite l’API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-using-the-java-api)

[Guida rapida (modalità SOAP): creazione di un documento PDF tramite l’API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Creare un documento PDF utilizzando l’API del servizio web {#create-a-pdf-document-using-the-web-service-api}

Crea un documento PDF utilizzando l’API di output (servizio web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Creare un oggetto client di output.

   * Creare un oggetto `OutputServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `OutputServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/OutputService?blob=mtom`). Non è necessario utilizzare l&#39;attributo `lc_version`. Questo attributo viene utilizzato quando si crea un riferimento a un servizio. Tuttavia, specificare `?blob=mtom` per utilizzare MTOM.
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `OutputServiceClient.Endpoint.Binding`. Eseguire il cast del valore restituito in `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegnare il nome utente dei moduli AEM al campo `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `OutputServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Fare riferimento a un&#39;origine dati XML.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare i dati XML che verranno uniti al documento PDF.
   * Creare un oggetto `System.IO.FileStream` richiamandone il costruttore e passando un valore stringa che rappresenta la posizione del file XML contenente i dati del modulo.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni della matrice di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare la matrice di byte con i dati di flusso richiamando il metodo `Read` dell&#39;oggetto `System.IO.FileStream` e passando la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando il relativo campo `MTOM` al contenuto della matrice di byte.

1. Imposta opzioni runtime di PDF

   * Creare un oggetto `PDFOutputOptionsSpec` utilizzando il relativo costruttore.
   * Impostare l&#39;opzione URI file assegnando un valore stringa che specifichi la posizione del file PDF generato dal servizio di output al membro dati `fileURI` dell&#39;oggetto `PDFOutputOptionsSpec`. L&#39;opzione URI file è relativa al server applicazioni J2EE che ospita AEM Forms, non al computer client.

1. Impostate le opzioni di runtime per il rendering.

   * Creare un oggetto `RenderOptionsSpec` utilizzando il relativo costruttore.
   * Memorizza nella cache la struttura del modulo per migliorare le prestazioni del servizio di output assegnando il valore `true` al membro dati `cacheEnabled` dell&#39;oggetto `RenderOptionsSpec`.

   >[!NOTE]
   >
   >Impossibile impostare la versione del documento PDF utilizzando il metodo `setPdfVersion` dell&#39;oggetto `RenderOptionsSpec` se il documento di input è un modulo di Acrobat (un modulo creato in Acrobat) o un documento XFA firmato o certificato. Il documento PDF di output conserva la versione originale di PDF. Analogamente, non è possibile impostare l&#39;opzione Adobe PDF con tag richiamando il metodo `setTaggedPDF`* dell&#39;oggetto `RenderOptionsSpec` se il documento di input è un modulo Acrobat o un documento XFA firmato o certificato.*

   >[!NOTE]
   >
   >Impossibile impostare l&#39;opzione PDF linearizzato utilizzando il membro `linearizedPDF` dell&#39;oggetto `RenderOptionsSpec` se il documento PDF di input è certificato o firmato digitalmente. (Vedi [Documenti Di PDF Con Firma Digitale &#x200B;](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)*.)*

1. Genera un documento PDF.

   Creare un documento PDF richiamando il metodo `generatePDFOutput` dell&#39;oggetto `OutputServiceService` e passando i valori seguenti:

   * Valore di enumerazione `TransformationFormat`. Per generare un documento PDF, specificare `TransformationFormat.PDF`.
   * Valore stringa che specifica il nome della struttura del modulo.
   * Valore stringa che specifica la directory principale del contenuto in cui si trova la struttura del modulo.
   * Oggetto `PDFOutputOptionsSpec` contenente le opzioni di runtime di PDF.
   * Oggetto `RenderOptionsSpec` contenente le opzioni di rendering in fase di esecuzione.
   * Oggetto `BLOB` contenente l&#39;origine dati XML contenente i dati da unire con la struttura del modulo.
   * Oggetto `BLOB` popolato dal metodo `generatePDFOutput`. Il metodo `generatePDFOutput` popola questo oggetto con i metadati generati che descrivono il documento. (Questo valore di parametro è richiesto solo per la chiamata del servizio Web).
   * Oggetto `BLOB` popolato dal metodo `generatePDFOutput`. Il metodo `generatePDFOutput` popola questo oggetto con i dati dei risultati. (Questo valore di parametro è richiesto solo per la chiamata del servizio Web).
   * Oggetto `OutputResult` contenente i risultati dell&#39;operazione. (Questo valore di parametro è richiesto solo per la chiamata del servizio Web).

   >[!NOTE]
   >
   >Quando si genera un documento PDF richiamando il metodo `generatePDFOutput`, non è possibile unire i dati con un modulo PDF XFA firmato o certificato. (Vedi [Documenti di firma digitale e certificazione &#x200B;](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-and-certifying-documents)*.)*

   >[!NOTE]
   >
   >È inoltre possibile creare un documento PDF richiamando il metodo `generatePDFOutput2` dell&#39;oggetto `OutputClient`. (Vedi [Passaggio dei documenti in Content Services (obsoleto) al servizio di output &#x200B;](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)*.)*

1. Recuperate i risultati dell&#39;operazione.

   * Creare un oggetto `System.IO.FileStream` richiamandone il costruttore e passando un valore stringa che rappresenta un percorso di file XML contenente i dati dei risultati. Verificare che l&#39;estensione del nome file sia .xml.
   * Creare una matrice di byte che memorizza il contenuto dei dati dell&#39;oggetto `BLOB` che è stato popolato con i dati dei risultati dal metodo `generatePDFOutput` dell&#39;oggetto `OutputServiceService` (ottavo parametro). Compilare la matrice di byte ottenendo il valore di `MTOM` `field` dell&#39;oggetto `BLOB`.
   * Creare un oggetto `System.IO.BinaryWriter` richiamandone il costruttore e passando l&#39;oggetto `System.IO.FileStream`.
   * Scrivere il contenuto della matrice di byte nel file XML richiamando il metodo `Write` dell&#39;oggetto `System.IO.BinaryWriter` e passando la matrice di byte.

   Consulta anche

[Riepilogo dei passaggi](creating-document-output-streams.md#summary-of-steps)

[Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamare AEM Forms con SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

   >[!NOTE]
   >
   >Metodo `generateOutput` dell&#39;oggetto `OutputServiceService` obsoleto.

## Creazione di documenti PDF/A {#creating-pdf-a-documents}

È possibile utilizzare il servizio di output per creare un documento PDF/A. Poiché PDF/A è un formato di archiviazione per la conservazione a lungo termine del contenuto del documento, tutti i font vengono incorporati e il file non viene compresso. Di conseguenza, un documento PDF/A è generalmente più grande di un documento PDF standard. Inoltre, un documento PDF/A non contiene contenuti audio e video. Analogamente ad altre attività del servizio di output, è possibile fornire sia una struttura di modulo che dati da unire a una struttura di modulo per creare un documento PDF/A.

La specifica PDF/A-1 è costituita da due livelli di conformità, ovvero a e b. La differenza principale tra i due è relativa al supporto della struttura logica (accessibilità), che non è richiesto per il livello di conformità b. Indipendentemente dal livello di conformità, PDF/A-1 stabilisce che tutti i font sono incorporati nel documento PDF/A generato.

Sebbene PDF/A sia lo standard per l&#39;archiviazione dei documenti PDF PDF, non è obbligatorio utilizzarlo per l&#39;archiviazione se un documento PDF standard soddisfa le esigenze della società. Lo scopo dello standard PDF/A è quello di stabilire un file PDF che possa essere memorizzato per un lungo periodo di tempo e che soddisfi i requisiti di conservazione dei documenti. Ad esempio, non è possibile incorporare un URL in un PDF/A perché nel tempo l’URL potrebbe diventare non valido.

L&#39;organizzazione deve valutare le proprie esigenze, il periodo di tempo in cui si intende conservare il documento, le considerazioni sulla dimensione del file e determinare la propria strategia di archiviazione. È possibile determinare a livello di programmazione se un documento PDF è compatibile con PDF/A utilizzando il servizio DocConverter. (Vedi [Determinazione A Livello Di Programmazione Della Conformità Di PDF/A](/help/forms/developing/pdf-a-documents.md#programmatically-determining-pdf-a-compliancy).)

Un documento di PDF/A deve utilizzare il tipo di carattere specificato nella struttura del modulo e non può essere sostituito. Di conseguenza, se un tipo di carattere che si trova all&#39;interno di un documento PDF non è disponibile nel sistema operativo host, si verifica un&#39;eccezione.

Quando un documento PDF/A viene aperto in Acrobat, viene visualizzato un messaggio che conferma che il documento è un documento PDF/A, come illustrato nella figura seguente.

![cp_cp_pdfamessage](assets/cp_cp_pdfamessage.png)

>[!NOTE]
>
>Il sito Web AIIM contiene una sezione di domande frequenti su PDF/A a cui è possibile accedere all&#39;indirizzo [https://www.loc.gov/preservation/digital/formats/fdd/fdd000125.shtml](https://www.loc.gov/preservation/digital/formats/fdd/fdd000125.shtml).

>[!NOTE]
>
>Per ulteriori informazioni sul servizio di output, vedere [Riferimento ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_65).

### Riepilogo dei passaggi {#summary_of_steps-1}

Per creare un documento PDF/A, effettuare le seguenti operazioni:

1. Includi file di progetto.
1. Creare un oggetto client di output.
1. Fare riferimento a un&#39;origine dati XML.
1. Impostare le opzioni di runtime di PDF/A.
1. Impostate le opzioni di runtime per il rendering.
1. Genera un documento PDF/A.
1. Recuperate i risultati dell&#39;operazione.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione personalizzata utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso della classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è implementato su JBoss)
* jbossall-client.jar (obbligatorio se AEM Forms è distribuito su JBoss)

se AEM Forms viene distribuito su un server applicazioni J2EE supportato che non è JBoss, è necessario sostituire i file adobe-utilities.jar e jbossall-client.jar con file JAR specifici per il server applicazioni J2EE in cui viene distribuito AEM Forms.

**Crea un oggetto client di output**

Prima di poter eseguire un&#39;operazione del servizio di output a livello di programmazione, è necessario creare un oggetto client del servizio di output. Se si utilizza l&#39;API Java, creare un oggetto `OutputClient`. Se si utilizza l&#39;API del servizio Web di output, creare un oggetto `OutputServiceService`.

**Riferimento a un&#39;origine dati XML**

Per unire i dati con la struttura del modulo, è necessario fare riferimento a un&#39;origine dati XML che contiene dati. Un elemento XML deve esistere per ogni campo modulo che si desidera compilare con i dati. Il nome dell&#39;elemento XML deve corrispondere al nome del campo. Un elemento XML viene ignorato se non corrisponde a un campo modulo o se il nome dell&#39;elemento XML non corrisponde al nome del campo. Se vengono specificati tutti gli elementi XML, non è necessario che l&#39;ordine di visualizzazione degli elementi XML corrisponda a quello specificato.

**Impostare le opzioni di runtime di PDF/A**

È possibile impostare l&#39;opzione URI file durante la creazione di un documento PDF/A. L&#39;URI è relativo al server applicazioni J2EE che ospita AEM Forms. In altre parole, se si imposta C:\Adobe, il file viene scritto nella cartella sul server, non nel computer client. L&#39;URI specifica il nome e la posizione del file PDF/A generato dal servizio di output.

**Impostare le opzioni di runtime di rendering**

È possibile impostare le opzioni di rendering in fase di esecuzione durante la creazione di documenti PDF/A. È possibile impostare due opzioni PDF/A correlate: `PDFAConformance` e `PDFARevisionNumber`. Il valore `PDFAConformance` si riferisce alla conformità di un documento PDF ai requisiti che specificano il livello di conservazione dei documenti elettronici a lungo termine. I valori validi per questa opzione sono `A` e `B`. Per informazioni sulla conformità di livello a e b, vedere la specifica ISO PDF/A-1 con titolo *ISO 19005-1 Document Management*.

Il valore `PDFARevisionNumber` fa riferimento al numero di revisione di un documento PDF/A. Per informazioni sul numero di revisione di un documento PDF/A, vedere la specifica ISO PDF/A-1 con titolo *ISO 19005-1 Document Management*.

>[!NOTE]
>
>Impossibile impostare l&#39;opzione Adobe PDF con tag su `false` durante la creazione di un documento PDF/A 1A. PDF/A 1A sarà sempre un documento di PDF con tag. Inoltre, non è possibile impostare l&#39;opzione Adobe PDF con tag su `true` durante la creazione di un documento PDF/A 1B. PDF/A 1B sarà sempre un documento di PDF senza tag.

**Generare un documento PDF/A**

Dopo aver fatto riferimento a un&#39;origine dati XML valida che contiene dati del modulo e aver impostato le opzioni di runtime, è possibile richiamare il servizio di output per generare un documento PDF/A.

**Recupera i risultati dell&#39;operazione**

Dopo l&#39;esecuzione di un&#39;operazione, il servizio di output restituisce vari elementi di dati, ad esempio dati XML, che specificano se l&#39;operazione è stata eseguita correttamente.

**Consulta anche**

[Creare un documento PDF/A utilizzando l’API Java](creating-document-output-streams.md#create-a-pdf-a-document-using-the-java-api)

[Creare un documento PDF/A utilizzando l’API del servizio web](creating-document-output-streams.md#create-a-pdf-a-document-using-the-web-service-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API servizio di output](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Creare un documento PDF/A utilizzando l’API Java {#create-a-pdf-a-document-using-the-java-api}

Crea un documento PDF/A utilizzando l’API di output (Java):

1. Includi file di progetto.

   Includi i file JAR client, come adobe-output-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto client di output.

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `OutputClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Fare riferimento a un&#39;origine dati XML.

   * Creare un oggetto `java.io.FileInputStream` che rappresenta l&#39;origine dati XML utilizzata per popolare il documento PDF/A utilizzando il relativo costruttore e passando un valore stringa che specifica la posizione del file XML.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Impostare le opzioni di runtime di PDF/A.

   * Creare un oggetto `PDFOutputOptionsSpec` utilizzando il relativo costruttore.
   * Impostare l&#39;opzione URI file richiamando il metodo `setFileURI` dell&#39;oggetto `PDFOutputOptionsSpec`. Passa un valore stringa che specifica la posizione del file PDF generato dal servizio di output. L&#39;opzione URI file è relativa al server applicazioni J2EE che ospita AEM Forms, non al computer client.

1. Impostate le opzioni di runtime per il rendering.

   * Creare un oggetto `RenderOptionsSpec` utilizzando il relativo costruttore.
   * Impostare il valore `PDFAConformance` richiamando il metodo `setPDFAConformance` dell&#39;oggetto `RenderOptionsSpec` e passando un valore enum `PDFAConformance` che specifica il livello di conformità. Ad esempio, per specificare il livello di conformità A, passare `PDFAConformance.A`.
   * Impostare il valore `PDFARevisionNumber` richiamando il metodo `setPDFARevisionNumber` dell&#39;oggetto `RenderOptionsSpec` e passando `PDFARevisionNumber.Revision_1`.

   >[!NOTE]
   >
   >La versione PDF di un documento PDF/A è 1.4, indipendentemente dal valore specificato per il metodo `setPdfVersion`*dell&#39;oggetto `RenderOptionsSpec`.*

1. Genera un documento PDF/A.

   Creare un documento PDF/A richiamando il metodo `generatePDFOutput` dell&#39;oggetto `OutputClient` e passando i valori seguenti:

   * Valore di enumerazione `TransformationFormat`. Per generare un documento PDF/A, specificare `TransformationFormat.PDFA`.
   * Valore stringa che specifica il nome della struttura del modulo.
   * Valore stringa che specifica la directory principale del contenuto in cui si trova la struttura del modulo.
   * Oggetto `PDFOutputOptionsSpec` contenente le opzioni di runtime di PDF.
   * Oggetto `RenderOptionsSpec` contenente le opzioni di rendering in fase di esecuzione.
   * L&#39;oggetto `com.adobe.idp.Document` che contiene l&#39;origine dati XML contenente i dati da unire con la struttura del modulo.

   Il metodo `generatePDFOutput` restituisce un oggetto `OutputResult` contenente i risultati dell&#39;operazione.

   >[!NOTE]
   >
   >Il metodo `getRecordLevelMetaDataList` dell&#39;oggetto `OutputResult` restituisce `null`.

   >[!NOTE]
   >
   >È inoltre possibile creare un documento PDF/A richiamando il metodo `generatePDFOutput`2 dell&#39;oggetto `OutputClient`. (Vedere [Passaggio di documenti in Content Services (obsoleto) al servizio di output](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service).)

1. Recuperate i risultati dell&#39;operazione.

   * Creare un oggetto `com.adobe.idp.Document` che rappresenta lo stato del metodo `generatePDFOutput` richiamando il metodo `getStatusDoc` dell&#39;oggetto `OutputResult`.
   * Creare un oggetto `java.io.File` che conterrà i risultati dell&#39;operazione. Verificare che l&#39;estensione del nome file sia .xml.
   * Richiamare il metodo `copyToFile` dell&#39;oggetto `com.adobe.idp.Document` per copiare il contenuto dell&#39;oggetto `com.adobe.idp.Document` nel file (assicurarsi di utilizzare l&#39;oggetto `com.adobe.idp.Document` restituito dal metodo `getStatusDoc`).

   >[!NOTE]
   >
   >Sebbene il servizio di output scriva il documento PDF/A nella posizione specificata dall&#39;argomento passato al metodo `setFileURI` dell&#39;oggetto `PDFOutputOptionsSpec`, è possibile recuperare in modo programmatico il documento PDF/A richiamando il metodo `getGeneratedDoc` dell&#39;oggetto `OutputResult`.

**Consulta anche**

[Riepilogo dei passaggi](creating-document-output-streams.md#summary-of-steps)

[Guida rapida (modalità SOAP): creazione di un documento PDF/A tramite l’API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-a-document-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

### Creare un documento PDF/A utilizzando l’API del servizio web {#create-a-pdf-a-document-using-the-web-service-api}

Crea un documento PDF/A utilizzando l’API di output (servizio web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Creare un oggetto client di output.

   * Creare un oggetto `OutputServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `OutputServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/OutputService?blob=mtom`). Non è necessario utilizzare l&#39;attributo `lc_version`. Questo attributo viene utilizzato quando si crea un riferimento a un servizio. Tuttavia, specificare `?blob=mtom` per utilizzare MTOM.
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `OutputServiceClient.Endpoint.Binding`. Eseguire il cast del valore restituito in `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegnare il nome utente dei moduli AEM al campo `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `OutputServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Fare riferimento a un&#39;origine dati XML.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare i dati che verranno uniti al documento PDF/A.
   * Creare un oggetto `System.IO.FileStream` richiamandone il costruttore e passando un valore stringa che rappresenta la posizione del file del documento PDF da crittografare e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni della matrice di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare la matrice di byte con i dati di flusso richiamando il metodo `Read` dell&#39;oggetto `System.IO.FileStream` e passando la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando il relativo campo `MTOM` al contenuto della matrice di byte.

1. Impostare le opzioni di runtime di PDF/A.

   * Creare un oggetto `PDFOutputOptionsSpec` utilizzando il relativo costruttore.
   * Impostare l&#39;opzione URI file assegnando un valore stringa che specifichi la posizione del file PDF generato dal servizio di output al membro dati `fileURI` dell&#39;oggetto `PDFOutputOptionsSpec`. L&#39;opzione URI file è relativa al server applicazioni J2EE che ospita AEM Forms, non al computer client

1. Impostate le opzioni di runtime per il rendering.

   * Creare un oggetto `RenderOptionsSpec` utilizzando il relativo costruttore.
   * Impostare il valore `PDFAConformance` assegnando un valore enum `PDFAConformance` al membro dati `PDFAConformance` dell&#39;oggetto `RenderOptionsSpec`. Ad esempio, per specificare il livello di conformità A, assegnare `PDFAConformance.A` a questo membro dati.
   * Impostare il valore `PDFARevisionNumber` assegnando un valore enum `PDFARevisionNumber` al membro dati `PDFARevisionNumber` dell&#39;oggetto `RenderOptionsSpec`. Assegna `PDFARevisionNumber.Revision_1` a questo membro dati.

   >[!NOTE]
   >
   >La versione PDF di un documento PDF/A è 1.4, indipendentemente dal valore specificato.

1. Genera un documento PDF/A.

   Creare un documento PDF richiamando il metodo `generatePDFOutput` dell&#39;oggetto `OutputServiceService` e passando i valori seguenti:

   * Valore di enumerazione TransformationFormat. Per generare un documento PDF, specificare `TransformationFormat.PDFA`.
   * Valore stringa che specifica il nome della struttura del modulo.
   * Valore stringa che specifica la directory principale del contenuto in cui si trova la struttura del modulo.
   * Oggetto `PDFOutputOptionsSpec` contenente le opzioni di runtime di PDF.
   * Oggetto `RenderOptionsSpec` contenente le opzioni di rendering in fase di esecuzione.
   * Oggetto `BLOB` contenente l&#39;origine dati XML contenente i dati da unire con la struttura del modulo.
   * Oggetto `BLOB` popolato dal metodo `generatePDFOutput`. Il metodo `generatePDFOutput` popola questo oggetto con i metadati generati che descrivono il documento. (Questo valore di parametro è obbligatorio solo per le chiamate al servizio web).
   * Oggetto `BLOB` popolato dal metodo `generatePDFOutput`. Il metodo `generatePDFOutput` popola questo oggetto con i dati dei risultati. (Questo valore di parametro è obbligatorio solo per le chiamate al servizio web).
   * Oggetto `OutputResult` contenente i risultati dell&#39;operazione. (Questo valore di parametro è obbligatorio solo per le chiamate al servizio web).

   >[!NOTE]
   >
   >È inoltre possibile creare un documento PDF/A richiamando il metodo `generatePDFOutput`2 dell&#39;oggetto `OutputClient`. (Vedere [Passaggio di documenti in Content Services (obsoleto) al servizio di output](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service).)

1. Recuperate i risultati dell&#39;operazione.

   * Creare un oggetto `System.IO.FileStream` richiamandone il costruttore e passando un valore stringa che rappresenta un percorso di file XML contenente i dati dei risultati. Verificare che l&#39;estensione del nome file sia .xml.
   * Creare una matrice di byte che memorizza il contenuto dei dati dell&#39;oggetto `BLOB` che è stato popolato con i dati dei risultati dal metodo `generatePDFOutput` dell&#39;oggetto `OutputServiceService` (ottavo parametro). Compilare la matrice di byte ottenendo il valore del campo `MTOM` dell&#39;oggetto `BLOB`.
   * Creare un oggetto `System.IO.BinaryWriter` richiamandone il costruttore e passando l&#39;oggetto `System.IO.FileStream`.
   * Scrivere il contenuto della matrice di byte nel file XML richiamando il metodo `Write` dell&#39;oggetto `System.IO.BinaryWriter` e passando la matrice di byte.

**Consulta anche**

[Riepilogo dei passaggi](creating-document-output-streams.md#summary-of-steps)

[Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamare AEM Forms con SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Passaggio di documenti in Content Services (obsoleto) al servizio di output {#passing-documents-located-in-content-services-deprecated-to-the-output-service}

Il servizio di output esegue il rendering di un modulo di PDF non interattivo basato su una struttura di modulo in genere salvata come file XDP e creata in Designer. È possibile passare un oggetto `com.adobe.idp.Document` contenente la struttura del modulo al servizio di output. Il servizio di output esegue quindi il rendering della struttura del modulo nell&#39;oggetto `com.adobe.idp.Document`.

Un vantaggio del passaggio di un oggetto `com.adobe.idp.Document` al servizio di output è che altre operazioni del servizio AEM Forms restituiscono un&#39;istanza `com.adobe.idp.Document`. In altre parole, è possibile ottenere un&#39;istanza `com.adobe.idp.Document` da un&#39;altra operazione di servizio ed eseguirne il rendering. Si supponga, ad esempio, che un file XDP sia memorizzato in un nodo Content Services (obsoleto) denominato `/Company Home/Form Designs`, come illustrato nella figura seguente.

È possibile recuperare in modo programmatico Loan.xdp da Content Services (obsoleto) e passare il file XDP al servizio di output all&#39;interno di un oggetto `com.adobe.idp.Document`.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Forms, vedere [Riferimento ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-2}

Per passare un documento ottenuto da Content Services (obsoleto) al servizio di output, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Creare un oggetto Output e un oggetto API Client di Document Management.
1. Recupera la progettazione del modulo da Content Services (obsoleto).
1. Esegui il rendering del modulo di PDF non interattivo.
1. Eseguire un&#39;azione con il flusso di dati.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se si utilizzano servizi Web, includere i file proxy.

**Creare un output e un oggetto API client di gestione documenti**

Prima di poter eseguire un&#39;operazione API del servizio di output a livello di programmazione, creare un oggetto API del client di output. Inoltre, poiché questo flusso di lavoro recupera un file XDP da Content Services (obsoleto), crea un oggetto API di gestione dei documenti.

**Recupera la progettazione del modulo da Content Services (obsoleto)**

Recupera il file XDP da Content Services (obsoleto) utilizzando l’API Java o del servizio web. Il file XDP viene restituito all&#39;interno di un&#39;istanza `com.adobe.idp.Document` (o di un&#39;istanza `BLOB` se si utilizzano i servizi Web). È quindi possibile passare l&#39;istanza `com.adobe.idp.Document` al servizio di output.

**Eseguire il rendering del modulo di PDF non interattivo**

Per eseguire il rendering di un modulo non interattivo, passare l&#39;istanza `com.adobe.idp.Document` restituita da Content Services (obsoleta) al servizio di output.

>[!NOTE]
>
>Due nuovi metodi denominati `generatePDFOutput2` e g `eneratePrintedOutput2`accettano un oggetto `com.adobe.idp.Document` che contiene una struttura di modulo. È inoltre possibile passare un `com.adobe.idp.Document` contenente la struttura del modulo al servizio di output quando si invia un flusso di stampa a una stampante di rete.

**Esegui un&#39;azione con il flusso di dati del modulo**

È possibile salvare il modulo non interattivo come file PDF. Il modulo può essere visualizzato in Adobe Reader o Acrobat.

**Consulta anche**

[Trasmettere i documenti al servizio di output utilizzando l’API Java](creating-document-output-streams.md#pass-documents-to-the-output-service-using-the-java-api)

[Trasmettere i documenti al servizio di output utilizzando l’API del servizio web](creating-document-output-streams.md#pass-documents-to-the-output-service-using-the-web-service-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API servizio di output](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

[Creazione di documenti PDF tramite frammenti](creating-document-output-streams.md#creating-pdf-documents-using-fragments)

### Trasmettere i documenti al servizio di output utilizzando l’API Java {#pass-documents-to-the-output-service-using-the-java-api}

Passa un documento recuperato da Content Services (obsoleto) utilizzando il servizio di output e l’API Content Services (obsoleto) (Java):

1. Includi file di progetto.

   Includi i file JAR client, come adobe-output-client.jar e adobe-contentservices-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto Output e un oggetto API Client di Document Management.

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione. (Vedere [Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * Creare un oggetto `OutputClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.
   * Creare un oggetto `DocumentManagementServiceClientImpl` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Recupera la progettazione del modulo da Content Services (obsoleto).

   Richiama il metodo `retrieveContent` dell&#39;oggetto `DocumentManagementServiceClientImpl` e passa i seguenti valori:

   * Valore stringa che specifica l&#39;archivio in cui viene aggiunto il contenuto. L&#39;archivio predefinito è `SpacesStore`. Questo valore è un parametro obbligatorio.
   * Valore stringa che specifica il percorso completo del contenuto da recuperare, ad esempio `/Company Home/Form Designs/Loan.xdp`. Questo valore è un parametro obbligatorio.
   * Valore stringa che specifica la versione. Questo valore è un parametro facoltativo e puoi trasmettere una stringa vuota. In questa situazione, viene recuperata la versione più recente.

   Il metodo `retrieveContent` restituisce un oggetto `CRCResult` che contiene il file XDP. Recuperare un&#39;istanza `com.adobe.idp.Document` richiamando il metodo `getDocument` dell&#39;oggetto `CRCResult`.

1. Esegui il rendering del modulo di PDF non interattivo.

   Richiama il metodo `generatePDFOutput2` dell&#39;oggetto `OutputClient` e passa i seguenti valori:

   * Valore di enumerazione `TransformationFormat`. Per generare un documento PDF, specificare `TransformationFormat.PDF`.
   * Valore stringa che specifica la directory principale del contenuto in cui si trovano le risorse aggiuntive, ad esempio le immagini.
   * Oggetto `com.adobe.idp.Document` che rappresenta la struttura del modulo (utilizzare l&#39;istanza restituita dal metodo `getDocument` dell&#39;oggetto `CRCResult`).
   * Oggetto `PDFOutputOptionsSpec` contenente le opzioni di runtime di PDF.
   * Oggetto `RenderOptionsSpec` contenente le opzioni di rendering in fase di esecuzione.
   * Oggetto `com.adobe.idp.Document` contenente l&#39;origine dati XML contenente i dati da unire con la struttura del modulo.

   Il metodo `generatePDFOutput2` restituisce un oggetto `OutputResult` contenente i risultati dell&#39;operazione.

1. Eseguire un&#39;azione con il flusso di dati del modulo.

   * Recuperare un oggetto `com.adobe.idp.Document` che rappresenta il modulo non interattivo richiamando il metodo `getGeneratedDoc` dell&#39;oggetto `OutputResult`.
   * Creare un oggetto `java.io.File` contenente i risultati dell&#39;operazione. Assicurati che l’estensione del nome file sia .pdf.
   * Richiamare il metodo `copyToFile` dell&#39;oggetto `com.adobe.idp.Document` per copiare il contenuto dell&#39;oggetto `com.adobe.idp.Document` nel file (assicurarsi di utilizzare l&#39;oggetto `com.adobe.idp.Document` restituito dal metodo `getGeneratedDoc`).

**Consulta anche**

[Riepilogo dei passaggi](creating-document-output-streams.md#summary-of-steps)

[Quick Start (modalità EJB): trasmissione dei documenti al servizio di output tramite l’API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-documents-to-the-output-service-using-the-java-api)

[Quick Start (modalità SOAP): trasmissione dei documenti al servizio di output tramite l’API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-documents-to-the-output-service-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Trasmettere i documenti al servizio di output utilizzando l’API del servizio web {#pass-documents-to-the-output-service-using-the-web-service-api}

Passa un documento recuperato da Content Services (obsoleto) utilizzando il servizio di output e l’API Content Services (obsoleto) (servizio web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Poiché questa applicazione client richiama due servizi AEM Forms, creare due riferimenti al servizio. Utilizzare la seguente definizione WSDL per il riferimento al servizio associato al servizio di output: `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   Utilizzare la seguente definizione WSDL per il riferimento al servizio associato al servizio Document Management: `http://localhost:8080/soap/services/DocumentManagementService?WSDL&lc_version=9.0.1`.

   Poiché il tipo di dati `BLOB` è comune a entrambi i riferimenti al servizio, il tipo di dati `BLOB` viene completamente qualificato quando viene utilizzato. Nel servizio Web corrispondente, avvio rapido, tutte le `BLOB` istanze sono completamente qualificate.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Creare un oggetto Output e un oggetto API Client di Document Management.

   * Creare un oggetto `OutputServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `OutputServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passare un valore stringa che specifica il file WSDL al servizio Forms (ad esempio, `http://localhost:8080/soap/services/OutputService?blob=mtom`). Non è necessario utilizzare l&#39;attributo `lc_version`. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `OutputServiceClient.Endpoint.Binding`. Eseguire il cast del valore restituito in `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegnare il nome utente dei moduli AEM al campo `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `OutputServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

   >[!NOTE]
   >
   >Ripetere questi passaggi per il client del servizio `DocumentManagementServiceClient`.

1. Recupera la progettazione del modulo da Content Services (obsoleto).

   Recuperare il contenuto richiamando il metodo `retrieveContent` dell&#39;oggetto `DocumentManagementServiceClient` e passando i valori seguenti:

   * Valore stringa che specifica l&#39;archivio in cui viene aggiunto il contenuto. L&#39;archivio predefinito è `SpacesStore`. Questo valore è un parametro obbligatorio.
   * Valore stringa che specifica il percorso completo del contenuto da recuperare, ad esempio `/Company Home/Form Designs/Loan.xdp`. Questo valore è un parametro obbligatorio.
   * Valore stringa che specifica la versione. Questo valore è un parametro facoltativo e puoi trasmettere una stringa vuota. In questa situazione, viene recuperata la versione più recente.
   * Parametro di output stringa che memorizza il valore del collegamento Sfoglia.
   * Un parametro di output `BLOB` che memorizza il contenuto. Puoi utilizzare questo parametro di output per recuperare il contenuto.
   * Un parametro di output `ServiceReference1.MyMapOf_xsd_string_To_xsd_anyType` che memorizza gli attributi del contenuto.
   * Un parametro di output `CRCResult`. Anziché utilizzare questo oggetto, è possibile utilizzare il parametro di output `BLOB` per recuperare il contenuto.

1. Esegui il rendering del modulo di PDF non interattivo.

   Richiama il metodo `generatePDFOutput2` dell&#39;oggetto `OutputServiceClient` e passa i seguenti valori:

   * Valore di enumerazione `TransformationFormat`. Per generare un documento PDF, specificare `TransformationFormat.PDF`.
   * Valore stringa che specifica la directory principale del contenuto in cui si trovano le risorse aggiuntive, ad esempio le immagini.
   * Oggetto `BLOB` che rappresenta la struttura del modulo (utilizzare l&#39;istanza `BLOB` restituita da Content Services (obsoleta)).
   * Oggetto `PDFOutputOptionsSpec` contenente le opzioni di runtime di PDF.
   * Oggetto `RenderOptionsSpec` contenente le opzioni di rendering in fase di esecuzione.
   * Oggetto `BLOB` contenente l&#39;origine dati XML contenente i dati da unire con la struttura del modulo.
   * Oggetto `BLOB` di output popolato dal metodo `generatePDFOutput2`. Il metodo `generatePDFOutput2` popola questo oggetto con i metadati generati che descrivono il documento. (Questo valore di parametro è richiesto solo per la chiamata del servizio Web).
   * Oggetto `OutputResult` di output contenente i risultati dell&#39;operazione. (Questo valore di parametro è richiesto solo per la chiamata del servizio Web).

   Il metodo `generatePDFOutput2` restituisce un oggetto `BLOB` che contiene il modulo non interattivo di PDF.

1. Eseguire un&#39;azione con il flusso di dati del modulo.

   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore. Passa un valore stringa che rappresenta la posizione del file del documento interattivo di PDF e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `BLOB` recuperato dal metodo `generatePDFOutput2`. Popolare la matrice di byte ottenendo il valore del membro dati `MTOM` dell&#39;oggetto `BLOB`.
   * Creare un oggetto `System.IO.BinaryWriter` richiamandone il costruttore e passando l&#39;oggetto `System.IO.FileStream`.
   * Scrivere il contenuto della matrice di byte in un file PDF richiamando il metodo `Write` dell&#39;oggetto `System.IO.BinaryWriter` e passando la matrice di byte.

**Consulta anche**

[Riepilogo dei passaggi](creating-document-output-streams.md#summary-of-steps)

[Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## Passaggio dei documenti nel repository al servizio di output {#passing-documents-located-in-the-repository-to-the-output-service}

Il servizio di output esegue il rendering di un modulo di PDF non interattivo basato su una struttura di modulo in genere salvata come file XDP e creata in Designer. È possibile passare un oggetto `com.adobe.idp.Document` contenente la struttura del modulo al servizio di output. Il servizio di output esegue quindi il rendering della struttura del modulo nell&#39;oggetto `com.adobe.idp.Document`.

Un vantaggio del passaggio di un oggetto `com.adobe.idp.Document` al servizio di output è che altre operazioni del servizio AEM Forms restituiscono un&#39;istanza `com.adobe.idp.Document`. In altre parole, è possibile ottenere un&#39;istanza `com.adobe.idp.Document` da un&#39;altra operazione di servizio ed eseguirne il rendering. Ad esempio, si supponga che un file XDP sia memorizzato nell’archivio AEM Forms, come illustrato nella figura seguente.

![pd_pd_formrepository](assets/pd_pd_formrepository.png)

La cartella *FormsFolder* è una posizione definita dall&#39;utente nel repository di AEM Forms (questa posizione è un esempio e non esiste per impostazione predefinita). In questo esempio, la struttura di un modulo denominata Loan.xdp si trova in questa cartella. Oltre alla progettazione del modulo, in questa posizione è possibile memorizzare anche altri materiali collaterali, ad esempio immagini. Il percorso di una risorsa nell’archivio AEM Forms è:

`Applications/Application-name/Application-version/Folder.../Filename`

È possibile recuperare in modo programmatico Loan.xdp dal repository di AEM Forms e passarlo al servizio di output all&#39;interno di un oggetto `com.adobe.idp.Document`.

Puoi creare un PDF basato su un file XDP nell’archivio utilizzando uno dei due modi seguenti. Puoi passare la posizione XDP per riferimento oppure recuperare in modo programmatico l’XDP dall’archivio e passarlo al servizio di output all’interno di un file XDP.

[Guida rapida (modalità EJB): creazione di un documento PDF basato su un file XDP dell&#39;applicazione mediante l&#39;API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-an-application-xdp-file-using-the-java-api) (mostra come passare il percorso del file XDP per riferimento).

[Avvio rapido (modalità EJB): passaggio di un documento nel repository di AEM Forms al servizio di output tramite l&#39;API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-a-document-located-in-the-repository-to-the-output-service-using-the-java-api) (mostra come recuperare in modo programmatico il file XDP dal repository di AEM Forms e passarlo al servizio di output all&#39;interno di un&#39;istanza `com.adobe.idp.Document`). (Questa sezione illustra come eseguire questa attività)

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Forms, vedere [Riferimento ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-3}

Per passare un documento ottenuto dal repository di AEM Forms al servizio di output, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Creare un oggetto Output e un oggetto API Client di Document Management.
1. Recupera la progettazione del modulo dall’archivio AEM Forms.
1. Esegui il rendering del modulo di PDF non interattivo.
1. Eseguire un&#39;azione con il flusso di dati.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se si utilizzano servizi Web, includere i file proxy.

**Creare un output e un oggetto API client di gestione documenti**

Prima di poter eseguire un&#39;operazione API del servizio di output a livello di programmazione, creare un oggetto API del client di output. Inoltre, poiché questo flusso di lavoro recupera un file XDP da Content Services (obsoleto), crea un oggetto API di gestione dei documenti.

**Recupera la struttura del modulo dal repository di AEM Forms**

Recupera il file XDP dall’archivio di AEM Forms utilizzando l’API dell’archivio. (Vedi [Lettura delle risorse](/help/forms/developing/aem-forms-repository.md#reading-resources).)

Il file XDP viene restituito all&#39;interno di un&#39;istanza `com.adobe.idp.Document` (o di un&#39;istanza `BLOB` se si utilizzano i servizi Web). È quindi possibile passare l&#39;istanza `com.adobe.idp.Document` al servizio di output.

**Eseguire il rendering del modulo di PDF non interattivo**

Per eseguire il rendering di un modulo non interattivo, passare l&#39;istanza `com.adobe.idp.Document` restituita utilizzando l&#39;API dell&#39;archivio di AEM Forms.

>[!NOTE]
>
>Due nuovi metodi denominati `generatePDFOutput2` e `generatePrintedOutput2`accettano un oggetto `com.adobe.idp.Document`che contiene una struttura di modulo. È inoltre possibile passare un `com.adobe.idp.Document` che contiene la struttura del modulo al servizio di output quando si invia un flusso di stampa a una stampante di rete.

**Esegui un&#39;azione con il flusso di dati del modulo**

È possibile salvare il modulo non interattivo come file PDF. Il modulo può essere visualizzato in Adobe Reader o Acrobat.

**Consulta anche**

[Trasmettere i documenti nel repository al servizio di output utilizzando l’API Java](creating-document-output-streams.md#pass-documents-located-in-the-repository-to-the-output-service-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API servizio di output](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

ResourceRepositoryClient

### Trasmettere i documenti nel repository al servizio di output utilizzando l’API Java {#pass-documents-located-in-the-repository-to-the-output-service-using-the-java-api}

Passa un documento recuperato dal repository utilizzando il servizio di output e l’API del repository (Java):

1. Includi file di progetto.

   Includi i file JAR client, come adobe-output-client.jar e adobe-repository-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto Output e un oggetto API Client di Document Management.

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione. (Vedere [Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * Creare un oggetto `OutputClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.
   * Creare un oggetto `DocumentManagementServiceClientImpl` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Recupera la progettazione del modulo dall’archivio di AEM Forms.

   Richiama il metodo `readResourceContent` dell&#39;oggetto `ResourceRepositoryClient` e passa un valore stringa che specifica il percorso URI al file XDP. Ad esempio, `/Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`. Questo valore è obbligatorio. Questo metodo restituisce un&#39;istanza `com.adobe.idp.Document` che rappresenta il file XDP.

1. Esegui il rendering del modulo di PDF non interattivo.

   Richiama il metodo `generatePDFOutput2` dell&#39;oggetto `OutputClient` e passa i seguenti valori:

   * Valore di enumerazione `TransformationFormat`. Per generare un documento PDF, specificare `TransformationFormat.PDF`.
   * Valore stringa che specifica la directory principale del contenuto in cui si trovano le risorse aggiuntive, ad esempio le immagini. Esempio: `repository:///Applications/FormsApplication/1.0/FormsFolder/`.
   * Oggetto `com.adobe.idp.Document` che rappresenta la struttura del modulo (utilizzare l&#39;istanza restituita dal metodo `readResourceContent` dell&#39;oggetto `ResourceRepositoryClient`).
   * Oggetto `PDFOutputOptionsSpec` contenente le opzioni di runtime di PDF.
   * Oggetto `RenderOptionsSpec` contenente le opzioni di rendering in fase di esecuzione.
   * Oggetto `com.adobe.idp.Document` contenente l&#39;origine dati XML contenente i dati da unire con la struttura del modulo.

   Il metodo `generatePDFOutput2` restituisce un oggetto `OutputResult` contenente i risultati dell&#39;operazione.

1. Eseguire un&#39;azione con il flusso di dati del modulo.

   * Recuperare un oggetto `com.adobe.idp.Document` che rappresenta il modulo non interattivo richiamando il metodo `getGeneratedDoc` dell&#39;oggetto `OutputResult`.
   * Creare un oggetto `java.io.File` contenente i risultati dell&#39;operazione. Assicurati che l’estensione del nome file sia .pdf.
   * Richiamare il metodo `copyToFile` dell&#39;oggetto `com.adobe.idp.Document` per copiare il contenuto dell&#39;oggetto `com.adobe.idp.Document` nel file (assicurarsi di utilizzare l&#39;oggetto `com.adobe.idp.Document` restituito dal metodo `getGeneratedDoc`).

**Consulta anche**

[Riepilogo dei passaggi](creating-document-output-streams.md#summary-of-steps)

[Guida rapida (modalità EJB): passaggio di un documento nel repository di AEM Forms al servizio di output tramite l’API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-a-document-located-in-the-repository-to-the-output-service-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Creazione di documenti PDF tramite frammenti {#creating-pdf-documents-using-fragments}

È possibile utilizzare i servizi Output e Assembler per creare un flusso di output, ad esempio un documento PDF, basato su frammenti. Il servizio Assembler assembla un documento XDP basato su frammenti in più file XDP. Il documento XDP assemblato viene passato al servizio di output, che crea un documento PDF. Anche se questo flusso di lavoro mostra un documento PDF in fase di generazione, il servizio di output può generare altri tipi di output, ad esempio ZPL, per questo flusso di lavoro. Un documento PDF viene utilizzato solo a scopo di discussione.

La figura seguente mostra questo flusso di lavoro.

![cp_cp_outputassemblefragments](assets/cp_cp_outputassemblefragments.png)

Prima di leggere *Creazione di documenti PDF tramite frammenti*, è consigliabile acquisire familiarità con l&#39;utilizzo del servizio Assembler per assemblare più documenti XDP. (Vedi [Assemblaggio di più frammenti XDP](/help/forms/developing/assembling-pdf-documents.md#assembling-multiple-xdp-fragments).)

>[!NOTE]
>
>È inoltre possibile passare una struttura di modulo assemblata dal servizio Assembler al servizio Forms anziché al servizio Output. La differenza principale tra il servizio di output e il servizio di Forms consiste nel fatto che il servizio di Forms genera documenti PDF interattivi e il servizio di output genera documenti PDF non interattivi. Inoltre, il servizio Forms non può generare flussi di output basati su stampante come ZPL.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio di output, vedere [Riferimento ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-4}

Per creare un documento PDF basato su frammenti, effettuare le seguenti operazioni:

1. Includi file di progetto.
1. Creare un oggetto client di output e assemblatore.
1. Utilizzare il servizio Assembler per generare la progettazione del modulo.
1. Utilizza il servizio di output per generare il documento PDF.
1. Salvare il documento PDF come file PDF.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

**Creare un oggetto client di output e assemblatore**

Prima di poter eseguire un&#39;operazione API del servizio di output a livello di programmazione, creare un oggetto API del client di output. Inoltre, poiché questo flusso di lavoro richiama il servizio Assembler per creare la progettazione del modulo, creare un oggetto API del client Assembler.

**Utilizzare il servizio Assembler per generare la struttura del modulo**

Utilizzare il servizio Assembler per generare la struttura del modulo utilizzando frammenti. Il servizio Assembler restituisce un&#39;istanza `com.adobe.idp.Document` che contiene la struttura del modulo.

**Utilizzare il servizio di output per generare il documento PDF**

È possibile utilizzare il servizio di output per generare un documento PDF utilizzando la struttura del modulo creata dal servizio Assembler. Passa l&#39;istanza `com.adobe.idp.Document` restituita dal servizio Assembler al servizio di output.

**Salvare il documento PDF come file PDF**

Dopo che il servizio di output genera un documento PDF, è possibile salvarlo come file PDF.

**Consulta anche**

[Creare un documento PDF basato su frammenti utilizzando l’API Java](creating-document-output-streams.md#create-a-pdf-document-based-on-fragments-using-the-java-api)

[Creare un documento PDF basato su frammenti utilizzando l’API del servizio web](creating-document-output-streams.md#create-a-pdf-document-based-on-fragments-using-the-web-service-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API servizio di output](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

[Assemblaggio di più frammenti XDP](/help/forms/developing/assembling-pdf-documents.md#assembling-multiple-xdp-fragments)

[Creazione di documenti PDF](creating-document-output-streams.md#creating-pdf-documents)

### Creare un documento PDF basato su frammenti utilizzando l’API Java {#create-a-pdf-document-based-on-fragments-using-the-java-api}

Crea un documento PDF basato su frammenti utilizzando l’API del servizio di output e l’API del servizio Assembler (Java):

1. Includi file di progetto.

   Includi i file JAR client, come adobe-output-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto client di output e assemblatore.

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `OutputClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.
   * Creare un oggetto `AssemblerServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Utilizzare il servizio Assembler per generare la progettazione del modulo.

   Richiama il metodo `invokeDDX` dell&#39;oggetto `AssemblerServiceClient` e passa i seguenti valori richiesti:

   * Oggetto `com.adobe.idp.Document` che rappresenta il documento DDX da utilizzare.
   * Oggetto `java.util.Map` contenente i file XDP di input.
   * Oggetto `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` che specifica le opzioni di runtime, inclusi il tipo di carattere predefinito e il livello del registro dei processi.

   Il metodo `invokeDDX` restituisce un oggetto `com.adobe.livecycle.assembler.client.AssemblerResult` che contiene il documento XDP assemblato. Per recuperare il documento XDP assemblato, effettuare le seguenti operazioni:

   * Richiama il metodo `getDocuments` dell&#39;oggetto `AssemblerResult`. Questo metodo restituisce un oggetto `java.util.Map`.
   * Scorrere l&#39;oggetto `java.util.Map` fino a trovare l&#39;oggetto `com.adobe.idp.Document` risultante.
   * Richiama il metodo `copyToFile` dell&#39;oggetto `com.adobe.idp.Document` per estrarre il documento XDP assemblato.

1. Utilizza il servizio di output per generare il documento PDF.

   Richiama il metodo `generatePDFOutput2` dell&#39;oggetto `OutputClient` e passa i seguenti valori:

   * Valore di enumerazione `TransformationFormat`. Per generare un documento PDF, specificare `TransformationFormat.PDF`
   * Valore stringa che specifica la directory principale del contenuto in cui si trovano le risorse aggiuntive, ad esempio le immagini
   * Oggetto `com.adobe.idp.Document` che rappresenta la struttura del modulo (utilizzare l&#39;istanza restituita dal servizio Assembler)
   * Un oggetto `PDFOutputOptionsSpec` che contiene le opzioni di runtime di PDF
   * Oggetto `RenderOptionsSpec` contenente le opzioni di rendering in fase di esecuzione
   * Oggetto `com.adobe.idp.Document` contenente l&#39;origine dati XML contenente i dati da unire con la struttura del modulo

   Il metodo `generatePDFOutput2` restituisce un oggetto `OutputResult` contenente i risultati dell&#39;operazione

1. Salvare il documento PDF come file PDF.

   * Recuperare un oggetto `com.adobe.idp.Document` che rappresenta il documento PDF richiamando il metodo `getGeneratedDoc` dell&#39;oggetto `OutputResult`.
   * Creare un oggetto `java.io.File` contenente i risultati dell&#39;operazione. Assicurati che l’estensione del nome file sia .pdf.
   * Richiama il metodo `copyToFile` dell&#39;oggetto `com.adobe.idp.Document` per copiare il contenuto dell&#39;oggetto `com.adobe.idp.Document` nel file. Assicurarsi di utilizzare l&#39;oggetto `com.adobe.idp.Document` restituito dal metodo `getGeneratedDoc`.

**Consulta anche**

[Riepilogo dei passaggi](creating-document-output-streams.md#summary-of-steps)

[Guida rapida (modalità EJB): creazione di un documento PDF basato su frammenti tramite API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-fragments-using-the-java-api)

[Guida rapida (modalità SOAP): creazione di un documento PDF basato su frammenti tramite API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-fragments-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

### Creare un documento PDF basato su frammenti utilizzando l’API del servizio web {#create-a-pdf-document-based-on-fragments-using-the-web-service-api}

Crea un documento PDF basato su frammenti utilizzando l’API del servizio di output e l’API del servizio Assembler (servizio web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Utilizzare la seguente definizione WSDL per il riferimento al servizio associato al servizio di output:

   ```java
    http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1.
   ```

   Utilizzare la seguente definizione WSDL per il riferimento al servizio associato al servizio Assembler:

   ```java
    http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1.
   ```

   Poiché il tipo di dati `BLOB` è comune a entrambi i riferimenti al servizio, il tipo di dati `BLOB` viene completamente qualificato quando viene utilizzato. Nel servizio Web corrispondente, avvio rapido, tutte le `BLOB` istanze sono completamente qualificate.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Creare un oggetto client di output e assemblatore.

   * Creare un oggetto `OutputServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `OutputServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/OutputService?blob=mtom`). Non è necessario utilizzare l&#39;attributo `lc_version`. Questo attributo viene utilizzato quando si crea un riferimento a un servizio. Tuttavia, specificare `?blob=mtom` per utilizzare MTOM.
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `OutputServiceClient.Endpoint.Binding`. Eseguire il cast del valore restituito in `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegnare il nome utente dei moduli AEM al campo `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `OutputServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

   >[!NOTE]
   >
   >Ripetere questi passaggi per l&#39;oggetto `AssemblerServiceClient`.

1. Utilizzare il servizio Assembler per generare la progettazione del modulo.

   Richiama il metodo `invokeDDX` dell&#39;oggetto `AssemblerServiceClient` e passa i seguenti valori:

   * Oggetto `BLOB` che rappresenta il documento DDX
   * L&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType` che contiene i file richiesti
   * Oggetto `AssemblerOptionSpec` che specifica le opzioni di runtime

   Il metodo `invokeDDX` restituisce un oggetto `AssemblerResult` contenente i risultati del processo ed eventuali eccezioni. Per ottenere il documento XDP appena creato, effettuare le seguenti operazioni:

   * Accedere al campo `documents` dell&#39;oggetto `AssemblerResult`, che è un oggetto `Map` contenente i documenti PDF risultanti.
   * Scorrere l&#39;oggetto `Map` per recuperare la struttura del modulo assemblato. Eseguire il cast del membro dell&#39;array `value` in un `BLOB`. Passa questa istanza `BLOB` al servizio di output.

1. Utilizza il servizio di output per generare il documento PDF.

   Richiama il metodo `generatePDFOutput2` dell&#39;oggetto `OutputServiceClient` e passa i seguenti valori:

   * Valore di enumerazione `TransformationFormat`. Per generare un documento PDF, specificare `TransformationFormat.PDF`.
   * Valore stringa che specifica la directory principale del contenuto in cui si trovano le risorse aggiuntive, ad esempio le immagini.
   * Oggetto `BLOB` che rappresenta la struttura del modulo (utilizzare l&#39;istanza `BLOB` restituita dal servizio Assembler).
   * Oggetto `PDFOutputOptionsSpec` contenente le opzioni di runtime di PDF.
   * Oggetto `RenderOptionsSpec` contenente le opzioni di rendering in fase di esecuzione.
   * Oggetto `BLOB` contenente l&#39;origine dati XML contenente i dati da unire con la struttura del modulo.
   * Oggetto `BLOB` di output popolato dal metodo `generatePDFOutput2`. Il metodo `generatePDFOutput2` popola questo oggetto con i metadati generati che descrivono il documento. (Questo valore di parametro è richiesto solo per la chiamata del servizio Web).
   * Oggetto `OutputResult` di output contenente i risultati dell&#39;operazione. (Questo valore di parametro è richiesto solo per la chiamata del servizio Web).

   Il metodo `generatePDFOutput2` restituisce un oggetto `BLOB` che contiene il modulo non interattivo di PDF.

1. Salvare il documento PDF come file PDF.

   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore. Passa un valore stringa che rappresenta la posizione del file del documento interattivo di PDF e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `BLOB` recuperato dal metodo `generatePDFOutput2`. Popolare la matrice di byte ottenendo il valore del membro dati `MTOM` dell&#39;oggetto `BLOB`.
   * Creare un oggetto `System.IO.BinaryWriter` richiamandone il costruttore e passando l&#39;oggetto `System.IO.FileStream`.
   * Scrivere il contenuto della matrice di byte in un file PDF richiamando il metodo `Write` dell&#39;oggetto `System.IO.BinaryWriter` e passando la matrice di byte.

**Consulta anche**

[Riepilogo dei passaggi](creating-document-output-streams.md#summary-of-steps)

[Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## Stampa su file {#printing-to-files}

È possibile utilizzare il servizio Output per stampare flussi quali PostScript, Printer Control Language (PCL) o i seguenti formati di etichette in un file:

* Zebra - ZPL
* Intermec - IPL
* Datamax - DPL
* TecToshiba - TPCL

Tramite il servizio di output è possibile unire i dati XML con una struttura di modulo e stampare il modulo in un file. La figura seguente mostra il servizio di output che crea i file laser ed label.

>[!NOTE]
>
>Per informazioni sull&#39;invio di flussi di stampa alle stampanti, vedere [Invio di flussi di stampa alle stampanti](creating-document-output-streams.md#sending-print-streams-to-printers).

>[!NOTE]
>
>Per ulteriori informazioni sul servizio di output, vedere [Riferimento ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-5}

Per stampare su un file, effettuare le seguenti operazioni:

1. Includi file di progetto.
1. Creare un oggetto client di output.
1. Fare riferimento a un&#39;origine dati XML.
1. Impostare le opzioni di runtime di stampa necessarie per stampare su un file.
1. Stampa il flusso di stampa su un file.
1. Recuperate i risultati dell&#39;operazione.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso della classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è implementato su JBoss)
* jbossall-client.jar (obbligatorio se AEM Forms è distribuito su JBoss)

se AEM Forms viene distribuito su un server applicazioni J2EE supportato che non è JBoss, è necessario sostituire i file adobe-utilities.jar e jbossall-client.jar con file JAR specifici per il server applicazioni J2EE in cui viene distribuito AEM Forms. (Vedi [Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).)

**Crea un oggetto client di output**

Prima di poter eseguire un&#39;operazione del servizio di output a livello di programmazione, è necessario creare un oggetto client del servizio di output. Se si utilizza l&#39;API Java, creare un oggetto `OutputClient`. Se si utilizza l&#39;API del servizio Web di output, creare un oggetto `OutputServiceService`.

**Riferimento a un&#39;origine dati XML**

Per stampare un documento contenente dati, è necessario fare riferimento a un&#39;origine dati XML contenente elementi XML per ogni campo modulo che si desidera compilare con i dati. Il nome dell&#39;elemento XML deve corrispondere al nome del campo. Un elemento XML viene ignorato se non corrisponde a un campo modulo o se il nome dell&#39;elemento XML non corrisponde al nome del campo. Se vengono specificati tutti gli elementi XML, non è necessario che l&#39;ordine di visualizzazione degli elementi XML corrisponda a quello specificato.

**Impostare le opzioni di runtime di stampa necessarie per stampare su un file**

Per stampare su un file, è necessario impostare l&#39;opzione di runtime URI file specificando la posizione e il nome del file in cui viene stampato il servizio di output. Ad esempio, per indicare al servizio di output di stampare un file PostScript denominato *MortgageForm.ps* in C:\Adobe, specificare C:\Adobe\MortgageForm.ps.

>[!NOTE]
>
>È possibile definire opzioni di runtime facoltative. Per informazioni su tutte le opzioni che è possibile impostare, vedere il riferimento alla classe `PrintedOutputOptionsSpec` in [Riferimento API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Stampa il flusso di stampa in un file**

Dopo aver fatto riferimento a un&#39;origine dati XML valida che contiene dati del modulo e aver impostato le opzioni di esecuzione della stampa, è possibile richiamare il servizio di output, che consente di stampare un file.

**Recupera i risultati dell&#39;operazione**

Una volta eseguita un&#39;operazione, il servizio di output restituisce vari elementi di dati, ad esempio dati XML, che specificano se l&#39;operazione è stata eseguita correttamente.

**Consulta anche**

[Stampare su file utilizzando l’API Java](creating-document-output-streams.md#print-to-files-using-the-java-api)

[Stampare su file utilizzando l’API del servizio web](creating-document-output-streams.md#print-to-files-using-the-web-service-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API servizio di output](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Stampare su file utilizzando l’API Java {#print-to-files-using-the-java-api}

Stampare su file utilizzando l’API di output (Java):

1. Includi file di progetto.

   Includi i file JAR client, come adobe-output-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto client di output.

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `OutputClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Fare riferimento a un&#39;origine dati XML.

   * Creare un oggetto `java.io.FileInputStream` che rappresenta l&#39;origine dati XML utilizzata per popolare il documento utilizzando il relativo costruttore e passando un valore stringa che specifica la posizione del file XML.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Impostare le opzioni di runtime di stampa necessarie per stampare su un file.

   * Creare un oggetto `PrintedOutputOptionsSpec` utilizzando il relativo costruttore.
   * Specificare il file richiamando il metodo `setFileURI` dell&#39;oggetto PrintedOutputOptionsSpec e passando un valore stringa che rappresenta il nome e la posizione del file. Se ad esempio si desidera che il servizio di output venga stampato in un file PostScript denominato MortgageForm.ps in C:\Adobe, specificare C:\\Adobe\MortgageForm.ps.
   * Specificare il numero di copie da stampare richiamando il metodo `setCopies` dell&#39;oggetto `PrintedOutputOptionsSpec` e passando un valore intero che rappresenta il numero di copie.

1. Stampa il flusso di stampa su un file.

   Stampare in un file richiamando il metodo `generatePrintedOutput` dell&#39;oggetto `OutputClient` e passando i valori seguenti:

   * Valore di enumerazione `PrintFormat` che specifica il formato del flusso di stampa da creare. Ad esempio, per creare un flusso di stampa PostScript, passare `PrintFormat.PostScript`.
   * Valore stringa che specifica il nome della struttura del modulo.
   * Valore stringa che specifica la posizione dei file di materiale promozionale correlati, ad esempio i file immagine.
   * Valore stringa che specifica la posizione del file XDC da utilizzare (è possibile passare `null` se è stato specificato il file XDC da utilizzare utilizzando l&#39;oggetto `PrintedOutputOptionsSpec`).
   * L&#39;oggetto `PrintedOutputOptionsSpec` che contiene le opzioni di runtime necessarie per stampare su un file.
   * L&#39;oggetto `com.adobe.idp.Document` che contiene l&#39;origine dati XML che contiene i dati del modulo.

   Il metodo `generatePrintedOutput` restituisce un oggetto `OutputResult` contenente i risultati dell&#39;operazione.

   >[!NOTE]
   >
   >Il metodo `getRecordLevelMetaDataList` dell&#39;oggetto `OutputResult` restituisce `null`.

1. Recuperate i risultati dell&#39;operazione.

   * Creare un oggetto `com.adobe.idp.Document` che rappresenta lo stato del metodo `generatePrintedOutput` richiamando il metodo `getStatusDoc` dell&#39;oggetto `OutputResult` (l&#39;oggetto `OutputResult` è stato restituito dal metodo `generatePrintedOutput`).
   * Creare un oggetto `java.io.File` che conterrà i risultati dell&#39;operazione. Assicurati che l’estensione del file sia XML.
   * Richiamare il metodo `copyToFile` dell&#39;oggetto `com.adobe.idp.Document` per copiare il contenuto dell&#39;oggetto `com.adobe.idp.Document` nel file (assicurarsi di utilizzare l&#39;oggetto `com.adobe.idp.Document` restituito dal metodo `getStatusDoc`).

**Consulta anche**

[Riepilogo dei passaggi](creating-document-output-streams.md#summary-of-steps)

[Quick Start (modalità SOAP): stampa su file tramite API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-printing-to-a-file-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

### Stampare su file utilizzando l’API del servizio web {#print-to-files-using-the-web-service-api}

Stampa su file tramite API di output (servizio Web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Creare un oggetto client di output.

   * Creare un oggetto `OutputServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `OutputServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/OutputService?blob=mtom`). Non è necessario utilizzare l&#39;attributo `lc_version`. Questo attributo viene utilizzato quando si crea un riferimento a un servizio. Tuttavia, specificare `?blob=mtom` per utilizzare MTOM.
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `OutputServiceClient.Endpoint.Binding`. Eseguire il cast del valore restituito in `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegnare il nome utente dei moduli AEM al campo `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `OutputServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Fare riferimento a un&#39;origine dati XML.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare i dati del modulo.
   * Creare un oggetto `System.IO.FileStream` richiamandone il costruttore e passando un valore stringa che specifica la posizione del file XML contenente i dati del modulo.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni della matrice di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare la matrice di byte con i dati di flusso richiamando il metodo `Read` dell&#39;oggetto `System.IO.FileStream` e passando la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando la relativa proprietà `binaryData` al contenuto della matrice di byte.

1. Impostare le opzioni di runtime di stampa necessarie per stampare su un file.

   * Creare un oggetto `PrintedOutputOptionsSpec` utilizzando il relativo costruttore.
   * Specificare il file assegnando un valore stringa che rappresenta la posizione e il nome del file al membro dati `fileURI` dell&#39;oggetto `PrintedOutputOptionsSpec`. Se ad esempio si desidera che il servizio di output venga stampato in un file PostScript denominato *MortgageForm.ps* in C:\Adobe, specificare C:\\Adobe\MortgageForm.ps.
   * Specificare il numero di copie da stampare assegnando un valore intero che rappresenta il numero di copie ai membri dati `copies` dell&#39;oggetto `PrintedOutputOptionsSpec`.

1. Stampa il flusso di stampa su un file.

   Stampare in un file richiamando il metodo `generatePrintedOutput` dell&#39;oggetto `OutputServiceService` e passando i valori seguenti:

   * Valore di enumerazione `PrintFormat` che specifica il formato del flusso di stampa da creare. Ad esempio, per creare un flusso di stampa PostScript, passare `PrintFormat.PostScript`.
   * Valore stringa che specifica il nome della struttura del modulo.
   * Valore stringa che specifica la posizione dei file di materiale promozionale correlati, ad esempio i file immagine.
   * Valore stringa che specifica la posizione del file XDC da utilizzare (è possibile passare `null` se è stato specificato il file XDC da utilizzare utilizzando l&#39;oggetto `PrintedOutputOptionsSpec`).
   * Oggetto `PrintedOutputOptionsSpec` contenente le opzioni di runtime di stampa necessarie per stampare su un file.
   * Oggetto `BLOB` contenente l&#39;origine dati XML che contiene i dati del modulo.
   * Oggetto `BLOB` popolato dal metodo `generatePDFOutput`. Il metodo `generatePDFOutput` popola questo oggetto con i metadati generati che descrivono il documento. (Questo valore di parametro è obbligatorio solo per le chiamate al servizio web).
   * Oggetto `BLOB` popolato dal metodo `generatePDFOutput`. Il metodo `generatePDFOutput` popola questo oggetto con i dati dei risultati. (Questo valore di parametro è obbligatorio solo per le chiamate al servizio web).
   * Oggetto `OutputResult` contenente i risultati dell&#39;operazione. (Questo valore di parametro è obbligatorio solo per le chiamate al servizio web).

1. Recuperate i risultati dell&#39;operazione.

   * Creare un oggetto `System.IO.FileStream` richiamandone il costruttore e passando un valore stringa che rappresenta un percorso di file XML contenente i dati dei risultati. Assicurati che l’estensione del file sia XML.
   * Creare una matrice di byte che memorizza il contenuto dei dati dell&#39;oggetto `BLOB` che è stato popolato con i dati dei risultati dal metodo `generatePDFOutput` dell&#39;oggetto `OutputServiceService` (ottavo parametro). Popolare la matrice di byte ottenendo il valore del membro dati `MTOM` dell&#39;oggetto `BLOB`.
   * Creare un oggetto `System.IO.BinaryWriter` richiamandone il costruttore e passando l&#39;oggetto `System.IO.FileStream`.
   * Scrivere il contenuto della matrice di byte nel file XML richiamando il metodo `Write` dell&#39;oggetto `System.IO.BinaryWriter` e passando la matrice di byte.

**Consulta anche**

[Riepilogo dei passaggi](creating-document-output-streams.md#summary-of-steps)

[Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamare AEM Forms con SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Invio di flussi di stampa alle stampanti {#sending-print-streams-to-printers}

È possibile utilizzare il servizio Output per inviare flussi di stampa come PostScript, Printer Control Language (PCL) o i formati di etichette seguenti alle stampanti di rete:

* Zebra - ZPL
* Intermec - IPL
* Datamax - DPL
* TecToshiba - TPCL

Il servizio Output consente di unire i dati XML con la struttura di un modulo e di generare il modulo come flusso di stampa. È ad esempio possibile creare un flusso di stampa PostScript e inviarlo a una stampante di rete. Nella figura seguente viene illustrato il servizio di output che invia flussi di stampa alle stampanti di rete.

>[!NOTE]
>
>Per illustrare come inviare un flusso di stampa a una stampante di rete, in questa sezione viene inviato un flusso di stampa PostScript a una stampante di rete utilizzando il protocollo della stampante SharedPrinter.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio di output, vedere [Riferimento ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-6}

Per inviare un flusso di stampa a una stampante di rete, effettuare le seguenti operazioni:

1. Includi file di progetto.
1. Creare un oggetto client di output.
1. Fare riferimento a un&#39;origine dati XML.
1. Impostare le opzioni di runtime di stampa
1. Recuperare un documento da stampare.
1. Invia il documento a una stampante di rete.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso della classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è implementato su JBoss)
* jbossall-client.jar (obbligatorio se AEM Forms è distribuito su JBoss)

se AEM Forms viene distribuito su un server applicazioni J2EE supportato che non è JBoss, è necessario sostituire i file adobe-utilities.jar e jbossall-client.jar con file JAR specifici per il server applicazioni J2EE in cui viene distribuito AEM Forms.

**Crea un oggetto client di output**

Prima di poter eseguire un&#39;operazione del servizio di output a livello di programmazione, creare un oggetto client del servizio di output. Se si utilizza l&#39;API Java, creare un oggetto `OutputClient`. Se si utilizza l&#39;API del servizio Web di output, creare un oggetto `OutputServiceClient`.

**Riferimento a un&#39;origine dati XML**

Per stampare un documento contenente dati, è necessario fare riferimento a un&#39;origine dati XML contenente elementi XML per ogni campo modulo che si desidera compilare con i dati. Il nome dell&#39;elemento XML deve corrispondere al nome del campo. Un elemento XML viene ignorato se non corrisponde a un campo modulo o se il nome dell&#39;elemento XML non corrisponde al nome del campo. Se vengono specificati tutti gli elementi XML, non è necessario che l&#39;ordine di visualizzazione degli elementi XML corrisponda a quello specificato.

**Impostare le opzioni di runtime di stampa**

È possibile impostare le opzioni di runtime durante l&#39;invio di un flusso di stampa a una stampante, incluse le seguenti opzioni:

* **Copie**: specifica il numero di copie da inviare alla stampante. Il valore predefinito è 1.
* **Graffetta**: quando si utilizza una cucitrice, viene impostata un&#39;opzione XCI. Questa opzione può essere specificata nel modello di configurazione dall&#39;elemento graffetta e viene utilizzata solo per le stampanti PS e PCL.
* **OutputJog**: viene impostata un&#39;opzione XCI quando le pagine di output devono essere spostate (fisicamente spostate nell&#39;area di output). Questa opzione è valida solo per le stampanti PS e PCL.
* **OutputBin**: valore XCI utilizzato per consentire al driver di stampa di selezionare il raccoglitore di output appropriato.

>[!NOTE]
>
>Per informazioni su tutte le opzioni di runtime che è possibile impostare, vedere il riferimento alla classe `PrintedOutputOptionsSpec`.

**Recuperare un documento da stampare**

Recuperare un flusso di stampa da inviare a una stampante. È ad esempio possibile recuperare un file PostScript e inviarlo a una stampante.

È possibile scegliere di inviare un file PDF se la stampante in uso supporta PDF. Tuttavia, un problema con l&#39;invio di un documento PDF a una stampante è che ogni produttore di stampanti ha un&#39;implementazione diversa dell&#39;interprete PDF. In altre parole, alcuni produttori di stampe utilizzano l&#39;interpretazione Adobe PDF, ma questo dipende dalla stampante. Altre stampanti hanno il proprio interprete PDF. Di conseguenza, i risultati di stampa possono variare.

Un altro limite dell&#39;invio di un documento PDF a una stampante è rappresentato dal fatto che non è possibile accedere al duplex, alla selezione del cassetto della carta e alla graffatura, se non tramite le impostazioni della stampante.

Per recuperare un documento da stampare, utilizzare il metodo `generatePrintedOutput`. Nella tabella seguente vengono specificati i tipi di contenuto impostati per un determinato flusso di stampa quando si utilizza il metodo `generatePrintedOutput`.

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
   <td><p>Crea un flusso di output PCL colore generico (5c).</p></td>
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
   <td><p>Crea un flusso di output Generic PostScript Level 2.</p></td>
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
>È inoltre possibile inviare un flusso di stampa a una stampante utilizzando il metodo `generatePrintedOutput2`. Tuttavia, gli avvii rapidi associati alla sezione Invio di flussi di stampa alle stampanti utilizzano il metodo `generatePrintedOutput`.

**Inviare il flusso di stampa a una stampante di rete**

Dopo aver recuperato un documento da stampare, è possibile richiamare il servizio Output, che invia un flusso di stampa a una stampante di rete. Affinché il servizio di output possa individuare correttamente la stampante, è necessario specificare sia il server di stampa che il nome della stampante. È inoltre necessario specificare il protocollo di stampa.

>[!NOTE]
>
>Se PDFG è installato sul server Forms e il server viene eseguito su Windows Server 2008, non è possibile utilizzare la proprietà SharedPrinter. In questo caso, utilizzare un protocollo diverso per la stampante.

>[!NOTE]
>
>Se si utilizza una stampante di rete e il meccanismo di accesso è SharedPrinter, è necessario specificare il percorso di rete completo della stampante.Inviare un flusso di stampa a una stampante di rete utilizzando l&#39;API Java

Inviare un flusso di stampa a una stampante di rete utilizzando l&#39;API di output (Java):

1. Includi file di progetto.

   Includi i file JAR client, come adobe-output-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto client di output

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `OutputClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Riferimento a un&#39;origine dati XML

   * Creare un oggetto `java.io.FileInputStream` che rappresenta l&#39;origine dati XML utilizzata per popolare il documento utilizzando il relativo costruttore e passando un valore stringa che specifica la posizione del file XML.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Impostare le opzioni di runtime di stampa

   Creare un oggetto `PrintedOutputOptionsSpec` che rappresenta le opzioni di runtime di stampa. È ad esempio possibile specificare il numero di copie da stampare richiamando il metodo `setCopies` dell&#39;oggetto `PrintedOutputOptionsSpec`.

   >[!NOTE]
   >
   >Impossibile impostare il valore di impaginazione utilizzando il metodo `setPagination` dell&#39;oggetto `PrintedOutputOptionsSpec` se si genera un flusso di stampa ZPL. Allo stesso modo, non potete impostare le seguenti opzioni per un flusso di stampa ZPL: OutputJog, PageOffset e Graffetta. Il metodo `setPagination` non è valido per la generazione di PostScript. È valida solo per la generazione PCL.

1. Recuperare un documento da stampare

   * Recuperare un documento da stampare richiamando il metodo `generatePrintedOutput` dell&#39;oggetto `OutputClient` e passando i valori seguenti:

      * Valore di enumerazione `PrintFormat` che specifica il flusso di stampa. Ad esempio, per creare un flusso di stampa PostScript, passare `PrintFormat.PostScript`.
      * Valore stringa che specifica il nome della struttura del modulo.
      * Valore stringa che specifica la posizione dei file di materiale promozionale correlati, ad esempio i file immagine.
      * Valore stringa che specifica la posizione del file XDC da utilizzare.
      * L&#39;oggetto `PrintedOutputOptionsSpec` che contiene le opzioni di runtime necessarie per stampare su un file.
      * Oggetto `com.adobe.idp.Document` che rappresenta l&#39;origine dati XML contenente i dati del modulo da unire con la struttura del modulo.

     Questo metodo restituisce un oggetto `OutputResult` contenente i risultati dell&#39;operazione.

   * Creare un oggetto `com.adobe.idp.Document` da inviare alla stampante richiamando il metodo `getGeneratedDoc` dell&#39;oggetto `OutputResult`. Questo metodo restituisce un oggetto `com.adobe.idp.Document`.

1. Inviare il flusso di stampa a una stampante di rete

   Inviare il flusso di stampa a una stampante di rete richiamando il metodo `sendToPrinter` dell&#39;oggetto `OutputClient` e passando i valori seguenti:

   * Oggetto `com.adobe.idp.Document` che rappresenta il flusso di stampa da inviare alla stampante.
   * Valore di enumerazione `PrinterProtocol` che specifica il protocollo della stampante da utilizzare. Ad esempio, per specificare il protocollo SharedPrinter, passare `PrinterProtocol.SharedPrinter`.
   * Valore stringa che specifica il nome del server di stampa. Ad esempio, supponendo che il nome del server di stampa sia PrintSever1, passare `\\\PrintSever1`.
   * Valore stringa che specifica il nome della stampante. Ad esempio, supponendo che il nome della stampante sia Printer1, passare `\\\PrintSever1\Printer1`.

   >[!NOTE]
   >
   >Il metodo `sendToPrinter` è stato aggiunto all&#39;API AEM Forms nella versione 8.2.1.

### Inviare un flusso di stampa a una stampante utilizzando l&#39;API del servizio Web {#send-a-print-stream-to-a-printer-using-the-web-service-api}

Inviare un flusso di stampa a una stampante di rete utilizzando l&#39;API di output (servizio Web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Creare un oggetto client di output.

   * Creare un oggetto `OutputServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `OutputServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/OutputService?blob=mtom`). Non è necessario utilizzare l&#39;attributo `lc_version`. Questo attributo viene utilizzato quando si crea un riferimento a un servizio. Tuttavia, specificare `?blob=mtom` per utilizzare MTOM.
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `OutputServiceClient.Endpoint.Binding`. Eseguire il cast del valore restituito in `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegnare il nome utente dei moduli AEM al campo `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `OutputServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Fare riferimento a un&#39;origine dati XML.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare i dati del modulo.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore. Passa un valore stringa che specifica la posizione del file XML contenente i dati del modulo.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. Determinare la lunghezza della matrice di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare la matrice di byte con i dati di flusso richiamando il metodo `Read` dell&#39;oggetto `System.IO.FileStream` e passando la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando il relativo campo `MTOM` al contenuto della matrice di byte.

1. Impostare le opzioni di runtime di stampa.

   Creare un oggetto `PrintedOutputOptionsSpec` utilizzando il relativo costruttore. È ad esempio possibile specificare il numero di copie da stampare assegnando un valore intero che rappresenta il numero di copie al membro dati `copies` dell&#39;oggetto `PrintedOutputOptionsSpec`.

   >[!NOTE]
   >
   >Impossibile impostare il valore di impaginazione utilizzando il membro dati `pagination` dell&#39;oggetto `PrintedOutputOptionsSpec` se si genera un flusso di stampa ZPL. Allo stesso modo, non potete impostare le seguenti opzioni per un flusso di stampa ZPL: OutputJog, PageOffset e Graffetta. Il membro dati `pagination` non è valido per la generazione di PostScript. È valida solo per la generazione PCL.

1. Recuperare un documento da stampare.

   * Recuperare un documento da stampare richiamando il metodo `generatePrintedOutput` dell&#39;oggetto `OutputServiceService` e passando i valori seguenti:

      * Valore di enumerazione `PrintFormat` che specifica il flusso di stampa. Ad esempio, per creare un flusso di stampa PostScript, passare `PrintFormat.PostScript`.
      * Valore stringa che specifica il nome della struttura del modulo.
      * Valore stringa che specifica la posizione dei file di materiale promozionale correlati, ad esempio i file immagine.
      * Valore stringa che specifica la posizione del file XDC da utilizzare.
      * Oggetto `PrintedOutputOptionsSpec` contenente le opzioni di runtime di stampa utilizzate per inviare un flusso di stampa a una stampante di rete.
      * Oggetto `BLOB` contenente l&#39;origine dati XML che contiene i dati del modulo.
      * Oggetto `BLOB` popolato dal metodo `generatePrintedOutput`. Il metodo `generatePrintedOutput` popola questo oggetto con i metadati generati che descrivono il documento. (Questo valore di parametro è obbligatorio solo per le chiamate al servizio web).
      * Oggetto `BLOB` popolato dal metodo `generatePrintedOutput`. Il metodo `generatePrintedOutput` popola questo oggetto con i dati dei risultati. (Questo valore di parametro è obbligatorio solo per le chiamate al servizio web).
      * Oggetto `OutputResult` contenente i risultati dell&#39;operazione. (Questo valore di parametro è obbligatorio solo per le chiamate al servizio web).

   * Creare un oggetto `BLOB` da inviare alla stampante ottenendo il valore del metodo `generatedDoc` dell&#39;oggetto `OutputResult`. Questo metodo restituisce un oggetto `BLOB` che contiene i dati PostScript restituiti dal metodo `generatePrintedOutput`.

1. Invia il flusso di stampa a una stampante di rete.

   Inviare il flusso di stampa a una stampante di rete richiamando il metodo `sendToPrinter` dell&#39;oggetto `OutputClient` e passando i valori seguenti:

   * Oggetto `BLOB` che rappresenta il flusso di stampa da inviare alla stampante.
   * Valore di enumerazione `PrinterProtocol` che specifica il protocollo della stampante da utilizzare. Ad esempio, per specificare il protocollo SharedPrinter, passare `PrinterProtocol.SharedPrinter`.
   * Valore `bool` che specifica se utilizzare il valore del parametro precedente. Passa il valore `true`. (Questo valore di parametro è obbligatorio solo per le chiamate al servizio web).
   * Valore stringa che specifica il nome del server di stampa. Ad esempio, supponendo che il nome del server di stampa sia PrintSever1, passare `\\\PrintSever1`.
   * Valore stringa che specifica il nome della stampante. Ad esempio, supponendo che il nome della stampante sia Printer1, passare `\\\PrintSever1\Printer1`.

   >[!NOTE]
   >
   >Il metodo `sendToPrinter` è stato aggiunto all&#39;API AEM Forms nella versione 8.2.1.

## Creazione di più file di output {#creating-multiple-output-files}

Il servizio di output può creare documenti separati per ogni record all&#39;interno di un&#39;origine dati XML o un singolo file contenente tutti i record (questa funzionalità è quella predefinita). Si supponga, ad esempio, che dieci record si trovino all&#39;interno di un&#39;origine dati XML e che il servizio di output debba creare documenti PDF separati (o altri tipi di output) per ogni record utilizzando l&#39;API Servizio di output. Di conseguenza, il servizio di output genera dieci documenti PDF. Anziché creare documenti, è possibile inviare più flussi di stampa a una stampante.

Nella figura seguente viene inoltre illustrato il servizio di output che elabora un file di dati XML contenente più record. Si supponga tuttavia di indicare al servizio di output di creare un singolo documento PDF contenente tutti i record di dati. In questa situazione, il servizio di output genera un documento contenente tutti i record.

Nella figura seguente viene illustrato il servizio di output che elabora un file di dati XML contenente più record. Si supponga di aver richiesto al servizio di output di creare un documento PDF separato per ogni record di dati. In questa situazione, il servizio di output genera un documento PDF separato per ogni record di dati.

![cm_outputbatchmany](assets/cm_outputbatchmany.png)

Nei dati XML seguenti viene illustrato un esempio di un file di dati contenente tre record di dati.

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

L&#39;elemento XML che inizia e termina ogni record di dati è `LoanRecord`. A questo elemento XML fa riferimento la logica dell&#39;applicazione che genera più file.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio di output, vedere [Riferimento ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-7}

Per creare più file PDF basati su un&#39;origine dati XML, effettuare le seguenti operazioni:

1. Includi file di progetto.
1. Creare un oggetto client di output.
1. Fare riferimento a un&#39;origine dati XML.
1. Impostare le opzioni di runtime di PDF.
1. Impostate le opzioni di runtime per il rendering.
1. Genera più file PDF.
1. Recuperate i risultati dell&#39;operazione.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso della classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è implementato su JBoss)
* jbossall-client.jar (obbligatorio se AEM Forms è distribuito su JBoss)

se AEM Forms viene distribuito su un server applicazioni J2EE supportato che non è JBoss, è necessario sostituire i file adobe-utilities.jar e jbossall-client.jar con file JAR specifici per il server applicazioni J2EE in cui viene distribuito AEM Forms.

**Crea un oggetto client di output**

Prima di poter eseguire un&#39;operazione del servizio di output a livello di programmazione, è necessario creare un oggetto client del servizio di output. Se si utilizza l&#39;API Java, creare un oggetto `OutputClient`. Se si utilizza l&#39;API del servizio Web di output, creare un oggetto `OutputServiceService`.

**Riferimento a un&#39;origine dati XML**

Fare riferimento a un&#39;origine dati XML che contiene più record. Per separare i record di dati è necessario utilizzare un elemento XML. Nell&#39;origine dati XML di esempio mostrata in precedenza in questa sezione, ad esempio, l&#39;elemento XML che separa i record di dati è denominato `LoanRecord`.

Un elemento XML deve esistere per ogni campo modulo che si desidera compilare con i dati. Il nome dell&#39;elemento XML deve corrispondere al nome del campo. Un elemento XML viene ignorato se non corrisponde a un campo modulo o se il nome dell&#39;elemento XML non corrisponde al nome del campo. Se vengono specificati tutti gli elementi XML, non è necessario che l&#39;ordine di visualizzazione degli elementi XML corrisponda a quello specificato.

**Imposta opzioni runtime di PDF**

Impostare le seguenti opzioni di runtime affinché il servizio di output possa creare più file in base a un&#39;origine dati XML:

* **Molti file**: specifica se il servizio di output crea uno o più documenti. È possibile specificare true o false. Per creare un documento separato per ogni record di dati nell&#39;origine dati XML, specificare true.
* **URI file**: specifica il percorso dei file generati dal servizio di output. Ad esempio, si supponga di specificare C:\\Adobe\forms\Loan.pdf. In questa situazione, il servizio di output crea un file denominato Loan.pdf e lo inserisce nella cartella C:\\Adobe\forms. In presenza di più file, i nomi dei file sono Loan0001.pdf, Loan0002.pdf, Loan0003.pdf e così via. Se si specifica un percorso di file, i file vengono posizionati sul server e non sul computer client.
* **Nome record**: specifica il nome dell&#39;elemento XML nell&#39;origine dati che separa i record di dati. Nell&#39;origine dati XML di esempio mostrata in precedenza in questa sezione, ad esempio, l&#39;elemento XML che separa i record di dati è denominato `LoanRecord`. Anziché impostare l&#39;opzione di runtime Nome record, è possibile impostare il livello record assegnandogli un valore numerico che indica il livello dell&#39;elemento contenente i record di dati. Tuttavia, è possibile impostare solo il Nome record o il Livello record. Non è possibile impostare entrambi i valori.)

**Impostare le opzioni di runtime di rendering**

È possibile impostare le opzioni di rendering in fase di esecuzione durante la creazione di più file. Anche se queste opzioni non sono obbligatorie (a differenza delle opzioni di runtime di output, che sono obbligatorie), è possibile eseguire attività quali il miglioramento delle prestazioni del servizio di output. È ad esempio possibile memorizzare nella cache la struttura del modulo utilizzata dal servizio di output per migliorare le prestazioni.

Quando il servizio di output elabora i record batch, legge i dati che contengono più record in modo incrementale. In altre parole, il servizio di output legge i dati nella memoria e li rilascia durante l’elaborazione del batch di record. Il servizio di output carica i dati in modo incrementale quando viene impostata una delle due opzioni di runtime. Se si imposta l&#39;opzione di runtime Nome record, il servizio di output legge i dati in modo incrementale. Analogamente, se si imposta l&#39;opzione di runtime Livello record su 2 o su un valore maggiore, il servizio di output legge i dati in modo incrementale.

È possibile controllare se il servizio di output esegue il caricamento incrementale utilizzando il metodo `setLazyLoading` dell&#39;oggetto `PDFOutputOptionsSpec` o `PrintedOutputOptionSpec`. È possibile passare il valore `false` a questo metodo che disattiva il caricamento incrementale.

**Generare più file PDF**

Dopo aver fatto riferimento a un&#39;origine dati XML valida che contiene più record di dati e aver impostato le opzioni di runtime, è possibile richiamare il servizio di output, che genera più file. Quando si generano più record, il metodo `getGeneratedDoc` dell&#39;oggetto `OutputResult` restituisce `null`.

**Recupera i risultati dell&#39;operazione**

Dopo l&#39;esecuzione di un&#39;operazione, il servizio di output restituisce dati XML che specificano se l&#39;operazione è stata eseguita correttamente. Il seguente XML viene restituito dal servizio di output. In questa situazione, il servizio di output ha generato 42 documenti.

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

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API servizio di output](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Creare più file PDF utilizzando l’API Java {#create-multiple-pdf-files-using-the-java-api}

Crea più file PDF utilizzando l’API di output (Java):

1. Includi file di progetto&quot;

   Includi i file JAR client, come adobe-output-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto client di output

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `OutputClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Riferimento a un&#39;origine dati XML

   * Creare un oggetto `java.io.FileInputStream` che rappresenta l&#39;origine dati XML contenente più record utilizzando il relativo costruttore e passando un valore stringa che specifica la posizione del file XML.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Imposta opzioni runtime di PDF

   * Creare un oggetto `PDFOutputOptionsSpec` utilizzando il relativo costruttore.
   * Impostare l&#39;opzione Molti file richiamando il metodo `setGenerateManyFiles` dell&#39;oggetto `PDFOutputOptionsSpec`. Passare ad esempio il valore `true` per indicare al servizio di output di creare un file PDF separato per ogni record nell&#39;origine dati XML. Se si passa `false`, il servizio di output genera un singolo documento PDF contenente tutti i record.
   * Impostare l&#39;opzione URI file richiamando il metodo `setFileUri` dell&#39;oggetto `PDFOutputOptionsSpec` e passando un valore stringa che specifica la posizione dei file generati dal servizio di output. L&#39;opzione URI file è relativa al server applicazioni J2EE che ospita AEM Forms, non al computer client.
   * Impostare l&#39;opzione Nome record richiamando il metodo `setRecordName` dell&#39;oggetto `OutputOptionsSpec` e passando un valore stringa che specifica il nome dell&#39;elemento XML nell&#39;origine dati che separa i record di dati. Si consideri ad esempio l&#39;origine dati XML illustrata in precedenza in questa sezione. Il nome dell&#39;elemento XML che separa i record di dati è LoanRecord).

1. Impostare le opzioni di runtime di rendering

   * Creare un oggetto `RenderOptionsSpec` utilizzando il relativo costruttore.
   * Memorizza nella cache la struttura del modulo per migliorare le prestazioni del servizio di output richiamando `setCacheEnabled` dell&#39;oggetto `RenderOptionsSpec` e passando un valore `Boolean` di `true`.

1. Genera più file PDF

   Generare più file PDF richiamando il metodo `generatePDFOutput` dell&#39;oggetto `OutputClient` e passando i valori seguenti:

   * Un valore enum `TransformationFormat`. Per generare un documento PDF, specificare `TransformationFormat.PDF`.
   * Valore stringa che specifica il nome della struttura del modulo.
   * Valore stringa che specifica la directory principale del contenuto in cui si trova la struttura del modulo.
   * Oggetto `PDFOutputOptionsSpec` contenente le opzioni di runtime di PDF.
   * Oggetto `RenderOptionsSpec` contenente le opzioni di rendering in fase di esecuzione.
   * Oggetto `com.adobe.idp.Document` contenente l&#39;origine dati XML contenente i dati da unire con la struttura del modulo.

   Il metodo `generatePDFOutput` restituisce un oggetto `OutputResult` contenente i risultati dell&#39;operazione.

1. Recuperare i risultati dell&#39;operazione

   * Creare un oggetto `java.io.File` che rappresenta un file XML contenente i risultati del metodo `generatePDFOutput`. Verificare che l&#39;estensione del nome file sia .xml.
   * Richiamare il metodo `copyToFile` dell&#39;oggetto `com.adobe.idp.Document` per copiare il contenuto dell&#39;oggetto `com.adobe.idp.Document` nel file (assicurarsi di utilizzare l&#39;oggetto `com.adobe.idp.Document` restituito dal metodo `applyUsageRights`).

**Consulta anche**

[Riepilogo dei passaggi](creating-document-output-streams.md#summary-of-steps)

[Guida rapida (modalità EJB): creazione di più file PDF tramite l’API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-multiple-pdf-files-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Creare più file PDF utilizzando l’API del servizio web {#create-multiple-pdf-files-using-the-web-service-api}

Crea più file PDF utilizzando l’API di output (servizio web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Creare un oggetto client di output.

   * Creare un oggetto `OutputServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `OutputServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/OutputService?blob=mtom`). Non è necessario utilizzare l&#39;attributo `lc_version`. Questo attributo viene utilizzato quando si crea un riferimento a un servizio. Tuttavia, specificare `?blob=mtom` per utilizzare MTOM.
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `OutputServiceClient.Endpoint.Binding`. Eseguire il cast del valore restituito in `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegnare il nome utente dei moduli AEM al campo `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `OutputServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Fare riferimento a un&#39;origine dati XML.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare i dati del modulo che contengono più record.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore. Passa un valore stringa che rappresenta la posizione del file XML contenente più record.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni della matrice di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare la matrice di byte con i dati di flusso richiamando il metodo `Read` dell&#39;oggetto `System.IO.FileStream` e passando la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando il relativo campo `MTOM` al contenuto della matrice di byte.

1. Impostare le opzioni di runtime di PDF.

   * Creare un oggetto `PDFOutputOptionsSpec` utilizzando il relativo costruttore.
   * Impostare l&#39;opzione Molti file assegnando un valore booleano al membro dati `generateManyFiles` dell&#39;oggetto `OutputOptionsSpec`. Assegnare ad esempio il valore `true` a questo membro dati per indicare al servizio di output di creare un file PDF separato per ogni record nell&#39;origine dati XML. Se si assegna `false` a questo membro dati, il servizio di output genera un singolo PDF contenente tutti i record.
   * Impostare l&#39;opzione URI file assegnando un valore stringa che specifichi la posizione dei file generati dal servizio di output al membro dati `fileURI` dell&#39;oggetto `OutputOptionsSpec`. L&#39;opzione URI file è relativa al server applicazioni J2EE che ospita AEM Forms, non al computer client.
   * Impostare l&#39;opzione del nome del record assegnando un valore stringa che specifichi il nome dell&#39;elemento XML nell&#39;origine dati che separa i record di dati dal membro dati `recordName` dell&#39;oggetto `OutputOptionsSpec`.
   * Impostare l&#39;opzione relativa alle copie assegnando un valore intero che specifichi il numero di copie generate dal servizio di output al membro dati `copies` dell&#39;oggetto `OutputOptionsSpec`.

1. Impostate le opzioni di runtime per il rendering.

   * Creare un oggetto `RenderOptionsSpec` utilizzando il relativo costruttore.
   * Memorizza nella cache la struttura del modulo per migliorare le prestazioni del servizio di output assegnando il valore `true` al membro dati `cacheEnabled` dell&#39;oggetto `RenderOptionsSpec`.

1. Genera più file PDF.

   Creare più file PDF richiamando il metodo `generatePDFOutput` dell&#39;oggetto `OutputServiceService` e passando i valori seguenti:

   * Valore enum TransformationFormat. Per generare un documento PDF, specificare `TransformationFormat.PDF`.
   * Valore stringa che specifica il nome della struttura del modulo.
   * Valore stringa che specifica la directory principale del contenuto in cui si trova la struttura del modulo.
   * Oggetto `PDFOutputOptionsSpec` contenente le opzioni di runtime di PDF.
   * Oggetto `RenderOptionsSpec` contenente le opzioni di rendering in fase di esecuzione.
   * Oggetto `BLOB` contenente l&#39;origine dati XML contenente i dati da unire con la struttura del modulo.
   * Oggetto `BLOB` popolato dal metodo `generatePDFOutput`. Il metodo `generatePDFOutput` popola questo oggetto con i metadati generati che descrivono il documento.
   * Oggetto `BLOB` popolato dal metodo `generatePDFOutput`. Il metodo `generatePDFOutput` popola questo oggetto con i dati dei risultati.
   * Oggetto `OutputResult` contenente i risultati dell&#39;operazione.

1. Recuperare i risultati dell&#39;operazione

   * Creare un oggetto `System.IO.FileStream` richiamandone il costruttore e passando un valore stringa che rappresenta un percorso di file XML contenente i dati dei risultati. Verificare che l&#39;estensione del nome file sia .xml.
   * Creare una matrice di byte che memorizza il contenuto dei dati dell&#39;oggetto `BLOB` che è stato popolato con i dati dei risultati dal metodo `generatePDFOutput` dell&#39;oggetto `OutputServiceService` (ottavo parametro). Popolare la matrice di byte ottenendo il valore del membro dati `binaryData` dell&#39;oggetto `BLOB`.
   * Creare un oggetto `System.IO.BinaryWriter` richiamandone il costruttore e passando l&#39;oggetto `System.IO.FileStream`.
   * Scrivere il contenuto della matrice di byte nel file XML richiamando il metodo `Write` dell&#39;oggetto `System.IO.BinaryWriter` e passando la matrice di byte.

**Consulta anche**

[Riepilogo dei passaggi](creating-document-output-streams.md#summary-of-steps)

[Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamare AEM Forms con SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Creazione di regole di ricerca {#creating-search-rules}

È possibile creare regole di ricerca in modo che il servizio di output esamini i dati di input e utilizzi diverse progettazioni di moduli in base al contenuto dei dati per generare l’output. Ad esempio, se il testo *mutuo* si trova all&#39;interno dei dati di input, il servizio di output può utilizzare una struttura di modulo denominata Mutuo.xdp. Analogamente, se il testo *automobile* è incluso nei dati di input, il servizio di output può utilizzare una struttura di modulo salvata come AutomobileLoan.xdp. Sebbene il servizio di output possa generare diversi tipi di output, questa sezione presuppone che il servizio di output generi un file PDF. Nel diagramma seguente viene illustrato il servizio di output che genera un file PDF elaborando un file di dati XML e utilizzando una delle numerose progettazioni di moduli.

Inoltre, il servizio di output è in grado di generare pacchetti di documenti, in cui vengono forniti più record nel set di dati e ogni record viene abbinato a una progettazione di moduli e viene generato un singolo documento composto da più progettazioni di moduli.

![cs_outputbatchmanyformdesigns2](assets/cs_outputbatchmanyformdesigns2.png)

>[!NOTE]
>
>Per ulteriori informazioni sul servizio di output, vedere [Riferimento ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-8}

Per indicare al servizio di output di utilizzare le regole di ricerca durante la generazione di un documento, effettuare le seguenti operazioni:

1. Includi file di progetto.
1. Creare un oggetto client di output.
1. Fare riferimento a un&#39;origine dati XML.
1. Definisci le regole di ricerca.
1. Impostare le opzioni di runtime di PDF.
1. Impostate le opzioni di runtime per il rendering.
1. Genera un documento PDF.
1. Recuperate i risultati dell&#39;operazione.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è implementato su JBoss)
* jbossall-client.jar (obbligatorio se AEM Forms è distribuito su JBoss)

se AEM Forms viene distribuito su un server applicazioni J2EE supportato che non è JBoss, è necessario sostituire adobe-utilities.jar e jbossall-client.jar con file JAR specifici per il server applicazioni J2EE in cui viene distribuito AEM Forms.

**Crea un oggetto client di output**

Prima di poter eseguire un&#39;operazione del servizio di output a livello di programmazione, è necessario creare un oggetto client del servizio di output.

**Riferimento a un&#39;origine dati XML**

Un elemento XML deve esistere per ogni campo modulo che si desidera compilare con i dati. Il nome dell&#39;elemento XML deve corrispondere al nome del campo. Un elemento XML viene ignorato se non corrisponde a un campo modulo o se il nome dell&#39;elemento XML non corrisponde al nome del campo. Non è necessario che corrispondano all&#39;ordine di visualizzazione degli elementi XML, purché siano specificati tutti gli elementi XML.

**Definire le regole di ricerca**

Per definire le regole di ricerca, è necessario definire uno o più pattern di testo che i servizi di output ricercano nei dati di input. Per ogni motivo di testo definito, è necessario specificare uno schema di modulo corrispondente utilizzato se il motivo di testo è posizionato. Se si trova un pattern di testo, il servizio di output utilizza il design del modulo corrispondente per generare l’output. Un esempio di modello di testo è *mutuo*.

>[!NOTE]
>
>Se i motivi di testo non sono posizionati, viene utilizzato il modulo predefinito. Verificare che tutte le progettazioni di moduli utilizzate siano nella directory principale del contenuto.

**Imposta opzioni runtime di PDF**

Per consentire al servizio di output di creare correttamente un documento PDF basato su più progettazioni di moduli, impostare le seguenti opzioni di runtime di PDF:

* **URI file**: specifica il nome e il percorso del file PDF generato dal servizio di output.
* **Regole**: specifica le regole definite.
* **LookAHead**: specifica il numero di byte da utilizzare dall&#39;inizio del file di dati di input per la ricerca dei pattern di testo definiti. Il valore predefinito è 500 byte.

**Impostare le opzioni di runtime di rendering**

È possibile impostare le opzioni di rendering in fase di esecuzione durante la creazione di file PDF. Sebbene queste opzioni non siano necessarie (a differenza delle opzioni di runtime di PDF), è possibile eseguire attività quali il miglioramento delle prestazioni del servizio di output. È ad esempio possibile memorizzare nella cache la struttura del modulo utilizzata dal servizio di output per migliorare le prestazioni.

**Generare un documento PDF**

Dopo aver fatto riferimento a un&#39;origine dati XML valida e aver impostato le opzioni di runtime, è possibile richiamare il servizio di output per generare un documento PDF. Se il servizio di output individua un motivo di testo specificato nei dati di input, utilizza la struttura del modulo corrispondente. Se non viene utilizzato un motivo di testo, il servizio di output utilizza la struttura predefinita del modulo.

**Recupera i risultati dell&#39;operazione**

Dopo l&#39;esecuzione di un&#39;operazione, il servizio di output restituisce dati XML che specificano se l&#39;operazione è stata eseguita correttamente.

**Consulta anche**

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API servizio di output](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Creare regole di ricerca tramite API Java {#create-search-rules-using-the-java-api}

Crea regole di ricerca utilizzando l’API di output (Java):

1. Includi file di progetto.

   Includi i file JAR client, come adobe-output-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto client di output.

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `OutputClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Fare riferimento a un&#39;origine dati XML.

   * Creare un oggetto `java.io.FileInputStream` che rappresenta l&#39;origine dati XML utilizzata per popolare il documento PDF utilizzando il relativo costruttore e passando un valore stringa che specifica la posizione del file XML.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Definisci le regole di ricerca.

   * Creare un oggetto `Rule` utilizzando il relativo costruttore.
   * Definire un pattern di testo richiamando il metodo `setPattern` dell&#39;oggetto `Rule` e passando un valore stringa che specifica un pattern di testo.
   * Definire la struttura del modulo corrispondente richiamando il metodo `setForm` dell&#39;oggetto `Rule`. Passa un valore stringa che specifica il nome della struttura del modulo.

   >[!NOTE]
   >
   >Per ogni motivo di testo che si desidera definire, ripetere i tre passaggi secondari precedenti.

   * Creare un oggetto `java.util.List` utilizzando un costruttore `java.util.ArrayList`.
   * Per ogni oggetto `Rule` creato, richiamare il metodo `add` dell&#39;oggetto `java.util.List` e passare l&#39;oggetto `Rule`.

1. Impostare le opzioni di runtime di PDF.

   * Creare un oggetto `PDFOutputOptionsSpec` utilizzando il relativo costruttore.
   * Specificare il nome e il percorso del file PDF generato dal servizio di output richiamando il metodo `setFileURI` dell&#39;oggetto `PDFOutputOptionsSpec`. Passa un valore stringa che specifica la posizione del file PDF. L&#39;opzione URI file è relativa al server applicazioni J2EE che ospita AEM Forms, non al computer client.
   * Impostare le regole definite richiamando il metodo `setRules` dell&#39;oggetto `PDFOutputOptionsSpec`. Passa l&#39;oggetto `java.util.List` che contiene gli oggetti `Rule`.
   * Impostare il numero di byte da analizzare per i pattern di testo definiti richiamando il metodo `setLookAhead` dell&#39;oggetto `PDFOutputOptionsSpec`. Passa un valore intero che rappresenta i numeri di byte.

1. Impostate le opzioni di runtime per il rendering.

   * Creare un oggetto `RenderOptionsSpec` utilizzando il relativo costruttore.
   * Memorizza nella cache la struttura del modulo per migliorare le prestazioni del servizio di output richiamando `setCacheEnabled` dell&#39;oggetto `RenderOptionsSpec` e passando `true`.

1. Genera un documento PDF.

   Generare un documento PDF basato su più progettazioni di moduli richiamando il metodo `generatePDFOutput` dell&#39;oggetto `OutputClient` e passando i valori seguenti:

   * Valore di enumerazione `TransformationFormat`. Per generare un documento PDF, specificare `TransformationFormat.PDF`.
   * Valore stringa che specifica il nome della struttura predefinita del modulo. In altre parole, la struttura del modulo utilizzata se non è stato individuato un motivo di testo.
   * Valore stringa che specifica la directory principale del contenuto in cui si trovano le progettazioni del modulo.
   * Oggetto `PDFOutputOptionsSpec` contenente le opzioni di runtime di PDF.
   * Oggetto `RenderOptionsSpec` contenente le opzioni di rendering in fase di esecuzione.
   * L&#39;oggetto `com.adobe.idp.Document` che contiene i dati del modulo in cui il servizio di output esegue la ricerca dei pattern di testo definiti.

   Il metodo `generatePDFOutput` restituisce un oggetto `OutputResult` contenente i risultati dell&#39;operazione.

1. Recuperate i risultati dell&#39;operazione.

   * Creare un oggetto `com.adobe.idp.Document` che rappresenta lo stato del metodo `generatePDFOutput` richiamando il metodo `getStatusDoc` dell&#39;oggetto `OutputResult`.
   * Creare un oggetto `java.io.File` che conterrà i risultati dell&#39;operazione. Verificare che l&#39;estensione del file sia .xml.
   * Richiamare il metodo `copyToFile` dell&#39;oggetto `com.adobe.idp.Document` per copiare il contenuto dell&#39;oggetto `com.adobe.idp.Document` nel file (assicurarsi di utilizzare l&#39;oggetto `com.adobe.idp.Document` restituito dal metodo `getStatusDoc`).

**Consulta anche**

[Riepilogo dei passaggi](creating-document-output-streams.md#summary-of-steps)

[Guida rapida (modalità EJB): creazione di regole di ricerca tramite l’API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-search-rules-using-the-java-api)

[Quick Start (modalità SOAP): creazione di regole di ricerca utilizzando l’API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-search-rules-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Creare regole di ricerca utilizzando l’API del servizio web {#create-search-rules-using-the-web-service-api}

Crea regole di ricerca utilizzando l’API di output (servizio web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Creare un oggetto client di output.

   * Creare un oggetto `OutputServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `OutputServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/OutputService?blob=mtom`). Non è necessario utilizzare l&#39;attributo `lc_version`. Questo attributo viene utilizzato quando si crea un riferimento a un servizio. Tuttavia, specificare `?blob=mtom` per utilizzare MTOM.
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `OutputServiceClient.Endpoint.Binding`. Eseguire il cast del valore restituito in `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegnare il nome utente dei moduli AEM al campo `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `OutputServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Fare riferimento a un&#39;origine dati XML.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare i dati che verranno uniti al documento PDF.
   * Creare un oggetto `System.IO.FileStream` richiamandone il costruttore e passando un valore stringa che rappresenta la posizione del file del documento PDF da crittografare e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni della matrice di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare la matrice di byte con i dati di flusso richiamando il metodo `Read` dell&#39;oggetto `System.IO.FileStream` e passando la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando il relativo campo `MTOM` al contenuto della matrice di byte.

1. Definisci le regole di ricerca.

   * Creare un oggetto `Rule` utilizzando il relativo costruttore.
   * Definire un pattern di testo assegnando un valore stringa che specifichi un pattern di testo al membro dati `pattern` dell&#39;oggetto `Rule`.
   * Definire la struttura del modulo corrispondente assegnando un valore stringa che specifichi la struttura del modulo al membro dati `form` dell&#39;oggetto `Rule`.

   >[!NOTE]
   >
   >Per ogni motivo di testo che si desidera definire, ripetere i tre passaggi secondari precedenti.

   * Creare un oggetto `MyArrayOf_xsd_anyType` che memorizza le regole.
   * Assegnare ogni oggetto `Rule` a un elemento dell&#39;array `MyArrayOf_xsd_anyType`. Richiama il metodo `Add` dell&#39;oggetto `MyArrayOf_xsd_anyType` per ogni oggetto `Rule`.

1. Imposta opzioni runtime di PDF

   * Creare un oggetto `PDFOutputOptionsSpec` utilizzando il relativo costruttore.
   * Impostare l&#39;opzione URI file assegnando un valore stringa che specifichi la posizione del file PDF generato dal servizio di output al membro dati `fileURI` dell&#39;oggetto `PDFOutputOptionsSpec`. L&#39;opzione URI file è relativa al server applicazioni J2EE che ospita AEM Forms, non al computer client.
   * Impostare l&#39;opzione relativa alle copie assegnando un valore intero che specifichi il numero di copie generate dal servizio di output al membro dati `copies` dell&#39;oggetto `PDFOutputOptionsSpec`.
   * Impostare le regole definite assegnando l&#39;oggetto `MyArrayOf_xsd_anyType` che memorizza le regole al membro dati `rules` dell&#39;oggetto `PDFOutputOptionsSpec`.
   * Impostare il numero di byte da analizzare per i pattern di testo definiti assegnando un valore intero che rappresenta il numero di byte da analizzare al metodo dati `lookAhead` dell&#39;oggetto `PDFOutputOptionsSpec`.

1. Impostare le opzioni di runtime di rendering

   * Creare un oggetto `RenderOptionsSpec` utilizzando il relativo costruttore.
   * Memorizza nella cache la struttura del modulo per migliorare le prestazioni del servizio di output assegnando il valore `true` al membro dati `cacheEnabled` dell&#39;oggetto `RenderOptionsSpec`.

   >[!NOTE]
   >
   >Impossibile impostare la versione del documento PDF utilizzando il membro `pdfVersion` dell&#39;oggetto `RenderOptionsSpec` se il documento di input è un modulo Acrobat. Il documento PDF di output conserva la versione PDF del modulo Acrobat. Analogamente, non è possibile impostare l&#39;opzione PDF con tag utilizzando il metodo `taggedPDF` dell&#39;oggetto `RenderOptionsSpec` se il documento di input è un modulo di Acrobat.

   >[!NOTE]
   >
   >Impossibile impostare l&#39;opzione PDF linearizzato utilizzando il membro `linearizedPDF` dell&#39;oggetto `RenderOptionsSpec` se il documento PDF di input è certificato o firmato digitalmente. Per informazioni, vedere [Firma digitale dei documenti di PDF](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents).

1. Generare un documento PDF

   Creare un documento PDF richiamando il metodo `generatePDFOutput` dell&#39;oggetto `OutputServiceService` e passando i valori seguenti:

   * Valore di enumerazione `TransformationFormat`. Per generare un documento PDF, specificare `TransformationFormat.PDF`.
   * Valore stringa che specifica il nome della struttura del modulo.
   * Valore stringa che specifica la directory principale del contenuto in cui si trova la struttura del modulo.
   * Oggetto `PDFOutputOptionsSpec` contenente le opzioni di runtime di PDF.
   * Oggetto `RenderOptionsSpec` contenente le opzioni di rendering in fase di esecuzione.
   * Oggetto `BLOB` contenente l&#39;origine dati XML contenente i dati da unire con la struttura del modulo.
   * Oggetto `BLOB` popolato dal metodo `generatePDFOutput`. Il metodo `generatePDFOutput` popola questo oggetto con i metadati generati che descrivono il documento. (Questo valore di parametro è richiesto solo per la chiamata del servizio Web).
   * Oggetto `BLOB` popolato dal metodo `generatePDFOutput`. Il metodo `generatePDFOutput` popola questo oggetto con i dati dei risultati. (Questo valore di parametro è richiesto solo per la chiamata del servizio Web).
   * Oggetto `OutputResult` contenente i risultati dell&#39;operazione. (Questo valore di parametro è richiesto solo per la chiamata del servizio Web).

   >[!NOTE]
   >
   >Quando si genera un documento PDF richiamando il metodo `generatePDFOutput`, non è possibile unire i dati con un modulo PDF XFA firmato, certificato o contenente diritti di utilizzo. Per informazioni sui diritti di utilizzo, vedere [Applicazione dei diritti di utilizzo ai documenti di PDF](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents).

1. Recuperare i risultati dell&#39;operazione

   * Creare un oggetto `System.IO.FileStream` richiamandone il costruttore e passando un valore stringa che rappresenta un percorso di file XML contenente i dati dei risultati. Assicurati che l’estensione del file sia XML.
   * Creare una matrice di byte che memorizza il contenuto dei dati dell&#39;oggetto `BLOB` che è stato popolato con i dati dei risultati dal metodo `generatePDFOutput` dell&#39;oggetto `OutputServiceService` (ottavo parametro). Popolare la matrice di byte ottenendo il valore del membro dati `MTOM` dell&#39;oggetto `BLOB`.
   * Creare un oggetto `System.IO.BinaryWriter` richiamandone il costruttore e passando l&#39;oggetto `System.IO.FileStream`.
   * Scrivere il contenuto della matrice di byte nel file XML richiamando il metodo `Write` dell&#39;oggetto `System.IO.BinaryWriter` e passando la matrice di byte.

**Consulta anche**

[Riepilogo dei passaggi](creating-document-output-streams.md#summary-of-steps)

[Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamare AEM Forms con SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Appiattimento documenti PDF {#flattening-pdf-documents}

È possibile utilizzare il servizio di output per trasformare un documento di PDF interattivo in un PDF non interattivo. Un documento PDF interattivo consente agli utenti di immettere o modificare i dati presenti nei campi del documento PDF. Il processo di trasformazione di un documento interattivo di PDF in un documento non interattivo di PDF è denominato *appiattimento*. Quando un documento PDF viene appiattito, un utente non può modificare i dati nei campi del documento. Uno dei motivi per appiattire un documento PDF è garantire che i dati non possano essere modificati.

È possibile appiattire i seguenti tipi di documenti PDF:

* Documenti interattivi di XFA PDF
* Acrobat Forms

Il tentativo di appiattire un PDF che è un documento PDF non interattivo causa un&#39;eccezione.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio di output, vedere [Riferimento ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-9}

Per appiattire un documento PDF interattivo in un documento PDF non interattivo, effettuare le seguenti operazioni:

1. Includi file di progetto.
1. Creare un oggetto client di output.
1. Recupera un documento interattivo di PDF.
1. Trasforma il documento PDF.
1. Salvare il documento PDF non interattivo come file PDF.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso della classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è implementato su JBoss)
* jbossall-client.jar (obbligatorio se AEM Forms è distribuito su JBoss)

se AEM Forms viene distribuito su un server applicazioni J2EE supportato che non è JBoss, è necessario sostituire i file adobe-utilities.jar e jbossall-client.jar con file JAR specifici per il server applicazioni J2EE in cui viene distribuito AEM Forms. Per informazioni sulla posizione di tutti i file JAR di AEM Forms, vedi [Inclusi i file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Crea un oggetto client di output**

Prima di poter eseguire un&#39;operazione del servizio di output a livello di programmazione, è necessario creare un oggetto client del servizio di output. Se si utilizza l&#39;API Java, creare un oggetto `OutputClient`. Se si utilizza l&#39;API del servizio Web di output, creare un oggetto `OutputServiceService`.

**Recuperare un documento interattivo di PDF**

Recuperare un documento PDF interattivo che si desidera trasformare in un documento PDF non interattivo. Se si tenta di trasformare un documento PDF non interattivo, viene generata un&#39;eccezione.

**Trasforma il documento PDF**

Dopo aver recuperato un documento PDF interattivo, è possibile trasformarlo in un documento PDF non interattivo. Il servizio di output restituisce un documento PDF non interattivo.

**Salvare il documento PDF non interattivo come file PDF**

È possibile salvare il documento PDF non interattivo come file PDF.

**Consulta anche**

[Appiattire un documento PDF utilizzando l’API Java](creating-document-output-streams.md#flatten-a-pdf-document-using-the-java-api)

[Appiattire un documento PDF utilizzando l’API del servizio web](creating-document-output-streams.md#flatten-a-pdf-document-using-the-web-service-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API servizio di output](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Appiattire un documento PDF utilizzando l’API Java {#flatten-a-pdf-document-using-the-java-api}

Appiattisci un documento PDF interattivo a un documento PDF non interattivo utilizzando l’API di output (Java):

1. Includi file di progetto.

   Includi i file JAR client, come adobe-output-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto client di output.

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `OutputClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Recupera un documento interattivo di PDF.

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento PDF interattivo da trasformare utilizzando il relativo costruttore e passando un valore stringa che specifica la posizione del file PDF interattivo.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Trasforma il documento PDF.

   Trasformare il documento PDF interattivo in un documento PDF non interattivo richiamando il metodo `transformPDF` dell&#39;oggetto `OutputServiceService` e passando i valori seguenti:

   * L&#39;oggetto `com.adobe.idp.Document` che contiene il documento interattivo di PDF.
   * Un valore enum `TransformationFormat`. Per generare un documento PDF non interattivo, specificare `TransformationFormat.PDF`.
   * Valore enum `PDFARevisionNumber` che specifica il numero di revisione. Poiché questo parametro è destinato a un documento PDF/A, è possibile specificare `null`.
   * Valore string che rappresenta il numero e l&#39;anno della modifica, separati da due punti. Poiché questo parametro è destinato a un documento PDF/A, è possibile specificare `null`.
   * Valore enum `PDFAConformance` che rappresenta il livello di conformità PDF/A. Poiché questo parametro è destinato a un documento PDF/A, è possibile specificare `null`.

   Il metodo `transformPDF` restituisce un oggetto `com.adobe.idp.Document` che contiene un documento PDF non interattivo.

1. Salvare il documento PDF non interattivo come file PDF.

   * Creare un oggetto `java.io.File` e verificare che l&#39;estensione del nome file sia pdf.
   * Richiamare il metodo `copyToFile` dell&#39;oggetto `Document` per copiare il contenuto dell&#39;oggetto `Document` nel file (assicurarsi di utilizzare l&#39;oggetto `Document` restituito dal metodo `transformPDF`).

**Consulta anche**

[Riepilogo dei passaggi](creating-document-output-streams.md#summary-of-steps)

[Quick Start (modalità EJB): trasformazione di un documento PDF tramite API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-transforming-a-pdf-document-using-the-java-api)

[Quick Start (modalità SOAP): trasformazione di un documento PDF tramite API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-transforming-a-pdf-document-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Appiattire un documento PDF utilizzando l’API del servizio web {#flatten-a-pdf-document-using-the-web-service-api}

Appiattisci un documento PDF interattivo a un documento PDF non interattivo utilizzando l’API di output (servizio web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Creare un oggetto client di output.

   * Creare un oggetto `OutputServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `OutputServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/OutputService?blob=mtom`). Non è necessario utilizzare l&#39;attributo `lc_version`. Questo attributo viene utilizzato quando si crea un riferimento a un servizio. Tuttavia, specificare `?blob=mtom` per utilizzare MTOM.
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `OutputServiceClient.Endpoint.Binding`. Eseguire il cast del valore restituito in `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegnare il nome utente dei moduli AEM al campo `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `OutputServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recupera un documento interattivo di PDF.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare il documento interattivo di PDF.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore stringa che rappresenta la posizione del file del documento interattivo di PDF.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni della matrice di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare la matrice di byte con i dati di flusso richiamando il metodo `Read` dell&#39;oggetto `System.IO.FileStream` e passando la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando la relativa proprietà `MTOM` al contenuto della matrice di byte.

1. Trasforma il documento PDF.

   Trasformare il documento PDF interattivo in un documento PDF non interattivo richiamando il metodo `transformPDF` dell&#39;oggetto `OutputClient` e passando i valori seguenti:

   * Oggetto `BLOB` contenente il documento interattivo di PDF.
   * Valore di enumerazione `TransformationFormat`. Per generare un documento PDF non interattivo, specificare `TransformationFormat.PDF`.
   * Valore enum `PDFARevisionNumber` che specifica il numero di revisione.
   * Valore booleano che specifica se viene utilizzato il valore enum `PDFARevisionNumber`. Poiché questo parametro è destinato a un documento PDF/A, è possibile specificare `false`.
   * Valore string che rappresenta il numero e l&#39;anno della modifica, separati da due punti. Poiché questo parametro è destinato a un documento PDF/A, è possibile specificare `null`.
   * Valore enum `PDFAConformance` che rappresenta il livello di conformità PDF/A.
   * Valore booleano che specifica se viene utilizzato il valore enum `PDFAConformance`. Poiché questo parametro è destinato a un documento PDF/A, è possibile specificare `false`.

   Il metodo `transformPDF` restituisce un oggetto `BLOB` che contiene un documento PDF non interattivo.

1. Salvare il documento PDF non interattivo come file PDF.

   * Creare un oggetto `System.IO.FileStream` richiamandone il costruttore e passando un valore stringa che rappresenta la posizione del file del documento PDF non interattivo.
   * Creare una matrice di byte che memorizza il contenuto dei dati dell&#39;oggetto `BLOB` restituito dal metodo `transformPDF`. Popolare la matrice di byte ottenendo il valore del membro dati `MTOM` dell&#39;oggetto `BLOB`.
   * Creare un oggetto `System.IO.BinaryWriter` richiamandone il costruttore e passando l&#39;oggetto `System.IO.FileStream`.
   * Scrivere il contenuto della matrice di byte in un file PDF richiamando il metodo `Write` dell&#39;oggetto `System.IO.BinaryWriter` e passando la matrice di byte.

**Consulta anche**

[Riepilogo dei passaggi](creating-document-output-streams.md#summary-of-steps)

[Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamare AEM Forms con SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
