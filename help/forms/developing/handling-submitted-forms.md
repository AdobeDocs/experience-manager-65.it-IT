---
title: Gestione dei Forms inviati
description: Utilizza il servizio Forms per recuperare i dati inviati immessi in un modulo interattivo. L’utente può inviare i dati del modulo nei formati XML, PDF e URL UTF-16.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 419335b2-2aae-4e83-98ff-18e61b7efa9c
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '2894'
ht-degree: 0%

---

# Gestione dei Forms inviati {#handling-submitted-forms}

**Gli esempi e gli esempi contenuti in questo documento sono solo per AEM Forms in ambiente JEE.**

Le applicazioni basate sul Web che consentono a un utente di compilare moduli interattivi richiedono l&#39;invio dei dati al server. Tramite il servizio Forms è possibile recuperare i dati immessi dall&#39;utente in un modulo interattivo. Dopo aver recuperato i dati, è possibile elaborarli per soddisfare i requisiti aziendali. È ad esempio possibile memorizzare i dati in un database, inviarli a un&#39;altra applicazione, inviarli a un altro servizio, unire i dati in una struttura di modulo, visualizzarli in un browser Web e così via.

I dati del modulo vengono inviati al servizio Forms come dati XML o PDF, opzione impostata in Designer. Un modulo inviato come XML consente di estrarre i singoli valori dei dati dei campi. In altre parole, è possibile estrarre il valore di ogni campo modulo immesso dall&#39;utente nel modulo. Un modulo inviato come dati PDF è costituito da dati binari e non da dati XML. È possibile salvare il modulo come file PDF o inviarlo a un altro servizio. Se si desidera estrarre dati da un modulo inviato come XML e quindi utilizzare i dati del modulo per creare un documento PDF, richiamare un&#39;altra operazione AEM Forms. (Vedi [Creazione di documenti PDF con dati XML inviati](/help/forms/developing/creating-pdf-documents-submitted-xml.md))

Il diagramma seguente mostra i dati inviati a un servlet Java denominato `HandleData` da un modulo interattivo visualizzato in un browser Web.

![hs_hs_handlesubmit](assets/hs_hs_handlesubmit.png)

Nella tabella seguente vengono illustrati i passaggi del diagramma.

<table>
 <thead>
  <tr>
   <th><p>Passaggio</p></th>
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
   <td><p>I dati vengono inviati al servlet Java <code>HandleData</code> come dati XML.</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>Il servlet Java <code>HandleData</code> contiene la logica dell'applicazione per recuperare i dati.</p></td>
  </tr>
 </tbody>
</table>

## Gestione dei dati XML inviati {#handling-submitted-xml-data}

Quando i dati del modulo vengono inviati come XML, è possibile recuperare i dati XML che rappresentano i dati inviati. Tutti i campi modulo vengono visualizzati come nodi in uno schema XML. I valori del nodo corrispondono ai valori inseriti dall&#39;utente. Considerare un modulo prestito in cui ogni campo del modulo viene visualizzato come un nodo all&#39;interno dei dati XML. Il valore di ciascun nodo corrisponde al valore inserito da un utente. Supponiamo che un utente riempia il modulo del prestito con i dati mostrati nel seguente modulo.

![hs_hs_loanformdata](assets/hs_hs_loanformdata.png)

Nella figura seguente vengono illustrati i dati XML corrispondenti recuperati mediante l&#39;API client del servizio Forms.

![hs_loandata](assets/hs_hs_loandata.png)

I campi nel modulo del prestito. Questi valori possono essere recuperati
utilizzo delle classi XML Java.

>[!NOTE]
>
>La struttura del modulo deve essere configurata correttamente in Designer affinché i dati vengano inviati come dati XML. Per configurare correttamente la struttura del modulo per l&#39;invio di dati XML, verificare che il pulsante Invia disponibile nella struttura del modulo sia impostato per l&#39;invio di dati XML. Per informazioni sull&#39;impostazione del pulsante Invia per inviare dati XML, vedere [AEM Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63).

## Gestione dei dati PDF inviati {#handling-submitted-pdf-data}

