---
title: Utilizzo delle utility PDF
seo-title: Utilizzo delle utility PDF
description: 'null'
seo-description: 'null'
uuid: a2ea2359-c547-4f1b-b6ca-f276f816e36a
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: d816bf2e-5236-4084-b7c4-c32b72cdff97
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '2548'
ht-degree: 1%

---


# Utilizzo delle utility PDF {#working-with-pdf-utilities}

**Informazioni sul servizio Utilità PDF**

Il servizio Utilità PDF consente di convertire i formati di file PDF e XDP, impostare e recuperare le proprietà del documento PDF e manipolare XMP metadati. Ad esempio, prima di convertire un documento PDF in un altro formato, è utile controllarne le proprietà per determinare quale operazione del servizio richiamare per la conversione.

È possibile eseguire le seguenti operazioni utilizzando il servizio Utilità PDF:

* Convertire i documenti PDF in documenti XDP.
* Convertire documenti XDP in documenti PDF. (Vedere [Conversione di documenti XDP in documenti PDF](pdf-utilities.md#converting-xdp-documents-into-pdf-documents).)
* Recuperare le proprietà del documento PDF. (Vedere [Recupero delle proprietà del documento PDF](pdf-utilities.md#retrieving-pdf-document-properties).)
* Salvate un documento PDF e ottimizzatelo per una visualizzazione Web rapida. (Vedere [Impostazione delle modalità di salvataggio dei documenti PDF](pdf-utilities.md#setting-pdf-document-save-modes).)

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Utilità PDF, vedere [Guida di riferimento dei servizi per  AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Conversione di documenti PDF in documenti XDP {#converting-pdf-documents-into-xdp-documents}

È possibile utilizzare le API Java di utilità PDF e i servizi Web per convertire i documenti PDF in documenti XDP a livello di programmazione.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Utilità PDF, vedere [Guida di riferimento dei servizi per  AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary-of-steps}

Per convertire un documento PDF in un documento XDP, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un client PDFUtilityService.
1. Richiamare l&#39;operazione di conversione da PDF a XDP.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, accertatevi di includere i file proxy.

**Creare un client PDFUtilityService**

Prima di eseguire un&#39;operazione Utilità PDF a livello di programmazione, è necessario creare un client PDFUtilityService. Con l&#39;API Java, ciò viene ottenuto creando un oggetto `PDFUtilityServiceClient`. Con l&#39;API del servizio Web, ciò viene ottenuto utilizzando un oggetto `PDFUtilityServiceService`.

**Richiamo dell&#39;operazione di conversione da PDF a XDP**

Dopo aver creato il client del servizio, è possibile richiamare l&#39;operazione di conversione da PDF a XDP.

**Consulta anche**

[Conversione di documenti PDF in documenti XDP mediante l&#39;API Java](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-java-api)

[Conversione di documenti PDF in documenti XDP tramite l&#39;API del servizio Web](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-web-service-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Convertire documenti PDF in documenti XDP utilizzando l&#39;API Java {#convert-pdf-documents-into-xdp-documents-using-the-java-api}

Convertite i documenti PDF in documenti XDP utilizzando l&#39;API PDF Utilities (Java):

1. Includi file di progetto

   Includete file JAR client, ad esempio adobe-pdfutility-client.jar, nel percorso di classe del progetto Java.

1. Creare un client PDFUtilityService

   Creare un oggetto `PDFUtilityServiceClient` utilizzando il relativo costruttore e passando un oggetto `ServiceClientFactory` che contiene proprietà di connessione.

1. Richiamo dell&#39;operazione di conversione da PDF a XDP

   Per eseguire la conversione, richiamare il metodo `convertPDFtoXDP` dell&#39;oggetto `PDFUtilityServiceClient` e trasmettere un oggetto `com.adobe.idp.Document` che rappresenta il file PDF. Il metodo restituisce un oggetto `com.adobe.idp.Document` che rappresenta il file XDP appena creato.

**Consulta anche**

[Conversione di documenti PDF in documenti XDP](pdf-utilities.md#converting-pdf-documents-into-xdp-documents)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Convertire documenti PDF in documenti XDP utilizzando l&#39;API del servizio Web {#convert-pdf-documents-into-xdp-documents-using-the-web-service-api}

Convertite i documenti PDF in documenti XDP utilizzando l&#39;API Utilità PDF (servizio Web):

1. Includi file di progetto

   * Creare un assembly client Microsoft .NET che utilizzi il file WSDL del servizio Utilità PDF.
   * Fare riferimento all&#39;assembly client Microsoft .NET.

1. Creare un client PDFUtilityService

   Creare un oggetto `PDFUtilityServiceService` utilizzando il costruttore della classe proxy.

1. Richiamo dell&#39;operazione di conversione da PDF a XDP

   Richiamare il metodo `PDFUtilityServiceService` dell&#39;oggetto `convertPDFtoXDP` e trasmettere un oggetto `BLOB` che rappresenta il file PDF. Il metodo restituisce un oggetto `BLOB` che rappresenta il file XDP appena creato.

**Consulta anche**

[Conversione di documenti PDF in documenti XDP](pdf-utilities.md#converting-pdf-documents-into-xdp-documents)

[Richiamo  AEM Forms con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Creazione di un assembly client .NET che utilizza la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Conversione di documenti XDP in documenti PDF {#converting-xdp-documents-into-pdf-documents}

È possibile utilizzare le API Java di utilità PDF e i servizi Web per convertire i documenti XDP in documenti PDF a livello di programmazione.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Utilità PDF, vedere [Guida di riferimento dei servizi per  AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-1}

Per convertire un documento XDP in un documento PDF, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un client PDFUtilityService.
1. Richiamare l&#39;operazione di conversione XDP in PDF.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, accertatevi di includere i file proxy.

**Creare un client PDFUtilityService**

Prima di eseguire un&#39;operazione Utilità PDF a livello di programmazione, è necessario creare un client PDFUtilityService. Con l&#39;API Java, ciò viene ottenuto creando un oggetto `PDFUtilityServiceClient`. Con l&#39;API del servizio Web, ciò viene ottenuto utilizzando un oggetto `PDFUtilityServiceService`.

**Richiamo dell&#39;operazione di conversione da XDP a PDF**

Dopo aver creato il client del servizio, potete richiamare l&#39;operazione di conversione da XDP a PDF.

**Consulta anche**

[Conversione di documenti XDP in documenti PDF tramite l&#39;API Java](pdf-utilities.md#convert-xdp-documents-into-pdf-documents-using-the-java-api)

[Conversione di documenti XDP in documenti PDF tramite l&#39;API del servizio Web](pdf-utilities.md#converting-xdp-documents-into-pdf-documents-using-the-web-service-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Convertire documenti XDP in documenti PDF utilizzando l&#39;API Java {#convert-xdp-documents-into-pdf-documents-using-the-java-api}

Convertite i documenti XDP in documenti PDF utilizzando l&#39;API PDF Utilities (Java):

1. Includi file di progetto

   Includete file JAR client, ad esempio adobe-pdfutility-client.jar, nel percorso di classe del progetto Java.

1. Creare un client PDFUtilityService

   Creare un oggetto `PDFUtilityServiceClient` utilizzando il relativo costruttore e passando un oggetto `ServiceClientFactory` che contiene proprietà di connessione.

1. Richiamo dell&#39;operazione di conversione da XDP a PDF

   Per eseguire la conversione, richiamare il metodo `convertXDPtoPDF` dell&#39;oggetto `PDFUtilityServiceClient` e trasmettere un oggetto `com.adobe.idp.Document` che rappresenta il file XDP. Il metodo restituisce un oggetto `com.adobe.idp.Document` che rappresenta il file PDF appena creato.

**Consulta anche**

[Conversione di documenti XDP in documenti PDF](pdf-utilities.md#converting-xdp-documents-into-pdf-documents)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Conversione di documenti XDP in documenti PDF tramite l&#39;API del servizio Web {#converting-xdp-documents-into-pdf-documents-using-the-web-service-api}

Convertite i documenti XDP in documenti PDF utilizzando l&#39;API di utilità PDF (Web Service API):

1. Includi file di progetto

   * Creare un assembly client Microsoft .NET che utilizzi il file WSDL del servizio Utilità PDF.
   * Fare riferimento all&#39;assembly client Microsoft .NET.

1. Creare un client PDFUtilityService

   Creare un oggetto `PDFUtilityServiceService` utilizzando il costruttore della classe proxy.

1. Richiamo dell&#39;operazione di conversione da XDP a PDF

   Per eseguire la conversione, richiamare il metodo `convertXDPtoPDF` dell&#39;oggetto `PDFUtilityServiceService` e trasmettere un oggetto `BLOB` che rappresenta il file XDP. Il metodo restituisce un oggetto `BLOB` che rappresenta il file PDF appena creato.

**Consulta anche**

[Conversione di documenti XDP in documenti PDF](pdf-utilities.md#converting-xdp-documents-into-pdf-documents)

[Richiamo  AEM Forms con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Creazione di un assembly client .NET che utilizza la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Recupero delle proprietà del documento PDF {#retrieving-pdf-document-properties}

È possibile utilizzare le API Java di utilità PDF e le API dei servizi Web per recuperare in modo programmatico le proprietà del documento PDF, ad esempio se il documento è un modulo compilabile o la versione minima  Acrobat necessaria per leggere il documento.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Utilità PDF, vedere [Guida di riferimento dei servizi per  AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)

### Riepilogo dei passaggi {#summary_of_steps-2}

Per recuperare le proprietà del documento PDF, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un client PDFUtilityService.
1. Richiamare l&#39;operazione di recupero delle proprietà.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, accertatevi di includere i file proxy.

**Creare un client PDFUtilityService**

Prima di eseguire un&#39;operazione Utilità PDF a livello di programmazione, è necessario creare un client PDFUtilityService. Con l&#39;API Java, ciò viene ottenuto creando un oggetto `PDFUtilityServiceClient`. Con l&#39;API del servizio Web, questo viene eseguito utilizzando un oggetto `PDFUtilityServiceService`.

**Richiamo dell&#39;operazione di recupero delle proprietà**

Dopo aver creato il client del servizio, potete richiamare l&#39;operazione di recupero delle proprietà.

**Consulta anche**

[Recupero delle proprietà del documento PDF tramite l&#39;API Java](pdf-utilities.md#retrieve-pdf-document-properties-using-the-java-api)

[Recupero delle proprietà del documento PDF tramite l&#39;API del servizio Web](pdf-utilities.md#retrieve-pdf-document-properties-using-the-web-service-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Recuperare le proprietà del documento PDF utilizzando l&#39;API Java {#retrieve-pdf-document-properties-using-the-java-api}

Recuperare le proprietà del documento PDF utilizzando l&#39;API PDF Utilities (Java):

1. Includi file di progetto

   Includete file JAR client, ad esempio adobe-pdfutility-client.jar, nel percorso di classe del progetto Java.

1. Creare un client PDFUtilityService

   Creare un oggetto `PDFUtilityServiceClient` utilizzando il relativo costruttore e passando un oggetto `ServiceClientFactory` che contiene proprietà di connessione.

1. Richiamo dell&#39;operazione di recupero delle proprietà

   Per eseguire la conversione, richiamare il metodo `PDFUtilityServiceClient` dell&#39;oggetto `getPDFProperties` e passare quanto segue:

   * Un oggetto `com.adobe.idp.Document` che rappresenta il documento PDF.
   * Un oggetto `PDFPropertiesOptionSpec` che contiene le proprietà da valutare.

   Il metodo restituisce un oggetto `PDFPropertiesResult` che contiene i risultati della query.

**Consulta anche**

[Recupero delle proprietà del documento PDF](pdf-utilities.md#retrieving-pdf-document-properties)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Recupero delle proprietà del documento PDF tramite l&#39;API del servizio Web {#retrieve-pdf-document-properties-using-the-web-service-api}

Recuperare le proprietà del documento PDF utilizzando l&#39;API del servizio Web Utilità PDF:

1. Includi file di progetto

   * Creare un assembly client Microsoft .NET che utilizzi il file WSDL del servizio Utilità PDF.
   * Fare riferimento all&#39;assembly client Microsoft .NET.

1. Creare un client PDFUtilityService

   Creare un oggetto `PDFUtilityServiceService` utilizzando il costruttore della classe proxy.

1. Richiamo dell&#39;operazione di recupero delle proprietà

   Per eseguire la conversione, richiamare il metodo `PDFUtilityServiceService` dell&#39;oggetto `getPDFProperties` e passare quanto segue:

   * Un oggetto `BLOB` che rappresenta il documento PDF.
   * Un oggetto `PDFPropertiesOptionSpec` che contiene le proprietà da valutare.

   Il metodo restituisce un oggetto `PDFPropertiesResult` che contiene i risultati della query.

**Consulta anche**

[Recupero delle proprietà del documento PDF](pdf-utilities.md#retrieving-pdf-document-properties)

[Richiamo  AEM Forms con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Creazione di un assembly client .NET che utilizza la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Impostazione delle modalità di salvataggio documenti PDF {#setting-pdf-document-save-modes}

È possibile utilizzare Java del servizio Utilità PDF e le API del servizio Web per impostare in modo programmatico una modalità di salvataggio per un documento PDF. Quando si utilizza il servizio Utilità PDF per impostare una modalità di salvataggio, il servizio Utilità PDF imposta solo la modalità di salvataggio e non salva il documento PDF. Il documento PDF viene salvato quando viene passato a un&#39;altra operazione del servizio. Ad esempio, è possibile utilizzare il servizio Utilità PDF per impostare una modalità di salvataggio specifica e passarla al servizio di cifratura, in cui il documento PDF viene effettivamente salvato e cifrato.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Utilità PDF, vedere [Guida di riferimento dei servizi per  AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-3}

Per impostare l&#39;opzione Salva per i documenti PDF, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un client PDFUtilityService.
1. Impostare la modalità di salvataggio.
1. Richiama l’operazione di salvataggio.
1. Passare il documento PDF a un&#39;altra operazione.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, accertatevi di includere i file proxy.

**Creare un client PDFUtilityService**

Prima di eseguire un&#39;operazione Utilità PDF a livello di programmazione, è necessario creare un client PDFUtilityService. Con l&#39;API Java, ciò viene ottenuto creando un oggetto `PDFUtilityServiceClient`. Con l&#39;API del servizio Web, questo viene eseguito utilizzando un oggetto `PDFUtilityServiceService`.

**Impostare la modalità Salva**

Potete scegliere una delle seguenti opzioni di salvataggio:

* `INCREMENTAL`: Per risparmiare in modo incrementale per ridurre il tempo necessario per risparmiare
* `FAST_WEB_VIEW`: salvare per una visualizzazione Web rapida
* `FULL`: Per risparmiare utilizzando un salvataggio completo (senza ottimizzazione)

**Richiamo dell&#39;operazione di salvataggio dello stile**

Dopo aver creato il client del servizio, potete richiamare l&#39;operazione di recupero delle proprietà.

**Trasmettere il documento PDF a un&#39;altra operazione  AEM Forms**

Dopo che il servizio Utilità PDF ha impostato la modalità di salvataggio specificata, passare il documento PDF a un&#39;altra operazione AEM Forms . Una volta restituito da tale operazione, il documento PDF viene salvato nella modalità specificata. Ad esempio, se si utilizza il servizio Utilità PDF per impostare la modalità `FAST_WEB_VIEW` e quindi passare il documento PDF all&#39;operazione `encryptUsingPassword` del servizio di cifratura, il documento PDF restituito viene cifrato con una password e salvato in modalità `FAST_WEB_VIEW`.

>[!NOTE]
>
>La sezione Avvio rapido associata a questa sezione imposta la modalità `FAST_WEB_VIEW` e quindi passa il documento PDF all&#39;operazione `encryptUsingPassword` del servizio di cifratura.

**Consulta anche**

[Impostazione delle opzioni di salvataggio dei documenti PDF tramite l&#39;API Java](pdf-utilities.md#set-pdf-document-save-options-using-the-java-api)

[Impostazione delle opzioni di salvataggio dei documenti PDF tramite l&#39;API del servizio Web](pdf-utilities.md#set-pdf-document-save-options-using-the-web-service-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Cifratura di documenti PDF con una password](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Impostare le opzioni di salvataggio dei documenti PDF utilizzando l&#39;API Java {#set-pdf-document-save-options-using-the-java-api}

Per impostare le opzioni di salvataggio del documento PDF, utilizzare l&#39;API PDF Utilities (Java):

1. Includi file di progetto

   Includete file JAR client, ad esempio adobe-pdfutility-client.jar, nel percorso di classe del progetto Java.

1. Creare un client PDFUtilityService

   Creare un oggetto `PDFUtilityServiceClient` utilizzando il relativo costruttore e passando un oggetto `ServiceClientFactory` che contiene proprietà di connessione.

1. Impostare la modalità Salva

   * Creare un oggetto `PDFUtilitySaveMode` utilizzando il relativo costruttore.
   * Impostare la modalità di salvataggio richiamando il metodo `PDFUtilitySaveMode` dell&#39;oggetto `setSaveStyle` e passando un valore di stringa che specifica la modalità di salvataggio. Ad esempio, per salvare la visualizzazione Web in modo rapido, passare `FAST_WEB_VIEW`.

1. Richiamo dell&#39;operazione di salvataggio dello stile

   Richiamare il metodo `PDFUtilityServiceClient` dell&#39;oggetto `setSaveMode` e trasmettere i seguenti valori:

   * Un oggetto `com.adobe.idp.Document` che rappresenta il documento PDF.
   * Un oggetto `PDFUtilitySaveMode` che contiene lo stile di salvataggio da utilizzare.
   * Un valore booleano utilizzato per determinare se ignorare eventuali impostazioni precedenti.

   Il metodo restituisce un oggetto `com.adobe.idp.Document` formattato utilizzando lo stile di salvataggio specificato.

1. Trasmettere il documento PDF a un&#39;altra operazione  AEM Forms

   * Passa l&#39;oggetto `com.adobe.idp.Document` restituito a un&#39;altra operazione AEM Forms .

**Consulta anche**

[Impostazione delle modalità di salvataggio dei documenti PDF](pdf-utilities.md#setting-pdf-document-save-modes)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Impostazione delle opzioni di salvataggio dei documenti PDF tramite l&#39;API del servizio Web {#set-pdf-document-save-options-using-the-web-service-api}

Per impostare le opzioni di salvataggio del documento PDF, utilizzare l&#39;API Utilità PDF (servizio Web):

1. Includi file di progetto

   * Creare un assembly client Microsoft .NET che utilizzi il file WSDL del servizio Utilità PDF.
   * Fare riferimento all&#39;assembly client Microsoft .NET.

1. Creare un client PDFUtilityService

   Creare un oggetto `PDFUtilityServiceService` utilizzando il costruttore della classe proxy.

1. Impostare la modalità Salva

   * Creare un oggetto `PDFUtilitySaveMode` utilizzando il relativo costruttore.
   * Impostare la modalità di salvataggio assegnando un valore stringa al metodo `PDFUtilitySaveMode` dell&#39;oggetto &lt;a1/> che specifica la modalità di salvataggio. `saveStyle` Ad esempio, per salvare la visualizzazione Web in modo rapido, specificate `FAST_WEB_VIEW`.

1. Richiamo dell&#39;operazione di salvataggio dello stile

   Richiamare il metodo `PDFUtilityServiceService` dell&#39;oggetto `setSaveMode` e trasmettere i seguenti valori:

   * Un oggetto `BLOB` che rappresenta il documento PDF.
   * Un oggetto `PDFUtilitySaveMode` che contiene lo stile di salvataggio da utilizzare.
   * Un valore booleano utilizzato per determinare se ignorare eventuali impostazioni precedenti.

   Il metodo restituisce un oggetto `BLOB` formattato utilizzando lo stile di salvataggio specificato. È quindi possibile salvare l&#39;oggetto come documento PDF.

1. Trasmettere il documento PDF a un&#39;altra operazione Forms

   * Passa l&#39;oggetto `BLOB` restituito a un&#39;altra operazione AEM Forms .

**Consulta anche**

[Impostazione delle modalità di salvataggio dei documenti PDF](pdf-utilities.md#setting-pdf-document-save-modes)

[Richiamo  AEM Forms con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Creazione di un assembly client .NET che utilizza la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Rimozione di informazioni riservate sui documenti PDF {#sanitizing-pdf-documents}

È possibile utilizzare le API Java di Utilità PDF per convertire i documenti PDF in documenti XDP a livello di programmazione.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Utilità PDF, vedere [Guida di riferimento dei servizi per  AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-4}

Per rimuovere completamente il documento PDF, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un client PDFUtilityService.
1. Richiamate l&#39;operazione di pulizia.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Per creare un&#39;applicazione client utilizzando Java, includete i file JAR necessari.

**Creare un client PDFUtilityService**

Prima di eseguire un&#39;operazione di pulizia a livello di programmazione, è necessario creare un client PDFUtilityService. Con l&#39;API Java, ciò viene ottenuto creando un oggetto `PDFUtilityServiceClient`.

**Richiamo dell&#39;operazione di conversione da PDF a XDP**

Dopo aver creato il client del servizio, potete richiamare l&#39;operazione di pulizia.

**Consulta anche**

[Conversione di documenti PDF in documenti XDP mediante l&#39;API Java](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-java-api)

[Conversione di documenti PDF in documenti XDP tramite l&#39;API del servizio Web](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-web-service-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Rimozione di informazioni riservate sui documenti PDF mediante l&#39;API Java {#sanitize-pdf-documents-using-the-java-api}

Rimozione di informazioni riservate sui documenti mediante l&#39;API PDF Utilities (Java):

1. Includi file di progetto

   Includete file JAR client, ad esempio adobe-pdfutility-client.jar, nel percorso di classe del progetto Java.

1. Creare un client PDFUtilityService

   Creare un oggetto `PDFUtilityServiceClient` utilizzando il relativo costruttore e passando un oggetto `ServiceClientFactory` che contiene proprietà di connessione.

1. Richiamo dell&#39;operazione di conversione da PDF a XDP

   Per eseguire la conversione, richiamare il metodo `convertPDFtoXDP` dell&#39;oggetto `PDFUtilityServiceClient` e trasmettere un oggetto `com.adobe.idp.Document` che rappresenta il file PDF. Il metodo restituisce un oggetto `com.adobe.idp.Document` che rappresenta il file XDP appena creato.

**Consulta anche**

[Rimozione di informazioni riservate sui documenti PDF](/help/forms/developing/pdf-utilities-service-java-api.md#quick-start-soap-mode-sanitizing-pdf-documents)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
