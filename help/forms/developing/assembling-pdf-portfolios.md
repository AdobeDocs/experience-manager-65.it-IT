---
title: Assemblaggio di portfolio PDF
seo-title: Assemblaggio di portfolio PDF
description: 'null'
seo-description: 'null'
uuid: 1778c90b-9d26-466b-a7c7-401d737395e0
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 023f0d9e-bfde-4879-a839-085fadffb48e
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '1785'
ht-degree: 0%

---


# Assemblaggio di portfolio PDF {#assembling-pdf-portfolios}

È possibile assemblare un portfolio PDF utilizzando l&#39;Assembler Java e l&#39;API del servizio Web. Un portfolio può combinare diversi documenti di vari tipi, tra cui file Word, file immagine (ad esempio, un file jpeg) e documenti PDF. Il layout del portfolio può essere impostato su stili diversi come *Griglia con anteprima*, *Sul layout Immagine* o persino *Rivoluzione*.

L&#39;illustrazione seguente è una schermata di un portfolio con layout *In stile immagine* .

![ap_ap_portfolio](assets/ap_ap_portfolio.png)

La creazione di un portfolio PDF è un&#39;alternativa priva di supporti cartacei al passaggio di una raccolta di documenti. Utilizzando AEM Forms è possibile creare portfolio richiamando il servizio Assembler con un documento DDX strutturato. Il seguente documento DDX è un esempio di documento DDX che crea un portfolio PDF.

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

Il documento DXX deve contenere un `Portfolio` tag con un `Navigator` tag nidificato. Il tag `<Resource name="navigator/image.xxx" source="myImage.png"/>` è necessario solo se `myNavigator` è assegnato come navigatore di layout onImage: `AdobeOnImage.nav`. Questo tag consente al servizio Assembler di selezionare l&#39;immagine da usare come sfondo del portfolio. Includete `PackageFiles` e `File` i tag per definire il nome file e il tipo MIME del file del pacchetto.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Assembler, vedere Riferimento [servizi per i AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Per ulteriori informazioni su un documento DDX, vedere Servizio [Assembler e Riferimento](https://www.adobe.com/go/learn_aemforms_ddx_63)DDX.

## Riepilogo dei passaggi {#summary-of-steps}

Per creare un portfolio PDF, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un client Assembler PDF.
1. Fare riferimento a un documento DDX esistente.
1. Fate riferimento ai documenti richiesti.
1. Impostare le opzioni di esecuzione.
1. Assemblate il portafoglio.
1. Salvate il portafoglio assemblato.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, accertatevi di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (richiesto se i AEM Forms sono distribuiti su JBoss)
* jbossall-client.jar (richiesto se i AEM Forms sono distribuiti su JBoss)

**Creare un client Assembler PDF**

Prima di eseguire un&#39;operazione Assembler a livello di programmazione, create un client di servizio Assembler.

**Riferimento a un documento DDX esistente**

Per assemblare un portfolio PDF è necessario fare riferimento a un documento DDX. Il documento DDX deve contenere gli elementi `Portfolio`, `Navigator` e `PackageFiles` .

**Riferimento ai documenti richiesti**

Per assemblare un portfolio PDF, fare riferimento a tutti i file che rappresentano i documenti da assemblare. Ad esempio, trasmettere al servizio Assembler tutti i file immagine specificati nel documento DDX. Tenere presente che a questi file viene fatto riferimento nel documento DDX specificato in questa sezione: *myImage.png* e *saint_bernard.jpg*.

Quando assemblate un portfolio PDF, passate un file NAV (un file di navigazione) al servizio Assembler. Il file NAV passato al servizio Assembler dipende dal tipo di portfolio PDF da creare. Ad esempio, per creare un *layout Immagine* , passate il file AdobeOnImage.nav. Potete individuare i file NAV nella cartella seguente:

`<Install folder>\Acrobat 9.0\Acrobat\Navigators`

Copiare il file NAV dalla directory di installazione di Acrobat 9 (o versione successiva). Posizionare il file NAV in un percorso in cui l&#39;applicazione client può accedervi. Tutti i file vengono passati al servizio Assembler all&#39;interno di un oggetto raccolta Map.

>[!NOTE]
>
>Gli avvii rapidi associati all’assemblaggio di portfolio PDF utilizzano AdobeOnImage.nav.

**Impostazione delle opzioni di esecuzione**

È possibile impostare opzioni di esecuzione che controllano il comportamento del servizio Assembler mentre esegue un processo. Ad esempio, potete impostare un&#39;opzione che indichi al servizio Assembler di continuare l&#39;elaborazione di un processo in caso di errore.

