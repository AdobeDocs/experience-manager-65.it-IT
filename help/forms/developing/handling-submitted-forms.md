---
title: Gestione di Forms inviato
seo-title: Gestione di Forms inviato
description: Utilizzare il servizio Forms per recuperare i dati inviati immessi in un modulo interattivo. L'utente può inviare i dati del modulo in formato XML, PDF e URL UTF-16.
seo-description: Utilizzare il servizio Forms per recuperare i dati inviati immessi in un modulo interattivo. L'utente può inviare i dati del modulo in formato XML, PDF e URL UTF-16.
uuid: 673b28f1-f023-4da8-a6a0-c5ff921c5f5d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 3d838027-6bde-4a71-a428-4d5102f7d799
translation-type: tm+mt
source-git-commit: 07889ead2ae402b5fb738ca08c7efe076ef33e44
workflow-type: tm+mt
source-wordcount: '2921'
ht-degree: 0%

---


# Gestione Forms inviata {#handling-submitted-forms}

Per le applicazioni basate sul Web che consentono a un utente di compilare moduli interattivi è necessario che i dati vengano inviati nuovamente al server. Il servizio Forms consente di recuperare i dati immessi dall&#39;utente in un modulo interattivo. Dopo aver recuperato i dati, puoi elaborarli per soddisfare i requisiti aziendali. Ad esempio, è possibile memorizzare i dati in un database, inviare i dati a un&#39;altra applicazione, inviare i dati a un altro servizio, unire i dati in una struttura del modulo, visualizzare i dati in un browser Web e così via.

I dati del modulo vengono inviati al servizio Forms come dati XML o PDF, opzione impostata in Designer. Un modulo inviato come XML consente di estrarre valori di dati di singoli campi. In altre parole, è possibile estrarre il valore di ciascun campo modulo immesso dall&#39;utente. Un modulo inviato come dati PDF è costituito da dati binari, non da dati XML. È possibile salvare il modulo come file PDF o inviarlo a un altro servizio. Per estrarre i dati da un modulo inviato come XML e quindi utilizzare i dati del modulo per creare un documento PDF, eseguire un&#39;altra operazione  AEM Forms. (Vedere [Creazione di documenti PDF con dati XML inviati](/help/forms/developing/creating-pdf-documents-submitted-xml.md))

Il diagramma seguente mostra i dati inviati a un Servlet Java denominato `HandleData` da un modulo interattivo visualizzato in un browser Web.

![hs_handlesubmit](assets/hs_hs_handlesubmit.png)

La tabella seguente illustra i passaggi del diagramma.

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
   <td><p>I dati vengono inviati a <code>HandleData</code> Java Servlet come dati XML.</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>Il servlet <code>HandleData</code> Java contiene la logica dell'applicazione per recuperare i dati.</p></td>
  </tr>
 </tbody>
</table>

## Gestione dei dati XML inviati {#handling-submitted-xml-data}

Quando i dati del modulo vengono inviati come XML, è possibile recuperare dati XML che rappresentano i dati inviati. Tutti i campi modulo vengono visualizzati come nodi in uno schema XML. I valori dei nodi corrispondono ai valori compilati dall&#39;utente. Si consideri un modulo di prestito in cui ogni campo del modulo viene visualizzato come un nodo all&#39;interno dei dati XML. Il valore di ciascun nodo corrisponde al valore che l&#39;utente compila. Si supponga che un utente riempia il modulo di prestito con i dati mostrati nel seguente modulo.

![hs_loanformdata](assets/hs_hs_loanformdata.png)

L&#39;illustrazione seguente mostra i dati XML corrispondenti recuperati utilizzando l&#39;API client del servizio Forms.

![hs_hs_loandata](assets/hs_hs_loandata.png)

I campi nel modulo di prestito. Questi valori possono essere recuperati
utilizzo di classi Java XML.

>[!NOTE]
>
>La struttura del modulo deve essere configurata correttamente in Designer per l&#39;invio dei dati come dati XML. Per configurare correttamente la struttura del modulo per l&#39;invio di dati XML, assicurarsi che il pulsante Invia, situato nella struttura del modulo, sia impostato per l&#39;invio di dati XML. Per informazioni sull&#39;impostazione del pulsante Invia per l&#39;invio di dati XML, vedere [ AEM Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63).

