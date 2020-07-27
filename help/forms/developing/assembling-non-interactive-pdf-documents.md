---
title: Assemblaggio di documenti PDF non interattivi
seo-title: Assemblaggio di documenti PDF non interattivi
description: 'null'
seo-description: 'null'
uuid: 0c7adeb4-9a3a-4ec5-ba33-c3642928d4ea
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 8a75c201-bd88-4809-be08-69de94656489
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '1760'
ht-degree: 0%

---


# Assemblaggio di documenti PDF non interattivi {#assembling-non-interactive-pdf-documents}

È possibile assemblare un documento PDF non interattivo utilizzando come input un modulo PDF interattivo. Si supponga quindi di disporre di un modulo che gli utenti possano utilizzare per immettere dati nei campi. È possibile trasmettere il modulo al servizio Assembler, restituendo al servizio Assembler un documento PDF che impedisce agli utenti di immettere dati nei campi. Questo documento è un modulo PDF non interattivo. Ad esempio, l&#39;illustrazione seguente mostra un&#39;applicazione mutuo che rappresenta un modulo interattivo.

Ai fini di questa discussione, si supponga di utilizzare il seguente documento DDX.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
      <PDF result="out.pdf">
        <PDF source="inDoc"/>
        <NoXFA/>
      </PDF>
 </DDX>