Considera un’applicazione web che richiama il servizio Forms. Dopo che il servizio Forms esegue il rendering di un modulo interattivo PDF in un browser Web client, l&#39;utente compila il modulo e lo invia nuovamente come dati PDF. Quando il servizio Forms riceve i dati PDF PDF, può inviarli a un altro servizio o salvarli come file PDF. Il diagramma seguente mostra il flusso logico dell’applicazione.

![hs_hs_savingforms](assets/hs_hs_savingforms.png)

Nella tabella seguente vengono descritti i passaggi del diagramma.

<table>
 <thead>
  <tr>
   <th><p>Passaggio</p></th>
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
   <td><p>Il servizio Forms esegue il rendering di un modulo PDF interattivo nel browser Web client.</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>L’utente compila un modulo interattivo e fa clic su un pulsante di invio. Il modulo viene inviato nuovamente al servizio Forms come dati PDF. Questa opzione è impostata in Designer.</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>Il servizio Forms salva i dati PDF come file PDF. </p></td>
  </tr>
 </tbody>
</table>

## Gestione dei dati URL UTF-16 inviati {#handling-submitted-url-utf-16-data}

Se i dati del modulo vengono inviati come dati URL UTF-16, il computer client richiede Adobe Reader o Acrobat 8.1 o versione successiva. Inoltre, se la progettazione del modulo contiene un pulsante di invio con dati codificati in URL (HTTP Post) e l’opzione di codifica dei dati è UTF-16, la progettazione del modulo deve essere modificata in un editor di testo come Blocco note. È possibile impostare l&#39;opzione di codifica su `UTF-16LE` o `UTF-16BE` per il pulsante di invio. Designer non fornisce questa funzionalità.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Forms, vedere [Riferimento ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Riepilogo dei passaggi {#summary-of-steps}

Per gestire i moduli inviati, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Crea un oggetto API client di Forms.
1. Recuperare i dati del modulo.
1. Determinare se l&#39;invio del modulo contiene file allegati.
1. Elabora i dati inviati.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

**Creare un oggetto API client di Forms**

Prima di poter eseguire a livello di programmazione un&#39;operazione API client del servizio Forms, è necessario creare un client del servizio Forms. Se si utilizza l&#39;API Java, creare un oggetto `FormsServiceClient`. Se si utilizza l&#39;API del servizio Web Forms, creare un oggetto `FormsService`.

**Recupera dati modulo**

Per recuperare i dati del modulo inviati, è necessario richiamare il metodo `processFormSubmission` dell&#39;oggetto `FormsServiceClient`. Quando si richiama questo metodo, è necessario specificare il tipo di contenuto del modulo inviato. Quando i dati vengono inviati da un browser Web client al servizio Forms, possono essere inviati come dati XML o PDF. Per recuperare i dati immessi nei campi modulo, è possibile inviare i dati come dati XML.

È inoltre possibile recuperare i campi modulo da un modulo inviato come dati PDF impostando le seguenti opzioni di runtime:

* Passare il seguente valore al metodo `processFormSubmission` come parametro del tipo di contenuto: `CONTENT_TYPE=application/pdf`.
* Imposta il valore `PDFToXDP` dell&#39;oggetto `RenderOptionsSpec` su `true`
* Imposta il valore `ExportDataFormat` dell&#39;oggetto `RenderOptionsSpec` su `XMLData`

Specificare il tipo di contenuto del modulo inviato quando si richiama il metodo `processFormSubmission`. L&#39;elenco seguente specifica i valori dei tipi di contenuto applicabili:

* **text/xml**: rappresenta il tipo di contenuto da utilizzare quando un modulo di PDF invia i dati del modulo come XML.
* **application/x-www-form-urlencoded**: rappresenta il tipo di contenuto da utilizzare quando un modulo HTML invia dati come XML.
* **application/pdf**: rappresenta il tipo di contenuto da utilizzare quando un modulo di PDF invia dati come PDF.

