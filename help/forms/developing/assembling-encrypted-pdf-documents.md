---
title: Assemblaggio di documenti PDF crittografati
seo-title: Assembling Encrypted PDF Documents
description: Assembla documenti PDF crittografati utilizzando l’API Java e l’API Web Service.
seo-description: Assemble encrypted PDF documents using the Java API and Web Service API.
uuid: d0948ec9-ab67-4fe4-9062-1c4938460b43
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 6d75c7b1-9c0e-47f3-bdb1-61acf16b97f9
role: Developer
exl-id: 2caaca74-640a-4257-a81b-3e8b295cd182
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1659'
ht-degree: 0%

---

# Assemblaggio di documenti PDF crittografati {#assembling-encrypted-pdf-documents}

**Esempi ed esempi in questo documento sono solo per AEM Forms in ambiente JEE.**

È possibile crittografare un documento PDF con una password utilizzando il servizio Assembler. Dopo aver crittografato un documento PDF con una password, è necessario che l’utente specifichi la password per visualizzare il documento PDF in Adobe Reader o Acrobat. Per crittografare un documento PDF con una password, il documento DDX deve contenere i valori degli elementi di crittografia necessari per crittografare un documento PDF.

Ai fini di questa discussione, si supponga che venga utilizzato il seguente documento DDX.

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

In questo documento DDX, notare che all&#39;attributo di origine è assegnato il valore `inDoc`. In situazioni in cui al servizio Assembler viene passato un solo documento PDF di input e viene restituito un documento PDF, e si richiama il `invokeOneDocument` operazione, assegnare il valore `inDoc` all’attributo sorgente di PDF. Quando si richiama il `invokeOneDocument` l&#39;operazione `inDoc` value è una chiave predefinita che deve essere specificata nel documento DDX.

Al contrario, quando trasmetti due o più documenti PDF di input al servizio Assembler, puoi richiamare il `invokeDDX` funzionamento. In questa situazione, assegna il nome file del documento di input PDF al `source` attributo.

