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
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1682'
ht-degree: 0%

---

# Rendering di HTML Forms tramite file CSS personalizzati {#rendering-html-forms-using-custom-css-files}

**Gli esempi e gli esempi contenuti in questo documento sono solo per l’ambiente AEM Forms su JEE.**

Il servizio Forms esegue il rendering dei moduli HTML in risposta a una richiesta HTTP da un browser web. Durante il rendering di un modulo HTML, il servizio Forms può fare riferimento a un file CSS personalizzato. Puoi creare un file CSS personalizzato per soddisfare i requisiti aziendali e fare riferimento a tale file CSS quando utilizzi il servizio Forms per il rendering dei moduli HTML.

Il servizio Forms analizza automaticamente il file CSS personalizzato. In altre parole, il servizio Forms non segnala gli errori che possono verificarsi se il file CSS personalizzato non è conforme agli standard CSS. In questa situazione, il servizio Forms ignora lo stile e continua con gli stili rimanenti nel file CSS.

L’elenco seguente specifica gli stili supportati in un file CSS personalizzato:

* **Coppie di tipo selettore a livello di classe**: se presenti in un file CSS personalizzato, vengono utilizzati i selettori utilizzati nel modulo HTML come stili di classe. Gli stili di classe non utilizzati vengono ignorati.
* **Coppie stile selettore livello identificatore**: vengono utilizzati tutti gli stili di identificatore, se presenti nel modulo HTML.
* **Coppie stile selettore livello elemento**: vengono utilizzati tutti gli stili di elemento, se presenti nel modulo HTML.
* **Priorità stile**: la priorità di stile (come importante) è supportata e può essere utilizzata in un file CSS personalizzato.
* **Tipo di file multimediale**: una o più coppie in stile selettore possono essere racchiuse in @media stile per definire il tipo di file multimediale. Il servizio Forms non verifica se il tipo di supporto specificato è supportato. Il tipo di file multimediale specificato nel file CSS personalizzato viene unito nel modulo HTML.

È possibile recuperare un file CSS di esempio utilizzando l&#39;applicazione FormsIVS. Caricare il modulo, selezionarlo nella pagina Struttura modulo di prova e fare clic su GeneraCSS. Non è necessario impostare il tipo di trasformazione HTML prima di fare clic sul pulsante. Quindi seleziona Salva. Puoi modificare questo file CSS per soddisfare i requisiti aziendali.

