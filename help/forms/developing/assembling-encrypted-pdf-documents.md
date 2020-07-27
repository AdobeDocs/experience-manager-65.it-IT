---
title: Assemblaggio di documenti PDF crittografati
seo-title: Assemblaggio di documenti PDF crittografati
description: 'null'
seo-description: 'null'
uuid: d0948ec9-ab67-4fe4-9062-1c4938460b43
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 6d75c7b1-9c0e-47f3-bdb1-61acf16b97f9
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '1639'
ht-degree: 0%

---


# Assemblaggio di documenti PDF crittografati {#assembling-encrypted-pdf-documents}

È possibile cifrare un documento PDF con una password utilizzando il servizio Assembler. Dopo aver crittografato un documento PDF con una password, l&#39;utente deve specificarla per visualizzare il documento PDF in Adobe Reader o Acrobat. Per cifrare un documento PDF con una password, il documento DDX deve contenere i valori degli elementi di cifratura necessari per la cifratura di un documento PDF.

Ai fini di questa discussione, si supponga di utilizzare il seguente documento DDX.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
        <PDF result="EncryptLoan.pdf" encryption="userProtect">
         <PDF source="inDoc" />
     </PDF>
     <PasswordEncryptionProfile name="userProtect" compatibilityLevel="Acrobat7">
         <OpenPassword>AdobeOpen</OpenPassword>
        </PasswordEncryptionProfile>
 </DDX>
