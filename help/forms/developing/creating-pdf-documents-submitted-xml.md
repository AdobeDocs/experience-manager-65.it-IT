---
title: Creazione di documenti PDF con i dati SubmittedXML
seo-title: Creating PDF Documents with SubmittedXML Data
description: Utilizza il servizio Forms per recuperare i dati del modulo immessi dall’utente in un modulo interattivo. Passa i dati del modulo a un’altra operazione del servizio AEM Forms e crea un documento PDF utilizzando i dati.
seo-description: Use the Forms service to retrieve the form data that the user entered into an interactive form. Pass the form data to another AEM Forms service operation and create a PDF document using the data.
uuid: 2676c614-8988-451b-ac7c-bd07731a3f5f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 62490230-a24e-419d-95bb-c0bb04a03f96
role: Developer
exl-id: d9d5b94a-9d10-4d90-9e10-5142f30ba4a3
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1320'
ht-degree: 0%

---

# Creazione di documenti PDF con i dati XML inviati {#creating-pdf-documents-with-submittedxml-data}

**Gli esempi e gli esempi contenuti in questo documento sono solo per l’ambiente AEM Forms su JEE.**

## Creazione di documenti PDF con i dati XML inviati {#creating-pdf-documents-with-submitted-xml-data}

Le applicazioni basate sul Web che consentono agli utenti di compilare moduli interattivi richiedono l&#39;invio dei dati al server. Tramite il servizio Forms è possibile recuperare i dati del modulo immessi dall&#39;utente in un modulo interattivo. Quindi puoi passare i dati del modulo a un’altra operazione del servizio AEM Forms e creare un documento PDF utilizzando i dati.

>[!NOTE]
>
>Prima di leggere questo contenuto, è consigliabile avere una solida conoscenza della gestione dei moduli inviati. Concetti quali la relazione tra la progettazione di un modulo e i dati XML inviati sono trattati in Gestione dei Forms inviati.

Prendi in considerazione il seguente flusso di lavoro che coinvolge tre servizi AEM Forms:

* Un utente invia dati XML al servizio Forms da un&#39;applicazione basata sul Web.
* Il servizio Forms viene utilizzato per elaborare il modulo inviato ed estrarre i campi del modulo. I dati del modulo possono essere elaborati. Ad esempio, i dati possono essere inviati a un database aziendale.
* I dati del modulo vengono inviati al servizio di output per creare un documento PDF non interattivo.
* Il documento PDF non interattivo viene archiviato in Content Services (obsoleto).

Il diagramma seguente fornisce una rappresentazione visiva del flusso di lavoro.

![cd_cd_finsrv_architecture_xml_pdf1](assets/cd_cd_finsrv_architecture_xml_pdf1.png)

Dopo che l’utente ha inviato il modulo dal browser Web client, il documento PDF non interattivo viene memorizzato in Content Services (obsoleto). Nella figura seguente viene illustrato un documento PDF memorizzato in Content Services (obsoleto).

![cd_cd_cs_gui](assets/cd_cd_cs_gui.png)

### Riepilogo dei passaggi {#summary-of-steps}

Per creare un documento di PDF non interattivo con i dati XML inviati e memorizzarlo nel documento di PDF in Content Services (obsoleto), effettuare le seguenti operazioni:

1. Includi file di progetto.
1. Creare oggetti Forms, Output e Document Management.
1. Recupera i dati del modulo utilizzando il servizio Forms.
1. Crea un documento PDF non interattivo utilizzando il servizio di output.
1. Memorizzare il modulo PDF in Content Services (obsoleto) utilizzando il servizio Document Management.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

**Creazione di oggetti Forms, Output e Document Management**

Prima di poter eseguire un&#39;operazione API del servizio Forms a livello di programmazione, creare un oggetto API del client Forms. Analogamente, poiché questo flusso di lavoro richiama i servizi Output e Document Management, creare sia un oggetto API client di output che un oggetto API client di Document Management.

**Recuperare i dati del modulo tramite il servizio Forms**

