---
title: Rendering HTML Forms con file CSS personalizzati
seo-title: Rendering HTML Forms con file CSS personalizzati
description: Utilizzare il servizio Forms per fare riferimento a file CSS personalizzati per eseguire il rendering dei moduli HTML in risposta a una richiesta HTTP da parte di un browser Web. È possibile eseguire il rendering di un modulo HTML che utilizza un file CSS utilizzando l'API Java e l'API del servizio Web.
seo-description: Utilizzare il servizio Forms per fare riferimento a file CSS personalizzati per eseguire il rendering dei moduli HTML in risposta a una richiesta HTTP da parte di un browser Web. È possibile eseguire il rendering di un modulo HTML che utilizza un file CSS utilizzando l'API Java e l'API del servizio Web.
uuid: a44e96f1-001d-48a2-8c96-15cb9d0c71b3
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 8fe7c072-7df0-44b7-92d0-bf39dc1e688a
translation-type: tm+mt
source-git-commit: 07889ead2ae402b5fb738ca08c7efe076ef33e44
workflow-type: tm+mt
source-wordcount: '1724'
ht-degree: 0%

---


# Rendering HTML Forms con file CSS personalizzati {#rendering-html-forms-using-custom-css-files}

Il servizio Forms esegue il rendering dei moduli HTML in risposta a una richiesta HTTP inviata da un browser Web. Durante il rendering di un modulo HTML, il servizio Forms può fare riferimento a un file CSS personalizzato. È possibile creare un file CSS personalizzato per soddisfare i requisiti aziendali e fare riferimento a tale file CSS quando si utilizza il servizio Forms per eseguire il rendering dei moduli HTML.

Il servizio Forms analizza in modo invisibile il file CSS personalizzato. In altre parole, il servizio Forms non segnala errori che potrebbero verificarsi se il file CSS personalizzato non è conforme agli standard CSS. In questa situazione, il servizio Forms ignora lo stile e continua con gli stili rimanenti che si trovano nel file CSS.

L&#39;elenco seguente specifica gli stili supportati in un file CSS personalizzato:

* **Coppie** stile selettore a livello di classe: Se presente in un file CSS personalizzato, vengono utilizzati i selettori utilizzati nel modulo HTML come stili di classe. Gli stili di classe non utilizzati vengono ignorati.
* **Coppie** stile selettore a livello di identificatore: Tutti gli stili di identificatore vengono utilizzati se usati nel modulo HTML.
* **Coppie** stile selettore livello elemento: Tutti gli stili di elemento vengono utilizzati se utilizzati nel modulo HTML.
* **Priorità** stile: La priorità di stile (come importante) è supportata e può essere utilizzata in un file CSS personalizzato.
* **Tipo** di supporto: Per definire il tipo di supporto, è possibile racchiudere una o più coppie di stile selettore nello stile @media. Il servizio Forms non verifica se il tipo di supporto specificato è supportato. Il tipo di supporto specificato nel file CSS personalizzato viene unito nel modulo HTML.

È possibile recuperare un file CSS di esempio utilizzando l&#39;applicazione FormsIVS. Caricate il modulo, selezionatelo nella pagina Struttura del modulo di prova e fate clic su GeneraCSS. Non è necessario impostare il tipo di trasformazione HTML prima di fare clic sul pulsante. Selezionare Salva. Potete modificare questo file CSS per soddisfare i vostri requisiti aziendali.

