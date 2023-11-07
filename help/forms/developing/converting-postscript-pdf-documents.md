---
title: Conversione di PostScript in documenti PDF
seo-title: Converting Postscript to PDF Documents
description: Utilizzare il servizio Distiller per convertire i file PostScript®, Encapsulated PostScript (EPS) e PRN in file PDF compatti, affidabili e più sicuri in rete. Il servizio Distiller converte grandi quantità di documenti di stampa in documenti elettronici, ad esempio fatture e rendiconti, utilizzando l'API Java e l'API del servizio Web.
seo-description: Use the Distiller service to convert PostScript®, Encapsulated PostScript (EPS), and PRN files to compact, reliable, and more secure PDF files over a network. The Distiller service converts large volumes of print documents to electronic documents, such as invoices and statements using the Java API and Web Service API.
uuid: 2143f406-1fdd-4551-a738-1a8388f8d478
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 06ad343a-f74d-41f5-b3c8-b85bb723ceeb
role: Developer
exl-id: 744df8b2-0c61-410f-89e9-20b8adddbf45
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1323'
ht-degree: 0%

---

# Conversione di PostScript in documenti PDF {#converting-postscript-to-pdf-documents}

**Gli esempi e gli esempi contenuti in questo documento sono solo per l’ambiente AEM Forms su JEE.**

## Informazioni sul servizio Distiller {#about-the-distiller-service}

