---
title: Conversione di PDF in file PostScript e immagine
seo-title: Conversione di PDF in file PostScript e immagine
description: Il servizio Converti PDF consente di convertire i documenti PDF in PostScript e in diversi formati di immagine (JPEG, JPEG 2000, PNG e TIFF) mediante l'API Java e l'API del servizio Web.
seo-description: Il servizio Converti PDF consente di convertire i documenti PDF in PostScript e in diversi formati di immagine (JPEG, JPEG 2000, PNG e TIFF) mediante l'API Java e l'API del servizio Web.
uuid: 07da0391-7180-4197-aaa6-ae753d753b84
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: f8707752-2c83-461a-b83d-708754b0f3f6
translation-type: tm+mt
source-git-commit: 07889ead2ae402b5fb738ca08c7efe076ef33e44
workflow-type: tm+mt
source-wordcount: '2832'
ht-degree: 0%

---


# Conversione da PDF a Postscript e file immagine {#converting-pdf-to-postscript-andimage-files}

**Informazioni sul servizio Converti PDF**

Il servizio Converti PDF converte i documenti PDF in PostScript e in diversi formati di immagine (JPEG, JPEG 2000, PNG e TIFF). La conversione di un documento PDF in PostScript è utile per la stampa automatica basata su server su qualsiasi stampante PostScript. La conversione di un documento PDF in un file TIFF multipagina è pratica quando si archiviano documenti in sistemi di gestione del contenuto che non supportano documenti PDF.

È possibile eseguire le operazioni seguenti utilizzando il servizio Converti PDF:

* Convertire i documenti PDF in PostScript.
* Convertire i documenti PDF in formati immagine.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Converti PDF, vedere [Guida di riferimento dei servizi per  AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Conversione di documenti PDF in PostScript {#converting-pdf-documents-to-postscript}

Questo argomento descrive come utilizzare l&#39;API Convert PDF Service (Java e il servizio Web) per convertire i documenti PDF in file PostScript a livello di programmazione. Il documento PDF convertito in file PostScript deve essere un documento PDF non interattivo. Se si tenta di convertire un documento PDF interattivo in un file PostScript, viene generata un&#39;eccezione.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Converti PDF, vedere [Guida di riferimento dei servizi per  AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary-of-steps}

Per convertire un documento PDF in un file PostScript, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un client di servizi Converti PDF.
1. Fare riferimento al documento PDF per la conversione in file PostScript.
1. Impostare le opzioni di esecuzione della conversione.
1. Convertire il documento PDF in un file PostScript.
1. Salvare il file PostScript.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, accertatevi di includere i file proxy.

**Creare un client Converti PDF**

Prima di eseguire un&#39;operazione di servizio Converti PDF a livello di programmazione, è necessario creare un client di servizi Converti PDF. Se utilizzate l&#39;API Java, create un oggetto `ConvertPdfServiceClient`. Se utilizzate l&#39;API del servizio Web, create un oggetto `ConvertPDFServiceService`.

In questa sezione viene utilizzata la funzionalità del servizio Web introdotta in  AEM Forms. Per accedere alle nuove funzionalità, è necessario creare l&#39;oggetto proxy utilizzando l&#39;attributo `lc_version`. (Vedere &quot;Accesso a nuove funzionalità tramite servizi Web&quot; in [Chiamata  AEM Forms tramite servizi Web](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services).)

**Fare riferimento al documento PDF per la conversione in file PostScript**

Fare riferimento al documento PDF da convertire in file PostScript. Come indicato in precedenza in questo argomento, il documento PDF deve essere un documento PDF non interattivo. Se si tenta di convertire un documento PDF interattivo in un file PostScript, viene generata un&#39;eccezione.

**Impostazione delle opzioni di esecuzione della conversione**

Quando si converte un documento PDF in un file PostScript, è possibile definire opzioni di esecuzione che specificano il tipo PostScript creato. Ad esempio, è possibile definire un file PostScript di livello 3.

In genere, il file PostScript generato riflette le dimensioni del documento PDF di input. Se si seleziona l&#39;opzione `ShrinkToFit` (che riduce l&#39;output del file PostScript per adattarlo alla pagina), non si verificherà alcuna differenza tra il documento PDF di input e il file PostScript generato. L&#39;opzione `ShrinkToFit` ha effetto solo se si seleziona la stampa su una dimensione di pagina inferiore rispetto al documento PDF di input. Per selezionare una dimensione di pagina più piccola, definite l&#39;opzione `PageSize`. Inoltre, si consiglia di impostare l&#39;opzione `RotateAndCenter` su `true` per ottenere l&#39;output PostScript corretto.

Analogamente, se si seleziona l&#39;opzione `ExpandToFit` (che espande l&#39;output del file PostScript per adattarlo alla pagina), l&#39;operazione ha effetto solo se si seleziona la stampa su una pagina di dimensioni maggiori rispetto al documento PDF di input. Per selezionare una dimensione di pagina più grande, definite l&#39;opzione `PageSize`. Inoltre, si consiglia di impostare l&#39;opzione `RotateAndCenter` su `true` per ottenere l&#39;output PostScript corretto.

>[!NOTE]
>
>Per informazioni sui valori di runtime che è possibile impostare, vedere il riferimento di classe `ToPSOptionsSpec` in [ Guida di riferimento delle API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Conversione del documento PDF in un file PostScript**

Dopo aver creato il client del servizio e impostato le opzioni di esecuzione, è possibile richiamare l&#39;operazione di conversione PostScript. Questa operazione richiede informazioni sul documento da convertire, compreso il livello PostScript preferito per il documento di destinazione.

**Salvare il file PostScript**

Dopo aver convertito il documento PDF in PostScript, è possibile salvare l&#39;output come file PostScript.

**Consulta anche**

[Conversione di un documento PDF in PS tramite l&#39;API Java](converting-pdf-postscript-image-files.md#convert-a-pdf-document-to-ps-using-the-java-api)

[Conversione di un documento PDF in PS tramite l&#39;API del servizio Web](converting-pdf-postscript-image-files.md#convert-a-pdf-document-to-ps-using-the-web-service-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Converti API servizio PDF - Avvio rapido](/help/forms/developing/convert-pdf-service-java-api.md#convert-pdf-service-java-api-quick-start-soap)

### Convertire un documento PDF in PS utilizzando l&#39;API Java {#convert-a-pdf-document-to-ps-using-the-java-api}

Convertire un documento PDF in PostScript utilizzando l&#39;API Convert PDF Service (Java):

1. Includere i file di progetto.

   Includete file JAR client, ad esempio adobe-convertpdf-client.jar, nel percorso di classe del progetto Java.

1. Creare un client Converti PDF.

   * Creare un oggetto `ServiceClientFactory` che contiene le proprietà di connessione.
   * Creare un oggetto `ConvertPdfServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Fare riferimento al documento PDF per la conversione in file PostScript.

   * Creare un oggetto `java.io.FileInputStream` utilizzando il relativo costruttore e passare un valore di stringa che specifica la posizione del documento PDF da convertire.
   * Creare un oggetto `com.adobe.idp.Document` che memorizza il documento PDF utilizzando il costruttore `com.adobe.idp.Document`. Passa l&#39;oggetto `java.io.FileInputStream` che contiene il documento PDF.

1. Impostare le opzioni di esecuzione della conversione.

   * Creare un oggetto `ToPSOptionsSpec` richiamandone il costruttore.
   * Impostare le opzioni di esecuzione richiamando un metodo appropriato che appartiene all&#39;oggetto `ToPSOptionsSpec`. Ad esempio, per definire il livello PostScript creato, richiamare il metodo `ToPSOptionsSpec` dell&#39;oggetto `setPsLevel` e passare un valore di enumerazione &lt;a2/> che specifica il livello PostScript. `PSLevel` Per informazioni su tutti i valori di runtime che è possibile impostare, vedere il riferimento di classe `ToPSOptionsSpec` in [ Guida di riferimento delle API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. Convertire il documento PDF in un file PostScript.

   Richiamare il metodo `ConvertPdfServiceClient`dell&#39;oggetto `toPS2` e trasmettere i valori seguenti:

   * Un oggetto `com.adobe.idp.Document` che rappresenta il documento PDF da convertire in file PostScript.
   * Un oggetto `ToPSOptionsSpec` che specifica le opzioni di esecuzione PostScript.

   Il metodo `toPS2` restituisce un oggetto `Document` che contiene il nuovo documento PostScript.

1. Salvare il file PostScript.

   * Create un oggetto `java.io.File` e accertatevi che l&#39;estensione del nome del file sia .ps.
   * Richiamare il metodo `Document` dell&#39;oggetto `copyToFile` per copiare nel file il contenuto dell&#39;oggetto `Document` (assicurarsi di utilizzare l&#39;oggetto `Document` restituito dal metodo `toPS2`).

**Consulta anche**

[Riepilogo dei passaggi](converting-pdf-postscript-image-files.md#summary-of-steps)

[Avvio rapido (modalità SOAP): Conversione di un documento PDF in PostScript tramite l&#39;API Java](/help/forms/developing/convert-pdf-service-java-api.md#quick-start-soap-mode-converting-a-pdf-document-to-postscript-using-the-java-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Convertire un documento PDF in PS utilizzando l&#39;API del servizio Web {#convert-a-pdf-document-to-ps-using-the-web-service-api}

Convertire un documento PDF in PostScript utilizzando l&#39;API Convert PDF Service (servizio Web):

1. Includere i file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/ConvertPDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituire `localhost` con l&#39;indirizzo IP del server che ospita  AEM Forms.

1. Creare un client Converti PDF.

   * Creare un oggetto `ConvertPdfServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `ConvertPdfServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passate un valore di stringa che specifica il WSDL al servizio AEM Forms  (ad esempio, `http://localhost:8080/soap/services/ConvertPDFService?blob=mtom`). Non è necessario utilizzare l&#39;attributo `lc_version`. Tuttavia, specificate `?blob=mtom`.
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `ConvertPdfServiceClient.Endpoint.Binding`. Inserite il valore restituito in `BasicHttpBinding`.
   * Impostare il campo `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto `MessageEncoding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilitate l&#39;autenticazione HTTP di base eseguendo le seguenti operazioni:

      * Assegnare il nome utente del modulo AEM al campo `ConvertPdfServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `ConvertPdfServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Fare riferimento al documento PDF per la conversione in file PostScript.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare un documento PDF convertito in un file PostScript.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF da convertire e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà `System.IO.FileStream` dell&#39;oggetto `Length`.
   * Compilare l&#39;array di byte con i dati del flusso richiamando il metodo `Read` dell&#39;oggetto `System.IO.FileStream` e passando l&#39;array di byte, la posizione iniziale e la lunghezza del flusso per la lettura.
   * Compilare l&#39;oggetto `BLOB` assegnando il relativo campo `MTOM` con il contenuto dell&#39;array di byte.

1. Impostare le opzioni di esecuzione della conversione.

   * Creare un oggetto `ToPSOptionsSpec` richiamandone il costruttore.
   * Impostare le opzioni di esecuzione assegnando un valore al membro dati dell&#39;oggetto `ToPSOptionsSpec`. Ad esempio, per definire il livello PostScript creato, assegnare un valore di enumerazione `PSLevel` al membro di dati `ToPSOptionsSpec` dell&#39;oggetto `psLevel`.

1. Convertire il documento PDF in un file PostScript.

   Richiamare il metodo `GeneratePDFServiceService` dell&#39;oggetto `toPS2` e trasmettere i seguenti valori:

   * Un oggetto `BLOB` che rappresenta il documento PDF da convertire in file PostScript
   * Un oggetto `ToPSOptionsSpec` che specifica le opzioni di esecuzione

   Al termine della conversione, estrarre i dati binari che rappresentano il documento PostScript accedendo alla proprietà `BLOB` dell&#39;oggetto `MTOM`. Questo restituisce un array di byte che è possibile scrivere in un file PostScript.

1. Salvare il file PostScript.

   * Creare un oggetto `System.IO.FileStream` richiamandone il costruttore. Passate un valore di stringa che rappresenta la posizione del file PS.
   * Creare un array di byte che memorizza il contenuto dei dati dell&#39;oggetto `BLOB` restituito dal metodo `encryptPDFUsingPassword`. Compilare l&#39;array di byte ottenendo il valore del campo `BLOB` dell&#39;oggetto `MTOM`.
   * Creare un oggetto `System.IO.BinaryWriter` richiamandone il costruttore e passando l&#39;oggetto `System.IO.FileStream`.
   * Scrivere il contenuto dell&#39;array di byte nel file PostScript richiamando il metodo `System.IO.BinaryWriter` dell&#39;oggetto `Write` e passando l&#39;array di byte.

**Consulta anche**

[Riepilogo dei passaggi](converting-pdf-postscript-image-files.md#summary-of-steps)

[Chiamata  AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chiamata  AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Conversione di documenti PDF in formati immagine {#converting-pdf-documents-to-image-formats}

È possibile utilizzare il servizio Converti PDF per convertire in modo programmatico i documenti PDF in formati immagine, quali JPEG, JPEG 2000, TIFF e PNG. Convertendo un documento PDF in un file immagine, è possibile utilizzare il documento PDF come file immagine. Ad esempio, potete inserire l&#39;immagine in un sistema di gestione del contenuto aziendale per l&#39;archiviazione.

Durante la conversione di un documento PDF in un&#39;immagine, il servizio Converti PDF crea un&#39;immagine separata per ogni pagina del documento. Se il documento ha 20 pagine, il servizio Converti PDF crea 20 file di immagine. Durante la conversione di un documento PDF in un formato immagine, è possibile creare immagini singole per ciascuna pagina del documento PDF o un singolo file di immagine per l&#39;intero documento PDF.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Converti PDF, vedere [Guida di riferimento dei servizi per  AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-1}

Per convertire un documento PDF in uno dei tipi supportati, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un client di servizi Converti PDF.
1. Recuperare il documento PDF da convertire.
1. Impostare le opzioni di esecuzione.
1. Convertire il PDF in un’immagine.
1. Recuperate i file immagine da una raccolta.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, accertatevi di includere i file proxy.

**Creare un client Converti PDF**

Prima di eseguire un&#39;operazione di servizio Converti PDF a livello di programmazione, è necessario creare un client di servizi Converti PDF. Se utilizzate l&#39;API Java, create un oggetto `ConvertPdfServiceClient`. Se utilizzate l&#39;API del servizio Web, create un oggetto `ConvertPDFServiceService`.

**Recuperare il documento PDF da convertire**

Per convertire un’immagine è necessario recuperare il documento PDF. Non è possibile convertire un documento PDF interattivo in un’immagine. Se tentate di farlo, viene generata un&#39;eccezione. Per convertire un documento PDF interattivo in un file immagine, è necessario appiattire il documento PDF prima di convertirlo. (Vedere [Appiattimento dei documenti PDF](/help/forms/developing/creating-document-output-streams.md#flattening-pdf-documents).)

**Impostazione delle opzioni di esecuzione**

È necessario impostare le opzioni di esecuzione, ad esempio il formato immagine e i valori di risoluzione. Per informazioni sui valori di runtime, vedere il riferimento di classe `ToImageOptionsSpec` in [ Guida di riferimento delle API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Conversione del PDF in un’immagine**

Dopo aver creato il client del servizio e impostato le opzioni di esecuzione, è possibile convertire il documento PDF in un&#39;immagine. Viene restituito un oggetto raccolta che contiene le immagini.

**Recuperare i file di immagine da una raccolta**

È possibile recuperare i file immagine da un oggetto raccolta restituito dal servizio Converti PDF. Ciascun elemento della raccolta è un&#39;istanza `com.adobe.idp.Document` (o un&#39;istanza `BLOB` se si utilizzano i servizi Web) che è possibile salvare come file di immagine, ad esempio un file JPG.

Il formato del file di immagine dipende dall&#39;opzione `ImageConvertFormat` di runtime. Se si imposta l&#39;opzione `ImageConvertFormat` runtime su `ImageConvertFormat.JPEG`, è possibile salvare i file immagine come file JPG.

**Consulta anche**

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Converti API servizio PDF - Avvio rapido](/help/forms/developing/convert-pdf-service-java-api.md#convert-pdf-service-java-api-quick-start-soap)

### Conversione di un documento PDF in file di immagine mediante l&#39;API Java {#convert-a-pdf-document-to-image-files-using-the-java-api}

Convertire un documento PDF in un formato immagine utilizzando l&#39;API del servizio Converti PDF (Java):

1. Includere i file di progetto.

   Includete file JAR client, ad esempio adobe-convertpdf-client.jar, nel percorso di classe del progetto Java.

1. Creare un client Converti PDF.

   * Creare un oggetto `ServiceClientFactory` che contiene le proprietà di connessione.
   * Creare un oggetto `ConvertPdfServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Recuperare il documento PDF da convertire.

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento PDF da convertire utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del documento PDF.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Impostare le opzioni di esecuzione.

   * Creare un oggetto `ToImageOptionsSpec` utilizzando il relativo costruttore.
   * Richiama i metodi che appartengono a questo oggetto come richiesto. Ad esempio, impostare il tipo di immagine richiamando il metodo `setImageConvertFormat` e passando un valore enum `ImageConvertFormat` che specifica il tipo di formato.

   >[!NOTE]
   >
   >L&#39;impostazione del valore di enumerazione `ImageConvertFormat` è obbligatoria.

1. Convertire il PDF in un’immagine.

   Richiamare il metodo `ConvertPdfServiceClient` dell&#39;oggetto `toImage2` e trasmettere i seguenti valori:

   * Un oggetto `com.adobe.idp.Document` che rappresenta il file PDF da convertire.
   * Un oggetto `com.adobe.livecycle.converpdfservice.client.ToImageOptionsSpec` che contiene le varie preferenze relative al formato immagine di destinazione.

   Il metodo `toImage2` restituisce un oggetto `java.util.List` che contiene immagini. Ciascun elemento della raccolta è un&#39;istanza `com.adobe.idp.Document`.

1. Recuperate i file immagine da una raccolta.

   Iterate l&#39;oggetto `java.util.List` per determinare se le immagini sono presenti. Ogni elemento è un&#39;istanza `com.adobe.idp.Document`. Salvate l&#39;immagine richiamando il metodo `com.adobe.idp.Document` dell&#39;oggetto `copyToFile` e passando un oggetto &lt;a2/>.`java.io.File`

**Consulta anche**

[Avvio rapido (modalità SOAP): Conversione di un documento PDF in file JPEG mediante l&#39;API Java](/help/forms/developing/convert-pdf-service-java-api.md#quick-start-soap-mode-converting-a-pdf-document-to-jpeg-files-using-the-java-api)

### Conversione di un documento PDF in file immagine mediante l&#39;API del servizio Web {#convert-a-pdf-document-to-image-files-using-the-web-service-api}

Convertire un documento PDF in un formato immagine utilizzando l&#39;API di servizio PDF Convert (servizio Web):

1. Includere i file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/ConvertPDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituire `localhost` con l&#39;indirizzo IP del server che ospita  AEM Forms.

1. Creare un client PDF convertito.

   * Creare un oggetto `ConvertPdfServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `ConvertPdfServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passate un valore di stringa che specifica il WSDL al servizio AEM Forms  (ad esempio, `http://localhost:8080/soap/services/ConvertPDFService?blob=mtom`). Non è necessario utilizzare l&#39;attributo `lc_version`. Tuttavia, specificate `?blob=mtom`.
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `ConvertPdfServiceClient.Endpoint.Binding`. Inserite il valore restituito in `BasicHttpBinding`.
   * Impostare il campo `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto `MessageEncoding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilitate l&#39;autenticazione HTTP di base eseguendo le seguenti operazioni:

      * Assegnare il nome utente del modulo AEM al campo `ConvertPdfServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `ConvertPdfServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recuperare il documento PDF da convertire.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. Questo oggetto `BLOB` viene utilizzato per memorizzare il modulo PDF.
   * Creare un oggetto `System.IO.FileStream` richiamandone il costruttore. Passa un valore di stringa che specifica la posizione del modulo PDF e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. Determinare la dimensione dell&#39;array di byte ottenendo la proprietà `System.IO.FileStream` dell&#39;oggetto `Length`.
   * Compilare l&#39;array di byte con i dati del flusso richiamando il metodo `System.IO.FileStream` dell&#39;oggetto `Read`. Passare l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando il relativo campo `MTOM` con il contenuto dell&#39;array di byte.

1. Impostare le opzioni di esecuzione.

   * Creare un oggetto `ToImageOptionsSpec` utilizzando il relativo costruttore.
   * Richiama i metodi che appartengono a questo oggetto come richiesto. Ad esempio, impostare il tipo di immagine richiamando il metodo `setImageConvertFormat` e passando un valore di enumerazione `ImageConvertFormat` che specifica il tipo di formato.

   >[!NOTE]
   >
   >L&#39;impostazione del valore di enumerazione `ImageConvertFormat` è obbligatoria.

1. Convertire il PDF in un’immagine.

   Richiamare il metodo `ConvertPDFServiceService` dell&#39;oggetto `toImage2` e trasmettere i seguenti valori:

   * Un oggetto `BLOB` che rappresenta il file da convertire
   * Un oggetto `ToImageOptionsSpec` che contiene le varie preferenze relative al formato immagine di destinazione

   Il metodo `toImage2` restituisce un oggetto `MyArrayOfBLOB` che contiene i file immagine appena creati.

1. Recuperate i file immagine da una raccolta.

   * Determinare il numero di elementi nell&#39;oggetto `MyArrayOfBLOB` ottenendo il valore del relativo campo `Count`. Ogni elemento è un oggetto `BLOB` che contiene l&#39;immagine.
   * Iterate l&#39;oggetto `MyArrayOfBLOB` e salvate ciascun file immagine.

**Consulta anche**

[Chiamata  AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chiamata  AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
