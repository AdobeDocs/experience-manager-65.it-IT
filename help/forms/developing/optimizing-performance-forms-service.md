---
title: Ottimizzazione delle prestazioni del servizio Forms
seo-title: Optimizing the Performance of theForms Service
description: Impostare le opzioni di esecuzione durante il rendering di un modulo e archiviare i file XDP nell'archivio per ottimizzare le prestazioni del servizio Forms.
seo-description: Set run-time options when rendering a form and store XDP files in the repository to optimize the performance of the Forms service.
uuid: 9040c09a-e5d0-432b-b1c5-ad46ab57c4fc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9f883483-b81e-42c6-a4a1-eb499dd112e7
role: Developer
exl-id: 5a746c6c-bf6e-4b25-ba7c-a35edb1f55f3
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1431'
ht-degree: 0%

---

# Ottimizzazione delle prestazioni del servizio Forms {#optimizing-the-performance-of-theforms-service}

**Esempi ed esempi in questo documento sono solo per AEM Forms in ambiente JEE.**

## Ottimizzazione delle prestazioni del servizio Forms {#optimizing-the-performance-of-the-forms-service}

Quando si esegue il rendering di un modulo, è possibile impostare opzioni di esecuzione che ottimizzano le prestazioni del servizio Forms. Un&#39;altra attività che è possibile eseguire per migliorare le prestazioni del servizio Forms è quella di memorizzare i file XDP nell&#39;archivio. Tuttavia, questa sezione non descrive come eseguire questa attività. (Vedi [Richiamo di un servizio tramite una libreria client Java](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library).)

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Forms, vedi [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary-of-steps}

Per ottimizzare le prestazioni del servizio Forms durante il rendering di un modulo, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Creare un oggetto API client Forms.
1. Impostare le opzioni di esecuzione delle prestazioni.
1. Eseguire il rendering del modulo.
1. Scrivere il flusso di dati del modulo sul browser Web client.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

**Creare un oggetto API client Forms**

Prima di poter eseguire programmaticamente un’operazione API client del servizio Forms, è necessario creare un client di servizio Forms. Se utilizzi l’API Java, crea un `FormsServiceClient` oggetto. Se utilizzi l’API del servizio Web Forms, crea un `FormsService` oggetto.

**Impostare le opzioni di runtime delle prestazioni**

Per migliorare le prestazioni del servizio Forms, puoi impostare le seguenti opzioni di esecuzione delle prestazioni:

* **Memorizzazione in cache dei moduli**: È possibile memorizzare nella cache del server un modulo di cui è stato eseguito il rendering come PDF. Ogni modulo viene memorizzato nella cache dopo essere stato generato per la prima volta. In un rendering successivo, se il modulo memorizzato nella cache è più recente della marca temporale della struttura del modulo, il modulo viene recuperato dalla cache. La memorizzazione nella cache dei moduli consente di migliorare le prestazioni del servizio Forms, in quanto non è necessario recuperare la struttura del modulo da un archivio.
* Il rendering delle guide dei moduli (obsolete) potrebbe richiedere più tempo rispetto ad altri tipi di trasformazione. Per migliorare le prestazioni, è consigliabile memorizzare nella cache le guide dei moduli (obsolete).
* **Opzione indipendente**: Se non si richiede al servizio Forms di eseguire calcoli lato server, è possibile impostare l&#39;opzione Standalone su `true`, che consente di eseguire il rendering dei moduli senza informazioni sullo stato. Le informazioni sullo stato sono necessarie se si desidera eseguire il rendering di un modulo interattivo per un utente finale che quindi immette informazioni nel modulo e lo invia nuovamente al servizio Forms. Il servizio Forms esegue quindi un’operazione di calcolo ed esegue il rendering del modulo per l’utente con i risultati visualizzati nel modulo. Se un modulo senza informazioni sullo stato viene inviato nuovamente al servizio Forms, sono disponibili solo i dati XML e i calcoli sul lato server non vengono eseguiti.
* **PDF lineare**: Viene organizzato un file PDF linearizzato per consentire un accesso incrementale efficiente in un ambiente di rete. Il file PDF è un file PDF valido sotto tutti gli aspetti ed è compatibile con tutti i visualizzatori esistenti e con altre applicazioni PDF. In altre parole, è possibile visualizzare un PDF linearizzato mentre è ancora in corso il download.
* Questa opzione non migliora le prestazioni quando si esegue il rendering di un modulo PDF sul client.
* **Opzione GuideRSL**: Abilita la generazione della Guida ai moduli (obsoleta) tramite librerie condivise in fase di esecuzione. Ciò significa che la prima richiesta scaricherà un file SWF più piccolo, più librerie condivise di maggiori dimensioni memorizzate nella cache del browser. Per ulteriori informazioni, consulta RSL nella documentazione di Flex.
* È inoltre possibile migliorare le prestazioni del servizio Forms eseguendo il rendering di un modulo sul client. (Vedi [Rendering di Forms sul client](/help/forms/developing/rendering-forms-client.md).)

