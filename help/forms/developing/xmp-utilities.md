---
title: Utilizzo delle utility XMP
seo-title: Utilizzo delle utility XMP
description: 'null'
seo-description: 'null'
uuid: 90ce6cef-efe1-456a-8e0c-5ba90249dda0
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 01d5677f-5c87-4a6e-987b-8eda9acc0b27
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '1369'
ht-degree: 1%

---


# Utilizzo delle utility XMP {#working-with-xmp-utilities}

**Informazioni sul servizio Utilità XMP**

I documenti PDF contengono metadati, ossia informazioni sul documento come distinte dal contenuto del documento, ad esempio testo e grafica. Adobe Extensible Metadata Platform (XMP) è uno standard per la gestione dei metadati del documento.

Il servizio Utilità XMP può recuperare e salvare i metadati XMP dai documenti PDF e importare i metadati XMP nei documenti PDF.

Potete eseguire le seguenti attività utilizzando il servizio Utilità XMP:

* Importare metadati nei documenti PDF. Consultate [Importazione di metadati in documenti](xmp-utilities.md#importing-metadata-into-pdf-documents)PDF.
* Esportare metadati dai documenti PDF. Consultate [Esportazione di metadati da documenti](xmp-utilities.md#exporting-metadata-from-pdf-documents)PDF.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Utilità XMP, consultate Riferimento [servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Importazione di metadati in documenti PDF {#importing-metadata-into-pdf-documents}

Potete utilizzare le API Java di utilità XMP e i servizi Web per importare i metadati XMP in un documento PDF a livello di programmazione. I metadati forniscono informazioni su un documento PDF, ad esempio l’autore del documento e le parole chiave correlate al documento. I metadati possono essere memorizzati nella finestra di dialogo Proprietà documento del documento, come illustrato nell&#39;illustrazione seguente.

![ww_ww_metadata_dialog](assets/ww_ww_metadatadialog.png)

Per importare i metadati in un documento PDF a livello di programmazione, è possibile utilizzare un documento XML esistente che specifica i valori dei metadati oppure utilizzare un oggetto di tipo `XMPUtilityMetadata`. Consultate Riferimento API per [AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

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
>Per ulteriori informazioni sul servizio Utilità XMP, consultate Riferimento [servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary-of-steps}

Per importare metadati XMP in un documento PDF, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Create un client XMPUtilityService.
1. Richiamate l’operazione di importazione dei metadati XMP.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, accertatevi di includere i file proxy.

**Creare un client XMPUtilityService**

Prima di eseguire un&#39;operazione XMP Utilities in modo programmatico, è necessario creare un client XMPUtilityService. Con l&#39;API Java, ciò viene ottenuto creando un `XMPUtilityServiceClient` oggetto. Con l&#39;API del servizio Web, questo viene ottenuto utilizzando un `XMPUtilityServiceService` oggetto.

**Richiamo dell’operazione di importazione dei metadati XMP**

Dopo aver creato il client del servizio, potete richiamare una delle operazioni di importazione dei metadati XMP per importare i metadati XMP nel documento PDF specificato.

**Consulta anche**

[Importare metadati XMP tramite l&#39;API Java](xmp-utilities.md#import-xmp-metadata-using-the-java-api)

[Importazione di metadati XMP tramite l&#39;API del servizio Web](xmp-utilities.md#importing-xmp-metadata-using-the-web-service-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Importare metadati XMP tramite l&#39;API Java {#import-xmp-metadata-using-the-java-api}

Importare metadati XMP utilizzando l&#39;API XMP Utilities (Java):

1. Includi file di progetto

   Includete file JAR client, ad esempio adobe-pdfutility-client.jar, nel percorso di classe del progetto Java.

   >[!NOTE]
   >
   >Il file adobe-pdfutility-client.jar contiene classi che consentono di richiamare il servizio Utilità XMP a livello di programmazione.

1. Creare un client XMPUtilityService

   Creare un `XMPUtilityServiceClient` oggetto utilizzando il relativo costruttore e passando un `ServiceClientFactory` oggetto che contiene le proprietà di connessione.

1. Richiamo dell’operazione di importazione dei metadati XMP

   Per modificare i metadati XMP, richiamate il metodo dell&#39; `XMPUtilityServiceClient` oggetto `importMetadata` o il relativo `importXMP` metodo.

   Se utilizzate il `importMetadata` metodo, inserite i seguenti valori:

   * Un `com.adobe.idp.Document` oggetto che rappresenta il file PDF.
   * Un `XMPUtilityMetadata` oggetto che contiene i metadati da importare.

   Se utilizzate il `importXMP` metodo, inserite i seguenti valori:

   * Un `com.adobe.idp.Document` oggetto che rappresenta il file PDF.
   * Un `com.adobe.idp.Document` oggetto che rappresenta un file XML contenente i metadati da importare.

   In entrambi i casi, il valore restituito è un `com.adobe.idp.Document` oggetto che rappresenta il file PDF con i nuovi metadati importati. È quindi possibile salvare l&#39;oggetto sul disco.

**Consulta anche**

[Importazione di metadati in documenti PDF](xmp-utilities.md#importing-metadata-into-pdf-documents)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Importazione di metadati XMP tramite l&#39;API del servizio Web {#importing-xmp-metadata-using-the-web-service-api}

Per importare i metadati XMP a livello di programmazione utilizzando l&#39;API del servizio Web Utilità XMP, effettuate le seguenti operazioni:

1. Includi file di progetto

   * Create un assembly client Microsoft .NET che utilizzi il file WSDL del servizio Utilità XMP. Consultate [Invocazione di AEM Forms con codifica](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)Base64.
   * Fare riferimento all&#39;assembly client Microsoft .NET. (Vedere [Creazione di un assembly client .NET che utilizza la codifica](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)Base64.)

1. Creare un client XMPUtilityService

   Creare un `XMPUtilityServiceService` oggetto utilizzando il costruttore della classe proxy.

1. Richiamo dell’operazione di importazione dei metadati XMP

   Per modificare i metadati XMP, richiamate il metodo dell&#39; `XMPUtilityServiceService` oggetto `importMetadata` o il relativo `importXMP` metodo.

   Se utilizzate il `importMetadata` metodo, inserite i seguenti valori:

   * Un `BLOB` oggetto che rappresenta il file PDF.
   * Un `XMPUtilityMetadata` oggetto che contiene i metadati da importare.

   Se utilizzate il `importXMP` metodo, inserite i seguenti valori:

   * Un `BLOB` oggetto che rappresenta il file PDF.
   * Un `BLOB` oggetto che rappresenta un file XML contenente i metadati da importare.

   In entrambi i casi, il valore restituito è un `BLOB` oggetto che rappresenta il file PDF con i nuovi metadati importati. È quindi possibile salvare l&#39;oggetto sul disco.

**Consulta anche**

[Importazione di metadati in documenti PDF](xmp-utilities.md#importing-metadata-into-pdf-documents)

<!--REVIEW: [Quick Start (Base64): Importing XMP metadata using the web service API](unresolvedlink-lc-qs-xmp-utilities-xu.xml#ws624e3cba99b79e12e69a9941333732bac8-7be8.2)-->

[Chiamata di AEM Forms mediante codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Creazione di un assembly client .NET che utilizza la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Esportazione di metadati da documenti PDF {#exporting-metadata-from-pdf-documents}

Potete utilizzare le API Java di utilità XMP e i servizi Web per recuperare e salvare in modo programmatico i metadati XMP da un documento PDF.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Utilità XMP, consultate Riferimento [servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-1}

Per esportare i metadati XMP da un documento PDF, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Create un client XMPUtilityService.
1. Richiamate l&#39;operazione di esportazione dei metadati XMP.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, accertatevi di includere i file proxy.

**Creare un client XMPUtilityService**

Prima di eseguire un&#39;operazione XMP Utilities in modo programmatico, è necessario creare un client XMPUtilityService. Con l&#39;API Java, se ciò si ottiene creando un `XMPUtilityServiceClient` oggetto. Con l&#39;API del servizio Web, questo viene eseguito utilizzando un `XMPUtilityServiceService` oggetto.

**Richiamo dell’operazione di esportazione dei metadati XMP**

Dopo aver creato il client del servizio, potete richiamare una delle operazioni di esportazione dei metadati XMP, che possono essere utilizzate per ispezionare i metadati XMP o salvarli su disco.

**Consulta anche**

[Importare metadati XMP tramite l&#39;API Java](xmp-utilities.md#import-xmp-metadata-using-the-java-api)

[Importazione di metadati XMP tramite l&#39;API del servizio Web](xmp-utilities.md#importing-xmp-metadata-using-the-web-service-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Esportare metadati XMP utilizzando l&#39;API Java {#export-xmp-metadata-using-the-java-api}

Esportate i metadati XMP utilizzando l&#39;API XMP Utilities (Java):

1. Includi file di progetto

   Includete file JAR client, ad esempio adobe-pdfutility-client.jar, nel percorso di classe del progetto Java.

   >[!NOTE]
   >
   >Il file adobe-pdfutility-client.jar contiene classi che consentono di richiamare il servizio XMP Utility a livello di programmazione.

1. Creare un client XMPUtilityService

   Creare un `XMPUtilityServiceClient` oggetto utilizzando il relativo costruttore e passando un `ServiceClientFactory` oggetto che contiene le proprietà di connessione.

1. Richiamo dell’operazione di importazione dei metadati XMP

   Per esaminare i metadati XMP, richiamare il `XMPUtilityServiceClient` metodo dell&#39; `exportMetadata` oggetto e trasmettere un `com.adobe.idp.Document` oggetto che rappresenta il file PDF. Il metodo restituisce un `XMPUtilityMetadata` oggetto che contiene i metadati recuperati.

   Per recuperare e salvare i metadati XMP, richiamare il metodo dell&#39; `XMPUtilityServiceClient` oggetto `exportXMP` e trasmettere un `com.adobe.idp.Document` oggetto che rappresenta il file PDF. Il metodo restituisce un `com.adobe.idp.Document` oggetto che contiene i metadati recuperati, che potete successivamente salvare su disco come file XML.

**Consulta anche**

[Esportazione di metadati da documenti PDF](xmp-utilities.md#exporting-metadata-from-pdf-documents)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Esportare metadati XMP tramite l&#39;API del servizio Web {#export-xmp-metadata-using-the-web-service-api}

Esportate i metadati XMP utilizzando l&#39;API Utilità XMP (servizio Web):

1. Includi file di progetto

   * Create un assembly client Microsoft .NET che utilizzi il file WSDL del servizio Utilità XMP.
   * Fare riferimento all&#39;assembly client Microsoft .NET.

1. Creare un client XMPUtilityService

   Creare un `XMPUtilityServiceService` oggetto utilizzando il costruttore della classe proxy.

1. Richiamo dell’operazione di importazione dei metadati XMP

   Per esaminare i metadati XMP, richiamare il `XMPUtilityServiceClient` metodo dell&#39; `exportMetadata` oggetto e trasmettere un `BLOB` oggetto che rappresenta il file PDF. Il metodo restituisce un `XMPUtilityMetadata` oggetto che contiene i metadati recuperati.

   Per recuperare e salvare i metadati XMP, richiamare il metodo dell&#39; `XMPUtilityServiceClient` oggetto `exportXMP` e trasmettere un `BLOB` oggetto che rappresenta il file PDF. Il metodo restituisce un `BLOB` oggetto che contiene i metadati recuperati, che potete successivamente salvare su disco come file XML.

**Consulta anche**

[Esportazione di metadati da documenti PDF](xmp-utilities.md#exporting-metadata-from-pdf-documents)

[Chiamata di AEM Forms mediante codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Creazione di un assembly client .NET che utilizza la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)
