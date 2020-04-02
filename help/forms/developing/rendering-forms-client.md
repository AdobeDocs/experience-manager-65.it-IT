---
title: Rendering dei moduli nel client
seo-title: Rendering dei moduli nel client
description: 'null'
seo-description: 'null'
uuid: 09bcc23d-28b0-473a-87f1-bc17e87620f4
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 08d36e9f-cafc-478e-9781-8fc29ac6262e
translation-type: tm+mt
source-git-commit: ab401a8007f6ea85c0e52169091ce7a38b3dbe5c

---


# Rendering dei moduli nel client {#rendering-forms-at-the-client}

## Rendering dei moduli nel client {#rendering-forms-at-the-client-inner}

È possibile ottimizzare la distribuzione del contenuto PDF e migliorare la capacità del servizio Forms di gestire il carico di rete utilizzando la funzionalità di rendering sul lato client di Acrobat o Adobe Reader. Questo processo è noto come rendering di un modulo sul client. Per eseguire il rendering di un modulo sul lato client, il dispositivo client (in genere un browser Web) deve utilizzare Acrobat 7.0 o Adobe Reader 7.0 o versione successiva.

Le modifiche apportate a un modulo derivanti dall&#39;esecuzione di script sul lato server non vengono riportate in un modulo di cui viene eseguito il rendering sul client, a meno che il sottomodulo principale non contenga l&#39; `restoreState` attributo impostato su `auto`. Per ulteriori informazioni su questo attributo, vedere [Designer moduli.](https://www.adobe.com/go/learn_aemforms_designer_63)

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Forms, consultate Riferimento [servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary-of-steps}

Per eseguire il rendering di un modulo sul client, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un oggetto API client Forms.
1. Impostate le opzioni di esecuzione del rendering client.
1. Eseguire il rendering di un modulo sul client.
1. Scrivere il modulo nel browser Web del client.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, accertatevi di includere i file proxy.

**Creare un oggetto API client Forms**

Prima di eseguire un&#39;operazione API client del servizio Forms a livello di programmazione, è necessario creare un client del servizio Forms. Se utilizzate l&#39;API Java, create un `FormsServiceClient` oggetto. Se si utilizza l&#39;API del servizio Web Forms, creare un `FormsService` oggetto.

**Impostazione delle opzioni di esecuzione del rendering client**

È necessario impostare l&#39;opzione di esecuzione del rendering client per eseguire il rendering di un modulo sul client impostando l&#39;opzione di esecuzione su `RenderAtClient` `true`. Questo determina la distribuzione del modulo al dispositivo client sul quale viene eseguito il rendering. Se `RenderAtClient` è `auto` (il valore predefinito), la struttura del modulo determina se eseguire il rendering del modulo sul lato client. La struttura del modulo deve essere una struttura del modulo con layout scorrevole.

L’opzione può essere impostata anche per l’esecuzione `SeedPDF` . L&#39; `SeedPDF` opzione combina il contenitore PDF (documento PDF di livello inferiore) con la struttura del modulo e i dati XML. Sia la struttura del modulo che i dati XML vengono inviati ad Acrobat o Adobe Reader, dove viene eseguito il rendering del modulo. L&#39; `SeedPDF` opzione può essere utilizzata quando il computer client non dispone di font utilizzati nel modulo, ad esempio quando un utente finale non dispone di una licenza per utilizzare un font concesso in licenza al proprietario del modulo.

Designer consente di creare un semplice file PDF dinamico da utilizzare come file PDF di base. Per eseguire questa operazione sono necessari i seguenti passaggi:

1. Determinare se è necessario incorporare font nel file PDF di livello inferiore. Il file PDF di livello inferiore dovrà contenere i font aggiuntivi richiesti dal modulo di cui si sta eseguendo il rendering. Durante l&#39;incorporazione di font nel file PDF di base, assicurarsi di non violare alcun contratto di licenza per i font. In Designer è possibile determinare se è possibile incorporare legalmente i font. In caso di font non incorporati nel modulo, in Designer viene visualizzato un messaggio in cui sono elencati i font che non è possibile incorporare. Questo messaggio non viene visualizzato in Designer per i documenti PDF statici.
1. Se si sta creando il file PDF di livello inferiore in Designer, è consigliabile aggiungere almeno un campo di testo contenente un messaggio. Il messaggio deve essere indirizzato agli utenti delle versioni precedenti di Adobe Reader in cui si dichiara che per visualizzare il documento è necessario Acrobat 7.0 o versioni successive o Adobe Reader 7.0 o versioni successive.
1. Salvare il file PDF di livello inferiore come file PDF dinamico con l’estensione del nome del file PDF.

