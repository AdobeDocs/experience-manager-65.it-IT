---
title: Gestione di Forms inviati
seo-title: Handling Submitted Forms
description: Utilizzare il servizio Forms per recuperare i dati inviati immessi in un modulo interattivo. L’utente può inviare i dati del modulo in formati XML, PDF e URL UTF-16.
seo-description: Use the Forms service to retrieve the submitted data entered in an interactive form. The user can submit the form data in XML, PDF, and URL UTF-16 formats.
uuid: 673b28f1-f023-4da8-a6a0-c5ff921c5f5d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 3d838027-6bde-4a71-a428-4d5102f7d799
role: Developer
exl-id: 419335b2-2aae-4e83-98ff-18e61b7efa9c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2904'
ht-degree: 0%

---

# Gestione di Forms inviati {#handling-submitted-forms}

**Esempi ed esempi in questo documento sono solo per AEM Forms in ambiente JEE.**

Per le applicazioni basate sul Web che consentono all’utente di compilare moduli interattivi è necessario che i dati vengano inviati nuovamente al server. Utilizzando il servizio Forms, è possibile recuperare i dati immessi dall’utente in un modulo interattivo. Dopo aver recuperato i dati, puoi elaborarli per soddisfare le tue esigenze aziendali. Ad esempio, è possibile memorizzare i dati in un database, inviare i dati a un’altra applicazione, inviare i dati a un altro servizio, unire i dati in una struttura del modulo, visualizzare i dati in un browser Web e così via.

I dati modulo vengono inviati al servizio Forms come dati XML o PDF, opzione impostata in Designer. Un modulo inviato come XML consente di estrarre singoli valori di dati di campo. In altre parole, è possibile estrarre il valore di ciascun campo modulo immesso dall’utente. Un modulo inviato come dati di PDF è costituito da dati binari, non da dati XML. È possibile salvare il modulo come file PDF o inviarlo a un altro servizio. Se si desidera estrarre dati da un modulo inviato come XML e quindi utilizzare i dati del modulo per creare un documento PDF, avviare un&#39;altra operazione AEM Forms. (Vedi [Creazione di documenti PDF con dati XML inviati](/help/forms/developing/creating-pdf-documents-submitted-xml.md))

Il diagramma seguente mostra i dati inviati a un servlet Java denominato `HandleData` da un modulo interattivo visualizzato in un browser web.

![hs_handlesubmit](assets/hs_hs_handlesubmit.png)

Nella tabella seguente sono descritti i passaggi del diagramma.

<table>
 <thead>
  <tr>
   <th><p>Incremento</p></th>
   <th><p>Descrizione</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>1</p></td>
   <td><p>Un utente compila un modulo interattivo e fa clic sul pulsante Invia del modulo.</p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>I dati vengono inviati al <code>HandleData</code> Java Servlet come dati XML.</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>La <code>HandleData</code> Java Servlet contiene la logica dell'applicazione per recuperare i dati.</p></td>
  </tr>
 </tbody>
</table>

## Gestione dei dati XML inviati {#handling-submitted-xml-data}

Quando i dati del modulo vengono inviati come XML, è possibile recuperare i dati XML che rappresentano i dati inviati. Tutti i campi modulo vengono visualizzati come nodi in uno schema XML. I valori dei nodi corrispondono ai valori inseriti dall&#39;utente. Si consideri un modulo di prestito in cui ogni campo del modulo viene visualizzato come un nodo all’interno dei dati XML. Il valore di ogni nodo corrisponde al valore che un utente compila. Supponiamo che un utente compili il modulo di prestito con i dati mostrati nel seguente modulo.

![hs_loanformdata](assets/hs_hs_loanformdata.png)

L’illustrazione seguente mostra i dati XML corrispondenti recuperati utilizzando l’API client del servizio Forms.

![hs_loandata](assets/hs_hs_loandata.png)

I campi nel modulo di prestito. Questi valori possono essere recuperati utilizzando le classi Java XML.

>[!NOTE]
>
>La struttura del modulo deve essere configurata correttamente in Designer per consentire l’invio dei dati come dati XML. Per configurare in modo appropriato la struttura del modulo per l’invio dei dati XML, assicurarsi che il pulsante Invia presente nella struttura del modulo sia impostato per l’invio dei dati XML. Per informazioni sull’impostazione del pulsante Invia per l’invio dei dati XML, vedere [AEM Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63).

