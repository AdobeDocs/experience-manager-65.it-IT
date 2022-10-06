---
title: Assemblaggio di documenti PDF a livello di programmazione
seo-title: Programmatically Assembling PDF Documents
description: Utilizza l’API del servizio Assembler per assemblare più documenti PDF in un singolo documento PDF utilizzando l’API Java e l’API Web Service.
seo-description: Use the Assembler service API to assemble multiple PDF documents into a single PDF document using the Java API and the Web Service API.
uuid: aa3f8f39-1fbc-48d0-82ff-6caaadf125fc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: ebe8136b-2a79-4035-b9d5-aa70a5bbd4af
role: Developer
exl-id: 7d6fd230-e477-4286-9fb3-18a3474e3e48
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2124'
ht-degree: 0%

---

# Assemblaggio di documenti PDF a livello di programmazione {#programmatically-assembling-pdf-documents}

**Esempi ed esempi in questo documento sono solo per AEM Forms in ambiente JEE.**

È possibile utilizzare l’API del servizio Assembler per assemblare più documenti PDF in un unico documento PDF. L’illustrazione seguente mostra tre documenti PDF che vengono uniti in un singolo documento PDF.

![pa_pa_document_assembly](assets/pa_pa_document_assembly.png)

Per assemblare due o più documenti PDF in un singolo documento PDF, è necessario un documento DDX. Un documento DDX descrive il documento PDF prodotto dal servizio Assembler. In altre parole, il documento DDX indica al servizio Assembler quali azioni eseguire.

Ai fini di questa discussione, si supponga che venga utilizzato il seguente documento DDX.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
     <PDF result="out.pdf">
         <PDF source="map.pdf" />
         <PDF source="directions.pdf" />
     </PDF>
 </DDX>
