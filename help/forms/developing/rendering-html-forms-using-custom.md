---
title: Rendering di HTML Forms tramite file CSS personalizzati
description: Utilizza il servizio Forms per fare riferimento a file CSS personalizzati per eseguire il rendering di moduli HTML in risposta a una richiesta HTTP da un browser web. Puoi eseguire il rendering di un modulo HTML che utilizza un file CSS utilizzando l’API Java e l’API del servizio web.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 5fa385a7-f030-4c0c-8938-0991d02ef361
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1682'
ht-degree: 0%

---

# Rendering di HTML Forms tramite file CSS personalizzati {#rendering-html-forms-using-custom-css-files}

**Gli esempi e gli esempi contenuti in questo documento sono solo per AEM Forms in ambiente JEE.**

Il servizio Forms esegue il rendering dei moduli HTML in risposta a una richiesta HTTP da un browser web. Durante il rendering di un modulo HTML, il servizio Forms può fare riferimento a un file CSS personalizzato. Puoi creare un file CSS personalizzato per soddisfare i requisiti aziendali e fare riferimento a tale file CSS quando utilizzi il servizio Forms per il rendering dei moduli HTML.

Il servizio Forms analizza automaticamente il file CSS personalizzato. In altre parole, il servizio Forms non segnala gli errori che possono verificarsi se il file CSS personalizzato non è conforme agli standard CSS. In questa situazione, il servizio Forms ignora lo stile e continua con gli stili rimanenti nel file CSS.

L’elenco seguente specifica gli stili supportati in un file CSS personalizzato:

* **Coppie di stile selettore a livello di classe**: se presenti in un file CSS personalizzato, vengono utilizzati i selettori utilizzati nel modulo HTML come stili di classe. Gli stili di classe non utilizzati vengono ignorati.
* **Coppie di tipo selettore a livello di identificatore**: vengono utilizzati tutti gli stili di identificatore se utilizzati nel modulo HTML.
* **Coppie di stile selettore a livello di elemento**: vengono utilizzati tutti gli stili di elemento se utilizzati nel modulo HTML.
* **Priorità stile**: priorità stile (come importante) supportata e utilizzabile in un file CSS personalizzato.
* **Tipo di file multimediale**: è possibile racchiudere una o più coppie di tipo selettore in @media stile per definire il tipo di file multimediale. Il servizio Forms non verifica se il tipo di supporto specificato è supportato. Il tipo di file multimediale specificato nel file CSS personalizzato viene unito nel modulo HTML.

È possibile recuperare un file CSS di esempio utilizzando l&#39;applicazione FormsIVS. Caricare il modulo, selezionarlo nella pagina Struttura modulo di prova e fare clic su GeneraCSS. Non è necessario impostare il tipo di trasformazione HTML prima di fare clic sul pulsante. Quindi seleziona Salva. Puoi modificare questo file CSS per soddisfare i requisiti aziendali.

