---
title: Invio di documenti a FormsService
seo-title: Invio di documenti a FormsService
description: 'null'
seo-description: 'null'
uuid: 841e97f3-ebb8-4340-81a9-b6db11f0ec82
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: e23de3c3-f8a0-459f-801e-a0942fb1c6aa
translation-type: tm+mt
source-git-commit: 7cbe3e94eddb81925072f68388649befbb027e6d

---


# Invio di documenti al servizio Forms {#passing-documents-to-the-formsservice}

Il servizio AEM Forms esegue il rendering dei moduli PDF interattivi su dispositivi client, in genere browser Web, per raccogliere informazioni dagli utenti. Un modulo PDF interattivo si basa su una struttura del modulo che in genere viene salvata come file XDP e creata in Designer. Con AEM Forms è possibile trasmettere al servizio Forms un oggetto `com.adobe.idp.Document` contenente la struttura del modulo. Il servizio Forms esegue quindi il rendering della struttura del modulo situata nell&#39; `com.adobe.idp.Document` oggetto.

Il vantaggio di passare un `com.adobe.idp.Document` oggetto al servizio Forms consiste nel fatto che altre operazioni del servizio restituiscono un&#39; `com.adobe.idp.Document` istanza. In altre parole, potete ottenere un’ `com.adobe.idp.Document` istanza da un’altra operazione del servizio ed eseguirne il rendering. Ad esempio, si supponga che un file XDP sia memorizzato in un nodo Content Services (obsoleto) denominato `/Company Home/Form Designs`, come illustrato nell&#39;illustrazione seguente.

È possibile recuperare Loan.xdp da Content Services (obsoleto) a livello di programmazione e passare il file XDP al servizio Forms all&#39;interno di un `com.adobe.idp.Document` oggetto.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Forms, consultate Riferimento [servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Riepilogo dei passaggi {#summary-of-steps}

Per passare un documento ottenuto da Content Services (obsoleto) (obsoleto) al servizio Forms, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un oggetto Forms e un oggetto API client Document Management.
1. Recuperare la struttura del modulo da Content Services (obsoleto).
1. Eseguire il rendering del modulo PDF interattivo.
1. Eseguire un&#39;azione con il flusso di dati del modulo.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, includete i file proxy.

**Creazione di un oggetto Forms e Document Management Client API**

Prima di eseguire un&#39;operazione API del servizio Forms a livello di programmazione, creare un oggetto API Client Forms. Inoltre, poiché questo flusso di lavoro recupera un file XDP da Content Services (obsoleto), create un oggetto API Document Management.

**Recuperare la struttura del modulo da Content Services (obsoleto)**

Recuperate il file XDP da Content Services (obsoleto) utilizzando l&#39;API Java o del servizio Web. Il file XDP viene restituito all&#39;interno di un&#39; `com.adobe.idp.Document` istanza (o di un&#39; `BLOB` istanza se si utilizzano i servizi Web). È quindi possibile passare l&#39; `com.adobe.idp.Document` istanza al servizio Forms.

**Rendering di un modulo PDF interattivo**

Per eseguire il rendering di un modulo interattivo, passare l&#39; `com.adobe.idp.Document` istanza restituita da Content Services (obsoleto) al servizio Forms.

>[!NOTE]
>
>È possibile trasmettere al servizio Forms una struttura del modulo `com.adobe.idp.Document` contenente tale struttura. Due nuovi metodi denominati `renderPDFForm2` e `renderHTMLForm2` accettano un `com.adobe.idp.Document` oggetto contenente una struttura del modulo.

**Eseguire un&#39;azione con il flusso di dati del modulo**

A seconda del tipo di applicazione client, è possibile scrivere il modulo in un browser Web client o salvarlo come file PDF. In genere, un&#39;applicazione basata sul Web scrive il modulo nel browser Web. Tuttavia, in genere un&#39;applicazione desktop salva il modulo come file PDF.

**Consulta anche**

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido dell&#39;API di Forms Service](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

## Trasmettere i documenti al servizio Forms tramite l&#39;API Java {#pass-documents-to-the-forms-service-using-the-java-api}

Trasmettere un documento ottenuto da Content Services (obsoleto) utilizzando il servizio Forms e Content Services API (obsoleto):

1. Includi file di progetto

   Includete file JAR client, ad esempio adobe-forms-client.jar e adobe-contentservices-client.jar, nel percorso di classe del progetto Java.

1. Creazione di un oggetto Forms e Document Management Client API

   * Creare un `ServiceClientFactory` oggetto che contenga proprietà di connessione. (Vedere [Impostazione delle proprietà](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)di connessione.)
   * Creare un `FormsServiceClient` oggetto utilizzando il relativo costruttore e passando l&#39; `ServiceClientFactory` oggetto.
   * Creare un `DocumentManagementServiceClientImpl` oggetto utilizzando il relativo costruttore e passando l&#39; `ServiceClientFactory` oggetto.