>[!NOTE]
>
>Prima di eseguire il rendering di un modulo di HTML che utilizza un file CSS personalizzato, è importante avere una solida conoscenza del rendering dei moduli di HTML. (vedere [Rendering di Forms come HTML](/help/forms/developing/rendering-forms-html.md).)

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Forms, consulta [Guida di riferimento dei servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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

**Rendering di un modulo HTML**

Per eseguire il rendering di un modulo di HTML, specificare una struttura di modulo creata in Designer e salvata come file XDP. Selezionare un tipo di trasformazione HTML. È ad esempio possibile specificare il tipo di trasformazione HTML che esegue il rendering di un HTML dinamico per Internet Explorer 5.0 o versione successiva.

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

   * Creare un `ServiceClientFactory` oggetto che contiene proprietà di connessione.
   * Creare un `FormsServiceClient` mediante il costruttore e passando il `ServiceClientFactory` oggetto.

1. Fai riferimento al file CSS

   * Creare un `HTMLRenderSpec` mediante il costruttore.
   * Per eseguire il rendering del modulo HTML che utilizza un file CSS personalizzato, richiama `HTMLRenderSpec` dell&#39;oggetto `setCustomCSSURI` e passa un valore stringa che specifica la posizione e il nome del file CSS.

1. Rendering di un modulo HTML

   Richiama `FormsServiceClient` dell&#39;oggetto `(Deprecated) (Deprecated) renderHTMLForm` e trasmettere i seguenti valori:

   * Valore stringa che specifica il nome della struttura del modulo, inclusa l&#39;estensione del nome file. Se si fa riferimento a una struttura di modulo che fa parte di un&#39;applicazione Forms, assicurarsi di specificare il percorso completo, ad esempio `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `TransformTo` valore enum che specifica il tipo di preferenza HTML. Ad esempio, per eseguire il rendering di un modulo di HTML compatibile con dynamic HTML per Internet Explorer 5.0 o versione successiva, specificare `TransformTo.MSDHTML`.
   * A `com.adobe.idp.Document` oggetto contenente dati da unire con il modulo. Se non desideri unire i dati, passa un campo vuoto `com.adobe.idp.Document` oggetto.
   * Il `HTMLRenderSpec` oggetto che memorizza le opzioni di runtime di HTML.
   * Un valore stringa che specifica il `HTTP_USER_AGENT` valore dell’intestazione, come `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
   * A `URLSpec` oggetto che memorizza i valori URI necessari per il rendering di un modulo HTML.
   * A `java.util.HashMap` oggetto che memorizza gli allegati. Questo è un parametro facoltativo e puoi specificare `null` se non si desidera allegare file al modulo.

   Il `(Deprecated) renderHTMLForm` il metodo restituisce un `FormsResult` oggetto contenente un flusso di dati modulo che deve essere scritto nel browser web client.

1. Scrivere il flusso di dati del modulo nel browser Web client

   * Creare un `com.adobe.idp.Document` oggetto richiamando il `FormsResult` dell&#39;oggetto `getOutputContent` metodo.
   * Ottieni il tipo di contenuto del `com.adobe.idp.Document` oggetto richiamando il relativo `getContentType` metodo.
   * Imposta il `javax.servlet.http.HttpServletResponse` tipo di contenuto dell&#39;oggetto richiamando il relativo `setContentType` e passando il tipo di contenuto del `com.adobe.idp.Document` oggetto.
   * Creare un `javax.servlet.ServletOutputStream` oggetto utilizzato per scrivere il flusso di dati del modulo nel browser web client richiamando `javax.servlet.h\ttp.HttpServletResponse` dell&#39;oggetto `getOutputStream` metodo.
   * Creare un `java.io.InputStream` oggetto richiamando il `com.adobe.idp.Document` dell&#39;oggetto `getInputStream` metodo.
   * Creare una matrice di byte e popolarla con il flusso di dati del modulo richiamando `InputStream` dell&#39;oggetto `read` e passando la matrice di byte come argomento.
   * Richiama `javax.servlet.ServletOutputStream` dell&#39;oggetto `write` metodo per inviare il flusso di dati del modulo al browser web client. Passare la matrice di byte al `write` metodo.

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

   Creare un `FormsService` e impostare i valori di autenticazione.

1. Fai riferimento al file CSS

   * Creare un `HTMLRenderSpec` mediante il costruttore.
   * Per eseguire il rendering del modulo HTML che utilizza un file CSS personalizzato, richiama `HTMLRenderSpec` dell&#39;oggetto `setCustomCSSURI` e passa un valore stringa che specifica la posizione e il nome del file CSS.

1. Rendering di un modulo HTML

   Richiama `FormsService` dell&#39;oggetto `(Deprecated) renderHTMLForm` e trasmettere i seguenti valori:

   * Valore stringa che specifica il nome della struttura del modulo, inclusa l&#39;estensione del nome file. Se si fa riferimento a una struttura di modulo che fa parte di un&#39;applicazione Forms, assicurarsi di specificare il percorso completo, ad esempio `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `TransformTo` valore enum che specifica il tipo di preferenza HTML. Ad esempio, per eseguire il rendering di un modulo di HTML compatibile con dynamic HTML per Internet Explorer 5.0 o versione successiva, specificare `TransformTo.MSDHTML`.
   * A `BLOB` oggetto contenente dati da unire con il modulo. Se non si desidera unire i dati, passare `null`. (vedere [Precompilazione di Forms con layout fluibili](/help/forms/developing/prepopulating-forms-flowable-layouts.md).)
   * Il `HTMLRenderSpec` oggetto che memorizza le opzioni di runtime di HTML.
   * Un valore stringa che specifica il `HTTP_USER_AGENT` valore dell’intestazione, come `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`. Se non si desidera impostare questo valore, è possibile passare una stringa vuota.
   * A `URLSpec` oggetto che memorizza i valori URI necessari per il rendering di un modulo HTML.
   * A `java.util.HashMap` oggetto che memorizza gli allegati. Questo è un parametro facoltativo e puoi specificare `null` se non si desidera allegare file al modulo.
   * Un campo vuoto `com.adobe.idp.services.holders.BLOBHolder` oggetto popolato da `(Deprecated) renderHTMLForm` metodo. Questo valore di parametro memorizza il modulo di cui è stato eseguito il rendering.
   * Un campo vuoto `com.adobe.idp.services.holders.BLOBHolder` oggetto popolato da `(Deprecated) renderHTMLForm` metodo. Questo parametro memorizza i dati XML di output.
   * Un campo vuoto `javax.xml.rpc.holders.LongHolder` oggetto popolato da `(Deprecated) renderHTMLForm` metodo. Questo argomento memorizza il numero di pagine nel modulo.
   * Un campo vuoto `javax.xml.rpc.holders.StringHolder` oggetto popolato da `(Deprecated) renderHTMLForm` metodo. Questo argomento memorizza il valore locale.
   * Un campo vuoto `javax.xml.rpc.holders.StringHolder` oggetto popolato da `(Deprecated) renderHTMLForm` metodo. Questo argomento memorizza il valore di rendering HTML utilizzato.
   * Un campo vuoto `com.adobe.idp.services.holders.FormsResultHolder` oggetto che conterrà i risultati dell&#39;operazione.

   Il `(Deprecated) renderHTMLForm` il metodo compila `com.adobe.idp.services.holders.FormsResultHolder` oggetto passato come ultimo valore di argomento con un flusso di dati del modulo che deve essere scritto nel browser web client.

1. Scrivere il flusso di dati del modulo nel browser Web client

   * Creare un `FormResult` dell&#39;oggetto ottenendo il valore del `com.adobe.idp.services.holders.FormsResultHolder` dell&#39;oggetto `value` membro dati.
   * Creare un `BLOB` oggetto che contiene i dati del modulo richiamando `FormsResult` dell&#39;oggetto `getOutputContent` metodo.
   * Ottieni il tipo di contenuto del `BLOB` oggetto richiamando il relativo `getContentType` metodo.
   * Imposta il `javax.servlet.http.HttpServletResponse` tipo di contenuto dell&#39;oggetto richiamando il relativo `setContentType` e passando il tipo di contenuto del `BLOB` oggetto.
   * Creare un `javax.servlet.ServletOutputStream` oggetto utilizzato per scrivere il flusso di dati del modulo nel browser web client richiamando `javax.servlet.http.HttpServletResponse` dell&#39;oggetto `getOutputStream` metodo.
   * Creare una matrice di byte e popolarla richiamando il `BLOB` dell&#39;oggetto `getBinaryData` metodo. Questa attività assegna il contenuto del `FormsResult` alla matrice di byte.
   * Richiama `javax.servlet.http.HttpServletResponse` dell&#39;oggetto `write` metodo per inviare il flusso di dati del modulo al browser web client. Passare la matrice di byte al `write` metodo.

**Consulta anche**

[Rendering di HTML Forms tramite file CSS personalizzati](#rendering-html-forms-using-custom-css-files)

[Richiamare AEM Forms utilizzando la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
