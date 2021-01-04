---
title: Assemblaggio di documenti con la numerazione Bates
seo-title: Assemblaggio di documenti con la numerazione Bates
description: 'Utilizzare la numerazione Bates per assemblare documenti PDF utilizzando l''API Java e il servizio Web. '
seo-description: 'Utilizzare la numerazione Bates per assemblare documenti PDF utilizzando l''API Java e il servizio Web. '
uuid: 28d5faeb-6915-41a2-b6a0-78d255df024f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 77e9b895-1313-4a5b-a2d5-cdb65bdc1966
translation-type: tm+mt
source-git-commit: 07889ead2ae402b5fb738ca08c7efe076ef33e44
workflow-type: tm+mt
source-wordcount: '1927'
ht-degree: 0%

---


# Assemblare documenti utilizzando la numerazione Bates {#assembling-documents-using-bates-numbering}

È possibile assemblare documenti PDF che contengono identificatori di pagina univoci utilizzando la numerazione Bates. *La* numerazione Bates è un metodo per applicare identificatori univoci a un batch di documenti correlati. A ogni pagina del documento (o set di documenti) viene assegnato un numero Bates che identifica in modo univoco la pagina. Ad esempio, i documenti di fabbricazione che contengono informazioni sulla distinta base e sono associati alla produzione di un assieme possono contenere un identificatore. Un numero Bates contiene un valore numerico incrementato sequenzialmente e un prefisso e un suffisso facoltativi. Il prefisso + suffisso numerico + è denominato *pattern di bates*.

L&#39;illustrazione seguente mostra un documento PDF contenente un identificatore univoco nell&#39;intestazione del documento.

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

Questo documento DDX unisce due documenti PDF denominati *map.pdf* e *sections.pdf* in un singolo documento PDF. Il documento PDF risultante contiene un&#39;intestazione costituita da un identificatore di pagina univoco. Ad esempio, il documento nell&#39;illustrazione precedente mostra 000016.

