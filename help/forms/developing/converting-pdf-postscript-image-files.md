---
title: Conversione di PDF in file Postscript e Image
seo-title: Converting PDF to Postscript andImage Files
description: Utilizza il servizio Convert PDF per convertire i documenti PDF in formato PostScript e in diversi formati di immagine (JPEG, JPEG 2000, PNG e TIFF) utilizzando l’API Java e l’API Web Service.
seo-description: Use the Convert PDF service to convert PDF documents to PostScript and to a number of image formats (JPEG, JPEG 2000, PNG, and TIFF) using the Java API and Web Service API.
uuid: 07da0391-7180-4197-aaa6-ae753d753b84
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: f8707752-2c83-461a-b83d-708754b0f3f6
role: Developer
exl-id: 31730c24-46c3-4111-9391-ccd4342740e9
source-git-commit: 135f50cc80f8bb449b2f1621db5e2564f5075968
workflow-type: tm+mt
source-wordcount: '2809'
ht-degree: 0%

---

# Conversione di PDF in file Postscript e di immagine {#converting-pdf-to-postscript-andimage-files}

**Esempi ed esempi in questo documento sono solo per AEM Forms in ambiente JEE.**

**Informazioni sul servizio Converti PDF**

Il servizio Convert PDF converte i documenti PDF in formato PostScript e in diversi formati immagine (JPEG, JPEG 2000, PNG e TIFF). La conversione di un documento PDF in PostScript è utile per la stampa automatica basata su server su qualsiasi stampante PostScript. La conversione di un documento PDF in un file TIFF multipagina è pratica quando si archiviano documenti in sistemi di gestione dei contenuti che non supportano documenti PDF.

Puoi eseguire queste attività utilizzando il servizio Convert PDF:

