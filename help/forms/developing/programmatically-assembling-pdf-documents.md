---
title: Assemblaggio programmatico di documenti PDF
seo-title: Assemblaggio programmatico di documenti PDF
description: Utilizza l’API del servizio Assembler per assemblare più documenti PDF in un unico documento PDF utilizzando l’API Java e l’API del servizio Web.
seo-description: Utilizza l’API del servizio Assembler per assemblare più documenti PDF in un unico documento PDF utilizzando l’API Java e l’API del servizio Web.
uuid: aa3f8f39-1fbc-48d0-82ff-6caaadf125fc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: ebe8136b-2a79-4035-b9d5-aa70a5bbd4af
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2153'
ht-degree: 0%

---


# Assemblaggio programmatico di documenti PDF {#programmatically-assembling-pdf-documents}

**Esempi ed esempi in questo documento sono solo per AEM Forms in ambiente JEE.**

È possibile utilizzare l&#39;API di Assembler Service per assemblare più documenti PDF in un unico documento PDF. L’illustrazione seguente mostra tre documenti PDF uniti in un singolo documento PDF.

![pa_pa_document_assembly](assets/pa_pa_document_assembly.png)

Per assemblare due o più documenti PDF in un unico documento PDF, è necessario un documento DDX. Un documento DDX descrive il documento PDF prodotto dal servizio Assembler. In altre parole, il documento DDX indica al servizio Assembler quali azioni eseguire.

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

Questo documento DDX unisce due documenti PDF denominati *map.pdf* e *directs.pdf* in un singolo documento PDF.

