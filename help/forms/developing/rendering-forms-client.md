---
title: Rendering di Forms sul client
seo-title: Rendering Forms at the Client
description: Ottimizza la distribuzione del contenuto PDF e migliora la capacità del servizio Forms di gestire il carico di rete utilizzando la funzionalità di rendering lato client di Acrobat o Adobe Reader
seo-description: Optimize the delivery of PDF content and improve the Forms service’s ability to handle network load by using the client-side rendering capability of Acrobat or Adobe Reader
uuid: 09bcc23d-28b0-473a-87f1-bc17e87620f4
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 08d36e9f-cafc-478e-9781-8fc29ac6262e
role: Developer
exl-id: e485980d-f200-46b7-9284-c9996003aa47
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1698'
ht-degree: 0%

---

# Rendering di Forms sul client {#rendering-forms-at-the-client}

**Esempi ed esempi in questo documento sono solo per AEM Forms in ambiente JEE.**

## Rendering di Forms sul client {#rendering-forms-at-the-client-inner}

Puoi ottimizzare la distribuzione dei contenuti di PDF e migliorare la capacità del servizio Forms di gestire il carico di rete utilizzando la funzionalità di rendering lato client di Acrobat o Adobe Reader. Questo processo è noto come rendering di un modulo sul client. Per eseguire il rendering di un modulo sul client, il dispositivo client (in genere un browser Web) deve utilizzare Acrobat 7.0 o Adobe Reader 7.0 o versione successiva.

