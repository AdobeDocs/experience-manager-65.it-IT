---
title: Utilizzo delle utility XMP
seo-title: Utilizzo delle utility XMP
description: Utilizza le API Java e Web Service di Utilità XMP per importare in modo programmatico i metadati XMP in un documento PDF e recuperare e salvare i metadati XMP da un documento PDF.
seo-description: Utilizza le API Java e Web Service di Utilità XMP per importare in modo programmatico i metadati XMP in un documento PDF e recuperare e salvare i metadati XMP da un documento PDF.
uuid: 90ce6cef-efe1-456a-8e0c-5ba90249dda0
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 01d5677f-5c87-4a6e-987b-8eda9acc0b27
role: Developer (Sviluppatore)
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1438'
ht-degree: 0%

---


# Utilizzo delle utility XMP {#working-with-xmp-utilities}

**Esempi ed esempi in questo documento sono solo per AEM Forms in ambiente JEE.**

**Informazioni sul servizio Utilità XMP**

I documenti PDF contengono metadati, ovvero informazioni relative al documento distinte dal contenuto del documento, ad esempio testo e grafica. Adobe Extensible Metadata Platform (XMP) è uno standard per la gestione dei metadati dei documenti.

Il servizio Utilità XMP può recuperare e salvare i metadati XMP dai documenti PDF e importare i metadati XMP nei documenti PDF.

Puoi eseguire queste attività utilizzando il servizio Utilità XMP:

* Importa metadati nei documenti PDF. (Consultare [Importazione di metadati in documenti PDF](xmp-utilities.md#importing-metadata-into-pdf-documents).)
* Esporta metadati da documenti PDF. (Vedere [Esportazione di metadati da documenti PDF](xmp-utilities.md#exporting-metadata-from-pdf-documents).)

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Utilità di XMP, consulta [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Importazione di metadati in documenti PDF {#importing-metadata-into-pdf-documents}

È possibile utilizzare Java utilità XMP e API di servizi Web per importare in modo programmatico i metadati XMP in un documento PDF. I metadati forniscono informazioni su un documento PDF, ad esempio l’autore del documento e le parole chiave correlate al documento. I metadati possono essere visualizzati nella finestra di dialogo Proprietà documento del documento, come illustrato di seguito.

![ww_ww_metadatadialog](assets/ww_ww_metadatadialog.png)

Per importare i metadati in un documento PDF a livello di programmazione, è possibile utilizzare un documento XML esistente che specifica i valori dei metadati oppure un oggetto di tipo `XMPUtilityMetadata`. (Consulta [Riferimento API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).)

>[!NOTE]
>
>Questa sezione illustra come utilizzare un documento XML per importare metadati in un documento PDF.

Il codice XML seguente contiene i valori di metadati corrispondenti all&#39;illustrazione precedente. Ad esempio, notare gli elementi in grassetto, che specificano le parole chiave.

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
>Per ulteriori informazioni sul servizio Utilità di XMP, consulta [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary-of-steps}

Per importare XMP metadati in un documento PDF, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Crea un client XMPUtilityService.
1. Richiama l’operazione di importazione dei metadati XMP.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

**Creare un client XMPUtilityService**

Prima di eseguire un&#39;operazione Utilità di XMP a livello di programmazione, è necessario creare un client XMPUtilityService. Con l’API Java, questo si ottiene creando un oggetto `XMPUtilityServiceClient` . Con l’API del servizio Web, questo viene eseguito utilizzando un oggetto `XMPUtilityServiceService` .

**Richiamare l’operazione di importazione dei metadati XMP**

Dopo aver creato il client di servizio, è possibile richiamare una delle operazioni di importazione dei metadati XMP per importare i metadati XMP nel documento PDF specificato.

**Consulta anche**

[Importare metadati XMP utilizzando l’API Java](xmp-utilities.md#import-xmp-metadata-using-the-java-api)

[Importazione di metadati XMP tramite l’API del servizio Web](xmp-utilities.md#importing-xmp-metadata-using-the-web-service-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Importare metadati XMP utilizzando l&#39;API Java {#import-xmp-metadata-using-the-java-api}

Importa i metadati XMP utilizzando l&#39;API XMP Utilities (Java):

1. Includi file di progetto

   Includi file JAR client, come adobe-pdfutility-client.jar, nel percorso di classe del progetto Java.

   >[!NOTE]
   >
   >Il file adobe-pdfutility-client.jar contiene classi che consentono di richiamare programmaticamente il servizio Utilità XMP.

1. Creare un client XMPUtilityService

   Creare un oggetto `XMPUtilityServiceClient` utilizzando il relativo costruttore e passando un oggetto `ServiceClientFactory` contenente proprietà di connessione.

1. Richiamare l’operazione di importazione dei metadati XMP

   Per modificare i metadati XMP, richiamare il metodo `importMetadata` dell&#39;oggetto `XMPUtilityServiceClient` o il relativo metodo `importXMP`.

   Se utilizzi il metodo `importMetadata`, specifica i seguenti valori:

   * Un oggetto `com.adobe.idp.Document` che rappresenta il file PDF.
   * Un oggetto `XMPUtilityMetadata` contenente i metadati da importare.

   Se utilizzi il metodo `importXMP`, specifica i seguenti valori:

   * Un oggetto `com.adobe.idp.Document` che rappresenta il file PDF.
   * Un oggetto `com.adobe.idp.Document` che rappresenta un file XML contenente i metadati da importare.

   In entrambi i casi, il valore restituito è un oggetto `com.adobe.idp.Document` che rappresenta il file PDF con i metadati appena importati. È quindi possibile salvare l&#39;oggetto sul disco.

**Consulta anche**

[Importazione di metadati in documenti PDF](xmp-utilities.md#importing-metadata-into-pdf-documents)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Importazione di metadati XMP utilizzando l&#39;API del servizio Web {#importing-xmp-metadata-using-the-web-service-api}

Per importare in modo programmatico i metadati XMP utilizzando l&#39;API del servizio Web XMP Utilities, esegui le seguenti attività:

1. Includi file di progetto

   * Creare un assembly client Microsoft .NET che utilizzi il file WSDL del servizio Utilità di XMP. (Vedere [Richiamo di AEM Forms utilizzando la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).)
   * Fare riferimento all&#39;assembly client Microsoft .NET. (Vedere [Creazione di un assembly client .NET che utilizza la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding).)

1. Creare un client XMPUtilityService

   Crea un oggetto `XMPUtilityServiceService` utilizzando il costruttore della classe proxy.

1. Richiamare l’operazione di importazione dei metadati XMP

   Per modificare i metadati XMP, richiamare il metodo `importMetadata` dell&#39;oggetto `XMPUtilityServiceService` o il relativo metodo `importXMP`.

   Se utilizzi il metodo `importMetadata`, specifica i seguenti valori:

   * Un oggetto `BLOB` che rappresenta il file PDF.
   * Un oggetto `XMPUtilityMetadata` contenente i metadati da importare.

   Se utilizzi il metodo `importXMP`, specifica i seguenti valori:

   * Un oggetto `BLOB` che rappresenta il file PDF.
   * Un oggetto `BLOB` che rappresenta un file XML contenente i metadati da importare.

   In entrambi i casi, il valore restituito è un oggetto `BLOB` che rappresenta il file PDF con i metadati appena importati. È quindi possibile salvare l&#39;oggetto sul disco.

**Consulta anche**

[Importazione di metadati in documenti PDF](xmp-utilities.md#importing-metadata-into-pdf-documents)

<!--REVIEW: [Quick Start (Base64): Importing XMP metadata using the web service API](unresolvedlink-lc-qs-xmp-utilities-xu.xml#ws624e3cba99b79e12e69a9941333732bac8-7be8.2)-->

[Richiamo di AEM Forms con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Creazione di un assembly client .NET che utilizza la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Esportazione di metadati da documenti PDF {#exporting-metadata-from-pdf-documents}

È possibile utilizzare Java utilità XMP e API di servizi Web per recuperare e salvare programmaticamente i metadati XMP da un documento PDF.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Utilità di XMP, consulta [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-1}

Per esportare XMP metadati da un documento PDF, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Crea un client XMPUtilityService.
1. Richiamare l’operazione di esportazione dei metadati XMP.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

**Creare un client XMPUtilityService**

Prima di eseguire un&#39;operazione Utilità di XMP a livello di programmazione, è necessario creare un client XMPUtilityService. Con Java AP, questo si ottiene creando un oggetto `XMPUtilityServiceClient` . Con l’API del servizio Web, questa operazione viene eseguita utilizzando un oggetto `XMPUtilityServiceService` .

**Richiamare l’operazione di esportazione dei metadati XMP**

Dopo aver creato il client di servizio, è possibile richiamare una delle operazioni di esportazione dei metadati XMP, che può essere utilizzata per ispezionare i metadati XMP o salvarli sul disco.

**Consulta anche**

[Importare metadati XMP utilizzando l’API Java](xmp-utilities.md#import-xmp-metadata-using-the-java-api)

[Importazione di metadati XMP tramite l’API del servizio Web](xmp-utilities.md#importing-xmp-metadata-using-the-web-service-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Esportare i metadati XMP utilizzando l&#39;API Java {#export-xmp-metadata-using-the-java-api}

Esporta metadati XMP utilizzando l&#39;API XMP Utilities (Java):

1. Includi file di progetto

   Includi file JAR client, come adobe-pdfutility-client.jar, nel percorso di classe del progetto Java.

   >[!NOTE]
   >
   >Il file adobe-pdfutility-client.jar contiene classi che consentono di richiamare programmaticamente il servizio Utility XMP.

1. Creare un client XMPUtilityService

   Creare un oggetto `XMPUtilityServiceClient` utilizzando il relativo costruttore e passando un oggetto `ServiceClientFactory` contenente proprietà di connessione.

1. Richiamare l’operazione di importazione dei metadati XMP

   Per esaminare i metadati XMP, richiamare il metodo `exportMetadata` dell’oggetto `com.adobe.idp.Document` e passare un oggetto `XMPUtilityServiceClient` che rappresenta il file PDF. Il metodo restituisce un oggetto `XMPUtilityMetadata` contenente i metadati recuperati.

   Per recuperare e salvare i metadati XMP, richiamare il metodo `exportXMP` dell’oggetto `com.adobe.idp.Document` e passare un oggetto `XMPUtilityServiceClient` che rappresenta il file PDF. Il metodo restituisce un oggetto `com.adobe.idp.Document` contenente i metadati recuperati, che è possibile successivamente salvare su disco come file XML.

**Consulta anche**

[Esportazione di metadati da documenti PDF](xmp-utilities.md#exporting-metadata-from-pdf-documents)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Esportare i metadati XMP utilizzando l&#39;API del servizio Web {#export-xmp-metadata-using-the-web-service-api}

Esporta metadati XMP utilizzando l&#39;API XMP Utilities (servizio Web):

1. Includi file di progetto

   * Creare un assembly client Microsoft .NET che utilizzi il file WSDL del servizio Utilità di XMP.
   * Fare riferimento all&#39;assembly client Microsoft .NET.

1. Creare un client XMPUtilityService

   Crea un oggetto `XMPUtilityServiceService` utilizzando il costruttore della classe proxy.

1. Richiamare l’operazione di importazione dei metadati XMP

   Per esaminare i metadati XMP, richiamare il metodo `exportMetadata` dell’oggetto `BLOB` e passare un oggetto `XMPUtilityServiceClient` che rappresenta il file PDF. Il metodo restituisce un oggetto `XMPUtilityMetadata` contenente i metadati recuperati.

   Per recuperare e salvare i metadati XMP, richiamare il metodo `exportXMP` dell’oggetto `BLOB` e passare un oggetto `XMPUtilityServiceClient` che rappresenta il file PDF. Il metodo restituisce un oggetto `BLOB` contenente i metadati recuperati, che è possibile successivamente salvare su disco come file XML.

**Consulta anche**

[Esportazione di metadati da documenti PDF](xmp-utilities.md#exporting-metadata-from-pdf-documents)

[Richiamo di AEM Forms con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Creazione di un assembly client .NET che utilizza la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)
