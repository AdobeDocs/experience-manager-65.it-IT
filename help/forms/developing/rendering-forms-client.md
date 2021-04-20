---
title: Rendering di Forms sul client
seo-title: Rendering di Forms sul client
description: Ottimizza la distribuzione dei contenuti PDF e migliora la capacità del servizio Forms di gestire il carico di rete utilizzando la funzionalità di rendering lato client di Acrobat o Adobe Reader
seo-description: Ottimizza la distribuzione dei contenuti PDF e migliora la capacità del servizio Forms di gestire il carico di rete utilizzando la funzionalità di rendering lato client di Acrobat o Adobe Reader
uuid: 09bcc23d-28b0-473a-87f1-bc17e87620f4
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 08d36e9f-cafc-478e-9781-8fc29ac6262e
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1731'
ht-degree: 0%

---


# Rendering di Forms sul client {#rendering-forms-at-the-client}

**Esempi ed esempi in questo documento sono solo per AEM Forms in ambiente JEE.**

## Rendering di Forms sul client {#rendering-forms-at-the-client-inner}

Puoi ottimizzare la distribuzione dei contenuti PDF e migliorare la capacità del servizio Forms di gestire il carico di rete utilizzando la funzionalità di rendering lato client di Acrobat o Adobe Reader. Questo processo è noto come rendering di un modulo sul client. Per eseguire il rendering di un modulo sul client, il dispositivo client (in genere un browser Web) deve utilizzare Acrobat 7.0 o Adobe Reader 7.0 o versione successiva.

