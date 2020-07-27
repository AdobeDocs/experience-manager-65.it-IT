---
title: Assemblaggio di documenti con la numerazione Bates
seo-title: Assemblaggio di documenti con la numerazione Bates
description: 'null'
seo-description: 'null'
uuid: 28d5faeb-6915-41a2-b6a0-78d255df024f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 77e9b895-1313-4a5b-a2d5-cdb65bdc1966
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '1901'
ht-degree: 0%

---


# Assemblaggio di documenti con la numerazione Bates {#assembling-documents-using-bates-numbering}

È possibile assemblare documenti PDF che contengono identificatori di pagina univoci utilizzando la numerazione Bates. *La numerazione* Bates è un metodo per applicare identificatori univoci a un batch di documenti correlati. A ogni pagina del documento (o set di documenti) viene assegnato un numero Bates che identifica in modo univoco la pagina. Ad esempio, i documenti di fabbricazione che contengono informazioni sulla distinta base e sono associati alla produzione di un assieme possono contenere un identificatore. Un numero Bates contiene un valore numerico incrementato sequenzialmente e un prefisso e un suffisso facoltativi. Il prefisso + il suffisso numerico + viene definito come pattern *di* batch.

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

Questo documento DDX unisce due documenti PDF denominati *map.pdf* e *directional.pdf* in un unico documento PDF. Il documento PDF risultante contiene un&#39;intestazione costituita da un identificatore di pagina univoco. Ad esempio, il documento nell&#39;illustrazione precedente mostra 000016.