## Gestione dei dati PDF inviati {#handling-submitted-pdf-data}

Considerate un&#39;applicazione Web che richiama il servizio Forms. Dopo che il servizio Forms ha eseguito il rendering di un modulo PDF interattivo in un browser Web client, l&#39;utente compila il modulo e lo invia nuovamente come dati PDF. Quando il servizio Forms riceve i dati PDF, può inviare i dati PDF a un altro servizio o salvarli come file PDF. Il diagramma seguente mostra il flusso logico dell&#39;applicazione.

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
   <td><p>Una pagina Web contiene un collegamento che accede a un Servlet Java che richiama il servizio Forms.</p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>Il servizio Forms esegue il rendering di un modulo PDF interattivo nel browser Web del client.</p></td>
  </tr>
  <tr>
   <td><p>1</p></td>
   <td><p>L'utente compila un modulo interattivo e fa clic su un pulsante di invio. Il modulo viene inviato nuovamente al servizio Forms come dati PDF. Questa opzione è impostata in Designer.</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>Il servizio Forms salva i dati PDF come file PDF. </p></td>
  </tr>
 </tbody>
</table>

## Gestione dei dati URL UTF-16 inviati {#handling-submitted-url-utf-16-data}

Se i dati del modulo vengono inviati come dati URL UTF-16, il computer client richiede  Adobe Reader o  Acrobat 8.1 o versione successiva. Inoltre, se la struttura del modulo contiene un pulsante di invio con dati URL codificati (HTTP Post) e l&#39;opzione di codifica dei dati è UTF-16, la struttura del modulo deve essere modificata in un editor di testo come Blocco note. È possibile impostare l&#39;opzione di codifica su `UTF-16LE` o `UTF-16BE` per il pulsante di invio. Designer non fornisce questa funzionalità.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Forms, vedere [Guida di riferimento dei servizi per  AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Riepilogo dei passaggi {#summary-of-steps}

Per gestire i moduli inviati, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un oggetto Forms Client API.
1. Recuperare i dati del modulo.
1. Determinare se l&#39;invio del modulo contiene file allegati.
1. Elabora i dati inviati.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, accertatevi di includere i file proxy.

**Creare un oggetto Forms Client API**

Prima di eseguire un&#39;operazione API client di Forms Service a livello di programmazione, è necessario creare un client di servizi Forms. Se utilizzate l&#39;API Java, create un oggetto `FormsServiceClient`. Se utilizzate l&#39;API del servizio Web di Forms, create un oggetto `FormsService`.

**Recupero dei dati del modulo**

Per recuperare i dati del modulo inviati, è necessario richiamare il metodo `FormsServiceClient` dell&#39;oggetto `processFormSubmission`. Quando si richiama questo metodo, è necessario specificare il tipo di contenuto del modulo inviato. Quando i dati vengono inviati da un browser Web client al servizio Forms, possono essere inviati come dati XML o PDF. Per recuperare i dati immessi nei campi del modulo, i dati possono essere inviati come dati XML.

È inoltre possibile recuperare i campi modulo da un modulo inviato come dati PDF impostando le seguenti opzioni di esecuzione:

* Passate il seguente valore al metodo `processFormSubmission` come parametro del tipo di contenuto: `CONTENT_TYPE=application/pdf`.
* Impostare il valore `RenderOptionsSpec` dell&#39;oggetto `PDFToXDP` su `true`
* Impostare il valore `RenderOptionsSpec` dell&#39;oggetto `ExportDataFormat` su `XMLData`

È possibile specificare il tipo di contenuto del modulo inviato quando si richiama il metodo `processFormSubmission`. L&#39;elenco seguente specifica i valori di tipo di contenuto applicabili:

* **text/xml**: Rappresenta il tipo di contenuto da utilizzare quando un modulo PDF invia dati del modulo come XML.
* **application/x-www-form-urlencoded**: Rappresenta il tipo di contenuto da utilizzare quando un modulo HTML invia dati come XML.
* **application/pdf**: Rappresenta il tipo di contenuto da utilizzare quando un modulo PDF invia dati come PDF.