```

In questo documento DDX, si noti che all&#39;attributo di origine è assegnato il valore `inDoc`. In situazioni in cui viene passato un solo documento PDF di input al servizio Assembler e viene restituito un documento PDF e si esegue l&#39; `invokeOneDocument` operazione, assegnare il valore `inDoc` all&#39;attributo di origine PDF. Quando si richiama l&#39; `invokeOneDocument` operazione, il `inDoc` valore è una chiave predefinita che deve essere specificata nel documento DDX.

Al contrario, quando si passano due o più documenti PDF di input al servizio Assembler, è possibile richiamare l&#39; `invokeDDX` operazione. In questa situazione, assegnare all&#39; `source` attributo il nome del file del documento PDF di input.

Il servizio di cifratura non deve necessariamente far parte dell’installazione di moduli AEM per cifrare un documento PDF con una password. Vedere [Cifratura e decrittografia di documenti](/help/forms/developing/encrypting-decrypting-pdf-documents.md)PDF.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Assembler, vedere Riferimento [servizi per i AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Per ulteriori informazioni su un documento DDX, vedere Servizio [Assembler e Riferimento](https://www.adobe.com/go/learn_aemforms_ddx_63)DDX.

## Riepilogo dei passaggi {#summary-of-steps}

Per assemblare un documento PDF crittografato, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un client Assembler PDF.
1. Fare riferimento a un documento DDX esistente.
1. Fare riferimento a un documento PDF non protetto.
1. Impostare le opzioni di esecuzione.
1. Cifra il documento.
1. Salvare il documento PDF crittografato.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, accertatevi di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (richiesto se i AEM Forms sono distribuiti su JBoss)
* jbossall-client.jar (richiesto se i AEM Forms sono distribuiti su JBoss)

se i AEM Forms sono distribuiti su un server applicazione J2EE supportato diverso da JBoss, è necessario sostituire i file adobe-utilities.jar e jbossall-client.jar con file JAR specifici del server applicazione J2EE in cui sono distribuiti i AEM Forms. Per informazioni sulla posizione di tutti i file JAR AEM Forms, vedere [Inclusione di file](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)libreria Java AEM Forms.

**Creare un client Assembler**

Prima di eseguire un&#39;operazione Assembler a livello di programmazione, è necessario creare un client di servizio Assembler.

**Riferimento a un documento DDX esistente**

Per assemblare un documento PDF è necessario fare riferimento a un documento DDX. Si consideri, ad esempio, il documento DDX introdotto in questa sezione. Per cifrare un documento PDF, il documento DDX deve contenere l&#39; `PasswordEncryptionProfile` elemento .

**Riferimento a un documento PDF non protetto**

Per cifrare un documento PDF non protetto è necessario fare riferimento a tale documento e passarlo al servizio Assembler. Se si fa riferimento a un documento PDF già crittografato, viene generata un&#39;eccezione.

**Impostazione delle opzioni di esecuzione**

È possibile impostare opzioni di esecuzione che controllano il comportamento del servizio Assembler mentre esegue un processo. Ad esempio, potete impostare un&#39;opzione che indichi al servizio Assembler di continuare l&#39;elaborazione di un processo in caso di errore. Per informazioni sulle opzioni di esecuzione che è possibile impostare, vedere il riferimento alla `AssemblerOptionSpec` classe in Riferimento API per [AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Crittografare il documento**

Dopo aver creato il client del servizio Assembler, fare riferimento al documento DDX che contiene informazioni di cifratura, fare riferimento a un documento PDF non protetto e impostare le opzioni di esecuzione, è possibile richiamare l&#39; `invokeOneDocument` operazione. Poiché al servizio Assembler viene passato un solo documento PDF di input (e viene restituito un documento), è possibile utilizzare l&#39; `invokeOneDocument` operazione invece dell&#39; `invokeDDX` operazione.

**Salvare il documento PDF crittografato**

Se al servizio Assembler viene passato un solo documento PDF, il servizio Assembler restituisce un singolo documento invece di un oggetto raccolta. In altre parole, quando si richiama l&#39; `invokeOneDocument` operazione, viene restituito un singolo documento. Poiché il documento DDX a cui si fa riferimento in questa sezione contiene informazioni di cifratura, il servizio Assembler restituisce un documento PDF crittografato con una password.

**Consulta anche**

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Assemblaggio di documenti PDF a livello di programmazione](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Assemblare un documento PDF crittografato utilizzando l&#39;API Java {#assemble-an-encrypted-pdf-document-using-the-java-api}

1. Includere i file di progetto.

   Includete file JAR client, ad esempio adobe-assembler-client.jar, nel percorso di classe del progetto Java.

1. Creare un client Assembler.

   * Creare un `ServiceClientFactory` oggetto che contenga proprietà di connessione.
   * Creare un `AssemblerServiceClient` oggetto utilizzando il relativo costruttore e passando l&#39; `ServiceClientFactory` oggetto.

1. Fare riferimento a un documento DDX esistente.

   * Creare un `java.io.FileInputStream` oggetto che rappresenta il documento DDX utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del file DDX.
   * Creare un `com.adobe.idp.Document` oggetto utilizzando il relativo costruttore e passando l&#39; `java.io.FileInputStream` oggetto.

1. Fare riferimento a un documento PDF non protetto.

   * Creare un `java.io.FileInputStream` oggetto utilizzando il relativo costruttore e passando la posizione di un documento PDF non protetto.
   * Creare un `com.adobe.idp.Document` oggetto e passare l&#39; `java.io.FileInputStream` oggetto che contiene il documento PDF. Questo `com.adobe.idp.Document` oggetto viene passato al `invokeOneDocument` metodo.

1. Impostare le opzioni di esecuzione.

   * Creare un `AssemblerOptionSpec` oggetto che memorizza le opzioni di esecuzione utilizzando il relativo costruttore.
   * Impostate le opzioni di runtime per soddisfare i requisiti aziendali richiamando un metodo che appartiene all&#39; `AssemblerOptionSpec` oggetto. Ad esempio, per indicare al servizio Assembler di continuare a elaborare un processo quando si verifica un errore, richiamare il metodo dell&#39; `AssemblerOptionSpec` oggetto `setFailOnError` e passare `false`.

1. Cifra il documento.

   Richiama il metodo dell’ `AssemblerServiceClient` oggetto `invokeOneDocument` e passa i seguenti valori:

   * Un `com.adobe.idp.Document` oggetto che rappresenta il documento DDX. Assicurarsi che il documento DDX contenga il valore `inDoc` per l&#39;elemento di origine PDF.
   * Un `com.adobe.idp.Document` oggetto che contiene il documento PDF non protetto.
   * Un `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` oggetto che specifica le opzioni di esecuzione, incluso il livello predefinito del font e del registro dei processi.

   Il `invokeOneDocument` metodo restituisce un `com.adobe.idp.Document` oggetto che contiene un documento PDF crittografato con password.

1. Salvare il documento PDF crittografato.

   * Create un `java.io.File` oggetto e accertatevi che l&#39;estensione del nome del file sia .pdf.
   * Richiamare il metodo dell&#39; `Document` oggetto `copyToFile` per copiare il contenuto dell&#39; `Document` oggetto nel file. Assicurarsi di utilizzare l&#39; `Document` oggetto restituito dal `invokeOneDocument` metodo.

**Consulta anche**

[Avvio rapido (modalità SOAP): Assemblaggio di un documento PDF crittografato tramite l&#39;API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-an-encrypted-pdf-document-using-the-java-api)

## Assemblare un documento PDF crittografato utilizzando l&#39;API del servizio Web {#assemble-an-encrypted-pdf-document-using-the-web-service-api}

1. Includere i file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Quando imposti un riferimento a un servizio, accertatevi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituire `localhost` con l&#39;indirizzo IP del server host AEM Forms.

1. Creare un client Assembler.

   * Creare un `AssemblerServiceClient` oggetto utilizzando il relativo costruttore predefinito.
   * Creare un `AssemblerServiceClient.Endpoint.Address` oggetto utilizzando il `System.ServiceModel.EndpointAddress` costruttore. Passate un valore di stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). Non è necessario utilizzare l&#39; `lc_version` attributo. Questo attributo viene utilizzato quando create un riferimento a un servizio.
   * Creare un `System.ServiceModel.BasicHttpBinding` oggetto ottenendo il valore del `AssemblerServiceClient.Endpoint.Binding` campo. Inserite il valore restituito in `BasicHttpBinding`.
   * Impostare il campo `System.ServiceModel.BasicHttpBinding` dell&#39; `MessageEncoding` oggetto su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilitate l&#39;autenticazione HTTP di base eseguendo le seguenti operazioni:

      * Assegnare il nome utente dei moduli AEM al campo `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Fare riferimento a un documento DDX esistente.

   * Creare un `BLOB` oggetto utilizzando il relativo costruttore. L&#39; `BLOB` oggetto viene utilizzato per memorizzare il documento DDX.
   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento DDX e la modalità in cui aprire il file.
   * Creare un array di byte che memorizza il contenuto dell&#39; `System.IO.FileStream` oggetto. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà dell&#39; `System.IO.FileStream` oggetto `Length` .
   * Compilare l&#39;array di byte con i dati del flusso richiamando il `System.IO.FileStream` `Read` metodo dell&#39;oggetto e passando l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39; `BLOB` oggetto assegnandone `MTOM` il campo con il contenuto dell&#39;array di byte.

