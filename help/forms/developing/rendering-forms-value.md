---
title: Rendering di Forms per valore
seo-title: Rendering Forms By Value
description: Utilizza l’API Forms (Java) per eseguire il rendering di un modulo per valore utilizzando l’API Java e l’API di servizio Web.
seo-description: Use the Forms API (Java) to render a form by value using the Java API and Web Service API.
uuid: b932cc54-662f-40ae-94e0-20ac82845f3b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: ddbb2b82-4c57-4845-a5be-2435902d312b
role: Developer
exl-id: a3a6a06d-ec90-4147-a5f0-e776a086ee12
source-git-commit: 0c7dba43dad8608b4a5de271e1e44942c950fb16
workflow-type: tm+mt
source-wordcount: '1835'
ht-degree: 0%

---

# Rendering di Forms per valore {#rendering-forms-by-value}

**Esempi ed esempi in questo documento sono solo per AEM Forms in ambiente JEE.**

In genere, una struttura del modulo creata in Designer viene trasmessa in riferimento al servizio Forms. Le strutture del modulo possono essere di grandi dimensioni e, di conseguenza, è più efficiente passarle con un riferimento per evitare di dover eseguire il marshalling dei byte della struttura del modulo in base al valore. Il servizio Forms può anche memorizzare nella cache la struttura del modulo in modo che, una volta memorizzata nella cache, non sia necessario leggere continuamente la struttura del modulo.

Se una struttura del modulo contiene un attributo UUID, viene memorizzata nella cache. Il valore UUID è univoco per tutte le strutture del modulo e viene utilizzato per identificare in modo univoco un modulo. Quando si esegue il rendering di un modulo in base al valore, il modulo deve essere memorizzato nella cache solo se utilizzato ripetutamente. Tuttavia, se il modulo non viene utilizzato ripetutamente e deve essere univoco, è possibile evitare di memorizzare il modulo nella cache utilizzando opzioni di memorizzazione nella cache impostate utilizzando l’API di AEM Forms.

Il servizio Forms può inoltre risolvere la posizione del contenuto collegato all’interno della struttura del modulo. Ad esempio, le immagini collegate a cui si fa riferimento all’interno della struttura del modulo sono URL relativi. Si presume sempre che il contenuto collegato sia relativo alla posizione della struttura del modulo. Pertanto, la risoluzione del contenuto collegato è una questione di determinare la sua posizione applicando il percorso relativo alla posizione assoluta della struttura del modulo.

Anziché passare una struttura del modulo per riferimento, è possibile passare una struttura del modulo per valore. Il passaggio di una struttura del modulo in base al valore è efficiente quando la struttura del modulo viene creata in modo dinamico; cioè, quando un&#39;applicazione client genera l&#39;XML che crea una struttura del modulo durante l&#39;esecuzione. In questa situazione una struttura del modulo non viene memorizzata in un archivio fisico perché è memorizzata in memoria. Quando si crea in modo dinamico una struttura del modulo in fase di esecuzione e la si passa per valore, è possibile memorizzare il modulo nella cache e migliorare le prestazioni del servizio Forms.

**Limitazioni del passaggio di un modulo per valore**

Quando una struttura del modulo viene passata per valore, si applicano le seguenti limitazioni:

* Nella struttura del modulo non è possibile inserire contenuto collegato relativo. Tutte le immagini e i frammenti devono essere incorporati nella struttura del modulo o essere indicati in modo assoluto.
* Impossibile eseguire calcoli lato server dopo il rendering del modulo. Se il modulo viene inviato nuovamente al servizio Forms, i dati vengono estratti e restituiti senza alcun calcolo lato server.
* Poiché HTML può utilizzare solo immagini collegate in fase di esecuzione, non è possibile generare HTML con immagini incorporate. Questo perché il servizio Forms supporta immagini incorporate con HTML recuperando le immagini da una struttura del modulo di riferimento. Poiché una struttura del modulo passata dal valore non dispone di una posizione di riferimento, non è possibile estrarre le immagini incorporate quando viene visualizzata la pagina HTML. Pertanto, i riferimenti immagine devono essere percorsi assoluti di cui eseguire il rendering in HTML.

