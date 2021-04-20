---
title: Conversione di Postscript in documenti PDF
seo-title: Conversione di Postscript in documenti PDF
description: Utilizza il servizio Distiller per convertire i file PostScript®, Encapsulated PostScript (EPS) e PRN in file PDF compatti, affidabili e più sicuri su una rete. Il servizio Distiller converte grandi volumi di documenti stampati in documenti elettronici, ad esempio fatture e istruzioni che utilizzano l’API Java e l’API Web Service.
seo-description: Utilizza il servizio Distiller per convertire i file PostScript®, Encapsulated PostScript (EPS) e PRN in file PDF compatti, affidabili e più sicuri su una rete. Il servizio Distiller converte grandi volumi di documenti stampati in documenti elettronici, ad esempio fatture e istruzioni che utilizzano l’API Java e l’API Web Service.
uuid: 2143f406-1fdd-4551-a738-1a8388f8d478
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 06ad343a-f74d-41f5-b3c8-b85bb723ceeb
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1380'
ht-degree: 0%

---


# Conversione di Postscript in documenti PDF {#converting-postscript-to-pdf-documents}

**Esempi ed esempi in questo documento sono solo per AEM Forms in ambiente JEE.**

## Informazioni sul servizio Distiller {#about-the-distiller-service}

Il servizio Distiller® converte i file PostScript®, Encapsulated PostScript (EPS) e PRN in file PDF compatti, affidabili e più sicuri su una rete. Il servizio Distiller viene spesso utilizzato per convertire grandi volumi di documenti stampati in documenti elettronici, ad esempio fatture e dichiarazioni. La conversione dei documenti in PDF consente inoltre alle aziende di inviare ai propri clienti una versione cartacea e una versione elettronica di un documento.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Distiller, consulta [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Conversione di PostScript in documenti PDF {#converting-postscript-to-pdf-documents-inner}

In questo argomento viene descritto come utilizzare l&#39;API del servizio Distiller (Java e servizio Web) per convertire programmaticamente i file PostScript (PS), Encapsulated PostScript (EPS) e PRN in documenti PDF.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Distiller, consulta [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Per convertire i file PostScript in documenti PDF, è necessario installare uno dei seguenti file sul server che ospita AEM Forms: Pacchetto ridistribuibile Acrobat 9 o Microsoft Visual C++ 2005.

### Riepilogo dei passaggi {#summary-of-steps}

Per convertire uno qualsiasi dei tipi supportati in un documento PDF, eseguire la procedura seguente:

1. Includi file di progetto.
1. Crea un client di servizio Distiller.
1. Recupera il file da convertire.
1. Richiamare l’operazione di creazione del PDF.
1. Salvare il documento PDF.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

**Creare un client di servizio Distiller**

Prima di poter eseguire un’operazione di servizio Distiller a livello di programmazione, è necessario creare un client di servizio Distiller. Se utilizzi l’API Java, crea un oggetto `DistillerServiceClient`. Se utilizzi l’API del servizio Web, crea un oggetto `DistillerServiceService`.

**Recupera il file da convertire**

È necessario recuperare il file da convertire. Ad esempio, per convertire un file PS in un documento PDF, è necessario recuperare il file PS.

**Richiamare l’operazione di creazione del PDF**

Dopo aver creato il client di servizio, è possibile richiamare l’operazione di creazione PDF. Questa operazione richiede informazioni sul documento da convertire, compreso il percorso del documento di destinazione.

**Salvare il documento PDF**

È possibile salvare il documento PDF come file PDF.

**Consulta anche**

[Convertire un file PostScript in PDF utilizzando l’API Java](converting-postscript-pdf-documents.md#convert-a-postscript-file-to-pdf-using-the-java-api)

[Conversione di un file PostScript in PDF tramite l’API del servizio Web](converting-postscript-pdf-documents.md#converting-a-postscript-file-to-pdf-using-the-web-service-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API del servizio di output](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Convertire un file PostScript in PDF utilizzando l&#39;API Java {#convert-a-postscript-file-to-pdf-using-the-java-api}

Convertire un file PostScript in un documento PDF utilizzando l’API di servizio Distiller (Java):

1. Includi file di progetto.

   Includi file JAR client, come adobe-distiller-client.jar, nel percorso di classe del progetto Java.

1. Crea un client di servizio Distiller.

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `DistillerServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Recupera il file da convertire.

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il file da convertire utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del file.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Richiamare l’operazione di creazione del PDF.

   Richiama il metodo `createPDF` dell&#39;oggetto `DistillerServiceClient` e passa i seguenti valori:

   * L&#39;oggetto `com.adobe.idp.Document` che rappresenta il file PS, EPS o PRN da convertire
   * Un oggetto `java.lang.String` che contiene il nome del file da convertire
   * Un oggetto `java.lang.String` che contiene il nome delle impostazioni Adobe PDF da utilizzare
   * Un oggetto `java.lang.String` che contiene il nome delle impostazioni di protezione da utilizzare
   * Un oggetto `com.adobe.idp.Document` facoltativo che contiene le impostazioni da applicare durante la generazione del documento PDF
   * Oggetto `com.adobe.idp.Document` facoltativo che contiene informazioni sui metadati da applicare al documento PDF

   Il metodo `createPDF` restituisce un oggetto `CreatePDFResult` contenente il nuovo documento PDF e un file di registro che può essere generato. Il file di registro in genere contiene messaggi di errore o di avviso generati dalla richiesta di conversione.

1. Salvare il documento PDF.

   Per ottenere il documento PDF appena creato, eseguire le operazioni seguenti:

   * Richiama il metodo `getCreatedDocument` dell&#39;oggetto `CreatePDFResult`. Restituisce un oggetto `com.adobe.idp.Document`.
   * Richiamare il metodo `copyToFile` dell&#39;oggetto `com.adobe.idp.Document` per estrarre il documento PDF.

   Analogamente, per ottenere il documento di registro, eseguire le operazioni seguenti.

   * Richiama il metodo `getLogDocument` dell&#39;oggetto `CreatePDFResult`. Restituisce un oggetto `com.adobe.idp.Document`.
   * Richiamare il metodo `copyToFile` dell&#39;oggetto `com.adobe.idp.Document` per estrarre il documento di registro.


**Consulta anche**

[Riepilogo dei passaggi](converting-postscript-pdf-documents.md#summary-of-steps)

[Avvio rapido (modalità SOAP): Conversione di un file PostScript in un documento PDF tramite l’API Java](/help/forms/developing/distiller-service-java-api-quick.md#quick-start-soap-mode-converting-a-postscript-file-to-a-pdf-document-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Conversione di un file PostScript in PDF utilizzando l&#39;API del servizio Web {#converting-a-postscript-file-to-pdf-using-the-web-service-api}

Convertire un file PostScript in un documento PDF utilizzando l&#39;API di Distiller Service (servizio Web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurati di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/DistillerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Crea un client di servizio Distiller.

   * Creare un oggetto `DistillerServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `DistillerServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/DistillerService?blob=mtom`). Non è necessario utilizzare l&#39;attributo `lc_version` . Questo attributo viene utilizzato quando si crea un riferimento a un servizio. Tuttavia, specifica `?blob=mtom` per utilizzare MTOM.
   * Crea un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `DistillerServiceClient.Endpoint.Binding` . Imposta il valore restituito su `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegna il nome utente del modulo di AEM al campo `DistillerServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore della password corrispondente al campo `DistillerServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recupera il file da convertire.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. Questo oggetto `BLOB` viene utilizzato per memorizzare il file da convertire in un documento PDF.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file e la modalità in cui aprire il file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni dell&#39;array di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare l’array di byte con i dati del flusso richiamando il metodo `Read` dell’oggetto `System.IO.FileStream` e passando l’array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando la relativa proprietà `MTOM` con il contenuto dell&#39;array di byte.

1. Richiamare l’operazione di creazione del PDF.

   Richiama il metodo `CreatePDF2` dell&#39;oggetto `DistillerServiceService` e passa i seguenti valori obbligatori:

   * L&#39;oggetto `BLOB` che rappresenta il file PS da convertire
   * Una stringa che contiene il nome del percorso del file da convertire
   * Un oggetto stringa contenente le impostazioni Adobe PDF da utilizzare (ad esempio, `Standard`)
   * Un oggetto string contenente le impostazioni di protezione da utilizzare (ad esempio, `No Securit`y)
   * Un oggetto `BLOB` facoltativo che contiene le impostazioni da applicare durante la generazione del documento PDF
   * Oggetto `BLOB` facoltativo che contiene informazioni sui metadati da applicare al documento PDF
   * Un parametro di output `BLOB` utilizzato per memorizzare il documento PDF
   * Un parametro di output `BLOB` utilizzato per memorizzare il registro

1. Salvare il documento PDF.

   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore. Passare un valore di stringa che rappresenta la posizione del file del documento PDF firmato e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `BLOB` restituito dal metodo `CreatePDF2` (il parametro di output). Compilare l&#39;array di byte ottenendo il valore del membro dati `BLOB` dell&#39;oggetto `MTOM`.
   * Creare un oggetto `System.IO.BinaryWriter` richiamandone il costruttore e passando l&#39;oggetto `System.IO.FileStream`.
   * Scrivi il contenuto dell’array di byte in un file PDF richiamando il metodo `Write` dell’oggetto `System.IO.BinaryWriter` e passando l’array di byte.

**Consulta anche**

[Riepilogo dei passaggi](converting-postscript-pdf-documents.md#summary-of-steps)

<!-- UNRESOLVED LINKS
[Quick Start (MTOM): Converting a PostScript file to a PDF document using the web service API](unresolvedlink-lc-qs-distiller-di.xml#ws624e3cba99b79e12e69a9941333732bac8-7f01.2)

[Quick Start (SwaRef): Converting a PostScript file to a PDF document using the web service API](unresolvedlink-lc-qs-distiller-di.xml#ws624e3cba99b79e12e69a9941333732bac8-7eff.2)
-->

[Richiamo di AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamo di AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
