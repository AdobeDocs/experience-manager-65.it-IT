---
title: Gestione dei moduli inviati
seo-title: Gestione dei moduli inviati
description: 'null'
seo-description: 'null'
uuid: 673b28f1-f023-4da8-a6a0-c5ff921c5f5d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 3d838027-6bde-4a71-a428-4d5102f7d799
translation-type: tm+mt
source-git-commit: 7cbe3e94eddb81925072f68388649befbb027e6d

---


# Gestione dei moduli inviati {#handling-submitted-forms}

Per le applicazioni basate sul Web che consentono a un utente di compilare moduli interattivi è necessario che i dati vengano inviati nuovamente al server. Il servizio Forms consente di recuperare i dati immessi dall&#39;utente in un modulo interattivo. Dopo aver recuperato i dati, puoi elaborarli per soddisfare i requisiti aziendali. Ad esempio, è possibile memorizzare i dati in un database, inviare i dati a un&#39;altra applicazione, inviare i dati a un altro servizio, unire i dati in una struttura del modulo, visualizzare i dati in un browser Web e così via.

I dati del modulo vengono inviati al servizio Forms come dati XML o PDF, opzione impostata in Designer. Un modulo inviato come XML consente di estrarre valori di dati di singoli campi. In altre parole, è possibile estrarre il valore di ciascun campo modulo immesso dall&#39;utente. Un modulo inviato come dati PDF è costituito da dati binari, non da dati XML. È possibile salvare il modulo come file PDF o inviarlo a un altro servizio. Se si desidera estrarre dati da un modulo inviato come XML e quindi utilizzare i dati del modulo per creare un documento PDF, è necessario richiamare un&#39;altra operazione AEM Forms. (Vedere [Creazione di documenti PDF con dati](/help/forms/developing/creating-pdf-documents-submitted-xml.md)XML inviati)

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

Nell&#39;illustrazione seguente sono visualizzati i dati XML corrispondenti recuperati utilizzando l&#39;API client del servizio Forms.

![hs_hs_loandata](assets/hs_hs_loandata.png)

I campi nel modulo di prestito. Questi valori possono essere recuperati utilizzando le classi Java XML.

>[!NOTE]
>
>La struttura del modulo deve essere configurata correttamente in Designer per l&#39;invio dei dati come dati XML. Per configurare correttamente la struttura del modulo per l&#39;invio di dati XML, assicurarsi che il pulsante Invia, situato nella struttura del modulo, sia impostato per l&#39;invio di dati XML. Per informazioni sull&#39;impostazione del pulsante Invia per l&#39;invio di dati XML, vedere [AEM Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63).

## Gestione dei dati PDF inviati {#handling-submitted-pdf-data}

Prendere in considerazione un&#39;applicazione Web che richiama il servizio Forms. Dopo che il servizio Forms ha eseguito il rendering di un modulo PDF interattivo in un browser Web client, l&#39;utente compila il modulo e lo invia nuovamente come dati PDF. Quando il servizio Forms riceve i dati PDF, può inviarli a un altro servizio o salvarli come file PDF. Il diagramma seguente mostra il flusso logico dell&#39;applicazione.

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
   <td><p>Una pagina Web contiene un collegamento che accede a un servlet Java che richiama il servizio Forms.</p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>Il servizio Forms esegue il rendering di un modulo PDF interattivo nel browser Web del client.</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>L'utente compila un modulo interattivo e fa clic su un pulsante di invio. Il modulo viene inviato nuovamente al servizio Forms come dati PDF. Questa opzione è impostata in Designer.</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>Il servizio Forms salva i dati PDF come file PDF. </p></td>
  </tr>
 </tbody>
</table>

## Gestione dei dati URL UTF-16 inviati {#handling-submitted-url-utf-16-data}

