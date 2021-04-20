---
title: Trasmissione di documenti a FormsService
seo-title: Trasmissione di documenti a FormsService
description: 'Passare al servizio Forms un oggetto com.adobe.idp.Document contenente la struttura del modulo. Il servizio Forms esegue il rendering della struttura del modulo situata nell’oggetto com.adobe.idp.Document . '
seo-description: Passare al servizio Forms un oggetto com.adobe.idp.Document contenente la struttura del modulo. Il servizio Forms esegue il rendering della struttura del modulo situata nell’oggetto com.adobe.idp.Document .
uuid: 841e97f3-ebb8-4340-81a9-b6db11f0ec82
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: e23de3c3-f8a0-459f-801e-a0942fb1c6aa
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1715'
ht-degree: 0%

---


# Trasmissione di documenti al servizio Forms {#passing-documents-to-the-formsservice}

**Esempi ed esempi in questo documento sono solo per AEM Forms in ambiente JEE.**

Il servizio AEM Forms esegue il rendering dei PDF forms interattivi sui dispositivi client, in genere nei browser web, per raccogliere informazioni dagli utenti. Un modulo PDF interattivo si basa su una struttura del modulo generalmente salvata come file XDP e creata in Designer. A partire da AEM Forms, è possibile passare al servizio Forms un oggetto `com.adobe.idp.Document` contenente la struttura del modulo. Il servizio Forms esegue quindi il rendering della struttura del modulo situata nell’oggetto `com.adobe.idp.Document` .

Il vantaggio di passare un oggetto `com.adobe.idp.Document` al servizio Forms è che altre operazioni del servizio restituiscono un&#39;istanza `com.adobe.idp.Document`. In altre parole, puoi ottenere un&#39;istanza `com.adobe.idp.Document` da un&#39;altra operazione di servizio ed eseguirne il rendering. Ad esempio, si supponga che un file XDP sia memorizzato in un nodo Content Services (obsoleto) denominato `/Company Home/Form Designs`, come illustrato nella figura seguente.

