---
title: Trasmissione di documenti a FormsService
seo-title: Passing Documents to the FormsService
description: Passare al servizio Forms un oggetto com.adobe.idp.Document contenente la struttura del modulo. Il servizio Forms esegue il rendering della struttura del modulo situata nell’oggetto com.adobe.idp.Document .
seo-description: Pass a com.adobe.idp.Document object that contains the form design to the Forms service. The Forms service renders the form design located in the com.adobe.idp.Document object.
uuid: 841e97f3-ebb8-4340-81a9-b6db11f0ec82
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: e23de3c3-f8a0-459f-801e-a0942fb1c6aa
role: Developer
exl-id: 29c7ebda-407a-464b-a9db-054163f5b737
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1684'
ht-degree: 0%

---

# Trasmissione di documenti al servizio Forms {#passing-documents-to-the-formsservice}

**Esempi ed esempi in questo documento sono solo per AEM Forms in ambiente JEE.**

Il servizio AEM Forms esegue il rendering dei PDF forms interattivi sui dispositivi client, in genere nei browser web, per raccogliere informazioni dagli utenti. Un modulo PDF interattivo si basa su una struttura del modulo generalmente salvata come file XDP e creata in Designer. A partire da AEM Forms, puoi trasmettere un `com.adobe.idp.Document` oggetto contenente la struttura del modulo al servizio Forms. Il servizio Forms esegue quindi il rendering della struttura del modulo che si trova nel `com.adobe.idp.Document` oggetto.

Il vantaggio di passare un `com.adobe.idp.Document` oggetto del servizio Forms: altre operazioni del servizio restituiscono un `com.adobe.idp.Document` istanza. Cioè, puoi ottenere un `com.adobe.idp.Document` istanza da un&#39;altra operazione di servizio ed esegui il rendering. Ad esempio, si supponga che un file XDP sia memorizzato in un nodo Content Services (obsoleto) denominato `/Company Home/Form Designs`, come illustrato nella figura seguente.

È possibile recuperare in modo programmatico il file Loan.xdp da Content Services (obsoleto) (obsoleto) e passare il file XDP al servizio Forms all&#39;interno di un `com.adobe.idp.Document` oggetto.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Forms, vedi [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Riepilogo dei passaggi {#summary-of-steps}

Per passare un documento ottenuto da Content Services (obsoleto) (obsoleto) al servizio Forms, esegui le seguenti attività:

1. Includi file di progetto.
1. Creare un oggetto Forms e un oggetto API client di gestione documenti.
1. Recupera la struttura del modulo da Content Services (obsoleto).
1. Eseguire il rendering del modulo PDF interattivo.
1. Eseguire un’azione con il flusso di dati del modulo.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, includi i file proxy.

**Creare un oggetto Forms e un oggetto API client di gestione dei documenti**

Prima di eseguire un’operazione API del servizio Forms a livello di programmazione, crea un oggetto API client Forms. Inoltre, poiché questo flusso di lavoro recupera un file XDP da Content Services (obsoleto), crea un oggetto API di gestione dei documenti.

**Recupera la struttura del modulo da Content Services (obsoleto)**

Recupera il file XDP da Content Services (obsoleto) utilizzando l’API Java o del servizio Web. Il file XDP viene restituito all&#39;interno di un `com.adobe.idp.Document` istanza (o `BLOB` (se utilizzi servizi web). È quindi possibile passare il `com.adobe.idp.Document` al servizio Forms.

**Rendering di un modulo PDF interattivo**

Per eseguire il rendering di un modulo interattivo, passare il `com.adobe.idp.Document` istanza restituita da Content Services (obsoleto) al servizio Forms.

>[!NOTE]
>
>Puoi trasmettere un `com.adobe.idp.Document` che contiene la struttura del modulo al servizio Forms. Due nuovi metodi denominati `renderPDFForm2` e `renderHTMLForm2` accettare `com.adobe.idp.Document` oggetto contenente una struttura del modulo.

**Eseguire un’azione con il flusso di dati del modulo**

A seconda del tipo di applicazione client, è possibile scrivere il modulo in un browser Web client o salvarlo come file PDF. In genere, un’applicazione basata sul Web scrive il modulo nel browser web. Tuttavia, in genere, un’applicazione desktop salva il modulo come file PDF.

