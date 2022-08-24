---
title: Assemblaggio di documenti PDF con segnalibri
seo-title: Assembling PDF Documents with Bookmarks
description: Utilizzare il servizio Assembler per modificare un documento PDF che contiene segnalibri per includere segnalibri utilizzando l'API Java e l'API Web Service.
seo-description: Use the Assembler service to modify a PDF document that does contain bookmarks to include bookmarks using the Java API and the Web Service API.
uuid: a306d2a6-0b12-4eb3-bff4-968a33417486
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9f4711a8-033c-4051-ab41-65a26838899b
role: Developer
exl-id: 2b938410-f51b-420b-b5d4-2ed13ec29c5a
source-git-commit: 135f50cc80f8bb449b2f1621db5e2564f5075968
workflow-type: tm+mt
source-wordcount: '2558'
ht-degree: 0%

---

# Assemblaggio di documenti PDF con segnalibri {#assembling-pdf-documents-with-bookmarks}

**Esempi ed esempi in questo documento sono solo per AEM Forms in ambiente JEE.**

È possibile assemblare un documento PDF contenente segnalibri. Ad esempio, si supponga di disporre di un documento PDF che non contiene segnalibri e si desidera modificarlo fornendo segnalibri. Utilizzando il servizio Assembler, è possibile passare un documento PDF che non contiene segnalibri e recuperare un documento PDF che contiene segnalibri.

I segnalibri contengono le seguenti proprietà:

* Titolo visualizzato come testo sullo schermo.
* Un&#39;azione che specifica cosa accade quando un utente fa clic sul segnalibro. L&#39;azione tipica di un segnalibro consiste nello spostamento in un&#39;altra posizione del documento corrente o nell&#39;aprire un altro documento PDF, anche se è possibile specificare altre azioni.

Ai fini di questa discussione, si supponga che venga utilizzato il seguente documento DDX.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
       <PDF result="FinalDoc.pdf">
          <PDF source="Loan.pdf">
             <Bookmarks source="doc2" />
          </PDF>
       </PDF>
 </DDX>
```

In questo documento DDX, notare che all&#39;attributo di origine è assegnato il valore `Loan.pdf`. Questo documento DDX specifica che un singolo documento PDF viene passato al servizio Assembler. Quando si assembla un documento PDF con segnalibri, è necessario specificare un documento XML con segnalibro che descrive i segnalibri nel documento risultante. Per specificare un documento XML di segnalibro, assicurarsi che il `Bookmarks` è specificato nel documento DDX.

In questo documento DDX di esempio, il `Bookmarks` element specifica `doc2` come valore. Questo valore indica che la mappa di input passata al servizio Assembler contiene una chiave denominata `doc2`. Il valore del `doc2` la chiave è `com.adobe.idp.Document` che rappresenta il documento XML del segnalibro. (Consultare &quot;Lingua dei segnalibri&quot; nella sezione [Servizio di assemblaggio e riferimento DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).)

In questo argomento viene utilizzato il seguente linguaggio di segnalibri XML per assemblare un documento PDF contenente segnalibri.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <Bookmarks xmlns="https://ns.adobe.com/pdf/bookmarks" version="1.0">
       <Bookmark>
          <Action>
             <Launch NewWindow="true">
                <File Name="C:\Adobe\LoanDetails.pdf" />
             </Launch>
          </Action>
         <Title>Open the Loan document</Title>
       </Bookmark>
 <Bookmark>
          <Action>
             <Launch>
                <Win Name="C:\WINDOWS\notepad.exe" />
             </Launch>
          </Action>
     <Title>Launch NotePad</Title>
       </Bookmark>
 </Bookmarks>
```

In questo documento XML del segnalibro, notare l&#39;elemento Action che definisce l&#39;azione eseguita quando un utente fa clic sul segnalibro. Sotto l&#39;elemento Action è l&#39;elemento Launch che avvia applicazioni, come NotePad e apre file, come i file PDF. Per aprire un file PDF, è necessario utilizzare l’elemento File che specifica il file da aprire. Ad esempio, nel file XML del segnalibro specificato in questa sezione, il nome del file aperto è LoanDetails.pdf.

