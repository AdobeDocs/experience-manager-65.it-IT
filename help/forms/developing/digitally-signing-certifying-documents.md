---
title: Firma digitale e certificazione dei documenti
seo-title: Firma digitale e certificazione dei documenti
description: 'null'
seo-description: 'null'
uuid: 6331de8a-2a9c-45bf-89d2-29f1ad5cc856
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 42de04bf-25e4-4478-a411-38671ed871ae
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '16977'
ht-degree: 0%

---


# Firma digitale e certificazione dei documenti {#digitally-signing-and-certifying-documents}

**Informazioni su Signature Service**

Il servizio Firma consente alla tua organizzazione di proteggere la sicurezza e la privacy dei documenti Adobe PDF che distribuisce e riceve. Questo servizio utilizza firme digitali e certificazione per garantire che solo i destinatari desiderati possano modificare i documenti. Poiché le funzioni di protezione vengono applicate al documento stesso, il documento rimane protetto e controllato per l&#39;intero ciclo di vita. Un documento rimane protetto oltre il firewall, quando viene scaricato offline e quando viene inviato nuovamente all&#39;organizzazione.

>[!NOTE]
>
>È possibile creare un gestore di firme personalizzato per il servizio Signature che viene richiamato quando vengono richiamate determinate operazioni, ad esempio la firma di un documento PDF.

**Nomi dei campi firma**

Per alcune operazioni del servizio Firma è necessario specificare il nome del campo firma in cui viene eseguita l&#39;operazione. Ad esempio, durante la firma di un documento PDF è possibile specificare il nome del campo firma da firmare. Si supponga che il nome completo di un campo firma sia `form1[0].Form1[0].SignatureField1[0]`. Potete specificare `SignatureField1[0]` invece di `form1[0].Form1[0].SignatureField1[0]`.