## Gestione dei dati PDF inviati {#handling-submitted-pdf-data}

Considera un&#39;applicazione web che richiama il servizio Forms. Dopo che il servizio Forms esegue il rendering di un modulo PDF interattivo in un browser Web client, l’utente compila il modulo e lo invia nuovamente come dati di PDF. Quando il servizio Forms riceve i dati di PDF, può inviare i dati di PDF a un altro servizio o salvarli come file PDF. Il diagramma seguente mostra il flusso logico dell’applicazione.

![hs_savingforms](assets/hs_hs_savingforms.png)

La tabella seguente descrive i passaggi descritti in questo diagramma.

<table>
 <thead>
  <tr>
   <th><p>Incremento</p></th>
   <th><p>Descrizione</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>1</p></td>
   <td><p>Una pagina web contiene un collegamento che accede a un servlet Java che richiama il servizio Forms.</p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>Il servizio Forms esegue il rendering di un modulo PDF interattivo nel browser Web del client.</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>L’utente compila un modulo interattivo e fa clic su un pulsante di invio. Il modulo viene inviato nuovamente al servizio Forms come dati di PDF. Questa opzione è impostata in Designer.</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>Il servizio Forms salva i dati di PDF come file PDF. </p></td>
  </tr>
 </tbody>
</table>

## Gestione dei dati dell’URL UTF-16 inviati {#handling-submitted-url-utf-16-data}

