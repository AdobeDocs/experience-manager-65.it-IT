---
title: Convalida dei documenti DDX
seo-title: Validating DDX Documents
description: Convalida un documento DDX a livello di programmazione utilizzando l’API Java e l’API Web Service.
seo-description: Validate a DDX document programmatically using the Java API and the Web Service API.
uuid: da668170-d2e9-4fff-aef5-432a856bd0bd
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 693859b0-a0c3-43f1-95c0-be48a90d7d8d
role: Developer
exl-id: 1f5a2cf3-ef6b-45b4-8fa8-b300e492fee1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1526'
ht-degree: 0%

---

# Convalida dei documenti DDX {#validating-ddx-documents}

**Esempi ed esempi in questo documento sono solo per AEM Forms in ambiente JEE.**

È possibile convalidare programmaticamente un documento DDX utilizzato dal servizio Assembler. In altre parole, utilizzando l&#39;API del servizio Assembler, è possibile determinare se un documento DDX è valido o meno. Ad esempio, se il documento DDX è stato aggiornato da una versione precedente di AEM Forms e si desidera verificarne la validità, è possibile convalidarlo utilizzando l&#39;API del servizio Assembler.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Assembler, vedere [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Per ulteriori informazioni su un documento DDX, consulta [Servizio di assemblaggio e riferimento DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Riepilogo dei passaggi {#summary-of-steps}

Per convalidare un documento DDX, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Creare un client Assembler.
1. Fai riferimento a un documento DDX esistente.
1. Impostare le opzioni di esecuzione per convalidare il documento DDX.
1. Esegui la convalida.
1. Salvare i risultati della convalida in un file di registro.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso della classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è distribuito su JBoss)
* jbossall-client.jar (richiesto se AEM Forms è distribuito su JBoss)

se AEM Forms è implementato su un server applicazioni J2EE supportato diverso da JBoss, è necessario sostituire i file adobe-utilities.jar e jbossall-client.jar con file JAR specifici per il server applicazioni J2EE in cui è implementato AEM Forms.

**Creare un client PDF Assembler**

Prima di poter eseguire un&#39;operazione Assembler a livello di programmazione, è necessario creare un client di servizio Assembler.

**Riferimento a un documento DDX esistente**

Per convalidare un documento DDX, è necessario fare riferimento a un documento DDX esistente.

**Impostare le opzioni di esecuzione per convalidare il documento DDX**

Quando si convalida un documento DDX, è necessario impostare opzioni di esecuzione specifiche che istruiscono il servizio Assembler di convalidare il documento DDX anziché eseguirlo. Inoltre, è possibile aumentare la quantità di informazioni che il servizio Assembler scrive nel file di registro.

**Esegui la convalida**

