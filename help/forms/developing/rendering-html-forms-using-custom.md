---
title: Rendering di HTML Forms utilizzando file CSS personalizzati
seo-title: Rendering di HTML Forms utilizzando file CSS personalizzati
description: Utilizza il servizio Forms per fare riferimento a file CSS personalizzati per eseguire il rendering dei moduli HTML in risposta a una richiesta HTTP da un browser web. È possibile eseguire il rendering di un modulo HTML che utilizza un file CSS utilizzando l’API Java e l’API Web Service.
seo-description: Utilizza il servizio Forms per fare riferimento a file CSS personalizzati per eseguire il rendering dei moduli HTML in risposta a una richiesta HTTP da un browser web. È possibile eseguire il rendering di un modulo HTML che utilizza un file CSS utilizzando l’API Java e l’API Web Service.
uuid: a44e96f1-001d-48a2-8c96-15cb9d0c71b3
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 8fe7c072-7df0-44b7-92d0-bf39dc1e688a
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1739'
ht-degree: 0%

---


# Rendering di Forms HTML utilizzando file CSS personalizzati {#rendering-html-forms-using-custom-css-files}

**Esempi ed esempi in questo documento sono solo per AEM Forms in ambiente JEE.**

Il servizio Forms esegue il rendering dei moduli HTML in risposta a una richiesta HTTP da parte di un browser Web. Quando si esegue il rendering di un modulo HTML, il servizio Forms può fare riferimento a un file CSS personalizzato. È possibile creare un file CSS personalizzato per soddisfare i requisiti aziendali e fare riferimento a tale file CSS quando si utilizza il servizio Forms per il rendering dei moduli HTML.

Il servizio Forms analizza silenziosamente il file CSS personalizzato. In altre parole, il servizio Forms non segnala gli errori che possono verificarsi se il file CSS personalizzato non è conforme agli standard CSS. In questa situazione, il servizio Forms ignora lo stile e continua con gli stili rimanenti che si trovano nel file CSS.

L’elenco seguente specifica gli stili supportati in un file CSS personalizzato:

* **Coppie** stile selettore a livello di classe: Se presente in un file CSS personalizzato, vengono utilizzati i selettori utilizzati nel modulo HTML come stili di classe. Gli stili di classe non utilizzati vengono ignorati.
* **Coppie** stile selettore a livello di identificatore: Se utilizzati nel modulo HTML, vengono utilizzati tutti gli stili di identificatore.
* **Coppie** stile selettore a livello di elemento: Tutti gli stili di elemento vengono utilizzati se sono utilizzati nel modulo HTML.
* **Priorità** stile: La priorità di stile (come importante) è supportata e può essere utilizzata in un file CSS personalizzato.
* **Tipo** di file multimediali: Per definire il tipo di supporto, è possibile racchiudere una o più coppie in stile selettore in stile @media. Il servizio Forms non controlla se il tipo di supporto specificato è supportato. Il tipo di supporto specificato nel file CSS personalizzato viene unito nel modulo HTML.

È possibile recuperare un file CSS di esempio utilizzando l’applicazione FormsIVS. Carica il modulo, selezionalo nella pagina Test Form Design e fai clic su GeneraCSS. Non è necessario impostare il tipo di trasformazione HTML prima di fare clic sul pulsante . Quindi seleziona salva. Puoi modificare questo file CSS per soddisfare i requisiti aziendali.

