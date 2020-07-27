---
title: Assemblare documenti PDF con segnalibri
seo-title: Assemblare documenti PDF con segnalibri
description: 'null'
seo-description: 'null'
uuid: a306d2a6-0b12-4eb3-bff4-968a33417486
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9f4711a8-033c-4051-ab41-65a26838899b
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '2526'
ht-degree: 0%

---


# Assemblare documenti PDF con segnalibri {#assembling-pdf-documents-with-bookmarks}

È possibile assemblare un documento PDF contenente segnalibri. Ad esempio, si supponga di disporre di un documento PDF che non contenga segnalibri e si desidera modificarlo inserendo dei segnalibri. Il servizio Assembler consente di trasmettere un documento PDF che non contiene segnalibri e di recuperare un documento PDF contenente segnalibri.

I segnalibri contengono le proprietà seguenti:

* Titolo che viene visualizzato come testo sullo schermo.
* Azione che specifica cosa accade quando un utente fa clic sul segnalibro. L&#39;azione tipica di un segnalibro consiste nello spostamento in un&#39;altra posizione nel documento corrente o nell&#39;aprire un altro documento PDF, anche se è possibile specificare altre azioni.

Ai fini di questa discussione, si supponga di utilizzare il seguente documento DDX.

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

In questo documento DDX, si noti che all&#39;attributo di origine è assegnato il valore `Loan.pdf`. Questo documento DDX specifica che un singolo documento PDF viene passato al servizio Assembler. Quando si assembla un documento PDF con segnalibri, è necessario specificare un documento XML con segnalibri che descrive i segnalibri nel documento finale. Per specificare un documento XML del segnalibro, assicurarsi che l&#39; `Bookmarks` elemento sia specificato nel documento DDX.

In questo documento DDX di esempio, l&#39; `Bookmarks` elemento specifica `doc2` come valore. Questo valore indica che la mappa di input passata al servizio Assembler contiene una chiave denominata `doc2`. Il valore della `doc2` chiave è un `com.adobe.idp.Document` valore che rappresenta il documento XML del segnalibro. (vedere &quot;Linguaggio dei segnalibri&quot; nel servizio [Assembler e DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63).)

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

All&#39;interno di questo documento XML del segnalibro, si noti l&#39;elemento Action che definisce l&#39;azione eseguita quando un utente fa clic sul segnalibro. Sotto l&#39;elemento Azione è presente l&#39;elemento Launch che avvia applicazioni, come NotePad e apre file, come i file PDF. Per aprire un file PDF, è necessario utilizzare l&#39;elemento File che specifica il file da aprire. Ad esempio, nel file XML del segnalibro specificato in questa sezione, il nome del file aperto è LoanDetails.pdf.