>[!NOTE]
>
>Alla sezione Gestione dell’Forms inviato verranno associati tre avvii rapidi corrispondenti. I PDF forms di gestione inviati come PDF tramite l&#39;introduzione rapida API Java dimostrano come gestire i dati PDF inviati. Il tipo di contenuto specificato in questo avvio rapido è `application/pdf`. Il rapido avvio della gestione dei PDF forms inviati come XML tramite l&#39;API Java illustra come gestire i dati XML inviati da un modulo PDF. Il tipo di contenuto specificato in questo avvio rapido è `text/xml`. Analogamente, il rapido avvio della gestione dei moduli HTML inviati come XML tramite l&#39;API Java illustra come gestire i dati XML inviati da un modulo HTML. Il tipo di contenuto specificato in questo avvio rapido è application/x-www-form-urlencoded.

È possibile recuperare i dati del modulo inviati al servizio Forms e determinarne lo stato di elaborazione. In altre parole, quando i dati vengono inviati al servizio Forms, non significa necessariamente che il servizio Forms abbia terminato l&#39;elaborazione dei dati e che i dati siano pronti per essere elaborati. Ad esempio, i dati possono essere inviati al servizio Forms in modo da poter eseguire un calcolo. Una volta completato il calcolo, all&#39;utente viene eseguito il rendering del modulo con i risultati del calcolo visualizzati. Prima di elaborare i dati inviati, si consiglia di determinare se il servizio Forms ha completato l&#39;elaborazione dei dati.

Il servizio Forms restituisce i seguenti valori per indicare se l&#39;elaborazione dei dati è terminata:

* **0 (Invia): i dati** inviati sono pronti per essere elaborati.
* **1 (Calculate):** Il servizio Forms ha eseguito un&#39;operazione di calcolo sui dati e i risultati devono essere restituiti all&#39;utente.
* **2 (Convalida):** i dati del modulo convalidati dal servizio Forms e i risultati devono essere restituiti all&#39;utente.
* **3 (Avanti):** La pagina corrente è cambiata con i risultati che devono essere scritti nell&#39;applicazione client.
* **4 (precedente**): La pagina corrente è cambiata con risultati che devono essere scritti nell&#39;applicazione client.

>[!NOTE]
>
>I calcoli e le convalide devono essere sottoposti a nuovo rendering per l&#39;utente. (Vedere [Calcolo dei dati del modulo](/help/forms/developing/calculating-form-data.md#calculating-form-data).

**Determinare se l&#39;invio del modulo contiene file allegati**

Forms inviato al servizio Forms può contenere file allegati. Ad esempio, utilizzando  riquadro allegato integrato di Acrobat, l&#39;utente può selezionare i file allegati da inviare insieme al modulo. Inoltre, un utente può selezionare gli allegati dei file utilizzando una barra degli strumenti HTML di cui viene eseguito il rendering con un file HTML.

Dopo aver determinato se un modulo contiene allegati, è possibile elaborare i dati. Ad esempio, è possibile salvare l&#39;allegato al file system locale.

>[!NOTE]
>
>Il modulo deve essere inviato come dati PDF per recuperare gli allegati del file. Se il modulo viene inviato come dati XML, gli allegati non vengono inviati.

**Elaborazione dei dati inviati**

A seconda del tipo di contenuto dei dati inviati, è possibile estrarre singoli valori dei campi modulo dai dati XML inviati o salvare i dati PDF inviati come file PDF (o inviarli a un altro servizio). Per estrarre singoli campi del modulo, convertire i dati XML inviati in un&#39;origine dati XML e quindi recuperare i valori dell&#39;origine dati XML utilizzando le classi `org.w3c.dom`.

**Consulta anche**

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido di Forms Service API](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Invio di documenti al servizio Forms](/help/forms/developing/passing-documents-forms-service.md)