>[!NOTE]
>
>Prima di eseguire il rendering di un modulo di HTML che utilizza un file CSS personalizzato, è importante avere una solida conoscenza del rendering dei moduli di HTML. (Vedi [Rendering di Forms come HTML](/help/forms/developing/rendering-forms-html.md).)

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Forms, vedere [Riferimento ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Riepilogo dei passaggi {#summary-of-steps}

Per eseguire il rendering di un modulo HTML che utilizza un file CSS, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Crea un oggetto API Java di Forms.
1. Fai riferimento al file CSS.
1. Eseguire il rendering di un modulo HTML.
1. Scrivere il flusso di dati del modulo nel browser Web client.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

**Creare un oggetto API Java di Forms**

Prima di poter eseguire a livello di programmazione un&#39;operazione supportata dal servizio Forms, è necessario creare un oggetto client Forms.

**Fai riferimento al file CSS**

Per eseguire il rendering di un modulo HTML che utilizza un file CSS personalizzato, accertati di fare riferimento a un file CSS esistente.

**Eseguire il rendering di un modulo HTML**

Per eseguire il rendering di un modulo HTML, specifica una struttura di modulo creata in Designer e salvata come file XDP. Selezionare un tipo di trasformazione HTML. È ad esempio possibile specificare il tipo di trasformazione HTML che esegue il rendering di un HTML dinamico per Internet Explorer 5.0 o versione successiva.

Il rendering di un modulo HTML richiede anche valori, come i valori URI necessari per il rendering di altri tipi di modulo.

**Scrivere il flusso di dati del modulo nel browser Web client**

Quando il servizio Forms esegue il rendering di un modulo HTML, restituisce un flusso di dati del modulo che è necessario scrivere nel browser Web client per rendere il modulo HTML visibile all&#39;utente.

**Consulta anche**

[Eseguire il rendering di un modulo HTML che utilizza un file CSS utilizzando l’API Java](#render-an-html-form-that-uses-a-css-file-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Guida introduttiva all’API di servizio Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Rendering dei PDF forms interattivi](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Rendering di Forms come HTML](/help/forms/developing/rendering-forms-html.md)

[Creazione di applicazioni Web per il rendering di Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

## Eseguire il rendering di un modulo HTML che utilizza un file CSS utilizzando l’API Java {#render-an-html-form-that-uses-a-css-file-using-the-java-api}

Esegui il rendering di un modulo HTML che utilizza un file CSS personalizzato utilizzando l’API Forms (Java):

1. Includi file di progetto

   Includi i file JAR client, ad esempio adobe-forms-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto API Java di Forms

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `FormsServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Fai riferimento al file CSS

   * Creare un oggetto `HTMLRenderSpec` utilizzando il relativo costruttore.
   * Per eseguire il rendering del modulo HTML che utilizza un file CSS personalizzato, richiamare il metodo `setCustomCSSURI` dell&#39;oggetto `HTMLRenderSpec` e passare un valore stringa che specifichi la posizione e il nome del file CSS.

1. Rendering di un modulo HTML

   Richiama il metodo `(Deprecated) (Deprecated) renderHTMLForm` dell&#39;oggetto `FormsServiceClient` e passa i seguenti valori:

   * Valore stringa che specifica il nome della struttura del modulo, inclusa l&#39;estensione del nome file. Se si fa riferimento a una struttura di modulo che fa parte di un&#39;applicazione Forms, assicurarsi di specificare il percorso completo, ad esempio `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Valore enum `TransformTo` che specifica il tipo di preferenza HTML. Per eseguire, ad esempio, il rendering di un modulo di HTML compatibile con dynamic HTML per Internet Explorer 5.0 o versione successiva, specificare `TransformTo.MSDHTML`.
   * Oggetto `com.adobe.idp.Document` contenente dati da unire al modulo. Se non si desidera unire i dati, passare un oggetto `com.adobe.idp.Document` vuoto.
   * L&#39;oggetto `HTMLRenderSpec` che memorizza le opzioni di runtime di HTML.
   * Valore stringa che specifica il valore dell&#39;intestazione `HTTP_USER_AGENT`, ad esempio `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
   * Oggetto `URLSpec` che memorizza i valori URI necessari per il rendering di un modulo HTML.
   * Oggetto `java.util.HashMap` che memorizza gli allegati. Questo è un parametro facoltativo ed è possibile specificare `null` se non si desidera allegare file al modulo.

   Il metodo `(Deprecated) renderHTMLForm` restituisce un oggetto `FormsResult` che contiene un flusso di dati del modulo che deve essere scritto nel browser Web client.

1. Scrivere il flusso di dati del modulo nel browser Web client

   * Creare un oggetto `com.adobe.idp.Document` richiamando il metodo `getOutputContent` dell&#39;oggetto `FormsResult`.
   * Ottenere il tipo di contenuto dell&#39;oggetto `com.adobe.idp.Document` richiamando il relativo metodo `getContentType`.
   * Impostare il tipo di contenuto dell&#39;oggetto `javax.servlet.http.HttpServletResponse` richiamando il relativo metodo `setContentType` e passando il tipo di contenuto dell&#39;oggetto `com.adobe.idp.Document`.
   * Creare un oggetto `javax.servlet.ServletOutputStream` utilizzato per scrivere il flusso di dati del modulo nel browser Web client richiamando il metodo `getOutputStream` dell&#39;oggetto `javax.servlet.h\ttp.HttpServletResponse`.
   * Creare un oggetto `java.io.InputStream` richiamando il metodo `getInputStream` dell&#39;oggetto `com.adobe.idp.Document`.
   * Creare una matrice di byte e popolarla con il flusso di dati del modulo richiamando il metodo `read` dell&#39;oggetto `InputStream` e passando la matrice di byte come argomento.
   * Richiama il metodo `write` dell&#39;oggetto `javax.servlet.ServletOutputStream` per inviare il flusso di dati del modulo al browser Web client. Passare la matrice di byte al metodo `write`.

**Consulta anche**

[Rendering di HTML Forms tramite file CSS personalizzati](#rendering-html-forms-using-custom-css-files)

[Quick Start (modalità SOAP): rendering di un modulo HTML che utilizza un file CSS utilizzando l’API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-that-uses-a-css-file-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Eseguire il rendering di un modulo HTML che utilizza un file CSS utilizzando l’API del servizio web {#render-an-html-form-that-uses-a-css-file-using-the-web-service-api}

Esegui il rendering di un modulo HTML che utilizza un file CSS personalizzato utilizzando l’API Forms (servizio web):

1. Includi file di progetto

   * Creare classi proxy Java che utilizzano il servizio Forms WSDL.
   * Includi le classi proxy Java nel percorso della classe.

1. Creare un oggetto API Java di Forms

   Creare un oggetto `FormsService` e impostare i valori di autenticazione.

1. Fai riferimento al file CSS

   * Creare un oggetto `HTMLRenderSpec` utilizzando il relativo costruttore.
   * Per eseguire il rendering del modulo HTML che utilizza un file CSS personalizzato, richiamare il metodo `setCustomCSSURI` dell&#39;oggetto `HTMLRenderSpec` e passare un valore stringa che specifichi la posizione e il nome del file CSS.

1. Rendering di un modulo HTML

   Richiama il metodo `(Deprecated) renderHTMLForm` dell&#39;oggetto `FormsService` e passa i seguenti valori:

   * Valore stringa che specifica il nome della struttura del modulo, inclusa l&#39;estensione del nome file. Se si fa riferimento a una struttura di modulo che fa parte di un&#39;applicazione Forms, assicurarsi di specificare il percorso completo, ad esempio `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Valore enum `TransformTo` che specifica il tipo di preferenza HTML. Per eseguire, ad esempio, il rendering di un modulo di HTML compatibile con dynamic HTML per Internet Explorer 5.0 o versione successiva, specificare `TransformTo.MSDHTML`.
   * Oggetto `BLOB` contenente dati da unire al modulo. Se non si desidera unire i dati, passare `null`. (Vedi [Precompilazione di Forms con layout percorribili](/help/forms/developing/prepopulating-forms-flowable-layouts.md).)
   * L&#39;oggetto `HTMLRenderSpec` che memorizza le opzioni di runtime di HTML.
   * Valore stringa che specifica il valore dell&#39;intestazione `HTTP_USER_AGENT`, ad esempio `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`. Se non si desidera impostare questo valore, è possibile passare una stringa vuota.
   * Oggetto `URLSpec` che memorizza i valori URI necessari per il rendering di un modulo HTML.
   * Oggetto `java.util.HashMap` che memorizza gli allegati. Questo è un parametro facoltativo ed è possibile specificare `null` se non si desidera allegare file al modulo.
   * Oggetto `com.adobe.idp.services.holders.BLOBHolder` vuoto popolato dal metodo `(Deprecated) renderHTMLForm`. Questo valore di parametro memorizza il modulo di cui è stato eseguito il rendering.
   * Oggetto `com.adobe.idp.services.holders.BLOBHolder` vuoto popolato dal metodo `(Deprecated) renderHTMLForm`. Questo parametro memorizza i dati XML di output.
   * Oggetto `javax.xml.rpc.holders.LongHolder` vuoto popolato dal metodo `(Deprecated) renderHTMLForm`. Questo argomento memorizza il numero di pagine nel modulo.
   * Oggetto `javax.xml.rpc.holders.StringHolder` vuoto popolato dal metodo `(Deprecated) renderHTMLForm`. Questo argomento memorizza il valore locale.
   * Oggetto `javax.xml.rpc.holders.StringHolder` vuoto popolato dal metodo `(Deprecated) renderHTMLForm`. Questo argomento memorizza il valore di rendering HTML utilizzato.
   * Oggetto `com.adobe.idp.services.holders.FormsResultHolder` vuoto che conterrà i risultati dell&#39;operazione.

   Il metodo `(Deprecated) renderHTMLForm` popola l&#39;oggetto `com.adobe.idp.services.holders.FormsResultHolder` passato come ultimo valore di argomento con un flusso di dati del modulo che deve essere scritto nel browser Web client.

1. Scrivere il flusso di dati del modulo nel browser Web client

   * Creare un oggetto `FormResult` ottenendo il valore del membro dati `value` dell&#39;oggetto `com.adobe.idp.services.holders.FormsResultHolder`.
   * Creare un oggetto `BLOB` contenente dati del modulo richiamando il metodo `getOutputContent` dell&#39;oggetto `FormsResult`.
   * Ottenere il tipo di contenuto dell&#39;oggetto `BLOB` richiamando il relativo metodo `getContentType`.
   * Impostare il tipo di contenuto dell&#39;oggetto `javax.servlet.http.HttpServletResponse` richiamando il relativo metodo `setContentType` e passando il tipo di contenuto dell&#39;oggetto `BLOB`.
   * Creare un oggetto `javax.servlet.ServletOutputStream` utilizzato per scrivere il flusso di dati del modulo nel browser Web client richiamando il metodo `getOutputStream` dell&#39;oggetto `javax.servlet.http.HttpServletResponse`.
   * Creare una matrice di byte e popolarla richiamando il metodo `getBinaryData` dell&#39;oggetto `BLOB`. Questa attività assegna il contenuto dell&#39;oggetto `FormsResult` alla matrice di byte.
   * Richiama il metodo `write` dell&#39;oggetto `javax.servlet.http.HttpServletResponse` per inviare il flusso di dati del modulo al browser Web client. Passare la matrice di byte al metodo `write`.

**Consulta anche**

[Rendering di HTML Forms tramite file CSS personalizzati](#rendering-html-forms-using-custom-css-files)

[Richiamare AEM Forms utilizzando la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
