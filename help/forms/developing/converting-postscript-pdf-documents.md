---
title: Conversione di PostScript in documenti PDF
seo-title: Conversione di PostScript in documenti PDF
description: 'null'
seo-description: 'null'
uuid: 2143f406-1fdd-4551-a738-1a8388f8d478
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 06ad343a-f74d-41f5-b3c8-b85bb723ceeb
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Conversione di PostScript in documenti PDF {#converting-postscript-to-pdf-documents}

## Informazioni sul servizio Distiller {#about-the-distiller-service}

Il servizio Distiller® converte i file PostScript®, Encapsulated PostScript (EPS) e PRN in file PDF compatti, affidabili e più sicuri in rete. Il servizio Distiller è spesso utilizzato per convertire grandi volumi di documenti stampati in documenti elettronici, come fatture e rendiconti. La conversione dei documenti in PDF consente inoltre alle aziende di inviare ai clienti una versione cartacea e una versione elettronica di un documento.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Distiller, consulta Riferimento [servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Conversione di PostScript in documenti PDF {#converting-postscript-to-pdf-documents-inner}

In questo argomento viene illustrato come utilizzare l&#39;API Distiller Service (Java e il servizio Web) per convertire i file PostScript (PS), Encapsulated PostScript (EPS) e PRN in documenti PDF a livello di programmazione.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Distiller, consulta Riferimento [servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Per convertire i file PostScript in documenti PDF, nel server in cui è installato AEM Forms deve essere installato uno dei seguenti file: Pacchetto ridistribuibile di Acrobat 9 o Microsoft Visual C++ 2005.

### Riepilogo dei passaggi {#summary-of-steps}

Per convertire uno dei tipi supportati in un documento PDF, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un client di servizi Distiller.
1. Recuperate il file da convertire.
1. Richiamate l’operazione di creazione PDF.
1. Salvare il documento PDF.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, accertatevi di includere i file proxy.

**Creare un client di servizio Distiller**

Prima di eseguire un&#39;operazione del servizio Distiller a livello di programmazione, è necessario creare un client del servizio Distiller. Se utilizzate l&#39;API Java, create un `DistillerServiceClient` oggetto. Se si utilizza l&#39;API del servizio Web, creare un `DistillerServiceService` oggetto.

**Recuperare il file da convertire**

È necessario recuperare il file da convertire. Ad esempio, per convertire un file PS in un documento PDF, dovete recuperare il file PS.

**Richiamo dell’operazione di creazione PDF**

Dopo aver creato il client di servizi, potete richiamare l’operazione di creazione PDF. Questa operazione richiede informazioni sul documento da convertire, compreso il percorso del documento di destinazione.

**Salvare il documento PDF**

È possibile salvare il documento PDF come file PDF.

**Consulta anche**

[Convertire un file PostScript in PDF utilizzando l&#39;API Java](converting-postscript-pdf-documents.md#convert-a-postscript-file-to-pdf-using-the-java-api)

[Conversione di un file PostScript in PDF tramite l&#39;API del servizio Web](converting-postscript-pdf-documents.md#converting-a-postscript-file-to-pdf-using-the-web-service-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API di Output Service](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Convertire un file PostScript in PDF utilizzando l&#39;API Java {#convert-a-postscript-file-to-pdf-using-the-java-api}

Convertire un file PostScript in un documento PDF utilizzando l&#39;API Distiller Service (Java):

1. Includere i file di progetto.

   Includete file JAR client, ad esempio adobe-distiller-client.jar, nel percorso di classe del progetto Java.

1. Creare un client di servizi Distiller.

   * Creare un `ServiceClientFactory` oggetto che contenga proprietà di connessione.
   * Creare un `DistillerServiceClient` oggetto utilizzando il relativo costruttore e passando l&#39; `ServiceClientFactory` oggetto.

1. Recuperate il file da convertire.

   * Creare un `java.io.FileInputStream` oggetto che rappresenta il file da convertire utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del file.
   * Creare un `com.adobe.idp.Document` oggetto utilizzando il relativo costruttore e passando l&#39; `java.io.FileInputStream` oggetto.

1. Richiamate l’operazione di creazione PDF.

   Richiama il metodo dell’ `DistillerServiceClient` oggetto `createPDF` e passa i seguenti valori:

   * L&#39; `com.adobe.idp.Document` oggetto che rappresenta il file PS, EPS o PRN da convertire
   * Un `java.lang.String` oggetto che contiene il nome del file da convertire
   * Un `java.lang.String` oggetto che contiene il nome delle impostazioni Adobe PDF da utilizzare
   * Un `java.lang.String` oggetto che contiene il nome delle impostazioni di protezione da utilizzare
   * Un `com.adobe.idp.Document` oggetto facoltativo che contiene le impostazioni da applicare durante la generazione del documento PDF
   * Un `com.adobe.idp.Document` oggetto facoltativo che contiene le informazioni sui metadati da applicare al documento PDF
   Il `createPDF` metodo restituisce un `CreatePDFResult` oggetto che contiene il nuovo documento PDF e un file di registro che può essere generato. Il file di registro in genere contiene messaggi di errore o di avviso generati dalla richiesta di conversione.

1. Salvare il documento PDF.

   Per ottenere il documento PDF appena creato, effettuare le seguenti operazioni:

   * Richiama il metodo dell’ `CreatePDFResult` oggetto `getCreatedDocument` . Questo restituisce un `com.adobe.idp.Document` oggetto.
   * Richiamare il metodo dell&#39; `com.adobe.idp.Document` oggetto `copyToFile` per estrarre il documento PDF.
   Analogamente, per ottenere il documento di registro, eseguire le operazioni seguenti.

   * Richiama il metodo dell’ `CreatePDFResult` oggetto `getLogDocument` . Questo restituisce un `com.adobe.idp.Document` oggetto.
   * Richiamare il metodo dell&#39; `com.adobe.idp.Document` oggetto `copyToFile` per estrarre il documento di registro.


**Consulta anche**

[Riepilogo dei passaggi](converting-postscript-pdf-documents.md#summary-of-steps)

[Avvio rapido (modalità SOAP): Conversione di un file PostScript in un documento PDF mediante l’API Java](/help/forms/developing/distiller-service-java-api-quick.md#quick-start-soap-mode-converting-a-postscript-file-to-a-pdf-document-using-the-java-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Conversione di un file PostScript in PDF tramite l&#39;API del servizio Web {#converting-a-postscript-file-to-pdf-using-the-web-service-api}

Convertire un file PostScript in PDF utilizzando l&#39;API Distiller Service (servizio Web):

1. Includere i file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/DistillerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituire `localhost` con l&#39;indirizzo IP del server in cui è installato AEM Forms.

1. Creare un client di servizi Distiller.

   * Creare un `DistillerServiceClient` oggetto utilizzando il relativo costruttore predefinito.
   * Creare un `DistillerServiceClient.Endpoint.Address` oggetto utilizzando il `System.ServiceModel.EndpointAddress` costruttore. Passa un valore di stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/DistillerService?blob=mtom`.) Non è necessario utilizzare l&#39; `lc_version` attributo. Questo attributo viene utilizzato quando create un riferimento a un servizio. Tuttavia, specificate `?blob=mtom` per utilizzare MTOM.
   * Creare un `System.ServiceModel.BasicHttpBinding` oggetto ottenendo il valore del `DistillerServiceClient.Endpoint.Binding` campo. Inserite il valore restituito in `BasicHttpBinding`.
   * Impostare il campo `System.ServiceModel.BasicHttpBinding` dell&#39; `MessageEncoding` oggetto su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilitate l&#39;autenticazione HTTP di base eseguendo le seguenti operazioni:

      * Assegnare il nome utente dei moduli AEM al campo `DistillerServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `DistillerServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recuperate il file da convertire.

   * Creare un `BLOB` oggetto utilizzando il relativo costruttore. Questo `BLOB` oggetto viene utilizzato per memorizzare il file da convertire in un documento PDF.
   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto dell&#39; `System.IO.FileStream` oggetto. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà dell&#39; `System.IO.FileStream` oggetto `Length` .
   * Compilare l&#39;array di byte con i dati del flusso richiamando il `System.IO.FileStream` `Read` metodo dell&#39;oggetto e passando l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39; `BLOB` oggetto assegnandone `MTOM` la proprietà con il contenuto dell&#39;array di byte.

1. Richiamate l’operazione di creazione PDF.

   Richiamare il metodo dell&#39; `DistillerServiceService` oggetto `CreatePDF2` e trasmettere i seguenti valori obbligatori:

   * L&#39; `BLOB` oggetto che rappresenta il file PS da convertire
   * Una stringa che contiene il nome percorso del file da convertire
   * Un oggetto stringa che contiene le impostazioni Adobe PDF da utilizzare (ad esempio, `Standard`)
   * Un oggetto stringa che contiene le impostazioni di protezione da utilizzare (ad esempio, `No Securit`y)
   * Un `BLOB` oggetto facoltativo che contiene le impostazioni da applicare durante la generazione del documento PDF
   * Un `BLOB` oggetto facoltativo che contiene le informazioni sui metadati da applicare al documento PDF
   * Parametro di `BLOB` output utilizzato per memorizzare il documento PDF
   * Un parametro `BLOB` di output utilizzato per memorizzare il registro

1. Salvare il documento PDF.

   * Creare un `System.IO.FileStream` oggetto richiamandone il costruttore. Passa un valore di stringa che rappresenta la posizione del file del documento PDF firmato e la modalità di apertura del file.
   * Create un array di byte che memorizza il contenuto dell&#39; `BLOB` oggetto restituito dal `CreatePDF2` metodo (il parametro di output). Compilare l&#39;array di byte ottenendo il valore del membro `BLOB` dati dell&#39; `MTOM` oggetto.
   * Creare un `System.IO.BinaryWriter` oggetto richiamando il relativo costruttore e passando l&#39; `System.IO.FileStream` oggetto.
   * Scrivere il contenuto dell&#39;array di byte in un file PDF richiamando il metodo dell&#39; `System.IO.BinaryWriter` oggetto `Write` e passando l&#39;array di byte.

**Consulta anche**

[Riepilogo dei passaggi](converting-postscript-pdf-documents.md#summary-of-steps)

<!-- UNRESOLVED LINKS
[Quick Start (MTOM): Converting a PostScript file to a PDF document using the web service API](unresolvedlink-lc-qs-distiller-di.xml#ws624e3cba99b79e12e69a9941333732bac8-7f01.2)

[Quick Start (SwaRef): Converting a PostScript file to a PDF document using the web service API](unresolvedlink-lc-qs-distiller-di.xml#ws624e3cba99b79e12e69a9941333732bac8-7eff.2)
-->

[Attivazione di moduli AEM tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamo di moduli AEM con SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
