---
title: Ottimizzazione delle prestazioni del servizio Forms
seo-title: Ottimizzazione delle prestazioni del servizio Forms
description: Impostare le opzioni di esecuzione durante il rendering di un modulo e archiviare i file XDP nell'archivio per ottimizzare le prestazioni del servizio Forms.
seo-description: Impostare le opzioni di esecuzione durante il rendering di un modulo e archiviare i file XDP nell'archivio per ottimizzare le prestazioni del servizio Forms.
uuid: 9040c09a-e5d0-432b-b1c5-ad46ab57c4fc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9f883483-b81e-42c6-a4a1-eb499dd112e7
translation-type: tm+mt
source-git-commit: 9cf46a26d2aa2e41b924a4de89cf8ab5fdeeefc6
workflow-type: tm+mt
source-wordcount: '1459'
ht-degree: 0%

---


# Ottimizzazione delle prestazioni del servizio Forms {#optimizing-the-performance-of-theforms-service}

**Esempi ed esempi in questo documento sono disponibili solo per  AEM Forms nell&#39;ambiente JEE.**

## Ottimizzazione delle prestazioni del servizio Forms {#optimizing-the-performance-of-the-forms-service}

Durante il rendering di un modulo, è possibile impostare opzioni di esecuzione che ottimizzino le prestazioni del servizio Forms. Un&#39;altra attività che è possibile eseguire per migliorare le prestazioni del servizio Forms consiste nell&#39;archiviare i file XDP nell&#39;archivio. Tuttavia, in questa sezione non viene descritto come eseguire questa attività. (Vedere [Chiamata di un servizio tramite una libreria client Java](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library).)

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Forms, vedere [Guida di riferimento dei servizi per  AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary-of-steps}

Per ottimizzare le prestazioni del servizio Forms durante il rendering di un modulo, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un oggetto Forms Client API.
1. Impostare le opzioni di esecuzione delle prestazioni.
1. Eseguire il rendering del modulo.
1. Scrivere il flusso di dati del modulo nel browser Web del client.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, accertatevi di includere i file proxy.

**Creare un oggetto Forms Client API**

Prima di eseguire un&#39;operazione API client di Forms Service a livello di programmazione, è necessario creare un client di servizi Forms. Se utilizzate l&#39;API Java, create un oggetto `FormsServiceClient`. Se utilizzate l&#39;API del servizio Web di Forms, create un oggetto `FormsService`.

**Impostazione delle opzioni di esecuzione delle prestazioni**

Potete impostare le seguenti opzioni di esecuzione delle prestazioni per migliorare le prestazioni del servizio Forms:

* **Memorizzazione nella cache** del modulo: È possibile memorizzare nella cache del server un modulo rappresentato come PDF. Ciascun modulo viene memorizzato nella cache dopo che è stato generato per la prima volta. In un rendering successivo, se il modulo memorizzato nella cache è più recente della marca temporale della struttura del modulo, il modulo viene recuperato dalla cache. Il caching dei moduli consente di migliorare le prestazioni del servizio Forms, in quanto non è necessario recuperare la struttura del modulo da un archivio.
* Il rendering delle guide modulo (obsoleto) potrebbe richiedere più tempo rispetto ad altri tipi di trasformazione. È consigliabile memorizzare nella cache le guide dei moduli (non approvato) per migliorare le prestazioni.
* **Opzione** Standalone: Se non è necessario che il servizio Forms esegua i calcoli sul lato server, è possibile impostare l&#39;opzione Standalone su  `true`, che consente di eseguire il rendering dei moduli senza informazioni sullo stato. Le informazioni sullo stato sono necessarie se si desidera eseguire il rendering di un modulo interattivo per un utente finale che immette quindi informazioni nel modulo e invia nuovamente il modulo al servizio Forms. Il servizio Forms esegue quindi un&#39;operazione di calcolo ed esegue il rendering del modulo per restituirlo all&#39;utente, con i risultati visualizzati nel modulo. Se un modulo senza informazioni sullo stato viene inviato nuovamente al servizio Forms, sono disponibili solo i dati XML e i calcoli sul lato server non vengono eseguiti.
* **PDF** lineare: Un file PDF linearizzato è organizzato per consentire un accesso incrementale efficiente in un ambiente di rete. Il file PDF è valido sotto tutti gli aspetti ed è compatibile con tutti i visualizzatori esistenti e con altre applicazioni PDF. In altre parole, un PDF linearizzato può essere visualizzato mentre è ancora in fase di download.
* Questa opzione non migliora le prestazioni durante il rendering di un modulo PDF sul client.
* **Opzione** GuideRSL: Abilita la generazione della guida del modulo (obsoleta) tramite librerie condivise in fase di esecuzione. Ciò significa che la prima richiesta scaricherà un file SWF più piccolo, più librerie condivise più grandi memorizzate nella cache del browser. Per ulteriori informazioni, consultate RSL nella documentazione Flex.
* È inoltre possibile migliorare le prestazioni del servizio Forms eseguendo il rendering di un modulo sul client. (Vedere [Rendering di Forms in Client](/help/forms/developing/rendering-forms-client.md).)