Se i dati del modulo vengono inviati come dati URL UTF-16, il computer client richiede Adobe Reader o Acrobat 8.1 o versione successiva. Inoltre, se la struttura del modulo contiene un pulsante di invio con dati URL codificati (HTTP Post) e l&#39;opzione di codifica dei dati è UTF-16, la struttura del modulo deve essere modificata in un editor di testo come Blocco note. È possibile impostare l&#39;opzione di codifica su `UTF-16LE` o `UTF-16BE` per il pulsante di invio. Designer non fornisce questa funzionalità.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Forms, consultate Riferimento [servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Riepilogo dei passaggi {#summary-of-steps}

Per gestire i moduli inviati, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un oggetto API client Forms.
1. Recuperare i dati del modulo.
1. Determinare se l&#39;invio del modulo contiene file allegati.
1. Elabora i dati inviati.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, accertatevi di includere i file proxy.

**Creare un oggetto API client Forms**

Prima di eseguire un&#39;operazione API client del servizio Forms a livello di programmazione, è necessario creare un client del servizio Forms. Se utilizzate l&#39;API Java, create un `FormsServiceClient` oggetto. Se si utilizza l&#39;API del servizio Web Forms, creare un `FormsService` oggetto.

**Recupero dei dati del modulo**

Per recuperare i dati del modulo inviati, è necessario richiamare il `FormsServiceClient` metodo `processFormSubmission` dell&#39;oggetto. Quando si richiama questo metodo, è necessario specificare il tipo di contenuto del modulo inviato. Quando i dati vengono inviati da un browser Web client al servizio Forms, possono essere inviati come dati XML o PDF. Per recuperare i dati immessi nei campi del modulo, i dati possono essere inviati come dati XML.

È inoltre possibile recuperare i campi modulo da un modulo inviato come dati PDF impostando le seguenti opzioni di esecuzione:

* Passate il seguente valore al `processFormSubmission` metodo come parametro del tipo di contenuto: `CONTENT_TYPE=application/pdf`.
* Impostare il valore dell&#39; `RenderOptionsSpec` oggetto `PDFToXDP` su `true`
* Impostare il valore dell&#39; `RenderOptionsSpec` oggetto `ExportDataFormat` su `XMLData`

È possibile specificare il tipo di contenuto del modulo inviato quando si richiama il `processFormSubmission` metodo. L&#39;elenco seguente specifica i valori di tipo di contenuto applicabili:

* **text/xml**: Rappresenta il tipo di contenuto da utilizzare quando un modulo PDF invia dati del modulo come XML.
* **application/x-www-form-urlencoded**: Rappresenta il tipo di contenuto da utilizzare quando un modulo HTML invia dati come XML.
* **application/pdf**: Rappresenta il tipo di contenuto da utilizzare quando un modulo PDF invia dati come PDF.

>[!NOTE]
>
>Nella sezione Gestione dei moduli inviati sono associati tre avvii rapidi corrispondenti. La gestione dei moduli PDF inviati come PDF tramite l&#39;introduzione rapida API Java illustra come gestire i dati PDF inviati. Il tipo di contenuto specificato in questo avvio rapido è `application/pdf`. La gestione dei moduli PDF inviati come XML tramite l&#39;avvio rapido dell&#39;API Java illustra come gestire i dati XML inviati da un modulo PDF. Il tipo di contenuto specificato in questo avvio rapido è `text/xml`. Analogamente, il rapido avvio della gestione dei moduli HTML inviati come XML tramite l&#39;API Java illustra come gestire i dati XML inviati da un modulo HTML. Il tipo di contenuto specificato in questo avvio rapido è application/x-www-form-urlencoded.

È possibile recuperare i dati del modulo inviati al servizio Forms e determinarne lo stato di elaborazione. In altre parole, quando i dati vengono inviati al servizio Forms, non significa necessariamente che il servizio Forms abbia terminato l&#39;elaborazione dei dati e che i dati siano pronti per essere elaborati. Ad esempio, è possibile inviare i dati al servizio Forms per eseguire un calcolo. Una volta completato il calcolo, all&#39;utente viene eseguito il rendering del modulo con i risultati del calcolo visualizzati. Prima di elaborare i dati inviati, si consiglia di determinare se il servizio Forms ha terminato l&#39;elaborazione dei dati.

Il servizio Forms restituisce i seguenti valori per indicare se ha completato l&#39;elaborazione dei dati:

