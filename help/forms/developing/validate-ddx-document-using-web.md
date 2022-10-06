---
title: Convalidare un documento DDX utilizzando l’API del servizio Web
seo-title: Validate a DDX document using theweb service API
description: Utilizzare l'API del servizio Assembler per convalidare un documento DDX.
seo-description: Use the Assembler Service API to validate a DDX document.
uuid: f6125746-6138-4e46-a1c4-fb24fd7399c5
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/validating_ddx_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a6fe91ab-3aa0-4b3d-87c0-6cf69a2c4cc4
role: Developer
exl-id: 069e5b10-ab93-4492-a70d-6a0d462105a6
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 0%

---

# Convalidare un documento DDX utilizzando l’API del servizio Web {#validate-a-ddx-document-using-theweb-service-api}

**Esempi ed esempi in questo documento sono solo per AEM Forms in ambiente JEE.**

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

[Convalida dei documenti DDX](/help/forms/developing/validating-ddx-documents.md#validating-ddx-documents)

[Richiamo di AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
