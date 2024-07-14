---
title: Assemblaggio di documenti mediante la numerazione Bates
description: Utilizza la numerazione Bates per assemblare documenti PDF utilizzando l’API Java e Web Service.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 2a4e21c4-f2f5-44cd-b8ed-7b572782a2f1
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1910'
ht-degree: 0%

---

# Assemblaggio di documenti mediante la numerazione Bates {#assembling-documents-using-bates-numbering}

**Gli esempi e gli esempi contenuti in questo documento sono solo per AEM Forms in ambiente JEE.**

È possibile assemblare documenti PDF che contengono identificatori di pagina univoci utilizzando la numerazione Bates. *La numerazione dei Bates* è un metodo per applicare identificatori univoci a un batch di documenti correlati. A ogni pagina del documento (o set di documenti) viene assegnato un numero Bates che identifica in modo univoco la pagina. Ad esempio, i documenti di fabbricazione che contengono informazioni sulla distinta base e sono associati alla produzione di un assieme possono contenere un identificatore. Un numero Bates contiene un valore numerico incrementato in sequenza e un prefisso e un suffisso opzionali. Il prefisso + suffisso numerico + viene indicato come pattern *bates*.

Nella figura seguente viene illustrato un documento PDF che contiene un identificatore univoco nell&#39;intestazione del documento.

![au_au_batesnumber](assets/au_au_batesnumber.png)

Ai fini della presente discussione, l&#39;identificatore di pagina univoco viene inserito nell&#39;intestazione di un documento. Si supponga di utilizzare il seguente documento DDX.

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

Questo documento DDX unisce due documenti PDF denominati *map.pdf* e *direction.pdf* in un unico documento PDF. Il documento PDF risultante contiene un&#39;intestazione costituita da un identificatore di pagina univoco. Ad esempio, il documento nell’illustrazione precedente mostra 000016.

