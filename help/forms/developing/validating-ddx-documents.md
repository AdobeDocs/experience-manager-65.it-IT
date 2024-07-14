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

**Gli esempi e gli esempi contenuti in questo documento sono solo per AEM Forms in ambiente JEE.**

È possibile convalidare a livello di programmazione un documento DDX utilizzato dal servizio Assembler. In altre parole, utilizzando l&#39;API del servizio Assembler, è possibile determinare se un documento DDX è valido o meno. Se ad esempio si è eseguito l&#39;aggiornamento da una versione precedente di AEM Forms e si desidera verificare che il documento DDX sia valido, è possibile convalidarlo utilizzando l&#39;API del servizio Assembler.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Assembler, vedere [Riferimento ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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

**Creare un client Assembler PDF**

Prima di poter eseguire un&#39;operazione Assembler a livello di programmazione, è necessario creare un client del servizio Assembler.

**Riferimento a un documento DDX esistente**

Per convalidare un documento DDX, è necessario fare riferimento a un documento DDX esistente.

**Impostare le opzioni di runtime per convalidare il documento DDX**

Durante la convalida di un documento DDX, è necessario impostare opzioni di runtime specifiche che indichino al servizio Assembler di convalidare il documento DDX anziché eseguirlo. È inoltre possibile aumentare la quantità di informazioni che il servizio Assembler scrive nel file di registro.

**Esegui la convalida**

Dopo aver creato il client del servizio Assembler, aver fatto riferimento al documento DDX e aver impostato le opzioni di runtime, è possibile richiamare l&#39;operazione `invokeDDX` per convalidare il documento DDX. Durante la convalida del documento DDX, è possibile passare `null` come parametro di mappa (questo parametro in genere memorizza i documenti PDF necessari all&#39;Assembler per eseguire le operazioni specificate nel documento DDX).