**Rendering del modulo**

Per eseguire il rendering del modulo dopo aver impostato le opzioni di prestazioni, utilizzare la stessa logica applicativa del rendering di un modulo senza opzioni di prestazioni.

**Scrivere il flusso di dati del modulo sul browser Web client**

Dopo il rendering di un modulo da parte del servizio Forms, restituisce un flusso di dati del modulo che è necessario scrivere nel browser Web client. Una volta scritto nel browser Web client, il modulo è visibile all’utente.

**Consulta anche**

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API di Forms Service](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Rendering di PDF forms interattivi](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Rendering di Forms as HTML](/help/forms/developing/rendering-forms-html.md)

[Creazione di applicazioni Web per il rendering di Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

### Ottimizzare le prestazioni utilizzando l’API Java {#optimize-the-performance-using-the-java-api}

Eseguire il rendering di un modulo con prestazioni ottimizzate utilizzando l’API Forms (Java):

1. Includi file di progetto

   Includi file JAR client, come adobe-forms-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto API client Forms

   * Crea un `ServiceClientFactory` oggetto contenente le proprietà di connessione.
   * Crea un `FormsServiceClient` utilizzando il relativo costruttore e passando `ServiceClientFactory` oggetto.

1. Impostare le opzioni di runtime delle prestazioni

   * Crea un `PDFFormRenderSpec` utilizzando il relativo costruttore.
   * Impostare l’opzione della cache del modulo richiamando il `PDFFormRenderSpec` dell’oggetto `setCacheEnabled` metodo e passaggio `true`.
   * Imposta l’opzione linearizzata richiamando il `PDFFormRenderSpec` dell’oggetto `setLinearizedPDF` metodo e passaggio `true.`

1. Rendering del modulo

   Richiama il `FormsServiceClient` dell’oggetto `renderPDFForm` e passare i seguenti valori:

   * Valore stringa che specifica il nome della struttura del modulo, inclusa l&#39;estensione del nome file.
   * A `com.adobe.idp.Document` oggetto contenente i dati da unire al modulo. Se non si desidera unire i dati, passare un valore vuoto `com.adobe.idp.Document` oggetto.
   * A `PDFFormRenderSpec` oggetto che memorizza le opzioni di esecuzione per migliorare le prestazioni.
   * A `URLSpec` oggetto che contiene i valori URI richiesti dal servizio Forms.
   * A `java.util.HashMap` oggetto che memorizza gli allegati di file. Si tratta di un parametro facoltativo ed è possibile specificare `null` se non si desidera allegare file al modulo.

   La `renderPDFForm` restituisce un `FormsResult` oggetto che contiene un flusso di dati del modulo che deve essere scritto nel browser Web client.

1. Scrivere il flusso di dati del modulo sul browser Web client

   * Crea un `javax.servlet.ServletOutputStream` oggetto utilizzato per inviare un flusso di dati del modulo al browser Web client.
   * Crea un `com.adobe.idp.Document` richiamando l&#39;oggetto `FormsResult` oggetto ‘s `getOutputContent` metodo .
   * Crea un `java.io.InputStream` richiamando l&#39;oggetto `com.adobe.idp.Document` dell’oggetto `getInputStream` metodo .
   * Creare un array di byte e compilarlo con il flusso di dati del modulo richiamando il `InputStream` dell’oggetto `read`e passare l&#39;array di byte come argomento.
   * Richiama il `javax.servlet.ServletOutputStream` dell’oggetto `write` per inviare il flusso di dati del modulo al browser Web client. Passa l&#39;array di byte al `write` metodo .

**Consulta anche**

[Avvio rapido (modalità SOAP): Ottimizzazione delle prestazioni tramite l’API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-optimizing-performance-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Ottimizzare le prestazioni utilizzando l’API del servizio Web {#optimize-the-performance-using-the-web-service-api}

Eseguire il rendering di un modulo con prestazioni ottimizzate utilizzando l’API Forms (servizio Web):

1. Includi file di progetto

   * Creare classi proxy Java che utilizzano il servizio WSDL di Forms.
   * Includi le classi proxy Java nel percorso della classe.

1. Creare un oggetto API client Forms

   Crea un `FormsService` e impostare i valori di autenticazione.

1. Impostare le opzioni di runtime delle prestazioni

   * Crea un `PDFFormRenderSpec` utilizzando il relativo costruttore.
   * Impostare l’opzione della cache del modulo richiamando il `PDFFormRenderSpec` dell’oggetto `setCacheEnabled` e passare true.
   * Imposta l&#39;opzione autonoma richiamando il `PDFFormRenderSpec` dell’oggetto `setStandAlone` e passare true.
   * Imposta l’opzione linearizzata richiamando il `PDFFormRenderSpec` dell’oggetto `setLinearizedPDF` e passare true.

1. Rendering del modulo

   Richiama il `FormsService` dell’oggetto `renderPDFForm` e passare i seguenti valori:

   * Valore stringa che specifica il nome della struttura del modulo, inclusa l&#39;estensione del nome file.
   * A `BLOB` oggetto contenente i dati da unire al modulo. Se non si desidera unire i dati, passare `null`.
   * A `PDFFormRenderSpecc` oggetto che memorizza le opzioni di esecuzione.
   * A `URLSpec` oggetto che contiene i valori URI richiesti dal servizio Forms.
   * A `java.util.HashMap` oggetto che memorizza gli allegati di file. Si tratta di un parametro facoltativo ed è possibile specificare `null` se non si desidera allegare file al modulo.
   * Un vuoto `com.adobe.idp.services.holders.BLOBHolder` oggetto popolato dal metodo . Viene utilizzato per memorizzare il modulo PDF di cui è stato eseguito il rendering.
   * Un vuoto `javax.xml.rpc.holders.LongHolder` oggetto popolato dal metodo . Questo argomento memorizza il numero di pagine nel modulo.
   * Un vuoto `javax.xml.rpc.holders.StringHolder` oggetto popolato dal metodo . (Questo argomento memorizza il valore delle impostazioni internazionali).
   * Un vuoto `com.adobe.idp.services.holders.FormsResultHolder` oggetto che conterrà i risultati dell&#39;operazione.

   La `renderPDFForm` popola il `com.adobe.idp.services.holders.FormsResultHolder` oggetto passato come ultimo valore argomento con un flusso di dati del modulo che deve essere scritto nel browser Web client.

1. Scrivere il flusso di dati del modulo sul browser Web client

   * Crea un `FormResult` ottenendo il valore del `com.adobe.idp.services.holders.FormsResultHolder` dell’oggetto `value` membro dati.
   * Crea un `javax.servlet.ServletOutputStream` oggetto utilizzato per inviare un flusso di dati del modulo al browser Web client.
   * Crea un `BLOB` oggetto che contiene i dati del modulo richiamando il `FormsResult` dell’oggetto `getOutputContent` metodo .
   * Creare un array di byte e compilarlo richiamando il `BLOB` dell’oggetto `getBinaryData` metodo . Questa attività assegna il contenuto del `FormsResult` all&#39;array di byte.
   * Richiama il `javax.servlet.http.HttpServletResponse` dell’oggetto `write` per inviare il flusso di dati del modulo al browser Web client. Passa l&#39;array di byte al `write` metodo .

**Consulta anche**

[Richiamo di AEM Forms con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
