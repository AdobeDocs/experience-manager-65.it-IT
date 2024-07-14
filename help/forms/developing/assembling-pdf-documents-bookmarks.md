---
title: Assemblaggio di documenti PDF con segnalibri
description: Utilizzare il servizio Assembler per modificare un documento di PDF che contiene segnalibri per includere segnalibri utilizzando l'API Java e l'API del servizio Web.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 2b938410-f51b-420b-b5d4-2ed13ec29c5a
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '2519'
ht-degree: 0%

---

# Assemblaggio di documenti PDF con segnalibri {#assembling-pdf-documents-with-bookmarks}

**Gli esempi e gli esempi contenuti in questo documento sono solo per AEM Forms in ambiente JEE.**

È possibile assemblare un documento PDF contenente segnalibri. Si supponga, ad esempio, di disporre di un documento PDF che non contiene segnalibri e di voler modificarlo fornendo segnalibri. Utilizzando il servizio Assembler, è possibile passare un documento PDF che non contiene segnalibri e restituire un documento PDF che contiene segnalibri.

I segnalibri contengono le seguenti proprietà:

* Titolo visualizzato come testo sullo schermo.
* Azione che specifica cosa accade quando un utente fa clic sul segnalibro. L&#39;azione tipica di un segnalibro consiste nello spostamento in un&#39;altra posizione nel documento corrente o nell&#39;apertura di un altro documento PDF, anche se è possibile specificare altre azioni.

Ai fini della presente discussione, si supponga che venga utilizzato il seguente documento DDX.

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

All&#39;interno di questo documento DDX, si noti che all&#39;attributo di origine viene assegnato il valore `Loan.pdf`. Questo documento DDX specifica che un singolo documento PDF viene passato al servizio Assembler. Durante l&#39;assemblaggio di un documento PDF con segnalibri, è necessario specificare un documento XML segnalibro che descriva i segnalibri presenti nel documento risultante. Per specificare un documento XML segnalibro, verificare che l&#39;elemento `Bookmarks` sia specificato nel documento DDX.

In questo esempio di documento DDX, l&#39;elemento `Bookmarks` specifica `doc2` come valore. Questo valore indica che la mappa di input passata al servizio Assembler contiene una chiave denominata `doc2`. Il valore della chiave `doc2` è un valore `com.adobe.idp.Document` che rappresenta il documento XML segnalibro. Consultate &quot;Bookmarks Language&quot; in [Assembler Service e riferimento DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

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

All&#39;interno di questo documento XML segnalibro, notare l&#39;elemento Action che definisce l&#39;azione eseguita quando un utente fa clic sul segnalibro. Sotto l&#39;elemento Action è l&#39;elemento Launch che avvia applicazioni, come NotePad, e apre file, come i file PDF. Per aprire un file PDF, è necessario utilizzare l&#39;elemento File che specifica il file da aprire. Ad esempio, nel file XML del segnalibro specificato in questa sezione, il nome del file aperto è LoanDetails.pdf.

>[!NOTE]
>
>Per informazioni complete sulle azioni supportate, vedere &quot; `Action` element&quot; in [Assembler Service e DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63).

Dato il documento DDX specificato in questa sezione e il file XML dei segnalibri come input, il servizio Assembler assembla un documento PDF contenente i seguenti segnalibri.

![aw_bmark](assets/aw_aw_bmark.png)

Quando un utente fa clic sul segnalibro *Apri dettagli prestito*, viene aperto LoanDetails.pdf. Analogamente, quando l&#39;utente fa clic sul segnalibro *Avvia NotePad*, NotePad viene avviato.

