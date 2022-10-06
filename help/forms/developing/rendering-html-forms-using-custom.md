---
title: Rendering di HTML Forms utilizzando file CSS personalizzati
seo-title: Rendering HTML Forms Using Custom CSS Files
description: Utilizza il servizio Forms per fare riferimento a file CSS personalizzati per eseguire il rendering dei moduli HTML in risposta a una richiesta HTTP da parte di un browser web. È possibile eseguire il rendering di un modulo HTML che utilizza un file CSS utilizzando l’API Java e l’API Web Service.
seo-description: Use the Forms service to refer to custom CSS files to render HTML forms in response to an HTTP request from a web browser. You can render an HTML form that uses a CSS file using the Java API and Web Service API.
uuid: a44e96f1-001d-48a2-8c96-15cb9d0c71b3
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 8fe7c072-7df0-44b7-92d0-bf39dc1e688a
role: Developer
exl-id: 5fa385a7-f030-4c0c-8938-0991d02ef361
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1688'
ht-degree: 0%

---

# Rendering di HTML Forms utilizzando file CSS personalizzati {#rendering-html-forms-using-custom-css-files}

**Esempi ed esempi in questo documento sono solo per AEM Forms in ambiente JEE.**

Il servizio Forms esegue il rendering dei moduli di HTML in risposta a una richiesta HTTP da parte di un browser Web. Durante il rendering di un modulo HTML, il servizio Forms può fare riferimento a un file CSS personalizzato. È possibile creare un file CSS personalizzato per soddisfare i requisiti aziendali e fare riferimento a tale file CSS quando si utilizza il servizio Forms per il rendering dei moduli HTML.

Il servizio Forms analizza silenziosamente il file CSS personalizzato. In altre parole, il servizio Forms non segnala gli errori che possono verificarsi se il file CSS personalizzato non è conforme agli standard CSS. In questa situazione, il servizio Forms ignora lo stile e continua con gli stili rimanenti che si trovano nel file CSS.

L’elenco seguente specifica gli stili supportati in un file CSS personalizzato:

* **Coppie stile selettore a livello di classe**: Se presente in un file CSS personalizzato, vengono utilizzati i selettori utilizzati nel modulo HTML come stili di classe. Gli stili di classe non utilizzati vengono ignorati.
* **Coppie stile selettore a livello di identificatore**: Se utilizzati nel modulo HTML, vengono utilizzati tutti gli stili di identificatore.
* **Coppie stile selettore a livello di elemento**: Tutti gli stili di elemento vengono utilizzati se sono utilizzati nel modulo HTML.
* **Priorità stile**: La priorità di stile (come importante) è supportata e può essere utilizzata in un file CSS personalizzato.
* **Tipo di supporto**: Per definire il tipo di supporto è possibile racchiudere una o più coppie stile selettore in stile @media. Il servizio Forms non controlla se il tipo di supporto specificato è supportato. Il tipo di supporto specificato nel file CSS personalizzato viene unito nel modulo HTML.

È possibile recuperare un file CSS di esempio utilizzando l’applicazione FormsIVS. Carica il modulo, selezionalo nella pagina Test Form Design e fai clic su GeneraCSS. Non è necessario impostare il tipo di trasformazione HTML prima di fare clic sul pulsante. Quindi seleziona salva. Puoi modificare questo file CSS per soddisfare i requisiti aziendali.

