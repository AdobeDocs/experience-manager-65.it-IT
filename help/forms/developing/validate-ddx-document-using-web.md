---
title: Convalidare un documento DDX utilizzando l’API del servizio web
description: Utilizza l’API del servizio Assembler per convalidare un documento DDX.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/validating_ddx_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
role: Developer
exl-id: 069e5b10-ab93-4492-a70d-6a0d462105a6
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 0%

---

# Convalidare un documento DDX utilizzando l’API del servizio web {#validate-a-ddx-document-using-theweb-service-api}

**Gli esempi e gli esempi contenuti in questo documento sono solo per l’ambiente AEM Forms su JEE.**

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

[Convalida dei documenti DDX](/help/forms/developing/validating-ddx-documents.md#validating-ddx-documents)

[Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