>[!NOTE]
>
>Prima di eseguire il rendering di un modulo HTML che utilizza un file CSS personalizzato, è importante avere una conoscenza approfondita del rendering dei moduli HTML. (Vedere [Rendering di Forms come HTML](/help/forms/developing/rendering-forms-html.md).)

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Forms, vedere [Guida di riferimento dei servizi per  AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Riepilogo dei passaggi {#summary-of-steps}

Per eseguire il rendering di un modulo HTML che utilizza un file CSS, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un oggetto Forms Java API.
1. Fate riferimento al file CSS.
1. Eseguire il rendering di un modulo HTML.
1. Scrivere il flusso di dati del modulo nel browser Web del client.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, accertatevi di includere i file proxy.

**Creare un oggetto API Forms Java**

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

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido di Forms Service API](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Rendering di PDF forms interattivi](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Rendering di Forms come HTML](/help/forms/developing/rendering-forms-html.md)

[Creazione di applicazioni Web per il rendering di Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

## Eseguire il rendering di un modulo HTML che utilizza un file CSS utilizzando l&#39;API Java {#render-an-html-form-that-uses-a-css-file-using-the-java-api}

Eseguire il rendering di un modulo HTML che utilizza un file CSS personalizzato utilizzando l&#39;API Forms (Java):

1. Includi file di progetto

   Includete file JAR client, ad esempio adobe-forms-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto API Forms Java

   * Creare un oggetto `ServiceClientFactory` che contiene le proprietà di connessione.
   * Creare un oggetto `FormsServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Riferimento al file CSS

   * Creare un oggetto `HTMLRenderSpec` utilizzando il relativo costruttore.
   * Per eseguire il rendering del modulo HTML che utilizza un file CSS personalizzato, richiamare il metodo `HTMLRenderSpec` dell&#39;oggetto &lt;a1/> e passare un valore di stringa che specifica la posizione e il nome del file CSS.`setCustomCSSURI`

1. Eseguire il rendering di un modulo HTML

   Richiamare il metodo `FormsServiceClient` dell&#39;oggetto `(Deprecated) (Deprecated) renderHTMLForm` e trasmettere i seguenti valori:

   * Una stringa che specifica il nome della struttura del modulo, inclusa l&#39;estensione del nome file. Se si fa riferimento a una struttura del modulo che fa parte di un&#39;applicazione Forms, è necessario specificare il percorso completo, ad esempio `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Un valore enum `TransformTo` che specifica il tipo di preferenza HTML. Ad esempio, per eseguire il rendering di un modulo HTML compatibile con HTML dinamico per Internet Explorer 5.0 o versione successiva, specificare `TransformTo.MSDHTML`.
   * Un oggetto `com.adobe.idp.Document` che contiene i dati da unire al modulo. Se non si desidera unire i dati, passare un oggetto `com.adobe.idp.Document` vuoto.
   * L&#39;oggetto `HTMLRenderSpec` che memorizza le opzioni di runtime HTML.
   * Un valore di stringa che specifica il valore dell&#39;intestazione `HTTP_USER_AGENT`, ad esempio `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
   * Un oggetto `URLSpec` che memorizza i valori URI richiesti per eseguire il rendering di un modulo HTML.
   * Un oggetto `java.util.HashMap` che memorizza gli allegati. Si tratta di un parametro facoltativo e è possibile specificare `null` se non si desidera allegare file al modulo.

   Il metodo `(Deprecated) renderHTMLForm` restituisce un oggetto `FormsResult` contenente un flusso di dati del modulo che deve essere scritto nel browser Web del client.

1. Scrivere il flusso di dati del modulo nel browser Web del client

   * Creare un oggetto `com.adobe.idp.Document` richiamando il metodo `FormsResult` object ‘s `getOutputContent`.
   * Ottenere il tipo di contenuto dell&#39;oggetto `com.adobe.idp.Document` richiamandone il metodo `getContentType`.
   * Impostare il tipo di contenuto dell&#39;oggetto `javax.servlet.http.HttpServletResponse` richiamandone il metodo `setContentType` e passando il tipo di contenuto dell&#39;oggetto `com.adobe.idp.Document`.
   * Creare un oggetto `javax.servlet.ServletOutputStream` utilizzato per scrivere il flusso di dati del modulo nel browser Web del client richiamando il metodo `javax.servlet.h\ttp.HttpServletResponse` dell&#39;oggetto `getOutputStream`.
   * Creare un oggetto `java.io.InputStream` richiamando il metodo `com.adobe.idp.Document` dell&#39;oggetto `getInputStream`.
   * Creare un array di byte e compilarlo con il flusso di dati del modulo richiamando il metodo `InputStream` dell&#39;oggetto `read` e passando l&#39;array di byte come argomento.
   * Richiamare il metodo `javax.servlet.ServletOutputStream` dell&#39;oggetto `write` per inviare il flusso di dati del modulo al browser Web del client. Passate l&#39;array di byte al metodo `write`.

**Consulta anche**

[Rendering HTML Forms con file CSS personalizzati](#rendering-html-forms-using-custom-css-files)

[Avvio rapido (modalità SOAP): Rendering di un modulo HTML che utilizza un file CSS utilizzando l&#39;API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-that-uses-a-css-file-using-the-java-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Eseguire il rendering di un modulo HTML che utilizza un file CSS utilizzando l&#39;API del servizio Web {#render-an-html-form-that-uses-a-css-file-using-the-web-service-api}

Eseguire il rendering di un modulo HTML che utilizza un file CSS personalizzato utilizzando l&#39;API di Forms (servizio Web):

1. Includi file di progetto

   * Creare classi proxy Java che utilizzano il servizio WSDL di Forms.
   * Includete le classi proxy Java nel percorso della classe.

1. Creare un oggetto API Forms Java

   Creare un oggetto `FormsService` e impostare i valori di autenticazione.

1. Riferimento al file CSS

   * Creare un oggetto `HTMLRenderSpec` utilizzando il relativo costruttore.
   * Per eseguire il rendering del modulo HTML che utilizza un file CSS personalizzato, richiamare il metodo `HTMLRenderSpec` dell&#39;oggetto &lt;a1/> e passare un valore di stringa che specifica la posizione e il nome del file CSS.`setCustomCSSURI`

1. Eseguire il rendering di un modulo HTML

   Richiamare il metodo `FormsService` dell&#39;oggetto `(Deprecated) renderHTMLForm` e trasmettere i seguenti valori:

   * Una stringa che specifica il nome della struttura del modulo, inclusa l&#39;estensione del nome file. Se si fa riferimento a una struttura del modulo che fa parte di un&#39;applicazione Forms, è necessario specificare il percorso completo, ad esempio `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Un valore enum `TransformTo` che specifica il tipo di preferenza HTML. Ad esempio, per eseguire il rendering di un modulo HTML compatibile con HTML dinamico per Internet Explorer 5.0 o versione successiva, specificare `TransformTo.MSDHTML`.
   * Un oggetto `BLOB` che contiene i dati da unire al modulo. Se non si desidera unire i dati, passare `null`. (Vedere [Precompilazione di Forms con layout scorrevoli](/help/forms/developing/prepopulating-forms-flowable-layouts.md).)
   * L&#39;oggetto `HTMLRenderSpec` che memorizza le opzioni di runtime HTML.
   * Un valore di stringa che specifica il valore dell&#39;intestazione `HTTP_USER_AGENT`, ad esempio `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`. Se non si desidera impostare questo valore, è possibile passare una stringa vuota.
   * Un oggetto `URLSpec` che memorizza i valori URI richiesti per eseguire il rendering di un modulo HTML.
   * Un oggetto `java.util.HashMap` che memorizza gli allegati. Si tratta di un parametro facoltativo e è possibile specificare `null` se non si desidera allegare file al modulo.
   * Un oggetto `com.adobe.idp.services.holders.BLOBHolder` vuoto compilato dal metodo `(Deprecated) renderHTMLForm`. Questo valore del parametro memorizza il modulo di cui è stato effettuato il rendering.
   * Un oggetto `com.adobe.idp.services.holders.BLOBHolder` vuoto compilato dal metodo `(Deprecated) renderHTMLForm`. Questo parametro memorizza i dati XML di output.
   * Un oggetto `javax.xml.rpc.holders.LongHolder` vuoto compilato dal metodo `(Deprecated) renderHTMLForm`. Questo argomento memorizza il numero di pagine nel modulo.
   * Un oggetto `javax.xml.rpc.holders.StringHolder` vuoto compilato dal metodo `(Deprecated) renderHTMLForm`. Questo argomento memorizza il valore delle impostazioni internazionali.
   * Un oggetto `javax.xml.rpc.holders.StringHolder` vuoto compilato dal metodo `(Deprecated) renderHTMLForm`. Questo argomento memorizza il valore di rendering HTML utilizzato.
   * Un oggetto `com.adobe.idp.services.holders.FormsResultHolder` vuoto che conterrà i risultati dell&#39;operazione.

   Il metodo `(Deprecated) renderHTMLForm` compila l&#39;oggetto `com.adobe.idp.services.holders.FormsResultHolder` passato come ultimo valore argomento con un flusso di dati del modulo che deve essere scritto nel browser Web del client.

1. Scrivere il flusso di dati del modulo nel browser Web del client

   * Creare un oggetto `FormResult` ottenendo il valore del membro di dati `com.adobe.idp.services.holders.FormsResultHolder` dell&#39;oggetto `value`.
   * Creare un oggetto `BLOB` contenente dati del modulo richiamando il metodo `FormsResult` dell&#39;oggetto `getOutputContent`.
   * Ottenere il tipo di contenuto dell&#39;oggetto `BLOB` richiamandone il metodo `getContentType`.
   * Impostare il tipo di contenuto dell&#39;oggetto `javax.servlet.http.HttpServletResponse` richiamandone il metodo `setContentType` e passando il tipo di contenuto dell&#39;oggetto `BLOB`.
   * Creare un oggetto `javax.servlet.ServletOutputStream` utilizzato per scrivere il flusso di dati del modulo nel browser Web del client richiamando il metodo `javax.servlet.http.HttpServletResponse` dell&#39;oggetto `getOutputStream`.
   * Creare un array di byte e compilarlo richiamando il metodo `BLOB` dell&#39;oggetto `getBinaryData`. Questa attività assegna il contenuto dell&#39;oggetto `FormsResult` all&#39;array di byte.
   * Richiamare il metodo `javax.servlet.http.HttpServletResponse` dell&#39;oggetto `write` per inviare il flusso di dati del modulo al browser Web del client. Passate l&#39;array di byte al metodo `write`.

**Consulta anche**

[Rendering HTML Forms con file CSS personalizzati](#rendering-html-forms-using-custom-css-files)

[Richiamo  AEM Forms con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