Le modifiche a un modulo risultanti dall’esecuzione di script sul lato server non vengono applicate a un modulo di cui è eseguito il rendering sul client, a meno che il sottomodulo principale non contenga l’attributo `restoreState` impostato su `auto`. Per ulteriori informazioni su questo attributo, consulta [Forms Designer.](https://www.adobe.com/go/learn_aemforms_designer_63)

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Forms, consulta [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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

Prima di poter eseguire programmaticamente un’operazione API client del servizio Forms, è necessario creare un client di servizio Forms. Se utilizzi l’API Java, crea un oggetto `FormsServiceClient`. Se utilizzi l’API del servizio Web Forms, crea un oggetto `FormsService`.

**Impostare le opzioni di esecuzione del rendering client**

Per eseguire il rendering di un modulo sul client, è necessario impostare l’opzione di esecuzione del rendering client su `true` impostando l’opzione di esecuzione `RenderAtClient` su . In questo modo il modulo viene consegnato al dispositivo client in cui viene eseguito il rendering. Se `RenderAtClient` è `auto` (il valore predefinito), la struttura del modulo determina se eseguire il rendering del modulo sul client. La struttura del modulo deve essere una struttura del modulo con un layout scorrevole.

L’opzione `SeedPDF` può essere impostata come opzione opzionale di runtime. L’opzione `SeedPDF` combina il contenitore PDF (documento PDF di seed) con la struttura del modulo e i dati XML. Sia la struttura del modulo che i dati XML vengono inviati ad Acrobat o Adobe Reader, dove viene eseguito il rendering del modulo. L’opzione `SeedPDF` può essere utilizzata quando nel computer client non sono presenti font utilizzati nel modulo, ad esempio quando un utente finale non dispone di una licenza per utilizzare un font concesso in licenza al proprietario del modulo.

Designer consente di creare un semplice file PDF dinamico da utilizzare come file PDF di seed. Per eseguire questa attività sono necessari i seguenti passaggi:

1. Stabilisci se è necessario incorporare font all’interno del file PDF di seed. Il file PDF di seed dovrà contenere font aggiuntivi richiesti dal modulo di cui si sta eseguendo il rendering. Quando incorpori font nel file PDF di seed, assicurati di non violare alcun contratto di licenza per font. In Designer è possibile determinare se è possibile incorporare legalmente i font. Al momento del salvataggio, se non è possibile incorporare font nel modulo, in Designer viene visualizzato un messaggio in cui sono elencati i font che non è possibile incorporare. Questo messaggio non viene visualizzato in Designer per i documenti PDF statici.
1. Se si sta creando il file PDF di seed in Designer, è consigliabile aggiungere almeno un campo di testo contenente un messaggio. Il messaggio deve essere indirizzato agli utenti delle versioni precedenti di Adobe Reader, dichiarando che per visualizzare il documento è necessario Acrobat 7.0 o versioni successive o Adobe Reader 7.0 o versioni successive.
1. Salvare il file PDF di seed come file PDF dinamico con l’estensione del nome del file PDF.

>[!NOTE]
>
>Non è necessario definire l’opzione di esecuzione dei PDF iniziali per eseguire il rendering di un modulo sul client. Se non si specifica un PDF di seed, il servizio Forms crea un pdf shell che non contiene oggetti COS ma contiene un wrapper PDF con il contenuto XDP effettivo incorporato all&#39;interno. I passaggi di questa sezione non impostano l’opzione di esecuzione PDF di seed. Per informazioni sugli oggetti COS, consulta la guida di riferimento Adobe PDF .

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

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `FormsServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Impostare le opzioni di esecuzione del rendering client

   * Creare un oggetto `PDFFormRenderSpec` utilizzando il relativo costruttore.
   * Impostare l&#39;opzione `RenderAtClient` runtime richiamando il metodo `PDFFormRenderSpec` dell&#39;oggetto `setRenderAtClient` e passando il valore enum `RenderAtClient.Yes`.

1. Eseguire il rendering di un modulo sul client

   Richiama il metodo `renderPDFForm` dell&#39;oggetto `FormsServiceClient` e passa i seguenti valori:

   * Valore stringa che specifica il nome della struttura del modulo, inclusa l&#39;estensione del nome file. Se si fa riferimento a una struttura del modulo che fa parte di un&#39;applicazione AEM Forms, assicurarsi di specificare il percorso completo, ad esempio `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Un oggetto `com.adobe.idp.Document` contenente i dati da unire al modulo. Se non si desidera unire i dati, passare un oggetto `com.adobe.idp.Document` vuoto.
   * Un oggetto `PDFFormRenderSpec` che memorizza le opzioni di esecuzione necessarie per eseguire il rendering di un modulo sul client.
   * Un oggetto `URLSpec` contenente valori URI richiesti dal servizio Forms per il rendering di un modulo.
   * Un oggetto `java.util.HashMap` che memorizza gli allegati di file. Questo è un parametro facoltativo ed è possibile specificare `null` se non si desidera allegare file al modulo.

   Il metodo `renderPDFForm` restituisce un oggetto `FormsResult` contenente un flusso di dati del modulo che deve essere scritto nel browser Web client.

1. Scrivere il flusso di dati del modulo sul browser Web client

   * Creare un oggetto `com.adobe.idp.Document` richiamando il metodo `FormsResult` object ‘s `getOutputContent` .
   * Ottenere il tipo di contenuto dell&#39;oggetto `com.adobe.idp.Document` richiamandone il metodo `getContentType`.
   * Impostare il tipo di contenuto dell&#39;oggetto `javax.servlet.http.HttpServletResponse` richiamandone il metodo `setContentType` e passando il tipo di contenuto dell&#39;oggetto `com.adobe.idp.Document`.
   * Creare un oggetto `javax.servlet.ServletOutputStream` utilizzato per scrivere il flusso di dati del modulo nel browser Web client richiamando il metodo `javax.servlet.http.HttpServletResponse` dell&#39;oggetto `getOutputStream`.
   * Creare un oggetto `java.io.InputStream` richiamando il metodo `com.adobe.idp.Document` dell&#39;oggetto `getInputStream`.
   * Creare una matrice di byte e compilarla con il flusso di dati del modulo richiamando il metodo `InputStream` dell&#39;oggetto `read` e passando la matrice di byte come argomento.
   * Richiamare il metodo `write` dell’oggetto `javax.servlet.ServletOutputStream` per inviare il flusso di dati del modulo al browser Web client. Passa l&#39;array di byte al metodo `write` .

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

   Creare un oggetto `FormsService` e impostare i valori di autenticazione.

1. Impostare le opzioni di esecuzione del rendering client

   * Creare un oggetto `PDFFormRenderSpec` utilizzando il relativo costruttore.
   * Impostare l&#39;opzione di esecuzione `RenderAtClient` richiamando il metodo `PDFFormRenderSpec` dell&#39;oggetto `setRenderAtClient` e passando il valore della stringa `RenderAtClient.Yes`.

1. Eseguire il rendering di un modulo sul client

   Richiama il metodo `renderPDFForm` dell&#39;oggetto `FormsService` e passa i seguenti valori:

   * Valore stringa che specifica il nome della struttura del modulo, inclusa l&#39;estensione del nome file. Se si fa riferimento a una struttura del modulo che fa parte di un&#39;applicazione Forms, assicurarsi di specificare il percorso completo, ad esempio `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Un oggetto `BLOB` contenente i dati da unire al modulo. Se non desideri unire i dati, passa `null`. (Consultare [Precompilazione di Forms con layout fluidi](/help/forms/developing/prepopulating-forms-flowable-layouts.md).)
   * Un oggetto `PDFFormRenderSpec` che memorizza le opzioni di esecuzione necessarie per eseguire il rendering di un modulo sul client.
   * Un oggetto `URLSpec` contenente valori URI richiesti dal servizio Forms.
   * Un oggetto `java.util.HashMap` che memorizza gli allegati di file. Questo è un parametro facoltativo ed è possibile specificare `null` se non si desidera allegare file al modulo.
   * Un oggetto `com.adobe.idp.services.holders.BLOBHolder` vuoto compilato dal metodo . Questo parametro viene utilizzato per memorizzare il modulo PDF di cui è stato effettuato il rendering.
   * Un oggetto `javax.xml.rpc.holders.LongHolder` vuoto compilato dal metodo . Questo argomento memorizza il numero di pagine nel modulo.
   * Un oggetto `javax.xml.rpc.holders.StringHolder` vuoto compilato dal metodo . (Questo argomento memorizza il valore delle impostazioni internazionali).
   * Un oggetto `com.adobe.idp.services.holders.FormsResultHolder` vuoto che conterrà i risultati dell&#39;operazione.

   Il metodo `renderPDFForm` popola l&#39;oggetto `com.adobe.idp.services.holders.FormsResultHolder` passato come ultimo valore dell&#39;argomento con un flusso di dati del modulo che deve essere scritto nel browser Web client.

1. Scrivere il flusso di dati del modulo sul browser Web client

   * Creare un oggetto `FormResult` ottenendo il valore del membro dati `com.adobe.idp.services.holders.FormsResultHolder` dell&#39;oggetto `value`.
   * Creare un oggetto `BLOB` che contiene dati del modulo richiamando il metodo `FormsResult` dell&#39;oggetto `getOutputContent`.
   * Ottenere il tipo di contenuto dell&#39;oggetto `BLOB` richiamandone il metodo `getContentType`.
   * Impostare il tipo di contenuto dell&#39;oggetto `javax.servlet.http.HttpServletResponse` richiamandone il metodo `setContentType` e passando il tipo di contenuto dell&#39;oggetto `BLOB`.
   * Creare un oggetto `javax.servlet.ServletOutputStream` utilizzato per scrivere il flusso di dati del modulo nel browser Web client richiamando il metodo `javax.servlet.http.HttpServletResponse` dell&#39;oggetto `getOutputStream`.
   * Creare una matrice di byte e compilarla richiamando il metodo `getBinaryData` dell&#39;oggetto `BLOB`. Questa attività assegna il contenuto dell&#39;oggetto `FormsResult` all&#39;array di byte.
   * Richiamare il metodo `write` dell’oggetto `javax.servlet.http.HttpServletResponse` per inviare il flusso di dati del modulo al browser Web client. Passa l&#39;array di byte al metodo `write` .

**Consulta anche**

[Rendering di Forms sul client](#rendering-forms-at-the-client)

[Richiamo di AEM Forms con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
