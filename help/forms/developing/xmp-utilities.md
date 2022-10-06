---
title: Utilizzo delle utility XMP
seo-title: Working with XMP Utilities
description: Utilizza le API Java e servizi Web di Utilità XMP per importare in modo programmatico i metadati XMP in un documento PDF e recuperare e salvare i metadati XMP da un documento PDF.
seo-description: Use the XMP Utilities Java and Web Service APIs to programmatically import XMP metadata into a PDF document and retrieve and save XMP metadata from a PDF document.
uuid: 90ce6cef-efe1-456a-8e0c-5ba90249dda0
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 01d5677f-5c87-4a6e-987b-8eda9acc0b27
role: Developer
exl-id: cff65f74-ba95-438e-88a4-5ec7d22aafba
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1405'
ht-degree: 0%

---

# Utilizzo delle utility XMP {#working-with-xmp-utilities}

**Esempi ed esempi in questo documento sono solo per AEM Forms in ambiente JEE.**

**Informazioni sul servizio Utilità XMP**

I documenti PDF contengono metadati, ovvero informazioni relative al documento distinte dal contenuto del documento, ad esempio testo e grafica. Adobe Extensible Metadata Platform (XMP) è uno standard per la gestione dei metadati dei documenti.

Il servizio Utilità di XMP può recuperare e salvare i metadati XMP dai documenti di PDF e importare metadati XMP nei documenti di PDF.

Puoi eseguire queste attività utilizzando il servizio Utilità XMP:

