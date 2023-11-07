---
title: Assemblaggio di documenti PDF a livello di programmazione
seo-title: Programmatically Assembling PDF Documents
description: Utilizza l’API del servizio Assembler per assemblare più documenti PDF in un singolo documento PDF utilizzando l’API Java e l’API del servizio Web.
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
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '2123'
ht-degree: 0%

---

# Assemblaggio di documenti PDF a livello di programmazione {#programmatically-assembling-pdf-documents}

**Gli esempi e gli esempi contenuti in questo documento sono solo per l’ambiente AEM Forms su JEE.**

È possibile utilizzare l’API del servizio Assembler per assemblare più documenti PDF in un unico documento PDF. Nella figura seguente sono illustrati tre documenti PDF che vengono uniti in un unico documento PDF.

![pa_pa_document_assembly](assets/pa_pa_document_assembly.png)

Per assemblare due o più documenti PDF in un unico documento PDF, è necessario un documento DDX. Un documento DDX descrive il documento PDF prodotto dal servizio Assembler. In altre parole, il documento DDX indica al servizio Assembler le azioni da eseguire.

Ai fini della presente discussione, si supponga che venga utilizzato il seguente documento DDX.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
     <PDF result="out.pdf">
         <PDF source="map.pdf" />
         <PDF source="directions.pdf" />
     </PDF>
 </DDX>
