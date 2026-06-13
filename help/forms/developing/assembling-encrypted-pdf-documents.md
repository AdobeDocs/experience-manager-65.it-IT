---
title: Assemblaggio di documenti PDF crittografati
description: Assembla documenti PDF crittografati utilizzando l’API Java e l’API dei servizi web.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 2caaca74-640a-4257-a81b-3e8b295cd182
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1676'
ht-degree: 1%

---

# Assemblaggio di documenti PDF crittografati {#assembling-encrypted-pdf-documents}

**Gli esempi e gli esempi contenuti in questo documento sono solo per AEM Forms in ambiente JEE.**

È possibile crittografare un documento PDF con una password utilizzando il servizio Assembler. Dopo aver crittografato un documento PDF con una password, l&#39;utente deve specificare la password per visualizzare il documento PDF in Adobe Reader o Acrobat. Per crittografare un documento PDF con una password, il documento DDX deve contenere i valori degli elementi di crittografia necessari per crittografare un documento PDF.

Ai fini della presente discussione, si supponga che venga utilizzato il seguente documento DDX.

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

All&#39;interno di questo documento DDX, si noti che all&#39;attributo di origine viene assegnato il valore `inDoc`. Nelle situazioni in cui viene passato un solo documento PDF di input al servizio Assembler e viene restituito un documento PDF e si richiama l&#39;operazione `invokeOneDocument`, assegnare il valore `inDoc` all&#39;attributo di origine di PDF. Quando si richiama l&#39;operazione `invokeOneDocument`, il valore `inDoc` è una chiave predefinita che deve essere specificata nel documento DDX.

Al contrario, quando si trasmettono due o più documenti PDF di input al servizio Assembler, è possibile richiamare l&#39;operazione `invokeDDX`. In questa situazione, assegnare il nome file del documento PDF di input all&#39;attributo `source`.

