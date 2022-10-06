---
title: Assemblaggio di documenti utilizzando la numerazione dei bates
seo-title: Assembling Documents Using Bates Numbering
description: Utilizzare la numerazione Bates per assemblare documenti PDF utilizzando l’API Java e Web Service.
seo-description: Use Bates numbering to assemble PDF documents using the Java and Web Service API.
uuid: 28d5faeb-6915-41a2-b6a0-78d255df024f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 77e9b895-1313-4a5b-a2d5-cdb65bdc1966
role: Developer
exl-id: 2a4e21c4-f2f5-44cd-b8ed-7b572782a2f1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1922'
ht-degree: 0%

---

# Assemblaggio di documenti utilizzando la numerazione dei bates {#assembling-documents-using-bates-numbering}

**Esempi ed esempi in questo documento sono solo per AEM Forms in ambiente JEE.**

È possibile assemblare documenti PDF contenenti identificatori di pagina univoci utilizzando la numerazione Bates. *Numerazione delle barre* è un metodo per applicare identificazioni univoche a un batch di documenti correlati. A ogni pagina del documento (o set di documenti) viene assegnato un numero Bates che identifica in modo univoco la pagina. Ad esempio, i documenti di fabbricazione che contengono informazioni sulla distinta base e sono associati alla produzione di un assieme possono contenere un identificatore. Un numero Bates contiene un valore numerico sequenzialmente incrementato e un prefisso e un suffisso facoltativi. Il prefisso + numerico + suffisso è indicato come *pattern a bordate*.

L’illustrazione seguente mostra un documento PDF contenente un identificatore univoco presente nell’intestazione del documento.

![au_au_batesnumber](assets/au_au_batesnumber.png)

Ai fini di questa discussione, l’identificatore univoco della pagina viene inserito nell’intestazione di un documento. Si supponga di utilizzare il seguente documento DDX.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
        <PDF result="out.pdf">
        <Header>
         <Center>
             <StyledText>
                 <p font-size="20pt"><BatesNumber/></p>
             </StyledText>
         </Center>
     </Header>
           <PDF source="map.pdf" />
          <PDF source="directions.pdf" />
          </PDF>
 </DDX>
