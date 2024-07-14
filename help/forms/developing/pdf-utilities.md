---
title: Utilizzo delle utilità PDF
description: Utilizza il servizio Utilità PDF per convertire i formati di file PDF e XDP, impostare e recuperare le proprietà dei documenti PDF e manipolare i metadati XMP.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: e4b204ee-7261-42b8-8db8-a92aa9fd0a28
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '2549'
ht-degree: 1%

---

# Utilizzo delle utilità PDF {#working-with-pdf-utilities}

**Gli esempi e gli esempi contenuti in questo documento sono solo per AEM Forms in ambiente JEE.**

**Informazioni sul servizio Utilità PDF**

Il servizio Utilità PDF può convertire i formati di file PDF e XDP, impostare e recuperare le proprietà dei documenti PDF e manipolare i metadati XMP. Ad esempio, prima di convertire un documento PDF in un altro formato, è utile esaminarne le proprietà per determinare quale operazione di servizio richiamare per la conversione.

Puoi eseguire queste attività utilizzando il servizio Utilità PDF:

* Convertire documenti PDF in documenti XDP.
* Convertire documenti XDP in documenti PDF. (Vedi [Conversione di documenti XDP in documenti PDF](pdf-utilities.md#converting-xdp-documents-into-pdf-documents).)
* Recuperare le proprietà del documento PDF. (Vedi [Recupero delle proprietà del documento PDF](pdf-utilities.md#retrieving-pdf-document-properties).)
* Salvare un documento PDF e ottimizzarlo per una rapida visualizzazione Web. (Vedi [Impostazione delle modalità di salvataggio del documento PDF](pdf-utilities.md#setting-pdf-document-save-modes).)

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Utilità PDF, vedere [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Conversione di documenti PDF in documenti XDP {#converting-pdf-documents-into-xdp-documents}

Puoi utilizzare le API Java e dei servizi web di PDF Utilities per convertire in modo programmatico i documenti PDF in documenti XDP.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Utilità PDF, vedere [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary-of-steps}

Per convertire un documento PDF in un documento XDP, effettuare le seguenti operazioni:

1. Includi file di progetto.
1. Creare un client PDFUtilityService.
1. Richiama il PDF all’operazione di conversione XDP.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

**Creare un client PDFUtilityService**

Prima di poter eseguire un&#39;operazione di utilità PDF a livello di programmazione, è necessario creare un client PDFUtilityService. Con l&#39;API Java, questo viene ottenuto creando un oggetto `PDFUtilityServiceClient`. Con l&#39;API del servizio Web, questa operazione viene eseguita utilizzando un oggetto `PDFUtilityServiceService`.

**Richiama il PDF all&#39;operazione di conversione XDP**

Dopo aver creato il client del servizio, è possibile richiamare il PDF all’operazione di conversione XDP.

**Consulta anche**

[Convertire documenti PDF in documenti XDP utilizzando l’API Java](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-java-api)

[Convertire documenti PDF in documenti XDP utilizzando l’API del servizio web](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-web-service-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Convertire documenti PDF in documenti XDP utilizzando l’API Java {#convert-pdf-documents-into-xdp-documents-using-the-java-api}

Converti documenti PDF in documenti XDP utilizzando l’API PDF Utilities (Java):

1. Includi file di progetto

   Includi i file JAR client, come adobe-pdfutility-client.jar, nel percorso di classe del progetto Java.

1. Creare un client PDFUtilityService

   Creare un oggetto `PDFUtilityServiceClient` utilizzando il relativo costruttore e passando un oggetto `ServiceClientFactory` che contiene proprietà di connessione.

1. Richiama il PDF all’operazione di conversione XDP

   Per eseguire la conversione, richiamare il metodo `convertPDFtoXDP` dell&#39;oggetto `PDFUtilityServiceClient` e passare un oggetto `com.adobe.idp.Document` che rappresenta il file PDF. Il metodo restituisce un oggetto `com.adobe.idp.Document` che rappresenta il file XDP appena creato.

**Consulta anche**

[Conversione di documenti PDF in documenti XDP](pdf-utilities.md#converting-pdf-documents-into-xdp-documents)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Convertire documenti PDF in documenti XDP utilizzando l’API del servizio web {#convert-pdf-documents-into-xdp-documents-using-the-web-service-api}

Converti documenti PDF in documenti XDP utilizzando l’API PDF Utilities (servizio web):

1. Includi file di progetto

   * Creare un assembly client Microsoft .NET che utilizzi il file WSDL del servizio Utilità PDF.
   * Fare riferimento all&#39;assembly client Microsoft .NET.

1. Creare un client PDFUtilityService

   Creare un oggetto `PDFUtilityServiceService` utilizzando il costruttore di classe proxy.

1. Richiama il PDF all’operazione di conversione XDP

   Richiama il metodo `convertPDFtoXDP` dell&#39;oggetto `PDFUtilityServiceService` e passa un oggetto `BLOB` che rappresenta il file PDF. Il metodo restituisce un oggetto `BLOB` che rappresenta il file XDP appena creato.

**Consulta anche**

[Conversione di documenti PDF in documenti XDP](pdf-utilities.md#converting-pdf-documents-into-xdp-documents)

[Richiamare AEM Forms utilizzando la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Creazione di un assembly client .NET che utilizza la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Conversione di documenti XDP in documenti PDF {#converting-xdp-documents-into-pdf-documents}

Puoi utilizzare le API Java e dei servizi web di PDF Utilities per convertire in modo programmatico i documenti XDP in documenti PDF.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Utilità PDF, vedere [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-1}

Per convertire un documento XDP in un documento PDF, effettuare le seguenti operazioni:

1. Includi file di progetto.
1. Creare un client PDFUtilityService.
1. Richiama l’operazione di conversione da XDP a PDF.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

**Creare un client PDFUtilityService**

Prima di poter eseguire un&#39;operazione di utilità PDF a livello di programmazione, è necessario creare un client PDFUtilityService. Con l&#39;API Java, questo viene ottenuto creando un oggetto `PDFUtilityServiceClient`. Con l&#39;API del servizio Web, questa operazione viene eseguita utilizzando un oggetto `PDFUtilityServiceService`.

**Richiama l&#39;operazione di conversione da XDP a PDF**

Dopo aver creato il client del servizio, puoi richiamare l’operazione di conversione da XDP a PDF.

**Consulta anche**

[Convertire documenti XDP in documenti PDF utilizzando l’API Java](pdf-utilities.md#convert-xdp-documents-into-pdf-documents-using-the-java-api)

[Conversione di documenti XDP in documenti PDF tramite l’API del servizio web](pdf-utilities.md#converting-xdp-documents-into-pdf-documents-using-the-web-service-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Convertire documenti XDP in documenti PDF utilizzando l’API Java {#convert-xdp-documents-into-pdf-documents-using-the-java-api}

Converti i documenti XDP in documenti PDF utilizzando l’API PDF Utilities (Java):

1. Includi file di progetto

   Includi i file JAR client, come adobe-pdfutility-client.jar, nel percorso di classe del progetto Java.

1. Creare un client PDFUtilityService

   Creare un oggetto `PDFUtilityServiceClient` utilizzando il relativo costruttore e passando un oggetto `ServiceClientFactory` che contiene proprietà di connessione.

1. Richiama l’operazione di conversione da XDP a PDF

   Per eseguire la conversione, richiamare il metodo `convertXDPtoPDF` dell&#39;oggetto `PDFUtilityServiceClient` e passare un oggetto `com.adobe.idp.Document` che rappresenta il file XDP. Il metodo restituisce un oggetto `com.adobe.idp.Document` che rappresenta il file PDF appena creato.

**Consulta anche**

[Conversione di documenti XDP in documenti PDF](pdf-utilities.md#converting-xdp-documents-into-pdf-documents)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Conversione di documenti XDP in documenti PDF tramite l’API del servizio web {#converting-xdp-documents-into-pdf-documents-using-the-web-service-api}

Converti i documenti XDP in documenti PDF utilizzando l’API PDF Utilities (API servizio web):

1. Includi file di progetto

   * Creare un assembly client Microsoft .NET che utilizzi il file WSDL del servizio Utilità PDF.
   * Fare riferimento all&#39;assembly client Microsoft .NET.

1. Creare un client PDFUtilityService

   Creare un oggetto `PDFUtilityServiceService` utilizzando il costruttore di classe proxy.

1. Richiama l’operazione di conversione da XDP a PDF

   Per eseguire la conversione, richiamare il metodo `convertXDPtoPDF` dell&#39;oggetto `PDFUtilityServiceService` e passare un oggetto `BLOB` che rappresenta il file XDP. Il metodo restituisce un oggetto `BLOB` che rappresenta il file PDF appena creato.

**Consulta anche**

[Conversione di documenti XDP in documenti PDF](pdf-utilities.md#converting-xdp-documents-into-pdf-documents)

[Richiamare AEM Forms utilizzando la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Creazione di un assembly client .NET che utilizza la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Recupero proprietà documento PDF {#retrieving-pdf-document-properties}

È possibile utilizzare le API Java e dei servizi Web di Utilità PDF per recuperare in modo programmatico le proprietà del documento di PDF, ad esempio se il documento è un modulo compilabile o la versione minima di Acrobat necessaria per leggere il documento.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Utilità PDF, vedere [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)

### Riepilogo dei passaggi {#summary_of_steps-2}

Per recuperare le proprietà del documento PDF, effettuare le seguenti operazioni:

1. Includi file di progetto.
1. Creare un client PDFUtilityService.
1. Richiama l’operazione di recupero delle proprietà.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

**Creare un client PDFUtilityService**

Prima di poter eseguire un&#39;operazione di utilità PDF a livello di programmazione, è necessario creare un client PDFUtilityService. Con l&#39;API Java, questo viene ottenuto creando un oggetto `PDFUtilityServiceClient`. Con l&#39;API del servizio Web, questa operazione viene eseguita utilizzando un oggetto `PDFUtilityServiceService`.

**Richiama l&#39;operazione di recupero delle proprietà**

Dopo aver creato il client del servizio, è possibile richiamare l&#39;operazione di recupero delle proprietà.

**Consulta anche**

[Recuperare le proprietà del documento PDF utilizzando l’API Java](pdf-utilities.md#retrieve-pdf-document-properties-using-the-java-api)

[Recuperare le proprietà del documento di PDF utilizzando l’API del servizio web](pdf-utilities.md#retrieve-pdf-document-properties-using-the-web-service-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Recuperare le proprietà del documento PDF utilizzando l’API Java {#retrieve-pdf-document-properties-using-the-java-api}

Recupera le proprietà del documento PDF utilizzando l’API PDF Utilities (Java):

1. Includi file di progetto

   Includi i file JAR client, come adobe-pdfutility-client.jar, nel percorso di classe del progetto Java.

1. Creare un client PDFUtilityService

   Creare un oggetto `PDFUtilityServiceClient` utilizzando il relativo costruttore e passando un oggetto `ServiceClientFactory` che contiene proprietà di connessione.

1. Richiama l’operazione di recupero delle proprietà

   Per eseguire la conversione, richiamare il metodo `getPDFProperties` dell&#39;oggetto `PDFUtilityServiceClient` e passare quanto segue:

   * Oggetto `com.adobe.idp.Document` che rappresenta il documento PDF.
   * Oggetto `PDFPropertiesOptionSpec` contenente le proprietà da valutare.

   Il metodo restituisce un oggetto `PDFPropertiesResult` che contiene i risultati della query.

**Consulta anche**

[Recupero proprietà documento PDF](pdf-utilities.md#retrieving-pdf-document-properties)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Recuperare le proprietà del documento di PDF utilizzando l’API del servizio web {#retrieve-pdf-document-properties-using-the-web-service-api}

Recupera le proprietà del documento PDF utilizzando l’API del servizio web PDF Utilities:

1. Includi file di progetto

   * Creare un assembly client Microsoft .NET che utilizzi il file WSDL del servizio Utilità PDF.
   * Fare riferimento all&#39;assembly client Microsoft .NET.

1. Creare un client PDFUtilityService

   Creare un oggetto `PDFUtilityServiceService` utilizzando il costruttore di classe proxy.

1. Richiama l’operazione di recupero delle proprietà

   Per eseguire la conversione, richiamare il metodo `getPDFProperties` dell&#39;oggetto `PDFUtilityServiceService` e passare quanto segue:

   * Oggetto `BLOB` che rappresenta il documento PDF.
   * Oggetto `PDFPropertiesOptionSpec` contenente le proprietà da valutare.

   Il metodo restituisce un oggetto `PDFPropertiesResult` che contiene i risultati della query.

**Consulta anche**

[Recupero proprietà documento PDF](pdf-utilities.md#retrieving-pdf-document-properties)

[Richiamare AEM Forms utilizzando la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Creazione di un assembly client .NET che utilizza la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Impostazione delle modalità di salvataggio dei documenti PDF {#setting-pdf-document-save-modes}

È possibile utilizzare il servizio Utilità PDF Java e le API del servizio Web per impostare a livello di programmazione una modalità di salvataggio per un documento di PDF. Quando si utilizza il servizio Utilità PDF per impostare una modalità di salvataggio, il servizio Utilità PDF imposta solo la modalità di salvataggio e non salva effettivamente il documento PDF. Il documento PDF viene salvato quando viene passato a un&#39;altra operazione di servizio. È ad esempio possibile utilizzare il servizio Utilità PDF per impostare una modalità di salvataggio specifica e passarla al servizio Crittografia, in cui il documento PDF viene effettivamente salvato e crittografato.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Utilità PDF, vedere [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-3}

Per impostare l&#39;opzione di salvataggio per i documenti PDF, effettuare le seguenti operazioni:

1. Includi file di progetto.
1. Creare un client PDFUtilityService.
1. Imposta la modalità di salvataggio.
1. Richiama l’operazione di salvataggio.
1. Passa il documento PDF a un&#39;altra operazione.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

**Creare un client PDFUtilityService**

Prima di poter eseguire un&#39;operazione di utilità PDF a livello di programmazione, è necessario creare un client PDFUtilityService. Con l&#39;API Java, questo viene ottenuto creando un oggetto `PDFUtilityServiceClient`. Con l&#39;API del servizio Web, questa operazione viene eseguita utilizzando un oggetto `PDFUtilityServiceService`.

**Imposta la modalità di salvataggio**

Potete scegliere una delle seguenti opzioni di salvataggio:

* `INCREMENTAL`: per risparmiare in modo incrementale per ridurre il tempo necessario al salvataggio
* `FAST_WEB_VIEW`: salva per la visualizzazione web veloce
* `FULL`: per salvare utilizzando un salvataggio completo (senza ottimizzazioni)

**Richiama l&#39;operazione di salvataggio dello stile**

Dopo aver creato il client del servizio, è possibile richiamare l&#39;operazione di recupero delle proprietà.

**Passare il documento PDF a un&#39;altra operazione AEM Forms**

Una volta che il servizio Utilità PDF ha impostato la modalità di salvataggio specificata, passare il documento PDF a un&#39;altra operazione AEM Forms. Una volta restituito da tale operazione, il documento PDF viene salvato nella modalità specificata. Se ad esempio si utilizza il servizio Utilità PDF per impostare la modalità `FAST_WEB_VIEW` e quindi si passa il documento PDF all&#39;operazione `encryptUsingPassword` del servizio di crittografia, il documento PDF restituito verrà crittografato con una password e salvato in modalità `FAST_WEB_VIEW`.

>[!NOTE]
>
>La Guida rapida associata a questa sezione imposta la modalità `FAST_WEB_VIEW` e quindi passa il documento PDF all&#39;operazione `encryptUsingPassword` del servizio di crittografia.

**Consulta anche**

[Impostare le opzioni di salvataggio dei documenti di PDF utilizzando l’API Java](pdf-utilities.md#set-pdf-document-save-options-using-the-java-api)

[Impostare le opzioni di salvataggio dei documenti di PDF utilizzando l’API del servizio Web](pdf-utilities.md#set-pdf-document-save-options-using-the-web-service-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Crittografia di documenti PDF con una password](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Impostare le opzioni di salvataggio dei documenti di PDF utilizzando l’API Java {#set-pdf-document-save-options-using-the-java-api}

Imposta le opzioni di salvataggio del documento PDF utilizzando l’API PDF Utilities (Java):

1. Includi file di progetto

   Includi i file JAR client, come adobe-pdfutility-client.jar, nel percorso di classe del progetto Java.

1. Creare un client PDFUtilityService

   Creare un oggetto `PDFUtilityServiceClient` utilizzando il relativo costruttore e passando un oggetto `ServiceClientFactory` che contiene proprietà di connessione.

1. Impostare la modalità di salvataggio

   * Creare un oggetto `PDFUtilitySaveMode` utilizzando il relativo costruttore.
   * Impostare la modalità di salvataggio richiamando il metodo `setSaveStyle` dell&#39;oggetto `PDFUtilitySaveMode` e passando un valore stringa che specifica la modalità di salvataggio. Ad esempio, per salvare per la visualizzazione Web veloce, passare `FAST_WEB_VIEW`.

1. Richiama l’operazione di salvataggio stile

   Richiama il metodo `setSaveMode` dell&#39;oggetto `PDFUtilityServiceClient` e passa i seguenti valori:

   * Oggetto `com.adobe.idp.Document` che rappresenta il documento PDF.
   * Oggetto `PDFUtilitySaveMode` contenente lo stile di salvataggio da utilizzare.
   * Valore booleano utilizzato per determinare se ignorare eventuali impostazioni precedenti.

   Il metodo restituisce un oggetto `com.adobe.idp.Document` formattato con lo stile di salvataggio specificato.

1. Passa il documento PDF a un’altra operazione AEM Forms

   * Passa l&#39;oggetto `com.adobe.idp.Document` restituito a un&#39;altra operazione AEM Forms.

**Consulta anche**

[Impostazione delle modalità di salvataggio dei documenti PDF](pdf-utilities.md#setting-pdf-document-save-modes)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Impostare le opzioni di salvataggio dei documenti di PDF utilizzando l’API del servizio Web {#set-pdf-document-save-options-using-the-web-service-api}

Impostare le opzioni di salvataggio del documento PDF utilizzando il punto di accesso Utilità PDF (servizio Web):

1. Includi file di progetto

   * Creare un assembly client Microsoft .NET che utilizzi il file WSDL del servizio Utilità PDF.
   * Fare riferimento all&#39;assembly client Microsoft .NET.

1. Creare un client PDFUtilityService

   Creare un oggetto `PDFUtilityServiceService` utilizzando il costruttore di classe proxy.

1. Impostare la modalità di salvataggio

   * Creare un oggetto `PDFUtilitySaveMode` utilizzando il relativo costruttore.
   * Impostare la modalità di salvataggio assegnando un valore stringa al metodo `saveStyle` dell&#39;oggetto `PDFUtilitySaveMode` che specifica la modalità di salvataggio. Ad esempio, per salvare per la visualizzazione Web veloce, specificare `FAST_WEB_VIEW`.

1. Richiama l’operazione di salvataggio stile

   Richiama il metodo `setSaveMode` dell&#39;oggetto `PDFUtilityServiceService` e passa i seguenti valori:

   * Oggetto `BLOB` che rappresenta il documento PDF.
   * Oggetto `PDFUtilitySaveMode` contenente lo stile di salvataggio da utilizzare.
   * Valore booleano utilizzato per determinare se ignorare eventuali impostazioni precedenti.

   Il metodo restituisce un oggetto `BLOB` formattato con lo stile di salvataggio specificato. È quindi possibile salvare l&#39;oggetto come documento PDF.

1. Passare il documento PDF a un&#39;altra operazione Forms

   * Passa l&#39;oggetto `BLOB` restituito a un&#39;altra operazione AEM Forms.

**Consulta anche**

[Impostazione delle modalità di salvataggio dei documenti PDF](pdf-utilities.md#setting-pdf-document-save-modes)

[Richiamare AEM Forms utilizzando la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Creazione di un assembly client .NET che utilizza la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Sanitizzazione dei documenti di PDF {#sanitizing-pdf-documents}

Puoi utilizzare le API Java di Utilità PDF per convertire in modo programmatico i documenti PDF in documenti XDP.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Utilità PDF, vedere [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-4}

Per bonificare il documento PDF, effettuare le seguenti operazioni:

1. Includi file di progetto.
1. Creare un client PDFUtilityService.
1. Richiama l&#39;operazione di bonifica.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Per creare un’applicazione client utilizzando Java, includi i file JAR necessari.

**Creare un client PDFUtilityService**

Prima di poter eseguire un&#39;operazione di bonifica a livello di programmazione, è necessario creare un client PDFUtilityService. Con l&#39;API Java, questo viene ottenuto creando un oggetto `PDFUtilityServiceClient`.

**Richiama il PDF all&#39;operazione di conversione XDP**

Dopo aver creato il client del servizio, è possibile richiamare l&#39;operazione di bonifica.

**Consulta anche**

[Convertire documenti PDF in documenti XDP utilizzando l’API Java](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-java-api)

[Convertire documenti PDF in documenti XDP utilizzando l’API del servizio web](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-web-service-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Sanitizzare i documenti di PDF utilizzando l’API Java {#sanitize-pdf-documents-using-the-java-api}

Proteggi i documenti utilizzando l’API PDF Utilities (Java):

1. Includi file di progetto

   Includi i file JAR client, come adobe-pdfutility-client.jar, nel percorso di classe del progetto Java.

1. Creare un client PDFUtilityService

   Creare un oggetto `PDFUtilityServiceClient` utilizzando il relativo costruttore e passando un oggetto `ServiceClientFactory` che contiene proprietà di connessione.

1. Richiama il PDF all’operazione di conversione XDP

   Per eseguire la conversione, richiamare il metodo `convertPDFtoXDP` dell&#39;oggetto `PDFUtilityServiceClient` e passare un oggetto `com.adobe.idp.Document` che rappresenta il file PDF. Il metodo restituisce un oggetto `com.adobe.idp.Document` che rappresenta il file XDP appena creato.

**Consulta anche**

[Pulizia dei documenti di PDF](/help/forms/developing/pdf-utilities-service-java-api.md#quick-start-soap-mode-sanitizing-pdf-documents)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
