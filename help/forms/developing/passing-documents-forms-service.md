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
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1677'
ht-degree: 0%

---

# Trasmissione di documenti al servizio Forms {#passing-documents-to-the-formsservice}

**Gli esempi e gli esempi contenuti in questo documento sono solo per AEM Forms in ambiente JEE.**

Il servizio AEM Forms esegue il rendering dei PDF forms interattivi sui dispositivi client, in genere i browser web, per raccogliere informazioni dagli utenti. Un modulo di PDF interattivo si basa su una struttura di modulo che in genere viene salvata come file XDP e creata in Designer. In AEM Forms, è possibile passare un oggetto `com.adobe.idp.Document` che contiene la struttura del modulo al servizio Forms. Il servizio Forms esegue quindi il rendering della struttura del modulo nell&#39;oggetto `com.adobe.idp.Document`.

Un vantaggio del passaggio di un oggetto `com.adobe.idp.Document` al servizio Forms è che altre operazioni del servizio restituiscono un&#39;istanza `com.adobe.idp.Document`. In altre parole, è possibile ottenere un&#39;istanza `com.adobe.idp.Document` da un&#39;altra operazione di servizio ed eseguirne il rendering. Si supponga, ad esempio, che un file XDP sia memorizzato in un nodo Content Services (obsoleto) denominato `/Company Home/Form Designs`, come illustrato nella figura seguente.

