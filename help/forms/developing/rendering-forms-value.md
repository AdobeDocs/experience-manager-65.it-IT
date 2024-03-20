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
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1822'
ht-degree: 0%

---

# Rendering di Forms per valore {#rendering-forms-by-value}

**Gli esempi e gli esempi contenuti in questo documento sono solo per l’ambiente AEM Forms su JEE.**

In genere, la progettazione di un modulo creata in Designer viene passata tramite riferimento al servizio Forms. Le progettazioni dei moduli possono essere di grandi dimensioni e, di conseguenza, è più efficiente trasmetterle per riferimento per evitare di dover eseguire il marshalling dei byte di progettazione dei moduli in base al valore. Il servizio Forms può anche memorizzare in cache la struttura del modulo in modo che, quando viene memorizzata nella cache, non debba leggerla continuamente.

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
>Per ulteriori informazioni sul servizio Forms, consulta [Guida di riferimento dei servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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

**Fare riferimento alla progettazione del modulo**

Quando si esegue il rendering di un modulo in base al valore, è necessario creare un `com.adobe.idp.Document` oggetto che contiene la struttura del modulo da riprodurre. È possibile fare riferimento a un file XDP esistente oppure creare in modo dinamico una struttura di modulo in fase di esecuzione e compilare un `com.adobe.idp.Document` con quei dati.

>[!NOTE]
>
>Questa sezione e il relativo metodo di avvio rapido fanno riferimento a un file XDP esistente.

**Eseguire il rendering di un modulo in base al valore**

Per eseguire il rendering di un modulo in base al valore, trasmettere un `com.adobe.idp.Document` istanza che contiene la struttura del modulo per il metodo di rendering `inDataDoc` (può essere uno qualsiasi dei `FormsServiceClient` i metodi di rendering dell&#39;oggetto, come `renderPDFForm`, `(Deprecated) renderHTMLForm`e così via). Questo valore di parametro è in genere riservato ai dati che vengono uniti al modulo. Allo stesso modo, passa un valore stringa vuoto al `formQuery` parametro. Normalmente questo parametro richiede un valore stringa che specifica il nome della struttura del modulo.

>[!NOTE]
>
>Per visualizzare i dati all&#39;interno del modulo, è necessario specificare i dati all&#39;interno del `xfa:datasets` elemento. Per informazioni sull’architettura XFA, consulta [https://www.pdfa.org/norm-refs/XFA-3_3.pdf](https://www.pdfa.org/norm-refs/XFA-3_3.pdf).

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

   * Creare un `ServiceClientFactory` oggetto che contiene proprietà di connessione.
   * Creare un `FormsServiceClient` mediante il costruttore e passando il `ServiceClientFactory` oggetto.

1. Fare riferimento alla progettazione del modulo

   * Creare un `java.io.FileInputStream` oggetto che rappresenta la struttura del modulo da riprodurre utilizzando il relativo costruttore e passando un valore stringa che specifica la posizione del file XDP.
   * Creare un `com.adobe.idp.Document` mediante il costruttore e passando il `java.io.FileInputStream` oggetto.

1. Eseguire il rendering di un modulo in base al valore

   Richiama `FormsServiceClient` dell&#39;oggetto `renderPDFForm` e trasmettere i seguenti valori:

   * Valore stringa vuoto. In genere questo parametro richiede un valore stringa che specifica il nome della struttura del modulo.
   * A `com.adobe.idp.Document` oggetto che contiene la struttura del modulo. Normalmente questo valore di parametro è riservato ai dati che vengono uniti con il modulo.
   * A `PDFFormRenderSpec` oggetto che memorizza le opzioni di runtime. Questo è un parametro facoltativo e puoi specificare `null` se non si desidera specificare le opzioni di runtime.
   * A `URLSpec` oggetto contenente valori URI richiesti dal servizio Forms.
   * A `java.util.HashMap` oggetto che memorizza gli allegati. Questo è un parametro facoltativo e puoi specificare `null` se non si desidera allegare file al modulo.

   Il `renderPDFForm` il metodo restituisce un `FormsResult` oggetto contenente un flusso di dati modulo che può essere scritto nel browser web client.

1. Scrivere il flusso di dati del modulo nel browser Web client

   * Creare un `com.adobe.idp.Document` oggetto richiamando il `FormsResult` dell&#39;oggetto `getOutputContent` metodo.
   * Ottieni il tipo di contenuto del `com.adobe.idp.Document` oggetto richiamando il relativo `getContentType` metodo.
   * Imposta il `javax.servlet.http.HttpServletResponse` tipo di contenuto dell&#39;oggetto richiamando il relativo `setContentType` e passando il tipo di contenuto del `com.adobe.idp.Document` oggetto.
   * Creare un `javax.servlet.ServletOutputStream` oggetto utilizzato per scrivere il flusso di dati del modulo nel browser web client richiamando `javax.servlet.http.HttpServletResponse` dell&#39;oggetto `getOutputStream` metodo.
   * Creare un `java.io.InputStream` oggetto richiamando il `com.adobe.idp.Document` dell&#39;oggetto `getInputStream` metodo.
   * Creare una matrice di byte e allocare le dimensioni della `InputStream` oggetto. Richiama `InputStream` dell&#39;oggetto `available` metodo per ottenere le dimensioni del `InputStream` oggetto.
   * Popolare la matrice di byte con il flusso di dati del modulo richiamando `InputStream` dell&#39;oggetto `read`e passando la matrice di byte come argomento.
   * Richiama `javax.servlet.ServletOutputStream` dell&#39;oggetto `write` metodo per inviare il flusso di dati del modulo al browser web client. Passare la matrice di byte al `write` metodo.

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

   Creare un `FormsService` e impostare i valori di autenticazione.

1. Fare riferimento alla progettazione del modulo

   * Creare un `java.io.FileInputStream` mediante il costruttore. Passa un valore stringa che specifica la posizione del file XDP.
   * Creare un `BLOB` mediante il costruttore. Il `BLOB` L&#39;oggetto viene utilizzato per memorizzare un documento PDF crittografato con una password.
   * Creare una matrice di byte che memorizza il contenuto della `java.io.FileInputStream` oggetto. È possibile determinare le dimensioni della matrice di byte ottenendo `java.io.FileInputStream` dimensione dell&#39;oggetto utilizzando il relativo `available` metodo.
   * Compilare la matrice di byte con i dati di flusso richiamando `java.io.FileInputStream` dell&#39;oggetto `read` e passando la matrice di byte.
   * Popolare il `BLOB` oggetto richiamando il relativo `setBinaryData` e passando la matrice di byte.

1. Eseguire il rendering di un modulo in base al valore

   Richiama `FormsService` dell&#39;oggetto `renderPDFForm` e trasmettere i seguenti valori:

   * Valore stringa vuoto. In genere questo parametro richiede un valore stringa che specifica il nome della struttura del modulo.
   * A `BLOB` oggetto che contiene la struttura del modulo. Normalmente questo valore di parametro è riservato ai dati che vengono uniti con il modulo.
   * A `PDFFormRenderSpec` oggetto che memorizza le opzioni di runtime. Questo è un parametro facoltativo e puoi specificare `null` se non si desidera specificare le opzioni di runtime.
   * A `URLSpec` oggetto contenente valori URI richiesti dal servizio Forms.
   * A `java.util.HashMap` oggetto che memorizza gli allegati. Questo è un parametro facoltativo e puoi specificare `null` se non si desidera allegare file al modulo.
   * Un campo vuoto `com.adobe.idp.services.holders.BLOBHolder` oggetto popolato dal metodo. Viene utilizzato per memorizzare il modulo PDF di cui è stato eseguito il rendering.
   * Un campo vuoto `javax.xml.rpc.holders.LongHolder` oggetto popolato dal metodo. Questo argomento consente di memorizzare il numero di pagine del modulo.
   * Un campo vuoto `javax.xml.rpc.holders.StringHolder` oggetto popolato dal metodo. Questo argomento consente di memorizzare il valore delle impostazioni locali.
   * Un campo vuoto `com.adobe.idp.services.holders.FormsResultHolder` oggetto che conterrà i risultati dell&#39;operazione.

   Il `renderPDFForm` il metodo compila `com.adobe.idp.services.holders.FormsResultHolder` oggetto passato come ultimo valore di argomento con un flusso di dati del modulo che deve essere scritto nel browser web client.

1. Scrivere il flusso di dati del modulo nel browser Web client

   * Creare un `FormResult` dell&#39;oggetto ottenendo il valore del `com.adobe.idp.services.holders.FormsResultHolder` dell&#39;oggetto `value` membro dati.
   * Creare un `BLOB` oggetto che contiene i dati del modulo richiamando `FormsResult` dell&#39;oggetto `getOutputContent` metodo.
   * Ottieni il tipo di contenuto del `BLOB` oggetto richiamando il relativo `getContentType` metodo.
   * Imposta il `javax.servlet.http.HttpServletResponse` tipo di contenuto dell&#39;oggetto richiamando il relativo `setContentType` e passando il tipo di contenuto del `BLOB` oggetto.
   * Creare un `javax.servlet.ServletOutputStream` oggetto utilizzato per scrivere il flusso di dati del modulo nel browser web client richiamando `javax.servlet.http.HttpServletResponse` dell&#39;oggetto `getOutputStream` metodo.
   * Creare una matrice di byte e popolarla richiamando il `BLOB` dell&#39;oggetto `getBinaryData` metodo. Questa attività assegna il contenuto del `FormsResult` alla matrice di byte.
   * Richiama `javax.servlet.http.HttpServletResponse` dell&#39;oggetto `write` metodo per inviare il flusso di dati del modulo al browser web client. Passare la matrice di byte al `write` metodo.

**Consulta anche**

[Rendering di Forms per valore](#rendering-forms-by-value)

[Richiamare AEM Forms utilizzando la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
