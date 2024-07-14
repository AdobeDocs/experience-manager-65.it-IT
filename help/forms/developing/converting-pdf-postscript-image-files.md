---
title: Conversione di PDF in file Postscript e Image
description: Utilizza il servizio Convert PDF per convertire i documenti PDF in PostScript e in diversi formati di immagine (JPEG, JPEG 2000, PNG e TIFF) utilizzando l’API Java e l’API del servizio Web.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 31730c24-46c3-4111-9391-ccd4342740e9
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '2774'
ht-degree: 0%

---

# Conversione di PDF in file PostScript e Image {#converting-pdf-to-postscript-andimage-files}

**Gli esempi e gli esempi contenuti in questo documento sono solo per AEM Forms in ambiente JEE.**

**Informazioni sul servizio Convert PDF**

Il servizio Convert PDF converte i documenti PDF in PostScript e in diversi formati di immagine (JPEG, JPEG 2000, PNG e TIFF). La conversione di un documento PDF in PostScript è utile per la stampa automatica basata su server su qualsiasi stampante PostScript. La conversione di un documento PDF in un file TIFF multipagina è pratica quando si archiviano documenti in sistemi di gestione del contenuto che non supportano i documenti PDF.

Puoi eseguire queste attività utilizzando il servizio Convert PDF:

* Convertire documenti PDF in PostScript.
* Converte i documenti PDF in formati immagine.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Convert PDF, vedere [Riferimento ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Conversione di documenti PDF in PostScript {#converting-pdf-documents-to-postscript}

Questo argomento descrive come utilizzare l’API Convert PDF Service (Java e servizio web) per convertire in modo programmatico i documenti PDF in file PostScript. Il documento PDF convertito in un file PostScript deve essere un documento PDF non interattivo. In altre parole, se si tenta di convertire un documento PDF interattivo in un file PostScript, viene generata un&#39;eccezione.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Convert PDF, vedere [Riferimento ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary-of-steps}

Per convertire un documento PDF in un file PostScript, effettuare le seguenti operazioni:

1. Includi file di progetto.
1. Creare un client del servizio Convert PDF.
1. Fare riferimento al documento PDF per la conversione in un file PostScript.
1. Impostare le opzioni di runtime di conversione.
1. Converte il documento PDF in un file PostScript.
1. Salva il file PostScript.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

**Creare un client Convert PDF**

Prima di poter eseguire a livello di programmazione un&#39;operazione del servizio Convert PDF, è necessario creare un client del servizio Convert PDF. Se si utilizza l&#39;API Java, creare un oggetto `ConvertPdfServiceClient`. Se si utilizza l&#39;API del servizio Web, creare un oggetto `ConvertPDFServiceService`.

In questa sezione vengono utilizzate le funzionalità dei servizi web introdotte in AEM Forms. Per accedere a una nuova funzionalità, è necessario creare l&#39;oggetto proxy utilizzando l&#39;attributo `lc_version`. (Vedi &quot;Accesso alle nuove funzionalità tramite i servizi Web&quot; in [Richiamo di AEM Forms tramite i servizi Web](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services).)

**Fai riferimento al documento PDF per convertirlo in un file PostScript**

Fare riferimento al documento PDF che si desidera convertire in un file PostScript. Come indicato in precedenza in questo argomento, il documento PDF deve essere un documento PDF non interattivo. Se si tenta di convertire un documento PDF interattivo in un file PostScript, viene generata un&#39;eccezione.

**Impostare le opzioni di runtime di conversione**

Quando si converte un documento PDF in un file PostScript, è possibile definire opzioni di runtime che specificano il tipo di PostScript creato. Ad esempio, puoi definire un file PostScript di livello 3.

In genere, il file PostScript generato rifletterà le dimensioni del documento di input PDF. Se si seleziona l&#39;opzione `ShrinkToFit` (che riduce l&#39;output del file PostScript per adattarlo alla pagina), non verrà visualizzata alcuna differenza tra il documento di input PDF e il file PostScript generato. L&#39;opzione `ShrinkToFit` ha effetto solo se si sceglie di stampare su una pagina di dimensioni inferiori rispetto al documento di input PDF. Per selezionare una dimensione di pagina inferiore, definire l&#39;opzione `PageSize`. È inoltre consigliabile impostare l&#39;opzione `RotateAndCenter` su `true` per ottenere l&#39;output PostScript corretto.

Analogamente, se si seleziona l&#39;opzione `ExpandToFit` (che espande l&#39;output del file PostScript per adattarlo alla pagina), l&#39;opzione avrà effetto solo se si sceglie di stampare su una pagina di dimensioni maggiori rispetto al documento di input PDF. Per selezionare una pagina di dimensioni maggiori, definire l&#39;opzione `PageSize`. È inoltre consigliabile impostare l&#39;opzione `RotateAndCenter` su `true` per ottenere l&#39;output PostScript corretto.

>[!NOTE]
>
>Per informazioni sui valori di runtime che è possibile impostare, vedere il riferimento alla classe `ToPSOptionsSpec` in [Riferimento API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Convertire il documento PDF in un file PostScript**

Dopo aver creato il client del servizio e impostato le opzioni di runtime, è possibile richiamare l&#39;operazione di conversione PostScript. Questa operazione richiede informazioni sul documento da convertire, incluso il livello PostScript preferito per il documento di destinazione.

**Salva il file PostScript**

Dopo aver convertito il documento PDF in PostScript, è possibile salvare l&#39;output come file PostScript.

**Consulta anche**

[Convertire un documento PDF in PS utilizzando l’API Java](converting-pdf-postscript-image-files.md#convert-a-pdf-document-to-ps-using-the-java-api)

[Convertire un documento PDF in PS utilizzando l’API del servizio web](converting-pdf-postscript-image-files.md#convert-a-pdf-document-to-ps-using-the-web-service-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Guida introduttiva alla conversione dell’API PDF Service](/help/forms/developing/convert-pdf-service-java-api.md#convert-pdf-service-java-api-quick-start-soap)

### Convertire un documento PDF in PS utilizzando l’API Java {#convert-a-pdf-document-to-ps-using-the-java-api}

Convertire un documento PDF in PostScript utilizzando l’API Convert PDF Service (Java):

1. Includi file di progetto.

   Includi i file JAR client, come adobe-convertpdf-client.jar, nel percorso di classe del progetto Java.

1. Creare un client Convert PDF.

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `ConvertPdfServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Fare riferimento al documento PDF per la conversione in un file PostScript.

   * Creare un oggetto `java.io.FileInputStream` utilizzando il relativo costruttore e passare un valore stringa che specifichi la posizione del documento PDF da convertire.
   * Creare un oggetto `com.adobe.idp.Document` che memorizza il documento PDF utilizzando il costruttore `com.adobe.idp.Document`. Passa l&#39;oggetto `java.io.FileInputStream` che contiene il documento PDF.

1. Impostare le opzioni di runtime di conversione.

   * Creare un oggetto `ToPSOptionsSpec` richiamando il relativo costruttore.
   * Impostare le opzioni di runtime richiamando un metodo appropriato appartenente all&#39;oggetto `ToPSOptionsSpec`. Per definire ad esempio il livello PostScript creato, richiamare il metodo `setPsLevel` dell&#39;oggetto `ToPSOptionsSpec` e passare un valore di enumerazione `PSLevel` che specifica il livello PostScript. Per informazioni su tutti i valori di runtime che è possibile impostare, vedere il riferimento alla classe `ToPSOptionsSpec` in [Riferimento API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. Converte il documento PDF in un file PostScript.

   Richiama il metodo `toPS2` dell&#39;oggetto `ConvertPdfServiceClient` e passa i seguenti valori:

   * Oggetto `com.adobe.idp.Document` che rappresenta il documento PDF da convertire in un file PostScript.
   * Oggetto `ToPSOptionsSpec` che specifica le opzioni di runtime di PostScript.

   Il metodo `toPS2` restituisce un oggetto `Document` contenente il nuovo documento PostScript.

1. Salva il file PostScript.

   * Creare un oggetto `java.io.File` e verificare che l&#39;estensione del nome file sia ps.
   * Richiamare il metodo `copyToFile` dell&#39;oggetto `Document` per copiare il contenuto dell&#39;oggetto `Document` nel file (assicurarsi di utilizzare l&#39;oggetto `Document` restituito dal metodo `toPS2`).

**Consulta anche**

[Riepilogo dei passaggi](converting-pdf-postscript-image-files.md#summary-of-steps)

[Guida rapida (modalità SOAP): conversione di un documento PDF in PostScript tramite API Java](/help/forms/developing/convert-pdf-service-java-api.md#quick-start-soap-mode-converting-a-pdf-document-to-postscript-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Convertire un documento PDF in PS utilizzando l’API del servizio web {#convert-a-pdf-document-to-ps-using-the-web-service-api}

Convertire un documento PDF in PostScript utilizzando l’API del servizio PDF Convert (servizio web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/ConvertPDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Creare un client Convert PDF.

   * Creare un oggetto `ConvertPdfServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `ConvertPdfServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/ConvertPDFService?blob=mtom`). Non è necessario utilizzare l&#39;attributo `lc_version`. Tuttavia, specificare `?blob=mtom`.
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `ConvertPdfServiceClient.Endpoint.Binding`. Eseguire il cast del valore restituito in `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegnare il nome utente dei moduli AEM al campo `ConvertPdfServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `ConvertPdfServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Fare riferimento al documento PDF per la conversione in un file PostScript.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare un documento PDF convertito in un file PostScript.
   * Creare un oggetto `System.IO.FileStream` richiamandone il costruttore e passando un valore stringa che rappresenta la posizione del file del documento PDF da convertire e la modalità di apertura del file in.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni della matrice di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare la matrice di byte con i dati di flusso richiamando il metodo `Read` dell&#39;oggetto `System.IO.FileStream` e passando la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando il relativo campo `MTOM` al contenuto della matrice di byte.

1. Impostare le opzioni di runtime di conversione.

   * Creare un oggetto `ToPSOptionsSpec` richiamando il relativo costruttore.
   * Impostare le opzioni di runtime assegnando un valore al membro dati dell&#39;oggetto `ToPSOptionsSpec`. Per definire ad esempio il livello PostScript creato, assegnare un valore di enumerazione `PSLevel` al membro dati `psLevel` dell&#39;oggetto `ToPSOptionsSpec`.

1. Converte il documento PDF in un file PostScript.

   Richiama il metodo `toPS2` dell&#39;oggetto `GeneratePDFServiceService` e passa i seguenti valori:

   * Oggetto `BLOB` che rappresenta il documento PDF da convertire in un file PostScript
   * Oggetto `ToPSOptionsSpec` che specifica le opzioni di runtime

   Al termine della conversione, estrarre i dati binari che rappresentano il documento PostScript accedendo alla proprietà `MTOM` dell&#39;oggetto `BLOB`. Restituisce una matrice di byte che è possibile scrivere in un file PostScript.

1. Salva il file PostScript.

   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore. Passa un valore stringa che rappresenta la posizione del file PS.
   * Creare una matrice di byte che memorizza il contenuto dei dati dell&#39;oggetto `BLOB` restituito dal metodo `encryptPDFUsingPassword`. Compilare la matrice di byte ottenendo il valore del campo `MTOM` dell&#39;oggetto `BLOB`.
   * Creare un oggetto `System.IO.BinaryWriter` richiamandone il costruttore e passando l&#39;oggetto `System.IO.FileStream`.
   * Scrivere il contenuto della matrice di byte nel file PostScript richiamando il metodo `Write` dell&#39;oggetto `System.IO.BinaryWriter` e passando la matrice di byte.

**Consulta anche**

[Riepilogo dei passaggi](converting-pdf-postscript-image-files.md#summary-of-steps)

[Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamare AEM Forms con SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Conversione di documenti PDF in formati immagine {#converting-pdf-documents-to-image-formats}

È possibile utilizzare il servizio Converti PDF per convertire in modo programmatico i documenti PDF in formati immagine, tra cui JPEG, JPEG 2000, TIFF e PNG. Convertendo un documento PDF in un file di immagine, è possibile utilizzare il documento PDF come file di immagine. Ad esempio, è possibile inserire l&#39;immagine in un sistema di gestione dei contenuti aziendali per lo storage.

Quando si converte un documento PDF in un&#39;immagine, il servizio Converti PDF crea un&#39;immagine separata per ogni pagina del documento. In altre parole, se il documento contiene 20 pagine, il servizio Convert PDF crea 20 file di immagine. Quando si converte un documento PDF in un formato immagine, è possibile creare singole immagini per ogni pagina all&#39;interno del documento PDF o un singolo file immagine per l&#39;intero documento PDF.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Convert PDF, vedere [Riferimento ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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

Prima di poter eseguire a livello di programmazione un&#39;operazione del servizio Convert PDF, è necessario creare un client del servizio Convert PDF. Se si utilizza l&#39;API Java, creare un oggetto `ConvertPdfServiceClient`. Se si utilizza l&#39;API del servizio Web, creare un oggetto `ConvertPDFServiceService`.

**Recupera il documento PDF da convertire**

Recuperate il documento PDF per convertirlo in immagine. Impossibile convertire un documento PDF interattivo in un&#39;immagine. Se tenti di farlo, viene generata un’eccezione. Per convertire un documento PDF interattivo in un file di immagine, è necessario appiattire il documento PDF prima di convertirlo. (Vedi [Appiattimento dei documenti di PDF](/help/forms/developing/creating-document-output-streams.md#flattening-pdf-documents).)

**Impostare le opzioni di runtime**

Impostate le opzioni di runtime, ad esempio il formato dell&#39;immagine e i valori di risoluzione. Per informazioni sui valori di runtime, vedere il riferimento alla classe `ToImageOptionsSpec` in [Riferimento API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Convertire il PDF in un&#39;immagine**

Dopo aver creato il client del servizio e aver impostato le opzioni di runtime, è possibile convertire il documento PDF in un&#39;immagine. Viene restituito un insieme di immagini.

**Recupera i file di immagine da una raccolta**

È possibile recuperare i file di immagine da un oggetto insieme restituito dal servizio Convert PDF. Ogni elemento della raccolta è un&#39;istanza `com.adobe.idp.Document` (o un&#39;istanza `BLOB` se si utilizzano i servizi Web) che è possibile salvare come file di immagine, ad esempio un file JPG.

Il formato del file di immagine dipende dall&#39;opzione di runtime `ImageConvertFormat`. In altre parole, se si imposta l&#39;opzione di runtime `ImageConvertFormat` su `ImageConvertFormat.JPEG`, è possibile salvare i file immagine come file JPG.

**Consulta anche**

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Guida introduttiva alla conversione dell’API PDF Service](/help/forms/developing/convert-pdf-service-java-api.md#convert-pdf-service-java-api-quick-start-soap)

### Convertire un documento PDF in file di immagine utilizzando l’API Java {#convert-a-pdf-document-to-image-files-using-the-java-api}

Convertire un documento PDF in un formato immagine utilizzando l’API del servizio PDF Convert (Java):

1. Includi file di progetto.

   Includi i file JAR client, come adobe-convertpdf-client.jar, nel percorso di classe del progetto Java.

1. Creare un client Convert PDF.

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `ConvertPdfServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Recuperare il documento PDF da convertire.

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento PDF da convertire utilizzando il relativo costruttore e passando un valore stringa che specifica la posizione del documento PDF.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Impostare le opzioni di runtime.

   * Creare un oggetto `ToImageOptionsSpec` utilizzando il relativo costruttore.
   * Richiama i metodi che appartengono a questo oggetto come richiesto. Ad esempio, impostare il tipo di immagine richiamando il metodo `setImageConvertFormat` e passando un valore enum `ImageConvertFormat` che specifica il tipo di formato.

   >[!NOTE]
   >
   >L&#39;impostazione del valore di enumerazione `ImageConvertFormat` è obbligatoria.

1. Converti il PDF in un’immagine.

   Richiama il metodo `toImage2` dell&#39;oggetto `ConvertPdfServiceClient` e passa i seguenti valori:

   * Oggetto `com.adobe.idp.Document` che rappresenta il file PDF da convertire.
   * Oggetto `com.adobe.livecycle.converpdfservice.client.ToImageOptionsSpec` contenente le varie preferenze relative al formato immagine di destinazione.

   Il metodo `toImage2` restituisce un oggetto `java.util.List` contenente immagini. Ogni elemento della raccolta è un&#39;istanza `com.adobe.idp.Document`.

1. Recupera i file immagine da una raccolta.

   Scorrere l&#39;oggetto `java.util.List` per determinare se le immagini sono presenti. Ogni elemento è un&#39;istanza `com.adobe.idp.Document`. Salvare l&#39;immagine richiamando il metodo `copyToFile` dell&#39;oggetto `com.adobe.idp.Document` e passando un oggetto `java.io.File`.

**Consulta anche**

[Guida rapida (modalità SOAP): conversione di un documento PDF in file JPEG tramite l’API Java](/help/forms/developing/convert-pdf-service-java-api.md#quick-start-soap-mode-converting-a-pdf-document-to-jpeg-files-using-the-java-api)

### Convertire un documento PDF in file immagine utilizzando l’API del servizio web {#convert-a-pdf-document-to-image-files-using-the-web-service-api}

Converti un documento PDF in un formato immagine utilizzando l’API del servizio PDF (servizio web) Convert:

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/ConvertPDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Creare un client di conversione PDF.

   * Creare un oggetto `ConvertPdfServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `ConvertPdfServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/ConvertPDFService?blob=mtom`). Non è necessario utilizzare l&#39;attributo `lc_version`. Tuttavia, specificare `?blob=mtom`.
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `ConvertPdfServiceClient.Endpoint.Binding`. Eseguire il cast del valore restituito in `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegnare il nome utente dei moduli AEM al campo `ConvertPdfServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `ConvertPdfServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recuperare il documento PDF da convertire.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. Questo oggetto `BLOB` viene utilizzato per memorizzare il modulo PDF.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore. Passa un valore stringa che specifica la posizione del modulo PDF e la modalità di apertura del file in.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. Determinare le dimensioni della matrice di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare la matrice di byte con i dati di flusso richiamando il metodo `Read` dell&#39;oggetto `System.IO.FileStream`. Passare la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando il relativo campo `MTOM` al contenuto della matrice di byte.

1. Impostare le opzioni di runtime.

   * Creare un oggetto `ToImageOptionsSpec` utilizzando il relativo costruttore.
   * Richiama i metodi che appartengono a questo oggetto come richiesto. Ad esempio, impostare il tipo di immagine richiamando il metodo `setImageConvertFormat` e passando un valore di enumerazione `ImageConvertFormat` che specifica il tipo di formato.

   >[!NOTE]
   >
   >L&#39;impostazione del valore di enumerazione `ImageConvertFormat` è obbligatoria.

1. Converti il PDF in un’immagine.

   Richiama il metodo `toImage2` dell&#39;oggetto `ConvertPDFServiceService` e passa i seguenti valori:

   * Oggetto `BLOB` che rappresenta il file da convertire
   * Oggetto `ToImageOptionsSpec` contenente le varie preferenze relative al formato immagine di destinazione

   Il metodo `toImage2` restituisce un oggetto `MyArrayOfBLOB` contenente i file immagine appena creati.

1. Recupera i file immagine da una raccolta.

   * Determinare il numero di elementi nell&#39;oggetto `MyArrayOfBLOB` ottenendo il valore del relativo campo `Count`. Ogni elemento è un oggetto `BLOB` che contiene l&#39;immagine.
   * Scorrere l&#39;oggetto `MyArrayOfBLOB` e salvare ogni file di immagine.

**Consulta anche**

[Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamare AEM Forms con SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