Per crittografare un documento PDF con una password non è necessario che il servizio Crittografia faccia parte dell&#39;installazione di AEM Forms. Vedere [Crittografia e decrittografia dei documenti di PDF](/help/forms/developing/encrypting-decrypting-pdf-documents.md).

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Assembler, vedere [Riferimento ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Per ulteriori informazioni su un documento DDX, vedere [Servizio assemblatore e riferimento DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Riepilogo dei passaggi {#summary-of-steps}

Per assemblare un documento PDF crittografato, effettuare le seguenti operazioni:

1. Includi file di progetto.
1. Creare un client Assembler di PDF.
1. Fare riferimento a un documento DDX esistente.
1. Fare riferimento a un documento PDF non protetto.
1. Impostare le opzioni di runtime.
1. Crittografare il documento.
1. Salvare il documento PDF crittografato.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso della classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è implementato su JBoss)
* jbossall-client.jar (obbligatorio se AEM Forms è distribuito su JBoss)

se AEM Forms viene distribuito su un server applicazioni J2EE supportato diverso da JBoss, è necessario sostituire i file adobe-utilities.jar e jbossall-client.jar con file JAR specifici per il server applicazioni J2EE su cui è distribuito AEM Forms. Per informazioni sulla posizione di tutti i file JAR di AEM Forms, vedi [Inclusi i file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un client Assembler**

Prima di poter eseguire un&#39;operazione Assembler a livello di programmazione, è necessario creare un client del servizio Assembler.

**Riferimento a un documento DDX esistente**

Per assemblare un documento PDF è necessario fare riferimento a un documento DDX. Si consideri ad esempio il documento DDX introdotto in questa sezione. Per crittografare un documento PDF, il documento DDX deve contenere l&#39;elemento `PasswordEncryptionProfile`.

**Riferimento a un documento PDF non protetto**

È necessario fare riferimento a un documento PDF non protetto e passarlo al servizio Assembler per crittografarlo. Se si fa riferimento a un documento PDF già crittografato, viene generata un&#39;eccezione.

**Impostare le opzioni di runtime**

È possibile impostare le opzioni di runtime che controllano il comportamento del servizio Assembler durante l&#39;esecuzione di un processo. È ad esempio possibile impostare un&#39;opzione che indichi al servizio Assembler di continuare l&#39;elaborazione di un processo in caso di errore. Per informazioni sulle opzioni di runtime che è possibile impostare, vedere il riferimento alla classe `AssemblerOptionSpec` in [Riferimento API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Crittografa il documento**

Dopo aver creato il client del servizio Assembler, aver fatto riferimento al documento DDX che contiene informazioni di crittografia, aver fatto riferimento a un documento PDF non protetto e aver impostato le opzioni di runtime, è possibile richiamare l&#39;operazione `invokeOneDocument`. Poiché al servizio Assembler viene passato un solo documento PDF di input (e viene restituito un documento), è possibile utilizzare l&#39;operazione `invokeOneDocument` anziché l&#39;operazione `invokeDDX`.

**Salvare il documento PDF crittografato**

Se al servizio Assembler viene passato un solo documento PDF, il servizio Assembler restituisce un singolo documento invece di un oggetto insieme. In altre parole, quando si richiama l&#39;operazione `invokeOneDocument`, viene restituito un singolo documento. Poiché il documento DDX a cui si fa riferimento in questa sezione contiene informazioni di crittografia, il servizio Assembler restituisce un documento PDF crittografato con una password.

**Consulta anche**

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Assemblaggio di documenti PDF a livello di programmazione](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Assemblare un documento PDF crittografato utilizzando l’API Java {#assemble-an-encrypted-pdf-document-using-the-java-api}

1. Includi file di progetto.

   Includi i file JAR client, come adobe-assembler-client.jar, nel percorso di classe del progetto Java.

1. Creare un client Assembler.

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `AssemblerServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Fare riferimento a un documento DDX esistente.

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento DDX utilizzando il relativo costruttore e passando un valore stringa che specifica la posizione del file DDX.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Fare riferimento a un documento PDF non protetto.

   * Creare un oggetto `java.io.FileInputStream` utilizzando il relativo costruttore e passando il percorso di un documento PDF non protetto.
   * Creare un oggetto `com.adobe.idp.Document` e passare l&#39;oggetto `java.io.FileInputStream` che contiene il documento PDF. L&#39;oggetto `com.adobe.idp.Document` è passato al metodo `invokeOneDocument`.

1. Impostare le opzioni di runtime.

   * Creare un oggetto `AssemblerOptionSpec` che memorizza le opzioni di runtime utilizzando il relativo costruttore.
   * Impostare le opzioni di runtime per soddisfare i requisiti aziendali richiamando un metodo che appartiene all&#39;oggetto `AssemblerOptionSpec`. Ad esempio, per indicare al servizio Assembler di continuare a elaborare un processo quando si verifica un errore, richiamare il metodo `setFailOnError` dell&#39;oggetto `AssemblerOptionSpec` e passare `false`.

1. Crittografare il documento.

   Richiama il metodo `invokeOneDocument` dell&#39;oggetto `AssemblerServiceClient` e passa i seguenti valori:

   * Oggetto `com.adobe.idp.Document` che rappresenta il documento DDX. Verificare che il documento DDX contenga il valore `inDoc` per l&#39;elemento di origine PDF.
   * Oggetto `com.adobe.idp.Document` contenente il documento PDF non protetto.
   * Oggetto `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` che specifica le opzioni di runtime, inclusi il tipo di carattere predefinito e il livello del registro dei processi.

   Il metodo `invokeOneDocument` restituisce un oggetto `com.adobe.idp.Document` che contiene un documento PDF crittografato con password.

1. Salvare il documento PDF crittografato.

   * Creare un oggetto `java.io.File` e verificare che l&#39;estensione del nome file sia pdf.
   * Richiama il metodo `copyToFile` dell&#39;oggetto `Document` per copiare il contenuto dell&#39;oggetto `Document` nel file. Assicurarsi di utilizzare l&#39;oggetto `Document` restituito dal metodo `invokeOneDocument`.

**Consulta anche**

[Guida rapida (modalità SOAP): assemblaggio di un documento PDF crittografato tramite l’API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-an-encrypted-pdf-document-using-the-java-api)

## Assemblare un documento PDF crittografato utilizzando l’API del servizio web {#assemble-an-encrypted-pdf-document-using-the-web-service-api}

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL durante l&#39;impostazione di un riferimento al servizio: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Creare un client Assembler.

   * Creare un oggetto `AssemblerServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `AssemblerServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). Non è necessario utilizzare l&#39;attributo `lc_version`. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `AssemblerServiceClient.Endpoint.Binding`. Eseguire il cast del valore restituito in `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegnare il nome utente di AEM Forms al campo `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Fare riferimento a un documento DDX esistente.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per archiviare il documento DDX.
   * Creare un oggetto `System.IO.FileStream` richiamandone il costruttore e passando un valore stringa che rappresenta la posizione del file del documento DDX e la modalità di apertura del file in.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni della matrice di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare la matrice di byte con i dati di flusso richiamando il metodo `Read` dell&#39;oggetto `System.IO.FileStream` e passando la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando il relativo campo `MTOM` al contenuto della matrice di byte.

1. Fare riferimento a un documento PDF non protetto.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare il documento PDF di input. Questo oggetto `BLOB` è passato a `invokeOneDocument` come argomento.
   * Creare un oggetto `System.IO.FileStream` richiamandone il costruttore e passando un valore stringa che rappresenta la posizione del file del documento PDF di input e la modalità di apertura del file in.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni della matrice di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare la matrice di byte con i dati di flusso richiamando il metodo `Read` dell&#39;oggetto `System.IO.FileStream` e passando la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando il relativo campo `MTOM` al contenuto della matrice di byte.

1. Impostare le opzioni di runtime.

   * Creare un oggetto `AssemblerOptionSpec` che memorizza le opzioni di runtime utilizzando il relativo costruttore.
   * Impostare le opzioni di runtime per soddisfare i requisiti aziendali assegnando un valore a un membro dati che appartiene all&#39;oggetto `AssemblerOptionSpec`. Ad esempio, per indicare al servizio Assembler di continuare a elaborare un processo quando si verifica un errore, assegnare `false` al membro dati `failOnError` dell&#39;oggetto `AssemblerOptionSpec`.

1. Crittografare il documento.

   Richiama il metodo `invokeOneDocument` dell&#39;oggetto `AssemblerServiceClient` e passa i seguenti valori:

   * Oggetto `BLOB` che rappresenta il documento DDX
   * Oggetto `BLOB` che rappresenta il documento PDF non protetto
   * Oggetto `AssemblerOptionSpec` che specifica le opzioni di runtime

   Il metodo `invokeOneDocument` restituisce un oggetto `BLOB` che contiene un documento PDF crittografato.

1. Salvare il documento PDF crittografato.

   * Creare un oggetto `System.IO.FileStream` richiamandone il costruttore e passando un valore stringa che rappresenta la posizione del file del documento PDF crittografato e la modalità di apertura del file in.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `BLOB` restituito dal metodo `invokeOneDocument`. Popolare la matrice di byte ottenendo il valore del membro dati `MTOM` dell&#39;oggetto `BLOB`.
   * Creare un oggetto `System.IO.BinaryWriter` richiamandone il costruttore e passando l&#39;oggetto `System.IO.FileStream`.
   * Scrivere il contenuto della matrice di byte in un file PDF richiamando il metodo `Write` dell&#39;oggetto `System.IO.BinaryWriter` e passando la matrice di byte.

**Consulta anche**

[Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
