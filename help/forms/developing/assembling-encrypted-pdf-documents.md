---
title: Assemblaggio di documenti PDF crittografati
seo-title: Assemblaggio di documenti PDF crittografati
description: Assemblate documenti PDF crittografati utilizzando l'API Java e l'API del servizio Web.
seo-description: Assemblate documenti PDF crittografati utilizzando l'API Java e l'API del servizio Web.
uuid: d0948ec9-ab67-4fe4-9062-1c4938460b43
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 6d75c7b1-9c0e-47f3-bdb1-61acf16b97f9
translation-type: tm+mt
source-git-commit: 07889ead2ae402b5fb738ca08c7efe076ef33e44
workflow-type: tm+mt
source-wordcount: '1661'
ht-degree: 0%

---


# Assemblaggio di documenti PDF crittografati {#assembling-encrypted-pdf-documents}

È possibile cifrare un documento PDF con una password utilizzando il servizio Assembler. Dopo aver crittografato un documento PDF con una password, l&#39;utente deve specificare la password per visualizzare il documento PDF in  Adobe Reader o  Acrobat. Per cifrare un documento PDF con una password, il documento DDX deve contenere i valori degli elementi di cifratura necessari per la cifratura di un documento PDF.

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

In questo documento DDX, si noti che all&#39;attributo di origine è assegnato il valore `inDoc`. In situazioni in cui viene passato un solo documento PDF di input al servizio Assembler e viene restituito un documento PDF, e si esegue l&#39;operazione `invokeOneDocument`, assegnare il valore `inDoc` all&#39;attributo di origine PDF. Quando si richiama l&#39;operazione `invokeOneDocument`, il valore `inDoc` è una chiave predefinita che deve essere specificata nel documento DDX.

Al contrario, quando si passano due o più documenti PDF di input al servizio Assembler, è possibile richiamare l&#39;operazione `invokeDDX`. In questa situazione, assegnare il nome del file del documento PDF di input all&#39;attributo `source`.

