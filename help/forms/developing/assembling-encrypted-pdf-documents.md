---
title: Assemblaggio di documenti PDF crittografati
seo-title: Assemblaggio di documenti PDF crittografati
description: Assembla documenti PDF crittografati utilizzando l’API Java e l’API del servizio Web.
seo-description: Assembla documenti PDF crittografati utilizzando l’API Java e l’API del servizio Web.
uuid: d0948ec9-ab67-4fe4-9062-1c4938460b43
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 6d75c7b1-9c0e-47f3-bdb1-61acf16b97f9
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1676'
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

In questo documento DDX, notare che all&#39;attributo di origine viene assegnato il valore `inDoc`. Nelle situazioni in cui viene passato un solo documento PDF di input al servizio Assembler e viene restituito un documento PDF e si richiama l&#39;operazione `invokeOneDocument`, assegnare il valore `inDoc` all&#39;attributo di origine PDF. Quando si richiama l&#39;operazione `invokeOneDocument`, il valore `inDoc` è una chiave predefinita che deve essere specificata nel documento DDX.

Al contrario, quando si trasmettono due o più documenti PDF di input al servizio Assembler, è possibile richiamare l&#39;operazione `invokeDDX`. In questa situazione, assegna il nome file del documento PDF di input all&#39;attributo `source` .

