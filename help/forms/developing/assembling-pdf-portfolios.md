---
title: Assemblaggio di Portfoli PDF
seo-title: Assembling PDF Portfolios
description: Assemblate un portfolio PDF per combinare diversi documenti di vari tipi, tra cui file Word, file immagine e documenti PDF. Puoi assemblare un portfolio PDF utilizzando un’API Java e un’API di servizio web.
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

**Gli esempi e gli esempi contenuti in questo documento sono solo per l’ambiente AEM Forms su JEE.**

Puoi assemblare un Portfolio PDF utilizzando l’API Assembler Java e del servizio web. Un portfolio può combinare diversi documenti di vari tipi, tra cui file Word, file di immagine (ad esempio, un file jpeg) e documenti PDF. Il layout del portfolio può essere impostato su stili diversi, come *Griglia con anteprima*, il *Su un’immagine* layout o pari *Rivoluzione*.

La figura seguente è una schermata di un portfolio con *Su un’immagine* layout stile.

![ap_ap_portfolio](assets/ap_ap_portfolio.png)

La creazione di un Portfolio PDF rappresenta un&#39;alternativa non cartacea al passaggio di una raccolta di documenti. Utilizzando AEM Forms è possibile creare portfolio richiamando il servizio Assembler con un documento DDX strutturato. Il seguente documento DDX è un esempio di documento DDX che crea un Portfolio di PDF.

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