Il servizio di cifratura non deve necessariamente far parte dell&#39;installazione dei moduli AEM per cifrare un documento PDF con una password. Vedere [Cifratura e decrittografia di documenti PDF](/help/forms/developing/encrypting-decrypting-pdf-documents.md).

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Assembler, vedere [Guida di riferimento dei servizi per  AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Per ulteriori informazioni su un documento DDX, vedere [Servizio Assembler e Riferimento DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

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
* adobe-utilities.jar (richiesto se  AEM Forms è distribuito su JBoss)
* jbossall-client.jar (richiesto se  AEM Forms è distribuito su JBoss)

se  AEM Forms è distribuito su un server applicazione J2EE supportato diverso da JBoss, è necessario sostituire i file adobe-utilities.jar e jbossall-client.jar con file JAR specifici del server applicazione J2EE in cui  AEM Forms è distribuito. Per informazioni sulla posizione di tutti  file AEM Forms JAR, vedere [Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un client Assembler**

Prima di eseguire un&#39;operazione Assembler a livello di programmazione, è necessario creare un client di servizio Assembler.

**Riferimento a un documento DDX esistente**

Per assemblare un documento PDF è necessario fare riferimento a un documento DDX. Si consideri, ad esempio, il documento DDX introdotto in questa sezione. Per cifrare un documento PDF, il documento DDX deve contenere l&#39;elemento `PasswordEncryptionProfile`.

**Riferimento a un documento PDF non protetto**

Per cifrare un documento PDF non protetto è necessario fare riferimento a tale documento e passarlo al servizio Assembler. Se si fa riferimento a un documento PDF già crittografato, viene generata un&#39;eccezione.

**Impostazione delle opzioni di esecuzione**

È possibile impostare opzioni di esecuzione che controllano il comportamento del servizio Assembler mentre esegue un processo. Ad esempio, potete impostare un&#39;opzione che indichi al servizio Assembler di continuare l&#39;elaborazione di un processo in caso di errore. Per informazioni sulle opzioni di esecuzione che è possibile impostare, vedere il riferimento alla classe `AssemblerOptionSpec` in [ Guida di riferimento delle API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Crittografare il documento**

Dopo aver creato il client del servizio Assembler, fare riferimento al documento DDX che contiene informazioni di cifratura, fare riferimento a un documento PDF non protetto e impostare le opzioni di esecuzione, è possibile richiamare l&#39;operazione `invokeOneDocument`. Poiché al servizio Assembler viene passato un solo documento PDF di input (e viene restituito un documento), è possibile utilizzare l&#39;operazione `invokeOneDocument` invece dell&#39;operazione `invokeDDX`.

**Salvare il documento PDF crittografato**

Se al servizio Assembler viene passato un solo documento PDF, il servizio Assembler restituisce un singolo documento invece di un oggetto raccolta. Ovvero, quando si richiama l&#39;operazione `invokeOneDocument`, viene restituito un singolo documento. Poiché il documento DDX a cui si fa riferimento in questa sezione contiene informazioni di cifratura, il servizio Assembler restituisce un documento PDF crittografato con una password.

**Consulta anche**

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Assemblaggio di documenti PDF a livello di programmazione](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Assemblare un documento PDF crittografato utilizzando l&#39;API Java {#assemble-an-encrypted-pdf-document-using-the-java-api}

1. Includere i file di progetto.

   Includete file JAR client, ad esempio adobe-assembler-client.jar, nel percorso di classe del progetto Java.

1. Creare un client Assembler.

   * Creare un oggetto `ServiceClientFactory` che contiene le proprietà di connessione.
   * Creare un oggetto `AssemblerServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Fare riferimento a un documento DDX esistente.

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento DDX utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del file DDX.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Fare riferimento a un documento PDF non protetto.

   * Creare un oggetto `java.io.FileInputStream` utilizzando il relativo costruttore e passando la posizione di un documento PDF non protetto.
   * Creare un oggetto `com.adobe.idp.Document` e passare l&#39;oggetto `java.io.FileInputStream` che contiene il documento PDF. Questo oggetto `com.adobe.idp.Document` viene passato al metodo `invokeOneDocument`.

1. Impostare le opzioni di esecuzione.

   * Creare un oggetto `AssemblerOptionSpec` che memorizza le opzioni di esecuzione utilizzando il relativo costruttore.
   * Impostate le opzioni di runtime per soddisfare i requisiti aziendali richiamando un metodo che appartiene all&#39;oggetto `AssemblerOptionSpec`. Ad esempio, per indicare al servizio Assembler di continuare a elaborare un processo quando si verifica un errore, richiamare il metodo `AssemblerOptionSpec` dell&#39;oggetto `setFailOnError` e passare `false`.

1. Cifra il documento.

   Richiamare il metodo `AssemblerServiceClient` dell&#39;oggetto `invokeOneDocument` e trasmettere i seguenti valori:

   * Un oggetto `com.adobe.idp.Document` che rappresenta il documento DDX. Assicurarsi che il documento DDX contenga il valore `inDoc` per l&#39;elemento di origine PDF.
   * Un oggetto `com.adobe.idp.Document` che contiene il documento PDF non protetto.
   * Un oggetto `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` che specifica le opzioni di esecuzione, incluso il font predefinito e il livello di registro del processo.

   Il metodo `invokeOneDocument` restituisce un oggetto `com.adobe.idp.Document` contenente un documento PDF crittografato con password.

1. Salvare il documento PDF crittografato.

   * Create un oggetto `java.io.File` e accertatevi che l&#39;estensione del nome del file sia .pdf.
   * Richiamare il metodo `Document` dell&#39;oggetto `copyToFile` per copiare nel file il contenuto dell&#39;oggetto `Document`. Assicurarsi di utilizzare l&#39;oggetto `Document` restituito dal metodo `invokeOneDocument`.

**Consulta anche**

[Avvio rapido (modalità SOAP): Assemblaggio di un documento PDF crittografato tramite l&#39;API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-an-encrypted-pdf-document-using-the-java-api)

## Assemblare un documento PDF crittografato utilizzando l&#39;API del servizio Web {#assemble-an-encrypted-pdf-document-using-the-web-service-api}

1. Includere i file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Quando imposti un riferimento a un servizio, accertatevi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituire `localhost` con l&#39;indirizzo IP del server che ospita  AEM Forms.

1. Creare un client Assembler.

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
   * Compilare l&#39;oggetto `BLOB` assegnando il relativo campo `MTOM` con il contenuto dell&#39;array di byte.

1. Fare riferimento a un documento PDF non protetto.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare il documento PDF di input. Questo oggetto `BLOB` viene passato al `invokeOneDocument` come argomento.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF di input e la modalità in cui aprire il file.
   * Creare un array di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà `System.IO.FileStream` dell&#39;oggetto `Length`.
   * Compilare l&#39;array di byte con i dati del flusso richiamando il metodo `Read` dell&#39;oggetto `System.IO.FileStream` e passando l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando il relativo campo `MTOM` con il contenuto dell&#39;array di byte.

1. Impostare le opzioni di esecuzione.

   * Creare un oggetto `AssemblerOptionSpec` che memorizza le opzioni di esecuzione utilizzando il relativo costruttore.
   * Impostare le opzioni di runtime per soddisfare i requisiti aziendali assegnando un valore a un membro di dati che appartiene all&#39;oggetto `AssemblerOptionSpec`. Ad esempio, per indicare al servizio Assembler di continuare l&#39;elaborazione di un processo in caso di errore, assegnare `false` al membro di dati `AssemblerOptionSpec` dell&#39;oggetto `failOnError`.

1. Cifra il documento.

   Richiamare il metodo `AssemblerServiceClient` dell&#39;oggetto `invokeOneDocument` e trasmettere i seguenti valori:

   * Un oggetto `BLOB` che rappresenta il documento DDX
   * Un oggetto `BLOB` che rappresenta il documento PDF non protetto
   * Un oggetto `AssemblerOptionSpec` che specifica le opzioni di esecuzione

   Il metodo `invokeOneDocument` restituisce un oggetto `BLOB` contenente un documento PDF crittografato.

1. Salvare il documento PDF crittografato.

   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF crittografato e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto dell&#39;oggetto `BLOB` restituito dal metodo `invokeOneDocument`. Compilare l&#39;array di byte ottenendo il valore del membro di dati `BLOB` dell&#39;oggetto `MTOM`.
   * Creare un oggetto `System.IO.BinaryWriter` richiamandone il costruttore e passando l&#39;oggetto `System.IO.FileStream`.
   * Scrivere il contenuto dell&#39;array di byte in un file PDF richiamando il metodo `System.IO.BinaryWriter` dell&#39;oggetto `Write` e passando l&#39;array di byte.

**Consulta anche**

[Chiamata  AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