>[!NOTE]
>
>Prima di leggere questa sezione, è consigliabile avere familiarità con l&#39;assemblaggio di documenti PDF utilizzando il servizio Assembler. In questa sezione non vengono descritti concetti quali la creazione di un oggetto raccolta contenente documenti di input o l&#39;apprendimento dell&#39;estrazione dei risultati dall&#39;oggetto raccolta restituito. (Vedi [Assemblaggio a livello di programmazione di documenti di PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md#programmatically-assembling-pdf-documents).)

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Assembler, vedere [Riferimento ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Per ulteriori informazioni su un documento DDX, vedere [Servizio assemblatore e riferimento DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Riepilogo dei passaggi {#summary-of-steps}

Per assemblare un documento PDF contenente segnalibri, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Creare un client PDF Assembler.
1. Fare riferimento a un documento DDX esistente.
1. Fare riferimento a un documento PDF a cui vengono aggiunti segnalibri.
1. Fare riferimento al documento XML segnalibro.
1. Aggiungere il documento PDF e il documento XML segnalibro a un insieme Map.
1. Impostare le opzioni di runtime.
1. Assemblare il documento PDF.
1. Salvare il documento PDF contenente i segnalibri.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso della classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è implementato su JBoss)
* jbossall-client.jar (obbligatorio se AEM Forms è distribuito su JBoss)

se AEM Forms viene distribuito su un server applicazioni J2EE supportato diverso da JBoss, è necessario sostituire i file adobe-utilities.jar e jbossall-client.jar con file JAR specifici per il server applicazioni J2EE su cui è distribuito AEM Forms. Per informazioni sulla posizione di tutti i file JAR di AEM Forms, vedi [Inclusi i file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un client Assembler PDF**

Prima di poter eseguire un&#39;operazione Assembler a livello di programmazione, è necessario creare un client del servizio Assembler.

**Riferimento a un documento DDX esistente**

Per assemblare un documento PDF è necessario fare riferimento a un documento DDX. Questo documento DDX deve contenere l&#39;elemento `Bookmarks`, che indica al servizio Assembler di assemblare un PDF contenente segnalibri. Per un esempio, vedere il documento DDX illustrato in precedenza in questa sezione.

**Riferimento a un documento PDF a cui sono aggiunti segnalibri**

Fare riferimento a un documento PDF a cui vengono aggiunti segnalibri. Non importa se il documento PDF a cui si fa riferimento contiene già segnalibri. Se l&#39;elemento `Bookmarks` è figlio dell&#39;elemento di origine PDF, i segnalibri sostituiranno quelli già esistenti nell&#39;origine PDF. Tuttavia, se desideri mantenere i segnalibri esistenti, assicurati che `Bookmarks` sia di pari livello dell&#39;elemento di origine PDF. Ad esempio, considera l’esempio seguente:

```xml
 <PDF result="foo">
      <PDF source="inDoc"/>
      <Bookmarks source="doc2"/>
 </PDF>
```

**Riferimento al documento XML segnalibro**

Per assemblare un PDF contenente nuovi segnalibri, è necessario fare riferimento a un documento XML segnalibro. Il documento XML segnalibro viene passato al servizio Assembler all&#39;interno dell&#39;insieme Map. Per un esempio, consultate il documento XML dei segnalibri mostrato in precedenza in questa sezione.

>[!NOTE]
>
>Consultare &quot;Bookmarks Language&quot; in [Assembler Service e DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63).

**Aggiungere il documento PDF e il documento XML segnalibro a una raccolta di mappe**

Aggiungere all&#39;insieme Map sia il documento PDF al quale vengono aggiunti segnalibri che il documento XML segnalibro. Pertanto, l&#39;insieme Map contiene due elementi: un documento PDF e il documento XML segnalibro.

**Impostare le opzioni di runtime**

È possibile impostare le opzioni di runtime che controllano il comportamento del servizio Assembler durante l&#39;esecuzione di un processo. È ad esempio possibile impostare un&#39;opzione che indichi al servizio Assembler di continuare l&#39;elaborazione di un processo in caso di errore. Per informazioni sulle opzioni di runtime che è possibile impostare, vedere il riferimento alla classe `AssemblerOptionSpec` in [Riferimento API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Assemblare il documento PDF**

Per assemblare un documento PDF contenente nuovi segnalibri, utilizzare l&#39;operazione `invokeDDX` del servizio Assembler. Il motivo per cui è necessario utilizzare l&#39;operazione `invokeDDX` rispetto ad altre operazioni del servizio Assembler come `invokeOneDocument` è che il servizio Assembler richiede un documento XML segnalibro passato all&#39;interno dell&#39;oggetto insieme Map. Questo oggetto è un parametro dell&#39;operazione `invokeDDX`.

**Salvare il documento PDF contenente i segnalibri**

Estrarre i risultati dall&#39;oggetto mappa restituito e salvare il documento PDF corrispondente. Consultare &quot;Estrarre i risultati&quot; in [Assemblaggio a livello di codice di documenti PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md).

**Consulta anche**

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Assemblaggio di documenti PDF a livello di programmazione](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Assemblare documenti PDF con segnalibri tramite API Java {#assemble-pdf-documents-with-bookmarks-using-the-java-api}

Assemblare un documento PDF con segnalibri utilizzando l&#39;API del servizio Assembler (Java):

1. Includi file di progetto.

   Includi i file JAR client, come adobe-assembler-client.jar, nel percorso di classe del progetto Java.

1. Creare un client PDF Assembler.

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione. (Vedere [Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * Creare un oggetto `AssemblerServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Fare riferimento a un documento DDX esistente.

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento DDX utilizzando il relativo costruttore e passando un valore stringa che specifica la posizione del file DDX.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Fare riferimento a un documento PDF a cui vengono aggiunti segnalibri.

   * Creare un oggetto `java.io.FileInputStream` utilizzando il relativo costruttore e passando il percorso del documento PDF.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passare l&#39;oggetto `java.io.FileInputStream` che contiene il documento PDF.

1. Fare riferimento al documento XML segnalibro.

   * Creare un oggetto `java.io.FileInputStream` utilizzando il relativo costruttore e passando il percorso del file XML che rappresenta il documento XML segnalibro.
   * Creare un oggetto `com.adobe.idp.Document` e passare l&#39;oggetto `java.io.FileInputStream` che contiene il documento PDF.

1. Aggiungere il documento PDF e il documento XML segnalibro a un insieme Map.

   * Creare un oggetto `java.util.Map` utilizzato per memorizzare sia il documento di input PDF che il documento XML segnalibro.
   * Aggiungere il documento di input PDF richiamando il metodo `put` dell&#39;oggetto `java.util.Map` e passando i seguenti argomenti:

      * Valore stringa che rappresenta il nome della chiave. Questo valore deve corrispondere al valore dell&#39;elemento di origine PDF specificato nel documento DDX.
      * Oggetto `com.adobe.idp.Document` contenente il documento PDF di input.

   * Aggiungere il documento XML segnalibro richiamando il metodo `put` dell&#39;oggetto `java.util.Map` e passando i seguenti argomenti:

      * Valore stringa che rappresenta il nome della chiave. Questo valore deve corrispondere al valore dell&#39;elemento di origine Segnalibri specificato nel documento DDX.
      * Oggetto `com.adobe.idp.Document` contenente il documento XML segnalibro.

1. Impostare le opzioni di runtime.

   * Creare un oggetto `AssemblerOptionSpec` che memorizza le opzioni di runtime utilizzando il relativo costruttore.
   * Impostare le opzioni di runtime per soddisfare i requisiti aziendali richiamando un metodo che appartiene all&#39;oggetto `AssemblerOptionSpec`. Ad esempio, per indicare al servizio Assembler di continuare a elaborare un processo quando si verifica un errore, richiamare il metodo `setFailOnError` dell&#39;oggetto `AssemblerOptionSpec` e passare `false`.

1. Assemblare il documento PDF.

   Richiama il metodo `invokeDDX` dell&#39;oggetto `AssemblerServiceClient` e passa i seguenti valori richiesti:

   * Oggetto `com.adobe.idp.Document` che rappresenta il documento DDX da utilizzare
   * Oggetto `java.util.Map` contenente sia il documento di input PDF che il documento XML segnalibro.
   * Oggetto `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` che specifica le opzioni di runtime, inclusi il tipo di carattere predefinito e il livello di registro del processo

   Il metodo `invokeDDX` restituisce un oggetto `com.adobe.livecycle.assembler.client.AssemblerResult` contenente i risultati del processo ed eventuali eccezioni.

1. Salvare il documento PDF contenente i segnalibri.

   Per ottenere il documento di PDF appena creato, effettuare le seguenti operazioni:

   * Richiama il metodo `getDocuments` dell&#39;oggetto `AssemblerResult`. Restituisce un oggetto `java.util.Map`.
   * Scorrere l&#39;oggetto `java.util.Map` fino a trovare l&#39;oggetto `com.adobe.idp.Document` risultante. È possibile utilizzare l&#39;elemento risultato PDF specificato nel documento DDX per ottenere il documento.
   * Richiama il metodo `copyToFile` dell&#39;oggetto `com.adobe.idp.Document` per estrarre il documento PDF.

**Consulta anche**

[Guida rapida (modalità SOAP): assemblaggio di documenti PDF con segnalibri tramite l’API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-pdf-documents-with-bookmarks-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Assemblare documenti PDF con segnalibri utilizzando l’API del servizio web {#assemble-pdf-documents-with-bookmarks-using-the-web-service-api}

Assemblare un documento PDF con segnalibri utilizzando l&#39;API del servizio Assembler (servizio Web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Creare un client PDF Assembler.

   * Creare un oggetto `AssemblerServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `AssemblerServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). Non è necessario utilizzare l&#39;attributo `lc_version`. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `AssemblerServiceClient.Endpoint.Binding`. Eseguire il cast del valore restituito in `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegnare il nome utente dei moduli AEM al campo `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Fare riferimento a un documento DDX esistente.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per archiviare il documento DDX.
   * Creare un oggetto `System.IO.FileStream` richiamandone il costruttore e passando un valore stringa che rappresenta la posizione del file del documento DDX e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni della matrice di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare la matrice di byte con i dati di flusso richiamando il metodo `Read` dell&#39;oggetto `System.IO.FileStream` e passando la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando il relativo campo `MTOM` al contenuto della matrice di byte.

1. Fare riferimento a un documento PDF a cui vengono aggiunti segnalibri.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare il PDF di input.
   * Creare un oggetto `System.IO.FileStream` richiamandone il costruttore e passando un valore stringa che rappresenta la posizione del file del documento PDF di input e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni della matrice di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare la matrice di byte con i dati di flusso richiamando il metodo `Read` dell&#39;oggetto `System.IO.FileStream` e passando la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando il relativo campo `MTOM` al contenuto della matrice di byte.

1. Fare riferimento al documento XML segnalibro.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare il documento XML segnalibro.
   * Creare un oggetto `System.IO.FileStream` richiamandone il costruttore e passando un valore stringa che rappresenta la posizione del file del documento PDF di input e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni della matrice di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare la matrice di byte con i dati di flusso richiamando il metodo `Read` dell&#39;oggetto `System.IO.FileStream` e passando la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando il relativo campo `MTOM` al contenuto della matrice di byte.

1. Aggiungere il documento PDF e il documento XML segnalibro a un insieme Map.

   * Creare un oggetto `MyMapOf_xsd_string_To_xsd_anyType`. Questo oggetto insieme viene utilizzato per memorizzare i documenti PDF di input e il documento XML segnalibro.
   * Per ogni documento di input PDF e per il documento XML segnalibro, creare un oggetto `MyMapOf_xsd_string_To_xsd_anyType_Item`.
   * Assegnare un valore stringa che rappresenta il nome chiave al campo `key` dell&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType_Item`. Questo valore deve corrispondere al valore dell&#39;elemento di origine PDF specificato nel documento DDX.
   * Assegnare l&#39;oggetto `BLOB` che memorizza il documento PDF al campo `value` dell&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType_Item`.
   * Aggiungere l&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType_Item` all&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType`. Richiama il metodo `Add` dell&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType` e passa l&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType`. (Eseguire questa operazione per ogni documento di input PDF e per il documento XML segnalibro.)

1. Impostare le opzioni di runtime.

   * Creare un oggetto `AssemblerOptionSpec` che memorizza le opzioni di runtime utilizzando il relativo costruttore.
   * Impostare le opzioni di runtime per soddisfare i requisiti aziendali assegnando un valore a un membro dati che appartiene all&#39;oggetto `AssemblerOptionSpec`. Ad esempio, per indicare al servizio Assembler di continuare a elaborare un processo quando si verifica un errore, assegnare `false` al membro dati `failOnError` dell&#39;oggetto `AssemblerOptionSpec`.

1. Assemblare il documento PDF.

   Richiama il metodo `invokeDDX` dell&#39;oggetto `AssemblerServiceClient` e passa i seguenti valori:

   * Oggetto `BLOB` che rappresenta il documento DDX
   * Array `MyMapOf_xsd_string_To_xsd_anyType` contenente i documenti di input
   * Oggetto `AssemblerOptionSpec` che specifica le opzioni di runtime

   Il metodo `invokeDDX` restituisce un oggetto `AssemblerResult` contenente i risultati del processo ed eventuali eccezioni.

1. Salvare il documento PDF contenente i segnalibri.

   Per ottenere il documento di PDF appena creato, effettuare le seguenti operazioni:

   * Accedere al campo `documents` dell&#39;oggetto `AssemblerResult`, che è un oggetto `Map` contenente i documenti PDF risultanti.
   * Scorrere l&#39;oggetto `Map` fino a trovare la chiave corrispondente al nome del documento risultante. Quindi esegui il cast di `value` del membro dell&#39;array in un `BLOB`.
   * Estrarre i dati binari che rappresentano il documento PDF accedendo al campo `MTOM` dell&#39;oggetto `BLOB`. Restituisce una matrice di byte che è possibile scrivere in un file PDF.

**Consulta anche**

[Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
