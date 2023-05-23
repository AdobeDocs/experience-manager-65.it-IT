---
title: Assemblaggio di documenti di PDF non interattivi
seo-title: Assembling Non-Interactive PDF Documents
description: Utilizza un modulo PDF non interattivo come input per assemblare un documento PDF non interattivo utilizzando l’API Java e l’API del servizio web.
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

# Assemblaggio di documenti di PDF non interattivi {#assembling-non-interactive-pdf-documents}

È possibile assemblare un documento PDF non interattivo quando si utilizza come input un modulo PDF interattivo. Si supponga di disporre di un modulo che gli utenti possono utilizzare per immettere dati nei relativi campi. È possibile passare tale modulo al servizio Assembler, in modo che quest&#39;ultimo restituisca un documento PDF che impedisce agli utenti di immettere dati nei propri campi. Questo documento è un modulo di PDF non interattivo. Nell&#39;illustrazione seguente, ad esempio, viene illustrata un&#39;applicazione ipotecaria che rappresenta un modulo interattivo.

Ai fini della presente discussione, si supponga che venga utilizzato il seguente documento DDX.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
      <PDF result="out.pdf">
        <PDF source="inDoc"/>
        <NoXFA/>
      </PDF>
 </DDX>
```

All&#39;interno di questo documento DDX, si noti che all&#39;attributo di origine viene assegnato il valore `inDoc`. Nei casi in cui al servizio Assembler viene passato un solo documento di input PDF e viene restituito un solo documento di input PDF, e si richiama `invokeOneDocument` operazione, assegna il valore `inDoc` all’attributo di origine PDF. Quando si richiama `invokeOneDocument` funzionamento, `inDoc` value è una chiave predefinita che deve essere specificata nel documento DDX.

Al contrario, quando si trasmettono due o più documenti di input PDF al servizio Assembler, è possibile richiamare `invokeDDX` operazione. In questa situazione, assegna il nome file del documento PDF di input a `source` attributo.

Questo documento DDX contiene `NoXFA` che indica al servizio Assembler di restituire un documento PDF non interattivo.

Il servizio Assembler può assemblare documenti PDF non interattivi senza che il servizio di output faccia parte dell’installazione dei moduli AEM se il documento PDF di input è basato su un modulo Acrobat o su un modulo XFA statico. Tuttavia, se il documento di input PDF è un modulo XFA dinamico, il servizio di output deve far parte dell’installazione dei moduli AEM. Se il servizio di output non fa parte dell’installazione dei moduli AEM quando viene assemblato un modulo XFA dinamico, viene generata un’eccezione. Consulta [Creazione di flussi di output dei documenti](/help/forms/developing/creating-document-output-streams.md).

>[!NOTE]
>
>Prima di leggere questa sezione, è consigliabile avere familiarità con l&#39;assemblaggio di documenti PDF utilizzando il servizio Assembler. In questa sezione non vengono descritti concetti quali la creazione di un oggetto raccolta contenente documenti di input o l&#39;apprendimento dell&#39;estrazione dei risultati dall&#39;oggetto raccolta restituito. (vedere [Assemblaggio di documenti PDF a livello di programmazione](/help/forms/developing/programmatically-assembling-pdf-documents.md).)

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Assembler, vedere [Guida di riferimento dei servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Per ulteriori informazioni su un documento DDX, vedere [Servizio assemblatore e riferimento DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Riepilogo dei passaggi {#summary-of-steps}

Per assemblare un documento PDF non interattivo, effettuare le seguenti operazioni:

1. Includi file di progetto.
1. Creare un client PDF Assembler.
1. Fare riferimento a un documento DDX esistente.
1. Fai riferimento a un documento di PDF interattivo.
1. Impostare le opzioni di runtime.
1. Assemblare il documento PDF.
1. Salva il documento PDF non interattivo.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso della classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è implementato su JBoss)
* jbossall-client.jar (obbligatorio se AEM Forms è distribuito su JBoss)

se AEM Forms viene distribuito su un server applicazioni J2EE supportato diverso da JBoss, è necessario sostituire i file adobe-utilities.jar e jbossall-client.jar con file JAR specifici per il server applicazioni J2EE su cui è distribuito AEM Forms.

**Creare un client Assembler**

Prima di poter eseguire un&#39;operazione Assembler a livello di programmazione, è necessario creare un client del servizio Assembler.

**Riferimento a un documento DDX esistente**

Per assemblare un documento PDF è necessario fare riferimento a un documento DDX. Questo documento DDX deve contenere `NoXFA` che indica al servizio Assembler di restituire un documento PDF non interattivo.

**Riferimento a un documento interattivo di PDF**

È necessario fare riferimento a un documento di PDF interattivo e passarlo al servizio Assembler per recuperare un documento di PDF non interattivo.

**Impostare le opzioni di runtime**

È possibile impostare le opzioni di runtime che controllano il comportamento del servizio Assembler durante l&#39;esecuzione di un processo. È ad esempio possibile impostare un&#39;opzione che indichi al servizio Assembler di continuare l&#39;elaborazione di un processo in caso di errore.

**Assemblare il documento PDF**

Dopo aver creato il client del servizio Assembler, aver fatto riferimento al documento DDX, aver creato un riferimento a un documento interattivo di PDF e aver impostato le opzioni di runtime, è possibile richiamare `invokeOneDocument` operazione. Poiché al servizio Assembler viene passato un solo documento di input PDF e viene restituito un singolo documento, è possibile utilizzare `invokeOneDocument` operazione anziché `invokeDDX` operazione.

**Salvare il documento PDF non interattivo**

Se al servizio Assembler viene passato un solo documento PDF, il servizio Assembler restituisce un singolo documento invece di un oggetto insieme. Cioè, quando si richiama il `invokeOneDocument` viene restituito un singolo documento. Poiché il documento DDX a cui si fa riferimento in questa sezione contiene istruzioni per la creazione di un documento PDF non interattivo, il servizio Assembler restituisce un documento PDF non interattivo che può essere salvato come file PDF.

**Consulta anche**

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Assemblaggio di documenti PDF a livello di programmazione](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Assemblare un documento PDF non interattivo utilizzando l’API Java {#assemble-a-non-interactive-pdf-document-using-the-java-api}

Assembla un documento PDF non interattivo utilizzando l’API del servizio Assembler (Java):

1. Includi file di progetto.

   Includi i file JAR client, come adobe-assembler-client.jar, nel percorso di classe del progetto Java.

1. Creare un client Assembler.

   * Creare un `ServiceClientFactory` oggetto che contiene proprietà di connessione.
   * Creare un `AssemblerServiceClient` mediante il costruttore e passando il `ServiceClientFactory` oggetto.

1. Fare riferimento a un documento DDX esistente.

   * Creare un `java.io.FileInputStream` oggetto che rappresenta il documento DDX utilizzando il relativo costruttore e passando un valore stringa che specifica la posizione del file DDX.
   * Creare un `com.adobe.idp.Document` mediante il costruttore e passando il `java.io.FileInputStream` oggetto.

1. Fai riferimento a un documento di PDF interattivo.

   * Creare un `java.io.FileInputStream` mediante il costruttore e passando la posizione di un documento interattivo di PDF.
   * Creare un `com.adobe.idp.Document` e passare il `java.io.FileInputStream` oggetto che contiene il documento PDF. Questo `com.adobe.idp.Document` l&#39;oggetto viene passato al `invokeOneDocument` metodo.

1. Impostare le opzioni di runtime.

   * Creare un `AssemblerOptionSpec` oggetto che memorizza le opzioni di runtime mediante il relativo costruttore.
   * Impostare le opzioni di runtime per soddisfare i requisiti aziendali richiamando un metodo che appartiene al `AssemblerOptionSpec` oggetto. Ad esempio, per indicare al servizio Assembler di continuare l&#39;elaborazione di un processo quando si verifica un errore, richiamare `AssemblerOptionSpec` dell&#39;oggetto `setFailOnError` metodo e passaggio `false`.

1. Assemblare il documento PDF.

   Richiama `AssemblerServiceClient` dell&#39;oggetto `invokeOneDocument` e trasmettere i seguenti valori:

   * A `com.adobe.idp.Document` oggetto che rappresenta il documento DDX. Verifica che il documento DDX contenga il valore `inDoc` per l’elemento sorgente PDF.
   * A `com.adobe.idp.Document` oggetto che contiene il documento interattivo PDF.
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` oggetto che specifica le opzioni di runtime, inclusi il tipo di carattere predefinito e il livello di registro del processo.

   Il `invokeOneDocument` il metodo restituisce un `com.adobe.idp.Document` oggetto contenente un documento PDF non interattivo.

