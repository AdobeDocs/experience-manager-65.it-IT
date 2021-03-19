---
title: Importazione ed esportazione di dati
seo-title: Importazione ed esportazione di dati
description: Utilizzare il servizio di integrazione dei dati modulo per importare i dati in un modulo PDF ed esportare i dati da un modulo PDF utilizzando l’API Java e l’API Web Service.
seo-description: Utilizzare il servizio di integrazione dei dati modulo per importare i dati in un modulo PDF ed esportare i dati da un modulo PDF utilizzando l’API Java e l’API Web Service.
uuid: 94ccb6f2-6e5f-43ea-a954-9a4402871a17
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 2e783745-c986-45ba-8e65-7437d114ca38
role: Developer (Sviluppatore)
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2811'
ht-degree: 0%

---


# Importazione ed esportazione di dati {#importing-and-exporting-data}

**Esempi ed esempi in questo documento sono solo per AEM Forms in ambiente JEE.**

## Informazioni sul servizio di integrazione dei dati dei moduli {#about-the-form-data-integration-service}

Il servizio di integrazione dei dati modulo può importare i dati in un modulo PDF ed esportarli da un modulo PDF. Le operazioni di importazione ed esportazione supportano due tipi di PDF forms:

* Un modulo Acrobat (creato in Acrobat) è un documento PDF contenente campi modulo.
* Un modulo XML di Adobe (creato in Designer) è un documento PDF conforme a XML Adobe XML Forms Architecture (XFA).

I dati modulo possono essere presenti in uno dei seguenti formati a seconda del tipo di modulo PDF:

* Un file XFDF, che è una versione XML del formato dati del modulo Acrobat.
* Un file XDP, file XML contenente le definizioni dei campi del modulo. Può anche contenere dati del campo modulo e un file PDF incorporato. È possibile utilizzare un file XDP generato da Designer solo se contiene un documento PDF incorporato con codifica base 64.

È possibile eseguire queste attività utilizzando il servizio di integrazione dei dati del modulo:

