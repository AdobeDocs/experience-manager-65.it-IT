---
title: Conversione di PDF in file Postscript e Image
description: Utilizza il servizio Convert PDF per convertire i documenti PDF in PostScript e in diversi formati di immagine (JPEG, JPEG 2000, PNG e TIFF) utilizzando l’API Java e l’API del servizio Web.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 31730c24-46c3-4111-9391-ccd4342740e9
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '2801'
ht-degree: 0%

---

# Conversione di PDF in file PostScript e Image {#converting-pdf-to-postscript-andimage-files}

**Gli esempi e gli esempi contenuti in questo documento sono solo per l’ambiente AEM Forms su JEE.**

**Informazioni sul servizio Convert PDF**

Il servizio Convert PDF converte i documenti PDF in PostScript e in diversi formati di immagine (JPEG, JPEG 2000, PNG e TIFF). La conversione di un documento PDF in PostScript è utile per la stampa automatica basata su server su qualsiasi stampante PostScript. La conversione di un documento PDF in un file TIFF multipagina è pratica quando si archiviano documenti in sistemi di gestione del contenuto che non supportano i documenti PDF.

Puoi eseguire queste attività utilizzando il servizio Convert PDF:

* Converte i documenti PDF in PostScript.
* Converte i documenti PDF in formati immagine.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Convert PDF, vedere [Guida di riferimento dei servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Conversione di documenti PDF in PostScript {#converting-pdf-documents-to-postscript}

In questo argomento viene descritto come utilizzare l&#39;API Convert PDF Service (Java e servizio Web) per convertire i documenti PDF in file PostScript a livello di programmazione. Il documento PDF convertito in file PostScript deve essere un documento PDF non interattivo. In altre parole, se si tenta di convertire un documento interattivo di PDF in un file PostScript, viene generata un&#39;eccezione.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Convert PDF, vedere [Guida di riferimento dei servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary-of-steps}

Per convertire un documento PDF in un file PostScript, effettuare le seguenti operazioni:

1. Includi file di progetto.
1. Creare un client del servizio Convert PDF.
1. Fare riferimento al documento PDF per convertirlo in un file PostScript.
1. Impostare le opzioni di runtime di conversione.
1. Converte il documento PDF in un file PostScript.
1. Salvare il file PostScript.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

**Creare un client Convert PDF**

Prima di poter eseguire a livello di programmazione un&#39;operazione del servizio Convert PDF, è necessario creare un client del servizio Convert PDF. Se utilizzi l’API Java, crea un’ `ConvertPdfServiceClient` oggetto. Se utilizzi l’API del servizio web, crea un’ `ConvertPDFServiceService` oggetto.

In questa sezione vengono utilizzate le funzionalità dei servizi web introdotte in AEM Forms. Per accedere a una nuova funzionalità, è necessario creare l&#39;oggetto proxy utilizzando `lc_version` attributo. (Consulta &quot;Accesso a nuove funzionalità tramite i servizi web&quot; in [Richiamare AEM Forms tramite servizi Web](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services).)

**Riferimento al documento PDF da convertire in un file PostScript**

Fare riferimento al documento PDF che si desidera convertire in un file PostScript. Come indicato in precedenza in questo argomento, il documento PDF deve essere un documento PDF non interattivo. Se si tenta di convertire un documento di PDF interattivo in un file PostScript, viene generata un&#39;eccezione.

**Impostare le opzioni di runtime di conversione**

Quando si converte un documento PDF in un file PostScript, è possibile definire opzioni di runtime che specificano il tipo di PostScript creato. Ad esempio, potete definire un file PostScript di livello 3.

In genere, il file PostScript generato rifletterà le dimensioni del documento di input PDF. Se si seleziona la `ShrinkToFit` (che riduce l&#39;output del file PostScript per adattarlo alla pagina), non vedrete alcuna differenza tra il documento di input PDF e il file PostScript generato. Il `ShrinkToFit` l&#39;opzione ha effetto solo se si sceglie di stampare su una pagina di dimensioni inferiori rispetto al documento di input PDF. Per selezionare una dimensione di pagina inferiore, definisci `PageSize` opzione. È inoltre consigliabile impostare `RotateAndCenter` opzione per `true` per ottenere l&#39;output PostScript corretto.

Allo stesso modo, se selezioni la `ExpandToFit` (che espande l&#39;output del file PostScript per adattarlo alla pagina), ha effetto solo se si sceglie di stampare su una pagina di dimensioni maggiori rispetto al documento di input PDF. Per selezionare una pagina di dimensioni maggiori, definisci `PageSize` opzione. È inoltre consigliabile impostare `RotateAndCenter` opzione per `true` per ottenere l&#39;output PostScript corretto.

>[!NOTE]
>
>Per informazioni sui valori di runtime che è possibile impostare, vedere `ToPSOptionsSpec` riferimento di classe in [Riferimento API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Convertire il documento PDF in un file PostScript**

Dopo aver creato il client di servizio e impostato le opzioni di runtime, è possibile richiamare l&#39;operazione di conversione PostScript. Questa operazione richiede informazioni sul documento da convertire, incluso il livello PostScript preferito per il documento di destinazione.

**Salvare il file PostScript**

Dopo aver convertito il documento PDF in PostScript, è possibile salvare l&#39;output come file PostScript.

**Consulta anche**

[Convertire un documento PDF in PS utilizzando l’API Java](converting-pdf-postscript-image-files.md#convert-a-pdf-document-to-ps-using-the-java-api)

[Convertire un documento PDF in PS utilizzando l’API del servizio web](converting-pdf-postscript-image-files.md#convert-a-pdf-document-to-ps-using-the-web-service-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Guida introduttiva alla conversione dell’API PDF Service](/help/forms/developing/convert-pdf-service-java-api.md#convert-pdf-service-java-api-quick-start-soap)

### Convertire un documento PDF in PS utilizzando l’API Java {#convert-a-pdf-document-to-ps-using-the-java-api}

Convertire un documento PDF in PostScript utilizzando l&#39;API del servizio PDF Convert (Java):

1. Includi file di progetto.

   Includi i file JAR client, come adobe-convertpdf-client.jar, nel percorso di classe del progetto Java.

1. Creare un client Convert PDF.

   * Creare un `ServiceClientFactory` oggetto che contiene proprietà di connessione.
   * Creare un `ConvertPdfServiceClient` mediante il costruttore e passando il `ServiceClientFactory` oggetto.

1. Fare riferimento al documento PDF per convertirlo in un file PostScript.

   * Creare un `java.io.FileInputStream` dell&#39;oggetto utilizzando il relativo costruttore e passare un valore stringa che specifica la posizione del documento PDF da convertire.
   * Creare un `com.adobe.idp.Document` oggetto che memorizza il documento PDF utilizzando `com.adobe.idp.Document` costruttore. Passa il `java.io.FileInputStream` oggetto che contiene il documento PDF.

1. Impostare le opzioni di runtime di conversione.

   * Creare un `ToPSOptionsSpec` richiamando il relativo costruttore.
   * Impostare le opzioni di runtime richiamando un metodo appropriato appartenente al `ToPSOptionsSpec` oggetto. Ad esempio, per definire il livello PostScript creato, richiamare `ToPSOptionsSpec` dell&#39;oggetto `setPsLevel` e trasmettere un `PSLevel` valore di enumerazione che specifica il livello PostScript. Per informazioni su tutti i valori di runtime che è possibile impostare, vedere `ToPSOptionsSpec` riferimento di classe in [Riferimento API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. Converte il documento PDF in un file PostScript.

   Richiama `ConvertPdfServiceClient`dell&#39;oggetto `toPS2` e trasmettere i seguenti valori:

   * A `com.adobe.idp.Document` oggetto che rappresenta il documento PDF da convertire in un file PostScript.
   * A `ToPSOptionsSpec` oggetto che specifica le opzioni di runtime PostScript.

   Il `toPS2` il metodo restituisce un `Document` oggetto che contiene il nuovo documento PostScript.

1. Salvare il file PostScript.

   * Creare un `java.io.File` e assicurarsi che l&#39;estensione del nome file sia ps.
   * Richiama `Document` dell&#39;oggetto `copyToFile` metodo per copiare il contenuto del `Document` al file (assicurati di utilizzare il `Document` oggetto restituito da `toPS2` metodo).

**Consulta anche**

[Riepilogo dei passaggi](converting-pdf-postscript-image-files.md#summary-of-steps)

[Guida rapida (modalità SOAP): conversione di un documento PDF in PostScript utilizzando l’API Java](/help/forms/developing/convert-pdf-service-java-api.md#quick-start-soap-mode-converting-a-pdf-document-to-postscript-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Convertire un documento PDF in PS utilizzando l’API del servizio web {#convert-a-pdf-document-to-ps-using-the-web-service-api}

Convertire un documento PDF in PostScript utilizzando l&#39;API del servizio PDF Convert (servizio Web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/ConvertPDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l’indirizzo IP del server che ospita AEM Forms.

1. Creare un client Convert PDF.

   * Creare un `ConvertPdfServiceClient` utilizzando il costruttore predefinito.
   * Creare un `ConvertPdfServiceClient.Endpoint.Address` oggetto utilizzando `System.ServiceModel.EndpointAddress` costruttore. Passa un valore stringa che specifica il file WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/ConvertPDFService?blob=mtom`.) Non è necessario utilizzare il `lc_version` attributo. Tuttavia, specifica `?blob=mtom`.
   * Creare un `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto ottenendo il valore del `ConvertPdfServiceClient.Endpoint.Binding` campo. Invia il valore restituito a `BasicHttpBinding`.
   * Imposta il `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegna al campo il nome utente dei moduli AEM `ConvertPdfServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore password corrispondente al campo `ConvertPdfServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Fare riferimento al documento PDF per convertirlo in un file PostScript.

   * Creare un `BLOB` mediante il costruttore. Il `BLOB` viene utilizzato per memorizzare un documento PDF convertito in un file PostScript.
   * Creare un `System.IO.FileStream` richiamando il costruttore e passando un valore stringa che rappresenta la posizione del file del documento PDF da convertire e la modalità di apertura del file in.
   * Creare una matrice di byte che memorizza il contenuto della `System.IO.FileStream` oggetto. È possibile determinare le dimensioni della matrice di byte ottenendo `System.IO.FileStream` dell&#39;oggetto `Length` proprietà.
   * Compilare la matrice di byte con i dati di flusso richiamando `System.IO.FileStream` dell&#39;oggetto `Read` e passando la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare il `BLOB` oggetto assegnando il relativo `MTOM` con il contenuto della matrice di byte.

1. Impostare le opzioni di runtime di conversione.

   * Creare un `ToPSOptionsSpec` richiamando il relativo costruttore.
   * Impostare le opzioni di runtime assegnando un valore alla `ToPSOptionsSpec` membro dati dell&#39;oggetto. Ad esempio, per definire il livello PostScript creato, assegnare un `PSLevel` valore di enumerazione per `ToPSOptionsSpec` dell&#39;oggetto `psLevel` membro dati.

1. Converte il documento PDF in un file PostScript.

   Richiama `GeneratePDFServiceService` dell&#39;oggetto `toPS2` e trasmettere i seguenti valori:

   * A `BLOB` oggetto che rappresenta il documento PDF da convertire in un file PostScript
   * A `ToPSOptionsSpec` oggetto che specifica le opzioni di runtime

   Al termine della conversione, estrarre i dati binari che rappresentano il documento PostScript accedendo al relativo `BLOB` dell&#39;oggetto `MTOM` proprietà. Restituisce una matrice di byte che è possibile scrivere in un file PostScript.

1. Salvare il file PostScript.

   * Creare un `System.IO.FileStream` richiamando il relativo costruttore. Passa un valore stringa che rappresenta la posizione del file PS.
   * Creare una matrice di byte che memorizza il contenuto dei dati `BLOB` oggetto restituito da `encryptPDFUsingPassword` metodo. Popolare la matrice di byte ottenendo il valore della `BLOB` dell&#39;oggetto `MTOM` campo.
   * Creare un `System.IO.BinaryWriter` oggetto richiamando il relativo costruttore e passando il `System.IO.FileStream` oggetto.
   * Scrivere il contenuto della matrice di byte nel file PostScript richiamando `System.IO.BinaryWriter` dell&#39;oggetto `Write` e passando la matrice di byte.

**Consulta anche**

[Riepilogo dei passaggi](converting-pdf-postscript-image-files.md#summary-of-steps)

[Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamare AEM Forms con SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Conversione di documenti PDF in formati immagine {#converting-pdf-documents-to-image-formats}

È possibile utilizzare il servizio Converti PDF per convertire in modo programmatico i documenti PDF in formati immagine, tra cui JPEG, JPEG 2000, TIFF e PNG. Convertendo un documento PDF in un file di immagine, è possibile utilizzare il documento PDF come file di immagine. Ad esempio, è possibile inserire l&#39;immagine in un sistema di gestione dei contenuti aziendali per lo storage.

Quando si converte un documento PDF in un&#39;immagine, il servizio Converti PDF crea un&#39;immagine separata per ogni pagina del documento. In altre parole, se il documento contiene 20 pagine, il servizio Convert PDF crea 20 file di immagine. Quando si converte un documento PDF in un formato immagine, è possibile creare singole immagini per ogni pagina all&#39;interno del documento PDF o un singolo file immagine per l&#39;intero documento PDF.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Convert PDF, vedere [Guida di riferimento dei servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-1}

Per convertire un documento PDF in uno qualsiasi dei tipi supportati, effettuare le seguenti operazioni:

1. Includi file di progetto.
1. Creare un client del servizio Convert PDF.
1. Recuperare il documento PDF da convertire.
1. Impostare le opzioni di runtime.
1. Converti il PDF in un’immagine.
1. Recupera i file immagine da una raccolta.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

**Creare un client Convert PDF**

Prima di poter eseguire a livello di programmazione un&#39;operazione del servizio Convert PDF, è necessario creare un client del servizio Convert PDF. Se utilizzi l’API Java, crea un’ `ConvertPdfServiceClient` oggetto. Se utilizzi l’API del servizio web, crea un’ `ConvertPDFServiceService` oggetto.

**Recupera il documento PDF da convertire**

Recuperate il documento PDF per convertirlo in immagine. Impossibile convertire un documento PDF interattivo in un&#39;immagine. Se tenti di farlo, viene generata un’eccezione. Per convertire un documento PDF interattivo in un file di immagine, è necessario appiattire il documento PDF prima di convertirlo. (vedere [Appiattimento documenti PDF](/help/forms/developing/creating-document-output-streams.md#flattening-pdf-documents).)

**Impostare le opzioni di runtime**

Impostate le opzioni di runtime, ad esempio il formato dell&#39;immagine e i valori di risoluzione. Per informazioni sui valori di runtime, vedere `ToImageOptionsSpec` riferimento di classe in [Riferimento API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Convertire il PDF in un&#39;immagine**

Dopo aver creato il client del servizio e aver impostato le opzioni di runtime, è possibile convertire il documento PDF in un&#39;immagine. Viene restituito un insieme di immagini.

**Recuperare i file immagine da una raccolta**

È possibile recuperare i file di immagine da un oggetto insieme restituito dal servizio Convert PDF. Ogni elemento della raccolta è un `com.adobe.idp.Document` istanza (o un `BLOB` se si utilizzano i servizi web) che è possibile salvare come file di immagine, ad esempio un file JPG.

Il formato del file di immagine dipende dal `ImageConvertFormat` opzione di runtime. In altre parole, se si imposta `ImageConvertFormat` opzione di runtime per `ImageConvertFormat.JPEG`, è possibile salvare i file immagine come file JPG.

**Consulta anche**

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Guida introduttiva alla conversione dell’API PDF Service](/help/forms/developing/convert-pdf-service-java-api.md#convert-pdf-service-java-api-quick-start-soap)

### Convertire un documento PDF in file di immagine utilizzando l’API Java {#convert-a-pdf-document-to-image-files-using-the-java-api}

Convertire un documento PDF in un formato immagine utilizzando l’API del servizio PDF Convert (Java):

1. Includi file di progetto.

   Includi i file JAR client, come adobe-convertpdf-client.jar, nel percorso di classe del progetto Java.

1. Creare un client Convert PDF.

   * Creare un `ServiceClientFactory` oggetto che contiene proprietà di connessione.
   * Creare un `ConvertPdfServiceClient` mediante il costruttore e passando il `ServiceClientFactory` oggetto.

1. Recuperare il documento PDF da convertire.

   * Creare un `java.io.FileInputStream` oggetto che rappresenta il documento PDF da convertire utilizzando il relativo costruttore e passando un valore stringa che specifica la posizione del documento PDF.
   * Creare un `com.adobe.idp.Document` mediante il costruttore e passando il `java.io.FileInputStream` oggetto.

1. Impostare le opzioni di runtime.

   * Creare un `ToImageOptionsSpec` mediante il costruttore.
   * Richiama i metodi che appartengono a questo oggetto come richiesto. Ad esempio, imposta il tipo di immagine richiamando il `setImageConvertFormat` e il passaggio di un `ImageConvertFormat` valore enum che specifica il tipo di formato.

   >[!NOTE]
   >
   >Impostazione di `ImageConvertFormat` valore di enumerazione obbligatorio.

1. Converti il PDF in un’immagine.

   Richiama `ConvertPdfServiceClient` dell&#39;oggetto `toImage2` e trasmettere i seguenti valori:

   * A `com.adobe.idp.Document` oggetto che rappresenta il file PDF da convertire.
   * A `com.adobe.livecycle.converpdfservice.client.ToImageOptionsSpec` oggetto contenente le varie preferenze relative al formato immagine di destinazione.

   Il `toImage2` il metodo restituisce un `java.util.List` oggetto contenente immagini. Ogni elemento della raccolta è un `com.adobe.idp.Document` dell&#39;istanza.

1. Recupera i file immagine da una raccolta.

   Effettua iterazione attraverso `java.util.List` per determinare se le immagini sono presenti. Ogni elemento è un `com.adobe.idp.Document` dell&#39;istanza. Salva l’immagine richiamando `com.adobe.idp.Document` dell&#39;oggetto `copyToFile` e il passaggio di un `java.io.File` oggetto.

**Consulta anche**

[Guida rapida (modalità SOAP): conversione di un documento PDF in file JPEG tramite l’API Java](/help/forms/developing/convert-pdf-service-java-api.md#quick-start-soap-mode-converting-a-pdf-document-to-jpeg-files-using-the-java-api)

### Convertire un documento PDF in file immagine utilizzando l’API del servizio web {#convert-a-pdf-document-to-image-files-using-the-web-service-api}

Converti un documento PDF in un formato immagine utilizzando l’API del servizio PDF (servizio web) Convert:

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/ConvertPDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l’indirizzo IP del server che ospita AEM Forms.

1. Creare un client di conversione PDF.

   * Creare un `ConvertPdfServiceClient` utilizzando il costruttore predefinito.
   * Creare un `ConvertPdfServiceClient.Endpoint.Address` oggetto utilizzando `System.ServiceModel.EndpointAddress` costruttore. Passa un valore stringa che specifica il file WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/ConvertPDFService?blob=mtom`.) Non è necessario utilizzare il `lc_version` attributo. Tuttavia, specifica `?blob=mtom`.
   * Creare un `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto ottenendo il valore del `ConvertPdfServiceClient.Endpoint.Binding` campo. Invia il valore restituito a `BasicHttpBinding`.
   * Imposta il `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegna al campo il nome utente dei moduli AEM `ConvertPdfServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore password corrispondente al campo `ConvertPdfServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recuperare il documento PDF da convertire.

   * Creare un `BLOB` mediante il costruttore. Questo `BLOB` L&#39;oggetto viene utilizzato per memorizzare il modulo PDF.
   * Creare un `System.IO.FileStream` richiamando il relativo costruttore. Passa un valore stringa che specifica la posizione del modulo PDF e la modalità di apertura del file in.
   * Creare una matrice di byte che memorizza il contenuto della `System.IO.FileStream` oggetto. Determinare le dimensioni della matrice di byte ottenendo `System.IO.FileStream` dell&#39;oggetto `Length` proprietà.
   * Compilare la matrice di byte con i dati di flusso richiamando `System.IO.FileStream` dell&#39;oggetto `Read` metodo. Passare la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare il `BLOB` oggetto assegnando il relativo `MTOM` con il contenuto della matrice di byte.

1. Impostare le opzioni di runtime.

   * Creare un `ToImageOptionsSpec` mediante il costruttore.
   * Richiama i metodi che appartengono a questo oggetto come richiesto. Ad esempio, imposta il tipo di immagine richiamando il `setImageConvertFormat` e il passaggio di un `ImageConvertFormat` valore di enumerazione che specifica il tipo di formato.

   >[!NOTE]
   >
   >Impostazione di `ImageConvertFormat` valore di enumerazione obbligatorio.

1. Converti il PDF in un’immagine.

   Richiama `ConvertPDFServiceService` dell&#39;oggetto `toImage2` e trasmettere i seguenti valori:

   * A `BLOB` oggetto che rappresenta il file da convertire
   * A `ToImageOptionsSpec` oggetto contenente le varie preferenze relative al formato immagine di destinazione

   Il `toImage2` il metodo restituisce un `MyArrayOfBLOB` oggetto contenente i file immagine appena creati.

1. Recupera i file immagine da una raccolta.

   * Determinare il numero di elementi nel `MyArrayOfBLOB` oggetto ottenendo il valore dei relativi `Count` campo. Ogni elemento è un `BLOB` oggetto che contiene l&#39;immagine.
   * Effettua iterazione attraverso `MyArrayOfBLOB` e salvare ogni file di immagine.

**Consulta anche**

[Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamare AEM Forms con SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
