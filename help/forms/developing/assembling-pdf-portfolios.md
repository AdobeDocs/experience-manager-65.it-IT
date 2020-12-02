---
title: Assemblare Portfoli PDF
seo-title: Assemblare Portfoli PDF
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


# Assemblaggio di Portfoli PDF {#assembling-pdf-portfolios}

È possibile assemblare un Portfolio PDF utilizzando l&#39;Assembler Java e l&#39;API del servizio Web. Un portfolio può combinare diversi documenti di vari tipi, tra cui file Word, file immagine (ad esempio, un file jpeg) e documenti PDF. Il layout del portfolio può essere impostato su stili diversi come la *Griglia con Preview*, il *Su un layout Immagine* o anche *Rivoluzione*.

L&#39;illustrazione seguente è una schermata di un portfolio con layout di stile *Su un&#39;immagine*.

![ap_ap_portfolio](assets/ap_ap_portfolio.png)

La creazione di un Portfolio PDF può essere utilizzata come alternativa inutilizzata al passaggio di una raccolta di documenti. Utilizzando  AEM Forms è possibile creare portfolio richiamando il servizio Assembler con un documento DDX strutturato. Il seguente documento DDX è un esempio di documento DDX che crea un Portfolio PDF.

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

Il documento DXX deve contenere un tag `Portfolio` con un tag nidificato `Navigator`. Notate che il tag `<Resource name="navigator/image.xxx" source="myImage.png"/>` è necessario solo se `myNavigator` è assegnato come navigatore di layout onImage: `AdobeOnImage.nav`. Questo tag consente al servizio Assembler di selezionare l&#39;immagine da usare come sfondo del portfolio. Includete i tag `PackageFiles` e `File` per definire il nome file e il tipo MIME del file del pacchetto.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Assembler, vedere [Guida di riferimento dei servizi per  AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Per ulteriori informazioni su un documento DDX, vedere [Servizio Assembler e Riferimento DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Riepilogo dei passaggi {#summary-of-steps}

Per creare un Portfolio PDF, effettuare le seguenti operazioni:

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
* adobe-utilities.jar (richiesto se  AEM Forms è distribuito su JBoss)
* jbossall-client.jar (richiesto se  AEM Forms è distribuito su JBoss)

**Creare un client Assembler PDF**

Prima di eseguire un&#39;operazione Assembler a livello di programmazione, create un client di servizio Assembler.

**Riferimento a un documento DDX esistente**

Per assemblare un Portfolio PDF è necessario fare riferimento a un documento DDX. Il documento DDX deve contenere gli elementi `Portfolio`, `Navigator` e `PackageFiles`.

**Riferimento ai documenti richiesti**

Per assemblare un Portfolio PDF, fare riferimento a tutti i file che rappresentano i documenti da assemblare. Ad esempio, trasmettere al servizio Assembler tutti i file immagine specificati nel documento DDX. Tenere presente che a questi file viene fatto riferimento nel documento DDX specificato in questa sezione: *myImage.png* e *saint_bernard.jpg*.

Quando assemblate un Portfolio PDF, passate un file NAV (un file di navigazione) al servizio Assembler. Il file NAV passato al servizio Assembler dipende dal tipo di Portfolio PDF da creare. Ad esempio, per creare un layout *Su un&#39;immagine*, passate il file AdobeOnImage.nav. Potete individuare i file NAV nella cartella seguente:

`<Install folder>\Acrobat 9.0\Acrobat\Navigators`

Copiate il file NAV dalla directory di installazione di  Acrobat 9 (o versione successiva). Posizionare il file NAV in un percorso in cui l&#39;applicazione client può accedervi. Tutti i file vengono passati al servizio Assembler all&#39;interno di un oggetto raccolta Map.

>[!NOTE]
>
>Gli avvii rapidi associati all’assemblaggio di Portfoli PDF utilizzano AdobeOnImage.nav.

**Impostazione delle opzioni di esecuzione**

È possibile impostare opzioni di esecuzione che controllano il comportamento del servizio Assembler mentre esegue un processo. Ad esempio, potete impostare un&#39;opzione che indichi al servizio Assembler di continuare l&#39;elaborazione di un processo in caso di errore.

**Assemblare il portafoglio**

