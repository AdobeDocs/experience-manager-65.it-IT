---
title: Rendering dei moduli per valore
seo-title: Rendering dei moduli per valore
description: 'null'
seo-description: 'null'
uuid: b932cc54-662f-40ae-94e0-20ac82845f3b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: ddbb2b82-4c57-4845-a5be-2435902d312b
translation-type: tm+mt
source-git-commit: 66bfd6870b4c09dc2ca1b66058e0b9e040a71507

---


# Rendering dei moduli per valore {#rendering-forms-by-value}

In genere, una struttura del modulo creata in Designer viene passata facendo riferimento al servizio Forms. Le strutture del modulo possono essere di grandi dimensioni e, di conseguenza, è più efficiente passarle mediante riferimento per evitare di dover eseguire il marshalling dei byte delle strutture del modulo in base al valore. Il servizio Forms consente inoltre di memorizzare nella cache la struttura del modulo in modo che, se memorizzata nella cache, non sia necessario leggere continuamente la struttura del modulo.

Se una struttura del modulo contiene un attributo UUID, viene memorizzata nella cache. Il valore UUID è univoco per tutte le strutture del modulo e viene utilizzato per identificare in modo univoco un modulo. Quando si esegue il rendering di un modulo in base al valore, il modulo deve essere memorizzato nella cache solo se utilizzato più volte. Tuttavia, se il modulo non viene utilizzato ripetutamente e deve essere univoco, è possibile evitare di memorizzarlo nella cache utilizzando opzioni di memorizzazione nella cache impostate tramite l&#39;API AEM Forms.

Il servizio Forms consente inoltre di risolvere la posizione del contenuto collegato all&#39;interno della struttura del modulo. Ad esempio, le immagini collegate a cui viene fatto riferimento nella struttura del modulo sono URL relativi. Si presume sempre che il contenuto collegato sia relativo alla posizione della struttura del modulo. Pertanto, per risolvere il contenuto collegato è necessario determinarne la posizione applicando il percorso relativo alla posizione assoluta della struttura del modulo.

Anziché trasmettere una struttura del modulo per riferimento, è possibile trasmettere una struttura del modulo per valore. Il passaggio di una struttura del modulo in base al valore è efficiente quando si crea in modo dinamico una struttura del modulo; ovvero quando un&#39;applicazione client genera l&#39;XML che crea una struttura del modulo in fase di esecuzione. In questo caso, una struttura del modulo non viene memorizzata in un archivio fisico perché è memorizzata in memoria. Durante la creazione dinamica di una struttura del modulo in fase di esecuzione e il suo passaggio per valore, è possibile memorizzare il modulo nella cache e migliorare le prestazioni del servizio Forms.

**Limiti di trasmissione di un modulo per valore**

Quando una struttura del modulo viene passata per valore, si applicano le seguenti limitazioni:

* Nessun contenuto collegato relativo può essere incluso nella struttura del modulo. Tutte le immagini e i frammenti devono essere incorporati nella struttura del modulo o essere denominati in modo assoluto.
* Non è possibile eseguire calcoli sul lato server dopo il rendering del modulo. Se il modulo viene nuovamente inviato al servizio Forms, i dati vengono estratti e restituiti senza calcoli sul lato server.
* Poiché HTML può utilizzare solo immagini collegate in fase di esecuzione, non è possibile generare HTML con immagini incorporate. Questo perché il servizio Forms supporta le immagini incorporate con HTML recuperando le immagini da una struttura del modulo di riferimento. Poiché una struttura del modulo passata per valore non dispone di una posizione di riferimento, non è possibile estrarre le immagini incorporate quando viene visualizzata la pagina HTML. Di conseguenza, i riferimenti immagine devono essere percorsi assoluti per il rendering in HTML.

