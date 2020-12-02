---
title: Convalida di documenti DDX
seo-title: Convalida di documenti DDX
description: 'null'
seo-description: 'null'
uuid: da668170-d2e9-4fff-aef5-432a856bd0bd
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 693859b0-a0c3-43f1-95c0-be48a90d7d8d
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1503'
ht-degree: 0%

---


# Convalida di documenti DDX {#validating-ddx-documents}

È possibile convalidare a livello di programmazione un documento DDX utilizzato dal servizio Assembler. Utilizzando l&#39;API del servizio Assembler è possibile determinare se un documento DDX è valido o meno. Ad esempio, se si è eseguito l&#39;aggiornamento da una versione precedente di AEM Forms  e si desidera verificare la validità del documento DDX, è possibile convalidarlo utilizzando l&#39;API del servizio Assembler.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Assembler, vedere [Guida di riferimento dei servizi per  AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Per ulteriori informazioni su un documento DDX, vedere [Servizio Assembler e Riferimento DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Riepilogo dei passaggi {#summary-of-steps}

Per convalidare un documento DDX, eseguire le operazioni seguenti:

1. Includere i file di progetto.
1. Creare un client Assembler.
1. Fare riferimento a un documento DDX esistente.
1. Impostare le opzioni di esecuzione per convalidare il documento DDX.
1. Eseguire la convalida.
1. Salvare i risultati della convalida in un file di registro.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, accertatevi di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (richiesto se  AEM Forms è distribuito su JBoss)
* jbossall-client.jar (richiesto se  AEM Forms è distribuito su JBoss)

se  AEM Forms è distribuito su un server applicazione J2EE supportato diverso da JBoss, è necessario sostituire i file adobe-utilities.jar e jbossall-client.jar con file JAR specifici del server applicazione J2EE in cui  AEM Forms è distribuito.

**Creare un client Assembler PDF**

Prima di eseguire un&#39;operazione Assembler a livello di programmazione, è necessario creare un client di servizio Assembler.

**Riferimento a un documento DDX esistente**

Per convalidare un documento DDX, è necessario fare riferimento a un documento DDX esistente.

**Impostazione delle opzioni di esecuzione per convalidare il documento DDX**

Durante la convalida di un documento DDX, è necessario impostare opzioni di esecuzione specifiche che indichino al servizio Assembler di convalidare il documento DDX anziché eseguirlo. Inoltre, potete aumentare la quantità di informazioni che il servizio Assembler scrive nel file di registro.

**Eseguire la convalida**

Dopo aver creato il client del servizio Assembler, fatto riferimento al documento DDX e impostato le opzioni di esecuzione, è possibile richiamare l&#39;operazione `invokeDDX` per convalidare il documento DDX. Durante la convalida del documento DDX, è possibile passare `null` come parametro della mappa (in genere questo parametro memorizza i documenti PDF richiesti dall&#39;Assembler per eseguire le operazioni specificate nel documento DDX).

Se la convalida non riesce, viene generata un&#39;eccezione e il file di registro contiene dettagli che spiegano perché il documento DDX non è valido può essere ottenuto dall&#39;istanza `OperationException`. Dopo l&#39;analisi XML di base e il controllo dello schema, viene eseguita la convalida rispetto alla specifica DDX. Tutti gli errori che si trovano nel documento DDX sono specificati nel registro.

**Salvare i risultati della convalida in un file di registro**

Il servizio Assembler restituisce i risultati di convalida che è possibile scrivere in un file di registro XML. La quantità di dettagli che il servizio Assembler scrive nel file di registro dipende dall&#39;opzione di esecuzione impostata.

**Consulta anche**