>[!NOTE]
>
>Per visualizzare un documento DDX che smonta un documento PDF, vedere [Disassemblaggio programmatico di documenti PDF](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents).

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Assembler, vedere [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Per ulteriori informazioni su un documento DDX, vedere [Servizio Assembler e Riferimento DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Considerazioni quando si richiama il servizio Assembler utilizzando i servizi Web {#considerations-when-invoking-assembler-service-using-web-services}

Quando si aggiungono intestazioni e piè di pagina durante l&#39;assemblaggio di documenti di grandi dimensioni, è possibile che si verifichi un errore `OutOfMemory` e che i file non vengano assemblati. Per ridurre la possibilità che si verifichi questo problema, aggiungi un elemento `DDXProcessorSetting` al documento DDX, come illustrato nell&#39;esempio seguente.

`<DDXProcessorSetting name="checkpoint" value="2000" />`

Puoi aggiungere questo elemento come elemento secondario dell’elemento `DDX` o come elemento secondario di un elemento `PDF result`. Il valore predefinito per questa impostazione è 0 (zero), che disattiva il controllo e il DDX si comporta come se l&#39;elemento `DDXProcessorSetting` non fosse presente. Se si è verificato un errore `OutOfMemory`, potrebbe essere necessario impostare il valore su un numero intero, in genere compreso tra 500 e 5000. Un piccolo valore di checkpoint genera un controllo più frequente.

## Riepilogo dei passaggi {#summary-of-steps}

Per assemblare un singolo documento PDF da più documenti PDF, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Creare un client Assembler PDF.
1. Fai riferimento a un documento DDX esistente.
1. Riferimento ai documenti PDF di input.
1. Impostare le opzioni di esecuzione.
1. Assemblare i documenti PDF di input.
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

**Creare un client Assembler PDF**

Prima di poter eseguire un&#39;operazione Assembler a livello di programmazione, è necessario creare un client Assembler.

**Riferimento a un documento DDX esistente**

Per assemblare un documento PDF è necessario fare riferimento a un documento DDX. Ad esempio, considera il documento DDX introdotto in questa sezione. Questo documento DDX indica al servizio Assembler di unire due documenti PDF in un unico documento PDF.

**Riferimento a documenti PDF di input**

Fare riferimento ai documenti PDF di input che si desidera passare al servizio Assembler. Ad esempio, se si desidera passare due documenti PDF di input denominati Mappa e indicazioni, è necessario passare i file PDF corrispondenti.

È necessario inserire sia il file map.pdf che il file directs.pdf in un oggetto raccolta. Il nome della chiave deve corrispondere al valore dell&#39;attributo di origine PDF nel documento DDX. Non importa quale sia il nome del file PDF se la chiave e l&#39;attributo di origine nel documento DDX corrispondono.

>[!NOTE]
>
>Se si richiama l&#39;operazione `invokeDDX`, viene restituito un oggetto `AssemblerResult` contenente un oggetto di raccolta. Questa operazione viene utilizzata quando si passano due o più documenti PDF di input al servizio Assembler. Tuttavia, se si passa un solo PDF di input al servizio Assembler e si prevede un solo documento di ritorno, richiamare l&#39;operazione `invokeOneDocument`. Quando si richiama questa operazione, viene restituito un singolo documento. Per informazioni sull&#39;utilizzo di questa operazione, vedere [Assemblaggio di documenti PDF crittografati](/help/forms/developing/assembling-encrypted-pdf-documents.md#assembling-encrypted-pdf-documents).

**Impostare le opzioni di esecuzione**

È possibile impostare le opzioni di esecuzione che controllano il comportamento del servizio Assembler mentre esegue un processo. Ad esempio, è possibile impostare un&#39;opzione che indica al servizio Assembler di continuare l&#39;elaborazione di un processo in caso di errore. Per informazioni sulle opzioni di esecuzione che è possibile impostare, vedere il riferimento alla classe `AssemblerOptionSpec` in [Riferimento API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Assemblare i documenti PDF di input**

Dopo aver creato il client di servizio, fare riferimento a un file DDX, creare un oggetto raccolta che memorizza i documenti PDF di input e impostare le opzioni di esecuzione, è possibile richiamare l&#39;operazione DDX. Quando si utilizza il documento DDX specificato in questa sezione, i file map.pdf e Direction.pdf vengono uniti in un unico documento PDF.

**Estrarre i risultati**

Il servizio Assembler restituisce un oggetto `java.util.Map` che può essere ottenuto dall&#39;oggetto `AssemblerResult` e che contiene i risultati dell&#39;operazione. L&#39;oggetto `java.util.Map` restituito contiene i documenti risultanti ed eventuali eccezioni.

Nella tabella seguente sono riepilogati alcuni dei valori chiave e dei tipi di oggetto che è possibile individuare nell&#39;oggetto `java.util.Map` restituito.

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

## Assemblare documenti PDF utilizzando l&#39;API Java {#assemble-pdf-documents-using-the-java-api}

Assemblare un documento PDF utilizzando l&#39;API del servizio Assembler (Java):

1. Includi file di progetto.

   Includi file JAR client, come adobe-assembler-client.jar, nel percorso di classe del progetto Java.

1. Creare un client Assembler PDF.

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `AssemblerServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Fai riferimento a un documento DDX esistente.

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento DDX utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del file DDX.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Riferimento ai documenti PDF di input.

   * Creare un oggetto `java.util.Map` utilizzato per memorizzare i documenti PDF di input utilizzando un costruttore `HashMap`.
   * Per ciascun documento PDF di input, creare un oggetto `java.io.FileInputStream` utilizzando il relativo costruttore e passando la posizione del documento PDF di input.
   * Per ciascun documento PDF di input, creare un oggetto `com.adobe.idp.Document` e passare l&#39;oggetto `java.io.FileInputStream` che contiene il documento PDF.
   * Per ciascun documento di input, aggiungere una voce all&#39;oggetto `java.util.Map` richiamando il relativo metodo `put` e passando i seguenti argomenti:

      * Valore stringa che rappresenta il nome della chiave. Questo valore deve corrispondere al valore dell&#39;elemento di origine PDF specificato nel documento DDX.
      * Un oggetto `com.adobe.idp.Document` (o `java.util.List` che specifica più documenti) contenente il documento PDF di origine.

1. Impostare le opzioni di esecuzione.

   * Creare un oggetto `AssemblerOptionSpec` che memorizza le opzioni di esecuzione utilizzando il relativo costruttore.
   * Impostare le opzioni di esecuzione per soddisfare i requisiti aziendali richiamando un metodo appartenente all&#39;oggetto `AssemblerOptionSpec`. Ad esempio, per dare istruzioni al servizio Assembler di continuare a elaborare un processo quando si verifica un errore, richiamare il metodo `setFailOnError` dell&#39;oggetto `AssemblerOptionSpec` e passare `false`.

1. Assemblare i documenti PDF di input.

   Richiama il metodo `invokeDDX` dell&#39;oggetto `AssemblerServiceClient` e passa i seguenti valori obbligatori:

   * Un oggetto `com.adobe.idp.Document` che rappresenta il documento DDX da utilizzare
   * Un oggetto `java.util.Map` che contiene i file PDF di input da assemblare
   * Un oggetto `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` che specifica le opzioni di esecuzione, incluso il tipo di carattere predefinito e il livello di registro dei processi

   Il metodo `invokeDDX` restituisce un oggetto `com.adobe.livecycle.assembler.client.AssemblerResult` che contiene i risultati del processo ed eventuali eccezioni.

1. Estrai i risultati.

   Per ottenere il documento PDF appena creato, eseguire le operazioni seguenti:

   * Richiama il metodo `getDocuments` dell&#39;oggetto `AssemblerResult`. Restituisce un oggetto `java.util.Map`.
   * Iterare l&#39;oggetto `java.util.Map` fino a trovare l&#39;oggetto `com.adobe.idp.Document` risultante. Per ottenere il documento è possibile utilizzare l&#39;elemento risultato PDF specificato nel documento DDX.
   * Richiamare il metodo `copyToFile` dell&#39;oggetto `com.adobe.idp.Document` per estrarre il documento PDF.

   >[!NOTE]
   >
   >Se `LOG_LEVEL` è stato impostato per produrre un registro, è possibile estrarre il registro utilizzando il metodo `AssemblerResult` dell&#39;oggetto `getJobLog`.

**Consulta anche**

[Avvio rapido (modalità SOAP): Assemblaggio di un documento PDF utilizzando l’API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-a-pdf-document-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Assemblare documenti PDF utilizzando l&#39;API del servizio Web {#assemble-pdf-documents-using-the-web-service-api}

Assemblare documenti PDF utilizzando l&#39;API del servizio Assembler (servizio Web):

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
   * Compilare l&#39;oggetto `BLOB` assegnando la relativa proprietà `MTOM` con il contenuto dell&#39;array di byte.

1. Riferimento ai documenti PDF di input.

   * Per ciascun documento PDF di input, creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare il documento PDF di input.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF di input e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni dell&#39;array di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare l’array di byte con i dati del flusso richiamando il metodo `Read` dell’oggetto `System.IO.FileStream`. Passa la matrice dei byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando il relativo campo `MTOM` con il contenuto dell&#39;array di byte.
   * Creare un oggetto `MyMapOf_xsd_string_To_xsd_anyType`. Questo oggetto raccolta viene utilizzato per memorizzare i documenti PDF di input.
   * Per ciascun documento PDF di input, creare un oggetto `MyMapOf_xsd_string_To_xsd_anyType_Item`. Ad esempio, se si utilizzano due documenti PDF di input, creare due oggetti `MyMapOf_xsd_string_To_xsd_anyType_Item`.
   * Assegna un valore stringa che rappresenta il nome della chiave al campo `MyMapOf_xsd_string_To_xsd_anyType_Item` dell&#39;oggetto `key`. Questo valore deve corrispondere al valore dell&#39;elemento di origine PDF specificato nel documento DDX. Esegui questa operazione per ogni documento PDF di input.
   * Assegnare l&#39;oggetto `BLOB` che memorizza il documento PDF nel campo `MyMapOf_xsd_string_To_xsd_anyType_Item` dell&#39;oggetto `value`. Esegui questa operazione per ogni documento PDF di input.
   * Aggiungere l&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType_Item` all&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType`. Richiama il metodo `Add` dell&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType` e passa l&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType`. Esegui questa operazione per ogni documento PDF di input.

1. Impostare le opzioni di esecuzione.

   * Creare un oggetto `AssemblerOptionSpec` che memorizza le opzioni di esecuzione utilizzando il relativo costruttore.
   * Impostare le opzioni di esecuzione per soddisfare i requisiti aziendali assegnando un valore a un membro dati appartenente all&#39;oggetto `AssemblerOptionSpec`. Ad esempio, per dare istruzioni al servizio Assembler di continuare a elaborare un processo in caso di errore, assegna `false` al membro dati `AssemblerOptionSpec` dell&#39;oggetto `failOnError`.

1. Assemblare i documenti PDF di input.

   Richiama il metodo `invoke` dell&#39;oggetto `AssemblerServiceClient` e passa i seguenti valori:

   * Un oggetto `BLOB` che rappresenta il documento DDX.
   * Array `mapItem` contenente i documenti PDF di input. Le chiavi devono corrispondere ai nomi dei file di origine PDF e i relativi valori devono essere gli oggetti `BLOB` che corrispondono a tali file.
   * Un oggetto `AssemblerOptionSpec` che specifica le opzioni di esecuzione.

   Il metodo `invoke` restituisce un oggetto `AssemblerResult` che contiene i risultati del processo ed eventuali eccezioni.

1. Estrai i risultati.

   Per ottenere il documento PDF appena creato, eseguire le operazioni seguenti:

   * Accedere al campo `documents` dell&#39;oggetto `AssemblerResult`, che è un oggetto `Map` che contiene i documenti PDF risultanti.
   * Iterare l&#39;oggetto `Map` fino a trovare la chiave che corrisponde al nome del documento risultante. Quindi eseguire il cast di `value` del membro della matrice su un `BLOB`.
   * Estrarre i dati binari che rappresentano il documento PDF accedendo alla proprietà `MTOM` dell’oggetto `BLOB` corrispondente. Restituisce una matrice di byte che è possibile scrivere in un file PDF.

   >[!NOTE]
   >
   >Se `LOG_LEVEL` è stato impostato per produrre un registro, è possibile estrarre il registro ottenendo il valore del membro dati `AssemblerResult` dell&#39;oggetto `jobLog`.

**Consulta anche**

[Richiamo di AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