* **** 0 (Invia): I dati inviati sono pronti per essere elaborati.
* **** 1 (Calcola): Il servizio Forms ha eseguito un&#39;operazione di calcolo sui dati e i risultati devono essere restituiti all&#39;utente.
* **** 2 (Convalida): I dati del modulo convalidati dal servizio Forms e i risultati devono essere restituiti all&#39;utente.
* **** 3 (successivo): La pagina corrente è cambiata con risultati che devono essere scritti nell&#39;applicazione client.
* **4 (precedente**): La pagina corrente è cambiata con risultati che devono essere scritti nell&#39;applicazione client.

>[!NOTE]
>
>I calcoli e le convalide devono essere sottoposti a nuovo rendering per l&#39;utente. (Vedere [Calcolo dei dati]del modulo(/help/forms/developing/rendering-forms-calculate-form-form-data-calculate-form-form-form-form-data-calculate-form.md#calculate-form-data)*.)*

**Determinare se l&#39;invio del modulo contiene allegati**

I moduli inviati al servizio Forms possono contenere file allegati. Ad esempio, utilizzando il riquadro allegato integrato di Acrobat, l&#39;utente può selezionare assieme al modulo i file allegati da inviare. Inoltre, un utente può selezionare gli allegati dei file utilizzando una barra degli strumenti HTML di cui viene eseguito il rendering con un file HTML.

Dopo aver determinato se un modulo contiene allegati, è possibile elaborare i dati. Ad esempio, è possibile salvare l&#39;allegato al file system locale.

>[!NOTE]
>
>Il modulo deve essere inviato come dati PDF per recuperare gli allegati del file. Se il modulo viene inviato come dati XML, gli allegati non vengono inviati.

**Elaborazione dei dati inviati**

A seconda del tipo di contenuto dei dati inviati, è possibile estrarre singoli valori dei campi modulo dai dati XML inviati o salvare i dati PDF inviati come file PDF (o inviarli a un altro servizio). Per estrarre singoli campi del modulo, convertire i dati XML inviati in un&#39;origine dati XML e quindi recuperare i valori dell&#39;origine dati XML utilizzando `org.w3c.dom` le classi.

**Consulta anche**

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido dell&#39;API di Forms Service](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Invio di documenti al servizio Forms](/help/forms/developing/passing-documents-forms-service.md)

[Creazione di applicazioni Web per il rendering di moduli](/help/forms/developing/creating-web-applications-renders-forms.md)

## Gestire i moduli inviati tramite l&#39;API Java {#handle-submitted-forms-using-the-java-api}

Gestire un modulo inviato utilizzando l&#39;API Forms (Java):

1. Includi file di progetto

   Includete file JAR client, ad esempio adobe-forms-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto API client Forms

   * Creare un `ServiceClientFactory` oggetto che contenga proprietà di connessione.
   * Creare un `FormsServiceClient` oggetto utilizzando il relativo costruttore e passando l&#39; `ServiceClientFactory` oggetto.