* Importare metadati nei documenti PDF. (Vedi [Importazione di metadati in documenti PDF](xmp-utilities.md#importing-metadata-into-pdf-documents).)
* Esporta metadati da documenti PDF. (Vedi [Esportazione di metadati da documenti PDF](xmp-utilities.md#exporting-metadata-from-pdf-documents).)

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Utilità XMP, consulta [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Importazione di metadati in documenti PDF {#importing-metadata-into-pdf-documents}

È possibile utilizzare le API di XMP Utilities Java e di servizi Web per importare in modo programmatico i metadati XMP in un documento PDF. I metadati forniscono informazioni su un documento di PDF, ad esempio l’autore del documento e le parole chiave correlate al documento. I metadati possono essere posizionati nella finestra di dialogo Proprietà documento del documento, come illustrato nella figura seguente.

![ww_ww_metadatadialog](assets/ww_ww_metadatadialog.png)

Per importare a livello di programmazione i metadati in un documento PDF, è possibile utilizzare un documento XML esistente che specifica i valori dei metadati oppure un oggetto di tipo `XMPUtilityMetadata`. (Vedi [Riferimento API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).)

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
>Per ulteriori informazioni sul servizio Utilità XMP, consulta [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary-of-steps}

Per importare XMP metadati in un documento PDF, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Crea un client XMPUtilityService.
1. Richiama l’operazione di importazione dei metadati XMP.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

**Creare un client XMPUtilityService**

Prima di eseguire un&#39;operazione Utilità di XMP a livello di programmazione, è necessario creare un client XMPUtilityService. Con l’API Java, si ottiene questo risultato creando un’ `XMPUtilityServiceClient` oggetto. Con l’API del servizio Web, si ottiene questo risultato utilizzando un’ `XMPUtilityServiceService` oggetto.

**Richiamare l’operazione di importazione dei metadati XMP**

Dopo aver creato il client di servizio, è possibile richiamare una delle operazioni di importazione dei metadati XMP per importare i metadati XMP nel documento di PDF specificato.

**Consulta anche**

[Importare metadati XMP utilizzando l’API Java](xmp-utilities.md#import-xmp-metadata-using-the-java-api)

[Importazione di metadati XMP tramite l’API del servizio Web](xmp-utilities.md#importing-xmp-metadata-using-the-web-service-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Importare metadati XMP utilizzando l’API Java {#import-xmp-metadata-using-the-java-api}

Importa i metadati XMP utilizzando l&#39;API XMP Utilities (Java):

1. Includi file di progetto

   Includi file JAR client, come adobe-pdfutility-client.jar, nel percorso di classe del progetto Java.

   >[!NOTE]
   >
   >Il file adobe-pdfutility-client.jar contiene classi che consentono di richiamare programmaticamente il servizio Utilità XMP.

1. Creare un client XMPUtilityService

   Crea un `XMPUtilityServiceClient` utilizzando il relativo costruttore e passando un `ServiceClientFactory` oggetto contenente le proprietà di connessione.

1. Richiamare l’operazione di importazione dei metadati XMP

   Per modificare i metadati del XMP, richiamare `XMPUtilityServiceClient` dell’oggetto `importMetadata` metodo o `importXMP` metodo .

   Se utilizzi `importMetadata` passa i seguenti valori:

   * A `com.adobe.idp.Document` oggetto che rappresenta il file PDF.
   * Un `XMPUtilityMetadata` che contiene i metadati da importare.

   Se utilizzi `importXMP` passa i seguenti valori:

   * A `com.adobe.idp.Document` oggetto che rappresenta il file PDF.
   * A `com.adobe.idp.Document` oggetto che rappresenta un file XML contenente i metadati da importare.

   In entrambi i casi, il valore restituito è un `com.adobe.idp.Document` oggetto che rappresenta il file PDF con i metadati appena importati. È quindi possibile salvare l&#39;oggetto sul disco.

**Consulta anche**

[Importazione di metadati in documenti PDF](xmp-utilities.md#importing-metadata-into-pdf-documents)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Importazione di metadati XMP tramite l’API del servizio Web {#importing-xmp-metadata-using-the-web-service-api}

Per importare in modo programmatico i metadati XMP utilizzando l&#39;API del servizio Web XMP Utilities, esegui le seguenti attività:

1. Includi file di progetto

   * Creare un assembly client Microsoft .NET che utilizzi il file WSDL del servizio Utilità di XMP. (Vedi [Richiamo di AEM Forms con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).)
   * Fare riferimento all&#39;assembly client Microsoft .NET. (Vedi [Creazione di un assembly client .NET che utilizza la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding).)

1. Creare un client XMPUtilityService

   Crea un `XMPUtilityServiceService` utilizzando il costruttore della classe proxy.

1. Richiamare l’operazione di importazione dei metadati XMP

   Per modificare i metadati del XMP, richiamare `XMPUtilityServiceService` dell’oggetto `importMetadata` metodo o `importXMP` metodo .

   Se utilizzi `importMetadata` passa i seguenti valori:

   * A `BLOB` oggetto che rappresenta il file PDF.
   * Un `XMPUtilityMetadata` che contiene i metadati da importare.

   Se utilizzi `importXMP` passa i seguenti valori:

   * A `BLOB` oggetto che rappresenta il file PDF.
   * A `BLOB` oggetto che rappresenta un file XML contenente i metadati da importare.

   In entrambi i casi, il valore restituito è un `BLOB` oggetto che rappresenta il file PDF con i metadati appena importati. È quindi possibile salvare l&#39;oggetto sul disco.

**Consulta anche**

[Importazione di metadati in documenti PDF](xmp-utilities.md#importing-metadata-into-pdf-documents)

<!--REVIEW: [Quick Start (Base64): Importing XMP metadata using the web service API](unresolvedlink-lc-qs-xmp-utilities-xu.xml#ws624e3cba99b79e12e69a9941333732bac8-7be8.2)-->

[Richiamo di AEM Forms con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Creazione di un assembly client .NET che utilizza la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Esportazione di metadati da documenti PDF {#exporting-metadata-from-pdf-documents}

È possibile utilizzare le API di XMP Utilities Java e di servizi Web per recuperare e salvare programmaticamente i metadati XMP da un documento PDF.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Utilità XMP, consulta [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-1}

Per esportare i metadati XMP da un documento PDF, esegui le seguenti operazioni:

1. Includi file di progetto.
1. Crea un client XMPUtilityService.
1. Richiamare l’operazione di esportazione dei metadati XMP.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

**Creare un client XMPUtilityService**

Prima di eseguire un&#39;operazione Utilità di XMP a livello di programmazione, è necessario creare un client XMPUtilityService. Con Java AP, questo si ottiene creando un `XMPUtilityServiceClient` oggetto. Con l’API del servizio Web, viene eseguito utilizzando un’ `XMPUtilityServiceService` oggetto.

**Richiamare l’operazione di esportazione dei metadati XMP**

Dopo aver creato il client di servizio, è possibile richiamare una delle operazioni di esportazione dei metadati XMP, che può essere utilizzata per ispezionare i metadati XMP o salvarli sul disco.

**Consulta anche**

[Importare metadati XMP utilizzando l’API Java](xmp-utilities.md#import-xmp-metadata-using-the-java-api)

[Importazione di metadati XMP tramite l’API del servizio Web](xmp-utilities.md#importing-xmp-metadata-using-the-web-service-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Esportare i metadati XMP utilizzando l’API Java {#export-xmp-metadata-using-the-java-api}

Esporta metadati XMP utilizzando l&#39;API XMP Utilities (Java):

1. Includi file di progetto

   Includi file JAR client, come adobe-pdfutility-client.jar, nel percorso di classe del progetto Java.

   >[!NOTE]
   >
   >Il file adobe-pdfutility-client.jar contiene classi che consentono di richiamare programmaticamente il servizio Utility XMP.

1. Creare un client XMPUtilityService

   Crea un `XMPUtilityServiceClient` utilizzando il relativo costruttore e passando un `ServiceClientFactory` oggetto contenente le proprietà di connessione.

1. Richiamare l’operazione di importazione dei metadati XMP

   Per esaminare i metadati XMP, richiama il `XMPUtilityServiceClient` dell’oggetto `exportMetadata` e trasmettere un `com.adobe.idp.Document` oggetto che rappresenta il file PDF. Il metodo restituisce un `XMPUtilityMetadata` oggetto contenente i metadati recuperati.

   Per recuperare e salvare i metadati XMP, richiama il `XMPUtilityServiceClient` dell’oggetto `exportXMP` e trasmettere un `com.adobe.idp.Document` oggetto che rappresenta il file PDF. Il metodo restituisce un `com.adobe.idp.Document` oggetto contenente i metadati recuperati, che è possibile salvare successivamente su disco come file XML.

**Consulta anche**

[Esportazione di metadati da documenti PDF](xmp-utilities.md#exporting-metadata-from-pdf-documents)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Esportare i metadati XMP utilizzando l’API del servizio Web {#export-xmp-metadata-using-the-web-service-api}

Esporta metadati XMP utilizzando l&#39;API XMP Utilities (servizio Web):

1. Includi file di progetto

   * Creare un assembly client Microsoft .NET che utilizzi il file WSDL del servizio Utilità di XMP.
   * Fare riferimento all&#39;assembly client Microsoft .NET.

1. Creare un client XMPUtilityService

   Crea un `XMPUtilityServiceService` utilizzando il costruttore della classe proxy.

1. Richiamare l’operazione di importazione dei metadati XMP

   Per esaminare i metadati XMP, richiama il `XMPUtilityServiceClient` dell’oggetto `exportMetadata` e trasmettere un `BLOB` oggetto che rappresenta il file PDF. Il metodo restituisce un `XMPUtilityMetadata` oggetto contenente i metadati recuperati.

   Per recuperare e salvare i metadati XMP, richiama il `XMPUtilityServiceClient` dell’oggetto `exportXMP` e trasmettere un `BLOB` oggetto che rappresenta il file PDF. Il metodo restituisce un `BLOB` oggetto contenente i metadati recuperati, che è possibile salvare successivamente su disco come file XML.

**Consulta anche**

[Esportazione di metadati da documenti PDF](xmp-utilities.md#exporting-metadata-from-pdf-documents)

[Richiamo di AEM Forms con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Creazione di un assembly client .NET che utilizza la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)