>[!NOTE]
>
>Sebbene sia possibile eseguire il rendering di diversi tipi di moduli in base al valore (ad esempio, moduli HTML o che contengono diritti di utilizzo), in questa sezione viene illustrato il rendering di moduli PDF interattivi.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Forms, consultate Riferimento [servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Riepilogo dei passaggi {#summary-of-steps}

Per eseguire il rendering di un modulo in base al valore, procedere come segue:

1. Includere i file di progetto.
1. Creare un oggetto API client Forms.
1. Fare riferimento alla struttura del modulo.
1. Eseguire il rendering di un modulo per valore.
1. Scrivere il flusso di dati del modulo nel browser Web del client.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se state creando un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate servizi Web, accertatevi di includere i file proxy.

**Creare un oggetto API client Forms**

Prima di poter importare i dati in un modulo PDF API client a livello di programmazione, è necessario creare un client di servizi di integrazione dati. Quando create un client di servizi, definite le impostazioni di connessione necessarie per richiamare un servizio.

**Riferimento alla struttura del modulo**

Quando si esegue il rendering di un modulo in base al valore, è necessario creare un `com.adobe.idp.Document` oggetto che contenga la struttura del modulo da sottoporre a rendering. È possibile fare riferimento a un file XDP esistente oppure creare in modo dinamico una struttura del modulo in fase di esecuzione e compilare un `com.adobe.idp.Document` modulo con tali dati.

>[!NOTE]
>
>Questa sezione e il relativo avvio rapido fanno riferimento a un file XDP esistente.

**Eseguire il rendering di un modulo per valore**

Per eseguire il rendering di un modulo in base al valore, passare un&#39; `com.adobe.idp.Document` istanza che contiene la struttura del modulo al `inDataDoc` parametro del metodo di rendering (può essere uno dei metodi di rendering dell&#39; `FormsServiceClient` oggetto come `renderPDFForm`, `(Deprecated) renderHTMLForm`e così via). Questo valore del parametro è in genere riservato ai dati uniti al modulo. Analogamente, trasmettere al `formQuery` parametro un valore di stringa vuoto. Normalmente questo parametro richiede un valore stringa che specifica il nome della struttura del modulo.

>[!NOTE]
>
>Se si desidera visualizzare i dati all&#39;interno del modulo, è necessario specificarli all&#39;interno dell&#39; `xfa:datasets` elemento . Per informazioni sull&#39;architettura XFA, visitate [https://partners.adobe.com/public/developer/xml/index_arch.html](https://partners.adobe.com/public/developer/xml/index_arch.html).

**Scrivere il flusso di dati del modulo nel browser Web del client**

Quando il servizio Forms esegue il rendering di un modulo per valore, restituisce un flusso di dati del modulo che è necessario scrivere nel browser Web del client. Una volta scritto nel browser Web del client, il modulo è visibile all&#39;utente.

**Consulta anche**

[Eseguire il rendering di un modulo per valore utilizzando l&#39;API Java](#render-a-form-by-value-using-the-java-api)

[Eseguire il rendering di un modulo per valore utilizzando l&#39;API del servizio Web](#render-a-form-by-value-using-the-web-service-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido dell&#39;API di Forms Service](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Invio di documenti al servizio Forms](/help/forms/developing/passing-documents-forms-service.md)

[Creazione di applicazioni Web per il rendering di moduli](/help/forms/developing/creating-web-applications-renders-forms.md)

## Eseguire il rendering di un modulo per valore utilizzando l&#39;API Java {#render-a-form-by-value-using-the-java-api}

Eseguire il rendering di un modulo in base al valore utilizzando l&#39;API Forms (Java):

1. Includi file di progetto

   Includete file JAR client, ad esempio adobe-forms-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto API client Forms

   * Creare un `ServiceClientFactory` oggetto che contenga proprietà di connessione.
   * Creare un `FormsServiceClient` oggetto utilizzando il relativo costruttore e passando l&#39; `ServiceClientFactory` oggetto.

1. Riferimento alla struttura del modulo

   * Creare un `java.io.FileInputStream` oggetto che rappresenta la struttura del modulo da sottoporre a rendering utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del file XDP.
   * Creare un `com.adobe.idp.Document` oggetto utilizzando il relativo costruttore e passando l&#39; `java.io.FileInputStream` oggetto.

1. Eseguire il rendering di un modulo per valore

   Richiama il metodo dell’ `FormsServiceClient` oggetto `renderPDFForm` e passa i seguenti valori:

   * Un valore di stringa vuoto. Normalmente questo parametro richiede un valore stringa che specifica il nome della struttura del modulo.
   * Un `com.adobe.idp.Document` oggetto che contiene la struttura del modulo. Normalmente questo valore di parametro è riservato ai dati uniti al modulo.
   * Un `PDFFormRenderSpec` oggetto che memorizza le opzioni di esecuzione. Si tratta di un parametro facoltativo e potete specificare `null` se non desiderate specificare le opzioni di esecuzione.
   * Un `URLSpec` oggetto che contiene valori URI richiesti dal servizio Forms.
   * Un `java.util.HashMap` oggetto che memorizza gli allegati. Si tratta di un parametro facoltativo e potete specificare `null` se non desiderate allegare file al modulo.
   Il `renderPDFForm` metodo restituisce un `FormsResult` oggetto che contiene un flusso di dati del modulo che può essere scritto nel browser Web del client.

1. Scrivere il flusso di dati del modulo nel browser Web del client

   * Creare un `com.adobe.idp.Document` oggetto richiamando il `FormsResult` metodo ‘s `getOutputContent` .
   * Ottenere il tipo di contenuto dell&#39; `com.adobe.idp.Document` oggetto richiamandone il `getContentType` metodo.
   * Impostare il tipo di contenuto dell&#39; `javax.servlet.http.HttpServletResponse` oggetto richiamandone `setContentType` il metodo e passando il tipo di contenuto dell&#39; `com.adobe.idp.Document` oggetto.
   * Creare un `javax.servlet.ServletOutputStream` oggetto utilizzato per scrivere il flusso di dati del modulo nel browser Web del client richiamando il `javax.servlet.http.HttpServletResponse` metodo dell&#39; `getOutputStream` oggetto.
   * Creare un `java.io.InputStream` oggetto richiamando il `com.adobe.idp.Document` metodo dell&#39; `getInputStream` oggetto.
   * Creare un array di byte e allocare le dimensioni dell&#39; `InputStream` oggetto. Richiamare il metodo dell&#39; `InputStream` oggetto `available` per ottenere le dimensioni dell&#39; `InputStream` oggetto.
   * Compilare l&#39;array di byte con il flusso di dati del modulo richiamando il `InputStream` `read`metodo dell&#39;oggetto e passando l&#39;array di byte come argomento.
   * Richiamare il metodo dell&#39; `javax.servlet.ServletOutputStream` oggetto `write` per inviare il flusso di dati del modulo al browser Web del client. Passa l&#39;array di byte al `write` metodo.

**Consulta anche**

[Rendering dei moduli per valore](/help/forms/developing/rendering-forms.md)

[Avvio rapido (modalità SOAP): Rendering per valore tramite l&#39;API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-by-value-using-the-java-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Eseguire il rendering di un modulo per valore utilizzando l&#39;API del servizio Web {#render-a-form-by-value-using-the-web-service-api}

Eseguire il rendering di un modulo per valore utilizzando l&#39;API di Forms (servizio Web):

1. Includi file di progetto

   * Creare classi proxy Java che utilizzano il WSDL del servizio Forms.
   * Includete le classi proxy Java nel percorso della classe.

1. Creare un oggetto API client Forms

   Creare un `FormsService` oggetto e impostare i valori di autenticazione.

1. Riferimento alla struttura del modulo

   * Creare un `java.io.FileInputStream` oggetto utilizzando il relativo costruttore. Passa un valore di stringa che specifica la posizione del file XDP.
   * Creare un `BLOB` oggetto utilizzando il relativo costruttore. L&#39; `BLOB` oggetto viene utilizzato per memorizzare un documento PDF cifrato con una password.
   * Creare un array di byte che memorizza il contenuto dell&#39; `java.io.FileInputStream` oggetto. È possibile determinare le dimensioni dell&#39;array di byte ottenendo le dimensioni dell&#39; `java.io.FileInputStream` oggetto utilizzando il relativo `available` metodo.
   * Compilare l&#39;array di byte con i dati del flusso richiamando il metodo dell&#39; `java.io.FileInputStream` oggetto `read` e passando l&#39;array di byte.
   * Compilare l&#39; `BLOB` oggetto richiamandone il `setBinaryData` metodo e passando l&#39;array di byte.

1. Eseguire il rendering di un modulo per valore

   Richiama il metodo dell’ `FormsService` oggetto `renderPDFForm` e passa i seguenti valori:

   * Un valore di stringa vuoto. Normalmente questo parametro richiede un valore stringa che specifica il nome della struttura del modulo.
   * Un `BLOB` oggetto che contiene la struttura del modulo. Normalmente questo valore di parametro è riservato ai dati uniti al modulo.
   * Un `PDFFormRenderSpec` oggetto che memorizza le opzioni di esecuzione. Si tratta di un parametro facoltativo e potete specificare `null` se non desiderate specificare le opzioni di esecuzione.
   * Un `URLSpec` oggetto che contiene valori URI richiesti dal servizio Forms.
   * Un `java.util.HashMap` oggetto che memorizza gli allegati. Si tratta di un parametro facoltativo e potete specificare `null` se non desiderate allegare file al modulo.
   * Un oggetto vuoto `com.adobe.idp.services.holders.BLOBHolder` compilato dal metodo. Viene utilizzato per memorizzare il modulo PDF di cui è stato effettuato il rendering.
   * Un oggetto vuoto `javax.xml.rpc.holders.LongHolder` compilato dal metodo. Questo argomento memorizza il numero di pagine nel modulo.
   * Un oggetto vuoto `javax.xml.rpc.holders.StringHolder` compilato dal metodo. (Questo argomento memorizza il valore delle impostazioni internazionali.)
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

[Rendering dei moduli per valore](#rendering-forms-by-value)

[Richiamo di moduli AEM con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
