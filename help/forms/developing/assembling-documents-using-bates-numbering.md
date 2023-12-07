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
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '1910'
ht-degree: 0%

---

# Assemblaggio di documenti mediante la numerazione Bates {#assembling-documents-using-bates-numbering}

**Gli esempi e gli esempi contenuti in questo documento sono solo per l’ambiente AEM Forms su JEE.**

È possibile assemblare documenti PDF che contengono identificatori di pagina univoci utilizzando la numerazione Bates. *Numerazione Bates* è un metodo per applicare identificatori univoci a un batch di documenti correlati. A ogni pagina del documento (o set di documenti) viene assegnato un numero Bates che identifica in modo univoco la pagina. Ad esempio, i documenti di fabbricazione che contengono informazioni sulla distinta base e sono associati alla produzione di un assieme possono contenere un identificatore. Un numero Bates contiene un valore numerico incrementato in sequenza e un prefisso e un suffisso opzionali. Il prefisso + suffisso numerico + viene indicato come *pattern di bates*.

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
>Prima di leggere questa sezione, è consigliabile avere familiarità con l&#39;assemblaggio di documenti PDF utilizzando il servizio Assembler. In questa sezione non vengono descritti i concetti, ad esempio la creazione di un oggetto di raccolta contenente documenti di input o l&#39;estrazione dei risultati dall&#39;oggetto di raccolta restituito. (vedere [Assemblaggio di documenti PDF a livello di programmazione](/help/forms/developing/programmatically-assembling-pdf-documents.md).)

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Assembler, vedere [Guida di riferimento dei servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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

Se AEM Forms viene distribuito su un server applicazioni J2EE supportato diverso da JBoss, è necessario sostituire i file adobe-utilities.jar e jbossall-client.jar con file JAR specifici per il server applicazioni J2EE in cui viene distribuito AEM Forms. Per informazioni sulla posizione di tutti i file JAR di AEM Forms, vedi [Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un client PDF Assembler**

Prima di poter eseguire un&#39;operazione Assembler a livello di programmazione, è necessario creare un client del servizio Assembler.

**Riferimento a un documento DDX esistente**

Per assemblare un documento PDF è necessario fare riferimento a un documento DDX. Si consideri ad esempio il documento DDX introdotto in questa sezione. Per assemblare un documento PDF contenente identificatori di pagina univoci, il documento DDX deve contenere `BatesNumber` elemento.

**Documentazione di input PDF di riferimento**

Per assemblare un documento PDF, è necessario fare riferimento ai documenti PDF di input. Ad esempio, è necessario fare riferimento ai documenti map.pdf e direction.pdf per assemblare questi documenti PDF in un unico documento PDF.

**Imposta il valore del numero Bates iniziale**

È possibile impostare il valore del numero Bates iniziale per soddisfare i requisiti aziendali. Ad esempio, si supponga che sia necessario impostare il valore iniziale su 000100. Se non si imposta il valore iniziale, viene 000000 il valore della prima pagina.

**Assemblare i documenti di input PDF**

Dopo aver creato il client del servizio Assembler, fare riferimento al documento DDX che contiene `BatesNumber` informazioni sull&#39;elemento, fare riferimento a un documento di input PDF e impostare le opzioni di runtime, è possibile richiamare `invokeDDX` operazione che determina l&#39;assemblaggio da parte del servizio Assembler di un documento PDF contenente identificatori di pagina univoci.

**Estrarre i risultati**

Il servizio Assembler restituisce un insieme che contiene i risultati del processo. È possibile estrarre il documento PDF risultante ed eventuali eccezioni generate. In questa situazione, un documento PDF crittografato si trova all&#39;interno dell&#39;oggetto raccolta.

>[!NOTE]
>
>Se si richiama l&#39;oggetto `invokeDDX` operazione. Questa operazione viene utilizzata quando si trasmettono due o più documenti di input PDF al servizio Assembler. Tuttavia, se si passa un solo documento di input PDF al servizio Assembler, è necessario richiamare `invokeOneDocument` operazione. Per informazioni sull&#39;utilizzo di questa operazione, vedere [Assemblaggio di documenti PDF crittografati](/help/forms/developing/assembling-encrypted-pdf-documents.md).

**Consulta anche**

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Assemblaggio di documenti PDF a livello di programmazione](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Assemblare documenti con numerazione Bates utilizzando l&#39;API Java {#assemble-documents-with-bates-numbering-using-the-java-api}

Assembla un documento PDF che utilizza identificatori di pagina univoci (numerazione Bates) utilizzando l’API del servizio Assembler (Java):

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
   * Per ogni documento di input PDF, crea un `java.io.FileInputStream` mediante il costruttore e passando la posizione del documento PDF di input. In questa situazione, passa il percorso di un documento di PDF non protetto.
   * Per ogni documento di input PDF, crea un `com.adobe.idp.Document` e passare il `java.io.FileInputStream` oggetto che contiene il documento PDF.
   * Aggiungi una voce al `java.util.Map` oggetto richiamando il relativo `put` e fornendo i seguenti argomenti:

      * Valore stringa che rappresenta il nome della chiave. Questo valore deve corrispondere al valore dell&#39;elemento di origine PDF specificato nel documento DDX. Il nome del file di origine PDF specificato nel documento DDX introdotto in questa sezione è Loan.pdf.
      * A `com.adobe.idp.Document` oggetto che contiene il documento PDF non protetto.

1. Imposta il valore del numero Bates iniziale.

   * Creare un `AssemblerOptionSpec` oggetto che memorizza le opzioni di runtime mediante il relativo costruttore.
   * Impostare il numero Bates iniziale richiamando il `AssemblerOptionSpec` dell&#39;oggetto `setFirstBatesNumber` e passando un valore numerico che specifica il valore iniziale.

1. Assemblare i documenti di input PDF.

   Richiama `AssemblerServiceClient` dell&#39;oggetto `invokeDDX` e trasmettere i seguenti valori richiesti:

   * A `com.adobe.idp.Document` oggetto che rappresenta il documento DDX.
   * A `java.util.Map` oggetto contenente il file PDF non protetto di input.
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` oggetto che specifica le opzioni di runtime, inclusi il tipo di carattere predefinito e il livello di registro del processo.

   Il `invokeDDX` il metodo restituisce un `com.adobe.livecycle.assembler.client.AssemblerResult` oggetto contenente un documento PDF crittografato con password.

1. Estrai i risultati.

   Per ottenere il documento di PDF appena creato, effettuare le seguenti operazioni:

   * Richiama `AssemblerResult` dell&#39;oggetto `getDocuments` metodo. Questa azione restituisce un `java.util.Map` oggetto.
   * Effettua iterazione attraverso `java.util.Map` finché non trovi il `com.adobe.idp.Document` oggetto.
   * Richiama `com.adobe.idp.Document` dell&#39;oggetto `copyToFile` per estrarre il documento PDF.

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
   * Creare un `System.IO.FileStream` richiamando il relativo costruttore e passando un valore stringa che rappresenta la posizione del file del documento DDX e la modalità di apertura del file in.
   * Creare una matrice di byte che memorizza il contenuto della `System.IO.FileStream` oggetto. È possibile determinare le dimensioni della matrice di byte ottenendo `System.IO.FileStream` dell&#39;oggetto `Length` proprietà.
   * Compilare la matrice di byte con i dati di flusso richiamando `System.IO.FileStream` dell&#39;oggetto `Read` metodo. Passare la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare il `BLOB` oggetto assegnando il relativo `MTOM` con il contenuto della matrice di byte.

1. Fai riferimento ai documenti di input PDF.

   * Per ogni documento di input PDF, crea un `BLOB` mediante il costruttore. Il `BLOB` L&#39;oggetto viene utilizzato per memorizzare il documento di input PDF.
   * Creare un `System.IO.FileStream` richiamando il relativo costruttore. Passa un valore stringa che rappresenta la posizione del file del documento PDF di input e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto della `System.IO.FileStream` oggetto. È possibile determinare le dimensioni della matrice di byte ottenendo `System.IO.FileStream` dell&#39;oggetto `Length` proprietà.
   * Compilare la matrice di byte con i dati di flusso richiamando `System.IO.FileStream` dell&#39;oggetto `Read` metodo. Passare la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare il `BLOB` oggetto assegnando il relativo `MTOM` con il contenuto della matrice di byte.
   * Creare un `MyMapOf_xsd_string_To_xsd_anyType` oggetto. Questo oggetto insieme viene utilizzato per memorizzare i documenti PDF di input.
   * Per ogni documento di input PDF, crea un `MyMapOf_xsd_string_To_xsd_anyType_Item` oggetto. Se ad esempio si utilizzano due documenti di input PDF, creare due `MyMapOf_xsd_string_To_xsd_anyType_Item` oggetti.
   * Assegna un valore stringa che rappresenta il nome della chiave al `MyMapOf_xsd_string_To_xsd_anyType_Item` dell&#39;oggetto `key` campo. Questo valore deve corrispondere al valore dell&#39;elemento di origine PDF specificato nel documento DDX. (Eseguire questa operazione per ogni documento di input PDF).
   * Assegna la `BLOB` oggetto che memorizza il documento PDF in `MyMapOf_xsd_string_To_xsd_anyType_Item` dell&#39;oggetto `value` campo. (Eseguire questa operazione per ogni documento di input PDF).
   * Aggiungi il `MyMapOf_xsd_string_To_xsd_anyType_Item` oggetto al `MyMapOf_xsd_string_To_xsd_anyType` oggetto. Richiama `MyMapOf_xsd_string_To_xsd_anyType` dell&#39;oggetto `Add` e trasmettere il `MyMapOf_xsd_string_To_xsd_anyType` oggetto. (Eseguire questa operazione per ogni documento di input PDF).

1. Imposta il valore del numero Bates iniziale.

   * Creare un `AssemblerOptionSpec` oggetto che memorizza le opzioni di runtime mediante il relativo costruttore.
   * Impostare il numero di Bates iniziale assegnando un valore numerico al `firstBatesNumber` membro dati che appartiene al `AssemblerOptionSpec` oggetto.

1. Assemblare i documenti di input PDF.

   Richiama `AssemblerServiceClient` dell&#39;oggetto `invoke` e trasmettere i seguenti valori:

   * A `BLOB` oggetto che rappresenta il documento DDX.
   * Il `MyMapOf_xsd_string_To_xsd_anyType` oggetto contenente i documenti PDF di input. Le chiavi devono corrispondere ai nomi dei file di origine di PDF e i relativi valori devono essere `BLOB` oggetti corrispondenti a tali file.
   * Un `AssemblerOptionSpec` oggetto che specifica le opzioni di runtime.

   Il `invoke` il metodo restituisce un `AssemblerResult` oggetto contenente i risultati del processo ed eventuali eccezioni verificatesi.

1. Estrai i risultati.

   Per ottenere il documento di PDF appena creato, effettuare le seguenti operazioni:

   * Accedere a `AssemblerResult` dell&#39;oggetto `documents` campo, che è un `Map` oggetto che contiene i documenti PDF risultanti.
   * Effettua iterazione attraverso `Map` finché non viene individuata la chiave corrispondente al nome del documento risultante. Quindi esegui il cast del membro di array `value` a un `BLOB`.
   * Estrarre i dati binari che rappresentano il documento PDF accedendo al relativo `BLOB` dell&#39;oggetto `MTOM` proprietà. Restituisce una matrice di byte che è possibile scrivere in un file PDF.

**Consulta anche**

[Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
