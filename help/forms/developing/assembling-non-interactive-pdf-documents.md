---
title: Assemblaggio di documenti PDF non interattivi
seo-title: Assembling Non-Interactive PDF Documents
description: Utilizza un modulo PDF non interattivo come input per assemblare un documento PDF non interattivo utilizzando l’API Java e l’API Web Service.
seo-description: Use a non-interactive PDF form as input to assemble a non-interactive PDF document using the Java API and Web Service API.
uuid: 0c7adeb4-9a3a-4ec5-ba33-c3642928d4ea
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 8a75c201-bd88-4809-be08-69de94656489
role: Developer
exl-id: 4677b9e5-3811-4de3-b4f4-9574b5898486
source-git-commit: 135f50cc80f8bb449b2f1621db5e2564f5075968
workflow-type: tm+mt
source-wordcount: '1775'
ht-degree: 0%

---

# Assemblaggio di documenti PDF non interattivi {#assembling-non-interactive-pdf-documents}

È possibile assemblare un documento PDF non interattivo utilizzando come input un modulo PDF interattivo. Si supponga quindi di disporre di un modulo che gli utenti possono utilizzare per immettere i dati nei campi. È possibile passare il modulo al servizio Assembler, in modo che il servizio Assembler restituisca un documento PDF che impedisce agli utenti di immettere dati nei campi. Questo documento è un modulo PDF non interattivo. Ad esempio, nell&#39;illustrazione seguente viene mostrata un&#39;applicazione mutuo che rappresenta un modulo interattivo.

Ai fini di questa discussione, si supponga che venga utilizzato il seguente documento DDX.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
      <PDF result="out.pdf">
        <PDF source="inDoc"/>
        <NoXFA/>
      </PDF>
 </DDX>