Se la convalida non riesce, viene generata un&#39;eccezione e il file di log contiene dettagli che spiegano perché il documento DDX non è valido. È possibile ottenerlo dall&#39;istanza `OperationException`. Dopo aver superato l&#39;analisi XML di base e il controllo dello schema, viene eseguita la convalida in base alla specifica DDX. Tutti gli errori presenti nel documento DDX vengono specificati nel registro.

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

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `AssemblerServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Fare riferimento a un documento DDX esistente.

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento DDX utilizzando il relativo costruttore e passando un valore stringa che specifica la posizione del file DDX.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Impostare le opzioni di runtime per convalidare il documento DDX.

   * Creare un oggetto `AssemblerOptionSpec` che memorizza le opzioni di runtime utilizzando il relativo costruttore.
   * Impostare l&#39;opzione di runtime che indica al servizio Assembler di convalidare il documento DDX richiamando il metodo setValidateOnly dell&#39;oggetto `AssemblerOptionSpec` e passando `true`.
   * Impostare la quantità di informazioni che il servizio Assembler scrive nel file di log richiamando il metodo `getLogLevel` dell&#39;oggetto `AssemblerOptionSpec` e fornendo un valore stringa che soddisfi i requisiti. Durante la convalida di un documento DDX, è necessario disporre di ulteriori informazioni scritte nel file di registro che possano essere utili per il processo di convalida. È quindi possibile passare il valore `FINE` o `FINER`.

1. Eseguire la convalida.

   Richiama il metodo `invokeDDX` dell&#39;oggetto `AssemblerServiceClient` e passa i seguenti valori:

   * Oggetto `com.adobe.idp.Document` che rappresenta il documento DDX.
   * Valore `null` per l&#39;oggetto java.io.Map che in genere memorizza i documenti PDF.
   * Oggetto `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` che specifica le opzioni di runtime.

   Il metodo `invokeDDX` restituisce un oggetto `AssemblerResult` che contiene informazioni che specificano se il documento DDX è valido.

1. Salvare i risultati della convalida in un file di registro.

   * Creare un oggetto `java.io.File` e verificare che l&#39;estensione del nome file sia .xml.
   * Richiama il metodo `getJobLog` dell&#39;oggetto `AssemblerResult`. Questo metodo restituisce un&#39;istanza `com.adobe.idp.Document` che contiene informazioni di convalida.
   * Richiama il metodo `copyToFile` dell&#39;oggetto `com.adobe.idp.Document` per copiare il contenuto dell&#39;oggetto `com.adobe.idp.Document` nel file.

   >[!NOTE]
   >
   >Se il documento DDX non è valido, viene generato un `OperationException`. Nell&#39;istruzione catch è possibile richiamare il metodo `getJobLog` dell&#39;oggetto `OperationException`.

**Consulta anche**

[Convalida dei documenti DDX](#validating-ddx-documents)

[Guida rapida (modalità SOAP): convalida dei documenti DDX tramite l&#39;API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-validating-ddx-documents-using-the-java-api) (modalità SOAP)

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

   * Creare un oggetto `AssemblerServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `AssemblerServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). Non è necessario utilizzare l&#39;attributo `lc_version`. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `AssemblerServiceClient.Endpoint.Binding`. Eseguire il cast del valore restituito in `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegnare il nome utente dei moduli AEM al campo `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Fare riferimento a un documento DDX esistente.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per archiviare il documento DDX.
   * Creare un oggetto `System.IO.FileStream` richiamandone il costruttore e passando un valore stringa che rappresenta la posizione del file del documento DDX e la modalità di apertura del file in.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni della matrice di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare la matrice di byte con i dati di flusso richiamando il metodo `Read` dell&#39;oggetto `System.IO.FileStream` e passando la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando la relativa proprietà `MTOM` al contenuto della matrice di byte.

1. Impostare le opzioni di runtime per convalidare il documento DDX.

   * Creare un oggetto `AssemblerOptionSpec` che memorizza le opzioni di runtime utilizzando il relativo costruttore.
   * Impostare l&#39;opzione di runtime che indica al servizio Assembler di convalidare il documento DDX assegnando il valore true al membro dati `validateOnly` dell&#39;oggetto `AssemblerOptionSpec`.
   * Impostare la quantità di informazioni che il servizio Assembler scrive nel file di log assegnando un valore stringa al membro dati `logLevel` dell&#39;oggetto `AssemblerOptionSpec`. Metodo Durante la convalida di un documento DDX, è necessario inserire nel file di registro ulteriori informazioni utili per il processo di convalida. È quindi possibile specificare il valore `FINE` o `FINER`. Per informazioni sulle opzioni di runtime che è possibile impostare, vedere il riferimento alla classe `AssemblerOptionSpec` in [Riferimento API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. Eseguire la convalida.

   Richiama il metodo `invokeDDX` dell&#39;oggetto `AssemblerServiceClient` e passa i seguenti valori:

   * Oggetto `BLOB` che rappresenta il documento DDX.
   * Valore `null` per l&#39;oggetto `Map` che in genere memorizza i documenti PDF.
   * Oggetto `AssemblerOptionSpec` che specifica le opzioni di runtime.

   Il metodo `invokeDDX` restituisce un oggetto `AssemblerResult` che contiene informazioni che specificano se il documento DDX è valido.

1. Salvare i risultati della convalida in un file di registro.

   * Creare un oggetto `System.IO.FileStream` richiamandone il costruttore e passando un valore stringa che rappresenta la posizione del file di log e la modalità di apertura del file in. Verificare che l&#39;estensione del nome file sia .xml.
   * Creare un oggetto `BLOB` che memorizza le informazioni di registro ottenendo il valore del membro dati `jobLog` dell&#39;oggetto `AssemblerResult`.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `BLOB`. Compilare la matrice di byte ottenendo il valore del campo `MTOM` dell&#39;oggetto `BLOB`.
   * Creare un oggetto `System.IO.BinaryWriter` richiamandone il costruttore e passando l&#39;oggetto `System.IO.FileStream`.
   * Scrivere il contenuto della matrice di byte in un file PDF richiamando il metodo `Write` dell&#39;oggetto `System.IO.BinaryWriter` e passando la matrice di byte.

   >[!NOTE]
   >
   >Se il documento DDX non è valido, viene generato un `OperationException`. Nell&#39;istruzione catch è possibile ottenere il valore del membro `jobLog` dell&#39;oggetto `OperationException`.

**Consulta anche**

[Convalida dei documenti DDX](#validating-ddx-documents)

[Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