A volte un conflitto causa la firma del campo errato da parte del servizio Firma (o un&#39;altra operazione che richiede il nome del campo firma). Questo conflitto è il risultato della `SignatureField1[0]` visualizzazione del nome in due o più punti dello stesso documento PDF. Ad esempio, si consideri un documento PDF che contiene due campi firma denominati `form1[0].Form1[0].SignatureField1[0]` e `form1[0].Form1[0].SubForm1[0].SignatureField1[0]` che è possibile specificare `SignatureField1[0]`. In questa situazione, il servizio Firma firma firma firma il primo campo da trovare durante l&#39;iterazione su tutti i campi firma del documento.

Se all&#39;interno di un documento PDF sono presenti più campi firma, è consigliabile specificare i nomi completi dei campi firma. Ovvero, specificate `form1[0].Form1[0].SignatureField1[0]`invece di `SignatureField1[0]`.

È possibile eseguire le operazioni seguenti utilizzando il servizio Firma:

* Aggiungere ed eliminare campi firma digitale a un documento PDF. (Vedere [Aggiunta di campi](digitally-signing-certifying-documents.md#adding-signature-fields)firma.)
* Recuperare i nomi dei campi firma presenti in un documento PDF. (Vedere [Recupero Dei Nomi](digitally-signing-certifying-documents.md#retrieving-signature-field-names)Dei Campi Firma.)
* Modificare i campi firma. (Vedere [Modifica dei campi](digitally-signing-certifying-documents.md#modifying-signature-fields)firma.)
* Firmare digitalmente i documenti PDF. (Vedere Firma [digitale di documenti](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)PDF.)
* Certificare documenti PDF. (Vedere [Certificazione di documenti](digitally-signing-certifying-documents.md#certifying-pdf-documents)PDF.)
* Convalidare le firme digitali presenti in un documento PDF. (Vedere [Verifica delle firme](digitally-signing-certifying-documents.md#verifying-digital-signatures)digitali.)
* Convalidare tutte le firme digitali presenti in un documento PDF. (Vedere [Verifica di più firme](digitally-signing-certifying-documents.md#verifying-digital-signatures)digitali.)
* Rimuovere una firma digitale da un campo firma. (Vedere [Rimozione delle firme](digitally-signing-certifying-documents.md#removing-digital-signatures)digitali.)

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Signature, vedere Riferimento [servizi per i AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Aggiunta di campi firma {#adding-signature-fields}

Le firme digitali vengono visualizzate nei campi firma, ovvero nei campi del modulo che contengono una rappresentazione grafica della firma. I campi firma possono essere visibili o invisibili. I firmatari possono utilizzare un campo firma preesistente oppure è possibile aggiungere un campo firma a livello di programmazione. In entrambi i casi, il campo firma deve esistere prima che sia possibile firmare un documento PDF.

È possibile aggiungere un campo firma a livello di programmazione utilizzando l&#39;API Java del servizio firma o l&#39;API del servizio Web Firma. È possibile aggiungere più campi firma a un documento PDF; tuttavia, ogni nome di campo firma deve essere univoco.

>[!NOTE]
>
>Alcuni tipi di documenti PDF non consentono l&#39;aggiunta programmatica di un campo firma. Per ulteriori informazioni sul servizio Firma e sull&#39;aggiunta di campi firma, vedere Riferimento [servizi per i AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary-of-steps}

Per aggiungere un campo firma a un documento PDF, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un client per le firme.
1. Ottenere un documento PDF al quale viene aggiunto un campo firma.
1. Aggiungere un campo firma.
1. Salvare il documento PDF come file PDF.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, accertatevi di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (richiesto se i AEM Forms sono distribuiti su JBoss)
* jbossall-client.jar (richiesto se i AEM Forms sono distribuiti su JBoss)

**Creare un client per le firme**

Prima di eseguire un&#39;operazione del servizio Firma a livello di programmazione, è necessario creare un client del servizio Firma.

**Ottenere un documento PDF a cui è aggiunto un campo firma**

È necessario ottenere un documento PDF al quale viene aggiunto un campo firma.

**Aggiunta di un campo firma**

Per aggiungere correttamente un campo firma a un documento PDF, è necessario specificare i valori delle coordinate che identificano la posizione del campo firma. Se si aggiunge un campo firma invisibile, questi valori non sono obbligatori. È inoltre possibile specificare quali campi del documento PDF vengono bloccati dopo che al campo firma è stata applicata la firma.

**Salvare il documento PDF come file PDF**

Dopo che il servizio Firma ha aggiunto un campo firma al documento PDF, è possibile salvare il documento come file PDF per consentirne l&#39;apertura in Acrobat o Adobe Reader.

**Consulta anche**

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Firma digitale di documenti PDF](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

### Aggiunta di campi firma tramite l&#39;API Java {#add-signature-fields-using-the-java-api}

Aggiungere un campo firma utilizzando l&#39;API Signature (Java):

1. Includi file di progetto

   Includete file JAR client, ad esempio adobe-signatures-client.jar, nel percorso di classe del progetto Java.

1. Creare un client per le firme

   * Creare un `ServiceClientFactory` oggetto che contenga proprietà di connessione.
   * Creare un `SignatureServiceClient` oggetto utilizzando il relativo costruttore e passando l&#39; `ServiceClientFactory` oggetto.

1. Ottenere un documento PDF a cui è aggiunto un campo firma

   * Creare un `java.io.FileInputStream` oggetto che rappresenta il documento PDF al quale viene aggiunto un campo firma utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del documento PDF.
   * Creare un `com.adobe.idp.Document` oggetto utilizzando il relativo costruttore e passando l&#39; `java.io.FileInputStream` oggetto.

1. Aggiunta di un campo firma

   * Creare un oggetto `PositionRectangle` che specifica la posizione del campo firma utilizzando il relativo costruttore. All&#39;interno del costruttore, specificate i valori delle coordinate.
   * Se necessario, creare un `FieldMDPOptions` oggetto che specifica i campi bloccati quando si applica una firma digitale al campo firma.
   * Aggiungere un campo firma a un documento PDF richiamando il metodo dell&#39; `SignatureServiceClient` oggetto `addSignatureField` e passando i seguenti valori:

      * A `com.adobe.idp`. `Document` che rappresenta il documento PDF al quale viene aggiunto un campo firma.
      * Una stringa che specifica il nome del campo firma.
      * Un `java.lang.Integer` valore che rappresenta il numero di pagina al quale viene aggiunto un campo firma.
      * Un `PositionRectangle` oggetto che specifica la posizione del campo firma.
      * Un `FieldMDPOptions` oggetto che specifica i campi del documento PDF bloccati dopo l&#39;applicazione di una firma digitale al campo firma. Questo valore di parametro è facoltativo e potete trasmettere `null`.
   * Un `PDFSeedValueOptions` oggetto che specifica vari valori di runtime. Questo valore di parametro è facoltativo e potete trasmettere `null`.

      Il `addSignatureField` metodo restituisce un `com.adobe.idp`. `Document` che rappresenta un documento PDF contenente un campo firma.
   >[!NOTE]
   >
   >È possibile richiamare il metodo dell&#39; `SignatureServiceClient` oggetto `addInvisibleSignatureField` per aggiungere un campo firma invisibile.

1. Salvare il documento PDF come file PDF

   * Create un `java.io.File` oggetto e accertatevi che l&#39;estensione del file sia .pdf.
   * Richiama il `com.adobe.idp`. `Document` metodo dell&#39;oggetto `copyToFile` per copiare il contenuto dell&#39; `Document` oggetto nel file. Accertatevi di utilizzare il `com.adobe.idp`. `Document` oggetto restituito dal `addSignatureField` metodo.

**Consulta anche**

[Avvio rapido dell&#39;API di Servizio firme](/help/forms/developing/signature-service-java-api-quick.md#signature-service-java-api-quick-start-soap)

### Aggiunta di campi firma tramite l&#39;API del servizio Web {#add-signature-fields-using-the-web-service-api}

Per aggiungere un campo firma utilizzando l&#39;API Signature (servizio Web):

1. Includi file di progetto

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituire `localhost` con l&#39;indirizzo IP del server host AEM Forms.

1. Creare un client per le firme

   * Creare un `SignatureServiceClient` oggetto utilizzando il relativo costruttore predefinito.
   * Creare un `SignatureServiceClient.Endpoint.Address` oggetto utilizzando il `System.ServiceModel.EndpointAddress` costruttore. Passate un valore di stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/SignatureService?WSDL`). Non è necessario utilizzare l&#39; `lc_version` attributo. Questo attributo viene utilizzato quando create un riferimento a un servizio.
   * Creare un `System.ServiceModel.BasicHttpBinding` oggetto ottenendo il valore del `SignatureServiceClient.Endpoint.Binding` campo. Inserite il valore restituito in `BasicHttpBinding`.
   * Impostare il campo `System.ServiceModel.BasicHttpBinding` dell&#39; `MessageEncoding` oggetto su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilitate l&#39;autenticazione HTTP di base eseguendo le seguenti operazioni:

      * Assegnare il nome utente dei moduli AEM al campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Ottenere un documento PDF a cui è aggiunto un campo firma

   * Creare un `BLOB` oggetto utilizzando il relativo costruttore. L&#39; `BLOB` oggetto viene utilizzato per memorizzare il documento PDF che conterrà un campo firma.
   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto dell&#39; `System.IO.FileStream` oggetto. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà dell&#39; `System.IO.FileStream` oggetto `Length` .
   * Compilare l&#39;array di byte con i dati del flusso richiamando il `System.IO.FileStream` `Read` metodo dell&#39;oggetto e passando l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39; `BLOB` oggetto assegnandone `MTOM` la proprietà con il contenuto dell&#39;array di byte.

1. Aggiunta di un campo firma

   Aggiungere un campo firma al documento PDF richiamando il metodo dell&#39; `SignatureServiceClient` oggetto `addSignatureField` e passando i seguenti valori:

   * Un `BLOB` oggetto che rappresenta il documento PDF al quale viene aggiunto un campo firma.
   * Una stringa che specifica il nome del campo firma.
   * Un valore intero che rappresenta il numero di pagina al quale viene aggiunto un campo firma.
   * Un `PositionRect` oggetto che specifica la posizione del campo firma.
   * Un `FieldMDPOptions` oggetto che specifica i campi del documento PDF bloccati dopo l&#39;applicazione di una firma digitale al campo firma. Questo valore di parametro è facoltativo e potete trasmettere `null`.
   * Un `PDFSeedValueOptions` oggetto che specifica vari valori di runtime. Questo valore di parametro è facoltativo e potete trasmettere `null`.

   Il `addSignatureField` metodo restituisce un `BLOB` oggetto che rappresenta un documento PDF contenente un campo firma.

1. Salvare il documento PDF come file PDF

   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF che conterrà il campo firma e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto dell&#39; `BLOB` oggetto restituito dal `addSignatureField` metodo. Compilare l&#39;array di byte ottenendo il valore del membro `BLOB` dati dell&#39; `binaryData` oggetto.
   * Creare un `System.IO.BinaryWriter` oggetto richiamando il relativo costruttore e passando l&#39; `System.IO.FileStream` oggetto.
   * Scrivere il contenuto dell&#39;array di byte in un file PDF richiamando il metodo dell&#39; `System.IO.BinaryWriter` oggetto `Write` e passando l&#39;array di byte.

**Consulta anche**

[Chiamata di AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chiamata di AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Recupero dei nomi dei campi firma {#retrieving-signature-field-names}

È possibile recuperare i nomi di tutti i campi firma presenti in un documento PDF che si desidera firmare o certificare. Se non si è certi dei nomi dei campi firma che si trovano in un documento PDF o si desidera verificarne i nomi, è possibile recuperarli a livello di programmazione. Il servizio Firma restituisce il nome completo del campo firma, ad esempio `form1[0].grantApplication[0].page1[0].SignatureField1[0]`.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Signature, vedere Riferimento [servizi per i AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)

### Riepilogo dei passaggi {#summary_of_steps-1}

Per recuperare i nomi dei campi firma, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un client per le firme.
1. Ottenere il documento PDF contenente i campi firma.
1. Recuperare i nomi dei campi firma.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, accertatevi di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (richiesto se i AEM Forms sono distribuiti su JBoss)
* jbossall-client.jar (richiesto se i AEM Forms sono distribuiti su JBoss)

Per informazioni sulla posizione di questi file JAR, vedere [Inclusione di file](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)libreria Java AEM Forms.

**Creare un client per le firme**

Prima di eseguire un&#39;operazione del servizio Firma a livello di programmazione, è necessario creare un client del servizio Firma.

**Ottenere il documento PDF contenente i campi firma**

Recuperare un documento PDF contenente campi firma.

**Recuperare i nomi dei campi firma**

È possibile recuperare i nomi dei campi firma dopo aver recuperato un documento PDF contenente uno o più campi firma.

**Consulta anche**

[Recupero dei nomi dei campi firma tramite l&#39;API Java](digitally-signing-certifying-documents.md#retrieve-signature-field-names-using-the-java-api)

[Recupero del campo firma tramite l&#39;API del servizio Web](digitally-signing-certifying-documents.md#retrieve-signature-field-using-the-web-service-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Aggiunta di campi firma](digitally-signing-certifying-documents.md#adding-signature-fields)

### Recupero dei nomi dei campi firma tramite l&#39;API Java {#retrieve-signature-field-names-using-the-java-api}

Recupera i nomi dei campi firma utilizzando l&#39;API Signature (Java):

1. Includi file di progetto

   Includete file JAR client, ad esempio adobe-signatures-client.jar, nel percorso di classe del progetto Java.

1. Creare un client per le firme

   * Creare un `ServiceClientFactory` oggetto che contenga proprietà di connessione.
   * Creare un `SignatureServiceClient` oggetto utilizzando il relativo costruttore e passando l&#39; `ServiceClientFactory` oggetto.

1. Ottenere il documento PDF contenente i campi firma

   * Creare un `java.io.FileInputStream` oggetto che rappresenta il documento PDF contenente campi firma utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del documento PDF.
   * Creare un `com.adobe.idp.Document` oggetto utilizzando il relativo costruttore e passando l&#39; `java.io.FileInputStream` oggetto.

1. Recuperare i nomi dei campi firma

   * Recuperare i nomi dei campi firma richiamando il metodo dell&#39; `SignatureServiceClient` oggetto `getSignatureFieldList` e passando l&#39;oggetto `com.adobe.idp.Document` che contiene il documento PDF contenente i campi firma. Questo metodo restituisce un `java.util.List` oggetto, in cui ogni elemento contiene un `PDFSignatureField` oggetto. Utilizzando questo oggetto, è possibile ottenere informazioni aggiuntive su un campo firma, ad esempio se è visibile o meno.
   * Eseguire un&#39;iterazione sull&#39; `java.util.List` oggetto per determinare se sono presenti nomi di campo firma. Per ciascun campo firma del documento PDF è possibile ottenere un `PDFSignatureField` oggetto a parte. Per ottenere il nome del campo firma, richiamare il metodo `PDFSignatureField` dell&#39;oggetto `getName` . Questo metodo restituisce un valore di stringa che specifica il nome del campo firma.

**Consulta anche**

[Recupero dei nomi dei campi firma](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

[Avvio rapido (modalità SOAP): Recupero dei nomi dei campi firma tramite l&#39;API Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-retrieving-signature-field-names-using-the-java-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Recupero del campo firma tramite l&#39;API del servizio Web {#retrieve-signature-field-using-the-web-service-api}

Recuperare i nomi dei campi firma utilizzando l&#39;API Signature (servizio Web):

1. Includi file di progetto

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituire `localhost` con l&#39;indirizzo IP del server host AEM Forms.

1. Creare un client per le firme

   * Creare un `SignatureServiceClient` oggetto utilizzando il relativo costruttore predefinito.
   * Creare un `SignatureServiceClient.Endpoint.Address` oggetto utilizzando il `System.ServiceModel.EndpointAddress` costruttore. Passate un valore di stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/SignatureService?WSDL`). Non è necessario utilizzare l&#39; `lc_version` attributo. Questo attributo viene utilizzato quando create un riferimento a un servizio.
   * Creare un `System.ServiceModel.BasicHttpBinding` oggetto ottenendo il valore del `SignatureServiceClient.Endpoint.Binding` campo. Inserite il valore restituito in `BasicHttpBinding`.
   * Impostare il campo `System.ServiceModel.BasicHttpBinding` dell&#39; `MessageEncoding` oggetto su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilitate l&#39;autenticazione HTTP di base eseguendo le seguenti operazioni:

      * Assegnare il nome utente dei moduli AEM al campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Ottenere il documento PDF contenente i campi firma

   * Creare un `BLOB` oggetto utilizzando il relativo costruttore. L&#39; `BLOB` oggetto viene utilizzato per memorizzare il documento PDF che contiene campi firma.
   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto dell&#39; `System.IO.FileStream` oggetto. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà dell&#39; `System.IO.FileStream` oggetto `Length` .
   * Compilare l&#39;array di byte con i dati del flusso richiamando il `System.IO.FileStream` `Read` metodo dell&#39;oggetto e passando l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39; `BLOB` oggetto assegnando al relativo `MTOM` campo il contenuto dell&#39;array di byte.

1. Recuperare i nomi dei campi firma

   * Recuperare i nomi dei campi firma richiamando il `SignatureServiceClient` metodo dell&#39; `getSignatureFieldList` oggetto e passando l&#39;oggetto `BLOB` che contiene il documento PDF contenente i campi firma. Questo metodo restituisce un oggetto `MyArrayOfPDFSignatureField` raccolta in cui ogni elemento contiene un `PDFSignatureField` oggetto.
   * Eseguire un&#39;iterazione sull&#39; `MyArrayOfPDFSignatureField` oggetto per determinare se sono presenti nomi di campo firma. Per ciascun campo firma del documento PDF è possibile ottenere un `PDFSignatureField` oggetto. Per ottenere il nome del campo firma, richiamare il metodo `PDFSignatureField` dell&#39;oggetto `getName` . Questo metodo restituisce un valore di stringa che specifica il nome del campo firma.

**Consulta anche**

[Recupero dei nomi dei campi firma](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

[Chiamata di AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chiamata di AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Modifica dei campi firma {#modifying-signature-fields}

È possibile modificare i campi firma che si trovano in un documento PDF utilizzando l&#39;API Java e l&#39;API del servizio Web. La modifica di un campo firma comporta la manipolazione dei valori del dizionario del blocco del campo firma o dei valori del dizionario dei valori iniziali.

Un dizionario *per il blocco dei* campi specifica un elenco di campi che vengono bloccati al momento della firma del campo firma. Un campo bloccato impedisce agli utenti di apportare modifiche al campo. Un dizionario *dei valori* iniziali contiene informazioni restrittive utilizzate al momento dell&#39;applicazione della firma. Ad esempio, è possibile modificare le autorizzazioni che controllano le azioni che possono verificarsi senza invalidare una firma.

Modificando un campo firma esistente, è possibile apportare modifiche al documento PDF per riflettere i diversi requisiti aziendali. Ad esempio, un nuovo requisito aziendale potrebbe richiedere il blocco di tutti i campi del documento dopo la firma del documento.

In questa sezione viene illustrato come modificare un campo firma modificando sia i valori del dizionario dei valori di blocco dei campi che i valori del dizionario dei valori dei valori iniziali. Le modifiche apportate al dizionario dei blocchi del campo firma causano il blocco di tutti i campi del documento PDF al momento della firma di un campo firma. Le modifiche apportate al dizionario dei valori iniziali non consentono l&#39;utilizzo di tipi specifici di modifiche al documento.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Firma e sulla modifica dei campi firma, vedere Riferimento [servizi per i AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-2}

Per modificare i campi firma contenuti in un documento PDF, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un client per le firme.
1. Ottenere il documento PDF contenente il campo firma da modificare.
1. Impostate i valori dei dizionari.
1. Modificare il campo firma.
1. Salvare il documento PDF come file PDF.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, accertatevi di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (richiesto se i AEM Forms sono distribuiti su JBoss)
* jbossall-client.jar (richiesto se i AEM Forms sono distribuiti su JBoss)

Per informazioni sulla posizione di questi file JAR, vedere [Inclusione di file](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)libreria Java di LiveCycle.

**Creare un client per le firme**

Prima di eseguire un&#39;operazione del servizio Firma a livello di programmazione, è necessario creare un client del servizio Firma.

**Ottenere il documento PDF contenente il campo firma da modificare**

Recuperare un documento PDF contenente il campo firma da modificare.

**Impostare i valori dei dizionari**

Per modificare un campo firma, assegnare valori al relativo dizionario di blocco del campo o al dizionario dei valori iniziali. Per specificare i valori del dizionario dei blocchi del campo firma è necessario specificare i campi del documento PDF che sono bloccati al momento della firma del campo firma. In questa sezione viene illustrato come bloccare tutti i campi.

È possibile impostare i seguenti valori del dizionario dei valori iniziali:

* **Controllo** revisione: Specifica se il controllo di revoca viene eseguito quando una firma viene applicata al campo firma.
* **Opzioni** certificato: Assegna valori al dizionario dei valori iniziali del certificato. Prima di specificare le opzioni del certificato, si consiglia di acquisire familiarità con un dizionario dei valori del certificato. (Vedere Riferimento [](https://www.adobe.com/devnet/acrobat/pdfs/pdf_reference_1-7.pdf)PDF.)
* **Opzioni** digest: Assegna algoritmi digest utilizzati per la firma. I valori validi sono SHA1, SHA256, SHA384, SHA512 e RIPEMD160.
* **Filtro**: Specifica il filtro utilizzato con il campo firma. Ad esempio, potete utilizzare il filtro Adobe.PPKLite. (Vedere Riferimento [](https://www.adobe.com/devnet/acrobat/pdfs/pdf_reference_1-7.pdf)PDF.)
* **Opzioni** contrassegno: Specifica i valori dei flag associati al campo firma. Il valore 1 indica che il firmatario deve utilizzare solo i valori specificati per la voce. Il valore 0 indica che sono consentiti altri valori. Ecco le posizioni Bit:

   * **1(Filtro):** Gestore di firme da utilizzare per firmare il campo firma
   * **2 (SubFilter):** Un array di nomi che indica codifiche accettabili da utilizzare per la firma
   * **3 (V)**: Numero di versione minimo richiesto del gestore di firme da utilizzare per firmare il campo firma
   * **4 (Motivi):** Un array di stringhe che specifica i possibili motivi per la firma di un documento
   * **5 (PDFLegalWarnings):** Un array di stringhe che specifica possibili attestazioni legali

* **Attestati** legali: Quando un documento è certificato, viene automaticamente analizzato per specifici tipi di contenuto che possono rendere il contenuto visibile di un documento ambiguo o fuorviante. Ad esempio, un’annotazione può oscurare il testo importante per comprendere ciò che viene certificato. Il processo di scansione genera avvisi che indicano la presenza di questo tipo di contenuto. Fornisce inoltre una spiegazione aggiuntiva del contenuto che potrebbe aver generato avvisi.
* **Autorizzazioni**: Specifica le autorizzazioni che possono essere utilizzate in un documento PDF senza invalidare la firma.
* **Motivi**: Specifica i motivi per cui il documento deve essere firmato.
* **Timestamp**: Specifica le opzioni di marca temporale. Ad esempio, è possibile impostare l&#39;URL del server di marca temporale utilizzato.
* **Versione**: Specifica il numero di versione minimo del gestore di firme da utilizzare per firmare il campo firma.

**Modifica del campo firma**

Dopo aver creato un client del servizio Firma, recuperare il documento PDF contenente il campo firma da modificare e impostare i valori del dizionario, è possibile richiedere al servizio Firma di modificare il campo firma. Il servizio Firma quindi restituisce un documento PDF contenente il campo firma modificato. Il documento PDF originale non viene modificato.

**Salvare il documento PDF come file PDF**

Salvare come file PDF il documento PDF contenente il campo firma modificato in modo che gli utenti possano aprirlo in Acrobat o Adobe Reader.

**Consulta anche**

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido dell&#39;API di Servizio firme](/help/forms/developing/signature-service-java-api-quick.md#signature-service-java-api-quick-start-soap)

[Firma digitale di documenti PDF](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

### Modificare i campi firma utilizzando l&#39;API Java {#modify-signature-fields-using-the-java-api}

Modificare un campo firma utilizzando l&#39;API Signature (Java):

1. Includi file di progetto

   Includete file JAR client, ad esempio adobe-signatures-client.jar, nel percorso di classe del progetto Java.

1. Creare un client per le firme

   * Creare un `ServiceClientFactory` oggetto che contenga proprietà di connessione.
   * Creare un `SignatureServiceClient` oggetto utilizzando il relativo costruttore e passando l&#39; `ServiceClientFactory` oggetto.

1. Ottenere il documento PDF contenente il campo firma da modificare

   * Creare un `java.io.FileInputStream` oggetto che rappresenta il documento PDF contenente il campo firma da modificare utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del documento PDF.
   * Creare un `com.adobe.idp.Document` oggetto utilizzando il relativo costruttore e passando l&#39; `java.io.FileInputStream` oggetto.

1. Impostare i valori dei dizionari

   * Creare un `PDFSignatureFieldProperties` oggetto utilizzando il relativo costruttore. Un `PDFSignatureFieldProperties` oggetto memorizza il dizionario del blocco del campo firma e le informazioni del dizionario dei valori iniziali.
   * Creare un `PDFSeedValueOptionSpec` oggetto utilizzando il relativo costruttore. Questo oggetto consente di impostare i valori del dizionario dei valori iniziali.
   * Non consentire modifiche al documento PDF richiamando il metodo dell&#39; `PDFSeedValueOptionSpec` oggetto `setMdpValue` e passando il valore di `MDPPermissions.NoChanges` enumerazione.
   * Creare un `FieldMDPOptionSpec` oggetto utilizzando il relativo costruttore. Questo oggetto consente di impostare i valori dei dizionari per il blocco dei campi firma.
   * Bloccare tutti i campi nel documento PDF richiamando il `FieldMDPOptionSpec` metodo dell&#39;oggetto `setMdpValue` e passando il valore di `FieldMDPAction.ALL` enumerazione.
   * Impostare le informazioni sul dizionario dei valori iniziali richiamando il `PDFSignatureFieldProperties` metodo dell&#39;oggetto `setSeedValue` e passando l&#39; `PDFSeedValueOptionSpec` oggetto.
   * Per impostare le informazioni sul dizionario del blocco del campo firma, richiamare il `PDFSignatureFieldProperties`metodo dell&#39; `setFieldMDP` oggetto e passare l&#39; `FieldMDPOptionSpec` oggetto.

   >[!NOTE]
   >
   >Per visualizzare tutti i valori del dizionario dei valori iniziali che è possibile impostare, vedere il riferimento alla `PDFSeedValueOptionSpec` classe. Consultate Riferimento API per [AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. Modifica del campo firma

   Modificare il campo firma richiamando il metodo dell&#39; `SignatureServiceClient` oggetto `modifySignatureField` e passando i seguenti valori:

   * L&#39; `com.adobe.idp.Document` oggetto che memorizza il documento PDF contenente il campo firma da modificare
   * Valore stringa che specifica il nome del campo firma
   * L&#39;oggetto `PDFSignatureFieldProperties` che memorizza il dizionario del blocco del campo firma e le informazioni sul dizionario dei valori iniziali

   Il `modifySignatureField` metodo restituisce un `com.adobe.idp.Document` oggetto che memorizza un documento PDF contenente il campo firma modificato.

1. Salvare il documento PDF come file PDF

   * Create un `java.io.File` oggetto e accertatevi che l&#39;estensione del nome del file sia .pdf.
   * Richiamare il metodo dell&#39; `com.adobe.idp.Document` oggetto `copyToFile` per copiare il contenuto dell&#39; `com.adobe.idp.Document` oggetto nel file. Assicurarsi di utilizzare l&#39; `com.adobe.idp.Document` oggetto restituito dal `modifySignatureField` metodo.

### Modificare i campi firma utilizzando l&#39;API del servizio Web {#modify-signature-fields-using-the-web-service-api}

Modificare un campo firma utilizzando l&#39;API Signature (servizio Web):

1. Includi file di progetto

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituire `localhost` con l&#39;indirizzo IP del server host AEM Forms.

1. Creare un client per le firme

   * Creare un `SignatureServiceClient` oggetto utilizzando il relativo costruttore predefinito.
   * Creare un `SignatureServiceClient.Endpoint.Address` oggetto utilizzando il `System.ServiceModel.EndpointAddress` costruttore. Passate un valore di stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/SignatureService?WSDL`). Non è necessario utilizzare l&#39; `lc_version` attributo. Questo attributo viene utilizzato quando create un riferimento a un servizio.
   * Creare un `System.ServiceModel.BasicHttpBinding` oggetto ottenendo il valore del `SignatureServiceClient.Endpoint.Binding` campo. Inserite il valore restituito in `BasicHttpBinding`.
   * Impostare il campo `System.ServiceModel.BasicHttpBinding` dell&#39; `MessageEncoding` oggetto su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilitate l&#39;autenticazione HTTP di base eseguendo le seguenti operazioni:

      * Assegnare il nome utente dei moduli AEM al campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Ottenere il documento PDF contenente il campo firma da modificare

   * Creare un `BLOB` oggetto utilizzando il relativo costruttore. L&#39; `BLOB` oggetto viene utilizzato per memorizzare il documento PDF contenente il campo firma da modificare.
   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto dell&#39; `System.IO.FileStream` oggetto. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà dell&#39; `System.IO.FileStream` oggetto `Length` .
   * Compilare l&#39;array di byte con i dati del flusso richiamando il `System.IO.FileStream` `Read` metodo dell&#39;oggetto e passando l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39; `BLOB` oggetto assegnando alla `MTOM` proprietà il contenuto dell&#39;array di byte.

1. Impostare i valori dei dizionari

   * Creare un `PDFSignatureFieldProperties` oggetto utilizzando il relativo costruttore. Questo oggetto memorizza il dizionario del blocco del campo firma e le informazioni del dizionario dei valori iniziali.
   * Creare un `PDFSeedValueOptionSpec` oggetto utilizzando il relativo costruttore. Questo oggetto consente di impostare i valori del dizionario dei valori iniziali.
   * Non consentire modifiche al documento PDF assegnando il valore di `MDPPermissions.NoChanges` enumerazione al membro `PDFSeedValueOptionSpec` dati dell&#39; `mdpValue` oggetto.
   * Creare un `FieldMDPOptionSpec` oggetto utilizzando il relativo costruttore. Questo oggetto consente di impostare i valori dei dizionari per il blocco dei campi firma.
   * Bloccare tutti i campi nel documento PDF assegnando il valore di `FieldMDPAction.ALL` enumerazione al membro `FieldMDPOptionSpec` dati dell&#39; `mdpValue` oggetto.
   * Impostare le informazioni sul dizionario dei valori iniziali assegnando l&#39; `PDFSeedValueOptionSpec` oggetto al membro `PDFSignatureFieldProperties` dei `seedValue` dati dell&#39;oggetto.
   * Impostare le informazioni sul dizionario dei blocchi del campo firma assegnando l&#39; `FieldMDPOptionSpec` oggetto al membro dei dati `PDFSignatureFieldProperties` dell&#39; `fieldMDP` oggetto.

   >[!NOTE]
   >
   >Per visualizzare tutti i valori del dizionario dei valori iniziali che è possibile impostare, vedere il riferimento alla `PDFSeedValueOptionSpec` classe. Consultate [Riferimento](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)API AEM Forms.

1. Modifica del campo firma

   Modificare il campo firma richiamando il metodo dell&#39; `SignatureServiceClient` oggetto `modifySignatureField` e passando i seguenti valori:

   * L&#39; `BLOB` oggetto che memorizza il documento PDF contenente il campo firma da modificare
   * Valore stringa che specifica il nome del campo firma
   * L&#39;oggetto `PDFSignatureFieldProperties` che memorizza il dizionario del blocco del campo firma e le informazioni sul dizionario dei valori iniziali

   Il `modifySignatureField` metodo restituisce un `BLOB` oggetto che memorizza un documento PDF contenente il campo firma modificato.

1. Salvare il documento PDF come file PDF

   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF che conterrà il campo firma e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto dell&#39; `BLOB` oggetto restituito dal `addSignatureField` metodo. Compilare l&#39;array di byte ottenendo il valore del membro `BLOB` dati dell&#39; `MTOM` oggetto.
   * Creare un `System.IO.BinaryWriter` oggetto richiamando il relativo costruttore e passando l&#39; `System.IO.FileStream` oggetto.
   * Scrivere il contenuto dell&#39;array di byte in un file PDF richiamando il metodo dell&#39; `System.IO.BinaryWriter` oggetto `Write` e passando l&#39;array di byte.

**Consulta anche**

[Chiamata di AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chiamata di AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Firma digitale di documenti PDF {#digitally-signing-pdf-documents}

Le firme digitali possono essere applicate ai documenti PDF per garantire un livello di protezione elevato. Le firme digitali, come le firme autografe, forniscono un mezzo mediante il quale i firmatari si identificano e pronunciano dichiarazioni su un documento. La tecnologia utilizzata per firmare digitalmente i documenti garantisce che sia il firmatario che i destinatari siano consapevoli di ciò che è stato firmato e che il documento non sia stato alterato dall&#39;apposizione della firma.

I documenti PDF sono firmati mediante la tecnologia a chiave pubblica. Un firmatario ha due chiavi: una chiave pubblica e una chiave privata. La chiave privata è memorizzata nella credenziale di un utente che deve essere disponibile al momento della firma. La chiave pubblica è memorizzata nel certificato dell&#39;utente e deve essere disponibile ai destinatari per convalidare la firma. Le informazioni sui certificati revocati si trovano negli elenchi di revoche di certificati (CRL) e nelle risposte del protocollo di stato del certificato online (OCSP) distribuite dalle autorità di certificazione (CA). L&#39;ora della firma può essere ottenuta da un&#39;origine affidabile nota come Autorità di marca temporale.

>[!NOTE]
>
>Prima di poter apporre una firma digitale a un documento PDF, è necessario assicurarsi di aggiungere il certificato ai AEM Forms. Un certificato viene aggiunto utilizzando la console di amministrazione o a livello di programmazione tramite l&#39;API di Trust Manager. (vedere [Importazione di credenziali tramite l&#39;API](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api)di Trust Manager).

È possibile firmare i documenti PDF a livello di programmazione. Durante la firma digitale di un documento PDF, è necessario fare riferimento a una credenziale di protezione esistente nei AEM Forms. La credenziale è la chiave privata utilizzata per la firma.

Durante la firma di un documento PDF, il servizio Firma esegue i seguenti passaggi:

1. Il servizio Signature recupera la credenziale dal TrustStore passando l&#39;alias specificato nella richiesta.
1. Il TrustStore cerca la credenziale specificata.
1. Le credenziali vengono restituite al servizio Firma e utilizzate per firmare il documento. La credenziale viene inoltre memorizzata nella cache rispetto all&#39;alias per richieste future.

Per informazioni sulla gestione delle credenziali di protezione, consultate la guida *Installazione e distribuzione di AEM Forms* per il server delle applicazioni.

>[!NOTE]
>
>Esistono differenze tra la firma e la certificazione dei documenti. (Vedere [Certificazione di documenti](digitally-signing-certifying-documents.md#certifying-pdf-documents)PDF.)

>[!NOTE]
>
>Non tutti i documenti PDF supportano la firma. Per ulteriori informazioni sul servizio Firma e sulla firma digitale dei documenti, vedere Riferimento [servizi per i AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Il servizio Signature non supporta i file XDP con dati PDF incorporati come input per un&#39;operazione, ad esempio la certificazione di un documento. Con questa azione il servizio Firma genera un `PDFOperationException`. Per risolvere il problema, convertire il file XDP in un file PDF utilizzando il servizio Utilità PDF, quindi passare il file PDF convertito a un&#39;operazione del servizio Firma. (Vedere [Utilizzo delle utility](/help/forms/developing/pdf-utilities.md#working-with-pdf-utilities)PDF.)

**Credenziali HSM di Cipher nShield**

Quando si utilizza una credenziale HSM di CipherShield per firmare o certificare un documento PDF, non è possibile utilizzare la nuova credenziale finché il server applicazione J2EE in cui sono stati distribuiti AEM Forms non viene riavviato. Tuttavia, è possibile impostare un valore di configurazione, in modo che l&#39;operazione di firma o certificazione funzioni senza riavviare il server applicazione J2EE.

Potete aggiungere il seguente valore di configurazione nel file cknfastrc, che si trova in /opt/nfast/cknfastrc (o c:\nfast\cknfastrc):

```shell
    CKNFAST_ASSUME_SINGLE_PROCESS=0
```

Dopo aver aggiunto questo valore di configurazione al file cknfastrc, è possibile utilizzare la nuova credenziale senza riavviare il server applicazione J2EE.

**Firma non attendibile**

Durante la certificazione e la firma dello stesso documento PDF, se la firma di certificazione non è affidabile, all&#39;apertura del documento PDF in Acrobat o Adobe Reader viene visualizzato un triangolo giallo contro la prima firma. La firma di certificazione deve essere ritenuta affidabile per evitare tale situazione.

**Firma di documenti basati su XFA**

Se si tenta di firmare un modulo basato su XFA utilizzando l&#39;API del servizio Firma, i dati potrebbero non essere presenti nella `View``Signed` posizione `Version` in Acrobat. Ad esempio, prendete in considerazione il seguente flusso di lavoro:

* Utilizzando un file XDP creato utilizzando Designer, è possibile unire una struttura del modulo contenente un campo firma e dati XML che contengono dati del modulo. Il servizio Moduli consente di generare un documento PDF interattivo.
* È possibile firmare il documento PDF utilizzando l&#39;API del servizio Firma.

### Riepilogo dei passaggi {#summary_of_steps-3}

Per firmare digitalmente un documento PDF, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un client del servizio Firma.
1. Richiedere la firma del documento PDF.
1. Firmare il documento PDF.
1. Salvare il documento PDF firmato come file PDF.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, accertatevi di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (richiesto se i AEM Forms sono distribuiti su JBoss)
* jbossall-client.jar (richiesto se i AEM Forms sono distribuiti su JBoss)

**Creare un client per firme**

Prima di eseguire un&#39;operazione del servizio Firma a livello di programmazione, è necessario creare un client del servizio Firma.

**Richiedere la firma del documento PDF**

Per firmare un documento PDF, è necessario ottenere un documento PDF contenente un campo firma. Se un documento PDF non contiene un campo firma, non può essere firmato. È possibile aggiungere un campo firma utilizzando Designer o a livello di programmazione.

**Firmare il documento PDF**

Durante la firma di un documento PDF, è possibile impostare le opzioni di esecuzione utilizzate dal servizio Firma. Potete impostare le seguenti opzioni:

* Opzioni di aspetto
* Controllo revoca
* Valori timestamp

È possibile impostare le opzioni di aspetto utilizzando un `PDFSignatureAppearanceOptionSpec` oggetto. Ad esempio, è possibile visualizzare la data all&#39;interno di una firma richiamando il metodo dell&#39; `PDFSignatureAppearanceOptionSpec` oggetto `setShowDate` e passando `true`.

È inoltre possibile specificare se eseguire o meno un controllo di revoca che determini la revoca del certificato utilizzato per firmare digitalmente un documento PDF. Per eseguire il controllo della revoca, è possibile specificare uno dei seguenti valori:

* **NoCheck**: Non eseguire il controllo della revoca.
* **BestEffort**: Tentate sempre di verificare la revoca di tutti i certificati nella catena. Se si verifica un problema nella verifica, si presume che la revoca sia valida. Se si verifica un errore, si supponga che il certificato non venga revocato.
* **CheckIfAvailable:** Verificare la revoca di tutti i certificati nella catena se sono disponibili informazioni sulla revoca. Se si verifica un problema nella verifica, si presume che la revoca non sia valida. Se si verifica un errore, si presuppone che il certificato sia revocato e non sia valido. Questo è il valore predefinito.
* **AlwaysCheck**: Verificare la revoca di tutti i certificati nella catena. Se le informazioni sulla revoca non sono presenti in alcun certificato, si presume che la revoca non sia valida.

Per eseguire il controllo della revoca su un certificato, è possibile specificare un URL di un server dell&#39;elenco di revoche di certificati (CRL) utilizzando un `CRLOptionSpec` oggetto. Tuttavia, se si desidera eseguire il controllo delle revoche e non si specifica un URL per un server CRL, il servizio Signature ottiene l&#39;URL dal certificato.

Invece di utilizzare un server CRL, è possibile utilizzare un server OCSP (Certificate Status Protocol) online durante il controllo delle revoche. In genere, quando si utilizza un server OCSP anziché un server CRL, il controllo di revoca viene eseguito più rapidamente. (vedere &quot;Protocollo di stato del certificato online&quot; all&#39;indirizzo [https://tools.ietf.org/html/rfc2560](https://tools.ietf.org/html/rfc2560).)

È possibile impostare l&#39;ordine del server CRL e OCSP utilizzato dal servizio Signature utilizzando Adobe Applications and Services. Ad esempio, se il server OCSP è impostato per primo in Adobe Applications and Services, il server OCSP è selezionato, seguito dal server CRL. (vedere &quot;Gestione di certificati e credenziali tramite Trust Store&quot; nell&#39;Aiuto di AAC).

Se si specifica di non eseguire il controllo di revoca, il servizio Firma non controlla se il certificato utilizzato per firmare o certificare un documento è stato revocato. In altre parole, le informazioni relative al server CRL e OCSP vengono ignorate.

>[!NOTE]
>
>Sebbene sia possibile specificare un CRL o un server OCSP nel certificato, è possibile sostituire l&#39;URL specificato nel certificato utilizzando un `CRLOptionSpec` oggetto e un `OCSPOptionSpec` oggetto. Ad esempio, per ignorare il server CRL, è possibile richiamare il metodo dell&#39; `CRLOptionSpec` oggetto `setLocalURI` .

La marca temporale indica il processo di tracciamento dell&#39;ora in cui un documento firmato o certificato è stato modificato. Una volta firmato, il documento non deve essere modificato, neanche dal proprietario del documento. La marca temporale consente di applicare la validità di un documento firmato o certificato. È possibile impostare le opzioni di marca temporale utilizzando un `TSPOptionSpec` oggetto. Ad esempio, potete specificare l&#39;URL di un server provider di marca temporale (TSP).

>[!NOTE]
>
>In Java e nel servizio Web passano attraverso le sezioni e il relativo avvio rapido, viene utilizzato il controllo delle revoche. Poiché non sono specificate informazioni sul server CRL o OCSP, le informazioni sul server vengono ottenute dal certificato utilizzato per firmare digitalmente il documento PDF.

Per firmare correttamente un documento PDF, è possibile specificare il nome completo del campo firma che conterrà la firma digitale, ad esempio `form1[0].#subform[1].SignatureField3[3]`. Quando si utilizza un campo modulo XFA, è possibile utilizzare anche il nome parziale del campo firma: `SignatureField3[3]`.

È inoltre necessario fare riferimento a una credenziale di protezione per firmare digitalmente un documento PDF. Per fare riferimento a una credenziale di protezione, è necessario specificare un alias. L’alias è un riferimento a una credenziale effettiva che potrebbe trovarsi in un file PKCS#12 (con estensione .pfx) o in un modulo di protezione hardware (HSM). Per informazioni sulle credenziali di protezione, vedere la guida *Installazione e distribuzione di AEM Forms* per il server delle applicazioni.

**Salvare il documento PDF firmato**

Dopo che il servizio Firma ha apposto la firma digitale al documento PDF, è possibile salvarlo come file PDF per consentire agli utenti di aprirlo in Acrobat o Adobe Reader.

**Consulta anche**

[Firma digitale di documenti PDF tramite l&#39;API Java](digitally-signing-certifying-documents.md#digitally-sign-pdf-documents-using-the-java-api)

[Firma digitale di documenti PDF tramite l&#39;API del servizio Web](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents-using-the-web-service-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Aggiunta di campi firma](digitally-signing-certifying-documents.md#adding-signature-fields)

[Recupero dei nomi dei campi firma](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

### Firma digitale di documenti PDF tramite l&#39;API Java {#digitally-sign-pdf-documents-using-the-java-api}

Firmare digitalmente un documento PDF utilizzando l&#39;API Signature (Java):

1. Includi file di progetto

   Includete file JAR client, ad esempio adobe-signatures-client.jar, nel percorso di classe del progetto Java.

1. Creare un client per firme

   * Creare un `ServiceClientFactory` oggetto che contenga proprietà di connessione.
   * Creare un `SignatureServiceClient` oggetto utilizzando il relativo costruttore e passando l&#39; `ServiceClientFactory` oggetto.

1. Richiedere la firma del documento PDF

   * Creare un oggetto `java.io.FileInputStream` che rappresenti il documento PDF da firmare digitalmente utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del documento PDF.
   * Creare un `com.adobe.idp.Document` oggetto utilizzando il relativo costruttore e passando l&#39; `java.io.FileInputStream` oggetto.

1. Firmare il documento PDF

   Firmare il documento PDF richiamando il metodo dell&#39; `SignatureServiceClient` oggetto `sign` e passando i seguenti valori:

   * Un `com.adobe.idp.Document` oggetto che rappresenta il documento PDF da firmare.
   * Una stringa che rappresenta il nome del campo firma che conterrà la firma digitale.
   * Un `Credential` oggetto che rappresenta la credenziale utilizzata per firmare digitalmente il documento PDF. Creare un `Credential` oggetto richiamando il `Credential` metodo statico dell&#39; `getInstance` oggetto e passando un valore di stringa che specifica il valore alias corrispondente alla credenziale di sicurezza.
   * Un `HashAlgorithm` oggetto che specifica un membro di dati statici che rappresenta l&#39;algoritmo hash da utilizzare per rigenerare il documento PDF. Ad esempio, potete specificare `HashAlgorithm.SHA1` l&#39;utilizzo dell&#39;algoritmo SHA1.
   * Valore stringa che rappresenta il motivo per cui il documento PDF è stato firmato digitalmente.
   * Una stringa che rappresenta le informazioni di contatto del firmatario.
   * Un `PDFSignatureAppearanceOptions` oggetto che controlla l&#39;aspetto della firma digitale. Ad esempio, è possibile utilizzare questo oggetto per aggiungere un logo personalizzato a una firma digitale.
   * Un `java.lang.Boolean` oggetto che specifica se eseguire il controllo di revoca sul certificato del firmatario.
   * Un `OCSPOptionSpec` oggetto che memorizza le preferenze per il supporto del protocollo OCSP (Online Certificate Status Protocol). Se il controllo della revoca non viene eseguito, questo parametro non viene utilizzato e potete specificare `null`.
   * Un `CRLPreferences` oggetto che memorizza le preferenze dell&#39;elenco di revoca dei certificati (CRL, Certificate Revocation List). Se il controllo della revoca non viene eseguito, questo parametro non viene utilizzato e potete specificare `null`.
   * Un `TSPPreferences` oggetto che memorizza le preferenze per il supporto del provider di marca temporale (TSP). Questo parametro è facoltativo e può essere `null`. Per ulteriori informazioni, consulta [AEM Forms API Reference](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)(Riferimento API per gli ).

   Il `sign` metodo restituisce un `com.adobe.idp.Document` oggetto che rappresenta il documento PDF firmato.

1. Salvare il documento PDF firmato

   * Create un `java.io.File` oggetto e accertatevi che l&#39;estensione del file sia .pdf.
   * Richiamare il `com.adobe.idp.Document` metodo dell&#39; `copyToFile` oggetto e passare `java.io.File`al file il contenuto dell&#39; `Document` oggetto. Assicurarsi di utilizzare l&#39; `com.adobe.idp.Document` oggetto restituito dal `sign` metodo.

**Consulta anche**

[Firma digitale di documenti PDF](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[Avvio rapido (modalità SOAP): Firma digitale di un documento PDF tramite l&#39;API Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-pdf-document-using-the-java-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Firma digitale di documenti PDF tramite l&#39;API del servizio Web {#digitally-signing-pdf-documents-using-the-web-service-api}

Per firmare digitalmente un documento PDF utilizzando l&#39;API Signature (servizio Web):

1. Includi file di progetto

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituire `localhost` con l&#39;indirizzo IP del server host AEM Forms.

1. Creare un client per firme

   * Creare un `SignatureServiceClient` oggetto utilizzando il relativo costruttore predefinito.
   * Creare un `SignatureServiceClient.Endpoint.Address` oggetto utilizzando il `System.ServiceModel.EndpointAddress` costruttore. Passate un valore di stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/SignatureService?WSDL`). Non è necessario utilizzare l&#39; `lc_version` attributo. Questo attributo viene utilizzato quando create un riferimento a un servizio.
   * Creare un `System.ServiceModel.BasicHttpBinding` oggetto ottenendo il valore del `SignatureServiceClient.Endpoint.Binding` campo. Inserite il valore restituito in `BasicHttpBinding`.
   * Impostare il campo `System.ServiceModel.BasicHttpBinding` dell&#39; `MessageEncoding` oggetto su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilitate l&#39;autenticazione HTTP di base eseguendo le seguenti operazioni:

      * Assegnare il nome utente dei moduli AEM al campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Richiedere la firma del documento PDF

   * Creare un `BLOB` oggetto utilizzando il relativo costruttore. L&#39; `BLOB` oggetto viene utilizzato per memorizzare un documento PDF firmato.
   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF da firmare e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto dell&#39; `System.IO.FileStream` oggetto. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà dell&#39; `System.IO.FileStream` oggetto `Length` .
   * Compilare l&#39;array di byte con i dati del flusso richiamando il `System.IO.FileStream` `Read` metodo dell&#39;oggetto e passando l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39; `BLOB` oggetto assegnando alla `MTOM` proprietà il contenuto dell&#39;array di byte.

1. Firmare il documento PDF

   Firmare il documento PDF richiamando il metodo dell&#39; `SignatureServiceClient` oggetto `sign` e passando i seguenti valori:

   * Un `BLOB` oggetto che rappresenta il documento PDF da firmare.
   * Una stringa che rappresenta il nome del campo firma che conterrà la firma digitale.
   * Un `Credential` oggetto che rappresenta la credenziale utilizzata per firmare digitalmente il documento PDF. Creare un `Credential` oggetto utilizzando il relativo costruttore e specificare l&#39;alias assegnando un valore alla `Credential` proprietà dell&#39; `alias` oggetto.
   * Un `HashAlgorithm` oggetto che specifica un membro di dati statici che rappresenta l&#39;algoritmo hash da utilizzare per rigenerare il documento PDF. Ad esempio, potete specificare `HashAlgorithm.SHA1` l&#39;utilizzo dell&#39;algoritmo SHA1.
   * Un valore booleano che specifica se utilizzare l&#39;algoritmo hash.
   * Valore stringa che rappresenta il motivo per cui il documento PDF è stato firmato digitalmente.
   * Un valore di stringa che rappresenta la posizione del firmatario.
   * Una stringa che rappresenta le informazioni di contatto del firmatario.
   * Un `PDFSignatureAppearanceOptions` oggetto che controlla l&#39;aspetto della firma digitale. Ad esempio, è possibile utilizzare questo oggetto per aggiungere un logo personalizzato a una firma digitale.
   * Un `System.Boolean` oggetto che specifica se eseguire il controllo di revoca sul certificato del firmatario. Se il controllo di revoca viene eseguito, viene incorporato nella firma. Il valore predefinito è `false`.
   * Un `OCSPOptionSpec` oggetto che memorizza le preferenze per il supporto del protocollo OCSP (Online Certificate Status Protocol). Se il controllo della revoca non viene eseguito, questo parametro non viene utilizzato e potete specificare `null`. Per informazioni su questo oggetto, vedere Riferimento API per [AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * Un `CRLPreferences` oggetto che memorizza le preferenze dell&#39;elenco di revoca dei certificati (CRL, Certificate Revocation List). Se il controllo della revoca non viene eseguito, questo parametro non viene utilizzato e potete specificare `null`.
   * Un `TSPPreferences` oggetto che memorizza le preferenze per il supporto del provider di marca temporale (TSP). Questo parametro è facoltativo e può essere `null`.

   Il `sign` metodo restituisce un `BLOB` oggetto che rappresenta il documento PDF firmato.

1. Salvare il documento PDF firmato

   * Creare un `System.IO.FileStream` oggetto richiamandone il costruttore. Passa un valore di stringa che rappresenta la posizione del file del documento PDF firmato e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto dell&#39; `BLOB` oggetto restituito dal `sign` metodo. Compilare l&#39;array di byte ottenendo il valore del membro `BLOB` dati dell&#39; `MTOM` oggetto.
   * Creare un `System.IO.BinaryWriter` oggetto richiamando il relativo costruttore e passando l&#39; `System.IO.FileStream` oggetto.
   * Scrivere il contenuto dell&#39;array di byte in un file PDF richiamando il metodo dell&#39; `System.IO.BinaryWriter` oggetto `Write` e passando l&#39;array di byte.

**Consulta anche**

[Firma digitale di documenti PDF](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[Chiamata di AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chiamata di AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Firma digitale di moduli interattivi {#digitally-signing-interactive-forms}

È possibile firmare un modulo interattivo creato dal servizio Forms. Ad esempio, prendete in considerazione il seguente flusso di lavoro:

* È possibile unire un modulo PDF basato su XFA creato utilizzando Designer e i dati del modulo contenuti in un documento XML utilizzando il servizio Forms. Il server Forms esegue il rendering di un modulo interattivo.
* È possibile firmare il modulo interattivo utilizzando l&#39;API del servizio firma.

Il risultato è un modulo PDF interattivo con firma digitale. Durante la firma di un modulo PDF basato su un modulo XFA, è necessario salvare il file PDF come modulo PDF statico di Adobe. Se si tenta di firmare un modulo PDF salvato come modulo PDF dinamico Adobe, si verifica un&#39;eccezione. Poiché si firma il modulo restituito dal servizio Forms, assicurarsi che contenga un campo firma.

>[!NOTE]
>
>Prima di poter firmare digitalmente un modulo interattivo, è necessario assicurarsi di aggiungere il certificato ai AEM Forms. Un certificato viene aggiunto utilizzando la console di amministrazione o a livello di programmazione tramite l&#39;API di Trust Manager. (vedere [Importazione di credenziali tramite l&#39;API](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api)di Trust Manager).

Quando si utilizza l&#39;API di Forms Service, impostare l&#39;opzione di `GenerateServerAppearance` esecuzione su `true`. Questa opzione in fase di esecuzione assicura che l&#39;aspetto del modulo generato sul server resti valido se aperto in Acrobat o Adobe Reader. È consigliabile impostare questa opzione di esecuzione al momento della generazione di un modulo interattivo da firmare tramite l&#39;API Forms.

>[!NOTE]
>
>Prima di leggere la firma digitale dei moduli interattivi, è consigliabile avere familiarità con la firma dei documenti PDF. (Vedere Firma [digitale di documenti](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)PDF.)

### Riepilogo dei passaggi {#summary_of_steps-4}

Per firmare digitalmente un modulo interattivo restituito dal servizio Forms, eseguire le operazioni seguenti:

1. Includere i file di progetto.
1. Creare un client Forms e Signatures.
1. Ottenere il modulo interattivo utilizzando il servizio Forms.
1. Firmare il modulo interattivo.
1. Salvare il documento PDF firmato come file PDF.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, accertatevi di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-forms-client.jar
* adobe-utilities.jar (richiesto se i AEM Forms sono distribuiti su JBoss)
* jbossall-client.jar (richiesto se i AEM Forms sono distribuiti su JBoss)

Per informazioni sulla posizione di questi file JAR, vedere [Inclusione di file](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)libreria Java AEM Forms.

**Creare un client Forms e Signatures**

Poiché in questo flusso di lavoro vengono richiamati sia i servizi Forms che i servizi Signature, è necessario creare sia un client del servizio Forms che un client del servizio Signature.

**Ottenere il modulo interattivo utilizzando il servizio Forms**

È possibile utilizzare il servizio Moduli per ottenere il modulo PDF interattivo da firmare. Come AEM Forms, è possibile trasmettere un `com.adobe.idp.Document` oggetto al servizio Forms che contiene il modulo da eseguire. Il nome di questo metodo è `renderPDFForm2`. Questo metodo restituisce un `com.adobe.idp.Document` oggetto che contiene il modulo da firmare. È possibile trasmettere questa `com.adobe.idp.Document` istanza al servizio Signature.

Analogamente, se si utilizzano i servizi Web, è possibile trasmettere l&#39; `BLOB` istanza restituita dal servizio Forms al servizio Signature.

>[!NOTE]
>
>L&#39;avvio rapido associato alla sezione Moduli interattivi per la firma digitale richiama il `renderPDFForm2` metodo.

**Firmare il modulo interattivo**

Durante la firma di un documento PDF, è possibile impostare le opzioni di esecuzione utilizzate dal servizio Firma. Potete impostare le seguenti opzioni:

* Opzioni di aspetto
* Controllo revoca
* Valori timestamp

È possibile impostare le opzioni di aspetto utilizzando un `PDFSignatureAppearanceOptionSpec` oggetto. Ad esempio, è possibile visualizzare la data all&#39;interno di una firma richiamando il metodo dell&#39; `PDFSignatureAppearanceOptionSpec` oggetto `setShowDate` e passando `true`.

**Salvare il documento PDF firmato**

Dopo che il servizio Firma ha apposto la firma digitale al documento PDF, è possibile salvarlo come file PDF. Il file PDF può essere aperto in Acrobat o Adobe Reader.

**Consulta anche**

[Firmare digitalmente un modulo interattivo utilizzando l&#39;API Java](digitally-signing-certifying-documents.md#digitally-sign-an-interactive-form-using-the-java-api)

[Firma digitale di un modulo interattivo tramite l&#39;API del servizio Web](digitally-signing-certifying-documents.md#digitally-sign-an-interactive-form-using-the-web-service-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Firma digitale di documenti PDF](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[Rendering di PDF forms interattivi](/help/forms/developing/rendering-forms.md#rendering-interactive-pdf-forms)

### Firmare digitalmente un modulo interattivo utilizzando l&#39;API Java {#digitally-sign-an-interactive-form-using-the-java-api}

Firmare digitalmente un modulo interattivo utilizzando l&#39;API Forms e Signature (Java):

1. Includi file di progetto

   Includete file JAR client, ad esempio adobe-signatures-client.jar e adobe-forms-client.jar, nel percorso di classe del progetto Java.

1. Creare un client Forms e Signatures

   * Creare un `ServiceClientFactory` oggetto che contenga proprietà di connessione.
   * Creare un `SignatureServiceClient` oggetto utilizzando il relativo costruttore e passando l&#39; `ServiceClientFactory` oggetto.
   * Creare un `FormsServiceClient` oggetto utilizzando il relativo costruttore e passando l&#39; `ServiceClientFactory` oggetto.

1. Ottenere il modulo interattivo utilizzando il servizio Forms

   * Creare un `java.io.FileInputStream` oggetto che rappresenta il documento PDF da trasmettere al servizio Forms utilizzando il relativo costruttore. Passa un valore di stringa che specifica la posizione del documento PDF.
   * Creare un `com.adobe.idp.Document` oggetto utilizzando il relativo costruttore e passando l&#39; `java.io.FileInputStream` oggetto.
   * Creare un `java.io.FileInputStream` oggetto che rappresenta il documento XML contenente i dati del modulo da trasmettere al servizio Forms utilizzando il relativo costruttore. Passa un valore di stringa che specifica la posizione del file XML.
   * Creare un `com.adobe.idp.Document` oggetto utilizzando il relativo costruttore e passando l&#39; `java.io.FileInputStream` oggetto.
   * Creare un oggetto `PDFFormRenderSpec` utilizzato per impostare le opzioni di esecuzione. Richiama il metodo dell’ `PDFFormRenderSpec` oggetto `setGenerateServerAppearance` e passa `true`.
   * Richiama il metodo dell’ `FormsServiceClient` oggetto `renderPDFForm2` e passa i seguenti valori:

      * Un `com.adobe.idp.Document` oggetto che contiene il modulo PDF di cui eseguire il rendering.
      * Un `com.adobe.idp.Document` oggetto che contiene i dati da unire al modulo.
      * Un `PDFFormRenderSpec` oggetto che memorizza le opzioni di esecuzione.
      * Un `URLSpec` oggetto che contiene valori URI richiesti dal servizio Forms. Potete specificare `null` il valore di questo parametro.
      * Un `java.util.HashMap` oggetto che memorizza gli allegati. Si tratta di un parametro facoltativo e potete specificare `null` se non desiderate allegare file al modulo.

      Il `renderPDFForm2` metodo restituisce un `FormsResult` oggetto che contiene un flusso di dati del modulo

   * Recuperare il modulo PDF richiamando il `FormsResult` metodo dell&#39; `getOutputContent` . Questo metodo restituisce un `com.adobe.idp.Document` oggetto che rappresenta il modulo interattivo.


1. Firmare il modulo interattivo

   Firmare il documento PDF richiamando il metodo dell&#39; `SignatureServiceClient` oggetto `sign` e passando i seguenti valori:

   * Un `com.adobe.idp.Document` oggetto che rappresenta il documento PDF da firmare. Assicurarsi che questo oggetto sia l&#39; `com.adobe.idp.Document` oggetto ottenuto dal servizio Forms.
   * Una stringa che rappresenta il nome del campo firma firmato.
   * Un `Credential` oggetto che rappresenta la credenziale utilizzata per firmare digitalmente il documento PDF. Creare un `Credential` oggetto richiamando il `Credential` metodo statico dell&#39;oggetto `getInstance` . Passa un valore di stringa che specifica il valore alias corrispondente alla credenziale di sicurezza.
   * Un `HashAlgorithm` oggetto che specifica un membro di dati statici che rappresenta l&#39;algoritmo hash da utilizzare per rigenerare il documento PDF. Ad esempio, potete specificare `HashAlgorithm.SHA1` l&#39;utilizzo dell&#39;algoritmo SHA1.
   * Valore stringa che rappresenta il motivo per cui il documento PDF è stato firmato digitalmente.
   * Una stringa che rappresenta le informazioni di contatto del firmatario.
   * Un `PDFSignatureAppearanceOptions` oggetto che controlla l&#39;aspetto della firma digitale. Ad esempio, è possibile utilizzare questo oggetto per aggiungere un logo personalizzato a una firma digitale.
   * Un `java.lang.Boolean` oggetto che specifica se eseguire il controllo di revoca sul certificato del firmatario.
   * Un `OCSPPreferences` oggetto che memorizza le preferenze per il supporto del protocollo OCSP (Online Certificate Status Protocol). Se il controllo della revoca non viene eseguito, questo parametro non viene utilizzato e potete specificare `null`.
   * Un `CRLPreferences` oggetto che memorizza le preferenze dell&#39;elenco di revoca dei certificati (CRL, Certificate Revocation List). Se il controllo della revoca non viene eseguito, questo parametro non viene utilizzato e potete specificare `null`.
   * Un `TSPPreferences` oggetto che memorizza le preferenze per il supporto del provider di marca temporale (TSP). Questo parametro è facoltativo e può essere `null`.

   Il `sign` metodo restituisce un `com.adobe.idp.Document` oggetto che rappresenta il documento PDF firmato.

1. Salvare il documento PDF firmato

   * Create un `java.io.File` oggetto e accertatevi che l&#39;estensione del nome file sia .pdf.
   * Richiamare il `com.adobe.idp.Document` metodo dell&#39; `copyToFile` oggetto e passare `java.io.File`al file il contenuto dell&#39; `Document` oggetto. Assicurarsi di utilizzare l&#39; `com.adobe.idp.Document` oggetto restituito dal `sign` metodo.

**Consulta anche**

[Firma digitale di moduli interattivi](digitally-signing-certifying-documents.md#digitally-signing-interactive-forms)

[Avvio rapido (modalità SOAP): Firma digitale di un documento PDF tramite l&#39;API Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-pdf-document-using-the-java-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Firma digitale di un modulo interattivo tramite l&#39;API del servizio Web {#digitally-sign-an-interactive-form-using-the-web-service-api}

Firmare digitalmente un modulo interattivo utilizzando l&#39;API Forms e Signature (servizio Web):

1. Includi file di progetto

   Creare un progetto Microsoft .NET che utilizza MTOM. Poiché questa applicazione client richiama due servizi AEM Forms, create due riferimenti di servizio. Utilizzare la seguente definizione WSDL per il riferimento al servizio associato al servizio Signature: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   Utilizzare la seguente definizione WSDL per il riferimento al servizio associato al servizio Forms: `http://localhost:8080/soap/services/FormsService?WSDL&lc_version=9.0.1`.

   Poiché il tipo di `BLOB` dati è comune a entrambi i riferimenti di servizio, è necessario qualificare completamente il tipo di `BLOB` dati quando viene utilizzato. Nella procedura di avvio rapido del servizio Web corrispondente, tutte `BLOB` le istanze sono completamente qualificate.

   >[!NOTE]
   >
   >Sostituire `localhost` con l&#39;indirizzo IP del server host AEM Forms.

1. Creare un client Forms e Signatures

   * Creare un `SignatureServiceClient` oggetto utilizzando il relativo costruttore predefinito.
   * Creare un `SignatureServiceClient.Endpoint.Address` oggetto utilizzando il `System.ServiceModel.EndpointAddress` costruttore. Passate un valore di stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/SignatureService?WSDL`). Non è necessario utilizzare l&#39; `lc_version` attributo. Questo attributo viene utilizzato quando create un riferimento a un servizio.
   * Creare un `System.ServiceModel.BasicHttpBinding` oggetto ottenendo il valore del `SignatureServiceClient.Endpoint.Binding` campo. Inserite il valore restituito in `BasicHttpBinding`.
   * Impostare il campo `System.ServiceModel.BasicHttpBinding` dell&#39; `MessageEncoding` oggetto su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilitate l&#39;autenticazione HTTP di base eseguendo le seguenti operazioni:

      * Assegnare il nome utente dei moduli AEM al campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

   >[!NOTE]
   >
   >Ripetere la procedura per il client del servizio Forms.

1. Ottenere il modulo interattivo utilizzando il servizio Forms

   * Creare un `BLOB` oggetto utilizzando il relativo costruttore. L&#39; `BLOB` oggetto viene utilizzato per memorizzare un documento PDF firmato.
   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF da firmare e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto dell&#39; `System.IO.FileStream` oggetto. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà dell&#39; `System.IO.FileStream` oggetto `Length` .
   * Compilare l&#39;array di byte con i dati del flusso richiamando il `System.IO.FileStream` `Read` metodo dell&#39;oggetto e passando l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39; `BLOB` oggetto assegnando alla `MTOM` proprietà il contenuto dell&#39;array di byte.
   * Creare un `BLOB` oggetto utilizzando il relativo costruttore. L&#39; `BLOB` oggetto viene utilizzato per memorizzare i dati del modulo.
   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file XML contenente i dati del modulo e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto dell&#39; `System.IO.FileStream` oggetto. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà dell&#39; `System.IO.FileStream` oggetto `Length` .
   * Compilare l&#39;array di byte con i dati del flusso richiamando il `System.IO.FileStream` `Read` metodo dell&#39;oggetto e passando l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39; `BLOB` oggetto assegnando alla `MTOM` proprietà il contenuto dell&#39;array di byte.
   * Creare un oggetto `PDFFormRenderSpec` utilizzato per impostare le opzioni di esecuzione. Assegnare il valore `true` al campo dell&#39; `PDFFormRenderSpec` oggetto `generateServerAppearance` .
   * Richiama il metodo dell’ `FormsServiceClient` oggetto `renderPDFForm2` e passa i seguenti valori:

      * Un `BLOB` oggetto che contiene il modulo PDF di cui eseguire il rendering.
      * Un `BLOB` oggetto che contiene i dati da unire al modulo.
      * Un `PDFFormRenderSpec` oggetto che memorizza le opzioni di esecuzione.
      * Un `URLSpec` oggetto che contiene valori URI richiesti dal servizio Forms. Potete specificare `null` il valore di questo parametro.
      * Un `java.util.HashMap` oggetto che memorizza gli allegati. Si tratta di un parametro facoltativo e potete specificare `null` se non desiderate allegare file al modulo.
      * Un parametro di output lungo utilizzato per memorizzare il numero di pagine nel modulo.
      * Un parametro di output della stringa utilizzato per il valore delle impostazioni internazionali.
      * Un `FormResult` valore che è un parametro di output utilizzato per memorizzare il modulo interattivo.
   * Mantenere il modulo PDF richiamando il campo `FormsResult` dell&#39; `outputContent` oggetto. Questo campo memorizza un `BLOB` oggetto che rappresenta il modulo interattivo.


1. Firmare il modulo interattivo

   Firmare il documento PDF richiamando il metodo dell&#39; `SignatureServiceClient` oggetto `sign` e passando i seguenti valori:

   * Un `BLOB` oggetto che rappresenta il documento PDF da firmare. Utilizzare l&#39; `BLOB` istanza restituita dal servizio Forms.
   * Una stringa che rappresenta il nome del campo firma firmato.
   * Un `Credential` oggetto che rappresenta la credenziale utilizzata per firmare digitalmente il documento PDF. Creare un `Credential` oggetto utilizzando il relativo costruttore e specificare l&#39;alias assegnando un valore alla `Credential` proprietà dell&#39; `alias` oggetto.
   * Un `HashAlgorithm` oggetto che specifica un membro di dati statici che rappresenta l&#39;algoritmo hash da utilizzare per rigenerare il documento PDF. Ad esempio, potete specificare `HashAlgorithm.SHA1` l&#39;utilizzo dell&#39;algoritmo SHA1.
   * Un valore booleano che specifica se utilizzare l&#39;algoritmo hash.
   * Valore stringa che rappresenta il motivo per cui il documento PDF è stato firmato digitalmente.
   * Un valore di stringa che rappresenta la posizione del firmatario.
   * Una stringa che rappresenta le informazioni di contatto del firmatario.
   * Un `PDFSignatureAppearanceOptions` oggetto che controlla l&#39;aspetto della firma digitale. Ad esempio, è possibile utilizzare questo oggetto per aggiungere un logo personalizzato a una firma digitale.
   * Un `System.Boolean` oggetto che specifica se eseguire il controllo di revoca sul certificato del firmatario. Se il controllo di revoca viene eseguito, viene incorporato nella firma. Il valore predefinito è `false`.
   * Un `OCSPPreferences` oggetto che memorizza le preferenze per il supporto del protocollo OCSP (Online Certificate Status Protocol). Se il controllo della revoca non viene eseguito, questo parametro non viene utilizzato e potete specificare `null`. Per informazioni su questo oggetto, vedere Riferimento API per [AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * Un `CRLPreferences` oggetto che memorizza le preferenze dell&#39;elenco di revoca dei certificati (CRL, Certificate Revocation List). Se il controllo della revoca non viene eseguito, questo parametro non viene utilizzato e potete specificare `null`.
   * Un `TSPPreferences` oggetto che memorizza le preferenze per il supporto del provider di marca temporale (TSP). Questo parametro è facoltativo e può essere `null`.

   Il `sign` metodo restituisce un `BLOB` oggetto che rappresenta il documento PDF firmato.

1. Salvare il documento PDF firmato

   * Creare un `System.IO.FileStream` oggetto richiamandone il costruttore. Passa un valore di stringa che rappresenta la posizione del file del documento PDF firmato e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto dell&#39; `BLOB` oggetto restituito dal `sign` metodo. Compilare l&#39;array di byte ottenendo il valore del membro `BLOB` dati dell&#39; `MTOM` oggetto.
   * Creare un `System.IO.BinaryWriter` oggetto richiamando il relativo costruttore e passando l&#39; `System.IO.FileStream` oggetto.
   * Scrivere il contenuto dell&#39;array di byte in un file PDF richiamando il metodo dell&#39; `System.IO.BinaryWriter` oggetto `Write` e passando l&#39;array di byte.

**Consulta anche**

[Firma digitale di moduli interattivi](digitally-signing-certifying-documents.md#digitally-signing-interactive-forms)

[Chiamata di AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## Certificazione di documenti PDF {#certifying-pdf-documents}

È possibile proteggere un documento PDF certificandolo con un particolare tipo di firma denominato firma certificata. Una firma certificata si distingue da una firma digitale nei seguenti modi:

* Deve essere la prima firma applicata al documento PDF; ovvero, al momento dell&#39;applicazione della firma certificata, tutti gli altri campi firma nel documento devono essere defirmati. In un documento PDF è consentita una sola firma certificata. Se si desidera firmare e certificare un documento PDF, è necessario certificarlo prima di firmarlo. Dopo aver certificato un documento PDF, è possibile apporre una firma digitale ad altri campi firma.
* L&#39;autore o l&#39;autore del documento può specificare che il documento può essere modificato in alcuni modi senza invalidare la firma certificata. Ad esempio, il documento può consentire la compilazione di moduli o commenti. Se l&#39;autore specifica che non è consentita una determinata modifica, Acrobat impedisce agli utenti di modificare il documento in questo modo. Se tali modifiche vengono apportate, ad esempio utilizzando un&#39;altra applicazione, la firma certificata non è valida e Acrobat visualizza un avviso all&#39;apertura del documento da parte dell&#39;utente. Se le firme non certificate, le modifiche non vengono impedite e le normali operazioni di modifica non invalidano la firma originale.
* Al momento della firma, il documento viene analizzato per individuare specifici tipi di contenuto che potrebbero rendere il contenuto di un documento ambiguo o fuorviante. Ad esempio, un’annotazione potrebbe oscurare del testo in una pagina importante per comprendere cosa viene certificato. Una spiegazione (attestato legale) può essere fornita su tale contenuto.

È possibile certificare i documenti PDF a livello di programmazione utilizzando l&#39;API Java del servizio di firma o l&#39;API del servizio Web per la firma. Durante la certificazione di un documento PDF, è necessario fare riferimento a una credenziale di protezione esistente nel servizio Credenziali. Per informazioni sulle credenziali di protezione, vedere la guida *Installazione e distribuzione di AEM Forms* per il server delle applicazioni.

>[!NOTE]
>
>Durante la certificazione e la firma dello stesso documento PDF, se la firma certificata non è affidabile, all&#39;apertura del documento PDF in Acrobat o Adobe Reader viene visualizzato un triangolo giallo accanto alla prima firma. La firma di certificazione deve essere ritenuta affidabile per evitare tale situazione.

>[!NOTE]
>
>Quando si utilizza una credenziale HSM di CipherShield per firmare o certificare un documento PDF, non è possibile utilizzare la nuova credenziale finché il server applicazione J2EE su cui sono distribuiti i AEM Forms non viene riavviato. Tuttavia, è possibile impostare un valore di configurazione, in modo che l&#39;operazione di firma o certificazione funzioni senza riavviare il server applicazione J2EE.

Potete aggiungere il seguente valore di configurazione nel file cknfastrc, che si trova in /opt/nfast/cknfastrc (o c:\nfast\cknfastrc):

```shell
    CKNFAST_ASSUME_SINGLE_PROCESS=0
```

Dopo aver aggiunto questo valore di configurazione al file cknfastrc, è possibile utilizzare la nuova credenziale senza riavviare il server applicazione J2EE.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Firma e sulla certificazione di un documento, vedere Riferimento [servizi per i AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-5}

Per certificare un documento PDF, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un client per le firme.
1. Ottenere il documento PDF da certificare.
1. Certificare il documento PDF.
1. Salvare il documento PDF certificato come file PDF.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, accertatevi di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (richiesto se i AEM Forms sono distribuiti su JBoss)
* jbossall-client.jar (richiesto se i AEM Forms sono distribuiti su JBoss)

Per informazioni sulla posizione di questi file JAR, vedere [Inclusione di file](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)libreria Java AEM Forms.

**Creare un client per le firme**

Prima di poter eseguire un&#39;operazione Firma a livello di programmazione, è necessario creare un client per le firme.

**Ottenere il documento PDF da certificare**

Per certificare un documento PDF, è necessario ottenere un documento PDF contenente un campo firma. Se un documento PDF non contiene un campo firma, non può essere certificato. È possibile aggiungere un campo firma utilizzando Designer o a livello di programmazione. Per informazioni sull&#39;aggiunta programmatica di un campo firma, vedere [Aggiunta di campi](digitally-signing-certifying-documents.md#adding-signature-fields)firma.

**Certificare il documento PDF**

Per certificare correttamente un documento PDF, è necessario immettere i valori seguenti, utilizzati dal servizio Firma per certificare un documento PDF:

* **Documento** PDF: Un documento PDF contenente un campo firma, ovvero un campo modulo contenente una rappresentazione grafica della firma certificata. Per poter essere certificato, un documento PDF deve contenere un campo firma. È possibile aggiungere un campo firma utilizzando Designer o a livello di programmazione. (Vedere [Aggiunta di campi](digitally-signing-certifying-documents.md#adding-signature-fields)firma.)
* **Nome** campo firma: Il nome completo del campo firma certificato. Il seguente valore è un esempio: `form1[0].#subform[1].SignatureField3[3]`. Quando si utilizza un campo modulo XFA, è possibile utilizzare anche il nome parziale del campo firma: `SignatureField3[3]`. Se per il nome del campo viene passato un valore null, viene creato e certificato in modo dinamico un campo firma invisibile.
* **Credenziali** di protezione: Credenziale utilizzata per certificare il documento PDF. Questa credenziale di sicurezza contiene una password e un alias, che devono corrispondere a un alias visualizzato nella credenziale che si trova all&#39;interno del servizio Credenziali. L’alias è un riferimento a una credenziale effettiva che potrebbe trovarsi in un file PKCS#12 (con estensione .pfx) o in un modulo di protezione hardware (HSM).
* **Algoritmo** hash: Algoritmo hash da utilizzare per rigenerare il documento PDF.
* **Motivo della firma**: Un valore visualizzato in Acrobat o Adobe Reader in modo che gli altri utenti siano a conoscenza del motivo della certificazione del documento PDF.
* **Posizione del firmatario**: Posizione del firmatario specificata dalla credenziale.
* **Informazioni** di contatto: Informazioni di contatto del firmatario, ad esempio indirizzo e numero di telefono.
* **Informazioni sulle** autorizzazioni: Autorizzazioni che controllano le azioni che un utente finale può eseguire su un documento senza che la firma certificata risulti non valida. Ad esempio, è possibile impostare l&#39;autorizzazione in modo che qualsiasi modifica al documento PDF induca la firma certificata a non essere valida.
* **Spiegazione** giuridica: Quando un documento è certificato, viene automaticamente analizzato per specifici tipi di contenuto che potrebbero rendere il contenuto di un documento ambiguo o fuorviante. Ad esempio, un’annotazione potrebbe oscurare del testo in una pagina importante per comprendere cosa viene certificato. Il processo di scansione genera avvisi su questi tipi di contenuto. Questo valore fornisce un&#39;ulteriore spiegazione del contenuto che potrebbe aver generato avvisi.
* **Opzioni** di aspetto: Opzioni che controllano l&#39;aspetto della firma certificata. Ad esempio, la firma certificata può visualizzare le informazioni sulla data.
* **Controllo** revoca: Questo valore specifica se il controllo di revoca viene eseguito per il certificato del firmatario. L&#39;impostazione predefinita di `false` indica che il controllo della revoca non viene eseguito.
* **Impostazioni** OCSP: Impostazioni per il supporto del protocollo OCSP (Online Certificate Status Protocol), che fornisce informazioni sullo stato delle credenziali utilizzate per certificare il documento PDF. Ad esempio, è possibile specificare l&#39;URL del server che fornisce informazioni sulle credenziali che si sta utilizzando per accedere al documento PDF.
* **Impostazioni** CRL: Impostazioni per le preferenze dell&#39;elenco di revoche di certificati (CRL, Certificate Revocation List) se il controllo di revoca viene eseguito. Ad esempio, è possibile specificare di verificare sempre se una credenziale è stata revocata.
* **Timestamp**: Impostazioni che definiscono le informazioni di marca temporale applicate alla firma certificata. Una marca temporale indica che dati specifici sono stati stabiliti prima di una determinata ora. Questa conoscenza consente di creare una relazione affidabile tra il firmatario e il verificatore.

**Salvare il documento PDF certificato come file PDF**

Dopo che il servizio Firma ha certificato il documento PDF, è possibile salvarlo come file PDF per consentire agli utenti di aprirlo in Acrobat o Adobe Reader.

**Consulta anche**

[Certificare i documenti PDF tramite l&#39;API Java](digitally-signing-certifying-documents.md#certify-pdf-documents-using-the-java-api)

[Certificare i documenti PDF mediante l&#39;API del servizio Web](digitally-signing-certifying-documents.md#certify-pdf-documents-using-the-web-service-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Aggiunta di campi firma](digitally-signing-certifying-documents.md#adding-signature-fields)

### Certificare i documenti PDF tramite l&#39;API Java {#certify-pdf-documents-using-the-java-api}

Certificare un documento PDF utilizzando l&#39;API Signature (Java):

1. Includi file di progetto

   Includete file JAR client, ad esempio adobe-signatures-client.jar, nel percorso di classe del progetto Java.

1. Creare un client per le firme

   * Creare un `ServiceClientFactory` oggetto che contenga proprietà di connessione.
   * Creare un `SignatureServiceClient` oggetto utilizzando il relativo costruttore e passando l&#39; `ServiceClientFactory` oggetto.

1. Ottenere il documento PDF da certificare

   * Creare un `java.io.FileInputStream` oggetto che rappresenta il documento PDF da certificare utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del documento PDF.
   * Creare un `com.adobe.idp.Document` oggetto utilizzando il relativo costruttore e passando l&#39; `java.io.FileInputStream` oggetto.

1. Certificare il documento PDF

   Certificare il documento PDF richiamando il metodo dell&#39; `SignatureServiceClient` oggetto `certify` e passando i seguenti valori:

   * L&#39; `com.adobe.idp.Document` oggetto che rappresenta il documento PDF da certificare.
   * Una stringa che rappresenta il nome del campo firma che conterrà la firma.
   * Un `Credential` oggetto che rappresenta la credenziale utilizzata per certificare il documento PDF. Creare un `Credential` oggetto richiamando il `Credential` metodo statico dell&#39; `getInstance` oggetto e passando un valore di stringa che specifica il valore alias corrispondente alla credenziale di sicurezza.
   * Un `HashAlgorithm` oggetto che specifica un membro di dati statici che rappresenta l&#39;algoritmo hash utilizzato per digest del documento PDF. Ad esempio, potete specificare `HashAlgorithm.SHA1` l&#39;utilizzo dell&#39;algoritmo SHA1.
   * Valore stringa che rappresenta il motivo per cui il documento PDF è stato certificato.
   * Una stringa che rappresenta le informazioni di contatto del firmatario.
   * Un `MDPPermissions` oggetto che specifica le azioni che è possibile eseguire sul documento PDF e che invalida la firma.
   * Un `PDFSignatureAppearanceOptions` oggetto che controlla l&#39;aspetto della firma certificata. Se necessario, modificare l&#39;aspetto della firma richiamando un metodo, ad esempio `setShowDate`.
   * Valore stringa che fornisce una spiegazione delle azioni che invalidano la firma.
   * Un `java.lang.Boolean` oggetto che specifica se eseguire il controllo di revoca sul certificato del firmatario. Se il controllo di revoca viene eseguito, viene incorporato nella firma. Il valore predefinito è `false`.
   * Un `java.lang.Boolean` oggetto che specifica se il campo firma certificato è bloccato. Se il campo è bloccato, il campo firma è contrassegnato come di sola lettura, le relative proprietà non possono essere modificate e non può essere cancellato da chiunque non disponga delle autorizzazioni necessarie. Il valore predefinito è `false`.
   * Un `OCSPPreferences` oggetto che memorizza le preferenze per il supporto del protocollo OCSP (Online Certificate Status Protocol). Se il controllo della revoca non viene eseguito, questo parametro non viene utilizzato e potete specificare `null`. Per informazioni su questo oggetto, vedere Riferimento API per [AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * Un `CRLPreferences` oggetto che memorizza le preferenze dell&#39;elenco di revoca dei certificati (CRL, Certificate Revocation List). Se il controllo della revoca non viene eseguito, questo parametro non viene utilizzato e potete specificare `null`.
   * Un `TSPPreferences` oggetto che memorizza le preferenze per il supporto del provider di marca temporale (TSP). Ad esempio, dopo aver creato un `TSPPreferences` oggetto, è possibile impostare l&#39;URL del server TSP richiamando il `TSPPreferences` metodo dell&#39;oggetto `setTspServerURL` . Questo parametro è facoltativo e può essere `null`. Per ulteriori informazioni, vedere Riferimento [servizi per i AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

   Il `certify` metodo restituisce un `com.adobe.idp.Document` oggetto che rappresenta il documento PDF certificato.

1. Salvare il documento PDF certificato come file PDF

   * Create un `java.io.File` oggetto e accertatevi che l&#39;estensione del file sia .pdf.
   * Richiamare il metodo dell&#39; `com.adobe.idp.Document` oggetto `copyToFile` per copiare il contenuto dell&#39; `com.adobe.idp.Document` oggetto nel file.

**Consulta anche**

[Certificazione di documenti PDF](digitally-signing-certifying-documents.md#certifying-pdf-documents)

[Avvio rapido (modalità SOAP): Certificazione di un documento PDF tramite l&#39;API Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-certifying-a-pdf-document-using-the-java-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Certificare i documenti PDF mediante l&#39;API del servizio Web {#certify-pdf-documents-using-the-web-service-api}

Certificare un documento PDF utilizzando l&#39;API Signature (servizio Web):

1. Includi file di progetto

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituire `localhost` con l&#39;indirizzo IP del server host AEM Forms.

1. Creare un client per le firme

   * Creare un `SignatureServiceClient` oggetto utilizzando il relativo costruttore predefinito.
   * Creare un `SignatureServiceClient.Endpoint.Address` oggetto utilizzando il `System.ServiceModel.EndpointAddress` costruttore. Passate un valore di stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/SignatureService?WSDL`). Non è necessario utilizzare l&#39; `lc_version` attributo. Questo attributo viene utilizzato quando create un riferimento a un servizio.
   * Creare un `System.ServiceModel.BasicHttpBinding` oggetto ottenendo il valore del `SignatureServiceClient.Endpoint.Binding` campo. Inserite il valore restituito in `BasicHttpBinding`.
   * Impostare il campo `System.ServiceModel.BasicHttpBinding` dell&#39; `MessageEncoding` oggetto su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilitate l&#39;autenticazione HTTP di base eseguendo le seguenti operazioni:

      * Assegnare il nome utente dei moduli AEM al campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Ottenere il documento PDF da certificare

   * Creare un `BLOB` oggetto utilizzando il relativo costruttore. L&#39; `BLOB` oggetto viene utilizzato per memorizzare un documento PDF certificato.
   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF da certificare e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto dell&#39; `System.IO.FileStream` oggetto. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà dell&#39; `System.IO.FileStream` oggetto `Length` .
   * Compilare l&#39;array di byte con i dati del flusso richiamando il `System.IO.FileStream` `Read` metodo dell&#39;oggetto e passando l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39; `BLOB` oggetto assegnando al membro `MTOM` dati il contenuto dell&#39;array di byte.

1. Certificare il documento PDF

   Certificare il documento PDF richiamando il metodo dell&#39; `SignatureServiceClient` oggetto `certify` e passando i seguenti valori:

   * L&#39; `BLOB` oggetto che rappresenta il documento PDF da certificare.
   * Una stringa che rappresenta il nome del campo firma che conterrà la firma.
   * Un `Credential` oggetto che rappresenta la credenziale utilizzata per certificare il documento PDF. Creare un `Credential` oggetto utilizzando il relativo costruttore e specificare l&#39;alias assegnando un valore alla `Credential` proprietà dell&#39; `alias` oggetto.
   * Un `HashAlgorithm` oggetto che specifica un membro di dati statici che rappresenta l&#39;algoritmo hash utilizzato per digest del documento PDF. Ad esempio, potete specificare `HashAlgorithm.SHA1` l&#39;utilizzo dell&#39;algoritmo SHA1.
   * Un valore booleano che specifica se utilizzare l&#39;algoritmo hash.
   * Valore stringa che rappresenta il motivo per cui il documento PDF è stato certificato.
   * Un valore di stringa che rappresenta la posizione del firmatario.
   * Una stringa che rappresenta le informazioni di contatto del firmatario.
   * Membro di dati statici di un `MDPPermissions` oggetto che specifica le azioni che è possibile eseguire sul documento PDF per annullare la validità della firma.
   * Un valore booleano che specifica se utilizzare l&#39; `MDPPermissions` oggetto passato come valore del parametro precedente.
   * Valore stringa che spiega le azioni che invalidano la firma.
   * Un `PDFSignatureAppearanceOptions` oggetto che controlla l&#39;aspetto della firma certificata. Creare un `PDFSignatureAppearanceOptions` oggetto utilizzando il relativo costruttore. È possibile modificare l&#39;aspetto della firma impostando uno dei relativi membri dati.
   * Un `System.Boolean` oggetto che specifica se eseguire il controllo di revoca sul certificato del firmatario. Se il controllo di revoca viene eseguito, viene incorporato nella firma. Il valore predefinito è `false`.
   * Un `System.Boolean` oggetto che specifica se il campo firma certificato è bloccato. Se il campo è bloccato, il campo firma è contrassegnato come di sola lettura, le relative proprietà non possono essere modificate e non può essere cancellato da chiunque non disponga delle autorizzazioni necessarie. Il valore predefinito è `false`.
   * Un `System.Boolean` oggetto che specifica se il campo firma è bloccato. Ovvero, se passate `true` al parametro precedente, passate `true` a questo parametro.
   * Un `OCSPPreferences` oggetto che memorizza le preferenze per il supporto del protocollo OCSP (Online Certificate Status Protocol), che fornisce informazioni sullo stato delle credenziali utilizzate per certificare il documento PDF. Se il controllo della revoca non viene eseguito, questo parametro non viene utilizzato e potete specificare `null`.
   * Un `CRLPreferences` oggetto che memorizza le preferenze dell&#39;elenco di revoca dei certificati (CRL, Certificate Revocation List). Se il controllo della revoca non viene eseguito, questo parametro non viene utilizzato e potete specificare `null`.
   * Un `TSPPreferences` oggetto che memorizza le preferenze per il supporto del provider di marca temporale (TSP). Ad esempio, dopo aver creato un `TSPPreferences` oggetto, è possibile impostare l&#39;URL del TSP impostando il membro `TSPPreferences` dati dell&#39; `tspServerURL` oggetto. Questo parametro è facoltativo e può essere `null`.

   Il `certify` metodo restituisce un `BLOB` oggetto che rappresenta il documento PDF certificato.

1. Salvare il documento PDF certificato come file PDF

   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF che conterrà il documento PDF certificato e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto dell&#39; `BLOB` oggetto restituito dal `certify` metodo. Compilare l&#39;array di byte ottenendo il valore del membro `BLOB` dati dell&#39; `binaryData` oggetto.
   * Creare un `System.IO.BinaryWriter` oggetto richiamando il relativo costruttore e passando l&#39; `System.IO.FileStream` oggetto.
   * Scrivere il contenuto dell&#39;array di byte in un file PDF richiamando il metodo dell&#39; `System.IO.BinaryWriter` oggetto `Write` e passando l&#39;array di byte.

**Consulta anche**

[Certificazione di documenti PDF](digitally-signing-certifying-documents.md#certifying-pdf-documents)

[Chiamata di AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chiamata di AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Verifica delle firme digitali {#verifying-digital-signatures}

È possibile verificare che il documento PDF firmato non sia stato modificato e che la firma digitale sia valida. Durante la verifica di una firma digitale, è possibile verificare lo stato della firma e le proprietà della firma, ad esempio l&#39;identità del firmatario. Prima di considerare affidabile una firma digitale, è consigliabile verificarla. Quando si verifica una firma digitale, fare riferimento a un documento PDF contenente una firma digitale.

Si supponga che l&#39;identità del firmatario sia sconosciuta. Quando si apre il documento PDF in Acrobat, viene visualizzato un messaggio di avviso che informa che l&#39;identità del firmatario è sconosciuta, come illustrato nell&#39;illustrazione seguente.

![vd_vd_verifysig](assets/vd_vd_verifysig.png)

Analogamente, se si verifica a livello di programmazione una firma digitale, è possibile determinare lo stato dell&#39;identità del firmatario. Ad esempio, se si verifica la firma digitale nel documento mostrato nell&#39;illustrazione precedente, si verifica che l&#39;identità del firmatario sia sconosciuta.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Signature e sulla verifica delle firme digitali, vedere Riferimento [servizi per i AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-6}

Per verificare una firma digitale, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un client per le firme.
1. Ottenere il documento PDF contenente la firma da verificare.
1. Impostare le opzioni di esecuzione PKI.
1. Verificare la firma digitale.
1. Determinare lo stato della firma.
1. Determinare l&#39;identità del firmatario.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, includete i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (richiesto se i AEM Forms sono distribuiti su JBoss)
* jbossall-client.jar (richiesto se i AEM Forms sono distribuiti su JBoss)

Per informazioni sulla posizione di questi file JAR, vedere [Inclusione di file](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)libreria Java AEM Forms.

**Creare un client per le firme**

Prima di eseguire un&#39;operazione del servizio Signature a livello di programmazione, creare un client del servizio Signature.

**Ottenere il documento PDF contenente la firma da verificare**

Per verificare una firma utilizzata per firmare o certificare digitalmente un documento PDF, è necessario ottenere un documento PDF contenente una firma.

**Impostazione delle opzioni di esecuzione PKI**

Impostare le seguenti opzioni di esecuzione PKI che il servizio Firma utilizza per la verifica delle firme in un documento PDF:

* Tempo di verifica
* Controllo revoca
* Valori di marca temporale

Come parte dell&#39;impostazione di queste opzioni, potete specificare il tempo di verifica. Ad esempio, è possibile selezionare l&#39;ora corrente (l&#39;ora nel computer del validatore), che indica l&#39;utilizzo dell&#39;ora corrente. Per informazioni sui diversi valori temporali, consultate il valore di `VerificationTime` enumerazione in Riferimento [API](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)AEM Forms.

È inoltre possibile specificare se eseguire il controllo delle revoche nell&#39;ambito del processo di verifica. Ad esempio, è possibile eseguire un controllo di revoca per determinare se il certificato è revocato. Per informazioni sulle opzioni di controllo della revoca, vedere il valore di `RevocationCheckStyle` enumerazione in Riferimento API [AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

Per eseguire il controllo di revoca su un certificato, specificare un URL di un server dell&#39;elenco di revoche di certificati (CRL) utilizzando un `CRLOptionSpec` oggetto. Tuttavia, se non si specifica un URL per il server CRL, il servizio Signature ottiene l&#39;URL dal certificato.

Invece di utilizzare un server CRL, è possibile utilizzare un server OCSP (Certificate Status Protocol) online durante il controllo delle revoche. In genere, quando si utilizza un server OCSP anziché un server CRL, il controllo di revoca viene eseguito più rapidamente. (Vedere Protocollo [di stato del certificato](https://tools.ietf.org/html/rfc2560)online.)

È possibile impostare l&#39;ordine del server CRL e OCSP utilizzato dal servizio Signature utilizzando Adobe Applications and Services. Ad esempio, se il server OCSP è impostato per primo in Adobe Applications and Services, il server OCSP è selezionato, seguito dal server CRL.

Se non si esegue il controllo di revoca, il servizio Firma non verifica la revoca del certificato. In altre parole, le informazioni relative al server CRL e OCSP vengono ignorate.

>[!NOTE]
>
>Potete ignorare l&#39;URL specificato nel certificato utilizzando un `CRLOptionSpec` oggetto e un `OCSPOptionSpec` oggetto. Ad esempio, per ignorare il server CRL, è possibile richiamare il metodo dell&#39; `CRLOptionSpec` oggetto `setLocalURI` .

La marca temporale è il processo di tracciamento dell&#39;ora in cui un documento firmato o certificato è stato modificato. Dopo la firma di un documento, nessuno può modificarlo. La marca temporale consente di applicare la validità di un documento firmato o certificato. È possibile impostare le opzioni di marca temporale utilizzando un `TSPOptionSpec` oggetto. Ad esempio, potete specificare l&#39;URL di un server provider di marca temporale (TSP).

>[!NOTE]
>
>All&#39;avvio rapido di Java e servizi Web, l&#39;ora di verifica è impostata su `VerificationTime.CURRENT_TIME` e il controllo della revoca è impostato su `RevocationCheckStyle.BestEffort`. Poiché non sono specificate informazioni sul server CRL o OCSP, le informazioni sul server vengono ottenute dal certificato.

**Verificare la firma digitale**

Per verificare correttamente una firma, specificare il nome completo del campo firma che contiene la firma, ad esempio `form1[0].#subform[1].SignatureField3[3]`. Quando si utilizza un campo modulo XFA, è anche possibile utilizzare il nome parziale del campo firma: `SignatureField3`.

Per impostazione predefinita, il servizio Firma limita a 65 minuti il tempo di firma di un documento dopo il periodo di validità. Se un utente tenta di verificare una firma all&#39;ora corrente e l&#39;ora di firma è successiva all&#39;ora corrente ed è compresa entro 65 minuti, il servizio Firma non genera un errore di verifica.

>[!NOTE]
>
>Per altri valori richiesti per la verifica della firma, vedere Riferimento [API per](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)AEM Forms.

**Determinare lo stato della firma**

Durante la verifica di una firma digitale, è possibile verificare lo stato della firma.

**Identificazione del firmatario**

Puoi determinare l&#39;identità del firmatario, che può essere uno dei seguenti valori:

* **Sconosciuto**: Il firmatario è sconosciuto perché non è possibile eseguire la verifica del firmatario.
* **Attendibile**: Il firmatario è affidabile.
* **Non attendibile**: Il firmatario non è attendibile.

**Consulta anche**

[Verifica delle firme digitali tramite l&#39;API Java](#verify-digital-signatures-using-the-java-api)

[Verifica delle firme digitali tramite l&#39;API del servizio Web](#verify-digital-signatures-using-the-web-service-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Verifica delle firme digitali tramite l&#39;API Java {#verify-digital-signatures-using-the-java-api}

Verificare una firma digitale utilizzando l&#39;API Signature Service (Java):

1. Includi file di progetto

   Includete file JAR client, ad esempio adobe-signatures-client.jar, nel percorso di classe del progetto Java.

1. Creare un client per le firme

   * Creare un `ServiceClientFactory` oggetto che contenga proprietà di connessione.
   * Creare un `SignatureServiceClient` oggetto utilizzando il relativo costruttore e passando l&#39; `ServiceClientFactory` oggetto.

1. Ottenere il documento PDF contenente la firma da verificare

   * Creare un `java.io.FileInputStream` oggetto che rappresenta il documento PDF contenente la firma da verificare utilizzando il relativo costruttore. Passa un valore di stringa che specifica la posizione del documento PDF.
   * Creare un `com.adobe.idp.Document` oggetto utilizzando il relativo costruttore e passando l&#39; `java.io.FileInputStream` oggetto.

1. Impostazione delle opzioni di esecuzione PKI

   * Creare un `PKIOptions` oggetto utilizzando il relativo costruttore.
   * Impostare il tempo di verifica richiamando il metodo dell&#39; `PKIOptions` oggetto `setVerificationTime` e passando un valore di `VerificationTime` enumerazione che specifica il tempo di verifica.
   * Impostare l&#39;opzione di controllo della revoca richiamando il metodo dell&#39; `PKIOptions` oggetto `setRevocationCheckStyle` e passando un valore di `RevocationCheckStyle` enumerazione che specifica se eseguire il controllo della revoca.

1. Verificare la firma digitale

   Verificare la firma richiamando il metodo dell&#39; `SignatureServiceClient` oggetto `verify2` e passando i seguenti valori:

   * Un `com.adobe.idp.Document` oggetto che contiene un documento PDF firmato o certificato digitalmente.
   * Valore stringa che rappresenta il nome del campo firma contenente la firma da verificare.
   * Un `PKIOptions` oggetto che contiene le opzioni di esecuzione PKI.
   * Un&#39; `VerifySPIOptions` istanza che contiene informazioni SPI. Potete specificare `null` questo parametro.

   Il `verify2` metodo restituisce un `PDFSignatureVerificationInfo` oggetto contenente informazioni che è possibile utilizzare per verificare la firma digitale.

1. Determinare lo stato della firma

   * Determinare lo stato della firma richiamando il `PDFSignatureVerificationInfo` metodo `getStatus` dell&#39;oggetto. Questo metodo restituisce un `SignatureStatus` oggetto che specifica lo stato della firma. Ad esempio, se un documento PDF firmato non viene modificato, questo metodo restituisce `SignatureStatus.DocumentSigNoChanges`.

1. Identificazione del firmatario

   * Determinare l&#39;identità del firmatario richiamando il `PDFSignatureVerificationInfo` metodo dell&#39; `getSigner` oggetto. Questo metodo restituisce un `IdentityInformation` oggetto.
   * Richiama il metodo dell&#39; `IdentityInformation` oggetto `getStatus` per determinare l&#39;identità del firmatario. Questo metodo restituisce un valore di `IdentityStatus` enumerazione che specifica l&#39;identità. Ad esempio, se il firmatario è affidabile, questo metodo restituisce `IdentityStatus.TRUSTED`.

**Consulta anche**

[Verifica delle firme digitali](#verify-digital-signatures-using-the-java-api)

[Avvio rapido (modalità SOAP): Verifica di una firma digitale mediante l&#39;API Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-verifying-a-digital-signature-using-the-java-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Verifica delle firme digitali tramite l&#39;API del servizio Web {#verify-digital-signatures-using-the-web-service-api}

Verificare una firma digitale utilizzando l&#39;API Signature Service (servizio Web):

1. Includi file di progetto

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituire `localhost` con l&#39;indirizzo IP del server host AEM Forms.

1. Creare un client per le firme

   * Creare un `SignatureServiceClient` oggetto utilizzando il relativo costruttore predefinito.
   * Creare un `SignatureServiceClient.Endpoint.Address` oggetto utilizzando il `System.ServiceModel.EndpointAddress` costruttore. Passate un valore di stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/SignatureService?WSDL`). Non è necessario utilizzare l&#39; `lc_version` attributo. Questo attributo viene utilizzato quando create un riferimento a un servizio.
   * Creare un `System.ServiceModel.BasicHttpBinding` oggetto ottenendo il valore del `SignatureServiceClient.Endpoint.Binding` campo. Inserite il valore restituito in `BasicHttpBinding`.
   * Impostare il campo `System.ServiceModel.BasicHttpBinding` dell&#39; `MessageEncoding` oggetto su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilitate l&#39;autenticazione HTTP di base eseguendo le seguenti operazioni:

      * Assegnare il nome utente dei moduli AEM al campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Ottenere il documento PDF contenente la firma da verificare

   * Creare un `BLOB` oggetto utilizzando il relativo costruttore. L&#39; `BLOB` oggetto viene utilizzato per memorizzare un documento PDF contenente una firma digitale o certificata da verificare.
   * Creare un `System.IO.FileStream` oggetto richiamandone il costruttore. Passa un valore di stringa che rappresenta la posizione del file del documento PDF firmato e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto dell&#39; `System.IO.FileStream` oggetto. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà dell&#39; `System.IO.FileStream` oggetto `Length` .
   * Compilare l&#39;array di byte con i dati del flusso richiamando il metodo dell&#39; `System.IO.FileStream` oggetto `Read` . Passare l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39; `BLOB` oggetto assegnando alla `MTOM` proprietà il contenuto dell&#39;array di byte.

1. Impostazione delle opzioni di esecuzione PKI

   * Creare un `PKIOptions` oggetto utilizzando il relativo costruttore.
   * Impostare l&#39;ora di verifica assegnando al membro dati dell&#39; `PKIOptions` oggetto `verificationTime` un valore di `VerificationTime` enumerazione che specifica il tempo di verifica.
   * Impostare l&#39;opzione di controllo della revoca assegnando al membro dei dati dell&#39; `PKIOptions` oggetto `revocationCheckStyle` un valore di `RevocationCheckStyle` enumerazione che specifica se eseguire il controllo della revoca.

1. Verificare la firma digitale

   Verificare la firma richiamando il metodo dell&#39; `SignatureServiceClient` oggetto `verify2` e passando i seguenti valori:

   * L&#39; `BLOB` oggetto che contiene un documento PDF con firma digitale o certificato.
   * Valore stringa che rappresenta il nome del campo firma contenente la firma da verificare.
   * Un `PKIOptions` oggetto che contiene le opzioni di esecuzione PKI.
   * Un&#39; `VerifySPIOptions` istanza che contiene informazioni SPI. Potete specificare `null` questo parametro.

   Il `verify2` metodo restituisce un `PDFSignatureVerificationInfo` oggetto contenente informazioni che è possibile utilizzare per verificare la firma digitale.

1. Determinare lo stato della firma

   Determinare lo stato della firma ottenendo il valore del membro `PDFSignatureVerificationInfo` dati dell&#39; `status` oggetto. Questo membro di dati memorizza un oggetto che specifica lo stato della firma. `SignatureStatus` Ad esempio, se un documento PDF firmato viene modificato, il membro `status` dati memorizza il valore `SignatureStatus.DocumentSigNoChanges`.

1. Identificazione del firmatario

   * Determinare l&#39;identità del firmatario recuperando il valore del membro `PDFSignatureVerificationInfo` dati `signer` dell&#39;oggetto. Questo membro restituisce un `IdentityInformation` oggetto.
   * Recuperare il membro dati dell&#39; `IdentityInformation` oggetto per determinare l&#39;identità del firmatario `status` . Questo membro dati restituisce un valore di `IdentityStatus` enumerazione che specifica l&#39;identità. Ad esempio, se il firmatario è affidabile, il membro restituirà `IdentityStatus.TRUSTED`.

**Consulta anche**

[Verifica delle firme digitali](#verify-digital-signatures-using-the-java-api)

[Chiamata di AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chiamata di AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Verifica di più firme digitali {#verifying-multiple-digital-signatures}

I AEM Forms consentono di verificare tutte le firme digitali presenti in un documento PDF. Si supponga che un documento PDF contenga più firme digitali come risultato di un processo aziendale che richiede la firma di più firmatari. Ad esempio, considerare una transazione finanziaria che richiede sia la firma di un funzionario prestiti che quella di un manager. È possibile utilizzare l&#39;API Java del servizio firma o l&#39;API del servizio Web per verificare tutte le firme presenti nel documento PDF. Durante la verifica di più firme digitali, è possibile verificare lo stato e le proprietà di ciascuna firma. Prima di rendere affidabile una firma digitale, è consigliabile verificarla. Si consiglia di avere familiarità con la verifica di una firma digitale singola.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Signature e sulla verifica delle firme digitali, vedere Riferimento [servizi per i AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-7}

Per verificare più firme digitali, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un client per le firme.
1. Ottenere il documento PDF contenente le firme da verificare.
1. Impostare le opzioni di esecuzione PKI.
1. Recupera tutte le firme digitali.
1. Iterare tutte le firme.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, includete i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (richiesto se i AEM Forms sono distribuiti su JBoss)
* jbossall-client.jar (richiesto se i AEM Forms sono distribuiti su JBoss)

Per informazioni sulla posizione di questi file JAR, vedere [Inclusione di file](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)libreria Java AEM Forms.

**Creare un client per le firme**

Prima di eseguire un&#39;operazione del servizio Signature a livello di programmazione, creare un client del servizio Signature.

**Ottenere il documento PDF contenente le firme per verificare**

Per verificare una firma utilizzata per firmare o certificare digitalmente un documento PDF, è necessario ottenere un documento PDF contenente una firma.

**Impostazione delle opzioni di runtime PKI**

Impostare le seguenti opzioni di esecuzione PKI che il servizio Firma utilizza per verificare tutte le firme in un documento PDF:

* Tempo di verifica
* Controllo revoca
* Valori di marca temporale

Come parte dell&#39;impostazione di queste opzioni, potete specificare il tempo di verifica. Ad esempio, è possibile selezionare l&#39;ora corrente (l&#39;ora nel computer del validatore), che indica l&#39;utilizzo dell&#39;ora corrente. Per informazioni sui diversi valori temporali, consultate il valore di `VerificationTime` enumerazione in Riferimento [API](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)AEM Forms.

È inoltre possibile specificare se eseguire il controllo delle revoche nell&#39;ambito del processo di verifica. Ad esempio, è possibile eseguire un controllo di revoca per determinare se il certificato è revocato. Per informazioni sulle opzioni di controllo della revoca, vedere il valore di `RevocationCheckStyle` enumerazione in Riferimento API [AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

Per eseguire il controllo di revoca su un certificato, specificare un URL di un server dell&#39;elenco di revoche di certificati (CRL) utilizzando un `CRLOptionSpec` oggetto. Tuttavia, se non si specifica un URL per un server CRL, il servizio Signature ottiene l&#39;URL dal certificato.

Invece di utilizzare un server CRL, è possibile utilizzare un server OCSP (Certificate Status Protocol) online durante il controllo delle revoche. In genere, quando si utilizza un server OCSP invece di un server CRL, il controllo di revoca viene eseguito più rapidamente. (Vedere Protocollo [di stato del certificato](https://tools.ietf.org/html/rfc2560)online.)

È possibile impostare l&#39;ordine del server CRL e OCSP utilizzato dal servizio Signature utilizzando Adobe Applications and Services. Ad esempio, se il server OCSP è impostato per primo in Adobe Applications and Services, il server OCSP è selezionato, seguito dal server CRL.

Se non si esegue il controllo di revoca, il servizio Firma non verifica la revoca del certificato. In altre parole, le informazioni relative al server CRL e OCSP vengono ignorate.

>[!NOTE]
>
>Potete ignorare l&#39;URL specificato nel certificato utilizzando un `CRLOptionSpec` oggetto e un `OCSPOptionSpec` oggetto. Ad esempio, per ignorare il server CRL, è possibile richiamare il metodo dell&#39; `CRLOptionSpec` oggetto `setLocalURI` .

La marca temporale è il processo di tracciamento dell&#39;ora in cui un documento firmato o certificato è stato modificato. Dopo la firma di un documento, nessuno può modificarlo. La marca temporale consente di applicare la validità di un documento firmato o certificato. È possibile impostare le opzioni di marca temporale utilizzando un `TSPOptionSpec` oggetto. Ad esempio, potete specificare l&#39;URL di un server provider di marca temporale (TSP).

>[!NOTE]
>
>All&#39;avvio rapido di Java e servizi Web, l&#39;ora di verifica è impostata su `VerificationTime.CURRENT_TIME` e il controllo della revoca è impostato su `RevocationCheckStyle.BestEffort`. Poiché non sono specificate informazioni sul server CRL o OCSP, le informazioni sul server vengono ottenute dal certificato.

**Recuperare tutte le firme digitali**

Per verificare tutte le firme digitali presenti in un documento PDF, recuperare le firme digitali dal documento PDF. Tutte le firme vengono restituite in un elenco. Come parte della verifica di una firma digitale, verificare lo stato della firma.

>[!NOTE]
>
>A differenza di quanto avviene per la verifica di una singola firma digitale, quando si verificano più firme non è necessario specificare il nome del campo firma.

**Itera attraverso tutte le firme**

Iterare attraverso ciascuna firma. Ovvero, per ogni firma, verificare la firma digitale e verificare l&#39;identità del firmatario e lo stato di ciascuna firma. (Vedere [Verifica delle firme](#verify-digital-signatures-using-the-java-api)digitali.)

>[!NOTE]
>
>Se il requisito è l&#39;intero documento, non è necessario eseguire l&#39;iterazione su tutte le firme.

**Consulta anche**

[Verifica di più firme digitali tramite l&#39;API Java](#verify-digital-signatures-using-the-java-api)

[Verifica di più firme digitali tramite l&#39;API del servizio Web](#verify-digital-signatures-using-the-web-service-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Verifica di più firme digitali tramite l&#39;API Java {#verify-multiple-digital-signatures-using-the-java-api}

Verificare più firme digitali utilizzando l&#39;API Signature Service (Java):

1. Includi file di progetto

   Includete file JAR client, ad esempio adobe-signatures-client.jar, nel percorso di classe del progetto Java.

1. Creare un client per le firme

   * Creare un `ServiceClientFactory` oggetto che contenga proprietà di connessione.
   * Creare un `SignatureServiceClient` oggetto utilizzando il relativo costruttore e passando l&#39; `ServiceClientFactory` oggetto.

1. Ottenere il documento PDF contenente le firme per verificare

   * Creare un `java.io.FileInputStream` oggetto che rappresenta il documento PDF contenente più firme digitali da verificare utilizzando il relativo costruttore. Passa un valore di stringa che specifica la posizione del documento PDF.
   * Creare un `com.adobe.idp.Document` oggetto utilizzando il relativo costruttore e passando l&#39; `java.io.FileInputStream` oggetto.

1. Impostazione delle opzioni di runtime PKI

   * Creare un `PKIOptions` oggetto utilizzando il relativo costruttore.
   * Impostare il tempo di verifica richiamando il metodo dell&#39; `PKIOptions` oggetto `setVerificationTime` e passando un valore di `VerificationTime` enumerazione che specifica il tempo di verifica.
   * Impostare l&#39;opzione di controllo della revoca richiamando il metodo dell&#39; `PKIOptions` oggetto `setRevocationCheckStyle` e passando un valore di `RevocationCheckStyle` enumerazione che specifica se eseguire il controllo della revoca.

1. Recuperare tutte le firme digitali

   Richiama il metodo dell’ `SignatureServiceClient` oggetto `verifyPDFDocument` e passa i seguenti valori:

   * Un `com.adobe.idp.Document` oggetto che contiene un documento PDF contenente più firme digitali.
   * Un `PKIOptions` oggetto che contiene le opzioni di esecuzione PKI.
   * Un&#39; `VerifySPIOptions` istanza che contiene informazioni SPI. Potete specificare `null` questo parametro.

   Il `verifyPDFDocument` metodo restituisce un `PDFDocumentVerificationInfo` oggetto che contiene informazioni su tutte le firme digitali presenti nel documento PDF.

1. Itera attraverso tutte le firme

   * Eseguire un&#39;iterazione attraverso tutte le firme richiamando il `PDFDocumentVerificationInfo` metodo dell&#39; `getVerificationInfos` oggetto. Questo metodo restituisce un `java.util.List` oggetto in cui ogni elemento è un `PDFSignatureVerificationInfo` oggetto. Utilizzare un `java.util.Iterator` oggetto per eseguire un&#39;iterazione nell&#39;elenco di firme.
   * Utilizzando l&#39; `PDFSignatureVerificationInfo` oggetto, è possibile eseguire attività quali determinare lo stato della firma richiamando il metodo dell&#39; `PDFSignatureVerificationInfo` oggetto `getStatus` . Questo metodo restituisce un oggetto il cui membro dati statico `SignatureStatus` informa l&#39;utente sullo stato della firma. Ad esempio, se la firma è sconosciuta, questo metodo restituisce `SignatureStatus.DocumentSignatureUnknown`.

**Consulta anche**

[Verifica di più firme digitali](#verifying-multiple-digital-signatures)

[Avvio rapido (modalità SOAP): Verifica di più firme digitali tramite l&#39;API Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-verifying-multiple-digital-signatures-using-the-java-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Verifica delle firme digitali](#verify-digital-signatures-using-the-java-api)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Verifica di più firme digitali tramite l&#39;API del servizio Web {#verifying-multiple-digital-signatures-using-the-web-service-api}

Verificare più firme digitali utilizzando l&#39;API Signature Service (servizio Web):

1. Includi file di progetto

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituire `localhost` con l&#39;indirizzo IP del server host AEM Forms.

1. Creare un client per le firme

   * Creare un `SignatureServiceClient` oggetto utilizzando il relativo costruttore predefinito.
   * Creare un `SignatureServiceClient.Endpoint.Address` oggetto utilizzando il `System.ServiceModel.EndpointAddress` costruttore. Passate un valore di stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/SignatureService?WSDL`). Non è necessario utilizzare l&#39; `lc_version` attributo. Questo attributo viene utilizzato quando create un riferimento a un servizio.
   * Creare un `System.ServiceModel.BasicHttpBinding` oggetto ottenendo il valore del `SignatureServiceClient.Endpoint.Binding` campo. Inserite il valore restituito in `BasicHttpBinding`.
   * Impostare il campo `System.ServiceModel.BasicHttpBinding` dell&#39; `MessageEncoding` oggetto su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilitate l&#39;autenticazione HTTP di base eseguendo le seguenti operazioni:

      * Assegnare il nome utente dei moduli AEM al campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Ottenere il documento PDF contenente le firme per verificare

   * Creare un `BLOB` oggetto utilizzando il relativo costruttore. L&#39; `BLOB` oggetto memorizza un documento PDF contenente più firme digitali da verificare.
   * Creare un `System.IO.FileStream` oggetto richiamandone il costruttore. Passare un valore di stringa che rappresenta la posizione del file del documento PDF e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto dell&#39; `System.IO.FileStream` oggetto. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà dell&#39; `System.IO.FileStream` oggetto `Length` .
   * Compilare l&#39;array di byte con i dati del flusso richiamando il metodo dell&#39; `System.IO.FileStream` oggetto `Read` . Passare l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39; `BLOB` oggetto assegnando alla `MTOM` proprietà il contenuto dell&#39;array di byte.

1. Impostazione delle opzioni di runtime PKI

   * Creare un `PKIOptions` oggetto utilizzando il relativo costruttore.
   * Impostare l&#39;ora di verifica assegnando al membro dati dell&#39; `PKIOptions` oggetto `verificationTime` un valore di `VerificationTime` enumerazione che specifica il tempo di verifica.
   * Impostare l&#39;opzione di controllo della revoca assegnando al membro dati dell&#39; `PKIOptions` oggetto `revocationCheckStyle` un valore di `RevocationCheckStyle` enumerazione che specifica se eseguire il controllo della revoca.

1. Recuperare tutte le firme digitali

   Richiama il metodo dell’ `SignatureServiceClient` oggetto `verifyPDFDocument` e passa i seguenti valori:

   * Un `BLOB` oggetto che contiene un documento PDF contenente più firme digitali.
   * Un `PKIOptions` oggetto che contiene le opzioni di esecuzione PKI.
   * Un&#39; `VerifySPIOptions` istanza che contiene informazioni SPI. Potete specificare null per questo parametro.

   Il `verifyPDFDocument` metodo restituisce un `PDFDocumentVerificationInfo` oggetto che contiene informazioni su tutte le firme digitali presenti nel documento PDF.

1. Itera attraverso tutte le firme

   * Consente di esaminare tutte le firme ottenendo il membro `PDFDocumentVerificationInfo` dati `verificationInfos` dell&#39;oggetto. Questo membro dati restituisce un `Object` array in cui ogni elemento è un `PDFSignatureVerificationInfo` oggetto.
   * Utilizzando l&#39; `PDFSignatureVerificationInfo` oggetto è possibile eseguire attività quali determinare lo stato della firma ottenendo il membro `PDFSignatureVerificationInfo` dati dell&#39; `status` oggetto. Questo membro dati restituisce un `SignatureStatus` oggetto il cui membro dati statico ti informa sullo stato della firma. Ad esempio, se la firma è sconosciuta, questo metodo restituisce `SignatureStatus.DocumentSignatureUnknown`.

**Consulta anche**

[Verifica di più firme digitali](#verifying-multiple-digital-signatures)

[Chiamata di AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chiamata di AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Rimozione di firme digitali {#removing-digital-signatures}

Per poter applicare una firma digitale più recente, è necessario rimuovere le firme digitali da un campo firma. Non è possibile sovrascrivere una firma digitale. Se si tenta di applicare una firma digitale a un campo firma contenente una firma, si verifica un&#39;eccezione.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Signature, vedere Riferimento [servizi per i AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-8}

Per rimuovere una firma digitale da un campo firma, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un client per le firme.
1. Ottenere il documento PDF contenente una firma da rimuovere.
1. Rimuovere la firma digitale dal campo firma.
1. Salvare il documento PDF come file PDF.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se state creando un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate servizi Web, accertatevi di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (richiesto se i AEM Forms sono distribuiti su JBoss)
* jbossall-client.jar (richiesto se i AEM Forms sono distribuiti su JBoss)

Per informazioni sulla posizione di questi file JAR, vedere [Inclusione di file](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)libreria Java AEM Forms.

**Creare un client per le firme**

Prima di eseguire un&#39;operazione del servizio Firma a livello di programmazione, è necessario creare un client del servizio Firma.

**Ottenere il documento PDF contenente una firma da rimuovere**

Per rimuovere una firma da un documento PDF, è necessario ottenere un documento PDF contenente una firma.

**Rimozione della firma digitale dal campo firma**

Per rimuovere correttamente una firma digitale da un documento PDF, è necessario specificare il nome del campo firma contenente la firma digitale. È inoltre necessario disporre dell&#39;autorizzazione per rimuovere la firma digitale; in caso contrario, si verifica un&#39;eccezione.

**Salvare il documento PDF come file PDF**

Dopo che il servizio Firma ha rimosso una firma digitale da un campo firma, è possibile salvare il documento PDF come file PDF per consentirne l&#39;apertura in Acrobat o Adobe Reader.

**Consulta anche**

[Rimozione di firme digitali tramite l&#39;API Java](digitally-signing-certifying-documents.md#remove-digital-signatures-using-the-java-api)

[Rimozione di firme digitali tramite l&#39;API del servizio Web](digitally-signing-certifying-documents.md#remove-digital-signatures-using-the-web-service-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Aggiunta di campi firma](digitally-signing-certifying-documents.md#adding-signature-fields)

### Rimozione di firme digitali tramite l&#39;API Java {#remove-digital-signatures-using-the-java-api}

Rimuovere una firma digitale utilizzando l&#39;API Signature (Java):

1. Includi file di progetto

   Includete file JAR client, ad esempio adobe-signatures-client.jar, nel percorso di classe del progetto Java.

1. Creare un client per le firme.

   * Creare un `ServiceClientFactory` oggetto che contenga proprietà di connessione.
   * Creare un `SignatureServiceClient` oggetto utilizzando il relativo costruttore e passando l&#39; `ServiceClientFactory` oggetto.

1. Ottenere il documento PDF contenente una firma da rimuovere

   * Creare un `java.io.FileInputStream` oggetto che rappresenta il documento PDF contenente la firma da rimuovere utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del documento PDF.
   * Creare un `com.adobe.idp.Document` oggetto utilizzando il relativo costruttore e passando l&#39; `java.io.FileInputStream` oggetto.

1. Rimozione della firma digitale dal campo firma

   Rimuovere una firma digitale da un campo firma richiamando il metodo dell&#39; `SignatureServiceClient` oggetto `clearSignatureField` e passando i seguenti valori:

   * Un `com.adobe.idp.Document` oggetto che rappresenta il documento PDF contenente la firma da rimuovere.
   * Una stringa che specifica il nome del campo firma contenente la firma digitale.

   Il `clearSignatureField` metodo restituisce un `com.adobe.idp.Document` oggetto che rappresenta il documento PDF da cui è stata rimossa la firma digitale.

1. Salvare il documento PDF come file PDF

   * Create un `java.io.File` oggetto e accertatevi che l&#39;estensione del file sia .pdf.
   * Richiama il metodo dell’ `com.adobe.idp.Document` oggetto `copyToFile` . Passate l&#39; `java.io.File` oggetto per copiare il contenuto dell&#39; `com.adobe.idp.Document` oggetto nel file. Assicurarsi di utilizzare l&#39; `Document` oggetto restituito dal `clearSignatureField` metodo.

**Consulta anche**

[Rimozione di firme digitali](digitally-signing-certifying-documents.md#removing-digital-signatures)

[Avvio rapido (modalità SOAP): Rimozione di una firma digitale mediante l&#39;API Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-removing-a-digital-signature-using-the-java-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Rimozione di firme digitali tramite l&#39;API del servizio Web {#remove-digital-signatures-using-the-web-service-api}

Rimuovere una firma digitale utilizzando l&#39;API Signature (servizio Web):

1. Includi file di progetto

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituire `localhost` con l&#39;indirizzo IP del server host AEM Forms.

1. Creare un client per le firme

   * Creare un `SignatureServiceClient` oggetto utilizzando il relativo costruttore predefinito.
   * Creare un `SignatureServiceClient.Endpoint.Address` oggetto utilizzando il `System.ServiceModel.EndpointAddress` costruttore. Passate un valore di stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/SignatureService?WSDL`). Non è necessario utilizzare l&#39; `lc_version` attributo. Questo attributo viene utilizzato quando create un riferimento a un servizio.
   * Creare un `System.ServiceModel.BasicHttpBinding` oggetto ottenendo il valore del `SignatureServiceClient.Endpoint.Binding` campo. Inserite il valore restituito in `BasicHttpBinding`.
   * Impostare il campo `System.ServiceModel.BasicHttpBinding` dell&#39; `MessageEncoding` oggetto su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilitate l&#39;autenticazione HTTP di base eseguendo le seguenti operazioni:

      * Assegnare il nome utente dei moduli AEM al campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Ottenere il documento PDF contenente una firma da rimuovere

   * Creare un `BLOB` oggetto utilizzando il relativo costruttore. L&#39; `BLOB` oggetto viene utilizzato per memorizzare un documento PDF contenente una firma digitale da rimuovere.
   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF firmato e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto dell&#39; `System.IO.FileStream` oggetto. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà dell&#39; `System.IO.FileStream` oggetto `Length` .
   * Compilare l&#39;array di byte con i dati del flusso richiamando il metodo dell&#39; `System.IO.FileStream` oggetto `Read` . Passare l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39; `BLOB` oggetto assegnandone `MTOM` la proprietà con il contenuto dell&#39;array di byte.

1. Rimozione della firma digitale dal campo firma

   Rimuovere la firma digitale richiamando il metodo dell&#39; `SignatureServiceClient` oggetto `clearSignatureField` e passando i seguenti valori:

   * Un `BLOB` oggetto che contiene il documento PDF firmato.
   * Una stringa che rappresenta il nome del campo firma contenente la firma digitale da rimuovere.

   Il `clearSignatureField` metodo restituisce un `BLOB` oggetto che rappresenta il documento PDF da cui è stata rimossa la firma digitale.

1. Salvare il documento PDF come file PDF

   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF contenente un campo firma vuoto e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto dell&#39; `BLOB` oggetto restituito dal `sign` metodo. Compilare l&#39;array di byte ottenendo il valore del membro `BLOB` dati dell&#39; `MTOM` oggetto.
   * Creare un `System.IO.BinaryWriter` oggetto richiamando il relativo costruttore e passando l&#39; `System.IO.FileStream` oggetto.
   * Scrivere il contenuto dell&#39;array di byte nel file PDF richiamando il metodo dell&#39; `System.IO.BinaryWriter` oggetto `Write` e passando l&#39;array di byte.

**Consulta anche**

[Rimozione di firme digitali](digitally-signing-certifying-documents.md#removing-digital-signatures)

[Chiamata di AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chiamata di AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