```

In questo documento DDX, notare che all&#39;attributo di origine è assegnato il valore `inDoc`. In situazioni in cui al servizio Assembler viene passato un solo documento PDF di input e viene restituito un documento PDF, e si richiama il `invokeOneDocument` operazione, assegnare il valore `inDoc` all’attributo sorgente di PDF. Quando si richiama il `invokeOneDocument` l&#39;operazione `inDoc` value è una chiave predefinita che deve essere specificata nel documento DDX.

Al contrario, quando trasmetti due o più documenti PDF di input al servizio Assembler, puoi richiamare il `invokeDDX` funzionamento. In questa situazione, assegna il nome file del documento di input PDF al `source` attributo.

Questo documento DDX contiene `NoXFA` che indica al servizio Assembler di restituire un documento PDF non interattivo.

Il servizio Assembler può assemblare documenti PDF non interattivi senza che il servizio Output faccia parte dell’installazione dei moduli AEM se il documento di input PDF è basato su un modulo Acrobat o su un modulo XFA statico. Tuttavia, se il documento PDF di input è un modulo XFA dinamico, il servizio Output deve far parte dell’installazione dei moduli AEM. Se il servizio Output non fa parte dell’installazione dei moduli AEM quando viene assemblato un modulo XFA dinamico, viene generata un’eccezione. Vedi [Creazione di flussi di output dei documenti](/help/forms/developing/creating-document-output-streams.md).

>[!NOTE]
>
>Prima di leggere questa sezione, è consigliabile avere familiarità con l’assemblaggio di documenti PDF tramite il servizio Assembler. In questa sezione non vengono descritti i concetti, ad esempio la creazione di un oggetto raccolta contenente documenti di input o l&#39;apprendimento della modalità di estrazione dei risultati dall&#39;oggetto di raccolta restituito. (Vedi [Assemblaggio di documenti PDF a livello di programmazione](/help/forms/developing/programmatically-assembling-pdf-documents.md).)

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Assembler, vedere [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Per ulteriori informazioni su un documento DDX, consulta [Servizio di assemblaggio e riferimento DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Riepilogo dei passaggi {#summary-of-steps}

Per assemblare un documento PDF non interattivo, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Creare un client PDF Assembler.
1. Fai riferimento a un documento DDX esistente.
1. Riferimento a un documento PDF interattivo.
1. Impostare le opzioni di esecuzione.
1. Assemblare il documento PDF.
1. Salvare il documento PDF non interattivo.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso della classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è distribuito su JBoss)
* jbossall-client.jar (richiesto se AEM Forms è distribuito su JBoss)

se AEM Forms è implementato su un server applicazioni J2EE supportato diverso da JBoss, è necessario sostituire i file adobe-utilities.jar e jbossall-client.jar con file JAR specifici per il server applicazioni J2EE in cui è implementato AEM Forms.

**Creare un client Assembler**

Prima di poter eseguire un&#39;operazione Assembler a livello di programmazione, è necessario creare un client di servizio Assembler.

**Riferimento a un documento DDX esistente**

Per assemblare un documento PDF è necessario fare riferimento a un documento DDX. Questo documento DDX deve contenere `NoXFA` che indica al servizio Assembler di restituire un documento PDF non interattivo.

**Riferimento a un documento PDF interattivo**

Per recuperare un documento PDF non interattivo, è necessario fare riferimento a un documento PDF interattivo e passarlo al servizio Assembler.

**Impostare le opzioni di esecuzione**

È possibile impostare le opzioni di esecuzione che controllano il comportamento del servizio Assembler mentre esegue un processo. Ad esempio, è possibile impostare un&#39;opzione che indica al servizio Assembler di continuare l&#39;elaborazione di un processo in caso di errore.

**Assemblare il documento PDF**

Dopo aver creato il client di servizio Assembler, fare riferimento al documento DDX, fare riferimento a un documento PDF interattivo e impostare le opzioni di esecuzione, è possibile richiamare `invokeOneDocument` funzionamento. Poiché al servizio Assembler viene passato un solo documento di input PDF e viene restituito un singolo documento, è possibile utilizzare il `invokeOneDocument` l&#39;operazione in contrapposizione al `invokeDDX` funzionamento.

**Salvare il documento PDF non interattivo**

Se al servizio Assembler viene passato un solo documento PDF, il servizio Assembler restituisce un singolo documento invece di un oggetto raccolta. In altre parole, quando si richiama il `invokeOneDocument` viene restituito un singolo documento. Poiché il documento DDX a cui si fa riferimento in questa sezione contiene istruzioni per la creazione di un documento PDF non interattivo, il servizio Assembler restituisce un documento PDF non interattivo che può essere salvato come file PDF.

**Consulta anche**

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Assemblaggio di documenti PDF a livello di programmazione](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Creare un documento PDF non interattivo utilizzando l’API Java {#assemble-a-non-interactive-pdf-document-using-the-java-api}

Assemblare un documento PDF non interattivo utilizzando l’API del servizio Assembler (Java):

1. Includi file di progetto.

   Includi file JAR client, come adobe-assembler-client.jar, nel percorso di classe del progetto Java.

1. Creare un client Assembler.

   * Crea un `ServiceClientFactory` oggetto contenente le proprietà di connessione.
   * Crea un `AssemblerServiceClient` utilizzando il relativo costruttore e passando `ServiceClientFactory` oggetto.

1. Fai riferimento a un documento DDX esistente.

   * Crea un `java.io.FileInputStream` oggetto che rappresenta il documento DDX utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del file DDX.
   * Crea un `com.adobe.idp.Document` utilizzando il relativo costruttore e passando `java.io.FileInputStream` oggetto.

1. Riferimento a un documento PDF interattivo.

   * Crea un `java.io.FileInputStream` utilizzando il relativo costruttore e passando la posizione di un documento PDF interattivo.
   * Crea un `com.adobe.idp.Document` e passare `java.io.FileInputStream` oggetto contenente il documento PDF. Questo `com.adobe.idp.Document` viene passato all&#39;oggetto `invokeOneDocument` metodo .

1. Impostare le opzioni di esecuzione.

   * Crea un `AssemblerOptionSpec` oggetto che memorizza le opzioni di esecuzione utilizzando il relativo costruttore.
   * Impostare le opzioni di esecuzione per soddisfare i requisiti aziendali richiamando un metodo che appartiene al `AssemblerOptionSpec` oggetto. Ad esempio, per dare istruzioni al servizio Assembler di continuare a elaborare un processo quando si verifica un errore, richiama il `AssemblerOptionSpec` dell’oggetto `setFailOnError` metodo e passaggio `false`.

1. Assemblare il documento PDF.

   Richiama il `AssemblerServiceClient` dell’oggetto `invokeOneDocument` e passare i seguenti valori:

   * A `com.adobe.idp.Document` oggetto che rappresenta il documento DDX. Assicurati che questo documento DDX contenga il valore `inDoc` per l’elemento sorgente PDF.
   * A `com.adobe.idp.Document` oggetto contenente il documento interattivo di PDF.
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` oggetto che specifica le opzioni di esecuzione, incluso il livello di carattere predefinito e di registro dei processi.

   La `invokeOneDocument` restituisce un `com.adobe.idp.Document` oggetto contenente un documento PDF non interattivo.

