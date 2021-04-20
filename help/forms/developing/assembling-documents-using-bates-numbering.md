---
title: Assemblaggio di documenti utilizzando la numerazione dei bates
seo-title: Assemblaggio di documenti utilizzando la numerazione dei bates
description: 'Utilizzare la numerazione Bates per assemblare documenti PDF utilizzando l''API Java e Web Service. '
seo-description: 'Utilizzare la numerazione Bates per assemblare documenti PDF utilizzando l''API Java e Web Service. '
uuid: 28d5faeb-6915-41a2-b6a0-78d255df024f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 77e9b895-1313-4a5b-a2d5-cdb65bdc1966
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1942'
ht-degree: 0%

---


# Assemblaggio di documenti utilizzando la numerazione dei Bates {#assembling-documents-using-bates-numbering}

**Esempi ed esempi in questo documento sono solo per AEM Forms in ambiente JEE.**

È possibile assemblare documenti PDF contenenti identificatori di pagina univoci utilizzando la numerazione Bates. *La* numerazione Bates è un metodo per applicare identificazioni univoche a un batch di documenti correlati. A ogni pagina del documento (o set di documenti) viene assegnato un numero Bates che identifica in modo univoco la pagina. Ad esempio, i documenti di fabbricazione che contengono informazioni sulla distinta base e sono associati alla produzione di un assieme possono contenere un identificatore. Un numero Bates contiene un valore numerico sequenzialmente incrementato e un prefisso e un suffisso facoltativi. Il prefisso + suffisso numerico + è indicato come *pattern di bates*.

L’illustrazione seguente mostra un documento PDF contenente un identificatore univoco situato nell’intestazione del documento.

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

Questo documento DDX unisce due documenti PDF denominati *map.pdf* e *directs.pdf* in un singolo documento PDF. Il documento PDF risultante contiene un’intestazione costituita da un identificatore di pagina univoco. Ad esempio, il documento nell&#39;illustrazione precedente mostra 000016.