```

Questo documento DDX unisce due documenti PDF denominati *map.pdf* e *direction.pdf* in un unico documento PDF.

>[!NOTE]
>
>Per visualizzare un documento DDX che disassembla un documento PDF, vedere [Disassemblaggio di documenti PDF a livello di programmazione](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents).

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Assembler, vedere [Guida di riferimento dei servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Per ulteriori informazioni su un documento DDX, vedere [Servizio assemblatore e riferimento DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Considerazioni durante la chiamata del servizio Assembler tramite servizi Web {#considerations-when-invoking-assembler-service-using-web-services}

Quando si aggiungono intestazioni e piè di pagina durante l&#39;assemblaggio di documenti di grandi dimensioni, è possibile che si verifichi un `OutOfMemory` e i file non verranno assemblati. Per ridurre la possibilità che si verifichi questo problema, aggiungi una `DDXProcessorSetting` al documento DDX, come illustrato nell&#39;esempio seguente.

`<DDXProcessorSetting name="checkpoint" value="2000" />`

Puoi aggiungere questo elemento come elemento secondario di `DDX` elemento o come elemento figlio di un `PDF result` elemento. Il valore predefinito per questa impostazione è 0 (zero), che disattiva il checkpoint e il DDX si comporta come se `DDXProcessorSetting` elemento non presente. Se hai incontrato un `OutOfMemory` errore, potrebbe essere necessario impostare il valore su un numero intero, in genere compreso tra 500 e 5000. Un valore di checkpoint ridotto determina un checkpoint più frequente.

## Riepilogo dei passaggi {#summary-of-steps}

Per assemblare un singolo documento PDF da più documenti PDF, effettuare le seguenti operazioni:

1. Includi file di progetto.
1. Creare un client PDF Assembler.
1. Fare riferimento a un documento DDX esistente.
1. Fai riferimento ai documenti di input PDF.
1. Impostare le opzioni di runtime.
1. Assemblare i documenti di input PDF.
1. Estrai i risultati.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso della classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è implementato su JBoss)
* jbossall-client.jar (obbligatorio se AEM Forms è distribuito su JBoss)

se AEM Forms viene distribuito su un server applicazioni J2EE supportato diverso da JBoss, è necessario sostituire i file adobe-utilities.jar e jbossall-client.jar con file JAR specifici per il server applicazioni J2EE in cui viene distribuito AEM Forms.

**Creare un client PDF Assembler**

Prima di poter eseguire un&#39;operazione Assembler a livello di programmazione, è necessario creare un client Assembler.

**Riferimento a un documento DDX esistente**

Per assemblare un documento PDF è necessario fare riferimento a un documento DDX. Si consideri ad esempio il documento DDX introdotto in questa sezione. Questo documento DDX indica al servizio Assembler di unire due documenti PDF in un unico documento PDF.

**Documentazione di input PDF di riferimento**

Fare riferimento ai documenti di input PDF che si desidera passare al servizio Assembler. Se ad esempio si desidera trasmettere due documenti PDF di input denominati Mappa e Direzioni, è necessario trasmettere i file PDF corrispondenti.

Il file map.pdf e il file direction.pdf devono essere inseriti in un oggetto insieme. Il nome della chiave deve corrispondere al valore dell&#39;attributo di origine PDF nel documento DDX. Non importa quale sia il nome del file PDF se la chiave e l&#39;attributo di origine nel documento DDX corrispondono.

>[!NOTE]
>
>Un `AssemblerResult` , che contiene un oggetto insieme, viene restituito se si richiama `invokeDDX` operazione. Questa operazione viene utilizzata quando si trasmettono due o più documenti di input PDF al servizio Assembler. Tuttavia, se si passa un solo PDF di input al servizio Assembler e si prevede un solo documento restituito, richiamare `invokeOneDocument` operazione. Quando si richiama questa operazione, viene restituito un singolo documento. Per informazioni sull&#39;utilizzo di questa operazione, vedere [Assemblaggio di documenti PDF crittografati](/help/forms/developing/assembling-encrypted-pdf-documents.md#assembling-encrypted-pdf-documents).

**Impostare le opzioni di runtime**

È possibile impostare le opzioni di runtime che controllano il comportamento del servizio Assembler durante l&#39;esecuzione di un processo. È ad esempio possibile impostare un&#39;opzione che indichi al servizio Assembler di continuare l&#39;elaborazione di un processo in caso di errore. Per informazioni sulle opzioni di runtime impostabili, vedere `AssemblerOptionSpec` riferimento di classe in [Riferimento API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Assemblare i documenti di input PDF**

Dopo aver creato il client di servizio, aver creato un riferimento a un file DDX, creato un oggetto insieme che memorizza i documenti di input PDF e impostato le opzioni di runtime, è possibile richiamare l&#39;operazione DDX. Quando si utilizza il documento DDX specificato in questa sezione, i file map.pdf e direction.pdf vengono uniti in un unico documento PDF.

**Estrarre i risultati**

Il servizio Assembler restituisce un `java.util.Map` oggetto, che può essere ottenuto da `AssemblerResult` e che contiene i risultati dell&#39;operazione. Il restituito `java.util.Map` contiene i documenti risultanti ed eventuali eccezioni.

Nella tabella seguente vengono riepilogati alcuni dei valori chiave e dei tipi di oggetto che possono essere presenti nel `java.util.Map` oggetto.

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
   <td><p>Contiene i documenti risultanti specificati in un elemento DDX risultante</p></td>
  </tr>
  <tr>
   <td><p><code><i>documentName</i></code></p></td>
   <td><p><code>Exception</code></p></td>
   <td><p>Contiene qualsiasi eccezione per il documento</p></td>
  </tr>
  <tr>
   <td><p><code>OutputMapConstants.LOG_NAME</code></p></td>
   <td><p><code>com.adobe.idp.Documen</code></p></td>
   <td><p>Contiene il registro di processo</p></td>
  </tr>
 </tbody>
</table>

**Consulta anche**

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Disassemblaggio di documenti PDF a livello di programmazione](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

## Assemblare documenti PDF utilizzando l’API Java {#assemble-pdf-documents-using-the-java-api}

Assembla un documento PDF utilizzando l’API del servizio Assembler (Java):

1. Includi file di progetto.

   Includi i file JAR client, come adobe-assembler-client.jar, nel percorso di classe del progetto Java.

1. Creare un client PDF Assembler.

   * Creare un `ServiceClientFactory` oggetto che contiene proprietà di connessione.
   * Creare un `AssemblerServiceClient` mediante il costruttore e passando il `ServiceClientFactory` oggetto.

1. Fare riferimento a un documento DDX esistente.

   * Creare un `java.io.FileInputStream` oggetto che rappresenta il documento DDX utilizzando il relativo costruttore e passando un valore stringa che specifica la posizione del file DDX.
   * Creare un `com.adobe.idp.Document` mediante il costruttore e passando il `java.io.FileInputStream` oggetto.

1. Fai riferimento ai documenti di input PDF.

   * Creare un `java.util.Map` oggetto utilizzato per memorizzare i documenti di input PDF utilizzando un `HashMap` costruttore.
   * Per ogni documento di input PDF, crea un `java.io.FileInputStream` mediante il costruttore e passando la posizione del documento PDF di input.
   * Per ogni documento di input PDF, crea un `com.adobe.idp.Document` e passare il `java.io.FileInputStream` oggetto che contiene il documento PDF.
   * Per ogni documento di input, aggiungi una voce al `java.util.Map` oggetto richiamando il relativo `put` e fornendo i seguenti argomenti:

      * Valore stringa che rappresenta il nome della chiave. Questo valore deve corrispondere al valore dell&#39;elemento di origine PDF specificato nel documento DDX.
      * A `com.adobe.idp.Document` oggetto (o `java.util.List` oggetto che specifica più documenti) che contiene il documento PDF di origine.

1. Impostare le opzioni di runtime.

   * Creare un `AssemblerOptionSpec` oggetto che memorizza le opzioni di runtime mediante il relativo costruttore.
   * Impostare le opzioni di runtime per soddisfare i requisiti aziendali richiamando un metodo che appartiene al `AssemblerOptionSpec` oggetto. Ad esempio, per indicare al servizio Assembler di continuare l&#39;elaborazione di un processo quando si verifica un errore, richiamare `AssemblerOptionSpec` dell&#39;oggetto `setFailOnError` metodo e passaggio `false`.

1. Assemblare i documenti di input PDF.

   Richiama `AssemblerServiceClient` dell&#39;oggetto `invokeDDX` e trasmettere i seguenti valori richiesti:

   * A `com.adobe.idp.Document` oggetto che rappresenta il documento DDX da utilizzare
   * A `java.util.Map` oggetto contenente i file PDF di input da assemblare
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` oggetto che specifica le opzioni di runtime, incluso il tipo di carattere predefinito e il livello di registro del processo

   Il `invokeDDX` il metodo restituisce un `com.adobe.livecycle.assembler.client.AssemblerResult` oggetto contenente i risultati del processo ed eventuali eccezioni verificatesi.

