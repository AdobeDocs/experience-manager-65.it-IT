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


# Assemblaggio di documenti PDF con segnalibri {#assembling-pdf-documents-with-bookmarks}

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

In questo documento DDX, si noti che all&#39;attributo di origine è assegnato il valore `Loan.pdf`. Questo documento DDX specifica che un singolo documento PDF viene passato al servizio Assembler. Quando si assembla un documento PDF con segnalibri, è necessario specificare un documento XML con segnalibri che descrive i segnalibri nel documento finale. Per specificare un documento XML del segnalibro, assicurarsi che l&#39;elemento `Bookmarks` sia specificato nel documento DDX.

In questo documento DDX di esempio, l&#39;elemento `Bookmarks` specifica `doc2` come valore. Questo valore indica che la mappa di input passata al servizio Assembler contiene una chiave denominata `doc2`. Il valore della chiave `doc2` è un valore `com.adobe.idp.Document` che rappresenta il documento XML del segnalibro. (Vedere &quot;Linguaggio dei segnalibri&quot; nel [Servizio Assembler e DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63).)

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
>Per informazioni complete sulle azioni supportate, vedere &quot; `Action` element&quot; (elemento [Assembler Service) e DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63).

Dato il documento DDX specificato in questa sezione e il file XML del segnalibro come input, il servizio Assembler assembla un documento PDF contenente i seguenti segnalibri.

![aw_aw_bmark](assets/aw_aw_bmark.png)

Quando un utente fa clic sul segnalibro *Apri i dettagli del prestito*, viene aperto il file LoanDetails.pdf. Analogamente, quando l&#39;utente fa clic sul segnalibro *Avvia NotePad*, viene avviato NotePad.