[Convalidare un documento DDX utilizzando l&#39;API Java](#validate-a-ddx-document-using-the-java-api)

[Convalida di un documento DDX tramite l&#39;API del servizio Web](#validate-a-ddx-document-using-the-web-service-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Assemblaggio di documenti PDF a livello di programmazione](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Convalidare un documento DDX utilizzando l&#39;API Java {#validate-a-ddx-document-using-the-java-api}

Convalidare un documento DDX utilizzando l&#39;API del servizio Assembler (Java):

1. Includere i file di progetto.

   Includete file JAR client, ad esempio adobe-assembler-client.jar, nel percorso di classe del progetto Java.

1. Creare un client Assembler PDF.

   * Creare un oggetto `ServiceClientFactory` che contiene le proprietà di connessione.
   * Creare un oggetto `AssemblerServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Fare riferimento a un documento DDX esistente.

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento DDX utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del file DDX.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Impostare le opzioni di esecuzione per convalidare il documento DDX.

   * Creare un oggetto `AssemblerOptionSpec` che memorizza le opzioni di esecuzione utilizzando il relativo costruttore.
   * Impostare l&#39;opzione di esecuzione che indica al servizio Assembler di convalidare il documento DDX richiamando il metodo setValidateOnly dell&#39;oggetto `AssemblerOptionSpec` e passando `true`.
   * Impostate la quantità di informazioni che il servizio Assembler scrive nel file di registro richiamando il metodo `AssemblerOptionSpec` dell&#39;oggetto `getLogLevel` e passando un valore di stringa in base alle vostre esigenze. Durante la convalida di un documento DDX, è necessario scrivere nel file di registro ulteriori informazioni utili al processo di convalida. Di conseguenza, è possibile trasmettere il valore `FINE` o `FINER`.

1. Eseguire la convalida.

   Richiamare il metodo `AssemblerServiceClient` dell&#39;oggetto `invokeDDX` e trasmettere i seguenti valori:

   * Un oggetto `com.adobe.idp.Document` che rappresenta il documento DDX.
   * Il valore `null` per l&#39;oggetto java.io.Map che in genere memorizza i documenti PDF.
   * Un oggetto `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` che specifica le opzioni di esecuzione.

   Il metodo `invokeDDX` restituisce un oggetto `AssemblerResult` che contiene informazioni che specificano se il documento DDX è valido.

1. Salvare i risultati della convalida in un file di registro.

   * Create un oggetto `java.io.File` e accertatevi che l&#39;estensione del nome del file sia .xml.
   * Richiamare il metodo `AssemblerResult` dell&#39;oggetto `getJobLog`. Questo metodo restituisce un&#39;istanza `com.adobe.idp.Document` che contiene informazioni di convalida.
   * Richiamare il metodo `com.adobe.idp.Document` dell&#39;oggetto `copyToFile` per copiare nel file il contenuto dell&#39;oggetto `com.adobe.idp.Document`.

   >[!NOTE]
   >
   >Se il documento DDX non è valido, viene generato un `OperationException`. All&#39;interno dell&#39;istruzione catch, è possibile richiamare il metodo `OperationException` dell&#39;oggetto `getJobLog`.

**Consulta anche**

[Convalida di documenti DDX](#validating-ddx-documents)

[Avvio rapido (modalità SOAP): Convalida dei documenti DDX tramite l&#39;API](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-validating-ddx-documents-using-the-java-api)  Java (modalità SOAP)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Convalida di un documento DDX utilizzando l&#39;API del servizio Web {#validate-a-ddx-document-using-the-web-service-api}

Convalidare un documento DDX utilizzando l&#39;API del servizio Assembler (servizio Web):

1. Includere i file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituire localhost con l&#39;indirizzo IP del server dei moduli.

1. Creare un client Assembler PDF.

   * Creare un oggetto `AssemblerServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `AssemblerServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passate un valore di stringa che specifica il WSDL al servizio AEM Forms  (ad esempio, `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). Non è necessario utilizzare l&#39;attributo `lc_version`. Questo attributo viene utilizzato quando create un riferimento a un servizio.
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `AssemblerServiceClient.Endpoint.Binding`. Inserite il valore restituito in `BasicHttpBinding`.
   * Impostare il campo `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto `MessageEncoding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilitate l&#39;autenticazione HTTP di base eseguendo le seguenti operazioni:

      * Assegnare il nome utente del modulo AEM al campo `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Fare riferimento a un documento DDX esistente.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare il documento DDX.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento DDX e la modalità in cui aprire il file.
   * Creare un array di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà `System.IO.FileStream` dell&#39;oggetto `Length`.
   * Compilare l&#39;array di byte con i dati del flusso richiamando il metodo `Read` dell&#39;oggetto `System.IO.FileStream` e passando l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnandone la proprietà `MTOM` con il contenuto dell&#39;array di byte.

1. Impostare le opzioni di esecuzione per convalidare il documento DDX.

   * Creare un oggetto `AssemblerOptionSpec` che memorizza le opzioni di esecuzione utilizzando il relativo costruttore.
   * Impostare l&#39;opzione di esecuzione che indica al servizio Assembler di convalidare il documento DDX assegnando il valore true al membro di dati `AssemblerOptionSpec` dell&#39;oggetto `validateOnly`.
   * Impostate la quantità di informazioni che il servizio Assembler scrive nel file di registro assegnando un valore stringa al membro di dati `AssemblerOptionSpec` dell&#39;oggetto `logLevel`. durante la convalida di un documento DDX, è necessario scrivere ulteriori informazioni nel file di registro per facilitare il processo di convalida. Di conseguenza, è possibile specificare il valore `FINE` o `FINER`. Per informazioni sulle opzioni di esecuzione che è possibile impostare, vedere il riferimento alla classe `AssemblerOptionSpec` in [ Guida di riferimento delle API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. Eseguire la convalida.

   Richiamare il metodo `AssemblerServiceClient` dell&#39;oggetto `invokeDDX` e trasmettere i seguenti valori:

   * Un oggetto `BLOB` che rappresenta il documento DDX.
   * Il valore `null` per l&#39;oggetto `Map` che in genere memorizza i documenti PDF.
   * Un oggetto `AssemblerOptionSpec` che specifica le opzioni di esecuzione.

   Il metodo `invokeDDX` restituisce un oggetto `AssemblerResult` che contiene informazioni che specificano se il documento DDX è valido.

1. Salvare i risultati della convalida in un file di registro.

   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file di registro e la modalità in cui aprire il file. Accertatevi che l’estensione del nome del file sia .xml.
   * Creare un oggetto `BLOB` che memorizza le informazioni del registro ottenendo il valore del membro di dati `AssemblerResult` dell&#39;oggetto `jobLog`.
   * Creare un array di byte che memorizza il contenuto dell&#39;oggetto `BLOB`. Compilare l&#39;array di byte ottenendo il valore del campo `BLOB` dell&#39;oggetto `MTOM`.
   * Creare un oggetto `System.IO.BinaryWriter` richiamandone il costruttore e passando l&#39;oggetto `System.IO.FileStream`.
   * Scrivere il contenuto dell&#39;array di byte in un file PDF richiamando il metodo `System.IO.BinaryWriter` dell&#39;oggetto `Write` e passando l&#39;array di byte.

   >[!NOTE]
   >
   >Se il documento DDX non è valido, viene generato un `OperationException`. All&#39;interno dell&#39;istruzione catch, è possibile ottenere il valore del membro `OperationException` dell&#39;oggetto `jobLog`.

**Consulta anche**

[Convalida di documenti DDX](#validating-ddx-documents)

[Chiamata  AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
