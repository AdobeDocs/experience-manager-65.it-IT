---
title: Conversione di PostScript in documenti PDF
description: Utilizza il servizio Distiller per convertire i file PostScript®, Encapsulated PostScript (EPS) e PRN in file PDF compatti, affidabili e più sicuri in rete. Il servizio Distiller converte grandi quantità di documenti di stampa in documenti elettronici, ad esempio fatture e rendiconti, utilizzando l'API Java e l'API del servizio Web.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 744df8b2-0c61-410f-89e9-20b8adddbf45
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1315'
ht-degree: 0%

---

# Conversione di PostScript in documenti PDF {#converting-postscript-to-pdf-documents}

**Gli esempi e gli esempi contenuti in questo documento sono solo per AEM Forms in ambiente JEE.**

## Informazioni sul servizio Distiller {#about-the-distiller-service}

Il servizio Distiller® converte i file PostScript®, EPS (Encapsulated PostScript) e PRN in file PDF compatti, affidabili e più sicuri in rete. Il servizio Distiller viene spesso utilizzato per convertire grandi quantità di documenti stampati in documenti elettronici, come fatture e rendiconti. La conversione dei documenti in PDF consente inoltre alle aziende di inviare ai propri clienti una versione cartacea e una versione elettronica di un documento.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Distiller, vedere [Riferimento ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Conversione di documenti PostScript in PDF {#converting-postscript-to-pdf-documents-inner}

In questo argomento viene descritto come utilizzare l&#39;API del servizio Distiller (Java e servizio Web) per convertire in modo programmatico i file PostScript (PS), Encapsulated PostScript (EPS) e PRN in documenti PDF.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Distiller, vedere [Riferimento ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Per convertire i file PostScript in documenti PDF AEM Forms, è necessario che nel server che ospita il pacchetto ridistribuibile Acrobat 9 o Microsoft Visual C++ 2005 sia installato uno dei seguenti elementi.

### Riepilogo dei passaggi {#summary-of-steps}

Per convertire uno qualsiasi dei tipi supportati in un documento PDF, effettuare le seguenti operazioni:

1. Includi file di progetto.
1. Creazione di un client di servizio Distiller.
1. Recuperate il file da convertire.
1. Richiama l’operazione di creazione di PDF.
1. Salvare il documento PDF.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

**Crea un client del servizio Distiller**

Prima di poter eseguire un&#39;operazione di servizio Distiller a livello di programmazione, è necessario creare un client di servizio Distiller. Se si utilizza l&#39;API Java, creare un oggetto `DistillerServiceClient`. Se si utilizza l&#39;API del servizio Web, creare un oggetto `DistillerServiceService`.

**Recupera il file da convertire**

Recuperate il file da convertire. Ad esempio, per convertire un file PS in un documento PDF, è necessario recuperare il file PS.

**Richiama l&#39;operazione di creazione di PDF**

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

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `DistillerServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Recuperate il file da convertire.

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il file da convertire utilizzando il relativo costruttore e passando un valore stringa che specifica la posizione del file.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Richiama l’operazione di creazione di PDF.

   Richiama il metodo `createPDF` dell&#39;oggetto `DistillerServiceClient` e passa i seguenti valori:

   * Oggetto `com.adobe.idp.Document` che rappresenta il file PS, EPS o PRN da convertire
   * Oggetto `java.lang.String` contenente il nome del file da convertire
   * Oggetto `java.lang.String` contenente il nome delle impostazioni Adobe PDF da utilizzare
   * Oggetto `java.lang.String` contenente il nome delle impostazioni di protezione da utilizzare
   * Oggetto `com.adobe.idp.Document` facoltativo contenente le impostazioni da applicare durante la generazione del documento PDF
   * Oggetto `com.adobe.idp.Document` facoltativo contenente informazioni sui metadati da applicare al documento PDF

   Il metodo `createPDF` restituisce un oggetto `CreatePDFResult` che contiene il nuovo documento PDF e un file di log che può essere generato. Il file di registro contiene in genere messaggi di errore o di avviso generati dalla richiesta di conversione.

1. Salvare il documento PDF.

   Per ottenere il documento di PDF appena creato, effettuare le seguenti operazioni:

   * Richiama il metodo `getCreatedDocument` dell&#39;oggetto `CreatePDFResult`. Restituisce un oggetto `com.adobe.idp.Document`.
   * Richiama il metodo `copyToFile` dell&#39;oggetto `com.adobe.idp.Document` per estrarre il documento PDF.

   Analogamente, per ottenere il documento di registro, effettuare le seguenti operazioni.

   * Richiama il metodo `getLogDocument` dell&#39;oggetto `CreatePDFResult`. Restituisce un oggetto `com.adobe.idp.Document`.
   * Richiama il metodo `copyToFile` dell&#39;oggetto `com.adobe.idp.Document` per estrarre il documento di log.

**Consulta anche**

[Riepilogo dei passaggi](converting-postscript-pdf-documents.md#summary-of-steps)

[Guida rapida (modalità SOAP): conversione di un file PostScript in un documento PDF tramite l’API Java](/help/forms/developing/distiller-service-java-api-quick.md#quick-start-soap-mode-converting-a-postscript-file-to-a-pdf-document-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Conversione di un file PostScript in PDF tramite l’API del servizio web {#converting-a-postscript-file-to-pdf-using-the-web-service-api}

Converti un file PostScript in documento PDF utilizzando l’API del servizio Distiller (servizio web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/DistillerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Creazione di un client di servizio Distiller.

   * Creare un oggetto `DistillerServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `DistillerServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/DistillerService?blob=mtom`). Non è necessario utilizzare l&#39;attributo `lc_version`. Questo attributo viene utilizzato quando si crea un riferimento a un servizio. Tuttavia, specificare `?blob=mtom` per utilizzare MTOM.
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `DistillerServiceClient.Endpoint.Binding`. Eseguire il cast del valore restituito in `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegnare il nome utente dei moduli AEM al campo `DistillerServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `DistillerServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recuperate il file da convertire.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. Questo oggetto `BLOB` viene utilizzato per memorizzare il file per la conversione in un documento PDF.
   * Creare un oggetto `System.IO.FileStream` richiamandone il costruttore e passando un valore stringa che rappresenta la posizione del file e la modalità di apertura del file in.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni della matrice di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare la matrice di byte con i dati di flusso richiamando il metodo `Read` dell&#39;oggetto `System.IO.FileStream` e passando la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando la relativa proprietà `MTOM` al contenuto della matrice di byte.

1. Richiama l’operazione di creazione di PDF.

   Richiama il metodo `CreatePDF2` dell&#39;oggetto `DistillerServiceService` e passa i seguenti valori richiesti:

   * Oggetto `BLOB` che rappresenta il file PS da convertire
   * Una stringa che contiene il percorso del file da convertire
   * Oggetto stringa contenente le impostazioni Adobe PDF da utilizzare (ad esempio, `Standard`)
   * Oggetto stringa contenente le impostazioni di protezione da utilizzare (ad esempio, `No Securit`y)
   * Oggetto `BLOB` facoltativo contenente le impostazioni da applicare durante la generazione del documento PDF
   * Oggetto `BLOB` facoltativo contenente informazioni sui metadati da applicare al documento PDF
   * Un parametro di output `BLOB` utilizzato per memorizzare il documento PDF
   * Un parametro di output `BLOB` utilizzato per memorizzare il registro

1. Salvare il documento PDF.

   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore. Passa un valore stringa che rappresenta la posizione del file del documento PDF firmato e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `BLOB` restituito dal metodo `CreatePDF2` (parametro di output). Popolare la matrice di byte ottenendo il valore del membro dati `MTOM` dell&#39;oggetto `BLOB`.
   * Creare un oggetto `System.IO.BinaryWriter` richiamandone il costruttore e passando l&#39;oggetto `System.IO.FileStream`.
   * Scrivere il contenuto della matrice di byte in un file PDF richiamando il metodo `Write` dell&#39;oggetto `System.IO.BinaryWriter` e passando la matrice di byte.

**Consulta anche**

[Riepilogo dei passaggi](converting-postscript-pdf-documents.md#summary-of-steps)

<!-- UNRESOLVED LINKS
[Quick Start (MTOM): Converting a PostScript file to a PDF document using the web service API](unresolvedlink-lc-qs-distiller-di.xml#ws624e3cba99b79e12e69a9941333732bac8-7f01.2)

[Quick Start (SwaRef): Converting a PostScript file to a PDF document using the web service API](unresolvedlink-lc-qs-distiller-di.xml#ws624e3cba99b79e12e69a9941333732bac8-7eff.2)
-->

[Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamare AEM Forms con SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
