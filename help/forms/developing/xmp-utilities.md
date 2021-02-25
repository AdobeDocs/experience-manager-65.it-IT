---
title: Utilizzo di XMP Utilities
seo-title: Utilizzo di XMP Utilities
description: Utilizzare le API Java e servizi Web di utilità XMP per importare in modo programmatico XMP metadati in un documento PDF e recuperare e salvare XMP metadati da un documento PDF.
seo-description: Utilizzare le API Java e servizi Web di utilità XMP per importare in modo programmatico XMP metadati in un documento PDF e recuperare e salvare XMP metadati da un documento PDF.
uuid: 90ce6cef-efe1-456a-8e0c-5ba90249dda0
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 01d5677f-5c87-4a6e-987b-8eda9acc0b27
translation-type: tm+mt
source-git-commit: 9cf46a26d2aa2e41b924a4de89cf8ab5fdeeefc6
workflow-type: tm+mt
source-wordcount: '1437'
ht-degree: 0%

---


# Utilizzo di XMP Utilities {#working-with-xmp-utilities}

**Esempi ed esempi in questo documento sono disponibili solo per  AEM Forms nell&#39;ambiente JEE.**

**Informazioni sul servizio Utilità XMP**

I documenti PDF contengono metadati, ossia informazioni sul documento come distinte dal contenuto del documento, ad esempio testo e grafica.  Adobe Extensible Metadata Platform (XMP) è uno standard per la gestione dei metadati del documento.

Il servizio Utilità XMP può recuperare e salvare XMP metadati dai documenti PDF e importare XMP metadati nei documenti PDF.

Potete eseguire le seguenti attività utilizzando il servizio Utilità XMP:

* Importare metadati nei documenti PDF. (Vedere [Importazione di metadati in documenti PDF](xmp-utilities.md#importing-metadata-into-pdf-documents).)
* Esportare metadati dai documenti PDF. (Vedere [Esportazione di metadati da documenti PDF](xmp-utilities.md#exporting-metadata-from-pdf-documents).)

>[!NOTE]
>
>Per ulteriori informazioni sul servizio XMP Utilities, vedere [Guida di riferimento dei servizi per  AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Importazione di metadati in documenti PDF {#importing-metadata-into-pdf-documents}

È possibile utilizzare le API Java di utilità XMP e i servizi Web per importare metadati XMP in un documento PDF a livello di programmazione. I metadati forniscono informazioni su un documento PDF, ad esempio l’autore del documento e le parole chiave correlate al documento. I metadati possono essere memorizzati nella finestra di dialogo Proprietà documento del documento, come illustrato nell&#39;illustrazione seguente.

![ww_ww_metadata_dialog](assets/ww_ww_metadatadialog.png)

Per importare i metadati in un documento PDF a livello di programmazione, è possibile utilizzare un documento XML esistente che specifica i valori dei metadati oppure utilizzare un oggetto di tipo `XMPUtilityMetadata`. (Vedere [ AEM Forms API Reference](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).)

>[!NOTE]
>
>In questa sezione viene illustrato come utilizzare un documento XML per importare metadati in un documento PDF.

Il codice XML seguente contiene i valori di metadati corrispondenti all&#39;illustrazione precedente. Ad esempio, notate gli elementi in grassetto, che specificano le parole chiave.

```xml
 <?xpacket begin="?" id="W5M0MpCehiHzreSzNTczkc9d"?>
 <x:xmpmeta xmlns:x="adobe:ns:meta/" x:xmptk="Adobe XMP Core 4.2-jc015 52.349034, 2008 Jun 20 00:30:39-PDT (debug)">
       <rdf:RDF xmlns:rdf="https://www.w3.org/1999/02/22-rdf-syntax-ns#">
          <rdf:Description rdf:about=""
                xmlns:xmp="https://ns.adobe.com/xap/1.0/">
             <xmp:MetadataDate>2008-10-22T10:52:21-04:00</xmp:MetadataDate>
             <xmp:CreatorTool>AEM Forms</xmp:CreatorTool>
             <xmp:ModifyDate>2008-10-22T10:52:21-04:00</xmp:ModifyDate>
             <xmp:CreateDate>2008-02-13T11:00:18-05:00</xmp:CreateDate>
          </rdf:Description>
          <rdf:Description rdf:about=""
                xmlns:pdf="https://ns.adobe.com/pdf/1.3/">
             <pdf:Producer>AEM Forms</pdf:Producer>
             <pdf:Keywords>keyword1, keyword2, keyword3,keyword4</pdf:Keywords>
          </rdf:Description>
          <rdf:Description rdf:about=""
                xmlns:xmpMM="https://ns.adobe.com/xap/1.0/mm/">
             <xmpMM:DocumentID>uuid:1cce1f84-331e-4d8d-8538-15441c271dd7</xmpMM:DocumentID>
             <xmpMM:InstanceID>uuid:cdda0ca6-7c91-4771-9dc9-796c8fe59350</xmpMM:InstanceID>
          </rdf:Description>
          <rdf:Description rdf:about=""
                >
             <dc:format>application/pdf</dc:format>
             <dc:description>
                <rdf:Alt>
                   <rdf:li xml:lang="x-default">Adobe Designer Sample</rdf:li>
                </rdf:Alt>
             </dc:description>
             <dc:title>
                <rdf:Alt>
                   <rdf:li xml:lang="x-default">Grant Application</rdf:li>
                </rdf:Alt>
             </dc:title>
             <dc:creator>
                <rdf:Seq>
                   <rdf:li>Tony Blue</rdf:li>
                </rdf:Seq>
             </dc:creator>
             <dc:subject>
                <rdf:Bag>
                   <rdf:li>keyword1</rdf:li>
                   <rdf:li>keyword2</rdf:li>
                   <rdf:li>keyword3</rdf:li>
                   <rdf:li>keyword4</rdf:li>
                </rdf:Bag>
             </dc:subject>
          </rdf:Description>
          <rdf:Description rdf:about=""
                xmlns:desc="https://ns.adobe.com/xfa/promoted-desc/">
             <desc:version rdf:parseType="Resource">
                <rdf:value>1.0</rdf:value>
                <desc:ref>/template/subform[1]</desc:ref>
             </desc:version>
             <desc:contact rdf:parseType="Resource">
                <rdf:value>Adobe Systems Incorporated</rdf:value>
                <desc:ref>/template/subform[1]</desc:ref>
             </desc:contact>
          </rdf:Description>
       </rdf:RDF>
 </x:xmpmeta>
```

>[!NOTE]
>
>Per ulteriori informazioni sul servizio XMP Utilities, vedere [Guida di riferimento dei servizi per  AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary-of-steps}

Per importare XMP metadati in un documento PDF, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Create un client XMPUtilityService.
1. Richiamate l’operazione di importazione dei metadati XMP.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, accertatevi di includere i file proxy.

**Creare un client XMPUtilityService**

Prima di eseguire un&#39;operazione Utilità XMP a livello di programmazione, è necessario creare un client XMPUtilityService. Con l&#39;API Java, ciò viene ottenuto creando un oggetto `XMPUtilityServiceClient`. Con l&#39;API del servizio Web, ciò viene ottenuto utilizzando un oggetto `XMPUtilityServiceService`.

**Richiamo dell’operazione di importazione dei metadati XMP**

Dopo aver creato il client del servizio, potete richiamare una delle operazioni di importazione dei metadati XMP per importare i metadati XMP nel documento PDF specificato.

**Consulta anche**

[Importare metadati XMP tramite l&#39;API Java](xmp-utilities.md#import-xmp-metadata-using-the-java-api)

[Importazione di metadati XMP tramite l&#39;API del servizio Web](xmp-utilities.md#importing-xmp-metadata-using-the-web-service-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Importare XMP metadati utilizzando l&#39;API Java {#import-xmp-metadata-using-the-java-api}

Importare XMP metadati utilizzando l&#39;API XMP Utilities (Java):

1. Includi file di progetto

   Includete file JAR client, ad esempio adobe-pdfutility-client.jar, nel percorso di classe del progetto Java.

   >[!NOTE]
   >
   >Il file adobe-pdfutility-client.jar contiene classi che consentono di richiamare il servizio Utilità XMP a livello di programmazione.

1. Creare un client XMPUtilityService

   Creare un oggetto `XMPUtilityServiceClient` utilizzando il relativo costruttore e passando un oggetto `ServiceClientFactory` che contiene proprietà di connessione.

1. Richiamo dell’operazione di importazione dei metadati XMP

   Per modificare i metadati XMP, invocare il metodo `XMPUtilityServiceClient` dell&#39;oggetto `importMetadata` o il relativo metodo `importXMP`.

   Se si utilizza il metodo `importMetadata`, trasmettere i valori seguenti:

   * Un oggetto `com.adobe.idp.Document` che rappresenta il file PDF.
   * Un oggetto `XMPUtilityMetadata` che contiene i metadati da importare.

   Se si utilizza il metodo `importXMP`, trasmettere i valori seguenti:

   * Un oggetto `com.adobe.idp.Document` che rappresenta il file PDF.
   * Un oggetto `com.adobe.idp.Document` che rappresenta un file XML contenente i metadati da importare.

   In entrambi i casi, il valore restituito è un oggetto `com.adobe.idp.Document` che rappresenta il file PDF con i metadati appena importati. È quindi possibile salvare l&#39;oggetto sul disco.

**Consulta anche**

[Importazione di metadati in documenti PDF](xmp-utilities.md#importing-metadata-into-pdf-documents)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Importazione di metadati XMP tramite l&#39;API del servizio Web {#importing-xmp-metadata-using-the-web-service-api}

Per importare i metadati XMP a livello di programmazione tramite l&#39;API del servizio Web XMP Utilities, effettuate le seguenti operazioni:

1. Includi file di progetto

   * Creare un assembly client Microsoft .NET che utilizzi il file WSDL del servizio Utilità XMP. (Vedere [Richiamo  AEM Forms con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).)
   * Fare riferimento all&#39;assembly client Microsoft .NET. (Vedere [Creazione di un assembly client .NET che utilizza la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding).)

1. Creare un client XMPUtilityService

   Creare un oggetto `XMPUtilityServiceService` utilizzando il costruttore della classe proxy.

1. Richiamo dell’operazione di importazione dei metadati XMP

   Per modificare i metadati XMP, invocare il metodo `XMPUtilityServiceService` dell&#39;oggetto `importMetadata` o il relativo metodo `importXMP`.

   Se si utilizza il metodo `importMetadata`, trasmettere i valori seguenti:

   * Un oggetto `BLOB` che rappresenta il file PDF.
   * Un oggetto `XMPUtilityMetadata` che contiene i metadati da importare.

   Se si utilizza il metodo `importXMP`, trasmettere i valori seguenti:

   * Un oggetto `BLOB` che rappresenta il file PDF.
   * Un oggetto `BLOB` che rappresenta un file XML contenente i metadati da importare.

   In entrambi i casi, il valore restituito è un oggetto `BLOB` che rappresenta il file PDF con i metadati appena importati. È quindi possibile salvare l&#39;oggetto sul disco.

**Consulta anche**

[Importazione di metadati in documenti PDF](xmp-utilities.md#importing-metadata-into-pdf-documents)

<!--REVIEW: [Quick Start (Base64): Importing XMP metadata using the web service API](unresolvedlink-lc-qs-xmp-utilities-xu.xml#ws624e3cba99b79e12e69a9941333732bac8-7be8.2)-->

[Richiamo  AEM Forms con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Creazione di un assembly client .NET che utilizza la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Esportazione di metadati da documenti PDF {#exporting-metadata-from-pdf-documents}

È possibile utilizzare le API Java XMP Utilities e i servizi Web per recuperare e salvare in modo programmatico i metadati XMP da un documento PDF.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio XMP Utilities, vedere [Guida di riferimento dei servizi per  AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-1}

Per esportare XMP metadati da un documento PDF, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Create un client XMPUtilityService.
1. Richiamate l’operazione di esportazione dei metadati XMP.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, accertatevi di includere i file proxy.

**Creare un client XMPUtilityService**

Prima di eseguire un&#39;operazione Utilità XMP a livello di programmazione, è necessario creare un client XMPUtilityService. Con l&#39;API Java, se questo viene realizzato creando un oggetto `XMPUtilityServiceClient`. Con l&#39;API del servizio Web, questo viene eseguito utilizzando un oggetto `XMPUtilityServiceService`.

**Richiamo dell’operazione di esportazione dei metadati XMP**

Dopo aver creato il client del servizio, potete richiamare una delle operazioni di esportazione dei metadati XMP, che possono essere utilizzate per ispezionare i metadati XMP o salvarli su disco.

**Consulta anche**

[Importare metadati XMP tramite l&#39;API Java](xmp-utilities.md#import-xmp-metadata-using-the-java-api)

[Importazione di metadati XMP tramite l&#39;API del servizio Web](xmp-utilities.md#importing-xmp-metadata-using-the-web-service-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Esportare XMP metadati utilizzando l&#39;API Java {#export-xmp-metadata-using-the-java-api}

Esportate XMP metadati utilizzando l&#39;API XMP Utilities (Java):

1. Includi file di progetto

   Includete file JAR client, ad esempio adobe-pdfutility-client.jar, nel percorso di classe del progetto Java.

   >[!NOTE]
   >
   >Il file adobe-pdfutility-client.jar contiene classi che consentono di richiamare il servizio Utility XMP a livello di programmazione.

1. Creare un client XMPUtilityService

   Creare un oggetto `XMPUtilityServiceClient` utilizzando il relativo costruttore e passando un oggetto `ServiceClientFactory` che contiene proprietà di connessione.

1. Richiamo dell’operazione di importazione dei metadati XMP

   Per esaminare i metadati XMP, richiamare il metodo `exportMetadata` dell&#39;oggetto `com.adobe.idp.Document` e passare un oggetto `XMPUtilityServiceClient` che rappresenta il file PDF. Il metodo restituisce un oggetto `XMPUtilityMetadata` che contiene i metadati recuperati.

   Per recuperare e salvare i metadati XMP, richiamare il metodo `exportXMP` dell&#39;oggetto `com.adobe.idp.Document` e trasmettere un oggetto `XMPUtilityServiceClient` che rappresenta il file PDF. Il metodo restituisce un oggetto `com.adobe.idp.Document` che contiene i metadati recuperati, che potete successivamente salvare su disco come file XML.

**Consulta anche**

[Esportazione di metadati da documenti PDF](xmp-utilities.md#exporting-metadata-from-pdf-documents)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Esportare XMP metadati utilizzando l&#39;API del servizio Web {#export-xmp-metadata-using-the-web-service-api}

Esportate XMP metadati utilizzando l&#39;API XMP Utilities (servizio Web):

1. Includi file di progetto

   * Creare un assembly client Microsoft .NET che utilizzi il file WSDL del servizio Utilità XMP.
   * Fare riferimento all&#39;assembly client Microsoft .NET.

1. Creare un client XMPUtilityService

   Creare un oggetto `XMPUtilityServiceService` utilizzando il costruttore della classe proxy.

1. Richiamo dell’operazione di importazione dei metadati XMP

   Per esaminare i metadati XMP, richiamare il metodo `exportMetadata` dell&#39;oggetto `BLOB` e passare un oggetto `XMPUtilityServiceClient` che rappresenta il file PDF. Il metodo restituisce un oggetto `XMPUtilityMetadata` che contiene i metadati recuperati.

   Per recuperare e salvare i metadati XMP, richiamare il metodo `exportXMP` dell&#39;oggetto `BLOB` e trasmettere un oggetto `XMPUtilityServiceClient` che rappresenta il file PDF. Il metodo restituisce un oggetto `BLOB` che contiene i metadati recuperati, che potete successivamente salvare su disco come file XML.

**Consulta anche**

[Esportazione di metadati da documenti PDF](xmp-utilities.md#exporting-metadata-from-pdf-documents)

[Richiamo  AEM Forms con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Creazione di un assembly client .NET che utilizza la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)
