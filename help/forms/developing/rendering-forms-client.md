---
title: Rendering di Forms nel client
description: Ottimizza la distribuzione dei contenuti PDF e migliora la capacità del servizio Forms di gestire il carico di rete utilizzando la funzionalità di rendering lato client di Acrobat o Adobe Reader
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: e485980d-f200-46b7-9284-c9996003aa47
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1690'
ht-degree: 0%

---

# Rendering di Forms nel client {#rendering-forms-at-the-client}

**Gli esempi e gli esempi contenuti in questo documento sono solo per l’ambiente AEM Forms su JEE.**

## Rendering di Forms nel client {#rendering-forms-at-the-client-inner}

Puoi ottimizzare la distribuzione dei contenuti PDF e migliorare la capacità del servizio Forms di gestire il carico di rete utilizzando la funzionalità di rendering lato client di Acrobat o Adobe Reader. Questo processo è noto come rendering di un modulo sul client. Per eseguire il rendering di un modulo sul client, il dispositivo client (in genere un browser web) deve utilizzare Acrobat 7.0 o Adobe Reader 7.0 o versione successiva.

Le modifiche a un modulo risultanti dall’esecuzione di script lato server non vengono applicate a un modulo sottoposto a rendering nel client, a meno che il sottomodulo principale non contenga `restoreState` attributo impostato su `auto`. Per ulteriori informazioni su questo attributo, consulta [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63)

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Forms, consulta [Guida di riferimento dei servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary-of-steps}

Per eseguire il rendering di un modulo sul client, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Crea un oggetto API client di Forms.
1. Impostare le opzioni di runtime di rendering del client.
1. Eseguire il rendering di un modulo nel client.
1. Scrivere il modulo nel browser Web client.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

**Creare un oggetto API client di Forms**

Prima di poter eseguire a livello di programmazione un&#39;operazione API client del servizio Forms, è necessario creare un client del servizio Forms. Se utilizzi l’API Java, crea un’ `FormsServiceClient` oggetto. Se utilizzi l’API del servizio web Forms, crea un’ `FormsService` oggetto.

**Impostare le opzioni di runtime di rendering del client**

Impostare l&#39;opzione di rendering client in fase di esecuzione per eseguire il rendering di un modulo sul client impostando `RenderAtClient` opzione di runtime per `true`. In questo modo il modulo viene consegnato al dispositivo client in cui viene eseguito il rendering. Se `RenderAtClient` è `auto` (valore predefinito), la struttura del modulo determina se il rendering del modulo viene eseguito sul client. La struttura del modulo deve essere una struttura di modulo con un layout scorrevole.

È possibile impostare un&#39;opzione di runtime facoltativa per `SeedPDF` opzione. Il `SeedPDF` combina il contenitore PDF (documento di seed PDF) con la struttura del modulo e i dati XML. Sia la struttura del modulo che i dati XML vengono inviati ad Acrobat o Adobe Reader, dove viene eseguito il rendering del modulo. Il `SeedPDF` L&#39;opzione può essere utilizzata quando il computer client non dispone di tipi di carattere utilizzati nel modulo, ad esempio quando un utente finale non dispone della licenza per utilizzare un tipo di carattere che il proprietario del modulo può utilizzare.

È possibile utilizzare Designer per creare un semplice file di PDF dinamico da utilizzare come file di PDF seed. Per eseguire questa attività sono necessari i seguenti passaggi:

1. Determinare se è necessario incorporare i tipi di carattere nel file di PDF seed. Il file di seed PDF deve contenere i font aggiuntivi richiesti dal modulo sottoposto a rendering. Quando si incorporano font nel file di PDF seed, assicurarsi di non violare alcun contratto di licenza per i font. In Designer, è possibile determinare se è possibile incorporare legalmente i tipi di carattere. Al momento del salvataggio, se sono presenti tipi di carattere che non è possibile incorporare nel modulo, in Designer viene visualizzato un messaggio in cui sono elencati i tipi di carattere che non è possibile incorporare. Questo messaggio non viene visualizzato in Designer per i documenti statici di PDF.
1. Se si sta creando il file di PDF seed in Designer, è consigliabile aggiungere almeno un campo di testo contenente un messaggio. Il messaggio deve essere indirizzato agli utenti delle versioni precedenti di Adobe Reader in cui si dichiara che per visualizzare il documento è necessario Acrobat 7.0 o versione successiva oppure Adobe Reader 7.0 o versione successiva.
1. Salvare il file di seed PDF come file di dynamic PDF con l&#39;estensione PDF.

