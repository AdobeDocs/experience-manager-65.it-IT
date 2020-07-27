---
title: Importazione ed esportazione di dati
seo-title: Importazione ed esportazione di dati
description: 'null'
seo-description: 'null'
uuid: 94ccb6f2-6e5f-43ea-a954-9a4402871a17
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 2e783745-c986-45ba-8e65-7437d114ca38
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '2742'
ht-degree: 0%

---


# Importazione ed esportazione di dati {#importing-and-exporting-data}

## Informazioni su Form Data Integration Service {#about-the-form-data-integration-service}

Il servizio di integrazione dei dati modulo può importare dati in un modulo PDF ed esportare dati da un modulo PDF. Le operazioni di importazione ed esportazione supportano due tipi di PDF forms:

* Un modulo Acrobat (creato in Acrobat) è un documento PDF che contiene campi modulo.
* Un modulo Adobe XML (creato in Designer) è un documento PDF conforme allo standard XML Adobe XML Forms Architecture (XFA).

I dati del modulo possono essere presenti in uno dei formati seguenti, a seconda del tipo di modulo PDF:

* Un file XFDF, che è una versione XML del formato dati del modulo Acrobat.
* Un file XDP, che è un file XML che contiene le definizioni dei campi del modulo. Può anche contenere dati del campo modulo e un file PDF incorporato. È possibile utilizzare un file XDP generato da Designer solo se contiene un documento PDF incorporato con codifica base 64.

È possibile eseguire le seguenti attività utilizzando il servizio di integrazione dei dati modulo:

* Importa dati in PDF forms. Per ulteriori informazioni, vedere [Importazione di dati](importing-exporting-data.md#importing-form-data)del modulo.
* Esportare dati dai PDF forms. Per ulteriori informazioni, vedere [Esportazione dei dati](importing-exporting-data.md#exporting-form-data)del modulo.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio di integrazione dei dati modulo, vedere Riferimento [servizi per i AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Importazione di dati modulo {#importing-form-data}

È possibile importare i dati del modulo in PDF forms interattivi utilizzando il servizio di integrazione dei dati del modulo. Un modulo PDF interattivo è un documento PDF contenente uno o più campi per la raccolta di informazioni da parte di un utente o per la visualizzazione di informazioni personalizzate. Il servizio di integrazione dei dati del modulo non supporta i calcoli del modulo, la convalida o gli script.

Per importare dati in un modulo creato in Designer, è necessario fare riferimento a un&#39;origine dati XML XDP valida. Esaminare il seguente modulo di richiesta di ipoteca.

![ie_ie_loanformdata](assets/ie_ie_loanformdata.png)

Per importare i valori dei dati in questo modulo, è necessario disporre di un&#39;origine dati XML XDP valida che corrisponda al modulo. Non è possibile utilizzare un&#39;origine dati XML arbitraria per importare dati in un modulo utilizzando il servizio di integrazione dati modulo. La differenza tra un&#39;origine dati XML arbitraria e un&#39;origine dati XML XDP sta nel fatto che un&#39;origine dati XDP è conforme a XML Forms Architecture (XFA). Il codice XML seguente rappresenta un&#39;origine dati XML XDP che corrisponde al modulo di esempio per l&#39;applicazione ipoteca.

```xml
 <?xml version="1.0" encoding="UTF-8" ?>
 - <xfa:datasets xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/">
 - <xfa:data>
 - <data>
     - <Layer>
         <closeDate>1/26/2007</closeDate>
         <lastName>Johnson</lastName>
         <firstName>Jerry</firstName>
         <mailingAddress>JJohnson@NoMailServer.com</mailingAddress>
         <city>New York</city>
         <zipCode>00501</zipCode>
         <state>NY</state>
         <dateBirth>26/08/1973</dateBirth>
         <middleInitials>D</middleInitials>
         <socialSecurityNumber>(555) 555-5555</socialSecurityNumber>
         <phoneNumber>5555550000</phoneNumber>
     </Layer>
     - <Mortgage>
         <mortgageAmount>295000.00</mortgageAmount>
         <monthlyMortgagePayment>1724.54</monthlyMortgagePayment>
         <purchasePrice>300000</purchasePrice>
         <downPayment>5000</downPayment>
         <term>25</term>
         <interestRate>5.00</interestRate>
     </Mortgage>
 </data>
 </xfa:data>
 </xfa:datasets>
```

>[!NOTE]
>
>Per ulteriori informazioni sul servizio di integrazione dei dati modulo, vedere Riferimento [servizi per i AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary-of-steps}

Per importare i dati del modulo in un modulo PDF, procedere come segue:

1. Includere i file di progetto.
1. Creare un client del servizio di integrazione dati modulo.
1. Fare riferimento a un modulo PDF.
1. Fare riferimento a un&#39;origine dati XML.
1. Importare i dati nel modulo PDF.
1. Salvare il modulo PDF come file PDF.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se state creando un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate servizi Web, accertatevi di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-formdataintegration-client.jar
* adobe-utilities.jar (richiesto se i AEM Forms sono distribuiti su JBoss)
* jbossall-client.jar (richiesto se i AEM Forms sono distribuiti su JBoss)

Per informazioni sulla posizione di questi file JAR, vedere [Inclusione di file](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)libreria Java AEM Forms.

**Creare un client del servizio di integrazione dei dati modulo**

Prima di poter importare i dati in un modulo PDF API client a livello di programmazione, è necessario creare un client di servizi di integrazione dati. Quando create un client di servizi, definite le impostazioni di connessione necessarie per richiamare un servizio. Per ulteriori informazioni, vedere [Impostazione delle proprietà](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)di connessione.

**Riferimento a un modulo PDF**

Per importare dati in un modulo PDF, è necessario fare riferimento a un modulo XML creato in Designer o a un modulo Acrobat creato in Acrobat.

**Riferimento a un&#39;origine dati XML**

Per importare i dati del modulo, è necessario fare riferimento a un&#39;origine dati valida. Per importare dati in un modulo XML XFA creato in Designer, è necessario utilizzare un&#39;origine dati XML XDP. Se si fa riferimento a un modulo Acrobat, è necessario utilizzare un&#39;origine dati XFDF. Per ogni campo in cui si desidera importare i dati, è necessario specificare un valore. Se un elemento posizionato nell&#39;origine dati XML non corrisponde a un campo del modulo, l&#39;elemento viene ignorato.

**Importazione di dati nel modulo PDF**

Dopo aver fatto riferimento a un modulo PDF e a un&#39;origine dati XML valida, è possibile importare i dati nel modulo PDF.

**Salvare il modulo PDF come file PDF**

Dopo aver importato i dati in un modulo, è possibile salvare il modulo come file PDF. Una volta salvato il file come PDF, l&#39;utente può aprire il modulo in Adobe Reader o Acrobat e visualizzarlo insieme ai dati importati.

**Consulta anche**

[Importare i dati del modulo utilizzando l&#39;API Java](importing-exporting-data.md#import-form-data-using-the-java-api)

[Importare i dati del modulo utilizzando l&#39;API del servizio Web](importing-exporting-data.md#import-form-data-using-the-web-service-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido dell&#39;API di Form Data Integration Service](/help/forms/developing/form-data-integration-service-java.md#form-data-integration-service-java-api-quick-start-soap)

[Esportazione dei dati del modulo](importing-exporting-data.md#exporting-form-data)

### Importare i dati del modulo utilizzando l&#39;API Java {#import-form-data-using-the-java-api}

Importare i dati del modulo utilizzando l&#39;API di integrazione dei dati del modulo (Java):

1. Includere i file di progetto.

   Includete file JAR client, ad esempio adobe-formdataintegration-client.jar, nel percorso di classe del progetto Java.

1. Creare un client del servizio di integrazione dati modulo.

   * Creare un `ServiceClientFactory` oggetto che contenga proprietà di connessione.
   * Creare un `FormDataIntegrationClient` oggetto utilizzando il relativo costruttore e passando l&#39; `ServiceClientFactory` oggetto.

1. Fare riferimento a un modulo PDF.

   * Creare un `java.io.FileInputStream` oggetto utilizzando il relativo costruttore. Passa un valore di stringa che specifica la posizione del modulo PDF.
   * Creare un `com.adobe.idp.Document` oggetto che memorizza il modulo PDF utilizzando il `com.adobe.idp.Document` costruttore. Trasmettere al costruttore l&#39;oggetto `java.io.FileInputStream` che contiene il modulo PDF.

1. Fare riferimento a un&#39;origine dati XML.

   * Creare un `java.io.FileInputStream` oggetto utilizzando il relativo costruttore e passare un valore di stringa che specifica la posizione del file XML contenente i dati da importare nel modulo.
   * Creare un `com.adobe.idp.Document` oggetto che memorizza i dati del modulo utilizzando il `com.adobe.idp.Document` costruttore. Trasmettere l&#39;oggetto `java.io.FileInputStream` che contiene i dati del modulo al costruttore.

1. Importare i dati nel modulo PDF.

   Importare dati nel modulo PDF richiamando il metodo dell&#39; `FormDataIntegrationClient` oggetto `importData` e passando i valori seguenti:

   * L&#39; `com.adobe.idp.Document` oggetto che memorizza il modulo PDF.
   * L&#39; `com.adobe.idp.Document` oggetto che memorizza i dati del modulo.

   Il `importData` metodo restituisce un `com.adobe.idp.Document` oggetto che memorizza un modulo PDF contenente i dati contenuti nell&#39;origine dati XML.

1. Salvare il modulo PDF come file PDF.

   * Creare un `java.io.File` oggetto e assicurarsi che l&#39;estensione del file sia &quot;.PDF&quot;.
   * Richiamare il metodo `Document` dell&#39;oggetto `copyToFile` per copiare il contenuto dell&#39; `Document` oggetto nel file (assicurarsi di utilizzare l&#39; `Document` oggetto restituito dal `importData` metodo).

**Consulta anche**

[Riepilogo dei passaggi](importing-exporting-data.md#summary-of-steps)

[Avvio rapido (modalità SOAP): Importazione di dati del modulo tramite l&#39;API Java](/help/forms/developing/form-data-integration-service-java.md#quick-start-soap-mode-importing-form-data-using-the-java-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Importare i dati del modulo utilizzando l&#39;API del servizio Web {#import-form-data-using-the-web-service-api}

Importare i dati del modulo utilizzando l&#39;API di integrazione dei dati del modulo (servizio Web):

1. Includere i file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/FormDataIntegration?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituire `localhost` con l&#39;indirizzo IP del server host AEM Forms.

1. Creare un client del servizio di integrazione dati modulo.

   * Creare un `FormDataIntegrationClient` oggetto utilizzando il relativo costruttore predefinito.
   * Creare un `FormDataIntegrationClient.Endpoint.Address` oggetto utilizzando il `System.ServiceModel.EndpointAddress` costruttore. Passa un valore di stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/FormDataIntegration?blob=mtom`.) Non è necessario utilizzare l&#39; `lc_version` attributo. Questo attributo viene utilizzato quando create un riferimento a un servizio. Tuttavia, specificate `?blob=mtom` per utilizzare MTOM.
   * Creare un `System.ServiceModel.BasicHttpBinding` oggetto ottenendo il valore del `FormDataIntegrationClient.Endpoint.Binding` campo. Inserite il valore restituito in `BasicHttpBinding`.
   * Impostare il campo `System.ServiceModel.BasicHttpBinding` dell&#39; `MessageEncoding` oggetto su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilitate l&#39;autenticazione HTTP di base eseguendo le seguenti operazioni:

      * Assegnare il nome utente dei moduli AEM al campo `FormDataIntegrationClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `FormDataIntegrationClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Fare riferimento a un modulo PDF.

   * Creare un `BLOB` oggetto utilizzando il relativo costruttore. Questo `BLOB` oggetto viene utilizzato per memorizzare il modulo PDF.
   * Creare un `System.IO.FileStream` oggetto richiamandone il costruttore. Passa un valore di stringa che specifica la posizione del modulo PDF e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto dell&#39; `System.IO.FileStream` oggetto. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà dell&#39; `System.IO.FileStream` oggetto `Length` .
   * Compilare l&#39;array di byte con i dati del flusso richiamando il metodo dell&#39; `System.IO.FileStream` oggetto `Read` . Passare l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39; `BLOB` oggetto assegnandone `MTOM` il campo con il contenuto dell&#39;array di byte.

1. Fare riferimento a un&#39;origine dati XML.

   * Creare un `BLOB` oggetto utilizzando il relativo costruttore. Questo `BLOB` oggetto viene utilizzato per memorizzare i dati importati nel modulo.
   * Creare un `System.IO.FileStream` oggetto richiamandone il costruttore. Passa un valore di stringa che specifica la posizione del file XML contenente i dati da importare e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto dell&#39; `System.IO.FileStream` oggetto. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà dell&#39; `System.IO.FileStream` oggetto `Length` .
   * Compilare l&#39;array di byte con i dati del flusso richiamando il metodo dell&#39; `System.IO.FileStream` oggetto `Read` . Passare l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39; `BLOB` oggetto assegnandone `MTOM` il campo con il contenuto dell&#39;array di byte.

1. Importare i dati nel modulo PDF.

   Importare dati nel modulo PDF richiamando il metodo dell&#39; `FormDataIntegrationClient` oggetto `importData` e passando i valori seguenti:

   * L&#39; `BLOB` oggetto che memorizza il modulo PDF.
   * L&#39; `BLOB` oggetto che memorizza i dati del modulo.

   Il `importData` metodo restituisce un `BLOB` oggetto che memorizza un modulo PDF contenente i dati contenuti nell&#39;origine dati XML.

1. Salvare il modulo PDF come file PDF.

   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file PDF.
   * Creare un array di byte che memorizza il contenuto dei dati dell&#39; `BLOB` oggetto restituito dal `importData` metodo. Compilare l&#39;array di byte ottenendo il valore del campo dell&#39; `BLOB` oggetto `MTOM` .
   * Creare un `System.IO.BinaryWriter` oggetto richiamando il relativo costruttore e passando l&#39; `System.IO.FileStream` oggetto.
   * Scrivere il contenuto dell&#39;array di byte in un file PDF richiamando il metodo dell&#39; `System.IO.BinaryWriter` oggetto `Write` e passando l&#39;array di byte.

**Consulta anche**

[Riepilogo dei passaggi](importing-exporting-data.md#summary-of-steps)

[Chiamata di AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## Esportazione dei dati del modulo {#exporting-form-data}

È possibile esportare i dati del modulo da un modulo PDF interattivo utilizzando il servizio di integrazione dei dati del modulo. Il formato dei dati esportati dipende dal tipo di modulo. Se il tipo di modulo è un modulo Acrobat creato in Acrobat, i dati esportati sono XFDF. Se il tipo di modulo è un modulo XML creato in Designer, i dati esportati sono XDP.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio di integrazione dei dati modulo, vedere Riferimento [servizi per i AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-1}

Per esportare i dati del modulo da un modulo PDF, procedere come segue:

1. Includi file di progetto
1. Creare un client del servizio di integrazione dati modulo.
1. Fare riferimento a un modulo PDF.
1. Esportare i dati dal modulo PDF.
1. Salvare i dati esportati come file XML.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se state creando un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate servizi Web, accertatevi di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-formdataintegration-client.jar
* adobe-utilities.jar (richiesto se i AEM Forms sono distribuiti su JBoss)
* jbossall-client.jar (richiesto se i AEM Forms sono distribuiti su JBoss)

**Creare un client del servizio di integrazione dei dati modulo**

Prima di poter importare i dati in un&#39;API formClient PDF a livello di programmazione, è necessario creare un client del servizio di integrazione dati. Quando create un client di servizi, definite le impostazioni di connessione necessarie per richiamare un servizio. Per informazioni, [impostare le proprietà](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)di connessione.

**Riferimento a un modulo PDF**

Per esportare dati da un modulo PDF, è necessario fare riferimento a un modulo PDF creato in Designer o Acrobat e contenente i dati del modulo. Se si tenta di esportare i dati da un modulo PDF vuoto, verrà visualizzato uno schema XML vuoto.

**Esportazione di dati dal modulo PDF**

Dopo aver fatto riferimento a un modulo PDF contenente dati del modulo, è possibile esportare i dati dal modulo. I dati vengono esportati all&#39;interno di uno schema XML basato sul modulo.

**Salvare i dati del modulo come file XML**

Dopo aver esportato i dati del modulo, è possibile salvarli come file XML. Una volta salvato il file come file XML, è possibile aprire il file XML all&#39;interno di un visualizzatore XML per visualizzare i dati del modulo.

**Consulta anche**

[Esportare i dati del modulo utilizzando l&#39;API Java](importing-exporting-data.md#export-form-data-using-the-java-api)

[Esportare i dati del modulo utilizzando l&#39;API del servizio Web](importing-exporting-data.md#export-form-data-using-the-web-service-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido dell&#39;API di Form Data Integration Service](/help/forms/developing/form-data-integration-service-java.md#form-data-integration-service-java-api-quick-start-soap)

[Importazione di dati modulo](importing-exporting-data.md#importing-form-data)

### Esportare i dati del modulo utilizzando l&#39;API Java {#export-form-data-using-the-java-api}

Esportare i dati del modulo utilizzando l&#39;API di integrazione dei dati del modulo (Java):

1. Includere i file di progetto.

   Includete file JAR client, ad esempio adobe-formdataintegration-client.jar, nel percorso di classe del progetto Java.

1. Creare un client del servizio di integrazione dati modulo.

   * Creare un `ServiceClientFactory` oggetto che contenga proprietà di connessione.
   * Creare un `FormDataIntegrationClient` oggetto utilizzando il relativo costruttore e passando l&#39; `ServiceClientFactory` oggetto.

1. Fare riferimento a un modulo PDF.

   * Creare un `java.io.FileInputStream` oggetto utilizzando il relativo costruttore e passare un valore di stringa che specifica la posizione del modulo PDF contenente i dati da esportare.
   * Creare un `com.adobe.idp.Document` oggetto che memorizza il modulo PDF utilizzando il `com.adobe.idp.Document` costruttore. Trasmettere al costruttore l&#39;oggetto `java.io.FileInputStream` che contiene il modulo PDF.

1. Esportare i dati dal modulo PDF.

   Esportare i dati del modulo richiamando il `FormDataIntegrationClient` metodo dell&#39; `exportData` oggetto e passando l&#39; `com.adobe.idp.Document` oggetto che memorizza il modulo PDF. Questo metodo restituisce un `com.adobe.idp.Document` oggetto che memorizza i dati del modulo come schema XML.

1. Salvare il modulo PDF come file PDF.

   * Creare un `java.io.File` oggetto e assicurarsi che l&#39;estensione del file sia XML.
   * Richiamare il metodo `Document` dell&#39;oggetto `copyToFile` per copiare il contenuto dell&#39; `Document` oggetto nel file (assicurarsi di utilizzare l&#39; `Document` oggetto restituito dal `exportData` metodo).

**Consulta anche**

[Riepilogo dei passaggi](importing-exporting-data.md#summary-of-steps)

[Avvio rapido (modalità SOAP): Esportazione dei dati del modulo tramite l&#39;API Java](/help/forms/developing/form-data-integration-service-java.md#quick-start-soap-mode-exporting-form-data-using-the-java-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Esportare i dati del modulo utilizzando l&#39;API del servizio Web {#export-form-data-using-the-web-service-api}

Esportare i dati del modulo utilizzando l&#39;API di integrazione dei dati del modulo (servizio Web):

1. Includere i file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/FormDataIntegration?WSDL&lc_version=9.0.1`.

   * Sostituire `localhost` con l&#39;indirizzo IP del server host AEM Forms.

1. Creare un client del servizio di integrazione dati modulo.

   * Creare un `FormDataIntegrationClient` oggetto utilizzando il relativo costruttore predefinito.
   * Creare un `FormDataIntegrationClient.Endpoint.Address` oggetto utilizzando il `System.ServiceModel.EndpointAddress` costruttore. Passa un valore di stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/FormDataIntegration?blob=mtom`.) Non è necessario utilizzare l&#39; `lc_version` attributo. Questo attributo viene utilizzato quando create un riferimento a un servizio. Tuttavia, specificate `?blob=mtom` per utilizzare MTOM.
   * Creare un `System.ServiceModel.BasicHttpBinding` oggetto ottenendo il valore del `FormDataIntegrationClient.Endpoint.Binding` campo. Inserite il valore restituito in `BasicHttpBinding`.
   * Impostare il campo `System.ServiceModel.BasicHttpBinding` dell&#39; `MessageEncoding` oggetto su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilitate l&#39;autenticazione HTTP di base eseguendo le seguenti operazioni:

      * Assegnare il nome utente dei moduli AEM al campo `FormDataIntegrationClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `FormDataIntegrationClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Fare riferimento a un modulo PDF.

   * Creare un `BLOB` oggetto utilizzando il relativo costruttore. Questo `BLOB` oggetto viene utilizzato per memorizzare il modulo PDF da cui vengono esportati i dati.
   * Creare un `System.IO.FileStream` oggetto richiamandone il costruttore. Passa un valore di stringa che specifica la posizione del modulo PDF e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto dell&#39; `System.IO.FileStream` oggetto. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà dell&#39; `System.IO.FileStream` oggetto `Length` .
   * Compilare l&#39;array di byte con i dati del flusso richiamando il `System.IO.FileStream` `Read` metodo dell&#39;oggetto e passando l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39; `BLOB` oggetto assegnandone `MTOM` il campo con il contenuto dell&#39;array di byte.

1. Esportare i dati dal modulo PDF.

   Importare i dati nel modulo PDF richiamando il `FormDataIntegrationClient` metodo dell&#39; `exportData` oggetto e passando l&#39; `BLOB` oggetto che memorizza il modulo PDF. Questo metodo restituisce un `BLOB` oggetto che memorizza i dati del modulo come schema XML.

1. Salvare il modulo PDF come file PDF.

   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file XML.
   * Creare un array di byte che memorizza il contenuto dei dati dell&#39; `BLOB` oggetto restituito dal `exportData` metodo. Compilare l&#39;array di byte ottenendo il valore del campo dell&#39; `BLOB` oggetto `MTOM` .
   * Creare un `System.IO.BinaryWriter` oggetto richiamando il relativo costruttore e passando l&#39; `System.IO.FileStream` oggetto.
   * Scrivere il contenuto dell&#39;array di byte in un file XML richiamando il metodo dell&#39; `System.IO.BinaryWriter` oggetto `Write` e passando l&#39;array di byte.

**Consulta anche**

[Riepilogo dei passaggi](importing-exporting-data.md#summary-of-steps)

[Chiamata di AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chiamata di AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