È possibile recuperare in modo programmatico il file Loan.xdp da Content Services (obsoleto) (obsoleto) e passare il file XDP al servizio Forms all&#39;interno di un oggetto `com.adobe.idp.Document` .

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Forms, consulta [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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

Recupera il file XDP da Content Services (obsoleto) utilizzando l’API Java o del servizio Web. Il file XDP viene restituito all&#39;interno di un&#39;istanza `com.adobe.idp.Document` (o di un&#39;istanza `BLOB` se utilizzi servizi web). Puoi quindi passare l’istanza `com.adobe.idp.Document` al servizio Forms.

**Rendering di un modulo PDF interattivo**

Per eseguire il rendering di un modulo interattivo, passa l’istanza `com.adobe.idp.Document` restituita da Content Services (obsoleta) al servizio Forms.

>[!NOTE]
>
>È possibile passare un `com.adobe.idp.Document` contenente la struttura del modulo al servizio Forms. Due nuovi metodi denominati `renderPDFForm2` e `renderHTMLForm2` accettano un oggetto `com.adobe.idp.Document` contenente una struttura del modulo.

**Eseguire un’azione con il flusso di dati del modulo**

A seconda del tipo di applicazione client, è possibile scrivere il modulo in un browser Web client o salvarlo come file PDF. In genere, un’applicazione basata sul Web scrive il modulo nel browser web. Tuttavia, in genere, un’applicazione desktop salva il modulo come file PDF.

**Consulta anche**

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API di Forms Service](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

## Trasmettere i documenti al servizio Forms utilizzando l&#39;API Java {#pass-documents-to-the-forms-service-using-the-java-api}

Passa un documento ottenuto da Content Services (obsoleto) utilizzando il servizio Forms e l’API Content Services (obsoleto):

1. Includi file di progetto

   Includi file JAR client, come adobe-forms-client.jar e adobe-contentservices-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto Forms e un oggetto API client di gestione dei documenti

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione. (Vedere [Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * Creare un oggetto `FormsServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.
   * Creare un oggetto `DocumentManagementServiceClientImpl` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Recupera la struttura del modulo da Content Services (obsoleto)

   Richiama il metodo `retrieveContent` dell&#39;oggetto `DocumentManagementServiceClientImpl` e passa i seguenti valori:

   * Valore stringa che specifica l&#39;archivio in cui viene aggiunto il contenuto. L&#39;archivio predefinito è `SpacesStore`. Questo valore è un parametro obbligatorio.
   * Valore stringa che specifica il percorso completo del contenuto da recuperare (ad esempio, `/Company Home/Form Designs/Loan.xdp`). Questo valore è un parametro obbligatorio.
   * Valore stringa che specifica la versione. Questo valore è un parametro facoltativo ed è possibile trasmettere una stringa vuota. In questa situazione, viene recuperata la versione più recente.

   Il metodo `retrieveContent` restituisce un oggetto `CRCResult` contenente il file XDP. Per ottenere un&#39;istanza `com.adobe.idp.Document`, richiama il metodo `CRCResult` dell&#39;oggetto `getDocument`.

1. Rendering di un modulo PDF interattivo

   Richiama il metodo `renderPDFForm2` dell&#39;oggetto `FormsServiceClient` e passa i seguenti valori:

   * Un oggetto `com.adobe.idp.Document` che contiene la struttura del modulo recuperata da Content Services (obsoleto).
   * Un oggetto `com.adobe.idp.Document` contenente i dati da unire al modulo. Se non si desidera unire i dati, passare un oggetto `com.adobe.idp.Document` vuoto.
   * Un oggetto `PDFFormRenderSpec` che memorizza le opzioni di esecuzione. Questo valore è un parametro facoltativo ed è possibile specificare `null` se non si desidera specificare le opzioni di esecuzione.
   * Un oggetto `URLSpec` che contiene valori URI. Questo valore è un parametro facoltativo ed è possibile specificare `null`.
   * Un oggetto `java.util.HashMap` che memorizza gli allegati di file. Questo valore è un parametro facoltativo ed è possibile specificare `null` se non si desidera allegare file al modulo.

   Il metodo `renderPDFForm` restituisce un oggetto `FormsResult` contenente un flusso di dati del modulo che deve essere scritto nel browser Web client.

1. Eseguire un’azione con il flusso di dati del modulo

   * Creare un oggetto `com.adobe.idp.Document` richiamando il metodo `FormsResult` object ‘s `getOutputContent` .
   * Ottenere il tipo di contenuto dell&#39;oggetto `com.adobe.idp.Document` richiamandone il metodo `getContentType`.
   * Impostare il tipo di contenuto dell&#39;oggetto `javax.servlet.http.HttpServletResponse` richiamandone il metodo `setContentType` e passando il tipo di contenuto dell&#39;oggetto `com.adobe.idp.Document`.
   * Creare un oggetto `javax.servlet.ServletOutputStream` utilizzato per scrivere il flusso di dati del modulo nel browser Web client richiamando il metodo `javax.servlet.http.HttpServletResponse` dell&#39;oggetto `getOutputStream`.
   * Creare un oggetto `java.io.InputStream` richiamando il metodo `com.adobe.idp.Document` dell&#39;oggetto `getInputStream`.
   * Creare una matrice di byte e compilarla con il flusso di dati del modulo richiamando il metodo `InputStream` dell&#39;oggetto `read`. Passa l&#39;array di byte come argomento.
   * Richiamare il metodo `write` dell’oggetto `javax.servlet.ServletOutputStream` per inviare il flusso di dati del modulo al browser Web client. Passa l&#39;array di byte al metodo `write` .

**Consulta anche**

[Avvio rapido (modalità SOAP): Trasmissione di documenti al servizio Forms tramite l’API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-passing-documents-to-the-forms-service-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Trasmettere i documenti al servizio Forms utilizzando l&#39;API del servizio Web {#pass-documents-to-the-forms-service-using-the-web-service-api}

Passa un documento ottenuto da Content Services (obsoleto) utilizzando il servizio Forms e l’API Content Services (obsoleto) (servizio Web):

1. Includi file di progetto

   Creare un progetto Microsoft .NET che utilizza MTOM. Poiché questa applicazione client richiama due servizi AEM Forms, crea due riferimenti al servizio. Utilizza la seguente definizione WSDL per il riferimento al servizio associato al servizio Forms: `http://localhost:8080/soap/services/FormsService?WSDL&lc_version=9.0.1`.

   Utilizzare la seguente definizione WSDL per il riferimento al servizio associato al servizio Document Management: `http://localhost:8080/soap/services/DocumentManagementService?WSDL&lc_version=9.0.1`.

   Poiché il tipo di dati `BLOB` è comune a entrambi i riferimenti di servizio, qualifica completamente il tipo di dati `BLOB` quando lo utilizzi. Nel corrispondente avvio rapido del servizio Web, tutte le istanze `BLOB` sono completamente qualificate.

   >[!NOTE]
   >
   >Sostituisci `localhost`con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Creare un oggetto Forms e un oggetto API client di gestione dei documenti

   * Creare un oggetto `FormsServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `FormsServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/FormsService?WSDL`). Non è necessario utilizzare l&#39;attributo `lc_version` . Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Crea un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `FormsServiceClient.Endpoint.Binding` . Imposta il valore restituito su `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegna il nome utente del modulo di AEM al campo `FormsServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore della password corrispondente al campo `FormsServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

   >[!NOTE]
   >
   >Ripeti questi passaggi per il client di servizio `DocumentManagementServiceClient`.

1. Recupera la struttura del modulo da Content Services (obsoleto)

   Recupera il contenuto richiamando il metodo `retrieveContent` dell’oggetto `DocumentManagementServiceClient` e passando i seguenti valori:

   * Valore stringa che specifica l&#39;archivio in cui viene aggiunto il contenuto. L&#39;archivio predefinito è `SpacesStore`. Questo valore è un parametro obbligatorio.
   * Valore stringa che specifica il percorso completo del contenuto da recuperare (ad esempio, `/Company Home/Form Designs/Loan.xdp`). Questo valore è un parametro obbligatorio.
   * Valore stringa che specifica la versione. Questo valore è un parametro facoltativo ed è possibile trasmettere una stringa vuota. In questa situazione, viene recuperata la versione più recente.
   * Parametro di output della stringa che memorizza il valore del collegamento di ricerca.
   * Un parametro di output `BLOB` che memorizza il contenuto. Puoi utilizzare questo parametro di output per recuperare il contenuto.
   * Un parametro di output `ServiceReference1.MyMapOf_xsd_string_To_xsd_anyType` che memorizza gli attributi di contenuto.
   * Un parametro di output `CRCResult`. Invece di utilizzare questo oggetto, è possibile utilizzare il parametro di output `BLOB` per ottenere il contenuto.

1. Rendering di un modulo PDF interattivo

   Richiama il metodo `renderPDFForm2` dell&#39;oggetto `FormsServiceClient` e passa i seguenti valori:

   * Un oggetto `BLOB` che contiene la struttura del modulo recuperata da Content Services (obsoleto).
   * Un oggetto `BLOB` contenente i dati da unire al modulo. Se non si desidera unire i dati, passare un oggetto `BLOB` vuoto.
   * Un oggetto `PDFFormRenderSpec` che memorizza le opzioni di esecuzione. Questo valore è un parametro facoltativo ed è possibile specificare `null` se non si desidera specificare le opzioni di esecuzione.
   * Un oggetto `URLSpec` che contiene valori URI. Questo valore è un parametro facoltativo ed è possibile specificare `null`.
   * Un oggetto `Map` che memorizza gli allegati di file. Questo valore è un parametro facoltativo ed è possibile specificare `null` se non si desidera allegare file al modulo.
   * Un parametro di output lungo utilizzato per memorizzare il conteggio delle pagine.
   * Un parametro di output della stringa utilizzato per memorizzare il valore delle impostazioni internazionali.
   * Un parametro di output `FormsResult` utilizzato per memorizzare il modulo PDF interattivo `.`

   Il metodo `renderPDFForm2` restituisce un oggetto `FormsResult` contenente il modulo PDF interattivo.

1. Eseguire un’azione con il flusso di dati del modulo

   * Creare un oggetto `BLOB` che contiene i dati del modulo ottenendo il valore del campo `FormsResult` dell&#39;oggetto `outputContent`.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore. Passare un valore di stringa che rappresenta la posizione del file del documento PDF interattivo e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `BLOB` recuperato dall&#39;oggetto `FormsResult`. Compilare l&#39;array di byte ottenendo il valore del membro dati `BLOB` dell&#39;oggetto `MTOM`.
   * Creare un oggetto `System.IO.BinaryWriter` richiamandone il costruttore e passando l&#39;oggetto `System.IO.FileStream`.
   * Scrivi il contenuto dell’array di byte in un file PDF richiamando il metodo `Write` dell’oggetto `System.IO.BinaryWriter` e passando l’array di byte.

**Consulta anche**

[Richiamo di AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
