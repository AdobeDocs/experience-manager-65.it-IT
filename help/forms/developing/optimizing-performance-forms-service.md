---
title: Ottimizzazione delle prestazioni del servizio Forms
description: Imposta le opzioni di runtime durante il rendering di un modulo e archivia i file XDP nell’archivio per ottimizzare le prestazioni del servizio Forms.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 5a746c6c-bf6e-4b25-ba7c-a35edb1f55f3
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1424'
ht-degree: 0%

---

# Ottimizzazione delle prestazioni del servizio Forms {#optimizing-the-performance-of-theforms-service}

**Gli esempi e gli esempi contenuti in questo documento sono solo per AEM Forms in ambiente JEE.**

## Ottimizzazione delle prestazioni del servizio Forms {#optimizing-the-performance-of-the-forms-service}

Durante il rendering di un modulo è possibile impostare opzioni di runtime che ottimizzano le prestazioni del servizio Forms. Un&#39;altra attività che è possibile eseguire per migliorare le prestazioni del servizio Forms consiste nell&#39;archiviare i file XDP nell&#39;archivio. Tuttavia, questa sezione non descrive come eseguire questa attività. (Vedi [Chiamata di un servizio tramite una libreria client Java](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library).)

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Forms, vedere [Riferimento ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary-of-steps}

Per ottimizzare le prestazioni del servizio Forms durante il rendering di un modulo, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Crea un oggetto API client di Forms.
1. Impostare le opzioni di runtime delle prestazioni.
1. Eseguire il rendering del modulo.
1. Scrivere il flusso di dati del modulo nel browser Web client.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

**Creare un oggetto API client di Forms**

Prima di poter eseguire a livello di programmazione un&#39;operazione API client del servizio Forms, è necessario creare un client del servizio Forms. Se si utilizza l&#39;API Java, creare un oggetto `FormsServiceClient`. Se si utilizza l&#39;API del servizio Web Forms, creare un oggetto `FormsService`.

**Impostare le opzioni di runtime delle prestazioni**

Per migliorare le prestazioni del servizio Forms, è possibile impostare le seguenti opzioni di runtime delle prestazioni:

* **Memorizzazione in cache dei moduli**: è possibile memorizzare in cache un modulo di cui è stato eseguito il rendering come PDF nella cache del server. Ogni modulo viene memorizzato nella cache dopo essere stato generato per la prima volta. In un rendering successivo, se il modulo memorizzato in cache è più recente della marca temporale del progetto del modulo, il modulo viene recuperato dalla cache. La memorizzazione nella cache dei moduli migliora le prestazioni del servizio Forms in quanto non è necessario recuperare la struttura del modulo da un archivio.
* Il rendering delle guide dei moduli (obsoleto) potrebbe richiedere più tempo rispetto ad altri tipi di trasformazione. È consigliabile memorizzare nella cache le guide dei moduli (obsoleto) per migliorare le prestazioni.
* **Opzione autonoma**: se non è necessario che il servizio Forms esegua i calcoli lato server, è possibile impostare l&#39;opzione Autonoma su `true`, in modo che venga eseguito il rendering dei moduli senza informazioni sullo stato. Le informazioni sullo stato sono necessarie se si desidera eseguire il rendering di un modulo interattivo a un utente finale che immette le informazioni nel modulo e lo invia nuovamente al servizio Forms. Il servizio Forms esegue quindi un&#39;operazione di calcolo e restituisce il modulo all&#39;utente con i risultati visualizzati nel modulo. Se un modulo senza informazioni sullo stato viene inviato nuovamente al servizio Forms, saranno disponibili solo i dati XML e non verranno eseguiti calcoli lato server.
* **PDF linearizzato**: un file PDF linearizzato è organizzato per consentire un accesso incrementale efficiente in un ambiente di rete. Il file PDF è un PDF valido sotto tutti gli aspetti ed è compatibile con tutti i visualizzatori esistenti e con altre applicazioni PDF. In altre parole, un PDF linearizzato può essere visualizzato mentre è ancora in fase di download.
* Questa opzione non migliora le prestazioni quando viene eseguito il rendering di un modulo PDF sul client.
* **Opzione GuideRSL**: abilita la generazione della Guida ai moduli (obsoleta) utilizzando le librerie condivise di runtime. Ciò significa che la prima richiesta scaricherà un file SWF più piccolo, oltre a librerie condivise più grandi memorizzate nella cache del browser. Per ulteriori informazioni, consulta RSL nella documentazione di Flex.
* Puoi anche migliorare le prestazioni del servizio Forms eseguendo il rendering di un modulo sul client. (Vedi [Rendering di Forms nel client](/help/forms/developing/rendering-forms-client.md).)

