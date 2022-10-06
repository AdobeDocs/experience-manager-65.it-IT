---
title: Utilizzo delle utility di PDF
seo-title: Working with PDF Utilities
description: Utilizzare il servizio Utilità di PDF per convertire i formati di file PDF e XDP, impostare e recuperare le proprietà del documento PDF e manipolare i metadati XMP.
seo-description: Use the PDF Utilities service to convert between PDF and XDP file formats, set and retrieve PDF document properties, and manipulate XMP metadata.
uuid: a2ea2359-c547-4f1b-b6ca-f276f816e36a
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: d816bf2e-5236-4084-b7c4-c32b72cdff97
role: Developer
exl-id: e4b204ee-7261-42b8-8db8-a92aa9fd0a28
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2579'
ht-degree: 1%

---

# Utilizzo delle utility di PDF {#working-with-pdf-utilities}

**Esempi ed esempi in questo documento sono solo per AEM Forms in ambiente JEE.**

**Informazioni sul servizio Utilità di PDF**

Il servizio Utilità di PDF può convertire i formati di file PDF e XDP, impostare e recuperare le proprietà del documento PDF e manipolare i metadati XMP. Ad esempio, prima di convertire un documento PDF in un altro formato, è utile controllare le relative proprietà per determinare quale operazione del servizio richiamare per la conversione.

Puoi eseguire queste attività utilizzando il servizio Utilità di PDF:

* Converti i documenti PDF in documenti XDP.
* Converti i documenti XDP in documenti PDF. (Vedi [Conversione di documenti XDP in documenti PDF](pdf-utilities.md#converting-xdp-documents-into-pdf-documents).)
* Recupera le proprietà del documento PDF. (Vedi [Recupero delle proprietà del documento di PDF](pdf-utilities.md#retrieving-pdf-document-properties).)
* Salvare un documento PDF e ottimizzarlo per una visualizzazione web rapida. (Vedi [Impostazione delle modalità di salvataggio dei documenti PDF](pdf-utilities.md#setting-pdf-document-save-modes).)

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Utilità di PDF, consulta [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Conversione di documenti PDF in documenti XDP {#converting-pdf-documents-into-xdp-documents}

È possibile utilizzare le API di PDF Utilities Java e dei servizi Web per convertire programmaticamente i documenti PDF in documenti XDP.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Utilità di PDF, consulta [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary-of-steps}

Per convertire un documento PDF in un documento XDP, esegui le seguenti operazioni:

1. Includi file di progetto.
1. Crea un client PDFUtilityService.
1. Richiama l’operazione di conversione da PDF a XDP.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

**Creare un client PDFUtilityService**

Prima di poter eseguire un&#39;operazione Utilità di PDF a livello di programmazione, è necessario creare un client PDFUtilityService. Con l’API Java, si ottiene questo risultato creando un’ `PDFUtilityServiceClient` oggetto. Con l’API del servizio Web, si ottiene questo risultato utilizzando un `PDFUtilityServiceService` oggetto.

**Richiamare l’operazione di conversione da PDF a XDP**

Dopo aver creato il client di servizio, è possibile richiamare l’operazione di conversione da PDF a XDP.

**Consulta anche**

[Convertire documenti PDF in documenti XDP utilizzando l’API Java](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-java-api)

[Convertire documenti PDF in documenti XDP utilizzando l’API del servizio Web](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-web-service-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Convertire documenti PDF in documenti XDP utilizzando l’API Java {#convert-pdf-documents-into-xdp-documents-using-the-java-api}

Convertire i documenti PDF in documenti XDP utilizzando l’API di utilità di PDF (Java):

1. Includi file di progetto

   Includi file JAR client, come adobe-pdfutility-client.jar, nel percorso di classe del progetto Java.

1. Creare un client PDFUtilityService

   Crea un `PDFUtilityServiceClient` utilizzando il relativo costruttore e passando un `ServiceClientFactory` oggetto contenente le proprietà di connessione.

1. Richiamare l’operazione di conversione da PDF a XDP

   Per eseguire la conversione, richiama il `PDFUtilityServiceClient` dell’oggetto `convertPDFtoXDP` e trasmettere un `com.adobe.idp.Document` oggetto che rappresenta il file PDF. Il metodo restituisce un `com.adobe.idp.Document` oggetto che rappresenta il file XDP appena creato.

**Consulta anche**

[Conversione di documenti PDF in documenti XDP](pdf-utilities.md#converting-pdf-documents-into-xdp-documents)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Convertire documenti PDF in documenti XDP utilizzando l’API del servizio Web {#convert-pdf-documents-into-xdp-documents-using-the-web-service-api}

Convertire i documenti PDF in documenti XDP utilizzando l’API Utilità di PDF (servizio Web):

1. Includi file di progetto

   * Creare un assembly client Microsoft .NET che utilizzi il file WSDL del servizio PDF Utilities.
   * Fare riferimento all&#39;assembly client Microsoft .NET.

1. Creare un client PDFUtilityService

   Crea un `PDFUtilityServiceService` utilizzando il costruttore della classe proxy.

1. Richiamare l’operazione di conversione da PDF a XDP

   Richiama il `PDFUtilityServiceService` dell’oggetto `convertPDFtoXDP` e trasmettere un `BLOB` oggetto che rappresenta il file PDF. Il metodo restituisce un `BLOB` oggetto che rappresenta il file XDP appena creato.

**Consulta anche**

[Conversione di documenti PDF in documenti XDP](pdf-utilities.md#converting-pdf-documents-into-xdp-documents)

[Richiamo di AEM Forms con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Creazione di un assembly client .NET che utilizza la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Conversione di documenti XDP in documenti PDF {#converting-xdp-documents-into-pdf-documents}

È possibile utilizzare le API di PDF Utilities Java e dei servizi Web per convertire programmaticamente i documenti XDP in documenti PDF.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Utilità di PDF, consulta [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-1}

Per convertire un documento XDP in un documento PDF, esegui le seguenti operazioni:

1. Includi file di progetto.
1. Crea un client PDFUtilityService.
1. Richiama l’operazione di conversione da XDP a PDF.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

**Creare un client PDFUtilityService**

Prima di poter eseguire un&#39;operazione Utilità di PDF a livello di programmazione, è necessario creare un client PDFUtilityService. Con l’API Java, si ottiene questo risultato creando un’ `PDFUtilityServiceClient` oggetto. Con l’API del servizio Web, si ottiene questo risultato utilizzando un `PDFUtilityServiceService` oggetto.

**Richiamare l’operazione di conversione da XDP a PDF**

Dopo aver creato il client di servizio, è possibile richiamare l’operazione di conversione da XDP a PDF.

**Consulta anche**

[Convertire documenti XDP in documenti PDF utilizzando l’API Java](pdf-utilities.md#convert-xdp-documents-into-pdf-documents-using-the-java-api)

[Conversione di documenti XDP in documenti PDF tramite l’API del servizio Web](pdf-utilities.md#converting-xdp-documents-into-pdf-documents-using-the-web-service-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Convertire documenti XDP in documenti PDF utilizzando l’API Java {#convert-xdp-documents-into-pdf-documents-using-the-java-api}

Convertire i documenti XDP in documenti PDF utilizzando l’API Utilità di PDF (Java):

1. Includi file di progetto

   Includi file JAR client, come adobe-pdfutility-client.jar, nel percorso di classe del progetto Java.

1. Creare un client PDFUtilityService

   Crea un `PDFUtilityServiceClient` utilizzando il relativo costruttore e passando un `ServiceClientFactory` oggetto contenente le proprietà di connessione.

1. Richiamare l’operazione di conversione da XDP a PDF

   Per eseguire la conversione, richiama il `PDFUtilityServiceClient` dell’oggetto `convertXDPtoPDF` e trasmettere un `com.adobe.idp.Document` oggetto che rappresenta il file XDP. Il metodo restituisce un `com.adobe.idp.Document` oggetto che rappresenta il file PDF appena creato.

**Consulta anche**

[Conversione di documenti XDP in documenti PDF](pdf-utilities.md#converting-xdp-documents-into-pdf-documents)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Conversione di documenti XDP in documenti PDF tramite l’API del servizio Web {#converting-xdp-documents-into-pdf-documents-using-the-web-service-api}

Convertire i documenti XDP in documenti PDF utilizzando l’API di PDF Utilities (API del servizio Web):

1. Includi file di progetto

   * Creare un assembly client Microsoft .NET che utilizzi il file WSDL del servizio PDF Utilities.
   * Fare riferimento all&#39;assembly client Microsoft .NET.

1. Creare un client PDFUtilityService

   Crea un `PDFUtilityServiceService` utilizzando il costruttore della classe proxy.

1. Richiamare l’operazione di conversione da XDP a PDF

   Per eseguire la conversione, richiama il `PDFUtilityServiceService` dell’oggetto `convertXDPtoPDF` e trasmettere un `BLOB` oggetto che rappresenta il file XDP. Il metodo restituisce un `BLOB` oggetto che rappresenta il file PDF appena creato.

**Consulta anche**

[Conversione di documenti XDP in documenti PDF](pdf-utilities.md#converting-xdp-documents-into-pdf-documents)

[Richiamo di AEM Forms con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Creazione di un assembly client .NET che utilizza la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Recupero delle proprietà del documento di PDF {#retrieving-pdf-document-properties}

È possibile utilizzare le API di PDF Utilities Java e dei servizi Web per recuperare in modo programmatico le proprietà del documento PDF, ad esempio se il documento è un modulo compilabile o la versione minima di Acrobat necessaria per leggere il documento.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Utilità di PDF, consulta [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)

### Riepilogo dei passaggi {#summary_of_steps-2}

Per recuperare le proprietà del documento PDF, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Crea un client PDFUtilityService.
1. Richiama l&#39;operazione di recupero delle proprietà.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

**Creare un client PDFUtilityService**

Prima di poter eseguire un&#39;operazione Utilità di PDF a livello di programmazione, è necessario creare un client PDFUtilityService. Con l’API Java, si ottiene questo risultato creando un’ `PDFUtilityServiceClient` oggetto. Con l’API del servizio Web, questa operazione viene eseguita utilizzando un `PDFUtilityServiceService` oggetto.

**Richiama dell&#39;operazione di recupero delle proprietà**

Dopo aver creato il client di servizio, è possibile richiamare l&#39;operazione di recupero delle proprietà.

**Consulta anche**

[Recuperare le proprietà del documento PDF utilizzando l’API Java](pdf-utilities.md#retrieve-pdf-document-properties-using-the-java-api)

[Recupera le proprietà del documento PDF utilizzando l’API del servizio Web](pdf-utilities.md#retrieve-pdf-document-properties-using-the-web-service-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Recuperare le proprietà del documento PDF utilizzando l’API Java {#retrieve-pdf-document-properties-using-the-java-api}

Recupera le proprietà del documento PDF utilizzando l’API Utilità di PDF (Java):

1. Includi file di progetto

   Includi file JAR client, come adobe-pdfutility-client.jar, nel percorso di classe del progetto Java.

1. Creare un client PDFUtilityService

   Crea un `PDFUtilityServiceClient` utilizzando il relativo costruttore e passando un `ServiceClientFactory` oggetto contenente le proprietà di connessione.

1. Richiama dell&#39;operazione di recupero delle proprietà

   Per eseguire la conversione, richiama il `PDFUtilityServiceClient` dell’oggetto `getPDFProperties` e passare quanto segue:

   * A `com.adobe.idp.Document` oggetto che rappresenta il documento PDF.
   * A `PDFPropertiesOptionSpec` oggetto contenente le proprietà da valutare.

   Il metodo restituisce un `PDFPropertiesResult` oggetto contenente i risultati della query.

**Consulta anche**

[Recupero delle proprietà del documento di PDF](pdf-utilities.md#retrieving-pdf-document-properties)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Recupera le proprietà del documento PDF utilizzando l’API del servizio Web {#retrieve-pdf-document-properties-using-the-web-service-api}

Recupera le proprietà del documento PDF utilizzando l’API del servizio Web PDF Utilities:

1. Includi file di progetto

   * Creare un assembly client Microsoft .NET che utilizzi il file WSDL del servizio PDF Utilities.
   * Fare riferimento all&#39;assembly client Microsoft .NET.

1. Creare un client PDFUtilityService

   Crea un `PDFUtilityServiceService` utilizzando il costruttore della classe proxy.

1. Richiama dell&#39;operazione di recupero delle proprietà

   Per eseguire la conversione, richiama il `PDFUtilityServiceService` dell’oggetto `getPDFProperties` e passare quanto segue:

   * A `BLOB` oggetto che rappresenta il documento PDF.
   * A `PDFPropertiesOptionSpec` oggetto contenente le proprietà da valutare.

   Il metodo restituisce un `PDFPropertiesResult` oggetto contenente i risultati della query.

**Consulta anche**

[Recupero delle proprietà del documento di PDF](pdf-utilities.md#retrieving-pdf-document-properties)

[Richiamo di AEM Forms con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Creazione di un assembly client .NET che utilizza la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Impostazione delle modalità di salvataggio dei documenti PDF {#setting-pdf-document-save-modes}

È possibile utilizzare le API del servizio PDF Utilities Java e del servizio Web per impostare programmaticamente una modalità di salvataggio per un documento PDF. Quando si utilizza il servizio Utilità di PDF per impostare una modalità di salvataggio, il servizio Utilità di PDF imposta solo la modalità di salvataggio e non salva effettivamente il documento PDF. Il documento PDF viene salvato quando viene passato a un&#39;altra operazione del servizio. Ad esempio, è possibile utilizzare il servizio Utilità di PDF per impostare una modalità di salvataggio specifica e passarla al servizio Crittografia, in cui il documento di PDF viene effettivamente salvato e crittografato.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Utilità di PDF, consulta [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-3}

Per impostare l’opzione di salvataggio per i documenti PDF, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Crea un client PDFUtilityService.
1. Imposta la modalità di salvataggio.
1. Richiama l’operazione di salvataggio.
1. Passa il documento PDF a un’altra operazione.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

**Creare un client PDFUtilityService**

Prima di poter eseguire un&#39;operazione Utilità di PDF a livello di programmazione, è necessario creare un client PDFUtilityService. Con l’API Java, si ottiene questo risultato creando un’ `PDFUtilityServiceClient` oggetto. Con l’API del servizio Web, questa operazione viene eseguita utilizzando un `PDFUtilityServiceService` oggetto.

**Imposta la modalità Salva**

Puoi scegliere una delle seguenti opzioni di salvataggio:

* `INCREMENTAL`: Per risparmiare in modo incrementale e ridurre il tempo necessario per risparmiare
* `FAST_WEB_VIEW`: salva per visualizzazione web rapida
* `FULL`: Per salvare utilizzando un salvataggio completo (senza ottimizzazioni)

**Richiamare l’operazione di salvataggio dello stile**

Dopo aver creato il client di servizio, è possibile richiamare l&#39;operazione di recupero delle proprietà.

**Passa il documento PDF a un’altra operazione AEM Forms**

Una volta che il servizio Utilità di PDF imposta la modalità di salvataggio specificata, passare il documento PDF a un’altra operazione AEM Forms. Una volta restituito da tale operazione, il documento PDF viene salvato nella modalità specificata. Ad esempio, se si utilizza il servizio Utilità di PDF per impostare il `FAST_WEB_VIEW` , quindi passa il documento PDF al servizio di cifratura `encryptUsingPassword` il documento PDF restituito viene crittografato con una password e salvato nel `FAST_WEB_VIEW` modalità.

>[!NOTE]
>
>La Guida rapida associata a questa sezione imposta la `FAST_WEB_VIEW` quindi passa il documento PDF al servizio di cifratura `encryptUsingPassword` funzionamento.

**Consulta anche**

[Impostare le opzioni di salvataggio dei documenti PDF utilizzando l’API Java](pdf-utilities.md#set-pdf-document-save-options-using-the-java-api)

[Impostare le opzioni di salvataggio dei documenti PDF utilizzando l’API del servizio Web](pdf-utilities.md#set-pdf-document-save-options-using-the-web-service-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Crittografia dei documenti PDF con una password](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Impostare le opzioni di salvataggio dei documenti PDF utilizzando l’API Java {#set-pdf-document-save-options-using-the-java-api}

Impostare le opzioni di salvataggio del documento di PDF utilizzando l’API Utilità di PDF (Java):

1. Includi file di progetto

   Includi file JAR client, come adobe-pdfutility-client.jar, nel percorso di classe del progetto Java.

1. Creare un client PDFUtilityService

   Crea un `PDFUtilityServiceClient` utilizzando il relativo costruttore e passando un `ServiceClientFactory` oggetto contenente le proprietà di connessione.

1. Imposta la modalità Salva

   * Crea un `PDFUtilitySaveMode` utilizzando il relativo costruttore.
   * Imposta la modalità di salvataggio richiamando il `PDFUtilitySaveMode` dell’oggetto `setSaveStyle` e passare un valore stringa che specifica la modalità di salvataggio. Ad esempio, per salvare la visualizzazione web rapida, passare `FAST_WEB_VIEW`.

1. Richiamare l’operazione di salvataggio dello stile

   Richiama il `PDFUtilityServiceClient` dell’oggetto `setSaveMode` e passare i seguenti valori:

   * A `com.adobe.idp.Document` oggetto che rappresenta il documento PDF.
   * A `PDFUtilitySaveMode` oggetto contenente lo stile di salvataggio da utilizzare.
   * Un valore booleano utilizzato per determinare se ignorare le impostazioni precedenti.

   Il metodo restituisce un `com.adobe.idp.Document` oggetto formattato utilizzando lo stile di salvataggio specificato.

1. Passa il documento PDF a un’altra operazione AEM Forms

   * Passa il restituito `com.adobe.idp.Document` a un&#39;altra operazione AEM Forms.

**Consulta anche**

[Impostazione delle modalità di salvataggio dei documenti PDF](pdf-utilities.md#setting-pdf-document-save-modes)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Impostare le opzioni di salvataggio dei documenti PDF utilizzando l’API del servizio Web {#set-pdf-document-save-options-using-the-web-service-api}

Impostare le opzioni di salvataggio del documento PDF utilizzando PDF Utilities AP (servizio Web):

1. Includi file di progetto

   * Creare un assembly client Microsoft .NET che utilizzi il file WSDL del servizio PDF Utilities.
   * Fare riferimento all&#39;assembly client Microsoft .NET.

1. Creare un client PDFUtilityService

   Crea un `PDFUtilityServiceService` utilizzando il costruttore della classe proxy.

1. Imposta la modalità Salva

   * Crea un `PDFUtilitySaveMode` utilizzando il relativo costruttore.
   * Imposta la modalità di salvataggio assegnando un valore stringa al `PDFUtilitySaveMode` dell’oggetto `saveStyle` metodo che specifica la modalità di salvataggio. Ad esempio, per salvare la visualizzazione web rapida, specifica `FAST_WEB_VIEW`.

1. Richiamare l’operazione di salvataggio dello stile

   Richiama il `PDFUtilityServiceService` dell’oggetto `setSaveMode` e passare i seguenti valori:

   * A `BLOB` oggetto che rappresenta il documento PDF.
   * A `PDFUtilitySaveMode` oggetto contenente lo stile di salvataggio da utilizzare.
   * Un valore booleano utilizzato per determinare se ignorare le impostazioni precedenti.

   Il metodo restituisce un `BLOB` oggetto formattato utilizzando lo stile di salvataggio specificato. È quindi possibile salvare l’oggetto come documento PDF.

1. Passa il documento PDF a un’altra operazione Forms

   * Passa il restituito `BLOB` a un&#39;altra operazione AEM Forms.

**Consulta anche**

[Impostazione delle modalità di salvataggio dei documenti PDF](pdf-utilities.md#setting-pdf-document-save-modes)

[Richiamo di AEM Forms con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Creazione di un assembly client .NET che utilizza la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Pulizia dei documenti PDF {#sanitizing-pdf-documents}

È possibile utilizzare le API Java di PDF Utilities per convertire programmaticamente i documenti PDF in documenti XDP.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Utilità di PDF, consulta [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-4}

Per eliminare il documento PDF, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Crea un client PDFUtilityService.
1. Richiamare l&#39;operazione di pulizia.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Per creare un&#39;applicazione client utilizzando Java, includi i file JAR necessari.

**Creare un client PDFUtilityService**

Prima di eseguire un&#39;operazione di pulizia a livello di programmazione, è necessario creare un client PDFUtilityService. Con l’API Java, si ottiene questo risultato creando un’ `PDFUtilityServiceClient` oggetto.

**Richiamare l’operazione di conversione da PDF a XDP**

Dopo aver creato il client di servizio, è possibile richiamare l&#39;operazione di pulizia.

**Consulta anche**

[Convertire documenti PDF in documenti XDP utilizzando l’API Java](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-java-api)

[Convertire documenti PDF in documenti XDP utilizzando l’API del servizio Web](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-web-service-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Abilitare i documenti PDF tramite l’API Java {#sanitize-pdf-documents-using-the-java-api}

È possibile rimuovere i documenti utilizzando l’API di Utilità di PDF (Java):

1. Includi file di progetto

   Includi file JAR client, come adobe-pdfutility-client.jar, nel percorso classe del progetto Java.

1. Creare un client PDFUtilityService

   Crea un `PDFUtilityServiceClient` utilizzando il relativo costruttore e passando un `ServiceClientFactory` oggetto contenente le proprietà di connessione.

1. Richiamare l’operazione di conversione da PDF a XDP

   Per eseguire la conversione, richiama il `PDFUtilityServiceClient` dell’oggetto `convertPDFtoXDP` e trasmettere un `com.adobe.idp.Document` oggetto che rappresenta il file PDF. Il metodo restituisce un `com.adobe.idp.Document` oggetto che rappresenta il file XDP appena creato.

**Consulta anche**

[Rimozione dei documenti di PDF](/help/forms/developing/pdf-utilities-service-java-api.md#quick-start-soap-mode-sanitizing-pdf-documents)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