1. Recupero dei dati del modulo

   * Per recuperare i dati del modulo inviati a un Servlet Java, creare un `com.adobe.idp.Document` oggetto utilizzando il relativo costruttore e richiamando il `javax.servlet.http.HttpServletResponse` metodo dell&#39;oggetto `getInputStream` dall&#39;interno del costruttore.
   * Creare un `RenderOptionsSpec` oggetto utilizzando il relativo costruttore. Impostare il valore delle impostazioni internazionali richiamando il metodo dell&#39; `RenderOptionsSpec` oggetto `setLocale` e passando un valore di stringa che specifica il valore delle impostazioni internazionali.
   >[!NOTE]
   >
   >È possibile indicare al servizio Forms di creare dati XDP o XML dal contenuto PDF inviato richiamando il metodo dell&#39; `RenderOptionsSpec` oggetto e passando `setPDF2XDP` nonché chiamando `true` e passando `setXMLData` `true`. È quindi possibile richiamare il metodo dell&#39; `FormsResult` oggetto `getOutputXML` per recuperare i dati XML che corrispondono ai dati XDP/XML. (L&#39; `FormsResult` oggetto viene restituito dal `processFormSubmission` metodo illustrato nel passaggio secondario successivo.)

   * Richiama il metodo dell’ `FormsServiceClient` oggetto `processFormSubmission` e passa i seguenti valori:

      * L&#39; `com.adobe.idp.Document` oggetto che contiene i dati del modulo.
      * Valore stringa che specifica le variabili di ambiente, comprese tutte le intestazioni HTTP rilevanti. Specificate il tipo di contenuto da gestire. Per gestire i dati XML, specificate il seguente valore di stringa per questo parametro: `CONTENT_TYPE=text/xml`. Per gestire i dati PDF, specificare il seguente valore di stringa per questo parametro: `CONTENT_TYPE=application/pdf`.
      * Un valore di stringa che specifica il valore dell&#39; `HTTP_USER_AGENT` intestazione, ad esempio, . `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`. Questo valore del parametro è facoltativo.
      * Un `RenderOptionsSpec` oggetto che memorizza le opzioni di esecuzione.
      Il `processFormSubmission` metodo restituisce un `FormsResult` oggetto contenente i risultati dell&#39;invio del modulo.

   * Determinare se il servizio Forms ha completato l&#39;elaborazione dei dati del modulo richiamando il `FormsResult` metodo dell&#39; `getAction` oggetto. Se questo metodo restituisce il valore, `0`i dati sono pronti per essere elaborati.



1. Determinare se l&#39;invio del modulo contiene allegati

   * Richiama il metodo dell’ `FormsResult` oggetto `getAttachments` . Questo metodo restituisce un `java.util.List` oggetto che contiene i file inviati con il modulo.
   * Eseguire un&#39;iterazione sull&#39; `java.util.List` oggetto per determinare se sono presenti allegati di file. In presenza di allegati, ogni elemento è un&#39; `com.adobe.idp.Document` istanza. È possibile salvare gli allegati richiamando il `com.adobe.idp.Document` metodo dell&#39;oggetto `copyToFile` e passando un `java.io.File` oggetto.
   >[!NOTE]
   >
   >Questo passaggio è applicabile solo se il modulo viene inviato come PDF.

1. Elaborazione dei dati inviati

   * Se il tipo di contenuto dei dati è `application/vnd.adobe.xdp+xml` o `text/xml`, creare la logica dell&#39;applicazione per recuperare i valori dei dati XML.

      * Creare un `com.adobe.idp.Document` oggetto richiamando il `FormsResult` metodo dell&#39; `getOutputContent` oggetto.
      * Creare un `java.io.InputStream` oggetto richiamando il `java.io.DataInputStream` costruttore e passando l&#39; `com.adobe.idp.Document` oggetto.
      * Creare un `org.w3c.dom.DocumentBuilderFactory` oggetto chiamando il `org.w3c.dom.DocumentBuilderFactory` metodo dell&#39; `newInstance` oggetto statico.
      * Creare un `org.w3c.dom.DocumentBuilder` oggetto richiamando il `org.w3c.dom.DocumentBuilderFactory` metodo dell&#39; `newDocumentBuilder` oggetto.
      * Creare un `org.w3c.dom.Document` oggetto richiamando il `org.w3c.dom.DocumentBuilder` metodo dell&#39; `parse` oggetto e passando l&#39; `java.io.InputStream` oggetto.
      * Recuperare il valore di ciascun nodo all&#39;interno del documento XML. Un modo per eseguire questa attività è creare un metodo personalizzato che accetta due parametri: l&#39; `org.w3c.dom.Document` oggetto e il nome del nodo di cui si desidera recuperare il valore. Questo metodo restituisce una stringa che rappresenta il valore del nodo. Nell&#39;esempio di codice che segue questo processo, viene chiamato questo metodo personalizzato `getNodeText`. Viene visualizzato il corpo di questo metodo.
   * Se il tipo di contenuto dei dati è `application/pdf`, creare la logica dell&#39;applicazione per salvare i dati PDF inviati come file PDF.

      * Creare un `com.adobe.idp.Document` oggetto richiamando il `FormsResult` metodo dell&#39; `getOutputContent` oggetto.
      * Creare un `java.io.File` oggetto utilizzando il relativo costruttore pubblico. Accertatevi di specificare PDF come estensione del nome file.
      * Compilare il file PDF richiamando il metodo dell&#39; `com.adobe.idp.Document` oggetto `copyToFile` e passando l&#39; `java.io.File` oggetto.