>[!NOTE]
>
>Nella sezione Gestione degli invii di Forms sono disponibili tre avvii rapidi corrispondenti. La sezione Gestione dei PDF forms inviati come PDF con la Guida introduttiva all’API Java illustra come gestire i dati PDF inviati. Il tipo di contenuto specificato in questo avvio rapido è `application/pdf`. La sezione Gestione dei PDF forms inviati come XML mediante l&#39;avvio rapido API Java illustra come gestire i dati XML inviati da un modulo PDF. Il tipo di contenuto specificato in questo avvio rapido è `text/xml`. Analogamente, la gestione dei moduli HTML inviati come XML mediante l&#39;avvio rapido API Java illustra come gestire i dati XML inviati da un modulo HTML. Il tipo di contenuto specificato in questo avvio rapido è application/x-www-form-urlencoded.

Recuperi i dati del modulo pubblicati nel servizio Forms e ne determini lo stato di elaborazione. In altre parole, quando i dati vengono inviati al servizio Forms, non significa necessariamente che il servizio Forms abbia terminato l’elaborazione dei dati e che i dati siano pronti per essere elaborati. Ad esempio, i dati possono essere inviati al servizio Forms in modo da poter eseguire un calcolo. Una volta completato il calcolo, il modulo viene riprodotto all’utente con i risultati del calcolo visualizzati. Prima di elaborare i dati inviati, è consigliabile determinare se il servizio Forms ha completato l&#39;elaborazione dei dati.

Il servizio Forms restituisce i seguenti valori per indicare se ha completato l’elaborazione dei dati:

* **0 (invio):** I dati inviati sono pronti per l&#39;elaborazione.
* **1 (calcolo):** Il servizio Forms ha eseguito un&#39;operazione di calcolo sui dati e i risultati devono essere restituiti all&#39;utente.
* **2 (Convalida):** I dati del modulo convalidati dal servizio Forms e i risultati devono essere restituiti all&#39;utente.
* **3 (successivo):** La pagina corrente è stata modificata con risultati che devono essere scritti nell&#39;applicazione client.
* **4 (Precedente**): la pagina corrente è cambiata con risultati che devono essere scritti nell&#39;applicazione client.

