---
title: Assemblaggio di documenti PDF con segnalibri
seo-title: Assemblaggio di documenti PDF con segnalibri
description: Utilizzare il servizio Assembler per modificare un documento PDF contenente segnalibri per includere segnalibri utilizzando l'API Java e l'API Web Service.
seo-description: Utilizzare il servizio Assembler per modificare un documento PDF contenente segnalibri per includere segnalibri utilizzando l'API Java e l'API Web Service.
uuid: a306d2a6-0b12-4eb3-bff4-968a33417486
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9f4711a8-033c-4051-ab41-65a26838899b
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2589'
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

In questo documento DDX, notare che all&#39;attributo di origine viene assegnato il valore `Loan.pdf`. Questo documento DDX specifica che un singolo documento PDF viene passato al servizio Assembler. Quando si assembla un documento PDF con segnalibri, è necessario specificare un documento XML con segnalibro che descriva i segnalibri nel documento risultante. Per specificare un documento XML segnalibro, assicurarsi che l&#39;elemento `Bookmarks` sia specificato nel documento DDX.

In questo documento DDX di esempio, l&#39;elemento `Bookmarks` specifica `doc2` come valore. Questo valore indica che la mappa di input passata al servizio Assembler contiene una chiave denominata `doc2`. Il valore della chiave `doc2` è un valore `com.adobe.idp.Document` che rappresenta il documento XML del segnalibro. (Vedere &quot;Lingua dei segnalibri&quot; in [Servizio Assembler e Riferimento DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).)

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

In questo documento XML del segnalibro, notare l&#39;elemento Action che definisce l&#39;azione eseguita quando un utente fa clic sul segnalibro. Sotto l&#39;elemento Azione è l&#39;elemento Launch che avvia applicazioni, come NotePad e apre file, come i file PDF. Per aprire un file PDF, è necessario utilizzare l’elemento File che specifica il file da aprire. Ad esempio, nel file XML del segnalibro specificato in questa sezione, il nome del file aperto è LoanDetails.pdf.