1. Salvare il documento PDF non interattivo.

   * Crea un `java.io.File` e assicurati che l&#39;estensione del nome del file sia .pdf.
   * Richiama il `Document` dell’oggetto `copyToFile` per copiare il contenuto del `Document` al file. Assicurati di utilizzare `Document` oggetto che `invokeOneDocument` metodo restituito.

* &quot;Avvio rapido (modalità SOAP): Assemblaggio di un documento PDF non interattivo utilizzando l’API Java&quot;

## Assemblare un documento PDF non interattivo utilizzando l’API del servizio Web {#assemble-a-non-interactive-pdf-document-using-the-web-service-api}

Assemblare un documento PDF non interattivo utilizzando l&#39;API del servizio Assembler (servizio Web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurati di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

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
   * Compilare l&#39;array di byte con i dati del flusso richiamando il `System.IO.FileStream` dell’oggetto `Read` metodo . Passa la matrice dei byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare `BLOB` oggetto assegnando il relativo `MTOM` con il contenuto dell&#39;array di byte.

1. Riferimento a un documento PDF interattivo.

   * Crea un `BLOB` utilizzando il relativo costruttore. La `BLOB` viene utilizzato per memorizzare il documento di input PDF. Questo `BLOB` viene passato all&#39;oggetto `invokeOneDocument` come argomento.
   * Crea un `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento di input PDF e la modalità in cui aprire il file.
   * Creare un array di byte che memorizza il contenuto del `System.IO.FileStream` oggetto. È possibile determinare le dimensioni dell&#39;array di byte ottenendo il `System.IO.FileStream` dell’oggetto `Length` proprietà.
   * Compilare l&#39;array di byte con i dati del flusso richiamando il `System.IO.FileStream` dell’oggetto `Read` metodo . Passa la matrice dei byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare `BLOB` oggetto assegnando il relativo `MTOM` con il contenuto dell&#39;array di byte.

1. Impostare le opzioni di esecuzione.

   * Crea un `AssemblerOptionSpec` oggetto che memorizza le opzioni di esecuzione utilizzando il relativo costruttore.
   * Impostare le opzioni di esecuzione per soddisfare i requisiti aziendali assegnando un valore a un membro dati che appartiene al `AssemblerOptionSpec` oggetto. Ad esempio, per dare istruzioni al servizio Assembler di continuare a elaborare un processo quando si verifica un errore, assegnare `false` al `AssemblerOptionSpec` dell’oggetto `failOnError` membro dati.

1. Assemblare il documento PDF.

   Richiama il `AssemblerServiceClient` dell’oggetto `invokeOneDocument` e passare i seguenti valori:

   * A `BLOB` oggetto che rappresenta il documento DDX
   * A `BLOB` oggetto che rappresenta il documento PDF interattivo
   * Un `AssemblerOptionSpec` oggetto che specifica le opzioni di esecuzione

   La `invokeOneDocument` restituisce un `BLOB` oggetto contenente un documento PDF non interattivo.

1. Salvare il documento PDF non interattivo.

   * Crea un `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF non interattivo e la modalità in cui aprire il file.
   * Creare un array di byte che memorizza il contenuto del `BLOB` oggetto che `invokeOneDocument` metodo restituito. Compilare l’array di byte ottenendo il valore del `BLOB` dell’oggetto `MTOM` campo .
   * Crea un `System.IO.BinaryWriter` richiamando il relativo costruttore e passando `System.IO.FileStream` oggetto.
   * Scrivi il contenuto dell’array di byte in un file PDF richiamando il `System.IO.BinaryWriter` dell’oggetto `Write` e passare l&#39;array di byte.

* &quot;Avvio rapido (MTOM): Assemblaggio di un documento PDF non interattivo utilizzando l’API del servizio Web&quot;.

**Consulta anche**

[Richiamo di AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
