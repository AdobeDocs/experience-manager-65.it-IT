---
title: Utilizzo delle utility PDF
seo-title: Utilizzo delle utility PDF
description: Utilizzare il servizio Utilità PDF per convertire i formati di file PDF e XDP, impostare e recuperare le proprietà del documento PDF e manipolare i metadati XMP.
seo-description: Utilizzare il servizio Utilità PDF per convertire i formati di file PDF e XDP, impostare e recuperare le proprietà del documento PDF e manipolare i metadati XMP.
uuid: a2ea2359-c547-4f1b-b6ca-f276f816e36a
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: d816bf2e-5236-4084-b7c4-c32b72cdff97
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2607'
ht-degree: 1%

---


# Utilizzo delle utility PDF {#working-with-pdf-utilities}

**Esempi ed esempi in questo documento sono solo per AEM Forms in ambiente JEE.**

**Informazioni sul servizio Utilità PDF**

Il servizio Utilità PDF può convertire tra i formati di file PDF e XDP, impostare e recuperare le proprietà del documento PDF e manipolare i metadati XMP. Ad esempio, prima di convertire un documento PDF in un altro formato, è utile controllare le relative proprietà per determinare quale operazione del servizio richiamare per la conversione.

È possibile eseguire queste operazioni utilizzando il servizio Utilità PDF:

