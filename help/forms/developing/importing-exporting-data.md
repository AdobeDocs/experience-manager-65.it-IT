---
title: Importazione ed esportazione di dati
seo-title: Importing and Exporting Data
description: Utilizza il servizio di integrazione dei dati del modulo per importare i dati in un modulo PDF ed esportare i dati da un modulo PDF utilizzando l’API Java e l’API del servizio Web.
seo-description: Use the Form Data Integration service to import data into a PDF form and export data from a PDF form using the Java API and Web Service API.
uuid: 94ccb6f2-6e5f-43ea-a954-9a4402871a17
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 2e783745-c986-45ba-8e65-7437d114ca38
role: Developer
exl-id: 96310e0a-8e95-4a55-9508-5298b8d67f83
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '2771'
ht-degree: 0%

---

# Importazione ed esportazione di dati {#importing-and-exporting-data}

**Gli esempi e gli esempi contenuti in questo documento sono solo per l’ambiente AEM Forms su JEE.**

## Informazioni sul servizio di integrazione dati modulo {#about-the-form-data-integration-service}

Il servizio di integrazione dei dati del modulo può importare dati in un modulo PDF ed esportare dati da un modulo PDF. Le operazioni di importazione ed esportazione supportano due tipi di PDF forms:

* Un modulo di Acrobat (creato in Acrobat) è un documento PDF che contiene campi modulo.
* Un modulo XML di Adobe (creato in Designer) è un documento PDF conforme all&#39;Adobe XML XML Forms Architecture (XFA).

I dati del modulo possono esistere in uno dei seguenti formati, a seconda del tipo di modulo PDF:

* Un file XFDF, una versione XML del formato dati del modulo Acrobat.
* Un file XDP, un file XML che contiene le definizioni dei campi modulo. Può anche contenere dati di campi modulo e un file PDF incorporato. Un file XDP generato da Designer può essere utilizzato solo se contiene un documento PDF con codifica base 64 incorporato.

Puoi eseguire queste attività utilizzando il servizio di integrazione dei dati del modulo:

