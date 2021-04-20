---
title: Firma digitale e certificazione dei documenti
seo-title: Firma digitale e certificazione dei documenti
description: Utilizzare il servizio Firma per aggiungere ed eliminare campi firma digitale in un documento PDF, recuperare i nomi dei campi firma presenti in un documento PDF, modificare i campi firma, firmare digitalmente documenti PDF, certificare documenti PDF, convalidare le firme digitali presenti in un documento PDF, convalidare tutte le firme digitali presenti in un documento PDF e rimuovere una firma digitale da un campo firma.
seo-description: Utilizzare il servizio Firma per aggiungere ed eliminare campi firma digitale in un documento PDF, recuperare i nomi dei campi firma presenti in un documento PDF, modificare i campi firma, firmare digitalmente documenti PDF, certificare documenti PDF, convalidare le firme digitali presenti in un documento PDF, convalidare tutte le firme digitali presenti in un documento PDF e rimuovere una firma digitale da un campo firma.
uuid: 6331de8a-2a9c-45bf-89d2-29f1ad5cc856
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 42de04bf-25e4-4478-a411-38671ed871ae
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '17114'
ht-degree: 0%

---


# Firma digitale e certificazione dei documenti {#digitally-signing-and-certifying-documents}

**Esempi ed esempi in questo documento sono solo per AEM Forms in ambiente JEE.**

**Informazioni sul servizio Firma**

Il servizio Firma consente alla tua organizzazione di proteggere la sicurezza e la privacy dei documenti Adobe PDF che distribuisce e riceve. Questo servizio utilizza le firme digitali e la certificazione per garantire che solo i destinatari a cui è destinato possano modificare i documenti. Poiché le funzioni di protezione vengono applicate al documento stesso, il documento rimane protetto e controllato per l&#39;intero ciclo di vita. Un documento rimane protetto oltre il firewall, quando viene scaricato offline e quando viene inviato nuovamente all&#39;organizzazione.

>[!NOTE]
>
>È possibile creare un gestore di firme personalizzato per il servizio Signature che viene richiamato quando vengono invocate determinate operazioni, ad esempio la firma di un documento PDF.

**Nomi dei campi firma**

Per alcune operazioni del servizio Firma è necessario specificare il nome del campo firma in cui viene eseguita un’operazione. Ad esempio, quando si firma un documento PDF, è necessario specificare il nome del campo firma da firmare. Si supponga che il nome completo di un campo firma sia `form1[0].Form1[0].SignatureField1[0]`. È possibile specificare `SignatureField1[0]` invece di `form1[0].Form1[0].SignatureField1[0]`.

A volte un conflitto causa la firma del campo errato da parte del servizio Firma o l’esecuzione di un’altra operazione che richiede il nome del campo firma. Questo conflitto è il risultato del nome `SignatureField1[0]` visualizzato in due o più posizioni nello stesso documento PDF. Ad esempio, si consideri un documento PDF contenente due campi firma denominati `form1[0].Form1[0].SignatureField1[0]` e `form1[0].Form1[0].SubForm1[0].SignatureField1[0]` e si specifica `SignatureField1[0]`. In questo caso, il servizio Firma firma firma firma il primo campo firma rilevato durante l’iterazione su tutti i campi firma del documento.

Se all’interno di un documento PDF sono presenti più campi firma, è consigliabile specificare i nomi completi dei campi firma. Cioè, specifica `form1[0].Form1[0].SignatureField1[0]`invece di `SignatureField1[0]`.

È possibile eseguire queste attività utilizzando il servizio Firma:

