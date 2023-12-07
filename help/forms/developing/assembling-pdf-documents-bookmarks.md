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
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '2519'
ht-degree: 0%

---

# Assemblaggio di documenti PDF con segnalibri {#assembling-pdf-documents-with-bookmarks}

**Gli esempi e gli esempi contenuti in questo documento sono solo per l’ambiente AEM Forms su JEE.**

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

All&#39;interno di questo documento DDX, si noti che all&#39;attributo di origine viene assegnato il valore `Loan.pdf`. Questo documento DDX specifica che un singolo documento PDF viene passato al servizio Assembler. Durante l&#39;assemblaggio di un documento PDF con segnalibri, è necessario specificare un documento XML segnalibro che descriva i segnalibri presenti nel documento risultante. Per specificare un documento XML segnalibro, assicurarsi che `Bookmarks` è specificato nel documento DDX.

In questo esempio di documento DDX, il `Bookmarks` specifica un elemento `doc2` come valore. Questo valore indica che la mappa di input passata al servizio Assembler contiene una chiave denominata `doc2`. Il valore della proprietà `doc2` la chiave è un `com.adobe.idp.Document` valore che rappresenta il documento XML segnalibro. (Consulta &quot;Lingua dei segnalibri&quot; in [Servizio assemblatore e riferimento DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).)

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
>Per informazioni complete sulle azioni supportate, vedi &quot; `Action` elemento&quot; nella [Servizio assemblatore e riferimento DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

Dato il documento DDX specificato in questa sezione e il file XML dei segnalibri come input, il servizio Assembler assembla un documento PDF contenente i seguenti segnalibri.

![aw_aw_bmark](assets/aw_aw_bmark.png)

Quando un utente fa clic su *Apri i dettagli del prestito* segnalibro, viene aperto LoanDetails.pdf. Analogamente, quando l’utente fa clic sul pulsante *Avvia Blocco note* segnalibro, NotePad viene avviato.

>[!NOTE]
>
>Prima di leggere questa sezione, è consigliabile avere familiarità con l&#39;assemblaggio di documenti PDF utilizzando il servizio Assembler. In questa sezione non vengono descritti concetti quali la creazione di un oggetto raccolta contenente documenti di input o l&#39;apprendimento dell&#39;estrazione dei risultati dall&#39;oggetto raccolta restituito. (vedere [Assemblaggio di documenti PDF a livello di programmazione](/help/forms/developing/programmatically-assembling-pdf-documents.md#programmatically-assembling-pdf-documents).)

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Assembler, vedere [Guida di riferimento dei servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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

se AEM Forms viene distribuito su un server applicazioni J2EE supportato diverso da JBoss, è necessario sostituire i file adobe-utilities.jar e jbossall-client.jar con file JAR specifici per il server applicazioni J2EE su cui è distribuito AEM Forms. Per informazioni sulla posizione di tutti i file JAR di AEM Forms, vedi [Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un client PDF Assembler**

Prima di poter eseguire un&#39;operazione Assembler a livello di programmazione, è necessario creare un client del servizio Assembler.

**Riferimento a un documento DDX esistente**

Per assemblare un documento PDF è necessario fare riferimento a un documento DDX. Questo documento DDX deve contenere `Bookmarks` che indica al servizio Assembler di assemblare un PDF contenente segnalibri. Per un esempio, vedere il documento DDX illustrato in precedenza in questa sezione.

**Fare riferimento a un documento PDF a cui vengono aggiunti segnalibri**

Fare riferimento a un documento PDF a cui vengono aggiunti segnalibri. Non importa se il documento PDF a cui si fa riferimento contiene già segnalibri. Se il `Bookmarks` è un elemento figlio dell&#39;elemento di origine PDF. I segnalibri sostituiranno quelli già esistenti nell&#39;origine PDF. Tuttavia, se si desidera mantenere i segnalibri esistenti, assicurarsi che `Bookmarks` è un elemento di pari livello dell’elemento sorgente PDF. Ad esempio, considera l’esempio seguente:

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
>Consulta &quot;Lingua dei segnalibri&quot; in [Servizio assemblatore e riferimento DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

**Aggiungere il documento PDF e il documento XML segnalibro a un insieme Map**

Aggiungere all&#39;insieme Map sia il documento PDF al quale vengono aggiunti segnalibri che il documento XML segnalibro. Pertanto, l&#39;insieme Map contiene due elementi: un documento PDF e il documento XML segnalibro.

**Impostare le opzioni di runtime**

È possibile impostare le opzioni di runtime che controllano il comportamento del servizio Assembler durante l&#39;esecuzione di un processo. È ad esempio possibile impostare un&#39;opzione che indichi al servizio Assembler di continuare l&#39;elaborazione di un processo in caso di errore. Per informazioni sulle opzioni di runtime impostabili, vedere `AssemblerOptionSpec` riferimento di classe in [Riferimento API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Assemblare il documento PDF**

Per assemblare un documento PDF contenente nuovi segnalibri, utilizzare il `invokeDDX` operazione. Il motivo per cui è necessario utilizzare `invokeDDX` rispetto ad altre operazioni del servizio Assembler, come `invokeOneDocument` è perché il servizio Assembler richiede un documento XML segnalibro passato all&#39;interno dell&#39;insieme Map. Questo oggetto è un parametro di `invokeDDX` operazione.

**Salva il documento PDF contenente i segnalibri**

Estrarre i risultati dall&#39;oggetto mappa restituito e salvare il documento PDF corrispondente. (Consulta &quot;Estrarre i risultati&quot; in [Assemblaggio di documenti PDF a livello di programmazione](/help/forms/developing/programmatically-assembling-pdf-documents.md).)

**Consulta anche**

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Assemblaggio di documenti PDF a livello di programmazione](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Assemblare documenti PDF con segnalibri tramite API Java {#assemble-pdf-documents-with-bookmarks-using-the-java-api}

Assemblare un documento PDF con segnalibri utilizzando l&#39;API del servizio Assembler (Java):

1. Includi file di progetto.

   Includi i file JAR client, come adobe-assembler-client.jar, nel percorso di classe del progetto Java.

1. Creare un client PDF Assembler.

   * Creare un `ServiceClientFactory` oggetto che contiene proprietà di connessione. (vedere [Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * Creare un `AssemblerServiceClient` mediante il costruttore e passando il `ServiceClientFactory` oggetto.

1. Fare riferimento a un documento DDX esistente.

   * Creare un `java.io.FileInputStream` oggetto che rappresenta il documento DDX utilizzando il relativo costruttore e passando un valore stringa che specifica la posizione del file DDX.
   * Creare un `com.adobe.idp.Document` mediante il costruttore e passando il `java.io.FileInputStream` oggetto.

1. Fare riferimento a un documento PDF a cui vengono aggiunti segnalibri.

   * Creare un `java.io.FileInputStream` mediante il costruttore e passando la posizione del documento PDF.
   * Creare un `com.adobe.idp.Document` mediante il costruttore e passare il `java.io.FileInputStream` oggetto che contiene il documento PDF.

1. Fare riferimento al documento XML segnalibro.

   * Creare un `java.io.FileInputStream` mediante il costruttore e passando la posizione del file XML che rappresenta il documento XML segnalibro.
   * Creare un `com.adobe.idp.Document` e passare il `java.io.FileInputStream` oggetto che contiene il documento PDF.

1. Aggiungere il documento PDF e il documento XML segnalibro a un insieme Map.

   * Creare un `java.util.Map` oggetto utilizzato per memorizzare sia il documento di input PDF che il documento XML segnalibro.
   * Aggiungere il documento di input PDF richiamando `java.util.Map` dell&#39;oggetto `put` e fornendo i seguenti argomenti:

      * Valore stringa che rappresenta il nome della chiave. Questo valore deve corrispondere al valore dell&#39;elemento di origine PDF specificato nel documento DDX.
      * A `com.adobe.idp.Document` oggetto che contiene il documento di input PDF.

   * Aggiungere il documento XML segnalibro richiamando `java.util.Map` dell&#39;oggetto `put` e fornendo i seguenti argomenti:

      * Valore stringa che rappresenta il nome della chiave. Questo valore deve corrispondere al valore dell&#39;elemento di origine Segnalibri specificato nel documento DDX.
      * A `com.adobe.idp.Document` oggetto che contiene il documento XML segnalibro.

1. Impostare le opzioni di runtime.

   * Creare un `AssemblerOptionSpec` oggetto che memorizza le opzioni di runtime mediante il relativo costruttore.
   * Impostare le opzioni di runtime per soddisfare i requisiti aziendali richiamando un metodo che appartiene al `AssemblerOptionSpec` oggetto. Ad esempio, per indicare al servizio Assembler di continuare l&#39;elaborazione di un processo quando si verifica un errore, richiamare `AssemblerOptionSpec` dell&#39;oggetto `setFailOnError` metodo e passaggio `false`.

1. Assemblare il documento PDF.

   Richiama `AssemblerServiceClient` dell&#39;oggetto `invokeDDX` e trasmettere i seguenti valori richiesti:

   * A `com.adobe.idp.Document` oggetto che rappresenta il documento DDX da utilizzare
   * A `java.util.Map` oggetto che contiene sia il documento di input PDF che il documento XML segnalibro.
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` oggetto che specifica le opzioni di runtime, incluso il tipo di carattere predefinito e il livello di registro del processo

   Il `invokeDDX` il metodo restituisce un `com.adobe.livecycle.assembler.client.AssemblerResult` oggetto contenente i risultati del processo ed eventuali eccezioni verificatesi.

1. Salvare il documento PDF contenente i segnalibri.

   Per ottenere il documento di PDF appena creato, effettuare le seguenti operazioni:

   * Richiama `AssemblerResult` dell&#39;oggetto `getDocuments` metodo. Questo restituisce un `java.util.Map` oggetto.
   * Effettua iterazione attraverso `java.util.Map` finché non viene individuato il risultato `com.adobe.idp.Document` oggetto. È possibile utilizzare l&#39;elemento risultato PDF specificato nel documento DDX per ottenere il documento.
   * Richiama `com.adobe.idp.Document` dell&#39;oggetto `copyToFile` per estrarre il documento PDF.

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
   >Sostituisci `localhost` con l’indirizzo IP del server che ospita AEM Forms.

1. Creare un client PDF Assembler.

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
   * Creare un `System.IO.FileStream` richiamando il relativo costruttore e passando un valore stringa che rappresenta la posizione del file del documento DDX e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto della `System.IO.FileStream` oggetto. È possibile determinare le dimensioni della matrice di byte ottenendo `System.IO.FileStream` dell&#39;oggetto `Length` proprietà.
   * Compilare la matrice di byte con i dati di flusso richiamando `System.IO.FileStream` dell&#39;oggetto `Read` e passando la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare il `BLOB` oggetto assegnando il relativo `MTOM` con il contenuto della matrice di byte.

1. Fare riferimento a un documento PDF a cui vengono aggiunti segnalibri.

   * Creare un `BLOB` mediante il costruttore. Il `BLOB` viene utilizzato per memorizzare il PDF di input.
   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore stringa che rappresenta la posizione del file del documento di input PDF e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto della `System.IO.FileStream` oggetto. È possibile determinare le dimensioni della matrice di byte ottenendo `System.IO.FileStream` dell&#39;oggetto `Length` proprietà.
   * Compilare la matrice di byte con i dati di flusso richiamando `System.IO.FileStream` dell&#39;oggetto `Read` e passando la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare il `BLOB` oggetto assegnando il relativo `MTOM` con il contenuto della matrice di byte.

1. Fare riferimento al documento XML segnalibro.

   * Creare un `BLOB` mediante il costruttore. Il `BLOB` L&#39;oggetto viene utilizzato per memorizzare il documento XML segnalibro.
   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore stringa che rappresenta la posizione del file del documento di input PDF e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto della `System.IO.FileStream` oggetto. È possibile determinare le dimensioni della matrice di byte ottenendo `System.IO.FileStream` dell&#39;oggetto `Length` proprietà.
   * Compilare la matrice di byte con i dati di flusso richiamando `System.IO.FileStream` dell&#39;oggetto `Read` e passando la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare il `BLOB` oggetto assegnando il relativo `MTOM` con il contenuto della matrice di byte.

1. Aggiungere il documento PDF e il documento XML segnalibro a un insieme Map.

   * Creare un `MyMapOf_xsd_string_To_xsd_anyType` oggetto. Questo oggetto insieme viene utilizzato per memorizzare i documenti PDF di input e il documento XML segnalibro.
   * Per ogni documento di input PDF e il documento XML del segnalibro, crea un `MyMapOf_xsd_string_To_xsd_anyType_Item` oggetto.
   * Assegna un valore stringa che rappresenta il nome della chiave al `MyMapOf_xsd_string_To_xsd_anyType_Item` dell&#39;oggetto `key` campo. Questo valore deve corrispondere al valore dell&#39;elemento di origine PDF specificato nel documento DDX.
   * Assegna la `BLOB` oggetto che memorizza il documento PDF in `MyMapOf_xsd_string_To_xsd_anyType_Item` dell&#39;oggetto `value` campo.
   * Aggiungi il `MyMapOf_xsd_string_To_xsd_anyType_Item` oggetto al `MyMapOf_xsd_string_To_xsd_anyType` oggetto. Richiama `MyMapOf_xsd_string_To_xsd_anyType` dell&#39;oggetto `Add` e trasmettere il `MyMapOf_xsd_string_To_xsd_anyType` oggetto. (Eseguire questa operazione per ogni documento di input PDF e per il documento XML segnalibro.)

1. Impostare le opzioni di runtime.

   * Creare un `AssemblerOptionSpec` oggetto che memorizza le opzioni di runtime mediante il relativo costruttore.
   * Impostare le opzioni di runtime per soddisfare i requisiti aziendali assegnando un valore a un membro dati che appartiene al `AssemblerOptionSpec` oggetto. Ad esempio, per indicare al servizio Assembler di continuare l&#39;elaborazione di un processo quando si verifica un errore, assegnare `false` al `AssemblerOptionSpec` dell&#39;oggetto `failOnError` membro dati.

1. Assemblare il documento PDF.

   Richiama `AssemblerServiceClient` dell&#39;oggetto `invokeDDX` e trasmettere i seguenti valori:

   * A `BLOB` oggetto che rappresenta il documento DDX
   * Il `MyMapOf_xsd_string_To_xsd_anyType` array contenente i documenti di input
   * Un `AssemblerOptionSpec` oggetto che specifica le opzioni di runtime

   Il `invokeDDX` il metodo restituisce un `AssemblerResult` oggetto contenente i risultati del processo ed eventuali eccezioni.

1. Salvare il documento PDF contenente i segnalibri.

   Per ottenere il documento di PDF appena creato, effettuare le seguenti operazioni:

   * Accedere a `AssemblerResult` dell&#39;oggetto `documents` campo, che è un `Map` oggetto che contiene i documenti PDF risultanti.
   * Effettua iterazione attraverso `Map` finché non viene individuata la chiave corrispondente al nome del documento risultante. Quindi esegui il cast del membro di array `value` a un `BLOB`.
   * Estrarre i dati binari che rappresentano il documento PDF accedendo al relativo `BLOB` dell&#39;oggetto `MTOM` campo. Restituisce una matrice di byte che è possibile scrivere in un file PDF.

**Consulta anche**

[Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