>[!NOTE]
>
>È necessario restituire all’utente i calcoli e le convalide. (Vedi [Calcolo dei dati del modulo](/help/forms/developing/calculating-form-data.md#calculating-form-data).

**Determinare se l&#39;invio del modulo contiene file allegati**

Forms inviato al servizio Forms può contenere allegati. Ad esempio, utilizzando il riquadro degli allegati integrato di Acrobat, un utente può selezionare i file allegati da inviare insieme al modulo. L’utente può inoltre selezionare i file allegati utilizzando una barra degli strumenti di HTML sottoposta a rendering con un file di HTML.

Dopo aver determinato se un modulo contiene file allegati, è possibile elaborare i dati. È ad esempio possibile salvare l&#39;allegato nel file system locale.

>[!NOTE]
>
>Il modulo deve essere inviato come dati PDF per recuperare gli allegati. Se il modulo viene inviato come dati XML, gli allegati non vengono inviati.

**Elabora i dati inviati**

A seconda del tipo di contenuto dei dati inviati, è possibile estrarre singoli valori dei campi modulo dai dati XML inviati oppure salvare i dati PDF inviati come file PDF (o inviarli a un altro servizio). Per estrarre singoli campi modulo, convertire i dati XML inviati in un&#39;origine dati XML e quindi recuperare i valori dell&#39;origine dati XML utilizzando le classi `org.w3c.dom`.

**Consulta anche**

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Guida introduttiva all’API di servizio Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Trasmissione di documenti al servizio Forms](/help/forms/developing/passing-documents-forms-service.md)

[Creazione di applicazioni Web per il rendering di Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

## Gestire i moduli inviati tramite l’API Java {#handle-submitted-forms-using-the-java-api}

Gestisci un modulo inviato utilizzando l’API Forms (Java):

1. Includi file di progetto

   Includi i file JAR client, ad esempio adobe-forms-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto API client di Forms

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `FormsServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Recupera dati modulo

   * Per recuperare i dati del modulo inviati a un servlet Java, creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e richiamando il metodo `getInputStream` dell&#39;oggetto `javax.servlet.http.HttpServletResponse` dal costruttore.
   * Creare un oggetto `RenderOptionsSpec` utilizzando il relativo costruttore. Impostare il valore delle impostazioni locali richiamando il metodo `setLocale` dell&#39;oggetto `RenderOptionsSpec` e passando un valore stringa che specifica il valore delle impostazioni locali.

   >[!NOTE]
   >
   >È possibile indicare al servizio Forms di creare dati XDP o XML dal contenuto PDF inviato richiamando il metodo `setPDF2XDP` dell&#39;oggetto `RenderOptionsSpec` e passando `true`, chiamando anche `setXMLData` e passando `true`. È quindi possibile richiamare il metodo `getOutputXML` dell&#39;oggetto `FormsResult` per recuperare i dati XML corrispondenti ai dati XDP/XML. (L&#39;oggetto `FormsResult` viene restituito dal metodo `processFormSubmission`, illustrato nel passaggio successivo).

   * Richiama il metodo `processFormSubmission` dell&#39;oggetto `FormsServiceClient` e passa i seguenti valori:

      * Oggetto `com.adobe.idp.Document` contenente i dati del modulo.
      * Valore stringa che specifica le variabili di ambiente, incluse tutte le intestazioni HTTP rilevanti. Specifica il tipo di contenuto da gestire. Per gestire i dati XML, specificare il valore stringa seguente per il parametro: `CONTENT_TYPE=text/xml`. Per gestire i dati di PDF, specificare il seguente valore stringa per questo parametro: `CONTENT_TYPE=application/pdf`.
      * Valore stringa che specifica il valore di intestazione `HTTP_USER_AGENT`, ad esempio. `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`. Il valore di questo parametro è facoltativo.
      * Un oggetto `RenderOptionsSpec` che memorizza le opzioni di runtime.

     Il metodo `processFormSubmission` restituisce un oggetto `FormsResult` contenente i risultati dell&#39;invio del modulo.

   * Determinare se il servizio Forms ha terminato l&#39;elaborazione dei dati del modulo richiamando il metodo `getAction` dell&#39;oggetto `FormsResult`. Se questo metodo restituisce il valore `0`, i dati sono pronti per essere elaborati.

1. Determinare se l&#39;invio del modulo contiene allegati

   * Richiama il metodo `getAttachments` dell&#39;oggetto `FormsResult`. Questo metodo restituisce un oggetto `java.util.List` contenente i file inviati con il modulo.
   * Scorrere l&#39;oggetto `java.util.List` per determinare se sono presenti allegati. Se sono presenti file allegati, ogni elemento è un&#39;istanza `com.adobe.idp.Document`. È possibile salvare i file allegati richiamando il metodo `copyToFile` dell&#39;oggetto `com.adobe.idp.Document` e passando un oggetto `java.io.File`.

   >[!NOTE]
   >
   >Questo passaggio è applicabile solo se il modulo viene inviato come PDF.

1. Elabora i dati inviati

   * Se il tipo di contenuto dei dati è `application/vnd.adobe.xdp+xml` o `text/xml`, creare una logica dell&#39;applicazione per recuperare i valori dei dati XML.

      * Creare un oggetto `com.adobe.idp.Document` richiamando il metodo `getOutputContent` dell&#39;oggetto `FormsResult`.
      * Creare un oggetto `java.io.InputStream` richiamando il costruttore `java.io.DataInputStream` e passando l&#39;oggetto `com.adobe.idp.Document`.
      * Creare un oggetto `org.w3c.dom.DocumentBuilderFactory` chiamando il metodo `newInstance` dell&#39;oggetto `org.w3c.dom.DocumentBuilderFactory` statico.
      * Creare un oggetto `org.w3c.dom.DocumentBuilder` richiamando il metodo `newDocumentBuilder` dell&#39;oggetto `org.w3c.dom.DocumentBuilderFactory`.
      * Creare un oggetto `org.w3c.dom.Document` richiamando il metodo `parse` dell&#39;oggetto `org.w3c.dom.DocumentBuilder` e passando l&#39;oggetto `java.io.InputStream`.
      * Recuperate il valore di ciascun nodo all&#39;interno del documento XML. Un modo per eseguire questa attività consiste nel creare un metodo personalizzato che accetti due parametri: l&#39;oggetto `org.w3c.dom.Document` e il nome del nodo di cui si desidera recuperare il valore. Questo metodo restituisce un valore stringa che rappresenta il valore del nodo. Nell&#39;esempio di codice che segue questo processo, il metodo personalizzato è denominato `getNodeText`. Viene visualizzato il corpo di questo metodo.

   * Se il tipo di contenuto dei dati è `application/pdf`, creare la logica dell&#39;applicazione per salvare i dati PDF inviati come file PDF.

      * Creare un oggetto `com.adobe.idp.Document` richiamando il metodo `getOutputContent` dell&#39;oggetto `FormsResult`.
      * Creare un oggetto `java.io.File` utilizzando il relativo costruttore pubblico. Assicurati di specificare PDF come estensione del nome file.
      * Compilare il file PDF richiamando il metodo `copyToFile` dell&#39;oggetto `com.adobe.idp.Document` e passando l&#39;oggetto `java.io.File`.

**Consulta anche**

[Quick Start (modalità SOAP): gestione dei PDF forms inviati come XML tramite API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-handling-pdf-forms-submitted-as-xml-using-the-java-api)

[Quick Start (modalità SOAP): gestione dei moduli HTML inviati come XML tramite l’API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-handling-html-forms-submitted-as-xml-using-the-java-api)

[Quick Start (modalità SOAP): gestione dei PDF forms inviati come PDF tramite l’API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-handling-pdf-forms-submitted-as-pdf-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Gestire i dati PDF inviati tramite l’API del servizio web {#handle-submitted-pdf-data-using-the-web-service-api}

Gestisci un modulo inviato utilizzando l’API Forms (servizio web):

1. Includi file di progetto

   * Creare classi proxy Java che utilizzano il servizio Forms WSDL.
   * Includi le classi proxy Java nel percorso della classe.

1. Creare un oggetto API client di Forms

   Creare un oggetto `FormsService` e impostare i valori di autenticazione.

1. Recupera dati modulo

   * Per recuperare i dati del modulo inviati a un servlet Java, creare un oggetto `BLOB` utilizzando il relativo costruttore.
   * Creare un oggetto `java.io.InputStream` richiamando il metodo `getInputStream` dell&#39;oggetto `javax.servlet.http.HttpServletResponse`.
   * Creare un oggetto `java.io.ByteArrayOutputStream` utilizzando il relativo costruttore e passando la lunghezza dell&#39;oggetto `java.io.InputStream`.
   * Copiare il contenuto dell&#39;oggetto `java.io.InputStream` nell&#39;oggetto `java.io.ByteArrayOutputStream`.
   * Creare una matrice di byte richiamando il metodo `toByteArray` dell&#39;oggetto `java.io.ByteArrayOutputStream`.
   * Compilare l&#39;oggetto `BLOB` richiamando il relativo metodo `setBinaryData` e passando la matrice di byte come argomento.
   * Creare un oggetto `RenderOptionsSpec` utilizzando il relativo costruttore. Impostare il valore delle impostazioni locali richiamando il metodo `setLocale` dell&#39;oggetto `RenderOptionsSpec` e passando un valore stringa che specifica il valore delle impostazioni locali.
   * Richiama il metodo `processFormSubmission` dell&#39;oggetto `FormsService` e passa i seguenti valori:

      * Oggetto `BLOB` contenente i dati del modulo.
      * Valore stringa che specifica le variabili di ambiente, incluse tutte le intestazioni HTTP rilevanti. Specifica il tipo di contenuto da gestire. Per gestire i dati XML, specificare il valore stringa seguente per il parametro: `CONTENT_TYPE=text/xml`. Per gestire i dati di PDF, specificare il seguente valore stringa per questo parametro: `CONTENT_TYPE=application/pdf`.
      * Valore stringa che specifica il valore dell&#39;intestazione `HTTP_USER_AGENT`, ad esempio `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
      * Un oggetto `RenderOptionsSpec` che memorizza le opzioni di runtime.
      * Oggetto `BLOBHolder` vuoto popolato dal metodo.
      * Oggetto `javax.xml.rpc.holders.StringHolder` vuoto popolato dal metodo.
      * Oggetto `BLOBHolder` vuoto popolato dal metodo.
      * Oggetto `BLOBHolder` vuoto popolato dal metodo.
      * Oggetto `javax.xml.rpc.holders.ShortHolder` vuoto popolato dal metodo.
      * Oggetto `MyArrayOf_xsd_anyTypeHolder` vuoto popolato dal metodo. Questo parametro viene utilizzato per memorizzare gli allegati dei file inviati insieme al modulo.
      * Oggetto `FormsResultHolder` vuoto popolato dal metodo con il modulo inviato.

     Il metodo `processFormSubmission` compila il parametro `FormsResultHolder` con i risultati dell&#39;invio del modulo.

   * Determinare se il servizio Forms ha terminato l&#39;elaborazione dei dati del modulo richiamando il metodo `getAction` dell&#39;oggetto `FormsResult`. Se questo metodo restituisce il valore `0`, i dati del modulo sono pronti per l&#39;elaborazione. È possibile ottenere un oggetto `FormsResult` ottenendo il valore del membro dati `value` dell&#39;oggetto `FormsResultHolder`.

1. Determinare se l&#39;invio del modulo contiene allegati

   Ottiene il valore del membro dati `value` dell&#39;oggetto `MyArrayOf_xsd_anyTypeHolder` (l&#39;oggetto `MyArrayOf_xsd_anyTypeHolder` è stato passato al metodo `processFormSubmission`). Questo membro dati restituisce un array di `Objects`. Ogni elemento all&#39;interno dell&#39;array `Object` è un `Object` che corrisponde ai file inviati insieme al modulo. È possibile ottenere ogni elemento all&#39;interno dell&#39;array e eseguirne il cast in un oggetto `BLOB`.

1. Elabora i dati inviati

   * Se il tipo di contenuto dei dati è `application/vnd.adobe.xdp+xml` o `text/xml`, creare una logica dell&#39;applicazione per recuperare i valori dei dati XML.

      * Creare un oggetto `BLOB` richiamando il metodo `getOutputContent` dell&#39;oggetto `FormsResult`.
      * Creare una matrice di byte richiamando il metodo `getBinaryData` dell&#39;oggetto `BLOB`.
      * Creare un oggetto `java.io.InputStream` richiamando il costruttore `java.io.ByteArrayInputStream` e passando la matrice di byte.
      * Creare un oggetto `org.w3c.dom.DocumentBuilderFactory` chiamando il metodo `newInstance` dell&#39;oggetto `org.w3c.dom.DocumentBuilderFactory` statico.
      * Creare un oggetto `org.w3c.dom.DocumentBuilder` richiamando il metodo `newDocumentBuilder` dell&#39;oggetto `org.w3c.dom.DocumentBuilderFactory`.
      * Creare un oggetto `org.w3c.dom.Document` richiamando il metodo `parse` dell&#39;oggetto `org.w3c.dom.DocumentBuilder` e passando l&#39;oggetto `java.io.InputStream`.
      * Recuperate il valore di ciascun nodo all&#39;interno del documento XML. Un modo per eseguire questa attività consiste nel creare un metodo personalizzato che accetti due parametri: l&#39;oggetto `org.w3c.dom.Document` e il nome del nodo di cui si desidera recuperare il valore. Questo metodo restituisce un valore stringa che rappresenta il valore del nodo. Nell&#39;esempio di codice che segue questo processo, il metodo personalizzato è denominato `getNodeText`. Viene visualizzato il corpo di questo metodo.

   * Se il tipo di contenuto dei dati è `application/pdf`, creare la logica dell&#39;applicazione per salvare i dati PDF inviati come file PDF.

      * Creare un oggetto `BLOB` richiamando il metodo `getOutputContent` dell&#39;oggetto `FormsResult`.
      * Creare una matrice di byte richiamando il metodo `getBinaryData` dell&#39;oggetto `BLOB`.
      * Creare un oggetto `java.io.File` utilizzando il relativo costruttore pubblico. Assicurati di specificare PDF come estensione del nome file.
      * Creare un oggetto `java.io.FileOutputStream` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.File`.
      * Compilare il file PDF richiamando il metodo `write` dell&#39;oggetto `java.io.FileOutputStream` e passando la matrice di byte.

**Consulta anche**

[Richiamare AEM Forms utilizzando la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
