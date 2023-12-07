---
title: Passaggio di documenti al servizio Forms
description: Passa al servizio Forms un oggetto com.adobe.idp.Document contenente la struttura del modulo. Il servizio Forms esegue il rendering della struttura del modulo nell'oggetto com.adobe.idp.Document.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 29c7ebda-407a-464b-a9db-054163f5b737
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '1677'
ht-degree: 0%

---

# Trasmissione di documenti al servizio Forms {#passing-documents-to-the-formsservice}

**Gli esempi e gli esempi contenuti in questo documento sono solo per l’ambiente AEM Forms su JEE.**

Il servizio AEM Forms esegue il rendering dei PDF forms interattivi sui dispositivi client, in genere i browser web, per raccogliere informazioni dagli utenti. Un modulo PDF interattivo si basa su una struttura di modulo che in genere viene salvata come file XDP e creata in Designer. A partire da AEM Forms, puoi trasmettere un `com.adobe.idp.Document` oggetto che contiene la struttura del modulo per il servizio Forms. Il servizio Forms esegue quindi il rendering della progettazione del modulo in `com.adobe.idp.Document` oggetto.

Il vantaggio di superare un `com.adobe.idp.Document` al servizio Forms è che altre operazioni del servizio restituiscono un `com.adobe.idp.Document` dell&#39;istanza. In altre parole, puoi ottenere un `com.adobe.idp.Document` da un&#39;altra operazione di servizio ed eseguirne il rendering. Ad esempio, si supponga che un file XDP sia memorizzato in un nodo Content Services (obsoleto) denominato `/Company Home/Form Designs`, come illustrato nella figura seguente.

