---
title: Rendering di Forms per valore
seo-title: Rendering di Forms per valore
description: 'null'
seo-description: 'null'
uuid: b932cc54-662f-40ae-94e0-20ac82845f3b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: ddbb2b82-4c57-4845-a5be-2435902d312b
translation-type: tm+mt
source-git-commit: 66bfd6870b4c09dc2ca1b66058e0b9e040a71507
workflow-type: tm+mt
source-wordcount: '1812'
ht-degree: 0%

---


# Rendering di Forms per valore {#rendering-forms-by-value}

In genere, una struttura del modulo creata in Designer viene trasmessa facendo riferimento al servizio Forms. Le strutture del modulo possono essere di grandi dimensioni e, di conseguenza, è più efficiente passarle mediante riferimento per evitare di dover eseguire il marshalling dei byte delle strutture del modulo in base al valore. Il servizio Forms può anche memorizzare nella cache la struttura del modulo, in modo che, se memorizzata nella cache, non debba essere continuamente letta.

Se una struttura del modulo contiene un attributo UUID, viene memorizzata nella cache. Il valore UUID è univoco per tutte le strutture del modulo e viene utilizzato per identificare in modo univoco un modulo. Quando si esegue il rendering di un modulo in base al valore, il modulo deve essere memorizzato nella cache solo se utilizzato più volte. Tuttavia, se il modulo non viene utilizzato ripetutamente e deve essere univoco, è possibile evitare di memorizzarlo nella cache utilizzando opzioni di memorizzazione nella cache impostate tramite l&#39;API AEM Forms .

Il servizio Forms può inoltre risolvere la posizione del contenuto collegato all&#39;interno della struttura del modulo. Ad esempio, le immagini collegate a cui viene fatto riferimento nella struttura del modulo sono URL relativi. Si presume sempre che il contenuto collegato sia relativo alla posizione della struttura del modulo. Pertanto, per risolvere il contenuto collegato è necessario determinarne la posizione applicando il percorso relativo alla posizione assoluta della struttura del modulo.

Anziché trasmettere una struttura del modulo per riferimento, è possibile trasmettere una struttura del modulo per valore. Il passaggio di una struttura del modulo in base al valore è efficiente quando si crea in modo dinamico una struttura del modulo; ovvero quando un&#39;applicazione client genera l&#39;XML che crea una struttura del modulo in fase di esecuzione. In questo caso, una struttura del modulo non viene memorizzata in un archivio fisico perché è memorizzata in memoria. Durante la creazione dinamica di una struttura del modulo in fase di esecuzione e il suo passaggio per valore, è possibile memorizzare il modulo nella cache e migliorare le prestazioni del servizio Forms.

**Limiti di trasmissione di un modulo per valore**

Quando una struttura del modulo viene passata per valore, si applicano le seguenti limitazioni:

* Nessun contenuto collegato relativo può essere incluso nella struttura del modulo. Tutte le immagini e i frammenti devono essere incorporati nella struttura del modulo o essere denominati in modo assoluto.
* Non è possibile eseguire calcoli sul lato server dopo il rendering del modulo. Se il modulo viene inviato nuovamente al servizio Forms, i dati vengono estratti e restituiti senza calcoli sul lato server.
* Poiché HTML può utilizzare solo immagini collegate in fase di esecuzione, non è possibile generare HTML con immagini incorporate. Questo perché il servizio Forms supporta le immagini incorporate con HTML recuperando le immagini da una struttura del modulo di riferimento. Poiché una struttura del modulo passata per valore non dispone di una posizione di riferimento, non è possibile estrarre le immagini incorporate quando viene visualizzata la pagina HTML. Di conseguenza, i riferimenti immagine devono essere percorsi assoluti per il rendering in HTML.

