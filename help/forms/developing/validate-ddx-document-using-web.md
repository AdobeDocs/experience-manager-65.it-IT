---
title: Convalidare un documento DDX utilizzando l’API del servizio Web
seo-title: Convalidare un documento DDX utilizzando l’API del servizio Web
description: Utilizzare l'API del servizio Assembler per convalidare un documento DDX.
seo-description: Utilizzare l'API del servizio Assembler per convalidare un documento DDX.
uuid: f6125746-6138-4e46-a1c4-fb24fd7399c5
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/validating_ddx_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a6fe91ab-3aa0-4b3d-87c0-6cf69a2c4cc4
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 0%

---


# Convalida un documento DDX utilizzando l&#39;API del servizio Web {#validate-a-ddx-document-using-theweb-service-api}

**Esempi ed esempi in questo documento sono solo per AEM Forms in ambiente JEE.**

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

[Convalida dei documenti DDX](/help/forms/developing/validating-ddx-documents.md#validating-ddx-documents)

[Richiamo di AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