>[!NOTE]
>
>Prima di eseguire il rendering di un modulo HTML che utilizza un file CSS personalizzato, è importante avere una conoscenza approfondita del rendering dei moduli di HTML. (Vedi [Rendering di Forms as HTML](/help/forms/developing/rendering-forms-html.md).)

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Forms, vedi [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Riepilogo dei passaggi {#summary-of-steps}

Per eseguire il rendering di un modulo HTML che utilizza un file CSS, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Crea un oggetto API Java Forms.
1. Fai riferimento al file CSS.
1. Eseguire il rendering di un modulo HTML.
1. Scrivere il flusso di dati del modulo sul browser Web client.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

**Creare un oggetto API Java di Forms**

Prima di poter eseguire in modo programmatico un’operazione supportata dal servizio Forms, è necessario creare un oggetto client Forms.

**Fai riferimento al file CSS**

Per eseguire il rendering di un modulo HTML che utilizza un file CSS personalizzato, assicurarsi di fare riferimento a un file CSS esistente.

**Rendering di un modulo HTML**

Per eseguire il rendering di un modulo HTML, è necessario specificare una struttura del modulo creata in Designer e salvata come file XDP. È inoltre necessario selezionare un tipo di trasformazione HTML. Ad esempio, è possibile specificare il tipo di trasformazione HTML che esegue il rendering di un HTML dinamico per Internet Explorer 5.0 o versione successiva.

Il rendering di un modulo HTML richiede anche valori, ad esempio valori URI necessari per il rendering di altri tipi di modulo.

**Scrivere il flusso di dati del modulo sul browser Web client**

Quando il servizio Forms esegue il rendering di un modulo HTML, restituisce un flusso di dati del modulo che è necessario scrivere nel browser Web del client per rendere il modulo HTML visibile all’utente.

**Consulta anche**

[Eseguire il rendering di un modulo HTML che utilizza un file CSS utilizzando l’API Java](#render-an-html-form-that-uses-a-css-file-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API di Forms Service](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Rendering di PDF forms interattivi](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Rendering di Forms as HTML](/help/forms/developing/rendering-forms-html.md)

[Creazione di applicazioni Web per il rendering di Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

## Eseguire il rendering di un modulo HTML che utilizza un file CSS utilizzando l’API Java {#render-an-html-form-that-uses-a-css-file-using-the-java-api}

Eseguire il rendering di un modulo HTML che utilizza un file CSS personalizzato utilizzando l’API Forms (Java):

1. Includi file di progetto

   Includi file JAR client, come adobe-forms-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto API Java di Forms

   * Crea un `ServiceClientFactory` oggetto contenente le proprietà di connessione.
   * Crea un `FormsServiceClient` utilizzando il relativo costruttore e passando `ServiceClientFactory` oggetto.

1. Fai riferimento al file CSS

   * Crea un `HTMLRenderSpec` utilizzando il relativo costruttore.
   * Per eseguire il rendering del modulo HTML che utilizza un file CSS personalizzato, richiamare `HTMLRenderSpec` dell’oggetto `setCustomCSSURI` e passare un valore stringa che specifica la posizione e il nome del file CSS.

1. Rendering di un modulo HTML

   Richiama il `FormsServiceClient` dell’oggetto `(Deprecated) (Deprecated) renderHTMLForm` e passare i seguenti valori:

   * Valore stringa che specifica il nome della struttura del modulo, inclusa l&#39;estensione del nome file. Se si fa riferimento a una struttura del modulo che fa parte di un&#39;applicazione Forms, verificare di specificare il percorso completo, ad esempio `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `TransformTo` valore enum che specifica il tipo di preferenza HTML. Ad esempio, per eseguire il rendering di un modulo HTML compatibile con Dynamic HTML per Internet Explorer 5.0 o versione successiva, specificare `TransformTo.MSDHTML`.
   * A `com.adobe.idp.Document` oggetto contenente i dati da unire al modulo. Se non si desidera unire i dati, passare un valore vuoto `com.adobe.idp.Document` oggetto.
   * La `HTMLRenderSpec` oggetto che memorizza le opzioni di runtime di HTML.
   * Un valore stringa che specifica la variabile `HTTP_USER_AGENT` valore di intestazione, ad esempio `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
   * A `URLSpec` oggetto che memorizza i valori URI necessari per eseguire il rendering di un modulo HTML.
   * A `java.util.HashMap` oggetto che memorizza gli allegati di file. Questo è un parametro facoltativo ed è possibile specificare `null` se non si desidera allegare file al modulo.

   La `(Deprecated) renderHTMLForm` restituisce un `FormsResult` oggetto che contiene un flusso di dati del modulo che deve essere scritto nel browser Web client.

1. Scrivere il flusso di dati del modulo sul browser Web client

   * Crea un `com.adobe.idp.Document` richiamando l&#39;oggetto `FormsResult` oggetto ‘s `getOutputContent` metodo .
   * Ottieni il tipo di contenuto del `com.adobe.idp.Document` richiamandone l&#39;oggetto `getContentType` metodo .
   * Imposta la `javax.servlet.http.HttpServletResponse` tipo di contenuto dell’oggetto richiamandone il tipo `setContentType` e passare il tipo di contenuto `com.adobe.idp.Document` oggetto.
   * Crea un `javax.servlet.ServletOutputStream` oggetto utilizzato per scrivere il flusso di dati del modulo nel browser Web client richiamando il `javax.servlet.h\ttp.HttpServletResponse` dell’oggetto `getOutputStream` metodo .
   * Crea un `java.io.InputStream` richiamando l&#39;oggetto `com.adobe.idp.Document` dell’oggetto `getInputStream` metodo .
   * Creare un array di byte e compilarlo con il flusso di dati del modulo richiamando il `InputStream` dell’oggetto `read` e passare l&#39;array di byte come argomento.
   * Richiama il `javax.servlet.ServletOutputStream` dell’oggetto `write` per inviare il flusso di dati del modulo al browser Web client. Passa l&#39;array di byte al `write` metodo .

**Consulta anche**

[Rendering di HTML Forms utilizzando file CSS personalizzati](#rendering-html-forms-using-custom-css-files)

[Avvio rapido (modalità SOAP): Rendering di un modulo HTML che utilizza un file CSS utilizzando l’API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-that-uses-a-css-file-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Eseguire il rendering di un modulo HTML che utilizza un file CSS utilizzando l’API del servizio Web {#render-an-html-form-that-uses-a-css-file-using-the-web-service-api}

Eseguire il rendering di un modulo HTML che utilizza un file CSS personalizzato utilizzando l’API Forms (servizio Web):

1. Includi file di progetto

   * Creare classi proxy Java che utilizzano il servizio WSDL di Forms.
   * Includi le classi proxy Java nel percorso della classe.

1. Creare un oggetto API Java di Forms

   Crea un `FormsService` e impostare i valori di autenticazione.

1. Fai riferimento al file CSS

   * Crea un `HTMLRenderSpec` utilizzando il relativo costruttore.
   * Per eseguire il rendering del modulo HTML che utilizza un file CSS personalizzato, richiamare `HTMLRenderSpec` dell’oggetto `setCustomCSSURI` e passare un valore stringa che specifica la posizione e il nome del file CSS.

1. Rendering di un modulo HTML

   Richiama il `FormsService` dell’oggetto `(Deprecated) renderHTMLForm` e passare i seguenti valori:

   * Valore stringa che specifica il nome della struttura del modulo, inclusa l&#39;estensione del nome file. Se si fa riferimento a una struttura del modulo che fa parte di un&#39;applicazione Forms, verificare di specificare il percorso completo, ad esempio `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `TransformTo` valore enum che specifica il tipo di preferenza HTML. Ad esempio, per eseguire il rendering di un modulo HTML compatibile con Dynamic HTML per Internet Explorer 5.0 o versione successiva, specificare `TransformTo.MSDHTML`.
   * A `BLOB` oggetto contenente i dati da unire al modulo. Se non si desidera unire i dati, passare `null`. (Vedi [Precompilazione di Forms con layout fluidi](/help/forms/developing/prepopulating-forms-flowable-layouts.md).)
   * La `HTMLRenderSpec` oggetto che memorizza le opzioni di runtime di HTML.
   * Un valore stringa che specifica la variabile `HTTP_USER_AGENT` valore di intestazione, ad esempio `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`. Se non si desidera impostare questo valore, è possibile passare una stringa vuota.
   * A `URLSpec` oggetto che memorizza i valori URI necessari per eseguire il rendering di un modulo HTML.
   * A `java.util.HashMap` oggetto che memorizza gli allegati di file. Questo è un parametro facoltativo ed è possibile specificare `null` se non si desidera allegare file al modulo.
   * Un vuoto `com.adobe.idp.services.holders.BLOBHolder` oggetto popolato da `(Deprecated) renderHTMLForm` metodo . Questo valore del parametro memorizza il modulo di cui è stato effettuato il rendering.
   * Un vuoto `com.adobe.idp.services.holders.BLOBHolder` oggetto popolato da `(Deprecated) renderHTMLForm` metodo . Questo parametro memorizza i dati XML di output.
   * Un vuoto `javax.xml.rpc.holders.LongHolder` oggetto popolato da `(Deprecated) renderHTMLForm` metodo . Questo argomento memorizza il numero di pagine nel modulo.
   * Un vuoto `javax.xml.rpc.holders.StringHolder` oggetto popolato da `(Deprecated) renderHTMLForm` metodo . Questo argomento memorizza il valore delle impostazioni internazionali.
   * Un vuoto `javax.xml.rpc.holders.StringHolder` oggetto popolato da `(Deprecated) renderHTMLForm` metodo . Questo argomento memorizza il valore di rendering di HTML utilizzato.
   * Un vuoto `com.adobe.idp.services.holders.FormsResultHolder` oggetto che conterrà i risultati dell&#39;operazione.

   La `(Deprecated) renderHTMLForm` popola il `com.adobe.idp.services.holders.FormsResultHolder` oggetto passato come ultimo valore argomento con un flusso di dati del modulo che deve essere scritto nel browser Web client.

1. Scrivere il flusso di dati del modulo sul browser Web client

   * Crea un `FormResult` ottenendo il valore del `com.adobe.idp.services.holders.FormsResultHolder` dell’oggetto `value` membro dati.
   * Crea un `BLOB` oggetto che contiene i dati del modulo richiamando il `FormsResult` dell’oggetto `getOutputContent` metodo .
   * Ottieni il tipo di contenuto del `BLOB` richiamandone l&#39;oggetto `getContentType` metodo .
   * Imposta la `javax.servlet.http.HttpServletResponse` tipo di contenuto dell’oggetto richiamandone il tipo `setContentType` e passare il tipo di contenuto `BLOB` oggetto.
   * Crea un `javax.servlet.ServletOutputStream` oggetto utilizzato per scrivere il flusso di dati del modulo nel browser Web client richiamando il `javax.servlet.http.HttpServletResponse` dell’oggetto `getOutputStream` metodo .
   * Creare un array di byte e compilarlo richiamando il `BLOB` dell’oggetto `getBinaryData` metodo . Questa attività assegna il contenuto del `FormsResult` all&#39;array di byte.
   * Richiama il `javax.servlet.http.HttpServletResponse` dell’oggetto `write` per inviare il flusso di dati del modulo al browser Web client. Passa l&#39;array di byte al `write` metodo .

**Consulta anche**

[Rendering di HTML Forms utilizzando file CSS personalizzati](#rendering-html-forms-using-custom-css-files)

[Richiamo di AEM Forms con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
