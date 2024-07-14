---
title: Assemblaggio di documenti PDF a livello di programmazione
description: Utilizza l’API del servizio Assembler per assemblare più documenti PDF in un singolo documento PDF utilizzando l’API Java e l’API del servizio Web.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 7d6fd230-e477-4286-9fb3-18a3474e3e48
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '2105'
ht-degree: 0%

---

# Assemblaggio di documenti PDF a livello di programmazione {#programmatically-assembling-pdf-documents}

**Gli esempi e gli esempi contenuti in questo documento sono solo per AEM Forms in ambiente JEE.**

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
>Per visualizzare un documento DDX che disassembla un documento PDF, vedere [Disassemblaggio a livello di codice dei documenti PDF](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents).

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Assembler, vedere [Riferimento ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Per ulteriori informazioni su un documento DDX, vedere [Servizio assemblatore e riferimento DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Considerazioni durante la chiamata del servizio Assembler tramite servizi Web {#considerations-when-invoking-assembler-service-using-web-services}

Quando si aggiungono intestazioni e piè di pagina durante l&#39;assemblaggio di documenti di grandi dimensioni, è possibile che si verifichi un errore `OutOfMemory` e che i file non vengano assemblati. Per ridurre la possibilità che si verifichi questo problema, aggiungere un elemento `DDXProcessorSetting` al documento DDX, come illustrato nell&#39;esempio seguente.

`<DDXProcessorSetting name="checkpoint" value="2000" />`

È possibile aggiungere questo elemento come elemento figlio dell&#39;elemento `DDX` o come elemento figlio di un elemento `PDF result`. Il valore predefinito per questa impostazione è 0 (zero), che disattiva il checkpoint e il DDX si comporta come se l&#39;elemento `DDXProcessorSetting` non fosse presente. Se si verifica un errore `OutOfMemory`, potrebbe essere necessario impostare il valore su un numero intero, in genere compreso tra 500 e 5000. Un valore di checkpoint ridotto determina un checkpoint più frequente.

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

**Creare un client Assembler PDF**

Prima di poter eseguire un&#39;operazione Assembler a livello di programmazione, è necessario creare un client Assembler.

**Riferimento a un documento DDX esistente**

Per assemblare un documento PDF è necessario fare riferimento a un documento DDX. Si consideri ad esempio il documento DDX introdotto in questa sezione. Questo documento DDX indica al servizio Assembler di unire due documenti PDF in un unico documento PDF.

**Riferimento ai documenti di input PDF**

Fare riferimento ai documenti di input PDF che si desidera passare al servizio Assembler. Se ad esempio si desidera trasmettere due documenti PDF di input denominati Mappa e Direzioni, è necessario trasmettere i file PDF corrispondenti.

Il file map.pdf e il file direction.pdf devono essere inseriti in un oggetto insieme. Il nome della chiave deve corrispondere al valore dell&#39;attributo di origine PDF nel documento DDX. Non importa quale sia il nome del file PDF se la chiave e l&#39;attributo di origine nel documento DDX corrispondono.

>[!NOTE]
>
>Se si richiama l&#39;operazione `invokeDDX`, viene restituito un oggetto `AssemblerResult` contenente un insieme. Questa operazione viene utilizzata quando si trasmettono due o più documenti di input PDF al servizio Assembler. Tuttavia, se si passa un solo PDF di input al servizio Assembler e si prevede un solo documento restituito, richiamare l&#39;operazione `invokeOneDocument`. Quando si richiama questa operazione, viene restituito un singolo documento. Per informazioni sull&#39;utilizzo di questa operazione, vedere [Assemblaggio di documenti crittografati di PDF](/help/forms/developing/assembling-encrypted-pdf-documents.md#assembling-encrypted-pdf-documents).

**Impostare le opzioni di runtime**

È possibile impostare le opzioni di runtime che controllano il comportamento del servizio Assembler durante l&#39;esecuzione di un processo. È ad esempio possibile impostare un&#39;opzione che indichi al servizio Assembler di continuare l&#39;elaborazione di un processo in caso di errore. Per informazioni sulle opzioni di runtime che è possibile impostare, vedere il riferimento alla classe `AssemblerOptionSpec` in [Riferimento API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Assemblare i documenti di input PDF**

Dopo aver creato il client di servizio, aver creato un riferimento a un file DDX, creato un oggetto insieme che memorizza i documenti di input PDF e impostato le opzioni di runtime, è possibile richiamare l&#39;operazione DDX. Quando si utilizza il documento DDX specificato in questa sezione, i file map.pdf e direction.pdf vengono uniti in un unico documento PDF.

**Estrai i risultati**

Il servizio Assembler restituisce un oggetto `java.util.Map` che può essere ottenuto dall&#39;oggetto `AssemblerResult` e che contiene i risultati dell&#39;operazione. L&#39;oggetto `java.util.Map` restituito contiene i documenti risultanti ed eventuali eccezioni.

Nella tabella seguente vengono riepilogati alcuni dei valori chiave e dei tipi di oggetto che possono trovarsi nell&#39;oggetto `java.util.Map` restituito.

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

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `AssemblerServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Fare riferimento a un documento DDX esistente.

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento DDX utilizzando il relativo costruttore e passando un valore stringa che specifica la posizione del file DDX.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Fai riferimento ai documenti di input PDF.

   * Creare un oggetto `java.util.Map` utilizzato per memorizzare i documenti di input PDF utilizzando un costruttore `HashMap`.
   * Per ogni documento di input PDF, creare un oggetto `java.io.FileInputStream` utilizzando il relativo costruttore e passando la posizione del documento di input PDF.
   * Per ogni documento di input PDF, creare un oggetto `com.adobe.idp.Document` e passare l&#39;oggetto `java.io.FileInputStream` che contiene il documento di input PDF.
   * Per ogni documento di input, aggiungere una voce all&#39;oggetto `java.util.Map` richiamando il relativo metodo `put` e passando i seguenti argomenti:

      * Valore stringa che rappresenta il nome della chiave. Questo valore deve corrispondere al valore dell&#39;elemento di origine PDF specificato nel documento DDX.
      * Oggetto `com.adobe.idp.Document` (o `java.util.List` che specifica più documenti) contenente il documento PDF di origine.

1. Impostare le opzioni di runtime.

   * Creare un oggetto `AssemblerOptionSpec` che memorizza le opzioni di runtime utilizzando il relativo costruttore.
   * Impostare le opzioni di runtime per soddisfare i requisiti aziendali richiamando un metodo che appartiene all&#39;oggetto `AssemblerOptionSpec`. Ad esempio, per indicare al servizio Assembler di continuare a elaborare un processo quando si verifica un errore, richiamare il metodo `setFailOnError` dell&#39;oggetto `AssemblerOptionSpec` e passare `false`.

1. Assemblare i documenti di input PDF.

   Richiama il metodo `invokeDDX` dell&#39;oggetto `AssemblerServiceClient` e passa i seguenti valori richiesti:

   * Oggetto `com.adobe.idp.Document` che rappresenta il documento DDX da utilizzare
   * Oggetto `java.util.Map` contenente i file PDF di input da assemblare
   * Oggetto `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` che specifica le opzioni di runtime, inclusi il tipo di carattere predefinito e il livello di registro del processo

   Il metodo `invokeDDX` restituisce un oggetto `com.adobe.livecycle.assembler.client.AssemblerResult` contenente i risultati del processo ed eventuali eccezioni.

1. Estrai i risultati.

   Per ottenere il documento di PDF appena creato, effettuare le seguenti operazioni:

   * Richiama il metodo `getDocuments` dell&#39;oggetto `AssemblerResult`. Restituisce un oggetto `java.util.Map`.
   * Scorrere l&#39;oggetto `java.util.Map` fino a trovare l&#39;oggetto `com.adobe.idp.Document` risultante. È possibile utilizzare l&#39;elemento risultato PDF specificato nel documento DDX per ottenere il documento.
   * Richiama il metodo `copyToFile` dell&#39;oggetto `com.adobe.idp.Document` per estrarre il documento PDF.

   >[!NOTE]
   >
   >Se `LOG_LEVEL` è stato impostato per produrre un registro, è possibile estrarlo utilizzando il metodo `getJobLog` dell&#39;oggetto `AssemblerResult`.

**Consulta anche**

[Quick Start (modalità SOAP): assemblaggio di un documento PDF tramite API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-a-pdf-document-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Assemblare documenti PDF utilizzando l’API del servizio web {#assemble-pdf-documents-using-the-web-service-api}

Assemblare documenti PDF utilizzando l’API del servizio Assembler (servizio web):

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
   * Compilare l&#39;oggetto `BLOB` assegnando la relativa proprietà `MTOM` al contenuto della matrice di byte.

1. Fai riferimento ai documenti di input PDF.

   * Per ogni documento di input PDF, creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare il documento PDF di input.
   * Creare un oggetto `System.IO.FileStream` richiamandone il costruttore e passando un valore stringa che rappresenta la posizione del file del documento PDF di input e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni della matrice di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare la matrice di byte con i dati di flusso richiamando il metodo `Read` dell&#39;oggetto `System.IO.FileStream`. Passare la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando il relativo campo `MTOM` al contenuto della matrice di byte.
   * Creare un oggetto `MyMapOf_xsd_string_To_xsd_anyType`. Questo oggetto insieme viene utilizzato per memorizzare i documenti di input PDF.
   * Per ogni documento di input PDF, creare un oggetto `MyMapOf_xsd_string_To_xsd_anyType_Item`. Se ad esempio si utilizzano due documenti di input PDF, creare due oggetti `MyMapOf_xsd_string_To_xsd_anyType_Item`.
   * Assegnare un valore stringa che rappresenta il nome chiave al campo `key` dell&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType_Item`. Questo valore deve corrispondere al valore dell&#39;elemento di origine PDF specificato nel documento DDX. (Eseguire questa operazione per ogni documento di input PDF).
   * Assegnare l&#39;oggetto `BLOB` che memorizza il documento PDF al campo `value` dell&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType_Item`. (Eseguire questa operazione per ogni documento di input PDF).
   * Aggiungere l&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType_Item` all&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType`. Richiama il metodo `Add` dell&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType` e passa l&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType`. (Eseguire questa operazione per ogni documento di input PDF).

1. Impostare le opzioni di runtime.

   * Creare un oggetto `AssemblerOptionSpec` che memorizza le opzioni di runtime utilizzando il relativo costruttore.
   * Impostare le opzioni di runtime per soddisfare i requisiti aziendali assegnando un valore a un membro dati che appartiene all&#39;oggetto `AssemblerOptionSpec`. Ad esempio, per indicare al servizio Assembler di continuare a elaborare un processo quando si verifica un errore, assegnare `false` al membro dati `failOnError` dell&#39;oggetto `AssemblerOptionSpec`.

1. Assemblare i documenti di input PDF.

   Richiama il metodo `invoke` dell&#39;oggetto `AssemblerServiceClient` e passa i seguenti valori:

   * Oggetto `BLOB` che rappresenta il documento DDX.
   * Matrice `mapItem` contenente i documenti PDF di input. Le chiavi devono corrispondere ai nomi dei file di origine di PDF e i relativi valori devono essere gli oggetti `BLOB` corrispondenti a tali file.
   * Oggetto `AssemblerOptionSpec` che specifica le opzioni di runtime.

   Il metodo `invoke` restituisce un oggetto `AssemblerResult` contenente i risultati del processo ed eventuali eccezioni.

1. Estrai i risultati.

   Per ottenere il documento di PDF appena creato, effettuare le seguenti operazioni:

   * Accedere al campo `documents` dell&#39;oggetto `AssemblerResult`, che è un oggetto `Map` contenente i documenti PDF risultanti.
   * Scorrere l&#39;oggetto `Map` fino a trovare la chiave corrispondente al nome del documento risultante. Quindi esegui il cast di `value` del membro dell&#39;array in un `BLOB`.
   * Estrarre i dati binari che rappresentano il documento PDF accedendo alla proprietà `MTOM` dell&#39;oggetto `BLOB`. Restituisce una matrice di byte che è possibile scrivere in un file PDF.

   >[!NOTE]
   >
   >Se `LOG_LEVEL` è stato impostato per produrre un log, è possibile estrarre il log ottenendo il valore del membro dati `jobLog` dell&#39;oggetto `AssemblerResult`.

**Consulta anche**

[Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
