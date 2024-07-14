---
title: Rendering di Forms per valore
description: Utilizza Forms API (Java) per eseguire il rendering di un modulo per valore utilizzando Java API e Web Service API.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: a3a6a06d-ec90-4147-a5f0-e776a086ee12
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1822'
ht-degree: 0%

---

# Rendering di Forms per valore {#rendering-forms-by-value}

**Gli esempi e gli esempi contenuti in questo documento sono solo per AEM Forms in ambiente JEE.**

In genere, la progettazione di un modulo creata in Designer viene passata in base al servizio Forms. Le progettazioni dei moduli possono essere di grandi dimensioni e, di conseguenza, è più efficiente trasmetterle per riferimento per evitare di dover eseguire il marshalling dei byte di progettazione dei moduli in base al valore. Il servizio Forms può anche memorizzare in cache la struttura del modulo in modo che, quando viene memorizzata nella cache, non debba leggerla continuamente.

Se una progettazione di modulo contiene un attributo UUID, viene memorizzata nella cache. Il valore UUID è univoco per tutte le progettazioni di moduli e viene utilizzato per identificare in modo univoco un modulo. Quando si esegue il rendering di un modulo in base al valore, il modulo deve essere memorizzato nella cache solo se viene utilizzato ripetutamente. Tuttavia, se il modulo non viene utilizzato ripetutamente e deve essere univoco, puoi evitare di memorizzarlo in cache utilizzando le opzioni di memorizzazione in cache impostate utilizzando l’API di AEM Forms.

Il servizio Forms può anche risolvere la posizione del contenuto collegato all’interno della progettazione del modulo. Ad esempio, le immagini collegate a cui si fa riferimento nella progettazione del modulo sono URL relativi. Si presume che il contenuto collegato sia sempre relativo alla posizione di progettazione del modulo. Pertanto, la risoluzione del contenuto collegato consiste nel determinarne la posizione applicando il percorso relativo alla posizione di progettazione assoluta del modulo.

Invece di passare una progettazione di modulo per riferimento, è possibile passare una progettazione di modulo per valore. Il passaggio di una progettazione di modulo in base al valore è efficiente quando la progettazione di un modulo viene creata in modo dinamico, ovvero quando un&#39;applicazione client genera il codice XML che crea una progettazione di modulo durante la fase di esecuzione. In questa situazione, la struttura di un modulo non viene memorizzata in un repository fisico perché è memorizzata. Durante la creazione dinamica di una progettazione di moduli in fase di esecuzione e il suo passaggio in base al valore, è possibile memorizzare il modulo nella cache e migliorare le prestazioni del servizio Forms.

**Limitazioni del passaggio di un modulo per valore**

Quando la progettazione di un modulo viene passata in base al valore, si applicano le seguenti limitazioni:

* Nessun contenuto collegato relativo può essere incluso nella progettazione del modulo. Tutte le immagini e i frammenti devono essere incorporati nella struttura del modulo o essere assolutamente referenziati.
* Non è possibile eseguire calcoli lato server dopo il rendering del modulo. Se il modulo viene inviato nuovamente al servizio Forms, i dati vengono estratti e restituiti senza calcoli lato server.
* Poiché HTML può utilizzare solo immagini collegate in fase di runtime, non è possibile generare HTML con immagini incorporate. Questo perché il servizio Forms supporta le immagini incorporate con HTML recuperando le immagini da una progettazione di modulo di riferimento. Poiché una struttura di modulo passata da un valore non dispone di una posizione di riferimento, le immagini incorporate non possono essere estratte durante la visualizzazione della pagina HTML. Pertanto, i riferimenti immagine devono essere percorsi assoluti per essere sottoposti a rendering in HTML.

