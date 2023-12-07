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
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '1424'
ht-degree: 0%

---

# Ottimizzazione delle prestazioni del servizio Forms {#optimizing-the-performance-of-theforms-service}

**Gli esempi e gli esempi contenuti in questo documento sono solo per l’ambiente AEM Forms su JEE.**

## Ottimizzazione delle prestazioni del servizio Forms {#optimizing-the-performance-of-the-forms-service}

Durante il rendering di un modulo è possibile impostare opzioni di runtime che ottimizzano le prestazioni del servizio Forms. Un&#39;altra attività che è possibile eseguire per migliorare le prestazioni del servizio Forms consiste nell&#39;archiviare i file XDP nell&#39;archivio. Tuttavia, questa sezione non descrive come eseguire questa attività. (vedere [Richiamare un servizio utilizzando una libreria client Java](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library).)

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Forms, consulta [Guida di riferimento dei servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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

Prima di poter eseguire a livello di programmazione un&#39;operazione API client del servizio Forms, è necessario creare un client del servizio Forms. Se utilizzi l’API Java, crea un’ `FormsServiceClient` oggetto. Se utilizzi l’API del servizio web Forms, crea un’ `FormsService` oggetto.

**Impostazione delle opzioni di runtime delle prestazioni**

Per migliorare le prestazioni del servizio Forms, è possibile impostare le seguenti opzioni di runtime delle prestazioni:

* **Memorizzazione nella cache dei moduli**: è possibile memorizzare in cache un modulo di cui è stato eseguito il rendering come PDF nella cache del server. Ogni modulo viene memorizzato nella cache dopo essere stato generato per la prima volta. In un rendering successivo, se il modulo memorizzato in cache è più recente della marca temporale del progetto del modulo, il modulo viene recuperato dalla cache. La memorizzazione nella cache dei moduli migliora le prestazioni del servizio Forms in quanto non è necessario recuperare la struttura del modulo da un archivio.
* Il rendering delle guide dei moduli (obsoleto) potrebbe richiedere più tempo rispetto ad altri tipi di trasformazione. È consigliabile memorizzare nella cache le guide dei moduli (obsoleto) per migliorare le prestazioni.
* **Opzione autonoma**: se non è necessario che il servizio Forms esegua calcoli lato server, è possibile impostare l’opzione Standalone su `true`, che comporta il rendering dei moduli senza informazioni sullo stato. Le informazioni sullo stato sono necessarie se si desidera eseguire il rendering di un modulo interattivo a un utente finale che immette le informazioni nel modulo e lo invia nuovamente al servizio Forms. Il servizio Forms esegue quindi un&#39;operazione di calcolo e restituisce il modulo all&#39;utente con i risultati visualizzati nel modulo. Se un modulo senza informazioni sullo stato viene inviato nuovamente al servizio Forms, saranno disponibili solo i dati XML e non verranno eseguiti calcoli lato server.
* **Linearized PDF**: file PDF linearizzato organizzato per consentire un accesso incrementale efficiente in un ambiente di rete. Il file PDF è un PDF valido sotto tutti gli aspetti ed è compatibile con tutti i visualizzatori esistenti e con altre applicazioni PDF. In altre parole, un PDF linearizzato può essere visualizzato mentre è ancora in fase di download.
* Questa opzione non migliora le prestazioni quando viene eseguito il rendering di un modulo PDF sul client.
* **Opzione GuideRSL**: abilita la generazione della Guida ai moduli (obsoleta) utilizzando le librerie condivise in fase di esecuzione. Ciò significa che la prima richiesta scaricherà un file SWF più piccolo, oltre a librerie condivise più grandi memorizzate nella cache del browser. Per ulteriori informazioni, consulta RSL nella documentazione di Flex.
* Puoi anche migliorare le prestazioni del servizio Forms eseguendo il rendering di un modulo sul client. (vedere [Rendering di Forms nel client](/help/forms/developing/rendering-forms-client.md).)

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

   * Creare un `ServiceClientFactory` oggetto che contiene proprietà di connessione.
   * Creare un `FormsServiceClient` mediante il costruttore e passando il `ServiceClientFactory` oggetto.

1. Impostazione delle opzioni di runtime delle prestazioni

   * Creare un `PDFFormRenderSpec` mediante il costruttore.
   * Imposta l’opzione cache del modulo richiamando `PDFFormRenderSpec` dell&#39;oggetto `setCacheEnabled` metodo e passaggio `true`.
   * Impostare l&#39;opzione linearizzato richiamando `PDFFormRenderSpec` dell&#39;oggetto `setLinearizedPDF` metodo e passaggio `true.`

1. Rendering del modulo

   Richiama `FormsServiceClient` dell&#39;oggetto `renderPDFForm` e trasmettere i seguenti valori:

   * Valore stringa che specifica il nome della struttura del modulo, inclusa l&#39;estensione del nome file.
   * A `com.adobe.idp.Document` oggetto contenente dati da unire con il modulo. Se non desideri unire i dati, passa un campo vuoto `com.adobe.idp.Document` oggetto.
   * A `PDFFormRenderSpec` oggetto che memorizza le opzioni di runtime per migliorare le prestazioni.
   * A `URLSpec` oggetto contenente valori URI richiesti dal servizio Forms.
   * A `java.util.HashMap` oggetto che memorizza gli allegati. Questo è un parametro facoltativo e puoi specificare `null` se non si desidera allegare file al modulo.

   Il `renderPDFForm` il metodo restituisce un `FormsResult` oggetto contenente un flusso di dati modulo che deve essere scritto nel browser web client.

1. Scrivere il flusso di dati del modulo nel browser Web client

   * Creare un `javax.servlet.ServletOutputStream` oggetto utilizzato per inviare un flusso di dati modulo al browser web client.
   * Creare un `com.adobe.idp.Document` oggetto richiamando il `FormsResult` oggetto &quot;s `getOutputContent` metodo.
   * Creare un `java.io.InputStream` oggetto richiamando il `com.adobe.idp.Document` dell&#39;oggetto `getInputStream` metodo.
   * Creare una matrice di byte e popolarla con il flusso di dati del modulo richiamando `InputStream` dell&#39;oggetto `read`e passando la matrice di byte come argomento.
   * Richiama `javax.servlet.ServletOutputStream` dell&#39;oggetto `write` metodo per inviare il flusso di dati del modulo al browser web client. Passare la matrice di byte al `write` metodo.

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

   Creare un `FormsService` e impostare i valori di autenticazione.

1. Impostazione delle opzioni di runtime delle prestazioni

   * Creare un `PDFFormRenderSpec` mediante il costruttore.
   * Imposta l’opzione cache del modulo richiamando `PDFFormRenderSpec` dell&#39;oggetto `setCacheEnabled` e passando true.
   * Impostare l&#39;opzione autonoma richiamando `PDFFormRenderSpec` dell&#39;oggetto `setStandAlone` e passando true.
   * Impostare l&#39;opzione linearizzato richiamando `PDFFormRenderSpec` dell&#39;oggetto `setLinearizedPDF` e passando true.

1. Rendering del modulo

   Richiama `FormsService` dell&#39;oggetto `renderPDFForm` e trasmettere i seguenti valori:

   * Valore stringa che specifica il nome della struttura del modulo, inclusa l&#39;estensione del nome file.
   * A `BLOB` oggetto contenente dati da unire con il modulo. Se non si desidera unire i dati, passare `null`.
   * A `PDFFormRenderSpecc` oggetto che memorizza le opzioni di runtime.
   * A `URLSpec` oggetto contenente valori URI richiesti dal servizio Forms.
   * A `java.util.HashMap` oggetto che memorizza gli allegati. Questo è un parametro facoltativo e puoi specificare `null` se non si desidera allegare file al modulo.
   * Un campo vuoto `com.adobe.idp.services.holders.BLOBHolder` oggetto popolato dal metodo. Viene utilizzato per memorizzare il modulo PDF di cui è stato eseguito il rendering.
   * Un campo vuoto `javax.xml.rpc.holders.LongHolder` oggetto popolato dal metodo. Questo argomento consente di memorizzare il numero di pagine nel modulo.
   * Un campo vuoto `javax.xml.rpc.holders.StringHolder` oggetto popolato dal metodo. Questo argomento consente di memorizzare il valore delle impostazioni locali.
   * Un campo vuoto `com.adobe.idp.services.holders.FormsResultHolder` oggetto che conterrà i risultati dell&#39;operazione.

   Il `renderPDFForm` il metodo compila `com.adobe.idp.services.holders.FormsResultHolder` oggetto passato come ultimo valore di argomento con un flusso di dati del modulo che deve essere scritto nel browser web client.

1. Scrivere il flusso di dati del modulo nel browser Web client

   * Creare un `FormResult` dell&#39;oggetto ottenendo il valore del `com.adobe.idp.services.holders.FormsResultHolder` dell&#39;oggetto `value` membro dati.
   * Creare un `javax.servlet.ServletOutputStream` oggetto utilizzato per inviare un flusso di dati modulo al browser web client.
   * Creare un `BLOB` oggetto che contiene i dati del modulo richiamando `FormsResult` dell&#39;oggetto `getOutputContent` metodo.
   * Creare una matrice di byte e popolarla richiamando il `BLOB` dell&#39;oggetto `getBinaryData` metodo. Questa attività assegna il contenuto del `FormsResult` alla matrice di byte.
   * Richiama `javax.servlet.http.HttpServletResponse` dell&#39;oggetto `write` metodo per inviare il flusso di dati del modulo al browser web client. Passare la matrice di byte al `write` metodo.

**Consulta anche**

[Richiamare AEM Forms utilizzando la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