>[!NOTE]
>
>Prima di leggere questa sezione, si consiglia di avere familiarità con l&#39;assemblaggio di documenti PDF utilizzando il servizio Assembler. In questa sezione non vengono descritti i concetti, ad esempio la creazione di un oggetto raccolta contenente documenti di input o l&#39;estrazione dei risultati dall&#39;oggetto raccolta restituito. (Vedere [Assemblaggio programmatico di documenti PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md).)

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Assembler, vedere [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Per ulteriori informazioni su un documento DDX, vedere [Servizio Assembler e Riferimento DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Riepilogo dei passaggi {#summary-of-steps}

Per assemblare un documento PDF contenente un identificatore di pagina univoco (numerazione Bates), eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Creare un client Assembler PDF.
1. Fai riferimento a un documento DDX esistente.
1. Riferimento ai documenti PDF di input.
1. Impostare il valore del numero Bates iniziale.
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

Se AEM Forms è distribuito su un server applicazioni J2EE supportato diverso da JBoss, è necessario sostituire i file adobe-utilities.jar e jbossall-client.jar con file JAR specifici per il server applicazioni J2EE in cui viene distribuito AEM Forms. Per informazioni sulla posizione di tutti i file JAR di AEM Forms, consulta [Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un client Assembler PDF**

Prima di poter eseguire un&#39;operazione Assembler a livello di programmazione, è necessario creare un client di servizio Assembler.

**Riferimento a un documento DDX esistente**

Per assemblare un documento PDF è necessario fare riferimento a un documento DDX. Ad esempio, considera il documento DDX introdotto in questa sezione. Per assemblare un documento PDF che contiene identificatori di pagina univoci, il documento DDX deve contenere l&#39;elemento `BatesNumber`.

**Riferimento a documenti PDF di input**

Per assemblare un documento PDF è necessario fare riferimento ai documenti PDF di input. Per assemblare questi documenti PDF in un unico documento PDF, ad esempio, è necessario fare riferimento ai documenti map.pdf e sections.pdf.

**Imposta il valore numero Bates iniziale**

È possibile impostare il valore iniziale del numero Bates in modo da soddisfare i requisiti aziendali. Ad esempio, si supponga che sia necessario impostare il valore iniziale su 000100. Se non si imposta il valore iniziale, il valore della prima pagina è 000000.

**Assemblare i documenti PDF di input**

Dopo aver creato il client di servizio Assembler, fare riferimento al documento DDX contenente le informazioni relative agli elementi `BatesNumber`, fare riferimento a un documento PDF di input e impostare le opzioni di esecuzione, è possibile richiamare l&#39;operazione `invokeDDX` che consente al servizio Assembler di assemblare un documento PDF contenente identificatori di pagina univoci.

**Estrarre i risultati**

Il servizio Assembler restituisce un oggetto raccolta contenente i risultati del processo. È possibile estrarre il documento PDF risultante ed eventuali eccezioni generate. In questa situazione, un documento PDF crittografato si trova all&#39;interno dell&#39;oggetto raccolta.

>[!NOTE]
>
>Se si richiama l&#39;operazione `invokeDDX`, viene restituito un oggetto di raccolta. Questa operazione viene utilizzata quando si passano due o più documenti PDF di input al servizio Assembler. Tuttavia, se si passa un solo documento PDF di input al servizio Assembler, è necessario richiamare l&#39;operazione `invokeOneDocument`. Per informazioni sull&#39;utilizzo di questa operazione, vedere [Assemblaggio di documenti PDF crittografati](/help/forms/developing/assembling-encrypted-pdf-documents.md).

**Consulta anche**

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Assemblaggio programmatico di documenti PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Assemblare i documenti con la numerazione Bates utilizzando l&#39;API Java {#assemble-documents-with-bates-numbering-using-the-java-api}

Assemblare un documento PDF che utilizza identificatori di pagina univoci (numerazione Bates) utilizzando l&#39;API del servizio Assembler (Java):

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
   * Per ciascun documento PDF di input, creare un oggetto `java.io.FileInputStream` utilizzando il relativo costruttore e passando la posizione del documento PDF di input. In questa situazione, passare la posizione di un documento PDF non protetto.
   * Per ciascun documento PDF di input, creare un oggetto `com.adobe.idp.Document` e passare l&#39;oggetto `java.io.FileInputStream` che contiene il documento PDF.
   * Aggiungere una voce all&#39;oggetto `java.util.Map` richiamando il relativo metodo `put` e passando i seguenti argomenti:

      * Valore stringa che rappresenta il nome della chiave. Questo valore deve corrispondere al valore dell&#39;elemento di origine PDF specificato nel documento DDX. Ad esempio, il nome del file di origine PDF specificato nel documento DDX introdotto in questa sezione è Loan.pdf.
      * Oggetto `com.adobe.idp.Document` contenente il documento PDF non protetto.

1. Impostare il valore del numero Bates iniziale.

   * Creare un oggetto `AssemblerOptionSpec` che memorizza le opzioni di esecuzione utilizzando il relativo costruttore.
   * Impostare il numero Bates iniziale richiamando l&#39;oggetto `setFirstBatesNumber` `AssemblerOptionSpec` e passando un valore numerico che specifica il valore iniziale.

1. Assemblare i documenti PDF di input.

   Richiama il metodo `invokeDDX` dell&#39;oggetto `AssemblerServiceClient` e passa i seguenti valori obbligatori:

   * Un oggetto `com.adobe.idp.Document` che rappresenta il documento DDX.
   * Un oggetto `java.util.Map` che contiene il file PDF non protetto di input.
   * Un oggetto `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` che specifica le opzioni di esecuzione, incluso il tipo di carattere predefinito e il livello di registro dei processi.

   Il metodo `invokeDDX` restituisce un oggetto `com.adobe.livecycle.assembler.client.AssemblerResult` contenente un documento PDF crittografato con password.

1. Estrai i risultati.

   Per ottenere il documento PDF appena creato, eseguire le operazioni seguenti:

   * Richiama il metodo `getDocuments` dell&#39;oggetto `AssemblerResult`. Questa azione restituisce un oggetto `java.util.Map`.
   * Iterare l&#39;oggetto `java.util.Map` fino a individuare l&#39;oggetto `com.adobe.idp.Document`.
   * Richiamare il metodo `copyToFile` dell&#39;oggetto `com.adobe.idp.Document` per estrarre il documento PDF.

**Consulta anche**

[Avvio rapido (modalità SOAP): Assemblaggio di un documento PDF con numerazione dei bates utilizzando l’API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-a-pdf-document-with-bates-numbering-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Assemblare i documenti con la numerazione Bates utilizzando l&#39;API del servizio Web {#assemble-documents-with-bates-numbering-using-the-web-service-api}

Assemblare un documento PDF che utilizza identificatori di pagina univoci (numerazione Bates) utilizzando l&#39;API del servizio Assembler (servizio Web):

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
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento DDX e la modalità in cui aprire il file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni dell&#39;array di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare l’array di byte con i dati del flusso richiamando il metodo `Read` dell’oggetto `System.IO.FileStream`. Passa la matrice dei byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando il relativo campo `MTOM` con il contenuto dell&#39;array di byte.

1. Riferimento ai documenti PDF di input.

   * Per ciascun documento PDF di input, creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare il documento PDF di input.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore. Passa un valore stringa che rappresenta la posizione del file del documento PDF di input e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni dell&#39;array di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare l’array di byte con i dati del flusso richiamando il metodo `Read` dell’oggetto `System.IO.FileStream`. Passa la matrice dei byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando la relativa proprietà `MTOM` con il contenuto dell&#39;array di byte.
   * Creare un oggetto `MyMapOf_xsd_string_To_xsd_anyType`. Questo oggetto raccolta viene utilizzato per memorizzare i documenti PDF di input.
   * Per ciascun documento PDF di input, creare un oggetto `MyMapOf_xsd_string_To_xsd_anyType_Item`. Ad esempio, se si utilizzano due documenti PDF di input, creare due oggetti `MyMapOf_xsd_string_To_xsd_anyType_Item`.
   * Assegna un valore stringa che rappresenta il nome della chiave al campo `MyMapOf_xsd_string_To_xsd_anyType_Item` dell&#39;oggetto `key`. Questo valore deve corrispondere al valore dell&#39;elemento di origine PDF specificato nel documento DDX. Esegui questa operazione per ogni documento PDF di input.
   * Assegnare l&#39;oggetto `BLOB` che memorizza il documento PDF nel campo `MyMapOf_xsd_string_To_xsd_anyType_Item` dell&#39;oggetto `value`. Esegui questa operazione per ogni documento PDF di input.
   * Aggiungere l&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType_Item` all&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType`. Richiama il metodo `Add` dell&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType` e passa l&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType`. Esegui questa operazione per ogni documento PDF di input.

1. Impostare il valore del numero Bates iniziale.

   * Creare un oggetto `AssemblerOptionSpec` che memorizza le opzioni di esecuzione utilizzando il relativo costruttore.
   * Impostare il numero Bates iniziale assegnando un valore numerico al membro dati `firstBatesNumber` che appartiene all&#39;oggetto `AssemblerOptionSpec`.

1. Assemblare i documenti PDF di input.

   Richiama il metodo `invoke` dell&#39;oggetto `AssemblerServiceClient` e passa i seguenti valori:

   * Un oggetto `BLOB` che rappresenta il documento DDX.
   * L&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType` che contiene i documenti PDF di input. Le chiavi devono corrispondere ai nomi dei file di origine PDF e i relativi valori devono essere gli oggetti `BLOB` che corrispondono a tali file.
   * Un oggetto `AssemblerOptionSpec` che specifica le opzioni di esecuzione.

   Il metodo `invoke` restituisce un oggetto `AssemblerResult` contenente i risultati del processo ed eventuali eccezioni.

1. Estrai i risultati.

   Per ottenere il documento PDF appena creato, eseguire le operazioni seguenti:

   * Accedere al campo `documents` dell&#39;oggetto `AssemblerResult`, che è un oggetto `Map` che contiene i documenti PDF risultanti.
   * Iterare l&#39;oggetto `Map` fino a trovare la chiave che corrisponde al nome del documento risultante. Quindi eseguire il cast di `value` del membro della matrice su un `BLOB`.
   * Estrarre i dati binari che rappresentano il documento PDF accedendo alla proprietà `MTOM` dell’oggetto `BLOB` corrispondente. Restituisce una matrice di byte che è possibile scrivere in un file PDF.

**Consulta anche**

[Richiamo di AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