1. Salva il documento PDF non interattivo.

   * Creare un `java.io.File` e assicurarsi che l&#39;estensione del nome file sia .pdf.
   * Richiama `Document` dell&#39;oggetto `copyToFile` metodo per copiare il contenuto del `Document` al file. Assicurati di utilizzare `Document` oggetto che `invokeOneDocument` metodo restituito.

* &quot;Guida rapida (modalità SOAP): assemblaggio di un documento PDF non interattivo tramite l’API Java&quot;

## Assemblare un documento PDF non interattivo utilizzando l’API del servizio web {#assemble-a-non-interactive-pdf-document-using-the-web-service-api}

Assembla un documento PDF non interattivo utilizzando l’API del servizio Assembler (servizio web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l’indirizzo IP del server che ospita AEM Forms.

1. Creare un client Assembler.

   * Creare un `AssemblerServiceClient` utilizzando il costruttore predefinito.
   * Creare un `AssemblerServiceClient.Endpoint.Address` oggetto utilizzando `System.ServiceModel.EndpointAddress` costruttore. Passa un valore stringa che specifica il file WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). Non è necessario utilizzare il `lc_version` attributo. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.
   * Creare un `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto ottenendo il valore del `AssemblerServiceClient.Endpoint.Binding` campo. Invia il valore restituito a `BasicHttpBinding`.
   * Imposta il `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegna al campo il nome utente dei moduli AEM `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore password corrispondente al campo `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Fare riferimento a un documento DDX esistente.

   * Creare un `BLOB` mediante il costruttore. Il `BLOB` viene utilizzato per memorizzare il documento DDX.
   * Creare un `System.IO.FileStream` richiamando il relativo costruttore e passando un valore stringa che rappresenta la posizione del file del documento DDX e la modalità di apertura del file in.
   * Creare una matrice di byte che memorizza il contenuto della `System.IO.FileStream` oggetto. È possibile determinare le dimensioni della matrice di byte ottenendo `System.IO.FileStream` dell&#39;oggetto `Length` proprietà.
   * Compilare la matrice di byte con i dati di flusso richiamando `System.IO.FileStream` dell&#39;oggetto `Read` metodo. Passare la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare il `BLOB` oggetto assegnando il relativo `MTOM` con il contenuto della matrice di byte.

