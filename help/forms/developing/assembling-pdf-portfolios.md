---
title: Assemblaggio di Portfoli PDF
seo-title: Assemblaggio di Portfoli PDF
description: Assembla un portfolio PDF per combinare diversi documenti di vari tipi, tra cui file Word, file immagine e documenti PDF. Puoi assemblare un portfolio PDF utilizzando un’API Java e un’API di servizio Web.
seo-description: Assembla un portfolio PDF per combinare diversi documenti di vari tipi, tra cui file Word, file immagine e documenti PDF. Puoi assemblare un portfolio PDF utilizzando un’API Java e un’API di servizio Web.
uuid: 1778c90b-9d26-466b-a7c7-401d737395e0
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 023f0d9e-bfde-4879-a839-085fadffb48e
role: Developer (Sviluppatore)
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1866'
ht-degree: 0%

---


# Assemblaggio di Portfoli PDF {#assembling-pdf-portfolios}

**Esempi ed esempi in questo documento sono solo per AEM Forms in ambiente JEE.**

È possibile assemblare un Portfolio PDF utilizzando l&#39;API Assembler Java e il servizio Web. Un portfolio può combinare diversi documenti di vari tipi, tra cui file word, file di immagini (ad esempio, un file jpeg) e documenti PDF. Il layout del portfolio può essere impostato su stili diversi come la *Griglia con Anteprima*, il *Su un layout Immagine* o anche *Rivoluzione*.

La figura seguente è una schermata di un portfolio con layout di stile *Su immagine*.

![ap_ap_portfolio](assets/ap_ap_portfolio.png)

La creazione di un Portfolio PDF è un’alternativa inutile al passaggio di una raccolta di documenti. Utilizzando AEM Forms è possibile creare portfolio richiamando il servizio Assembler con un documento DDX strutturato. Il seguente documento DDX è un esempio di documento DDX che crea un Portfolio PDF.

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

Il documento DXX deve contenere un tag `Portfolio` nidificato con un tag `Navigator` nidificato. Il tag `<Resource name="navigator/image.xxx" source="myImage.png"/>` è necessario solo se `myNavigator` è assegnato come navigatore di layout onImage: `AdobeOnImage.nav`. Questo tag consente al servizio Assembler di selezionare l&#39;immagine da utilizzare come sfondo del portfolio. Includi i tag `PackageFiles` e `File` per definire il nome file e il tipo MIME del file in pacchetto.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Assembler, vedere [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Per ulteriori informazioni su un documento DDX, vedere [Servizio Assembler e Riferimento DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Riepilogo dei passaggi {#summary-of-steps}

Per creare un Portfolio PDF, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Creare un client Assembler PDF.
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

**Creare un client Assembler PDF**

Prima di eseguire un&#39;operazione Assembler a livello di programmazione, creare un client di servizio Assembler.

**Riferimento a un documento DDX esistente**

Per assemblare un Portfolio PDF è necessario fare riferimento a un documento DDX. Questo documento DDX deve contenere gli elementi `Portfolio`, `Navigator` e `PackageFiles`.

**Riferimento ai documenti richiesti**

Per assemblare un Portfolio PDF, fare riferimento a tutti i file che rappresentano i documenti da assemblare. Ad esempio, trasmettere al servizio Assembler tutti i file immagine specificati nel documento DDX. Tieni presente che nel documento DDX specificato in questa sezione viene fatto riferimento a questi file: *myImage.png* e *saint_bernard.jpg*.

Quando si assembla un Portfolio PDF, passare un file NAV (un file navigatore) al servizio Assembler. Il file NAV passato al servizio Assembler dipende dal tipo di Portfolio PDF da creare. Ad esempio, per creare un layout *Su un&#39;immagine*, passa il file AdobeOnImage.nav. È possibile individuare i file NAV nella cartella seguente:

`<Install folder>\Acrobat 9.0\Acrobat\Navigators`

Copia il file NAV dalla directory di installazione di Acrobat 9 (o versioni successive). Posizionare il file NAV in un percorso in cui l’applicazione client può accedervi. Tutti i file vengono passati al servizio Assembler all&#39;interno di un oggetto raccolta Map.

>[!NOTE]
>
>Gli avvii rapidi associati all&#39;assemblaggio di Portfoli PDF utilizzano AdobeOnImage.nav.