* Importa dati in PDF forms. Per informazioni, consultare [Importazione di dati modulo](importing-exporting-data.md#importing-form-data).
* Esporta dati dai PDF forms. Per informazioni, consultare [Esportazione di dati modulo](importing-exporting-data.md#exporting-form-data).

>[!NOTE]
>
>Per ulteriori informazioni sul servizio di integrazione dei dati dei moduli, vedere [Guida di riferimento dei servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Importazione di dati modulo {#importing-form-data}

È possibile importare i dati del modulo in PDF forms interattivi utilizzando il servizio di integrazione dei dati del modulo. Un modulo PDF interattivo è un documento PDF contenente uno o più campi per la raccolta di informazioni da parte di un utente o per la visualizzazione di informazioni personalizzate. Il servizio di integrazione dei dati del modulo non supporta i calcoli dei moduli, la convalida o gli script.

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
>Per ulteriori informazioni sul servizio di integrazione dei dati dei moduli, vedere [Guida di riferimento dei servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary-of-steps}

Per importare i dati del modulo in un modulo PDF, procedere come segue:

1. Includi file di progetto.
1. Creare un client del servizio di integrazione dei dati dei moduli.
1. Riferimento a un modulo PDF.
1. Fare riferimento a un&#39;origine dati XML.
1. Importare i dati nel modulo PDF.
1. Salvare il modulo PDF come file PDF.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-formdataintegration-client.jar
* adobe-utilities.jar (obbligatorio se AEM Forms è distribuito su JBoss)
* jbossall-client.jar (obbligatorio se AEM Forms è distribuito su JBoss)

Per informazioni sulla posizione di questi file JAR, consulta [Inclusione dei file della libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un client del servizio di integrazione dei dati di un modulo**

Prima di poter importare i dati in modo programmatico in un’API client del modulo PDF, è necessario creare un client del servizio di integrazione dei dati. Quando crei un client di servizio, definisci le impostazioni di connessione necessarie per richiamare un servizio. Per informazioni, vedere [Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

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

### Importare i dati del modulo utilizzando l’API Java {#import-form-data-using-the-java-api}

Importare i dati del modulo utilizzando l’API di integrazione dei dati del modulo (Java):

1. Includi file di progetto.

   Includi file JAR client, come adobe-formdataintegration-client.jar, nel percorso classe del progetto Java.

1. Creare un client del servizio di integrazione dei dati dei moduli.

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `FormDataIntegrationClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Riferimento a un modulo PDF.

   * Creare un oggetto `java.io.FileInputStream` utilizzando il relativo costruttore. Passa un valore stringa che specifica la posizione del modulo PDF.
   * Creare un oggetto `com.adobe.idp.Document` che memorizza il modulo PDF utilizzando il costruttore `com.adobe.idp.Document`. Passa l’oggetto `java.io.FileInputStream` che contiene il modulo PDF al costruttore.

1. Fare riferimento a un&#39;origine dati XML.

   * Creare un oggetto `java.io.FileInputStream` utilizzando il relativo costruttore e passare un valore stringa che specifica la posizione del file XML contenente i dati da importare nel modulo.
   * Creare un oggetto `com.adobe.idp.Document` che memorizza i dati del modulo utilizzando il costruttore `com.adobe.idp.Document`. Passa l&#39;oggetto `java.io.FileInputStream` che contiene i dati del modulo al costruttore.

1. Importare i dati nel modulo PDF.

   Importa i dati nel modulo PDF richiamando il metodo `importData` dell&#39;oggetto `FormDataIntegrationClient` e passando i seguenti valori:

   * L’oggetto `com.adobe.idp.Document` che memorizza il modulo PDF.
   * L&#39;oggetto `com.adobe.idp.Document` che memorizza i dati del modulo.

   Il metodo `importData` restituisce un oggetto `com.adobe.idp.Document` che memorizza un modulo PDF contenente i dati presenti nell&#39;origine dati XML.

1. Salvare il modulo PDF come file PDF.

   * Crea un oggetto `java.io.File` e assicurati che l&#39;estensione del file sia &quot;.PDF&quot;.
   * Richiamare il metodo `copyToFile` dell&#39;oggetto `Document` per copiare il contenuto dell&#39;oggetto `Document` nel file (assicurarsi di utilizzare l&#39;oggetto `Document` restituito dal metodo `importData`).

**Consulta anche**

[Riepilogo dei passaggi](importing-exporting-data.md#summary-of-steps)

[Avvio rapido (modalità SOAP): Importazione di dati del modulo tramite l’API Java](/help/forms/developing/form-data-integration-service-java.md#quick-start-soap-mode-importing-form-data-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Importare dati modulo utilizzando l’API del servizio Web {#import-form-data-using-the-web-service-api}

Importare i dati del modulo utilizzando l’API di integrazione dei dati del modulo (servizio Web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurati di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/FormDataIntegration?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Creare un client del servizio di integrazione dei dati dei moduli.

   * Creare un oggetto `FormDataIntegrationClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `FormDataIntegrationClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/FormDataIntegration?blob=mtom`). Non è necessario utilizzare l&#39;attributo `lc_version` . Questo attributo viene utilizzato quando si crea un riferimento a un servizio. Tuttavia, specifica `?blob=mtom` per utilizzare MTOM.
   * Crea un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `FormDataIntegrationClient.Endpoint.Binding` . Imposta il valore restituito su `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegna il nome utente del modulo di AEM al campo `FormDataIntegrationClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore della password corrispondente al campo `FormDataIntegrationClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Riferimento a un modulo PDF.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. Questo oggetto `BLOB` viene utilizzato per memorizzare il modulo PDF.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore. Passare un valore stringa che specifichi la posizione del modulo PDF e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni dell&#39;array di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare l’array di byte con i dati del flusso richiamando il metodo `Read` dell’oggetto `System.IO.FileStream`. Passa la matrice dei byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando il relativo campo `MTOM` con il contenuto dell&#39;array di byte.

1. Fare riferimento a un&#39;origine dati XML.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. Questo oggetto `BLOB` viene utilizzato per memorizzare i dati importati nel modulo.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore. Passa un valore stringa che specifica la posizione del file XML contenente i dati da importare e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni dell&#39;array di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare l’array di byte con i dati del flusso richiamando il metodo `Read` dell’oggetto `System.IO.FileStream`. Passa la matrice dei byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando il relativo campo `MTOM` con il contenuto dell&#39;array di byte.

1. Importare i dati nel modulo PDF.

   Importare i dati nel modulo PDF richiamando il metodo `importData` dell’oggetto `FormDataIntegrationClient` e passando i seguenti valori:

   * L’oggetto `BLOB` che memorizza il modulo PDF.
   * L&#39;oggetto `BLOB` che memorizza i dati del modulo.

   Il metodo `importData` restituisce un oggetto `BLOB` che memorizza un modulo PDF contenente i dati presenti nell&#39;origine dati XML.

1. Salvare il modulo PDF come file PDF.

   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file PDF.
   * Creare una matrice di byte che memorizza il contenuto dei dati dell&#39;oggetto `BLOB` restituito dal metodo `importData`. Compilare l’array di byte ottenendo il valore del campo `BLOB` dell’oggetto `MTOM`.
   * Creare un oggetto `System.IO.BinaryWriter` richiamandone il costruttore e passando l&#39;oggetto `System.IO.FileStream`.
   * Scrivi il contenuto dell’array di byte in un file PDF richiamando il metodo `Write` dell’oggetto `System.IO.BinaryWriter` e passando l’array di byte.

**Consulta anche**

[Riepilogo dei passaggi](importing-exporting-data.md#summary-of-steps)

[Richiamo di AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## Esportazione dei dati del modulo {#exporting-form-data}

È possibile esportare i dati dei moduli da un modulo PDF interattivo utilizzando il servizio di integrazione dei dati del modulo. Il formato dei dati esportati dipende dal tipo di modulo. Se il tipo di modulo è un modulo Acrobat creato in Acrobat, i dati esportati sono XFDF. Se il tipo di modulo è un modulo XML creato in Designer, i dati esportati sono XDP.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio di integrazione dei dati dei moduli, vedere [Guida di riferimento dei servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-1}

Per esportare i dati del modulo da un modulo PDF, eseguire le operazioni seguenti:

1. Includi file di progetto
1. Creare un client del servizio di integrazione dei dati dei moduli.
1. Riferimento a un modulo PDF.
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

Per esportare i dati da un modulo PDF, è necessario fare riferimento a un modulo PDF creato in Designer o Acrobat e contenente i dati del modulo. Se si tenta di esportare dati da un modulo PDF vuoto, si otterrà uno schema XML vuoto.

**Esportare dati dal modulo PDF**

Dopo aver fatto riferimento a un modulo PDF contenente dati del modulo, è possibile esportarli dal modulo. I dati vengono esportati all’interno di uno schema XML basato sul modulo.

**Salvare i dati del modulo come file XML**

Dopo aver esportato i dati del modulo, è possibile salvarli come file XML. Una volta salvato come file XML, è possibile aprire il file XML all’interno di un visualizzatore XML per visualizzare i dati del modulo.

**Consulta anche**

[Esportare i dati del modulo utilizzando l’API Java](importing-exporting-data.md#export-form-data-using-the-java-api)

[Esportare i dati dei moduli utilizzando l’API del servizio Web](importing-exporting-data.md#export-form-data-using-the-web-service-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido dell&#39;API del servizio di integrazione dei dati per modulo](/help/forms/developing/form-data-integration-service-java.md#form-data-integration-service-java-api-quick-start-soap)

[Importazione di dati modulo](importing-exporting-data.md#importing-form-data)

### Esportare i dati dei moduli utilizzando l’API Java {#export-form-data-using-the-java-api}

Esportare i dati dei moduli utilizzando l’API di integrazione dei dati dei moduli (Java):

1. Includi file di progetto.

   Includi file JAR client, come adobe-formdataintegration-client.jar, nel percorso classe del progetto Java.

1. Creare un client del servizio di integrazione dei dati dei moduli.

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `FormDataIntegrationClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Riferimento a un modulo PDF.

   * Creare un oggetto `java.io.FileInputStream` utilizzando il relativo costruttore e passare un valore stringa che specifichi la posizione del modulo PDF contenente i dati da esportare.
   * Creare un oggetto `com.adobe.idp.Document` che memorizza il modulo PDF utilizzando il costruttore `com.adobe.idp.Document`. Passa l’oggetto `java.io.FileInputStream` che contiene il modulo PDF al costruttore.

1. Esporta dati dal modulo PDF.

   Esportare i dati del modulo richiamando il metodo `exportData` dell’oggetto `com.adobe.idp.Document` e passando l’oggetto `FormDataIntegrationClient` in cui è memorizzato il modulo PDF. Questo metodo restituisce un oggetto `com.adobe.idp.Document` che memorizza i dati del modulo come schema XML.

1. Salvare il modulo PDF come file PDF.

   * Crea un oggetto `java.io.File` e assicurati che l&#39;estensione del file sia XML.
   * Richiamare il metodo `copyToFile` dell&#39;oggetto `Document` per copiare il contenuto dell&#39;oggetto `Document` nel file (assicurarsi di utilizzare l&#39;oggetto `Document` restituito dal metodo `exportData`).

**Consulta anche**

[Riepilogo dei passaggi](importing-exporting-data.md#summary-of-steps)

[Avvio rapido (modalità SOAP): Esportazione dei dati modulo tramite l’API Java](/help/forms/developing/form-data-integration-service-java.md#quick-start-soap-mode-exporting-form-data-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Esportare i dati dei moduli utilizzando l’API del servizio Web {#export-form-data-using-the-web-service-api}

Esportare i dati del modulo utilizzando l’API di integrazione dei dati del modulo (servizio Web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurati di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/FormDataIntegration?WSDL&lc_version=9.0.1`.

   * Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Creare un client del servizio di integrazione dei dati dei moduli.

   * Creare un oggetto `FormDataIntegrationClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `FormDataIntegrationClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/FormDataIntegration?blob=mtom`). Non è necessario utilizzare l&#39;attributo `lc_version` . Questo attributo viene utilizzato quando si crea un riferimento a un servizio. Tuttavia, specifica `?blob=mtom` per utilizzare MTOM.
   * Crea un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `FormDataIntegrationClient.Endpoint.Binding` . Imposta il valore restituito su `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegna il nome utente del modulo di AEM al campo `FormDataIntegrationClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore della password corrispondente al campo `FormDataIntegrationClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Riferimento a un modulo PDF.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. Questo oggetto `BLOB` viene utilizzato per memorizzare il modulo PDF da cui vengono esportati i dati.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore. Passare un valore stringa che specifichi la posizione del modulo PDF e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni dell&#39;array di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare l’array di byte con i dati del flusso richiamando il metodo `Read` dell’oggetto `System.IO.FileStream` e passando l’array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando il relativo campo `MTOM` con il contenuto dell&#39;array di byte.

1. Esporta dati dal modulo PDF.

   Importare i dati nel modulo PDF richiamando il metodo `exportData` dell’oggetto `BLOB` e passando l’oggetto `FormDataIntegrationClient` in cui è memorizzato il modulo PDF. Questo metodo restituisce un oggetto `BLOB` che memorizza i dati del modulo come schema XML.

1. Salvare il modulo PDF come file PDF.

   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file XML.
   * Creare una matrice di byte che memorizza il contenuto dei dati dell&#39;oggetto `BLOB` restituito dal metodo `exportData`. Compilare l’array di byte ottenendo il valore del campo `BLOB` dell’oggetto `MTOM`.
   * Creare un oggetto `System.IO.BinaryWriter` richiamandone il costruttore e passando l&#39;oggetto `System.IO.FileStream`.
   * Scrivere il contenuto dell&#39;array di byte in un file XML richiamando il metodo `Write` dell&#39;oggetto `System.IO.BinaryWriter` e passando l&#39;array di byte.

**Consulta anche**

[Riepilogo dei passaggi](importing-exporting-data.md#summary-of-steps)

[Richiamo di AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamo di AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
