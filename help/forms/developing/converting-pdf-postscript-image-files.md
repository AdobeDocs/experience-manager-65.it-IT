---
title: Conversione di file PDF in file Postscript e di immagine
seo-title: Conversione di file PDF in file Postscript e di immagine
description: Utilizzare il servizio Converti PDF per convertire i documenti PDF in PostScript e in diversi formati di immagine (JPEG, JPEG 2000, PNG e TIFF) utilizzando l'API Java e l'API Web Service.
seo-description: Utilizzare il servizio Converti PDF per convertire i documenti PDF in PostScript e in diversi formati di immagine (JPEG, JPEG 2000, PNG e TIFF) utilizzando l'API Java e l'API Web Service.
uuid: 07da0391-7180-4197-aaa6-ae753d753b84
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: f8707752-2c83-461a-b83d-708754b0f3f6
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2847'
ht-degree: 0%

---


# Conversione di file PDF in file Postscript e immagine {#converting-pdf-to-postscript-andimage-files}

**Esempi ed esempi in questo documento sono solo per AEM Forms in ambiente JEE.**

**Informazioni sul servizio Converti PDF**

Il servizio Converti PDF converte i documenti PDF in PostScript e in diversi formati di immagine (JPEG, JPEG 2000, PNG e TIFF). La conversione di un documento PDF in PostScript è utile per la stampa automatica basata su server su qualsiasi stampante PostScript. La conversione di un documento PDF in un file TIFF multipagina è pratica quando si archiviano documenti in sistemi di gestione dei contenuti che non supportano documenti PDF.

È possibile eseguire queste operazioni utilizzando il servizio Converti PDF:

* Converti documenti PDF in PostScript.
* Convertire documenti PDF in formati immagine.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Converti PDF, vedere [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Conversione di documenti PDF in PostScript {#converting-pdf-documents-to-postscript}

In questo argomento viene descritto come utilizzare l’API di servizio Converti PDF (Java e servizio Web) per convertire programmaticamente i documenti PDF in file PostScript. Il documento PDF convertito in file PostScript deve essere un documento PDF non interattivo. In altre parole, se si tenta di convertire un documento PDF interattivo in un file PostScript, viene generata un&#39;eccezione.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Converti PDF, vedere [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary-of-steps}

Per convertire un documento PDF in un file PostScript, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Crea un client di servizio Converti PDF.
1. Fare riferimento al documento PDF per la conversione in un file PostScript.
1. Imposta le opzioni di esecuzione della conversione.
1. Convertire il documento PDF in un file PostScript.
1. Salvare il file PostScript.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

**Creare un client di conversione PDF**

Prima di poter eseguire in modo programmatico un’operazione del servizio Converti PDF, è necessario creare un client di servizio Converti PDF. Se utilizzi l’API Java, crea un oggetto `ConvertPdfServiceClient`. Se utilizzi l’API del servizio Web, crea un oggetto `ConvertPDFServiceService`.

Questa sezione utilizza la funzionalità del servizio Web introdotta in AEM Forms. Per accedere alle nuove funzionalità, è necessario creare l&#39;oggetto proxy utilizzando l&#39;attributo `lc_version` . (Vedere &quot;Accesso a nuove funzionalità tramite i servizi Web&quot; in [Richiamo di AEM Forms tramite i servizi Web](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services).)

**Fare riferimento al documento PDF per la conversione in un file PostScript**

Fare riferimento al documento PDF che si desidera convertire in un file PostScript. Come indicato in precedenza in questo argomento, il documento PDF deve essere un documento PDF non interattivo. Se si tenta di convertire un documento PDF interattivo in un file PostScript, viene generata un&#39;eccezione.

**Impostare le opzioni di esecuzione della conversione**

Durante la conversione di un documento PDF in un file PostScript, è possibile definire le opzioni di esecuzione che specificano il tipo PostScript creato. Ad esempio, è possibile definire un file PostScript di livello 3.

In genere, il file PostScript generato riflette le dimensioni del documento PDF di input. Se si seleziona l&#39;opzione `ShrinkToFit` (che riduce l&#39;output del file PostScript per adattarlo alla pagina), non si vedrà una differenza tra il documento PDF di input e il file PostScript generato. L’opzione `ShrinkToFit` ha effetto solo se si sceglie di stampare su una pagina di dimensioni inferiori rispetto al documento PDF di input. Per selezionare una dimensione di pagina più piccola, definisci l’opzione `PageSize` . Inoltre, si consiglia di impostare l&#39;opzione `RotateAndCenter` su `true` per ottenere l&#39;output PostScript corretto.

Allo stesso modo, se si seleziona l&#39;opzione `ExpandToFit` (che espande l&#39;output del file PostScript per adattarlo alla pagina), l&#39;operazione ha effetto solo se si sceglie di stampare su una pagina di dimensioni maggiori rispetto al documento PDF di input. Per selezionare una dimensione di pagina maggiore, definisci l’opzione `PageSize` . Inoltre, si consiglia di impostare l&#39;opzione `RotateAndCenter` su `true` per ottenere l&#39;output PostScript corretto.

>[!NOTE]
>
>Per informazioni sui valori di esecuzione impostabili, vedere il riferimento alla classe `ToPSOptionsSpec` in [Riferimento API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Convertire il documento PDF in un file PostScript**

Dopo aver creato il client di servizio e impostato le opzioni di esecuzione, è possibile richiamare l&#39;operazione di conversione PostScript. Questa operazione richiede informazioni sul documento da convertire, compreso il livello PostScript preferito per il documento di destinazione.

**Salva il file PostScript**

Dopo aver convertito il documento PDF in PostScript, è possibile salvare l&#39;output come file PostScript.

**Consulta anche**

[Convertire un documento PDF in PS utilizzando l’API Java](converting-pdf-postscript-image-files.md#convert-a-pdf-document-to-ps-using-the-java-api)

[Convertire un documento PDF in PS utilizzando l&#39;API del servizio Web](converting-pdf-postscript-image-files.md#convert-a-pdf-document-to-ps-using-the-web-service-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Guida rapida alla conversione delle API del servizio PDF](/help/forms/developing/convert-pdf-service-java-api.md#convert-pdf-service-java-api-quick-start-soap)

### Convertire un documento PDF in PS utilizzando l&#39;API Java {#convert-a-pdf-document-to-ps-using-the-java-api}

Convertire un documento PDF in PostScript utilizzando l’API di servizio PDF (Java) Converti:

1. Includi file di progetto.

   Includi file JAR client, ad esempio adobe-convertpdf-client.jar, nel percorso di classe del progetto Java.

1. Creare un client Converti PDF.

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `ConvertPdfServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Fare riferimento al documento PDF per la conversione in un file PostScript.

   * Creare un oggetto `java.io.FileInputStream` utilizzando il relativo costruttore e passare un valore stringa che specifichi la posizione del documento PDF da convertire.
   * Creare un oggetto `com.adobe.idp.Document` che memorizza il documento PDF utilizzando il costruttore `com.adobe.idp.Document`. Passa l&#39;oggetto `java.io.FileInputStream` che contiene il documento PDF.

1. Imposta le opzioni di esecuzione della conversione.

   * Creare un oggetto `ToPSOptionsSpec` richiamando il relativo costruttore.
   * Impostare le opzioni di esecuzione richiamando un metodo appropriato appartenente all&#39;oggetto `ToPSOptionsSpec`. Ad esempio, per definire il livello PostScript creato, richiamare il metodo `setPsLevel` dell&#39;oggetto `ToPSOptionsSpec` e passare un valore di enumerazione `PSLevel` che specifica il livello PostScript. Per informazioni su tutti i valori di runtime impostabili, vedere il riferimento alla classe `ToPSOptionsSpec` in [Riferimento API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. Convertire il documento PDF in un file PostScript.

   Richiama il metodo `toPS2` dell&#39;oggetto `ConvertPdfServiceClient`e passa i seguenti valori:

   * Un oggetto `com.adobe.idp.Document` che rappresenta il documento PDF da convertire in un file PostScript.
   * Oggetto `ToPSOptionsSpec` che specifica le opzioni di esecuzione PostScript.

   Il metodo `toPS2` restituisce un oggetto `Document` contenente il nuovo documento PostScript.

1. Salvare il file PostScript.

   * Crea un oggetto `java.io.File` e assicurati che l&#39;estensione del nome file sia .ps.
   * Richiamare il metodo `copyToFile` dell&#39;oggetto `Document` per copiare il contenuto dell&#39;oggetto `Document` nel file (assicurarsi di utilizzare l&#39;oggetto `Document` restituito dal metodo `toPS2`).

**Consulta anche**

[Riepilogo dei passaggi](converting-pdf-postscript-image-files.md#summary-of-steps)

[Avvio rapido (modalità SOAP): Conversione di un documento PDF in PostScript tramite l’API Java](/help/forms/developing/convert-pdf-service-java-api.md#quick-start-soap-mode-converting-a-pdf-document-to-postscript-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Convertire un documento PDF in PS utilizzando l&#39;API del servizio Web {#convert-a-pdf-document-to-ps-using-the-web-service-api}

Convertire un documento PDF in PostScript utilizzando l&#39;API di servizio PDF Convert (servizio Web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurati di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/ConvertPDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Creare un client Converti PDF.

   * Creare un oggetto `ConvertPdfServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `ConvertPdfServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/ConvertPDFService?blob=mtom`). Non è necessario utilizzare l&#39;attributo `lc_version` . Tuttavia, specifica `?blob=mtom`.
   * Crea un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `ConvertPdfServiceClient.Endpoint.Binding` . Imposta il valore restituito su `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegna il nome utente del modulo di AEM al campo `ConvertPdfServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore della password corrispondente al campo `ConvertPdfServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Fare riferimento al documento PDF per la conversione in un file PostScript.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare un documento PDF convertito in un file PostScript.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF da convertire e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni dell&#39;array di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare l’array di byte con i dati del flusso richiamando il metodo `Read` dell’oggetto `System.IO.FileStream` e passando l’array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando il relativo campo `MTOM` con il contenuto dell&#39;array di byte.

1. Imposta le opzioni di esecuzione della conversione.

   * Creare un oggetto `ToPSOptionsSpec` richiamando il relativo costruttore.
   * Impostare le opzioni di esecuzione assegnando un valore al membro dati dell&#39;oggetto `ToPSOptionsSpec`. Ad esempio, per definire il livello PostScript creato, assegnare un valore di enumerazione `PSLevel` al membro dati `ToPSOptionsSpec` dell&#39;oggetto `psLevel`.

1. Convertire il documento PDF in un file PostScript.

   Richiama il metodo `toPS2` dell&#39;oggetto `GeneratePDFServiceService` e passa i seguenti valori:

   * Un oggetto `BLOB` che rappresenta il documento PDF da convertire in un file PostScript
   * Un oggetto `ToPSOptionsSpec` che specifica le opzioni di esecuzione

   Al termine della conversione, estrarre i dati binari che rappresentano il documento PostScript accedendo alla proprietà `BLOB` dell&#39;oggetto `MTOM` corrispondente. Restituisce un array di byte che è possibile scrivere in un file PostScript.

1. Salvare il file PostScript.

   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore. Passa un valore stringa che rappresenta la posizione del file PS.
   * Creare una matrice di byte che memorizza il contenuto dei dati dell&#39;oggetto `BLOB` restituito dal metodo `encryptPDFUsingPassword`. Compilare l’array di byte ottenendo il valore del campo `BLOB` dell’oggetto `MTOM`.
   * Creare un oggetto `System.IO.BinaryWriter` richiamandone il costruttore e passando l&#39;oggetto `System.IO.FileStream`.
   * Scrivere il contenuto dell&#39;array di byte nel file PostScript richiamando il metodo `System.IO.BinaryWriter` dell&#39;oggetto `Write` e passando l&#39;array di byte.

**Consulta anche**

[Riepilogo dei passaggi](converting-pdf-postscript-image-files.md#summary-of-steps)

[Richiamo di AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamo di AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Conversione di documenti PDF in formati immagine {#converting-pdf-documents-to-image-formats}

È possibile utilizzare il servizio Converti PDF per convertire programmaticamente i documenti PDF in formati immagine, quali JPEG, JPEG 2000, TIFF e PNG. Convertendo un documento PDF in un file di immagine, è possibile utilizzare il documento PDF come file di immagine. Ad esempio, è possibile inserire l&#39;immagine in un sistema di gestione dei contenuti aziendali per lo storage.

Durante la conversione di un documento PDF in un’immagine, il servizio Converti PDF crea un’immagine separata per ogni pagina del documento. In altre parole, se il documento ha 20 pagine, il servizio Converti PDF crea 20 file di immagine. Durante la conversione di un documento PDF in un formato immagine, è possibile creare immagini singole per ogni pagina all’interno del documento PDF o un singolo file di immagine per l’intero documento PDF.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Converti PDF, vedere [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-1}

Per convertire un documento PDF in uno qualsiasi dei tipi supportati, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Crea un client di servizio Converti PDF.
1. Recuperare il documento PDF da convertire.
1. Impostare le opzioni di esecuzione.
1. Converti il PDF in un’immagine.
1. Recupera i file immagine da una raccolta.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

**Creare un client di conversione PDF**

Prima di poter eseguire in modo programmatico un’operazione del servizio Converti PDF, è necessario creare un client di servizio Converti PDF. Se utilizzi l’API Java, crea un oggetto `ConvertPdfServiceClient`. Se utilizzi l’API del servizio Web, crea un oggetto `ConvertPDFServiceService`.

**Recupera il documento PDF da convertire**

È necessario recuperare il documento PDF per convertirlo in un’immagine. Non è possibile convertire un documento PDF interattivo in un’immagine. Se tenti di farlo, viene generata un&#39;eccezione. Per convertire un documento PDF interattivo in un file di immagine, è necessario appiattire il documento PDF prima di convertirlo. (Vedere [Flattening dei documenti PDF](/help/forms/developing/creating-document-output-streams.md#flattening-pdf-documents).)

**Impostare le opzioni di esecuzione**

È necessario impostare le opzioni di esecuzione, ad esempio il formato immagine e i valori di risoluzione. Per informazioni sui valori di runtime, consulta il riferimento alla classe `ToImageOptionsSpec` in [Riferimento API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Convertire il PDF in un’immagine**

Dopo aver creato il client di servizio e impostato le opzioni di esecuzione, è possibile convertire il documento PDF in un&#39;immagine. Viene restituito un oggetto raccolta contenente le immagini.

**Recuperare i file immagine da una raccolta**

È possibile recuperare i file immagine da un oggetto raccolta restituito dal servizio Converti PDF. Ogni elemento della raccolta è un&#39;istanza `com.adobe.idp.Document` (o un&#39;istanza `BLOB` se utilizzi i servizi web) che puoi salvare come file di immagine, ad esempio un file JPG.

Il formato del file di immagine dipende dall&#39;opzione `ImageConvertFormat` runtime. In altre parole, se imposti l&#39;opzione `ImageConvertFormat` run-time su `ImageConvertFormat.JPEG`, puoi salvare i file immagine come file JPG.

**Consulta anche**

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Guida rapida alla conversione delle API del servizio PDF](/help/forms/developing/convert-pdf-service-java-api.md#convert-pdf-service-java-api-quick-start-soap)

### Convertire un documento PDF in file di immagini utilizzando l&#39;API Java {#convert-a-pdf-document-to-image-files-using-the-java-api}

Convertire un documento PDF in un formato immagine utilizzando l’API del servizio Converti PDF (Java):

1. Includi file di progetto.

   Includi file JAR client, ad esempio adobe-convertpdf-client.jar, nel percorso di classe del progetto Java.

1. Creare un client Converti PDF.

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `ConvertPdfServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Recuperare il documento PDF da convertire.

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento PDF da convertire utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del documento PDF.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Impostare le opzioni di esecuzione.

   * Creare un oggetto `ToImageOptionsSpec` utilizzando il relativo costruttore.
   * Richiama i metodi che appartengono a questo oggetto come richiesto. Ad esempio, imposta il tipo di immagine richiamando il metodo `setImageConvertFormat` e passando un valore di enum `ImageConvertFormat` che specifica il tipo di formato.

   >[!NOTE]
   >
   >L&#39;impostazione del valore di enumerazione `ImageConvertFormat` è obbligatoria.

1. Converti il PDF in un’immagine.

   Richiama il metodo `toImage2` dell&#39;oggetto `ConvertPdfServiceClient` e passa i seguenti valori:

   * Un oggetto `com.adobe.idp.Document` che rappresenta il file PDF da convertire.
   * Un oggetto `com.adobe.livecycle.converpdfservice.client.ToImageOptionsSpec` che contiene le varie preferenze relative al formato immagine di destinazione.

   Il metodo `toImage2` restituisce un oggetto `java.util.List` che contiene immagini. Ogni elemento della raccolta è un&#39;istanza `com.adobe.idp.Document`.

1. Recupera i file immagine da una raccolta.

   Itera attraverso l&#39;oggetto `java.util.List` per determinare se le immagini sono presenti. Ogni elemento è un&#39;istanza `com.adobe.idp.Document`. Salvare l’immagine richiamando il metodo `copyToFile` dell’oggetto `java.io.File` e passando un oggetto `com.adobe.idp.Document`.

**Consulta anche**

[Avvio rapido (modalità SOAP): Conversione di un documento PDF in file JPEG utilizzando l’API Java](/help/forms/developing/convert-pdf-service-java-api.md#quick-start-soap-mode-converting-a-pdf-document-to-jpeg-files-using-the-java-api)

### Convertire un documento PDF in file di immagini utilizzando l&#39;API del servizio Web {#convert-a-pdf-document-to-image-files-using-the-web-service-api}

Convertire un documento PDF in un formato immagine utilizzando l’API del servizio PDF Converti (servizio Web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurati di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/ConvertPDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Crea un client PDF convertito.

   * Creare un oggetto `ConvertPdfServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `ConvertPdfServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/ConvertPDFService?blob=mtom`). Non è necessario utilizzare l&#39;attributo `lc_version` . Tuttavia, specifica `?blob=mtom`.
   * Crea un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `ConvertPdfServiceClient.Endpoint.Binding` . Imposta il valore restituito su `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegna il nome utente del modulo di AEM al campo `ConvertPdfServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore della password corrispondente al campo `ConvertPdfServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recuperare il documento PDF da convertire.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. Questo oggetto `BLOB` viene utilizzato per memorizzare il modulo PDF.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore. Passare un valore stringa che specifichi la posizione del modulo PDF e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. Determina le dimensioni dell&#39;array di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare l’array di byte con i dati del flusso richiamando il metodo `Read` dell’oggetto `System.IO.FileStream`. Passa la matrice dei byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando il relativo campo `MTOM` con il contenuto dell&#39;array di byte.

1. Impostare le opzioni di esecuzione.

   * Creare un oggetto `ToImageOptionsSpec` utilizzando il relativo costruttore.
   * Richiama i metodi che appartengono a questo oggetto come richiesto. Ad esempio, imposta il tipo di immagine richiamando il metodo `setImageConvertFormat` e passando un valore di enumerazione `ImageConvertFormat` che specifica il tipo di formato.

   >[!NOTE]
   >
   >L&#39;impostazione del valore di enumerazione `ImageConvertFormat` è obbligatoria.

1. Converti il PDF in un’immagine.

   Richiama il metodo `toImage2` dell&#39;oggetto `ConvertPDFServiceService` e passa i seguenti valori:

   * Un oggetto `BLOB` che rappresenta il file da convertire
   * Un oggetto `ToImageOptionsSpec` che contiene le varie preferenze relative al formato immagine di destinazione

   Il metodo `toImage2` restituisce un oggetto `MyArrayOfBLOB` contenente i file di immagine appena creati.

1. Recupera i file immagine da una raccolta.

   * Determinare il numero di elementi nell&#39;oggetto `MyArrayOfBLOB` ottenendo il valore del relativo campo `Count`. Ogni elemento è un oggetto `BLOB` che contiene l&#39;immagine.
   * Itera attraverso l&#39;oggetto `MyArrayOfBLOB` e salva ogni file di immagine.

**Consulta anche**

[Richiamo di AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamo di AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