Recupera i dati del modulo inviati al servizio Forms. È possibile elaborare i dati inviati per soddisfare i requisiti aziendali. È ad esempio possibile memorizzare i dati dei moduli in un database aziendale. Tuttavia, per creare un documento di PDF non interattivo, i dati del modulo vengono passati al servizio di output.

**Crea un documento PDF non interattivo utilizzando il servizio di output.**

Utilizzare il servizio di output per creare un documento PDF non interattivo basato sulla struttura di un modulo e sui dati del modulo XML. Nel flusso di lavoro, i dati del modulo vengono recuperati dal servizio Forms.

**Memorizzare il modulo PDF in Content Services (obsoleto) utilizzando il servizio Document Management**

Utilizza l’API del servizio Document Management per memorizzare un documento PDF in Content Services (obsoleto).

**Consulta anche**

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Guida introduttiva all’API di servizio Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

### Creare un documento PDF con i dati XML inviati utilizzando l’API Java {#create-a-pdf-document-with-submitted-xml-data-using-the-java-api}

Crea un documento PDF con i dati XML inviati utilizzando Forms, Output e Document Management API (Java):

1. Includi file di progetto

   Includi i file JAR dei client, come adobe-forms-client.jar, adobe-output-client.jar e adobe-contentservices-client.jar nel percorso di classe del progetto Java.

1. Creazione di oggetti Forms, Output e Document Management

   * Creare un `ServiceClientFactory` oggetto che contiene proprietà di connessione.
   * Creare un `FormsServiceClient` mediante il costruttore e passando il `ServiceClientFactory` oggetto.
   * Creare un `OutputClient` mediante il costruttore e passando il `ServiceClientFactory` oggetto.
   * Creare un `DocumentManagementServiceClientImpl` mediante il costruttore e passando il `ServiceClientFactory` oggetto.