1. Fare riferimento a un documento PDF non protetto.

   * Creare un `BLOB` oggetto utilizzando il relativo costruttore. L&#39; `BLOB` oggetto viene utilizzato per memorizzare il documento PDF di input. Questo `BLOB` oggetto viene passato all&#39;oggetto `invokeOneDocument` come argomento.
   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF di input e la modalità in cui aprire il file.
   * Creare un array di byte che memorizza il contenuto dell&#39; `System.IO.FileStream` oggetto. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà dell&#39; `System.IO.FileStream` oggetto `Length` .
   * Compilare l&#39;array di byte con i dati del flusso richiamando il `System.IO.FileStream` `Read` metodo dell&#39;oggetto e passando l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39; `BLOB` oggetto assegnandone `MTOM` il campo con il contenuto dell&#39;array di byte.

1. Impostare le opzioni di esecuzione.

   * Creare un `AssemblerOptionSpec` oggetto che memorizza le opzioni di esecuzione utilizzando il relativo costruttore.
   * Impostare le opzioni di runtime per soddisfare i requisiti aziendali assegnando un valore a un membro di dati che appartiene all&#39; `AssemblerOptionSpec` oggetto. Ad esempio, per indicare al servizio Assembler di continuare l&#39;elaborazione di un processo in caso di errore, assegnare `false` al membro `AssemblerOptionSpec` dati dell&#39; `failOnError` oggetto.

1. Cifra il documento.

   Richiama il metodo dell’ `AssemblerServiceClient` oggetto `invokeOneDocument` e passa i seguenti valori:

   * Un `BLOB` oggetto che rappresenta il documento DDX
   * Un `BLOB` oggetto che rappresenta il documento PDF non protetto
   * Un oggetto `AssemblerOptionSpec` che specifica le opzioni di esecuzione

   Il `invokeOneDocument` metodo restituisce un `BLOB` oggetto che contiene un documento PDF crittografato.

1. Salvare il documento PDF crittografato.

   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF crittografato e la modalità in cui aprire il file.
   * Creare un array di byte che memorizza il contenuto dell&#39; `BLOB` oggetto restituito dal `invokeOneDocument` metodo. Compilare l&#39;array di byte ottenendo il valore del membro `BLOB` dati dell&#39; `MTOM` oggetto.
   * Creare un `System.IO.BinaryWriter` oggetto richiamando il relativo costruttore e passando l&#39; `System.IO.FileStream` oggetto.
   * Scrivere il contenuto dell&#39;array di byte in un file PDF richiamando il metodo dell&#39; `System.IO.BinaryWriter` oggetto `Write` e passando l&#39;array di byte.

**Consulta anche**

[Chiamata di AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