1. Estrai i risultati.

   Per ottenere il documento di PDF appena creato, effettuare le seguenti operazioni:

   * Richiama `AssemblerResult` dell&#39;oggetto `getDocuments` metodo. Questo restituisce un `java.util.Map` oggetto.
   * Effettua iterazione attraverso `java.util.Map` finché non viene individuato il risultato `com.adobe.idp.Document` oggetto. È possibile utilizzare l&#39;elemento risultato PDF specificato nel documento DDX per ottenere il documento.
   * Richiama `com.adobe.idp.Document` dell&#39;oggetto `copyToFile` per estrarre il documento PDF.

   >[!NOTE]
   >
   >Se `LOG_LEVEL` è stato impostato per produrre un registro, è possibile estrarre il registro utilizzando `AssemblerResult` dell&#39;oggetto `getJobLog` metodo.

**Consulta anche**

[Guida rapida (modalità SOAP): assemblaggio di un documento PDF tramite l’API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-a-pdf-document-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Assemblare documenti PDF utilizzando l’API del servizio web {#assemble-pdf-documents-using-the-web-service-api}

Assemblare documenti PDF utilizzando l’API del servizio Assembler (servizio web):

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

1. Fai riferimento ai documenti di input PDF.

   * Per ogni documento di input PDF, crea un `BLOB` mediante il costruttore. Il `BLOB` L&#39;oggetto viene utilizzato per memorizzare il documento di input PDF.
   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore stringa che rappresenta la posizione del file del documento di input PDF e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto della `System.IO.FileStream` oggetto. È possibile determinare le dimensioni della matrice di byte ottenendo `System.IO.FileStream` dell&#39;oggetto `Length` proprietà.
   * Compilare la matrice di byte con i dati di flusso richiamando `System.IO.FileStream` dell&#39;oggetto `Read` metodo. Passare la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare il `BLOB` oggetto assegnando il relativo `MTOM` con il contenuto della matrice di byte.
   * Creare un `MyMapOf_xsd_string_To_xsd_anyType` oggetto. Questo oggetto insieme viene utilizzato per memorizzare i documenti di input PDF.
   * Per ogni documento di input PDF, crea un `MyMapOf_xsd_string_To_xsd_anyType_Item` oggetto. Se ad esempio si utilizzano due documenti di input PDF, creare due `MyMapOf_xsd_string_To_xsd_anyType_Item` oggetti.
   * Assegna un valore stringa che rappresenta il nome della chiave al `MyMapOf_xsd_string_To_xsd_anyType_Item` dell&#39;oggetto `key` campo. Questo valore deve corrispondere al valore dell&#39;elemento di origine PDF specificato nel documento DDX. (Eseguire questa operazione per ogni documento di input PDF).
   * Assegna la `BLOB` oggetto che memorizza il documento PDF in `MyMapOf_xsd_string_To_xsd_anyType_Item` dell&#39;oggetto `value` campo. (Eseguire questa operazione per ogni documento di input PDF).
   * Aggiungi il `MyMapOf_xsd_string_To_xsd_anyType_Item` oggetto al `MyMapOf_xsd_string_To_xsd_anyType` oggetto. Richiama `MyMapOf_xsd_string_To_xsd_anyType` dell&#39;oggetto `Add` e trasmettere il `MyMapOf_xsd_string_To_xsd_anyType` oggetto. (Eseguire questa operazione per ogni documento di input PDF).

1. Impostare le opzioni di runtime.

   * Creare un `AssemblerOptionSpec` oggetto che memorizza le opzioni di runtime mediante il relativo costruttore.
   * Impostare le opzioni di runtime per soddisfare i requisiti aziendali assegnando un valore a un membro dati che appartiene al `AssemblerOptionSpec` oggetto. Ad esempio, per indicare al servizio Assembler di continuare l&#39;elaborazione di un processo quando si verifica un errore, assegnare `false` al `AssemblerOptionSpec` dell&#39;oggetto `failOnError` membro dati.

1. Assemblare i documenti di input PDF.

   Richiama `AssemblerServiceClient` dell&#39;oggetto `invoke` e trasmettere i seguenti valori:

   * A `BLOB` oggetto che rappresenta il documento DDX.
   * Il `mapItem` array contenente i documenti PDF di input. Le chiavi devono corrispondere ai nomi dei file di origine di PDF e i relativi valori devono essere `BLOB` oggetti corrispondenti a tali file.
   * Un `AssemblerOptionSpec` oggetto che specifica le opzioni di runtime.

   Il `invoke` il metodo restituisce un `AssemblerResult` oggetto contenente i risultati del processo ed eventuali eccezioni.

1. Estrai i risultati.

   Per ottenere il documento di PDF appena creato, effettuare le seguenti operazioni:

   * Accedere a `AssemblerResult` dell&#39;oggetto `documents` campo, che è un `Map` oggetto che contiene i documenti PDF risultanti.
   * Effettua iterazione attraverso `Map` finché non viene individuata la chiave corrispondente al nome del documento risultante. Quindi esegui il cast del membro dell’array `value` a un `BLOB`.
   * Estrarre i dati binari che rappresentano il documento PDF accedendo al relativo `BLOB` dell&#39;oggetto `MTOM` proprietà. Restituisce una matrice di byte che è possibile scrivere in un file PDF.

   >[!NOTE]
   >
   >Se `LOG_LEVEL` è stato impostato per produrre un registro, è possibile estrarre il registro ottenendo il valore `AssemblerResult` dell&#39;oggetto `jobLog` membro dati.

**Consulta anche**

[Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