**Eseguire il rendering del modulo**

Per eseguire il rendering del modulo dopo aver impostato le opzioni di prestazioni, è necessario utilizzare la stessa logica applicativa utilizzata per eseguire il rendering di un modulo senza opzioni di prestazioni.

**Scrivere il flusso di dati del modulo nel browser Web del client**

Dopo il rendering di un modulo da parte del servizio Forms, viene restituito un flusso di dati del modulo che è necessario scrivere nel browser Web del client. Una volta scritto nel browser Web del client, il modulo è visibile all&#39;utente.

**Consulta anche**

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido di Forms Service API](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Rendering di PDF forms interattivi](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Rendering di Forms come HTML](/help/forms/developing/rendering-forms-html.md)

[Creazione di applicazioni Web per il rendering di Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

### Ottimizzate le prestazioni utilizzando l&#39;API Java {#optimize-the-performance-using-the-java-api}

Eseguire il rendering di un modulo con prestazioni ottimizzate utilizzando l&#39;API Forms (Java):

1. Includi file di progetto

   Includete file JAR client, ad esempio adobe-forms-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto Forms Client API

   * Creare un oggetto `ServiceClientFactory` che contiene le proprietà di connessione.
   * Creare un oggetto `FormsServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Impostazione delle opzioni di esecuzione delle prestazioni

   * Creare un oggetto `PDFFormRenderSpec` utilizzando il relativo costruttore.
   * Impostare l&#39;opzione della cache del modulo richiamando il metodo `setCacheEnabled` dell&#39;oggetto `true` e passando `PDFFormRenderSpec`.
   * Impostare l&#39;opzione linearizzata richiamando il metodo `PDFFormRenderSpec` dell&#39;oggetto `setLinearizedPDF` e passando `true.`

1. Eseguire il rendering del modulo

   Richiamare il metodo `FormsServiceClient` dell&#39;oggetto `renderPDFForm` e trasmettere i seguenti valori:

   * Una stringa che specifica il nome della struttura del modulo, inclusa l&#39;estensione del nome file.
   * Un oggetto `com.adobe.idp.Document` che contiene i dati da unire al modulo. Se non si desidera unire i dati, passare un oggetto `com.adobe.idp.Document` vuoto.
   * Un oggetto `PDFFormRenderSpec` che memorizza le opzioni di esecuzione per migliorare le prestazioni.
   * Un oggetto `URLSpec` che contiene valori URI richiesti dal servizio Forms.
   * Un oggetto `java.util.HashMap` che memorizza gli allegati. Si tratta di un parametro facoltativo ed è possibile specificare `null` se non si desidera allegare file al modulo.

   Il metodo `renderPDFForm` restituisce un oggetto `FormsResult` contenente un flusso di dati del modulo che deve essere scritto nel browser Web del client.

1. Scrivere il flusso di dati del modulo nel browser Web del client

   * Creare un oggetto `javax.servlet.ServletOutputStream` utilizzato per inviare un flusso di dati del modulo al browser Web del client.
   * Creare un oggetto `com.adobe.idp.Document` richiamando il metodo `FormsResult` object ‘s `getOutputContent`.
   * Creare un oggetto `java.io.InputStream` richiamando il metodo `com.adobe.idp.Document` dell&#39;oggetto `getInputStream`.
   * Creare un array di byte e compilarlo con il flusso di dati del modulo richiamando il metodo `InputStream` dell&#39;oggetto `read`e passando l&#39;array di byte come argomento.
   * Richiamare il metodo `javax.servlet.ServletOutputStream` dell&#39;oggetto `write` per inviare il flusso di dati del modulo al browser Web del client. Passate l&#39;array di byte al metodo `write`.

**Consulta anche**

[Avvio rapido (modalità SOAP): Ottimizzazione delle prestazioni mediante l&#39;API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-optimizing-performance-using-the-java-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Ottimizzate le prestazioni utilizzando l&#39;API del servizio Web {#optimize-the-performance-using-the-web-service-api}

Eseguire il rendering di un modulo con prestazioni ottimizzate utilizzando l&#39;API Forms (servizio Web):

1. Includi file di progetto

   * Creare classi proxy Java che utilizzano il servizio WSDL di Forms.
   * Includete le classi proxy Java nel percorso della classe.

1. Creare un oggetto Forms Client API

   Creare un oggetto `FormsService` e impostare i valori di autenticazione.

1. Impostazione delle opzioni di esecuzione delle prestazioni

   * Creare un oggetto `PDFFormRenderSpec` utilizzando il relativo costruttore.
   * Impostare l&#39;opzione della cache del modulo richiamando il metodo `setCacheEnabled` dell&#39;oggetto `PDFFormRenderSpec` e passando true.
   * Impostate l&#39;opzione standalone richiamando il metodo `setStandAlone` dell&#39;oggetto `PDFFormRenderSpec` e passando true.
   * Impostate l&#39;opzione linearizzata richiamando il metodo `setLinearizedPDF` dell&#39;oggetto e passando true.`PDFFormRenderSpec`

1. Eseguire il rendering del modulo

   Richiamare il metodo `FormsService` dell&#39;oggetto `renderPDFForm` e trasmettere i seguenti valori:

   * Una stringa che specifica il nome della struttura del modulo, inclusa l&#39;estensione del nome file.
   * Un oggetto `BLOB` che contiene i dati da unire al modulo. Se non si desidera unire i dati, passare `null`.
   * Un oggetto `PDFFormRenderSpecc` che memorizza le opzioni di esecuzione.
   * Un oggetto `URLSpec` che contiene valori URI richiesti dal servizio Forms.
   * Un oggetto `java.util.HashMap` che memorizza gli allegati. Si tratta di un parametro facoltativo ed è possibile specificare `null` se non si desidera allegare file al modulo.
   * Un oggetto `com.adobe.idp.services.holders.BLOBHolder` vuoto compilato dal metodo. Viene utilizzato per memorizzare il modulo PDF di cui è stato effettuato il rendering.
   * Un oggetto `javax.xml.rpc.holders.LongHolder` vuoto compilato dal metodo. (Questo argomento memorizza il numero di pagine nel modulo).
   * Un oggetto `javax.xml.rpc.holders.StringHolder` vuoto compilato dal metodo. (Questo argomento memorizza il valore delle impostazioni internazionali).
   * Un oggetto `com.adobe.idp.services.holders.FormsResultHolder` vuoto che conterrà i risultati dell&#39;operazione.

   Il metodo `renderPDFForm` compila l&#39;oggetto `com.adobe.idp.services.holders.FormsResultHolder` passato come ultimo valore argomento con un flusso di dati del modulo che deve essere scritto nel browser Web del client.

1. Scrivere il flusso di dati del modulo nel browser Web del client

   * Creare un oggetto `FormResult` ottenendo il valore del membro di dati `com.adobe.idp.services.holders.FormsResultHolder` dell&#39;oggetto `value`.
   * Creare un oggetto `javax.servlet.ServletOutputStream` utilizzato per inviare un flusso di dati del modulo al browser Web del client.
   * Creare un oggetto `BLOB` contenente dati del modulo richiamando il metodo `FormsResult` dell&#39;oggetto `getOutputContent`.
   * Creare un array di byte e compilarlo richiamando il metodo `BLOB` dell&#39;oggetto `getBinaryData`. Questa attività assegna il contenuto dell&#39;oggetto `FormsResult` all&#39;array di byte.
   * Richiamare il metodo `javax.servlet.http.HttpServletResponse` dell&#39;oggetto `write` per inviare il flusso di dati del modulo al browser Web del client. Passate l&#39;array di byte al metodo `write`.

**Consulta anche**

[Richiamo  AEM Forms con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