>[!NOTE]
>
>Per informazioni complete sulle azioni supportate, vedere &quot; `Action` element&quot; (elemento) in Servizio [Assembler e Riferimento](https://www.adobe.com/go/learn_aemforms_ddx_63)DDX.

Dato il documento DDX specificato in questa sezione e il file XML del segnalibro come input, il servizio Assembler assembla un documento PDF contenente i seguenti segnalibri.

![aw_aw_bmark](assets/aw_aw_bmark.png)

Quando un utente fa clic sul segnalibro *Apri dettagli* prestito, viene aperto il file LoanDetails.pdf. Analogamente, quando l&#39;utente fa clic sul segnalibro *Avvia NotePad* , viene avviato NotePad.

>[!NOTE]
>
>Prima di leggere questa sezione, è consigliabile avere familiarità con l&#39;assemblaggio di documenti PDF tramite il servizio Assembler. In questa sezione non vengono discussi concetti, ad esempio la creazione di un oggetto raccolta che contiene documenti di input o l&#39;apprendimento di come estrarre i risultati dall&#39;oggetto raccolta restituito. (Vedere Assemblaggio [di documenti](/help/forms/developing/programmatically-assembling-pdf-documents.md#programmatically-assembling-pdf-documents)PDF a livello di programmazione.)

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Assembler, vedere Riferimento [servizi per i AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Per ulteriori informazioni su un documento DDX, vedere Servizio [Assembler e Riferimento](https://www.adobe.com/go/learn_aemforms_ddx_63)DDX.

## Riepilogo dei passaggi {#summary-of-steps}

Per assemblare un documento PDF contenente segnalibri, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un client Assembler PDF.
1. Fare riferimento a un documento DDX esistente.
1. Fare riferimento a un documento PDF al quale vengono aggiunti i segnalibri.
1. Fare riferimento al documento XML del segnalibro.
1. Aggiungere il documento PDF e il documento XML del segnalibro a una raccolta Mappa.
1. Impostare le opzioni di esecuzione.
1. Assemblare il documento PDF.
1. Salvare il documento PDF contenente i segnalibri.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, accertatevi di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (richiesto se i AEM Forms sono distribuiti su JBoss)
* jbossall-client.jar (richiesto se i AEM Forms sono distribuiti su JBoss)

se i AEM Forms sono distribuiti su un server applicazione J2EE supportato diverso da JBoss, è necessario sostituire i file adobe-utilities.jar e jbossall-client.jar con file JAR specifici del server applicazione J2EE in cui sono distribuiti i AEM Forms. Per informazioni sulla posizione di tutti i file JAR AEM Forms, vedere [Inclusione di file](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)libreria Java AEM Forms.

**Creare un client Assembler PDF**

Prima di eseguire un&#39;operazione Assembler a livello di programmazione, è necessario creare un client di servizio Assembler.

**Riferimento a un documento DDX esistente**

Per assemblare un documento PDF è necessario fare riferimento a un documento DDX. Questo documento DDX deve contenere l&#39; `Bookmarks` elemento, che richiede al servizio Assembler di assemblare un PDF contenente segnalibri. (Per un esempio, vedere il documento DDX illustrato in precedenza in questa sezione).

**Riferimento a un documento PDF al quale vengono aggiunti i segnalibri**

Fare riferimento a un documento PDF al quale vengono aggiunti i segnalibri. Non importa se il documento PDF di riferimento contiene già dei segnalibri. Se l&#39; `Bookmarks` elemento è un elemento secondario dell&#39;elemento sorgente PDF, i segnalibri sostituiranno quelli già esistenti nell&#39;origine PDF. Tuttavia, se si desidera mantenere i segnalibri esistenti, assicurarsi che `Bookmarks` sia un elemento di pari livello dell&#39;elemento sorgente PDF. Ad esempio, considerate quanto segue:

```xml
 <PDF result="foo">
      <PDF source="inDoc"/>
      <Bookmarks source="doc2"/>
 </PDF>
```

**Riferimento al documento XML del segnalibro**

Per assemblare un PDF contenente nuovi segnalibri, è necessario fare riferimento a un documento XML con segnalibro. Il documento XML del segnalibro viene passato al servizio Assembler all&#39;interno dell&#39;oggetto raccolta Map. (Per un esempio, vedere il documento XML del segnalibro illustrato in precedenza in questa sezione).

>[!NOTE]
>
>Vedere &quot;Bookmarks Language&quot; nel servizio [Assembler e DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63).

**Aggiungere il documento PDF e il documento XML del segnalibro a una raccolta Mappa**

È necessario aggiungere alla raccolta Mappa sia il documento PDF al quale vengono aggiunti i segnalibri, sia il documento XML del segnalibro. Pertanto, l&#39;oggetto insieme Map contiene due elementi: un documento PDF e il documento XML del segnalibro.

**Impostazione delle opzioni di esecuzione**

È possibile impostare opzioni di esecuzione che controllano il comportamento del servizio Assembler mentre esegue un processo. Ad esempio, potete impostare un&#39;opzione che indichi al servizio Assembler di continuare l&#39;elaborazione di un processo in caso di errore. Per informazioni sulle opzioni di esecuzione che è possibile impostare, vedere il riferimento alla `AssemblerOptionSpec` classe in Riferimento API per [AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Assemblare il documento PDF**

Per assemblare un documento PDF contenente nuovi segnalibri, utilizzare l&#39; `invokeDDX` operazione del servizio Assembler. Il motivo per cui è necessario utilizzare l&#39; `invokeDDX` operazione al posto di altre operazioni del servizio Assembler, ad esempio, `invokeOneDocument` è dovuto al fatto che il servizio Assembler richiede un documento XML con segnalibro passato all&#39;interno dell&#39;oggetto dell&#39;insieme Map. Questo oggetto è un parametro dell&#39; `invokeDDX` operazione.

**Salvare il documento PDF contenente i segnalibri**

È necessario estrarre i risultati dall&#39;oggetto mappa restituito e salvare il documento PDF corrispondente. (Vedere &quot;Estrai i risultati&quot; in Assemblaggio [di documenti](/help/forms/developing/programmatically-assembling-pdf-documents.md)PDF a livello di programmazione.)

**Consulta anche**

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Assemblaggio di documenti PDF a livello di programmazione](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Assemblare documenti PDF con segnalibri utilizzando l&#39;API Java {#assemble-pdf-documents-with-bookmarks-using-the-java-api}

Assemblate un documento PDF con segnalibri utilizzando l&#39;API di Assembler Service (Java):

1. Includere i file di progetto.

   Includete file JAR client, ad esempio adobe-assembler-client.jar, nel percorso di classe del progetto Java.

1. Creare un client Assembler PDF.

   * Creare un `ServiceClientFactory` oggetto che contenga proprietà di connessione. (Vedere [Impostazione delle proprietà](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)di connessione.)
   * Creare un `AssemblerServiceClient` oggetto utilizzando il relativo costruttore e passando l&#39; `ServiceClientFactory` oggetto.

1. Fare riferimento a un documento DDX esistente.

   * Creare un `java.io.FileInputStream` oggetto che rappresenta il documento DDX utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del file DDX.
   * Creare un `com.adobe.idp.Document` oggetto utilizzando il relativo costruttore e passando l&#39; `java.io.FileInputStream` oggetto.

1. Fare riferimento a un documento PDF al quale vengono aggiunti i segnalibri.

   * Creare un `java.io.FileInputStream` oggetto utilizzando il relativo costruttore e passando la posizione del documento PDF.
   * Creare un `com.adobe.idp.Document` oggetto utilizzando il relativo costruttore e passare l&#39; `java.io.FileInputStream` oggetto che contiene il documento PDF.

1. Fare riferimento al documento XML del segnalibro.

   * Creare un `java.io.FileInputStream` oggetto utilizzando il relativo costruttore e passando la posizione del file XML che rappresenta il documento XML del segnalibro.
   * Creare un `com.adobe.idp.Document` oggetto e passare l&#39; `java.io.FileInputStream` oggetto che contiene il documento PDF.

1. Aggiungere il documento PDF e il documento XML del segnalibro a una raccolta Mappa.

   * Creare un `java.util.Map` oggetto utilizzato per memorizzare sia il documento PDF di input che il documento XML del segnalibro.
   * Aggiungere il documento PDF di input richiamando il metodo dell&#39; `java.util.Map` oggetto `put` e passando gli argomenti seguenti:

      * Un valore di stringa che rappresenta il nome della chiave. Questo valore deve corrispondere al valore dell&#39;elemento di origine PDF specificato nel documento DDX.
      * Un `com.adobe.idp.Document` oggetto che contiene il documento PDF di input.
   * Aggiungere il documento XML del segnalibro richiamando il metodo dell&#39; `java.util.Map` oggetto `put` e passando gli argomenti seguenti:

      * Un valore di stringa che rappresenta il nome della chiave. Questo valore deve corrispondere al valore dell&#39;elemento di origine Segnalibri specificato nel documento DDX.
      * Un `com.adobe.idp.Document` oggetto che contiene il documento XML del segnalibro.


1. Impostare le opzioni di esecuzione.

   * Creare un `AssemblerOptionSpec` oggetto che memorizza le opzioni di esecuzione utilizzando il relativo costruttore.
   * Impostate le opzioni di runtime per soddisfare i requisiti aziendali richiamando un metodo che appartiene all&#39; `AssemblerOptionSpec` oggetto. Ad esempio, per indicare al servizio Assembler di continuare a elaborare un processo quando si verifica un errore, richiamare il metodo dell&#39; `AssemblerOptionSpec` oggetto `setFailOnError` e passare `false`.

1. Assemblare il documento PDF.

   Richiamare il metodo dell&#39; `AssemblerServiceClient` oggetto `invokeDDX` e trasmettere i seguenti valori obbligatori:

   * Un `com.adobe.idp.Document` oggetto che rappresenta il documento DDX da utilizzare
   * Un `java.util.Map` oggetto che contiene sia il documento PDF di input che il documento XML del segnalibro.
   * Un `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` oggetto che specifica le opzioni di esecuzione, incluso il font predefinito e il livello di registro del processo

   Il `invokeDDX` metodo restituisce un `com.adobe.livecycle.assembler.client.AssemblerResult` oggetto che contiene i risultati del processo ed eventuali eccezioni.

1. Salvare il documento PDF contenente i segnalibri.

   Per ottenere il documento PDF appena creato, effettuare le seguenti operazioni:

   * Richiama il metodo dell’ `AssemblerResult` oggetto `getDocuments` . Questo restituisce un `java.util.Map` oggetto.
   * Eseguire un&#39;iterazione sull&#39; `java.util.Map` oggetto fino a individuare l&#39; `com.adobe.idp.Document` oggetto risultante. Per ottenere il documento è possibile utilizzare l&#39;elemento risultato PDF specificato nel documento DDX.
   * Richiamare il metodo dell&#39; `com.adobe.idp.Document` oggetto `copyToFile` per estrarre il documento PDF.

**Consulta anche**

[Avvio rapido (modalità SOAP): Assemblare documenti PDF con segnalibri mediante l&#39;API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-pdf-documents-with-bookmarks-using-the-java-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Assemblare documenti PDF con segnalibri utilizzando l&#39;API del servizio Web {#assemble-pdf-documents-with-bookmarks-using-the-web-service-api}

Assemblate un documento PDF con segnalibri utilizzando l&#39;API di Assembler Service (servizio Web):

1. Includere i file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituire `localhost` con l&#39;indirizzo IP del server host AEM Forms.

1. Creare un client Assembler PDF.

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
   * Compilare l&#39;array di byte con i dati del flusso richiamando il `System.IO.FileStream` `Read` metodo dell&#39;oggetto e passando l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39; `BLOB` oggetto assegnandone `MTOM` il campo con il contenuto dell&#39;array di byte.

1. Fare riferimento a un documento PDF al quale vengono aggiunti i segnalibri.

   * Creare un `BLOB` oggetto utilizzando il relativo costruttore. L&#39; `BLOB` oggetto viene utilizzato per memorizzare il PDF di input.
   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF di input e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto dell&#39; `System.IO.FileStream` oggetto. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà dell&#39; `System.IO.FileStream` oggetto `Length` .
   * Compilare l&#39;array di byte con i dati del flusso richiamando il `System.IO.FileStream` `Read` metodo dell&#39;oggetto e passando l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39; `BLOB` oggetto assegnandone `MTOM` il campo con il contenuto dell&#39;array di byte.

1. Fare riferimento al documento XML del segnalibro.

   * Creare un `BLOB` oggetto utilizzando il relativo costruttore. L&#39; `BLOB` oggetto viene utilizzato per memorizzare il documento XML del segnalibro.
   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF di input e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto dell&#39; `System.IO.FileStream` oggetto. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà dell&#39; `System.IO.FileStream` oggetto `Length` .
   * Compilare l&#39;array di byte con i dati del flusso richiamando il `System.IO.FileStream` `Read` metodo dell&#39;oggetto e passando l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39; `BLOB` oggetto assegnandone `MTOM` il campo con il contenuto dell&#39;array di byte.

1. Aggiungere il documento PDF e il documento XML del segnalibro a una raccolta Mappa.

   * Create a `MyMapOf_xsd_string_To_xsd_anyType` object. Questo oggetto raccolta viene utilizzato per memorizzare i documenti PDF di input e il documento XML del segnalibro.
   * Per ciascun documento PDF di input e il documento XML del segnalibro, creare un `MyMapOf_xsd_string_To_xsd_anyType_Item` oggetto.
   * Assegnare un valore di stringa che rappresenta il nome chiave al campo dell&#39; `MyMapOf_xsd_string_To_xsd_anyType_Item` oggetto `key` . Questo valore deve corrispondere al valore dell&#39;elemento di origine PDF specificato nel documento DDX.
   * Assegnare l&#39; `BLOB` oggetto che memorizza il documento PDF nel campo dell&#39; `MyMapOf_xsd_string_To_xsd_anyType_Item` oggetto `value` .
   * Aggiungere l&#39; `MyMapOf_xsd_string_To_xsd_anyType_Item` oggetto all&#39; `MyMapOf_xsd_string_To_xsd_anyType` oggetto. Richiamare il `MyMapOf_xsd_string_To_xsd_anyType` metodo dell&#39;oggetto `Add` e passare l&#39; `MyMapOf_xsd_string_To_xsd_anyType` oggetto. (Eseguire questa operazione per ciascun documento PDF di input e per il documento XML del segnalibro).

1. Impostare le opzioni di esecuzione.

   * Creare un `AssemblerOptionSpec` oggetto che memorizza le opzioni di esecuzione utilizzando il relativo costruttore.
   * Impostare le opzioni di runtime per soddisfare i requisiti aziendali assegnando un valore a un membro di dati che appartiene all&#39; `AssemblerOptionSpec` oggetto. Ad esempio, per indicare al servizio Assembler di continuare l&#39;elaborazione di un processo in caso di errore, assegnare `false` al membro `AssemblerOptionSpec` dati dell&#39; `failOnError` oggetto.

1. Assemblare il documento PDF.

   Richiama il metodo dell’ `AssemblerServiceClient` oggetto `invokeDDX` e passa i seguenti valori:

   * Un `BLOB` oggetto che rappresenta il documento DDX
   * L&#39; `MyMapOf_xsd_string_To_xsd_anyType` array che contiene i documenti di input
   * Un oggetto `AssemblerOptionSpec` che specifica le opzioni di esecuzione

   Il `invokeDDX` metodo restituisce un `AssemblerResult` oggetto che contiene i risultati del processo ed eventuali eccezioni.

1. Salvare il documento PDF contenente i segnalibri.

   Per ottenere il documento PDF appena creato, effettuare le seguenti operazioni:

   * Accedere al campo dell&#39; `AssemblerResult` oggetto `documents` , ovvero un `Map` oggetto che contiene i documenti PDF risultanti.
   * Eseguire un&#39;iterazione sull&#39; `Map` oggetto fino a individuare la chiave che corrisponde al nome del documento risultante. Quindi, inserite l&#39;elemento `value` dell&#39;array in un `BLOB`.
   * Estrarre i dati binari che rappresentano il documento PDF accedendo al campo dell&#39; `BLOB` oggetto `MTOM` . Questo restituisce un array di byte che è possibile scrivere in un file PDF.

**Consulta anche**

[Chiamata di AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