```

Questo documento DDX unisce due documenti PDF denominati *map.pdf* e *sections.pdf* in un singolo documento PDF. Il documento PDF risultante contiene un’intestazione costituita da un identificatore di pagina univoco. Ad esempio, il documento nell&#39;illustrazione precedente mostra 000016.

>[!NOTE]
>
>Prima di leggere questa sezione, è consigliabile avere familiarità con l’assemblaggio di documenti PDF tramite il servizio Assembler. In questa sezione non vengono descritti i concetti, ad esempio la creazione di un oggetto raccolta contenente documenti di input o l&#39;estrazione dei risultati dall&#39;oggetto raccolta restituito. (Vedi [Assemblaggio di documenti PDF a livello di programmazione](/help/forms/developing/programmatically-assembling-pdf-documents.md).)

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Assembler, vedere [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Per ulteriori informazioni su un documento DDX, consulta [Servizio di assemblaggio e riferimento DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Riepilogo dei passaggi {#summary-of-steps}

Per assemblare un documento PDF contenente un identificatore di pagina univoco (numerazione Bates), eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Creare un client PDF Assembler.
1. Fai riferimento a un documento DDX esistente.
1. Riferimento ai documenti PDF di input.
1. Impostare il valore del numero Bates iniziale.
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

Se AEM Forms è distribuito su un server applicazioni J2EE supportato diverso da JBoss, è necessario sostituire i file adobe-utilities.jar e jbossall-client.jar con file JAR specifici per il server applicazioni J2EE in cui viene distribuito AEM Forms. Per informazioni sulla posizione di tutti i file JAR di AEM Forms, vedi [Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un client PDF Assembler**

Prima di poter eseguire un&#39;operazione Assembler a livello di programmazione, è necessario creare un client di servizio Assembler.

**Riferimento a un documento DDX esistente**

Per assemblare un documento PDF è necessario fare riferimento a un documento DDX. Ad esempio, considera il documento DDX introdotto in questa sezione. Per assemblare un documento PDF che contiene identificatori di pagina univoci, il documento DDX deve contenere `BatesNumber` elemento.

**Riferimento ai documenti PDF**

Per assemblare un documento PDF, è necessario fare riferimento ai documenti PDF di input. Ad esempio, per assemblare questi documenti PDF in un unico documento PDF è necessario fare riferimento ai documenti map.pdf e directs.pdf .

**Imposta il valore numero Bates iniziale**

È possibile impostare il valore iniziale del numero Bates in modo da soddisfare i requisiti aziendali. Ad esempio, si supponga che sia necessario impostare il valore iniziale su 000100. Se non si imposta il valore iniziale, il valore della prima pagina è 000000.

**Assemblare i documenti di input PDF**

Dopo aver creato il client di servizio Assembler, fare riferimento al documento DDX che contiene `BatesNumber` informazioni sugli elementi, fare riferimento a un documento di input PDF e impostare le opzioni di esecuzione, è possibile richiamare `invokeDDX` che consente al servizio Assembler di assemblare un documento PDF contenente identificatori di pagina univoci.

**Estrarre i risultati**

Il servizio Assembler restituisce un oggetto raccolta contenente i risultati del processo. È possibile estrarre il documento PDF risultante ed eventuali eccezioni generate. In questa situazione, all&#39;interno dell&#39;oggetto raccolta si trova un documento PDF crittografato.

>[!NOTE]
>
>Viene restituito un oggetto raccolta se si richiama l&#39; `invokeDDX` funzionamento. Questa operazione viene utilizzata quando si passano due o più documenti di input PDF al servizio Assembler. Tuttavia, se si passa un solo documento di input PDF al servizio Assembler, è necessario richiamare il `invokeOneDocument` funzionamento. Per informazioni sull&#39;utilizzo di questa operazione, vedi [Assemblaggio di documenti PDF crittografati](/help/forms/developing/assembling-encrypted-pdf-documents.md).

**Consulta anche**

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Assemblaggio di documenti PDF a livello di programmazione](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Assemblare i documenti con la numerazione Bates utilizzando l&#39;API Java {#assemble-documents-with-bates-numbering-using-the-java-api}

Assemblare un documento PDF che utilizza identificatori di pagina univoci (numerazione Bates) utilizzando l&#39;API del servizio Assembler (Java):

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
   * Per ogni documento di input PDF, crea un `java.io.FileInputStream` utilizzando il relativo costruttore e passando la posizione del documento di input PDF. In questa situazione, passare la posizione di un documento PDF non protetto.
   * Per ogni documento di input PDF, crea un `com.adobe.idp.Document` e passare `java.io.FileInputStream` oggetto contenente il documento PDF.
   * Aggiungi una voce al `java.util.Map` richiamandone l&#39;oggetto `put` e passare gli argomenti seguenti:

      * Valore stringa che rappresenta il nome della chiave. Questo valore deve corrispondere al valore dell&#39;elemento di origine PDF specificato nel documento DDX. Ad esempio, il nome del file di origine PDF specificato nel documento DDX introdotto in questa sezione è Loan.pdf.
      * A `com.adobe.idp.Document` oggetto contenente il documento PDF non protetto.

1. Impostare il valore del numero Bates iniziale.

   * Crea un `AssemblerOptionSpec` oggetto che memorizza le opzioni di esecuzione utilizzando il relativo costruttore.
   * Imposta il numero iniziale di Bates richiamando il `AssemblerOptionSpec` dell’oggetto `setFirstBatesNumber` e passare un valore numerico che specifica il valore iniziale.

1. Assemblare i documenti di input PDF.

   Richiama il `AssemblerServiceClient` dell’oggetto `invokeDDX` e trasmettere i seguenti valori richiesti:

   * A `com.adobe.idp.Document` oggetto che rappresenta il documento DDX.
   * A `java.util.Map` oggetto che contiene il file PDF non protetto di input.
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` oggetto che specifica le opzioni di esecuzione, incluso il livello di carattere predefinito e di registro dei processi.

   La `invokeDDX` restituisce un `com.adobe.livecycle.assembler.client.AssemblerResult` oggetto contenente un documento PDF crittografato con password.

1. Estrai i risultati.

   Per ottenere il documento PDF appena creato, eseguire le operazioni seguenti:

   * Richiama il `AssemblerResult` dell’oggetto `getDocuments` metodo . Questa azione restituisce un `java.util.Map` oggetto.
   * Itera attraverso il `java.util.Map` finché non trovi `com.adobe.idp.Document` oggetto.
   * Richiama il `com.adobe.idp.Document` dell’oggetto `copyToFile` per estrarre il documento PDF.

**Consulta anche**