>[!NOTE]
>
>Sebbene sia possibile eseguire il rendering di diversi tipi di moduli in base al valore, ad esempio moduli HTML o moduli che contengono diritti di utilizzo, in questa sezione viene descritto come eseguire il rendering di PDF forms interattivi.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Forms, vedere [Riferimento ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Riepilogo dei passaggi {#summary-of-steps}

Per eseguire il rendering di un modulo in base al valore, effettuare le seguenti operazioni:

1. Includi file di progetto.
1. Crea un oggetto API client di Forms.
1. Fare riferimento alla progettazione del modulo.
1. Eseguire il rendering di un modulo per valore.
1. Scrivere il flusso di dati del modulo nel browser Web client.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

**Creare un oggetto API client di Forms**

Prima di poter importare i dati in modo programmatico in un modulo PDF API client, è necessario creare un client del servizio di integrazione dati. Quando si crea un client di servizio, vengono definite le impostazioni di connessione necessarie per richiamare un servizio.

**Fai riferimento alla progettazione del modulo**

Quando si esegue il rendering di un modulo in base al valore, è necessario creare un oggetto `com.adobe.idp.Document` contenente la struttura del modulo da riprodurre. È possibile fare riferimento a un file XDP esistente oppure creare dinamicamente una struttura di modulo in fase di esecuzione e popolare un `com.adobe.idp.Document` con tali dati.

>[!NOTE]
>
>Questa sezione e il relativo metodo di avvio rapido fanno riferimento a un file XDP esistente.

**Eseguire il rendering di un modulo per valore**

Per eseguire il rendering di un modulo in base al valore, passare un&#39;istanza `com.adobe.idp.Document` contenente la struttura del modulo al parametro `inDataDoc` del metodo di rendering (può essere uno qualsiasi dei metodi di rendering dell&#39;oggetto `FormsServiceClient`, ad esempio `renderPDFForm`, `(Deprecated) renderHTMLForm` e così via). Questo valore di parametro è in genere riservato ai dati che vengono uniti al modulo. Allo stesso modo, passare un valore stringa vuoto al parametro `formQuery`. Normalmente questo parametro richiede un valore stringa che specifica il nome della struttura del modulo.

>[!NOTE]
>
>Per visualizzare i dati all&#39;interno del modulo, è necessario specificare i dati all&#39;interno dell&#39;elemento `xfa:datasets`. Per informazioni sull&#39;architettura XFA, vai a [https://www.pdfa.org/norm-refs/XFA-3_3.pdf](https://www.pdfa.org/norm-refs/XFA-3_3.pdf).

**Scrivere il flusso di dati del modulo nel browser Web client**

Quando il servizio Forms esegue il rendering di un modulo in base al valore, restituisce un flusso di dati del modulo che è necessario scrivere nel browser Web client. Quando viene scritto nel browser Web client, il modulo è visibile all&#39;utente.

**Consulta anche**

[Eseguire il rendering di un modulo per valore utilizzando l’API Java](#render-a-form-by-value-using-the-java-api)

[Eseguire il rendering di un modulo per valore utilizzando l’API del servizio web](#render-a-form-by-value-using-the-web-service-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Guida introduttiva all’API di servizio Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Trasmissione di documenti al servizio Forms](/help/forms/developing/passing-documents-forms-service.md)

[Creazione di applicazioni Web per il rendering di Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

## Eseguire il rendering di un modulo per valore utilizzando l’API Java {#render-a-form-by-value-using-the-java-api}

Eseguire il rendering di un modulo per valore utilizzando l’API Forms (Java):

1. Includi file di progetto

   Includi i file JAR client, ad esempio adobe-forms-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto API client di Forms

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `FormsServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Fare riferimento alla progettazione del modulo

   * Creare un oggetto `java.io.FileInputStream` che rappresenta la struttura del modulo da riprodurre utilizzando il relativo costruttore e passando un valore stringa che specifica la posizione del file XDP.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Eseguire il rendering di un modulo in base al valore

   Richiama il metodo `renderPDFForm` dell&#39;oggetto `FormsServiceClient` e passa i seguenti valori:

   * Valore stringa vuoto. In genere questo parametro richiede un valore stringa che specifica il nome della struttura del modulo.
   * Oggetto `com.adobe.idp.Document` contenente la struttura del modulo. Normalmente questo valore di parametro è riservato ai dati che vengono uniti con il modulo.
   * Un oggetto `PDFFormRenderSpec` che memorizza le opzioni di runtime. Questo è un parametro facoltativo ed è possibile specificare `null` se non si desidera specificare le opzioni di runtime.
   * Oggetto `URLSpec` contenente i valori URI richiesti dal servizio Forms.
   * Oggetto `java.util.HashMap` che memorizza gli allegati. Questo è un parametro facoltativo ed è possibile specificare `null` se non si desidera allegare file al modulo.

   Il metodo `renderPDFForm` restituisce un oggetto `FormsResult` contenente un flusso di dati modulo che può essere scritto nel browser Web client.

1. Scrivere il flusso di dati del modulo nel browser Web client

   * Creare un oggetto `com.adobe.idp.Document` richiamando il metodo `getOutputContent` dell&#39;oggetto `FormsResult`.
   * Ottenere il tipo di contenuto dell&#39;oggetto `com.adobe.idp.Document` richiamando il relativo metodo `getContentType`.
   * Impostare il tipo di contenuto dell&#39;oggetto `javax.servlet.http.HttpServletResponse` richiamando il relativo metodo `setContentType` e passando il tipo di contenuto dell&#39;oggetto `com.adobe.idp.Document`.
   * Creare un oggetto `javax.servlet.ServletOutputStream` utilizzato per scrivere il flusso di dati del modulo nel browser Web client richiamando il metodo `getOutputStream` dell&#39;oggetto `javax.servlet.http.HttpServletResponse`.
   * Creare un oggetto `java.io.InputStream` richiamando il metodo `getInputStream` dell&#39;oggetto `com.adobe.idp.Document`.
   * Creare una matrice di byte e allocare le dimensioni dell&#39;oggetto `InputStream`. Richiama il metodo `available` dell&#39;oggetto `InputStream` per ottenere le dimensioni dell&#39;oggetto `InputStream`.
   * Compilare la matrice di byte con il flusso di dati del modulo richiamando il metodo `read` dell&#39;oggetto `InputStream` e passando la matrice di byte come argomento.
   * Richiama il metodo `write` dell&#39;oggetto `javax.servlet.ServletOutputStream` per inviare il flusso di dati del modulo al browser Web client. Passare la matrice di byte al metodo `write`.

**Consulta anche**

[Rendering di Forms per valore](/help/forms/developing/rendering-forms.md)

[Quick Start (modalità SOAP): rendering per valore utilizzando l’API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-by-value-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Eseguire il rendering di un modulo per valore utilizzando l’API del servizio web {#render-a-form-by-value-using-the-web-service-api}

Eseguire il rendering di un modulo in base al valore utilizzando l’API di Forms (servizio web):

1. Includi file di progetto

   * Creare classi proxy Java che utilizzano il servizio Forms WSDL.
   * Includi le classi proxy Java nel percorso della classe.

1. Creare un oggetto API client di Forms

   Creare un oggetto `FormsService` e impostare i valori di autenticazione.

1. Fare riferimento alla progettazione del modulo

   * Creare un oggetto `java.io.FileInputStream` utilizzando il relativo costruttore. Passa un valore stringa che specifica la posizione del file XDP.
   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare un documento PDF crittografato con una password.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `java.io.FileInputStream`. È possibile determinare la dimensione della matrice di byte ottenendo la dimensione dell&#39;oggetto `java.io.FileInputStream` utilizzando il relativo metodo `available`.
   * Compilare la matrice di byte con i dati di flusso richiamando il metodo `read` dell&#39;oggetto `java.io.FileInputStream` e passando la matrice di byte.
   * Compilare l&#39;oggetto `BLOB` richiamando il relativo metodo `setBinaryData` e passando la matrice di byte.

1. Eseguire il rendering di un modulo in base al valore

   Richiama il metodo `renderPDFForm` dell&#39;oggetto `FormsService` e passa i seguenti valori:

   * Valore stringa vuoto. In genere questo parametro richiede un valore stringa che specifica il nome della struttura del modulo.
   * Oggetto `BLOB` contenente la struttura del modulo. Normalmente questo valore di parametro è riservato ai dati che vengono uniti con il modulo.
   * Un oggetto `PDFFormRenderSpec` che memorizza le opzioni di runtime. Questo è un parametro facoltativo ed è possibile specificare `null` se non si desidera specificare le opzioni di runtime.
   * Oggetto `URLSpec` contenente i valori URI richiesti dal servizio Forms.
   * Oggetto `java.util.HashMap` che memorizza gli allegati. Questo è un parametro facoltativo ed è possibile specificare `null` se non si desidera allegare file al modulo.
   * Oggetto `com.adobe.idp.services.holders.BLOBHolder` vuoto popolato dal metodo. Viene utilizzato per memorizzare il modulo PDF di cui è stato eseguito il rendering.
   * Oggetto `javax.xml.rpc.holders.LongHolder` vuoto popolato dal metodo. Questo argomento consente di memorizzare il numero di pagine del modulo.
   * Oggetto `javax.xml.rpc.holders.StringHolder` vuoto popolato dal metodo. Questo argomento consente di memorizzare il valore delle impostazioni locali.
   * Oggetto `com.adobe.idp.services.holders.FormsResultHolder` vuoto che conterrà i risultati dell&#39;operazione.

   Il metodo `renderPDFForm` popola l&#39;oggetto `com.adobe.idp.services.holders.FormsResultHolder` passato come ultimo valore di argomento con un flusso di dati del modulo che deve essere scritto nel browser Web client.

1. Scrivere il flusso di dati del modulo nel browser Web client

   * Creare un oggetto `FormResult` ottenendo il valore del membro dati `value` dell&#39;oggetto `com.adobe.idp.services.holders.FormsResultHolder`.
   * Creare un oggetto `BLOB` contenente dati del modulo richiamando il metodo `getOutputContent` dell&#39;oggetto `FormsResult`.
   * Ottenere il tipo di contenuto dell&#39;oggetto `BLOB` richiamando il relativo metodo `getContentType`.
   * Impostare il tipo di contenuto dell&#39;oggetto `javax.servlet.http.HttpServletResponse` richiamando il relativo metodo `setContentType` e passando il tipo di contenuto dell&#39;oggetto `BLOB`.
   * Creare un oggetto `javax.servlet.ServletOutputStream` utilizzato per scrivere il flusso di dati del modulo nel browser Web client richiamando il metodo `getOutputStream` dell&#39;oggetto `javax.servlet.http.HttpServletResponse`.
   * Creare una matrice di byte e popolarla richiamando il metodo `getBinaryData` dell&#39;oggetto `BLOB`. Questa attività assegna il contenuto dell&#39;oggetto `FormsResult` alla matrice di byte.
   * Richiama il metodo `write` dell&#39;oggetto `javax.servlet.http.HttpServletResponse` per inviare il flusso di dati del modulo al browser Web client. Passare la matrice di byte al metodo `write`.

**Consulta anche**

[Rendering di Forms per valore](#rendering-forms-by-value)

[Richiamare AEM Forms utilizzando la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
