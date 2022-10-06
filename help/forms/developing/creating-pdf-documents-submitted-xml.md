---
title: Creazione di documenti PDF con dati XML inviati
seo-title: Creating PDF Documents with SubmittedXML Data
description: Utilizzare il servizio Forms per recuperare i dati del modulo immessi dall’utente in un modulo interattivo. Passa i dati del modulo a un’altra operazione del servizio AEM Forms e crea un documento PDF utilizzando i dati.
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

# Creazione di documenti PDF con dati XML inviati {#creating-pdf-documents-with-submittedxml-data}

**Esempi ed esempi in questo documento sono solo per AEM Forms in ambiente JEE.**

## Creazione di documenti PDF con dati XML inviati {#creating-pdf-documents-with-submitted-xml-data}

Per le applicazioni basate sul Web che consentono agli utenti di compilare moduli interattivi, i dati devono essere inviati nuovamente al server. Utilizzando il servizio Forms, è possibile recuperare i dati del modulo immessi dall’utente in un modulo interattivo. È quindi possibile passare i dati del modulo a un’altra operazione del servizio AEM Forms e creare un documento PDF utilizzando i dati.

>[!NOTE]
>
>Prima di leggere questo contenuto, è consigliabile avere una conoscenza approfondita della gestione dei moduli inviati. Concetti come la relazione tra una struttura del modulo e i dati XML inviati sono descritti in Gestione di Forms inviati.

Considera il seguente flusso di lavoro che coinvolge tre servizi AEM Forms:

* Un utente invia dati XML al servizio Forms da un&#39;applicazione basata sul Web.
* Il servizio Forms viene utilizzato per elaborare il modulo inviato ed estrarre i campi del modulo. I dati del modulo possono essere elaborati. Ad esempio, i dati possono essere inviati a un database aziendale.
* I dati del modulo vengono inviati al servizio Output per creare un documento PDF non interattivo.
* Il documento PDF non interattivo viene memorizzato in Content Services (obsoleto).

Il diagramma seguente fornisce una rappresentazione visiva di questo flusso di lavoro.

![cd_cd_finsrv_architecture_xml_pdf1](assets/cd_cd_finsrv_architecture_xml_pdf1.png)

Dopo l’invio del modulo dal browser Web del client, il documento PDF non interattivo viene memorizzato in Content Services (obsoleto). Nell&#39;illustrazione seguente viene illustrato un documento PDF memorizzato in Content Services (obsoleto).

![cd_cd_cs_gui](assets/cd_cd_cs_gui.png)

### Riepilogo dei passaggi {#summary-of-steps}

Per creare un documento PDF non interattivo con dati XML inviati e archiviarlo nel documento PDF in Content Services (obsoleto), eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Creazione di oggetti Forms, Output e Document Management.
1. Recupera i dati del modulo utilizzando il servizio Forms.
1. Creare un documento PDF non interattivo utilizzando il servizio Output.
1. Archiviare il modulo PDF in Content Services (obsoleto) utilizzando il servizio Document Management.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

**Creazione di oggetti Forms, Output e Document Management**

Prima di eseguire un’operazione API del servizio Forms a livello di programmazione, crea un oggetto API client Forms. Allo stesso modo, poiché questo flusso di lavoro richiama i servizi di Output e Document Management, crea sia un oggetto API client di output che un oggetto API client di Document Management.

**Recupera i dati del modulo utilizzando il servizio Forms**

Recupera i dati del modulo inviati al servizio Forms. Puoi elaborare i dati inviati per soddisfare le tue esigenze aziendali. Ad esempio, è possibile memorizzare i dati del modulo in un database aziendale. Tuttavia, per creare un documento PDF non interattivo, i dati del modulo vengono passati al servizio Output.

**Creare un documento PDF non interattivo utilizzando il servizio Output.**

Utilizzare il servizio Output per creare un documento PDF non interattivo basato su una struttura del modulo e sui dati del modulo XML. Nel flusso di lavoro, i dati del modulo vengono recuperati dal servizio Forms.

**Archiviare il modulo PDF in Content Services (obsoleto) utilizzando il servizio Document Management**

Utilizza l’API del servizio Gestione documenti per memorizzare un documento PDF in Content Services (obsoleto).

