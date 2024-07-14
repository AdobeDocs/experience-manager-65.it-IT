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
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 0%

---

# Convalidare un documento DDX utilizzando l’API del servizio web {#validate-a-ddx-document-using-theweb-service-api}

**Gli esempi e gli esempi contenuti in questo documento sono solo per AEM Forms in ambiente JEE.**

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

[Convalida dei documenti DDX](/help/forms/developing/validating-ddx-documents.md#validating-ddx-documents)

[Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