Per crittografare un documento PDF con una password, non è necessario che il servizio di cifratura faccia parte dell’installazione dei moduli AEM. Vedi [Crittografia e decrittografia dei documenti PDF](/help/forms/developing/encrypting-decrypting-pdf-documents.md).

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Assembler, vedere [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Per ulteriori informazioni su un documento DDX, consulta [Servizio di assemblaggio e riferimento DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Riepilogo dei passaggi {#summary-of-steps}

Per assemblare un documento PDF crittografato, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Creare un client PDF Assembler.
1. Fai riferimento a un documento DDX esistente.
1. Fare riferimento a un documento PDF non protetto.
1. Impostare le opzioni di esecuzione.
1. Crittografare il documento.
1. Salvare il documento PDF crittografato.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso della classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è distribuito su JBoss)
* jbossall-client.jar (richiesto se AEM Forms è distribuito su JBoss)

se AEM Forms è implementato su un server applicazioni J2EE supportato diverso da JBoss, è necessario sostituire i file adobe-utilities.jar e jbossall-client.jar con file JAR specifici per il server applicazioni J2EE in cui è implementato AEM Forms. Per informazioni sulla posizione di tutti i file JAR di AEM Forms, vedi [Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un client Assembler**

Prima di poter eseguire un&#39;operazione Assembler a livello di programmazione, è necessario creare un client di servizio Assembler.

**Riferimento a un documento DDX esistente**

Per assemblare un documento PDF è necessario fare riferimento a un documento DDX. Ad esempio, considera il documento DDX introdotto in questa sezione. Per crittografare un documento PDF, il documento DDX deve contenere `PasswordEncryptionProfile` elemento.

**Riferimento a un documento PDF non protetto**

Per crittografare un documento PDF non protetto, è necessario fare riferimento a tale documento e passarlo al servizio Assembler. Se si fa riferimento a un documento PDF già crittografato, viene generata un&#39;eccezione.

**Impostare le opzioni di esecuzione**

È possibile impostare le opzioni di esecuzione che controllano il comportamento del servizio Assembler mentre esegue un processo. Ad esempio, è possibile impostare un&#39;opzione che indica al servizio Assembler di continuare l&#39;elaborazione di un processo in caso di errore. Per informazioni sulle opzioni di esecuzione che è possibile impostare, vedere la `AssemblerOptionSpec` riferimento di classe in [Riferimento API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Crittografare il documento**

Dopo aver creato il client del servizio Assembler, fare riferimento al documento DDX contenente informazioni sulla crittografia, fare riferimento a un documento PDF non protetto e impostare le opzioni di esecuzione, è possibile richiamare il `invokeOneDocument` funzionamento. Poiché al servizio Assembler viene passato un solo documento di input PDF (e viene restituito un documento), è possibile utilizzare il `invokeOneDocument` al posto del `invokeDDX` funzionamento.

**Salvare il documento PDF crittografato**

Se al servizio Assembler viene passato un solo documento PDF, il servizio Assembler restituisce un singolo documento invece di un oggetto raccolta. In altre parole, quando si richiama il `invokeOneDocument` viene restituito un singolo documento. Poiché il documento DDX a cui si fa riferimento in questa sezione contiene informazioni sulla crittografia, il servizio Assembler restituisce un documento PDF crittografato con una password.

**Consulta anche**

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Assemblaggio di documenti PDF a livello di programmazione](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Assemblare un documento PDF crittografato utilizzando l’API Java {#assemble-an-encrypted-pdf-document-using-the-java-api}

1. Includi file di progetto.

   Includi file JAR client, come adobe-assembler-client.jar, nel percorso di classe del progetto Java.

1. Creare un client Assembler.

   * Crea un `ServiceClientFactory` oggetto contenente le proprietà di connessione.
   * Crea un `AssemblerServiceClient` utilizzando il relativo costruttore e passando `ServiceClientFactory` oggetto.

1. Fai riferimento a un documento DDX esistente.

   * Crea un `java.io.FileInputStream` oggetto che rappresenta il documento DDX utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del file DDX.
   * Crea un `com.adobe.idp.Document` utilizzando il relativo costruttore e passando `java.io.FileInputStream` oggetto.

1. Fare riferimento a un documento PDF non protetto.

   * Crea un `java.io.FileInputStream` utilizzando il relativo costruttore e passando la posizione di un documento PDF non protetto.
   * Crea un `com.adobe.idp.Document` e passare `java.io.FileInputStream` oggetto contenente il documento PDF. Questo `com.adobe.idp.Document` viene passato all&#39;oggetto `invokeOneDocument` metodo .

1. Impostare le opzioni di esecuzione.

   * Crea un `AssemblerOptionSpec` oggetto che memorizza le opzioni di esecuzione utilizzando il relativo costruttore.
   * Impostare le opzioni di esecuzione per soddisfare i requisiti aziendali richiamando un metodo che appartiene al `AssemblerOptionSpec` oggetto. Ad esempio, per dare istruzioni al servizio Assembler di continuare a elaborare un processo quando si verifica un errore, richiama il `AssemblerOptionSpec` dell’oggetto `setFailOnError` metodo e passaggio `false`.

1. Crittografare il documento.

   Richiama il `AssemblerServiceClient` dell’oggetto `invokeOneDocument` e passare i seguenti valori:

   * A `com.adobe.idp.Document` oggetto che rappresenta il documento DDX. Assicurati che questo documento DDX contenga il valore `inDoc` per l’elemento sorgente PDF.
   * A `com.adobe.idp.Document` oggetto contenente il documento PDF non protetto.
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` oggetto che specifica le opzioni di esecuzione, incluso il livello di carattere predefinito e di registro dei processi.

   La `invokeOneDocument` restituisce un `com.adobe.idp.Document` oggetto contenente un documento PDF crittografato con password.

1. Salvare il documento PDF crittografato.

   * Crea un `java.io.File` e assicurati che l&#39;estensione del nome del file sia .pdf.
   * Richiama il `Document` dell’oggetto `copyToFile` per copiare il contenuto del `Document` al file. Assicurati di utilizzare `Document` oggetto che `invokeOneDocument` metodo restituito.

**Consulta anche**

[Avvio rapido (modalità SOAP): Assemblaggio di un documento PDF crittografato utilizzando l’API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-an-encrypted-pdf-document-using-the-java-api)

## Assemblare un documento PDF crittografato utilizzando l’API del servizio Web {#assemble-an-encrypted-pdf-document-using-the-web-service-api}

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Quando imposti un riferimento a un servizio, assicurati di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l’indirizzo IP del server che ospita AEM Forms.

1. Creare un client Assembler.

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

1. Fare riferimento a un documento PDF non protetto.

   * Crea un `BLOB` utilizzando il relativo costruttore. La `BLOB` viene utilizzato per memorizzare il documento di input PDF. Questo `BLOB` viene passato all&#39;oggetto `invokeOneDocument` come argomento.
   * Crea un `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento di input PDF e la modalità in cui aprire il file.
   * Creare un array di byte che memorizza il contenuto del `System.IO.FileStream` oggetto. È possibile determinare le dimensioni dell&#39;array di byte ottenendo il `System.IO.FileStream` dell’oggetto `Length` proprietà.
   * Compilare l&#39;array di byte con i dati del flusso richiamando il `System.IO.FileStream` dell’oggetto `Read` e passare l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare `BLOB` oggetto assegnando il relativo `MTOM` con il contenuto dell&#39;array di byte.

1. Impostare le opzioni di esecuzione.

   * Crea un `AssemblerOptionSpec` oggetto che memorizza le opzioni di esecuzione utilizzando il relativo costruttore.
   * Impostare le opzioni di esecuzione per soddisfare i requisiti aziendali assegnando un valore a un membro dati che appartiene al `AssemblerOptionSpec` oggetto. Ad esempio, per dare istruzioni al servizio Assembler di continuare a elaborare un processo quando si verifica un errore, assegnare `false` al `AssemblerOptionSpec` dell’oggetto `failOnError` membro dati.

1. Crittografare il documento.

   Richiama il `AssemblerServiceClient` dell’oggetto `invokeOneDocument` e passare i seguenti valori:

   * A `BLOB` oggetto che rappresenta il documento DDX
   * A `BLOB` oggetto che rappresenta il documento PDF non protetto
   * Un `AssemblerOptionSpec` oggetto che specifica le opzioni di esecuzione

   La `invokeOneDocument` restituisce un `BLOB` oggetto contenente un documento PDF crittografato.

1. Salvare il documento PDF crittografato.

   * Crea un `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF crittografato e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto del `BLOB` oggetto che `invokeOneDocument` metodo restituito. Compilare l’array di byte ottenendo il valore del `BLOB` dell’oggetto `MTOM` membro dati.
   * Crea un `System.IO.BinaryWriter` richiamando il relativo costruttore e passando `System.IO.FileStream` oggetto.
   * Scrivi il contenuto dell’array di byte in un file PDF richiamando il `System.IO.BinaryWriter` dell’oggetto `Write` e passare l&#39;array di byte.

**Consulta anche**

[Richiamo di AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