**Consulta anche**

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API di Forms Service](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

### Creare un documento PDF con i dati XML inviati tramite l’API Java {#create-a-pdf-document-with-submitted-xml-data-using-the-java-api}

Creare un documento PDF con i dati XML inviati utilizzando l’API Forms, Output e Document Management (Java):

1. Includi file di progetto

   Includi file JAR client, come adobe-forms-client.jar, adobe-output-client.jar e adobe-contentservices-client.jar nel percorso classe del progetto Java.

1. Creazione di oggetti Forms, Output e Document Management

   * Crea un `ServiceClientFactory` oggetto contenente le proprietà di connessione.
   * Crea un `FormsServiceClient` utilizzando il relativo costruttore e passando `ServiceClientFactory` oggetto.
   * Crea un `OutputClient` utilizzando il relativo costruttore e passando `ServiceClientFactory` oggetto.
   * Crea un `DocumentManagementServiceClientImpl` utilizzando il relativo costruttore e passando `ServiceClientFactory` oggetto.

1. Recupera i dati del modulo utilizzando il servizio Forms

   * Richiama il `FormsServiceClient` dell’oggetto `processFormSubmission` e passare i seguenti valori:

      * La `com.adobe.idp.Document` oggetto contenente i dati del modulo.
      * Valore stringa che specifica le variabili di ambiente, comprese tutte le intestazioni HTTP rilevanti. Specifica il tipo di contenuto da gestire specificando uno o più valori per il `CONTENT_TYPE` variabile di ambiente. Ad esempio, per gestire i dati XML, specificare il seguente valore di stringa per questo parametro: `CONTENT_TYPE=text/xml`.
      * Un valore stringa che specifica la variabile `HTTP_USER_AGENT` valore di intestazione, ad esempio `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
      * A `RenderOptionsSpec` oggetto che memorizza le opzioni di esecuzione.

      La `processFormSubmission` restituisce un `FormsResult` oggetto contenente i risultati dell&#39;invio del modulo.

   * Determinare se il servizio Forms ha completato l’elaborazione dei dati del modulo richiamando il `FormsResult` dell’oggetto `getAction` metodo . Se questo metodo restituisce il valore `0`, i dati sono pronti per essere elaborati.
   * Recupera i dati del modulo creando un `com.adobe.idp.Document` richiamando l&#39;oggetto `FormsResult` dell’oggetto `getOutputContent` metodo . Questo oggetto contiene i dati del modulo che possono essere inviati al servizio Output.
   * Crea un `java.io.InputStream` richiamando l&#39;oggetto `java.io.DataInputStream` costruttore e passaggio `com.adobe.idp.Document` oggetto.
   * Crea un `org.w3c.dom.DocumentBuilderFactory` chiamando l&#39;oggetto statico `org.w3c.dom.DocumentBuilderFactory` dell’oggetto `newInstance` metodo .
   * Crea un `org.w3c.dom.DocumentBuilder` richiamando l&#39;oggetto `org.w3c.dom.DocumentBuilderFactory` dell’oggetto `newDocumentBuilder` metodo .
   * Crea un `org.w3c.dom.Document` richiamando l&#39;oggetto `org.w3c.dom.DocumentBuilder` dell’oggetto `parse` e passare `java.io.InputStream` oggetto.
   * Recupera il valore di ogni nodo all&#39;interno del documento XML. Un modo per eseguire questa attività consiste nel creare un metodo personalizzato che accetta due parametri: la `org.w3c.dom.Document` e il nome del nodo di cui si desidera recuperare il valore. Questo metodo restituisce un valore stringa che rappresenta il valore del nodo. Nell&#39;esempio di codice che segue questo processo, questo metodo personalizzato viene chiamato `getNodeText`. Viene mostrato il corpo di questo metodo.


1. Creare un documento PDF non interattivo utilizzando il servizio Output.

   Creare un documento PDF richiamando il `OutputClient` dell’oggetto `generatePDFOutput` e passando i seguenti valori:

   * A `TransformationFormat` valore enum. Per generare un documento PDF, specificare `TransformationFormat.PDF`.
   * Valore stringa che specifica il nome della struttura del modulo. Verificare che la struttura del modulo sia compatibile con i dati del modulo recuperati dal servizio Forms.
   * Valore stringa che specifica la directory principale del contenuto in cui si trova la struttura del modulo.
   * A `PDFOutputOptionsSpec` oggetto contenente le opzioni di runtime di PDF.
   * A `RenderOptionsSpec` oggetto contenente le opzioni di esecuzione del rendering.
   * La `com.adobe.idp.Document` oggetto contenente l’origine dati XML contenente i dati da unire alla struttura del modulo. Assicurati che questo oggetto sia stato restituito dal `FormsResult` dell’oggetto `getOutputContent` metodo .
   * La `generatePDFOutput` restituisce un `OutputResult` oggetto contenente i risultati dell&#39;operazione.
   * Recupera il documento PDF non interattivo richiamando il `OutputResult` dell’oggetto `getGeneratedDoc` metodo . Questo metodo restituisce un `com.adobe.idp.Document` istanza che rappresenta il documento PDF non interattivo.

1. Archiviare il modulo PDF in Content Services (obsoleto) utilizzando il servizio Document Management

   Aggiungi il contenuto richiamando il `DocumentManagementServiceClientImpl` dell’oggetto `storeContent` e passando i seguenti valori:

   * Valore stringa che specifica l&#39;archivio in cui viene aggiunto il contenuto. Lo store predefinito è `SpacesStore`. Questo valore è un parametro obbligatorio.
   * Un valore stringa che specifica il percorso completo dello spazio in cui viene aggiunto il contenuto (ad esempio, `/Company Home/Test Directory`). Questo valore è un parametro obbligatorio.
   * Nome del nodo che rappresenta il nuovo contenuto (ad esempio, `MortgageForm.pdf`). Questo valore è un parametro obbligatorio.
   * Valore stringa che specifica il tipo di nodo. Per aggiungere nuovo contenuto, ad esempio un file PDF, specificare `{https://www.alfresco.org/model/content/1.0}content`. Questo valore è un parametro obbligatorio.
   * A `com.adobe.idp.Document` oggetto che rappresenta il contenuto. Questo valore è un parametro obbligatorio.
   * Valore stringa che specifica il valore di codifica, ad esempio `UTF-8`). Questo valore è un parametro obbligatorio.
   * Un `UpdateVersionType` valore di enumerazione che specifica come gestire le informazioni sulla versione (ad esempio, `UpdateVersionType.INCREMENT_MAJOR_VERSION` per incrementare la versione del contenuto. ) Questo valore è un parametro obbligatorio.
   * A `java.util.List` istanza che specifica gli aspetti correlati al contenuto. Questo valore è un parametro facoltativo ed è possibile specificare `null`.
   * A `java.util.Map` oggetto che memorizza gli attributi del contenuto.

   La `storeContent` restituisce un `CRCResult` oggetto che descrive il contenuto. Utilizzo di un `CRCResult` ad esempio, puoi ottenere il valore di identificatore univoco del contenuto. Per eseguire questa operazione, richiamare la `CRCResult` dell’oggetto `getNodeUuid` metodo .

**Consulta anche**

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
