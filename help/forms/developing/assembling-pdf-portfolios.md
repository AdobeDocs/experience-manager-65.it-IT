---
title: Assemblaggio di Portfoli PDF
seo-title: Assembling PDF Portfolios
description: Assembla un portfolio PDF per combinare diversi documenti di vari tipi, tra cui file word, file di immagini e documenti PDF. Puoi assemblare un portfolio PDF utilizzando un’API Java e un’API di servizio Web.
seo-description: Assemble a PDF portfolio to combine several documents of various types, including word file, image files, and PDF documents. You can assemble a PDF portfolio using a Java API and a Web Service API.
uuid: 1778c90b-9d26-466b-a7c7-401d737395e0
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 023f0d9e-bfde-4879-a839-085fadffb48e
role: Developer
exl-id: d2bd7c3e-4f75-4234-a7aa-ee8524430493
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1828'
ht-degree: 0%

---

# Assemblaggio di Portfoli PDF {#assembling-pdf-portfolios}

**Esempi ed esempi in questo documento sono solo per AEM Forms in ambiente JEE.**

Puoi assemblare un Portfolio PDF utilizzando l’API di Assembler Java e servizio Web. Un portfolio può combinare diversi documenti di vari tipi, tra cui file word, file di immagini (ad esempio, un file jpeg) e documenti PDF. Il layout del portfolio può essere impostato su stili diversi, come il *Griglia con anteprima*, *Su un&#39;immagine* layout o pari *Rivoluzione*.

La seguente illustrazione è una schermata di un portfolio con *Su un&#39;immagine* layout stile.

![ap_ap_portfolio](assets/ap_ap_portfolio.png)

La creazione di un Portfolio PDF è un&#39;alternativa inutile al passaggio di una raccolta di documenti. Utilizzando AEM Forms è possibile creare portfolio richiamando il servizio Assembler con un documento DDX strutturato. Il seguente documento DDX è un esempio di documento DDX che crea un Portfolio PDF.

```xml
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
     <PDF result="portfolio1.pdf">
         <Portfolio>
             <Navigator source="myNavigator">
                 <Resource name="navigator/image.xxx" source="myImage.png"/>
             </Navigator>
         </Portfolio>
         <PackageFiles source="dog1"  >
              <FieldData name="X">72</FieldData>
             <FieldData name="Y">72</FieldData>
             <File filename="saint_bernard.jpg" mimetype="image/jpeg"/>
         </PackageFiles>
         <PackageFiles source="dog2"  >
             <FieldData name="X">120</FieldData>
             <FieldData name="Y">216</FieldData>
             <File filename="greyhound.pdf"/>
         </PackageFiles>
     </PDF>
 </DDX>
```

Il documento DXX deve contenere un `Portfolio` con un tag nidificato `Navigator` tag . Nota il tag `<Resource name="navigator/image.xxx" source="myImage.png"/>` è necessario solo se `myNavigator` viene assegnato come navigatore layout onImage: `AdobeOnImage.nav`. Questo tag consente al servizio Assembler di selezionare l&#39;immagine da utilizzare come sfondo del portfolio. Includi `PackageFiles` e `File` tag per definire il nome file e il tipo MIME del file in pacchetto.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Assembler, vedere [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Per ulteriori informazioni su un documento DDX, consulta [Servizio di assemblaggio e riferimento DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Riepilogo dei passaggi {#summary-of-steps}

Per creare un Portfolio PDF, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Creare un client PDF Assembler.
1. Fai riferimento a un documento DDX esistente.
1. Fare riferimento ai documenti richiesti.
1. Impostare le opzioni di esecuzione.
1. Assembla il portafoglio.
1. Salva il portafoglio assemblato.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso della classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è distribuito su JBoss)
* jbossall-client.jar (richiesto se AEM Forms è distribuito su JBoss)

**Creare un client PDF Assembler**

Prima di eseguire un&#39;operazione Assembler a livello di programmazione, creare un client di servizio Assembler.

**Riferimento a un documento DDX esistente**

Per assemblare un Portfolio PDF è necessario fare riferimento a un documento DDX. Questo documento DDX deve contenere `Portfolio`, `Navigator` e `PackageFiles` elementi.

**Riferimento ai documenti richiesti**

Per assemblare un Portfolio PDF, fare riferimento a tutti i file che rappresentano i documenti da assemblare. Ad esempio, trasmettere al servizio Assembler tutti i file immagine specificati nel documento DDX. Tieni presente che nel documento DDX specificato in questa sezione viene fatto riferimento a questi file: *myImage.png* e *saint_bernard.jpg*.

Quando si assembla un Portfolio PDF, passare un file NAV (un file navigatore) al servizio Assembler. Il file NAV passato al servizio Assembler dipende dal tipo di Portfolio PDF da creare. Ad esempio, per creare un *Su un&#39;immagine* , passa il file AdobeOnImage.nav. È possibile individuare i file NAV nella cartella seguente:

`<Install folder>\Acrobat 9.0\Acrobat\Navigators`

Copia il file NAV dalla directory di installazione di Acrobat 9 (o versioni successive). Posizionare il file NAV in un percorso in cui l’applicazione client può accedervi. Tutti i file vengono passati al servizio Assembler all&#39;interno di un oggetto raccolta Map.

>[!NOTE]
>
>Gli avvii rapidi associati all’assemblaggio di Portfoli PDF utilizzano AdobeOnImage.nav.

**Impostare le opzioni di esecuzione**

È possibile impostare le opzioni di esecuzione che controllano il comportamento del servizio Assembler mentre esegue un processo. Ad esempio, è possibile impostare un&#39;opzione che indica al servizio Assembler di continuare l&#39;elaborazione di un processo in caso di errore.

**Assembla il portafoglio**

Per assemblare un Portfolio PDF, è necessario chiamare il `invokeDDX` funzionamento. Il servizio Assembler restituisce il Portfolio PDF all&#39;interno di un oggetto raccolta.

**Salva il portafoglio assemblato**

All&#39;interno di un oggetto raccolta viene restituito un Portfolio PDF. Iterare l’oggetto raccolta e salvare il Portfolio PDF come file PDF.

**Consulta anche**

[Creare un Portfolio PDF utilizzando l’API Java](#assemble-a-pdf-portfolio-using-the-java-api)

[Assemblare un Portfolio PDF utilizzando l’API del servizio Web](#assemble-a-pdf-portfolio-using-the-web-service-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Assemblaggio di documenti PDF a livello di programmazione](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Creare un Portfolio PDF utilizzando l’API Java {#assemble-a-pdf-portfolio-using-the-java-api}

Assemblare un Portfolio PDF utilizzando l&#39;API del servizio Assembler (Java):

1. Includi file di progetto.

   Includi file JAR client, come adobe-assembler-client.jar, nel percorso di classe del progetto Java.

1. Creare un client PDF Assembler.

   * Crea un `ServiceClientFactory` oggetto contenente le proprietà di connessione.
   * Crea un `AssemblerServiceClient` utilizzando il relativo costruttore e passando `ServiceClientFactory` oggetto.

1. Fai riferimento a un documento DDX esistente.

   * Crea un `java.io.FileInputStream` oggetto che rappresenta il documento DDX utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del file DDX.
   * Crea un `com.adobe.idp.Document` utilizzando il relativo costruttore e passando `java.io.FileInputStream` oggetto.

1. Fare riferimento ai documenti richiesti.

   * Crea un `java.util.Map` oggetto utilizzato per memorizzare i documenti PDF di input utilizzando un `HashMap` costruttore.
   * Crea un `java.io.FileInputStream` utilizzando il relativo costruttore. Passa la posizione del file NAV richiesto (ripeti questa attività per ogni file necessario per creare un portfolio).
   * Crea un `com.adobe.idp.Document` e passare `java.io.FileInputStream` oggetto che contiene il file NAV (ripetere questa attività per ogni file necessario per creare un portfolio).
   * Aggiungi una voce al `java.util.Map` richiamandone l&#39;oggetto `put` e passare gli argomenti seguenti:

      * Valore stringa che rappresenta il nome della chiave. Questo valore deve corrispondere al valore dell&#39;elemento di origine specificato nel documento DDX. (ripeti questa attività per ogni file necessario per creare un portfolio).
      * A `com.adobe.idp.Document` oggetto contenente il documento PDF. (ripeti questa attività per ogni file necessario per creare un portfolio).

1. Impostare le opzioni di esecuzione.

   * Crea un `AssemblerOptionSpec` oggetto che memorizza le opzioni di esecuzione utilizzando il relativo costruttore.
   * Impostare le opzioni di esecuzione per soddisfare i requisiti aziendali richiamando un metodo che appartiene al `AssemblerOptionSpec` oggetto. Ad esempio, per dare istruzioni al servizio Assembler di continuare a elaborare un processo quando si verifica un errore, richiama il `AssemblerOptionSpec` dell’oggetto `setFailOnError` metodo e passaggio `false`.

1. Assembla il portafoglio.

   Richiama il `AssemblerServiceClient` dell’oggetto `invokeDDX` e trasmettere i seguenti valori richiesti:

   * A `com.adobe.idp.Document` oggetto che rappresenta il documento DDX da utilizzare
   * A `java.util.Map` che contiene i file necessari per creare un Portfolio PDF.
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` oggetto che specifica le opzioni di runtime, tra cui il font predefinito e il livello di log del processo

   La `invokeDDX` restituisce un `com.adobe.livecycle.assembler.client.AssemblerResult` oggetto che contiene il Portfolio PDF assemblato ed eventuali eccezioni.

1. Salva il portafoglio assemblato.

   Per ottenere il Portfolio PDF, esegui le seguenti operazioni:

   * Richiama il `AssemblerResult` dell’oggetto `getDocuments` metodo . Questo metodo restituisce un `java.util.Map` oggetto.
   * Itera attraverso il `java.util.Map` finché non trovi il risultato `com.adobe.idp.Document` oggetto.
   * Richiama il `com.adobe.idp.Document` dell’oggetto `copyToFile` per estrarre il Portfolio PDF.

**Consulta anche**

[Avvio rapido (modalità SOAP): Assemblaggio di Portfoli PDF tramite l’API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-pdf-portfolios-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Assemblare un Portfolio PDF utilizzando l’API del servizio Web {#assemble-a-pdf-portfolio-using-the-web-service-api}

Assemblare un Portfolio PDF utilizzando l&#39;API del servizio Assembler (servizio Web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Quando imposti un riferimento a un servizio, assicurati di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

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
   * Compilare l&#39;array di byte con i dati del flusso richiamando il `System.IO.FileStream` dell’oggetto `Read` metodo . Passa la matrice dei byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare `BLOB` oggetto assegnando il relativo `MTOM` con il contenuto dell&#39;array di byte.

1. Fare riferimento ai documenti richiesti.

   * Per ogni file di input, crea un `BLOB` utilizzando il relativo costruttore. La `BLOB` viene utilizzato per memorizzare il file di input.
   * Crea un `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file di input e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto del `System.IO.FileStream` oggetto. È possibile determinare le dimensioni dell&#39;array di byte ottenendo il `System.IO.FileStream` dell’oggetto `Length` proprietà.
   * Compilare l&#39;array di byte con i dati del flusso richiamando il `System.IO.FileStream` dell’oggetto `Read` metodo . Passa la matrice dei byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare `BLOB` oggetto assegnando il relativo `MTOM` con il contenuto dell&#39;array di byte.
   * Crea un `MyMapOf_xsd_string_To_xsd_anyType` oggetto. Questo oggetto raccolta viene utilizzato per memorizzare i file di input necessari per creare un Portfolio PDF.
   * Per ogni file di input, crea un `MyMapOf_xsd_string_To_xsd_anyType_Item` oggetto.
   * Assegna un valore stringa che rappresenta il nome della chiave al `MyMapOf_xsd_string_To_xsd_anyType_Item` dell&#39;oggetto `key` campo . Questo valore deve corrispondere al valore dell&#39;elemento specificato nel documento DDX. Esegui questa operazione per ogni file di input.
   * Assegna `BLOB` oggetto che memorizza il file di input nel `MyMapOf_xsd_string_To_xsd_anyType_Item` dell&#39;oggetto `value` campo . Esegui questa operazione per ogni documento di input PDF.
   * Aggiungi il `MyMapOf_xsd_string_To_xsd_anyType_Item` dell&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType` oggetto. Richiama il `MyMapOf_xsd_string_To_xsd_anyType` dell&#39;oggetto `Add` e passare il `MyMapOf_xsd_string_To_xsd_anyType` oggetto. Esegui questa operazione per ogni documento di input PDF.

1. Impostare le opzioni di esecuzione.

   * Crea un `AssemblerOptionSpec` oggetto che memorizza le opzioni di esecuzione utilizzando il relativo costruttore.
   * Impostare le opzioni di esecuzione per soddisfare i requisiti aziendali assegnando un valore a un membro dati che appartiene al `AssemblerOptionSpec` oggetto. Ad esempio, per dare istruzioni al servizio Assembler di continuare a elaborare un processo quando si verifica un errore, assegnare `false` al `AssemblerOptionSpec` dell’oggetto `failOnError` membro dati.

1. Assembla il portafoglio.

   Richiama il `AssemblerServiceClient` dell’oggetto `invokeDDX` e passare i seguenti valori:

   * A `BLOB` oggetto che rappresenta il documento DDX
   * La `MyMapOf_xsd_string_To_xsd_anyType` oggetto contenente i file richiesti
   * Un `AssemblerOptionSpec` oggetto che specifica le opzioni di esecuzione

   La `invokeDDX` restituisce un `AssemblerResult` oggetto contenente i risultati del processo ed eventuali eccezioni.

1. Salva il portafoglio assemblato.

   Per ottenere il Portfolio PDF appena creato, esegui le seguenti operazioni:

   * Accedere al `AssemblerResult` dell’oggetto `documents` un campo `Map` oggetto contenente i documenti PDF risultanti.
   * Itera attraverso il `Map` per ottenere ogni documento risultante. Quindi, eseguire il cast del membro dell&#39;array `value` a `BLOB`.
   * Estrarre i dati binari che rappresentano il documento PDF accedendo ai relativi `BLOB` dell’oggetto `MTOM` proprietà. Restituisce una matrice di byte che è possibile scrivere in un file PDF.

**Consulta anche**

[Richiamo di AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamo di AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