Il servizio Distiller® converte i file PostScript®, Encapsulated PostScript (EPS) e PRN in file PDF compatti, affidabili e più sicuri in rete. Il servizio Distiller viene spesso utilizzato per convertire grandi quantità di documenti stampati in documenti elettronici, come fatture e rendiconti. La conversione dei documenti in PDF consente inoltre alle aziende di inviare ai propri clienti una versione cartacea e una versione elettronica di un documento.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Distiller, consulta [Guida di riferimento dei servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Conversione di documenti PostScript in documenti PDF {#converting-postscript-to-pdf-documents-inner}

In questo argomento viene descritto come utilizzare l&#39;API di Distiller Service (Java e servizio Web) per convertire in modo programmatico i file PostScript (PS), Encapsulated PostScript (EPS) e PRN in documenti PDF.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Distiller, consulta [Guida di riferimento dei servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Per convertire i file PostScript in documenti PDF, è necessario che nel server che ospita AEM Forms sia installato uno dei seguenti pacchetti ridistribuibili: Acrobat 9 o Microsoft Visual C++ 2005.

### Riepilogo dei passaggi {#summary-of-steps}

Per convertire uno qualsiasi dei tipi supportati in un documento PDF, effettuare le seguenti operazioni:

1. Includi file di progetto.
1. Creazione di un client di servizio Distiller.
1. Recuperate il file da convertire.
1. Richiama l’operazione di creazione di PDF.
1. Salvare il documento PDF.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

**Creazione di un client di servizio Distiller**

Prima di poter eseguire un&#39;operazione di servizio Distiller a livello di programmazione, è necessario creare un client di servizio Distiller. Se utilizzi l’API Java, crea un’ `DistillerServiceClient` oggetto. Se utilizzi l’API del servizio web, crea un’ `DistillerServiceService` oggetto.

**Recupera il file da convertire**

Recuperate il file da convertire. Ad esempio, per convertire un file PS in un documento PDF, è necessario recuperare il file PS.

**Richiama l’operazione di creazione di PDF**

Dopo aver creato il client del servizio, è possibile richiamare l&#39;operazione di creazione PDF. Questa operazione richiede informazioni sul documento da convertire, incluso il percorso del documento di destinazione.

**Salva il documento PDF**

È possibile salvare il documento PDF come file PDF.

**Consulta anche**

[Convertire un file PostScript in PDF utilizzando l’API Java](converting-postscript-pdf-documents.md#convert-a-postscript-file-to-pdf-using-the-java-api)

[Conversione di un file PostScript in PDF tramite l’API del servizio web](converting-postscript-pdf-documents.md#converting-a-postscript-file-to-pdf-using-the-web-service-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API servizio di output](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Convertire un file PostScript in PDF utilizzando l’API Java {#convert-a-postscript-file-to-pdf-using-the-java-api}

Converti un file PostScript in documento PDF utilizzando l’API di servizio Distiller (Java):

1. Includi file di progetto.

   Includi i file JAR client, come adobe-distiller-client.jar, nel percorso di classe del progetto Java.

1. Creazione di un client di servizio Distiller.

   * Creare un `ServiceClientFactory` oggetto che contiene proprietà di connessione.
   * Creare un `DistillerServiceClient` mediante il costruttore e passando il `ServiceClientFactory` oggetto.

1. Recuperate il file da convertire.

   * Creare un `java.io.FileInputStream` oggetto che rappresenta il file da convertire utilizzando il relativo costruttore e passando un valore stringa che specifica la posizione del file.
   * Creare un `com.adobe.idp.Document` mediante il costruttore e passando il `java.io.FileInputStream` oggetto.

1. Richiama l’operazione di creazione di PDF.

   Richiama `DistillerServiceClient` dell&#39;oggetto `createPDF` e trasmettere i seguenti valori:

   * Il `com.adobe.idp.Document` oggetto che rappresenta il file PS, EPS o PRN da convertire
   * A `java.lang.String` oggetto contenente il nome del file da convertire
   * A `java.lang.String` oggetto contenente il nome delle impostazioni Adobe PDF da utilizzare
   * A `java.lang.String` oggetto contenente il nome delle impostazioni di protezione da utilizzare
   * Un&#39;opzione `com.adobe.idp.Document` oggetto contenente le impostazioni da applicare durante la generazione del documento PDF
   * Un&#39;opzione `com.adobe.idp.Document` oggetto contenente informazioni sui metadati da applicare al documento PDF

   Il `createPDF` il metodo restituisce un `CreatePDFResult` oggetto contenente il nuovo documento PDF e un file di registro che può essere generato. Il file di registro contiene in genere messaggi di errore o di avviso generati dalla richiesta di conversione.

1. Salvare il documento PDF.

   Per ottenere il documento di PDF appena creato, effettuare le seguenti operazioni:

   * Richiama `CreatePDFResult` dell&#39;oggetto `getCreatedDocument` metodo. Questo restituisce un `com.adobe.idp.Document` oggetto.
   * Richiama `com.adobe.idp.Document` dell&#39;oggetto `copyToFile` per estrarre il documento PDF.

   Analogamente, per ottenere il documento di registro, effettuare le seguenti operazioni.

   * Richiama `CreatePDFResult` dell&#39;oggetto `getLogDocument` metodo. Questo restituisce un `com.adobe.idp.Document` oggetto.
   * Richiama `com.adobe.idp.Document` dell&#39;oggetto `copyToFile` per estrarre il documento di log.

**Consulta anche**

[Riepilogo dei passaggi](converting-postscript-pdf-documents.md#summary-of-steps)

[Guida rapida (modalità SOAP): conversione di un file PostScript in un documento PDF tramite l’API Java](/help/forms/developing/distiller-service-java-api-quick.md#quick-start-soap-mode-converting-a-postscript-file-to-a-pdf-document-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Conversione di un file PostScript in PDF tramite l’API del servizio web {#converting-a-postscript-file-to-pdf-using-the-web-service-api}

Convertire un file PostScript in un documento PDF utilizzando l’API del servizio Distiller (servizio web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/DistillerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l’indirizzo IP del server che ospita AEM Forms.

1. Creazione di un client di servizio Distiller.

   * Creare un `DistillerServiceClient` utilizzando il costruttore predefinito.
   * Creare un `DistillerServiceClient.Endpoint.Address` oggetto utilizzando `System.ServiceModel.EndpointAddress` costruttore. Passa un valore stringa che specifica il file WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/DistillerService?blob=mtom`.) Non è necessario utilizzare il `lc_version` attributo. Questo attributo viene utilizzato quando si crea un riferimento a un servizio. Tuttavia, specifica `?blob=mtom` per utilizzare MTOM.
   * Creare un `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto ottenendo il valore del `DistillerServiceClient.Endpoint.Binding` campo. Invia il valore restituito a `BasicHttpBinding`.
   * Imposta il `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegna al campo il nome utente dei moduli AEM `DistillerServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore password corrispondente al campo `DistillerServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recuperate il file da convertire.

   * Creare un `BLOB` mediante il costruttore. Questo `BLOB` L&#39;oggetto viene utilizzato per memorizzare il file da convertire in un documento PDF.
   * Creare un `System.IO.FileStream` richiamando il relativo costruttore e passando un valore stringa che rappresenta la posizione del file e la modalità di apertura del file in.
   * Creare una matrice di byte che memorizza il contenuto della `System.IO.FileStream` oggetto. È possibile determinare le dimensioni della matrice di byte ottenendo `System.IO.FileStream` dell&#39;oggetto `Length` proprietà.
   * Compilare la matrice di byte con i dati di flusso richiamando `System.IO.FileStream` dell&#39;oggetto `Read` e passando la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare il `BLOB` oggetto assegnando il relativo `MTOM` con il contenuto della matrice di byte.

1. Richiama l’operazione di creazione di PDF.

   Richiama `DistillerServiceService` dell&#39;oggetto `CreatePDF2` e trasmettere i seguenti valori richiesti:

   * Il `BLOB` oggetto che rappresenta il file PS da convertire
   * Una stringa che contiene il percorso del file da convertire
   * Oggetto stringa contenente le impostazioni Adobe PDF da utilizzare (ad esempio, `Standard`)
   * Oggetto stringa contenente le impostazioni di protezione da utilizzare (ad esempio, `No Securit`y)
   * Un&#39;opzione `BLOB` oggetto contenente le impostazioni da applicare durante la generazione del documento PDF
   * Un&#39;opzione `BLOB` oggetto contenente informazioni sui metadati da applicare al documento PDF
   * A `BLOB` parametro di output utilizzato per memorizzare il documento PDF
   * A `BLOB` parametro di output utilizzato per memorizzare il registro

1. Salvare il documento PDF.

   * Creare un `System.IO.FileStream` richiamando il relativo costruttore. Passa un valore stringa che rappresenta la posizione del file del documento PDF firmato e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto della `BLOB` oggetto restituito da `CreatePDF2` (il parametro di output). Popolare la matrice di byte ottenendo il valore della `BLOB` dell&#39;oggetto `MTOM` membro dati.
   * Creare un `System.IO.BinaryWriter` oggetto richiamando il relativo costruttore e passando il `System.IO.FileStream` oggetto.
   * Scrivere il contenuto della matrice di byte in un file PDF richiamando `System.IO.BinaryWriter` dell&#39;oggetto `Write` e passando la matrice di byte.

**Consulta anche**

[Riepilogo dei passaggi](converting-postscript-pdf-documents.md#summary-of-steps)

<!-- UNRESOLVED LINKS
[Quick Start (MTOM): Converting a PostScript file to a PDF document using the web service API](unresolvedlink-lc-qs-distiller-di.xml#ws624e3cba99b79e12e69a9941333732bac8-7f01.2)

[Quick Start (SwaRef): Converting a PostScript file to a PDF document using the web service API](unresolvedlink-lc-qs-distiller-di.xml#ws624e3cba99b79e12e69a9941333732bac8-7eff.2)
-->

[Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamare AEM Forms con SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
