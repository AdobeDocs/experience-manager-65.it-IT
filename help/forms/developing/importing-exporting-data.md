---
title: Importazione ed esportazione di dati
seo-title: Importing and Exporting Data
description: Utilizza il servizio di integrazione dei dati modulo per importare i dati in un modulo PDF ed esportare i dati da un modulo PDF utilizzando l’API Java e l’API Web Service.
seo-description: Use the Form Data Integration service to import data into a PDF form and export data from a PDF form using the Java API and Web Service API.
uuid: 94ccb6f2-6e5f-43ea-a954-9a4402871a17
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 2e783745-c986-45ba-8e65-7437d114ca38
role: Developer
exl-id: 96310e0a-8e95-4a55-9508-5298b8d67f83
source-git-commit: 135f50cc80f8bb449b2f1621db5e2564f5075968
workflow-type: tm+mt
source-wordcount: '2778'
ht-degree: 0%

---

# Importazione ed esportazione di dati {#importing-and-exporting-data}

**Esempi ed esempi in questo documento sono solo per AEM Forms in ambiente JEE.**

## Informazioni sul servizio di integrazione dei dati dei moduli {#about-the-form-data-integration-service}

Il servizio di integrazione dei dati modulo può importare dati in un modulo PDF ed esportare dati da un modulo PDF. Le operazioni di importazione ed esportazione supportano due tipi di PDF forms:

* Un modulo Acrobat (creato in Acrobat) è un documento PDF contenente campi modulo.
* Un modulo XML di Adobe (creato in Designer) è un documento di PDF conforme a XML Adobe XML Forms Architecture (XFA).

I dati modulo possono essere presenti in uno dei seguenti formati a seconda del tipo di modulo PDF:

* Un file XFDF, che è una versione XML del formato dati del modulo Acrobat.
* Un file XDP, file XML contenente le definizioni dei campi del modulo. Può anche contenere dati del campo modulo e un file PDF incorporato. È possibile utilizzare un file XDP generato da Designer solo se contiene un documento PDF incorporato con codifica base 64.

È possibile eseguire queste attività utilizzando il servizio di integrazione dei dati del modulo:

