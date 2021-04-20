---
title: Convalida dei documenti DDX
seo-title: Convalida dei documenti DDX
description: Convalida un documento DDX a livello di programmazione utilizzando l’API Java e l’API Web Service.
seo-description: Convalida un documento DDX a livello di programmazione utilizzando l’API Java e l’API Web Service.
uuid: da668170-d2e9-4fff-aef5-432a856bd0bd
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 693859b0-a0c3-43f1-95c0-be48a90d7d8d
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1544'
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
>Per ulteriori informazioni su un documento DDX, vedere [Servizio Assembler e Riferimento DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

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

**Creare un client Assembler PDF**

Prima di poter eseguire un&#39;operazione Assembler a livello di programmazione, è necessario creare un client di servizio Assembler.

**Riferimento a un documento DDX esistente**

Per convalidare un documento DDX, è necessario fare riferimento a un documento DDX esistente.

**Impostare le opzioni di esecuzione per convalidare il documento DDX**

Quando si convalida un documento DDX, è necessario impostare opzioni di esecuzione specifiche che istruiscono il servizio Assembler a convalidare il documento DDX anziché eseguirlo. Inoltre, è possibile aumentare la quantità di informazioni che il servizio Assembler scrive nel file di registro.

**Esegui la convalida**

Dopo aver creato il client di servizio Assembler, fare riferimento al documento DDX e impostare le opzioni di esecuzione, è possibile richiamare l&#39;operazione `invokeDDX` per convalidare il documento DDX. Quando si convalida il documento DDX, è possibile passare `null` come parametro di mappa (questo parametro in genere memorizza i documenti PDF richiesti dall&#39;Assembler per eseguire le operazioni specificate nel documento DDX).

Se la convalida non riesce, viene generata un&#39;eccezione e il file di registro contiene dettagli che spiegano perché il documento DDX non è valido può essere ottenuto dall&#39;istanza `OperationException`. Una volta superata l&#39;analisi XML di base e il controllo dello schema, viene eseguita la convalida rispetto alla specifica DDX. Tutti gli errori che si trovano nel documento DDX sono specificati nel registro.

**Salvare i risultati della convalida in un file di registro**

Il servizio Assembler restituisce i risultati della convalida che è possibile scrivere in un file di log XML. La quantità di dettagli che il servizio Assembler scrive nel file di registro dipende dall&#39;opzione di esecuzione impostata.

**Consulta anche**

[Convalidare un documento DDX utilizzando l’API Java](#validate-a-ddx-document-using-the-java-api)

[Convalidare un documento DDX utilizzando l’API del servizio Web](#validate-a-ddx-document-using-the-web-service-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Assemblaggio programmatico di documenti PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Convalida un documento DDX utilizzando l&#39;API Java {#validate-a-ddx-document-using-the-java-api}

Convalida un documento DDX utilizzando l&#39;API del servizio Assembler (Java):

1. Includi file di progetto.

   Includi file JAR client, come adobe-assembler-client.jar, nel percorso di classe del progetto Java.

1. Creare un client Assembler PDF.

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `AssemblerServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Fai riferimento a un documento DDX esistente.

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento DDX utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del file DDX.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Impostare le opzioni di esecuzione per convalidare il documento DDX.

   * Creare un oggetto `AssemblerOptionSpec` che memorizza le opzioni di esecuzione utilizzando il relativo costruttore.
   * Impostare l&#39;opzione di esecuzione che indica al servizio Assembler di convalidare il documento DDX richiamando il metodo setValidateOnly dell&#39;oggetto `AssemblerOptionSpec` e passando `true`.
   * Impostare la quantità di informazioni che il servizio Assembler scrive nel file di registro richiamando il metodo `AssemblerOptionSpec` dell&#39;oggetto `getLogLevel` e passando un valore di stringa soddisfa le tue esigenze. Durante la convalida di un documento DDX, è necessario scrivere ulteriori informazioni nel file di registro per facilitare il processo di convalida. Di conseguenza, è possibile trasmettere il valore `FINE` o `FINER`.

1. Esegui la convalida.

   Richiama il metodo `invokeDDX` dell&#39;oggetto `AssemblerServiceClient` e passa i seguenti valori:

   * Un oggetto `com.adobe.idp.Document` che rappresenta il documento DDX.
   * Il valore `null` per l&#39;oggetto java.io.Map che in genere memorizza i documenti PDF.
   * Un oggetto `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` che specifica le opzioni di esecuzione.

   Il metodo `invokeDDX` restituisce un oggetto `AssemblerResult` contenente informazioni che specificano se il documento DDX è valido.

1. Salvare i risultati della convalida in un file di registro.

   * Crea un oggetto `java.io.File` e assicurati che l&#39;estensione del nome file sia .xml.
   * Richiama il metodo `getJobLog` dell&#39;oggetto `AssemblerResult`. Questo metodo restituisce un&#39;istanza `com.adobe.idp.Document` che contiene informazioni di convalida.
   * Richiamare il metodo `copyToFile` dell&#39;oggetto `com.adobe.idp.Document` per copiare nel file il contenuto dell&#39;oggetto `com.adobe.idp.Document`.

   >[!NOTE]
   >
   >Se il documento DDX non è valido, viene generato un `OperationException`. All’interno dell’istruzione catch, è possibile richiamare il metodo `OperationException` dell’oggetto `getJobLog`.

**Consulta anche**

[Convalida dei documenti DDX](#validating-ddx-documents)

[Avvio rapido (modalità SOAP): Convalida dei documenti DDX utilizzando l’API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-validating-ddx-documents-using-the-java-api)  (modalità SOAP)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Convalida un documento DDX utilizzando l&#39;API del servizio Web {#validate-a-ddx-document-using-the-web-service-api}

Convalida un documento DDX utilizzando l&#39;API del servizio Assembler (servizio Web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurati di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituire localhost con l’indirizzo IP del server dei moduli.

1. Creare un client Assembler PDF.

   * Creare un oggetto `AssemblerServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `AssemblerServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). Non è necessario utilizzare l&#39;attributo `lc_version` . Questo attributo viene utilizzato quando si crea un riferimento a un servizio.
   * Crea un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `AssemblerServiceClient.Endpoint.Binding` . Imposta il valore restituito su `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegna il nome utente del modulo di AEM al campo `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore della password corrispondente al campo `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Fai riferimento a un documento DDX esistente.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare il documento DDX.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento DDX e la modalità in cui aprire il file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni dell&#39;array di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare l’array di byte con i dati del flusso richiamando il metodo `Read` dell’oggetto `System.IO.FileStream` e passando l’array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando la relativa proprietà `MTOM` con il contenuto dell&#39;array di byte.

1. Impostare le opzioni di esecuzione per convalidare il documento DDX.

   * Creare un oggetto `AssemblerOptionSpec` che memorizza le opzioni di esecuzione utilizzando il relativo costruttore.
   * Impostare l&#39;opzione di esecuzione che indica al servizio Assembler di convalidare il documento DDX assegnando il valore true al membro dati `AssemblerOptionSpec` dell&#39;oggetto `validateOnly`.
   * Impostare la quantità di informazioni che il servizio Assembler scrive nel file di registro assegnando un valore stringa al membro dati `AssemblerOptionSpec` dell&#39;oggetto `logLevel`. metodo Durante la convalida di un documento DDX, è necessario scrivere ulteriori informazioni nel file di registro per facilitare il processo di convalida. Di conseguenza, è possibile specificare il valore `FINE` o `FINER`. Per informazioni sulle opzioni di esecuzione che è possibile impostare, vedere il riferimento alla classe `AssemblerOptionSpec` in [Riferimento API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. Esegui la convalida.

   Richiama il metodo `invokeDDX` dell&#39;oggetto `AssemblerServiceClient` e passa i seguenti valori:

   * Un oggetto `BLOB` che rappresenta il documento DDX.
   * Il valore `null` dell&#39;oggetto `Map` che in genere memorizza i documenti PDF.
   * Un oggetto `AssemblerOptionSpec` che specifica le opzioni di esecuzione.

   Il metodo `invokeDDX` restituisce un oggetto `AssemblerResult` contenente informazioni che specificano se il documento DDX è valido.

1. Salvare i risultati della convalida in un file di registro.

   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file di registro e la modalità di apertura del file. Assicurati che l&#39;estensione del nome file sia .xml.
   * Creare un oggetto `BLOB` che memorizza le informazioni di registro ottenendo il valore del membro dati `AssemblerResult` dell&#39;oggetto `jobLog`.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `BLOB`. Compilare l’array di byte ottenendo il valore del campo `BLOB` dell’oggetto `MTOM`.
   * Creare un oggetto `System.IO.BinaryWriter` richiamandone il costruttore e passando l&#39;oggetto `System.IO.FileStream`.
   * Scrivi il contenuto dell’array di byte in un file PDF richiamando il metodo `Write` dell’oggetto `System.IO.BinaryWriter` e passando l’array di byte.

   >[!NOTE]
   >
   >Se il documento DDX non è valido, viene generato un `OperationException`. All&#39;interno dell&#39;istruzione catch, è possibile ottenere il valore del membro `OperationException` dell&#39;oggetto `jobLog`.

**Consulta anche**

[Convalida dei documenti DDX](#validating-ddx-documents)

[Richiamo di AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