**Consulta anche**

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API di Forms Service](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

## Trasmettere documenti al servizio Forms utilizzando l’API Java {#pass-documents-to-the-forms-service-using-the-java-api}

Passa un documento ottenuto da Content Services (obsoleto) utilizzando il servizio Forms e l’API Content Services (obsoleto):

1. Includi file di progetto

   Includi file JAR client, come adobe-forms-client.jar e adobe-contentservices-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto Forms e un oggetto API client di gestione dei documenti

   * Crea un `ServiceClientFactory` oggetto contenente le proprietà di connessione. (Vedi [Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * Crea un `FormsServiceClient` utilizzando il relativo costruttore e passando `ServiceClientFactory` oggetto.
   * Crea un `DocumentManagementServiceClientImpl` utilizzando il relativo costruttore e passando `ServiceClientFactory` oggetto.

1. Recupera la struttura del modulo da Content Services (obsoleto)

   Richiama il `DocumentManagementServiceClientImpl` dell’oggetto `retrieveContent` e passare i seguenti valori:

   * Valore stringa che specifica l&#39;archivio in cui viene aggiunto il contenuto. Lo store predefinito è `SpacesStore`. Questo valore è un parametro obbligatorio.
   * Valore stringa che specifica il percorso completo del contenuto da recuperare (ad esempio, `/Company Home/Form Designs/Loan.xdp`). Questo valore è un parametro obbligatorio.
   * Valore stringa che specifica la versione. Questo valore è un parametro facoltativo ed è possibile trasmettere una stringa vuota. In questa situazione, viene recuperata la versione più recente.

   La `retrieveContent` restituisce un `CRCResult` oggetto che contiene il file XDP. Ottenere un `com.adobe.idp.Document` richiamando la `CRCResult` dell’oggetto `getDocument` metodo .

1. Rendering di un modulo PDF interattivo

   Richiama il `FormsServiceClient` dell’oggetto `renderPDFForm2` e passare i seguenti valori:

   * A `com.adobe.idp.Document` oggetto contenente la struttura del modulo recuperata da Content Services (obsoleto).
   * A `com.adobe.idp.Document` oggetto contenente i dati da unire al modulo. Se non si desidera unire i dati, passare un valore vuoto `com.adobe.idp.Document` oggetto.
   * A `PDFFormRenderSpec` oggetto che memorizza le opzioni di esecuzione. Questo valore è un parametro facoltativo ed è possibile specificare `null` se non si desidera specificare le opzioni di esecuzione.
   * A `URLSpec` oggetto che contiene valori URI. Questo valore è un parametro facoltativo ed è possibile specificare `null`.
   * A `java.util.HashMap` oggetto che memorizza gli allegati di file. Questo valore è un parametro facoltativo ed è possibile specificare `null` se non si desidera allegare file al modulo.

   La `renderPDFForm` restituisce un `FormsResult` oggetto che contiene un flusso di dati del modulo che deve essere scritto nel browser Web client.

1. Eseguire un’azione con il flusso di dati del modulo

   * Crea un `com.adobe.idp.Document` richiamando l&#39;oggetto `FormsResult` oggetto ‘s `getOutputContent` metodo .
   * Ottieni il tipo di contenuto del `com.adobe.idp.Document` richiamandone l&#39;oggetto `getContentType` metodo .
   * Imposta la `javax.servlet.http.HttpServletResponse` tipo di contenuto dell’oggetto richiamandone il tipo `setContentType` e passare il tipo di contenuto `com.adobe.idp.Document` oggetto.
   * Crea un `javax.servlet.ServletOutputStream` oggetto utilizzato per scrivere il flusso di dati del modulo nel browser Web client richiamando il `javax.servlet.http.HttpServletResponse` dell’oggetto `getOutputStream` metodo .
   * Crea un `java.io.InputStream` richiamando l&#39;oggetto `com.adobe.idp.Document` dell’oggetto `getInputStream` metodo .
   * Creare un array di byte e compilarlo con il flusso di dati del modulo richiamando il `InputStream` dell’oggetto `read` metodo . Passa l&#39;array di byte come argomento.
   * Richiama il `javax.servlet.ServletOutputStream` dell’oggetto `write` per inviare il flusso di dati del modulo al browser Web client. Passa l&#39;array di byte al `write` metodo .

**Consulta anche**

[Avvio rapido (modalità SOAP): Trasmissione di documenti al servizio Forms tramite l’API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-passing-documents-to-the-forms-service-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Trasmettere i documenti al servizio Forms utilizzando l’API del servizio Web {#pass-documents-to-the-forms-service-using-the-web-service-api}

Passa un documento ottenuto da Content Services (obsoleto) utilizzando il servizio Forms e l’API Content Services (obsoleto) (servizio Web):

1. Includi file di progetto

   Creare un progetto Microsoft .NET che utilizza MTOM. Poiché questa applicazione client richiama due servizi AEM Forms, crea due riferimenti al servizio. Utilizza la seguente definizione WSDL per il riferimento al servizio associato al servizio Forms: `http://localhost:8080/soap/services/FormsService?WSDL&lc_version=9.0.1`.

   Utilizzare la seguente definizione WSDL per il riferimento al servizio associato al servizio Document Management: `http://localhost:8080/soap/services/DocumentManagementService?WSDL&lc_version=9.0.1`.

   Perché `BLOB` il tipo di dati è comune a entrambi i riferimenti di servizio e definisce completamente il `BLOB` tipo di dati quando viene utilizzato. All&#39;avvio rapido del servizio Web corrispondente, `BLOB` le istanze sono completamente qualificate.

   >[!NOTE]
   >
   >Sostituisci `localhost`con l’indirizzo IP del server che ospita AEM Forms.

1. Creare un oggetto Forms e un oggetto API client di gestione dei documenti

   * Crea un `FormsServiceClient` utilizzando il relativo costruttore predefinito.
   * Crea un `FormsServiceClient.Endpoint.Address` utilizzando `System.ServiceModel.EndpointAddress` costruttore. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/FormsService?WSDL`). Non è necessario utilizzare il `lc_version` attributo. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Crea un `System.ServiceModel.BasicHttpBinding` ottenendo il valore del `FormsServiceClient.Endpoint.Binding` campo . Imposta il valore restituito su `BasicHttpBinding`.
   * Imposta la `System.ServiceModel.BasicHttpBinding` dell’oggetto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegnare il nome utente del modulo di AEM al campo `FormsServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore della password corrispondente al campo `FormsServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

   >[!NOTE]
   >
   >Ripeti questi passaggi per `DocumentManagementServiceClient`client di servizio.

1. Recupera la struttura del modulo da Content Services (obsoleto)

   Recupera il contenuto richiamando il `DocumentManagementServiceClient` dell’oggetto `retrieveContent` e passando i seguenti valori:

   * Valore stringa che specifica l&#39;archivio in cui viene aggiunto il contenuto. Lo store predefinito è `SpacesStore`. Questo valore è un parametro obbligatorio.
   * Valore stringa che specifica il percorso completo del contenuto da recuperare (ad esempio, `/Company Home/Form Designs/Loan.xdp`). Questo valore è un parametro obbligatorio.
   * Valore stringa che specifica la versione. Questo valore è un parametro facoltativo ed è possibile trasmettere una stringa vuota. In questa situazione, viene recuperata la versione più recente.
   * Parametro di output della stringa che memorizza il valore del collegamento di ricerca.
   * A `BLOB` parametro di output che memorizza il contenuto. Puoi utilizzare questo parametro di output per recuperare il contenuto.
   * A `ServiceReference1.MyMapOf_xsd_string_To_xsd_anyType` parametro di output che memorizza gli attributi di contenuto.
   * A `CRCResult` parametro di output. Invece di utilizzare questo oggetto, è possibile utilizzare il `BLOB` parametro di output per ottenere il contenuto.

1. Rendering di un modulo PDF interattivo

   Richiama il `FormsServiceClient` dell’oggetto `renderPDFForm2` e passare i seguenti valori:

   * A `BLOB` oggetto contenente la struttura del modulo recuperata da Content Services (obsoleto).
   * A `BLOB` oggetto contenente i dati da unire al modulo. Se non si desidera unire i dati, passare un valore vuoto `BLOB` oggetto.
   * A `PDFFormRenderSpec` oggetto che memorizza le opzioni di esecuzione. Questo valore è un parametro facoltativo ed è possibile specificare `null` se non si desidera specificare le opzioni di esecuzione.
   * A `URLSpec` oggetto che contiene valori URI. Questo valore è un parametro facoltativo ed è possibile specificare `null`.
   * A `Map` oggetto che memorizza gli allegati di file. Questo valore è un parametro facoltativo ed è possibile specificare `null` se non si desidera allegare file al modulo.
   * Un parametro di output lungo utilizzato per memorizzare il conteggio delle pagine.
   * Un parametro di output della stringa utilizzato per memorizzare il valore delle impostazioni internazionali.
   * A `FormsResult` parametro di output utilizzato per memorizzare il modulo interattivo di PDF `.`

   La `renderPDFForm2` restituisce un `FormsResult` oggetto contenente il modulo interattivo di PDF.

1. Eseguire un’azione con il flusso di dati del modulo

   * Crea un `BLOB` oggetto che contiene i dati del modulo ottenendo il valore `FormsResult` dell’oggetto `outputContent` campo .
   * Crea un `System.IO.FileStream` richiamando il relativo costruttore. Passa un valore stringa che rappresenta la posizione del file del documento PDF interattivo e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto del `BLOB` oggetto recuperato dal `FormsResult` oggetto. Compilare l’array di byte ottenendo il valore del `BLOB` dell’oggetto `MTOM` membro dati.
   * Crea un `System.IO.BinaryWriter` richiamando il relativo costruttore e passando `System.IO.FileStream` oggetto.
   * Scrivi il contenuto dell’array di byte in un file PDF richiamando il `System.IO.BinaryWriter` dell’oggetto `Write` e passare l&#39;array di byte.

**Consulta anche**

[Richiamo di AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
