---
title: Creazione di documenti PDF con dati XML inviati
seo-title: Creazione di documenti PDF con dati XML inviati
description: 'null'
seo-description: 'null'
uuid: 2676c614-8988-451b-ac7c-bd07731a3f5f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 62490230-a24e-419d-95bb-c0bb04a03f96
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Creazione di documenti PDF con dati XML inviati {#creating-pdf-documents-with-submittedxml-data}

## Creazione di documenti PDF con dati XML inviati {#creating-pdf-documents-with-submitted-xml-data}

Le applicazioni basate sul Web che consentono agli utenti di compilare moduli interattivi richiedono l&#39;invio dei dati al server. Il servizio Forms consente di recuperare i dati del modulo immessi dall&#39;utente in un modulo interattivo. È quindi possibile trasmettere i dati del modulo a un&#39;altra operazione del servizio AEM Forms e creare un documento PDF utilizzando i dati.

>[!NOTE]
>
>Prima di leggere questo contenuto, si consiglia di avere una buona conoscenza della gestione dei moduli inviati. Concetti come la relazione tra una struttura del modulo e i dati XML inviati sono trattati in Gestione dei moduli inviati.

Considerate il seguente flusso di lavoro che include tre servizi AEM Forms:

* Un utente invia dati XML al servizio Forms da un&#39;applicazione basata sul Web.
* Il servizio Forms consente di elaborare i campi modulo inviati ed estrarre. È possibile elaborare i dati del modulo. Ad esempio, i dati possono essere inviati a un database aziendale.
* I dati del modulo vengono inviati al servizio Output per creare un documento PDF non interattivo.
* Il documento PDF non interattivo è memorizzato in Content Services (obsoleto).

Il diagramma seguente fornisce una rappresentazione visiva del flusso di lavoro.

![cd_cd_finsrv_architecture_xml_pdf1](assets/cd_cd_finsrv_architecture_xml_pdf1.png)

Dopo che l&#39;utente ha inviato il modulo dal browser Web del client, il documento PDF non interattivo viene memorizzato in Content Services (obsoleto). L&#39;illustrazione seguente mostra un documento PDF memorizzato in Content Services (obsoleto).

![cd_cd_cs_gui](assets/cd_cd_cs_gui.png)

### Riepilogo dei passaggi {#summary-of-steps}

Per creare un documento PDF non interattivo con dati XML inviati e archiviarlo nel documento PDF in Content Services (obsoleto), eseguire le operazioni seguenti:

1. Includere i file di progetto.
1. Creare oggetti Forms, Output e Document Management.
1. Recuperare i dati del modulo utilizzando il servizio Forms.
1. Creare un documento PDF non interattivo utilizzando il servizio Output.
1. Archiviare il modulo PDF in Content Services (obsoleto) utilizzando il servizio Document Management.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, accertatevi di includere i file proxy.

**Creare oggetti Forms, Output e Gestione documenti**

Prima di eseguire un&#39;operazione API del servizio Forms a livello di programmazione, creare un oggetto API Client Forms. Analogamente, poiché questo flusso di lavoro richiama i servizi Output e Document Management, create sia un oggetto API Client di Output che un oggetto API client di Document Management.

**Recupero dei dati del modulo con il servizio Forms**

Recuperare i dati del modulo inviati al servizio Forms. Puoi elaborare i dati inviati per soddisfare i requisiti aziendali. Ad esempio, è possibile memorizzare i dati del modulo in un database aziendale. Tuttavia, per creare un documento PDF non interattivo, i dati del modulo vengono passati al servizio Output.

**Creare un documento PDF non interattivo utilizzando il servizio Output.**

Utilizzare il servizio Output per creare un documento PDF non interattivo basato su una struttura del modulo e sui dati del modulo XML. Nel flusso di lavoro, i dati del modulo vengono recuperati dal servizio Forms.

**Archiviare il modulo PDF in Content Services (obsoleto) utilizzando il servizio Document Management**

Utilizzare l&#39;API del servizio Document Management per archiviare un documento PDF in Content Services (obsoleto).

**Consulta anche**

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido dell&#39;API di Forms Service](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

### Creazione di un documento PDF con dati XML inviati tramite l&#39;API Java {#create-a-pdf-document-with-submitted-xml-data-using-the-java-api}

Creare un documento PDF con dati XML inviati utilizzando l&#39;API Forms, Output e Document Management (Java):

1. Includi file di progetto

   Includete file JAR client, ad esempio adobe-forms-client.jar, adobe-output-client.jar e adobe-contentservices-client.jar nel percorso di classe del progetto Java.

1. Creare oggetti Forms, Output e Gestione documenti

   * Creare un `ServiceClientFactory` oggetto che contenga proprietà di connessione.
   * Creare un `FormsServiceClient` oggetto utilizzando il relativo costruttore e passando l&#39; `ServiceClientFactory` oggetto.
   * Creare un `OutputClient` oggetto utilizzando il relativo costruttore e passando l&#39; `ServiceClientFactory` oggetto.
   * Creare un `DocumentManagementServiceClientImpl` oggetto utilizzando il relativo costruttore e passando l&#39; `ServiceClientFactory` oggetto.

1. Recupero dei dati del modulo con il servizio Forms

   * Richiama il metodo dell’ `FormsServiceClient` oggetto `processFormSubmission` e passa i seguenti valori:

      * L&#39; `com.adobe.idp.Document` oggetto che contiene i dati del modulo.
      * Valore stringa che specifica le variabili di ambiente, comprese tutte le intestazioni HTTP pertinenti. Specificate il tipo di contenuto da gestire specificando uno o più valori per la variabile di `CONTENT_TYPE` ambiente. Ad esempio, per gestire i dati XML, specificare il seguente valore di stringa per questo parametro: `CONTENT_TYPE=text/xml`.
      * Una stringa che specifica il valore dell&#39; `HTTP_USER_AGENT` intestazione, ad esempio `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
      * Un `RenderOptionsSpec` oggetto che memorizza le opzioni di esecuzione.
      Il `processFormSubmission` metodo restituisce un `FormsResult` oggetto contenente i risultati dell&#39;invio del modulo.

   * Determinare se il servizio Forms ha completato l&#39;elaborazione dei dati del modulo richiamando il `FormsResult` metodo dell&#39; `getAction` oggetto. Se questo metodo restituisce il valore, `0`i dati sono pronti per essere elaborati.
   * Recuperare i dati del modulo creando un `com.adobe.idp.Document` oggetto richiamando il `FormsResult` metodo dell&#39; `getOutputContent` oggetto. (Questo oggetto contiene i dati del modulo che è possibile inviare al servizio Output).
   * Creare un `java.io.InputStream` oggetto richiamando il `java.io.DataInputStream` costruttore e passando l&#39; `com.adobe.idp.Document` oggetto.
   * Creare un `org.w3c.dom.DocumentBuilderFactory` oggetto chiamando il `org.w3c.dom.DocumentBuilderFactory` metodo dell&#39; `newInstance` oggetto statico.
   * Creare un `org.w3c.dom.DocumentBuilder` oggetto richiamando il `org.w3c.dom.DocumentBuilderFactory` metodo dell&#39; `newDocumentBuilder` oggetto.
   * Creare un `org.w3c.dom.Document` oggetto richiamando il `org.w3c.dom.DocumentBuilder` metodo dell&#39; `parse` oggetto e passando l&#39; `java.io.InputStream` oggetto.
   * Recuperare il valore di ciascun nodo all&#39;interno del documento XML. Un modo per eseguire questa attività è creare un metodo personalizzato che accetta due parametri: l&#39; `org.w3c.dom.Document` oggetto e il nome del nodo di cui si desidera recuperare il valore. Questo metodo restituisce una stringa che rappresenta il valore del nodo. Nell&#39;esempio di codice che segue questo processo, viene chiamato questo metodo personalizzato `getNodeText`. Viene visualizzato il corpo di questo metodo.


1. Creare un documento PDF non interattivo utilizzando il servizio Output.

   Creare un documento PDF richiamando il metodo dell&#39; `OutputClient` oggetto `generatePDFOutput` e passando i seguenti valori:

   * Un valore `TransformationFormat` enum. Per generare un documento PDF, specificare `TransformationFormat.PDF`.
   * Una stringa che specifica il nome della struttura del modulo. Verificare che la struttura del modulo sia compatibile con i dati del modulo recuperati dal servizio Forms.
   * Una stringa che specifica il livello principale del contenuto in cui si trova la struttura del modulo.
   * Un `PDFOutputOptionsSpec` oggetto che contiene opzioni di esecuzione PDF.
   * Un `RenderOptionsSpec` oggetto che contiene opzioni di esecuzione del rendering.
   * L&#39; `com.adobe.idp.Document` oggetto che contiene l&#39;origine dati XML contenente i dati da unire alla struttura del modulo. Assicurarsi che l&#39;oggetto sia stato restituito dal `FormsResult` metodo dell&#39; `getOutputContent` .
   * Il `generatePDFOutput` metodo restituisce un `OutputResult` oggetto che contiene i risultati dell&#39;operazione.
   * Recuperare il documento PDF non interattivo richiamando il `OutputResult` metodo dell&#39; `getGeneratedDoc` oggetto. Questo metodo restituisce un’ `com.adobe.idp.Document` istanza che rappresenta il documento PDF non interattivo.

1. Archiviare il modulo PDF in Content Services (obsoleto) utilizzando il servizio Document Management

   Aggiungete il contenuto richiamando il metodo dell&#39; `DocumentManagementServiceClientImpl` oggetto `storeContent` e passando i seguenti valori:

   * Valore stringa che specifica lo store in cui viene aggiunto il contenuto. Lo store predefinito è `SpacesStore`. Questo valore è un parametro obbligatorio.
   * Un valore di stringa che specifica il percorso completo dello spazio in cui viene aggiunto il contenuto (ad esempio, `/Company Home/Test Directory`). Questo valore è un parametro obbligatorio.
   * Il nome del nodo che rappresenta il nuovo contenuto (ad esempio, `MortgageForm.pdf`). Questo valore è un parametro obbligatorio.
   * Un valore di stringa che specifica il tipo di nodo. Per aggiungere nuovo contenuto, ad esempio un file PDF, specificare `{https://www.alfresco.org/model/content/1.0}content`. Questo valore è un parametro obbligatorio.
   * Un `com.adobe.idp.Document` oggetto che rappresenta il contenuto. Questo valore è un parametro obbligatorio.
   * Un valore di stringa che specifica il valore di codifica (ad esempio, `UTF-8`). Questo valore è un parametro obbligatorio.
   * Un valore di `UpdateVersionType` enumerazione che specifica come gestire le informazioni sulla versione (ad esempio, `UpdateVersionType.INCREMENT_MAJOR_VERSION` per incrementare la versione del contenuto). ) Questo valore è un parametro obbligatorio.
   * Un&#39; `java.util.List` istanza che specifica gli aspetti correlati al contenuto. Questo valore è un parametro facoltativo ed è possibile specificarlo `null`.
   * Un `java.util.Map` oggetto che memorizza gli attributi del contenuto.
   Il `storeContent` metodo restituisce un `CRCResult` oggetto che descrive il contenuto. Utilizzando un `CRCResult` oggetto potete, ad esempio, ottenere il valore identificativo univoco del contenuto. Per eseguire questa operazione, richiamare il `CRCResult` metodo dell&#39; `getNodeUuid` .

**Consulta anche**

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
