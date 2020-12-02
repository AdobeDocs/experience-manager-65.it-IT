---
title: Convalida di un documento DDX utilizzando l'API del servizio Web
seo-title: Convalida di un documento DDX utilizzando l'API del servizio Web
description: 'null'
seo-description: 'null'
uuid: f6125746-6138-4e46-a1c4-fb24fd7399c5
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/validating_ddx_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a6fe91ab-3aa0-4b3d-87c0-6cf69a2c4cc4
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 0%

---


# Convalida di un documento DDX utilizzando l&#39;API del servizio Web {#validate-a-ddx-document-using-theweb-service-api}

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

[Convalida di documenti DDX](/help/forms/developing/validating-ddx-documents.md#validating-ddx-documents)

[Chiamata  AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
