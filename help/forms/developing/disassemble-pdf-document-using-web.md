---
title: Smontare un documento PDF utilizzando l'API del servizio Web
seo-title: Smontare un documento PDF utilizzando l'API del servizio Web
description: 'null'
seo-description: 'null'
uuid: d6283dc5-e333-49d0-abde-1d390662f4fe
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/programmatically_disassembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 49584fb4-8c3a-4d73-acd6-0879a67f6093
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Smontare un documento PDF utilizzando l&#39;API del servizio Web {#disassemble-a-pdf-document-usingthe-web-service-api}

Smontare un documento PDF utilizzando l&#39;API Assembler Service (servizio Web):

1. Includere i file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Quando imposti un riferimento a un servizio, accertatevi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituire `localhost` con l&#39;indirizzo IP del server in cui è installato AEM Forms.

1. Creare un client Assembler PDF.

   * Creare un `AssemblerServiceClient` oggetto utilizzando il relativo costruttore predefinito.
   * Creare un `AssemblerServiceClient.Endpoint.Address` oggetto utilizzando il `System.ServiceModel.EndpointAddress` costruttore. Passa un valore di stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). Non è necessario utilizzare l&#39; `lc_version` attributo. Questo attributo viene utilizzato quando create un riferimento a un servizio.
   * Creare un `System.ServiceModel.BasicHttpBinding` oggetto ottenendo il valore del `AssemblerServiceClient.Endpoint.Binding` campo. Inserite il valore restituito in `BasicHttpBinding`.
   * Impostare il campo `System.ServiceModel.BasicHttpBinding` dell&#39; `MessageEncoding` oggetto su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilitate l&#39;autenticazione HTTP di base eseguendo le seguenti operazioni:

      * Assegnare il nome utente dei moduli AEM al campo `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Fare riferimento a un documento DDX esistente.

   * Creare un `BLOB` oggetto utilizzando il relativo costruttore. L&#39; `BLOB` oggetto viene utilizzato per memorizzare il documento DDX.
   * Creare un `System.IO.FileStream` oggetto richiamandone il costruttore. Passa un valore di stringa che rappresenta la posizione del file del documento DDX e la modalità in cui aprire il file.
   * Creare un array di byte che memorizza il contenuto dell&#39; `System.IO.FileStream` oggetto. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà dell&#39; `System.IO.FileStream` oggetto `Length` .
   * Compilare l&#39;array di byte con i dati del flusso richiamando il `System.IO.FileStream` `Read` metodo dell&#39;oggetto e passando l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39; `BLOB` oggetto assegnandone `MTOM` la proprietà con il contenuto dell&#39;array di byte.

1. Fare riferimento a un documento PDF per smontare.

   * Creare un `BLOB` oggetto utilizzando il relativo costruttore. L&#39; `BLOB` oggetto viene utilizzato per memorizzare il documento PDF di input. Questo `BLOB` oggetto viene passato all&#39;oggetto `invokeOneDocument` come argomento.
   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF di input e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto dell&#39; `System.IO.FileStream` oggetto. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà dell&#39; `System.IO.FileStream` oggetto `Length` .
   * Compilare l&#39;array di byte con i dati del flusso richiamando il `System.IO.FileStream` `Read` metodo dell&#39;oggetto e passando l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39; `BLOB` oggetto assegnando al relativo `MTOM` campo il contenuto dell&#39;array di byte.
   * Create a `MyMapOf_xsd_string_To_xsd_anyType` object. Questo oggetto raccolta viene utilizzato per memorizzare il PDF per la scomposizione.
   * Create a `MyMapOf_xsd_string_To_xsd_anyType_Item` object.
   * Assegnare un valore di stringa che rappresenta il nome chiave al campo dell&#39; `MyMapOf_xsd_string_To_xsd_anyType_Item` oggetto `key` . Questo valore deve corrispondere al valore dell&#39;elemento di origine PDF specificato nel documento DDX.
   * Assegnare l&#39; `BLOB` oggetto che memorizza il documento PDF nel campo dell&#39; `MyMapOf_xsd_string_To_xsd_anyType_Item` oggetto `value` .
   * Aggiungere l&#39; `MyMapOf_xsd_string_To_xsd_anyType_Item` oggetto all&#39; `MyMapOf_xsd_string_To_xsd_anyType` oggetto. Richiamare il metodo dell’ `MyMapOf_xsd_string_To_xsd_anyType` oggetto `Add` e passare l’ `MyMapOf_xsd_string_To_xsd_anyType` oggetto.

1. Impostare le opzioni di esecuzione.

   * Creare un `AssemblerOptionSpec` oggetto che memorizza le opzioni di esecuzione utilizzando il relativo costruttore.
   * Impostare le opzioni di runtime per soddisfare i requisiti aziendali assegnando un valore a un membro di dati appartenente all&#39; `AssemblerOptionSpec` oggetto. Ad esempio, per indicare al servizio Assembler di continuare a elaborare un processo in caso di errore, assegnare `false` al campo dell&#39; `AssemblerOptionSpec` oggetto `failOnError` .

1. Smontare il documento PDF.

   Richiama il metodo dell’ `AssemblerServiceClient` oggetto `invokeDDX` e passa i seguenti valori:

   * Un `BLOB` oggetto che rappresenta il documento DDX che smonta il documento PDF
   * L&#39; `MyMapOf_xsd_string_To_xsd_anyType` oggetto che contiene il documento PDF da smontare
   * Un oggetto `AssemblerOptionSpec` che specifica le opzioni di esecuzione
   Il `invokeDDX` metodo restituisce un `AssemblerResult` oggetto che contiene i risultati del processo ed eventuali eccezioni.

1. Salvare i documenti PDF smontati.

   Per ottenere i documenti PDF appena creati, effettuare le seguenti operazioni:

   * Accedere al campo dell&#39; `AssemblerResult` oggetto `documents` , ovvero un `Map` oggetto che contiene i documenti PDF smontati.
   * Eseguire un&#39;iterazione sull&#39; `Map` oggetto per ottenere ogni documento risultante. Quindi, inserite il membro dell&#39;array `value` in un `BLOB`.
   * Estrarre i dati binari che rappresentano il documento PDF accedendo alla `BLOB` proprietà dell&#39; `MTOM` oggetto. Questo restituisce un array di byte che è possibile scrivere in un file PDF.

**Consulta anche**

[Scomposizione programmatica dei documenti PDF](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

[Attivazione di moduli AEM tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