1. Recuperare i dati del modulo tramite il servizio Forms

   * Richiama `FormsServiceClient` dell&#39;oggetto `processFormSubmission` e trasmettere i seguenti valori:

      * Il `com.adobe.idp.Document` oggetto che contiene i dati del modulo.
      * Valore stringa che specifica le variabili di ambiente, incluse tutte le intestazioni HTTP rilevanti. Specificare il tipo di contenuto da gestire specificando uno o più valori per `CONTENT_TYPE` variabile di ambiente. Ad esempio, per gestire i dati XML, specificare il seguente valore stringa per questo parametro: `CONTENT_TYPE=text/xml`.
      * Un valore stringa che specifica il `HTTP_USER_AGENT` valore dell’intestazione, come `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
      * A `RenderOptionsSpec` oggetto che memorizza le opzioni di runtime.

      Il `processFormSubmission` il metodo restituisce un `FormsResult` oggetto contenente i risultati dell’invio del modulo.

   * Determinare se il servizio Forms ha terminato l&#39;elaborazione dei dati del modulo richiamando `FormsResult` dell&#39;oggetto `getAction` metodo. Se questo metodo restituisce il valore `0`, i dati sono pronti per l’elaborazione.
   * Recuperare i dati del modulo creando un `com.adobe.idp.Document` oggetto richiamando il `FormsResult` dell&#39;oggetto `getOutputContent` metodo. Questo oggetto contiene dati del modulo che possono essere inviati al servizio di output.
   * Creare un `java.io.InputStream` oggetto richiamando il `java.io.DataInputStream` costruttore e passaggio `com.adobe.idp.Document` oggetto.
   * Creare un `org.w3c.dom.DocumentBuilderFactory` oggetto chiamando l&#39;oggetto statico `org.w3c.dom.DocumentBuilderFactory` dell&#39;oggetto `newInstance` metodo.
   * Creare un `org.w3c.dom.DocumentBuilder` oggetto richiamando il `org.w3c.dom.DocumentBuilderFactory` dell&#39;oggetto `newDocumentBuilder` metodo.
   * Creare un `org.w3c.dom.Document` oggetto richiamando il `org.w3c.dom.DocumentBuilder` dell&#39;oggetto `parse` e passando il `java.io.InputStream` oggetto.
   * Recuperate il valore di ciascun nodo all&#39;interno del documento XML. Un modo per eseguire questa attività consiste nel creare un metodo personalizzato che accetti due parametri: `org.w3c.dom.Document` e il nome del nodo di cui si desidera recuperare il valore. Questo metodo restituisce un valore stringa che rappresenta il valore del nodo. Nell&#39;esempio di codice che segue questo processo, questo metodo personalizzato viene chiamato `getNodeText`. Viene visualizzato il corpo di questo metodo.


1. Crea un documento PDF non interattivo utilizzando il servizio di output.

   Creare un documento PDF richiamando `OutputClient` dell&#39;oggetto `generatePDFOutput` e fornendo i seguenti valori:

   * A `TransformationFormat` valore enum. Per generare un documento PDF, specifica `TransformationFormat.PDF`.
   * Valore stringa che specifica il nome della struttura del modulo. Assicurati che la progettazione del modulo sia compatibile con i dati del modulo recuperati dal servizio Forms.
   * Valore stringa che specifica la directory principale del contenuto in cui si trova la struttura del modulo.
   * A `PDFOutputOptionsSpec` oggetto contenente le opzioni di runtime di PDF.
   * A `RenderOptionsSpec` oggetto contenente le opzioni di rendering in fase di esecuzione.
   * Il `com.adobe.idp.Document` oggetto contenente l&#39;origine dati XML contenente i dati da unire con la struttura del modulo. Assicurati che questo oggetto sia stato restituito da `FormsResult` dell&#39;oggetto `getOutputContent` metodo.
   * Il `generatePDFOutput` il metodo restituisce un `OutputResult` oggetto che contiene i risultati dell&#39;operazione.
   * Recupera il documento PDF non interattivo richiamando il `OutputResult` dell&#39;oggetto `getGeneratedDoc` metodo. Questo metodo restituisce un `com.adobe.idp.Document` che rappresenta il documento PDF non interattivo.

1. Memorizzare il modulo PDF in Content Services (obsoleto) utilizzando il servizio Document Management

   Aggiungi il contenuto richiamando `DocumentManagementServiceClientImpl` dell&#39;oggetto `storeContent` e fornendo i seguenti valori:

   * Valore stringa che specifica l&#39;archivio in cui viene aggiunto il contenuto. L’archivio predefinito è `SpacesStore`. Questo valore è un parametro obbligatorio.
   * Valore stringa che specifica il percorso completo dello spazio in cui viene aggiunto il contenuto (ad esempio, `/Company Home/Test Directory`). Questo valore è un parametro obbligatorio.
   * Il nome del nodo che rappresenta il nuovo contenuto (ad esempio, `MortgageForm.pdf`). Questo valore è un parametro obbligatorio.
   * Valore stringa che specifica il tipo di nodo. Per aggiungere nuovo contenuto, ad esempio un file PDF, specificare `{https://www.alfresco.org/model/content/1.0}content`. Questo valore è un parametro obbligatorio.
   * A `com.adobe.idp.Document` oggetto che rappresenta il contenuto. Questo valore è un parametro obbligatorio.
   * Valore stringa che specifica il valore di codifica, ad esempio `UTF-8`). Questo valore è un parametro obbligatorio.
   * Un `UpdateVersionType` valore di enumerazione che specifica come gestire le informazioni sulla versione (ad esempio, `UpdateVersionType.INCREMENT_MAJOR_VERSION` per incrementare la versione del contenuto. ) Questo valore è un parametro obbligatorio.
   * A `java.util.List` che specifica gli aspetti relativi al contenuto. Questo valore è un parametro facoltativo e puoi specificare `null`.
   * A `java.util.Map` oggetto che memorizza gli attributi del contenuto.

   Il `storeContent` il metodo restituisce un `CRCResult` oggetto che descrive il contenuto. Utilizzo di un `CRCResult` , ad esempio, puoi ottenere il valore dell’identificatore univoco del contenuto. Per eseguire questa attività, richiama `CRCResult` dell&#39;oggetto `getNodeUuid` metodo.

**Consulta anche**

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