Le modifiche a un modulo risultanti dall’esecuzione di script sul lato server non vengono applicate a un modulo di cui è eseguito il rendering sul client, a meno che il sottomodulo principale non contenga `restoreState` attributo impostato su `auto`. Per ulteriori informazioni su questo attributo, consulta [Forms Designer.](https://www.adobe.com/go/learn_aemforms_designer_63)

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Forms, vedi [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary-of-steps}

Per eseguire il rendering di un modulo sul client, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Creare un oggetto API client Forms.
1. Imposta le opzioni di esecuzione del rendering client.
1. Eseguire il rendering di un modulo sul client.
1. Scrivere il modulo sul browser Web client.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

**Creare un oggetto API client Forms**

Prima di poter eseguire programmaticamente un’operazione API client del servizio Forms, è necessario creare un client di servizio Forms. Se utilizzi l’API Java, crea un `FormsServiceClient` oggetto. Se utilizzi l’API del servizio Web Forms, crea un `FormsService` oggetto.

**Impostare le opzioni di esecuzione del rendering client**

È necessario impostare l’opzione di esecuzione del rendering del client per eseguire il rendering di un modulo sul client impostando il `RenderAtClient` opzione di esecuzione su `true`. In questo modo il modulo viene consegnato al dispositivo client in cui viene eseguito il rendering. Se `RenderAtClient` è `auto` (valore predefinito), la struttura del modulo determina se eseguire il rendering del modulo sul client. La struttura del modulo deve essere una struttura del modulo con un layout scorrevole.

Un&#39;opzione opzionale di runtime che è possibile impostare è la variabile `SeedPDF` opzione . La `SeedPDF` combina il contenitore PDF (documento PDF di seed) con la struttura del modulo e i dati XML. Sia la struttura del modulo che i dati XML vengono inviati ad Acrobat o Adobe Reader, dove viene eseguito il rendering del modulo. La `SeedPDF` è possibile utilizzare questa opzione quando nel computer client non sono presenti font utilizzati nel modulo, ad esempio quando un utente finale non dispone di una licenza per utilizzare un font concesso in licenza al proprietario del modulo.

Designer consente di creare un semplice file PDF dinamico da utilizzare come file PDF di seed. Per eseguire questa attività sono necessari i seguenti passaggi:

1. Stabilire se è necessario incorporare font all’interno del file PDF seed. Il file seed PDF dovrà contenere font aggiuntivi richiesti dal modulo di cui si sta eseguendo il rendering. Quando incorpori font nel file PDF di seed, assicurati di non violare alcun contratto di licenza per font. In Designer è possibile determinare se è possibile incorporare legalmente i font. Al momento del salvataggio, se non è possibile incorporare font nel modulo, in Designer viene visualizzato un messaggio in cui sono elencati i font che non è possibile incorporare. Questo messaggio non viene visualizzato in Designer per i documenti PDF statici.
1. Se si sta creando il file PDF di seed in Designer, è consigliabile aggiungere almeno un campo di testo contenente un messaggio. Il messaggio deve essere indirizzato agli utenti delle versioni precedenti di Adobe Reader, dichiarando che per visualizzare il documento è necessario Acrobat 7.0 o versioni successive o Adobe Reader 7.0 o versioni successive.
1. Salva il file PDF di seed come file PDF dinamico con l’estensione del nome file PDF.

>[!NOTE]
>
>Non è necessario definire l’opzione di esecuzione di PDF seed per eseguire il rendering di un modulo sul client. Se non si specifica un PDF seed, il servizio Forms crea un file pdf shell che non contiene oggetti COS ma contiene un wrapper PDF con il contenuto XDP effettivo incorporato all&#39;interno. I passaggi di questa sezione non impostano l’opzione di esecuzione di PDF seed. Per informazioni sugli oggetti COS, consulta la guida di riferimento Adobe PDF .

**Eseguire il rendering di un modulo sul client**

Per eseguire il rendering di un modulo sul client, è necessario assicurarsi che le opzioni di esecuzione del rendering client siano incluse nella logica dell’applicazione per il rendering di un modulo.

**Scrivere il flusso di dati del modulo sul browser Web client**

Il servizio Forms crea un flusso di dati del modulo che è necessario scrivere nel browser Web client. Una volta scritto nel browser Web client, il modulo viene sottoposto a rendering da Acrobat 7.0 o Adobe Reader 7.0 o versione successiva ed è visibile all’utente.

**Consulta anche**

[Eseguire il rendering di un modulo sul client utilizzando l’API Java](#render-a-form-at-the-client-using-the-java-api)

[Eseguire il rendering di un modulo sul client utilizzando l’API del servizio Web](#render-a-form-at-the-client-using-the-web-service-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API di Forms Service](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Trasmissione di documenti al servizio Forms](/help/forms/developing/passing-documents-forms-service.md)

[Creazione di applicazioni Web per il rendering di Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

### Eseguire il rendering di un modulo sul client utilizzando l’API Java {#render-a-form-at-the-client-using-the-java-api}

Eseguire il rendering di un modulo sul client utilizzando l’API Forms (Java):

1. Includi file di progetto

   Includi file JAR client, come adobe-forms-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto API client Forms

   * Crea un `ServiceClientFactory` oggetto contenente le proprietà di connessione.
   * Crea un `FormsServiceClient` utilizzando il relativo costruttore e passando `ServiceClientFactory` oggetto.

1. Impostare le opzioni di esecuzione del rendering client

   * Crea un `PDFFormRenderSpec` utilizzando il relativo costruttore.
   * Imposta la `RenderAtClient` opzione di esecuzione richiamando il `PDFFormRenderSpec` dell’oggetto `setRenderAtClient` e passando il valore enum `RenderAtClient.Yes`.

1. Eseguire il rendering di un modulo sul client

   Richiama il `FormsServiceClient` dell’oggetto `renderPDFForm` e passare i seguenti valori:

   * Valore stringa che specifica il nome della struttura del modulo, inclusa l&#39;estensione del nome file. Se si fa riferimento a una struttura del modulo che fa parte di un’applicazione AEM Forms, verificare di specificare il percorso completo, ad esempio `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `com.adobe.idp.Document` oggetto contenente i dati da unire al modulo. Se non si desidera unire i dati, passare un valore vuoto `com.adobe.idp.Document` oggetto.
   * A `PDFFormRenderSpec` oggetto che memorizza le opzioni di esecuzione necessarie per eseguire il rendering di un modulo sul client.
   * A `URLSpec` oggetto contenente valori URI richiesti dal servizio Forms per il rendering di un modulo.
   * A `java.util.HashMap` oggetto che memorizza gli allegati di file. Si tratta di un parametro facoltativo ed è possibile specificare `null` se non si desidera allegare file al modulo.

   La `renderPDFForm` restituisce un `FormsResult` oggetto che contiene un flusso di dati del modulo che deve essere scritto nel browser Web client.

1. Scrivere il flusso di dati del modulo sul browser Web client

   * Crea un `com.adobe.idp.Document` richiamando l&#39;oggetto `FormsResult` oggetto ‘s `getOutputContent` metodo .
   * Ottieni il tipo di contenuto del `com.adobe.idp.Document` richiamandone l&#39;oggetto `getContentType` metodo .
   * Imposta la `javax.servlet.http.HttpServletResponse` tipo di contenuto dell’oggetto richiamandone il tipo `setContentType` e passare il tipo di contenuto `com.adobe.idp.Document` oggetto.
   * Crea un `javax.servlet.ServletOutputStream` oggetto utilizzato per scrivere il flusso di dati del modulo nel browser Web client richiamando il `javax.servlet.http.HttpServletResponse` dell’oggetto `getOutputStream` metodo .
   * Crea un `java.io.InputStream` richiamando l&#39;oggetto `com.adobe.idp.Document` dell’oggetto `getInputStream` metodo .
   * Creare un array di byte e compilarlo con il flusso di dati del modulo richiamando il `InputStream` dell’oggetto `read` e passare l&#39;array di byte come argomento.
   * Richiama il `javax.servlet.ServletOutputStream` dell’oggetto `write` per inviare il flusso di dati del modulo al browser Web client. Passa l&#39;array di byte al `write` metodo .

**Consulta anche**

[Avvio rapido (modalità SOAP): Rendering di un modulo sul client utilizzando l’API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-form-at-the-client-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Eseguire il rendering di un modulo sul client utilizzando l’API del servizio Web {#render-a-form-at-the-client-using-the-web-service-api}

Eseguire il rendering di un modulo sul client utilizzando l’API Forms (servizio Web):

1. Includi file di progetto

   * Creare classi proxy Java che utilizzano il servizio WSDL di Forms.
   * Includi le classi proxy Java nel percorso della classe.

1. Creare un oggetto API client Forms

   Crea un `FormsService` e impostare i valori di autenticazione.

1. Impostare le opzioni di esecuzione del rendering client

   * Crea un `PDFFormRenderSpec` utilizzando il relativo costruttore.
   * Imposta la `RenderAtClient` opzione di esecuzione richiamando il `PDFFormRenderSpec` dell’oggetto `setRenderAtClient` e passare il valore della stringa `RenderAtClient.Yes`.

1. Eseguire il rendering di un modulo sul client

   Richiama il `FormsService` dell’oggetto `renderPDFForm` e passare i seguenti valori:

   * Valore stringa che specifica il nome della struttura del modulo, inclusa l&#39;estensione del nome file. Se si fa riferimento a una struttura del modulo che fa parte di un&#39;applicazione Forms, verificare di specificare il percorso completo, ad esempio `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `BLOB` oggetto contenente i dati da unire al modulo. Se non si desidera unire i dati, passare `null`. (Vedi [Precompilazione di Forms con layout fluidi](/help/forms/developing/prepopulating-forms-flowable-layouts.md).)
   * A `PDFFormRenderSpec` oggetto che memorizza le opzioni di esecuzione necessarie per eseguire il rendering di un modulo sul client.
   * A `URLSpec` oggetto che contiene i valori URI richiesti dal servizio Forms.
   * A `java.util.HashMap` oggetto che memorizza gli allegati di file. Si tratta di un parametro facoltativo ed è possibile specificare `null` se non si desidera allegare file al modulo.
   * Un vuoto `com.adobe.idp.services.holders.BLOBHolder` oggetto popolato dal metodo . Questo parametro viene utilizzato per memorizzare il modulo PDF di cui è stato eseguito il rendering.
   * Un vuoto `javax.xml.rpc.holders.LongHolder` oggetto popolato dal metodo . Questo argomento memorizza il numero di pagine nel modulo.
   * Un vuoto `javax.xml.rpc.holders.StringHolder` oggetto popolato dal metodo . (Questo argomento memorizza il valore delle impostazioni internazionali).
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

[Rendering di Forms sul client](#rendering-forms-at-the-client)

[Richiamo di AEM Forms con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
