---
title: Conversione di Postscript in documenti PDF
seo-title: Converting Postscript to PDF Documents
description: Utilizza il servizio Distiller per convertire i file PostScript®, Encapsulated PostScript (EPS) e PRN in file PDF compatti, affidabili e più sicuri su una rete. Il servizio Distiller converte grandi volumi di documenti stampati in documenti elettronici, ad esempio fatture e istruzioni che utilizzano l’API Java e l’API Web Service.
seo-description: Use the Distiller service to convert PostScript®, Encapsulated PostScript (EPS), and PRN files to compact, reliable, and more secure PDF files over a network. The Distiller service converts large volumes of print documents to electronic documents, such as invoices and statements using the Java API and Web Service API.
uuid: 2143f406-1fdd-4551-a738-1a8388f8d478
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 06ad343a-f74d-41f5-b3c8-b85bb723ceeb
role: Developer
exl-id: 744df8b2-0c61-410f-89e9-20b8adddbf45
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1325'
ht-degree: 0%

---

# Conversione di Postscript in documenti PDF {#converting-postscript-to-pdf-documents}

**Esempi ed esempi in questo documento sono solo per AEM Forms in ambiente JEE.**

## Informazioni sul servizio Distiller {#about-the-distiller-service}

Il servizio Distiller® converte i file PostScript®, Encapsulated PostScript (EPS) e PRN in file PDF compatti, affidabili e più sicuri su una rete. Il servizio Distiller viene spesso utilizzato per convertire grandi volumi di documenti stampati in documenti elettronici, ad esempio fatture e dichiarazioni. La conversione dei documenti in PDF consente inoltre alle aziende di inviare ai propri clienti una versione cartacea e una versione elettronica di un documento.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Distiller, vedi [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Conversione di documenti PostScript in documenti PDF {#converting-postscript-to-pdf-documents-inner}

In questo argomento viene descritto come utilizzare l’API del servizio Distiller (Java e servizio Web) per convertire programmaticamente i file PostScript (PS), Encapsulated PostScript (EPS) e PRN in documenti PDF.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Distiller, vedi [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Per convertire i file PostScript in documenti PDF, è necessario installare uno dei seguenti file sul server che ospita AEM Forms: Pacchetto ridistribuibile Acrobat 9 o Microsoft Visual C++ 2005.

### Riepilogo dei passaggi {#summary-of-steps}

Per convertire uno qualsiasi dei tipi supportati in un documento PDF, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Crea un client di servizio Distiller.
1. Recupera il file da convertire.
1. Richiama l’operazione di creazione di PDF.
1. Salvare il documento PDF.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

**Creare un client di servizio Distiller**

Prima di poter eseguire un’operazione di servizio Distiller a livello di programmazione, è necessario creare un client di servizio Distiller. Se utilizzi l’API Java, crea un `DistillerServiceClient` oggetto. Se utilizzi l’API del servizio Web, crea un `DistillerServiceService` oggetto.

**Recupera il file da convertire**

È necessario recuperare il file da convertire. Ad esempio, per convertire un file PS in un documento PDF, è necessario recuperare il file PS.

**Richiamare l’operazione di creazione di PDF**

Dopo aver creato il client di servizio, è possibile richiamare l’operazione di creazione di PDF. Questa operazione richiede informazioni sul documento da convertire, compreso il percorso del documento di destinazione.

**Salvare il documento PDF**

È possibile salvare il documento PDF come file PDF.

**Consulta anche**

[Convertire un file PostScript in PDF utilizzando l’API Java](converting-postscript-pdf-documents.md#convert-a-postscript-file-to-pdf-using-the-java-api)

[Conversione di un file PostScript in PDF tramite l’API del servizio Web](converting-postscript-pdf-documents.md#converting-a-postscript-file-to-pdf-using-the-web-service-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API del servizio di output](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Convertire un file PostScript in PDF utilizzando l’API Java {#convert-a-postscript-file-to-pdf-using-the-java-api}

Convertire un file PostScript in un documento PDF utilizzando l’API del servizio Distiller (Java):

1. Includi file di progetto.

   Includi file JAR client, come adobe-distiller-client.jar, nel percorso di classe del progetto Java.

1. Crea un client di servizio Distiller.

   * Crea un `ServiceClientFactory` oggetto contenente le proprietà di connessione.
   * Crea un `DistillerServiceClient` utilizzando il relativo costruttore e passando `ServiceClientFactory` oggetto.

1. Recupera il file da convertire.

   * Crea un `java.io.FileInputStream` oggetto che rappresenta il file da convertire utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del file.
   * Crea un `com.adobe.idp.Document` utilizzando il relativo costruttore e passando `java.io.FileInputStream` oggetto.

1. Richiama l’operazione di creazione di PDF.

   Richiama il `DistillerServiceClient` dell’oggetto `createPDF` e passare i seguenti valori:

   * La `com.adobe.idp.Document` oggetto che rappresenta il file PS, EPS o PRN da convertire
   * A `java.lang.String` oggetto contenente il nome del file da convertire
   * A `java.lang.String` oggetto contenente il nome delle impostazioni Adobe PDF da utilizzare
   * A `java.lang.String` oggetto contenente il nome delle impostazioni di protezione da utilizzare
   * Facoltativo `com.adobe.idp.Document` oggetto contenente le impostazioni da applicare durante la generazione del documento PDF
   * Facoltativo `com.adobe.idp.Document` oggetto contenente le informazioni sui metadati da applicare al documento PDF

   La `createPDF` restituisce un `CreatePDFResult` oggetto contenente il nuovo documento PDF e un file di registro che può essere generato. Il file di registro in genere contiene messaggi di errore o di avviso generati dalla richiesta di conversione.

1. Salvare il documento PDF.

   Per ottenere il documento PDF appena creato, eseguire le operazioni seguenti:

   * Richiama il `CreatePDFResult` dell’oggetto `getCreatedDocument` metodo . Questo restituisce un `com.adobe.idp.Document` oggetto.
   * Richiama il `com.adobe.idp.Document` dell’oggetto `copyToFile` per estrarre il documento PDF.

   Analogamente, per ottenere il documento di registro, eseguire le operazioni seguenti.

   * Richiama il `CreatePDFResult` dell’oggetto `getLogDocument` metodo . Questo restituisce un `com.adobe.idp.Document` oggetto.
   * Richiama il `com.adobe.idp.Document` dell’oggetto `copyToFile` metodo per estrarre il documento di registro.


**Consulta anche**

[Riepilogo dei passaggi](converting-postscript-pdf-documents.md#summary-of-steps)

[Avvio rapido (modalità SOAP): Conversione di un file PostScript in un documento PDF tramite l’API Java](/help/forms/developing/distiller-service-java-api-quick.md#quick-start-soap-mode-converting-a-postscript-file-to-a-pdf-document-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Conversione di un file PostScript in PDF tramite l’API del servizio Web {#converting-a-postscript-file-to-pdf-using-the-web-service-api}

Convertire un file PostScript in un documento PDF utilizzando l’API del servizio Distiller (servizio Web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurati di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/DistillerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l’indirizzo IP del server che ospita AEM Forms.

1. Crea un client di servizio Distiller.

   * Crea un `DistillerServiceClient` utilizzando il relativo costruttore predefinito.
   * Crea un `DistillerServiceClient.Endpoint.Address` utilizzando `System.ServiceModel.EndpointAddress` costruttore. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/DistillerService?blob=mtom`.) Non è necessario utilizzare il `lc_version` attributo. Questo attributo viene utilizzato quando si crea un riferimento a un servizio. Tuttavia, specifica `?blob=mtom` per utilizzare MTOM.
   * Crea un `System.ServiceModel.BasicHttpBinding` ottenendo il valore del `DistillerServiceClient.Endpoint.Binding` campo . Imposta il valore restituito su `BasicHttpBinding`.
   * Imposta la `System.ServiceModel.BasicHttpBinding` dell’oggetto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegnare il nome utente del modulo di AEM al campo `DistillerServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore della password corrispondente al campo `DistillerServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recupera il file da convertire.

   * Crea un `BLOB` utilizzando il relativo costruttore. Questo `BLOB` viene utilizzato per memorizzare il file da convertire in un documento PDF.
   * Crea un `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto del `System.IO.FileStream` oggetto. È possibile determinare le dimensioni dell&#39;array di byte ottenendo il `System.IO.FileStream` dell’oggetto `Length` proprietà.
   * Compilare l&#39;array di byte con i dati del flusso richiamando il `System.IO.FileStream` dell’oggetto `Read` e passare l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare `BLOB` oggetto assegnando il relativo `MTOM` con il contenuto dell&#39;array di byte.

1. Richiama l’operazione di creazione di PDF.

   Richiama il `DistillerServiceService` dell’oggetto `CreatePDF2` e trasmettere i seguenti valori richiesti:

   * La `BLOB` oggetto che rappresenta il file PS da convertire
   * Una stringa che contiene il nome del percorso del file da convertire
   * Un oggetto stringa contenente le impostazioni Adobe PDF da utilizzare, ad esempio `Standard`)
   * Un oggetto stringa contenente le impostazioni di protezione da utilizzare, ad esempio `No Securit`a)
   * Facoltativo `BLOB` oggetto contenente le impostazioni da applicare durante la generazione del documento PDF
   * Facoltativo `BLOB` oggetto contenente le informazioni sui metadati da applicare al documento PDF
   * A `BLOB` parametro di output utilizzato per memorizzare il documento PDF
   * A `BLOB` parametro di output utilizzato per memorizzare il registro

1. Salvare il documento PDF.

   * Crea un `System.IO.FileStream` richiamando il relativo costruttore. Passa un valore stringa che rappresenta la posizione del file del documento PDF firmato e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto del `BLOB` oggetto restituito da `CreatePDF2` (il parametro di output). Compilare l’array di byte ottenendo il valore del `BLOB` dell’oggetto `MTOM` membro dati.
   * Crea un `System.IO.BinaryWriter` richiamando il relativo costruttore e passando `System.IO.FileStream` oggetto.
   * Scrivi il contenuto dell’array di byte in un file PDF richiamando il `System.IO.BinaryWriter` dell’oggetto `Write` e passare l&#39;array di byte.

**Consulta anche**

[Riepilogo dei passaggi](converting-postscript-pdf-documents.md#summary-of-steps)

<!-- UNRESOLVED LINKS
[Quick Start (MTOM): Converting a PostScript file to a PDF document using the web service API](unresolvedlink-lc-qs-distiller-di.xml#ws624e3cba99b79e12e69a9941333732bac8-7f01.2)

[Quick Start (SwaRef): Converting a PostScript file to a PDF document using the web service API](unresolvedlink-lc-qs-distiller-di.xml#ws624e3cba99b79e12e69a9941333732bac8-7eff.2)
-->

[Richiamo di AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamo di AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