>[!NOTE]
>
>Non è necessario definire l’opzione runtime di seed PDF per eseguire il rendering di un modulo sul client. Se non specifichi un PDF di seed, il servizio Forms crea un PDF shell che non contiene oggetti COS, ma un wrapper PDF con il contenuto XDP effettivo incorporato all’interno. I passaggi descritti in questa sezione non impostano l&#39;opzione di runtime di seed PDF. Per informazioni sugli oggetti COS, consultate la guida di riferimento di Adobe PDF.

**Eseguire il rendering di un modulo sul client**

Per eseguire il rendering di un modulo sul client, è necessario assicurarsi che le opzioni di runtime di rendering del client siano incluse nella logica dell’applicazione per eseguire il rendering di un modulo.

**Scrivere il flusso di dati del modulo nel browser Web client**

Il servizio Forms crea un flusso di dati modulo che è necessario scrivere nel browser Web client. Quando viene scritto nel browser web client, il modulo viene renderizzato da Acrobat 7.0 o Adobe Reader 7.0 o versione successiva ed è visibile all’utente.

**Consulta anche**

[Eseguire il rendering di un modulo sul client utilizzando l’API Java](#render-a-form-at-the-client-using-the-java-api)

[Eseguire il rendering di un modulo sul client utilizzando l’API del servizio web](#render-a-form-at-the-client-using-the-web-service-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Guida introduttiva all’API di servizio Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Trasmissione di documenti al servizio Forms](/help/forms/developing/passing-documents-forms-service.md)

[Creazione di applicazioni Web per il rendering di Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

### Eseguire il rendering di un modulo sul client utilizzando l’API Java {#render-a-form-at-the-client-using-the-java-api}

Esegui il rendering di un modulo sul client utilizzando l’API Forms (Java):

1. Includi file di progetto

   Includi i file JAR client, ad esempio adobe-forms-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto API client di Forms

   * Creare un `ServiceClientFactory` oggetto che contiene proprietà di connessione.
   * Creare un `FormsServiceClient` mediante il costruttore e passando il `ServiceClientFactory` oggetto.

1. Impostare le opzioni di runtime di rendering del client

   * Creare un `PDFFormRenderSpec` mediante il costruttore.
   * Imposta il `RenderAtClient` runtime richiamando l&#39;opzione `PDFFormRenderSpec` dell&#39;oggetto `setRenderAtClient` e passando il valore enum `RenderAtClient.Yes`.

1. Eseguire il rendering di un modulo sul client

   Richiama `FormsServiceClient` dell&#39;oggetto `renderPDFForm` e trasmettere i seguenti valori:

   * Valore stringa che specifica il nome della struttura del modulo, inclusa l&#39;estensione del nome file. Se si fa riferimento a una progettazione di modulo che fa parte di un&#39;applicazione AEM Forms, assicurarsi di specificare il percorso completo, ad esempio `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `com.adobe.idp.Document` oggetto contenente dati da unire con il modulo. Se non desideri unire i dati, passa un campo vuoto `com.adobe.idp.Document` oggetto.
   * A `PDFFormRenderSpec` oggetto che memorizza le opzioni di runtime necessarie per eseguire il rendering di un modulo sul client.
   * A `URLSpec` oggetto contenente valori URI richiesti dal servizio Forms per il rendering di un modulo.
   * A `java.util.HashMap` oggetto che memorizza gli allegati. Questo è un parametro facoltativo e puoi specificare `null` se non si desidera allegare file al modulo.

   Il `renderPDFForm` il metodo restituisce un `FormsResult` oggetto contenente un flusso di dati modulo che deve essere scritto nel browser web client.

1. Scrivere il flusso di dati del modulo nel browser Web client

   * Creare un `com.adobe.idp.Document` oggetto richiamando il `FormsResult` oggetto &quot;s `getOutputContent` metodo.
   * Ottieni il tipo di contenuto del `com.adobe.idp.Document` oggetto richiamando il relativo `getContentType` metodo.
   * Imposta il `javax.servlet.http.HttpServletResponse` tipo di contenuto dell&#39;oggetto richiamando il relativo `setContentType` e passando il tipo di contenuto del `com.adobe.idp.Document` oggetto.
   * Creare un `javax.servlet.ServletOutputStream` oggetto utilizzato per scrivere il flusso di dati del modulo nel browser web client richiamando `javax.servlet.http.HttpServletResponse` dell&#39;oggetto `getOutputStream` metodo.
   * Creare un `java.io.InputStream` oggetto richiamando il `com.adobe.idp.Document` dell&#39;oggetto `getInputStream` metodo.
   * Creare una matrice di byte e popolarla con il flusso di dati del modulo richiamando `InputStream` dell&#39;oggetto `read` e passando la matrice di byte come argomento.
   * Richiama `javax.servlet.ServletOutputStream` dell&#39;oggetto `write` metodo per inviare il flusso di dati del modulo al browser web client. Passare la matrice di byte al `write` metodo.

**Consulta anche**

[Quick Start (modalità SOAP): rendering di un modulo sul client tramite l’API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-form-at-the-client-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Eseguire il rendering di un modulo sul client utilizzando l’API del servizio web {#render-a-form-at-the-client-using-the-web-service-api}

Esegui il rendering di un modulo sul client utilizzando l’API Forms (servizio web):

1. Includi file di progetto

   * Creare classi proxy Java che utilizzano il servizio Forms WSDL.
   * Includi le classi proxy Java nel percorso della classe.

1. Creare un oggetto API client di Forms

   Creare un `FormsService` e impostare i valori di autenticazione.

1. Impostare le opzioni di runtime di rendering del client

   * Creare un `PDFFormRenderSpec` mediante il costruttore.
   * Imposta il `RenderAtClient` runtime richiamando l&#39;opzione `PDFFormRenderSpec` dell&#39;oggetto `setRenderAtClient` e passando il valore stringa `RenderAtClient.Yes`.

1. Eseguire il rendering di un modulo sul client

   Richiama `FormsService` dell&#39;oggetto `renderPDFForm` e trasmettere i seguenti valori:

   * Valore stringa che specifica il nome della struttura del modulo, inclusa l&#39;estensione del nome file. Se si fa riferimento a una struttura di modulo che fa parte di un&#39;applicazione Forms, assicurarsi di specificare il percorso completo, ad esempio `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `BLOB` oggetto contenente dati da unire con il modulo. Se non si desidera unire i dati, passare `null`. (vedere [Precompilazione di Forms con layout fluibili](/help/forms/developing/prepopulating-forms-flowable-layouts.md).)
   * A `PDFFormRenderSpec` oggetto che memorizza le opzioni di runtime necessarie per eseguire il rendering di un modulo sul client.
   * A `URLSpec` oggetto contenente valori URI richiesti dal servizio Forms.
   * A `java.util.HashMap` oggetto che memorizza gli allegati. Questo è un parametro facoltativo e puoi specificare `null` se non si desidera allegare file al modulo.
   * Un campo vuoto `com.adobe.idp.services.holders.BLOBHolder` oggetto popolato dal metodo. Questo parametro viene utilizzato per memorizzare il modulo PDF di cui è stato eseguito il rendering.
   * Un campo vuoto `javax.xml.rpc.holders.LongHolder` oggetto popolato dal metodo. Questo argomento consente di memorizzare il numero di pagine nel modulo.
   * Un campo vuoto `javax.xml.rpc.holders.StringHolder` oggetto popolato dal metodo. Questo argomento consente di memorizzare il valore delle impostazioni locali.
   * Un campo vuoto `com.adobe.idp.services.holders.FormsResultHolder` oggetto che conterrà i risultati dell&#39;operazione.

   Il `renderPDFForm` il metodo compila `com.adobe.idp.services.holders.FormsResultHolder` oggetto passato come ultimo valore di argomento con un flusso di dati del modulo che deve essere scritto nel browser web client.

1. Scrivere il flusso di dati del modulo nel browser Web client

   * Creare un `FormResult` dell&#39;oggetto ottenendo il valore del `com.adobe.idp.services.holders.FormsResultHolder` dell&#39;oggetto `value` membro dati.
   * Creare un `BLOB` oggetto che contiene i dati del modulo richiamando `FormsResult` dell&#39;oggetto `getOutputContent` metodo.
   * Ottieni il tipo di contenuto del `BLOB` oggetto richiamando il relativo `getContentType` metodo.
   * Imposta il `javax.servlet.http.HttpServletResponse` tipo di contenuto dell&#39;oggetto richiamando il relativo `setContentType` e passando il tipo di contenuto del `BLOB` oggetto.
   * Creare un `javax.servlet.ServletOutputStream` oggetto utilizzato per scrivere il flusso di dati del modulo nel browser web client richiamando `javax.servlet.http.HttpServletResponse` dell&#39;oggetto `getOutputStream` metodo.
   * Creare una matrice di byte e popolarla richiamando il `BLOB` dell&#39;oggetto `getBinaryData` metodo. Questa attività assegna il contenuto del `FormsResult` alla matrice di byte.
   * Richiama `javax.servlet.http.HttpServletResponse` dell&#39;oggetto `write` metodo per inviare il flusso di dati del modulo al browser web client. Passare la matrice di byte al `write` metodo.

**Consulta anche**

[Rendering di Forms nel client](#rendering-forms-at-the-client)

[Richiamare AEM Forms utilizzando la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