>[!NOTE]
>
>Per informazioni complete sulle azioni supportate, vedi &quot; `Action` &quot; nel [Servizio di assemblaggio e riferimento DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

Dato il documento DDX specificato in questa sezione e il file XML del segnalibro come input, il servizio Assembler assembla un documento PDF contenente i seguenti segnalibri.

![aw_aw_bmark](assets/aw_aw_bmark.png)

Quando un utente fa clic sul pulsante *Apri i dettagli del prestito* viene aperto il file LoanDetails.pdf. Allo stesso modo, quando l&#39;utente fa clic sul *Avvia NotePad* segnalibro, NotePad viene avviato.

>[!NOTE]
>
>Prima di leggere questa sezione, è consigliabile avere familiarità con l’assemblaggio di documenti PDF tramite il servizio Assembler. In questa sezione non vengono descritti i concetti, ad esempio la creazione di un oggetto raccolta contenente documenti di input o l&#39;apprendimento della modalità di estrazione dei risultati dall&#39;oggetto di raccolta restituito. (Vedi [Assemblaggio di documenti PDF a livello di programmazione](/help/forms/developing/programmatically-assembling-pdf-documents.md#programmatically-assembling-pdf-documents).)

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Assembler, vedere [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Per ulteriori informazioni su un documento DDX, consulta [Servizio di assemblaggio e riferimento DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Riepilogo dei passaggi {#summary-of-steps}

Per assemblare un documento PDF contenente segnalibri, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Creare un client PDF Assembler.
1. Fai riferimento a un documento DDX esistente.
1. Fare riferimento a un documento PDF a cui vengono aggiunti i segnalibri.
1. Fare riferimento al documento XML del segnalibro.
1. Aggiungere il documento PDF e il documento XML del segnalibro a una raccolta Mappa.
1. Impostare le opzioni di esecuzione.
1. Assemblare il documento PDF.
1. Salvare il documento PDF contenente segnalibri.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso della classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è distribuito su JBoss)
* jbossall-client.jar (richiesto se AEM Forms è distribuito su JBoss)

se AEM Forms è implementato su un server applicazioni J2EE supportato diverso da JBoss, è necessario sostituire i file adobe-utilities.jar e jbossall-client.jar con file JAR specifici per il server applicazioni J2EE in cui è implementato AEM Forms. Per informazioni sulla posizione di tutti i file JAR di AEM Forms, vedi [Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un client PDF Assembler**

Prima di poter eseguire un&#39;operazione Assembler a livello di programmazione, è necessario creare un client di servizio Assembler.

**Riferimento a un documento DDX esistente**

Per assemblare un documento PDF è necessario fare riferimento a un documento DDX. Questo documento DDX deve contenere `Bookmarks` che indica al servizio Assembler di assemblare un PDF che contiene segnalibri. Per un esempio, vedere il documento DDX mostrato in precedenza in questa sezione.

**Riferimento a un documento PDF a cui vengono aggiunti i segnalibri**

Fare riferimento a un documento PDF a cui vengono aggiunti i segnalibri. Non importa se il documento PDF a cui si fa riferimento contiene già dei segnalibri. Se la `Bookmarks` è un elemento secondario dell’elemento sorgente di PDF, quindi i segnalibri sostituiranno quelli già esistenti nell’origine di PDF. Tuttavia, se desideri mantenere i segnalibri esistenti, assicurati che `Bookmarks` è un elemento di pari livello dell’elemento sorgente di PDF. Ad esempio, considera l’esempio seguente:

```xml
 <PDF result="foo">
      <PDF source="inDoc"/>
      <Bookmarks source="doc2"/>
 </PDF>
```

**Riferimento al documento XML del segnalibro**

Per assemblare un PDF che contiene nuovi segnalibri, è necessario fare riferimento a un documento XML di segnalibro. Il documento XML del segnalibro viene passato al servizio Assembler all&#39;interno dell&#39;oggetto raccolta Mappa. Per un esempio, vedere il documento XML del segnalibro mostrato in precedenza in questa sezione.

>[!NOTE]
>
>Consultare &quot;Lingua dei segnalibri&quot; nella sezione [Servizio di assemblaggio e riferimento DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

**Aggiungere il documento PDF e il documento XML del segnalibro a una raccolta Mappa**

È necessario aggiungere all&#39;insieme Map sia il documento PDF a cui vengono aggiunti i segnalibri sia il documento XML dei segnalibri. Pertanto, l&#39;oggetto raccolta Mappa contiene due elementi: un documento PDF e il documento XML del segnalibro.

**Impostare le opzioni di esecuzione**

È possibile impostare le opzioni di esecuzione che controllano il comportamento del servizio Assembler mentre esegue un processo. Ad esempio, è possibile impostare un&#39;opzione che indica al servizio Assembler di continuare l&#39;elaborazione di un processo in caso di errore. Per informazioni sulle opzioni di esecuzione che è possibile impostare, vedere la `AssemblerOptionSpec` riferimento di classe in [Riferimento API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Assemblare il documento PDF**

Per assemblare un documento PDF contenente nuovi segnalibri, utilizzare il servizio Assembler `invokeDDX` funzionamento. Il motivo per cui devi utilizzare il `invokeDDX` funzionamento a differenza di altre operazioni di servizio Assembler, come `invokeOneDocument` è perché il servizio Assembler richiede un documento XML del segnalibro passato all&#39;interno dell&#39;oggetto raccolta Map. Questo oggetto è un parametro del `invokeDDX` funzionamento.

**Salvare il documento PDF contenente segnalibri**

È necessario estrarre i risultati dall’oggetto mappa restituito e salvare il documento PDF corrispondente. (Vedi &quot;Estrarre i risultati&quot; in [Assemblaggio di documenti PDF a livello di programmazione](/help/forms/developing/programmatically-assembling-pdf-documents.md).)

**Consulta anche**

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Assemblaggio di documenti PDF a livello di programmazione](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Assemblare documenti PDF con segnalibri utilizzando l’API Java {#assemble-pdf-documents-with-bookmarks-using-the-java-api}

Assemblare un documento PDF con segnalibri utilizzando l&#39;API del servizio Assembler (Java):

1. Includi file di progetto.

   Includi file JAR client, come adobe-assembler-client.jar, nel percorso di classe del progetto Java.

1. Creare un client PDF Assembler.

   * Crea un `ServiceClientFactory` oggetto contenente le proprietà di connessione. (Vedi [Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * Crea un `AssemblerServiceClient` utilizzando il relativo costruttore e passando `ServiceClientFactory` oggetto.

1. Fai riferimento a un documento DDX esistente.

   * Crea un `java.io.FileInputStream` oggetto che rappresenta il documento DDX utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del file DDX.
   * Crea un `com.adobe.idp.Document` utilizzando il relativo costruttore e passando `java.io.FileInputStream` oggetto.

1. Fare riferimento a un documento PDF a cui vengono aggiunti i segnalibri.

   * Crea un `java.io.FileInputStream` utilizzando il relativo costruttore e passando la posizione del documento PDF.
   * Crea un `com.adobe.idp.Document` utilizzando il relativo costruttore e passando `java.io.FileInputStream` oggetto contenente il documento PDF.

1. Fare riferimento al documento XML del segnalibro.

   * Crea un `java.io.FileInputStream` utilizzando il relativo costruttore e passando la posizione del file XML che rappresenta il documento XML del segnalibro.
   * Crea un `com.adobe.idp.Document` e passare `java.io.FileInputStream` oggetto contenente il documento PDF.

1. Aggiungere il documento PDF e il documento XML del segnalibro a una raccolta Mappa.

   * Crea un `java.util.Map` oggetto utilizzato per memorizzare sia il documento PDF di input che il documento XML del segnalibro.
   * Aggiungi il documento di input PDF richiamando il `java.util.Map` dell’oggetto `put` e passare gli argomenti seguenti:

      * Valore stringa che rappresenta il nome della chiave. Questo valore deve corrispondere al valore dell&#39;elemento di origine PDF specificato nel documento DDX.
      * A `com.adobe.idp.Document` oggetto contenente il documento di input PDF.
   * Aggiungi il documento XML del segnalibro richiamando il `java.util.Map` dell’oggetto `put` e passare gli argomenti seguenti:

      * Valore stringa che rappresenta il nome della chiave. Questo valore deve corrispondere al valore dell&#39;elemento di origine Segnalibri specificato nel documento DDX.
      * A `com.adobe.idp.Document` oggetto che contiene il documento XML del segnalibro.


1. Impostare le opzioni di esecuzione.

   * Crea un `AssemblerOptionSpec` oggetto che memorizza le opzioni di esecuzione utilizzando il relativo costruttore.
   * Impostare le opzioni di esecuzione per soddisfare i requisiti aziendali richiamando un metodo che appartiene al `AssemblerOptionSpec` oggetto. Ad esempio, per dare istruzioni al servizio Assembler di continuare a elaborare un processo quando si verifica un errore, richiama il `AssemblerOptionSpec` dell’oggetto `setFailOnError` metodo e passaggio `false`.

1. Assemblare il documento PDF.

   Richiama il `AssemblerServiceClient` dell’oggetto `invokeDDX` e trasmettere i seguenti valori richiesti:

   * A `com.adobe.idp.Document` oggetto che rappresenta il documento DDX da utilizzare
   * A `java.util.Map` oggetto contenente sia il documento PDF di input che il documento XML del segnalibro.
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` oggetto che specifica le opzioni di esecuzione, incluso il tipo di carattere predefinito e il livello di log del processo

   La `invokeDDX` restituisce un `com.adobe.livecycle.assembler.client.AssemblerResult` oggetto contenente i risultati del processo ed eventuali eccezioni.

1. Salvare il documento PDF contenente segnalibri.

   Per ottenere il documento PDF appena creato, eseguire le operazioni seguenti:

   * Richiama il `AssemblerResult` dell’oggetto `getDocuments` metodo . Questo restituisce un `java.util.Map` oggetto.
   * Itera attraverso il `java.util.Map` finché non trovi il risultato `com.adobe.idp.Document` oggetto. Per ottenere il documento è possibile utilizzare l&#39;elemento risultato di PDF specificato nel documento DDX.
   * Richiama il `com.adobe.idp.Document` dell’oggetto `copyToFile` per estrarre il documento PDF.

**Consulta anche**

[Avvio rapido (modalità SOAP): Assemblaggio di documenti PDF con segnalibri tramite API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-pdf-documents-with-bookmarks-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Assemblare documenti PDF con segnalibri utilizzando l’API del servizio Web {#assemble-pdf-documents-with-bookmarks-using-the-web-service-api}

Assemblare un documento PDF con segnalibri utilizzando l&#39;API del servizio Assembler (servizio Web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurati di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l’indirizzo IP del server che ospita AEM Forms.

1. Creare un client PDF Assembler.

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
   * Crea un `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento DDX e la modalità in cui aprire il file.
   * Creare un array di byte che memorizza il contenuto del `System.IO.FileStream` oggetto. È possibile determinare le dimensioni dell&#39;array di byte ottenendo il `System.IO.FileStream` dell’oggetto `Length` proprietà.
   * Compilare l&#39;array di byte con i dati del flusso richiamando il `System.IO.FileStream` dell’oggetto `Read` e passare l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare `BLOB` oggetto assegnando il relativo `MTOM` con il contenuto dell&#39;array di byte.

1. Fare riferimento a un documento PDF a cui vengono aggiunti i segnalibri.

   * Crea un `BLOB` utilizzando il relativo costruttore. La `BLOB` viene utilizzato per memorizzare il PDF di input.
   * Crea un `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento di input PDF e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto del `System.IO.FileStream` oggetto. È possibile determinare le dimensioni dell&#39;array di byte ottenendo il `System.IO.FileStream` dell’oggetto `Length` proprietà.
   * Compilare l&#39;array di byte con i dati del flusso richiamando il `System.IO.FileStream` dell’oggetto `Read` e passare l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare `BLOB` oggetto assegnando il relativo `MTOM` con il contenuto dell&#39;array di byte.

1. Fare riferimento al documento XML del segnalibro.

   * Crea un `BLOB` utilizzando il relativo costruttore. La `BLOB` viene utilizzato per memorizzare il documento XML del segnalibro.
   * Crea un `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento di input PDF e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto del `System.IO.FileStream` oggetto. È possibile determinare le dimensioni dell&#39;array di byte ottenendo il `System.IO.FileStream` dell’oggetto `Length` proprietà.
   * Compilare l&#39;array di byte con i dati del flusso richiamando il `System.IO.FileStream` dell’oggetto `Read` e passare l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare `BLOB` oggetto assegnando il relativo `MTOM` con il contenuto dell&#39;array di byte.

1. Aggiungere il documento PDF e il documento XML del segnalibro a una raccolta Mappa.

   * Crea un `MyMapOf_xsd_string_To_xsd_anyType` oggetto. Questo oggetto raccolta viene utilizzato per memorizzare i documenti PDF di input e il documento XML del segnalibro.
   * Per ogni documento PDF di input e documento XML del segnalibro , crea un `MyMapOf_xsd_string_To_xsd_anyType_Item` oggetto.
   * Assegna un valore stringa che rappresenta il nome della chiave al `MyMapOf_xsd_string_To_xsd_anyType_Item` dell&#39;oggetto `key` campo . Questo valore deve corrispondere al valore dell&#39;elemento di origine PDF specificato nel documento DDX.
   * Assegna `BLOB` oggetto che memorizza il documento PDF nella `MyMapOf_xsd_string_To_xsd_anyType_Item` dell&#39;oggetto `value` campo .
   * Aggiungi il `MyMapOf_xsd_string_To_xsd_anyType_Item` dell&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType` oggetto. Richiama il `MyMapOf_xsd_string_To_xsd_anyType` dell&#39;oggetto `Add` e passare il `MyMapOf_xsd_string_To_xsd_anyType` oggetto. Eseguire questa operazione per ogni documento PDF di input e per il documento XML del segnalibro.

1. Impostare le opzioni di esecuzione.

   * Crea un `AssemblerOptionSpec` oggetto che memorizza le opzioni di esecuzione utilizzando il relativo costruttore.
   * Impostare le opzioni di esecuzione per soddisfare i requisiti aziendali assegnando un valore a un membro dati che appartiene al `AssemblerOptionSpec` oggetto. Ad esempio, per dare istruzioni al servizio Assembler di continuare a elaborare un processo quando si verifica un errore, assegnare `false` al `AssemblerOptionSpec` dell’oggetto `failOnError` membro dati.

1. Assemblare il documento PDF.

   Richiama il `AssemblerServiceClient` dell’oggetto `invokeDDX` e passare i seguenti valori:

   * A `BLOB` oggetto che rappresenta il documento DDX
   * La `MyMapOf_xsd_string_To_xsd_anyType` array contenente i documenti di input
   * Un `AssemblerOptionSpec` oggetto che specifica le opzioni di esecuzione

   La `invokeDDX` restituisce un `AssemblerResult` oggetto contenente i risultati del processo ed eventuali eccezioni.

1. Salvare il documento PDF contenente segnalibri.

   Per ottenere il documento PDF appena creato, eseguire le operazioni seguenti:

   * Accedere al `AssemblerResult` dell’oggetto `documents` un campo `Map` oggetto contenente i documenti PDF risultanti.
   * Itera attraverso il `Map` finché non viene trovata la chiave che corrisponde al nome del documento risultante. Quindi eseguire il cast del membro della matrice `value` a `BLOB`.
   * Estrarre i dati binari che rappresentano il documento PDF accedendo ai relativi `BLOB` dell’oggetto `MTOM` campo . Restituisce una matrice di byte che è possibile scrivere in un file PDF.

**Consulta anche**

[Richiamo di AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