* Convertire documenti PDF in PostScript.
* Convertire i documenti PDF in formati immagine.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Convert PDF, consulta [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Conversione di documenti PDF in PostScript {#converting-pdf-documents-to-postscript}

In questo argomento viene descritto come utilizzare l’API di Convert PDF Service (Java e servizio Web) per convertire programmaticamente i documenti PDF in file PostScript. Il documento PDF convertito in file PostScript deve essere un documento PDF non interattivo. In altre parole, se si tenta di convertire un documento PDF interattivo in un file PostScript, viene generata un&#39;eccezione.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Convert PDF, consulta [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary-of-steps}

Per convertire un documento PDF in un file PostScript, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Creare un client di servizio Convert PDF.
1. Fare riferimento al documento PDF per la conversione in un file PostScript.
1. Imposta le opzioni di esecuzione della conversione.
1. Convertire il documento PDF in un file PostScript.
1. Salvare il file PostScript.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

**Creare un client Convert PDF**

Prima di poter eseguire in modo programmatico un’operazione del servizio Convert PDF, è necessario creare un client di servizio Convert PDF. Se utilizzi l’API Java, crea un `ConvertPdfServiceClient` oggetto. Se utilizzi l’API del servizio Web, crea un `ConvertPDFServiceService` oggetto.

Questa sezione utilizza la funzionalità del servizio Web introdotta in AEM Forms. Per accedere alle nuove funzionalità, è necessario creare l&#39;oggetto proxy utilizzando `lc_version` attributo. (Consultare &quot;Accesso a nuove funzionalità tramite i servizi web&quot; in [Richiamo di AEM Forms tramite i servizi web](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services).)

**Fare riferimento al documento PDF per la conversione in un file PostScript**

Fare riferimento al documento PDF che si desidera convertire in un file PostScript. Come indicato in precedenza in questo argomento, il documento PDF deve essere un documento PDF non interattivo. Se si tenta di convertire un documento PDF interattivo in un file PostScript, viene generata un&#39;eccezione.

**Impostare le opzioni di esecuzione della conversione**

Durante la conversione di un documento PDF in un file PostScript, è possibile definire opzioni di esecuzione che specificano il tipo PostScript creato. Ad esempio, è possibile definire un file PostScript di livello 3.

In genere, il file PostScript generato riflette le dimensioni del documento di input PDF. Se selezioni la `ShrinkToFit` (che riduce l&#39;output del file PostScript per adattarlo alla pagina), non si vedrà una differenza tra il documento di input PDF e il file PostScript generato. La `ShrinkToFit` l’opzione ha effetto solo se si sceglie di stampare su una pagina di dimensioni inferiori rispetto al documento di input PDF. Per selezionare una dimensione di pagina più piccola, definisci la `PageSize` opzione . Inoltre, è consigliabile impostare la variabile `RotateAndCenter` opzione per `true` per ottenere l&#39;output PostScript corretto.

Allo stesso modo, se selezioni la `ExpandToFit` (che espande l&#39;output del file PostScript per adattarlo alla pagina), ha effetto solo se si sceglie di stampare su una pagina di dimensioni maggiori rispetto al documento di input PDF. Per selezionare una dimensione di pagina più grande, definisci la `PageSize` opzione . Inoltre, è consigliabile impostare la variabile `RotateAndCenter` opzione per `true` per ottenere l&#39;output PostScript corretto.

>[!NOTE]
>
>Per informazioni sui valori di esecuzione impostabili, vedere la `ToPSOptionsSpec` riferimento di classe in [Riferimento API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Convertire il documento PDF in un file PostScript**

Dopo aver creato il client di servizio e impostato le opzioni di esecuzione, è possibile richiamare l&#39;operazione di conversione PostScript. Questa operazione richiede informazioni sul documento da convertire, compreso il livello PostScript preferito per il documento di destinazione.

**Salva il file PostScript**

Dopo aver convertito il documento PDF in PostScript, è possibile salvare l&#39;output come file PostScript.

**Consulta anche**

[Convertire un documento PDF in PS utilizzando l’API Java](converting-pdf-postscript-image-files.md#convert-a-pdf-document-to-ps-using-the-java-api)

[Convertire un documento PDF in PS utilizzando l’API del servizio Web](converting-pdf-postscript-image-files.md#convert-a-pdf-document-to-ps-using-the-web-service-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido dell’API per la conversione di PDF Service](/help/forms/developing/convert-pdf-service-java-api.md#convert-pdf-service-java-api-quick-start-soap)

### Convertire un documento PDF in PS utilizzando l’API Java {#convert-a-pdf-document-to-ps-using-the-java-api}

Convertire un documento PDF in PostScript utilizzando l’API Convert PDF Service (Java):

1. Includi file di progetto.

   Includi file JAR client, ad esempio adobe-convertpdf-client.jar, nel percorso di classe del progetto Java.

1. Creare un client Convert PDF.

   * Crea un `ServiceClientFactory` oggetto contenente le proprietà di connessione.
   * Crea un `ConvertPdfServiceClient` utilizzando il relativo costruttore e passando `ServiceClientFactory` oggetto.

1. Fare riferimento al documento PDF per la conversione in un file PostScript.

   * Crea un `java.io.FileInputStream` utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del documento PDF da convertire.
   * Crea un `com.adobe.idp.Document` oggetto che memorizza il documento PDF utilizzando `com.adobe.idp.Document` costruttore. Passa la `java.io.FileInputStream` oggetto contenente il documento PDF.

1. Imposta le opzioni di esecuzione della conversione.

   * Crea un `ToPSOptionsSpec` richiamando il relativo costruttore.
   * Imposta le opzioni di esecuzione richiamando un metodo appropriato che appartiene al `ToPSOptionsSpec` oggetto. Ad esempio, per definire il livello PostScript creato, richiamare la `ToPSOptionsSpec` dell’oggetto `setPsLevel` e passare un `PSLevel` valore di enumerazione che specifica il livello PostScript. Per informazioni su tutti i valori di runtime che è possibile impostare, vedere la `ToPSOptionsSpec` riferimento di classe in [Riferimento API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. Convertire il documento PDF in un file PostScript.

   Richiama il `ConvertPdfServiceClient`dell’oggetto `toPS2` e passare i seguenti valori:

   * A `com.adobe.idp.Document` oggetto che rappresenta il documento PDF da convertire in un file PostScript.
   * A `ToPSOptionsSpec` oggetto che specifica le opzioni di esecuzione PostScript.

   La `toPS2` restituisce un `Document` oggetto contenente il nuovo documento PostScript.

1. Salvare il file PostScript.

   * Crea un `java.io.File` e assicurati che l&#39;estensione del nome del file sia .ps.
   * Richiama il `Document` dell’oggetto `copyToFile` per copiare il contenuto del `Document` al file (assicurati di utilizzare `Document` oggetto restituito da `toPS2` metodo).

**Consulta anche**

[Riepilogo dei passaggi](converting-pdf-postscript-image-files.md#summary-of-steps)

[Avvio rapido (modalità SOAP): Conversione di un documento PDF in PostScript tramite l’API Java](/help/forms/developing/convert-pdf-service-java-api.md#quick-start-soap-mode-converting-a-pdf-document-to-postscript-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Convertire un documento PDF in PS utilizzando l’API del servizio Web {#convert-a-pdf-document-to-ps-using-the-web-service-api}

Convertire un documento PDF in PostScript utilizzando l’API Convert PDF Service (servizio Web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurati di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/ConvertPDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l’indirizzo IP del server che ospita AEM Forms.

1. Creare un client Convert PDF.

   * Crea un `ConvertPdfServiceClient` utilizzando il relativo costruttore predefinito.
   * Crea un `ConvertPdfServiceClient.Endpoint.Address` utilizzando `System.ServiceModel.EndpointAddress` costruttore. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/ConvertPDFService?blob=mtom`.) Non è necessario utilizzare il `lc_version` attributo. Tuttavia, specifica `?blob=mtom`.
   * Crea un `System.ServiceModel.BasicHttpBinding` ottenendo il valore del `ConvertPdfServiceClient.Endpoint.Binding` campo . Imposta il valore restituito su `BasicHttpBinding`.
   * Imposta la `System.ServiceModel.BasicHttpBinding` dell’oggetto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegnare il nome utente del modulo di AEM al campo `ConvertPdfServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore della password corrispondente al campo `ConvertPdfServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Fare riferimento al documento PDF per la conversione in un file PostScript.

   * Crea un `BLOB` utilizzando il relativo costruttore. La `BLOB` viene utilizzato per memorizzare un documento PDF convertito in un file PostScript.
   * Crea un `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF da convertire e la modalità in cui aprire il file.
   * Creare un array di byte che memorizza il contenuto del `System.IO.FileStream` oggetto. È possibile determinare le dimensioni dell&#39;array di byte ottenendo il `System.IO.FileStream` dell’oggetto `Length` proprietà.
   * Compilare l&#39;array di byte con i dati del flusso richiamando il `System.IO.FileStream` dell’oggetto `Read` e passare l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare `BLOB` oggetto assegnando il relativo `MTOM` con il contenuto dell&#39;array di byte.

1. Imposta le opzioni di esecuzione della conversione.

   * Crea un `ToPSOptionsSpec` richiamando il relativo costruttore.
   * Impostare le opzioni di esecuzione assegnando un valore al `ToPSOptionsSpec` membro dati dell’oggetto. Ad esempio, per definire il livello PostScript creato, assegnare un `PSLevel` valore di enumerazione nel `ToPSOptionsSpec` dell’oggetto `psLevel` membro dati.

1. Convertire il documento PDF in un file PostScript.

   Richiama il `GeneratePDFServiceService` dell’oggetto `toPS2` e passare i seguenti valori:

   * A `BLOB` oggetto che rappresenta il documento PDF da convertire in un file PostScript
   * A `ToPSOptionsSpec` oggetto che specifica le opzioni di esecuzione

   Al termine della conversione, estrarre i dati binari che rappresentano il documento PostScript accedendo al relativo `BLOB` dell’oggetto `MTOM` proprietà. Restituisce un array di byte che è possibile scrivere in un file PostScript.

1. Salvare il file PostScript.

   * Crea un `System.IO.FileStream` richiamando il relativo costruttore. Passa un valore stringa che rappresenta la posizione del file PS.
   * Creare un array di byte che memorizza il contenuto dei dati del `BLOB` oggetto restituito da `encryptPDFUsingPassword` metodo . Compilare l’array di byte ottenendo il valore del `BLOB` dell’oggetto `MTOM` campo .
   * Crea un `System.IO.BinaryWriter` richiamando il relativo costruttore e passando `System.IO.FileStream` oggetto.
   * Scrivi il contenuto dell&#39;array di byte al file PostScript richiamando il `System.IO.BinaryWriter` dell’oggetto `Write` e passare l&#39;array di byte.

**Consulta anche**

[Riepilogo dei passaggi](converting-pdf-postscript-image-files.md#summary-of-steps)

[Richiamo di AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamo di AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Conversione di documenti PDF in formati immagine {#converting-pdf-documents-to-image-formats}

È possibile utilizzare il servizio Convert PDF per convertire programmaticamente i documenti PDF in formati immagine, quali JPEG, JPEG 2000, TIFF e PNG. Convertendo un documento PDF in un file di immagine, è possibile utilizzare il documento PDF come file di immagine. Ad esempio, è possibile inserire l&#39;immagine in un sistema di gestione dei contenuti aziendali per lo storage.

Durante la conversione di un documento PDF in un’immagine, il servizio Convert PDF crea un’immagine separata per ogni pagina del documento. In altre parole, se il documento ha 20 pagine, il servizio Convert PDF crea 20 file di immagine. Durante la conversione di un documento PDF in un formato immagine, è possibile creare immagini singole per ogni pagina all’interno del documento PDF o un singolo file di immagine per l’intero documento PDF.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Convert PDF, consulta [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-1}

Per convertire un documento PDF in uno qualsiasi dei tipi supportati, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Creare un client di servizio Convert PDF.
1. Recupera il documento PDF da convertire.
1. Impostare le opzioni di esecuzione.
1. Converti il PDF in un’immagine.
1. Recupera i file immagine da una raccolta.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

**Creare un client Convert PDF**

Prima di poter eseguire in modo programmatico un’operazione del servizio Convert PDF, è necessario creare un client di servizio Convert PDF. Se utilizzi l’API Java, crea un `ConvertPdfServiceClient` oggetto. Se utilizzi l’API del servizio Web, crea un `ConvertPDFServiceService` oggetto.

**Recupera il documento PDF da convertire**

È necessario recuperare il documento PDF per convertirlo in un’immagine. Non è possibile convertire un documento PDF interattivo in un’immagine. Se tenti di farlo, viene generata un&#39;eccezione. Per convertire un documento PDF interattivo in un file di immagine, è necessario appiattire il documento PDF prima di convertirlo. (Vedi [Flatting dei documenti PDF](/help/forms/developing/creating-document-output-streams.md#flattening-pdf-documents).)

**Impostare le opzioni di esecuzione**

È necessario impostare le opzioni di esecuzione, ad esempio il formato immagine e i valori di risoluzione. Per informazioni sui valori di runtime, consulta la sezione `ToImageOptionsSpec` riferimento di classe in [Riferimento API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Convertire PDF in un’immagine**

Dopo aver creato il client di servizio e impostato le opzioni di esecuzione, è possibile convertire il documento di PDF in un’immagine. Viene restituito un oggetto raccolta contenente le immagini.

**Recuperare i file immagine da una raccolta**

È possibile recuperare i file immagine da un oggetto raccolta restituito dal servizio Convert PDF. Ogni elemento della raccolta è un `com.adobe.idp.Document` istanza (o `BLOB` se si utilizzano servizi Web) è possibile salvare come file immagine, ad esempio un file JPG.

Il formato del file di immagine dipende dal `ImageConvertFormat` opzione di esecuzione. Se si imposta il `ImageConvertFormat` opzione di esecuzione su `ImageConvertFormat.JPEG`, è possibile salvare i file immagine come file di JPG.

**Consulta anche**

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido dell’API per la conversione di PDF Service](/help/forms/developing/convert-pdf-service-java-api.md#convert-pdf-service-java-api-quick-start-soap)

### Convertire un documento PDF in file di immagini utilizzando l’API Java {#convert-a-pdf-document-to-image-files-using-the-java-api}

Convertire un documento PDF in un formato immagine utilizzando l’API del servizio Convert PDF (Java):

1. Includi file di progetto.

   Includi file JAR client, ad esempio adobe-convertpdf-client.jar, nel percorso di classe del progetto Java.

1. Creare un client Convert PDF.

   * Crea un `ServiceClientFactory` oggetto contenente le proprietà di connessione.
   * Crea un `ConvertPdfServiceClient` utilizzando il relativo costruttore e passando `ServiceClientFactory` oggetto.

1. Recupera il documento PDF da convertire.

   * Crea un `java.io.FileInputStream` oggetto che rappresenta il documento PDF da convertire utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del documento PDF.
   * Crea un `com.adobe.idp.Document` utilizzando il relativo costruttore e passando `java.io.FileInputStream` oggetto.

1. Impostare le opzioni di esecuzione.

   * Crea un `ToImageOptionsSpec` utilizzando il relativo costruttore.
   * Richiama i metodi che appartengono a questo oggetto come richiesto. Ad esempio, imposta il tipo di immagine richiamando il `setImageConvertFormat` metodo e passaggio di un `ImageConvertFormat` valore enum che specifica il tipo di formato.

   >[!NOTE]
   >
   >Impostazione della `ImageConvertFormat` il valore di enumerazione è obbligatorio.

1. Converti il PDF in un’immagine.

   Richiama il `ConvertPdfServiceClient` dell’oggetto `toImage2` e passare i seguenti valori:

   * A `com.adobe.idp.Document` oggetto che rappresenta il file PDF da convertire.
   * A `com.adobe.livecycle.converpdfservice.client.ToImageOptionsSpec` oggetto contenente le varie preferenze relative al formato immagine di destinazione.

   La `toImage2` restituisce un `java.util.List` oggetto che contiene immagini. Ogni elemento della raccolta è un `com.adobe.idp.Document` istanza.

1. Recupera i file immagine da una raccolta.

   Itera attraverso il `java.util.List` per determinare se le immagini sono presenti. Ogni elemento è un `com.adobe.idp.Document` istanza. Salva l’immagine richiamando il `com.adobe.idp.Document` dell’oggetto `copyToFile` e passare un `java.io.File` oggetto.

**Consulta anche**

[Avvio rapido (modalità SOAP): Conversione di un documento PDF in file JPEG tramite l’API Java](/help/forms/developing/convert-pdf-service-java-api.md#quick-start-soap-mode-converting-a-pdf-document-to-jpeg-files-using-the-java-api)

### Convertire un documento PDF in file di immagini utilizzando l’API del servizio Web {#convert-a-pdf-document-to-image-files-using-the-web-service-api}

Convertire un documento PDF in un formato immagine utilizzando l’API Convert PDF Service (servizio Web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurati di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/ConvertPDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l’indirizzo IP del server che ospita AEM Forms.

1. Crea un client PDF convertito.

   * Crea un `ConvertPdfServiceClient` utilizzando il relativo costruttore predefinito.
   * Crea un `ConvertPdfServiceClient.Endpoint.Address` utilizzando `System.ServiceModel.EndpointAddress` costruttore. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/ConvertPDFService?blob=mtom`.) Non è necessario utilizzare il `lc_version` attributo. Tuttavia, specifica `?blob=mtom`.
   * Crea un `System.ServiceModel.BasicHttpBinding` ottenendo il valore del `ConvertPdfServiceClient.Endpoint.Binding` campo . Imposta il valore restituito su `BasicHttpBinding`.
   * Imposta la `System.ServiceModel.BasicHttpBinding` dell’oggetto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegnare il nome utente del modulo di AEM al campo `ConvertPdfServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore della password corrispondente al campo `ConvertPdfServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recupera il documento PDF da convertire.

   * Crea un `BLOB` utilizzando il relativo costruttore. Questo `BLOB` viene utilizzato per memorizzare il modulo PDF.
   * Crea un `System.IO.FileStream` richiamando il relativo costruttore. Passa un valore stringa che specifica la posizione del modulo PDF e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto del `System.IO.FileStream` oggetto. Determina le dimensioni dell&#39;array di byte ottenendo il `System.IO.FileStream` dell’oggetto `Length` proprietà.
   * Compilare l&#39;array di byte con i dati del flusso richiamando il `System.IO.FileStream` dell’oggetto `Read` metodo . Passa la matrice dei byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare `BLOB` oggetto assegnando il relativo `MTOM` con il contenuto dell&#39;array di byte.

1. Impostare le opzioni di esecuzione.

   * Crea un `ToImageOptionsSpec` utilizzando il relativo costruttore.
   * Richiama i metodi che appartengono a questo oggetto come richiesto. Ad esempio, imposta il tipo di immagine richiamando il `setImageConvertFormat` metodo e passaggio di un `ImageConvertFormat` valore di enumerazione che specifica il tipo di formato.

   >[!NOTE]
   >
   >Impostazione della `ImageConvertFormat` il valore di enumerazione è obbligatorio.

1. Converti il PDF in un’immagine.

   Richiama il `ConvertPDFServiceService` dell’oggetto `toImage2` e passare i seguenti valori:

   * A `BLOB` oggetto che rappresenta il file da convertire
   * A `ToImageOptionsSpec` oggetto contenente le varie preferenze relative al formato immagine di destinazione

   La `toImage2` restituisce un `MyArrayOfBLOB` che contiene i file immagine appena creati.

1. Recupera i file immagine da una raccolta.

   * Determinare il numero di elementi nel `MyArrayOfBLOB` ottenendo il valore del relativo `Count` campo . Ogni elemento è un `BLOB` oggetto che contiene l&#39;immagine.
   * Itera attraverso il `MyArrayOfBLOB` e salvare ogni file di immagine.

**Consulta anche**

[Richiamo di AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamo di AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