>[!NOTE]
>
>Per eseguire il rendering di un modulo sul client, non è necessario definire l&#39;opzione di esecuzione PDF di livello inferiore. Se non si specifica un PDF di livello inferiore, il servizio Forms crea un pdf contenitore che non conterrà oggetti COS ma conterrà un wrapper PDF con il contenuto XDP effettivo incorporato al suo interno. I passaggi descritti in questa sezione non impostano l&#39;opzione per l&#39;esecuzione dei PDF iniziali. Per informazioni sugli oggetti COS, vedere la guida di riferimento di Adobe PDF.

**Eseguire il rendering di un modulo sul client**

Per eseguire il rendering di un modulo sul client, è necessario assicurarsi che le opzioni di esecuzione del rendering del client siano incluse nella logica dell&#39;applicazione per eseguire il rendering di un modulo.

**Scrivere il flusso di dati del modulo nel browser Web del client**

Il servizio Forms crea un flusso di dati del modulo da scrivere nel browser Web del client. Una volta scritto nel browser Web del client, il modulo viene rappresentato da Acrobat 7.0 o Adobe Reader 7.0 o versione successiva ed è visibile all&#39;utente.

**Consulta anche**

[Eseguire il rendering di un modulo sul client utilizzando l&#39;API Java](#render-a-form-at-the-client-using-the-java-api)

[Eseguire il rendering di un modulo sul client utilizzando l&#39;API del servizio Web](#render-a-form-at-the-client-using-the-web-service-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido dell&#39;API di Forms Service](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Invio di documenti al servizio Forms](/help/forms/developing/passing-documents-forms-service.md)

[Creazione di applicazioni Web per il rendering di moduli](/help/forms/developing/creating-web-applications-renders-forms.md)

### Eseguire il rendering di un modulo sul client utilizzando l&#39;API Java {#render-a-form-at-the-client-using-the-java-api}

Eseguire il rendering di un modulo sul client utilizzando l&#39;API Forms (Java):

1. Includi file di progetto

   Includete file JAR client, ad esempio adobe-forms-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto API client Forms

   * Creare un `ServiceClientFactory` oggetto che contenga proprietà di connessione.
   * Creare un `FormsServiceClient` oggetto utilizzando il relativo costruttore e passando l&#39; `ServiceClientFactory` oggetto.

1. Impostazione delle opzioni di esecuzione del rendering client

   * Creare un `PDFFormRenderSpec` oggetto utilizzando il relativo costruttore.
   * Impostare l&#39;opzione di `RenderAtClient` esecuzione richiamando il metodo dell&#39; `PDFFormRenderSpec` oggetto `setRenderAtClient` e passando il valore enum `RenderAtClient.Yes`.

1. Eseguire il rendering di un modulo sul client

   Richiama il metodo dell’ `FormsServiceClient` oggetto `renderPDFForm` e passa i seguenti valori:

   * Una stringa che specifica il nome della struttura del modulo, inclusa l&#39;estensione del nome file. Se si fa riferimento a una struttura del modulo che fa parte di un&#39;applicazione AEM Forms, è necessario specificare il percorso completo, ad esempio `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Un `com.adobe.idp.Document` oggetto che contiene i dati da unire al modulo. Se non si desidera unire i dati, passare un `com.adobe.idp.Document` oggetto vuoto.
   * Un `PDFFormRenderSpec` oggetto che memorizza le opzioni di esecuzione necessarie per eseguire il rendering di un modulo sul client.
   * Un `URLSpec` oggetto che contiene valori URI richiesti dal servizio Forms per eseguire il rendering di un modulo.
   * Un `java.util.HashMap` oggetto che memorizza gli allegati. Si tratta di un parametro facoltativo e potete specificare `null` se non desiderate allegare file al modulo.
   Il `renderPDFForm` metodo restituisce un `FormsResult` oggetto che contiene un flusso di dati del modulo che deve essere scritto nel browser Web del client.

1. Scrivere il flusso di dati del modulo nel browser Web del client

   * Creare un `com.adobe.idp.Document` oggetto richiamando il `FormsResult` metodo ‘s `getOutputContent` .
   * Ottenere il tipo di contenuto dell&#39; `com.adobe.idp.Document` oggetto richiamandone il `getContentType` metodo.
   * Impostare il tipo di contenuto dell&#39; `javax.servlet.http.HttpServletResponse` oggetto richiamandone `setContentType` il metodo e passando il tipo di contenuto dell&#39; `com.adobe.idp.Document` oggetto.
   * Creare un `javax.servlet.ServletOutputStream` oggetto utilizzato per scrivere il flusso di dati del modulo nel browser Web del client richiamando il `javax.servlet.http.HttpServletResponse` metodo dell&#39; `getOutputStream` oggetto.
   * Creare un `java.io.InputStream` oggetto richiamando il `com.adobe.idp.Document` metodo dell&#39; `getInputStream` oggetto.
   * Creare un array di byte e compilarlo con il flusso di dati del modulo richiamando il metodo dell&#39; `InputStream` oggetto `read` e passando l&#39;array di byte come argomento.
   * Richiamare il metodo dell&#39; `javax.servlet.ServletOutputStream` oggetto `write` per inviare il flusso di dati del modulo al browser Web del client. Passa l&#39;array di byte al `write` metodo.

**Consulta anche**

[Avvio rapido (modalità SOAP): Rendering di un modulo sul client mediante l&#39;API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-form-at-the-client-using-the-java-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Eseguire il rendering di un modulo sul client utilizzando l&#39;API del servizio Web {#render-a-form-at-the-client-using-the-web-service-api}

Eseguire il rendering di un modulo sul client utilizzando l&#39;API di Forms (servizio Web):

1. Includi file di progetto

   * Creare classi proxy Java che utilizzano il WSDL del servizio Forms.
   * Includete le classi proxy Java nel percorso della classe.

1. Creare un oggetto API client Forms

   Creare un `FormsService` oggetto e impostare i valori di autenticazione.

1. Impostazione delle opzioni di esecuzione del rendering client

   * Creare un `PDFFormRenderSpec` oggetto utilizzando il relativo costruttore.
   * Impostare l&#39;opzione di `RenderAtClient` esecuzione richiamando il metodo dell&#39; `PDFFormRenderSpec` oggetto `setRenderAtClient` e passando il valore della stringa `RenderAtClient.Yes`.

1. Eseguire il rendering di un modulo sul client

   Richiama il metodo dell’ `FormsService` oggetto `renderPDFForm` e passa i seguenti valori:

   * Una stringa che specifica il nome della struttura del modulo, inclusa l&#39;estensione del nome file. Se si fa riferimento a una struttura del modulo che fa parte di un&#39;applicazione Forms, è necessario specificare il percorso completo, ad esempio `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Un `BLOB` oggetto che contiene i dati da unire al modulo. Se non si desidera unire i dati, passare `null`. (Vedere [Precompilazione dei moduli con layout](/help/forms/developing/prepopulating-forms-flowable-layouts.md)scorrevoli.)
   * Un `PDFFormRenderSpec` oggetto che memorizza le opzioni di esecuzione necessarie per eseguire il rendering di un modulo sul client.
   * Un `URLSpec` oggetto che contiene valori URI richiesti dal servizio Forms.
   * Un `java.util.HashMap` oggetto che memorizza gli allegati. Si tratta di un parametro facoltativo e potete specificare `null` se non desiderate allegare file al modulo.
   * Un oggetto vuoto `com.adobe.idp.services.holders.BLOBHolder` compilato dal metodo. Questo parametro viene utilizzato per memorizzare il modulo PDF di cui è stato effettuato il rendering.
   * Un oggetto vuoto `javax.xml.rpc.holders.LongHolder` compilato dal metodo. (Questo argomento memorizza il numero di pagine nel modulo).
   * Un oggetto vuoto `javax.xml.rpc.holders.StringHolder` compilato dal metodo. (Questo argomento memorizza il valore delle impostazioni internazionali).
   * Un oggetto vuoto `com.adobe.idp.services.holders.FormsResultHolder` che conterrà i risultati dell&#39;operazione.
   Il `renderPDFForm` metodo compila l&#39; `com.adobe.idp.services.holders.FormsResultHolder` oggetto passato come valore dell&#39;ultimo argomento con un flusso di dati del modulo che deve essere scritto nel browser Web del client.

1. Scrivere il flusso di dati del modulo nel browser Web del client

   * Creare un `FormResult` oggetto ottenendo il valore del membro `com.adobe.idp.services.holders.FormsResultHolder` dati dell&#39; `value` oggetto.
   * Creare un `BLOB` oggetto che contenga dati del modulo richiamando il `FormsResult` metodo dell&#39; `getOutputContent` oggetto.
   * Ottenere il tipo di contenuto dell&#39; `BLOB` oggetto richiamandone il `getContentType` metodo.
   * Impostare il tipo di contenuto dell&#39; `javax.servlet.http.HttpServletResponse` oggetto richiamandone `setContentType` il metodo e passando il tipo di contenuto dell&#39; `BLOB` oggetto.
   * Creare un `javax.servlet.ServletOutputStream` oggetto utilizzato per scrivere il flusso di dati del modulo nel browser Web del client richiamando il `javax.servlet.http.HttpServletResponse` metodo dell&#39; `getOutputStream` oggetto.
   * Creare un array di byte e compilarlo richiamando il metodo dell&#39; `BLOB` oggetto `getBinaryData` . Questa attività assegna il contenuto dell&#39; `FormsResult` oggetto all&#39;array di byte.
   * Richiamare il metodo dell&#39; `javax.servlet.http.HttpServletResponse` oggetto `write` per inviare il flusso di dati del modulo al browser Web del client. Passa l&#39;array di byte al `write` metodo.

**Consulta anche**

[Rendering dei moduli nel client](#rendering-forms-at-the-client)

[Richiamo di moduli AEM con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