**Consulta anche**

[Avvio rapido (modalità SOAP): Gestione dei moduli PDF inviati come XML mediante l&#39;API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-handling-pdf-forms-submitted-as-xml-using-the-java-api)

[Avvio rapido (modalità SOAP): Gestione dei moduli HTML inviati come XML mediante l&#39;API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-handling-html-forms-submitted-as-xml-using-the-java-api)

[Avvio rapido (modalità SOAP): Gestione dei moduli PDF inviati come PDF tramite l&#39;API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-handling-pdf-forms-submitted-as-pdf-using-the-java-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Gestione dei dati PDF inviati tramite l&#39;API del servizio Web {#handle-submitted-pdf-data-using-the-web-service-api}

Gestire un modulo inviato utilizzando l&#39;API Forms (servizio Web):

1. Includi file di progetto

   * Creare classi proxy Java che utilizzano il WSDL del servizio Forms.
   * Includete le classi proxy Java nel percorso della classe.

1. Creare un oggetto API client Forms

   Creare un `FormsService` oggetto e impostare i valori di autenticazione.

1. Recupero dei dati del modulo

   * Per recuperare i dati del modulo inviati a un Servlet Java, creare un `BLOB` oggetto utilizzando il relativo costruttore.
   * Creare un `java.io.InputStream` oggetto richiamando il `javax.servlet.http.HttpServletResponse` metodo dell&#39; `getInputStream` oggetto.
   * Creare un `java.io.ByteArrayOutputStream` oggetto utilizzando il relativo costruttore e passando la lunghezza dell&#39; `java.io.InputStream` oggetto.
   * Copiare il contenuto dell&#39; `java.io.InputStream` oggetto nell&#39; `java.io.ByteArrayOutputStream` oggetto.
   * Creare un array di byte richiamando il metodo dell&#39; `java.io.ByteArrayOutputStream` oggetto `toByteArray` .
   * Compilare l&#39; `BLOB` oggetto richiamandone il `setBinaryData` metodo e passando l&#39;array di byte come argomento.
   * Creare un `RenderOptionsSpec` oggetto utilizzando il relativo costruttore. Impostare il valore delle impostazioni internazionali richiamando il metodo dell&#39; `RenderOptionsSpec` oggetto `setLocale` e passando un valore di stringa che specifica il valore delle impostazioni internazionali.
   * Richiama il metodo dell’ `FormsService` oggetto `processFormSubmission` e passa i seguenti valori:

      * L&#39; `BLOB` oggetto che contiene i dati del modulo.
      * Valore stringa che specifica le variabili di ambiente, comprese tutte le intestazioni HTTP rilevanti. Specificate il tipo di contenuto da gestire. Per gestire i dati XML, specificate il seguente valore di stringa per questo parametro: `CONTENT_TYPE=text/xml`. Per gestire i dati PDF, specificare il seguente valore di stringa per questo parametro: `CONTENT_TYPE=application/pdf`.
      * Un valore di stringa che specifica il valore dell&#39; `HTTP_USER_AGENT` intestazione; ad esempio, `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
      * Un `RenderOptionsSpec` oggetto che memorizza le opzioni di esecuzione.
      * Un oggetto vuoto `BLOBHolder` compilato dal metodo.
      * Un oggetto vuoto `javax.xml.rpc.holders.StringHolder` compilato dal metodo.
      * Un oggetto vuoto `BLOBHolder` compilato dal metodo.
      * Un oggetto vuoto `BLOBHolder` compilato dal metodo.
      * Un oggetto vuoto `javax.xml.rpc.holders.ShortHolder` compilato dal metodo.
      * Un oggetto vuoto `MyArrayOf_xsd_anyTypeHolder` compilato dal metodo. Questo parametro viene utilizzato per memorizzare gli allegati inviati insieme al modulo.
      * Un `FormsResultHolder` oggetto vuoto compilato dal metodo con il modulo inviato.
      Il `processFormSubmission` metodo compila il `FormsResultHolder` parametro con i risultati dell&#39;invio del modulo.

   * Determinare se il servizio Forms ha completato l&#39;elaborazione dei dati del modulo richiamando il `FormsResult` metodo dell&#39; `getAction` oggetto. Se questo metodo restituisce il valore, i dati del modulo sono pronti per essere elaborati. `0` È possibile ottenere un `FormsResult` oggetto ottenendo il valore del membro `FormsResultHolder` dati `value` dell&#39;oggetto.


1. Determinare se l&#39;invio del modulo contiene allegati

   Ottenere il valore del membro `MyArrayOf_xsd_anyTypeHolder` dati dell&#39; `value` oggetto (l&#39; `MyArrayOf_xsd_anyTypeHolder` oggetto è stato passato al `processFormSubmission` metodo). Questo membro di dati restituisce un array di `Objects`. Ogni elemento all&#39;interno dell&#39; `Object` array corrisponde `Object`ai file inviati insieme al modulo. È possibile ottenere ogni elemento all&#39;interno della matrice e inviarlo a un `BLOB` oggetto.

1. Elaborazione dei dati inviati

   * Se il tipo di contenuto dei dati è `application/vnd.adobe.xdp+xml` o `text/xml`, creare la logica dell&#39;applicazione per recuperare i valori dei dati XML.

      * Creare un `BLOB` oggetto richiamando il `FormsResult` metodo dell&#39; `getOutputContent` oggetto.
      * Creare un array di byte richiamando il metodo dell&#39; `BLOB` oggetto `getBinaryData` .
      * Creare un `java.io.InputStream` oggetto richiamando il `java.io.ByteArrayInputStream` costruttore e passando l&#39;array di byte.
      * Creare un `org.w3c.dom.DocumentBuilderFactory` oggetto chiamando il `org.w3c.dom.DocumentBuilderFactory` metodo dell&#39; `newInstance` oggetto statico.
      * Creare un `org.w3c.dom.DocumentBuilder` oggetto richiamando il `org.w3c.dom.DocumentBuilderFactory` metodo dell&#39; `newDocumentBuilder` oggetto.
      * Creare un `org.w3c.dom.Document` oggetto richiamando il `org.w3c.dom.DocumentBuilder` metodo dell&#39; `parse` oggetto e passando l&#39; `java.io.InputStream` oggetto.
      * Recuperare il valore di ciascun nodo all&#39;interno del documento XML. Un modo per eseguire questa attività è creare un metodo personalizzato che accetta due parametri: l&#39; `org.w3c.dom.Document` oggetto e il nome del nodo di cui si desidera recuperare il valore. Questo metodo restituisce una stringa che rappresenta il valore del nodo. Nell&#39;esempio di codice che segue questo processo, viene chiamato questo metodo personalizzato `getNodeText`. Viene visualizzato il corpo di questo metodo.
   * Se il tipo di contenuto dei dati è `application/pdf`, creare la logica dell&#39;applicazione per salvare i dati PDF inviati come file PDF.

      * Creare un `BLOB` oggetto richiamando il `FormsResult` metodo dell&#39; `getOutputContent` oggetto.
      * Creare un array di byte richiamando il metodo dell&#39; `BLOB` oggetto `getBinaryData` .
      * Creare un `java.io.File` oggetto utilizzando il relativo costruttore pubblico. Accertatevi di specificare PDF come estensione del nome file.
      * Creare un `java.io.FileOutputStream` oggetto utilizzando il relativo costruttore e passando l&#39; `java.io.File` oggetto.
      * Compilare il file PDF richiamando il metodo dell&#39; `java.io.FileOutputStream` oggetto `write` e passando l&#39;array di byte.


**Consulta anche**

[Richiamo di moduli AEM con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)