Puoi recuperare in modo programmatico Loan.xdp da Content Services (obsoleto) (obsoleto) e passare il file XDP al servizio Forms all’interno di un `com.adobe.idp.Document` oggetto.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Forms, consulta [Guida di riferimento dei servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Riepilogo dei passaggi {#summary-of-steps}

Per passare un documento ottenuto da Content Services (obsoleto) (obsoleto) al servizio Forms, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Creare un oggetto Forms e un oggetto API Client di Document Management.
1. Recupera la progettazione del modulo da Content Services (obsoleto).
1. Esegui il rendering del modulo di PDF interattivo.
1. Eseguire un&#39;azione con il flusso di dati del modulo.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se si utilizzano servizi Web, includere i file proxy.

**Creare un oggetto Forms e un oggetto API client di Document Management**

Prima di poter eseguire un&#39;operazione API del servizio Forms a livello di programmazione, creare un oggetto API del client Forms. Inoltre, poiché questo flusso di lavoro recupera un file XDP da Content Services (obsoleto), crea un oggetto API di gestione dei documenti.

**Recuperare la progettazione del modulo da Content Services (obsoleto)**

Recupera il file XDP da Content Services (obsoleto) utilizzando l’API Java o del servizio web. Il file XDP viene restituito all’interno di un `com.adobe.idp.Document` istanza (o un `BLOB` se si utilizzano i servizi web). È quindi possibile trasmettere `com.adobe.idp.Document` al servizio Forms.

**Rendering di un modulo PDF interattivo**

Per riprodurre un modulo interattivo, trasmettere `com.adobe.idp.Document` istanza restituita da Content Services (obsoleta) al servizio Forms.

>[!NOTE]
>
>È possibile passare un `com.adobe.idp.Document` che contiene la struttura del modulo per il servizio Forms. Due nuovi metodi: `renderPDFForm2` e `renderHTMLForm2` accetta un `com.adobe.idp.Document` oggetto che contiene una struttura di modulo.

**Eseguire un&#39;azione con il flusso di dati del modulo**

A seconda del tipo di applicazione client, è possibile scrivere il modulo in un browser Web client o salvarlo come file PDF. In genere, un&#39;applicazione basata sul Web scrive il modulo nel browser Web. Tuttavia, un&#39;applicazione desktop in genere salva il modulo come file PDF.

**Consulta anche**

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Guida introduttiva all’API di servizio Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

## Trasmettere i documenti al servizio Forms tramite API Java {#pass-documents-to-the-forms-service-using-the-java-api}

Passa un documento ottenuto da Content Services (obsoleto) utilizzando il servizio Forms e l’API Content Services (obsoleto) (Java):

1. Includi file di progetto

   Includi i file JAR client, come adobe-forms-client.jar e adobe-contentservices-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto Forms e un oggetto API client di Document Management

   * Creare un `ServiceClientFactory` oggetto che contiene proprietà di connessione. (vedere [Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * Creare un `FormsServiceClient` mediante il costruttore e passando il `ServiceClientFactory` oggetto.
   * Creare un `DocumentManagementServiceClientImpl` mediante il costruttore e passando il `ServiceClientFactory` oggetto.

1. Recuperare la progettazione del modulo da Content Services (obsoleto)

   Richiama `DocumentManagementServiceClientImpl` dell&#39;oggetto `retrieveContent` e trasmettere i seguenti valori:

   * Valore stringa che specifica l&#39;archivio in cui viene aggiunto il contenuto. L’archivio predefinito è `SpacesStore`. Questo valore è un parametro obbligatorio.
   * Valore stringa che specifica il percorso completo del contenuto da recuperare (ad esempio, `/Company Home/Form Designs/Loan.xdp`). Questo valore è un parametro obbligatorio.
   * Valore stringa che specifica la versione. Questo valore è un parametro facoltativo e puoi trasmettere una stringa vuota. In questa situazione, viene recuperata la versione più recente.

   Il `retrieveContent` il metodo restituisce un `CRCResult` oggetto che contiene il file XDP. Ottenere un `com.adobe.idp.Document` richiamando il `CRCResult` dell&#39;oggetto `getDocument` metodo.

1. Rendering di un modulo PDF interattivo

   Richiama `FormsServiceClient` dell&#39;oggetto `renderPDFForm2` e trasmettere i seguenti valori:

   * A `com.adobe.idp.Document` oggetto che contiene la struttura del modulo recuperata da Content Services (obsoleto).
   * A `com.adobe.idp.Document` oggetto contenente dati da unire con il modulo. Se non desideri unire i dati, passa un campo vuoto `com.adobe.idp.Document` oggetto.
   * A `PDFFormRenderSpec` oggetto che memorizza le opzioni di runtime. Questo valore è un parametro facoltativo ed è possibile specificare `null` se non si desidera specificare le opzioni di runtime.
   * A `URLSpec` oggetto che contiene valori URI. Questo valore è un parametro facoltativo ed è possibile specificare `null`.
   * A `java.util.HashMap` oggetto che memorizza gli allegati. Questo valore è un parametro facoltativo ed è possibile specificare `null` se non si desidera allegare file al modulo.

   Il `renderPDFForm` il metodo restituisce un `FormsResult` oggetto contenente un flusso di dati modulo che deve essere scritto nel browser web client.

1. Eseguire un&#39;azione con il flusso di dati del modulo

   * Creare un `com.adobe.idp.Document` oggetto richiamando il `FormsResult` oggetto &quot;s `getOutputContent` metodo.
   * Ottieni il tipo di contenuto del `com.adobe.idp.Document` oggetto richiamando il relativo `getContentType` metodo.
   * Imposta il `javax.servlet.http.HttpServletResponse` tipo di contenuto dell&#39;oggetto richiamando il relativo `setContentType` e passando il tipo di contenuto del `com.adobe.idp.Document` oggetto.
   * Creare un `javax.servlet.ServletOutputStream` oggetto utilizzato per scrivere il flusso di dati del modulo nel browser web client richiamando `javax.servlet.http.HttpServletResponse` dell&#39;oggetto `getOutputStream` metodo.
   * Creare un `java.io.InputStream` oggetto richiamando il `com.adobe.idp.Document` dell&#39;oggetto `getInputStream` metodo.
   * Creare una matrice di byte e popolarla con il flusso di dati del modulo richiamando `InputStream` dell&#39;oggetto `read` metodo. Passa la matrice di byte come argomento.
   * Richiama `javax.servlet.ServletOutputStream` dell&#39;oggetto `write` metodo per inviare il flusso di dati del modulo al browser web client. Passare la matrice di byte al `write` metodo.

**Consulta anche**

[Quick Start (modalità SOAP): passaggio di documenti al servizio Forms utilizzando l’API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-passing-documents-to-the-forms-service-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Trasmettere i documenti al servizio Forms utilizzando l’API del servizio web {#pass-documents-to-the-forms-service-using-the-web-service-api}

Passa un documento ottenuto da Content Services (obsoleto) utilizzando il servizio Forms e Content Services (obsoleto) API (servizio web):

1. Includi file di progetto

   Creare un progetto Microsoft .NET che utilizza MTOM. Poiché questa applicazione client richiama due servizi AEM Forms, creare due riferimenti al servizio. Utilizza la seguente definizione WSDL per il riferimento al servizio associato al servizio Forms: `http://localhost:8080/soap/services/FormsService?WSDL&lc_version=9.0.1`.

   Utilizzare la seguente definizione WSDL per il riferimento al servizio associato al servizio Document Management: `http://localhost:8080/soap/services/DocumentManagementService?WSDL&lc_version=9.0.1`.

   Perché il `BLOB` il tipo di dati è comune a entrambi i riferimenti di servizio, qualifica completa `BLOB` tipo di dati quando lo si utilizza. Nel servizio Web corrispondente, tutte le `BLOB` le istanze sono completamente qualificate.

   >[!NOTE]
   >
   >Sostituisci `localhost`con l’indirizzo IP del server che ospita AEM Forms.

1. Creare un oggetto Forms e un oggetto API client di Document Management

   * Creare un `FormsServiceClient` utilizzando il costruttore predefinito.
   * Creare un `FormsServiceClient.Endpoint.Address` oggetto utilizzando `System.ServiceModel.EndpointAddress` costruttore. Passa un valore stringa che specifica il file WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/FormsService?WSDL`). Non è necessario utilizzare il `lc_version` attributo. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Creare un `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto ottenendo il valore del `FormsServiceClient.Endpoint.Binding` campo. Invia il valore restituito a `BasicHttpBinding`.
   * Imposta il `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegna al campo il nome utente dei moduli AEM `FormsServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore password corrispondente al campo `FormsServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

   >[!NOTE]
   >
   >Ripeti questi passaggi per `DocumentManagementServiceClient`client del servizio.

1. Recuperare la progettazione del modulo da Content Services (obsoleto)

   Recupera il contenuto richiamando `DocumentManagementServiceClient` dell&#39;oggetto `retrieveContent` e fornendo i seguenti valori:

   * Valore stringa che specifica l&#39;archivio in cui viene aggiunto il contenuto. L’archivio predefinito è `SpacesStore`. Questo valore è un parametro obbligatorio.
   * Valore stringa che specifica il percorso completo del contenuto da recuperare (ad esempio, `/Company Home/Form Designs/Loan.xdp`). Questo valore è un parametro obbligatorio.
   * Valore stringa che specifica la versione. Questo valore è un parametro facoltativo e puoi trasmettere una stringa vuota. In questa situazione, viene recuperata la versione più recente.
   * Parametro di output stringa che memorizza il valore del collegamento Sfoglia.
   * A `BLOB` parametro di output che memorizza il contenuto. Puoi utilizzare questo parametro di output per recuperare il contenuto.
   * A `ServiceReference1.MyMapOf_xsd_string_To_xsd_anyType` parametro di output che memorizza gli attributi del contenuto.
   * A `CRCResult` parametro di output. Invece di utilizzare questo oggetto, puoi utilizzare `BLOB` parametro di output per ottenere il contenuto.

1. Rendering di un modulo PDF interattivo

   Richiama `FormsServiceClient` dell&#39;oggetto `renderPDFForm2` e trasmettere i seguenti valori:

   * A `BLOB` oggetto che contiene la struttura del modulo recuperata da Content Services (obsoleto).
   * A `BLOB` oggetto contenente dati da unire con il modulo. Se non desideri unire i dati, passa un campo vuoto `BLOB` oggetto.
   * A `PDFFormRenderSpec` oggetto che memorizza le opzioni di runtime. Questo valore è un parametro facoltativo ed è possibile specificare `null` se non si desidera specificare le opzioni di runtime.
   * A `URLSpec` oggetto che contiene valori URI. Questo valore è un parametro facoltativo ed è possibile specificare `null`.
   * A `Map` oggetto che memorizza gli allegati. Questo valore è un parametro facoltativo ed è possibile specificare `null` se non si desidera allegare file al modulo.
   * Un parametro di output lungo utilizzato per memorizzare il conteggio delle pagine.
   * Parametro di output stringa utilizzato per memorizzare il valore delle impostazioni locali.
   * A `FormsResult` parametro di output utilizzato per memorizzare il modulo di interactrive PDF `.`

   Il `renderPDFForm2` il metodo restituisce un `FormsResult` oggetto che contiene il modulo PDF interattivo.

1. Eseguire un&#39;azione con il flusso di dati del modulo

   * Creare un `BLOB` oggetto che contiene i dati del modulo ottenendo il valore di `FormsResult` dell&#39;oggetto `outputContent` campo.
   * Creare un `System.IO.FileStream` richiamando il relativo costruttore. Passa un valore stringa che rappresenta la posizione del file del documento interattivo di PDF e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto della `BLOB` oggetto recuperato da `FormsResult` oggetto. Popolare la matrice di byte ottenendo il valore della `BLOB` dell&#39;oggetto `MTOM` membro dati.
   * Creare un `System.IO.BinaryWriter` oggetto richiamando il relativo costruttore e passando il `System.IO.FileStream` oggetto.
   * Scrivere il contenuto della matrice di byte in un file PDF richiamando `System.IO.BinaryWriter` dell&#39;oggetto `Write` e passando la matrice di byte.

**Consulta anche**

[Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