* Importare dati nei PDF forms. Per informazioni, consulta [Importazione dati modulo](importing-exporting-data.md#importing-form-data).
* Esporta dati dai PDF forms. Per informazioni, consulta [Esportazione dati modulo](importing-exporting-data.md#exporting-form-data).

>[!NOTE]
>
>Per ulteriori informazioni sul servizio di integrazione dei dati del modulo, vedi [Guida di riferimento dei servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Importazione dati modulo {#importing-form-data}

Puoi importare i dati del modulo in PDF forms interattivi utilizzando il servizio Integrazione dati modulo. Un modulo PDF interattivo è un documento PDF che contiene uno o più campi per la raccolta di informazioni da un utente o la visualizzazione di informazioni personalizzate. Il servizio di integrazione dei dati del modulo non supporta i calcoli, la convalida o gli script dei moduli.

Per importare dati in un modulo creato in Designer, è necessario fare riferimento a un&#39;origine dati XML XDP valida. Prendi in considerazione il seguente esempio di modulo di richiesta di mutuo.

![ie_ie_loanformdata](assets/ie_ie_loanformdata.png)

Per importare i valori dei dati in questo modulo, è necessario disporre di un&#39;origine dati XML XDP valida che corrisponda al modulo. Non è possibile utilizzare un&#39;origine dati XML arbitraria per importare dati in un modulo utilizzando il servizio Integrazione dati modulo. La differenza tra un&#39;origine dati XML arbitraria e un&#39;origine dati XML XDP consiste nel fatto che un&#39;origine dati XDP è conforme all&#39;architettura XML Forms (XFA). Il codice XML seguente rappresenta un&#39;origine dati XML XDP che corrisponde al modulo di applicazione ipotecaria di esempio.

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
>Per ulteriori informazioni sul servizio di integrazione dei dati del modulo, vedi [Guida di riferimento dei servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary-of-steps}

Per importare i dati del modulo in un modulo PDF, effettuare le seguenti operazioni:

1. Includi file di progetto.
1. Creare un client del servizio di integrazione dei dati del modulo.
1. Fai riferimento a un modulo di PDF.
1. Fare riferimento a un&#39;origine dati XML.
1. Importare dati nel modulo PDF.
1. Salvare il modulo PDF come file PDF.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-formdataintegration-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è implementato su JBoss)
* jbossall-client.jar (obbligatorio se AEM Forms è distribuito su JBoss)

Per informazioni sulla posizione di questi file JAR, vedi [Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un client del servizio di integrazione dati modulo**

Prima di poter importare i dati in modo programmatico in un modulo PDF API client, è necessario creare un client del servizio di integrazione dati. Quando si crea un client di servizio, vengono definite le impostazioni di connessione necessarie per richiamare un servizio. Per informazioni, consulta [Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

**Fai riferimento a un modulo PDF**

Per importare dati in un modulo PDF, è necessario fare riferimento a un modulo XML creato in Designer o a un modulo Acrobat creato in Acrobat.

**Riferimento a un&#39;origine dati XML**

Per importare i dati del modulo, è necessario fare riferimento a un&#39;origine dati valida. Per importare dati in un modulo XML XFA creato in Designer, è necessario utilizzare un&#39;origine dati XML XDP. Se si fa riferimento a un modulo di Acrobat, è necessario utilizzare un&#39;origine dati XFDF. Per ogni campo in cui si desidera importare i dati, è necessario specificare un valore. Se un elemento nell&#39;origine dati XML non corrisponde a un campo nel modulo, l&#39;elemento verrà ignorato.

**Importare dati nel modulo PDF**

Dopo aver fatto riferimento a un modulo PDF e a un&#39;origine dati XML valida, è possibile importare i dati nel modulo PDF.

**Salvare il modulo PDF come file PDF**

Dopo aver importato i dati in un modulo, è possibile salvarlo come file PDF. Una volta salvato come file PDF, l’utente può aprire il modulo in Adobe Reader o Acrobat e visualizzarlo con i dati importati.

**Consulta anche**

[Importare dati modulo tramite API Java](importing-exporting-data.md#import-form-data-using-the-java-api)

[Importare dati modulo utilizzando l’API del servizio web](importing-exporting-data.md#import-form-data-using-the-web-service-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Guida introduttiva API Servizio di integrazione dati moduli](/help/forms/developing/form-data-integration-service-java.md#form-data-integration-service-java-api-quick-start-soap)

[Esportazione dati modulo](importing-exporting-data.md#exporting-form-data)

### Importare dati modulo tramite API Java {#import-form-data-using-the-java-api}

Importa i dati del modulo utilizzando l’API di integrazione dei dati del modulo (Java):

1. Includi file di progetto.

   Includi i file JAR client, ad esempio adobe-formdataintegration-client.jar, nel percorso di classe del progetto Java.

1. Creare un client del servizio di integrazione dei dati del modulo.

   * Creare un `ServiceClientFactory` oggetto che contiene proprietà di connessione.
   * Creare un `FormDataIntegrationClient` mediante il costruttore e passando il `ServiceClientFactory` oggetto.

1. Fai riferimento a un modulo di PDF.

   * Creare un `java.io.FileInputStream` mediante il costruttore. Passa un valore stringa che specifica la posizione del modulo PDF.
   * Creare un `com.adobe.idp.Document` oggetto che memorizza il modulo PDF utilizzando `com.adobe.idp.Document` costruttore. Passa il `java.io.FileInputStream` oggetto che contiene il form PDF al costruttore.

1. Fare riferimento a un&#39;origine dati XML.

   * Creare un `java.io.FileInputStream` mediante il costruttore e passare un valore stringa che specifica la posizione del file XML contenente i dati da importare nel modulo.
   * Creare un `com.adobe.idp.Document` oggetto che memorizza i dati del modulo utilizzando `com.adobe.idp.Document` costruttore. Passa il `java.io.FileInputStream` oggetto che contiene i dati del modulo per il costruttore.

1. Importare dati nel modulo PDF.

   Importare dati nel modulo PDF richiamando `FormDataIntegrationClient` dell&#39;oggetto `importData` e fornendo i seguenti valori:

   * Il `com.adobe.idp.Document` oggetto che memorizza il modulo PDF.
   * Il `com.adobe.idp.Document` oggetto che memorizza i dati del modulo.

   Il `importData` il metodo restituisce un `com.adobe.idp.Document` oggetto che memorizza un modulo PDF contenente i dati nell&#39;origine dati XML.

1. Salvare il modulo PDF come file PDF.

   * Creare un `java.io.File` e assicurarsi che l&#39;estensione del file sia &quot;.PDF&quot;.
   * Richiama `Document` dell&#39;oggetto `copyToFile` metodo per copiare il contenuto del `Document` al file (assicurati di utilizzare il `Document` oggetto restituito da `importData` metodo).

**Consulta anche**

[Riepilogo dei passaggi](importing-exporting-data.md#summary-of-steps)

[Quick Start (modalità SOAP): importazione di dati dai moduli tramite API Java](/help/forms/developing/form-data-integration-service-java.md#quick-start-soap-mode-importing-form-data-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Importare dati modulo utilizzando l’API del servizio web {#import-form-data-using-the-web-service-api}

Importa i dati del modulo utilizzando l’API di integrazione dei dati del modulo (servizio web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/FormDataIntegration?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l’indirizzo IP del server che ospita AEM Forms.

1. Creare un client del servizio di integrazione dei dati del modulo.

   * Creare un `FormDataIntegrationClient` utilizzando il costruttore predefinito.
   * Creare un `FormDataIntegrationClient.Endpoint.Address` oggetto utilizzando `System.ServiceModel.EndpointAddress` costruttore. Passa un valore stringa che specifica il file WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/FormDataIntegration?blob=mtom`.) Non è necessario utilizzare il `lc_version` attributo. Questo attributo viene utilizzato quando si crea un riferimento a un servizio. Tuttavia, specifica `?blob=mtom` per utilizzare MTOM.
   * Creare un `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto ottenendo il valore del `FormDataIntegrationClient.Endpoint.Binding` campo. Invia il valore restituito a `BasicHttpBinding`.
   * Imposta il `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegna al campo il nome utente dei moduli AEM `FormDataIntegrationClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore password corrispondente al campo `FormDataIntegrationClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Fai riferimento a un modulo di PDF.

   * Creare un `BLOB` mediante il costruttore. Questo `BLOB` L&#39;oggetto viene utilizzato per memorizzare il modulo PDF.
   * Creare un `System.IO.FileStream` richiamando il relativo costruttore. Passa un valore stringa che specifica la posizione del modulo PDF e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto della `System.IO.FileStream` oggetto. È possibile determinare le dimensioni della matrice di byte ottenendo `System.IO.FileStream` dell&#39;oggetto `Length` proprietà.
   * Compilare la matrice di byte con i dati di flusso richiamando `System.IO.FileStream` dell&#39;oggetto `Read` metodo. Passare la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare il `BLOB` oggetto assegnando il relativo `MTOM` con il contenuto della matrice di byte.

1. Fare riferimento a un&#39;origine dati XML.

   * Creare un `BLOB` mediante il costruttore. Questo `BLOB` L&#39;oggetto viene utilizzato per memorizzare i dati importati nel modulo.
   * Creare un `System.IO.FileStream` richiamando il relativo costruttore. Passa un valore stringa che specifica la posizione del file XML contenente i dati da importare e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto della `System.IO.FileStream` oggetto. È possibile determinare le dimensioni della matrice di byte ottenendo `System.IO.FileStream` dell&#39;oggetto `Length` proprietà.
   * Compilare la matrice di byte con i dati di flusso richiamando `System.IO.FileStream` dell&#39;oggetto `Read` metodo. Passare la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare il `BLOB` oggetto assegnando il relativo `MTOM` con il contenuto della matrice di byte.

1. Importare dati nel modulo PDF.

   Importare dati nel modulo PDF richiamando `FormDataIntegrationClient` dell&#39;oggetto `importData` e fornendo i seguenti valori:

   * Il `BLOB` oggetto che memorizza il modulo PDF.
   * Il `BLOB` oggetto che memorizza i dati del modulo.

   Il `importData` il metodo restituisce un `BLOB` oggetto che memorizza un modulo PDF contenente i dati nell&#39;origine dati XML.

1. Salvare il modulo PDF come file PDF.

   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore stringa che rappresenta la posizione del file PDF.
   * Creare una matrice di byte che memorizza il contenuto dei dati `BLOB` oggetto restituito da `importData` metodo. Popolare la matrice di byte ottenendo il valore della `BLOB` dell&#39;oggetto `MTOM` campo.
   * Creare un `System.IO.BinaryWriter` oggetto richiamando il relativo costruttore e passando il `System.IO.FileStream` oggetto.
   * Scrivere il contenuto della matrice di byte in un file PDF richiamando `System.IO.BinaryWriter` dell&#39;oggetto `Write` e passando la matrice di byte.

**Consulta anche**

[Riepilogo dei passaggi](importing-exporting-data.md#summary-of-steps)

[Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## Esportazione dati modulo {#exporting-form-data}

Puoi esportare i dati di un modulo PDF interattivo utilizzando il servizio Integrazione dati modulo. Il formato dei dati esportati dipende dal tipo di modulo. Se il tipo di modulo è un modulo di Acrobat creato in Acrobat, i dati esportati sono XFDF. Se il tipo di modulo è un modulo XML creato in Designer, i dati esportati saranno XDP.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio di integrazione dei dati del modulo, vedi [Guida di riferimento dei servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-1}

Per esportare i dati di un modulo PDF, effettuare le seguenti operazioni:

1. Includi file di progetto
1. Creare un client del servizio di integrazione dei dati del modulo.
1. Fai riferimento a un modulo di PDF.
1. Esporta dati dal modulo PDF.
1. Salvare i dati esportati come file XML.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-formdataintegration-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è implementato su JBoss)
* jbossall-client.jar (obbligatorio se AEM Forms è distribuito su JBoss)

**Creare un client del servizio di integrazione dati modulo**

Prima di poter importare i dati a livello di programmazione in un’API PDF formClient, è necessario creare un client del servizio di integrazione dei dati. Quando si crea un client di servizio, vengono definite le impostazioni di connessione necessarie per richiamare un servizio. Per informazioni, [Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

**Fai riferimento a un modulo PDF**

Per esportare dati da un modulo PDF, è necessario fare riferimento a un modulo PDF creato in Designer o Acrobat e contenente dati del modulo. Se si tenta di esportare dati da un modulo PDF vuoto, si otterrà uno schema XML vuoto.

**Esportare dati dal modulo PDF**

Dopo aver fatto riferimento a un modulo PDF contenente dati del modulo, è possibile esportare i dati dal modulo. I dati vengono esportati all&#39;interno di uno schema XML basato sul modulo.

**Salvare i dati del modulo come file XML**

Dopo aver esportato i dati del modulo, è possibile salvarli come file XML. Una volta salvato come file XML, è possibile aprire il file XML all&#39;interno di un visualizzatore XML per visualizzare i dati del modulo.

**Consulta anche**

[Esportare i dati del modulo utilizzando l’API Java](importing-exporting-data.md#export-form-data-using-the-java-api)

[Esportare i dati del modulo utilizzando l’API del servizio web](importing-exporting-data.md#export-form-data-using-the-web-service-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Guida introduttiva API Servizio di integrazione dati moduli](/help/forms/developing/form-data-integration-service-java.md#form-data-integration-service-java-api-quick-start-soap)

[Importazione dati modulo](importing-exporting-data.md#importing-form-data)

### Esportare i dati del modulo utilizzando l’API Java {#export-form-data-using-the-java-api}

Esporta i dati del modulo utilizzando l’API di integrazione dei dati del modulo (Java):

1. Includi file di progetto.

   Includi i file JAR client, ad esempio adobe-formdataintegration-client.jar, nel percorso di classe del progetto Java.

1. Creare un client del servizio di integrazione dei dati del modulo.

   * Creare un `ServiceClientFactory` oggetto che contiene proprietà di connessione.
   * Creare un `FormDataIntegrationClient` mediante il costruttore e passando il `ServiceClientFactory` oggetto.

1. Fai riferimento a un modulo di PDF.

   * Creare un `java.io.FileInputStream` mediante il costruttore e passare un valore stringa che specifica la posizione del modulo PDF contenente i dati da esportare.
   * Creare un `com.adobe.idp.Document` oggetto che memorizza il modulo PDF utilizzando `com.adobe.idp.Document` costruttore. Passa il `java.io.FileInputStream` oggetto che contiene il form PDF al costruttore.

1. Esporta dati dal modulo PDF.

   Esporta dati modulo richiamando `FormDataIntegrationClient` dell&#39;oggetto `exportData` e trasmettere il `com.adobe.idp.Document` oggetto che memorizza il modulo PDF. Questo metodo restituisce un `com.adobe.idp.Document` oggetto che memorizza i dati del modulo come schema XML.

1. Salvare il modulo PDF come file PDF.

   * Creare un `java.io.File` e assicurarsi che l&#39;estensione del file sia XML.
   * Richiama `Document` dell&#39;oggetto `copyToFile` metodo per copiare il contenuto del `Document` al file (assicurati di utilizzare il `Document` oggetto restituito da `exportData` metodo).

**Consulta anche**

[Riepilogo dei passaggi](importing-exporting-data.md#summary-of-steps)

[Quick Start (modalità SOAP): esportazione dei dati del modulo tramite API Java](/help/forms/developing/form-data-integration-service-java.md#quick-start-soap-mode-exporting-form-data-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Esportare i dati del modulo utilizzando l’API del servizio web {#export-form-data-using-the-web-service-api}

Esporta i dati del modulo utilizzando l’API di integrazione dei dati del modulo (servizio web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/FormDataIntegration?WSDL&lc_version=9.0.1`.

   * Sostituisci `localhost` con l’indirizzo IP del server che ospita AEM Forms.

1. Creare un client del servizio di integrazione dei dati del modulo.

   * Creare un `FormDataIntegrationClient` utilizzando il costruttore predefinito.
   * Creare un `FormDataIntegrationClient.Endpoint.Address` oggetto utilizzando `System.ServiceModel.EndpointAddress` costruttore. Passa un valore stringa che specifica il file WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/FormDataIntegration?blob=mtom`.) Non è necessario utilizzare il `lc_version` attributo. Questo attributo viene utilizzato quando si crea un riferimento a un servizio. Tuttavia, specifica `?blob=mtom` per utilizzare MTOM.
   * Creare un `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto ottenendo il valore del `FormDataIntegrationClient.Endpoint.Binding` campo. Invia il valore restituito a `BasicHttpBinding`.
   * Imposta il `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegna al campo il nome utente dei moduli AEM `FormDataIntegrationClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore password corrispondente al campo `FormDataIntegrationClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Fai riferimento a un modulo di PDF.

   * Creare un `BLOB` mediante il costruttore. Questo `BLOB` L&#39;oggetto viene utilizzato per memorizzare il modulo PDF da cui vengono esportati i dati.
   * Creare un `System.IO.FileStream` richiamando il relativo costruttore. Passa un valore stringa che specifica la posizione del modulo PDF e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto della `System.IO.FileStream` oggetto. È possibile determinare le dimensioni della matrice di byte ottenendo `System.IO.FileStream` dell&#39;oggetto `Length` proprietà.
   * Compilare la matrice di byte con i dati di flusso richiamando `System.IO.FileStream` dell&#39;oggetto `Read` e passando la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare il `BLOB` oggetto assegnando il relativo `MTOM` con il contenuto della matrice di byte.

1. Esporta dati dal modulo PDF.

   Importare dati nel modulo PDF richiamando `FormDataIntegrationClient` dell&#39;oggetto `exportData` e trasmettere il `BLOB` oggetto che memorizza il modulo PDF. Questo metodo restituisce un `BLOB` oggetto che memorizza i dati del modulo come schema XML.

1. Salvare il modulo PDF come file PDF.

   * Creare un `System.IO.FileStream` richiamando il relativo costruttore e passando un valore stringa che rappresenta la posizione del file XML.
   * Creare una matrice di byte che memorizza il contenuto dei dati `BLOB` oggetto restituito da `exportData` metodo. Popolare la matrice di byte ottenendo il valore della `BLOB` dell&#39;oggetto `MTOM` campo.
   * Creare un `System.IO.BinaryWriter` oggetto richiamando il relativo costruttore e passando il `System.IO.FileStream` oggetto.
   * Scrivere il contenuto della matrice di byte in un file XML richiamando `System.IO.BinaryWriter` dell&#39;oggetto `Write` e passando la matrice di byte.

**Consulta anche**

[Riepilogo dei passaggi](importing-exporting-data.md#summary-of-steps)

[Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamare AEM Forms con SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