[Creazione di applicazioni Web per il rendering di Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

## Gestire i moduli inviati utilizzando l&#39;API Java {#handle-submitted-forms-using-the-java-api}

Gestire un modulo inviato utilizzando l&#39;API Forms (Java):

1. Includi file di progetto

   Includete file JAR client, ad esempio adobe-forms-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto Forms Client API

   * Creare un oggetto `ServiceClientFactory` che contiene le proprietà di connessione.
   * Creare un oggetto `FormsServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Recupero dei dati del modulo

   * Per recuperare i dati del modulo inviati a un Servlet Java, creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e richiamando il metodo `javax.servlet.http.HttpServletResponse` dell&#39;oggetto `getInputStream` dall&#39;interno del costruttore.
   * Creare un oggetto `RenderOptionsSpec` utilizzando il relativo costruttore. Impostare il valore delle impostazioni internazionali richiamando il metodo `setLocale` dell&#39;oggetto `RenderOptionsSpec` e passando un valore di stringa che specifica il valore delle impostazioni internazionali.

   >[!NOTE]
   >
   >È possibile indicare al servizio Forms di creare dati XDP o XML dal contenuto PDF inviato richiamando il metodo `RenderOptionsSpec` dell&#39;oggetto &lt;a1/> e passando `setPDF2XDP`, nonché chiamando `true` e passando `setXMLData`. `true` È quindi possibile richiamare il metodo `FormsResult` dell&#39;oggetto `getOutputXML` per recuperare i dati XML che corrispondono ai dati XDP/XML. (L&#39;oggetto `FormsResult` viene restituito dal metodo `processFormSubmission`, illustrato nel passaggio secondario successivo.)

   * Richiamare il metodo `FormsServiceClient` dell&#39;oggetto `processFormSubmission` e trasmettere i seguenti valori:

      * L&#39;oggetto `com.adobe.idp.Document` che contiene i dati del modulo.
      * Valore stringa che specifica le variabili di ambiente, comprese tutte le intestazioni HTTP rilevanti. Specificate il tipo di contenuto da gestire. Per gestire i dati XML, specificate il seguente valore di stringa per questo parametro: `CONTENT_TYPE=text/xml`. Per gestire i dati PDF, specificare il seguente valore di stringa per questo parametro: `CONTENT_TYPE=application/pdf`.
      * Un valore di stringa che specifica il valore di intestazione `HTTP_USER_AGENT`, ad esempio, . `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`. Questo valore del parametro è facoltativo.
      * Un oggetto `RenderOptionsSpec` che memorizza le opzioni di esecuzione.

      Il metodo `processFormSubmission` restituisce un oggetto `FormsResult` contenente i risultati dell&#39;invio del modulo.

   * Determinare se il servizio Forms ha completato l&#39;elaborazione dei dati del modulo richiamando il metodo `FormsResult` dell&#39;oggetto `getAction`. Se questo metodo restituisce il valore `0`, i dati sono pronti per essere elaborati.



1. Determinare se l&#39;invio del modulo contiene file allegati

   * Richiamare il metodo `FormsResult` dell&#39;oggetto `getAttachments`. Questo metodo restituisce un oggetto `java.util.List` che contiene i file inviati con il modulo.
   * Iterate l&#39;oggetto `java.util.List` per determinare se sono presenti allegati di file. Se sono presenti allegati, ogni elemento è un&#39;istanza `com.adobe.idp.Document`. È possibile salvare gli allegati richiamando il metodo `com.adobe.idp.Document` dell&#39;oggetto `copyToFile` e passando un oggetto &lt;a2/>.`java.io.File`

   >[!NOTE]
   >
   >Questo passaggio è applicabile solo se il modulo viene inviato come PDF.

1. Elaborazione dei dati inviati

   * Se il tipo di contenuto dei dati è `application/vnd.adobe.xdp+xml` o `text/xml`, creare la logica dell&#39;applicazione per recuperare i valori dei dati XML.

      * Creare un oggetto `com.adobe.idp.Document` richiamando il metodo `FormsResult` dell&#39;oggetto `getOutputContent`.
      * Creare un oggetto `java.io.InputStream` richiamando il costruttore `java.io.DataInputStream` e passando l&#39;oggetto `com.adobe.idp.Document`.
      * Creare un oggetto `org.w3c.dom.DocumentBuilderFactory` chiamando il metodo `org.w3c.dom.DocumentBuilderFactory` statico dell&#39;oggetto `newInstance`.
      * Creare un oggetto `org.w3c.dom.DocumentBuilder` richiamando il metodo `org.w3c.dom.DocumentBuilderFactory` dell&#39;oggetto `newDocumentBuilder`.
      * Creare un oggetto `org.w3c.dom.Document` richiamando il metodo `org.w3c.dom.DocumentBuilder` dell&#39;oggetto `parse` e passando l&#39;oggetto `java.io.InputStream`.
      * Recuperare il valore di ciascun nodo all&#39;interno del documento XML. Un modo per eseguire questa attività è creare un metodo personalizzato che accetta due parametri: l&#39;oggetto `org.w3c.dom.Document` e il nome del nodo di cui si desidera recuperare il valore. Questo metodo restituisce una stringa che rappresenta il valore del nodo. Nell&#39;esempio di codice che segue questo processo, questo metodo personalizzato è denominato `getNodeText`. Viene visualizzato il corpo di questo metodo.
   * Se il tipo di contenuto dei dati è `application/pdf`, creare la logica dell&#39;applicazione per salvare i dati PDF inviati come file PDF.

      * Creare un oggetto `com.adobe.idp.Document` richiamando il metodo `FormsResult` dell&#39;oggetto `getOutputContent`.
      * Creare un oggetto `java.io.File` utilizzando il relativo costruttore pubblico. Accertatevi di specificare PDF come estensione del nome file.
      * Compilare il file PDF richiamando il metodo `com.adobe.idp.Document` dell&#39;oggetto `copyToFile` e passando l&#39;oggetto &lt;a2/>.`java.io.File`


**Consulta anche**

[Avvio rapido (modalità SOAP): Gestione dei PDF forms inviati come XML tramite l&#39;API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-handling-pdf-forms-submitted-as-xml-using-the-java-api)

[Avvio rapido (modalità SOAP): Gestione dei moduli HTML inviati come XML mediante l&#39;API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-handling-html-forms-submitted-as-xml-using-the-java-api)

[Avvio rapido (modalità SOAP): Gestione dei PDF forms inviati come PDF tramite l&#39;API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-handling-pdf-forms-submitted-as-pdf-using-the-java-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Gestire i dati PDF inviati utilizzando l&#39;API del servizio Web {#handle-submitted-pdf-data-using-the-web-service-api}

Gestire un modulo inviato utilizzando l&#39;API Forms (servizio Web):

1. Includi file di progetto

   * Creare classi proxy Java che utilizzano il servizio WSDL di Forms.
   * Includete le classi proxy Java nel percorso della classe.

1. Creare un oggetto Forms Client API

   Creare un oggetto `FormsService` e impostare i valori di autenticazione.

1. Recupero dei dati del modulo

   * Per recuperare i dati del modulo inviati a un Servlet Java, creare un oggetto `BLOB` utilizzando il relativo costruttore.
   * Creare un oggetto `java.io.InputStream` richiamando il metodo `javax.servlet.http.HttpServletResponse` dell&#39;oggetto `getInputStream`.
   * Creare un oggetto `java.io.ByteArrayOutputStream` utilizzando il relativo costruttore e passando la lunghezza dell&#39;oggetto `java.io.InputStream`.
   * Copiare il contenuto dell&#39;oggetto `java.io.InputStream` nell&#39;oggetto `java.io.ByteArrayOutputStream`.
   * Creare un array di byte richiamando il metodo `java.io.ByteArrayOutputStream` dell&#39;oggetto `toByteArray`.
   * Compilare l&#39;oggetto `BLOB` richiamandone il metodo `setBinaryData` e passando l&#39;array di byte come argomento.
   * Creare un oggetto `RenderOptionsSpec` utilizzando il relativo costruttore. Impostare il valore delle impostazioni internazionali richiamando il metodo `setLocale` dell&#39;oggetto `RenderOptionsSpec` e passando un valore di stringa che specifica il valore delle impostazioni internazionali.
   * Richiamare il metodo `FormsService` dell&#39;oggetto `processFormSubmission` e trasmettere i seguenti valori:

      * L&#39;oggetto `BLOB` che contiene i dati del modulo.
      * Valore stringa che specifica le variabili di ambiente, comprese tutte le intestazioni HTTP rilevanti. Specificate il tipo di contenuto da gestire. Per gestire i dati XML, specificate il seguente valore di stringa per questo parametro: `CONTENT_TYPE=text/xml`. Per gestire i dati PDF, specificare il seguente valore di stringa per questo parametro: `CONTENT_TYPE=application/pdf`.
      * Un valore di stringa che specifica il valore di intestazione `HTTP_USER_AGENT`; ad esempio, `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
      * Un oggetto `RenderOptionsSpec` che memorizza le opzioni di esecuzione.
      * Un oggetto `BLOBHolder` vuoto compilato dal metodo.
      * Un oggetto `javax.xml.rpc.holders.StringHolder` vuoto compilato dal metodo.
      * Un oggetto `BLOBHolder` vuoto compilato dal metodo.
      * Un oggetto `BLOBHolder` vuoto compilato dal metodo.
      * Un oggetto `javax.xml.rpc.holders.ShortHolder` vuoto compilato dal metodo.
      * Un oggetto `MyArrayOf_xsd_anyTypeHolder` vuoto compilato dal metodo. Questo parametro viene utilizzato per memorizzare gli allegati inviati insieme al modulo.
      * Un oggetto `FormsResultHolder` vuoto compilato dal metodo con il modulo inviato.

      Il metodo `processFormSubmission` popola il parametro `FormsResultHolder` con i risultati dell&#39;invio del modulo.

   * Determinare se il servizio Forms ha completato l&#39;elaborazione dei dati del modulo richiamando il metodo `FormsResult` dell&#39;oggetto `getAction`. Se questo metodo restituisce il valore `0`, i dati del modulo sono pronti per essere elaborati. È possibile ottenere un oggetto `FormsResult` ottenendo il valore del membro di dati `FormsResultHolder` dell&#39;oggetto `value`.


1. Determinare se l&#39;invio del modulo contiene file allegati

   Ottenere il valore del membro di dati `MyArrayOf_xsd_anyTypeHolder` dell&#39;oggetto `value` (l&#39;oggetto `MyArrayOf_xsd_anyTypeHolder` è stato passato al metodo `processFormSubmission`). Questo membro di dati restituisce un array di `Objects`. Ogni elemento all&#39;interno dell&#39;array `Object` è un elemento `Object`che corrisponde ai file inviati insieme al modulo. È possibile ottenere ogni elemento all&#39;interno dell&#39;array e inviarlo a un oggetto `BLOB`.

1. Elaborazione dei dati inviati

   * Se il tipo di contenuto dei dati è `application/vnd.adobe.xdp+xml` o `text/xml`, creare la logica dell&#39;applicazione per recuperare i valori dei dati XML.

      * Creare un oggetto `BLOB` richiamando il metodo `FormsResult` dell&#39;oggetto `getOutputContent`.
      * Creare un array di byte richiamando il metodo `BLOB` dell&#39;oggetto `getBinaryData`.
      * Creare un oggetto `java.io.InputStream` richiamando il costruttore `java.io.ByteArrayInputStream` e passando l&#39;array di byte.
      * Creare un oggetto `org.w3c.dom.DocumentBuilderFactory` chiamando il metodo `org.w3c.dom.DocumentBuilderFactory` statico dell&#39;oggetto `newInstance`.
      * Creare un oggetto `org.w3c.dom.DocumentBuilder` richiamando il metodo `org.w3c.dom.DocumentBuilderFactory` dell&#39;oggetto `newDocumentBuilder`.
      * Creare un oggetto `org.w3c.dom.Document` richiamando il metodo `org.w3c.dom.DocumentBuilder` dell&#39;oggetto `parse` e passando l&#39;oggetto `java.io.InputStream`.
      * Recuperare il valore di ciascun nodo all&#39;interno del documento XML. Un modo per eseguire questa attività è creare un metodo personalizzato che accetta due parametri: l&#39;oggetto `org.w3c.dom.Document` e il nome del nodo di cui si desidera recuperare il valore. Questo metodo restituisce una stringa che rappresenta il valore del nodo. Nell&#39;esempio di codice che segue questo processo, questo metodo personalizzato è denominato `getNodeText`. Viene visualizzato il corpo di questo metodo.
   * Se il tipo di contenuto dei dati è `application/pdf`, creare la logica dell&#39;applicazione per salvare i dati PDF inviati come file PDF.

      * Creare un oggetto `BLOB` richiamando il metodo `FormsResult` dell&#39;oggetto `getOutputContent`.
      * Creare un array di byte richiamando il metodo `BLOB` dell&#39;oggetto `getBinaryData`.
      * Creare un oggetto `java.io.File` utilizzando il relativo costruttore pubblico. Accertatevi di specificare PDF come estensione del nome file.
      * Creare un oggetto `java.io.FileOutputStream` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.File`.
      * Compilare il file PDF richiamando il metodo `write` dell&#39;oggetto `java.io.FileOutputStream` e passando l&#39;array di byte.


**Consulta anche**

[Richiamo  AEM Forms con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)