* Importa dati in PDF forms. Per informazioni, consulta [Importazione di dati modulo](importing-exporting-data.md#importing-form-data).
* Esporta dati dai PDF forms. Per informazioni, consulta [Esportazione dei dati del modulo](importing-exporting-data.md#exporting-form-data).

>[!NOTE]
>
>Per ulteriori informazioni sul servizio di integrazione dei dati modulo, vedi [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Importazione di dati modulo {#importing-form-data}

È possibile importare i dati del modulo in PDF forms interattivi utilizzando il servizio di integrazione dei dati del modulo. Un modulo PDF interattivo è un documento di PDF contenente uno o più campi per la raccolta di informazioni da parte di un utente o per la visualizzazione di informazioni personalizzate. Il servizio di integrazione dei dati del modulo non supporta i calcoli dei moduli, la convalida o gli script.

Per importare i dati in un modulo creato in Designer, è necessario fare riferimento a un’origine dati XML XDP valida. Considerare l&#39;esempio seguente del modulo di richiesta di mutuo.

![ie_ie_loanformdata](assets/ie_ie_loanformdata.png)

Per importare i valori dei dati in questo modulo, è necessario disporre di un’origine dati XML XDP valida che corrisponda al modulo. Non è possibile utilizzare un’origine dati XML arbitraria per importare dati in un modulo utilizzando il servizio di integrazione dei dati del modulo. La differenza tra un&#39;origine dati XML arbitraria e un&#39;origine dati XML XDP è che un&#39;origine dati XDP è conforme a XML Forms Architecture (XFA). Il seguente XML rappresenta un&#39;origine dati XML XDP che corrisponde al modulo di applicazione per ipoteca di esempio.

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
>Per ulteriori informazioni sul servizio di integrazione dei dati modulo, vedi [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary-of-steps}

Per importare i dati del modulo in un modulo PDF, procedere come segue:

1. Includi file di progetto.
1. Creare un client del servizio di integrazione dei dati dei moduli.
1. Fare riferimento a un modulo PDF.
1. Fare riferimento a un&#39;origine dati XML.
1. Importare dati nel modulo PDF.
1. Salvare il modulo PDF come file PDF.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-formdataintegration-client.jar
* adobe-utilities.jar (obbligatorio se AEM Forms è distribuito su JBoss)
* jbossall-client.jar (obbligatorio se AEM Forms è distribuito su JBoss)

Per informazioni sulla posizione di questi file JAR, vedi [Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un client del servizio di integrazione dei dati di un modulo**

Prima di poter importare i dati in modo programmatico in un’API client di PDF, è necessario creare un client del servizio di integrazione dei dati. Quando crei un client di servizio, definisci le impostazioni di connessione necessarie per richiamare un servizio. Per informazioni, consulta [Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

**Riferimento a un modulo PDF**

Per importare i dati in un modulo PDF, è necessario fare riferimento a un modulo XML creato in Designer o a un modulo Acrobat creato in Acrobat.

**Riferimento a un’origine dati XML**

Per importare i dati del modulo, è necessario fare riferimento a un’origine dati valida. Per importare i dati in un modulo XML XFA creato in Designer, è necessario utilizzare un’origine dati XML XDP. Se si fa riferimento a un modulo Acrobat, è necessario utilizzare un’origine dati XFDF. Per ogni campo in cui si desidera importare i dati, è necessario specificare un valore. Se un elemento situato nell’origine dati XML non corrisponde a un campo del modulo, l’elemento viene ignorato.

**Importare dati nel modulo PDF**

Dopo aver fatto riferimento a un modulo PDF e a un’origine dati XML valida, è possibile importare i dati nel modulo PDF.

**Salvare il modulo PDF come file PDF**

Dopo aver importato i dati in un modulo, è possibile salvarli come file PDF. Una volta salvato come file PDF, l’utente può aprire il modulo in Adobe Reader o Acrobat e visualizzarlo con i dati importati.

**Consulta anche**

[Importare dati modulo utilizzando l’API Java](importing-exporting-data.md#import-form-data-using-the-java-api)

[Importare dati modulo tramite l’API del servizio Web](importing-exporting-data.md#import-form-data-using-the-web-service-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido dell&#39;API del servizio di integrazione dei dati per modulo](/help/forms/developing/form-data-integration-service-java.md#form-data-integration-service-java-api-quick-start-soap)

[Esportazione dei dati del modulo](importing-exporting-data.md#exporting-form-data)

### Importare dati modulo utilizzando l’API Java {#import-form-data-using-the-java-api}

Importare i dati del modulo utilizzando l’API di integrazione dei dati del modulo (Java):

1. Includi file di progetto.

   Includi file JAR client, come adobe-formdataintegration-client.jar, nel percorso classe del progetto Java.

1. Creare un client del servizio di integrazione dei dati dei moduli.

   * Crea un `ServiceClientFactory` oggetto contenente le proprietà di connessione.
   * Crea un `FormDataIntegrationClient` utilizzando il relativo costruttore e passando `ServiceClientFactory` oggetto.

1. Fare riferimento a un modulo PDF.

   * Crea un `java.io.FileInputStream` utilizzando il relativo costruttore. Passa un valore stringa che specifica la posizione del modulo PDF.
   * Crea un `com.adobe.idp.Document` oggetto che memorizza il modulo PDF utilizzando `com.adobe.idp.Document` costruttore. Passa la `java.io.FileInputStream` oggetto contenente il modulo PDF al costruttore.

1. Fare riferimento a un&#39;origine dati XML.

   * Crea un `java.io.FileInputStream` utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del file XML contenente i dati da importare nel modulo.
   * Crea un `com.adobe.idp.Document` oggetto che memorizza i dati del modulo utilizzando `com.adobe.idp.Document` costruttore. Passa la `java.io.FileInputStream` oggetto contenente i dati del modulo al costruttore.

1. Importare dati nel modulo PDF.

   Importa dati nel modulo PDF richiamando il `FormDataIntegrationClient` dell’oggetto `importData` e passando i seguenti valori:

   * La `com.adobe.idp.Document` oggetto che memorizza il modulo PDF.
   * La `com.adobe.idp.Document` oggetto che memorizza i dati del modulo.

   La `importData` restituisce un `com.adobe.idp.Document` oggetto che memorizza un modulo PDF contenente i dati presenti nell&#39;origine dati XML.

1. Salvare il modulo PDF come file PDF.

   * Crea un `java.io.File` e assicurati che l&#39;estensione del file sia &quot;.PDF&quot;.
   * Richiama il `Document` dell’oggetto `copyToFile` per copiare il contenuto del `Document` al file (assicurati di utilizzare `Document` oggetto restituito da `importData` metodo).

**Consulta anche**

[Riepilogo dei passaggi](importing-exporting-data.md#summary-of-steps)

[Avvio rapido (modalità SOAP): Importazione di dati del modulo tramite l’API Java](/help/forms/developing/form-data-integration-service-java.md#quick-start-soap-mode-importing-form-data-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Importare dati modulo tramite l’API del servizio Web {#import-form-data-using-the-web-service-api}

Importare i dati del modulo utilizzando l’API di integrazione dei dati del modulo (servizio Web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurati di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/FormDataIntegration?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l’indirizzo IP del server che ospita AEM Forms.

1. Creare un client del servizio di integrazione dei dati dei moduli.

   * Crea un `FormDataIntegrationClient` utilizzando il relativo costruttore predefinito.
   * Crea un `FormDataIntegrationClient.Endpoint.Address` utilizzando `System.ServiceModel.EndpointAddress` costruttore. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/FormDataIntegration?blob=mtom`.) Non è necessario utilizzare il `lc_version` attributo. Questo attributo viene utilizzato quando si crea un riferimento a un servizio. Tuttavia, specifica `?blob=mtom` per utilizzare MTOM.
   * Crea un `System.ServiceModel.BasicHttpBinding` ottenendo il valore del `FormDataIntegrationClient.Endpoint.Binding` campo . Imposta il valore restituito su `BasicHttpBinding`.
   * Imposta la `System.ServiceModel.BasicHttpBinding` dell’oggetto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegnare il nome utente del modulo di AEM al campo `FormDataIntegrationClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore della password corrispondente al campo `FormDataIntegrationClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Fare riferimento a un modulo PDF.

   * Crea un `BLOB` utilizzando il relativo costruttore. Questo `BLOB` viene utilizzato per memorizzare il modulo PDF.
   * Crea un `System.IO.FileStream` richiamando il relativo costruttore. Passa un valore stringa che specifica la posizione del modulo PDF e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto del `System.IO.FileStream` oggetto. È possibile determinare le dimensioni dell&#39;array di byte ottenendo il `System.IO.FileStream` dell’oggetto `Length` proprietà.
   * Compilare l&#39;array di byte con i dati del flusso richiamando il `System.IO.FileStream` dell’oggetto `Read` metodo . Passa la matrice dei byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare `BLOB` oggetto assegnando il relativo `MTOM` con il contenuto dell&#39;array di byte.

1. Fare riferimento a un&#39;origine dati XML.

   * Crea un `BLOB` utilizzando il relativo costruttore. Questo `BLOB` viene utilizzato per memorizzare i dati importati nel modulo.
   * Crea un `System.IO.FileStream` richiamando il relativo costruttore. Passa un valore stringa che specifica la posizione del file XML contenente i dati da importare e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto del `System.IO.FileStream` oggetto. È possibile determinare le dimensioni dell&#39;array di byte ottenendo il `System.IO.FileStream` dell’oggetto `Length` proprietà.
   * Compilare l&#39;array di byte con i dati del flusso richiamando il `System.IO.FileStream` dell’oggetto `Read` metodo . Passa la matrice dei byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare `BLOB` oggetto assegnando il relativo `MTOM` con il contenuto dell&#39;array di byte.

1. Importare dati nel modulo PDF.

   Importa i dati nel modulo PDF richiamando il `FormDataIntegrationClient` dell’oggetto `importData` e passando i seguenti valori:

   * La `BLOB` oggetto che memorizza il modulo PDF.
   * La `BLOB` oggetto che memorizza i dati del modulo.

   La `importData` restituisce un `BLOB` oggetto che memorizza un modulo PDF contenente i dati presenti nell&#39;origine dati XML.

1. Salvare il modulo PDF come file PDF.

   * Crea un `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file PDF.
   * Creare un array di byte che memorizza il contenuto dei dati del `BLOB` oggetto restituito da `importData` metodo . Compilare l’array di byte ottenendo il valore del `BLOB` dell’oggetto `MTOM` campo .
   * Crea un `System.IO.BinaryWriter` richiamando il relativo costruttore e passando `System.IO.FileStream` oggetto.
   * Scrivi il contenuto dell’array di byte in un file PDF richiamando il `System.IO.BinaryWriter` dell’oggetto `Write` e passare l&#39;array di byte.

**Consulta anche**

[Riepilogo dei passaggi](importing-exporting-data.md#summary-of-steps)

[Richiamo di AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## Esportazione dei dati del modulo {#exporting-form-data}

È possibile esportare i dati dei moduli da un modulo PDF interattivo utilizzando il servizio di integrazione dei dati del modulo. Il formato dei dati esportati dipende dal tipo di modulo. Se il tipo di modulo è un modulo Acrobat creato in Acrobat, i dati esportati sono XFDF. Se il tipo di modulo è un modulo XML creato in Designer, i dati esportati sono XDP.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio di integrazione dei dati modulo, vedi [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-1}

Per esportare i dati del modulo da un modulo PDF, eseguire le operazioni seguenti:

1. Includi file di progetto
1. Creare un client del servizio di integrazione dei dati dei moduli.
1. Fare riferimento a un modulo PDF.
1. Esporta dati dal modulo PDF.
1. Salvare i dati esportati come file XML.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-formdataintegration-client.jar
* adobe-utilities.jar (obbligatorio se AEM Forms è distribuito su JBoss)
* jbossall-client.jar (obbligatorio se AEM Forms è distribuito su JBoss)

**Creare un client del servizio di integrazione dei dati di un modulo**

Prima di poter importare i dati in modo programmatico in un’API PDF formClient, è necessario creare un client del servizio di integrazione dei dati. Quando crei un client di servizio, definisci le impostazioni di connessione necessarie per richiamare un servizio. Per informazioni, [Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

**Riferimento a un modulo PDF**

Per esportare dati da un modulo PDF, è necessario fare riferimento a un modulo PDF creato in Designer o Acrobat e contenente i dati del modulo. Se si tenta di esportare dati da un modulo PDF vuoto, verrà visualizzato uno schema XML vuoto.

**Esportare dati dal modulo PDF**

Dopo aver fatto riferimento a un modulo PDF contenente dati del modulo, è possibile esportare i dati dal modulo. I dati vengono esportati all’interno di uno schema XML basato sul modulo.

**Salvare i dati del modulo come file XML**

Dopo aver esportato i dati del modulo, è possibile salvarli come file XML. Una volta salvato come file XML, è possibile aprire il file XML all’interno di un visualizzatore XML per visualizzare i dati del modulo.

**Consulta anche**

[Esportare i dati del modulo utilizzando l’API Java](importing-exporting-data.md#export-form-data-using-the-java-api)

[Esportare i dati dei moduli utilizzando l’API del servizio Web](importing-exporting-data.md#export-form-data-using-the-web-service-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido dell&#39;API del servizio di integrazione dei dati per modulo](/help/forms/developing/form-data-integration-service-java.md#form-data-integration-service-java-api-quick-start-soap)

[Importazione di dati modulo](importing-exporting-data.md#importing-form-data)

### Esportare i dati del modulo utilizzando l’API Java {#export-form-data-using-the-java-api}

Esportare i dati dei moduli utilizzando l’API di integrazione dei dati dei moduli (Java):

1. Includi file di progetto.

   Includi file JAR client, come adobe-formdataintegration-client.jar, nel percorso classe del progetto Java.

1. Creare un client del servizio di integrazione dei dati dei moduli.

   * Crea un `ServiceClientFactory` oggetto contenente le proprietà di connessione.
   * Crea un `FormDataIntegrationClient` utilizzando il relativo costruttore e passando `ServiceClientFactory` oggetto.

1. Fare riferimento a un modulo PDF.

   * Crea un `java.io.FileInputStream` utilizzando il relativo costruttore e passando un valore stringa che specifica la posizione del modulo PDF contenente i dati da esportare.
   * Crea un `com.adobe.idp.Document` oggetto che memorizza il modulo PDF utilizzando `com.adobe.idp.Document` costruttore. Passa la `java.io.FileInputStream` oggetto contenente il modulo PDF al costruttore.

1. Esporta dati dal modulo PDF.

   Esporta dati modulo richiamando il `FormDataIntegrationClient` dell’oggetto `exportData` e passare il `com.adobe.idp.Document` oggetto che memorizza il modulo PDF. Questo metodo restituisce un `com.adobe.idp.Document` oggetto che memorizza i dati del modulo come schema XML.

1. Salvare il modulo PDF come file PDF.

   * Crea un `java.io.File` e assicurati che l&#39;estensione del file sia XML.
   * Richiama il `Document` dell’oggetto `copyToFile` per copiare il contenuto del `Document` al file (assicurati di utilizzare `Document` oggetto restituito da `exportData` metodo).

**Consulta anche**

[Riepilogo dei passaggi](importing-exporting-data.md#summary-of-steps)

[Avvio rapido (modalità SOAP): Esportazione dei dati modulo tramite l’API Java](/help/forms/developing/form-data-integration-service-java.md#quick-start-soap-mode-exporting-form-data-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Esportare i dati dei moduli utilizzando l’API del servizio Web {#export-form-data-using-the-web-service-api}

Esportare i dati del modulo utilizzando l’API di integrazione dei dati del modulo (servizio Web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurati di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/FormDataIntegration?WSDL&lc_version=9.0.1`.

   * Sostituisci `localhost` con l’indirizzo IP del server che ospita AEM Forms.

1. Creare un client del servizio di integrazione dei dati dei moduli.

   * Crea un `FormDataIntegrationClient` utilizzando il relativo costruttore predefinito.
   * Crea un `FormDataIntegrationClient.Endpoint.Address` utilizzando `System.ServiceModel.EndpointAddress` costruttore. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/FormDataIntegration?blob=mtom`.) Non è necessario utilizzare il `lc_version` attributo. Questo attributo viene utilizzato quando si crea un riferimento a un servizio. Tuttavia, specifica `?blob=mtom` per utilizzare MTOM.
   * Crea un `System.ServiceModel.BasicHttpBinding` ottenendo il valore del `FormDataIntegrationClient.Endpoint.Binding` campo . Imposta il valore restituito su `BasicHttpBinding`.
   * Imposta la `System.ServiceModel.BasicHttpBinding` dell’oggetto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegnare il nome utente del modulo di AEM al campo `FormDataIntegrationClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore della password corrispondente al campo `FormDataIntegrationClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Fare riferimento a un modulo PDF.

   * Crea un `BLOB` utilizzando il relativo costruttore. Questo `BLOB` viene utilizzato per memorizzare il modulo PDF da cui vengono esportati i dati.
   * Crea un `System.IO.FileStream` richiamando il relativo costruttore. Passa un valore stringa che specifica la posizione del modulo PDF e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto del `System.IO.FileStream` oggetto. È possibile determinare le dimensioni dell&#39;array di byte ottenendo il `System.IO.FileStream` dell’oggetto `Length` proprietà.
   * Compilare l&#39;array di byte con i dati del flusso richiamando il `System.IO.FileStream` dell’oggetto `Read` e passare l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare `BLOB` oggetto assegnando il relativo `MTOM` con il contenuto dell&#39;array di byte.

1. Esporta dati dal modulo PDF.

   Importa dati nel modulo PDF richiamando il `FormDataIntegrationClient` dell’oggetto `exportData` e passare il `BLOB` oggetto che memorizza il modulo PDF. Questo metodo restituisce un `BLOB` oggetto che memorizza i dati del modulo come schema XML.

1. Salvare il modulo PDF come file PDF.

   * Crea un `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file XML.
   * Creare un array di byte che memorizza il contenuto dei dati del `BLOB` oggetto restituito da `exportData` metodo . Compilare l’array di byte ottenendo il valore del `BLOB` dell’oggetto `MTOM` campo .
   * Crea un `System.IO.BinaryWriter` richiamando il relativo costruttore e passando `System.IO.FileStream` oggetto.
   * Scrivere il contenuto dell&#39;array di byte in un file XML richiamando il `System.IO.BinaryWriter` dell’oggetto `Write` e passare l&#39;array di byte.

**Consulta anche**

[Riepilogo dei passaggi](importing-exporting-data.md#summary-of-steps)

[Richiamo di AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamo di AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