È possibile recuperare in modo programmatico Loan.xdp da Content Services (obsoleto) (obsoleto) e passare il file XDP al servizio Forms in un oggetto `com.adobe.idp.Document`.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Forms, vedere [Riferimento ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Riepilogo dei passaggi {#summary-of-steps}

Per passare un documento ottenuto da Content Services (obsoleto) (obsoleto) al servizio Forms, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Creare un oggetto Forms e un oggetto API Client di Document Management.
1. Recupera la progettazione del modulo da Content Services (obsoleto).
1. Esegui il rendering del modulo di PDF interattivo.
1. Eseguire un&#39;azione con il flusso di dati del modulo.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se si utilizzano servizi Web, includere i file proxy.

**Creare un oggetto API client di gestione documenti e Forms**

Prima di poter eseguire un&#39;operazione API del servizio Forms a livello di programmazione, creare un oggetto API del client Forms. Inoltre, poiché questo flusso di lavoro recupera un file XDP da Content Services (obsoleto), crea un oggetto API di gestione dei documenti.

**Recupera la progettazione del modulo da Content Services (obsoleto)**

Recupera il file XDP da Content Services (obsoleto) utilizzando l’API Java o del servizio web. Il file XDP viene restituito all&#39;interno di un&#39;istanza `com.adobe.idp.Document` (o di un&#39;istanza `BLOB` se si utilizzano i servizi Web). È quindi possibile passare l&#39;istanza `com.adobe.idp.Document` al servizio Forms.

**Eseguire il rendering di un modulo PDF interattivo**

Per eseguire il rendering di un modulo interattivo, passare l&#39;istanza `com.adobe.idp.Document` restituita da Content Services (obsoleta) al servizio Forms.

>[!NOTE]
>
>È possibile passare un `com.adobe.idp.Document` che contiene la struttura del modulo al servizio Forms. Due nuovi metodi denominati `renderPDFForm2` e `renderHTMLForm2` accettano un oggetto `com.adobe.idp.Document` che contiene una struttura di modulo.

**Esegui un&#39;azione con il flusso di dati del modulo**

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

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione. (Vedere [Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * Creare un oggetto `FormsServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.
   * Creare un oggetto `DocumentManagementServiceClientImpl` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Recuperare la progettazione del modulo da Content Services (obsoleto)

   Richiama il metodo `retrieveContent` dell&#39;oggetto `DocumentManagementServiceClientImpl` e passa i seguenti valori:

   * Valore stringa che specifica l&#39;archivio in cui viene aggiunto il contenuto. L&#39;archivio predefinito è `SpacesStore`. Questo valore è un parametro obbligatorio.
   * Valore stringa che specifica il percorso completo del contenuto da recuperare, ad esempio `/Company Home/Form Designs/Loan.xdp`. Questo valore è un parametro obbligatorio.
   * Valore stringa che specifica la versione. Questo valore è un parametro facoltativo e puoi trasmettere una stringa vuota. In questa situazione, viene recuperata la versione più recente.

   Il metodo `retrieveContent` restituisce un oggetto `CRCResult` che contiene il file XDP. Ottenere un&#39;istanza `com.adobe.idp.Document` richiamando il metodo `getDocument` dell&#39;oggetto `CRCResult`.

1. Rendering di un modulo PDF interattivo

   Richiama il metodo `renderPDFForm2` dell&#39;oggetto `FormsServiceClient` e passa i seguenti valori:

   * Oggetto `com.adobe.idp.Document` contenente la struttura del modulo recuperato da Content Services (obsoleto).
   * Oggetto `com.adobe.idp.Document` contenente dati da unire al modulo. Se non si desidera unire i dati, passare un oggetto `com.adobe.idp.Document` vuoto.
   * Un oggetto `PDFFormRenderSpec` che memorizza le opzioni di runtime. Questo valore è un parametro facoltativo ed è possibile specificare `null` se non si desidera specificare le opzioni di runtime.
   * Oggetto `URLSpec` contenente valori URI. Questo valore è un parametro facoltativo ed è possibile specificare `null`.
   * Oggetto `java.util.HashMap` che memorizza gli allegati. Questo valore è un parametro facoltativo ed è possibile specificare `null` se non si desidera allegare file al modulo.

   Il metodo `renderPDFForm` restituisce un oggetto `FormsResult` che contiene un flusso di dati del modulo che deve essere scritto nel browser Web client.

1. Eseguire un&#39;azione con il flusso di dati del modulo

   * Creare un oggetto `com.adobe.idp.Document` richiamando il metodo `getOutputContent` dell&#39;oggetto `FormsResult`.
   * Ottenere il tipo di contenuto dell&#39;oggetto `com.adobe.idp.Document` richiamando il relativo metodo `getContentType`.
   * Impostare il tipo di contenuto dell&#39;oggetto `javax.servlet.http.HttpServletResponse` richiamando il relativo metodo `setContentType` e passando il tipo di contenuto dell&#39;oggetto `com.adobe.idp.Document`.
   * Creare un oggetto `javax.servlet.ServletOutputStream` utilizzato per scrivere il flusso di dati del modulo nel browser Web client richiamando il metodo `getOutputStream` dell&#39;oggetto `javax.servlet.http.HttpServletResponse`.
   * Creare un oggetto `java.io.InputStream` richiamando il metodo `getInputStream` dell&#39;oggetto `com.adobe.idp.Document`.
   * Creare una matrice di byte e popolarla con il flusso di dati del modulo richiamando il metodo `read` dell&#39;oggetto `InputStream`. Passa la matrice di byte come argomento.
   * Richiama il metodo `write` dell&#39;oggetto `javax.servlet.ServletOutputStream` per inviare il flusso di dati del modulo al browser Web client. Passare la matrice di byte al metodo `write`.

**Consulta anche**

[Quick Start (modalità SOAP): trasmissione di documenti al servizio Forms tramite l’API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-passing-documents-to-the-forms-service-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Trasmettere i documenti al servizio Forms utilizzando l’API del servizio web {#pass-documents-to-the-forms-service-using-the-web-service-api}

Passa un documento ottenuto da Content Services (obsoleto) utilizzando il servizio Forms e Content Services (obsoleto) API (servizio web):

1. Includi file di progetto

   Creare un progetto Microsoft .NET che utilizza MTOM. Poiché questa applicazione client richiama due servizi AEM Forms, creare due riferimenti al servizio. Utilizzare la seguente definizione WSDL per il riferimento al servizio associato al servizio Forms: `http://localhost:8080/soap/services/FormsService?WSDL&lc_version=9.0.1`.

   Utilizzare la seguente definizione WSDL per il riferimento al servizio associato al servizio Document Management: `http://localhost:8080/soap/services/DocumentManagementService?WSDL&lc_version=9.0.1`.

   Poiché il tipo di dati `BLOB` è comune a entrambi i riferimenti al servizio, il tipo di dati `BLOB` viene completamente qualificato quando viene utilizzato. Nel servizio Web corrispondente, avvio rapido, tutte le `BLOB` istanze sono completamente qualificate.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Creare un oggetto Forms e un oggetto API client di Document Management

   * Creare un oggetto `FormsServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `FormsServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/FormsService?WSDL`). Non è necessario utilizzare l&#39;attributo `lc_version`. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `FormsServiceClient.Endpoint.Binding`. Eseguire il cast del valore restituito in `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegnare il nome utente dei moduli AEM al campo `FormsServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `FormsServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

   >[!NOTE]
   >
   >Ripetere questi passaggi per il client del servizio `DocumentManagementServiceClient`.

1. Recuperare la progettazione del modulo da Content Services (obsoleto)

   Recuperare il contenuto richiamando il metodo `retrieveContent` dell&#39;oggetto `DocumentManagementServiceClient` e passando i valori seguenti:

   * Valore stringa che specifica l&#39;archivio in cui viene aggiunto il contenuto. L&#39;archivio predefinito è `SpacesStore`. Questo valore è un parametro obbligatorio.
   * Valore stringa che specifica il percorso completo del contenuto da recuperare, ad esempio `/Company Home/Form Designs/Loan.xdp`. Questo valore è un parametro obbligatorio.
   * Valore stringa che specifica la versione. Questo valore è un parametro facoltativo e puoi trasmettere una stringa vuota. In questa situazione, viene recuperata la versione più recente.
   * Parametro di output stringa che memorizza il valore del collegamento Sfoglia.
   * Un parametro di output `BLOB` che memorizza il contenuto. Puoi utilizzare questo parametro di output per recuperare il contenuto.
   * Un parametro di output `ServiceReference1.MyMapOf_xsd_string_To_xsd_anyType` che memorizza gli attributi del contenuto.
   * Un parametro di output `CRCResult`. Anziché utilizzare questo oggetto, è possibile utilizzare il parametro di output `BLOB` per ottenere il contenuto.

1. Rendering di un modulo PDF interattivo

   Richiama il metodo `renderPDFForm2` dell&#39;oggetto `FormsServiceClient` e passa i seguenti valori:

   * Oggetto `BLOB` contenente la struttura del modulo recuperato da Content Services (obsoleto).
   * Oggetto `BLOB` contenente dati da unire al modulo. Se non si desidera unire i dati, passare un oggetto `BLOB` vuoto.
   * Un oggetto `PDFFormRenderSpec` che memorizza le opzioni di runtime. Questo valore è un parametro facoltativo ed è possibile specificare `null` se non si desidera specificare le opzioni di runtime.
   * Oggetto `URLSpec` contenente valori URI. Questo valore è un parametro facoltativo ed è possibile specificare `null`.
   * Oggetto `Map` che memorizza gli allegati. Questo valore è un parametro facoltativo ed è possibile specificare `null` se non si desidera allegare file al modulo.
   * Un parametro di output lungo utilizzato per memorizzare il conteggio delle pagine.
   * Parametro di output stringa utilizzato per memorizzare il valore delle impostazioni locali.
   * Un parametro di output `FormsResult` utilizzato per memorizzare il modulo di interactrive PDF `.`

   Il metodo `renderPDFForm2` restituisce un oggetto `FormsResult` che contiene il modulo PDF interattivo.

1. Eseguire un&#39;azione con il flusso di dati del modulo

   * Creare un oggetto `BLOB` contenente dati del modulo ottenendo il valore del campo `outputContent` dell&#39;oggetto `FormsResult`.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore. Passa un valore stringa che rappresenta la posizione del file del documento interattivo di PDF e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `BLOB` recuperato dall&#39;oggetto `FormsResult`. Popolare la matrice di byte ottenendo il valore del membro dati `MTOM` dell&#39;oggetto `BLOB`.
   * Creare un oggetto `System.IO.BinaryWriter` richiamandone il costruttore e passando l&#39;oggetto `System.IO.FileStream`.
   * Scrivere il contenuto della matrice di byte in un file PDF richiamando il metodo `Write` dell&#39;oggetto `System.IO.BinaryWriter` e passando la matrice di byte.

**Consulta anche**

[Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