```

Questo documento DDX unisce due documenti PDF denominati *map.pdf* e *sections.pdf* in un singolo documento PDF.

>[!NOTE]
>
>Per visualizzare un documento DDX che smonta un documento PDF, vedere [Smontaggio programmatico dei documenti PDF](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents).

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Assembler, vedere [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Per ulteriori informazioni su un documento DDX, consulta [Servizio di assemblaggio e riferimento DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Considerazioni quando si richiama il servizio Assembler utilizzando i servizi web {#considerations-when-invoking-assembler-service-using-web-services}

Quando si aggiungono intestazioni e piè di pagina durante l&#39;assemblaggio di documenti di grandi dimensioni, si può incontrare un `OutOfMemory` e i file non verranno assemblati. Per ridurre la possibilità che si verifichi questo problema, aggiungi una `DDXProcessorSetting` al documento DDX, come illustrato nell&#39;esempio seguente.

`<DDXProcessorSetting name="checkpoint" value="2000" />`

Puoi aggiungere questo elemento come elemento secondario di `DDX` elemento o come figlio di un `PDF result` elemento. Il valore predefinito per questa impostazione è 0 (zero), che disattiva il checkpoint e il DDX si comporta come se `DDXProcessorSetting` elemento non presente. Se hai rilevato un `OutOfMemory` errore, potrebbe essere necessario impostare il valore su un numero intero, in genere compreso tra 500 e 5000. Un piccolo valore di checkpoint genera un controllo più frequente.

## Riepilogo dei passaggi {#summary-of-steps}

Per assemblare un singolo documento PDF da più documenti PDF, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Creare un client PDF Assembler.
1. Fai riferimento a un documento DDX esistente.
1. Riferimento ai documenti PDF di input.
1. Impostare le opzioni di esecuzione.
1. Assemblare i documenti di input PDF.
1. Estrai i risultati.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso della classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è distribuito su JBoss)
* jbossall-client.jar (richiesto se AEM Forms è distribuito su JBoss)

se AEM Forms è distribuito su un server applicazioni J2EE supportato diverso da JBoss, è necessario sostituire i file adobe-utilities.jar e jbossall-client.jar con file JAR specifici per il server applicazioni J2EE in cui viene distribuito AEM Forms.

**Creare un client PDF Assembler**

Prima di poter eseguire un&#39;operazione Assembler a livello di programmazione, è necessario creare un client Assembler.

**Riferimento a un documento DDX esistente**

Per assemblare un documento PDF è necessario fare riferimento a un documento DDX. Ad esempio, considera il documento DDX introdotto in questa sezione. Questo documento DDX indica al servizio Assembler di unire due documenti PDF in un singolo documento PDF.

**Riferimento ai documenti PDF**

Fare riferimento ai documenti PDF di input che si desidera passare al servizio Assembler. Ad esempio, se desideri trasmettere due documenti PDF di input denominati Mappa e direzioni, devi passare i file PDF corrispondenti.

È necessario inserire sia il file map.pdf che il file directs.pdf in un oggetto raccolta. Il nome della chiave deve corrispondere al valore dell&#39;attributo di origine PDF nel documento DDX. Non importa quale sia il nome del file PDF se la chiave e l&#39;attributo di origine nel documento DDX corrispondono.

>[!NOTE]
>
>Un `AssemblerResult` se si richiama l&#39;oggetto , che contiene un oggetto raccolta, viene restituito `invokeDDX` funzionamento. Questa operazione viene utilizzata quando si passano due o più documenti di input PDF al servizio Assembler. Tuttavia, se si passa un solo PDF di input al servizio Assembler e si prevede un solo documento di ritorno, richiamare `invokeOneDocument` funzionamento. Quando si richiama questa operazione, viene restituito un singolo documento. Per informazioni sull&#39;utilizzo di questa operazione, vedi [Assemblaggio di documenti PDF crittografati](/help/forms/developing/assembling-encrypted-pdf-documents.md#assembling-encrypted-pdf-documents).

**Impostare le opzioni di esecuzione**

È possibile impostare le opzioni di esecuzione che controllano il comportamento del servizio Assembler mentre esegue un processo. Ad esempio, è possibile impostare un&#39;opzione che indica al servizio Assembler di continuare l&#39;elaborazione di un processo in caso di errore. Per informazioni sulle opzioni di esecuzione che è possibile impostare, vedere la `AssemblerOptionSpec` riferimento di classe in [Riferimento API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Assemblare i documenti di input PDF**

Dopo aver creato il client di servizio, fare riferimento a un file DDX, creare un oggetto raccolta che memorizza i documenti PDF di input e impostare le opzioni di esecuzione, è possibile richiamare l&#39;operazione DDX. Quando si utilizza il documento DDX specificato in questa sezione, i file map.pdf e Direction.pdf vengono uniti in un unico documento PDF.

**Estrarre i risultati**

Il servizio Assembler restituisce un `java.util.Map` che può essere ottenuto dal `AssemblerResult` e che contiene i risultati dell&#39;operazione. Il restituito `java.util.Map` contiene i documenti risultanti ed eventuali eccezioni.

Nella tabella seguente sono riepilogati alcuni dei valori chiave e dei tipi di oggetto che è possibile individuare nella `java.util.Map` oggetto.

<table>
 <thead>
  <tr>
   <th><p>Valore chiave</p></th>
   <th><p>Tipo di oggetto</p></th>
   <th><p>Descrizione</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p><code><i>documentName</i></code></p></td>
   <td><p><code>com.adobe.idp.Document</code></p></td>
   <td><p>Contiene i documenti risultanti specificati in un elemento risultante DDX</p></td>
  </tr>
  <tr>
   <td><p><code><i>documentName</i></code></p></td>
   <td><p><code>Exception</code></p></td>
   <td><p>Contiene eventuali eccezioni per il documento</p></td>
  </tr>
  <tr>
   <td><p><code>OutputMapConstants.LOG_NAME</code></p></td>
   <td><p><code>com.adobe.idp.Documen</code></p></td>
   <td><p>Contiene il registro dei processi</p></td>
  </tr>
 </tbody>
</table>

**Consulta anche**

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Smontaggio programmatico dei documenti PDF](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

## Assemblare documenti PDF utilizzando l’API Java {#assemble-pdf-documents-using-the-java-api}

Assemblare un documento PDF utilizzando l’API del servizio Assembler (Java):

1. Includi file di progetto.

   Includi file JAR client, come adobe-assembler-client.jar, nel percorso di classe del progetto Java.

1. Creare un client PDF Assembler.

   * Crea un `ServiceClientFactory` oggetto contenente le proprietà di connessione.
   * Crea un `AssemblerServiceClient` utilizzando il relativo costruttore e passando `ServiceClientFactory` oggetto.

1. Fai riferimento a un documento DDX esistente.

   * Crea un `java.io.FileInputStream` oggetto che rappresenta il documento DDX utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del file DDX.
   * Crea un `com.adobe.idp.Document` utilizzando il relativo costruttore e passando `java.io.FileInputStream` oggetto.

1. Riferimento ai documenti PDF di input.

   * Crea un `java.util.Map` oggetto utilizzato per memorizzare i documenti PDF di input utilizzando un `HashMap` costruttore.
   * Per ogni documento di input PDF, crea un `java.io.FileInputStream` utilizzando il relativo costruttore e passando la posizione del documento di input PDF.
   * Per ogni documento di input PDF, crea un `com.adobe.idp.Document` e passare `java.io.FileInputStream` oggetto contenente il documento PDF.
   * Per ogni documento di input, aggiungi una voce al `java.util.Map` richiamandone l&#39;oggetto `put` e passare gli argomenti seguenti:

      * Valore stringa che rappresenta il nome della chiave. Questo valore deve corrispondere al valore dell&#39;elemento di origine PDF specificato nel documento DDX.
      * A `com.adobe.idp.Document` (o `java.util.List` oggetto che specifica più documenti) contenente il documento di origine PDF.

1. Impostare le opzioni di esecuzione.

   * Crea un `AssemblerOptionSpec` oggetto che memorizza le opzioni di esecuzione utilizzando il relativo costruttore.
   * Impostare le opzioni di esecuzione per soddisfare i requisiti aziendali richiamando un metodo che appartiene al `AssemblerOptionSpec` oggetto. Ad esempio, per dare istruzioni al servizio Assembler di continuare a elaborare un processo quando si verifica un errore, richiama il `AssemblerOptionSpec` dell’oggetto `setFailOnError` metodo e passaggio `false`.

1. Assemblare i documenti di input PDF.

   Richiama il `AssemblerServiceClient` dell’oggetto `invokeDDX` e trasmettere i seguenti valori richiesti:

   * A `com.adobe.idp.Document` oggetto che rappresenta il documento DDX da utilizzare
   * A `java.util.Map` oggetto contenente i file di input PDF da assemblare
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` oggetto che specifica le opzioni di esecuzione, incluso il tipo di carattere predefinito e il livello di log del processo

   La `invokeDDX` restituisce un `com.adobe.livecycle.assembler.client.AssemblerResult` oggetto contenente i risultati del processo ed eventuali eccezioni.

