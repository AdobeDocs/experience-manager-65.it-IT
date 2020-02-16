---
title: Rendering di moduli HTML con file CSS personalizzati
seo-title: Rendering di moduli HTML con file CSS personalizzati
description: 'null'
seo-description: 'null'
uuid: a44e96f1-001d-48a2-8c96-15cb9d0c71b3
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 8fe7c072-7df0-44b7-92d0-bf39dc1e688a
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Rendering di moduli HTML con file CSS personalizzati {#rendering-html-forms-using-custom-css-files}

Il servizio Forms esegue il rendering dei moduli HTML in risposta a una richiesta HTTP effettuata da un browser Web. Durante il rendering di un modulo HTML, il servizio Forms può fare riferimento a un file CSS personalizzato. È possibile creare un file CSS personalizzato per soddisfare i requisiti aziendali e fare riferimento a tale file CSS quando si utilizza il servizio Forms per eseguire il rendering dei moduli HTML.

Il servizio Forms analizza in modo invisibile il file CSS personalizzato. In altre parole, il servizio Forms non segnala errori che potrebbero verificarsi se il file CSS personalizzato non è conforme agli standard CSS. In questa situazione, il servizio Forms ignora lo stile e continua con gli stili rimanenti che si trovano nel file CSS.

L&#39;elenco seguente specifica gli stili supportati in un file CSS personalizzato:

* **Coppie** stile selettore a livello di classe: Se presente in un file CSS personalizzato, vengono utilizzati i selettori utilizzati nel modulo HTML come stili di classe. Gli stili di classe non utilizzati vengono ignorati.
* **Coppie** stile selettore a livello di identificatore: Tutti gli stili di identificatore vengono utilizzati se usati nel modulo HTML.
* **Coppie** stile selettore livello elemento: Tutti gli stili di elemento vengono utilizzati se utilizzati nel modulo HTML.
* **Priorità** stile: La priorità di stile (come importante) è supportata e può essere utilizzata in un file CSS personalizzato.
* **Tipo** di supporto: Per definire il tipo di supporto, è possibile racchiudere una o più coppie di stile selettore nello stile @media. Il servizio Forms non controlla se il tipo di supporto specificato è supportato. Il tipo di supporto specificato nel file CSS personalizzato viene unito nel modulo HTML.

È possibile recuperare un file CSS di esempio utilizzando l&#39;applicazione FormsIVS. Caricate il modulo, selezionatelo nella pagina Struttura del modulo di prova e fate clic su GeneraCSS. Non è necessario impostare il tipo di trasformazione HTML prima di fare clic sul pulsante. Selezionare Salva. Potete modificare questo file CSS per soddisfare i vostri requisiti aziendali.

>[!NOTE]
>
>Prima di eseguire il rendering di un modulo HTML che utilizza un file CSS personalizzato, è importante avere una conoscenza approfondita del rendering dei moduli HTML. (Vedere [Rendering dei moduli come HTML](/help/forms/developing/rendering-forms-html.md).)

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Forms, consultate Riferimento [servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Riepilogo dei passaggi {#summary-of-steps}

Per eseguire il rendering di un modulo HTML che utilizza un file CSS, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un oggetto API Java di Forms.
1. Fate riferimento al file CSS.
1. Eseguire il rendering di un modulo HTML.
1. Scrivere il flusso di dati del modulo nel browser Web del client.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, accertatevi di includere i file proxy.

**Creare un oggetto API Java Forms**

Prima di eseguire un&#39;operazione supportata dal servizio Forms a livello di programmazione, è necessario creare un oggetto client Forms.

**Riferimento al file CSS**

Per eseguire il rendering di un modulo HTML che utilizza un file CSS personalizzato, assicurarsi di fare riferimento a un file CSS esistente.

**Eseguire il rendering di un modulo HTML**

Per eseguire il rendering di un modulo HTML, è necessario specificare una struttura del modulo creata in Designer e salvata come file XDP. È inoltre necessario selezionare un tipo di trasformazione HTML. Ad esempio, potete specificare il tipo di trasformazione HTML che esegue il rendering di un HTML dinamico per Internet Explorer 5.0 o versione successiva.

Il rendering di un modulo HTML richiede anche valori, ad esempio valori URI, necessari per eseguire il rendering di altri tipi di modulo.

**Scrivere il flusso di dati del modulo nel browser Web del client**

Quando il servizio Forms esegue il rendering di un modulo HTML, restituisce un flusso di dati del modulo che è necessario scrivere nel browser Web del client per rendere il modulo HTML visibile all&#39;utente.

**Consulta anche**

[Eseguire il rendering di un modulo HTML che utilizza un file CSS utilizzando l&#39;API Java](#render-an-html-form-that-uses-a-css-file-using-the-java-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido dell&#39;API di Forms Service](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Rendering di moduli PDF interattivi](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Rendering dei moduli come HTML](/help/forms/developing/rendering-forms-html.md)

[Creazione di applicazioni Web per il rendering di moduli](/help/forms/developing/creating-web-applications-renders-forms.md)

## Eseguire il rendering di un modulo HTML che utilizza un file CSS utilizzando l&#39;API Java {#render-an-html-form-that-uses-a-css-file-using-the-java-api}

Eseguire il rendering di un modulo HTML che utilizza un file CSS personalizzato utilizzando l&#39;API Forms (Java):

1. Includi file di progetto

   Includete file JAR client, ad esempio adobe-forms-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto API Java Forms

   * Creare un `ServiceClientFactory` oggetto che contenga proprietà di connessione.
   * Creare un `FormsServiceClient` oggetto utilizzando il relativo costruttore e passando l&#39; `ServiceClientFactory` oggetto.

1. Riferimento al file CSS

   * Creare un `HTMLRenderSpec` oggetto utilizzando il relativo costruttore.
   * Per eseguire il rendering del modulo HTML che utilizza un file CSS personalizzato, richiamare il metodo dell&#39; `HTMLRenderSpec` oggetto `setCustomCSSURI` e passare un valore di stringa che specifica la posizione e il nome del file CSS.

1. Eseguire il rendering di un modulo HTML

   Richiama il metodo dell’ `FormsServiceClient` oggetto `(Deprecated) (Deprecated) renderHTMLForm` e passa i seguenti valori:

   * Una stringa che specifica il nome della struttura del modulo, inclusa l&#39;estensione del nome file. Se si fa riferimento a una struttura del modulo che fa parte di un&#39;applicazione Forms, è necessario specificare il percorso completo, ad esempio `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Un valore `TransformTo` enum che specifica il tipo di preferenza HTML. Ad esempio, per eseguire il rendering di un modulo HTML compatibile con HTML dinamico per Internet Explorer 5.0 o versione successiva, specificare `TransformTo.MSDHTML`.
   * Un `com.adobe.idp.Document` oggetto che contiene i dati da unire al modulo. Se non si desidera unire i dati, passare un `com.adobe.idp.Document` oggetto vuoto.
   * L&#39; `HTMLRenderSpec` oggetto che memorizza le opzioni di runtime HTML.
   * Una stringa che specifica il valore dell&#39; `HTTP_USER_AGENT` intestazione, ad esempio `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
   * Un `URLSpec` oggetto che memorizza i valori URI richiesti per eseguire il rendering di un modulo HTML.
   * Un `java.util.HashMap` oggetto che memorizza gli allegati. Si tratta di un parametro facoltativo e è possibile specificare `null` se non si desidera allegare file al modulo.
   Il `(Deprecated) renderHTMLForm` metodo restituisce un `FormsResult` oggetto che contiene un flusso di dati del modulo da scrivere nel browser Web del client.

1. Scrivere il flusso di dati del modulo nel browser Web del client

   * Creare un `com.adobe.idp.Document` oggetto richiamando il `FormsResult` metodo ‘s `getOutputContent` .
   * Ottenere il tipo di contenuto dell&#39; `com.adobe.idp.Document` oggetto richiamandone il `getContentType` metodo.
   * Impostare il tipo di contenuto dell&#39; `javax.servlet.http.HttpServletResponse` oggetto richiamandone `setContentType` il metodo e passando il tipo di contenuto dell&#39; `com.adobe.idp.Document` oggetto.
   * Creare un `javax.servlet.ServletOutputStream` oggetto utilizzato per scrivere il flusso di dati del modulo nel browser Web del client richiamando il `javax.servlet.h\ttp.HttpServletResponse` metodo dell&#39; `getOutputStream` oggetto.
   * Creare un `java.io.InputStream` oggetto richiamando il `com.adobe.idp.Document` metodo dell&#39; `getInputStream` oggetto.
   * Creare un array di byte e compilarlo con il flusso di dati del modulo richiamando il metodo dell&#39; `InputStream` oggetto `read` e passando l&#39;array di byte come argomento.
   * Richiamare il metodo dell&#39; `javax.servlet.ServletOutputStream` oggetto `write` per inviare il flusso di dati del modulo al browser Web del client. Passa l&#39;array di byte al `write` metodo.

**Consulta anche**

[Rendering di moduli HTML con file CSS personalizzati](#rendering-html-forms-using-custom-css-files)

[Avvio rapido (modalità SOAP): Rendering di un modulo HTML che utilizza un file CSS utilizzando l&#39;API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-that-uses-a-css-file-using-the-java-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Eseguire il rendering di un modulo HTML che utilizza un file CSS utilizzando l&#39;API del servizio Web {#render-an-html-form-that-uses-a-css-file-using-the-web-service-api}

Eseguire il rendering di un modulo HTML che utilizza un file CSS personalizzato utilizzando l&#39;API Forms (servizio Web):

1. Includi file di progetto

   * Creare classi proxy Java che utilizzano il WSDL del servizio Forms.
   * Includete le classi proxy Java nel percorso della classe.

1. Creare un oggetto API Java Forms

   Creare un `FormsService` oggetto e impostare i valori di autenticazione.

1. Riferimento al file CSS

   * Creare un `HTMLRenderSpec` oggetto utilizzando il relativo costruttore.
   * Per eseguire il rendering del modulo HTML che utilizza un file CSS personalizzato, richiamare il metodo dell&#39; `HTMLRenderSpec` oggetto `setCustomCSSURI` e passare un valore di stringa che specifica la posizione e il nome del file CSS.

1. Eseguire il rendering di un modulo HTML

   Richiama il metodo dell’ `FormsService` oggetto `(Deprecated) renderHTMLForm` e passa i seguenti valori:

   * Una stringa che specifica il nome della struttura del modulo, inclusa l&#39;estensione del nome file. Se si fa riferimento a una struttura del modulo che fa parte di un&#39;applicazione Forms, è necessario specificare il percorso completo, ad esempio `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Un valore `TransformTo` enum che specifica il tipo di preferenza HTML. Ad esempio, per eseguire il rendering di un modulo HTML compatibile con HTML dinamico per Internet Explorer 5.0 o versione successiva, specificare `TransformTo.MSDHTML`.
   * Un `BLOB` oggetto che contiene i dati da unire al modulo. Se non si desidera unire i dati, passare `null`. (vedere [Precompilazione di moduli con layout]scorrevoli(/help/forms/developing/rendering-forms-prepopolating-forms-flowable-layouts-prepopolating.md#prepopolating-forms-with-flowable-layouts).)
   * L&#39; `HTMLRenderSpec` oggetto che memorizza le opzioni di runtime HTML.
   * Una stringa che specifica il valore dell&#39; `HTTP_USER_AGENT` intestazione, ad esempio `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`. Se non si desidera impostare questo valore, è possibile passare una stringa vuota.
   * Un `URLSpec` oggetto che memorizza i valori URI richiesti per eseguire il rendering di un modulo HTML.
   * Un `java.util.HashMap` oggetto che memorizza gli allegati. Si tratta di un parametro facoltativo e è possibile specificare `null` se non si desidera allegare file al modulo.
   * Un oggetto vuoto `com.adobe.idp.services.holders.BLOBHolder` compilato dal `(Deprecated) renderHTMLForm` metodo. Questo valore del parametro memorizza il modulo di cui è stato effettuato il rendering.
   * Un oggetto vuoto `com.adobe.idp.services.holders.BLOBHolder` compilato dal `(Deprecated) renderHTMLForm` metodo. Questo parametro memorizza i dati XML di output.
   * Un oggetto vuoto `javax.xml.rpc.holders.LongHolder` compilato dal `(Deprecated) renderHTMLForm` metodo. Questo argomento memorizza il numero di pagine nel modulo.
   * Un oggetto vuoto `javax.xml.rpc.holders.StringHolder` compilato dal `(Deprecated) renderHTMLForm` metodo. Questo argomento memorizza il valore delle impostazioni internazionali.
   * Un oggetto vuoto `javax.xml.rpc.holders.StringHolder` compilato dal `(Deprecated) renderHTMLForm` metodo. Questo argomento memorizza il valore di rendering HTML utilizzato.
   * Un oggetto vuoto `com.adobe.idp.services.holders.FormsResultHolder` che conterrà i risultati dell&#39;operazione.
   Il `(Deprecated) renderHTMLForm` metodo compila l&#39; `com.adobe.idp.services.holders.FormsResultHolder` oggetto passato come ultimo valore argomento con un flusso di dati del modulo che deve essere scritto nel browser Web del client.

1. Scrivere il flusso di dati del modulo nel browser Web del client

   * Creare un `FormResult` oggetto ottenendo il valore del membro `com.adobe.idp.services.holders.FormsResultHolder` dati dell&#39; `value` oggetto.
   * Creare un `BLOB` oggetto che contenga dati del modulo richiamando il `FormsResult` metodo dell&#39; `getOutputContent` oggetto.
   * Ottenere il tipo di contenuto dell&#39; `BLOB` oggetto richiamandone il `getContentType` metodo.
   * Impostare il tipo di contenuto dell&#39; `javax.servlet.http.HttpServletResponse` oggetto richiamandone `setContentType` il metodo e passando il tipo di contenuto dell&#39; `BLOB` oggetto.
   * Creare un `javax.servlet.ServletOutputStream` oggetto utilizzato per scrivere il flusso di dati del modulo nel browser Web del client richiamando il `javax.servlet.http.HttpServletResponse` metodo dell&#39; `getOutputStream` oggetto.
   * Creare un array di byte e compilarlo richiamando il metodo dell&#39; `BLOB` oggetto `getBinaryData` . Questa attività assegna il contenuto dell&#39; `FormsResult` oggetto all&#39;array di byte.
   * Richiamare il metodo dell&#39; `javax.servlet.http.HttpServletResponse` oggetto `write` per inviare il flusso di dati del modulo al browser Web del client. Passa l&#39;array di byte al `write` metodo.

**Consulta anche**

[Rendering di moduli HTML con file CSS personalizzati](#rendering-html-forms-using-custom-css-files)

[Richiamo di moduli AEM con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