>[!NOTE]
>
>Prima di leggere questa sezione, è consigliabile avere familiarità con l&#39;assemblaggio di documenti PDF tramite il servizio Assembler. In questa sezione non vengono descritti i concetti, ad esempio la creazione di un oggetto raccolta contenente documenti di input o l&#39;estrazione dei risultati dall&#39;oggetto raccolta restituito. (Vedere [Assemblaggio programmatico di documenti PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md).)

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Assembler, vedere [Guida di riferimento dei servizi per  AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Per ulteriori informazioni su un documento DDX, vedere [Servizio Assembler e Riferimento DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Riepilogo dei passaggi {#summary-of-steps}

Per assemblare un documento PDF contenente un unico identificatore di pagina (numerazione Bates), effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un client Assembler PDF.
1. Fare riferimento a un documento DDX esistente.
1. Riferimento a documenti PDF in input.
1. Impostate il valore numero Bates iniziale.
1. Assemblare i documenti PDF di input.
1. Estrarre i risultati.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, accertatevi di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (richiesto se  AEM Forms è distribuito su JBoss)
* jbossall-client.jar (richiesto se  AEM Forms è distribuito su JBoss)

Se  AEM Forms è distribuito su un server applicazione J2EE supportato diverso da JBoss, è necessario sostituire i file adobe-utilities.jar e jbossall-client.jar con file JAR specifici del server applicazione J2EE in cui  AEM Forms è distribuito. Per informazioni sulla posizione di tutti  file AEM Forms JAR, vedere [Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un client Assembler PDF**

Prima di eseguire un&#39;operazione Assembler a livello di programmazione, è necessario creare un client di servizio Assembler.

**Riferimento a un documento DDX esistente**

Per assemblare un documento PDF è necessario fare riferimento a un documento DDX. Si consideri, ad esempio, il documento DDX introdotto in questa sezione. Per assemblare un documento PDF che contiene identificatori di pagina univoci, il documento DDX deve contenere l&#39;elemento `BatesNumber`.

**Riferimento a documenti PDF in input**

Per assemblare un documento PDF è necessario fare riferimento ai documenti PDF di input. Ad esempio, per assemblare questi documenti PDF in un singolo documento PDF è necessario fare riferimento ai documenti map.pdf e directional.pdf.

**Impostare il valore numero Bates iniziale**

Puoi impostare il valore iniziale del numero Bates per soddisfare i requisiti aziendali. Ad esempio, si supponga che sia necessario impostare il valore iniziale su 000100. Se non si imposta il valore iniziale, il valore della prima pagina è 000000.

**Assemblare i documenti PDF in input**

Dopo aver creato il client del servizio Assembler, fare riferimento al documento DDX che contiene le informazioni relative agli elementi `BatesNumber`, fare riferimento a un documento PDF di input e impostare le opzioni di esecuzione, è possibile richiamare l&#39;operazione `invokeDDX` che consente al servizio Assembler di assemblare un documento PDF contenente identificatori di pagina univoci.

**Estrarre i risultati**

Il servizio Assembler restituisce un oggetto insieme contenente i risultati del processo. È possibile estrarre il documento PDF risultante ed eventuali eccezioni generate. In questa situazione, un documento PDF crittografato si trova all&#39;interno dell&#39;oggetto raccolta.

>[!NOTE]
>
>Se si richiama l&#39;operazione `invokeDDX`, viene restituito un oggetto raccolta. Questa operazione viene utilizzata per trasmettere due o più documenti PDF di input al servizio Assembler. Tuttavia, se si passa un solo documento PDF di input al servizio Assembler, è necessario richiamare l&#39;operazione `invokeOneDocument`. Per informazioni sull&#39;utilizzo di questa operazione, vedere [Assemblaggio di documenti PDF crittografati](/help/forms/developing/assembling-encrypted-pdf-documents.md).

**Consulta anche**

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Assemblaggio di documenti PDF a livello di programmazione](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Assemblate i documenti con la numerazione Bates utilizzando l&#39;API Java {#assemble-documents-with-bates-numbering-using-the-java-api}

Assemblate un documento PDF che utilizza identificatori di pagina univoci (numerazione Bates) utilizzando l&#39;API Assembler Service (Java):

1. Includere i file di progetto.

   Includete file JAR client, ad esempio adobe-assembler-client.jar, nel percorso di classe del progetto Java.

1. Creare un client Assembler PDF.

   * Creare un oggetto `ServiceClientFactory` che contiene le proprietà di connessione.
   * Creare un oggetto `AssemblerServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Fare riferimento a un documento DDX esistente.

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento DDX utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del file DDX.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Riferimento a documenti PDF in input.

   * Creare un oggetto `java.util.Map` utilizzato per memorizzare i documenti PDF di input utilizzando un costruttore `HashMap`.
   * Per ciascun documento PDF di input, creare un oggetto `java.io.FileInputStream` utilizzando il relativo costruttore e passando la posizione del documento PDF di input. In questa situazione, passare la posizione di un documento PDF non protetto.
   * Per ciascun documento PDF di input, creare un oggetto `com.adobe.idp.Document` e passare l&#39;oggetto `java.io.FileInputStream` che contiene il documento PDF.
   * Aggiungere una voce all&#39;oggetto `java.util.Map` richiamandone il metodo `put` e trasmettendo gli argomenti seguenti:

      * Un valore di stringa che rappresenta il nome della chiave. Questo valore deve corrispondere al valore dell&#39;elemento di origine PDF specificato nel documento DDX. Ad esempio, il nome del file di origine PDF specificato nel documento DDX introdotto in questa sezione è Loan.pdf.
      * Un oggetto `com.adobe.idp.Document` che contiene il documento PDF non protetto.

1. Impostate il valore numero Bates iniziale.

   * Creare un oggetto `AssemblerOptionSpec` che memorizza le opzioni di esecuzione utilizzando il relativo costruttore.
   * Impostare il numero Bates iniziale richiamando l&#39;oggetto `AssemblerOptionSpec` e passando un valore numerico che specifica il valore iniziale.`setFirstBatesNumber`

1. Assemblare i documenti PDF di input.

   Richiamare il metodo `AssemblerServiceClient` dell&#39;oggetto `invokeDDX` e trasmettere i seguenti valori obbligatori:

   * Un oggetto `com.adobe.idp.Document` che rappresenta il documento DDX.
   * Un oggetto `java.util.Map` che contiene il file PDF non protetto di input.
   * Un oggetto `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` che specifica le opzioni di esecuzione, incluso il font predefinito e il livello di registro del processo.

   Il metodo `invokeDDX` restituisce un oggetto `com.adobe.livecycle.assembler.client.AssemblerResult` contenente un documento PDF crittografato con password.

1. Estrarre i risultati.

   Per ottenere il documento PDF appena creato, effettuare le seguenti operazioni:

   * Richiamare il metodo `AssemblerResult` dell&#39;oggetto `getDocuments`. Questa azione restituisce un oggetto `java.util.Map`.
   * Iterate l&#39;oggetto `java.util.Map` fino a individuare l&#39;oggetto `com.adobe.idp.Document`.
   * Richiamare il metodo `com.adobe.idp.Document` dell&#39;oggetto `copyToFile` per estrarre il documento PDF.

**Consulta anche**

[Avvio rapido (modalità SOAP): Assemblare un documento PDF con la numerazione dei bates utilizzando l&#39;API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-a-pdf-document-with-bates-numbering-using-the-java-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Assemblate i documenti con la numerazione Bates utilizzando l&#39;API del servizio Web {#assemble-documents-with-bates-numbering-using-the-web-service-api}

Assemblate un documento PDF che utilizza identificatori di pagina univoci (numerazione Bates) utilizzando l&#39;API Assembler Service (servizio Web):

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
   * Compilare l&#39;array di byte con i dati del flusso richiamando il metodo `System.IO.FileStream` dell&#39;oggetto `Read`. Passare l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando il relativo campo `MTOM` con il contenuto dell&#39;array di byte.

1. Riferimento a documenti PDF in input.

   * Per ciascun documento PDF di input, creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare il documento PDF di input.
   * Creare un oggetto `System.IO.FileStream` richiamandone il costruttore. Passa un valore di stringa che rappresenta la posizione del file del documento PDF di input e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà `System.IO.FileStream` dell&#39;oggetto `Length`.
   * Compilare l&#39;array di byte con i dati del flusso richiamando il metodo `System.IO.FileStream` dell&#39;oggetto `Read`. Passare l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnandone la proprietà `MTOM` con il contenuto dell&#39;array di byte.
   * Creare un oggetto `MyMapOf_xsd_string_To_xsd_anyType`. Questo oggetto raccolta viene utilizzato per memorizzare i documenti PDF di input.
   * Per ciascun documento PDF di input, creare un oggetto `MyMapOf_xsd_string_To_xsd_anyType_Item`. Ad esempio, se si utilizzano due documenti PDF di input, creare due oggetti `MyMapOf_xsd_string_To_xsd_anyType_Item`.
   * Assegnare un valore di stringa che rappresenta il nome chiave al campo `MyMapOf_xsd_string_To_xsd_anyType_Item` dell&#39;oggetto `key`. Questo valore deve corrispondere al valore dell&#39;elemento di origine PDF specificato nel documento DDX. (Eseguire questa operazione per ciascun documento PDF di input.)
   * Assegnare l&#39;oggetto `BLOB` che memorizza il documento PDF nel campo `MyMapOf_xsd_string_To_xsd_anyType_Item` dell&#39;oggetto `value`. (Eseguire questa operazione per ciascun documento PDF di input.)
   * Aggiungere l&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType_Item` all&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType`. Richiamare il metodo `MyMapOf_xsd_string_To_xsd_anyType` dell&#39;oggetto `Add` e passare l&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType`. (Eseguire questa operazione per ciascun documento PDF di input.)

1. Impostate il valore numero Bates iniziale.

   * Creare un oggetto `AssemblerOptionSpec` che memorizza le opzioni di esecuzione utilizzando il relativo costruttore.
   * Impostare il numero Bates iniziale assegnando un valore numerico al membro di dati `firstBatesNumber` che appartiene all&#39;oggetto `AssemblerOptionSpec`.

1. Assemblare i documenti PDF di input.

   Richiamare il metodo `AssemblerServiceClient` dell&#39;oggetto `invoke` e trasmettere i seguenti valori:

   * Un oggetto `BLOB` che rappresenta il documento DDX.
   * L&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType` che contiene i documenti PDF di input. Le chiavi devono corrispondere ai nomi dei file sorgente PDF e i relativi valori devono essere gli oggetti `BLOB` che corrispondono a tali file.
   * Un oggetto `AssemblerOptionSpec` che specifica le opzioni di esecuzione.

   Il metodo `invoke` restituisce un oggetto `AssemblerResult` che contiene i risultati del processo ed eventuali eccezioni.

1. Estrarre i risultati.

   Per ottenere il documento PDF appena creato, effettuare le seguenti operazioni:

   * Accedere al campo `documents` dell&#39;oggetto `AssemblerResult`, che è un oggetto `Map` che contiene i documenti PDF risultanti.
   * Iterate l&#39;oggetto `Map` fino a trovare la chiave che corrisponde al nome del documento risultante. Quindi, inserire l&#39;elemento `value` del membro della matrice in un elemento `BLOB`.
   * Estrarre i dati binari che rappresentano il documento PDF accedendo alla proprietà `BLOB` dell&#39;oggetto `MTOM`. Questo restituisce un array di byte che è possibile scrivere in un file PDF.

**Consulta anche**

[Chiamata  AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
