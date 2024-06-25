---
title: Convalida dei documenti DDX
description: Convalidare un documento DDX a livello di programmazione utilizzando l'API Java e l'API del servizio Web.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 1f5a2cf3-ef6b-45b4-8fa8-b300e492fee1
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1507'
ht-degree: 0%

---

# Convalida dei documenti DDX {#validating-ddx-documents}

**Gli esempi e gli esempi contenuti in questo documento sono solo per l’ambiente AEM Forms su JEE.**

È possibile convalidare a livello di programmazione un documento DDX utilizzato dal servizio Assembler. In altre parole, utilizzando l&#39;API del servizio Assembler, è possibile determinare se un documento DDX è valido o meno. Se ad esempio si è eseguito l&#39;aggiornamento da una versione precedente di AEM Forms e si desidera verificare che il documento DDX sia valido, è possibile convalidarlo utilizzando l&#39;API del servizio Assembler.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Assembler, vedere [Guida di riferimento dei servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Per ulteriori informazioni su un documento DDX, vedere [Servizio assemblatore e riferimento DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Riepilogo dei passaggi {#summary-of-steps}

Per convalidare un documento DDX, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Creare un client Assembler.
1. Fare riferimento a un documento DDX esistente.
1. Impostare le opzioni di runtime per convalidare il documento DDX.
1. Eseguire la convalida.
1. Salvare i risultati della convalida in un file di registro.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso della classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è implementato su JBoss)
* jbossall-client.jar (obbligatorio se AEM Forms è distribuito su JBoss)

se AEM Forms viene distribuito su un server applicazioni J2EE supportato diverso da JBoss, è necessario sostituire i file adobe-utilities.jar e jbossall-client.jar con file JAR specifici per il server applicazioni J2EE su cui è distribuito AEM Forms.

**Creare un client PDF Assembler**

Prima di poter eseguire un&#39;operazione Assembler a livello di programmazione, è necessario creare un client del servizio Assembler.

**Riferimento a un documento DDX esistente**

Per convalidare un documento DDX, è necessario fare riferimento a un documento DDX esistente.

**Impostare le opzioni di runtime per convalidare il documento DDX**

Durante la convalida di un documento DDX, è necessario impostare opzioni di runtime specifiche che indichino al servizio Assembler di convalidare il documento DDX anziché eseguirlo. È inoltre possibile aumentare la quantità di informazioni che il servizio Assembler scrive nel file di registro.

**Eseguire la convalida**