* Converti documenti PDF in documenti XDP.
* Converti i documenti XDP in documenti PDF. (Vedere [Conversione di documenti XDP in documenti PDF](pdf-utilities.md#converting-xdp-documents-into-pdf-documents).)
* Recupera le proprietà del documento PDF. (Vedere [Recupero proprietà documento PDF](pdf-utilities.md#retrieving-pdf-document-properties).)
* Salvare un documento PDF e ottimizzarlo per una visualizzazione web rapida. (Vedere [Impostazione delle modalità di salvataggio dei documenti PDF](pdf-utilities.md#setting-pdf-document-save-modes).)

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Utilità PDF, vedere [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Conversione di documenti PDF in documenti XDP {#converting-pdf-documents-into-xdp-documents}

È possibile utilizzare Java utilità PDF e API di servizi Web per convertire programmaticamente i documenti PDF in documenti XDP.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Utilità PDF, vedere [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary-of-steps}

Per convertire un documento PDF in un documento XDP, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Crea un client PDFUtilityService.
1. Richiama l’operazione di conversione da PDF a XDP.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

**Creare un client PDFUtilityService**

Prima di eseguire un&#39;operazione Utilità PDF a livello di programmazione, è necessario creare un client PDFUtilityService. Con l’API Java, questo si ottiene creando un oggetto `PDFUtilityServiceClient` . Con l’API del servizio Web, questo viene eseguito utilizzando un oggetto `PDFUtilityServiceService` .

**Richiamare l’operazione di conversione da PDF a XDP**

Dopo aver creato il client di servizio, puoi richiamare l’operazione di conversione da PDF a XDP.

**Consulta anche**

[Convertire documenti PDF in documenti XDP utilizzando l’API Java](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-java-api)

[Convertire documenti PDF in documenti XDP utilizzando l’API del servizio Web](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-web-service-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Convertire documenti PDF in documenti XDP utilizzando l&#39;API Java {#convert-pdf-documents-into-xdp-documents-using-the-java-api}

Convertire i documenti PDF in documenti XDP utilizzando l’API di utilità PDF (Java):

1. Includi file di progetto

   Includi file JAR client, come adobe-pdfutility-client.jar, nel percorso di classe del progetto Java.

1. Creare un client PDFUtilityService

   Creare un oggetto `PDFUtilityServiceClient` utilizzando il relativo costruttore e passando un oggetto `ServiceClientFactory` contenente proprietà di connessione.

1. Richiamare l’operazione di conversione da PDF a XDP

   Per eseguire la conversione, richiamare il metodo `convertPDFtoXDP` dell’oggetto `PDFUtilityServiceClient` e passare un oggetto `com.adobe.idp.Document` che rappresenta il file PDF. Il metodo restituisce un oggetto `com.adobe.idp.Document` che rappresenta il file XDP appena creato.

**Consulta anche**

[Conversione di documenti PDF in documenti XDP](pdf-utilities.md#converting-pdf-documents-into-xdp-documents)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Convertire documenti PDF in documenti XDP utilizzando l&#39;API del servizio Web {#convert-pdf-documents-into-xdp-documents-using-the-web-service-api}

Convertire i documenti PDF in documenti XDP utilizzando l’API Utilità PDF (servizio Web):

1. Includi file di progetto

   * Creare un assembly client Microsoft .NET che utilizzi il file WSDL del servizio Utilità PDF.
   * Fare riferimento all&#39;assembly client Microsoft .NET.

1. Creare un client PDFUtilityService

   Crea un oggetto `PDFUtilityServiceService` utilizzando il costruttore della classe proxy.

1. Richiamare l’operazione di conversione da PDF a XDP

   Richiamare il metodo `convertPDFtoXDP` dell&#39;oggetto `PDFUtilityServiceService` e passare un oggetto `BLOB` che rappresenta il file PDF. Il metodo restituisce un oggetto `BLOB` che rappresenta il file XDP appena creato.

**Consulta anche**

[Conversione di documenti PDF in documenti XDP](pdf-utilities.md#converting-pdf-documents-into-xdp-documents)

[Richiamo di AEM Forms con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Creazione di un assembly client .NET che utilizza la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Conversione di documenti XDP in documenti PDF {#converting-xdp-documents-into-pdf-documents}

È possibile utilizzare Java utilità PDF e API di servizi Web per convertire programmaticamente i documenti XDP in documenti PDF.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Utilità PDF, vedere [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-1}

Per convertire un documento XDP in un documento PDF, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Crea un client PDFUtilityService.
1. Richiamare l’operazione di conversione da XDP a PDF.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

**Creare un client PDFUtilityService**

Prima di eseguire un&#39;operazione Utilità PDF a livello di programmazione, è necessario creare un client PDFUtilityService. Con l’API Java, questo si ottiene creando un oggetto `PDFUtilityServiceClient` . Con l’API del servizio Web, questo viene eseguito utilizzando un oggetto `PDFUtilityServiceService` .

**Richiamare l’operazione di conversione da XDP a PDF**

Dopo aver creato il client di servizio, puoi richiamare l’operazione di conversione da XDP a PDF.

**Consulta anche**

[Convertire documenti XDP in documenti PDF utilizzando l’API Java](pdf-utilities.md#convert-xdp-documents-into-pdf-documents-using-the-java-api)

[Conversione di documenti XDP in documenti PDF tramite l’API del servizio Web](pdf-utilities.md#converting-xdp-documents-into-pdf-documents-using-the-web-service-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Convertire documenti XDP in documenti PDF utilizzando l&#39;API Java {#convert-xdp-documents-into-pdf-documents-using-the-java-api}

Convertire i documenti XDP in documenti PDF utilizzando l’API di utilità PDF (Java):

1. Includi file di progetto

   Includi file JAR client, come adobe-pdfutility-client.jar, nel percorso di classe del progetto Java.

1. Creare un client PDFUtilityService

   Creare un oggetto `PDFUtilityServiceClient` utilizzando il relativo costruttore e passando un oggetto `ServiceClientFactory` contenente proprietà di connessione.

1. Richiamare l’operazione di conversione da XDP a PDF

   Per eseguire la conversione, richiamare il metodo `convertXDPtoPDF` dell&#39;oggetto `PDFUtilityServiceClient` e passare un oggetto `com.adobe.idp.Document` che rappresenta il file XDP. Il metodo restituisce un oggetto `com.adobe.idp.Document` che rappresenta il file PDF appena creato.

**Consulta anche**

[Conversione di documenti XDP in documenti PDF](pdf-utilities.md#converting-xdp-documents-into-pdf-documents)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Conversione di documenti XDP in documenti PDF utilizzando l&#39;API del servizio Web {#converting-xdp-documents-into-pdf-documents-using-the-web-service-api}

Convertire i documenti XDP in documenti PDF utilizzando l&#39;API di utilità PDF (API del servizio Web):

1. Includi file di progetto

   * Creare un assembly client Microsoft .NET che utilizzi il file WSDL del servizio Utilità PDF.
   * Fare riferimento all&#39;assembly client Microsoft .NET.

1. Creare un client PDFUtilityService

   Crea un oggetto `PDFUtilityServiceService` utilizzando il costruttore della classe proxy.

1. Richiamare l’operazione di conversione da XDP a PDF

   Per eseguire la conversione, richiamare il metodo `convertXDPtoPDF` dell&#39;oggetto `PDFUtilityServiceService` e passare un oggetto `BLOB` che rappresenta il file XDP. Il metodo restituisce un oggetto `BLOB` che rappresenta il file PDF appena creato.

**Consulta anche**

[Conversione di documenti XDP in documenti PDF](pdf-utilities.md#converting-xdp-documents-into-pdf-documents)

[Richiamo di AEM Forms con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Creazione di un assembly client .NET che utilizza la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Recupero proprietà documento PDF {#retrieving-pdf-document-properties}

È possibile utilizzare Java utilità PDF e API di servizi Web per recuperare in modo programmatico le proprietà del documento PDF, ad esempio se il documento è un modulo compilabile o la versione minima di Acrobat necessaria per leggere il documento.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Utilità PDF, vedere [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)

### Riepilogo dei passaggi {#summary_of_steps-2}

Per recuperare le proprietà del documento PDF, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Crea un client PDFUtilityService.
1. Richiama l&#39;operazione di recupero delle proprietà.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

**Creare un client PDFUtilityService**

Prima di eseguire un&#39;operazione Utilità PDF a livello di programmazione, è necessario creare un client PDFUtilityService. Con l’API Java, questo si ottiene creando un oggetto `PDFUtilityServiceClient` . Con l’API del servizio Web, questa operazione viene eseguita utilizzando un oggetto `PDFUtilityServiceService` .

**Richiama dell&#39;operazione di recupero delle proprietà**

Dopo aver creato il client di servizio, è possibile richiamare l&#39;operazione di recupero delle proprietà.

**Consulta anche**

[Recupera le proprietà del documento PDF utilizzando l’API Java](pdf-utilities.md#retrieve-pdf-document-properties-using-the-java-api)

[Recupera le proprietà del documento PDF utilizzando l’API del servizio Web](pdf-utilities.md#retrieve-pdf-document-properties-using-the-web-service-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Recupera le proprietà del documento PDF utilizzando l’API Java {#retrieve-pdf-document-properties-using-the-java-api}

Recupera le proprietà del documento PDF utilizzando l’API Utilità PDF (Java):

1. Includi file di progetto

   Includi file JAR client, come adobe-pdfutility-client.jar, nel percorso di classe del progetto Java.

1. Creare un client PDFUtilityService

   Creare un oggetto `PDFUtilityServiceClient` utilizzando il relativo costruttore e passando un oggetto `ServiceClientFactory` contenente proprietà di connessione.

1. Richiama dell&#39;operazione di recupero delle proprietà

   Per eseguire la conversione, richiamare il metodo `getPDFProperties` dell’oggetto `PDFUtilityServiceClient` e passare quanto segue:

   * Un oggetto `com.adobe.idp.Document` che rappresenta il documento PDF.
   * Un oggetto `PDFPropertiesOptionSpec` contenente le proprietà da valutare.

   Il metodo restituisce un oggetto `PDFPropertiesResult` contenente i risultati della query.

**Consulta anche**

[Recupero delle proprietà del documento PDF](pdf-utilities.md#retrieving-pdf-document-properties)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Recupera le proprietà del documento PDF utilizzando l&#39;API del servizio Web {#retrieve-pdf-document-properties-using-the-web-service-api}

Recupera le proprietà del documento PDF utilizzando l&#39;API del servizio Web Utilità PDF:

1. Includi file di progetto

   * Creare un assembly client Microsoft .NET che utilizzi il file WSDL del servizio Utilità PDF.
   * Fare riferimento all&#39;assembly client Microsoft .NET.

1. Creare un client PDFUtilityService

   Crea un oggetto `PDFUtilityServiceService` utilizzando il costruttore della classe proxy.

1. Richiama dell&#39;operazione di recupero delle proprietà

   Per eseguire la conversione, richiamare il metodo `getPDFProperties` dell’oggetto `PDFUtilityServiceService` e passare quanto segue:

   * Un oggetto `BLOB` che rappresenta il documento PDF.
   * Un oggetto `PDFPropertiesOptionSpec` contenente le proprietà da valutare.

   Il metodo restituisce un oggetto `PDFPropertiesResult` contenente i risultati della query.

**Consulta anche**

[Recupero delle proprietà del documento PDF](pdf-utilities.md#retrieving-pdf-document-properties)

[Richiamo di AEM Forms con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Creazione di un assembly client .NET che utilizza la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Impostazione delle modalità di salvataggio dei documenti PDF {#setting-pdf-document-save-modes}

È possibile utilizzare le API del servizio Utilità PDF Java e del servizio Web per impostare programmaticamente una modalità di salvataggio per un documento PDF. Quando si utilizza il servizio Utilità PDF per impostare una modalità di salvataggio, il servizio Utilità PDF imposta solo la modalità di salvataggio e non salva effettivamente il documento PDF. Il documento PDF viene salvato quando viene passato a un&#39;altra operazione del servizio. Ad esempio, è possibile utilizzare il servizio Utilità PDF per impostare una modalità di salvataggio specifica e passarla al servizio di cifratura, in cui il documento PDF viene effettivamente salvato e cifrato.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Utilità PDF, vedere [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-3}

Per impostare l’opzione di salvataggio per i documenti PDF, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Crea un client PDFUtilityService.
1. Imposta la modalità di salvataggio.
1. Richiama l’operazione di salvataggio.
1. Passare il documento PDF a un&#39;altra operazione.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

**Creare un client PDFUtilityService**

Prima di eseguire un&#39;operazione Utilità PDF a livello di programmazione, è necessario creare un client PDFUtilityService. Con l’API Java, questo si ottiene creando un oggetto `PDFUtilityServiceClient` . Con l’API del servizio Web, questa operazione viene eseguita utilizzando un oggetto `PDFUtilityServiceService` .

**Imposta la modalità Salva**

Puoi scegliere una delle seguenti opzioni di salvataggio:

* `INCREMENTAL`: Per risparmiare in modo incrementale e ridurre il tempo necessario per risparmiare
* `FAST_WEB_VIEW`: salva per visualizzazione web rapida
* `FULL`: Per salvare utilizzando un salvataggio completo (senza ottimizzazioni)

**Richiamare l’operazione di salvataggio dello stile**

Dopo aver creato il client di servizio, è possibile richiamare l&#39;operazione di recupero delle proprietà.

**Trasmettere il documento PDF a un’altra operazione AEM Forms**

Una volta che il servizio Utilità PDF imposta la modalità di salvataggio specificata, passare il documento PDF a un&#39;altra operazione AEM Forms. Una volta restituito da tale operazione, il documento PDF viene salvato nella modalità specificata. Ad esempio, se si utilizza il servizio Utilità PDF per impostare la modalità `FAST_WEB_VIEW` e quindi passare il documento PDF all’operazione `encryptUsingPassword` del servizio di cifratura, il documento PDF restituito viene cifrato con una password e salvato in modalità `FAST_WEB_VIEW`.

>[!NOTE]
>
>La Guida rapida associata a questa sezione imposta la modalità `FAST_WEB_VIEW` e quindi trasmette il documento PDF all’operazione `encryptUsingPassword` del servizio di cifratura.

**Consulta anche**

[Impostare le opzioni di salvataggio dei documenti PDF utilizzando l’API Java](pdf-utilities.md#set-pdf-document-save-options-using-the-java-api)

[Impostare le opzioni di salvataggio dei documenti PDF utilizzando l’API del servizio Web](pdf-utilities.md#set-pdf-document-save-options-using-the-web-service-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Cifratura di documenti PDF con password](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Impostare le opzioni di salvataggio dei documenti PDF utilizzando l&#39;API Java {#set-pdf-document-save-options-using-the-java-api}

Impostare le opzioni di salvataggio del documento PDF utilizzando l’API Utilità PDF (Java):

1. Includi file di progetto

   Includi file JAR client, come adobe-pdfutility-client.jar, nel percorso di classe del progetto Java.

1. Creare un client PDFUtilityService

   Creare un oggetto `PDFUtilityServiceClient` utilizzando il relativo costruttore e passando un oggetto `ServiceClientFactory` contenente proprietà di connessione.

1. Imposta la modalità Salva

   * Creare un oggetto `PDFUtilitySaveMode` utilizzando il relativo costruttore.
   * Impostare la modalità di salvataggio richiamando il metodo `setSaveStyle` dell&#39;oggetto `PDFUtilitySaveMode` e passando un valore di stringa che specifica la modalità di salvataggio. Ad esempio, per salvare la visualizzazione web rapida, passare `FAST_WEB_VIEW`.

1. Richiamare l’operazione di salvataggio dello stile

   Richiama il metodo `setSaveMode` dell&#39;oggetto `PDFUtilityServiceClient` e passa i seguenti valori:

   * Un oggetto `com.adobe.idp.Document` che rappresenta il documento PDF.
   * Un oggetto `PDFUtilitySaveMode` contenente lo stile di salvataggio da utilizzare.
   * Un valore booleano utilizzato per determinare se ignorare le impostazioni precedenti.

   Il metodo restituisce un oggetto `com.adobe.idp.Document` formattato utilizzando lo stile di salvataggio specificato.

1. Trasmettere il documento PDF a un’altra operazione AEM Forms

   * Passa l&#39;oggetto `com.adobe.idp.Document` restituito a un&#39;altra operazione AEM Forms.

**Consulta anche**

[Impostazione delle modalità di salvataggio dei documenti PDF](pdf-utilities.md#setting-pdf-document-save-modes)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Impostare le opzioni di salvataggio dei documenti PDF utilizzando l&#39;API del servizio Web {#set-pdf-document-save-options-using-the-web-service-api}

Impostare le opzioni di salvataggio del documento PDF utilizzando l&#39;utilità PDF AP (servizio Web):

1. Includi file di progetto

   * Creare un assembly client Microsoft .NET che utilizzi il file WSDL del servizio Utilità PDF.
   * Fare riferimento all&#39;assembly client Microsoft .NET.

1. Creare un client PDFUtilityService

   Crea un oggetto `PDFUtilityServiceService` utilizzando il costruttore della classe proxy.

1. Imposta la modalità Salva

   * Creare un oggetto `PDFUtilitySaveMode` utilizzando il relativo costruttore.
   * Impostare la modalità di salvataggio assegnando un valore stringa al metodo `saveStyle` dell&#39;oggetto `PDFUtilitySaveMode` che specifica la modalità di salvataggio. Ad esempio, per salvare la visualizzazione web rapida, specificare `FAST_WEB_VIEW`.

1. Richiamare l’operazione di salvataggio dello stile

   Richiama il metodo `setSaveMode` dell&#39;oggetto `PDFUtilityServiceService` e passa i seguenti valori:

   * Un oggetto `BLOB` che rappresenta il documento PDF.
   * Un oggetto `PDFUtilitySaveMode` contenente lo stile di salvataggio da utilizzare.
   * Un valore booleano utilizzato per determinare se ignorare le impostazioni precedenti.

   Il metodo restituisce un oggetto `BLOB` formattato utilizzando lo stile di salvataggio specificato. È quindi possibile salvare l’oggetto come documento PDF.

1. Passa il documento PDF a un’altra operazione Forms

   * Passa l&#39;oggetto `BLOB` restituito a un&#39;altra operazione AEM Forms.

**Consulta anche**

[Impostazione delle modalità di salvataggio dei documenti PDF](pdf-utilities.md#setting-pdf-document-save-modes)

[Richiamo di AEM Forms con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Creazione di un assembly client .NET che utilizza la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Rimozione dei documenti PDF {#sanitizing-pdf-documents}

È possibile utilizzare le API Java di utilità PDF per convertire programmaticamente i documenti PDF in documenti XDP.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Utilità PDF, vedere [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-4}

Per eliminare il documento PDF, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Crea un client PDFUtilityService.
1. Richiamare l&#39;operazione di pulizia.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Per creare un&#39;applicazione client utilizzando Java, includi i file JAR necessari.

**Creare un client PDFUtilityService**

Prima di eseguire un&#39;operazione di pulizia a livello di programmazione, è necessario creare un client PDFUtilityService. Con l’API Java, questo si ottiene creando un oggetto `PDFUtilityServiceClient` .

**Richiamare l’operazione di conversione da PDF a XDP**

Dopo aver creato il client di servizio, è possibile richiamare l&#39;operazione di pulizia.

**Consulta anche**

[Convertire documenti PDF in documenti XDP utilizzando l’API Java](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-java-api)

[Convertire documenti PDF in documenti XDP utilizzando l’API del servizio Web](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-web-service-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Rimuovere i documenti PDF utilizzando l&#39;API Java {#sanitize-pdf-documents-using-the-java-api}

È possibile rimuovere i documenti utilizzando l’API Utilità PDF (Java):

1. Includi file di progetto

   Includi file JAR client, come adobe-pdfutility-client.jar, nel percorso classe del progetto Java.

1. Creare un client PDFUtilityService

   Creare un oggetto `PDFUtilityServiceClient` utilizzando il relativo costruttore e passando un oggetto `ServiceClientFactory` contenente proprietà di connessione.

1. Richiamare l’operazione di conversione da PDF a XDP

   Per eseguire la conversione, richiamare il metodo `convertPDFtoXDP` dell’oggetto `PDFUtilityServiceClient` e passare un oggetto `com.adobe.idp.Document` che rappresenta il file PDF. Il metodo restituisce un oggetto `com.adobe.idp.Document` che rappresenta il file XDP appena creato.

**Consulta anche**

[Rimozione dei documenti PDF](/help/forms/developing/pdf-utilities-service-java-api.md#quick-start-soap-mode-sanitizing-pdf-documents)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