1. Estrai i risultati.

   Per ottenere il documento PDF appena creato, eseguire le operazioni seguenti:

   * Richiama il `AssemblerResult` dell’oggetto `getDocuments` metodo . Questo restituisce un `java.util.Map` oggetto.
   * Itera attraverso il `java.util.Map` finché non trovi il risultato `com.adobe.idp.Document` oggetto. Per ottenere il documento è possibile utilizzare l&#39;elemento risultato di PDF specificato nel documento DDX.
   * Richiama il `com.adobe.idp.Document` dell’oggetto `copyToFile` per estrarre il documento PDF.

   >[!NOTE]
   >
   >Se `LOG_LEVEL` è stato impostato per produrre un log, è possibile estrarre il log utilizzando il `AssemblerResult` dell&#39;oggetto `getJobLog` metodo .

**Consulta anche**

[Avvio rapido (modalità SOAP): Assemblaggio di un documento PDF tramite l’API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-a-pdf-document-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Assemblare documenti PDF utilizzando l’API del servizio Web {#assemble-pdf-documents-using-the-web-service-api}

Assemblare i documenti PDF utilizzando l&#39;API del servizio Assembler (servizio Web):

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

1. Riferimento ai documenti PDF di input.

   * Per ogni documento di input PDF, crea un `BLOB` utilizzando il relativo costruttore. La `BLOB` viene utilizzato per memorizzare il documento di input PDF.
   * Crea un `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento di input PDF e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto del `System.IO.FileStream` oggetto. È possibile determinare le dimensioni dell&#39;array di byte ottenendo il `System.IO.FileStream` dell’oggetto `Length` proprietà.
   * Compilare l&#39;array di byte con i dati del flusso richiamando il `System.IO.FileStream` dell’oggetto `Read` metodo . Passa la matrice dei byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare `BLOB` oggetto assegnando il relativo `MTOM` con il contenuto dell&#39;array di byte.
   * Crea un `MyMapOf_xsd_string_To_xsd_anyType` oggetto. Questo oggetto raccolta viene utilizzato per memorizzare i documenti PDF di input.
   * Per ogni documento di input PDF, crea un `MyMapOf_xsd_string_To_xsd_anyType_Item` oggetto. Ad esempio, se si utilizzano due documenti PDF di input, crearne due `MyMapOf_xsd_string_To_xsd_anyType_Item` oggetti.
   * Assegna un valore stringa che rappresenta il nome della chiave al `MyMapOf_xsd_string_To_xsd_anyType_Item` dell&#39;oggetto `key` campo . Questo valore deve corrispondere al valore dell&#39;elemento di origine PDF specificato nel documento DDX. Esegui questa operazione per ogni documento di input PDF.
   * Assegna `BLOB` oggetto che memorizza il documento PDF nella `MyMapOf_xsd_string_To_xsd_anyType_Item` dell&#39;oggetto `value` campo . Esegui questa operazione per ogni documento di input PDF.
   * Aggiungi il `MyMapOf_xsd_string_To_xsd_anyType_Item` dell&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType` oggetto. Richiama il `MyMapOf_xsd_string_To_xsd_anyType` dell&#39;oggetto `Add` e passare il `MyMapOf_xsd_string_To_xsd_anyType` oggetto. Esegui questa operazione per ogni documento di input PDF.

1. Impostare le opzioni di esecuzione.

   * Crea un `AssemblerOptionSpec` oggetto che memorizza le opzioni di esecuzione utilizzando il relativo costruttore.
   * Impostare le opzioni di esecuzione per soddisfare i requisiti aziendali assegnando un valore a un membro dati che appartiene al `AssemblerOptionSpec` oggetto. Ad esempio, per dare istruzioni al servizio Assembler di continuare a elaborare un processo quando si verifica un errore, assegnare `false` al `AssemblerOptionSpec` dell’oggetto `failOnError` membro dati.

1. Assemblare i documenti di input PDF.

   Richiama il `AssemblerServiceClient` dell’oggetto `invoke` e passare i seguenti valori:

   * A `BLOB` oggetto che rappresenta il documento DDX.
   * La `mapItem` che contiene i documenti PDF di input. Le chiavi devono corrispondere ai nomi dei file di origine di PDF e i relativi valori devono essere `BLOB` oggetti corrispondenti a tali file.
   * Un `AssemblerOptionSpec` oggetto che specifica le opzioni di esecuzione.

   La `invoke` restituisce un `AssemblerResult` oggetto contenente i risultati del processo ed eventuali eccezioni.

1. Estrai i risultati.

   Per ottenere il documento PDF appena creato, eseguire le operazioni seguenti:

   * Accedere al `AssemblerResult` dell’oggetto `documents` un campo `Map` oggetto contenente i documenti PDF risultanti.
   * Itera attraverso il `Map` finché non viene trovata la chiave che corrisponde al nome del documento risultante. Quindi eseguire il cast del membro della matrice `value` a `BLOB`.
   * Estrarre i dati binari che rappresentano il documento PDF accedendo ai relativi `BLOB` dell’oggetto `MTOM` proprietà. Restituisce una matrice di byte che è possibile scrivere in un file PDF.

   >[!NOTE]
   >
   >Se `LOG_LEVEL` è stato impostato per produrre un log, è possibile estrarre il log ottenendo il valore del `AssemblerResult` dell&#39;oggetto `jobLog` membro dati.

**Consulta anche**

[Richiamo di AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