Per assemblare un Portfolio PDF, è necessario chiamare l&#39;operazione `invokeDDX`. Il servizio Assembler restituisce il Portfolio PDF all&#39;interno di un oggetto raccolta.

**Salva il portafoglio assemblato**

Un Portfolio PDF viene restituito all&#39;interno di un oggetto raccolta. Iterare l&#39;oggetto raccolta e salvare l&#39;Portfolio PDF come file PDF.

**Consulta anche**

[Assemblare un Portfolio PDF utilizzando l&#39;API Java](#assemble-a-pdf-portfolio-using-the-java-api)

[Assemblare un Portfolio PDF utilizzando l&#39;API del servizio Web](#assemble-a-pdf-portfolio-using-the-web-service-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Assemblaggio di documenti PDF a livello di programmazione](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Assemblare un Portfolio PDF utilizzando l&#39;API Java {#assemble-a-pdf-portfolio-using-the-java-api}

Assemblate un Portfolio PDF utilizzando l&#39;API di Assembler Service (Java):

1. Includere i file di progetto.

   Includete file JAR client, ad esempio adobe-assembler-client.jar, nel percorso di classe del progetto Java.

1. Creare un client Assembler PDF.

   * Creare un oggetto `ServiceClientFactory` che contiene le proprietà di connessione.
   * Creare un oggetto `AssemblerServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Fare riferimento a un documento DDX esistente.

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento DDX utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del file DDX.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Fate riferimento ai documenti richiesti.

   * Creare un oggetto `java.util.Map` utilizzato per memorizzare i documenti PDF di input utilizzando un costruttore `HashMap`.
   * Creare un oggetto `java.io.FileInputStream` utilizzando il relativo costruttore. Passa la posizione del file NAV richiesto (ripeti questa attività per ogni file necessario per creare un portfolio).
   * Create un oggetto `com.adobe.idp.Document` e passate l&#39;oggetto `java.io.FileInputStream` che contiene il file NAV (ripetete questa attività per ogni file necessario per creare un portfolio).
   * Aggiungere una voce all&#39;oggetto `java.util.Map` richiamandone il metodo `put` e trasmettendo gli argomenti seguenti:

      * Un valore di stringa che rappresenta il nome della chiave. Questo valore deve corrispondere al valore dell&#39;elemento di origine specificato nel documento DDX. Ripetete questa attività per ogni file necessario per creare un portfolio.
      * Un oggetto `com.adobe.idp.Document` che contiene il documento PDF. Ripetete questa attività per ogni file necessario per creare un portfolio.

1. Impostare le opzioni di esecuzione.

   * Creare un oggetto `AssemblerOptionSpec` che memorizza le opzioni di esecuzione utilizzando il relativo costruttore.
   * Impostate le opzioni di runtime per soddisfare i requisiti aziendali richiamando un metodo che appartiene all&#39;oggetto `AssemblerOptionSpec`. Ad esempio, per indicare al servizio Assembler di continuare a elaborare un processo quando si verifica un errore, richiamare il metodo `AssemblerOptionSpec` dell&#39;oggetto `setFailOnError` e passare `false`.

1. Assemblate il portafoglio.

   Richiamare il metodo `AssemblerServiceClient` dell&#39;oggetto `invokeDDX` e trasmettere i seguenti valori obbligatori:

   * Un oggetto `com.adobe.idp.Document` che rappresenta il documento DDX da utilizzare
   * Un oggetto `java.util.Map` che contiene i file necessari per creare un Portfolio PDF.
   * Un oggetto `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` che specifica le opzioni di runtime, incluso il font predefinito e il livello di registro del processo

   Il metodo `invokeDDX` restituisce un oggetto `com.adobe.livecycle.assembler.client.AssemblerResult` che contiene l&#39;Portfolio PDF assemblato ed eventuali eccezioni che si sono verificate.

1. Salvate il portafoglio assemblato.

   Per ottenere l’Portfolio PDF, effettuare le seguenti operazioni:

   * Richiamare il metodo `AssemblerResult` dell&#39;oggetto `getDocuments`. Questo metodo restituisce un oggetto `java.util.Map`.
   * Iterate l&#39;oggetto `java.util.Map` fino a individuare l&#39;oggetto `com.adobe.idp.Document` risultante.
   * Richiamare il metodo `com.adobe.idp.Document` dell&#39;oggetto `copyToFile` per estrarre l&#39;Portfolio PDF.

**Consulta anche**

[Avvio rapido (modalità SOAP): Assemblare Portfoli PDF utilizzando l&#39;API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-pdf-portfolios-using-the-java-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Assemblare un Portfolio PDF utilizzando l&#39;API del servizio Web {#assemble-a-pdf-portfolio-using-the-web-service-api}

Assemblate un Portfolio PDF utilizzando l&#39;API di Assembler Service (servizio Web):

1. Includere i file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Quando imposti un riferimento a un servizio, accertatevi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

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
   * Compilare l&#39;oggetto `BLOB` assegnandone la proprietà `MTOM` con il contenuto dell&#39;array di byte.

1. Fate riferimento ai documenti richiesti.

   * Per ciascun file di input, creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare il file di input.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file di input e la modalità in cui aprire il file.
   * Creare un array di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà `System.IO.FileStream` dell&#39;oggetto `Length`.
   * Compilare l&#39;array di byte con i dati del flusso richiamando il metodo `System.IO.FileStream` dell&#39;oggetto `Read`. Passare l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando il relativo campo `MTOM` con il contenuto dell&#39;array di byte.
   * Creare un oggetto `MyMapOf_xsd_string_To_xsd_anyType`. Questo oggetto raccolta viene utilizzato per memorizzare i file di input necessari per creare un Portfolio PDF.
   * Per ciascun file di input, create un oggetto `MyMapOf_xsd_string_To_xsd_anyType_Item`.
   * Assegnare un valore di stringa che rappresenta il nome chiave al campo `MyMapOf_xsd_string_To_xsd_anyType_Item` dell&#39;oggetto `key`. Questo valore deve corrispondere al valore dell&#39;elemento specificato nel documento DDX. (Eseguire questa operazione per ciascun file di input).
   * Assegnare l&#39;oggetto `BLOB` che memorizza il file di input nel campo `MyMapOf_xsd_string_To_xsd_anyType_Item` dell&#39;oggetto `value`. (Eseguire questa operazione per ciascun documento PDF di input.)
   * Aggiungere l&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType_Item` all&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType`. Richiamare il metodo `MyMapOf_xsd_string_To_xsd_anyType` dell&#39;oggetto `Add` e passare l&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType`. (Eseguire questa operazione per ciascun documento PDF di input.)

1. Impostare le opzioni di esecuzione.

   * Creare un oggetto `AssemblerOptionSpec` che memorizza le opzioni di esecuzione utilizzando il relativo costruttore.
   * Impostare le opzioni di runtime per soddisfare i requisiti aziendali assegnando un valore a un membro di dati che appartiene all&#39;oggetto `AssemblerOptionSpec`. Ad esempio, per indicare al servizio Assembler di continuare l&#39;elaborazione di un processo in caso di errore, assegnare `false` al membro di dati `AssemblerOptionSpec` dell&#39;oggetto `failOnError`.

1. Assemblate il portafoglio.

   Richiamare il metodo `AssemblerServiceClient` dell&#39;oggetto `invokeDDX` e trasmettere i seguenti valori:

   * Un oggetto `BLOB` che rappresenta il documento DDX
   * L&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType` che contiene i file richiesti
   * Un oggetto `AssemblerOptionSpec` che specifica le opzioni di esecuzione

   Il metodo `invokeDDX` restituisce un oggetto `AssemblerResult` che contiene i risultati del processo ed eventuali eccezioni.

1. Salvate il portafoglio assemblato.

   Per ottenere l’Portfolio PDF appena creato, effettuare le seguenti operazioni:

   * Accedere al campo `documents` dell&#39;oggetto `AssemblerResult`, che è un oggetto `Map` contenente i documenti PDF risultanti.
   * Iterate l&#39;oggetto `Map` per ottenere ogni documento risultante. Quindi, proiettare l&#39;elemento `value` del membro della matrice su un elemento `BLOB`.
   * Estrarre i dati binari che rappresentano il documento PDF accedendo alla proprietà `BLOB` dell&#39;oggetto `MTOM`. Questo restituisce un array di byte che è possibile scrivere in un file PDF.

**Consulta anche**

[Chiamata  AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chiamata  AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