>[!NOTE]
>
>Prima di leggere questa sezione, è consigliabile avere familiarità con l&#39;assemblaggio di documenti PDF utilizzando il servizio Assembler. In questa sezione non vengono descritti i concetti, ad esempio la creazione di un oggetto di raccolta contenente documenti di input o l&#39;estrazione dei risultati dall&#39;oggetto di raccolta restituito. (Vedi [Assemblaggio a livello di programmazione di documenti di PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md).)

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Assembler, vedere [Riferimento ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Per ulteriori informazioni su un documento DDX, vedere [Servizio assemblatore e riferimento DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Riepilogo dei passaggi {#summary-of-steps}

Per assemblare un documento PDF contenente un identificatore di pagina univoco (numerazione Bates), effettuare le seguenti operazioni:

1. Includi file di progetto.
1. Creare un client PDF Assembler.
1. Fare riferimento a un documento DDX esistente.
1. Fai riferimento ai documenti di input PDF.
1. Imposta il valore del numero Bates iniziale.
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

Se AEM Forms viene distribuito su un server applicazioni J2EE supportato diverso da JBoss, è necessario sostituire i file adobe-utilities.jar e jbossall-client.jar con file JAR specifici per il server applicazioni J2EE in cui viene distribuito AEM Forms. Per informazioni sulla posizione di tutti i file JAR di AEM Forms, vedi [Inclusi i file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un client Assembler PDF**

Prima di poter eseguire un&#39;operazione Assembler a livello di programmazione, è necessario creare un client del servizio Assembler.

**Riferimento a un documento DDX esistente**

Per assemblare un documento PDF è necessario fare riferimento a un documento DDX. Si consideri ad esempio il documento DDX introdotto in questa sezione. Per assemblare un documento PDF contenente identificatori di pagina univoci, il documento DDX deve contenere l&#39;elemento `BatesNumber`.

**Riferimento ai documenti di input PDF**

Per assemblare un documento PDF, è necessario fare riferimento ai documenti PDF di input. Ad esempio, è necessario fare riferimento ai documenti map.pdf e direction.pdf per assemblare questi documenti PDF in un unico documento PDF.

**Imposta il valore del numero Bates iniziale**

È possibile impostare il valore del numero Bates iniziale per soddisfare i requisiti aziendali. Ad esempio, si supponga che sia necessario impostare il valore iniziale su 000100. Se non si imposta il valore iniziale, viene 000000 il valore della prima pagina.

**Assemblare i documenti di input PDF**

Dopo aver creato il client del servizio Assembler, aver fatto riferimento al documento DDX contenente le informazioni sull&#39;elemento `BatesNumber`, aver fatto riferimento a un documento di input PDF e aver impostato le opzioni di runtime, è possibile richiamare l&#39;operazione `invokeDDX` che determina l&#39;assemblaggio di un documento di PDF contenente identificatori di pagina univoci da parte del servizio Assembler.

**Estrai i risultati**

Il servizio Assembler restituisce un insieme che contiene i risultati del processo. È possibile estrarre il documento PDF risultante ed eventuali eccezioni generate. In questa situazione, un documento PDF crittografato si trova all&#39;interno dell&#39;oggetto raccolta.

>[!NOTE]
>
>Se si richiama l&#39;operazione `invokeDDX`, verrà restituito un oggetto raccolta. Questa operazione viene utilizzata quando si trasmettono due o più documenti di input PDF al servizio Assembler. Tuttavia, se si passa un solo documento di input PDF al servizio Assembler, è necessario richiamare l&#39;operazione `invokeOneDocument`. Per informazioni sull&#39;utilizzo di questa operazione, vedere [Assemblaggio di documenti crittografati di PDF](/help/forms/developing/assembling-encrypted-pdf-documents.md).

**Consulta anche**

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Assemblaggio di documenti PDF a livello di programmazione](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Assemblare documenti con numerazione Bates utilizzando l&#39;API Java {#assemble-documents-with-bates-numbering-using-the-java-api}

Assembla un documento PDF che utilizza identificatori di pagina univoci (numerazione Bates) utilizzando l’API del servizio Assembler (Java):

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
   * Per ogni documento di input PDF, creare un oggetto `java.io.FileInputStream` utilizzando il relativo costruttore e passando la posizione del documento di input PDF. In questa situazione, passa il percorso di un documento di PDF non protetto.
   * Per ogni documento di input PDF, creare un oggetto `com.adobe.idp.Document` e passare l&#39;oggetto `java.io.FileInputStream` che contiene il documento di input PDF.
   * Aggiungere una voce all&#39;oggetto `java.util.Map` richiamando il relativo metodo `put` e passando i seguenti argomenti:

      * Valore stringa che rappresenta il nome della chiave. Questo valore deve corrispondere al valore dell&#39;elemento di origine PDF specificato nel documento DDX. Il nome del file di origine PDF specificato nel documento DDX introdotto in questa sezione è Loan.pdf.
      * Oggetto `com.adobe.idp.Document` contenente il documento PDF non protetto.

1. Imposta il valore del numero Bates iniziale.

   * Creare un oggetto `AssemblerOptionSpec` che memorizza le opzioni di runtime utilizzando il relativo costruttore.
   * Impostare il numero Bates iniziale richiamando `setFirstBatesNumber` dell&#39;oggetto `AssemblerOptionSpec` e passando un valore numerico che specifica il valore iniziale.

1. Assemblare i documenti di input PDF.

   Richiama il metodo `invokeDDX` dell&#39;oggetto `AssemblerServiceClient` e passa i seguenti valori richiesti:

   * Oggetto `com.adobe.idp.Document` che rappresenta il documento DDX.
   * Oggetto `java.util.Map` contenente il file PDF non protetto di input.
   * Oggetto `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` che specifica le opzioni di runtime, inclusi il tipo di carattere predefinito e il livello del registro dei processi.

   Il metodo `invokeDDX` restituisce un oggetto `com.adobe.livecycle.assembler.client.AssemblerResult` contenente un documento PDF crittografato con password.

1. Estrai i risultati.

   Per ottenere il documento di PDF appena creato, effettuare le seguenti operazioni:

   * Richiama il metodo `getDocuments` dell&#39;oggetto `AssemblerResult`. Questa azione restituisce un oggetto `java.util.Map`.
   * Scorrere l&#39;oggetto `java.util.Map` fino a trovare l&#39;oggetto `com.adobe.idp.Document`.
   * Richiama il metodo `copyToFile` dell&#39;oggetto `com.adobe.idp.Document` per estrarre il documento PDF.

**Consulta anche**

[Guida rapida (modalità SOAP): assemblaggio di un documento PDF con numerazione Bates tramite l’API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-a-pdf-document-with-bates-numbering-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Assemblare documenti con numerazione Bates utilizzando l&#39;API del servizio Web {#assemble-documents-with-bates-numbering-using-the-web-service-api}

Assembla un documento PDF che utilizza identificatori di pagina univoci (numerazione Bates) utilizzando l’API del servizio Assembler (servizio web):

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
   * Creare un oggetto `System.IO.FileStream` richiamandone il costruttore e passando un valore stringa che rappresenta la posizione del file del documento DDX e la modalità di apertura del file in.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni della matrice di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare la matrice di byte con i dati di flusso richiamando il metodo `Read` dell&#39;oggetto `System.IO.FileStream`. Passare la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando il relativo campo `MTOM` al contenuto della matrice di byte.

1. Fai riferimento ai documenti di input PDF.

   * Per ogni documento di input PDF, creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare il documento PDF di input.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore. Passa un valore stringa che rappresenta la posizione del file del documento PDF di input e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni della matrice di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare la matrice di byte con i dati di flusso richiamando il metodo `Read` dell&#39;oggetto `System.IO.FileStream`. Passare la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando la relativa proprietà `MTOM` al contenuto della matrice di byte.
   * Creare un oggetto `MyMapOf_xsd_string_To_xsd_anyType`. Questo oggetto insieme viene utilizzato per memorizzare i documenti PDF di input.
   * Per ogni documento di input PDF, creare un oggetto `MyMapOf_xsd_string_To_xsd_anyType_Item`. Se ad esempio si utilizzano due documenti di input PDF, creare due oggetti `MyMapOf_xsd_string_To_xsd_anyType_Item`.
   * Assegnare un valore stringa che rappresenta il nome chiave al campo `key` dell&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType_Item`. Questo valore deve corrispondere al valore dell&#39;elemento di origine PDF specificato nel documento DDX. (Eseguire questa operazione per ogni documento di input PDF).
   * Assegnare l&#39;oggetto `BLOB` che memorizza il documento PDF al campo `value` dell&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType_Item`. (Eseguire questa operazione per ogni documento di input PDF).
   * Aggiungere l&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType_Item` all&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType`. Richiama il metodo `Add` dell&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType` e passa l&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType`. (Eseguire questa operazione per ogni documento di input PDF).

1. Imposta il valore del numero Bates iniziale.

   * Creare un oggetto `AssemblerOptionSpec` che memorizza le opzioni di runtime utilizzando il relativo costruttore.
   * Impostare il numero Bates iniziale assegnando un valore numerico al membro dati `firstBatesNumber` che appartiene all&#39;oggetto `AssemblerOptionSpec`.

1. Assemblare i documenti di input PDF.

   Richiama il metodo `invoke` dell&#39;oggetto `AssemblerServiceClient` e passa i seguenti valori:

   * Oggetto `BLOB` che rappresenta il documento DDX.
   * Oggetto `MyMapOf_xsd_string_To_xsd_anyType` contenente i documenti PDF di input. Le chiavi devono corrispondere ai nomi dei file di origine di PDF e i relativi valori devono essere gli oggetti `BLOB` corrispondenti a tali file.
   * Oggetto `AssemblerOptionSpec` che specifica le opzioni di runtime.

   Il metodo `invoke` restituisce un oggetto `AssemblerResult` contenente i risultati del processo ed eventuali eccezioni.

1. Estrai i risultati.

   Per ottenere il documento di PDF appena creato, effettuare le seguenti operazioni:

   * Accedere al campo `documents` dell&#39;oggetto `AssemblerResult`, che è un oggetto `Map` contenente i documenti PDF risultanti.
   * Scorrere l&#39;oggetto `Map` fino a trovare la chiave corrispondente al nome del documento risultante. Quindi esegui il cast di `value` del membro dell&#39;array in un `BLOB`.
   * Estrarre i dati binari che rappresentano il documento PDF accedendo alla proprietà `MTOM` dell&#39;oggetto `BLOB`. Restituisce una matrice di byte che è possibile scrivere in un file PDF.

**Consulta anche**

[Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