```

In questo documento DDX, si noti che all&#39;attributo di origine è assegnato il valore `inDoc`. In situazioni in cui viene passato un solo documento PDF di input al servizio Assembler e viene restituito un documento PDF e si esegue l&#39; `invokeOneDocument` operazione, assegnare il valore `inDoc` all&#39;attributo di origine PDF. Quando si richiama l&#39; `invokeOneDocument` operazione, il `inDoc` valore è una chiave predefinita che deve essere specificata nel documento DDX.

Al contrario, quando si passano due o più documenti PDF di input al servizio Assembler, è possibile richiamare l&#39; `invokeDDX` operazione. In questa situazione, assegnare all&#39; `source` attributo il nome del file del documento PDF di input.

Questo documento DDX contiene l&#39; `NoXFA` elemento, che indica al servizio Assembler di restituire un documento PDF non interattivo.

Il servizio Assembler può assemblare documenti PDF non interattivi senza che il servizio Output faccia parte dell’installazione di moduli AEM, se il documento PDF di input è basato su un modulo Acrobat o su un modulo XFA statico. Tuttavia, se il documento PDF di input è un modulo XFA dinamico, il servizio Output deve far parte dell&#39;installazione dei moduli AEM. Se il servizio Output non fa parte dell&#39;installazione dei moduli AEM quando viene assemblato un modulo XFA dinamico, viene generata un&#39;eccezione. Vedere [Creazione di flussi](/help/forms/developing/creating-document-output-streams.md)di output dei documenti.

>[!NOTE]
>
>Prima di leggere questa sezione, è consigliabile avere familiarità con l&#39;assemblaggio di documenti PDF tramite il servizio Assembler. In questa sezione non vengono discussi concetti, ad esempio la creazione di un oggetto raccolta che contiene documenti di input o l&#39;apprendimento di come estrarre i risultati dall&#39;oggetto raccolta restituito. (Vedere Assemblaggio [di documenti](/help/forms/developing/programmatically-assembling-pdf-documents.md)PDF a livello di programmazione.)

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Assembler, vedere Riferimento [servizi per i AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Per ulteriori informazioni su un documento DDX, vedere Servizio [Assembler e Riferimento](https://www.adobe.com/go/learn_aemforms_ddx_63)DDX.

## Riepilogo dei passaggi {#summary-of-steps}

Per assemblare un documento PDF non interattivo, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un client Assembler PDF.
1. Fare riferimento a un documento DDX esistente.
1. Fare riferimento a un documento PDF interattivo.
1. Impostare le opzioni di esecuzione.
1. Assemblare il documento PDF.
1. Salvare il documento PDF non interattivo.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, accertatevi di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (richiesto se i AEM Forms sono distribuiti su JBoss)
* jbossall-client.jar (richiesto se i AEM Forms sono distribuiti su JBoss)

se i AEM Forms sono distribuiti su un server applicazione J2EE supportato diverso da JBoss, è necessario sostituire i file adobe-utilities.jar e jbossall-client.jar con file JAR specifici del server applicazione J2EE in cui sono distribuiti i AEM Forms.

**Creare un client Assembler**

Prima di eseguire un&#39;operazione Assembler a livello di programmazione, è necessario creare un client di servizio Assembler.

**Riferimento a un documento DDX esistente**

Per assemblare un documento PDF è necessario fare riferimento a un documento DDX. Questo documento DDX deve contenere l&#39; `NoXFA` elemento, che richiede al servizio Assembler di restituire un documento PDF non interattivo.

**Riferimento a un documento PDF interattivo**

Per ripristinare un documento PDF non interattivo, è necessario fare riferimento a un documento PDF interattivo e passarlo al servizio Assembler.

**Impostazione delle opzioni di esecuzione**

È possibile impostare opzioni di esecuzione che controllano il comportamento del servizio Assembler mentre esegue un processo. Ad esempio, potete impostare un&#39;opzione che indichi al servizio Assembler di continuare l&#39;elaborazione di un processo in caso di errore.

**Assemblare il documento PDF**

Dopo aver creato il client del servizio Assembler, fatto riferimento al documento DDX, fatto riferimento a un documento PDF interattivo e impostato le opzioni di esecuzione, è possibile richiamare l&#39; `invokeOneDocument` operazione. Poiché al servizio Assembler viene passato un solo documento PDF di input e viene restituito un solo documento, è possibile utilizzare l&#39; `invokeOneDocument` operazione in opposizione all&#39; `invokeDDX` operazione.

**Salvare il documento PDF non interattivo**

Se al servizio Assembler viene passato un solo documento PDF, il servizio Assembler restituisce un singolo documento invece di un oggetto raccolta. In altre parole, quando si richiama l&#39; `invokeOneDocument` operazione, viene restituito un singolo documento. Poiché il documento DDX a cui si fa riferimento in questa sezione contiene istruzioni per la creazione di un documento PDF non interattivo, il servizio Assembler restituisce un documento PDF non interattivo che può essere salvato come file PDF.

**Consulta anche**

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Assemblaggio di documenti PDF a livello di programmazione](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Assemblare un documento PDF non interattivo utilizzando l&#39;API Java {#assemble-a-non-interactive-pdf-document-using-the-java-api}

Assemblate un documento PDF non interattivo utilizzando l&#39;API del servizio Assembler (Java):

1. Includere i file di progetto.

   Includete file JAR client, ad esempio adobe-assembler-client.jar, nel percorso di classe del progetto Java.

1. Creare un client Assembler.

   * Creare un `ServiceClientFactory` oggetto che contenga proprietà di connessione.
   * Creare un `AssemblerServiceClient` oggetto utilizzando il relativo costruttore e passando l&#39; `ServiceClientFactory` oggetto.

1. Fare riferimento a un documento DDX esistente.

   * Creare un `java.io.FileInputStream` oggetto che rappresenta il documento DDX utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del file DDX.
   * Creare un `com.adobe.idp.Document` oggetto utilizzando il relativo costruttore e passando l&#39; `java.io.FileInputStream` oggetto.

1. Fare riferimento a un documento PDF interattivo.

   * Creare un `java.io.FileInputStream` oggetto utilizzando il relativo costruttore e passando la posizione di un documento PDF interattivo.
   * Creare un `com.adobe.idp.Document` oggetto e passare l&#39; `java.io.FileInputStream` oggetto che contiene il documento PDF. Questo `com.adobe.idp.Document` oggetto viene passato al `invokeOneDocument` metodo.

1. Impostare le opzioni di esecuzione.

   * Creare un `AssemblerOptionSpec` oggetto che memorizza le opzioni di esecuzione utilizzando il relativo costruttore.
   * Impostate le opzioni di runtime per soddisfare i requisiti aziendali richiamando un metodo che appartiene all&#39; `AssemblerOptionSpec` oggetto. Ad esempio, per indicare al servizio Assembler di continuare a elaborare un processo quando si verifica un errore, richiamare il metodo dell&#39; `AssemblerOptionSpec` oggetto `setFailOnError` e passare `false`.

1. Assemblare il documento PDF.

   Richiama il metodo dell’ `AssemblerServiceClient` oggetto `invokeOneDocument` e passa i seguenti valori:

   * Un `com.adobe.idp.Document` oggetto che rappresenta il documento DDX. Assicurarsi che il documento DDX contenga il valore `inDoc` per l&#39;elemento di origine PDF.
   * Un `com.adobe.idp.Document` oggetto che contiene il documento PDF interattivo.
   * Un `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` oggetto che specifica le opzioni di esecuzione, incluso il livello predefinito del font e del registro dei processi.

   Il `invokeOneDocument` metodo restituisce un `com.adobe.idp.Document` oggetto che contiene un documento PDF non interattivo.

1. Salvare il documento PDF non interattivo.

   * Create un `java.io.File` oggetto e accertatevi che l&#39;estensione del nome del file sia .pdf.
   * Richiamare il metodo dell&#39; `Document` oggetto `copyToFile` per copiare il contenuto dell&#39; `Document` oggetto nel file. Assicurarsi di utilizzare l&#39; `Document` oggetto restituito dal `invokeOneDocument` metodo.

* &quot;Avvio rapido (modalità SOAP): Assemblare un documento PDF non interattivo utilizzando l&#39;API Java&quot;

## Assemblare un documento PDF non interattivo utilizzando l&#39;API del servizio Web {#assemble-a-non-interactive-pdf-document-using-the-web-service-api}

Assemblate un documento PDF non interattivo utilizzando l&#39;API del servizio Assembler (servizio Web):

1. Includere i file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

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
   * Compilare l&#39;array di byte con i dati del flusso richiamando il metodo dell&#39; `System.IO.FileStream` oggetto `Read` . Passare l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39; `BLOB` oggetto assegnandone `MTOM` il campo con il contenuto dell&#39;array di byte.

1. Fare riferimento a un documento PDF interattivo.

   * Creare un `BLOB` oggetto utilizzando il relativo costruttore. L&#39; `BLOB` oggetto viene utilizzato per memorizzare il documento PDF di input. Questo `BLOB` oggetto viene passato all&#39;oggetto `invokeOneDocument` come argomento.
   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF di input e la modalità in cui aprire il file.
   * Creare un array di byte che memorizza il contenuto dell&#39; `System.IO.FileStream` oggetto. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà dell&#39; `System.IO.FileStream` oggetto `Length` .
   * Compilare l&#39;array di byte con i dati del flusso richiamando il metodo dell&#39; `System.IO.FileStream` oggetto `Read` . Passare l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39; `BLOB` oggetto assegnandone `MTOM` il campo con il contenuto dell&#39;array di byte.

1. Impostare le opzioni di esecuzione.

   * Creare un `AssemblerOptionSpec` oggetto che memorizza le opzioni di esecuzione utilizzando il relativo costruttore.
   * Impostare le opzioni di runtime per soddisfare i requisiti aziendali assegnando un valore a un membro di dati che appartiene all&#39; `AssemblerOptionSpec` oggetto. Ad esempio, per indicare al servizio Assembler di continuare l&#39;elaborazione di un processo in caso di errore, assegnare `false` al membro `AssemblerOptionSpec` dati dell&#39; `failOnError` oggetto.

1. Assemblare il documento PDF.

   Richiama il metodo dell’ `AssemblerServiceClient` oggetto `invokeOneDocument` e passa i seguenti valori:

   * Un `BLOB` oggetto che rappresenta il documento DDX
   * Un `BLOB` oggetto che rappresenta il documento PDF interattivo
   * Un oggetto `AssemblerOptionSpec` che specifica le opzioni di esecuzione

   Il `invokeOneDocument` metodo restituisce un `BLOB` oggetto che contiene un documento PDF non interattivo.

1. Salvare il documento PDF non interattivo.

   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF non interattivo e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto dell&#39; `BLOB` oggetto restituito dal `invokeOneDocument` metodo. Compilare l&#39;array di byte ottenendo il valore del campo dell&#39; `BLOB` oggetto `MTOM` .
   * Creare un `System.IO.BinaryWriter` oggetto richiamando il relativo costruttore e passando l&#39; `System.IO.FileStream` oggetto.
   * Scrivere il contenuto dell&#39;array di byte in un file PDF richiamando il metodo dell&#39; `System.IO.BinaryWriter` oggetto `Write` e passando l&#39;array di byte.

* &quot;Avvio rapido (MTOM): Assemblare un documento PDF non interattivo utilizzando l&#39;API del servizio Web&quot;.

**Consulta anche**

[Chiamata di AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