Dopo aver creato il client di servizio Assembler, fare riferimento al documento DDX e impostare le opzioni di esecuzione, è possibile richiamare il `invokeDDX` per convalidare il documento DDX. Quando si convalida il documento DDX, è possibile passare `null` come parametro map (questo parametro in genere memorizza i documenti PDF richiesti dall&#39;Assembler per eseguire le operazioni specificate nel documento DDX).

Se la convalida non riesce, viene generata un&#39;eccezione e il file di registro contiene dettagli che spiegano perché il documento DDX non è valido può essere ottenuto da `OperationException` istanza. Una volta superata l&#39;analisi XML di base e il controllo dello schema, viene eseguita la convalida rispetto alla specifica DDX. Tutti gli errori che si trovano nel documento DDX sono specificati nel registro.

**Salvare i risultati della convalida in un file di registro**

Il servizio Assembler restituisce i risultati della convalida che è possibile scrivere in un file di log XML. La quantità di dettagli che il servizio Assembler scrive nel file di registro dipende dall&#39;opzione di esecuzione impostata.

**Consulta anche**

[Convalidare un documento DDX utilizzando l’API Java](#validate-a-ddx-document-using-the-java-api)

[Convalidare un documento DDX utilizzando l’API del servizio Web](#validate-a-ddx-document-using-the-web-service-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Assemblaggio di documenti PDF a livello di programmazione](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Convalidare un documento DDX utilizzando l’API Java {#validate-a-ddx-document-using-the-java-api}

Convalida un documento DDX utilizzando l&#39;API del servizio Assembler (Java):

1. Includi file di progetto.

   Includi file JAR client, come adobe-assembler-client.jar, nel percorso di classe del progetto Java.

1. Creare un client PDF Assembler.

   * Crea un `ServiceClientFactory` oggetto contenente le proprietà di connessione.
   * Crea un `AssemblerServiceClient` utilizzando il relativo costruttore e passando `ServiceClientFactory` oggetto.

1. Fai riferimento a un documento DDX esistente.

   * Crea un `java.io.FileInputStream` oggetto che rappresenta il documento DDX utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del file DDX.
   * Crea un `com.adobe.idp.Document` utilizzando il relativo costruttore e passando `java.io.FileInputStream` oggetto.

1. Impostare le opzioni di esecuzione per convalidare il documento DDX.

   * Crea un `AssemblerOptionSpec` oggetto che memorizza le opzioni di esecuzione utilizzando il relativo costruttore.
   * Impostare l&#39;opzione di esecuzione che indica al servizio Assembler di convalidare il documento DDX richiamando il `AssemblerOptionSpec` il metodo setValidateOnly dell&#39;oggetto e il passaggio `true`.
   * Impostare la quantità di informazioni che il servizio Assembler scrive nel file di registro richiamando il `AssemblerOptionSpec` dell’oggetto `getLogLevel` e il passaggio di un valore stringa soddisfa le tue esigenze. Durante la convalida di un documento DDX, è necessario scrivere ulteriori informazioni nel file di registro per facilitare il processo di convalida. Di conseguenza, puoi trasmettere il valore `FINE` o `FINER`.

1. Esegui la convalida.

   Richiama il `AssemblerServiceClient` dell’oggetto `invokeDDX` e passare i seguenti valori:

   * A `com.adobe.idp.Document` oggetto che rappresenta il documento DDX.
   * Il valore `null` per l’oggetto java.io.Map che in genere memorizza i documenti PDF.
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` oggetto che specifica le opzioni di esecuzione.

   La `invokeDDX` restituisce un `AssemblerResult` oggetto contenente informazioni che specificano se il documento DDX è valido.

1. Salvare i risultati della convalida in un file di registro.

   * Crea un `java.io.File` e assicurati che l&#39;estensione del nome del file sia .xml.
   * Richiama il `AssemblerResult` dell’oggetto `getJobLog` metodo . Questo metodo restituisce un `com.adobe.idp.Document` istanza che contiene informazioni di convalida.
   * Richiama il `com.adobe.idp.Document` dell’oggetto `copyToFile` per copiare il contenuto del `com.adobe.idp.Document` al file.

   >[!NOTE]
   >
   >Se il documento DDX non è valido, un `OperationException` è gettato. All’interno dell’istruzione catch, è possibile richiamare `OperationException` dell&#39;oggetto `getJobLog` metodo .

**Consulta anche**

[Convalida dei documenti DDX](#validating-ddx-documents)

[Avvio rapido (modalità SOAP): Convalida dei documenti DDX tramite API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-validating-ddx-documents-using-the-java-api) (modalità SOAP)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Convalidare un documento DDX utilizzando l’API del servizio Web {#validate-a-ddx-document-using-the-web-service-api}

Convalida un documento DDX utilizzando l&#39;API del servizio Assembler (servizio Web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurati di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituire localhost con l’indirizzo IP del server dei moduli.

1. Creare un client PDF Assembler.

   * Crea un `AssemblerServiceClient` utilizzando il relativo costruttore predefinito.
   * Crea un `AssemblerServiceClient.Endpoint.Address` utilizzando `System.ServiceModel.EndpointAddress` costruttore. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). Non è necessario utilizzare il `lc_version` attributo. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.
   * Crea un `System.ServiceModel.BasicHttpBinding` ottenendo il valore del `AssemblerServiceClient.Endpoint.Binding` campo . Imposta il valore restituito su `BasicHttpBinding`.
   * Imposta la `System.ServiceModel.BasicHttpBinding` dell’oggetto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegnare il nome utente del modulo di AEM al campo `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore della password corrispondente al campo `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Fai riferimento a un documento DDX esistente.

   * Crea un `BLOB` utilizzando il relativo costruttore. La `BLOB` viene utilizzato per memorizzare il documento DDX.
   * Crea un `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento DDX e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto del `System.IO.FileStream` oggetto. È possibile determinare le dimensioni dell&#39;array di byte ottenendo il `System.IO.FileStream` dell’oggetto `Length` proprietà.
   * Compilare l&#39;array di byte con i dati del flusso richiamando il `System.IO.FileStream` dell’oggetto `Read` e passare l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare `BLOB` oggetto assegnando il relativo `MTOM` con il contenuto dell&#39;array di byte.

1. Impostare le opzioni di esecuzione per convalidare il documento DDX.

   * Crea un `AssemblerOptionSpec` oggetto che memorizza le opzioni di esecuzione utilizzando il relativo costruttore.
   * Impostare l&#39;opzione di esecuzione che indica al servizio Assembler di convalidare il documento DDX assegnando il valore true al `AssemblerOptionSpec` dell’oggetto `validateOnly` membro dati.
   * Impostare la quantità di informazioni che il servizio Assembler scrive nel file di registro assegnando un valore stringa al `AssemblerOptionSpec` dell’oggetto `logLevel` membro dati. metodo Durante la convalida di un documento DDX, è necessario scrivere ulteriori informazioni nel file di registro per facilitare il processo di convalida. Di conseguenza, è possibile specificare il valore `FINE` o `FINER`. Per informazioni sulle opzioni di esecuzione che è possibile impostare, vedere la `AssemblerOptionSpec` riferimento di classe in [Riferimento API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. Esegui la convalida.

   Richiama il `AssemblerServiceClient` dell’oggetto `invokeDDX` e passare i seguenti valori:

   * A `BLOB` oggetto che rappresenta il documento DDX.
   * Il valore `null` per `Map` oggetto che in genere memorizza i documenti PDF.
   * Un `AssemblerOptionSpec` oggetto che specifica le opzioni di esecuzione.

   La `invokeDDX` restituisce un `AssemblerResult` oggetto contenente informazioni che specificano se il documento DDX è valido.

1. Salvare i risultati della convalida in un file di registro.

   * Crea un `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file di log e la modalità di apertura del file. Assicurati che l&#39;estensione del nome file sia .xml.
   * Crea un `BLOB` oggetto che memorizza le informazioni del registro ottenendo il valore del `AssemblerResult` dell’oggetto `jobLog` membro dati.
   * Creare un array di byte che memorizza il contenuto del `BLOB` oggetto. Compilare l’array di byte ottenendo il valore del `BLOB` dell’oggetto `MTOM` campo .
   * Crea un `System.IO.BinaryWriter` richiamando il relativo costruttore e passando `System.IO.FileStream` oggetto.
   * Scrivi il contenuto dell’array di byte in un file PDF richiamando il `System.IO.BinaryWriter` dell’oggetto `Write` e passare l&#39;array di byte.

   >[!NOTE]
   >
   >Se il documento DDX non è valido, un `OperationException` è gettato. All’interno dell’istruzione catch, è possibile ottenere il valore del `OperationException` dell&#39;oggetto `jobLog` membro.

**Consulta anche**

[Convalida dei documenti DDX](#validating-ddx-documents)

[Richiamo di AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