Per crittografare un documento PDF con una password, non è necessario che il servizio di cifratura faccia parte dell’installazione dei moduli AEM. Consultare [Crittografia e decrittografia di documenti PDF](/help/forms/developing/encrypting-decrypting-pdf-documents.md).

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Assembler, vedere [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Per ulteriori informazioni su un documento DDX, vedere [Servizio Assembler e Riferimento DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Riepilogo dei passaggi {#summary-of-steps}

Per assemblare un documento PDF crittografato, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Creare un client Assembler PDF.
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

se AEM Forms è implementato su un server applicazioni J2EE supportato diverso da JBoss, è necessario sostituire i file adobe-utilities.jar e jbossall-client.jar con file JAR specifici per il server applicazioni J2EE in cui è implementato AEM Forms. Per informazioni sulla posizione di tutti i file JAR di AEM Forms, consulta [Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un client Assembler**

Prima di poter eseguire un&#39;operazione Assembler a livello di programmazione, è necessario creare un client di servizio Assembler.

**Riferimento a un documento DDX esistente**

Per assemblare un documento PDF è necessario fare riferimento a un documento DDX. Ad esempio, considera il documento DDX introdotto in questa sezione. Per crittografare un documento PDF, il documento DDX deve contenere l&#39;elemento `PasswordEncryptionProfile` .

**Riferimento a un documento PDF non protetto**

Per crittografare un documento PDF non protetto, è necessario fare riferimento a tale documento e passarlo al servizio Assembler. Se si fa riferimento a un documento PDF già crittografato, viene generata un&#39;eccezione.

**Impostare le opzioni di esecuzione**

È possibile impostare le opzioni di esecuzione che controllano il comportamento del servizio Assembler mentre esegue un processo. Ad esempio, è possibile impostare un&#39;opzione che indica al servizio Assembler di continuare l&#39;elaborazione di un processo in caso di errore. Per informazioni sulle opzioni di esecuzione che è possibile impostare, vedere il riferimento alla classe `AssemblerOptionSpec` in [Riferimento API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Crittografare il documento**

Dopo aver creato il client di servizio Assembler, fare riferimento al documento DDX contenente informazioni sulla crittografia, fare riferimento a un documento PDF non protetto e impostare le opzioni di esecuzione, è possibile richiamare l&#39;operazione `invokeOneDocument`. Poiché al servizio Assembler viene passato un solo documento PDF di input (e viene restituito un solo documento), è possibile utilizzare l&#39;operazione `invokeOneDocument` invece dell&#39;operazione `invokeDDX`.

**Salvare il documento PDF crittografato**

Se al servizio Assembler viene passato un solo documento PDF, il servizio Assembler restituisce un singolo documento invece di un oggetto raccolta. In altre parole, quando si richiama l&#39;operazione `invokeOneDocument`, viene restituito un singolo documento. Poiché il documento DDX a cui si fa riferimento in questa sezione contiene informazioni di crittografia, il servizio Assembler restituisce un documento PDF crittografato con una password.

**Consulta anche**

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Assemblaggio programmatico di documenti PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Assemblare un documento PDF crittografato utilizzando l&#39;API Java {#assemble-an-encrypted-pdf-document-using-the-java-api}

1. Includi file di progetto.

   Includi file JAR client, come adobe-assembler-client.jar, nel percorso di classe del progetto Java.

1. Creare un client Assembler.

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `AssemblerServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Fai riferimento a un documento DDX esistente.

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento DDX utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del file DDX.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Fare riferimento a un documento PDF non protetto.

   * Creare un oggetto `java.io.FileInputStream` utilizzando il relativo costruttore e passando la posizione di un documento PDF non protetto.
   * Creare un oggetto `com.adobe.idp.Document` e passare l&#39;oggetto `java.io.FileInputStream` che contiene il documento PDF. Questo oggetto `com.adobe.idp.Document` viene passato al metodo `invokeOneDocument` .

1. Impostare le opzioni di esecuzione.

   * Creare un oggetto `AssemblerOptionSpec` che memorizza le opzioni di esecuzione utilizzando il relativo costruttore.
   * Impostare le opzioni di esecuzione per soddisfare i requisiti aziendali richiamando un metodo appartenente all&#39;oggetto `AssemblerOptionSpec`. Ad esempio, per dare istruzioni al servizio Assembler di continuare a elaborare un processo quando si verifica un errore, richiamare il metodo `setFailOnError` dell&#39;oggetto `AssemblerOptionSpec` e passare `false`.

1. Crittografare il documento.

   Richiama il metodo `invokeOneDocument` dell&#39;oggetto `AssemblerServiceClient` e passa i seguenti valori:

   * Un oggetto `com.adobe.idp.Document` che rappresenta il documento DDX. Assicurati che questo documento DDX contenga il valore `inDoc` per l&#39;elemento di origine PDF.
   * Oggetto `com.adobe.idp.Document` contenente il documento PDF non protetto.
   * Un oggetto `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` che specifica le opzioni di esecuzione, incluso il tipo di carattere predefinito e il livello di registro dei processi.

   Il metodo `invokeOneDocument` restituisce un oggetto `com.adobe.idp.Document` contenente un documento PDF crittografato con password.

1. Salvare il documento PDF crittografato.

   * Crea un oggetto `java.io.File` e assicurati che l&#39;estensione del nome file sia .pdf.
   * Richiamare il metodo `copyToFile` dell&#39;oggetto `Document` per copiare nel file il contenuto dell&#39;oggetto `Document`. Assicurarsi di utilizzare l&#39;oggetto `Document` restituito dal metodo `invokeOneDocument`.

**Consulta anche**

[Avvio rapido (modalità SOAP): Assemblaggio di un documento PDF crittografato utilizzando l’API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-an-encrypted-pdf-document-using-the-java-api)

## Assemblare un documento PDF crittografato utilizzando l&#39;API del servizio Web {#assemble-an-encrypted-pdf-document-using-the-web-service-api}

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Quando imposti un riferimento a un servizio, assicurati di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Creare un client Assembler.

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
   * Compilare l&#39;oggetto `BLOB` assegnando il relativo campo `MTOM` con il contenuto dell&#39;array di byte.

1. Fare riferimento a un documento PDF non protetto.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare il documento PDF di input. Questo oggetto `BLOB` viene passato a `invokeOneDocument` come argomento.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF di input e la modalità in cui aprire il file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni dell&#39;array di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare l’array di byte con i dati del flusso richiamando il metodo `Read` dell’oggetto `System.IO.FileStream` e passando l’array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando il relativo campo `MTOM` con il contenuto dell&#39;array di byte.

1. Impostare le opzioni di esecuzione.

   * Creare un oggetto `AssemblerOptionSpec` che memorizza le opzioni di esecuzione utilizzando il relativo costruttore.
   * Impostare le opzioni di esecuzione per soddisfare i requisiti aziendali assegnando un valore a un membro dati appartenente all&#39;oggetto `AssemblerOptionSpec`. Ad esempio, per dare istruzioni al servizio Assembler di continuare a elaborare un processo in caso di errore, assegna `false` al membro dati `AssemblerOptionSpec` dell&#39;oggetto `failOnError`.

1. Crittografare il documento.

   Richiama il metodo `invokeOneDocument` dell&#39;oggetto `AssemblerServiceClient` e passa i seguenti valori:

   * Un oggetto `BLOB` che rappresenta il documento DDX
   * Un oggetto `BLOB` che rappresenta il documento PDF non protetto
   * Un oggetto `AssemblerOptionSpec` che specifica le opzioni di esecuzione

   Il metodo `invokeOneDocument` restituisce un oggetto `BLOB` contenente un documento PDF crittografato.

1. Salvare il documento PDF crittografato.

   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF crittografato e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `BLOB` restituito dal metodo `invokeOneDocument`. Compilare l&#39;array di byte ottenendo il valore del membro dati `BLOB` dell&#39;oggetto `MTOM`.
   * Creare un oggetto `System.IO.BinaryWriter` richiamandone il costruttore e passando l&#39;oggetto `System.IO.FileStream`.
   * Scrivi il contenuto dell’array di byte in un file PDF richiamando il metodo `Write` dell’oggetto `System.IO.BinaryWriter` e passando l’array di byte.

**Consulta anche**

[Richiamo di AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