**Impostare le opzioni di esecuzione**

È possibile impostare le opzioni di esecuzione che controllano il comportamento del servizio Assembler mentre esegue un processo. Ad esempio, è possibile impostare un&#39;opzione che indica al servizio Assembler di continuare l&#39;elaborazione di un processo in caso di errore.

**Assembla il portafoglio**

Per assemblare un Portfolio PDF, è necessario chiamare l&#39;operazione `invokeDDX`. Il servizio Assembler restituisce il Portfolio PDF all&#39;interno di un oggetto raccolta.

**Salva il portafoglio assemblato**

All&#39;interno di un oggetto raccolta viene restituito un Portfolio PDF. Iterare l&#39;oggetto raccolta e salvare il Portfolio PDF come file PDF.

**Consulta anche**

[Assemblare un Portfolio PDF utilizzando l’API Java](#assemble-a-pdf-portfolio-using-the-java-api)

[Assemblare un Portfolio PDF utilizzando l’API del servizio Web](#assemble-a-pdf-portfolio-using-the-web-service-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Assemblaggio programmatico di documenti PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Assemblare un Portfolio PDF utilizzando l&#39;API Java {#assemble-a-pdf-portfolio-using-the-java-api}

Assemblare un Portfolio PDF utilizzando l&#39;API del servizio Assembler (Java):

1. Includi file di progetto.

   Includi file JAR client, come adobe-assembler-client.jar, nel percorso di classe del progetto Java.

1. Creare un client Assembler PDF.

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `AssemblerServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Fai riferimento a un documento DDX esistente.

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento DDX utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del file DDX.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Fare riferimento ai documenti richiesti.

   * Creare un oggetto `java.util.Map` utilizzato per memorizzare i documenti PDF di input utilizzando un costruttore `HashMap`.
   * Creare un oggetto `java.io.FileInputStream` utilizzando il relativo costruttore. Passa la posizione del file NAV richiesto (ripeti questa attività per ogni file necessario per creare un portfolio).
   * Crea un oggetto `com.adobe.idp.Document` e passa l&#39;oggetto `java.io.FileInputStream` che contiene il file NAV (ripeti questa attività per ogni file necessario per creare un portfolio).
   * Aggiungere una voce all&#39;oggetto `java.util.Map` richiamando il relativo metodo `put` e passando i seguenti argomenti:

      * Valore stringa che rappresenta il nome della chiave. Questo valore deve corrispondere al valore dell&#39;elemento di origine specificato nel documento DDX. (ripeti questa attività per ogni file necessario per creare un portfolio).
      * Un oggetto `com.adobe.idp.Document` contenente il documento PDF. (ripeti questa attività per ogni file necessario per creare un portfolio).

1. Impostare le opzioni di esecuzione.

   * Creare un oggetto `AssemblerOptionSpec` che memorizza le opzioni di esecuzione utilizzando il relativo costruttore.
   * Impostare le opzioni di esecuzione per soddisfare i requisiti aziendali richiamando un metodo appartenente all&#39;oggetto `AssemblerOptionSpec`. Ad esempio, per dare istruzioni al servizio Assembler di continuare a elaborare un processo quando si verifica un errore, richiamare il metodo `setFailOnError` dell&#39;oggetto `AssemblerOptionSpec` e passare `false`.

1. Assembla il portafoglio.

   Richiama il metodo `invokeDDX` dell&#39;oggetto `AssemblerServiceClient` e passa i seguenti valori obbligatori:

   * Un oggetto `com.adobe.idp.Document` che rappresenta il documento DDX da utilizzare
   * Un oggetto `java.util.Map` contenente i file necessari per creare un Portfolio PDF.
   * Un oggetto `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` che specifica le opzioni di runtime, incluso il font predefinito e il livello del log di lavoro

   Il metodo `invokeDDX` restituisce un oggetto `com.adobe.livecycle.assembler.client.AssemblerResult` contenente il Portfolio PDF assemblato ed eventuali eccezioni.

1. Salva il portafoglio assemblato.

   Per ottenere il Portfolio PDF, eseguire le operazioni seguenti:

   * Richiama il metodo `getDocuments` dell&#39;oggetto `AssemblerResult`. Questo metodo restituisce un oggetto `java.util.Map`.
   * Iterare l&#39;oggetto `java.util.Map` fino a trovare l&#39;oggetto `com.adobe.idp.Document` risultante.
   * Richiamare il metodo `copyToFile` dell&#39;oggetto `com.adobe.idp.Document` per estrarre il Portfolio PDF.

**Consulta anche**

[Avvio rapido (modalità SOAP): Assemblaggio di Portfoli PDF tramite l’API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-pdf-portfolios-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Assemblare un Portfolio PDF utilizzando l&#39;API del servizio Web {#assemble-a-pdf-portfolio-using-the-web-service-api}

Assemblare un Portfolio PDF utilizzando l&#39;API del servizio Assembler (servizio Web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Quando imposti un riferimento a un servizio, assicurati di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

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
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento DDX e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni dell&#39;array di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare l’array di byte con i dati del flusso richiamando il metodo `Read` dell’oggetto `System.IO.FileStream`. Passa la matrice dei byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando la relativa proprietà `MTOM` con il contenuto dell&#39;array di byte.

1. Fare riferimento ai documenti richiesti.

   * Per ogni file di input, creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare il file di input.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file di input e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni dell&#39;array di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare l’array di byte con i dati del flusso richiamando il metodo `Read` dell’oggetto `System.IO.FileStream`. Passa la matrice dei byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando il relativo campo `MTOM` con il contenuto dell&#39;array di byte.
   * Creare un oggetto `MyMapOf_xsd_string_To_xsd_anyType`. Questo oggetto raccolta viene utilizzato per memorizzare i file di input necessari per creare un Portfolio PDF.
   * Per ciascun file di input, creare un oggetto `MyMapOf_xsd_string_To_xsd_anyType_Item`.
   * Assegna un valore stringa che rappresenta il nome della chiave al campo `MyMapOf_xsd_string_To_xsd_anyType_Item` dell&#39;oggetto `key`. Questo valore deve corrispondere al valore dell&#39;elemento specificato nel documento DDX. Esegui questa operazione per ogni file di input.
   * Assegna l&#39;oggetto `BLOB` che memorizza il file di input nel campo `MyMapOf_xsd_string_To_xsd_anyType_Item` dell&#39;oggetto `value`. Esegui questa operazione per ogni documento PDF di input.
   * Aggiungere l&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType_Item` all&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType`. Richiama il metodo `Add` dell&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType` e passa l&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType`. Esegui questa operazione per ogni documento PDF di input.

1. Impostare le opzioni di esecuzione.

   * Creare un oggetto `AssemblerOptionSpec` che memorizza le opzioni di esecuzione utilizzando il relativo costruttore.
   * Impostare le opzioni di esecuzione per soddisfare i requisiti aziendali assegnando un valore a un membro dati appartenente all&#39;oggetto `AssemblerOptionSpec`. Ad esempio, per dare istruzioni al servizio Assembler di continuare a elaborare un processo in caso di errore, assegna `false` al membro dati `AssemblerOptionSpec` dell&#39;oggetto `failOnError`.

1. Assembla il portafoglio.

   Richiama il metodo `invokeDDX` dell&#39;oggetto `AssemblerServiceClient` e passa i seguenti valori:

   * Un oggetto `BLOB` che rappresenta il documento DDX
   * L&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType` che contiene i file richiesti
   * Un oggetto `AssemblerOptionSpec` che specifica le opzioni di esecuzione

   Il metodo `invokeDDX` restituisce un oggetto `AssemblerResult` contenente i risultati del processo ed eventuali eccezioni.

1. Salva il portafoglio assemblato.

   Per ottenere il Portfolio PDF appena creato, eseguire le operazioni seguenti:

   * Accedere al campo `documents` dell&#39;oggetto `AssemblerResult`, che è un oggetto `Map` che contiene i documenti PDF risultanti.
   * Iterare attraverso l&#39;oggetto `Map` per ottenere ogni documento risultante. Quindi, eseguire il cast di `value` del membro della matrice su un `BLOB`.
   * Estrarre i dati binari che rappresentano il documento PDF accedendo alla proprietà `MTOM` dell’oggetto `BLOB` corrispondente. Restituisce una matrice di byte che è possibile scrivere in un file PDF.

**Consulta anche**

[Richiamo di AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamo di AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