>[!NOTE]
>
>Sebbene sia possibile eseguire il rendering di diversi tipi di moduli per valore (ad esempio, moduli di HTML o moduli che contengono diritti di utilizzo), in questa sezione viene illustrato il rendering dei PDF forms interattivi.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Forms, vedi [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Riepilogo dei passaggi {#summary-of-steps}

Per eseguire il rendering di un modulo in base al valore, procedere come segue:

1. Includi file di progetto.
1. Creare un oggetto API client Forms.
1. Fare riferimento alla struttura del modulo.
1. Eseguire il rendering di un modulo per valore.
1. Scrivere il flusso di dati del modulo sul browser Web client.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

**Creare un oggetto API client Forms**

Prima di poter importare i dati in modo programmatico in un’API client di PDF, è necessario creare un client del servizio di integrazione dei dati. Quando crei un client di servizio, definisci le impostazioni di connessione necessarie per richiamare un servizio.

**Riferimento alla struttura del modulo**

Quando si esegue il rendering di un modulo per valore, è necessario creare un `com.adobe.idp.Document` oggetto che contiene la struttura del modulo da sottoporre a rendering. È possibile fare riferimento a un file XDP esistente oppure creare in modo dinamico una struttura del modulo in fase di esecuzione e compilare un `com.adobe.idp.Document` con quei dati.

>[!NOTE]
>
>Questa sezione e il relativo avvio rapido fanno riferimento a un file XDP esistente.

**Rendering di un modulo per valore**

Per eseguire il rendering di un modulo in base al valore, trasmettere un messaggio `com.adobe.idp.Document` istanza che contiene la struttura del modulo al metodo di rendering `inDataDoc` (può essere uno dei `FormsServiceClient` i metodi di rendering dell’oggetto, ad esempio `renderPDFForm`, `(Deprecated) renderHTMLForm`e così via). Questo valore di parametro è normalmente riservato ai dati uniti al modulo. Analogamente, passare un valore di stringa vuoto al `formQuery` parametro . Normalmente questo parametro richiede un valore stringa che specifica il nome della struttura del modulo.

>[!NOTE]
>
>Se si desidera visualizzare i dati all’interno del modulo, è necessario specificarli all’interno della `xfa:datasets` elemento. Per informazioni sull&#39;architettura XFA, vai a [https://www.pdfa.org/norm-refs/XFA-3_3.pdf](https://www.pdfa.org/norm-refs/XFA-3_3.pdf).

**Scrivere il flusso di dati del modulo sul browser Web client**

Quando il servizio Forms esegue il rendering di un modulo per valore, restituisce un flusso di dati del modulo che è necessario scrivere nel browser Web client. Una volta scritto nel browser Web client, il modulo è visibile all’utente.

**Consulta anche**

[Eseguire il rendering di un modulo per valore utilizzando l’API Java](#render-a-form-by-value-using-the-java-api)

[Eseguire il rendering di un modulo per valore utilizzando l’API del servizio Web](#render-a-form-by-value-using-the-web-service-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API di Forms Service](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Trasmissione di documenti al servizio Forms](/help/forms/developing/passing-documents-forms-service.md)

[Creazione di applicazioni Web per il rendering di Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

## Eseguire il rendering di un modulo per valore utilizzando l’API Java {#render-a-form-by-value-using-the-java-api}

Eseguire il rendering di un modulo per valore utilizzando l’API Forms (Java):

1. Includi file di progetto

   Includi file JAR client, come adobe-forms-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto API client Forms

   * Crea un `ServiceClientFactory` oggetto contenente le proprietà di connessione.
   * Crea un `FormsServiceClient` utilizzando il relativo costruttore e passando `ServiceClientFactory` oggetto.

1. Riferimento alla struttura del modulo

   * Crea un `java.io.FileInputStream` oggetto che rappresenta la struttura del modulo di cui eseguire il rendering utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del file XDP.
   * Crea un `com.adobe.idp.Document` utilizzando il relativo costruttore e passando `java.io.FileInputStream` oggetto.

1. Rendering di un modulo per valore

   Richiama il `FormsServiceClient` dell’oggetto `renderPDFForm` e passare i seguenti valori:

   * Valore stringa vuoto. Normalmente questo parametro richiede un valore stringa che specifica il nome della struttura del modulo.
   * A `com.adobe.idp.Document` oggetto contenente la struttura del modulo. Normalmente questo valore di parametro è riservato ai dati uniti al modulo.
   * A `PDFFormRenderSpec` oggetto che memorizza le opzioni di esecuzione. Si tratta di un parametro facoltativo ed è possibile specificare `null` se non si desidera specificare le opzioni di esecuzione.
   * A `URLSpec` oggetto che contiene i valori URI richiesti dal servizio Forms.
   * A `java.util.HashMap` oggetto che memorizza gli allegati di file. Si tratta di un parametro facoltativo ed è possibile specificare `null` se non si desidera allegare file al modulo.

   La `renderPDFForm` restituisce un `FormsResult` oggetto che contiene un flusso di dati del modulo che può essere scritto nel browser Web client.

1. Scrivere il flusso di dati del modulo sul browser Web client

   * Crea un `com.adobe.idp.Document` richiamando l&#39;oggetto `FormsResult` oggetto ‘s `getOutputContent` metodo .
   * Ottieni il tipo di contenuto del `com.adobe.idp.Document` richiamandone l&#39;oggetto `getContentType` metodo .
   * Imposta la `javax.servlet.http.HttpServletResponse` tipo di contenuto dell’oggetto richiamandone il tipo `setContentType` e passare il tipo di contenuto `com.adobe.idp.Document` oggetto.
   * Crea un `javax.servlet.ServletOutputStream` oggetto utilizzato per scrivere il flusso di dati del modulo nel browser Web client richiamando il `javax.servlet.http.HttpServletResponse` dell’oggetto `getOutputStream` metodo .
   * Crea un `java.io.InputStream` richiamando l&#39;oggetto `com.adobe.idp.Document` dell’oggetto `getInputStream` metodo .
   * Creare un array di byte e allocare le dimensioni del `InputStream` oggetto. Richiama il `InputStream` dell’oggetto `available` per ottenere le dimensioni del `InputStream` oggetto.
   * Compilare l’array di byte con il flusso di dati del modulo richiamando l’ `InputStream` dell’oggetto `read`e passare l&#39;array di byte come argomento.
   * Richiama il `javax.servlet.ServletOutputStream` dell’oggetto `write` per inviare il flusso di dati del modulo al browser Web client. Passa l&#39;array di byte al `write` metodo .

**Consulta anche**

[Rendering di Forms per valore](/help/forms/developing/rendering-forms.md)

[Avvio rapido (modalità SOAP): Rendering per valore utilizzando l’API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-by-value-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Eseguire il rendering di un modulo per valore utilizzando l’API del servizio Web {#render-a-form-by-value-using-the-web-service-api}

Eseguire il rendering di un modulo per valore utilizzando l’API Forms (servizio Web):

1. Includi file di progetto

   * Creare classi proxy Java che utilizzano il servizio WSDL di Forms.
   * Includi le classi proxy Java nel percorso della classe.

1. Creare un oggetto API client Forms

   Crea un `FormsService` e impostare i valori di autenticazione.

1. Riferimento alla struttura del modulo

   * Crea un `java.io.FileInputStream` utilizzando il relativo costruttore. Passa un valore stringa che specifica la posizione del file XDP.
   * Crea un `BLOB` utilizzando il relativo costruttore. La `BLOB` viene utilizzato per memorizzare un documento PDF crittografato con una password.
   * Creare un array di byte che memorizza il contenuto del `java.io.FileInputStream` oggetto. È possibile determinare le dimensioni dell&#39;array di byte ottenendo il `java.io.FileInputStream` dimensioni dell’oggetto utilizzando `available` metodo .
   * Compilare l&#39;array di byte con i dati del flusso richiamando il `java.io.FileInputStream` dell’oggetto `read` e passare l&#39;array di byte.
   * Popolare `BLOB` richiamandone l&#39;oggetto `setBinaryData` e passare l&#39;array di byte.

1. Rendering di un modulo per valore

   Richiama il `FormsService` dell’oggetto `renderPDFForm` e passare i seguenti valori:

   * Valore stringa vuoto. Normalmente questo parametro richiede un valore stringa che specifica il nome della struttura del modulo.
   * A `BLOB` oggetto contenente la struttura del modulo. Normalmente questo valore di parametro è riservato ai dati uniti al modulo.
   * A `PDFFormRenderSpec` oggetto che memorizza le opzioni di esecuzione. Si tratta di un parametro facoltativo ed è possibile specificare `null` se non si desidera specificare le opzioni di esecuzione.
   * A `URLSpec` oggetto che contiene i valori URI richiesti dal servizio Forms.
   * A `java.util.HashMap` oggetto che memorizza gli allegati di file. Si tratta di un parametro facoltativo ed è possibile specificare `null` se non si desidera allegare file al modulo.
   * Un vuoto `com.adobe.idp.services.holders.BLOBHolder` oggetto popolato dal metodo . Viene utilizzato per memorizzare il modulo PDF di cui è stato eseguito il rendering.
   * Un vuoto `javax.xml.rpc.holders.LongHolder` oggetto popolato dal metodo . Questo argomento memorizza il numero di pagine nel modulo.
   * Un vuoto `javax.xml.rpc.holders.StringHolder` oggetto popolato dal metodo . Questo argomento memorizza il valore delle impostazioni internazionali.
   * Un vuoto `com.adobe.idp.services.holders.FormsResultHolder` oggetto che conterrà i risultati dell&#39;operazione.

   La `renderPDFForm` popola il `com.adobe.idp.services.holders.FormsResultHolder` oggetto passato come ultimo valore argomento con un flusso di dati del modulo che deve essere scritto nel browser Web client.

1. Scrivere il flusso di dati del modulo sul browser Web client

   * Crea un `FormResult` ottenendo il valore del `com.adobe.idp.services.holders.FormsResultHolder` dell’oggetto `value` membro dati.
   * Crea un `BLOB` oggetto che contiene i dati del modulo richiamando il `FormsResult` dell’oggetto `getOutputContent` metodo .
   * Ottieni il tipo di contenuto del `BLOB` richiamandone l&#39;oggetto `getContentType` metodo .
   * Imposta la `javax.servlet.http.HttpServletResponse` tipo di contenuto dell’oggetto richiamandone il tipo `setContentType` e passare il tipo di contenuto `BLOB` oggetto.
   * Crea un `javax.servlet.ServletOutputStream` oggetto utilizzato per scrivere il flusso di dati del modulo nel browser Web client richiamando il `javax.servlet.http.HttpServletResponse` dell’oggetto `getOutputStream` metodo .
   * Creare un array di byte e compilarlo richiamando il `BLOB` dell’oggetto `getBinaryData` metodo . Questa attività assegna il contenuto del `FormsResult` all&#39;array di byte.
   * Richiama il `javax.servlet.http.HttpServletResponse` dell’oggetto `write` per inviare il flusso di dati del modulo al browser Web client. Passa l&#39;array di byte al `write` metodo .

**Consulta anche**

[Rendering di Forms per valore](#rendering-forms-by-value)

[Richiamo di AEM Forms con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