Il documento DXX deve contenere `Portfolio` con un tag nidificato `Navigator` tag. Prendi nota del tag `<Resource name="navigator/image.xxx" source="myImage.png"/>` è necessario solo se `myNavigator` viene assegnato come navigatore layout onImage: `AdobeOnImage.nav`. Questo tag consente al servizio Assembler di selezionare l’immagine da utilizzare come sfondo del portfolio. Includi `PackageFiles` e `File` tag per definire il nome file e il tipo MIME del file inserito nel pacchetto.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Assembler, vedere [Guida di riferimento dei servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Per ulteriori informazioni su un documento DDX, vedere [Servizio assemblatore e riferimento DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Riepilogo dei passaggi {#summary-of-steps}

Per creare un Portfolio di PDF, effettuare le seguenti operazioni:

1. Includi file di progetto.
1. Creare un client PDF Assembler.
1. Fare riferimento a un documento DDX esistente.
1. Fai riferimento ai documenti richiesti.
1. Impostare le opzioni di runtime.
1. Assembla il portfolio.
1. Salvare il portfolio assemblato.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso della classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è implementato su JBoss)
* jbossall-client.jar (obbligatorio se AEM Forms è distribuito su JBoss)

**Creare un client PDF Assembler**

Prima di eseguire un&#39;operazione Assembler a livello di programmazione, creare un client del servizio Assembler.

**Riferimento a un documento DDX esistente**

Per assemblare un Portfolio di PDF è necessario fare riferimento a un documento DDX. Questo documento DDX deve contenere `Portfolio`, `Navigator` e `PackageFiles` elementi.

**Fai riferimento ai documenti richiesti**

Per assemblare un Portfolio di PDF, fate riferimento a tutti i file che rappresentano i documenti da assemblare. Ad esempio, passare tutti i file di immagine specificati nel documento DDX al servizio Assembler. Si noti che a questi file viene fatto riferimento nel documento DDX specificato in questa sezione: *myImage.png* e *saint_bernard.jpg*.

Durante l&#39;assemblaggio di un Portfolio PDF, passare un file NAV (un file di navigazione) al servizio Assembler. Il file NAV passato al servizio Assembler dipende dal tipo di Portfolio PDF da creare. Ad esempio, per creare un’ *Su un’immagine* , passa il file AdobeOnImage.nav. È possibile individuare i file NAV nella cartella seguente:

`<Install folder>\Acrobat 9.0\Acrobat\Navigators`

Copia il file NAV dalla directory di installazione di Acrobat 9 (o successiva). Posizionare il file NAV in una posizione in cui l&#39;applicazione client possa accedervi. Tutti i file vengono passati al servizio Assembler all&#39;interno di un insieme Map.

>[!NOTE]
>
>Gli avvii rapidi associati all&#39;assemblaggio di Portfoli PDF utilizzano AdobeOnImage.nav.

**Impostare le opzioni di runtime**

È possibile impostare le opzioni di runtime che controllano il comportamento del servizio Assembler durante l&#39;esecuzione di un processo. È ad esempio possibile impostare un&#39;opzione che indichi al servizio Assembler di continuare l&#39;elaborazione di un processo in caso di errore.

**Assemblare il portfolio**

Per assemblare un Portfolio di PDF, chiamare `invokeDDX` operazione. Il servizio Assembler restituisce il Portfolio PDF all&#39;interno di un oggetto insieme.

**Salvare il portfolio assemblato**

Un Portfolio PDF viene restituito all&#39;interno di un insieme. Scorrere l&#39;oggetto insieme e salvare il Portfolio PDF come file PDF.

**Consulta anche**

[Assemblare un Portfolio PDF utilizzando l’API Java](#assemble-a-pdf-portfolio-using-the-java-api)

[Assemblare un Portfolio PDF utilizzando l’API del servizio web](#assemble-a-pdf-portfolio-using-the-web-service-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Assemblaggio di documenti PDF a livello di programmazione](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Assemblare un Portfolio PDF utilizzando l’API Java {#assemble-a-pdf-portfolio-using-the-java-api}

Assemblare un Portfolio PDF utilizzando l&#39;API del servizio Assembler (Java):

1. Includi file di progetto.

   Includi i file JAR client, come adobe-assembler-client.jar, nel percorso di classe del progetto Java.

1. Creare un client PDF Assembler.

   * Creare un `ServiceClientFactory` oggetto che contiene proprietà di connessione.
   * Creare un `AssemblerServiceClient` mediante il costruttore e passando il `ServiceClientFactory` oggetto.

1. Fare riferimento a un documento DDX esistente.

   * Creare un `java.io.FileInputStream` oggetto che rappresenta il documento DDX utilizzando il relativo costruttore e passando un valore stringa che specifica la posizione del file DDX.
   * Creare un `com.adobe.idp.Document` mediante il costruttore e passando il `java.io.FileInputStream` oggetto.

1. Fai riferimento ai documenti richiesti.

   * Creare un `java.util.Map` oggetto utilizzato per memorizzare i documenti di input PDF utilizzando un `HashMap` costruttore.
   * Creare un `java.io.FileInputStream` mediante il costruttore. Passa la posizione del file NAV richiesto (ripeti questa attività per ogni file necessario per creare un portfolio).
   * Creare un `com.adobe.idp.Document` e passare il `java.io.FileInputStream` oggetto contenente il file NAV (ripetere questa operazione per ogni file necessario per creare un portfolio).
   * Aggiungi una voce al `java.util.Map` oggetto richiamando il relativo `put` e fornendo i seguenti argomenti:

      * Valore stringa che rappresenta il nome della chiave. Questo valore deve corrispondere al valore dell&#39;elemento di origine specificato nel documento DDX. (ripeti questa attività per ogni file necessario per creare un portfolio).
      * A `com.adobe.idp.Document` oggetto che contiene il documento PDF. (ripeti questa attività per ogni file necessario per creare un portfolio).

1. Impostare le opzioni di runtime.

   * Creare un `AssemblerOptionSpec` oggetto che memorizza le opzioni di runtime mediante il relativo costruttore.
   * Impostare le opzioni di runtime per soddisfare i requisiti aziendali richiamando un metodo che appartiene al `AssemblerOptionSpec` oggetto. Ad esempio, per indicare al servizio Assembler di continuare l&#39;elaborazione di un processo quando si verifica un errore, richiamare `AssemblerOptionSpec` dell&#39;oggetto `setFailOnError` metodo e passaggio `false`.

1. Assembla il portfolio.

   Richiama `AssemblerServiceClient` dell&#39;oggetto `invokeDDX` e trasmettere i seguenti valori richiesti:

   * A `com.adobe.idp.Document` oggetto che rappresenta il documento DDX da utilizzare
   * A `java.util.Map` oggetto contenente i file necessari per creare un Portfolio PDF.
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` oggetto che specifica le opzioni di runtime, inclusi il tipo di carattere predefinito e il livello di registro del processo

   Il `invokeDDX` il metodo restituisce un `com.adobe.livecycle.assembler.client.AssemblerResult` oggetto che contiene il Portfolio di PDF assemblato ed eventuali eccezioni verificatesi.

1. Salvare il portfolio assemblato.

   Per ottenere il Portfolio PDF, effettuare le seguenti operazioni:

   * Richiama `AssemblerResult` dell&#39;oggetto `getDocuments` metodo. Questo metodo restituisce un `java.util.Map` oggetto.
   * Effettua iterazione attraverso `java.util.Map` finché non viene individuato il risultato `com.adobe.idp.Document` oggetto.
   * Richiama `com.adobe.idp.Document` dell&#39;oggetto `copyToFile` per estrarre il Portfolio PDF.

**Consulta anche**

[Quick Start (modalità SOAP): assemblaggio di Portfoli PDF tramite l’API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-pdf-portfolios-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Assemblare un Portfolio PDF utilizzando l’API del servizio web {#assemble-a-pdf-portfolio-using-the-web-service-api}

Assemblare un Portfolio PDF utilizzando l&#39;API del servizio Assembler (servizio Web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL durante l&#39;impostazione di un riferimento al servizio: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

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
   * Creare un `System.IO.FileStream` richiamando il relativo costruttore e passando un valore stringa che rappresenta la posizione del file del documento DDX e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto della `System.IO.FileStream` oggetto. È possibile determinare le dimensioni della matrice di byte ottenendo `System.IO.FileStream` dell&#39;oggetto `Length` proprietà.
   * Compilare la matrice di byte con i dati di flusso richiamando `System.IO.FileStream` dell&#39;oggetto `Read` metodo. Passare la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare il `BLOB` oggetto assegnando il relativo `MTOM` con il contenuto della matrice di byte.

1. Fai riferimento ai documenti richiesti.

   * Per ogni file di input, crea un `BLOB` mediante il costruttore. Il `BLOB` viene utilizzato per memorizzare il file di input.
   * Creare un `System.IO.FileStream` dell&#39;oggetto richiamando il relativo costruttore e passando un valore stringa che rappresenta la posizione del file di input e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto della `System.IO.FileStream` oggetto. È possibile determinare le dimensioni della matrice di byte ottenendo `System.IO.FileStream` dell&#39;oggetto `Length` proprietà.
   * Compilare la matrice di byte con i dati di flusso richiamando `System.IO.FileStream` dell&#39;oggetto `Read` metodo. Passare la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare il `BLOB` oggetto assegnando il relativo `MTOM` con il contenuto della matrice di byte.
   * Creare un `MyMapOf_xsd_string_To_xsd_anyType` oggetto. Questo oggetto insieme viene utilizzato per memorizzare i file di input necessari per la creazione di un Portfolio di PDF.
   * Per ogni file di input, crea un `MyMapOf_xsd_string_To_xsd_anyType_Item` oggetto.
   * Assegna un valore stringa che rappresenta il nome della chiave al `MyMapOf_xsd_string_To_xsd_anyType_Item` dell&#39;oggetto `key` campo. Questo valore deve corrispondere al valore dell&#39;elemento specificato nel documento DDX. (Eseguire questa operazione per ciascun file di input).
   * Assegna la `BLOB` oggetto che memorizza il file di input in `MyMapOf_xsd_string_To_xsd_anyType_Item` dell&#39;oggetto `value` campo. (Eseguire questa operazione per ogni documento di input PDF).
   * Aggiungi il `MyMapOf_xsd_string_To_xsd_anyType_Item` oggetto al `MyMapOf_xsd_string_To_xsd_anyType` oggetto. Richiama `MyMapOf_xsd_string_To_xsd_anyType` dell&#39;oggetto `Add` e trasmettere il `MyMapOf_xsd_string_To_xsd_anyType` oggetto. (Eseguire questa operazione per ogni documento di input PDF).

1. Impostare le opzioni di runtime.

   * Creare un `AssemblerOptionSpec` oggetto che memorizza le opzioni di runtime mediante il relativo costruttore.
   * Impostare le opzioni di runtime per soddisfare i requisiti aziendali assegnando un valore a un membro dati che appartiene al `AssemblerOptionSpec` oggetto. Ad esempio, per indicare al servizio Assembler di continuare l&#39;elaborazione di un processo quando si verifica un errore, assegnare `false` al `AssemblerOptionSpec` dell&#39;oggetto `failOnError` membro dati.

1. Assembla il portfolio.

   Richiama `AssemblerServiceClient` dell&#39;oggetto `invokeDDX` e trasmettere i seguenti valori:

   * A `BLOB` oggetto che rappresenta il documento DDX
   * Il `MyMapOf_xsd_string_To_xsd_anyType` oggetto contenente i file richiesti
   * Un `AssemblerOptionSpec` oggetto che specifica le opzioni di runtime

   Il `invokeDDX` il metodo restituisce un `AssemblerResult` oggetto contenente i risultati del processo ed eventuali eccezioni verificatesi.

1. Salvare il portfolio assemblato.

   Per ottenere il Portfolio di PDF appena creato, effettuare le seguenti operazioni:

   * Accedere a `AssemblerResult` dell&#39;oggetto `documents` campo, che è un `Map` oggetto contenente i documenti PDF risultanti.
   * Effettua iterazione attraverso `Map` per ottenere ogni documento risultante. Quindi, esegui il cast del membro dell’array `value` a un `BLOB`.
   * Estrarre i dati binari che rappresentano il documento PDF accedendo al relativo `BLOB` dell&#39;oggetto `MTOM` proprietà. Restituisce una matrice di byte che è possibile scrivere in un file PDF.

**Consulta anche**

[Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamare AEM Forms con SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