Dopo aver creato il client del servizio Assembler, aver fatto riferimento al documento DDX e aver impostato le opzioni di runtime, è possibile richiamare `invokeDDX` operazione per convalidare il documento DDX. Durante la convalida del documento DDX, è possibile trasmettere `null` come parametro map (questo parametro in genere memorizza i documenti PDF necessari all&#39;Assembler per eseguire le operazioni specificate nel documento DDX).

Se la convalida non riesce, viene generata un&#39;eccezione e il file di registro contiene dettagli che spiegano perché il documento DDX non è valido. `OperationException` dell&#39;istanza. Dopo aver superato l&#39;analisi XML di base e il controllo dello schema, viene eseguita la convalida in base alla specifica DDX. Tutti gli errori presenti nel documento DDX vengono specificati nel registro.

**Salvare i risultati della convalida in un file di registro**

Il servizio Assembler restituisce i risultati della convalida che è possibile scrivere in un file di log XML. La quantità di dettagli che il servizio Assembler scrive nel file di log dipende dall&#39;opzione di runtime impostata.

**Consulta anche**

[Convalidare un documento DDX utilizzando l’API Java](#validate-a-ddx-document-using-the-java-api)

[Convalidare un documento DDX utilizzando l’API del servizio web](#validate-a-ddx-document-using-the-web-service-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Assemblaggio di documenti PDF a livello di programmazione](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Convalidare un documento DDX utilizzando l’API Java {#validate-a-ddx-document-using-the-java-api}

Convalidare un documento DDX utilizzando l&#39;API del servizio Assembler (Java):

1. Includi file di progetto.

   Includi i file JAR client, come adobe-assembler-client.jar, nel percorso di classe del progetto Java.

1. Creare un client PDF Assembler.

   * Creare un `ServiceClientFactory` oggetto che contiene proprietà di connessione.
   * Creare un `AssemblerServiceClient` mediante il costruttore e passando il `ServiceClientFactory` oggetto.

1. Fare riferimento a un documento DDX esistente.

   * Creare un `java.io.FileInputStream` oggetto che rappresenta il documento DDX utilizzando il relativo costruttore e passando un valore stringa che specifica la posizione del file DDX.
   * Creare un `com.adobe.idp.Document` mediante il costruttore e passando il `java.io.FileInputStream` oggetto.

1. Impostare le opzioni di runtime per convalidare il documento DDX.

   * Creare un `AssemblerOptionSpec` oggetto che memorizza le opzioni di runtime mediante il relativo costruttore.
   * Impostare l&#39;opzione di runtime che indica al servizio Assembler di convalidare il documento DDX richiamando `AssemblerOptionSpec` metodo setValidateOnly dell&#39;oggetto e passaggio `true`.
   * Impostare la quantità di informazioni che il servizio Assembler scrive nel file di log richiamando `AssemblerOptionSpec` dell&#39;oggetto `getLogLevel` e il passaggio di un valore stringa soddisfa le tue esigenze. Durante la convalida di un documento DDX, è necessario disporre di ulteriori informazioni scritte nel file di registro che possano essere utili per il processo di convalida. Di conseguenza, puoi trasmettere il valore `FINE` o `FINER`.

1. Eseguire la convalida.

   Richiama `AssemblerServiceClient` dell&#39;oggetto `invokeDDX` e trasmettere i seguenti valori:

   * A `com.adobe.idp.Document` oggetto che rappresenta il documento DDX.
   * Il valore `null` per l&#39;oggetto java.io.Map che in genere memorizza i documenti PDF.
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` oggetto che specifica le opzioni di runtime.

   Il `invokeDDX` il metodo restituisce un `AssemblerResult` oggetto contenente informazioni che specificano se il documento DDX è valido.

1. Salvare i risultati della convalida in un file di registro.

   * Creare un `java.io.File` e assicurarsi che l&#39;estensione del nome file sia .xml.
   * Richiama `AssemblerResult` dell&#39;oggetto `getJobLog` metodo. Questo metodo restituisce un `com.adobe.idp.Document` istanza che contiene informazioni di convalida.
   * Richiama `com.adobe.idp.Document` dell&#39;oggetto `copyToFile` metodo per copiare il contenuto del `com.adobe.idp.Document` al file.

   >[!NOTE]
   >
   >Se il documento DDX non è valido, `OperationException` viene lanciato. All’interno dell’istruzione catch, puoi richiamare `OperationException` dell&#39;oggetto `getJobLog` metodo.

**Consulta anche**

[Convalida dei documenti DDX](#validating-ddx-documents)

[Guida rapida (modalità SOAP): convalida dei documenti DDX tramite l’API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-validating-ddx-documents-using-the-java-api) (modalità SOAP)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Convalidare un documento DDX utilizzando l’API del servizio web {#validate-a-ddx-document-using-the-web-service-api}

Convalidare un documento DDX utilizzando l&#39;API del servizio Assembler (servizio Web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituire localhost con l&#39;indirizzo IP di Forms Server.

1. Creare un client PDF Assembler.

   * Creare un `AssemblerServiceClient` utilizzando il costruttore predefinito.
   * Creare un `AssemblerServiceClient.Endpoint.Address` oggetto utilizzando `System.ServiceModel.EndpointAddress` costruttore. Passa un valore stringa che specifica il file WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). Non è necessario utilizzare il `lc_version` attributo. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.
   * Creare un `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto ottenendo il valore del `AssemblerServiceClient.Endpoint.Binding` campo. Invia il valore restituito a `BasicHttpBinding`.
   * Imposta il `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegna al campo il nome utente dei moduli AEM `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore password corrispondente al campo `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Fare riferimento a un documento DDX esistente.

   * Creare un `BLOB` mediante il costruttore. Il `BLOB` viene utilizzato per memorizzare il documento DDX.
   * Creare un `System.IO.FileStream` richiamando il relativo costruttore e passando un valore stringa che rappresenta la posizione del file del documento DDX e la modalità di apertura del file in.
   * Creare una matrice di byte che memorizza il contenuto della `System.IO.FileStream` oggetto. È possibile determinare le dimensioni della matrice di byte ottenendo `System.IO.FileStream` dell&#39;oggetto `Length` proprietà.
   * Compilare la matrice di byte con i dati di flusso richiamando `System.IO.FileStream` dell&#39;oggetto `Read` e passando la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare il `BLOB` oggetto assegnando il relativo `MTOM` con il contenuto della matrice di byte.

1. Impostare le opzioni di runtime per convalidare il documento DDX.

   * Creare un `AssemblerOptionSpec` oggetto che memorizza le opzioni di runtime mediante il relativo costruttore.
   * Impostare l&#39;opzione di runtime che indica al servizio Assembler di convalidare il documento DDX assegnando il valore true al `AssemblerOptionSpec` dell&#39;oggetto `validateOnly` membro dati.
   * Impostare la quantità di informazioni che il servizio Assembler scrive nel file di log assegnando un valore stringa al file `AssemblerOptionSpec` dell&#39;oggetto `logLevel` membro dati. Metodo Durante la convalida di un documento DDX, è necessario inserire nel file di registro ulteriori informazioni utili per il processo di convalida. Puoi quindi specificare il valore `FINE` o `FINER`. Per informazioni sulle opzioni di runtime impostabili, vedere `AssemblerOptionSpec` riferimento di classe in [Riferimento API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. Eseguire la convalida.

   Richiama `AssemblerServiceClient` dell&#39;oggetto `invokeDDX` e trasmettere i seguenti valori:

   * A `BLOB` oggetto che rappresenta il documento DDX.
   * Il valore `null` per `Map` oggetto che in genere memorizza i documenti PDF.
   * Un `AssemblerOptionSpec` oggetto che specifica le opzioni di runtime.

   Il `invokeDDX` il metodo restituisce un `AssemblerResult` oggetto contenente informazioni che specificano se il documento DDX è valido.

1. Salvare i risultati della convalida in un file di registro.

   * Creare un `System.IO.FileStream` richiamando il costruttore e passando un valore stringa che rappresenta la posizione del file di log e la modalità di apertura del file in. Verificare che l&#39;estensione del nome file sia .xml.
   * Creare un `BLOB` oggetto che memorizza le informazioni di registro ottenendo il valore del `AssemblerResult` dell&#39;oggetto `jobLog` membro dati.
   * Creare una matrice di byte che memorizza il contenuto della `BLOB` oggetto. Popolare la matrice di byte ottenendo il valore della `BLOB` dell&#39;oggetto `MTOM` campo.
   * Creare un `System.IO.BinaryWriter` oggetto richiamando il relativo costruttore e passando il `System.IO.FileStream` oggetto.
   * Scrivere il contenuto della matrice di byte in un file PDF richiamando `System.IO.BinaryWriter` dell&#39;oggetto `Write` e passando la matrice di byte.

   >[!NOTE]
   >
   >Se il documento DDX non è valido, `OperationException` viene lanciato. Nell’istruzione catch, puoi ottenere il valore della proprietà `OperationException` dell&#39;oggetto `jobLog` membro.

**Consulta anche**

[Convalida dei documenti DDX](#validating-ddx-documents)

[Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