>[!NOTE]
>
>Per informazioni complete sulle azioni supportate, vedi &quot; `Action` element&quot; in [Servizio Assembler e Riferimento DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

Dato il documento DDX specificato in questa sezione e il file XML del segnalibro come input, il servizio Assembler assembla un documento PDF contenente i seguenti segnalibri.

![aw_aw_bmark](assets/aw_aw_bmark.png)

Quando un utente fa clic sul segnalibro *Apri i dettagli del prestito*, viene aperto il file LoanDetails.pdf. Allo stesso modo, quando l&#39;utente fa clic sul segnalibro *Avvia NotePad*, viene avviato NotePad.

>[!NOTE]
>
>Prima di leggere questa sezione, si consiglia di avere familiarità con l&#39;assemblaggio di documenti PDF utilizzando il servizio Assembler. In questa sezione non vengono descritti i concetti, ad esempio la creazione di un oggetto raccolta contenente documenti di input o l&#39;apprendimento della modalità di estrazione dei risultati dall&#39;oggetto di raccolta restituito. (Vedere [Assemblaggio programmatico di documenti PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md#programmatically-assembling-pdf-documents).)

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Assembler, vedere [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Per ulteriori informazioni su un documento DDX, vedere [Servizio Assembler e Riferimento DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Riepilogo dei passaggi {#summary-of-steps}

Per assemblare un documento PDF contenente segnalibri, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Creare un client Assembler PDF.
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

se AEM Forms è implementato su un server applicazioni J2EE supportato diverso da JBoss, è necessario sostituire i file adobe-utilities.jar e jbossall-client.jar con file JAR specifici per il server applicazioni J2EE in cui è implementato AEM Forms. Per informazioni sulla posizione di tutti i file JAR di AEM Forms, consulta [Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un client Assembler PDF**

Prima di poter eseguire un&#39;operazione Assembler a livello di programmazione, è necessario creare un client di servizio Assembler.

**Riferimento a un documento DDX esistente**

Per assemblare un documento PDF è necessario fare riferimento a un documento DDX. Questo documento DDX deve contenere l&#39;elemento `Bookmarks` che indica al servizio Assembler di assemblare un PDF contenente segnalibri. Per un esempio, vedere il documento DDX mostrato in precedenza in questa sezione.

**Riferimento a un documento PDF al quale vengono aggiunti i segnalibri**

Fare riferimento a un documento PDF a cui vengono aggiunti i segnalibri. Non importa se il documento PDF a cui si fa riferimento contiene già dei segnalibri. Se l’elemento `Bookmarks` è un elemento secondario dell’elemento sorgente PDF, i segnalibri sostituiranno quelli già esistenti nell’origine PDF. Tuttavia, se desideri mantenere i segnalibri esistenti, assicurati che `Bookmarks` sia un elemento di pari livello dell’elemento sorgente PDF. Ad esempio, considera l’esempio seguente:

```xml
 <PDF result="foo">
      <PDF source="inDoc"/>
      <Bookmarks source="doc2"/>
 </PDF>
```

**Riferimento al documento XML del segnalibro**

Per assemblare un PDF contenente nuovi segnalibri, è necessario fare riferimento a un documento XML segnalibro. Il documento XML del segnalibro viene passato al servizio Assembler all&#39;interno dell&#39;oggetto raccolta Mappa. Per un esempio, vedere il documento XML del segnalibro mostrato in precedenza in questa sezione.

>[!NOTE]
>
>Vedere &quot;Lingua dei segnalibri&quot; nel [Servizio di assemblaggio e Riferimento DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

**Aggiungere il documento PDF e il documento XML del segnalibro a una raccolta Mappa**

È necessario aggiungere all&#39;insieme Map sia il documento PDF a cui vengono aggiunti i segnalibri sia il documento XML del segnalibro. Pertanto, l&#39;oggetto raccolta Mappa contiene due elementi: un documento PDF e il documento XML del segnalibro.

**Impostare le opzioni di esecuzione**

È possibile impostare le opzioni di esecuzione che controllano il comportamento del servizio Assembler mentre esegue un processo. Ad esempio, è possibile impostare un&#39;opzione che indica al servizio Assembler di continuare l&#39;elaborazione di un processo in caso di errore. Per informazioni sulle opzioni di esecuzione che è possibile impostare, vedere il riferimento alla classe `AssemblerOptionSpec` in [Riferimento API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Assembla il documento PDF**

Per assemblare un documento PDF contenente nuovi segnalibri, utilizzare l&#39;operazione `invokeDDX` del servizio Assembler. Il motivo per cui è necessario utilizzare l&#39;operazione `invokeDDX` rispetto ad altre operazioni del servizio Assembler, come `invokeOneDocument`, è che il servizio Assembler richiede un documento XML di segnalibro passato all&#39;interno dell&#39;oggetto di raccolta Mappa. Questo oggetto è un parametro dell&#39;operazione `invokeDDX`.

**Salvare il documento PDF contenente segnalibri**

È necessario estrarre i risultati dall’oggetto mappa restituito e salvare il documento PDF corrispondente. (Vedere &quot;Estrarre i risultati&quot; in [Assemblaggio programmatico di documenti PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md).)

**Consulta anche**

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Assemblaggio programmatico di documenti PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Assemblare documenti PDF con segnalibri utilizzando l&#39;API Java {#assemble-pdf-documents-with-bookmarks-using-the-java-api}

Assemblare un documento PDF con segnalibri utilizzando l&#39;API del servizio Assembler (Java):

1. Includi file di progetto.

   Includi file JAR client, come adobe-assembler-client.jar, nel percorso di classe del progetto Java.

1. Creare un client Assembler PDF.

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione. (Vedere [Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * Creare un oggetto `AssemblerServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Fai riferimento a un documento DDX esistente.

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento DDX utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del file DDX.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Fare riferimento a un documento PDF a cui vengono aggiunti i segnalibri.

   * Creare un oggetto `java.io.FileInputStream` utilizzando il relativo costruttore e passando la posizione del documento PDF.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passare l&#39;oggetto `java.io.FileInputStream` che contiene il documento PDF.

1. Fare riferimento al documento XML del segnalibro.

   * Creare un oggetto `java.io.FileInputStream` utilizzando il relativo costruttore e passando la posizione del file XML che rappresenta il documento XML del segnalibro.
   * Creare un oggetto `com.adobe.idp.Document` e passare l&#39;oggetto `java.io.FileInputStream` che contiene il documento PDF.

1. Aggiungere il documento PDF e il documento XML del segnalibro a una raccolta Mappa.

   * Creare un oggetto `java.util.Map` utilizzato per memorizzare sia il documento PDF di input che il documento XML del segnalibro.
   * Aggiungere il documento PDF di input richiamando il metodo `put` dell’oggetto `java.util.Map` e passando i seguenti argomenti:

      * Valore stringa che rappresenta il nome della chiave. Questo valore deve corrispondere al valore dell&#39;elemento di origine PDF specificato nel documento DDX.
      * Un oggetto `com.adobe.idp.Document` contenente il documento PDF di input.
   * Aggiungere il documento XML del segnalibro richiamando il metodo `java.util.Map` dell&#39;oggetto `put` e passando i seguenti argomenti:

      * Valore stringa che rappresenta il nome della chiave. Questo valore deve corrispondere al valore dell&#39;elemento di origine Segnalibri specificato nel documento DDX.
      * Un oggetto `com.adobe.idp.Document` che contiene il documento XML del segnalibro.


1. Impostare le opzioni di esecuzione.

   * Creare un oggetto `AssemblerOptionSpec` che memorizza le opzioni di esecuzione utilizzando il relativo costruttore.
   * Impostare le opzioni di esecuzione per soddisfare i requisiti aziendali richiamando un metodo appartenente all&#39;oggetto `AssemblerOptionSpec`. Ad esempio, per dare istruzioni al servizio Assembler di continuare a elaborare un processo quando si verifica un errore, richiamare il metodo `setFailOnError` dell&#39;oggetto `AssemblerOptionSpec` e passare `false`.

1. Assemblare il documento PDF.

   Richiama il metodo `invokeDDX` dell&#39;oggetto `AssemblerServiceClient` e passa i seguenti valori obbligatori:

   * Un oggetto `com.adobe.idp.Document` che rappresenta il documento DDX da utilizzare
   * Un oggetto `java.util.Map` che contiene sia il documento PDF di input che il documento XML del segnalibro.
   * Un oggetto `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` che specifica le opzioni di esecuzione, incluso il tipo di carattere predefinito e il livello di registro dei processi

   Il metodo `invokeDDX` restituisce un oggetto `com.adobe.livecycle.assembler.client.AssemblerResult` che contiene i risultati del processo ed eventuali eccezioni.

1. Salvare il documento PDF contenente segnalibri.

   Per ottenere il documento PDF appena creato, eseguire le operazioni seguenti:

   * Richiama il metodo `getDocuments` dell&#39;oggetto `AssemblerResult`. Restituisce un oggetto `java.util.Map`.
   * Iterare l&#39;oggetto `java.util.Map` fino a trovare l&#39;oggetto `com.adobe.idp.Document` risultante. Per ottenere il documento è possibile utilizzare l&#39;elemento risultato PDF specificato nel documento DDX.
   * Richiamare il metodo `copyToFile` dell&#39;oggetto `com.adobe.idp.Document` per estrarre il documento PDF.

**Consulta anche**

[Avvio rapido (modalità SOAP): Assemblaggio di documenti PDF con segnalibri tramite API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-pdf-documents-with-bookmarks-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Assemblare documenti PDF con segnalibri utilizzando l&#39;API del servizio Web {#assemble-pdf-documents-with-bookmarks-using-the-web-service-api}

Assemblare un documento PDF con segnalibri utilizzando l&#39;API del servizio Assembler (servizio Web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurati di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Creare un client Assembler PDF.

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
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento DDX e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni dell&#39;array di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare l’array di byte con i dati del flusso richiamando il metodo `Read` dell’oggetto `System.IO.FileStream` e passando l’array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando il relativo campo `MTOM` con il contenuto dell&#39;array di byte.

1. Fare riferimento a un documento PDF a cui vengono aggiunti i segnalibri.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L’oggetto `BLOB` viene utilizzato per memorizzare il PDF di input.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF di input e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni dell&#39;array di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare l’array di byte con i dati del flusso richiamando il metodo `Read` dell’oggetto `System.IO.FileStream` e passando l’array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando il relativo campo `MTOM` con il contenuto dell&#39;array di byte.

1. Fare riferimento al documento XML del segnalibro.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare il documento XML del segnalibro.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF di input e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni dell&#39;array di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare l’array di byte con i dati del flusso richiamando il metodo `Read` dell’oggetto `System.IO.FileStream` e passando l’array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando il relativo campo `MTOM` con il contenuto dell&#39;array di byte.

1. Aggiungere il documento PDF e il documento XML del segnalibro a una raccolta Mappa.

   * Creare un oggetto `MyMapOf_xsd_string_To_xsd_anyType`. Questo oggetto raccolta viene utilizzato per memorizzare i documenti PDF di input e il documento XML del segnalibro.
   * Per ciascun documento PDF di input e per il documento XML del segnalibro , creare un oggetto `MyMapOf_xsd_string_To_xsd_anyType_Item`.
   * Assegna un valore stringa che rappresenta il nome della chiave al campo `MyMapOf_xsd_string_To_xsd_anyType_Item` dell&#39;oggetto `key`. Questo valore deve corrispondere al valore dell&#39;elemento di origine PDF specificato nel documento DDX.
   * Assegnare l&#39;oggetto `BLOB` che memorizza il documento PDF nel campo `MyMapOf_xsd_string_To_xsd_anyType_Item` dell&#39;oggetto `value`.
   * Aggiungere l&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType_Item` all&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType`. Richiama il metodo `Add` dell&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType` e passa l&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType`. (Esegui questa operazione per ogni documento PDF di input e per il documento XML del segnalibro.)

1. Impostare le opzioni di esecuzione.

   * Creare un oggetto `AssemblerOptionSpec` che memorizza le opzioni di esecuzione utilizzando il relativo costruttore.
   * Impostare le opzioni di esecuzione per soddisfare i requisiti aziendali assegnando un valore a un membro dati appartenente all&#39;oggetto `AssemblerOptionSpec`. Ad esempio, per dare istruzioni al servizio Assembler di continuare a elaborare un processo in caso di errore, assegna `false` al membro dati `AssemblerOptionSpec` dell&#39;oggetto `failOnError`.

1. Assemblare il documento PDF.

   Richiama il metodo `invokeDDX` dell&#39;oggetto `AssemblerServiceClient` e passa i seguenti valori:

   * Un oggetto `BLOB` che rappresenta il documento DDX
   * Array `MyMapOf_xsd_string_To_xsd_anyType` contenente i documenti di input
   * Un oggetto `AssemblerOptionSpec` che specifica le opzioni di esecuzione

   Il metodo `invokeDDX` restituisce un oggetto `AssemblerResult` che contiene i risultati del processo ed eventuali eccezioni.

1. Salvare il documento PDF contenente segnalibri.

   Per ottenere il documento PDF appena creato, eseguire le operazioni seguenti:

   * Accedere al campo `documents` dell&#39;oggetto `AssemblerResult`, che è un oggetto `Map` che contiene i documenti PDF risultanti.
   * Iterare l&#39;oggetto `Map` fino a trovare la chiave che corrisponde al nome del documento risultante. Quindi eseguire il cast di `value` del membro della matrice su un `BLOB`.
   * Estrarre i dati binari che rappresentano il documento PDF accedendo al relativo campo `MTOM` dell’oggetto `BLOB`. Restituisce una matrice di byte che è possibile scrivere in un file PDF.

**Consulta anche**

[Richiamo di AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