1. Fai riferimento a un documento di PDF interattivo.

   * Creare un `BLOB` mediante il costruttore. Il `BLOB` L&#39;oggetto viene utilizzato per memorizzare il documento di input PDF. Questo `BLOB` l&#39;oggetto viene passato al `invokeOneDocument` come argomento.
   * Creare un `System.IO.FileStream` richiamando il relativo costruttore e passando un valore stringa che rappresenta la posizione del file del documento di input PDF e la modalità di apertura del file in.
   * Creare una matrice di byte che memorizza il contenuto della `System.IO.FileStream` oggetto. È possibile determinare le dimensioni della matrice di byte ottenendo `System.IO.FileStream` dell&#39;oggetto `Length` proprietà.
   * Compilare la matrice di byte con i dati di flusso richiamando `System.IO.FileStream` dell&#39;oggetto `Read` metodo. Passare la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare il `BLOB` oggetto assegnando il relativo `MTOM` con il contenuto della matrice di byte.

1. Impostare le opzioni di runtime.

   * Creare un `AssemblerOptionSpec` oggetto che memorizza le opzioni di runtime mediante il relativo costruttore.
   * Impostare le opzioni di runtime per soddisfare i requisiti aziendali assegnando un valore a un membro dati che appartiene al `AssemblerOptionSpec` oggetto. Ad esempio, per indicare al servizio Assembler di continuare l&#39;elaborazione di un processo quando si verifica un errore, assegnare `false` al `AssemblerOptionSpec` dell&#39;oggetto `failOnError` membro dati.

1. Assemblare il documento PDF.

   Richiama `AssemblerServiceClient` dell&#39;oggetto `invokeOneDocument` e trasmettere i seguenti valori:

   * A `BLOB` oggetto che rappresenta il documento DDX
   * A `BLOB` oggetto che rappresenta il documento interattivo PDF
   * Un `AssemblerOptionSpec` oggetto che specifica le opzioni di runtime

   Il `invokeOneDocument` il metodo restituisce un `BLOB` oggetto contenente un documento PDF non interattivo.

1. Salva il documento PDF non interattivo.

   * Creare un `System.IO.FileStream` richiamando il costruttore e passando un valore stringa che rappresenta la posizione del file del documento PDF non interattivo e la modalità di apertura del file in.
   * Creare una matrice di byte che memorizza il contenuto della `BLOB` oggetto che `invokeOneDocument` metodo restituito. Popolare la matrice di byte ottenendo il valore della `BLOB` dell&#39;oggetto `MTOM` campo.
   * Creare un `System.IO.BinaryWriter` oggetto richiamando il relativo costruttore e passando il `System.IO.FileStream` oggetto.
   * Scrivere il contenuto della matrice di byte in un file PDF richiamando `System.IO.BinaryWriter` dell&#39;oggetto `Write` e passando la matrice di byte.

* &quot;Guida rapida (MTOM): assemblaggio di un documento PDF non interattivo tramite l’API del servizio web&quot;.

**Consulta anche**

[Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