1. Recuperare la struttura del modulo da Content Services (obsoleto)

   Richiama il metodo dell’ `DocumentManagementServiceClientImpl` oggetto `retrieveContent` e passa i seguenti valori:

   * Valore stringa che specifica lo store in cui viene aggiunto il contenuto. Lo store predefinito è `SpacesStore`. Questo valore è un parametro obbligatorio.
   * Un valore di stringa che specifica il percorso completo del contenuto da recuperare (ad esempio, `/Company Home/Form Designs/Loan.xdp`). Questo valore è un parametro obbligatorio.
   * Un valore di stringa che specifica la versione. Questo valore è un parametro facoltativo e potete trasmettere una stringa vuota. In questa situazione, viene recuperata la versione più recente.
   Il `retrieveContent` metodo restituisce un `CRCResult` oggetto che contiene il file XDP. Ottenete un&#39; `com.adobe.idp.Document` istanza richiamando il `CRCResult` metodo dell&#39; `getDocument` oggetto.

1. Rendering di un modulo PDF interattivo

   Richiama il metodo dell’ `FormsServiceClient` oggetto `renderPDFForm2` e passa i seguenti valori:

   * Un `com.adobe.idp.Document` oggetto che contiene la struttura del modulo recuperata da Content Services (obsoleto).
   * Un `com.adobe.idp.Document` oggetto che contiene i dati da unire al modulo. Se non si desidera unire i dati, passare un `com.adobe.idp.Document` oggetto vuoto.
   * Un `PDFFormRenderSpec` oggetto che memorizza le opzioni di esecuzione. Questo valore è un parametro facoltativo ed è possibile specificare `null` se non si desidera specificare le opzioni di esecuzione.
   * Un `URLSpec` oggetto che contiene valori URI. Questo valore è un parametro facoltativo ed è possibile specificarlo `null`.
   * Un `java.util.HashMap` oggetto che memorizza gli allegati. Questo valore è un parametro facoltativo ed è possibile specificare `null` se non si desidera allegare file al modulo.
   Il `renderPDFForm` metodo restituisce un `FormsResult` oggetto che contiene un flusso di dati del modulo da scrivere nel browser Web del client.

1. Eseguire un&#39;azione con il flusso di dati del modulo

   * Creare un `com.adobe.idp.Document` oggetto richiamando il `FormsResult` metodo ‘s `getOutputContent` .
   * Ottenere il tipo di contenuto dell&#39; `com.adobe.idp.Document` oggetto richiamandone il `getContentType` metodo.
   * Impostare il tipo di contenuto dell&#39; `javax.servlet.http.HttpServletResponse` oggetto richiamandone `setContentType` il metodo e passando il tipo di contenuto dell&#39; `com.adobe.idp.Document` oggetto.
   * Creare un `javax.servlet.ServletOutputStream` oggetto utilizzato per scrivere il flusso di dati del modulo nel browser Web del client richiamando il `javax.servlet.http.HttpServletResponse` metodo dell&#39; `getOutputStream` oggetto.
   * Creare un `java.io.InputStream` oggetto richiamando il `com.adobe.idp.Document` metodo dell&#39; `getInputStream` oggetto.
   * Creare un array di byte e compilarlo con il flusso di dati del modulo richiamando il `InputStream` metodo dell&#39; `read` . Trasmettere l&#39;array di byte come argomento.
   * Richiamare il metodo dell&#39; `javax.servlet.ServletOutputStream` oggetto `write` per inviare il flusso di dati del modulo al browser Web del client. Passa l&#39;array di byte al `write` metodo.

**Consulta anche**