>[!NOTE]
>
>Prima di leggere questa sezione, è consigliabile avere familiarità con l&#39;assemblaggio di documenti PDF tramite il servizio Assembler. In questa sezione non vengono descritti i concetti, ad esempio la creazione di un oggetto raccolta contenente documenti di input o l&#39;estrazione dei risultati dall&#39;oggetto raccolta restituito. (Vedere Assemblaggio [di documenti](/help/forms/developing/programmatically-assembling-pdf-documents.md)PDF a livello di programmazione.)

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Assembler, vedere Riferimento [servizi per i AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Per ulteriori informazioni su un documento DDX, vedere Servizio [Assembler e Riferimento](https://www.adobe.com/go/learn_aemforms_ddx_63)DDX.

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
* adobe-utilities.jar (richiesto se i AEM Forms sono distribuiti su JBoss)
* jbossall-client.jar (richiesto se i AEM Forms sono distribuiti su JBoss)

Se i AEM Forms sono distribuiti su un server applicazione J2EE supportato diverso da JBoss, è necessario sostituire i file adobe-utilities.jar e jbossall-client.jar con file JAR specifici del server applicazione J2EE in cui sono distribuiti i AEM Forms. Per informazioni sulla posizione di tutti i file JAR AEM Forms, vedere [Inclusione di file](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)libreria Java AEM Forms.

**Creare un client Assembler PDF**

Prima di eseguire un&#39;operazione Assembler a livello di programmazione, è necessario creare un client di servizio Assembler.

**Riferimento a un documento DDX esistente**

Per assemblare un documento PDF è necessario fare riferimento a un documento DDX. Si consideri, ad esempio, il documento DDX introdotto in questa sezione. Per assemblare un documento PDF che contiene identificatori di pagina univoci, il documento DDX deve contenere l&#39; `BatesNumber` elemento .

**Riferimento a documenti PDF in input**

Per assemblare un documento PDF è necessario fare riferimento ai documenti PDF di input. Ad esempio, per assemblare questi documenti PDF in un singolo documento PDF è necessario fare riferimento ai documenti map.pdf e guidelines.pdf.

**Impostare il valore numero Bates iniziale**

Puoi impostare il valore iniziale del numero Bates per soddisfare i requisiti aziendali. Ad esempio, si supponga che sia necessario impostare il valore iniziale su 000100. Se non si imposta il valore iniziale, il valore della prima pagina è 000000.

**Assemblare i documenti PDF in input**

Dopo aver creato il client del servizio Assembler, fare riferimento al documento DDX che contiene informazioni sugli `BatesNumber` elementi, fare riferimento a un documento PDF di input e impostare le opzioni di esecuzione, è possibile richiamare l&#39; `invokeDDX` operazione che determina l&#39;assemblaggio di un documento PDF contenente identificatori di pagina univoci da parte del servizio Assembler.

**Estrarre i risultati**

Il servizio Assembler restituisce un oggetto insieme contenente i risultati del processo. È possibile estrarre il documento PDF risultante ed eventuali eccezioni generate. In questa situazione, un documento PDF crittografato si trova all&#39;interno dell&#39;oggetto raccolta.

>[!NOTE]
>
>Se si richiama l&#39; `invokeDDX` operazione, viene restituito un oggetto raccolta. Questa operazione viene utilizzata per trasmettere due o più documenti PDF di input al servizio Assembler. Tuttavia, se trasmettete un solo documento PDF di input al servizio Assembler, è necessario richiamare l&#39; `invokeOneDocument` operazione. Per informazioni sull&#39;utilizzo di questa operazione, vedere [Assemblaggio di documenti](/help/forms/developing/assembling-encrypted-pdf-documents.md)PDF crittografati.

**Consulta anche**

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Assemblaggio di documenti PDF a livello di programmazione](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Assemblare i documenti con la numerazione Bates utilizzando l&#39;API Java {#assemble-documents-with-bates-numbering-using-the-java-api}

Assemblate un documento PDF che utilizza identificatori di pagina univoci (numerazione Bates) utilizzando l&#39;API Assembler Service (Java):

1. Includere i file di progetto.

   Includete file JAR client, ad esempio adobe-assembler-client.jar, nel percorso di classe del progetto Java.

1. Creare un client Assembler PDF.

   * Creare un `ServiceClientFactory` oggetto che contenga proprietà di connessione.
   * Creare un `AssemblerServiceClient` oggetto utilizzando il relativo costruttore e passando l&#39; `ServiceClientFactory` oggetto.

1. Fare riferimento a un documento DDX esistente.

   * Creare un `java.io.FileInputStream` oggetto che rappresenta il documento DDX utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del file DDX.
   * Creare un `com.adobe.idp.Document` oggetto utilizzando il relativo costruttore e passando l&#39; `java.io.FileInputStream` oggetto.

1. Riferimento a documenti PDF in input.

   * Creare un `java.util.Map` oggetto utilizzato per memorizzare i documenti PDF di input utilizzando un `HashMap` costruttore.
   * Per ciascun documento PDF di input, creare un `java.io.FileInputStream` oggetto utilizzando il relativo costruttore e passando la posizione del documento PDF di input. In questa situazione, passare la posizione di un documento PDF non protetto.
   * Per ciascun documento PDF di input, creare un `com.adobe.idp.Document` oggetto e passare l&#39; `java.io.FileInputStream` oggetto che contiene il documento PDF.
   * Aggiungere una voce all&#39; `java.util.Map` oggetto richiamandone il `put` metodo e passando gli argomenti seguenti:

      * Un valore di stringa che rappresenta il nome della chiave. Questo valore deve corrispondere al valore dell&#39;elemento di origine PDF specificato nel documento DDX. Ad esempio, il nome del file di origine PDF specificato nel documento DDX introdotto in questa sezione è Loan.pdf.
      * Un `com.adobe.idp.Document` oggetto che contiene il documento PDF non protetto.

1. Impostate il valore numero Bates iniziale.

   * Creare un `AssemblerOptionSpec` oggetto che memorizza le opzioni di esecuzione utilizzando il relativo costruttore.
   * Impostare il numero Bates iniziale richiamando l&#39; `AssemblerOptionSpec` oggetto `setFirstBatesNumber` e passando un valore numerico che specifica il valore iniziale.

1. Assemblare i documenti PDF di input.

   Richiamare il metodo dell&#39; `AssemblerServiceClient` oggetto `invokeDDX` e trasmettere i seguenti valori obbligatori:

   * Un `com.adobe.idp.Document` oggetto che rappresenta il documento DDX.
   * Un `java.util.Map` oggetto che contiene il file PDF non protetto di input.
   * Un `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` oggetto che specifica le opzioni di esecuzione, incluso il livello predefinito del font e del registro dei processi.

   Il `invokeDDX` metodo restituisce un `com.adobe.livecycle.assembler.client.AssemblerResult` oggetto che contiene un documento PDF crittografato con password.

1. Estrarre i risultati.

   Per ottenere il documento PDF appena creato, effettuare le seguenti operazioni:

   * Richiama il metodo dell’ `AssemblerResult` oggetto `getDocuments` . Questa azione restituisce un `java.util.Map` oggetto.
   * Eseguire un&#39;iterazione sull&#39; `java.util.Map` oggetto fino a individuare l&#39; `com.adobe.idp.Document` oggetto.
   * Richiamare il metodo dell&#39; `com.adobe.idp.Document` oggetto `copyToFile` per estrarre il documento PDF.

**Consulta anche**

[Avvio rapido (modalità SOAP): Assemblare un documento PDF con la numerazione dei bates utilizzando l&#39;API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-a-pdf-document-with-bates-numbering-using-the-java-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Assemblare i documenti con la numerazione Bates utilizzando l&#39;API del servizio Web {#assemble-documents-with-bates-numbering-using-the-web-service-api}

Assemblate un documento PDF che utilizza identificatori di pagina univoci (numerazione Bates) utilizzando l&#39;API Assembler Service (servizio Web):

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
   * Compilare l&#39;array di byte con i dati del flusso richiamando il metodo dell&#39; `System.IO.FileStream` oggetto `Read` . Passare l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39; `BLOB` oggetto assegnandone `MTOM` il campo con il contenuto dell&#39;array di byte.

1. Riferimento a documenti PDF in input.

   * Per ciascun documento PDF di input, creare un `BLOB` oggetto utilizzando il relativo costruttore. L&#39; `BLOB` oggetto viene utilizzato per memorizzare il documento PDF di input.
   * Creare un `System.IO.FileStream` oggetto richiamandone il costruttore. Passa un valore di stringa che rappresenta la posizione del file del documento PDF di input e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto dell&#39; `System.IO.FileStream` oggetto. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà dell&#39; `System.IO.FileStream` oggetto `Length` .
   * Compilare l&#39;array di byte con i dati del flusso richiamando il metodo dell&#39; `System.IO.FileStream` oggetto `Read` . Passare l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39; `BLOB` oggetto assegnandone `MTOM` la proprietà con il contenuto dell&#39;array di byte.
   * Create a `MyMapOf_xsd_string_To_xsd_anyType` object. Questo oggetto raccolta viene utilizzato per memorizzare i documenti PDF di input.
   * Per ciascun documento PDF di input, creare un `MyMapOf_xsd_string_To_xsd_anyType_Item` oggetto. Ad esempio, se si utilizzano due documenti PDF di input, creare due `MyMapOf_xsd_string_To_xsd_anyType_Item` oggetti.
   * Assegnare un valore di stringa che rappresenta il nome chiave al campo dell&#39; `MyMapOf_xsd_string_To_xsd_anyType_Item` oggetto `key` . Questo valore deve corrispondere al valore dell&#39;elemento di origine PDF specificato nel documento DDX. (Eseguire questa operazione per ciascun documento PDF di input.)
   * Assegnare l&#39; `BLOB` oggetto che memorizza il documento PDF nel campo dell&#39; `MyMapOf_xsd_string_To_xsd_anyType_Item` oggetto `value` . (Eseguire questa operazione per ciascun documento PDF di input.)
   * Aggiungere l&#39; `MyMapOf_xsd_string_To_xsd_anyType_Item` oggetto all&#39; `MyMapOf_xsd_string_To_xsd_anyType` oggetto. Richiamare il `MyMapOf_xsd_string_To_xsd_anyType` metodo dell&#39;oggetto `Add` e passare l&#39; `MyMapOf_xsd_string_To_xsd_anyType` oggetto. (Eseguire questa operazione per ciascun documento PDF di input.)

1. Impostate il valore numero Bates iniziale.

   * Creare un `AssemblerOptionSpec` oggetto che memorizza le opzioni di esecuzione utilizzando il relativo costruttore.
   * Impostare il numero Bates iniziale assegnando un valore numerico al membro `firstBatesNumber` dati che appartiene all&#39; `AssemblerOptionSpec` oggetto.

1. Assemblare i documenti PDF di input.

   Richiama il metodo dell’ `AssemblerServiceClient` oggetto `invoke` e passa i seguenti valori:

   * Un `BLOB` oggetto che rappresenta il documento DDX.
   * L&#39; `MyMapOf_xsd_string_To_xsd_anyType` oggetto che contiene i documenti PDF di input. Le chiavi devono corrispondere ai nomi dei file sorgente PDF e i relativi valori devono essere gli `BLOB` oggetti che corrispondono a tali file.
   * Un `AssemblerOptionSpec` oggetto che specifica le opzioni di esecuzione.

   Il `invoke` metodo restituisce un `AssemblerResult` oggetto che contiene i risultati del processo ed eventuali eccezioni.

1. Estrarre i risultati.

   Per ottenere il documento PDF appena creato, effettuare le seguenti operazioni:

   * Accedere al campo dell&#39; `AssemblerResult` oggetto `documents` , ovvero un `Map` oggetto che contiene i documenti PDF risultanti.
   * Eseguire un&#39;iterazione sull&#39; `Map` oggetto fino a individuare la chiave che corrisponde al nome del documento risultante. Quindi, inserite l&#39;elemento `value` dell&#39;array in un `BLOB`.
   * Estrarre i dati binari che rappresentano il documento PDF accedendo alla `BLOB` proprietà dell&#39; `MTOM` oggetto. Questo restituisce un array di byte che è possibile scrivere in un file PDF.

**Consulta anche**

[Chiamata di AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