[Avvio rapido (modalità SOAP): Assemblaggio di un documento PDF con la numerazione dei percorsi utilizzando l’API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-a-pdf-document-with-bates-numbering-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Assemblare i documenti con la numerazione Bates utilizzando l&#39;API del servizio Web {#assemble-documents-with-bates-numbering-using-the-web-service-api}

Assemblare un documento PDF che utilizza identificatori di pagina univoci (numerazione Bates) utilizzando l&#39;API del servizio Assembler (servizio Web):

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
   * Crea un `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento DDX e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto del `System.IO.FileStream` oggetto. È possibile determinare le dimensioni dell&#39;array di byte ottenendo il `System.IO.FileStream` dell’oggetto `Length` proprietà.
   * Compilare l&#39;array di byte con i dati del flusso richiamando il `System.IO.FileStream` dell’oggetto `Read` metodo . Passa la matrice dei byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare `BLOB` oggetto assegnando il relativo `MTOM` con il contenuto dell&#39;array di byte.

1. Riferimento ai documenti PDF di input.

   * Per ogni documento di input PDF, crea un `BLOB` utilizzando il relativo costruttore. La `BLOB` viene utilizzato per memorizzare il documento di input PDF.
   * Crea un `System.IO.FileStream` richiamando il relativo costruttore. Passa un valore stringa che rappresenta la posizione del file del documento PDF di input e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto del `System.IO.FileStream` oggetto. È possibile determinare le dimensioni dell&#39;array di byte ottenendo il `System.IO.FileStream` dell’oggetto `Length` proprietà.
   * Compilare l&#39;array di byte con i dati del flusso richiamando il `System.IO.FileStream` dell’oggetto `Read` metodo . Passa la matrice dei byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare `BLOB` oggetto assegnando il relativo `MTOM` con il contenuto dell&#39;array di byte.
   * Crea un `MyMapOf_xsd_string_To_xsd_anyType` oggetto. Questo oggetto raccolta viene utilizzato per memorizzare i documenti PDF di input.
   * Per ogni documento di input PDF, crea un `MyMapOf_xsd_string_To_xsd_anyType_Item` oggetto. Ad esempio, se si utilizzano due documenti PDF di input, crearne due `MyMapOf_xsd_string_To_xsd_anyType_Item` oggetti.
   * Assegna un valore stringa che rappresenta il nome della chiave al `MyMapOf_xsd_string_To_xsd_anyType_Item` dell&#39;oggetto `key` campo . Questo valore deve corrispondere al valore dell&#39;elemento di origine PDF specificato nel documento DDX. Esegui questa operazione per ogni documento di input PDF.
   * Assegna `BLOB` oggetto che memorizza il documento PDF nella `MyMapOf_xsd_string_To_xsd_anyType_Item` dell&#39;oggetto `value` campo . Esegui questa operazione per ogni documento di input PDF.
   * Aggiungi il `MyMapOf_xsd_string_To_xsd_anyType_Item` dell&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType` oggetto. Richiama il `MyMapOf_xsd_string_To_xsd_anyType` dell&#39;oggetto `Add` e passare il `MyMapOf_xsd_string_To_xsd_anyType` oggetto. Esegui questa operazione per ogni documento di input PDF.

1. Impostare il valore del numero Bates iniziale.

   * Crea un `AssemblerOptionSpec` oggetto che memorizza le opzioni di esecuzione utilizzando il relativo costruttore.
   * Impostare il numero iniziale di Bates assegnando un valore numerico al `firstBatesNumber` membro dei dati che appartiene al `AssemblerOptionSpec` oggetto.

1. Assemblare i documenti di input PDF.

   Richiama il `AssemblerServiceClient` dell’oggetto `invoke` e passare i seguenti valori:

   * A `BLOB` oggetto che rappresenta il documento DDX.
   * La `MyMapOf_xsd_string_To_xsd_anyType` oggetto che contiene i documenti PDF di input. Le chiavi devono corrispondere ai nomi dei file di origine di PDF e i relativi valori devono essere `BLOB` oggetti corrispondenti a tali file.
   * Un `AssemblerOptionSpec` oggetto che specifica le opzioni di esecuzione.

   La `invoke` restituisce un `AssemblerResult` oggetto contenente i risultati del processo ed eventuali eccezioni.

1. Estrai i risultati.

   Per ottenere il documento PDF appena creato, eseguire le operazioni seguenti:

   * Accedere al `AssemblerResult` dell’oggetto `documents` un campo `Map` oggetto contenente i documenti PDF risultanti.
   * Itera attraverso il `Map` finché non viene trovata la chiave che corrisponde al nome del documento risultante. Quindi eseguire il cast del membro della matrice `value` a `BLOB`.
   * Estrarre i dati binari che rappresentano il documento PDF accedendo ai relativi `BLOB` dell’oggetto `MTOM` proprietà. Restituisce una matrice di byte che è possibile scrivere in un file PDF.

**Consulta anche**

[Richiamo di AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