>[!NOTE]
>
>Prima di leggere questa sezione, è consigliabile avere familiarità con l&#39;assemblaggio di documenti PDF tramite il servizio Assembler. In questa sezione non vengono discussi concetti, ad esempio la creazione di un oggetto raccolta che contiene documenti di input o l&#39;apprendimento di come estrarre i risultati dall&#39;oggetto raccolta restituito. (Vedere [Assemblaggio programmatico di documenti PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md#programmatically-assembling-pdf-documents).)

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Assembler, vedere [Guida di riferimento dei servizi per  AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Per ulteriori informazioni su un documento DDX, vedere [Servizio Assembler e Riferimento DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

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
* adobe-utilities.jar (richiesto se  AEM Forms è distribuito su JBoss)
* jbossall-client.jar (richiesto se  AEM Forms è distribuito su JBoss)

se  AEM Forms è distribuito su un server applicazione J2EE supportato diverso da JBoss, è necessario sostituire i file adobe-utilities.jar e jbossall-client.jar con file JAR specifici del server applicazione J2EE in cui  AEM Forms è distribuito. Per informazioni sulla posizione di tutti  file AEM Forms JAR, vedere [Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un client Assembler PDF**

Prima di eseguire un&#39;operazione Assembler a livello di programmazione, è necessario creare un client di servizio Assembler.

**Riferimento a un documento DDX esistente**

Per assemblare un documento PDF è necessario fare riferimento a un documento DDX. Questo documento DDX deve contenere l&#39;elemento `Bookmarks`, che indica al servizio Assembler di assemblare un PDF contenente segnalibri. (Per un esempio, vedere il documento DDX illustrato in precedenza in questa sezione).

**Riferimento a un documento PDF al quale vengono aggiunti i segnalibri**

Fare riferimento a un documento PDF al quale vengono aggiunti i segnalibri. Non importa se il documento PDF di riferimento contiene già dei segnalibri. Se l&#39;elemento `Bookmarks` è un elemento secondario dell&#39;elemento sorgente PDF, i segnalibri sostituiranno quelli già esistenti nell&#39;origine PDF. Tuttavia, se si desidera mantenere i segnalibri esistenti, assicurarsi che `Bookmarks` sia un elemento di pari livello dell&#39;elemento sorgente PDF. Ad esempio, considerate quanto segue:

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
>Vedere &quot;Bookmarks Language&quot; in [Assembler Service e DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63).

**Aggiungere il documento PDF e il documento XML del segnalibro a una raccolta Mappa**

È necessario aggiungere alla raccolta Mappa sia il documento PDF al quale vengono aggiunti i segnalibri, sia il documento XML del segnalibro. Pertanto, l&#39;oggetto insieme Map contiene due elementi: un documento PDF e il documento XML del segnalibro.

**Impostazione delle opzioni di esecuzione**

È possibile impostare opzioni di esecuzione che controllano il comportamento del servizio Assembler mentre esegue un processo. Ad esempio, potete impostare un&#39;opzione che indichi al servizio Assembler di continuare l&#39;elaborazione di un processo in caso di errore. Per informazioni sulle opzioni di esecuzione che è possibile impostare, vedere il riferimento alla classe `AssemblerOptionSpec` in [ Guida di riferimento delle API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Assemblare il documento PDF**

Per assemblare un documento PDF contenente nuovi segnalibri, utilizzare l&#39;operazione `invokeDDX` del servizio Assembler. Il motivo per cui è necessario utilizzare l&#39;operazione `invokeDDX` rispetto ad altre operazioni del servizio Assembler, come `invokeOneDocument`, è dovuto al fatto che il servizio Assembler richiede un documento XML con segnalibro passato all&#39;interno dell&#39;oggetto dell&#39;insieme Map. Questo oggetto è un parametro dell&#39;operazione `invokeDDX`.

**Salvare il documento PDF contenente i segnalibri**

È necessario estrarre i risultati dall&#39;oggetto mappa restituito e salvare il documento PDF corrispondente. (Vedere &quot;Estrai i risultati&quot; in [Assemblaggio programmatico di documenti PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md).)

**Consulta anche**

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Assemblaggio di documenti PDF a livello di programmazione](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Assemblare documenti PDF con segnalibri utilizzando l&#39;API Java {#assemble-pdf-documents-with-bookmarks-using-the-java-api}

Assemblate un documento PDF con segnalibri utilizzando l&#39;API di Assembler Service (Java):

1. Includere i file di progetto.

   Includete file JAR client, ad esempio adobe-assembler-client.jar, nel percorso di classe del progetto Java.

1. Creare un client Assembler PDF.

   * Creare un oggetto `ServiceClientFactory` che contiene le proprietà di connessione. (Vedere [Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * Creare un oggetto `AssemblerServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Fare riferimento a un documento DDX esistente.

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento DDX utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del file DDX.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Fare riferimento a un documento PDF al quale vengono aggiunti i segnalibri.

   * Creare un oggetto `java.io.FileInputStream` utilizzando il relativo costruttore e passando la posizione del documento PDF.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passare l&#39;oggetto `java.io.FileInputStream` che contiene il documento PDF.

1. Fare riferimento al documento XML del segnalibro.

   * Creare un oggetto `java.io.FileInputStream` utilizzando il relativo costruttore e passando la posizione del file XML che rappresenta il documento XML del segnalibro.
   * Creare un oggetto `com.adobe.idp.Document` e passare l&#39;oggetto `java.io.FileInputStream` che contiene il documento PDF.

1. Aggiungere il documento PDF e il documento XML del segnalibro a una raccolta Mappa.

   * Creare un oggetto `java.util.Map` utilizzato per memorizzare sia il documento PDF di input che il documento XML del segnalibro.
   * Aggiungere il documento PDF di input richiamando il metodo `put` dell&#39;oggetto `java.util.Map` e passando gli argomenti seguenti:

      * Un valore di stringa che rappresenta il nome della chiave. Questo valore deve corrispondere al valore dell&#39;elemento di origine PDF specificato nel documento DDX.
      * Un oggetto `com.adobe.idp.Document` che contiene il documento PDF di input.
   * Aggiungete il documento XML del segnalibro richiamando il metodo `put` dell&#39;oggetto `java.util.Map` e passando gli argomenti seguenti:

      * Un valore di stringa che rappresenta il nome della chiave. Questo valore deve corrispondere al valore dell&#39;elemento di origine Segnalibri specificato nel documento DDX.
      * Un oggetto `com.adobe.idp.Document` che contiene il documento XML del segnalibro.


1. Impostare le opzioni di esecuzione.

   * Creare un oggetto `AssemblerOptionSpec` che memorizza le opzioni di esecuzione utilizzando il relativo costruttore.
   * Impostate le opzioni di runtime per soddisfare i requisiti aziendali richiamando un metodo che appartiene all&#39;oggetto `AssemblerOptionSpec`. Ad esempio, per indicare al servizio Assembler di continuare a elaborare un processo quando si verifica un errore, richiamare il metodo `AssemblerOptionSpec` dell&#39;oggetto `setFailOnError` e passare `false`.

1. Assemblare il documento PDF.

   Richiamare il metodo `AssemblerServiceClient` dell&#39;oggetto `invokeDDX` e trasmettere i seguenti valori obbligatori:

   * Un oggetto `com.adobe.idp.Document` che rappresenta il documento DDX da utilizzare
   * Un oggetto `java.util.Map` che contiene sia il documento PDF di input che il documento XML del segnalibro.
   * Un oggetto `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` che specifica le opzioni di esecuzione, incluso il font predefinito e il livello di registro del processo

   Il metodo `invokeDDX` restituisce un oggetto `com.adobe.livecycle.assembler.client.AssemblerResult` che contiene i risultati del processo ed eventuali eccezioni.

1. Salvare il documento PDF contenente i segnalibri.

   Per ottenere il documento PDF appena creato, effettuare le seguenti operazioni:

   * Richiamare il metodo `AssemblerResult` dell&#39;oggetto `getDocuments`. Questo restituisce un oggetto `java.util.Map`.
   * Iterate l&#39;oggetto `java.util.Map` fino a individuare l&#39;oggetto `com.adobe.idp.Document` risultante. Per ottenere il documento è possibile utilizzare l&#39;elemento risultato PDF specificato nel documento DDX.
   * Richiamare il metodo `com.adobe.idp.Document` dell&#39;oggetto `copyToFile` per estrarre il documento PDF.

**Consulta anche**

[Avvio rapido (modalità SOAP): Assemblare documenti PDF con segnalibri mediante l&#39;API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-pdf-documents-with-bookmarks-using-the-java-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Assemblare documenti PDF con segnalibri utilizzando l&#39;API del servizio Web {#assemble-pdf-documents-with-bookmarks-using-the-web-service-api}

Assemblate un documento PDF con segnalibri utilizzando l&#39;API di Assembler Service (servizio Web):

1. Includere i file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituire `localhost` con l&#39;indirizzo IP del server che ospita  AEM Forms.

1. Creare un client Assembler PDF.

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

1. Fare riferimento a un documento PDF al quale vengono aggiunti i segnalibri.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare il PDF di input.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF di input e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà `System.IO.FileStream` dell&#39;oggetto `Length`.
   * Compilare l&#39;array di byte con i dati del flusso richiamando il metodo `Read` dell&#39;oggetto `System.IO.FileStream` e passando l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando il relativo campo `MTOM` con il contenuto dell&#39;array di byte.

1. Fare riferimento al documento XML del segnalibro.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare il documento XML del segnalibro.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF di input e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà `System.IO.FileStream` dell&#39;oggetto `Length`.
   * Compilare l&#39;array di byte con i dati del flusso richiamando il metodo `Read` dell&#39;oggetto `System.IO.FileStream` e passando l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando il relativo campo `MTOM` con il contenuto dell&#39;array di byte.

1. Aggiungere il documento PDF e il documento XML del segnalibro a una raccolta Mappa.

   * Creare un oggetto `MyMapOf_xsd_string_To_xsd_anyType`. Questo oggetto raccolta viene utilizzato per memorizzare i documenti PDF di input e il documento XML del segnalibro.
   * Per ciascun documento PDF di input e il documento XML del segnalibro, creare un oggetto `MyMapOf_xsd_string_To_xsd_anyType_Item`.
   * Assegnare un valore di stringa che rappresenta il nome chiave al campo `MyMapOf_xsd_string_To_xsd_anyType_Item` dell&#39;oggetto `key`. Questo valore deve corrispondere al valore dell&#39;elemento di origine PDF specificato nel documento DDX.
   * Assegnare l&#39;oggetto `BLOB` che memorizza il documento PDF nel campo `MyMapOf_xsd_string_To_xsd_anyType_Item` dell&#39;oggetto `value`.
   * Aggiungere l&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType_Item` all&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType`. Richiamare il metodo `MyMapOf_xsd_string_To_xsd_anyType` dell&#39;oggetto `Add` e passare l&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType`. (Eseguire questa operazione per ciascun documento PDF di input e per il documento XML del segnalibro).

1. Impostare le opzioni di esecuzione.

   * Creare un oggetto `AssemblerOptionSpec` che memorizza le opzioni di esecuzione utilizzando il relativo costruttore.
   * Impostare le opzioni di runtime per soddisfare i requisiti aziendali assegnando un valore a un membro di dati che appartiene all&#39;oggetto `AssemblerOptionSpec`. Ad esempio, per indicare al servizio Assembler di continuare l&#39;elaborazione di un processo in caso di errore, assegnare `false` al membro di dati `AssemblerOptionSpec` dell&#39;oggetto `failOnError`.

1. Assemblare il documento PDF.

   Richiamare il metodo `AssemblerServiceClient` dell&#39;oggetto `invokeDDX` e trasmettere i seguenti valori:

   * Un oggetto `BLOB` che rappresenta il documento DDX
   * L&#39;array `MyMapOf_xsd_string_To_xsd_anyType` che contiene i documenti di input
   * Un oggetto `AssemblerOptionSpec` che specifica le opzioni di esecuzione

   Il metodo `invokeDDX` restituisce un oggetto `AssemblerResult` che contiene i risultati del processo ed eventuali eccezioni.

1. Salvare il documento PDF contenente i segnalibri.

   Per ottenere il documento PDF appena creato, effettuare le seguenti operazioni:

   * Accedere al campo `documents` dell&#39;oggetto `AssemblerResult`, che è un oggetto `Map` che contiene i documenti PDF risultanti.
   * Iterate l&#39;oggetto `Map` fino a trovare la chiave che corrisponde al nome del documento risultante. Quindi, inserire l&#39;elemento `value` del membro della matrice in un elemento `BLOB`.
   * Estrarre i dati binari che rappresentano il documento PDF accedendo al relativo campo `BLOB` dell&#39;oggetto &lt;a1/>. `MTOM` Questo restituisce un array di byte che è possibile scrivere in un file PDF.

**Consulta anche**

[Chiamata  AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