>[!NOTE]
>
>Anche se è possibile eseguire il rendering di diversi tipi di moduli per valore (ad esempio, moduli HTML o che contengono diritti di utilizzo), in questa sezione viene illustrato il rendering di PDF forms interattivi.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Forms, vedere [Guida di riferimento dei servizi per  AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Riepilogo dei passaggi {#summary-of-steps}

Per eseguire il rendering di un modulo in base al valore, procedere come segue:

1. Includere i file di progetto.
1. Creare un oggetto Forms Client API.
1. Fare riferimento alla struttura del modulo.
1. Eseguire il rendering di un modulo per valore.
1. Scrivere il flusso di dati del modulo nel browser Web del client.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se state creando un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate servizi Web, accertatevi di includere i file proxy.

**Creare un oggetto Forms Client API**

Prima di poter importare i dati in un modulo PDF API client a livello di programmazione, è necessario creare un client di servizi di integrazione dati. Quando create un client di servizi, definite le impostazioni di connessione necessarie per richiamare un servizio.

**Riferimento alla struttura del modulo**

Quando si esegue il rendering di un modulo in base al valore, è necessario creare un oggetto `com.adobe.idp.Document` che contenga la struttura del modulo da sottoporre a rendering. È possibile fare riferimento a un file XDP esistente oppure creare in modo dinamico una struttura del modulo in fase di esecuzione e compilare un `com.adobe.idp.Document` con tali dati.

>[!NOTE]
>
>Questa sezione e il relativo avvio rapido fanno riferimento a un file XDP esistente.

**Eseguire il rendering di un modulo per valore**

Per eseguire il rendering di un modulo in base al valore, passare un&#39;istanza `com.adobe.idp.Document` che contiene la struttura del modulo al parametro `inDataDoc` del metodo di rendering (può essere uno dei metodi di rendering dell&#39;oggetto `FormsServiceClient` come `renderPDFForm`, `(Deprecated) renderHTMLForm` e così via). Questo valore del parametro è in genere riservato ai dati uniti al modulo. Analogamente, trasmettere un valore di stringa vuoto al parametro `formQuery`. Normalmente questo parametro richiede un valore stringa che specifica il nome della struttura del modulo.

>[!NOTE]
>
>Se si desidera visualizzare i dati all&#39;interno del modulo, è necessario specificarli all&#39;interno dell&#39;elemento `xfa:datasets`. Per informazioni sull&#39;architettura XFA, visitare il sito Web [https://partners.adobe.com/public/developer/xml/index_arch.html](https://partners.adobe.com/public/developer/xml/index_arch.html).

**Scrivere il flusso di dati del modulo nel browser Web del client**

Quando il servizio Forms esegue il rendering di un modulo per valore, restituisce un flusso di dati del modulo che è necessario scrivere nel browser Web del client. Una volta scritto nel browser Web del client, il modulo è visibile all&#39;utente.

**Consulta anche**

[Eseguire il rendering di un modulo per valore utilizzando l&#39;API Java](#render-a-form-by-value-using-the-java-api)

[Eseguire il rendering di un modulo per valore utilizzando l&#39;API del servizio Web](#render-a-form-by-value-using-the-web-service-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido di Forms Service API](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Invio di documenti al servizio Forms](/help/forms/developing/passing-documents-forms-service.md)

[Creazione di applicazioni Web per il rendering di Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

## Eseguire il rendering di un modulo per valore utilizzando l&#39;API Java {#render-a-form-by-value-using-the-java-api}

Eseguire il rendering di un modulo per valore utilizzando l&#39;API di Forms (Java):

1. Includi file di progetto

   Includete file JAR client, ad esempio adobe-forms-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto Forms Client API

   * Creare un oggetto `ServiceClientFactory` che contiene le proprietà di connessione.
   * Creare un oggetto `FormsServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Riferimento alla struttura del modulo

   * Creare un oggetto `java.io.FileInputStream` che rappresenta la struttura del modulo da eseguire di rendering utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del file XDP.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Eseguire il rendering di un modulo per valore

   Richiamare il metodo `FormsServiceClient` dell&#39;oggetto `renderPDFForm` e trasmettere i seguenti valori:

   * Un valore di stringa vuoto. Normalmente questo parametro richiede un valore stringa che specifica il nome della struttura del modulo.
   * Un oggetto `com.adobe.idp.Document` che contiene la struttura del modulo. Normalmente questo valore di parametro è riservato ai dati uniti al modulo.
   * Un oggetto `PDFFormRenderSpec` che memorizza le opzioni di esecuzione. Si tratta di un parametro facoltativo e potete specificare `null` se non desiderate specificare le opzioni di esecuzione.
   * Un oggetto `URLSpec` che contiene valori URI richiesti dal servizio Forms.
   * Un oggetto `java.util.HashMap` che memorizza gli allegati. Si tratta di un parametro facoltativo ed è possibile specificare `null` se non si desidera allegare file al modulo.

   Il metodo `renderPDFForm` restituisce un oggetto `FormsResult` contenente un flusso di dati del modulo che può essere scritto nel browser Web del client.

1. Scrivere il flusso di dati del modulo nel browser Web del client

   * Creare un oggetto `com.adobe.idp.Document` richiamando il metodo `FormsResult` object ‘s `getOutputContent`.
   * Ottenere il tipo di contenuto dell&#39;oggetto `com.adobe.idp.Document` richiamandone il metodo `getContentType`.
   * Impostare il tipo di contenuto dell&#39;oggetto `javax.servlet.http.HttpServletResponse` richiamandone il metodo `setContentType` e passando il tipo di contenuto dell&#39;oggetto `com.adobe.idp.Document`.
   * Creare un oggetto `javax.servlet.ServletOutputStream` utilizzato per scrivere il flusso di dati del modulo nel browser Web del client richiamando il metodo `javax.servlet.http.HttpServletResponse` dell&#39;oggetto `getOutputStream`.
   * Creare un oggetto `java.io.InputStream` richiamando il metodo `com.adobe.idp.Document` dell&#39;oggetto `getInputStream`.
   * Creare un array di byte e allocare le dimensioni dell&#39;oggetto `InputStream`. Richiamare il metodo `InputStream` dell&#39;oggetto `available` per ottenere le dimensioni dell&#39;oggetto `InputStream`.
   * Compilare l&#39;array di byte con il flusso di dati del modulo richiamando il metodo `read`dell&#39;oggetto `InputStream` e passando l&#39;array di byte come argomento.
   * Richiamare il metodo `javax.servlet.ServletOutputStream` dell&#39;oggetto `write` per inviare il flusso di dati del modulo al browser Web del client. Passate l&#39;array di byte al metodo `write`.

**Consulta anche**

[Rendering di Forms per valore](/help/forms/developing/rendering-forms.md)

[Avvio rapido (modalità SOAP): Rendering per valore tramite l&#39;API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-by-value-using-the-java-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Eseguire il rendering di un modulo per valore utilizzando l&#39;API del servizio Web {#render-a-form-by-value-using-the-web-service-api}

Eseguire il rendering di un modulo per valore utilizzando l&#39;API di Forms (servizio Web):

1. Includi file di progetto

   * Creare classi proxy Java che utilizzano il servizio WSDL di Forms.
   * Includete le classi proxy Java nel percorso della classe.

1. Creare un oggetto Forms Client API

   Creare un oggetto `FormsService` e impostare i valori di autenticazione.

1. Riferimento alla struttura del modulo

   * Creare un oggetto `java.io.FileInputStream` utilizzando il relativo costruttore. Passa un valore di stringa che specifica la posizione del file XDP.
   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare un documento PDF cifrato con una password.
   * Creare un array di byte che memorizza il contenuto dell&#39;oggetto `java.io.FileInputStream`. È possibile determinare la dimensione dell&#39;array di byte ottenendo la dimensione dell&#39;oggetto `java.io.FileInputStream` utilizzando il metodo `available` corrispondente.
   * Compilare l&#39;array di byte con i dati del flusso richiamando il metodo `java.io.FileInputStream` dell&#39;oggetto `read` e passando l&#39;array di byte.
   * Compilare l&#39;oggetto `BLOB` richiamandone il metodo `setBinaryData` e passando l&#39;array di byte.

1. Eseguire il rendering di un modulo per valore

   Richiamare il metodo `FormsService` dell&#39;oggetto `renderPDFForm` e trasmettere i seguenti valori:

   * Un valore di stringa vuoto. Normalmente questo parametro richiede un valore stringa che specifica il nome della struttura del modulo.
   * Un oggetto `BLOB` che contiene la struttura del modulo. Normalmente questo valore di parametro è riservato ai dati uniti al modulo.
   * Un oggetto `PDFFormRenderSpec` che memorizza le opzioni di esecuzione. Si tratta di un parametro facoltativo e potete specificare `null` se non desiderate specificare le opzioni di esecuzione.
   * Un oggetto `URLSpec` che contiene valori URI richiesti dal servizio Forms.
   * Un oggetto `java.util.HashMap` che memorizza gli allegati. Si tratta di un parametro facoltativo ed è possibile specificare `null` se non si desidera allegare file al modulo.
   * Un oggetto `com.adobe.idp.services.holders.BLOBHolder` vuoto compilato dal metodo. Viene utilizzato per memorizzare il modulo PDF di cui è stato effettuato il rendering.
   * Un oggetto `javax.xml.rpc.holders.LongHolder` vuoto compilato dal metodo. Questo argomento memorizza il numero di pagine nel modulo.
   * Un oggetto `javax.xml.rpc.holders.StringHolder` vuoto compilato dal metodo. (Questo argomento memorizza il valore delle impostazioni internazionali.)
   * Un oggetto `com.adobe.idp.services.holders.FormsResultHolder` vuoto che conterrà i risultati dell&#39;operazione.

   Il metodo `renderPDFForm` compila l&#39;oggetto `com.adobe.idp.services.holders.FormsResultHolder` passato come ultimo valore argomento con un flusso di dati del modulo che deve essere scritto nel browser Web del client.

1. Scrivere il flusso di dati del modulo nel browser Web del client

   * Creare un oggetto `FormResult` ottenendo il valore del membro di dati `com.adobe.idp.services.holders.FormsResultHolder` dell&#39;oggetto `value`.
   * Creare un oggetto `BLOB` contenente dati del modulo richiamando il metodo `FormsResult` dell&#39;oggetto `getOutputContent`.
   * Ottenere il tipo di contenuto dell&#39;oggetto `BLOB` richiamandone il metodo `getContentType`.
   * Impostare il tipo di contenuto dell&#39;oggetto `javax.servlet.http.HttpServletResponse` richiamandone il metodo `setContentType` e passando il tipo di contenuto dell&#39;oggetto `BLOB`.
   * Creare un oggetto `javax.servlet.ServletOutputStream` utilizzato per scrivere il flusso di dati del modulo nel browser Web del client richiamando il metodo `javax.servlet.http.HttpServletResponse` dell&#39;oggetto `getOutputStream`.
   * Creare un array di byte e compilarlo richiamando il metodo `BLOB` dell&#39;oggetto `getBinaryData`. Questa attività assegna il contenuto dell&#39;oggetto `FormsResult` all&#39;array di byte.
   * Richiamare il metodo `javax.servlet.http.HttpServletResponse` dell&#39;oggetto `write` per inviare il flusso di dati del modulo al browser Web del client. Passate l&#39;array di byte al metodo `write`.

**Consulta anche**

[Rendering di Forms per valore](#rendering-forms-by-value)

[Richiamo  AEM Forms con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