Se i dati del modulo vengono inviati come dati URL UTF-16, il computer client richiede Adobe Reader o Acrobat 8.1 o versione successiva. Anche se la struttura del modulo contiene un pulsante di invio con dati codificati tramite URL (HTTP Post) e l’opzione di codifica dei dati è UTF-16, la struttura del modulo deve essere modificata in un editor di testo come Blocco note. Puoi impostare l’opzione di codifica su `UTF-16LE` o `UTF-16BE` per il pulsante di invio. Designer non fornisce questa funzionalità.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Forms, vedi [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Riepilogo dei passaggi {#summary-of-steps}

Per gestire i moduli inviati, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Creare un oggetto API client Forms.
1. Recupera i dati del modulo.
1. Determinare se l’invio del modulo contiene allegati di file.
1. Elabora i dati inviati.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

**Creare un oggetto API client Forms**

Prima di poter eseguire programmaticamente un’operazione API client del servizio Forms, è necessario creare un client di servizio Forms. Se utilizzi l’API Java, crea un `FormsServiceClient` oggetto. Se utilizzi l’API del servizio Web Forms, crea un `FormsService` oggetto.

**Recupera dati modulo**

Per recuperare i dati del modulo inviati, è necessario invocare il `FormsServiceClient` dell’oggetto `processFormSubmission` metodo . Quando si richiama questo metodo, è necessario specificare il tipo di contenuto del modulo inviato. Quando i dati vengono inviati da un browser Web client al servizio Forms, possono essere inviati come dati XML o PDF. Per recuperare i dati immessi nei campi modulo, è possibile inviare i dati come dati XML.

È inoltre possibile recuperare i campi modulo da un modulo inviato come dati di PDF impostando le seguenti opzioni di esecuzione:

* Passa il seguente valore al `processFormSubmission` come parametro del tipo di contenuto: `CONTENT_TYPE=application/pdf`.
* Imposta la `RenderOptionsSpec` dell’oggetto `PDFToXDP` valore a `true`
* Imposta la `RenderOptionsSpec` dell’oggetto `ExportDataFormat` valore a `XMLData`

È possibile specificare il tipo di contenuto del modulo inviato quando si richiama il `processFormSubmission` metodo . Nell&#39;elenco seguente sono specificati i valori del tipo di contenuto applicabili:

* **text/xml**: Rappresenta il tipo di contenuto da utilizzare quando un modulo PDF invia dati del modulo come XML.
* **application/x-www-form-urlencoded**: Rappresenta il tipo di contenuto da utilizzare quando un modulo HTML invia dati come XML.
* **application/pdf**: Rappresenta il tipo di contenuto da utilizzare quando un modulo PDF invia dati come PDF.

>[!NOTE]
>
>Noterai che sono presenti tre avvii rapidi corrispondenti associati alla sezione Gestione del Forms inviato . La guida rapida alla gestione dei PDF forms inviati come PDF tramite l’API Java illustra come gestire i dati di PDF inviati. Il tipo di contenuto specificato in questo avvio rapido è `application/pdf`. Il rapido avvio di Gestione dei PDF forms inviati come XML tramite l’API Java illustra come gestire i dati XML inviati da un modulo PDF. Il tipo di contenuto specificato in questo avvio rapido è `text/xml`. Analogamente, la gestione dei moduli HTML inviati come XML tramite l’avvio rapido dell’API Java illustra come gestire i dati XML inviati da un modulo HTML. Il tipo di contenuto specificato in questo avvio rapido è application/x-www-form-urlencoded .

È possibile recuperare i dati del modulo inviati al servizio Forms e determinarne lo stato di elaborazione. In altre parole, quando i dati vengono inviati al servizio Forms, non significa necessariamente che il servizio Forms abbia terminato l’elaborazione dei dati e che i dati siano pronti per essere elaborati. Ad esempio, i dati possono essere inviati al servizio Forms in modo da poter eseguire un calcolo. Una volta completato il calcolo, viene eseguito il rendering del modulo all’utente con i risultati del calcolo visualizzati. Prima di elaborare i dati inviati, è consigliabile determinare se il servizio Forms ha terminato l’elaborazione dei dati.

Il servizio Forms restituisce i seguenti valori per indicare se l’elaborazione dei dati è terminata:

* **0 (Invia):** I dati inviati sono pronti per essere elaborati.
* **1 (Calcola):** Il servizio Forms ha eseguito un’operazione di calcolo sui dati e i risultati devono essere resi nuovamente all’utente.
* **2 (Convalida):** I dati del modulo convalidati dal servizio Forms e i risultati devono essere resi all’utente.
* **3 (successivo):** La pagina corrente è cambiata con risultati che devono essere scritti nell’applicazione client.
* **4 (Precedente**): La pagina corrente è cambiata con risultati che devono essere scritti nell’applicazione client.

>[!NOTE]
>
>È necessario eseguire nuovamente il rendering dei calcoli e delle convalide per l&#39;utente. (Vedi [Calcolo dei dati del modulo](/help/forms/developing/calculating-form-data.md#calculating-form-data).

**Determinare se l’invio del modulo contiene allegati di file**

Forms inviato al servizio Forms può contenere allegati di file. Ad esempio, utilizzando il riquadro allegato integrato di Acrobat, un utente può selezionare file allegati da inviare insieme al modulo. Inoltre, un utente può selezionare file allegati utilizzando una barra degli strumenti di HTML di cui è eseguito il rendering con un file HTML.

Dopo aver determinato se un modulo contiene allegati ai file, è possibile elaborare i dati. Ad esempio, è possibile salvare l&#39;allegato al file system locale.

>[!NOTE]
>
>Per recuperare gli allegati del file, è necessario inviare il modulo come dati di PDF. Se il modulo viene inviato come dati XML, gli allegati di file non vengono inviati.

**Elaborazione dei dati inviati**

A seconda del tipo di contenuto dei dati inviati, è possibile estrarre singoli valori di campo modulo dai dati XML inviati o salvare i dati di PDF inviati come file PDF (o inviarli a un altro servizio). Per estrarre singoli campi del modulo, convertire i dati XML inviati in un’origine dati XML e quindi recuperare i valori dell’origine dati XML utilizzando `org.w3c.dom` classi.

**Consulta anche**

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API di Forms Service](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Trasmissione di documenti al servizio Forms](/help/forms/developing/passing-documents-forms-service.md)

[Creazione di applicazioni Web per il rendering di Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

## Gestire i moduli inviati tramite l’API Java {#handle-submitted-forms-using-the-java-api}

Gestire un modulo inviato utilizzando l’API Forms (Java):

1. Includi file di progetto

   Includi file JAR client, come adobe-forms-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto API client Forms

   * Crea un `ServiceClientFactory` oggetto contenente le proprietà di connessione.
   * Crea un `FormsServiceClient` utilizzando il relativo costruttore e passando `ServiceClientFactory` oggetto.

1. Recupera dati modulo

   * Per recuperare i dati del modulo inviati a un servlet Java, crea un `com.adobe.idp.Document` utilizzando il relativo costruttore e richiamando il `javax.servlet.http.HttpServletResponse` dell’oggetto `getInputStream` dall&#39;interno del costruttore.
   * Crea un `RenderOptionsSpec` utilizzando il relativo costruttore. Imposta il valore delle impostazioni internazionali richiamando il `RenderOptionsSpec` dell’oggetto `setLocale` e passare un valore stringa che specifica il valore delle impostazioni internazionali.

   >[!NOTE]
   >
   >È possibile istruire il servizio Forms per creare dati XDP o XML dal contenuto PDF inviato richiamando il `RenderOptionsSpec` dell’oggetto `setPDF2XDP` metodo e passaggio `true` e anche chiamando `setXMLData` e di passaggio `true`. Puoi quindi richiamare la `FormsResult` dell’oggetto `getOutputXML` per recuperare i dati XML corrispondenti ai dati XDP/XML. (2) `FormsResult` viene restituito dall&#39;oggetto `processFormSubmission` , illustrato nel passaggio successivo.)

   * Richiama il `FormsServiceClient` dell’oggetto `processFormSubmission` e passare i seguenti valori:

      * La `com.adobe.idp.Document` oggetto contenente i dati del modulo.
      * Valore stringa che specifica le variabili di ambiente, comprese tutte le intestazioni HTTP rilevanti. Specifica il tipo di contenuto da gestire. Per gestire i dati XML, specificare il seguente valore di stringa per questo parametro: `CONTENT_TYPE=text/xml`. Per gestire i dati di PDF, specificare il seguente valore stringa per questo parametro: `CONTENT_TYPE=application/pdf`.
      * Un valore stringa che specifica la variabile `HTTP_USER_AGENT` valore di intestazione, ad esempio . `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`. Questo valore del parametro è facoltativo.
      * A `RenderOptionsSpec` oggetto che memorizza le opzioni di esecuzione.

      La `processFormSubmission` restituisce un `FormsResult` oggetto contenente i risultati dell&#39;invio del modulo.

   * Determinare se il servizio Forms ha completato l’elaborazione dei dati del modulo richiamando il `FormsResult` dell’oggetto `getAction` metodo . Se questo metodo restituisce il valore `0`, i dati sono pronti per essere elaborati.



1. Determinare se l’invio del modulo contiene allegati di file

   * Richiama il `FormsResult` dell’oggetto `getAttachments` metodo . Questo metodo restituisce un `java.util.List` oggetto contenente file inviati con il modulo.
   * Itera attraverso il `java.util.List` oggetto per determinare se sono presenti allegati di file. Se sono presenti allegati di file, ogni elemento è un `com.adobe.idp.Document` istanza. È possibile salvare gli allegati del file richiamando il `com.adobe.idp.Document` dell’oggetto `copyToFile` e passare un `java.io.File` oggetto.

   >[!NOTE]
   >
   >Questo passaggio è applicabile solo se il modulo viene inviato come PDF.

1. Elaborazione dei dati inviati

   * Se il tipo di contenuto dati è `application/vnd.adobe.xdp+xml` o `text/xml`, crea una logica di applicazione per recuperare i valori dei dati XML.

      * Crea un `com.adobe.idp.Document` richiamando l&#39;oggetto `FormsResult` dell’oggetto `getOutputContent` metodo .
      * Crea un `java.io.InputStream` richiamando l&#39;oggetto `java.io.DataInputStream` costruttore e passaggio `com.adobe.idp.Document` oggetto.
      * Crea un `org.w3c.dom.DocumentBuilderFactory` chiamando l&#39;oggetto statico `org.w3c.dom.DocumentBuilderFactory` dell’oggetto `newInstance` metodo .
      * Crea un `org.w3c.dom.DocumentBuilder` richiamando l&#39;oggetto `org.w3c.dom.DocumentBuilderFactory` dell’oggetto `newDocumentBuilder` metodo .
      * Crea un `org.w3c.dom.Document` richiamando l&#39;oggetto `org.w3c.dom.DocumentBuilder` dell’oggetto `parse` e passare `java.io.InputStream` oggetto.
      * Recupera il valore di ogni nodo all&#39;interno del documento XML. Un modo per eseguire questa attività consiste nel creare un metodo personalizzato che accetta due parametri: la `org.w3c.dom.Document` e il nome del nodo di cui si desidera recuperare il valore. Questo metodo restituisce un valore stringa che rappresenta il valore del nodo. Nell&#39;esempio di codice che segue questo processo, questo metodo personalizzato viene chiamato `getNodeText`. Viene mostrato il corpo di questo metodo.
   * Se il tipo di contenuto dati è `application/pdf`, crea una logica di applicazione per salvare i dati PDF inviati come file PDF.

      * Crea un `com.adobe.idp.Document` richiamando l&#39;oggetto `FormsResult` dell’oggetto `getOutputContent` metodo .
      * Crea un `java.io.File` utilizzando il relativo costruttore pubblico. Assicurati di specificare PDF come estensione del nome file.
      * Compilare il file PDF richiamando il `com.adobe.idp.Document` dell’oggetto `copyToFile` e passare `java.io.File` oggetto.


**Consulta anche**

[Avvio rapido (modalità SOAP): Gestione dei PDF forms inviati come XML tramite l’API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-handling-pdf-forms-submitted-as-xml-using-the-java-api)

[Avvio rapido (modalità SOAP): Gestione dei moduli HTML inviati come XML tramite l’API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-handling-html-forms-submitted-as-xml-using-the-java-api)

[Avvio rapido (modalità SOAP): Gestione dei PDF forms inviati come PDF tramite l’API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-handling-pdf-forms-submitted-as-pdf-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Gestire i dati PDF inviati utilizzando l’API del servizio Web {#handle-submitted-pdf-data-using-the-web-service-api}

Gestire un modulo inviato utilizzando l’API Forms (servizio Web):

1. Includi file di progetto

   * Creare classi proxy Java che utilizzano il servizio WSDL di Forms.
   * Includi le classi proxy Java nel percorso della classe.

1. Creare un oggetto API client Forms

   Crea un `FormsService` e impostare i valori di autenticazione.

1. Recupera dati modulo

   * Per recuperare i dati del modulo inviati a un servlet Java, crea un `BLOB` utilizzando il relativo costruttore.
   * Crea un `java.io.InputStream` richiamando l&#39;oggetto `javax.servlet.http.HttpServletResponse` dell’oggetto `getInputStream` metodo .
   * Crea un `java.io.ByteArrayOutputStream` utilizzando il relativo costruttore e passando la lunghezza del `java.io.InputStream` oggetto.
   * Copia il contenuto del `java.io.InputStream` nell&#39;oggetto `java.io.ByteArrayOutputStream` oggetto.
   * Crea un array di byte richiamando il `java.io.ByteArrayOutputStream` dell’oggetto `toByteArray` metodo .
   * Popolare `BLOB` richiamandone l&#39;oggetto `setBinaryData` e passare l&#39;array di byte come argomento.
   * Crea un `RenderOptionsSpec` utilizzando il relativo costruttore. Imposta il valore delle impostazioni internazionali richiamando il `RenderOptionsSpec` dell’oggetto `setLocale` e passare un valore stringa che specifica il valore delle impostazioni internazionali.
   * Richiama il `FormsService` dell’oggetto `processFormSubmission` e passare i seguenti valori:

      * La `BLOB` oggetto contenente i dati del modulo.
      * Valore stringa che specifica le variabili di ambiente, comprese tutte le intestazioni HTTP rilevanti. Specifica il tipo di contenuto da gestire. Per gestire i dati XML, specificare il seguente valore di stringa per questo parametro: `CONTENT_TYPE=text/xml`. Per gestire i dati di PDF, specificare il seguente valore stringa per questo parametro: `CONTENT_TYPE=application/pdf`.
      * Un valore stringa che specifica la variabile `HTTP_USER_AGENT` valore di intestazione; ad esempio, `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
      * A `RenderOptionsSpec` oggetto che memorizza le opzioni di esecuzione.
      * Un vuoto `BLOBHolder` oggetto popolato dal metodo .
      * Un vuoto `javax.xml.rpc.holders.StringHolder` oggetto popolato dal metodo .
      * Un vuoto `BLOBHolder` oggetto popolato dal metodo .
      * Un vuoto `BLOBHolder` oggetto popolato dal metodo .
      * Un vuoto `javax.xml.rpc.holders.ShortHolder` oggetto popolato dal metodo .
      * Un vuoto `MyArrayOf_xsd_anyTypeHolder` oggetto popolato dal metodo . Questo parametro viene utilizzato per memorizzare gli allegati dei file inviati insieme al modulo.
      * Un vuoto `FormsResultHolder` oggetto compilato dal metodo con il modulo inviato.

      La `processFormSubmission` popola il `FormsResultHolder` con i risultati dell’invio del modulo.

   * Determinare se il servizio Forms ha completato l’elaborazione dei dati del modulo richiamando il `FormsResult` dell’oggetto `getAction` metodo . Se questo metodo restituisce il valore `0`, i dati del modulo sono pronti per essere elaborati. Puoi ottenere un `FormsResult` ottenendo il valore del `FormsResultHolder` dell’oggetto `value` membro dati.


1. Determinare se l’invio del modulo contiene allegati di file

   Ottieni il valore del `MyArrayOf_xsd_anyTypeHolder` dell’oggetto `value` membro (il `MyArrayOf_xsd_anyTypeHolder` è stato passato all&#39;oggetto `processFormSubmission` metodo). Questo membro dati restituisce una matrice di `Objects`. Ogni elemento all’interno del `Object` un array `Object`corrisponde ai file inviati insieme al modulo. È possibile ottenere ogni elemento all’interno dell’array e inviarlo a un `BLOB` oggetto.

1. Elaborazione dei dati inviati

   * Se il tipo di contenuto dati è `application/vnd.adobe.xdp+xml` o `text/xml`, crea una logica di applicazione per recuperare i valori dei dati XML.

      * Crea un `BLOB` richiamando l&#39;oggetto `FormsResult` dell’oggetto `getOutputContent` metodo .
      * Crea un array di byte richiamando il `BLOB` dell’oggetto `getBinaryData` metodo .
      * Crea un `java.io.InputStream` richiamando l&#39;oggetto `java.io.ByteArrayInputStream` e passare la matrice dei byte.
      * Crea un `org.w3c.dom.DocumentBuilderFactory` chiamando l&#39;oggetto statico `org.w3c.dom.DocumentBuilderFactory` dell’oggetto `newInstance` metodo .
      * Crea un `org.w3c.dom.DocumentBuilder` richiamando l&#39;oggetto `org.w3c.dom.DocumentBuilderFactory` dell’oggetto `newDocumentBuilder` metodo .
      * Crea un `org.w3c.dom.Document` richiamando l&#39;oggetto `org.w3c.dom.DocumentBuilder` dell’oggetto `parse` e passare `java.io.InputStream` oggetto.
      * Recupera il valore di ogni nodo all&#39;interno del documento XML. Un modo per eseguire questa attività consiste nel creare un metodo personalizzato che accetta due parametri: la `org.w3c.dom.Document` e il nome del nodo di cui si desidera recuperare il valore. Questo metodo restituisce un valore stringa che rappresenta il valore del nodo. Nell&#39;esempio di codice che segue questo processo, questo metodo personalizzato viene chiamato `getNodeText`. Viene mostrato il corpo di questo metodo.
   * Se il tipo di contenuto dati è `application/pdf`, crea una logica di applicazione per salvare i dati PDF inviati come file PDF.

      * Crea un `BLOB` richiamando l&#39;oggetto `FormsResult` dell’oggetto `getOutputContent` metodo .
      * Crea un array di byte richiamando il `BLOB` dell’oggetto `getBinaryData` metodo .
      * Crea un `java.io.File` utilizzando il relativo costruttore pubblico. Assicurati di specificare PDF come estensione del nome file.
      * Crea un `java.io.FileOutputStream` utilizzando il relativo costruttore e passando `java.io.File` oggetto.
      * Compilare il file PDF richiamando il `java.io.FileOutputStream` dell’oggetto `write` e passare l&#39;array di byte.


**Consulta anche**

[Richiamo di AEM Forms con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