**Assemblare il portafoglio**

Per assemblare un portfolio PDF, è necessario chiamare l&#39; `invokeDDX` operazione. Il servizio Assembler restituisce il portfolio PDF all&#39;interno di un oggetto raccolta.

**Salva il portafoglio assemblato**

Un portfolio PDF viene restituito all&#39;interno di un oggetto raccolta. Iterare l&#39;oggetto raccolta e salvare il portfolio PDF come file PDF.

**Consulta anche**

[Assemblare un portfolio PDF utilizzando l&#39;API Java](#assemble-a-pdf-portfolio-using-the-java-api)

[Assemblare un portfolio PDF utilizzando l&#39;API del servizio Web](#assemble-a-pdf-portfolio-using-the-web-service-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Assemblaggio di documenti PDF a livello di programmazione](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Assemblare un portfolio PDF utilizzando l&#39;API Java {#assemble-a-pdf-portfolio-using-the-java-api}

Assemblate un portfolio PDF utilizzando l&#39;API di Assembler Service (Java):

1. Includere i file di progetto.

   Includete file JAR client, ad esempio adobe-assembler-client.jar, nel percorso di classe del progetto Java.

1. Creare un client Assembler PDF.

   * Creare un `ServiceClientFactory` oggetto che contenga proprietà di connessione.
   * Creare un `AssemblerServiceClient` oggetto utilizzando il relativo costruttore e passando l&#39; `ServiceClientFactory` oggetto.

1. Fare riferimento a un documento DDX esistente.

   * Creare un `java.io.FileInputStream` oggetto che rappresenta il documento DDX utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del file DDX.
   * Creare un `com.adobe.idp.Document` oggetto utilizzando il relativo costruttore e passando l&#39; `java.io.FileInputStream` oggetto.

1. Fate riferimento ai documenti richiesti.

   * Creare un oggetto `java.util.Map` utilizzato per memorizzare i documenti PDF di input utilizzando un `HashMap` costruttore.
   * Creare un `java.io.FileInputStream` oggetto utilizzando il relativo costruttore. Passa la posizione del file NAV richiesto (ripeti questa attività per ogni file necessario per creare un portfolio).
   * Create un `com.adobe.idp.Document` oggetto e passate l&#39; `java.io.FileInputStream` oggetto che contiene il file NAV (ripetete questa attività per ogni file necessario per creare un portfolio).
   * Aggiungere una voce all&#39; `java.util.Map` oggetto richiamandone il `put` metodo e passando gli argomenti seguenti:

      * Un valore di stringa che rappresenta il nome della chiave. Questo valore deve corrispondere al valore dell&#39;elemento di origine specificato nel documento DDX. Ripetete questa attività per ogni file necessario per creare un portfolio.
      * Un `com.adobe.idp.Document` oggetto che contiene il documento PDF. Ripetete questa attività per ogni file necessario per creare un portfolio.

1. Impostare le opzioni di esecuzione.

   * Creare un `AssemblerOptionSpec` oggetto che memorizza le opzioni di esecuzione utilizzando il relativo costruttore.
   * Impostate le opzioni di runtime per soddisfare i requisiti aziendali richiamando un metodo che appartiene all&#39; `AssemblerOptionSpec` oggetto. Ad esempio, per indicare al servizio Assembler di continuare a elaborare un processo quando si verifica un errore, richiamare il metodo dell&#39; `AssemblerOptionSpec` oggetto `setFailOnError` e passare `false`.

1. Assemblate il portafoglio.

   Richiamare il metodo dell&#39; `AssemblerServiceClient` oggetto `invokeDDX` e trasmettere i seguenti valori obbligatori:

   * Un `com.adobe.idp.Document` oggetto che rappresenta il documento DDX da utilizzare
   * Un `java.util.Map` oggetto che contiene i file necessari per creare un portfolio PDF.
   * Un `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` oggetto che specifica le opzioni di runtime, incluso il font predefinito e il livello di registro del processo

   Il `invokeDDX` metodo restituisce un `com.adobe.livecycle.assembler.client.AssemblerResult` oggetto che contiene il portfolio PDF assemblato ed eventuali eccezioni.

1. Salvate il portafoglio assemblato.

   Per ottenere il portfolio PDF, effettuare le seguenti operazioni:

   * Richiama il metodo dell’ `AssemblerResult` oggetto `getDocuments` . Questo metodo restituisce un `java.util.Map` oggetto.
   * Eseguire un&#39;iterazione sull&#39; `java.util.Map` oggetto fino a individuare l&#39; `com.adobe.idp.Document` oggetto risultante.
   * Richiamare il metodo dell&#39; `com.adobe.idp.Document` oggetto `copyToFile` per estrarre il portfolio PDF.

**Consulta anche**

[Avvio rapido (modalità SOAP): Assemblare portfolio PDF utilizzando l&#39;API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-pdf-portfolios-using-the-java-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Assemblare un portfolio PDF utilizzando l&#39;API del servizio Web {#assemble-a-pdf-portfolio-using-the-web-service-api}

Assemblate un portfolio PDF utilizzando l&#39;API di Assembler Service (servizio Web):

1. Includere i file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Quando imposti un riferimento a un servizio, accertatevi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

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
   * Compilare l&#39; `BLOB` oggetto assegnandone `MTOM` la proprietà con il contenuto dell&#39;array di byte.

1. Fate riferimento ai documenti richiesti.

   * Per ciascun file di input, creare un `BLOB` oggetto utilizzando il relativo costruttore. L&#39; `BLOB` oggetto viene utilizzato per memorizzare il file di input.
   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file di input e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto dell&#39; `System.IO.FileStream` oggetto. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà dell&#39; `System.IO.FileStream` oggetto `Length` .
   * Compilare l&#39;array di byte con i dati del flusso richiamando il metodo dell&#39; `System.IO.FileStream` oggetto `Read` . Passare l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39; `BLOB` oggetto assegnandone `MTOM` il campo con il contenuto dell&#39;array di byte.
   * Create a `MyMapOf_xsd_string_To_xsd_anyType` object. Questo oggetto raccolta viene utilizzato per memorizzare i file di input necessari per creare un portfolio PDF.
   * Per ciascun file di input, creare un `MyMapOf_xsd_string_To_xsd_anyType_Item` oggetto.
   * Assegnare un valore di stringa che rappresenta il nome chiave al campo dell&#39; `MyMapOf_xsd_string_To_xsd_anyType_Item` oggetto `key` . Questo valore deve corrispondere al valore dell&#39;elemento specificato nel documento DDX. (Eseguire questa operazione per ciascun file di input).
   * Assegnare l&#39; `BLOB` oggetto che memorizza il file di input al `MyMapOf_xsd_string_To_xsd_anyType_Item` campo dell&#39; `value` oggetto. (Eseguire questa operazione per ciascun documento PDF di input.)
   * Aggiungere l&#39; `MyMapOf_xsd_string_To_xsd_anyType_Item` oggetto all&#39; `MyMapOf_xsd_string_To_xsd_anyType` oggetto. Richiamare il `MyMapOf_xsd_string_To_xsd_anyType` metodo dell&#39;oggetto `Add` e passare l&#39; `MyMapOf_xsd_string_To_xsd_anyType` oggetto. (Eseguire questa operazione per ciascun documento PDF di input.)

1. Impostare le opzioni di esecuzione.

   * Creare un `AssemblerOptionSpec` oggetto che memorizza le opzioni di esecuzione utilizzando il relativo costruttore.
   * Impostare le opzioni di runtime per soddisfare i requisiti aziendali assegnando un valore a un membro di dati che appartiene all&#39; `AssemblerOptionSpec` oggetto. Ad esempio, per indicare al servizio Assembler di continuare l&#39;elaborazione di un processo in caso di errore, assegnare `false` al membro `AssemblerOptionSpec` dati dell&#39; `failOnError` oggetto.

1. Assemblate il portafoglio.

   Richiama il metodo dell’ `AssemblerServiceClient` oggetto `invokeDDX` e passa i seguenti valori:

   * Un `BLOB` oggetto che rappresenta il documento DDX
   * L&#39; `MyMapOf_xsd_string_To_xsd_anyType` oggetto che contiene i file richiesti
   * Un oggetto `AssemblerOptionSpec` che specifica le opzioni di esecuzione

   Il `invokeDDX` metodo restituisce un `AssemblerResult` oggetto che contiene i risultati del processo ed eventuali eccezioni.

1. Salvate il portafoglio assemblato.

   Per ottenere il portfolio PDF appena creato, effettuare le seguenti operazioni:

   * Accedere al campo `AssemblerResult` dell&#39; `documents` oggetto, ovvero un `Map` oggetto che contiene i documenti PDF risultanti.
   * Eseguire un&#39;iterazione sull&#39; `Map` oggetto per ottenere ogni documento risultante. Quindi, inserite il membro dell&#39;array `value` in un `BLOB`.
   * Estrarre i dati binari che rappresentano il documento PDF accedendo alla `BLOB` proprietà dell&#39; `MTOM` oggetto. Questo restituisce un array di byte che è possibile scrivere in un file PDF.

**Consulta anche**

[Chiamata di AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chiamata di AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
