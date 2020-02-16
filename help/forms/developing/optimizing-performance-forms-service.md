---
title: Ottimizzazione delle prestazioni del servizio Forms
seo-title: Ottimizzazione delle prestazioni del servizio Forms
description: 'null'
seo-description: 'null'
uuid: 9040c09a-e5d0-432b-b1c5-ad46ab57c4fc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9f883483-b81e-42c6-a4a1-eb499dd112e7
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Ottimizzazione delle prestazioni del servizio Forms {#optimizing-the-performance-of-theforms-service}

## Ottimizzazione delle prestazioni del servizio Forms {#optimizing-the-performance-of-the-forms-service}

Durante il rendering di un modulo, è possibile impostare opzioni di esecuzione che ottimizzino le prestazioni del servizio Forms. Un&#39;altra attività che è possibile eseguire per migliorare le prestazioni del servizio Forms consiste nell&#39;archiviare i file XDP nell&#39;archivio. Tuttavia, in questa sezione non viene descritto come eseguire questa attività. (Vedete [Chiamata di un servizio tramite una libreria](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)client Java.)

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Forms, consultate Riferimento [servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary-of-steps}

Per ottimizzare le prestazioni del servizio Forms durante il rendering di un modulo, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un oggetto API client Forms.
1. Impostare le opzioni di esecuzione delle prestazioni.
1. Eseguire il rendering del modulo.
1. Scrivere il flusso di dati del modulo nel browser Web del client.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, accertatevi di includere i file proxy.

**Creare un oggetto API client Forms**

Prima di eseguire un&#39;operazione API client del servizio Forms a livello di programmazione, è necessario creare un client del servizio Forms. Se utilizzate l&#39;API Java, create un `FormsServiceClient` oggetto. Se si utilizza l&#39;API del servizio Web Forms, creare un `FormsService` oggetto.

**Impostazione delle opzioni di esecuzione delle prestazioni**

Per migliorare le prestazioni del servizio Forms è possibile impostare le seguenti opzioni di esecuzione delle prestazioni:

* **Memorizzazione nella cache** del modulo: È possibile memorizzare nella cache del server un modulo rappresentato come PDF. Ciascun modulo viene memorizzato nella cache dopo che è stato generato per la prima volta. In un rendering successivo, se il modulo memorizzato nella cache è più recente della marca temporale della struttura del modulo, il modulo viene recuperato dalla cache. La memorizzazione nella cache dei moduli consente di migliorare le prestazioni del servizio Forms, in quanto non è necessario recuperare la struttura del modulo da un archivio.
* Il rendering delle guide modulo (obsoleto) potrebbe richiedere più tempo rispetto ad altri tipi di trasformazione. È consigliabile memorizzare nella cache le guide dei moduli (non approvato) per migliorare le prestazioni.
* **Opzione** Standalone: Se non è necessario che il servizio Forms esegua i calcoli sul lato server, è possibile impostare l&#39;opzione Standalone su `true`, che consente di eseguire il rendering dei moduli senza informazioni sullo stato. Le informazioni sullo stato sono necessarie se si desidera eseguire il rendering di un modulo interattivo per un utente finale che immette quindi informazioni nel modulo e lo invia nuovamente al servizio Forms. Il servizio Forms esegue quindi un&#39;operazione di calcolo ed esegue il rendering del modulo per l&#39;utente, con i risultati visualizzati nel modulo. Se un modulo senza informazioni sullo stato viene inviato nuovamente al servizio Forms, sono disponibili solo i dati XML e i calcoli sul lato server non vengono eseguiti.
* **PDF** lineare: Un file PDF linearizzato è organizzato per consentire un accesso incrementale efficiente in un ambiente di rete. Il file PDF è valido sotto tutti gli aspetti ed è compatibile con tutti i visualizzatori esistenti e con altre applicazioni PDF. In altre parole, un PDF linearizzato può essere visualizzato mentre è ancora in fase di download.
* Questa opzione non migliora le prestazioni durante il rendering di un modulo PDF sul client.
* **Opzione** GuideRSL: Abilita la generazione della guida del modulo (obsoleta) tramite librerie condivise in fase di esecuzione. Ciò significa che la prima richiesta scaricherà un file SWF più piccolo, più librerie condivise più grandi memorizzate nella cache del browser. Per ulteriori informazioni, consultate RSL nella documentazione Flex.
* È inoltre possibile migliorare le prestazioni del servizio Forms eseguendo il rendering di un modulo sul client. (Vedere [Rendering dei moduli in Client](/help/forms/developing/rendering-forms-client.md).)

**Eseguire il rendering del modulo**

Per eseguire il rendering del modulo dopo aver impostato le opzioni di prestazioni, è necessario utilizzare la stessa logica applicativa utilizzata per eseguire il rendering di un modulo senza opzioni di prestazioni.

**Scrivere il flusso di dati del modulo nel browser Web del client**

Dopo il rendering di un modulo da parte del servizio Forms, viene restituito un flusso di dati del modulo che è necessario scrivere nel browser Web del client. Una volta scritto nel browser Web del client, il modulo è visibile all&#39;utente.

**Consulta anche**

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido dell&#39;API di Forms Service](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Rendering di moduli PDF interattivi](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Rendering dei moduli come HTML](/help/forms/developing/rendering-forms-html.md)

[Creazione di applicazioni Web per il rendering di moduli](/help/forms/developing/creating-web-applications-renders-forms.md)

### Ottimizzate le prestazioni mediante l&#39;API Java {#optimize-the-performance-using-the-java-api}

Eseguire il rendering di un modulo con prestazioni ottimizzate utilizzando l&#39;API Forms (Java):

1. Includi file di progetto

   Includete file JAR client, ad esempio adobe-forms-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto API client Forms

   * Creare un `ServiceClientFactory` oggetto che contenga proprietà di connessione.
   * Creare un `FormsServiceClient` oggetto utilizzando il relativo costruttore e passando l&#39; `ServiceClientFactory` oggetto.

1. Impostazione delle opzioni di esecuzione delle prestazioni

   * Creare un `PDFFormRenderSpec` oggetto utilizzando il relativo costruttore.
   * Impostare l&#39;opzione della cache del modulo richiamando il `PDFFormRenderSpec` metodo dell&#39; `setCacheEnabled` oggetto e passando `true`.
   * Impostare l&#39;opzione linearizzata richiamando il metodo dell&#39; `PDFFormRenderSpec` oggetto `setLinearizedPDF` e passando `true.`

1. Eseguire il rendering del modulo

   Richiama il metodo dell’ `FormsServiceClient` oggetto `renderPDFForm` e passa i seguenti valori:

   * Una stringa che specifica il nome della struttura del modulo, inclusa l&#39;estensione del nome file.
   * Un `com.adobe.idp.Document` oggetto che contiene i dati da unire al modulo. Se non si desidera unire i dati, passare un `com.adobe.idp.Document` oggetto vuoto.
   * Un `PDFFormRenderSpec` oggetto che memorizza le opzioni di esecuzione per migliorare le prestazioni.
   * Un `URLSpec` oggetto che contiene valori URI richiesti dal servizio Forms.
   * Un `java.util.HashMap` oggetto che memorizza gli allegati. Si tratta di un parametro facoltativo e potete specificare `null` se non desiderate allegare file al modulo.
   Il `renderPDFForm` metodo restituisce un `FormsResult` oggetto che contiene un flusso di dati del modulo da scrivere nel browser Web del client.

1. Scrivere il flusso di dati del modulo nel browser Web del client

   * Creare un `javax.servlet.ServletOutputStream` oggetto utilizzato per inviare un flusso di dati del modulo al browser Web del client.
   * Creare un `com.adobe.idp.Document` oggetto richiamando il `FormsResult` metodo ‘s `getOutputContent` .
   * Creare un `java.io.InputStream` oggetto richiamando il `com.adobe.idp.Document` metodo dell&#39; `getInputStream` oggetto.
   * Creare un array di byte e compilarlo con il flusso di dati del modulo richiamando il `InputStream` `read`metodo dell&#39;oggetto e passando l&#39;array di byte come argomento.
   * Richiamare il metodo dell&#39; `javax.servlet.ServletOutputStream` oggetto `write` per inviare il flusso di dati del modulo al browser Web del client. Passa l&#39;array di byte al `write` metodo.

**Consulta anche**

[Avvio rapido (modalità SOAP): Ottimizzazione delle prestazioni mediante l&#39;API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-optimizing-performance-using-the-java-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Ottimizzare le prestazioni mediante l&#39;API del servizio Web {#optimize-the-performance-using-the-web-service-api}

Eseguire il rendering di un modulo con prestazioni ottimizzate utilizzando l&#39;API di Forms (servizio Web):

1. Includi file di progetto

   * Creare classi proxy Java che utilizzano il WSDL del servizio Forms.
   * Includete le classi proxy Java nel percorso della classe.

1. Creare un oggetto API client Forms

   Creare un `FormsService` oggetto e impostare i valori di autenticazione.

1. Impostazione delle opzioni di esecuzione delle prestazioni

   * Creare un `PDFFormRenderSpec` oggetto utilizzando il relativo costruttore.
   * Impostare l&#39;opzione della cache del modulo richiamando il metodo dell&#39; `PDFFormRenderSpec` oggetto `setCacheEnabled` e passando true.
   * Impostare l&#39;opzione standalone richiamando il metodo dell&#39; `PDFFormRenderSpec` oggetto `setStandAlone` e passando true.
   * Impostare l&#39;opzione linearizzata richiamando il metodo dell&#39; `PDFFormRenderSpec` oggetto `setLinearizedPDF` e passando true.

1. Eseguire il rendering del modulo

   Richiama il metodo dell’ `FormsService` oggetto `renderPDFForm` e passa i seguenti valori:

   * Una stringa che specifica il nome della struttura del modulo, inclusa l&#39;estensione del nome file.
   * Un `BLOB` oggetto che contiene i dati da unire al modulo. Se non si desidera unire i dati, passare `null`.
   * Un `PDFFormRenderSpecc` oggetto che memorizza le opzioni di esecuzione.
   * Un `URLSpec` oggetto che contiene valori URI richiesti dal servizio Forms.
   * Un `java.util.HashMap` oggetto che memorizza gli allegati. Si tratta di un parametro facoltativo e potete specificare `null` se non desiderate allegare file al modulo.
   * Un oggetto vuoto `com.adobe.idp.services.holders.BLOBHolder` compilato dal metodo. Viene utilizzato per memorizzare il modulo PDF di cui è stato effettuato il rendering.
   * Un oggetto vuoto `javax.xml.rpc.holders.LongHolder` compilato dal metodo. (Questo argomento memorizza il numero di pagine nel modulo).
   * Un oggetto vuoto `javax.xml.rpc.holders.StringHolder` compilato dal metodo. (Questo argomento memorizza il valore delle impostazioni internazionali).
   * Un oggetto vuoto `com.adobe.idp.services.holders.FormsResultHolder` che conterrà i risultati dell&#39;operazione.
   Il `renderPDFForm` metodo compila l&#39; `com.adobe.idp.services.holders.FormsResultHolder` oggetto passato come ultimo valore argomento con un flusso di dati del modulo che deve essere scritto nel browser Web del client.

1. Scrivere il flusso di dati del modulo nel browser Web del client

   * Creare un `FormResult` oggetto ottenendo il valore del membro `com.adobe.idp.services.holders.FormsResultHolder` dati dell&#39; `value` oggetto.
   * Creare un `javax.servlet.ServletOutputStream` oggetto utilizzato per inviare un flusso di dati del modulo al browser Web del client.
   * Creare un `BLOB` oggetto che contenga dati del modulo richiamando il `FormsResult` metodo dell&#39; `getOutputContent` oggetto.
   * Creare un array di byte e compilarlo richiamando il metodo dell&#39; `BLOB` oggetto `getBinaryData` . Questa attività assegna il contenuto dell&#39; `FormsResult` oggetto all&#39;array di byte.
   * Richiamare il metodo dell&#39; `javax.servlet.http.HttpServletResponse` oggetto `write` per inviare il flusso di dati del modulo al browser Web del client. Passa l&#39;array di byte al `write` metodo.

**Consulta anche**

[Richiamo di moduli AEM con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