* Aggiungere ed eliminare campi firma digitale in un documento PDF. (Vedere [Aggiunta di campi firma](digitally-signing-certifying-documents.md#adding-signature-fields).)
* Recupera i nomi dei campi firma presenti in un documento PDF. (Vedere [Recupero dei nomi dei campi firma](digitally-signing-certifying-documents.md#retrieving-signature-field-names).)
* Modificare i campi firma. (Vedere [Modifica dei campi firma](digitally-signing-certifying-documents.md#modifying-signature-fields).)
* Firma digitale dei documenti PDF. (Consultare [Firma digitale di documenti PDF](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents).)
* Certifica i documenti PDF. (Vedere [Certificazione di documenti PDF](digitally-signing-certifying-documents.md#certifying-pdf-documents).)
* Convalida delle firme digitali presenti in un documento PDF. (Consultare [Verifica delle firme digitali](digitally-signing-certifying-documents.md#verifying-digital-signatures).)
* Convalida di tutte le firme digitali presenti in un documento PDF. (Consultare [Verifica di più firme digitali](digitally-signing-certifying-documents.md#verifying-digital-signatures).)
* Rimuovere una firma digitale da un campo firma. (Vedere [Rimozione di firme digitali](digitally-signing-certifying-documents.md#removing-digital-signatures).)

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Signature, vedere [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Aggiunta di campi firma {#adding-signature-fields}

Le firme digitali vengono visualizzate nei campi firma, ovvero nei campi modulo che contengono una rappresentazione grafica della firma. I campi firma possono essere visibili o invisibili. I firmatari possono utilizzare un campo firma preesistente oppure aggiungere un campo firma a livello di programmazione. In entrambi i casi, è necessario che il campo firma esista prima che sia possibile firmare un documento PDF.

È possibile aggiungere un campo firma a livello di programmazione utilizzando l’API Java del servizio Firma o l’API del servizio Web Firma. È possibile aggiungere più campi firma a un documento PDF; tuttavia, ogni nome del campo firma deve essere univoco.

>[!NOTE]
>
>Alcuni tipi di documenti PDF non consentono l’aggiunta programmatica di un campo firma. Per ulteriori informazioni sul servizio Signature e sull&#39;aggiunta di campi firma, vedere [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary-of-steps}

Per aggiungere un campo firma a un documento PDF, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Creare un client di firma.
1. Ottenere un documento PDF a cui viene aggiunto un campo firma.
1. Aggiungere un campo firma.
1. Salvare il documento PDF come file PDF.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è distribuito su JBoss)
* jbossall-client.jar (richiesto se AEM Forms è distribuito su JBoss)

**Creare un client di firma**

Prima di poter eseguire un’operazione del servizio Firma a livello di programmazione, è necessario creare un client del servizio Signature.

**Ottenere un documento PDF al quale viene aggiunto un campo firma**

È necessario ottenere un documento PDF al quale viene aggiunto un campo firma.

**Aggiungere un campo firma**

Per aggiungere correttamente un campo firma a un documento PDF, è necessario specificare i valori di coordinate che identificano la posizione del campo firma. Se si aggiunge un campo firma invisibile, questi valori non sono obbligatori. È inoltre possibile specificare quali campi del documento PDF sono bloccati dopo l’applicazione della firma al campo firma.

**Salvare il documento PDF come file PDF**

Dopo aver aggiunto un campo firma al documento PDF, è possibile salvarlo come file PDF per consentire agli utenti di aprirlo in Acrobat o Adobe Reader.

**Consulta anche**

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Firma digitale di documenti PDF](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

### Aggiungere campi firma utilizzando l’API Java {#add-signature-fields-using-the-java-api}

Aggiungere un campo firma utilizzando l’API Firma (Java):

1. Includi file di progetto

   Includi file JAR client, ad esempio adobe-signatures-client.jar, nel percorso di classe del progetto Java.

1. Creare un client di firma

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `SignatureServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Ottenere un documento PDF al quale viene aggiunto un campo firma

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento PDF a cui viene aggiunto un campo firma utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del documento PDF.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Aggiungere un campo firma

   * Creare un oggetto `PositionRectangle` che specifica la posizione del campo firma utilizzando il relativo costruttore. All&#39;interno del costruttore, specificare i valori delle coordinate.
   * Se necessario, creare un oggetto `FieldMDPOptions` che specifichi i campi bloccati quando al campo firma viene applicata una firma digitale.
   * Aggiungere un campo firma a un documento PDF richiamando il metodo `addSignatureField` dell’oggetto `SignatureServiceClient` e passando i seguenti valori:

      * A `com.adobe.idp`. `Document` oggetto che rappresenta il documento PDF a cui viene aggiunto un campo firma.
      * Valore stringa che specifica il nome del campo firma.
      * Valore `java.lang.Integer` che rappresenta il numero di pagina a cui viene aggiunto un campo firma.
      * Un oggetto `PositionRectangle` che specifica la posizione del campo firma.
      * Oggetto `FieldMDPOptions` che specifica i campi del documento PDF bloccati dopo l’applicazione della firma digitale al campo firma. Questo valore del parametro è facoltativo ed è possibile trasmettere `null`.
   * Un oggetto `PDFSeedValueOptions` che specifica diversi valori di esecuzione. Questo valore del parametro è facoltativo ed è possibile trasmettere `null`.

      Il metodo `addSignatureField` restituisce un valore `com.adobe.idp`. `Document` oggetto che rappresenta un documento PDF contenente un campo firma.
   >[!NOTE]
   >
   >È possibile richiamare il metodo `addInvisibleSignatureField` dell&#39;oggetto `SignatureServiceClient` per aggiungere un campo firma invisibile.

1. Salvare il documento PDF come file PDF

   * Crea un oggetto `java.io.File` e assicurati che l&#39;estensione del file sia .pdf.
   * Richiama il `com.adobe.idp`. `Document` il  `copyToFile` metodo dell&#39;oggetto per copiare il contenuto dell&#39; `Document` oggetto nel file. Assicurati di utilizzare il `com.adobe.idp`. `Document` oggetto restituito dal  `addSignatureField` metodo .

**Consulta anche**

[Avvio rapido API Servizio firma](/help/forms/developing/signature-service-java-api-quick.md#signature-service-java-api-quick-start-soap)

### Aggiungere campi firma utilizzando l’API del servizio Web {#add-signature-fields-using-the-web-service-api}

Per aggiungere un campo firma utilizzando l’API Firma (servizio Web):

1. Includi file di progetto

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurati di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Creare un client di firma

   * Creare un oggetto `SignatureServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `SignatureServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/SignatureService?WSDL`). Non è necessario utilizzare l&#39;attributo `lc_version` . Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Crea un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `SignatureServiceClient.Endpoint.Binding` . Imposta il valore restituito su `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegna il nome utente del modulo di AEM al campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore della password corrispondente al campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Ottenere un documento PDF al quale viene aggiunto un campo firma

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L’oggetto `BLOB` viene utilizzato per memorizzare il documento PDF che conterrà un campo firma.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni dell&#39;array di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare l’array di byte con i dati del flusso richiamando il metodo `Read` dell’oggetto `System.IO.FileStream` e passando l’array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando la relativa proprietà `MTOM` con il contenuto dell&#39;array di byte.

1. Aggiungere un campo firma

   Aggiungere un campo firma al documento PDF richiamando il metodo `addSignatureField` dell’oggetto `SignatureServiceClient` e passando i seguenti valori:

   * Un oggetto `BLOB` che rappresenta il documento PDF a cui viene aggiunto un campo firma.
   * Valore stringa che specifica il nome del campo firma.
   * Un valore intero che rappresenta il numero di pagina a cui viene aggiunto un campo firma.
   * Un oggetto `PositionRect` che specifica la posizione del campo firma.
   * Oggetto `FieldMDPOptions` che specifica i campi del documento PDF bloccati dopo l’applicazione della firma digitale al campo firma. Questo valore del parametro è facoltativo ed è possibile trasmettere `null`.
   * Un oggetto `PDFSeedValueOptions` che specifica diversi valori di esecuzione. Questo valore del parametro è facoltativo ed è possibile trasmettere `null`.

   Il metodo `addSignatureField` restituisce un oggetto `BLOB` che rappresenta un documento PDF contenente un campo firma.

1. Salvare il documento PDF come file PDF

   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF che conterrà il campo firma e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `BLOB` restituito dal metodo `addSignatureField`. Compilare l&#39;array di byte ottenendo il valore del membro dati `BLOB` dell&#39;oggetto `binaryData`.
   * Creare un oggetto `System.IO.BinaryWriter` richiamandone il costruttore e passando l&#39;oggetto `System.IO.FileStream`.
   * Scrivi il contenuto dell’array di byte in un file PDF richiamando il metodo `Write` dell’oggetto `System.IO.BinaryWriter` e passando l’array di byte.

**Consulta anche**

[Richiamo di AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamo di AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Recupero dei nomi dei campi firma {#retrieving-signature-field-names}

È possibile recuperare i nomi di tutti i campi firma presenti in un documento PDF che si desidera firmare o certificare. Se non si è certi dei nomi dei campi firma presenti in un documento PDF o si desidera verificarli, è possibile recuperarli a livello di programmazione. Il servizio Firma restituisce il nome completo del campo firma, ad esempio `form1[0].grantApplication[0].page1[0].SignatureField1[0]`.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Firma, vedere [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)

### Riepilogo dei passaggi {#summary_of_steps-1}

Per recuperare i nomi dei campi firma, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Creare un client di firma.
1. Ottenere il documento PDF contenente i campi firma.
1. Recupera i nomi dei campi firma.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è distribuito su JBoss)
* jbossall-client.jar (richiesto se AEM Forms è distribuito su JBoss)

Per informazioni sulla posizione di questi file JAR, consulta [Inclusione dei file della libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un client di firma**

Prima di poter eseguire un’operazione del servizio Firma a livello di programmazione, è necessario creare un client del servizio Signature.

**Ottenere il documento PDF contenente i campi firma**

Recupera un documento PDF contenente campi firma.

**Recupera i nomi dei campi firma**

È possibile recuperare i nomi dei campi firma dopo aver recuperato un documento PDF contenente uno o più campi firma.

**Consulta anche**

[Recupera i nomi dei campi firma utilizzando l’API Java](digitally-signing-certifying-documents.md#retrieve-signature-field-names-using-the-java-api)

[Recupera il campo firma utilizzando l’API del servizio Web](digitally-signing-certifying-documents.md#retrieve-signature-field-using-the-web-service-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Aggiunta di campi firma](digitally-signing-certifying-documents.md#adding-signature-fields)

### Recupera i nomi dei campi firma utilizzando l’API Java {#retrieve-signature-field-names-using-the-java-api}

Recupera i nomi dei campi firma utilizzando l’API firma (Java):

1. Includi file di progetto

   Includi file JAR client, come adobe-signatures-client.jar, nel percorso di classe del progetto Java.

1. Creare un client di firma

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `SignatureServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Ottenere il documento PDF contenente i campi firma

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento PDF contenente campi firma utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del documento PDF.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Recupera i nomi dei campi firma

   * Recupera i nomi dei campi firma richiamando il metodo `getSignatureFieldList` dell’oggetto `SignatureServiceClient` e passando l’oggetto `com.adobe.idp.Document` che contiene il documento PDF contenente i campi firma. Questo metodo restituisce un oggetto `java.util.List`, in cui ogni elemento contiene un oggetto `PDFSignatureField`. Utilizzando questo oggetto è possibile ottenere informazioni aggiuntive su un campo firma, ad esempio se è visibile.
   * Iterare l’oggetto `java.util.List` per determinare se sono presenti nomi di campo firma. Per ogni campo firma del documento PDF è possibile ottenere un oggetto `PDFSignatureField` separato. Per ottenere il nome del campo firma, richiamare il metodo `getName` dell’oggetto `PDFSignatureField`. Questo metodo restituisce un valore stringa che specifica il nome del campo firma.

**Consulta anche**

[Recupero dei nomi dei campi firma](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

[Avvio rapido (modalità SOAP): Recupero dei nomi dei campi firma tramite API Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-retrieving-signature-field-names-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Recupera il campo firma utilizzando l’API del servizio Web {#retrieve-signature-field-using-the-web-service-api}

Recupera i nomi dei campi firma utilizzando l’API firma (servizio Web):

1. Includi file di progetto

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurati di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Creare un client di firma

   * Creare un oggetto `SignatureServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `SignatureServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/SignatureService?WSDL`). Non è necessario utilizzare l&#39;attributo `lc_version` . Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Crea un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `SignatureServiceClient.Endpoint.Binding` . Imposta il valore restituito su `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegna il nome utente del modulo di AEM al campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore della password corrispondente al campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Ottenere il documento PDF contenente i campi firma

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L’oggetto `BLOB` viene utilizzato per memorizzare il documento PDF contenente campi firma.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni dell&#39;array di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare l’array di byte con i dati del flusso richiamando il metodo `Read` dell’oggetto `System.IO.FileStream` e passando l’array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando al relativo campo `MTOM` il contenuto dell&#39;array di byte.

1. Recupera i nomi dei campi firma

   * Recupera i nomi dei campi firma richiamando il metodo `getSignatureFieldList` dell’oggetto `BLOB` e passando l’oggetto `SignatureServiceClient` che contiene il documento PDF contenente i campi firma. Questo metodo restituisce un oggetto raccolta `MyArrayOfPDFSignatureField` in cui ogni elemento contiene un oggetto `PDFSignatureField`.
   * Iterare l’oggetto `MyArrayOfPDFSignatureField` per determinare se sono presenti nomi di campo firma. Per ogni campo firma del documento PDF è possibile ottenere un oggetto `PDFSignatureField`. Per ottenere il nome del campo firma, richiamare il metodo `getName` dell’oggetto `PDFSignatureField`. Questo metodo restituisce un valore stringa che specifica il nome del campo firma.

**Consulta anche**

[Recupero dei nomi dei campi firma](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

[Richiamo di AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamo di AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Modifica dei campi firma {#modifying-signature-fields}

È possibile modificare i campi firma che si trovano in un documento PDF utilizzando l’API Java e l’API del servizio Web. La modifica di un campo firma comporta la manipolazione dei valori del dizionario di blocco del campo firma o dei valori del dizionario dei valori di seed.

Un *dizionario di blocco dei campi* specifica un elenco di campi che sono bloccati al momento della firma del campo firma. Un campo bloccato impedisce agli utenti di apportare modifiche al campo. Un *dizionario dei valori di seed* contiene informazioni vincolanti utilizzate al momento dell&#39;applicazione della firma. Ad esempio, è possibile modificare le autorizzazioni per controllare le azioni che possono verificarsi senza annullare la validità di una firma.

Modificando un campo firma esistente, è possibile apportare modifiche al documento PDF per riflettere i cambiamenti dei requisiti aziendali. Ad esempio, un nuovo requisito aziendale potrebbe richiedere il blocco di tutti i campi del documento dopo la firma del documento.

In questa sezione viene illustrato come modificare un campo firma modificando sia i valori del dizionario di blocco dei campi che i valori del dizionario dei valori dei valori di seed. Le modifiche apportate al dizionario di blocco dei campi firma comportano il blocco di tutti i campi del documento PDF quando un campo firma viene firmato. Le modifiche apportate al dizionario dei valori di seed non consentono l’utilizzo di tipi specifici di modifiche al documento.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Firma e sulla modifica dei campi firma, vedere [Guida di riferimento ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-2}

Per modificare i campi firma presenti in un documento PDF, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Creare un client di firma.
1. Ottenere il documento PDF contenente il campo firma da modificare.
1. Imposta i valori del dizionario.
1. Modificare il campo firma.
1. Salvare il documento PDF come file PDF.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è distribuito su JBoss)
* jbossall-client.jar (richiesto se AEM Forms è distribuito su JBoss)

Per informazioni sulla posizione di questi file JAR, consulta [Inclusione dei file della libreria Java di LiveCycle](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un client di firma**

Prima di poter eseguire un’operazione del servizio Firma a livello di programmazione, è necessario creare un client del servizio Signature.

**Ottenere il documento PDF contenente il campo firma da modificare**

Recuperare un documento PDF contenente il campo firma da modificare.

**Impostare i valori dei dizionari**

Per modificare un campo firma, assegnare valori al dizionario di blocco dei campi o al dizionario dei valori di seed corrispondente. Per specificare i valori del dizionario di blocco dei campi firma è necessario specificare i campi del documento PDF bloccati al momento della firma del campo firma. (Questa sezione illustra come bloccare tutti i campi.)

È possibile impostare i seguenti valori del dizionario dei valori di seed:

* **Controllo delle** revisioni: Specifica se il controllo di revoca viene eseguito quando viene applicata una firma al campo firma.
* **Opzioni** certificato: Assegna valori al dizionario dei valori di seed del certificato. Prima di specificare le opzioni del certificato, è consigliabile acquisire familiarità con un dizionario dei valori di seed del certificato. (Vedere [Riferimento PDF](https://www.adobe.com/devnet/acrobat/pdfs/pdf_reference_1-7.pdf).)
* **Opzioni** digest: Assegna algoritmi digest utilizzati per la firma. I valori validi sono SHA1, SHA256, SHA384, SHA512 e RIPEMD160.
* **Filtro**: Specifica il filtro utilizzato con il campo firma. Ad esempio, puoi utilizzare il filtro Adobe.PPKLite . (Vedere [Riferimento PDF](https://www.adobe.com/devnet/acrobat/pdfs/pdf_reference_1-7.pdf).)
* **Opzioni** contrassegno: Specifica i valori dei flag associati al campo firma. Il valore 1 indica che un firmatario deve utilizzare solo i valori specificati per la voce. Il valore 0 indica che sono consentiti altri valori. Ecco le posizioni Bit:

   * **1(Filtro):** gestore di firme da utilizzare per firmare il campo firma
   * **2 (SubFilter):** array di nomi che indicano codifiche accettabili da utilizzare per la firma
   * **3 (V)**: Numero di versione minimo richiesto del gestore di firme da utilizzare per firmare il campo firma
   * **4 (Motivi):** array di stringhe che specificano possibili motivi per la firma di un documento
   * **5 (PDFLegalWarnings):** array di stringhe che specificano possibili attestazioni legali

* **Attestati** legali: Quando un documento è certificato, viene automaticamente analizzato per specifici tipi di contenuto che possono rendere ambigui o fuorvianti i contenuti visibili di un documento. Ad esempio, un’annotazione può oscurare il testo importante per comprendere cosa viene certificato. Il processo di scansione genera avvisi che indicano la presenza di questo tipo di contenuto. Fornisce inoltre una spiegazione aggiuntiva del contenuto che potrebbe aver generato avvisi.
* **Autorizzazioni**: Specifica le autorizzazioni che possono essere utilizzate in un documento PDF senza invalidare la firma.
* **Motivi**: Specifica i motivi per cui il documento deve essere firmato.
* **Timestamp**: Specifica le opzioni di marca temporale. Ad esempio, è possibile impostare l’URL del server di marca temporale utilizzato.
* **Versione**: Specifica il numero di versione minimo del gestore di firme da utilizzare per firmare il campo firma.

**Modificare il campo firma**

Dopo aver creato un client del servizio Firma, recuperare il documento PDF contenente il campo firma da modificare e impostare i valori del dizionario, è possibile richiedere al servizio Firma di modificare il campo firma. Il servizio Firma restituisce quindi un documento PDF contenente il campo firma modificato. Il documento PDF originale non viene modificato.

**Salvare il documento PDF come file PDF**

Salvare come file PDF il documento PDF contenente il campo firma modificato in modo che gli utenti possano aprirlo in Acrobat o Adobe Reader.

**Consulta anche**

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API Servizio firma](/help/forms/developing/signature-service-java-api-quick.md#signature-service-java-api-quick-start-soap)

[Firma digitale di documenti PDF](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

### Modificare i campi firma utilizzando l’API Java {#modify-signature-fields-using-the-java-api}

Modificare un campo firma utilizzando l’API Firma (Java):

1. Includi file di progetto

   Includi file JAR client, ad esempio adobe-signatures-client.jar, nel percorso di classe del progetto Java.

1. Creare un client di firma

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `SignatureServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Ottenere il documento PDF contenente il campo firma da modificare

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento PDF contenente il campo firma da modificare utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del documento PDF.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Impostare i valori dei dizionari

   * Creare un oggetto `PDFSignatureFieldProperties` utilizzando il relativo costruttore. Un oggetto `PDFSignatureFieldProperties` memorizza informazioni sul dizionario di blocco dei campi firma e sul dizionario dei valori di seed.
   * Creare un oggetto `PDFSeedValueOptionSpec` utilizzando il relativo costruttore. Questo oggetto consente di impostare i valori del dizionario dei valori di seed.
   * Non consentire le modifiche al documento PDF richiamando il metodo `setMdpValue` dell’oggetto `MDPPermissions.NoChanges` e passando il valore di enumerazione `PDFSeedValueOptionSpec`.
   * Creare un oggetto `FieldMDPOptionSpec` utilizzando il relativo costruttore. Questo oggetto consente di impostare i valori del dizionario di blocco dei campi firma.
   * Bloccare tutti i campi nel documento PDF richiamando il metodo `setMdpValue` dell’oggetto `FieldMDPAction.ALL` e passando il valore di enumerazione `FieldMDPOptionSpec`.
   * Impostare le informazioni sul dizionario dei valori di seed richiamando il metodo `setSeedValue` dell’oggetto `PDFSeedValueOptionSpec` e passando l’oggetto `PDFSignatureFieldProperties`.
   * Per impostare le informazioni sul dizionario di blocco dei campi firma, richiamare il metodo `setFieldMDP` dell’oggetto `FieldMDPOptionSpec` e passare l’oggetto `PDFSignatureFieldProperties`.

   >[!NOTE]
   >
   >Per visualizzare tutti i valori del dizionario dei valori di seed che è possibile impostare, vedere il riferimento alla classe `PDFSeedValueOptionSpec`. (Consulta [Riferimento API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).)

1. Modificare il campo firma

   Modificare il campo firma richiamando il metodo `modifySignatureField` dell’oggetto `SignatureServiceClient` e passando i seguenti valori:

   * L&#39;oggetto `com.adobe.idp.Document` che memorizza il documento PDF contenente il campo firma da modificare
   * Valore stringa che specifica il nome del campo firma
   * Oggetto `PDFSignatureFieldProperties` che memorizza le informazioni sul dizionario di blocco dei campi firma e sul dizionario dei valori di seed

   Il metodo `modifySignatureField` restituisce un oggetto `com.adobe.idp.Document` che memorizza un documento PDF contenente il campo firma modificato.

1. Salvare il documento PDF come file PDF

   * Crea un oggetto `java.io.File` e assicurati che l&#39;estensione del nome file sia .pdf.
   * Richiamare il metodo `copyToFile` dell&#39;oggetto `com.adobe.idp.Document` per copiare nel file il contenuto dell&#39;oggetto `com.adobe.idp.Document`. Assicurarsi di utilizzare l&#39;oggetto `com.adobe.idp.Document` restituito dal metodo `modifySignatureField`.

### Modificare i campi firma utilizzando l’API del servizio Web {#modify-signature-fields-using-the-web-service-api}

Modificare un campo firma utilizzando l’API Firma (servizio Web):

1. Includi file di progetto

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurati di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Creare un client di firma

   * Creare un oggetto `SignatureServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `SignatureServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/SignatureService?WSDL`). Non è necessario utilizzare l&#39;attributo `lc_version` . Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Crea un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `SignatureServiceClient.Endpoint.Binding` . Imposta il valore restituito su `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegna il nome utente del modulo di AEM al campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore della password corrispondente al campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Ottenere il documento PDF contenente il campo firma da modificare

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L’oggetto `BLOB` viene utilizzato per memorizzare il documento PDF contenente il campo firma da modificare.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni dell&#39;array di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare l’array di byte con i dati del flusso richiamando il metodo `Read` dell’oggetto `System.IO.FileStream` e passando l’array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando alla relativa proprietà `MTOM` il contenuto dell&#39;array di byte.

1. Impostare i valori dei dizionari

   * Creare un oggetto `PDFSignatureFieldProperties` utilizzando il relativo costruttore. Questo oggetto memorizza le informazioni sul dizionario di blocco dei campi firma e sul dizionario dei valori di seed.
   * Creare un oggetto `PDFSeedValueOptionSpec` utilizzando il relativo costruttore. Questo oggetto consente di impostare i valori del dizionario dei valori di seed.
   * Non consentire le modifiche al documento PDF assegnando il valore di enumerazione `MDPPermissions.NoChanges` al membro dati `PDFSeedValueOptionSpec` dell&#39;oggetto `mdpValue`.
   * Creare un oggetto `FieldMDPOptionSpec` utilizzando il relativo costruttore. Questo oggetto consente di impostare i valori del dizionario di blocco dei campi firma.
   * Bloccare tutti i campi nel documento PDF assegnando il valore di enumerazione `FieldMDPAction.ALL` al membro dati `FieldMDPOptionSpec` dell’oggetto `mdpValue`.
   * Impostare le informazioni sul dizionario dei valori di seed assegnando l&#39;oggetto `PDFSeedValueOptionSpec` al membro dati `PDFSignatureFieldProperties` dell&#39;oggetto `seedValue`.
   * Impostare le informazioni sul dizionario di blocco dei campi firma assegnando l&#39;oggetto `FieldMDPOptionSpec` al membro dati `PDFSignatureFieldProperties` dell&#39;oggetto `fieldMDP`.

   >[!NOTE]
   >
   >Per visualizzare tutti i valori del dizionario dei valori di seed che è possibile impostare, vedere il riferimento alla classe `PDFSeedValueOptionSpec`. (Consulta [Riferimento API AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)).

1. Modificare il campo firma

   Modificare il campo firma richiamando il metodo `modifySignatureField` dell’oggetto `SignatureServiceClient` e passando i seguenti valori:

   * L&#39;oggetto `BLOB` che memorizza il documento PDF contenente il campo firma da modificare
   * Valore stringa che specifica il nome del campo firma
   * Oggetto `PDFSignatureFieldProperties` che memorizza le informazioni sul dizionario di blocco dei campi firma e sul dizionario dei valori di seed

   Il metodo `modifySignatureField` restituisce un oggetto `BLOB` che memorizza un documento PDF contenente il campo firma modificato.

1. Salvare il documento PDF come file PDF

   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF che conterrà il campo firma e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `BLOB` restituito dal metodo `addSignatureField`. Compilare l&#39;array di byte ottenendo il valore del membro dati `BLOB` dell&#39;oggetto `MTOM`.
   * Creare un oggetto `System.IO.BinaryWriter` richiamandone il costruttore e passando l&#39;oggetto `System.IO.FileStream`.
   * Scrivi il contenuto dell’array di byte in un file PDF richiamando il metodo `Write` dell’oggetto `System.IO.BinaryWriter` e passando l’array di byte.

**Consulta anche**

[Richiamo di AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamo di AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Firma digitale di documenti PDF {#digitally-signing-pdf-documents}

Le firme digitali possono essere applicate ai documenti PDF per garantire un livello di protezione. Le firme digitali, come le firme scritte a mano, forniscono un mezzo con cui i firmatari si identificano e fanno dichiarazioni su un documento. La tecnologia utilizzata per la firma digitale dei documenti aiuta a garantire che sia il firmatario che i destinatari siano chiari su ciò che è stato firmato e fiduciosi che il documento non sia stato modificato dopo la firma.

I documenti PDF sono firmati tramite la tecnologia a chiave pubblica. Un firmatario ha due chiavi: una chiave pubblica e una chiave privata. La chiave privata viene memorizzata nella credenziale di un utente che deve essere disponibile al momento della firma. La chiave pubblica è memorizzata nel certificato dell’utente e deve essere disponibile ai destinatari per convalidare la firma. Le informazioni sui certificati revocati si trovano nelle risposte degli elenchi di revoche dei certificati (CRL) e del protocollo di stato dei certificati online (OCSP) distribuite dalle autorità di certificazione (CA). L’ora della firma può essere ottenuta da una fonte attendibile nota come Autorità di marcatura temporale.

>[!NOTE]
>
>Prima di poter firmare digitalmente un documento PDF, è necessario assicurarsi di aggiungere il certificato ad AEM Forms. Un certificato viene aggiunto tramite la console di amministrazione o a livello di programmazione utilizzando l’API di Trust Manager. (Vedere [Importazione delle credenziali tramite l&#39;API di Trust Manager](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api).)

È possibile firmare digitalmente i documenti PDF a livello di programmazione. Durante la firma digitale di un documento PDF, è necessario fare riferimento a una credenziale di protezione esistente in AEM Forms. La credenziale è la chiave privata utilizzata per la firma.

Quando un documento PDF viene firmato, il servizio Firma esegue i seguenti passaggi:

1. Il servizio Signature recupera la credenziale dal TrustStore passando l&#39;alias specificato nella richiesta.
1. Il TrustStore cerca la credenziale specificata.
1. La credenziale viene restituita al servizio Firma e viene utilizzata per firmare il documento. La credenziale viene anche memorizzata nella cache rispetto all’alias per le richieste future.

Per informazioni sulla gestione delle credenziali di protezione, consulta la guida *Installazione e distribuzione di AEM Forms* per il server delle applicazioni.

>[!NOTE]
>
>Esistono differenze tra la firma e la certificazione dei documenti. (Vedere [Certificazione di documenti PDF](digitally-signing-certifying-documents.md#certifying-pdf-documents).)

>[!NOTE]
>
>La firma non è supportata da tutti i documenti PDF. Per ulteriori informazioni sul servizio Firma e sulla firma digitale dei documenti, vedere [Guida di riferimento ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Il servizio Signature non supporta i file XDP con dati PDF incorporati come input per un’operazione, ad esempio la certificazione di un documento. Questa azione causa la generazione di un `PDFOperationException` da parte del servizio Signature. Per risolvere il problema, convertire il file XDP in un file PDF utilizzando il servizio Utilità PDF, quindi passare il file PDF convertito a un’operazione del servizio Firma. (Vedere [Uso delle utility PDF](/help/forms/developing/pdf-utilities.md#working-with-pdf-utilities).)

**Cipher in Shield credenziale HSM**

Quando si utilizza una credenziale HSM Cipher in Shield per firmare o certificare un documento PDF, non è possibile utilizzare la nuova credenziale finché non viene riavviato il server dell&#39;applicazione J2EE in cui è distribuito AEM Forms. Tuttavia, è possibile impostare un valore di configurazione, in modo che l&#39;operazione di firma o certificazione funzioni senza riavviare il server dell&#39;applicazione J2EE.

Puoi aggiungere il seguente valore di configurazione nel file cknfastrc, che si trova in /opt/nfast/cknfastrc (o c:\nfast\cknfastrc):

```shell
    CKNFAST_ASSUME_SINGLE_PROCESS=0
```

Dopo aver aggiunto questo valore di configurazione al file cknfastrc, è possibile utilizzare la nuova credenziale senza riavviare il server dell&#39;applicazione J2EE.

**Firma non attendibile**

Durante la certificazione e la firma dello stesso documento PDF, se la firma di certificazione non è attendibile, viene visualizzato un triangolo giallo rispetto alla prima firma all’apertura del documento PDF in Acrobat o Adobe Reader. La firma di certificazione deve essere attendibile per evitare questa situazione.

**Firma di documenti che sono moduli basati su XFA**

Se si tenta di firmare un modulo basato su XFA utilizzando l’API del servizio Firma, i dati potrebbero mancare nel percorso `View` `Signed` `Version` presente in Acrobat. Ad esempio, considera il seguente flusso di lavoro:

* Se si utilizza un file XDP creato utilizzando Designer, è possibile unire una struttura del modulo contenente un campo firma e dati XML contenenti i dati del modulo. Il servizio Forms consente di generare un documento PDF interattivo.
* È possibile firmare il documento PDF utilizzando l’API del servizio Firma.

### Riepilogo dei passaggi {#summary_of_steps-3}

Per firmare digitalmente un documento PDF, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Creare un client del servizio Firma.
1. Richiedere la firma del documento PDF.
1. Firma il documento PDF.
1. Salvare il documento PDF firmato come file PDF.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è distribuito su JBoss)
* jbossall-client.jar (richiesto se AEM Forms è distribuito su JBoss)

**Creare un client di firme**

Prima di poter eseguire un’operazione del servizio Firma a livello di programmazione, è necessario creare un client del servizio Signature.

**Richiedere la firma del documento PDF**

Per firmare un documento PDF, è necessario ottenere un documento PDF contenente un campo firma. Se un documento PDF non contiene un campo firma, non può essere firmato. È possibile aggiungere un campo firma utilizzando Designer o a livello di programmazione.

**Firma il documento PDF**

Quando si firma un documento PDF, è possibile impostare le opzioni di esecuzione utilizzate dal servizio Firma. Puoi impostare le seguenti opzioni:

* Opzioni di aspetto
* Controllo della revoca
* Valori di marca temporale

Per impostare le opzioni di aspetto, utilizzare un oggetto `PDFSignatureAppearanceOptionSpec`. Ad esempio, è possibile visualizzare la data all’interno di una firma richiamando il metodo `setShowDate` dell’oggetto `true` e passando `PDFSignatureAppearanceOptionSpec`.

È inoltre possibile specificare se eseguire o meno un controllo di revoca che determini la revoca del certificato utilizzato per la firma digitale di un documento PDF. Per eseguire il controllo di revoca, è possibile specificare uno dei seguenti valori:

* **NoCheck**: Non eseguire il controllo di revoca.
* **Migliore** sforzo: Tentare sempre di verificare la revoca di tutti i certificati nella catena. Se si verifica un problema nel controllo, si presume che la revoca sia valida. Se si verifica un errore, si supponga che il certificato non sia revocato.
* **CheckIfAvailable:** verifica la revoca di tutti i certificati nella catena se sono disponibili informazioni sulla revoca. Se si verifica un problema nel controllo, si presume che la revoca non sia valida. Se si verifica un errore, si supponga che il certificato sia revocato e non valido. Questo è il valore predefinito.
* **AlwaysCheck**: Verifica la revoca di tutti i certificati nella catena. Se le informazioni di revoca non sono presenti in alcun certificato, si presume che la revoca non sia valida.

Per eseguire il controllo di revoca su un certificato, è possibile specificare un URL per un server dell’elenco di revoche di certificati (CRL) utilizzando un oggetto `CRLOptionSpec`. Tuttavia, se si desidera eseguire il controllo di revoca e non si specifica un URL a un server CRL, il servizio Signature ottiene l’URL dal certificato.

Invece di utilizzare un server CRL, è possibile utilizzare un server OCSP (Online Certificate Status Protocol) quando si esegue il controllo di revoca. In genere, quando si utilizza un server OCSP anziché un server CRL, il controllo di revoca viene eseguito più rapidamente. (Vedi &quot;Protocollo di stato del certificato online&quot; in [https://tools.ietf.org/html/rfc2560](https://tools.ietf.org/html/rfc2560).)

È possibile impostare l&#39;ordine del server CRL e OCSP utilizzato dal servizio Signature utilizzando le applicazioni e i servizi Adobe. Ad esempio, se il server OCSP è impostato per primo in Adobe Applications and Services, viene controllato il server OCSP, seguito dal server CRL. (Consulta &quot;Gestione di certificati e credenziali tramite Trust Store&quot; nella Guida di AAC).

Se si specifica di non eseguire il controllo di revoca, il servizio Firma non controlla se il certificato utilizzato per firmare o certificare un documento è stato revocato. In altre parole, le informazioni sul server CRL e OCSP vengono ignorate.

>[!NOTE]
>
>Anche se è possibile specificare un CRL o un server OCSP nel certificato, è possibile sostituire l’URL specificato nel certificato utilizzando un oggetto `CRLOptionSpec` e un oggetto `OCSPOptionSpec`. Ad esempio, per ignorare il server CRL, è possibile richiamare il metodo `setLocalURI` dell’oggetto `CRLOptionSpec`.

Per marca temporale si intende il processo di tracciamento dell’ora in cui un documento firmato o certificato è stato modificato. Una volta firmato, il documento non deve essere modificato nemmeno dal proprietario del documento. L’indicazione dell’ora aiuta a garantire la validità di un documento firmato o certificato. È possibile impostare le opzioni di marca temporale utilizzando un oggetto `TSPOptionSpec`. Ad esempio, puoi specificare l’URL di un server del provider di servizi di marca temporale (TSP).

>[!NOTE]
>
>Nel Java e nel servizio Web passano attraverso le sezioni e il corrispondente avvio rapido, viene utilizzato il controllo di revoca. Poiché non sono specificate informazioni sul server CRL o OCSP, le informazioni sul server vengono ottenute dal certificato utilizzato per firmare digitalmente il documento PDF.

Per firmare correttamente un documento PDF, è possibile specificare il nome completo del campo firma che conterrà la firma digitale, ad esempio `form1[0].#subform[1].SignatureField3[3]`. Quando si utilizza un campo modulo XFA, è possibile utilizzare anche il nome parziale del campo firma: `SignatureField3[3]`.

Per firmare digitalmente un documento PDF è inoltre necessario fare riferimento a una credenziale di protezione. Per fare riferimento a una credenziale di protezione, specificare un alias. L’alias è un riferimento a una credenziale effettiva che può trovarsi in un file PKCS#12 (con estensione .pfx) o in un modulo di protezione hardware (HSM). Per informazioni sulle credenziali di protezione, consulta la guida *Installazione e distribuzione di AEM Forms* per il server delle applicazioni.

**Salvare il documento PDF firmato**

Dopo che il servizio Firma firma ha apposto la firma digitale al documento PDF, è possibile salvarlo come file PDF per consentire agli utenti di aprirlo in Acrobat o Adobe Reader.

**Consulta anche**

[Firma digitale dei documenti PDF utilizzando l’API Java](digitally-signing-certifying-documents.md#digitally-sign-pdf-documents-using-the-java-api)

[Firma digitale di documenti PDF tramite l’API del servizio Web](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents-using-the-web-service-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Aggiunta di campi firma](digitally-signing-certifying-documents.md#adding-signature-fields)

[Recupero dei nomi dei campi firma](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

### Firma digitale dei documenti PDF utilizzando l&#39;API Java {#digitally-sign-pdf-documents-using-the-java-api}

Firma digitale di un documento PDF utilizzando l’API Firma (Java):

1. Includi file di progetto

   Includi file JAR client, ad esempio adobe-signatures-client.jar, nel percorso di classe del progetto Java.

1. Creare un client di firme

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `SignatureServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Richiedere la firma del documento PDF

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento PDF da firmare digitalmente utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del documento PDF.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Firma il documento PDF

   Firma il documento PDF richiamando il metodo `sign` dell’oggetto `SignatureServiceClient` e passando i seguenti valori:

   * Un oggetto `com.adobe.idp.Document` che rappresenta il documento PDF da firmare.
   * Valore stringa che rappresenta il nome del campo firma che conterrà la firma digitale.
   * Oggetto `Credential` che rappresenta la credenziale utilizzata per firmare digitalmente il documento PDF. Creare un oggetto `Credential` richiamando il metodo statico `Credential` dell&#39;oggetto e passando un valore di stringa che specifica il valore di alias corrispondente alla credenziale di sicurezza.`getInstance`
   * Oggetto `HashAlgorithm` che specifica un membro di dati statico che rappresenta l&#39;algoritmo hash da utilizzare per digest del documento PDF. Ad esempio, puoi specificare `HashAlgorithm.SHA1` per utilizzare l’algoritmo SHA1.
   * Valore stringa che rappresenta il motivo per cui il documento PDF è stato firmato digitalmente.
   * Valore stringa che rappresenta le informazioni di contatto del firmatario.
   * Oggetto `PDFSignatureAppearanceOptions` che controlla l&#39;aspetto della firma digitale. Ad esempio, è possibile utilizzare questo oggetto per aggiungere un logo personalizzato a una firma digitale.
   * Un oggetto `java.lang.Boolean` che specifica se eseguire il controllo di revoca sul certificato del firmatario.
   * Un oggetto `OCSPOptionSpec` che memorizza le preferenze per il supporto del protocollo OCSP (Online Certificate Status Protocol). Se il controllo di revoca non viene eseguito, questo parametro non viene utilizzato ed è possibile specificare `null`.
   * Un oggetto `CRLPreferences` che memorizza le preferenze dell’elenco di revoche di certificati (CRL). Se il controllo di revoca non viene eseguito, questo parametro non viene utilizzato ed è possibile specificare `null`.
   * Un oggetto `TSPPreferences` che memorizza le preferenze per il supporto del provider di timestamp (TSP). Questo parametro è facoltativo e può essere `null`. Per ulteriori informazioni, consulta [Riferimento API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

   Il metodo `sign` restituisce un oggetto `com.adobe.idp.Document` che rappresenta il documento PDF firmato.

1. Salvare il documento PDF firmato

   * Crea un oggetto `java.io.File` e assicurati che l&#39;estensione del file sia .pdf.
   * Richiamare il metodo `copyToFile` dell&#39;oggetto `com.adobe.idp.Document` e passare `java.io.File`per copiare il contenuto dell&#39;oggetto `Document` nel file . Assicurarsi di utilizzare l&#39;oggetto `com.adobe.idp.Document` restituito dal metodo `sign`.

**Consulta anche**

[Firma digitale di documenti PDF](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[Avvio rapido (modalità SOAP): Firma digitale di un documento PDF tramite l’API Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-pdf-document-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Firma digitale di documenti PDF utilizzando l&#39;API del servizio Web {#digitally-signing-pdf-documents-using-the-web-service-api}

Per firmare digitalmente un documento PDF utilizzando l’API Firma (servizio Web):

1. Includi file di progetto

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurati di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Creare un client di firme

   * Creare un oggetto `SignatureServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `SignatureServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/SignatureService?WSDL`). Non è necessario utilizzare l&#39;attributo `lc_version` . Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Crea un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `SignatureServiceClient.Endpoint.Binding` . Imposta il valore restituito su `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegna il nome utente del modulo di AEM al campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore della password corrispondente al campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Richiedere la firma del documento PDF

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare un documento PDF firmato.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF da firmare e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni dell&#39;array di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare l’array di byte con i dati del flusso richiamando il metodo `Read` dell’oggetto `System.IO.FileStream` e passando l’array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando alla relativa proprietà `MTOM` il contenuto dell&#39;array di byte.

1. Firma il documento PDF

   Firma il documento PDF richiamando il metodo `sign` dell’oggetto `SignatureServiceClient` e passando i seguenti valori:

   * Un oggetto `BLOB` che rappresenta il documento PDF da firmare.
   * Valore stringa che rappresenta il nome del campo firma che conterrà la firma digitale.
   * Oggetto `Credential` che rappresenta la credenziale utilizzata per firmare digitalmente il documento PDF. Creare un oggetto `Credential` utilizzando il relativo costruttore e specificare l&#39;alias assegnando un valore alla proprietà `Credential` dell&#39;oggetto `alias`.
   * Oggetto `HashAlgorithm` che specifica un membro di dati statico che rappresenta l&#39;algoritmo hash da utilizzare per digest del documento PDF. Ad esempio, puoi specificare `HashAlgorithm.SHA1` per utilizzare l’algoritmo SHA1.
   * Un valore booleano che specifica se viene utilizzato l&#39;algoritmo hash.
   * Valore stringa che rappresenta il motivo per cui il documento PDF è stato firmato digitalmente.
   * Valore stringa che rappresenta la posizione del firmatario.
   * Valore stringa che rappresenta le informazioni di contatto del firmatario.
   * Oggetto `PDFSignatureAppearanceOptions` che controlla l&#39;aspetto della firma digitale. Ad esempio, è possibile utilizzare questo oggetto per aggiungere un logo personalizzato a una firma digitale.
   * Un oggetto `System.Boolean` che specifica se eseguire il controllo di revoca sul certificato del firmatario. Se il controllo di revoca viene eseguito, viene incorporato nella firma. Il valore predefinito è `false`.
   * Un oggetto `OCSPOptionSpec` che memorizza le preferenze per il supporto del protocollo OCSP (Online Certificate Status Protocol). Se il controllo di revoca non viene eseguito, questo parametro non viene utilizzato ed è possibile specificare `null`. Per informazioni su questo oggetto, consulta [Riferimento API AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * Un oggetto `CRLPreferences` che memorizza le preferenze dell’elenco di revoche di certificati (CRL). Se il controllo di revoca non viene eseguito, questo parametro non viene utilizzato ed è possibile specificare `null`.
   * Un oggetto `TSPPreferences` che memorizza le preferenze per il supporto del provider di timestamp (TSP). Questo parametro è facoltativo e può essere `null`.

   Il metodo `sign` restituisce un oggetto `BLOB` che rappresenta il documento PDF firmato.

1. Salvare il documento PDF firmato

   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore. Passare un valore di stringa che rappresenta la posizione del file del documento PDF firmato e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `BLOB` restituito dal metodo `sign`. Compilare l&#39;array di byte ottenendo il valore del membro dati `BLOB` dell&#39;oggetto `MTOM`.
   * Creare un oggetto `System.IO.BinaryWriter` richiamandone il costruttore e passando l&#39;oggetto `System.IO.FileStream`.
   * Scrivi il contenuto dell’array di byte in un file PDF richiamando il metodo `Write` dell’oggetto `System.IO.BinaryWriter` e passando l’array di byte.

**Consulta anche**

[Firma digitale di documenti PDF](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[Richiamo di AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamo di AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Firma digitale di Forms interattivo {#digitally-signing-interactive-forms}

È possibile firmare un modulo interattivo creato dal servizio Forms. Ad esempio, considera il seguente flusso di lavoro:

* È possibile unire un modulo PDF basato su XFA creato utilizzando Designer e i dati del modulo contenuti in un documento XML utilizzando il servizio Forms. Il server Forms esegue il rendering di un modulo interattivo.
* È possibile firmare il modulo interattivo utilizzando l’API del servizio Firma.

Il risultato è un modulo PDF interattivo con firma digitale. Quando si firma un modulo PDF basato su un modulo XFA, assicurarsi di salvare il file PDF come modulo PDF statico di Adobe. Se si tenta di firmare un modulo PDF salvato come Adobe di modulo PDF dinamico, si verifica un’eccezione. Poiché si firma il modulo restituito dal servizio Forms, assicurarsi che contenga un campo firma.

>[!NOTE]
>
>Prima di poter firmare digitalmente un modulo interattivo, è necessario assicurarsi di aggiungere il certificato ad AEM Forms. Un certificato viene aggiunto tramite la console di amministrazione o a livello di programmazione utilizzando l’API di Trust Manager. (Vedere [Importazione delle credenziali tramite l&#39;API di Trust Manager](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api).)

Quando utilizzi l’API del servizio Forms, imposta l’opzione `GenerateServerAppearance` runtime su `true`. Questa opzione di esecuzione assicura che l’aspetto del modulo generato sul server rimanga valido quando viene aperto in Acrobat o Adobe Reader. È consigliabile impostare questa opzione di esecuzione quando si genera un modulo interattivo da firmare utilizzando l’API Forms.

>[!NOTE]
>
>Prima di leggere la firma digitale di Forms interattivo, è consigliabile avere familiarità con la firma dei documenti PDF. (Consultare [Firma digitale di documenti PDF](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents).)

### Riepilogo dei passaggi {#summary_of_steps-4}

Per firmare digitalmente un modulo interattivo restituito dal servizio Forms, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Creare un client Forms e Firme.
1. Ottenere il modulo interattivo utilizzando il servizio Forms.
1. Firma il modulo interattivo.
1. Salvare il documento PDF firmato come file PDF.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-forms-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è distribuito su JBoss)
* jbossall-client.jar (richiesto se AEM Forms è distribuito su JBoss)

Per informazioni sulla posizione di questi file JAR, consulta [Inclusione dei file della libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un client Forms e Firme**

Poiché questo flusso di lavoro richiama sia Forms che i servizi Signature, crea sia un client di servizio Forms che un client di servizio Signature.

**Ottenere il modulo interattivo utilizzando il servizio Forms**

È possibile utilizzare il servizio Forms per ottenere il modulo PDF interattivo da firmare. A partire da AEM Forms, è possibile passare un oggetto `com.adobe.idp.Document` al servizio Forms che contiene il modulo da riprodurre. Il nome di questo metodo è `renderPDFForm2`. Questo metodo restituisce un oggetto `com.adobe.idp.Document` contenente il modulo da firmare. Puoi passare questa istanza `com.adobe.idp.Document` al servizio Signature.

Analogamente, se si utilizzano servizi Web, è possibile passare l&#39;istanza `BLOB` restituita dal servizio Forms al servizio Signature.

>[!NOTE]
>
>L&#39;avvio rapido associato alla sezione Forms interattiva firma digitale richiama il metodo `renderPDFForm2` .

**Firma del modulo interattivo**

Quando si firma un documento PDF, è possibile impostare le opzioni di esecuzione utilizzate dal servizio Firma. Puoi impostare le seguenti opzioni:

* Opzioni di aspetto
* Controllo della revoca
* Valori di marca temporale

Per impostare le opzioni di aspetto, utilizzare un oggetto `PDFSignatureAppearanceOptionSpec`. Ad esempio, è possibile visualizzare la data all’interno di una firma richiamando il metodo `setShowDate` dell’oggetto `true` e passando `PDFSignatureAppearanceOptionSpec`.

**Salvare il documento PDF firmato**

Dopo aver apposto la firma digitale al documento PDF da parte del servizio Firma, è possibile salvarlo come file PDF. Il file PDF può essere aperto in Acrobat o Adobe Reader.

**Consulta anche**

[Firma digitale di un modulo interattivo utilizzando l’API Java](digitally-signing-certifying-documents.md#digitally-sign-an-interactive-form-using-the-java-api)

[Firma digitale di un modulo interattivo utilizzando l’API del servizio Web](digitally-signing-certifying-documents.md#digitally-sign-an-interactive-form-using-the-web-service-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Firma digitale di documenti PDF](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[Rendering di PDF forms interattivi](/help/forms/developing/rendering-forms.md#rendering-interactive-pdf-forms)

### Firma digitale di un modulo interattivo utilizzando l’API Java {#digitally-sign-an-interactive-form-using-the-java-api}

Firma digitale di un modulo interattivo utilizzando l’API Forms e Signature (Java):

1. Includi file di progetto

   Includi file JAR client, come adobe-signatures-client.jar e adobe-forms-client.jar, nel percorso classico del progetto Java.

1. Creare un client Forms e Firme

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `SignatureServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.
   * Creare un oggetto `FormsServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Ottenere il modulo interattivo utilizzando il servizio Forms

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento PDF da passare al servizio Forms utilizzando il relativo costruttore. Passa un valore stringa che specifica la posizione del documento PDF.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.
   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento XML contenente i dati del modulo da passare al servizio Forms utilizzando il relativo costruttore. Passa un valore di stringa che specifica la posizione del file XML.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.
   * Creare un oggetto `PDFFormRenderSpec` utilizzato per impostare le opzioni di esecuzione. Richiama il metodo `setGenerateServerAppearance` dell&#39;oggetto `PDFFormRenderSpec` e passa `true`.
   * Richiama il metodo `renderPDFForm2` dell&#39;oggetto `FormsServiceClient` e passa i seguenti valori:

      * Un oggetto `com.adobe.idp.Document` contenente il modulo PDF da eseguire.
      * Un oggetto `com.adobe.idp.Document` contenente i dati da unire al modulo.
      * Un oggetto `PDFFormRenderSpec` che memorizza le opzioni di esecuzione.
      * Un oggetto `URLSpec` contenente valori URI richiesti dal servizio Forms. Puoi specificare `null` per questo valore di parametro.
      * Un oggetto `java.util.HashMap` che memorizza gli allegati di file. Questo è un parametro facoltativo ed è possibile specificare `null` se non si desidera allegare file al modulo.

      Il metodo `renderPDFForm2` restituisce un oggetto `FormsResult` che contiene un flusso di dati del modulo

   * Recupera il modulo PDF richiamando il metodo `getOutputContent` dell’oggetto `FormsResult`. Questo metodo restituisce un oggetto `com.adobe.idp.Document` che rappresenta il modulo interattivo.


1. Firma del modulo interattivo

   Firma il documento PDF richiamando il metodo `sign` dell’oggetto `SignatureServiceClient` e passando i seguenti valori:

   * Un oggetto `com.adobe.idp.Document` che rappresenta il documento PDF da firmare. Assicurati che questo oggetto sia l&#39; `com.adobe.idp.Document` oggetto ottenuto dal servizio Forms.
   * Valore stringa che rappresenta il nome del campo firma firmato.
   * Oggetto `Credential` che rappresenta la credenziale utilizzata per firmare digitalmente il documento PDF. Creare un oggetto `Credential` richiamando il metodo statico `Credential` dell&#39;oggetto `getInstance`. Passa un valore di stringa che specifica il valore di alias corrispondente alla credenziale di sicurezza.
   * Oggetto `HashAlgorithm` che specifica un membro di dati statico che rappresenta l&#39;algoritmo hash da utilizzare per digest del documento PDF. Ad esempio, puoi specificare `HashAlgorithm.SHA1` per utilizzare l’algoritmo SHA1.
   * Valore stringa che rappresenta il motivo per cui il documento PDF è stato firmato digitalmente.
   * Valore stringa che rappresenta le informazioni di contatto del firmatario.
   * Oggetto `PDFSignatureAppearanceOptions` che controlla l&#39;aspetto della firma digitale. Ad esempio, è possibile utilizzare questo oggetto per aggiungere un logo personalizzato a una firma digitale.
   * Un oggetto `java.lang.Boolean` che specifica se eseguire il controllo di revoca sul certificato del firmatario.
   * Un oggetto `OCSPPreferences` che memorizza le preferenze per il supporto del protocollo OCSP (Online Certificate Status Protocol). Se il controllo di revoca non viene eseguito, questo parametro non viene utilizzato ed è possibile specificare `null`.
   * Un oggetto `CRLPreferences` che memorizza le preferenze dell’elenco di revoche di certificati (CRL). Se il controllo di revoca non viene eseguito, questo parametro non viene utilizzato ed è possibile specificare `null`.
   * Un oggetto `TSPPreferences` che memorizza le preferenze per il supporto del provider di timestamp (TSP). Questo parametro è facoltativo e può essere `null`.

   Il metodo `sign` restituisce un oggetto `com.adobe.idp.Document` che rappresenta il documento PDF firmato.

1. Salvare il documento PDF firmato

   * Crea un oggetto `java.io.File` e assicurati che l&#39;estensione del nome file sia .pdf.
   * Richiamare il metodo `copyToFile` dell&#39;oggetto `com.adobe.idp.Document` e passare `java.io.File`per copiare il contenuto dell&#39;oggetto `Document` nel file . Assicurarsi di utilizzare l&#39;oggetto `com.adobe.idp.Document` restituito dal metodo `sign`.

**Consulta anche**

[Firma digitale di Forms interattivo](digitally-signing-certifying-documents.md#digitally-signing-interactive-forms)

[Avvio rapido (modalità SOAP): Firma digitale di un documento PDF tramite l’API Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-pdf-document-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Firma digitale di un modulo interattivo utilizzando l’API del servizio Web {#digitally-sign-an-interactive-form-using-the-web-service-api}

Firma digitale di un modulo interattivo utilizzando l’API Forms e Signature (servizio Web):

1. Includi file di progetto

   Creare un progetto Microsoft .NET che utilizza MTOM. Poiché questa applicazione client richiama due servizi AEM Forms, crea due riferimenti al servizio. Utilizzare la seguente definizione WSDL per il riferimento al servizio associato al servizio Signature: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   Utilizza la seguente definizione WSDL per il riferimento al servizio associato al servizio Forms: `http://localhost:8080/soap/services/FormsService?WSDL&lc_version=9.0.1`.

   Poiché il tipo di dati `BLOB` è comune a entrambi i riferimenti di servizio, qualifica completamente il tipo di dati `BLOB` quando lo utilizzi. Nel corrispondente avvio rapido del servizio Web, tutte le istanze `BLOB` sono completamente qualificate.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Creare un client Forms e Firme

   * Creare un oggetto `SignatureServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `SignatureServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/SignatureService?WSDL`). Non è necessario utilizzare l&#39;attributo `lc_version` . Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Crea un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `SignatureServiceClient.Endpoint.Binding` . Imposta il valore restituito su `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegna il nome utente del modulo di AEM al campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore della password corrispondente al campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

   >[!NOTE]
   >
   >Ripeti questi passaggi per il client di servizio Forms.

1. Ottenere il modulo interattivo utilizzando il servizio Forms

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare un documento PDF firmato.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF da firmare e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni dell&#39;array di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare l’array di byte con i dati del flusso richiamando il metodo `Read` dell’oggetto `System.IO.FileStream` e passando l’array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando alla relativa proprietà `MTOM` il contenuto dell&#39;array di byte.
   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L’oggetto `BLOB` viene utilizzato per memorizzare i dati del modulo.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file XML contenente i dati del modulo e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni dell&#39;array di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare l’array di byte con i dati del flusso richiamando il metodo `Read` dell’oggetto `System.IO.FileStream` e passando l’array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando alla relativa proprietà `MTOM` il contenuto dell&#39;array di byte.
   * Creare un oggetto `PDFFormRenderSpec` utilizzato per impostare le opzioni di esecuzione. Assegna il valore `true` al campo `PDFFormRenderSpec` dell’oggetto `generateServerAppearance`.
   * Richiama il metodo `renderPDFForm2` dell&#39;oggetto `FormsServiceClient` e passa i seguenti valori:

      * Un oggetto `BLOB` contenente il modulo PDF da eseguire.
      * Un oggetto `BLOB` contenente i dati da unire al modulo.
      * Un oggetto `PDFFormRenderSpec` che memorizza le opzioni di esecuzione.
      * Un oggetto `URLSpec` contenente valori URI richiesti dal servizio Forms. Puoi specificare `null` per questo valore di parametro.
      * Un oggetto `java.util.HashMap` che memorizza gli allegati di file. Questo è un parametro facoltativo ed è possibile specificare `null` se non si desidera allegare file al modulo.
      * Parametro di output lungo utilizzato per memorizzare il numero di pagine nel modulo.
      * Un parametro di output della stringa utilizzato per il valore delle impostazioni internazionali.
      * Un valore `FormResult` che è un parametro di output utilizzato per memorizzare il modulo interattivo.
   * Recuperare il modulo PDF richiamando il campo `outputContent` dell’oggetto `FormsResult`. Questo campo memorizza un oggetto `BLOB` che rappresenta il modulo interattivo.


1. Firma del modulo interattivo

   Firma il documento PDF richiamando il metodo `sign` dell’oggetto `SignatureServiceClient` e passando i seguenti valori:

   * Un oggetto `BLOB` che rappresenta il documento PDF da firmare. Utilizza l’istanza `BLOB` restituita dal servizio Forms.
   * Valore stringa che rappresenta il nome del campo firma firmato.
   * Oggetto `Credential` che rappresenta la credenziale utilizzata per firmare digitalmente il documento PDF. Creare un oggetto `Credential` utilizzando il relativo costruttore e specificare l&#39;alias assegnando un valore alla proprietà `Credential` dell&#39;oggetto `alias`.
   * Oggetto `HashAlgorithm` che specifica un membro di dati statico che rappresenta l&#39;algoritmo hash da utilizzare per digest del documento PDF. Ad esempio, puoi specificare `HashAlgorithm.SHA1` per utilizzare l’algoritmo SHA1.
   * Un valore booleano che specifica se viene utilizzato l&#39;algoritmo hash.
   * Valore stringa che rappresenta il motivo per cui il documento PDF è stato firmato digitalmente.
   * Valore stringa che rappresenta la posizione del firmatario.
   * Valore stringa che rappresenta le informazioni di contatto del firmatario.
   * Oggetto `PDFSignatureAppearanceOptions` che controlla l&#39;aspetto della firma digitale. Ad esempio, è possibile utilizzare questo oggetto per aggiungere un logo personalizzato a una firma digitale.
   * Un oggetto `System.Boolean` che specifica se eseguire il controllo di revoca sul certificato del firmatario. Se il controllo di revoca viene eseguito, viene incorporato nella firma. Il valore predefinito è `false`.
   * Un oggetto `OCSPPreferences` che memorizza le preferenze per il supporto del protocollo OCSP (Online Certificate Status Protocol). Se il controllo di revoca non viene eseguito, questo parametro non viene utilizzato ed è possibile specificare `null`. Per informazioni su questo oggetto, consulta [Riferimento API AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * Un oggetto `CRLPreferences` che memorizza le preferenze dell’elenco di revoche di certificati (CRL). Se il controllo di revoca non viene eseguito, questo parametro non viene utilizzato ed è possibile specificare `null`.
   * Un oggetto `TSPPreferences` che memorizza le preferenze per il supporto del provider di timestamp (TSP). Questo parametro è facoltativo e può essere `null`.

   Il metodo `sign` restituisce un oggetto `BLOB` che rappresenta il documento PDF firmato.

1. Salvare il documento PDF firmato

   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore. Passare un valore di stringa che rappresenta la posizione del file del documento PDF firmato e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `BLOB` restituito dal metodo `sign`. Compilare l&#39;array di byte ottenendo il valore del membro dati `BLOB` dell&#39;oggetto `MTOM`.
   * Creare un oggetto `System.IO.BinaryWriter` richiamandone il costruttore e passando l&#39;oggetto `System.IO.FileStream`.
   * Scrivi il contenuto dell’array di byte in un file PDF richiamando il metodo `Write` dell’oggetto `System.IO.BinaryWriter` e passando l’array di byte.

**Consulta anche**

[Firma digitale di Forms interattivo](digitally-signing-certifying-documents.md#digitally-signing-interactive-forms)

[Richiamo di AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## Certificazione di documenti PDF {#certifying-pdf-documents}

È possibile proteggere un documento PDF certificandolo con un particolare tipo di firma denominato firma certificata. Una firma certificata si distingue da una firma digitale nei seguenti modi:

* Deve essere la prima firma applicata al documento PDF; in altre parole, al momento dell’applicazione della firma certificata, tutti gli altri campi firma del documento devono essere defirmati. In un documento PDF è consentita una sola firma certificata. Se si desidera firmare e certificare un documento PDF, è necessario certificarlo prima di firmarlo. Dopo aver certificato un documento PDF, è possibile firmare digitalmente altri campi firma.
* L&#39;autore o l&#39;autore del documento può specificare che il documento può essere modificato in alcuni modi senza invalidare la firma certificata. Ad esempio, il documento può consentire la compilazione di moduli o commenti. Se l’autore specifica che una determinata modifica non è consentita, Acrobat impedisce agli utenti di modificare il documento in questo modo. Se vengono apportate tali modifiche, ad esempio utilizzando un’altra applicazione, la firma certificata non è valida e Acrobat visualizza un avviso quando un utente apre il documento. Con le firme non certificate, le modifiche non vengono impedite e le normali operazioni di modifica non invalidano la firma originale.
* Al momento della firma, il documento viene analizzato per individuare tipi specifici di contenuto che potrebbero rendere il contenuto di un documento ambiguo o fuorviante. Ad esempio, un’annotazione potrebbe nascondere del testo in una pagina importante per comprendere cosa viene certificato. Una spiegazione (attestato legale) può essere fornita su tale contenuto.

È possibile certificare i documenti PDF a livello di programmazione utilizzando l’API Java del servizio Firma o l’API del servizio Web Firma. Quando si certifica un documento PDF, è necessario fare riferimento a una credenziale di protezione esistente nel servizio Credenziali. Per informazioni sulle credenziali di protezione, consulta la guida *Installazione e distribuzione di AEM Forms* per il server delle applicazioni.

>[!NOTE]
>
>Durante la certificazione e la firma dello stesso documento PDF, se la firma di certificazione non è attendibile, viene visualizzato un triangolo giallo accanto alla prima firma all’apertura del documento PDF in Acrobat o Adobe Reader. La firma di certificazione deve essere ritenuta attendibile per evitare questa situazione.

>[!NOTE]
>
>Quando si utilizza una credenziale HSM Cipher in Shield per firmare o certificare un documento PDF, la nuova credenziale non può essere utilizzata fino al riavvio del server dell&#39;applicazione J2EE in cui viene distribuito AEM Forms. Tuttavia, è possibile impostare un valore di configurazione, in modo che l&#39;operazione di firma o certificazione funzioni senza riavviare il server dell&#39;applicazione J2EE.

Puoi aggiungere il seguente valore di configurazione nel file cknfastrc, che si trova in /opt/nfast/cknfastrc (o c:\nfast\cknfastrc):

```shell
    CKNFAST_ASSUME_SINGLE_PROCESS=0
```

Dopo aver aggiunto questo valore di configurazione al file cknfastrc, è possibile utilizzare la nuova credenziale senza riavviare il server dell&#39;applicazione J2EE.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Firma e sulla certificazione di un documento, vedere [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-5}

Per certificare un documento PDF, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Creare un client di firma.
1. Ottenere il documento PDF da certificare.
1. Certifica il documento PDF.
1. Salvare il documento PDF certificato come file PDF.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è distribuito su JBoss)
* jbossall-client.jar (richiesto se AEM Forms è distribuito su JBoss)

Per informazioni sulla posizione di questi file JAR, consulta [Inclusione dei file della libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un client di firma**

Prima di poter eseguire un’operazione Firma a livello di programmazione, è necessario creare un client Signature.

**Ottenere il documento PDF da certificare**

Per certificare un documento PDF, è necessario ottenere un documento PDF contenente un campo firma. Se un documento PDF non contiene un campo firma, non può essere certificato. È possibile aggiungere un campo firma utilizzando Designer o a livello di programmazione. Per informazioni sull&#39;aggiunta programmatica di un campo firma, vedere [Aggiunta di campi firma](digitally-signing-certifying-documents.md#adding-signature-fields).

**Certifica il documento PDF**

Per certificare correttamente un documento PDF, è necessario immettere i seguenti valori utilizzati dal servizio Firma per certificare un documento PDF:

* **Documento** PDF: Documento PDF contenente un campo firma, ovvero un campo modulo contenente una rappresentazione grafica della firma certificata. Per poter essere certificato, un documento PDF deve contenere un campo firma. È possibile aggiungere un campo firma utilizzando Designer o a livello di programmazione. (Vedere [Aggiunta di campi firma](digitally-signing-certifying-documents.md#adding-signature-fields).)
* **Nome** campo firma: Nome completo del campo firma certificato. Il seguente valore è un esempio: `form1[0].#subform[1].SignatureField3[3]`. Quando si utilizza un campo modulo XFA, è possibile utilizzare anche il nome parziale del campo firma: `SignatureField3[3]`. Se per il nome del campo viene passato un valore nullo, viene creato e certificato in modo dinamico un campo firma invisibile.
* **Credenziali** di protezione: Credenziale utilizzata per certificare il documento PDF. Questa credenziale di sicurezza contiene una password e un alias, che devono corrispondere a un alias visualizzato nella credenziale che si trova all&#39;interno del servizio Credenziali. L’alias è un riferimento a una credenziale effettiva che può trovarsi in un file PKCS#12 (con estensione .pfx) o in un modulo di protezione hardware (HSM).
* **Algoritmo** hash: Algoritmo hash da utilizzare per digest del documento PDF.
* **Motivo della firma**: Un valore visualizzato in Acrobat o Adobe Reader in modo che altri utenti siano a conoscenza del motivo per cui il documento PDF è stato certificato.
* **Posizione del firmatario**: Posizione del firmatario specificata dalla credenziale.
* **Informazioni** di contatto: Informazioni di contatto del firmatario, ad esempio indirizzo e numero di telefono.
* **Informazioni sulle** autorizzazioni: Autorizzazioni che controllano le azioni che un utente finale può eseguire su un documento senza che la firma certificata risulti non valida. Ad esempio, è possibile impostare l’autorizzazione in modo che qualsiasi modifica apportata al documento PDF renda la firma certificata non valida.
* **Spiegazione** legale: Quando un documento viene certificato, viene automaticamente analizzato per specifici tipi di contenuto che potrebbero rendere il contenuto di un documento ambiguo o fuorviante. Ad esempio, un’annotazione potrebbe nascondere del testo in una pagina importante per comprendere cosa viene certificato. Il processo di scansione genera avvisi su questi tipi di contenuto. Questo valore fornisce un’ulteriore spiegazione del contenuto che potrebbe aver generato avvisi.
* **Opzioni** di aspetto: Opzioni che controllano l’aspetto della firma certificata. Ad esempio, la firma certificata può visualizzare informazioni sulla data.
* **Controllo** di revoca: Questo valore specifica se il controllo di revoca viene eseguito per il certificato del firmatario. L&#39;impostazione predefinita di `false` indica che il controllo di revoca non viene eseguito.
* **Impostazioni** OCSP: Impostazioni per il supporto del protocollo OCSP (Online Certificate Status Protocol), che fornisce informazioni sullo stato delle credenziali utilizzate per certificare il documento PDF. Ad esempio, è possibile specificare l’URL del server che fornisce informazioni sulle credenziali utilizzate per accedere al documento PDF.
* **Impostazioni** CRL: Impostazioni delle preferenze dell&#39;elenco di revoche dei certificati (CRL) se si esegue il controllo di revoca. Ad esempio, è possibile specificare di verificare sempre se una credenziale è stata revocata.
* **Timestamp**: Impostazioni che definiscono le informazioni di marca temporale applicate alla firma certificata. Una marca temporale indica che dati specifici sono stati stabiliti prima di un certo periodo di tempo. Questa conoscenza aiuta a creare un rapporto di fiducia tra il firmatario e il verificatore.

**Salvare il documento PDF certificato come file PDF**

Dopo che il servizio Firma ha certificato il documento PDF, è possibile salvarlo come file PDF in modo che gli utenti possano aprirlo in Acrobat o Adobe Reader.

**Consulta anche**

[Certificare i documenti PDF utilizzando l’API Java](digitally-signing-certifying-documents.md#certify-pdf-documents-using-the-java-api)

[Certificare i documenti PDF utilizzando l’API del servizio Web](digitally-signing-certifying-documents.md#certify-pdf-documents-using-the-web-service-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Aggiunta di campi firma](digitally-signing-certifying-documents.md#adding-signature-fields)

### Certificare i documenti PDF utilizzando l&#39;API Java {#certify-pdf-documents-using-the-java-api}

Certifica un documento PDF utilizzando l’API Firma (Java):

1. Includi file di progetto

   Includi file JAR client, ad esempio adobe-signatures-client.jar, nel percorso di classe del progetto Java.

1. Creare un client di firma

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `SignatureServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Ottenere il documento PDF da certificare

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento PDF da certificare utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del documento PDF.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Certifica il documento PDF

   Certificare il documento PDF richiamando il metodo `certify` dell&#39;oggetto `SignatureServiceClient` e passando i seguenti valori:

   * L&#39;oggetto `com.adobe.idp.Document` che rappresenta il documento PDF da certificare.
   * Valore stringa che rappresenta il nome del campo firma che conterrà la firma.
   * Un oggetto `Credential` che rappresenta la credenziale utilizzata per certificare il documento PDF. Creare un oggetto `Credential` richiamando il metodo statico `Credential` dell&#39;oggetto e passando un valore di stringa che specifica il valore di alias corrispondente alla credenziale di sicurezza.`getInstance`
   * Oggetto `HashAlgorithm` che specifica un membro di dati statico che rappresenta l’algoritmo hash utilizzato per digest del documento PDF. Ad esempio, puoi specificare `HashAlgorithm.SHA1` per utilizzare l’algoritmo SHA1.
   * Valore stringa che rappresenta il motivo per cui il documento PDF è stato certificato.
   * Valore stringa che rappresenta le informazioni di contatto del firmatario.
   * Oggetto `MDPPermissions` che specifica le azioni che è possibile eseguire sul documento PDF che invalida la firma.
   * Oggetto `PDFSignatureAppearanceOptions` che controlla l&#39;aspetto della firma certificata. Se lo desideri, modifica l’aspetto della firma richiamando un metodo, ad esempio `setShowDate`.
   * Valore stringa che fornisce una spiegazione delle azioni che invalidano la firma.
   * Un oggetto `java.lang.Boolean` che specifica se eseguire il controllo di revoca sul certificato del firmatario. Se il controllo di revoca viene eseguito, viene incorporato nella firma. Il valore predefinito è `false`.
   * Un oggetto `java.lang.Boolean` che specifica se il campo firma certificato è bloccato. Se il campo è bloccato, il campo firma è contrassegnato come di sola lettura, le relative proprietà non possono essere modificate e non può essere cancellato da un utente che non dispone delle autorizzazioni necessarie. Il valore predefinito è `false`.
   * Un oggetto `OCSPPreferences` che memorizza le preferenze per il supporto del protocollo OCSP (Online Certificate Status Protocol). Se il controllo di revoca non viene eseguito, questo parametro non viene utilizzato ed è possibile specificare `null`. Per informazioni su questo oggetto, consultare [Riferimento API AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * Un oggetto `CRLPreferences` che memorizza le preferenze dell’elenco di revoche di certificati (CRL). Se il controllo di revoca non viene eseguito, questo parametro non viene utilizzato ed è possibile specificare `null`.
   * Un oggetto `TSPPreferences` che memorizza le preferenze per il supporto del provider di timestamp (TSP). Ad esempio, dopo aver creato un oggetto `TSPPreferences`, è possibile impostare l’URL del server TSP richiamando il metodo `TSPPreferences` dell’oggetto `setTspServerURL`. Questo parametro è facoltativo e può essere `null`. Per ulteriori informazioni, consulta [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

   Il metodo `certify` restituisce un oggetto `com.adobe.idp.Document` che rappresenta il documento PDF certificato.

1. Salvare il documento PDF certificato come file PDF

   * Crea un oggetto `java.io.File` e assicurati che l&#39;estensione del file sia .pdf.
   * Richiamare il metodo `copyToFile` dell&#39;oggetto `com.adobe.idp.Document` per copiare nel file il contenuto dell&#39;oggetto `com.adobe.idp.Document`.

**Consulta anche**

[Certificazione dei documenti PDF](digitally-signing-certifying-documents.md#certifying-pdf-documents)

[Avvio rapido (modalità SOAP): Certificazione di un documento PDF tramite l’API Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-certifying-a-pdf-document-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Certificare i documenti PDF utilizzando l&#39;API del servizio Web {#certify-pdf-documents-using-the-web-service-api}

Certifica un documento PDF utilizzando l’API Signature (servizio Web):

1. Includi file di progetto

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurati di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Creare un client di firma

   * Creare un oggetto `SignatureServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `SignatureServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/SignatureService?WSDL`). Non è necessario utilizzare l&#39;attributo `lc_version` . Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Crea un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `SignatureServiceClient.Endpoint.Binding` . Imposta il valore restituito su `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegna il nome utente del modulo di AEM al campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore della password corrispondente al campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Ottenere il documento PDF da certificare

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare un documento PDF certificato.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF da certificare e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni dell&#39;array di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare l’array di byte con i dati del flusso richiamando il metodo `Read` dell’oggetto `System.IO.FileStream` e passando l’array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando al relativo membro dati `MTOM` il contenuto dell&#39;array di byte.

1. Certifica il documento PDF

   Certificare il documento PDF richiamando il metodo `certify` dell&#39;oggetto `SignatureServiceClient` e passando i seguenti valori:

   * L&#39;oggetto `BLOB` che rappresenta il documento PDF da certificare.
   * Valore stringa che rappresenta il nome del campo firma che conterrà la firma.
   * Un oggetto `Credential` che rappresenta la credenziale utilizzata per certificare il documento PDF. Creare un oggetto `Credential` utilizzando il relativo costruttore e specificare l&#39;alias assegnando un valore alla proprietà `Credential` dell&#39;oggetto `alias`.
   * Oggetto `HashAlgorithm` che specifica un membro di dati statico che rappresenta l’algoritmo hash utilizzato per digest del documento PDF. Ad esempio, puoi specificare `HashAlgorithm.SHA1` per utilizzare l’algoritmo SHA1.
   * Un valore booleano che specifica se viene utilizzato l&#39;algoritmo hash.
   * Valore stringa che rappresenta il motivo per cui il documento PDF è stato certificato.
   * Valore stringa che rappresenta la posizione del firmatario.
   * Valore stringa che rappresenta le informazioni di contatto del firmatario.
   * Membro di dati statico dell’oggetto `MDPPermissions` che specifica le azioni che è possibile eseguire sul documento PDF che ne invalida la firma.
   * Un valore booleano che specifica se utilizzare l&#39;oggetto `MDPPermissions` passato come valore del parametro precedente.
   * Valore stringa che spiega le azioni che invalidano la firma.
   * Oggetto `PDFSignatureAppearanceOptions` che controlla l&#39;aspetto della firma certificata. Creare un oggetto `PDFSignatureAppearanceOptions` utilizzando il relativo costruttore. È possibile modificare l’aspetto della firma impostando uno dei relativi membri dati.
   * Un oggetto `System.Boolean` che specifica se eseguire il controllo di revoca sul certificato del firmatario. Se il controllo di revoca viene eseguito, viene incorporato nella firma. Il valore predefinito è `false`.
   * Un oggetto `System.Boolean` che specifica se il campo firma certificato è bloccato. Se il campo è bloccato, il campo firma è contrassegnato come di sola lettura, le relative proprietà non possono essere modificate e non può essere cancellato da un utente che non dispone delle autorizzazioni necessarie. Il valore predefinito è `false`.
   * Un oggetto `System.Boolean` che specifica se il campo firma è bloccato. In altre parole, se passi `true` al parametro precedente, passa `true` a questo parametro.
   * Oggetto `OCSPPreferences` che memorizza le preferenze per il supporto del protocollo OCSP (Online Certificate Status Protocol), che fornisce informazioni sullo stato delle credenziali utilizzate per certificare il documento PDF. Se il controllo di revoca non viene eseguito, questo parametro non viene utilizzato ed è possibile specificare `null`.
   * Un oggetto `CRLPreferences` che memorizza le preferenze dell’elenco di revoche di certificati (CRL). Se il controllo di revoca non viene eseguito, questo parametro non viene utilizzato ed è possibile specificare `null`.
   * Un oggetto `TSPPreferences` che memorizza le preferenze per il supporto del provider di timestamp (TSP). Ad esempio, dopo aver creato un oggetto `TSPPreferences`, è possibile impostare l’URL del TSP impostando il membro dati `TSPPreferences` dell’oggetto `tspServerURL`. Questo parametro è facoltativo e può essere `null`.

   Il metodo `certify` restituisce un oggetto `BLOB` che rappresenta il documento PDF certificato.

1. Salvare il documento PDF certificato come file PDF

   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF che conterrà il documento PDF certificato e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `BLOB` restituito dal metodo `certify`. Compilare l&#39;array di byte ottenendo il valore del membro dati `BLOB` dell&#39;oggetto `binaryData`.
   * Creare un oggetto `System.IO.BinaryWriter` richiamandone il costruttore e passando l&#39;oggetto `System.IO.FileStream`.
   * Scrivi il contenuto dell’array di byte in un file PDF richiamando il metodo `Write` dell’oggetto `System.IO.BinaryWriter` e passando l’array di byte.

**Consulta anche**

[Certificazione dei documenti PDF](digitally-signing-certifying-documents.md#certifying-pdf-documents)

[Richiamo di AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamo di AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Verifica delle firme digitali {#verifying-digital-signatures}

È possibile verificare le firme digitali per verificare che un documento PDF firmato non sia stato modificato e che la firma digitale sia valida. Quando si verifica una firma digitale, è possibile controllare lo stato della firma e le relative proprietà, ad esempio l’identità del firmatario. Prima di considerare attendibile una firma digitale, è consigliabile verificarla. Quando si verifica una firma digitale, fare riferimento a un documento PDF contenente una firma digitale.

Supponiamo che l’identità del firmatario sia sconosciuta. Quando si apre il documento PDF in Acrobat, un messaggio di avviso segnala che l’identità del firmatario è sconosciuta, come illustrato nella figura seguente.

![vd_vd_verifysig](assets/vd_vd_verifysig.png)

Allo stesso modo, quando si verifica programmaticamente una firma digitale, è possibile determinare lo stato dell’identità del firmatario. Ad esempio, se si verifica la firma digitale nel documento mostrato nell’illustrazione precedente, l’identità del firmatario è sconosciuta.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Signature e sulla verifica delle firme digitali, vedere [Guida di riferimento dei servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-6}

Per verificare una firma digitale, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Creare un client di firma.
1. Ottenere il documento PDF contenente la firma da verificare.
1. Impostare le opzioni di esecuzione PKI.
1. Verificare la firma digitale.
1. Determinare lo stato della firma.
1. Determinare l’identità del firmatario.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, includi i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è distribuito su JBoss)
* jbossall-client.jar (richiesto se AEM Forms è distribuito su JBoss)

Per informazioni sulla posizione di questi file JAR, consulta [Inclusione dei file della libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un client di firma**

Prima di eseguire un’operazione del servizio Firma a livello di programmazione, creare un client del servizio Signature.

**Ottenere il documento PDF contenente la firma da verificare**

Per verificare una firma utilizzata per firmare o certificare digitalmente un documento PDF, ottenere un documento PDF contenente una firma.

**Impostare le opzioni di esecuzione PKI**

Impostare le opzioni di esecuzione PKI che il servizio Firma utilizza per la verifica delle firme in un documento PDF:

* Tempo di verifica
* Controllo della revoca
* Valori di marca temporale

Per impostare queste opzioni, puoi specificare il tempo di verifica. Ad esempio, è possibile selezionare l&#39;ora corrente (l&#39;ora nel computer della convalida), che indica l&#39;ora corrente. Per informazioni sui diversi valori temporali, vedi il valore di enumerazione `VerificationTime` in [Riferimento API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

È inoltre possibile specificare se eseguire il controllo di revoca nell&#39;ambito del processo di verifica. Ad esempio, è possibile eseguire un controllo di revoca per determinare se il certificato è revocato. Per informazioni sulle opzioni di verifica della revoca, vedere il valore di enumerazione `RevocationCheckStyle` in [Riferimento API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

Per eseguire il controllo di revoca su un certificato, specificare un URL per un server dell’elenco di revoche di certificati (CRL) utilizzando un oggetto `CRLOptionSpec`. Tuttavia, se non si specifica un URL per il server CRL, il servizio Firma ottiene l’URL dal certificato.

Invece di utilizzare un server CRL, è possibile utilizzare un server OCSP (Online Certificate Status Protocol) quando si esegue il controllo di revoca. In genere, quando si utilizza un server OCSP anziché un server CRL, il controllo di revoca viene eseguito più rapidamente. (Vedere [Protocollo di stato del certificato online](https://tools.ietf.org/html/rfc2560).)

È possibile impostare l&#39;ordine del server CRL e OCSP utilizzato dal servizio Signature utilizzando Adobe Applications e Services. Ad esempio, se il server OCSP è impostato per primo in Adobe Applications and Services, viene controllato il server OCSP, seguito dal server CRL.

Se non si esegue il controllo di revoca, il servizio Firma non controlla la revoca del certificato. In altre parole, le informazioni sul server CRL e OCSP vengono ignorate.

>[!NOTE]
>
>Puoi sovrascrivere l’URL specificato nel certificato utilizzando un oggetto `CRLOptionSpec` e un oggetto `OCSPOptionSpec`. Ad esempio, per ignorare il server CRL, è possibile richiamare il metodo `setLocalURI` dell’oggetto `CRLOptionSpec`.

Timestamp è il processo di tracciamento dell&#39;ora in cui un documento firmato o certificato è stato modificato. Dopo la firma di un documento, nessuno può modificarlo. L’indicazione dell’ora aiuta a garantire la validità di un documento firmato o certificato. È possibile impostare le opzioni di marca temporale utilizzando un oggetto `TSPOptionSpec`. Ad esempio, puoi specificare l’URL di un server del provider di servizi di marca temporale (TSP).

>[!NOTE]
>
>All&#39;avvio rapido di Java e servizi web, il tempo di verifica è impostato su `VerificationTime.CURRENT_TIME` e il controllo di revoca è impostato su `RevocationCheckStyle.BestEffort`. Poiché non sono specificate informazioni sul server CRL o OCSP, le informazioni sul server vengono ottenute dal certificato.

**Verificare la firma digitale**

Per verificare correttamente una firma, specificare il nome completo del campo firma contenente la firma, ad esempio `form1[0].#subform[1].SignatureField3[3]`. Quando si utilizza un campo modulo XFA, è anche possibile utilizzare il nome parziale del campo firma : `SignatureField3`.

Per impostazione predefinita, il servizio Firma limita a 65 minuti il tempo di firma di un documento dopo il periodo di convalida. Se un utente tenta di verificare una firma al momento attuale e l’ora di firma è successiva all’ora corrente ed è entro 65 minuti, il servizio Firma non crea un errore di verifica.

>[!NOTE]
>
>Per gli altri valori richiesti per la verifica di una firma, consulta [Riferimento API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Determinare lo stato della firma**

Per verificare lo stato della firma digitale, è possibile controllarne lo stato.

**Determinare l’identità del firmatario**

Puoi determinare l’identità del firmatario, che può essere uno dei seguenti valori:

* **Sconosciuto**: Il firmatario è sconosciuto perché non è possibile eseguire la verifica del firmatario.
* **Attendibile**: Questo firmatario è affidabile.
* **Non attendibile**: Il firmatario non è attendibile.

**Consulta anche**

[Verificare le firme digitali tramite l’API Java](#verify-digital-signatures-using-the-java-api)

[Verifica delle firme digitali tramite l’API del servizio Web](#verify-digital-signatures-using-the-web-service-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Verifica delle firme digitali tramite l’API Java {#verify-digital-signatures-using-the-java-api}

Verificare la firma digitale utilizzando l’API Servizio firme (Java):

1. Includi file di progetto

   Includi file JAR client, ad esempio adobe-signatures-client.jar, nel percorso di classe del progetto Java.

1. Creare un client di firma

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `SignatureServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Ottenere il documento PDF contenente la firma da verificare

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento PDF contenente la firma da verificare utilizzando il relativo costruttore. Passa un valore stringa che specifica la posizione del documento PDF.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Impostare le opzioni di esecuzione PKI

   * Creare un oggetto `PKIOptions` utilizzando il relativo costruttore.
   * Impostare il tempo di verifica richiamando il metodo `setVerificationTime` dell&#39;oggetto `PKIOptions` e passando un valore di enumerazione `VerificationTime` che specifica il tempo di verifica.
   * Impostare l&#39;opzione di verifica della revoca richiamando il metodo `setRevocationCheckStyle` dell&#39;oggetto `PKIOptions` e passando un valore di enumerazione `RevocationCheckStyle` che specifica se eseguire il controllo della revoca.

1. Verificare la firma digitale

   Verificare la firma richiamando il metodo `verify2` dell&#39;oggetto `SignatureServiceClient` e passando i seguenti valori:

   * Oggetto `com.adobe.idp.Document` contenente un documento PDF firmato o certificato digitalmente.
   * Valore stringa che rappresenta il nome del campo firma contenente la firma da verificare.
   * Un oggetto `PKIOptions` contenente opzioni di esecuzione PKI.
   * Un&#39;istanza `VerifySPIOptions` che contiene informazioni SPI. Puoi specificare `null` per questo parametro.

   Il metodo `verify2` restituisce un oggetto `PDFSignatureVerificationInfo` contenente informazioni che possono essere utilizzate per verificare la firma digitale.

1. Determinare lo stato della firma

   * Determinare lo stato della firma richiamando il metodo `getStatus` dell’oggetto `PDFSignatureVerificationInfo`. Questo metodo restituisce un oggetto `SignatureStatus` che specifica lo stato della firma. Ad esempio, se un documento PDF firmato non viene modificato, questo metodo restituisce `SignatureStatus.DocumentSigNoChanges`.

1. Determinare l’identità del firmatario

   * Determina l’identità del firmatario richiamando il metodo `getSigner` dell’oggetto `PDFSignatureVerificationInfo` . Questo metodo restituisce un oggetto `IdentityInformation`.
   * Richiama il metodo `getStatus` dell&#39;oggetto `IdentityInformation` per determinare l&#39;identità del firmatario. Questo metodo restituisce un valore di enumerazione `IdentityStatus` che specifica l&#39;identità. Ad esempio, se il firmatario è attendibile, questo metodo restituisce `IdentityStatus.TRUSTED`.

**Consulta anche**

[Verifica delle firme digitali](#verify-digital-signatures-using-the-java-api)

[Avvio rapido (modalità SOAP): Verifica di una firma digitale tramite l’API Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-verifying-a-digital-signature-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Verifica delle firme digitali tramite l’API del servizio Web {#verify-digital-signatures-using-the-web-service-api}

Verificare la firma digitale utilizzando l’API Servizio firme (servizio Web):

1. Includi file di progetto

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurati di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Creare un client di firma

   * Creare un oggetto `SignatureServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `SignatureServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/SignatureService?WSDL`). Non è necessario utilizzare l&#39;attributo `lc_version` . Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Crea un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `SignatureServiceClient.Endpoint.Binding` . Imposta il valore restituito su `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegna il nome utente del modulo di AEM al campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore della password corrispondente al campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Ottenere il documento PDF contenente la firma da verificare

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare un documento PDF contenente una firma digitale o certificata da verificare.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore. Passare un valore di stringa che rappresenta la posizione del file del documento PDF firmato e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni dell&#39;array di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare l’array di byte con i dati del flusso richiamando il metodo `Read` dell’oggetto `System.IO.FileStream`. Passa la matrice dei byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando alla relativa proprietà `MTOM` il contenuto dell&#39;array di byte.

1. Impostare le opzioni di esecuzione PKI

   * Creare un oggetto `PKIOptions` utilizzando il relativo costruttore.
   * Impostare il tempo di verifica assegnando al membro dati `verificationTime` dell&#39;oggetto `VerificationTime` un valore di enumerazione `PKIOptions` che specifica il tempo di verifica.
   * Impostare l&#39;opzione di verifica della revoca assegnando al membro dati `revocationCheckStyle` dell&#39;oggetto `RevocationCheckStyle` un valore di enumerazione `PKIOptions` che specifica se eseguire il controllo della revoca.

1. Verificare la firma digitale

   Verificare la firma richiamando il metodo `verify2` dell&#39;oggetto `SignatureServiceClient` e passando i seguenti valori:

   * L&#39;oggetto `BLOB` che contiene un documento PDF firmato o certificato digitalmente.
   * Valore stringa che rappresenta il nome del campo firma contenente la firma da verificare.
   * Un oggetto `PKIOptions` contenente opzioni di esecuzione PKI.
   * Un&#39;istanza `VerifySPIOptions` che contiene informazioni SPI. Puoi specificare `null` per questo parametro.

   Il metodo `verify2` restituisce un oggetto `PDFSignatureVerificationInfo` contenente informazioni che possono essere utilizzate per verificare la firma digitale.

1. Determinare lo stato della firma

   Determinare lo stato della firma ottenendo il valore del membro dati `PDFSignatureVerificationInfo` dell’oggetto `status`. Questo membro dati memorizza un oggetto `SignatureStatus` che specifica lo stato della firma. Ad esempio, se un documento PDF firmato viene modificato, il membro dati `status` memorizza il valore `SignatureStatus.DocumentSigNoChanges`.

1. Determinare l’identità del firmatario

   * Determinare l’identità del firmatario recuperando il valore del membro dati `PDFSignatureVerificationInfo` dell’oggetto `signer`. Questo membro restituisce un oggetto `IdentityInformation`.
   * Recupera il membro dati `status` dell’oggetto `IdentityInformation` per determinare l’identità del firmatario. Questo membro dati restituisce un valore di enumerazione `IdentityStatus` che specifica l&#39;identità. Ad esempio, se il firmatario è attendibile, questo membro restituisce `IdentityStatus.TRUSTED`.

**Consulta anche**

[Verifica delle firme digitali](#verify-digital-signatures-using-the-java-api)

[Richiamo di AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamo di AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Verifica di più firme digitali {#verifying-multiple-digital-signatures}

AEM Forms consente di verificare tutte le firme digitali presenti in un documento PDF. Si supponga che un documento PDF contenga più firme digitali come risultato di un processo aziendale che richiede la firma di più firmatari. Ad esempio, considera una transazione finanziaria che richiede sia la firma di un funzionario del prestito che di un responsabile. È possibile utilizzare l’API Java del servizio Firma o l’API del servizio Web per verificare tutte le firme presenti nel documento PDF. Quando si verificano più firme digitali, è possibile controllare lo stato e le proprietà di ciascuna firma. Prima di considerare attendibile una firma digitale, è consigliabile verificarla. Si consiglia di verificare una firma digitale unica.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Signature e sulla verifica delle firme digitali, vedere [Guida di riferimento dei servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-7}

Per verificare più firme digitali, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Creare un client di firma.
1. Ottenere il documento PDF contenente le firme da verificare.
1. Impostare le opzioni di esecuzione PKI.
1. Recupera tutte le firme digitali.
1. Itera tutte le firme.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, includi i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è distribuito su JBoss)
* jbossall-client.jar (richiesto se AEM Forms è distribuito su JBoss)

Per informazioni sulla posizione di questi file JAR, consulta [Inclusione dei file della libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un client di firma**

Prima di eseguire un’operazione del servizio Firma a livello di programmazione, creare un client del servizio Signature.

**Ottenere il documento PDF contenente le firme da verificare**

Per verificare una firma utilizzata per firmare o certificare digitalmente un documento PDF, ottenere un documento PDF contenente una firma.

**Impostare le opzioni di runtime PKI**

Impostare le opzioni di esecuzione PKI che il servizio Firma utilizza per verificare tutte le firme presenti in un documento PDF:

* Tempo di verifica
* Controllo della revoca
* Valori di marca temporale

Per impostare queste opzioni, puoi specificare il tempo di verifica. Ad esempio, è possibile selezionare l&#39;ora corrente (l&#39;ora nel computer della convalida), che indica l&#39;ora corrente. Per informazioni sui diversi valori temporali, vedi il valore di enumerazione `VerificationTime` in [Riferimento API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

È inoltre possibile specificare se eseguire il controllo di revoca nell&#39;ambito del processo di verifica. Ad esempio, è possibile eseguire un controllo di revoca per determinare se il certificato è revocato. Per informazioni sulle opzioni di verifica della revoca, vedere il valore di enumerazione `RevocationCheckStyle` in [Riferimento API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

Per eseguire il controllo di revoca su un certificato, specificare un URL per un server dell’elenco di revoche di certificati (CRL) utilizzando un oggetto `CRLOptionSpec`. Tuttavia, se non si specifica un URL per un server CRL, il servizio Firma ottiene l’URL dal certificato.

Invece di utilizzare un server CRL, è possibile utilizzare un server OCSP (Online Certificate Status Protocol) quando si esegue il controllo di revoca. In genere, quando si utilizza un server OCSP invece di un server CRL, il controllo di revoca viene eseguito più rapidamente. (Vedere [Protocollo di stato del certificato online](https://tools.ietf.org/html/rfc2560).)

È possibile impostare l&#39;ordine del server CRL e OCSP utilizzato dal servizio Signature utilizzando Adobe Applications e Services. Ad esempio, se il server OCSP è impostato per primo in Adobe Applications and Services, il server OCSP viene controllato, seguito dal server CRL.

Se non si esegue il controllo di revoca, il servizio Firma non controlla la revoca del certificato. In altre parole, le informazioni sul server CRL e OCSP vengono ignorate.

>[!NOTE]
>
>Puoi sovrascrivere l’URL specificato nel certificato utilizzando un oggetto `CRLOptionSpec` e un oggetto `OCSPOptionSpec`. Ad esempio, per ignorare il server CRL, è possibile richiamare il metodo `setLocalURI` dell’oggetto `CRLOptionSpec`.

Timestamp è il processo di tracciamento dell&#39;ora in cui un documento firmato o certificato è stato modificato. Dopo la firma di un documento, nessuno può modificarlo. L’indicazione dell’ora aiuta a garantire la validità di un documento firmato o certificato. È possibile impostare le opzioni di marca temporale utilizzando un oggetto `TSPOptionSpec`. Ad esempio, puoi specificare l’URL di un server del provider di servizi di marca temporale (TSP).

>[!NOTE]
>
>All&#39;avvio rapido di Java e servizi web, il tempo di verifica è impostato su `VerificationTime.CURRENT_TIME` e il controllo di revoca è impostato su `RevocationCheckStyle.BestEffort`. Poiché non sono specificate informazioni sul server CRL o OCSP, le informazioni sul server vengono ottenute dal certificato.

**Recupera tutte le firme digitali**

Per verificare tutte le firme digitali presenti in un documento PDF, recuperare le firme digitali dal documento PDF. Tutte le firme vengono restituite in un elenco. Per verificare una firma digitale, controllare lo stato della firma.

>[!NOTE]
>
>A differenza di quando si verifica una singola firma digitale, quando si verificano più firme, non è necessario specificare il nome del campo firma.

**Itera attraverso tutte le firme**

Itera attraverso ogni firma. In altre parole, per ogni firma, verifica la firma digitale e controlla l’identità del firmatario e lo stato di ciascuna firma. (Consultare [Verifica delle firme digitali](#verify-digital-signatures-using-the-java-api).)

>[!NOTE]
>
>Non è necessario eseguire iterazioni su tutte le firme se il requisito è l&#39;intero documento.

**Consulta anche**

[Verifica di più firme digitali tramite l’API Java](#verify-digital-signatures-using-the-java-api)

[Verifica di più firme digitali tramite l’API del servizio Web](#verify-digital-signatures-using-the-web-service-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Verificare più firme digitali utilizzando l&#39;API Java {#verify-multiple-digital-signatures-using-the-java-api}

Verificare più firme digitali utilizzando l’API Servizio firme (Java):

1. Includi file di progetto

   Includi file JAR client, ad esempio adobe-signatures-client.jar, nel percorso di classe del progetto Java.

1. Creare un client di firma

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `SignatureServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Ottenere il documento PDF contenente le firme da verificare

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento PDF contenente più firme digitali da verificare utilizzando il relativo costruttore. Passa un valore stringa che specifica la posizione del documento PDF.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Impostare le opzioni di runtime PKI

   * Creare un oggetto `PKIOptions` utilizzando il relativo costruttore.
   * Impostare il tempo di verifica richiamando il metodo `setVerificationTime` dell&#39;oggetto `PKIOptions` e passando un valore di enumerazione `VerificationTime` che specifica il tempo di verifica.
   * Impostare l&#39;opzione di controllo della revoca richiamando il metodo `setRevocationCheckStyle` dell&#39;oggetto `RevocationCheckStyle` e passando un valore di enumerazione `PKIOptions` che specifica se eseguire il controllo della revoca.

1. Recupera tutte le firme digitali

   Richiama il metodo `verifyPDFDocument` dell&#39;oggetto `SignatureServiceClient` e passa i seguenti valori:

   * Oggetto `com.adobe.idp.Document` contenente un documento PDF contenente più firme digitali.
   * Un oggetto `PKIOptions` contenente opzioni di esecuzione PKI.
   * Un&#39;istanza `VerifySPIOptions` che contiene informazioni SPI. Puoi specificare `null` per questo parametro.

   Il metodo `verifyPDFDocument` restituisce un oggetto `PDFDocumentVerificationInfo` contenente informazioni su tutte le firme digitali presenti nel documento PDF.

1. Itera attraverso tutte le firme

   * Itera tutte le firme richiamando il metodo `getVerificationInfos` dell&#39;oggetto `PDFDocumentVerificationInfo`. Questo metodo restituisce un oggetto `java.util.List` in cui ogni elemento è un oggetto `PDFSignatureVerificationInfo`. Utilizzare un oggetto `java.util.Iterator` per eseguire iterazioni nell&#39;elenco di firme.
   * Utilizzando l’oggetto `PDFSignatureVerificationInfo` è possibile eseguire attività quali determinare lo stato della firma richiamando il metodo `PDFSignatureVerificationInfo` dell’oggetto `getStatus`. Questo metodo restituisce un oggetto `SignatureStatus` il cui membro dati statico informa l&#39;utente dello stato della firma. Ad esempio, se la firma è sconosciuta, questo metodo restituisce `SignatureStatus.DocumentSignatureUnknown`.

**Consulta anche**

[Verifica di più firme digitali](#verifying-multiple-digital-signatures)

[Avvio rapido (modalità SOAP): Verifica di più firme digitali tramite l’API Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-verifying-multiple-digital-signatures-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Verifica delle firme digitali](#verify-digital-signatures-using-the-java-api)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Verifica di più firme digitali tramite l’API del servizio Web {#verifying-multiple-digital-signatures-using-the-web-service-api}

Verificare più firme digitali utilizzando l’API Servizio firme (servizio Web):

1. Includi file di progetto

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurati di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Creare un client di firma

   * Creare un oggetto `SignatureServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `SignatureServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/SignatureService?WSDL`). Non è necessario utilizzare l&#39;attributo `lc_version` . Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Crea un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `SignatureServiceClient.Endpoint.Binding` . Imposta il valore restituito su `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegna il nome utente del modulo di AEM al campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore della password corrispondente al campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Ottenere il documento PDF contenente le firme da verificare

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` memorizza un documento PDF contenente più firme digitali da verificare.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore. Passare un valore di stringa che rappresenta la posizione del file del documento PDF e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni dell&#39;array di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare l’array di byte con i dati del flusso richiamando il metodo `Read` dell’oggetto `System.IO.FileStream`. Passa la matrice dei byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando alla relativa proprietà `MTOM` il contenuto dell&#39;array di byte.

1. Impostare le opzioni di runtime PKI

   * Creare un oggetto `PKIOptions` utilizzando il relativo costruttore.
   * Impostare il tempo di verifica assegnando al membro dati `verificationTime` dell&#39;oggetto `VerificationTime` un valore di enumerazione `PKIOptions` che specifica il tempo di verifica.
   * Impostare l&#39;opzione di controllo di revoca assegnando al membro dati `revocationCheckStyle` dell&#39;oggetto `RevocationCheckStyle` un valore di enumerazione `PKIOptions` che specifica se eseguire il controllo di revoca.

1. Recupera tutte le firme digitali

   Richiama il metodo `verifyPDFDocument` dell&#39;oggetto `SignatureServiceClient` e passa i seguenti valori:

   * Oggetto `BLOB` contenente un documento PDF contenente più firme digitali.
   * Un oggetto `PKIOptions` contenente opzioni di esecuzione PKI.
   * Un&#39;istanza `VerifySPIOptions` che contiene informazioni SPI. È possibile specificare null per questo parametro.

   Il metodo `verifyPDFDocument` restituisce un oggetto `PDFDocumentVerificationInfo` contenente informazioni su tutte le firme digitali presenti nel documento PDF.

1. Itera attraverso tutte le firme

   * Itera tutte le firme ottenendo il membro dati `verificationInfos` dell&#39;oggetto `PDFDocumentVerificationInfo`. Questo membro dati restituisce un array `Object` in cui ogni elemento è un oggetto `PDFSignatureVerificationInfo`.
   * Utilizzando l’oggetto `PDFSignatureVerificationInfo` è possibile eseguire attività quali determinare lo stato della firma ottenendo il membro dati `PDFSignatureVerificationInfo` dell’oggetto `status`. Questo membro dati restituisce un oggetto `SignatureStatus` il cui membro dati statico ti informa sullo stato della firma. Ad esempio, se la firma è sconosciuta, questo metodo restituisce `SignatureStatus.DocumentSignatureUnknown`.

**Consulta anche**

[Verifica di più firme digitali](#verifying-multiple-digital-signatures)

[Richiamo di AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamo di AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Rimozione di firme digitali {#removing-digital-signatures}

È necessario rimuovere le firme digitali da un campo firma prima di poter applicare una firma digitale più recente. Impossibile sovrascrivere una firma digitale. Se si tenta di applicare una firma digitale a un campo firma contenente una firma, si verifica un&#39;eccezione.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Signature, vedere [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-8}

Per rimuovere una firma digitale da un campo firma, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Creare un client di firma.
1. Ottenere il documento PDF contenente una firma da rimuovere.
1. Rimuovere la firma digitale dal campo firma.
1. Salvare il documento PDF come file PDF.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è distribuito su JBoss)
* jbossall-client.jar (richiesto se AEM Forms è distribuito su JBoss)

Per informazioni sulla posizione di questi file JAR, consulta [Inclusione dei file della libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un client di firma**

Prima di poter eseguire un’operazione del servizio Firma a livello di programmazione, è necessario creare un client del servizio Signature.

**Ottenere il documento PDF contenente una firma da rimuovere**

Per rimuovere una firma da un documento PDF, è necessario ottenere un documento PDF contenente una firma.

**Rimuovere la firma digitale dal campo firma**

Per rimuovere correttamente una firma digitale da un documento PDF, è necessario specificare il nome del campo firma contenente la firma digitale. Inoltre, è necessario disporre dell&#39;autorizzazione per rimuovere la firma digitale; in caso contrario, si verifica un&#39;eccezione.

**Salvare il documento PDF come file PDF**

Dopo che il servizio Firma rimuove una firma digitale da un campo firma, è possibile salvare il documento PDF come file PDF in modo che gli utenti possano aprirlo in Acrobat o Adobe Reader.

**Consulta anche**

[Rimuovere le firme digitali tramite l’API Java](digitally-signing-certifying-documents.md#remove-digital-signatures-using-the-java-api)

[Rimuovere le firme digitali tramite l’API del servizio Web](digitally-signing-certifying-documents.md#remove-digital-signatures-using-the-web-service-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Aggiunta di campi firma](digitally-signing-certifying-documents.md#adding-signature-fields)

### Rimuovere le firme digitali utilizzando l&#39;API Java {#remove-digital-signatures-using-the-java-api}

Rimuovere una firma digitale utilizzando l’API Firma (Java):

1. Includi file di progetto

   Includi file JAR client, ad esempio adobe-signatures-client.jar, nel percorso di classe del progetto Java.

1. Creare un client di firma.

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `SignatureServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Ottenere il documento PDF contenente una firma da rimuovere

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento PDF contenente la firma da rimuovere utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del documento PDF.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Rimuovere la firma digitale dal campo firma

   Rimuovere una firma digitale da un campo firma richiamando il metodo `clearSignatureField` dell’oggetto `SignatureServiceClient` e passando i seguenti valori:

   * Un oggetto `com.adobe.idp.Document` che rappresenta il documento PDF contenente la firma da rimuovere.
   * Valore stringa che specifica il nome del campo firma contenente la firma digitale.

   Il metodo `clearSignatureField` restituisce un oggetto `com.adobe.idp.Document` che rappresenta il documento PDF da cui è stata rimossa la firma digitale.

1. Salvare il documento PDF come file PDF

   * Crea un oggetto `java.io.File` e assicurati che l&#39;estensione del file sia .pdf.
   * Richiama il metodo `copyToFile` dell&#39;oggetto `com.adobe.idp.Document`. Passa l&#39;oggetto `java.io.File` per copiare il contenuto dell&#39;oggetto `com.adobe.idp.Document` nel file . Assicurarsi di utilizzare l&#39;oggetto `Document` restituito dal metodo `clearSignatureField`.

**Consulta anche**

[Rimozione di firme digitali](digitally-signing-certifying-documents.md#removing-digital-signatures)

[Avvio rapido (modalità SOAP): Rimozione di una firma digitale tramite l’API Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-removing-a-digital-signature-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Rimuovere le firme digitali utilizzando l&#39;API del servizio Web {#remove-digital-signatures-using-the-web-service-api}

Rimuovere una firma digitale utilizzando l’API Signature (servizio Web):

1. Includi file di progetto

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurati di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Creare un client di firma

   * Creare un oggetto `SignatureServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `SignatureServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/SignatureService?WSDL`). Non è necessario utilizzare l&#39;attributo `lc_version` . Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Crea un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `SignatureServiceClient.Endpoint.Binding` . Imposta il valore restituito su `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegna il nome utente del modulo di AEM al campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore della password corrispondente al campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Ottenere il documento PDF contenente una firma da rimuovere

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare un documento PDF contenente una firma digitale da rimuovere.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF firmato e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni dell&#39;array di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare l’array di byte con i dati del flusso richiamando il metodo `Read` dell’oggetto `System.IO.FileStream`. Passa la matrice dei byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando la relativa proprietà `MTOM` con il contenuto dell&#39;array di byte.

1. Rimuovere la firma digitale dal campo firma

   Rimuovere la firma digitale richiamando il metodo `clearSignatureField` dell&#39;oggetto `SignatureServiceClient` e passando i seguenti valori:

   * Oggetto `BLOB` contenente il documento PDF firmato.
   * Valore stringa che rappresenta il nome del campo firma contenente la firma digitale da rimuovere.

   Il metodo `clearSignatureField` restituisce un oggetto `BLOB` che rappresenta il documento PDF da cui è stata rimossa la firma digitale.

1. Salvare il documento PDF come file PDF

   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF contenente un campo firma vuoto e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `BLOB` restituito dal metodo `sign`. Compilare l&#39;array di byte ottenendo il valore del membro dati `BLOB` dell&#39;oggetto `MTOM`.
   * Creare un oggetto `System.IO.BinaryWriter` richiamandone il costruttore e passando l&#39;oggetto `System.IO.FileStream`.
   * Scrivere il contenuto dell’array di byte nel file PDF richiamando il metodo `System.IO.BinaryWriter` dell’oggetto `Write` e passando l’array di byte.

**Consulta anche**

[Rimozione di firme digitali](digitally-signing-certifying-documents.md#removing-digital-signatures)

[Richiamo di AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamo di AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