[Avvio rapido (modalità SOAP): Invio di documenti al servizio Forms tramite l&#39;API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-passing-documents-to-the-forms-service-using-the-java-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Trasmettere i documenti a Forms Service tramite l&#39;API del servizio Web {#pass-documents-to-the-forms-service-using-the-web-service-api}

Trasmettere un documento ottenuto da Content Services (obsoleto) utilizzando il servizio Forms e Content Services API (obsoleto) (servizio Web):

1. Includi file di progetto

   Creare un progetto Microsoft .NET che utilizza MTOM. Poiché questa applicazione client richiama due servizi AEM Forms, create due riferimenti al servizio. Utilizzare la seguente definizione WSDL per il riferimento al servizio associato al servizio Forms: `http://localhost:8080/soap/services/FormsService?WSDL&lc_version=9.0.1`.

   Utilizzate la seguente definizione WSDL per il riferimento al servizio associato al servizio Document Management: `http://localhost:8080/soap/services/DocumentManagementService?WSDL&lc_version=9.0.1`.

   Poiché il tipo di `BLOB` dati è comune a entrambi i riferimenti di servizio, è necessario qualificare completamente il tipo di `BLOB` dati quando viene utilizzato. Nella procedura di avvio rapido del servizio Web corrispondente, tutte `BLOB` le istanze sono completamente qualificate.

   >[!NOTE]
   >
   >Sostituire `localhost`con l&#39;indirizzo IP del server in cui è installato AEM Forms.

1. Creazione di un oggetto Forms e Document Management Client API

   * Creare un `FormsServiceClient` oggetto utilizzando il relativo costruttore predefinito.
   * Creare un `FormsServiceClient.Endpoint.Address` oggetto utilizzando il `System.ServiceModel.EndpointAddress` costruttore. Passa un valore di stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/FormsService?WSDL`). Non è necessario utilizzare l&#39; `lc_version` attributo. Questo attributo viene utilizzato quando create un riferimento a un servizio.
   * Creare un `System.ServiceModel.BasicHttpBinding` oggetto ottenendo il valore del `FormsServiceClient.Endpoint.Binding` campo. Inserite il valore restituito in `BasicHttpBinding`.
   * Impostare il campo `System.ServiceModel.BasicHttpBinding` dell&#39; `MessageEncoding` oggetto su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilitate l&#39;autenticazione HTTP di base eseguendo le seguenti operazioni:

      * Assegnare il nome utente dei moduli AEM al campo `FormsServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `FormsServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.
   >[!NOTE]
   >
   >Ripetete questi passaggi per il client di `DocumentManagementServiceClient`servizio.

1. Recuperare la struttura del modulo da Content Services (obsoleto)

   Recuperare il contenuto richiamando il metodo dell&#39; `DocumentManagementServiceClient` oggetto `retrieveContent` e passando i seguenti valori:

   * Valore stringa che specifica lo store in cui viene aggiunto il contenuto. Lo store predefinito è `SpacesStore`. Questo valore è un parametro obbligatorio.
   * Un valore di stringa che specifica il percorso completo del contenuto da recuperare (ad esempio, `/Company Home/Form Designs/Loan.xdp`). Questo valore è un parametro obbligatorio.
   * Un valore di stringa che specifica la versione. Questo valore è un parametro facoltativo e potete trasmettere una stringa vuota. In questa situazione, viene recuperata la versione più recente.
   * Un parametro di output della stringa che memorizza il valore del collegamento di ricerca.
   * Un parametro di `BLOB` output che memorizza il contenuto. Potete usare questo parametro di output per recuperare il contenuto.
   * Un parametro `ServiceReference1.MyMapOf_xsd_string_To_xsd_anyType` di output che memorizza gli attributi di contenuto.
   * Un parametro `CRCResult` di output. Invece di utilizzare questo oggetto, potete utilizzare il parametro `BLOB` output per ottenere il contenuto.

1. Rendering di un modulo PDF interattivo

   Richiama il metodo dell’ `FormsServiceClient` oggetto `renderPDFForm2` e passa i seguenti valori:

   * Un `BLOB` oggetto che contiene la struttura del modulo recuperata da Content Services (obsoleto).
   * Un `BLOB` oggetto che contiene i dati da unire al modulo. Se non si desidera unire i dati, passare un `BLOB` oggetto vuoto.
   * Un `PDFFormRenderSpec` oggetto che memorizza le opzioni di esecuzione. Questo valore è un parametro facoltativo ed è possibile specificare `null` se non si desidera specificare le opzioni di esecuzione.
   * Un `URLSpec` oggetto che contiene valori URI. Questo valore è un parametro facoltativo ed è possibile specificarlo `null`.
   * Un `Map` oggetto che memorizza gli allegati. Questo valore è un parametro facoltativo ed è possibile specificare `null` se non si desidera allegare file al modulo.
   * Un parametro di output lungo utilizzato per memorizzare il conteggio delle pagine.
   * Un parametro di output della stringa utilizzato per memorizzare il valore delle impostazioni internazionali.
   * Parametro di `FormsResult` output utilizzato per memorizzare il modulo PDF interattivo `.`
   Il `renderPDFForm2` metodo restituisce un `FormsResult` oggetto che contiene il modulo PDF interattivo.

1. Eseguire un&#39;azione con il flusso di dati del modulo

   * Creare un `BLOB` oggetto che contenga dati del modulo ottenendo il valore del campo dell&#39; `FormsResult` oggetto `outputContent` .
   * Creare un `System.IO.FileStream` oggetto richiamandone il costruttore. Passare un valore di stringa che rappresenta la posizione del file del documento PDF interattivo e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto dell&#39; `BLOB` oggetto recuperato dall&#39; `FormsResult` oggetto. Compilare l&#39;array di byte ottenendo il valore del membro `BLOB` dati dell&#39; `MTOM` oggetto.
   * Creare un `System.IO.BinaryWriter` oggetto richiamando il relativo costruttore e passando l&#39; `System.IO.FileStream` oggetto.
   * Scrivere il contenuto dell&#39;array di byte in un file PDF richiamando il metodo dell&#39; `System.IO.BinaryWriter` oggetto `Write` e passando l&#39;array di byte.

**Consulta anche**

[Attivazione di moduli AEM tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