**Rendering del modulo**

Per eseguire il rendering del modulo dopo aver impostato le opzioni relative alle prestazioni, è necessario utilizzare la stessa logica di applicazione utilizzata per il rendering di un modulo senza le opzioni relative alle prestazioni.

**Scrivere il flusso di dati del modulo nel browser Web client**

Dopo che il servizio Forms esegue il rendering di un modulo, restituisce un flusso di dati del modulo che è necessario scrivere nel browser Web client. Quando viene scritto nel browser Web client, il modulo è visibile all&#39;utente.

**Consulta anche**

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Guida introduttiva all’API di servizio Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Rendering dei PDF forms interattivi](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Rendering di Forms come HTML](/help/forms/developing/rendering-forms-html.md)

[Creazione di applicazioni Web per il rendering di Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

### Ottimizzare le prestazioni utilizzando l’API Java {#optimize-the-performance-using-the-java-api}

Esegui il rendering di un modulo con prestazioni ottimizzate utilizzando l’API Forms (Java):

1. Includi file di progetto

   Includi i file JAR client, ad esempio adobe-forms-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto API client di Forms

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `FormsServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Impostazione delle opzioni di runtime delle prestazioni

   * Creare un oggetto `PDFFormRenderSpec` utilizzando il relativo costruttore.
   * Impostare l&#39;opzione cache modulo richiamando il metodo `setCacheEnabled` dell&#39;oggetto `PDFFormRenderSpec` e passando `true`.
   * Impostare l&#39;opzione linearizzata richiamando il metodo `setLinearizedPDF` dell&#39;oggetto `PDFFormRenderSpec` e passando `true.`

1. Rendering del modulo

   Richiama il metodo `renderPDFForm` dell&#39;oggetto `FormsServiceClient` e passa i seguenti valori:

   * Valore stringa che specifica il nome della struttura del modulo, inclusa l&#39;estensione del nome file.
   * Oggetto `com.adobe.idp.Document` contenente dati da unire al modulo. Se non si desidera unire i dati, passare un oggetto `com.adobe.idp.Document` vuoto.
   * Un oggetto `PDFFormRenderSpec` che memorizza le opzioni di runtime per migliorare le prestazioni.
   * Oggetto `URLSpec` contenente i valori URI richiesti dal servizio Forms.
   * Oggetto `java.util.HashMap` che memorizza gli allegati. Questo è un parametro facoltativo ed è possibile specificare `null` se non si desidera allegare file al modulo.

   Il metodo `renderPDFForm` restituisce un oggetto `FormsResult` che contiene un flusso di dati del modulo che deve essere scritto nel browser Web client.

1. Scrivere il flusso di dati del modulo nel browser Web client

   * Creare un oggetto `javax.servlet.ServletOutputStream` utilizzato per inviare un flusso di dati modulo al browser Web client.
   * Creare un oggetto `com.adobe.idp.Document` richiamando il metodo `getOutputContent` dell&#39;oggetto `FormsResult`.
   * Creare un oggetto `java.io.InputStream` richiamando il metodo `getInputStream` dell&#39;oggetto `com.adobe.idp.Document`.
   * Creare una matrice di byte e popolarla con il flusso di dati del modulo richiamando il metodo `read` dell&#39;oggetto `InputStream` e passando la matrice di byte come argomento.
   * Richiama il metodo `write` dell&#39;oggetto `javax.servlet.ServletOutputStream` per inviare il flusso di dati del modulo al browser Web client. Passare la matrice di byte al metodo `write`.

**Consulta anche**

[Quick Start (modalità SOAP): ottimizzazione delle prestazioni tramite l’API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-optimizing-performance-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Ottimizzare le prestazioni utilizzando l’API del servizio web {#optimize-the-performance-using-the-web-service-api}

Esegui il rendering di un modulo con prestazioni ottimizzate utilizzando l’API di Forms (servizio web):

1. Includi file di progetto

   * Creare classi proxy Java che utilizzano il servizio Forms WSDL.
   * Includi le classi proxy Java nel percorso della classe.

1. Creare un oggetto API client di Forms

   Creare un oggetto `FormsService` e impostare i valori di autenticazione.

1. Impostazione delle opzioni di runtime delle prestazioni

   * Creare un oggetto `PDFFormRenderSpec` utilizzando il relativo costruttore.
   * Impostare l&#39;opzione cache modulo richiamando il metodo `setCacheEnabled` dell&#39;oggetto `PDFFormRenderSpec` e passando true.
   * Impostare l&#39;opzione autonoma richiamando il metodo `setStandAlone` dell&#39;oggetto `PDFFormRenderSpec` e passando true.
   * Impostare l&#39;opzione linearizzata richiamando il metodo `setLinearizedPDF` dell&#39;oggetto `PDFFormRenderSpec` e passando true.

1. Rendering del modulo

   Richiama il metodo `renderPDFForm` dell&#39;oggetto `FormsService` e passa i seguenti valori:

   * Valore stringa che specifica il nome della struttura del modulo, inclusa l&#39;estensione del nome file.
   * Oggetto `BLOB` contenente dati da unire al modulo. Se non si desidera unire i dati, passare `null`.
   * Un oggetto `PDFFormRenderSpecc` che memorizza le opzioni di runtime.
   * Oggetto `URLSpec` contenente i valori URI richiesti dal servizio Forms.
   * Oggetto `java.util.HashMap` che memorizza gli allegati. Questo è un parametro facoltativo ed è possibile specificare `null` se non si desidera allegare file al modulo.
   * Oggetto `com.adobe.idp.services.holders.BLOBHolder` vuoto popolato dal metodo. Viene utilizzato per memorizzare il modulo PDF di cui è stato eseguito il rendering.
   * Oggetto `javax.xml.rpc.holders.LongHolder` vuoto popolato dal metodo. Questo argomento consente di memorizzare il numero di pagine nel modulo.
   * Oggetto `javax.xml.rpc.holders.StringHolder` vuoto popolato dal metodo. Questo argomento consente di memorizzare il valore delle impostazioni locali.
   * Oggetto `com.adobe.idp.services.holders.FormsResultHolder` vuoto che conterrà i risultati dell&#39;operazione.

   Il metodo `renderPDFForm` popola l&#39;oggetto `com.adobe.idp.services.holders.FormsResultHolder` passato come ultimo valore di argomento con un flusso di dati del modulo che deve essere scritto nel browser Web client.

1. Scrivere il flusso di dati del modulo nel browser Web client

   * Creare un oggetto `FormResult` ottenendo il valore del membro dati `value` dell&#39;oggetto `com.adobe.idp.services.holders.FormsResultHolder`.
   * Creare un oggetto `javax.servlet.ServletOutputStream` utilizzato per inviare un flusso di dati modulo al browser Web client.
   * Creare un oggetto `BLOB` contenente dati del modulo richiamando il metodo `getOutputContent` dell&#39;oggetto `FormsResult`.
   * Creare una matrice di byte e popolarla richiamando il metodo `getBinaryData` dell&#39;oggetto `BLOB`. Questa attività assegna il contenuto dell&#39;oggetto `FormsResult` alla matrice di byte.
   * Richiama il metodo `write` dell&#39;oggetto `javax.servlet.http.HttpServletResponse` per inviare il flusso di dati del modulo al browser Web client. Passare la matrice di byte al metodo `write`.

**Consulta anche**

[Richiamare AEM Forms utilizzando la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