>[!NOTE]
>
>Prima di eseguire il rendering di un modulo HTML che utilizza un file CSS personalizzato, è importante avere una conoscenza approfondita del rendering dei moduli HTML. (Vedere [Rendering di Forms come HTML](/help/forms/developing/rendering-forms-html.md).)

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Forms, consulta [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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

Il rendering di un modulo HTML richiede anche valori quali i valori URI necessari per il rendering di altri tipi di modulo.

**Scrivere il flusso di dati del modulo sul browser Web client**

Quando il servizio Forms esegue il rendering di un modulo HTML, restituisce un flusso di dati del modulo che è necessario scrivere nel browser Web del client per rendere il modulo HTML visibile all’utente.

**Consulta anche**

[Eseguire il rendering di un modulo HTML che utilizza un file CSS utilizzando l’API Java](#render-an-html-form-that-uses-a-css-file-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API di Forms Service](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Rendering di PDF forms interattivi](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Rendering di Forms come HTML](/help/forms/developing/rendering-forms-html.md)

[Creazione di applicazioni Web per il rendering di Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

## Eseguire il rendering di un modulo HTML che utilizza un file CSS utilizzando l&#39;API Java {#render-an-html-form-that-uses-a-css-file-using-the-java-api}

Eseguire il rendering di un modulo HTML che utilizza un file CSS personalizzato utilizzando l’API Forms (Java):

1. Includi file di progetto

   Includi file JAR client, come adobe-forms-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto API Java di Forms

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `FormsServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Fai riferimento al file CSS

   * Creare un oggetto `HTMLRenderSpec` utilizzando il relativo costruttore.
   * Per eseguire il rendering del modulo HTML che utilizza un file CSS personalizzato, richiamare il metodo `setCustomCSSURI` dell’oggetto `HTMLRenderSpec` e passare un valore di stringa che specifica la posizione e il nome del file CSS.

1. Rendering di un modulo HTML

   Richiama il metodo `(Deprecated) (Deprecated) renderHTMLForm` dell&#39;oggetto `FormsServiceClient` e passa i seguenti valori:

   * Valore stringa che specifica il nome della struttura del modulo, inclusa l&#39;estensione del nome file. Se si fa riferimento a una struttura del modulo che fa parte di un&#39;applicazione Forms, assicurarsi di specificare il percorso completo, ad esempio `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Valore enum `TransformTo` che specifica il tipo di preferenza HTML. Ad esempio, per eseguire il rendering di un modulo HTML compatibile con HTML dinamico per Internet Explorer 5.0 o versione successiva, specificare `TransformTo.MSDHTML`.
   * Un oggetto `com.adobe.idp.Document` contenente i dati da unire al modulo. Se non si desidera unire i dati, passare un oggetto `com.adobe.idp.Document` vuoto.
   * L&#39;oggetto `HTMLRenderSpec` che memorizza le opzioni di runtime HTML.
   * Valore stringa che specifica il valore di intestazione `HTTP_USER_AGENT`, ad esempio `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
   * Un oggetto `URLSpec` che memorizza i valori URI necessari per il rendering di un modulo HTML.
   * Un oggetto `java.util.HashMap` che memorizza gli allegati di file. Questo è un parametro facoltativo ed è possibile specificare `null` se non si desidera allegare file al modulo.

   Il metodo `(Deprecated) renderHTMLForm` restituisce un oggetto `FormsResult` contenente un flusso di dati del modulo che deve essere scritto nel browser Web client.

1. Scrivere il flusso di dati del modulo sul browser Web client

   * Creare un oggetto `com.adobe.idp.Document` richiamando il metodo `FormsResult` object ‘s `getOutputContent` .
   * Ottenere il tipo di contenuto dell&#39;oggetto `com.adobe.idp.Document` richiamandone il metodo `getContentType`.
   * Impostare il tipo di contenuto dell&#39;oggetto `javax.servlet.http.HttpServletResponse` richiamandone il metodo `setContentType` e passando il tipo di contenuto dell&#39;oggetto `com.adobe.idp.Document`.
   * Creare un oggetto `javax.servlet.ServletOutputStream` utilizzato per scrivere il flusso di dati del modulo nel browser Web client richiamando il metodo `javax.servlet.h\ttp.HttpServletResponse` dell&#39;oggetto `getOutputStream`.
   * Creare un oggetto `java.io.InputStream` richiamando il metodo `com.adobe.idp.Document` dell&#39;oggetto `getInputStream`.
   * Creare una matrice di byte e compilarla con il flusso di dati del modulo richiamando il metodo `InputStream` dell&#39;oggetto `read` e passando la matrice di byte come argomento.
   * Richiamare il metodo `write` dell’oggetto `javax.servlet.ServletOutputStream` per inviare il flusso di dati del modulo al browser Web client. Passa l&#39;array di byte al metodo `write` .

**Consulta anche**

[Rendering di HTML Forms utilizzando file CSS personalizzati](#rendering-html-forms-using-custom-css-files)

[Avvio rapido (modalità SOAP): Rendering di un modulo HTML che utilizza un file CSS utilizzando l’API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-that-uses-a-css-file-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Eseguire il rendering di un modulo HTML che utilizza un file CSS utilizzando l&#39;API del servizio Web {#render-an-html-form-that-uses-a-css-file-using-the-web-service-api}

Eseguire il rendering di un modulo HTML che utilizza un file CSS personalizzato utilizzando l’API Forms (servizio Web):

1. Includi file di progetto

   * Creare classi proxy Java che utilizzano il servizio WSDL di Forms.
   * Includi le classi proxy Java nel percorso della classe.

1. Creare un oggetto API Java di Forms

   Creare un oggetto `FormsService` e impostare i valori di autenticazione.

1. Fai riferimento al file CSS

   * Creare un oggetto `HTMLRenderSpec` utilizzando il relativo costruttore.
   * Per eseguire il rendering del modulo HTML che utilizza un file CSS personalizzato, richiamare il metodo `setCustomCSSURI` dell’oggetto `HTMLRenderSpec` e passare un valore di stringa che specifica la posizione e il nome del file CSS.

1. Rendering di un modulo HTML

   Richiama il metodo `(Deprecated) renderHTMLForm` dell&#39;oggetto `FormsService` e passa i seguenti valori:

   * Valore stringa che specifica il nome della struttura del modulo, inclusa l&#39;estensione del nome file. Se si fa riferimento a una struttura del modulo che fa parte di un&#39;applicazione Forms, assicurarsi di specificare il percorso completo, ad esempio `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Valore enum `TransformTo` che specifica il tipo di preferenza HTML. Ad esempio, per eseguire il rendering di un modulo HTML compatibile con HTML dinamico per Internet Explorer 5.0 o versione successiva, specificare `TransformTo.MSDHTML`.
   * Un oggetto `BLOB` contenente i dati da unire al modulo. Se non desideri unire i dati, passa `null`. (Consultare [Precompilazione di Forms con layout fluidi](/help/forms/developing/prepopulating-forms-flowable-layouts.md).)
   * L&#39;oggetto `HTMLRenderSpec` che memorizza le opzioni di runtime HTML.
   * Valore stringa che specifica il valore di intestazione `HTTP_USER_AGENT`, ad esempio `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`. Se non si desidera impostare questo valore, è possibile passare una stringa vuota.
   * Un oggetto `URLSpec` che memorizza i valori URI necessari per il rendering di un modulo HTML.
   * Un oggetto `java.util.HashMap` che memorizza gli allegati di file. Questo è un parametro facoltativo ed è possibile specificare `null` se non si desidera allegare file al modulo.
   * Un oggetto `com.adobe.idp.services.holders.BLOBHolder` vuoto compilato dal metodo `(Deprecated) renderHTMLForm`. Questo valore del parametro memorizza il modulo di cui è stato effettuato il rendering.
   * Un oggetto `com.adobe.idp.services.holders.BLOBHolder` vuoto compilato dal metodo `(Deprecated) renderHTMLForm`. Questo parametro memorizza i dati XML di output.
   * Un oggetto `javax.xml.rpc.holders.LongHolder` vuoto compilato dal metodo `(Deprecated) renderHTMLForm`. Questo argomento memorizza il numero di pagine nel modulo.
   * Un oggetto `javax.xml.rpc.holders.StringHolder` vuoto compilato dal metodo `(Deprecated) renderHTMLForm`. Questo argomento memorizza il valore delle impostazioni internazionali.
   * Un oggetto `javax.xml.rpc.holders.StringHolder` vuoto compilato dal metodo `(Deprecated) renderHTMLForm`. Questo argomento memorizza il valore di rendering HTML utilizzato.
   * Un oggetto `com.adobe.idp.services.holders.FormsResultHolder` vuoto che conterrà i risultati dell&#39;operazione.

   Il metodo `(Deprecated) renderHTMLForm` popola l&#39;oggetto `com.adobe.idp.services.holders.FormsResultHolder` passato come ultimo valore dell&#39;argomento con un flusso di dati del modulo che deve essere scritto nel browser Web client.

1. Scrivere il flusso di dati del modulo sul browser Web client

   * Creare un oggetto `FormResult` ottenendo il valore del membro dati `com.adobe.idp.services.holders.FormsResultHolder` dell&#39;oggetto `value`.
   * Creare un oggetto `BLOB` che contiene dati del modulo richiamando il metodo `FormsResult` dell&#39;oggetto `getOutputContent`.
   * Ottenere il tipo di contenuto dell&#39;oggetto `BLOB` richiamandone il metodo `getContentType`.
   * Impostare il tipo di contenuto dell&#39;oggetto `javax.servlet.http.HttpServletResponse` richiamandone il metodo `setContentType` e passando il tipo di contenuto dell&#39;oggetto `BLOB`.
   * Creare un oggetto `javax.servlet.ServletOutputStream` utilizzato per scrivere il flusso di dati del modulo nel browser Web client richiamando il metodo `javax.servlet.http.HttpServletResponse` dell&#39;oggetto `getOutputStream`.
   * Creare una matrice di byte e compilarla richiamando il metodo `getBinaryData` dell&#39;oggetto `BLOB`. Questa attività assegna il contenuto dell&#39;oggetto `FormsResult` all&#39;array di byte.
   * Richiamare il metodo `write` dell’oggetto `javax.servlet.http.HttpServletResponse` per inviare il flusso di dati del modulo al browser Web client. Passa l&#39;array di byte al metodo `write` .

**Consulta anche**

[Rendering di HTML Forms utilizzando file CSS personalizzati](#rendering-html-forms-using-custom-css-files)

[Richiamo di AEM Forms con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
