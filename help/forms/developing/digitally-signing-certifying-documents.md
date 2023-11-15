---
title: Firma digitale e certificazione dei documenti
description: Utilizzare il servizio Firma per aggiungere ed eliminare campi di firma digitale in un documento PDF, recuperare i nomi dei campi di firma in un documento PDF, modificare i campi di firma, firmare digitalmente i documenti PDF, certificare i documenti PDF, convalidare le firme digitali in un documento PDF, convalidare tutte le firme digitali in un documento PDF e rimuovere una firma digitale da un campo di firma.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: c200f345-40ab-46fd-b6ed-f3af0a23796b
source-git-commit: 7f35fdee9dbca9dfd3992b56579d6d06633f8dec
workflow-type: tm+mt
source-wordcount: '17027'
ht-degree: 0%

---

# Firma digitale e certificazione dei documenti {#digitally-signing-and-certifying-documents}

**Gli esempi e gli esempi contenuti in questo documento sono solo per l’ambiente AEM Forms su JEE.**

**Informazioni sul servizio di firma**

Il servizio di firma consente all&#39;organizzazione di proteggere la sicurezza e la privacy dei documenti Adobe PDF che distribuisce e riceve. Questo servizio utilizza firme digitali e certificazione per garantire che solo i destinatari desiderati possano modificare i documenti. Poiché le funzioni di protezione vengono applicate al documento stesso, quest&#39;ultimo rimane protetto e controllato per l&#39;intero ciclo di vita. Un documento rimane protetto oltre il firewall, quando viene scaricato offline e quando viene inviato di nuovo alla tua organizzazione.

>[!NOTE]
>
>È possibile creare un gestore di firma personalizzato per il servizio di firma che viene richiamato quando vengono richiamate determinate operazioni, ad esempio la firma di un documento PDF.

**Nomi dei campi di firma**

Per alcune operazioni del servizio di firma è necessario specificare il nome del campo firma in cui viene eseguita un&#39;operazione. Quando si firma un documento PDF, ad esempio, si specifica il nome del campo firma da firmare. Si supponga che il nome completo di un campo firma sia `form1[0].Form1[0].SignatureField1[0]`. È possibile specificare `SignatureField1[0]` invece di `form1[0].Form1[0].SignatureField1[0]`.

A volte un conflitto causa la firma del campo errato da parte del servizio di firma (o l&#39;esecuzione di un&#39;altra operazione che richiede il nome del campo della firma). Questo conflitto è il risultato del nome `SignatureField1[0]` in due o più posizioni nello stesso documento PDF. Si consideri ad esempio un documento PDF contenente due campi firma denominati `form1[0].Form1[0].SignatureField1[0]` e `form1[0].Form1[0].SubForm1[0].SignatureField1[0]` e si specifica `SignatureField1[0]`. In questa situazione, il servizio Firma firma il primo campo firma trovato durante l&#39;iterazione di tutti i campi firma del documento.

Se in un documento PDF sono presenti più campi firma, è consigliabile specificare i nomi completi dei campi firma. Ovvero specificare `form1[0].Form1[0].SignatureField1[0]`invece di `SignatureField1[0]`.

È possibile eseguire queste attività utilizzando il servizio di firma:

* Aggiungere ed eliminare campi di firma digitale in un documento PDF. (vedere [Aggiunta di campi firma](digitally-signing-certifying-documents.md#adding-signature-fields).)
* Recuperare i nomi dei campi firma in un documento PDF. (vedere [Recupero dei nomi dei campi firma](digitally-signing-certifying-documents.md#retrieving-signature-field-names).)
* Modificare i campi della firma. (vedere [Modifica dei campi della firma](digitally-signing-certifying-documents.md#modifying-signature-fields).)
* Apporre una firma digitale ai documenti PDF. (vedere [Firma digitale dei documenti di PDF](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents).)
* Certifica i documenti di PDF. (vedere [Certificazione dei documenti di PDF](digitally-signing-certifying-documents.md#certifying-pdf-documents).)
* Convalidare le firme digitali in un documento PDF. (vedere [Verifica delle firme digitali](digitally-signing-certifying-documents.md#verifying-digital-signatures).)
* Convalida tutte le firme digitali in un documento PDF. (vedere [Verifica di più firme digitali](digitally-signing-certifying-documents.md#verifying-digital-signatures).)
* Rimuovere una firma digitale da un campo firma. (vedere [Rimozione di firme digitali](digitally-signing-certifying-documents.md#removing-digital-signatures).)

>[!NOTE]
>
>Per ulteriori informazioni sul servizio di firma, vedere [Guida di riferimento dei servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)..

## Aggiunta di campi firma {#adding-signature-fields}

Le firme digitali vengono visualizzate nei campi firma, ovvero nei campi modulo che contengono una rappresentazione grafica della firma. I campi di firma possono essere visibili o invisibili. I firmatari possono utilizzare un campo di firma preesistente oppure è possibile aggiungere un campo di firma a livello di programmazione. In entrambi i casi, il campo firma deve esistere prima che un documento PDF possa essere firmato.

Puoi aggiungere un campo di firma a livello di programmazione utilizzando l’API Java di Signature Service o l’API del servizio web di firma. È possibile aggiungere più di un campo firma a un documento di PDF; tuttavia, ogni nome di campo firma deve essere univoco.

>[!NOTE]
>
>Alcuni tipi di documenti di PDF non consentono di aggiungere un campo firma a livello di programmazione. Per ulteriori informazioni sul servizio Firma e sull&#39;aggiunta di campi di firma, vedere [Guida di riferimento dei servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary-of-steps}

Per aggiungere un campo firma a un documento PDF, eseguire le attività seguenti:

1. Includi file di progetto.
1. Creare un client di firma.
1. Ottiene un documento PDF a cui viene aggiunto un campo firma.
1. Aggiungi un campo firma.
1. Salvare il documento PDF come file PDF.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è implementato su JBoss)
* jbossall-client.jar (obbligatorio se AEM Forms è distribuito su JBoss)

**Creare un client di firma**

Prima di poter eseguire un&#39;operazione del servizio di firma a livello di programmazione, è necessario creare un client del servizio di firma.

**Ottieni un documento PDF a cui viene aggiunto un campo firma**

È necessario ottenere un documento PDF a cui viene aggiunto un campo firma.

**Aggiungi un campo firma**

Per aggiungere correttamente un campo firma a un documento PDF, è necessario specificare valori di coordinate che identificano la posizione del campo firma. Se si aggiunge un campo firma invisibile, questi valori non sono obbligatori. È inoltre possibile specificare quali campi del documento PDF vengono bloccati dopo l&#39;applicazione di una firma al campo firma.

**Salvare il documento PDF come file PDF**

Dopo che il servizio di firma ha aggiunto un campo firma al documento PDF, è possibile salvare il documento come file PDF in modo che gli utenti possano aprirlo in Acrobat o Adobe Reader.

**Consulta anche**

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Firma digitale dei documenti di PDF](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

### Aggiungere campi di firma utilizzando l’API Java {#add-signature-fields-using-the-java-api}

Aggiungi un campo firma utilizzando Signature API (Java):

1. Includi file di progetto

   Includi i file JAR dei client, ad esempio adobe-signatures-client.jar, nel percorso di classe del progetto Java.

1. Creare un client di firma

   * Creare un `ServiceClientFactory` oggetto che contiene proprietà di connessione.
   * Creare un `SignatureServiceClient` mediante il costruttore e passando il `ServiceClientFactory` oggetto.

1. Ottieni un documento PDF a cui viene aggiunto un campo firma

   * Creare un `java.io.FileInputStream` oggetto che rappresenta il documento PDF al quale viene aggiunto un campo firma utilizzando il relativo costruttore e passando un valore stringa che specifica la posizione del documento PDF.
   * Creare un `com.adobe.idp.Document` mediante il costruttore e passando il `java.io.FileInputStream` oggetto.

1. Aggiungi un campo firma

   * Creare un `PositionRectangle` oggetto che specifica la posizione del campo firma utilizzando il relativo costruttore. All&#39;interno del costruttore, specificate i valori delle coordinate.
   * Se lo desideri, crea un’ `FieldMDPOptions` oggetto che specifica i campi bloccati quando viene applicata una firma digitale al campo firma.
   * Aggiungere un campo firma a un documento PDF richiamando il `SignatureServiceClient` dell&#39;oggetto `addSignatureField` e fornendo i seguenti valori:

      * A `com.adobe.idp`. `Document` oggetto che rappresenta il documento PDF al quale viene aggiunto un campo firma.
      * Valore stringa che specifica il nome del campo della firma.
      * A `java.lang.Integer` valore che rappresenta il numero di pagina a cui viene aggiunto un campo firma.
      * A `PositionRectangle` oggetto che specifica la posizione del campo firma.
      * A `FieldMDPOptions` oggetto che specifica i campi del documento PDF bloccati dopo l&#39;applicazione di una firma digitale al campo firma. Il valore di questo parametro è facoltativo ed è possibile trasmettere `null`.

   * A `PDFSeedValueOptions` oggetto che specifica vari valori di runtime. Il valore di questo parametro è facoltativo ed è possibile trasmettere `null`.

     Il `addSignatureField` il metodo restituisce un `com.adobe.idp`. `Document` oggetto che rappresenta un documento PDF contenente un campo firma.

   >[!NOTE]
   >
   >È possibile richiamare `SignatureServiceClient` dell&#39;oggetto `addInvisibleSignatureField` per aggiungere un campo firma invisibile.

1. Salvare il documento PDF come file PDF

   * Creare un `java.io.File` e assicurarsi che l&#39;estensione del file sia .pdf.
   * Richiama `com.adobe.idp`. `Document` dell&#39;oggetto `copyToFile` metodo per copiare il contenuto del `Document` al file. Assicurati di utilizzare `com.adobe.idp`. `Document` oggetto restituito da `addSignatureField` metodo.

**Consulta anche**

[Avvio rapido API di Signature Service](/help/forms/developing/signature-service-java-api-quick.md#signature-service-java-api-quick-start-soap)

### Aggiungere campi di firma utilizzando l’API del servizio web {#add-signature-fields-using-the-web-service-api}

Per aggiungere un campo di firma utilizzando l’API di firma (servizio web):

1. Includi file di progetto

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l’indirizzo IP del server che ospita AEM Forms.

1. Creare un client di firma

   * Creare un `SignatureServiceClient` utilizzando il costruttore predefinito.
   * Creare un `SignatureServiceClient.Endpoint.Address` oggetto utilizzando `System.ServiceModel.EndpointAddress` costruttore. Passa un valore stringa che specifica il file WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/SignatureService?WSDL`). Non è necessario utilizzare il `lc_version` attributo. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Creare un `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto ottenendo il valore del `SignatureServiceClient.Endpoint.Binding` campo. Invia il valore restituito a `BasicHttpBinding`.
   * Imposta il `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegna al campo il nome utente dei moduli AEM `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore password corrispondente al campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Ottieni un documento PDF a cui viene aggiunto un campo firma

   * Creare un `BLOB` mediante il costruttore. Il `BLOB` L&#39;oggetto viene utilizzato per memorizzare il documento PDF che conterrà un campo di firma.
   * Creare un `System.IO.FileStream` dell&#39;oggetto richiamando il relativo costruttore e passando un valore stringa che rappresenta la posizione del file del documento PDF e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto della `System.IO.FileStream` oggetto. È possibile determinare le dimensioni della matrice di byte ottenendo `System.IO.FileStream` dell&#39;oggetto `Length` proprietà.
   * Compilare la matrice di byte con i dati di flusso richiamando `System.IO.FileStream` dell&#39;oggetto `Read` e passando la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare il `BLOB` oggetto assegnando il relativo `MTOM` con il contenuto della matrice di byte.

1. Aggiungi un campo firma

   Aggiungere un campo firma al documento PDF richiamando il `SignatureServiceClient` dell&#39;oggetto `addSignatureField` e fornendo i seguenti valori:

   * A `BLOB` oggetto che rappresenta il documento PDF al quale viene aggiunto un campo firma.
   * Valore stringa che specifica il nome del campo della firma.
   * Valore intero che rappresenta il numero di pagina a cui viene aggiunto un campo firma.
   * A `PositionRect` oggetto che specifica la posizione del campo firma.
   * A `FieldMDPOptions` oggetto che specifica i campi del documento PDF bloccati dopo l&#39;applicazione di una firma digitale al campo firma. Il valore di questo parametro è facoltativo ed è possibile trasmettere `null`.
   * A `PDFSeedValueOptions` oggetto che specifica vari valori di runtime. Il valore di questo parametro è facoltativo ed è possibile trasmettere `null`.

   Il `addSignatureField` il metodo restituisce un `BLOB` oggetto che rappresenta un documento PDF contenente un campo firma.

1. Salvare il documento PDF come file PDF

   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore stringa che rappresenta la posizione del file del documento PDF che conterrà il campo firma e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto della `BLOB` oggetto restituito da `addSignatureField` metodo. Popolare la matrice di byte ottenendo il valore della `BLOB` dell&#39;oggetto `binaryData` membro dati.
   * Creare un `System.IO.BinaryWriter` oggetto richiamando il relativo costruttore e passando il `System.IO.FileStream` oggetto.
   * Scrivere il contenuto della matrice di byte in un file PDF richiamando `System.IO.BinaryWriter` dell&#39;oggetto `Write` e passando la matrice di byte.

**Consulta anche**

[Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamare AEM Forms con SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Recupero dei nomi dei campi firma {#retrieving-signature-field-names}

È possibile recuperare i nomi di tutti i campi firma presenti in un documento PDF che si desidera firmare o certificare. Se non si è certi dei nomi dei campi firma presenti in un documento PDF o si desidera verificarli, è possibile recuperarli a livello di programmazione. Il servizio di firma restituisce il nome completo del campo della firma, ad esempio `form1[0].grantApplication[0].page1[0].SignatureField1[0]`.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio di firma, vedere [Guida di riferimento dei servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)

### Riepilogo dei passaggi {#summary_of_steps-1}

Per recuperare i nomi dei campi della firma, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Creare un client di firma.
1. Ottiene il documento PDF contenente i campi firma.
1. Recuperare i nomi dei campi firma.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è implementato su JBoss)
* jbossall-client.jar (obbligatorio se AEM Forms è distribuito su JBoss)

Per informazioni sulla posizione di questi file JAR, vedi [Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un client di firma**

Prima di poter eseguire un&#39;operazione del servizio di firma a livello di programmazione, è necessario creare un client del servizio di firma.

**Ottieni il documento PDF contenente i campi firma**

Recuperare un documento PDF contenente campi di firma.

**Recuperare i nomi dei campi firma**

È possibile recuperare i nomi dei campi firma dopo aver recuperato un documento PDF contenente uno o più campi firma.

**Consulta anche**

[Recuperare i nomi dei campi della firma utilizzando l’API Java](digitally-signing-certifying-documents.md#retrieve-signature-field-names-using-the-java-api)

[Recuperare il campo della firma utilizzando l’API del servizio web](digitally-signing-certifying-documents.md#retrieve-signature-field-using-the-web-service-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Aggiunta di campi firma](digitally-signing-certifying-documents.md#adding-signature-fields)

### Recuperare i nomi dei campi della firma utilizzando l’API Java {#retrieve-signature-field-names-using-the-java-api}

Recupera i nomi dei campi della firma utilizzando Signature API (Java):

1. Includi file di progetto

   Includi i file JAR dei client, ad esempio adobe-signatures-client.jar, nel percorso di classe del progetto Java.

1. Creare un client di firma

   * Creare un `ServiceClientFactory` oggetto che contiene proprietà di connessione.
   * Creare un `SignatureServiceClient` mediante il costruttore e passando il `ServiceClientFactory` oggetto.

1. Ottieni il documento PDF contenente i campi firma

   * Creare un `java.io.FileInputStream` oggetto che rappresenta il documento PDF che contiene campi firma mediante il costruttore e che trasmette un valore stringa che specifica la posizione del documento PDF.
   * Creare un `com.adobe.idp.Document` mediante il costruttore e passando il `java.io.FileInputStream` oggetto.

1. Recuperare i nomi dei campi firma

   * Recuperare i nomi dei campi della firma richiamando `SignatureServiceClient` dell&#39;oggetto `getSignatureFieldList` e passando il `com.adobe.idp.Document` oggetto contenente il documento PDF contenente i campi firma. Questo metodo restituisce un `java.util.List` oggetto, in cui ogni elemento contiene un `PDFSignatureField` oggetto. Utilizzando questo oggetto, è possibile ottenere ulteriori informazioni su un campo firma, ad esempio se è visibile o meno.
   * Effettua iterazione attraverso `java.util.List` oggetto per determinare se sono presenti nomi di campi di firma. Per ogni campo di firma nel documento PDF, è possibile ottenere un `PDFSignatureField` oggetto. Per ottenere il nome del campo firma, richiamare `PDFSignatureField` dell&#39;oggetto `getName` metodo. Questo metodo restituisce un valore stringa che specifica il nome del campo della firma.

**Consulta anche**

[Recupero dei nomi dei campi firma](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

[Quick Start (modalità SOAP): recupero dei nomi dei campi della firma tramite l’API Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-retrieving-signature-field-names-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Recuperare il campo della firma utilizzando l’API del servizio web {#retrieve-signature-field-using-the-web-service-api}

Recupera i nomi dei campi della firma utilizzando Signature API (servizio web):

1. Includi file di progetto

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l’indirizzo IP del server che ospita AEM Forms.

1. Creare un client di firma

   * Creare un `SignatureServiceClient` utilizzando il costruttore predefinito.
   * Creare un `SignatureServiceClient.Endpoint.Address` oggetto utilizzando `System.ServiceModel.EndpointAddress` costruttore. Passa un valore stringa che specifica il file WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/SignatureService?WSDL`). Non è necessario utilizzare il `lc_version` attributo. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Creare un `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto ottenendo il valore del `SignatureServiceClient.Endpoint.Binding` campo. Invia il valore restituito a `BasicHttpBinding`.
   * Imposta il `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegna al campo il nome utente dei moduli AEM `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore password corrispondente al campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Ottieni il documento PDF contenente i campi firma

   * Creare un `BLOB` mediante il costruttore. Il `BLOB` L&#39;oggetto viene utilizzato per memorizzare il documento PDF che contiene i campi firma.
   * Creare un `System.IO.FileStream` dell&#39;oggetto richiamando il relativo costruttore e passando un valore stringa che rappresenta la posizione del file del documento PDF e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto della `System.IO.FileStream` oggetto. È possibile determinare le dimensioni della matrice di byte ottenendo `System.IO.FileStream` dell&#39;oggetto `Length` proprietà.
   * Compilare la matrice di byte con i dati di flusso richiamando `System.IO.FileStream` dell&#39;oggetto `Read` e passando la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare il `BLOB` oggetto assegnando il relativo `MTOM` campo del contenuto della matrice di byte.

1. Recuperare i nomi dei campi firma

   * Recuperare i nomi dei campi firma richiamando `SignatureServiceClient` dell&#39;oggetto `getSignatureFieldList` e passando il `BLOB` oggetto contenente il documento PDF contenente i campi firma. Questo metodo restituisce un `MyArrayOfPDFSignatureField` insieme in cui ogni elemento contiene un elemento `PDFSignatureField` oggetto.
   * Effettua iterazione attraverso `MyArrayOfPDFSignatureField` per determinare se sono presenti nomi di campi di firma. Per ogni campo di firma nel documento PDF, è possibile ottenere un `PDFSignatureField` oggetto. Per ottenere il nome del campo firma, richiamare `PDFSignatureField` dell&#39;oggetto `getName` metodo. Questo metodo restituisce un valore stringa che specifica il nome del campo della firma.

**Consulta anche**

[Recupero dei nomi dei campi firma](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

[Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamare AEM Forms con SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Modifica dei campi della firma {#modifying-signature-fields}

Puoi modificare i campi della firma presenti in un documento PDF utilizzando l’API Java e l’API del servizio web. La modifica di un campo di firma comporta la modifica dei valori del dizionario del blocco del campo di firma o dei valori del dizionario dei valori iniziali.

A *dizionario blocco campo* specifica un elenco di campi bloccati quando il campo firma è firmato. Un campo bloccato impedisce agli utenti di apportare modifiche al campo. A *dizionario dei valori iniziali* contiene informazioni vincolanti utilizzate al momento dell&#39;applicazione della firma. È ad esempio possibile modificare le autorizzazioni che controllano le azioni che possono essere eseguite senza invalidare una firma.

Modificando un campo di firma esistente, è possibile modificare il documento PDF in modo che rifletta i requisiti aziendali in continua evoluzione. Ad esempio, un nuovo requisito aziendale potrebbe richiedere il blocco di tutti i campi del documento dopo la firma del documento.

In questa sezione viene illustrato come modificare un campo di firma modificando i valori del dizionario dei blocchi di campi e del dizionario dei valori iniziali. Le modifiche apportate al dizionario di blocco dei campi della firma determinano il blocco di tutti i campi del documento PDF quando viene firmato un campo della firma. Le modifiche apportate al dizionario dei valori iniziali non consentono tipi specifici di modifiche al documento.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Firma e sulla modifica dei campi della firma, vedere [Guida di riferimento dei servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-2}

Per modificare i campi di firma in un documento PDF, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Creare un client di firma.
1. Ottiene il documento PDF contenente il campo firma da modificare.
1. Imposta i valori del dizionario.
1. Modificare il campo firma.
1. Salvare il documento PDF come file PDF.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è implementato su JBoss)
* jbossall-client.jar (obbligatorio se AEM Forms è distribuito su JBoss)

Per informazioni sulla posizione di questi file JAR, vedi [Inclusione di file di libreria Java di LiveCycle](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un client di firma**

Prima di poter eseguire un&#39;operazione del servizio di firma a livello di programmazione, è necessario creare un client del servizio di firma.

**Ottiene il documento PDF contenente il campo firma da modificare**

Recuperare un documento PDF contenente il campo firma da modificare.

**Impostare i valori del dizionario**

Per modificare un campo di firma, assegnare valori al relativo dizionario di blocco dei campi o al dizionario dei valori iniziali. Per specificare i valori del dizionario di blocco del campo firma è necessario specificare i campi del documento PDF che vengono bloccati quando il campo firma viene firmato. Questa sezione illustra come bloccare tutti i campi.

È possibile impostare i seguenti valori del dizionario dei valori iniziali:

* **Controllo delle revisioni**: specifica se viene eseguito il controllo della revoca quando viene applicata una firma al campo firma.
* **Opzioni certificato**: assegna valori al dizionario dei valori iniziali del certificato. Prima di specificare le opzioni del certificato, è consigliabile acquisire familiarità con un dizionario dei valori iniziali del certificato. (vedere [Riferimento PDF](https://www.adobe.com/devnet/acrobat/pdfs/pdf_reference_1-7.pdf).)
* **Opzioni riepilogo**: assegna gli algoritmi di digest utilizzati per la firma. I valori validi sono SHA1, SHA256, SHA384, SHA512 e RIPEMD160.
* **Filtro**: specifica il filtro utilizzato con il campo firma. È ad esempio possibile utilizzare il filtro Adobe.PPKLite. (vedere [Riferimento PDF](https://www.adobe.com/devnet/acrobat/pdfs/pdf_reference_1-7.pdf).)
* **Opzioni di contrassegno**: specifica i valori dei flag associati al campo della firma. Il valore 1 indica che un firmatario deve utilizzare solo i valori specificati per la voce. Il valore 0 indica che sono consentiti altri valori. Di seguito sono riportate le posizioni di bit:

   * **1(Filtro):** Gestore della firma da utilizzare per firmare il campo della firma
   * **2 (Filtro secondario):** Matrice di nomi che indicano le codifiche accettabili da utilizzare per la firma
   * **3 (V)**: numero di versione minimo richiesto del gestore di firma da utilizzare per firmare il campo firma
   * **4 (Motivi):** Matrice di stringhe che specifica i possibili motivi per la firma di un documento
   * **5 (PDFLegalWarnings):** Matrice di stringhe che specifica le possibili attestazioni legali

* **Attestati legali**: quando un documento è certificato, viene automaticamente analizzato per individuare tipi specifici di contenuto che possono rendere ambiguo o fuorviante il contenuto visibile di un documento. Ad esempio, un’annotazione può oscurare il testo importante per comprendere ciò che viene certificato. Il processo di scansione genera avvisi che indicano la presenza di questo tipo di contenuto. Fornisce inoltre una spiegazione aggiuntiva del contenuto che potrebbe aver generato avvisi.
* **Autorizzazioni**: specifica le autorizzazioni che possono essere utilizzate in un documento PDF senza invalidare la firma.
* **Motivi**: specifica i motivi per cui il documento deve essere firmato.
* **Timestamp**: specifica le opzioni di marca temporale. È possibile, ad esempio, impostare l&#39;URL del server di marca temporale utilizzato.
* **Versione**: specifica il numero di versione minimo del gestore di firma da utilizzare per firmare il campo firma.

**Modificare il campo firma**

Dopo aver creato un client del servizio di firma, recuperato il documento PDF contenente il campo firma da modificare e impostato i valori del dizionario, è possibile indicare al servizio di firma di modificare il campo firma. Il servizio di firma restituisce quindi un documento PDF contenente il campo della firma modificato. Il documento PDF originale non subisce modifiche.

**Salvare il documento PDF come file PDF**

Salvare il documento PDF contenente il campo firma modificato come file PDF in modo che gli utenti possano aprirlo in Acrobat o Adobe Reader.

**Consulta anche**

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API di Signature Service](/help/forms/developing/signature-service-java-api-quick.md#signature-service-java-api-quick-start-soap)

[Firma digitale dei documenti di PDF](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

### Modificare i campi della firma utilizzando l’API Java {#modify-signature-fields-using-the-java-api}

Modifica un campo di firma utilizzando Signature API (Java):

1. Includi file di progetto

   Includi i file JAR dei client, ad esempio adobe-signatures-client.jar, nel percorso di classe del progetto Java.

1. Creare un client di firma

   * Creare un `ServiceClientFactory` oggetto che contiene proprietà di connessione.
   * Creare un `SignatureServiceClient` mediante il costruttore e passando il `ServiceClientFactory` oggetto.

1. Ottiene il documento PDF contenente il campo firma da modificare

   * Creare un `java.io.FileInputStream` oggetto che rappresenta il documento PDF contenente il campo firma da modificare utilizzando il relativo costruttore e passando un valore stringa che specifica la posizione del documento PDF.
   * Creare un `com.adobe.idp.Document` mediante il costruttore e passando il `java.io.FileInputStream` oggetto.

1. Impostare i valori del dizionario

   * Creare un `PDFSignatureFieldProperties` mediante il costruttore. A `PDFSignatureFieldProperties` l&#39;oggetto memorizza le informazioni del dizionario del blocco del campo della firma e del dizionario dei valori iniziali.
   * Creare un `PDFSeedValueOptionSpec` mediante il costruttore. Questo oggetto consente di impostare i valori del dizionario dei valori iniziali.
   * Non consentire modifiche al documento PDF richiamando `PDFSeedValueOptionSpec` dell&#39;oggetto `setMdpValue` e passando il `MDPPermissions.NoChanges` valore di enumerazione.
   * Creare un `FieldMDPOptionSpec` mediante il costruttore. Questo oggetto consente di impostare i valori del dizionario di blocco del campo della firma.
   * Blocca tutti i campi nel documento PDF richiamando `FieldMDPOptionSpec` dell&#39;oggetto `setMdpValue` e passando il `FieldMDPAction.ALL` valore di enumerazione.
   * Impostare le informazioni del dizionario dei valori iniziali richiamando `PDFSignatureFieldProperties` dell&#39;oggetto `setSeedValue` e passando il `PDFSeedValueOptionSpec` oggetto.
   * Impostare le informazioni del dizionario di blocco del campo della firma richiamando `PDFSignatureFieldProperties`dell&#39;oggetto `setFieldMDP` e passando il `FieldMDPOptionSpec` oggetto.

   >[!NOTE]
   >
   >Per visualizzare tutti i valori del dizionario dei valori iniziali che è possibile impostare, vedere `PDFSeedValueOptionSpec` riferimento di classe. (vedere [Riferimento API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).)

1. Modificare il campo firma

   Modificare il campo firma richiamando `SignatureServiceClient` dell&#39;oggetto `modifySignatureField` e fornendo i seguenti valori:

   * Il `com.adobe.idp.Document` oggetto che memorizza il documento PDF contenente il campo firma da modificare
   * Valore stringa che specifica il nome del campo della firma
   * Il `PDFSignatureFieldProperties` oggetto che memorizza le informazioni del dizionario del blocco del campo della firma e del dizionario del valore seed

   Il `modifySignatureField` il metodo restituisce un `com.adobe.idp.Document` oggetto che memorizza un documento PDF contenente il campo firma modificato.

1. Salvare il documento PDF come file PDF

   * Creare un `java.io.File` e assicurarsi che l&#39;estensione del nome file sia .pdf.
   * Richiama `com.adobe.idp.Document` dell&#39;oggetto `copyToFile` metodo per copiare il contenuto del `com.adobe.idp.Document` al file. Assicurati di utilizzare `com.adobe.idp.Document` oggetto che `modifySignatureField` metodo restituito.

### Modificare i campi della firma utilizzando l’API del servizio web {#modify-signature-fields-using-the-web-service-api}

Modifica un campo di firma utilizzando Signature API (servizio web):

1. Includi file di progetto

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l’indirizzo IP del server che ospita AEM Forms.

1. Creare un client di firma

   * Creare un `SignatureServiceClient` utilizzando il costruttore predefinito.
   * Creare un `SignatureServiceClient.Endpoint.Address` oggetto utilizzando `System.ServiceModel.EndpointAddress` costruttore. Passa un valore stringa che specifica il file WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/SignatureService?WSDL`). Non è necessario utilizzare il `lc_version` attributo. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Creare un `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto ottenendo il valore del `SignatureServiceClient.Endpoint.Binding` campo. Invia il valore restituito a `BasicHttpBinding`.
   * Imposta il `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegna al campo il nome utente dei moduli AEM `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore password corrispondente al campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Ottiene il documento PDF contenente il campo firma da modificare

   * Creare un `BLOB` mediante il costruttore. Il `BLOB` L&#39;oggetto viene utilizzato per memorizzare il documento PDF contenente il campo firma da modificare.
   * Creare un `System.IO.FileStream` dell&#39;oggetto richiamando il relativo costruttore e passando un valore stringa che rappresenta la posizione del file del documento PDF e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto della `System.IO.FileStream` oggetto. È possibile determinare le dimensioni della matrice di byte ottenendo `System.IO.FileStream` dell&#39;oggetto `Length` proprietà.
   * Compilare la matrice di byte con i dati di flusso richiamando `System.IO.FileStream` dell&#39;oggetto `Read` e passando la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare il `BLOB` oggetto assegnando il relativo `MTOM` proprietà il contenuto della matrice di byte.

1. Impostare i valori del dizionario

   * Creare un `PDFSignatureFieldProperties` mediante il costruttore. Questo oggetto memorizza le informazioni del dizionario del blocco del campo della firma e del dizionario dei valori iniziali.
   * Creare un `PDFSeedValueOptionSpec` mediante il costruttore. Questo oggetto consente di impostare i valori del dizionario dei valori iniziali.
   * Non consentire modifiche al documento PDF assegnando `MDPPermissions.NoChanges` valore di enumerazione per `PDFSeedValueOptionSpec` dell&#39;oggetto `mdpValue` membro dati.
   * Creare un `FieldMDPOptionSpec` mediante il costruttore. Questo oggetto consente di impostare i valori del dizionario di blocco del campo della firma.
   * Blocca tutti i campi nel documento PDF assegnando il `FieldMDPAction.ALL` valore di enumerazione per `FieldMDPOptionSpec` dell&#39;oggetto `mdpValue` membro dati.
   * Impostare le informazioni del dizionario dei valori iniziali assegnando `PDFSeedValueOptionSpec` oggetto al `PDFSignatureFieldProperties` dell&#39;oggetto `seedValue` membro dati.
   * Impostare le informazioni del dizionario di blocco del campo della firma assegnando `FieldMDPOptionSpec` oggetto al `PDFSignatureFieldProperties` dell&#39;oggetto `fieldMDP` membro dati.

   >[!NOTE]
   >
   >Per visualizzare tutti i valori del dizionario dei valori iniziali che è possibile impostare, vedere `PDFSeedValueOptionSpec` riferimento di classe. (vedere [Riferimento API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)).

1. Modificare il campo firma

   Modificare il campo firma richiamando `SignatureServiceClient` dell&#39;oggetto `modifySignatureField` e fornendo i seguenti valori:

   * Il `BLOB` oggetto che memorizza il documento PDF contenente il campo firma da modificare
   * Valore stringa che specifica il nome del campo della firma
   * Il `PDFSignatureFieldProperties` oggetto che memorizza le informazioni del dizionario del blocco del campo della firma e del dizionario del valore seed

   Il `modifySignatureField` il metodo restituisce un `BLOB` oggetto che memorizza un documento PDF contenente il campo firma modificato.

1. Salvare il documento PDF come file PDF

   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore stringa che rappresenta la posizione del file del documento PDF che conterrà il campo firma e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto della `BLOB` oggetto che `addSignatureField` restituisce. Popolare la matrice di byte ottenendo il valore della `BLOB` dell&#39;oggetto `MTOM` membro dati.
   * Creare un `System.IO.BinaryWriter` oggetto richiamando il relativo costruttore e passando il `System.IO.FileStream` oggetto.
   * Scrivere il contenuto della matrice di byte in un file PDF richiamando `System.IO.BinaryWriter` dell&#39;oggetto `Write` e passando la matrice di byte.

**Consulta anche**

[Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamare AEM Forms con SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Firma digitale dei documenti di PDF {#digitally-signing-pdf-documents}

Le firme digitali possono essere applicate ai documenti PDF per garantire un livello di sicurezza adeguato. Le firme digitali, come le firme scritte a mano, forniscono un mezzo mediante il quale i firmatari si identificano e rilasciano dichiarazioni su un documento. La tecnologia utilizzata per apporre la firma digitale ai documenti consente di garantire che il firmatario e i destinatari siano chiari su ciò che è stato firmato e certi che il documento non sia stato modificato dopo la firma.

I documenti PDF sono firmati mediante una tecnologia a chiave pubblica. Un firmatario ha due chiavi: una chiave pubblica e una chiave privata. La chiave privata viene memorizzata nelle credenziali di un utente che devono essere disponibili al momento della firma. La chiave pubblica viene archiviata nel certificato dell&#39;utente che deve essere disponibile per i destinatari per convalidare la firma. Le informazioni sui certificati revocati si trovano nelle risposte CRL (Certificate Revocation List) e OCSP (Online Certificate Status Protocol) distribuite dalle autorità di certificazione (CA). L’ora della firma può essere ottenuta da una fonte attendibile nota come autorità di marca temporale.

>[!NOTE]
>
>Prima di poter aggiungere una firma digitale a un documento di PDF, è necessario assicurarsi di aggiungere il certificato ad AEM Forms. Un certificato viene aggiunto utilizzando la console di amministrazione o a livello di programmazione utilizzando l’API di Trust Manager. (vedere [Importazione delle credenziali tramite l&#39;API di Gestione trust](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api).)

È possibile apporre una firma digitale ai documenti PDF a livello di programmazione. Quando si firma digitalmente un documento PDF, è necessario fare riferimento a una credenziale di sicurezza esistente in AEM Forms. Le credenziali sono la chiave privata utilizzata per la firma.

Il servizio di firma esegue i passaggi seguenti quando viene firmato un documento di PDF:

1. Il servizio di firma recupera le credenziali dal Truststore passando l&#39;alias specificato nella richiesta.
1. Truststore cerca le credenziali specificate.
1. Le credenziali vengono restituite al servizio di firma e utilizzate per firmare il documento. Le credenziali vengono anche memorizzate nella cache in base all’alias per le richieste future.

Per informazioni sulla gestione delle credenziali di protezione, vedere *Installazione e distribuzione di AEM Forms* per il server applicazioni.

>[!NOTE]
>
>Esistono differenze tra la firma e la certificazione dei documenti. (vedere [Certificazione dei documenti di PDF](digitally-signing-certifying-documents.md#certifying-pdf-documents).)

>[!NOTE]
>
>Non tutti i documenti di PDF supportano la firma. Per ulteriori informazioni sul servizio Firma e sulla firma digitale dei documenti, vedere [Guida di riferimento dei servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Il servizio di firma non supporta file XDP con dati PDF incorporati come input per un&#39;operazione, ad esempio la certificazione di un documento. Questa azione fa sì che il servizio di firma generi un `PDFOperationException`. Per risolvere il problema, convertire il file XDP in un file PDF utilizzando il servizio Utilità PDF, quindi passare il file PDF convertito a un&#39;operazione del servizio di firma. (vedere [Utilizzo delle utilità PDF](/help/forms/developing/pdf-utilities.md#working-with-pdf-utilities).)

**Cifra credenziali HSM nShield**

Quando si utilizza una credenziale HSM nShield di crittografia per firmare o certificare un documento PDF, non è possibile utilizzare la nuova credenziale fino al riavvio del server applicazioni J2EE in cui è distribuito AEM Forms. Tuttavia, è possibile impostare un valore di configurazione, in modo che l&#39;operazione di firma o di certificazione funzioni senza riavviare il server applicazioni J2EE.

È possibile aggiungere il seguente valore di configurazione nel file cknfastrc, che si trova in /opt/nfast/cknfastrc (o c:\nfast\cknfastrc):

```shell
    CKNFAST_ASSUME_SINGLE_PROCESS=0
```

Dopo aver aggiunto questo valore di configurazione al file cknfastrc, è possibile utilizzare le nuove credenziali senza riavviare il server applicazioni J2EE.

**Firma non attendibile**

Quando si certifica e firma lo stesso documento PDF, se la firma di certificazione non è attendibile, sulla prima firma viene visualizzato un triangolo giallo all’apertura del documento PDF in Acrobat o Adobe Reader. La firma di certificazione deve essere attendibile per evitare questa situazione.

**Firma di documenti basati su XFA**

Se tenti di firmare un modulo basato su XFA utilizzando l’API del servizio di firma, i dati potrebbero non essere presenti nel `View` `Signed` `Version` in Acrobat. Ad esempio, considera il seguente flusso di lavoro:

* Utilizzando un file XDP creato mediante Designer, si unisce una struttura di modulo contenente un campo firma e dati XML contenenti dati modulo. Puoi utilizzare il servizio Forms per generare un documento interattivo di PDF.
* Firma il documento PDF utilizzando l’API del servizio di firma.

### Riepilogo dei passaggi {#summary_of_steps-3}

Per apporre una firma digitale a un documento PDF, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Creare un client del servizio di firma.
1. Ottieni il documento PDF da firmare.
1. Firma il documento di PDF.
1. Salvare il documento PDF firmato come file PDF.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è implementato su JBoss)
* jbossall-client.jar (obbligatorio se AEM Forms è distribuito su JBoss)

**Creare un client Firme**

Prima di poter eseguire un&#39;operazione del servizio di firma a livello di programmazione, è necessario creare un client del servizio di firma.

**Ottieni il documento PDF da firmare**

Per firmare un documento di PDF, è necessario ottenere un documento di PDF contenente un campo firma. Se un documento PDF non contiene un campo firma, non può essere firmato. È possibile aggiungere un campo firma utilizzando Designer o a livello di programmazione.

**Firma il documento PDF**

Quando si firma un documento di PDF, è possibile impostare le opzioni di runtime utilizzate dal servizio di firma. È possibile impostare le seguenti opzioni:

* Opzioni di aspetto
* Verifica della revoca
* Valori di marca temporale

Per impostare le opzioni di aspetto, utilizzate una `PDFSignatureAppearanceOptionSpec` oggetto. Ad esempio, è possibile visualizzare la data all’interno di una firma richiamando il `PDFSignatureAppearanceOptionSpec` dell&#39;oggetto `setShowDate` metodo e passaggio `true`.

È inoltre possibile specificare se eseguire o meno un controllo di revoca che determini se il certificato utilizzato per firmare digitalmente un documento di PDF è stato revocato. Per eseguire il controllo della revoca, è possibile specificare uno dei seguenti valori:

* **NoCheck**: non eseguire il controllo della revoca.
* **BestEffort**: cerca sempre di verificare la presenza di revoche di tutti i certificati nella catena. Se si verificano problemi durante il controllo, la revoca viene considerata valida. In caso di errori, si supponga che il certificato non venga revocato.
* **CheckIfAvailable** Verificare la revoca di tutti i certificati della catena se sono disponibili informazioni sulla revoca. Se si verificano problemi durante il controllo, la revoca viene considerata non valida. In caso di errori, si supponga che il certificato sia stato revocato e che non sia valido. (Questo è il valore predefinito.)
* **AlwaysCheck**: verifica la revoca di tutti i certificati della catena. Se le informazioni sulla revoca non sono presenti in alcun certificato, la revoca verrà considerata non valida.

Per eseguire il controllo di revoca su un certificato, è possibile specificare un URL di un server di elenco di revoche di certificati (CRL) utilizzando un `CRLOptionSpec` oggetto. Tuttavia, se si desidera eseguire il controllo di revoca e non si specifica un URL per un server CRL, il servizio di firma ottiene l&#39;URL dal certificato.

Anziché utilizzare un server CRL, è possibile utilizzare un server OCSP (Certificate Status Protocol) online durante la verifica della revoca. In genere, quando si utilizza un server OCSP anziché un server CRL, il controllo di revoca viene eseguito più rapidamente. (Consulta &quot;Online Certificate Status Protocol&quot; (Protocollo sullo stato dei certificati online) all’indirizzo [https://tools.ietf.org/html/rfc2560](https://tools.ietf.org/html/rfc2560).)

È possibile impostare l&#39;ordine dei server CRL e OCSP utilizzato dal servizio di firma utilizzando Adobe Applications and Services. Se, ad esempio, il server OCSP è impostato prima in Adobe Applications and Services, viene selezionato il server OCSP, seguito dal server CRL. Consultate &quot;Gestione di certificati e credenziali tramite l&#39;archivio fonti attendibili&quot; nella Guida di AAC.

Se si specifica di non eseguire il controllo di revoca, il servizio di firma non verifica se il certificato utilizzato per firmare o certificare un documento è stato revocato. In altre parole, le informazioni del server CRL e OCSP vengono ignorate.

>[!NOTE]
>
>Sebbene nel certificato sia possibile specificare un CRL o un server OCSP, è possibile sovrascrivere l&#39;URL specificato nel certificato utilizzando un `CRLOptionSpec` e un `OCSPOptionSpec` oggetto. Ad esempio, per ignorare il server CRL, puoi richiamare `CRLOptionSpec` dell&#39;oggetto `setLocalURI` metodo.

La marca temporale si riferisce al processo di tracciamento dell’ora in cui un documento firmato o certificato è stato modificato. Una volta firmato, il documento non deve essere modificato, nemmeno dal proprietario del documento. La marca temporale consente di applicare la validità di un documento firmato o certificato. È possibile impostare le opzioni di marca temporale utilizzando un `TSPOptionSpec` oggetto. Ad esempio, puoi specificare l’URL di un server provider di marca temporale (TSP).

>[!NOTE]
>
>Nelle sezioni di Java e del servizio web, e nei relativi avvii rapidi, viene utilizzato il controllo delle revoche. Poiché non vengono specificate informazioni sul server CRL o OCSP, le informazioni sul server vengono ottenute dal certificato utilizzato per firmare digitalmente il documento PDF.

Per firmare correttamente un documento PDF, è possibile specificare il nome completo del campo firma che conterrà la firma digitale, ad esempio `form1[0].#subform[1].SignatureField3[3]`. Quando si utilizza un campo modulo XFA, è possibile utilizzare anche il nome parziale del campo firma: `SignatureField3[3]`.

Per apporre la firma digitale a un documento PDF, è inoltre necessario fare riferimento a una credenziale di protezione. Per fare riferimento a una credenziale di protezione, specificare un alias. L’alias è un riferimento a una credenziale effettiva che può trovarsi in un file PKCS#12 (con estensione .pfx) o in un modulo di sicurezza hardware (HSM). Per informazioni sulle credenziali di protezione, vedere *Installazione e distribuzione di AEM Forms* per il server applicazioni.

**Salva il documento PDF firmato**

Dopo che il servizio di firma digitale ha apposto la firma al documento PDF, è possibile salvarlo come file PDF in modo che gli utenti possano aprirlo in Acrobat o Adobe Reader.

**Consulta anche**

[Firmare digitalmente i documenti PDF utilizzando l’API Java](digitally-signing-certifying-documents.md#digitally-sign-pdf-documents-using-the-java-api)

[Firma digitale di documenti PDF tramite l’API del servizio web](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents-using-the-web-service-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Aggiunta di campi firma](digitally-signing-certifying-documents.md#adding-signature-fields)

[Recupero dei nomi dei campi firma](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

### Firmare digitalmente i documenti PDF utilizzando l’API Java {#digitally-sign-pdf-documents-using-the-java-api}

Firmare digitalmente un documento PDF utilizzando Signature API (Java):

1. Includi file di progetto

   Includi i file JAR dei client, ad esempio adobe-signatures-client.jar, nel percorso di classe del progetto Java.

1. Creare un client Firme

   * Creare un `ServiceClientFactory` oggetto che contiene proprietà di connessione.
   * Creare un `SignatureServiceClient` mediante il costruttore e passando il `ServiceClientFactory` oggetto.

1. Ottieni il documento PDF da firmare

   * Creare un `java.io.FileInputStream` oggetto che rappresenta il documento PDF da firmare digitalmente utilizzando il relativo costruttore e passando un valore stringa che specifica la posizione del documento PDF.
   * Creare un `com.adobe.idp.Document` mediante il costruttore e passando il `java.io.FileInputStream` oggetto.

1. Firma il documento PDF

   Firma il documento PDF richiamando `SignatureServiceClient` dell&#39;oggetto `sign` e fornendo i seguenti valori:

   * A `com.adobe.idp.Document` oggetto che rappresenta il documento PDF da firmare.
   * Valore string che rappresenta il nome del campo firma che conterrà la firma digitale.
   * A `Credential` oggetto che rappresenta le credenziali utilizzate per apporre una firma digitale al documento PDF. Creare un `Credential` oggetto richiamando il `Credential` statico dell&#39;oggetto `getInstance` e passando un valore stringa che specifica il valore di alias corrispondente alle credenziali di sicurezza.
   * A `HashAlgorithm` oggetto che specifica un membro dati statico che rappresenta l&#39;algoritmo hash da utilizzare per digerire il documento PDF. Ad esempio, puoi specificare `HashAlgorithm.SHA1` per utilizzare l’algoritmo SHA1.
   * Valore stringa che rappresenta il motivo per cui il documento PDF è stato firmato digitalmente.
   * Valore stringa che rappresenta le informazioni di contatto del firmatario.
   * A `PDFSignatureAppearanceOptions` oggetto che controlla l&#39;aspetto della firma digitale. È ad esempio possibile utilizzare questo oggetto per aggiungere un logo personalizzato a una firma digitale.
   * A `java.lang.Boolean` oggetto che specifica se eseguire il controllo di revoca sul certificato del firmatario.
   * Un `OCSPOptionSpec` oggetto che memorizza le preferenze per il supporto del protocollo OCSP (Online Certificate Status Protocol). Se non viene eseguito il controllo della revoca, questo parametro non viene utilizzato ed è possibile specificare `null`.
   * A `CRLPreferences` oggetto che memorizza le preferenze dell&#39;elenco di revoche di certificati (CRL). Se non viene eseguito il controllo della revoca, questo parametro non viene utilizzato ed è possibile specificare `null`.
   * A `TSPPreferences` oggetto che memorizza le preferenze per il supporto del provider di marca temporale (TSP). Questo parametro è facoltativo e può essere `null`. Per ulteriori informazioni, consulta [Riferimento API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

   Il `sign` il metodo restituisce un `com.adobe.idp.Document` oggetto che rappresenta il documento PDF firmato.

1. Salva il documento PDF firmato

   * Creare un `java.io.File` e assicurarsi che l&#39;estensione del file sia .pdf.
   * Richiama `com.adobe.idp.Document` dell&#39;oggetto `copyToFile` metodo e passaggio `java.io.File`per copiare il contenuto del `Document` al file. Assicurati di utilizzare `com.adobe.idp.Document` oggetto restituito da `sign` metodo.

**Consulta anche**

[Firma digitale dei documenti di PDF](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[Quick Start (modalità SOAP): firma digitale di un documento PDF tramite l’API Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-pdf-document-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Firma digitale di documenti PDF tramite l’API del servizio web {#digitally-signing-pdf-documents-using-the-web-service-api}

Per firmare digitalmente un documento PDF utilizzando l’API di firma (servizio web):

1. Includi file di progetto

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l’indirizzo IP del server che ospita AEM Forms.

1. Creare un client Firme

   * Creare un `SignatureServiceClient` utilizzando il costruttore predefinito.
   * Creare un `SignatureServiceClient.Endpoint.Address` oggetto utilizzando `System.ServiceModel.EndpointAddress` costruttore. Passa un valore stringa che specifica il file WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/SignatureService?WSDL`). Non è necessario utilizzare il `lc_version` attributo. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Creare un `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto ottenendo il valore del `SignatureServiceClient.Endpoint.Binding` campo. Invia il valore restituito a `BasicHttpBinding`.
   * Imposta il `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegna al campo il nome utente dei moduli AEM `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore password corrispondente al campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Ottieni il documento PDF da firmare

   * Creare un `BLOB` mediante il costruttore. Il `BLOB` L&#39;oggetto viene utilizzato per memorizzare un documento PDF firmato.
   * Creare un `System.IO.FileStream` richiamando il costruttore e passando un valore stringa che rappresenta la posizione del file del documento PDF da firmare e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto della `System.IO.FileStream` oggetto. È possibile determinare le dimensioni della matrice di byte ottenendo `System.IO.FileStream` dell&#39;oggetto `Length` proprietà.
   * Compilare la matrice di byte con i dati di flusso richiamando `System.IO.FileStream` dell&#39;oggetto `Read` e passando la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare il `BLOB` oggetto assegnando il relativo `MTOM` proprietà il contenuto della matrice di byte.

1. Firma il documento PDF

   Firma il documento PDF richiamando `SignatureServiceClient` dell&#39;oggetto `sign` e fornendo i seguenti valori:

   * A `BLOB` oggetto che rappresenta il documento PDF da firmare.
   * Valore string che rappresenta il nome del campo firma che conterrà la firma digitale.
   * A `Credential` oggetto che rappresenta le credenziali utilizzate per apporre una firma digitale al documento PDF. Creare un `Credential` mediante il costruttore e specificare l&#39;alias assegnando un valore al `Credential` dell&#39;oggetto `alias` proprietà.
   * A `HashAlgorithm` oggetto che specifica un membro dati statico che rappresenta l&#39;algoritmo hash da utilizzare per digerire il documento PDF. Ad esempio, puoi specificare `HashAlgorithm.SHA1` per utilizzare l’algoritmo SHA1.
   * Un valore booleano che specifica se viene utilizzato l’algoritmo hash.
   * Valore stringa che rappresenta il motivo per cui il documento PDF è stato firmato digitalmente.
   * Valore stringa che rappresenta la posizione del firmatario.
   * Valore stringa che rappresenta le informazioni di contatto del firmatario.
   * A `PDFSignatureAppearanceOptions` oggetto che controlla l&#39;aspetto della firma digitale. È ad esempio possibile utilizzare questo oggetto per aggiungere un logo personalizzato a una firma digitale.
   * A `System.Boolean` oggetto che specifica se eseguire il controllo di revoca sul certificato del firmatario. Se la verifica della revoca viene eseguita, viene incorporata nella firma. Il valore predefinito è `false`.
   * Un `OCSPOptionSpec` oggetto che memorizza le preferenze per il supporto del protocollo OCSP (Online Certificate Status Protocol). Se non viene eseguito il controllo della revoca, questo parametro non viene utilizzato ed è possibile specificare `null`. Per informazioni su questo oggetto, vedi [Riferimento API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * A `CRLPreferences` oggetto che memorizza le preferenze dell&#39;elenco di revoche di certificati (CRL). Se non viene eseguito il controllo della revoca, questo parametro non viene utilizzato ed è possibile specificare `null`.
   * A `TSPPreferences` oggetto che memorizza le preferenze per il supporto del provider di marca temporale (TSP). Questo parametro è facoltativo e può essere `null`.

   Il `sign` il metodo restituisce un `BLOB` oggetto che rappresenta il documento PDF firmato.

1. Salva il documento PDF firmato

   * Creare un `System.IO.FileStream` richiamando il relativo costruttore. Passa un valore stringa che rappresenta la posizione del file del documento PDF firmato e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto della `BLOB` oggetto restituito da `sign` metodo. Popolare la matrice di byte ottenendo il valore della `BLOB` dell&#39;oggetto `MTOM` membro dati.
   * Creare un `System.IO.BinaryWriter` oggetto richiamando il relativo costruttore e passando il `System.IO.FileStream` oggetto.
   * Scrivere il contenuto della matrice di byte in un file PDF richiamando `System.IO.BinaryWriter` dell&#39;oggetto `Write` e passando la matrice di byte.

**Consulta anche**

[Firma digitale dei documenti di PDF](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamare AEM Forms con SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Forms interattivo con firma digitale {#digitally-signing-interactive-forms}

È possibile firmare un modulo interattivo creato dal servizio Forms. Ad esempio, considera il seguente flusso di lavoro:

* È possibile unire un modulo PDF basato su XFA creato utilizzando Designer e i dati del modulo in un documento XML utilizzando il servizio Forms. Il server Forms esegue il rendering di un modulo interattivo.
* Firmi il modulo interattivo utilizzando l’API del servizio di firma.

Il risultato è un modulo PDF interattivo con firma digitale. Quando firmi un modulo PDF basato su un modulo XFA, accertati di salvare il file PDF come modulo Adobe Static PDF. Se si tenta di firmare un modulo PDF salvato come modulo Adobe Dynamic PDF, si verifica un&#39;eccezione. Poiché stai firmando il modulo restituito dal servizio Forms, accertati che il modulo contenga un campo firma.

>[!NOTE]
>
>Prima di poter aggiungere una firma digitale a un modulo interattivo, è necessario assicurarsi di aggiungere il certificato ad AEM Forms. Un certificato viene aggiunto utilizzando la console di amministrazione o a livello di programmazione utilizzando l’API di Trust Manager. (vedere [Importazione delle credenziali tramite l&#39;API di Gestione trust](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api).)

Quando utilizzi l’API di servizio Forms, imposta il `GenerateServerAppearance` opzione di runtime per `true`. Questa opzione di runtime garantisce che l&#39;aspetto del modulo generato sul server rimanga valido quando viene aperto in Acrobat o Adobe Reader. È consigliabile impostare questa opzione di runtime durante la generazione di un modulo interattivo da firmare utilizzando l’API Forms.

>[!NOTE]
>
>Prima di leggere Digitally Signing Interactive Forms, è consigliabile avere familiarità con la firma dei documenti di PDF. (vedere [Firma digitale dei documenti di PDF](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents).)

### Riepilogo dei passaggi {#summary_of_steps-4}

Per apporre una firma digitale a un modulo interattivo restituito dal servizio Forms, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Creazione di un client Forms e Signatures.
1. Ottieni il modulo interattivo utilizzando il servizio Forms.
1. Firma il modulo interattivo.
1. Salvare il documento PDF firmato come file PDF.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-forms-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è implementato su JBoss)
* jbossall-client.jar (obbligatorio se AEM Forms è distribuito su JBoss)

Per informazioni sulla posizione di questi file JAR, vedi [Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creazione di un client Forms e Signatures**

Poiché questo flusso di lavoro richiama sia i servizi Forms che Signature, creare sia un client di servizi Forms che un client di servizi Signature.

**Ottenere il modulo interattivo utilizzando il servizio Forms**

Puoi utilizzare il servizio Forms per ottenere il modulo interattivo di PDF da firmare. A partire da AEM Forms, puoi trasmettere un `com.adobe.idp.Document` al servizio Forms che contiene il modulo da riprodurre. Il nome di questo metodo è `renderPDFForm2`. Questo metodo restituisce un `com.adobe.idp.Document` oggetto contenente il modulo da firmare. Puoi trasmettere questo `com.adobe.idp.Document` al servizio di firma.

Allo stesso modo, se utilizzi i servizi web, puoi trasmettere `BLOB` istanza che il servizio Forms restituisce al servizio Signature.

>[!NOTE]
>
>L&#39;avvio rapido associato alla sezione Forms interattiva con firma digitale richiama `renderPDFForm2` metodo.

**Firma il modulo interattivo**

Quando si firma un documento di PDF, è possibile impostare le opzioni di runtime utilizzate dal servizio di firma. È possibile impostare le seguenti opzioni:

* Opzioni di aspetto
* Verifica della revoca
* Valori di marca temporale

Per impostare le opzioni di aspetto, utilizzate una `PDFSignatureAppearanceOptionSpec` oggetto. Ad esempio, è possibile visualizzare la data all’interno di una firma richiamando il `PDFSignatureAppearanceOptionSpec` dell&#39;oggetto `setShowDate` metodo e passaggio `true`.

**Salva il documento PDF firmato**

Dopo che il servizio di firma digitale ha firmato il documento PDF, è possibile salvarlo come file PDF. Il file PDF può essere aperto in Acrobat o Adobe Reader.

**Consulta anche**

[Firmare digitalmente un modulo interattivo utilizzando l’API Java](digitally-signing-certifying-documents.md#digitally-sign-an-interactive-form-using-the-java-api)

[Firmare digitalmente un modulo interattivo utilizzando l’API del servizio web](digitally-signing-certifying-documents.md#digitally-sign-an-interactive-form-using-the-web-service-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Firma digitale dei documenti di PDF](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[Rendering dei PDF forms interattivi](/help/forms/developing/rendering-forms.md#rendering-interactive-pdf-forms)

### Firmare digitalmente un modulo interattivo utilizzando l’API Java {#digitally-sign-an-interactive-form-using-the-java-api}

Apporre una firma digitale a un modulo interattivo utilizzando Forms e Signature API (Java):

1. Includi file di progetto

   Includi i file JAR dei client, ad esempio adobe-signatures-client.jar e adobe-forms-client.jar, nel percorso di classe del progetto Java.

1. Creazione di un client Forms e Signatures

   * Creare un `ServiceClientFactory` oggetto che contiene proprietà di connessione.
   * Creare un `SignatureServiceClient` mediante il costruttore e passando il `ServiceClientFactory` oggetto.
   * Creare un `FormsServiceClient` mediante il costruttore e passando il `ServiceClientFactory` oggetto.

1. Ottenere il modulo interattivo utilizzando il servizio Forms

   * Creare un `java.io.FileInputStream` oggetto che rappresenta il documento PDF da passare al servizio Forms tramite il relativo costruttore. Passa un valore stringa che specifica la posizione del documento PDF.
   * Creare un `com.adobe.idp.Document` mediante il costruttore e passando il `java.io.FileInputStream` oggetto.
   * Creare un `java.io.FileInputStream` oggetto che rappresenta il documento XML contenente i dati del modulo da passare al servizio Forms mediante il relativo costruttore. Passa un valore stringa che specifica la posizione del file XML.
   * Creare un `com.adobe.idp.Document` mediante il costruttore e passando il `java.io.FileInputStream` oggetto.
   * Creare un `PDFFormRenderSpec` oggetto utilizzato per impostare le opzioni di runtime. Richiama `PDFFormRenderSpec` dell&#39;oggetto `setGenerateServerAppearance` metodo e passaggio `true`.
   * Richiama `FormsServiceClient` dell&#39;oggetto `renderPDFForm2` e trasmettere i seguenti valori:

      * A `com.adobe.idp.Document` oggetto che contiene il modulo PDF da riprodurre.
      * A `com.adobe.idp.Document` oggetto contenente dati da unire con il modulo.
      * A `PDFFormRenderSpec` oggetto che memorizza le opzioni di runtime.
      * A `URLSpec` oggetto contenente valori URI richiesti dal servizio Forms. È possibile specificare `null` per questo valore di parametro.
      * A `java.util.HashMap` oggetto che memorizza gli allegati. Questo è un parametro facoltativo e puoi specificare `null` se non si desidera allegare file al modulo.

     Il `renderPDFForm2` il metodo restituisce un `FormsResult` oggetto che contiene un flusso di dati modulo

   * Recuperare il modulo PDF richiamando `FormsResult` dell&#39;oggetto `getOutputContent` metodo. Questo metodo restituisce un `com.adobe.idp.Document` oggetto che rappresenta il modulo interattivo.

1. Firma il modulo interattivo

   Firma il documento PDF richiamando `SignatureServiceClient` dell&#39;oggetto `sign` e fornendo i seguenti valori:

   * A `com.adobe.idp.Document` oggetto che rappresenta il documento PDF da firmare. Assicurati che questo oggetto sia `com.adobe.idp.Document` oggetto ottenuto dal servizio Forms.
   * Valore stringa che rappresenta il nome del campo firma firmato.
   * A `Credential` oggetto che rappresenta le credenziali utilizzate per apporre una firma digitale al documento PDF. Creare un `Credential` oggetto richiamando il `Credential` statico dell&#39;oggetto `getInstance` metodo. Passa un valore stringa che specifica il valore alias corrispondente alle credenziali di sicurezza.
   * A `HashAlgorithm` oggetto che specifica un membro dati statico che rappresenta l&#39;algoritmo hash da utilizzare per digerire il documento PDF. Ad esempio, puoi specificare `HashAlgorithm.SHA1` per utilizzare l’algoritmo SHA1.
   * Valore stringa che rappresenta il motivo per cui il documento PDF è stato firmato digitalmente.
   * Valore stringa che rappresenta le informazioni di contatto del firmatario.
   * A `PDFSignatureAppearanceOptions` oggetto che controlla l&#39;aspetto della firma digitale. È ad esempio possibile utilizzare questo oggetto per aggiungere un logo personalizzato a una firma digitale.
   * A `java.lang.Boolean` oggetto che specifica se eseguire il controllo di revoca sul certificato del firmatario.
   * Un `OCSPPreferences` oggetto che memorizza le preferenze per il supporto del protocollo OCSP (Online Certificate Status Protocol). Se non viene eseguito il controllo della revoca, questo parametro non viene utilizzato ed è possibile specificare `null`.
   * A `CRLPreferences` oggetto che memorizza le preferenze dell&#39;elenco di revoche di certificati (CRL). Se non viene eseguito il controllo della revoca, questo parametro non viene utilizzato ed è possibile specificare `null`.
   * A `TSPPreferences` oggetto che memorizza le preferenze per il supporto del provider di marca temporale (TSP). Questo parametro è facoltativo e può essere `null`.

   Il `sign` il metodo restituisce un `com.adobe.idp.Document` oggetto che rappresenta il documento PDF firmato.

1. Salva il documento PDF firmato

   * Creare un `java.io.File` e assicurarsi che l&#39;estensione del nome file sia .pdf.
   * Richiama `com.adobe.idp.Document` dell&#39;oggetto `copyToFile` metodo e passaggio `java.io.File`per copiare il contenuto del `Document` al file. Assicurati di utilizzare `com.adobe.idp.Document` oggetto che `sign` metodo restituito.

**Consulta anche**

[Forms interattivo con firma digitale](digitally-signing-certifying-documents.md#digitally-signing-interactive-forms)

[Quick Start (modalità SOAP): firma digitale di un documento PDF tramite l’API Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-pdf-document-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Firmare digitalmente un modulo interattivo utilizzando l’API del servizio web {#digitally-sign-an-interactive-form-using-the-web-service-api}

Firmare digitalmente un modulo interattivo utilizzando Forms e Signature API (servizio web):

1. Includi file di progetto

   Creare un progetto Microsoft .NET che utilizza MTOM. Poiché questa applicazione client richiama due servizi AEM Forms, creare due riferimenti al servizio. Utilizza la seguente definizione WSDL per il riferimento al servizio associato al servizio di firma: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   Utilizza la seguente definizione WSDL per il riferimento al servizio associato al servizio Forms: `http://localhost:8080/soap/services/FormsService?WSDL&lc_version=9.0.1`.

   Perché il `BLOB` il tipo di dati è comune a entrambi i riferimenti di servizio, qualifica completa `BLOB` tipo di dati quando lo si utilizza. Nel servizio Web corrispondente, tutte le `BLOB` le istanze sono completamente qualificate.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l’indirizzo IP del server che ospita AEM Forms.

1. Creazione di un client Forms e Signatures

   * Creare un `SignatureServiceClient` utilizzando il costruttore predefinito.
   * Creare un `SignatureServiceClient.Endpoint.Address` oggetto utilizzando `System.ServiceModel.EndpointAddress` costruttore. Passa un valore stringa che specifica il file WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/SignatureService?WSDL`). Non è necessario utilizzare il `lc_version` attributo. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Creare un `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto ottenendo il valore del `SignatureServiceClient.Endpoint.Binding` campo. Invia il valore restituito a `BasicHttpBinding`.
   * Imposta il `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegna al campo il nome utente dei moduli AEM `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore password corrispondente al campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

   >[!NOTE]
   >
   >Ripetere questi passaggi per il client del servizio Forms.

1. Ottenere il modulo interattivo utilizzando il servizio Forms

   * Creare un `BLOB` mediante il costruttore. Il `BLOB` L&#39;oggetto viene utilizzato per memorizzare un documento PDF firmato.
   * Creare un `System.IO.FileStream` richiamando il costruttore e passando un valore stringa che rappresenta la posizione del file del documento PDF da firmare e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto della `System.IO.FileStream` oggetto. È possibile determinare le dimensioni della matrice di byte ottenendo `System.IO.FileStream` dell&#39;oggetto `Length` proprietà.
   * Compilare la matrice di byte con i dati di flusso richiamando `System.IO.FileStream` dell&#39;oggetto `Read` e passando la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare il `BLOB` oggetto assegnando il relativo `MTOM` proprietà il contenuto della matrice di byte.
   * Creare un `BLOB` mediante il costruttore. Il `BLOB` L&#39;oggetto viene utilizzato per memorizzare i dati del modulo.
   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore stringa che rappresenta la posizione del file XML contenente i dati del modulo e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto della `System.IO.FileStream` oggetto. È possibile determinare le dimensioni della matrice di byte ottenendo `System.IO.FileStream` dell&#39;oggetto `Length` proprietà.
   * Compilare la matrice di byte con i dati di flusso richiamando `System.IO.FileStream` dell&#39;oggetto `Read` e passando la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare il `BLOB` oggetto assegnando il relativo `MTOM` proprietà il contenuto della matrice di byte.
   * Creare un `PDFFormRenderSpec` oggetto utilizzato per impostare le opzioni di runtime. Assegna il valore `true` al `PDFFormRenderSpec` dell&#39;oggetto `generateServerAppearance` campo.
   * Richiama `FormsServiceClient` dell&#39;oggetto `renderPDFForm2` e trasmettere i seguenti valori:

      * A `BLOB` oggetto che contiene il modulo PDF da riprodurre.
      * A `BLOB` oggetto contenente dati da unire con il modulo.
      * A `PDFFormRenderSpec` oggetto che memorizza le opzioni di runtime.
      * A `URLSpec` oggetto contenente valori URI richiesti dal servizio Forms. È possibile specificare `null` per questo valore di parametro.
      * A `java.util.HashMap` oggetto che memorizza gli allegati. Questo è un parametro facoltativo e puoi specificare `null` se non si desidera allegare file al modulo.
      * Parametro di output lungo utilizzato per memorizzare il numero di pagine nel modulo.
      * Parametro di output stringa utilizzato per il valore locale.
      * A `FormResult` valore che è un parametro di output utilizzato per memorizzare il modulo interattivo.

   * Recuperare il modulo PDF richiamando `FormsResult` dell&#39;oggetto `outputContent` campo. Questo campo memorizza una `BLOB` oggetto che rappresenta il modulo interattivo.

1. Firma il modulo interattivo

   Firma il documento PDF richiamando `SignatureServiceClient` dell&#39;oggetto `sign` e fornendo i seguenti valori:

   * A `BLOB` oggetto che rappresenta il documento PDF da firmare. Utilizza il `BLOB` istanza restituita dal servizio Forms.
   * Valore stringa che rappresenta il nome del campo firma firmato.
   * A `Credential` oggetto che rappresenta le credenziali utilizzate per apporre una firma digitale al documento PDF. Creare un `Credential` mediante il costruttore e specificare l&#39;alias assegnando un valore al `Credential` dell&#39;oggetto `alias` proprietà.
   * A `HashAlgorithm` oggetto che specifica un membro dati statico che rappresenta l&#39;algoritmo hash da utilizzare per digerire il documento PDF. Ad esempio, puoi specificare `HashAlgorithm.SHA1` per utilizzare l’algoritmo SHA1.
   * Un valore booleano che specifica se viene utilizzato l’algoritmo hash.
   * Valore stringa che rappresenta il motivo per cui il documento PDF è stato firmato digitalmente.
   * Valore stringa che rappresenta la posizione del firmatario.
   * Valore stringa che rappresenta le informazioni di contatto del firmatario.
   * A `PDFSignatureAppearanceOptions` oggetto che controlla l&#39;aspetto della firma digitale. È ad esempio possibile utilizzare questo oggetto per aggiungere un logo personalizzato a una firma digitale.
   * A `System.Boolean` oggetto che specifica se eseguire il controllo di revoca sul certificato del firmatario. Se la verifica della revoca viene eseguita, viene incorporata nella firma. Il valore predefinito è `false`.
   * Un `OCSPPreferences` oggetto che memorizza le preferenze per il supporto del protocollo OCSP (Online Certificate Status Protocol). Se non viene eseguito il controllo della revoca, questo parametro non viene utilizzato ed è possibile specificare `null`. Per informazioni su questo oggetto, vedi [Riferimento API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * A `CRLPreferences` oggetto che memorizza le preferenze dell&#39;elenco di revoche di certificati (CRL). Se non viene eseguito il controllo della revoca, questo parametro non viene utilizzato ed è possibile specificare `null`.
   * A `TSPPreferences` oggetto che memorizza le preferenze per il supporto del provider di marca temporale (TSP). Questo parametro è facoltativo e può essere `null`.

   Il `sign` il metodo restituisce un `BLOB` oggetto che rappresenta il documento PDF firmato.

1. Salva il documento PDF firmato

   * Creare un `System.IO.FileStream` richiamando il relativo costruttore. Passa un valore stringa che rappresenta la posizione del file del documento PDF firmato e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto della `BLOB` oggetto restituito da `sign` metodo. Popolare la matrice di byte ottenendo il valore della `BLOB` dell&#39;oggetto `MTOM` membro dati.
   * Creare un `System.IO.BinaryWriter` oggetto richiamando il relativo costruttore e passando il `System.IO.FileStream` oggetto.
   * Scrivere il contenuto della matrice di byte in un file PDF richiamando `System.IO.BinaryWriter` dell&#39;oggetto `Write` e passando la matrice di byte.

**Consulta anche**

[Forms interattivo con firma digitale](digitally-signing-certifying-documents.md#digitally-signing-interactive-forms)

[Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## Certificazione dei documenti di PDF {#certifying-pdf-documents}

È possibile proteggere un documento PDF certificandolo con un tipo particolare di firma, denominata firma certificata. Una firma certificata si distingue da una firma digitale nei seguenti modi:

* Deve essere la prima firma applicata al documento PDF, ovvero, al momento dell&#39;applicazione della firma certificata, tutti gli altri campi della firma presenti nel documento devono essere non firmati. In un documento PDF è consentita una sola firma certificata. Se si desidera firmare e certificare un documento PDF, è necessario certificarlo prima di firmarlo. Dopo aver certificato un documento PDF, è possibile firmare digitalmente ulteriori campi di firma.
* L&#39;autore o l&#39;originatore del documento può specificare che il documento può essere modificato in alcuni modi senza invalidare la firma certificata. Ad esempio, il documento può consentire la compilazione di moduli o la creazione di commenti. Se l’autore specifica che una determinata modifica non è consentita, Acrobat impedisce agli utenti di modificare il documento in questo modo. Se vengono apportate tali modifiche, ad esempio utilizzando un’altra applicazione, la firma certificata non è valida e Acrobat genera un avviso quando un utente apre il documento. Con le firme non certificate, le modifiche non vengono impedite e le normali operazioni di modifica non invalidano la firma originale.
* Al momento della firma, il documento viene analizzato per individuare tipi specifici di contenuto che potrebbero rendere ambiguo o fuorviante il contenuto di un documento. Ad esempio, un’annotazione potrebbe oscurare del testo su una pagina importante per comprendere cosa viene certificato. Su tale contenuto può essere fornita una spiegazione (attestazione legale).

Puoi certificare i documenti di PDF a livello di programmazione utilizzando l’API Java di Signature Service o l’API del servizio web di Signature. Quando si certifica un documento PDF, è necessario fare riferimento a una credenziale di protezione esistente nel servizio Credenziali. Per informazioni sulle credenziali di protezione, vedere *Installazione e distribuzione di AEM Forms* per il server applicazioni.

>[!NOTE]
>
>Quando si certifica e firma lo stesso documento PDF, se la firma di certificazione non è attendibile, accanto alla prima firma viene visualizzato un triangolo giallo quando si apre il documento PDF in Acrobat o Adobe Reader. La firma di certificazione deve essere attendibile per evitare questa situazione.

>[!NOTE]
>
>Quando si utilizza una credenziale HSM nShield di crittografia per firmare o certificare un documento PDF, non è possibile utilizzare la nuova credenziale fino al riavvio del server applicazioni J2EE in cui viene distribuito AEM Forms. Tuttavia, è possibile impostare un valore di configurazione, in modo che l&#39;operazione di firma o di certificazione funzioni senza riavviare il server applicazioni J2EE.

È possibile aggiungere il seguente valore di configurazione nel file cknfastrc, che si trova in /opt/nfast/cknfastrc (o c:\nfast\cknfastrc):

```shell
    CKNFAST_ASSUME_SINGLE_PROCESS=0
```

Dopo aver aggiunto questo valore di configurazione al file cknfastrc, è possibile utilizzare le nuove credenziali senza riavviare il server applicazioni J2EE.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio di firma e sulla certificazione di un documento, vedere [Guida di riferimento dei servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-5}

Per certificare un documento PDF, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Creare un client di firma.
1. Ottieni il documento PDF da certificare.
1. Certifica il documento PDF.
1. Salvare il documento PDF certificato come file PDF.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è implementato su JBoss)
* jbossall-client.jar (obbligatorio se AEM Forms è distribuito su JBoss)

Per informazioni sulla posizione di questi file JAR, vedi [Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un client di firma**

Prima di poter eseguire un&#39;operazione di firma a livello di programmazione, è necessario creare un client di firma.

**Ottieni il documento PDF da certificare**

Per certificare un documento di PDF, è necessario ottenere un documento di PDF contenente un campo firma. Se un documento PDF non contiene un campo firma, non può essere certificato. È possibile aggiungere un campo firma utilizzando Designer o a livello di programmazione. Per informazioni sull&#39;aggiunta a livello di programmazione di un campo di firma, vedere [Aggiunta di campi firma](digitally-signing-certifying-documents.md#adding-signature-fields).

**Certifica il documento PDF**

Per certificare un documento PDF, è necessario disporre dei seguenti valori di input utilizzati dal servizio di firma per certificare un documento PDF:

* **documento PDF**: documento PDF che contiene un campo firma, ovvero un campo modulo contenente una rappresentazione grafica della firma certificata. Un documento PDF deve contenere un campo firma prima di poter essere certificato. È possibile aggiungere un campo firma utilizzando Designer o a livello di programmazione. (vedere [Aggiunta di campi firma](digitally-signing-certifying-documents.md#adding-signature-fields).)
* **Nome campo firma**: nome completo del campo della firma certificato. Il seguente valore è un esempio: `form1[0].#subform[1].SignatureField3[3]`. Quando si utilizza un campo modulo XFA, è possibile utilizzare anche il nome parziale del campo firma: `SignatureField3[3]`. Se viene passato un valore nullo per il nome del campo, viene creato e certificato dinamicamente un campo di firma invisibile.
* **Credenziali di sicurezza**: credenziale utilizzata per certificare il documento PDF. Questa credenziale di protezione contiene una password e un alias, che devono corrispondere a un alias visualizzato nella credenziale che si trova nel servizio Credenziale. L’alias è un riferimento a una credenziale effettiva che può trovarsi in un file PKCS#12 (con estensione .pfx) o in un modulo di sicurezza hardware (HSM).
* **Algoritmo hash**: algoritmo hash da utilizzare per assimilare il documento PDF.
* **Motivo della firma**: valore visualizzato in Acrobat o Adobe Reader in modo che gli altri utenti conoscano il motivo per cui il documento PDF è stato certificato.
* **Posizione del firmatario**: posizione del firmatario specificata dalle credenziali.
* **Informazioni di contatto**: informazioni di contatto del firmatario, come indirizzo e numero di telefono.
* **Informazioni autorizzazione**: autorizzazioni che controllano le azioni che un utente finale può eseguire su un documento senza che la firma certificata risulti non valida. È ad esempio possibile impostare l&#39;autorizzazione in modo che qualsiasi modifica apportata al documento PDF provochi la mancata validità della firma certificata.
* **Spiegazione legale**: quando un documento viene certificato, viene automaticamente analizzato per individuare tipi specifici di contenuto che potrebbero rendere ambiguo o fuorviante il contenuto di un documento. Ad esempio, un’annotazione potrebbe oscurare del testo su una pagina importante per comprendere cosa viene certificato. Il processo di scansione genera avvisi su questi tipi di contenuto. Questo valore fornisce una spiegazione aggiuntiva del contenuto che potrebbe aver generato avvisi.
* **Opzioni di aspetto**: opzioni che controllano l&#39;aspetto della firma certificata. Ad esempio, la firma certificata può visualizzare informazioni sulla data.
* **Verifica della revoca**: questo valore specifica se viene eseguito il controllo di revoca per il certificato del firmatario. Impostazione predefinita di `false` significa che non è stato eseguito il controllo di revoca.
* **Impostazioni OCSP**: impostazioni per il supporto del protocollo OCSP (Online Certificate Status Protocol), che fornisce informazioni sullo stato delle credenziali utilizzate per certificare il documento PDF. È possibile, ad esempio, specificare l&#39;URL del server che fornisce informazioni sulle credenziali utilizzate per accedere al documento PDF.
* **Impostazioni CRL**: impostazioni per le preferenze dell’elenco di revoche di certificati (CRL) se viene eseguito il controllo della revoca. Ad esempio, è possibile specificare di controllare sempre se una credenziale è stata revocata.
* **Marca temporale**: impostazioni che definiscono le informazioni di marca temporale applicate alla firma certificata. Una marca temporale indica che dati specifici sono stati stabiliti prima di un certo periodo di tempo. Questa conoscenza consente di creare una relazione di affidabilità tra il firmatario e il verificatore.

**Salvare il documento PDF certificato come file PDF**

Dopo che il servizio di firma ha certificato il documento PDF, è possibile salvarlo come file PDF in modo che gli utenti possano aprirlo in Acrobat o Adobe Reader.

**Consulta anche**

[Certifica i documenti di PDF utilizzando l’API Java](digitally-signing-certifying-documents.md#certify-pdf-documents-using-the-java-api)

[Certifica i documenti di PDF utilizzando l’API del servizio web](digitally-signing-certifying-documents.md#certify-pdf-documents-using-the-web-service-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Aggiunta di campi firma](digitally-signing-certifying-documents.md#adding-signature-fields)

### Certifica i documenti di PDF utilizzando l’API Java {#certify-pdf-documents-using-the-java-api}

Certifica un documento PDF utilizzando Signature API (Java):

1. Includi file di progetto

   Includi i file JAR dei client, ad esempio adobe-signatures-client.jar, nel percorso di classe del progetto Java.

1. Creare un client di firma

   * Creare un `ServiceClientFactory` oggetto che contiene proprietà di connessione.
   * Creare un `SignatureServiceClient` mediante il costruttore e passando il `ServiceClientFactory` oggetto.

1. Ottieni il documento PDF da certificare

   * Creare un `java.io.FileInputStream` oggetto che rappresenta il documento PDF da certificare utilizzando il relativo costruttore e passando un valore stringa che specifica la posizione del documento PDF.
   * Creare un `com.adobe.idp.Document` mediante il costruttore e passando il `java.io.FileInputStream` oggetto.

1. Certifica il documento PDF

   Certifica il documento del PDF richiamando `SignatureServiceClient` dell&#39;oggetto `certify` e fornendo i seguenti valori:

   * Il `com.adobe.idp.Document` oggetto che rappresenta il documento PDF da certificare.
   * Valore stringa che rappresenta il nome del campo firma che conterrà la firma.
   * A `Credential` oggetto che rappresenta le credenziali utilizzate per certificare il documento PDF. Creare un `Credential` oggetto richiamando il `Credential` statico dell&#39;oggetto `getInstance` e passando un valore stringa che specifica il valore di alias corrispondente alle credenziali di sicurezza.
   * A `HashAlgorithm` oggetto che specifica un membro dati statico che rappresenta l&#39;algoritmo hash utilizzato per digerire il documento PDF. Ad esempio, puoi specificare `HashAlgorithm.SHA1` per utilizzare l’algoritmo SHA1.
   * Valore stringa che rappresenta il motivo per cui il documento PDF è stato certificato.
   * Valore stringa che rappresenta le informazioni di contatto del firmatario.
   * A `MDPPermissions` oggetto che specifica le azioni che possono essere eseguite sul documento PDF che invalidano la firma.
   * A `PDFSignatureAppearanceOptions` oggetto che controlla l&#39;aspetto della firma certificata. Se necessario, modificare l&#39;aspetto della firma richiamando un metodo, ad esempio `setShowDate`.
   * Valore stringa che fornisce una spiegazione delle azioni che invalidano la firma.
   * A `java.lang.Boolean` oggetto che specifica se eseguire il controllo di revoca sul certificato del firmatario. Se la verifica della revoca viene eseguita, viene incorporata nella firma. Il valore predefinito è `false`.
   * A `java.lang.Boolean` oggetto che specifica se il campo firma da certificare è bloccato. Se il campo è bloccato, il campo firma viene contrassegnato come di sola lettura, le relative proprietà non possono essere modificate e non possono essere cancellate da utenti che non dispongono delle autorizzazioni necessarie. Il valore predefinito è `false`.
   * Un `OCSPPreferences` oggetto che memorizza le preferenze per il supporto del protocollo OCSP (Online Certificate Status Protocol). Se non viene eseguito il controllo della revoca, questo parametro non viene utilizzato ed è possibile specificare `null`. Per informazioni su questo oggetto, vedere [Riferimento API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * A `CRLPreferences` oggetto che memorizza le preferenze dell&#39;elenco di revoche di certificati (CRL). Se non viene eseguito il controllo della revoca, questo parametro non viene utilizzato ed è possibile specificare `null`.
   * A `TSPPreferences` oggetto che memorizza le preferenze per il supporto del provider di marca temporale (TSP). Ad esempio, dopo aver creato un’ `TSPPreferences` dell&#39;oggetto, è possibile impostare l&#39;URL del server TSP richiamando `TSPPreferences` dell&#39;oggetto `setTspServerURL` metodo. Questo parametro è facoltativo e può essere `null`. Per ulteriori informazioni, consulta [Guida di riferimento dei servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

   Il `certify` il metodo restituisce un `com.adobe.idp.Document` oggetto che rappresenta il documento PDF certificato.

1. Salvare il documento PDF certificato come file PDF

   * Creare un `java.io.File` e assicurarsi che l&#39;estensione del file sia .pdf.
   * Richiama `com.adobe.idp.Document` dell&#39;oggetto `copyToFile` metodo per copiare il contenuto del `com.adobe.idp.Document` al file.

**Consulta anche**

[Certificazione dei documenti di PDF](digitally-signing-certifying-documents.md#certifying-pdf-documents)

[Quick Start (modalità SOAP): certificazione di un documento PDF tramite l’API Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-certifying-a-pdf-document-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Certifica i documenti di PDF utilizzando l’API del servizio web {#certify-pdf-documents-using-the-web-service-api}

Certifica un documento PDF utilizzando l’API di firma (servizio web):

1. Includi file di progetto

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l’indirizzo IP del server che ospita AEM Forms.

1. Creare un client di firma

   * Creare un `SignatureServiceClient` utilizzando il costruttore predefinito.
   * Creare un `SignatureServiceClient.Endpoint.Address` oggetto utilizzando `System.ServiceModel.EndpointAddress` costruttore. Passa un valore stringa che specifica il file WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/SignatureService?WSDL`). Non è necessario utilizzare il `lc_version` attributo. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Creare un `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto ottenendo il valore del `SignatureServiceClient.Endpoint.Binding` campo. Invia il valore restituito a `BasicHttpBinding`.
   * Imposta il `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegna al campo il nome utente dei moduli AEM `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore password corrispondente al campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Ottieni il documento PDF da certificare

   * Creare un `BLOB` mediante il costruttore. Il `BLOB` L&#39;oggetto viene utilizzato per memorizzare un documento PDF certificato.
   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore stringa che rappresenta la posizione del file del documento PDF da certificare e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto della `System.IO.FileStream` oggetto. È possibile determinare le dimensioni della matrice di byte ottenendo `System.IO.FileStream` dell&#39;oggetto `Length` proprietà.
   * Compilare la matrice di byte con i dati di flusso richiamando `System.IO.FileStream` dell&#39;oggetto `Read` e passando la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare il `BLOB` oggetto assegnando il relativo `MTOM` membro dati il contenuto della matrice di byte.

1. Certifica il documento PDF

   Certifica il documento del PDF richiamando `SignatureServiceClient` dell&#39;oggetto `certify` e fornendo i seguenti valori:

   * Il `BLOB` oggetto che rappresenta il documento PDF da certificare.
   * Valore stringa che rappresenta il nome del campo firma che conterrà la firma.
   * A `Credential` oggetto che rappresenta le credenziali utilizzate per certificare il documento PDF. Creare un `Credential` mediante il costruttore e specificare l&#39;alias assegnando un valore al `Credential` dell&#39;oggetto `alias` proprietà.
   * A `HashAlgorithm` oggetto che specifica un membro dati statico che rappresenta l&#39;algoritmo hash utilizzato per digerire il documento PDF. Ad esempio, puoi specificare `HashAlgorithm.SHA1` per utilizzare l’algoritmo SHA1.
   * Un valore booleano che specifica se viene utilizzato l’algoritmo hash.
   * Valore stringa che rappresenta il motivo per cui il documento PDF è stato certificato.
   * Valore stringa che rappresenta la posizione del firmatario.
   * Valore stringa che rappresenta le informazioni di contatto del firmatario.
   * Un `MDPPermissions` membro dati statico dell&#39;oggetto che specifica le azioni che possono essere eseguite sul documento PDF che invalidano la firma.
   * Un valore booleano che specifica se utilizzare `MDPPermissions` oggetto passato come valore del parametro precedente.
   * Valore stringa che spiega quali azioni invalidano la firma.
   * A `PDFSignatureAppearanceOptions` oggetto che controlla l&#39;aspetto della firma certificata. Creare un `PDFSignatureAppearanceOptions` mediante il costruttore. È possibile modificare l&#39;aspetto della firma impostandone uno dei membri dati.
   * A `System.Boolean` oggetto che specifica se eseguire il controllo di revoca sul certificato del firmatario. Se la verifica della revoca viene eseguita, viene incorporata nella firma. Il valore predefinito è `false`.
   * A `System.Boolean` oggetto che specifica se il campo firma da certificare è bloccato. Se il campo è bloccato, il campo firma viene contrassegnato come di sola lettura, le relative proprietà non possono essere modificate e non possono essere cancellate da utenti che non dispongono delle autorizzazioni necessarie. Il valore predefinito è `false`.
   * A `System.Boolean` oggetto che specifica se il campo firma è bloccato. Cioè, se passi `true` al parametro precedente, quindi passa `true` a questo parametro.
   * Un `OCSPPreferences` oggetto che memorizza le preferenze per il supporto del protocollo OCSP (Online Certificate Status Protocol), che fornisce informazioni sullo stato delle credenziali utilizzate per certificare il documento PDF. Se non viene eseguito il controllo della revoca, questo parametro non viene utilizzato ed è possibile specificare `null`.
   * A `CRLPreferences` oggetto che memorizza le preferenze dell&#39;elenco di revoche di certificati (CRL). Se non viene eseguito il controllo della revoca, questo parametro non viene utilizzato ed è possibile specificare `null`.
   * A `TSPPreferences` oggetto che memorizza le preferenze per il supporto del provider di marca temporale (TSP). Ad esempio, dopo aver creato un’ `TSPPreferences` , è possibile impostare l&#39;URL del TSP impostando il `TSPPreferences` dell&#39;oggetto `tspServerURL` membro dati. Questo parametro è facoltativo e può essere `null`.

   Il `certify` il metodo restituisce un `BLOB` oggetto che rappresenta il documento PDF certificato.

1. Salvare il documento PDF certificato come file PDF

   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore stringa che rappresenta la posizione del file del documento PDF che conterrà il documento PDF certificato e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto della `BLOB` oggetto restituito da `certify` metodo. Popolare la matrice di byte ottenendo il valore della `BLOB` dell&#39;oggetto `binaryData` membro dati.
   * Creare un `System.IO.BinaryWriter` oggetto richiamando il relativo costruttore e passando il `System.IO.FileStream` oggetto.
   * Scrivere il contenuto della matrice di byte in un file PDF richiamando `System.IO.BinaryWriter` dell&#39;oggetto `Write` e passando la matrice di byte.

**Consulta anche**

[Certificazione dei documenti di PDF](digitally-signing-certifying-documents.md#certifying-pdf-documents)

[Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamare AEM Forms con SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Verifica delle firme digitali {#verifying-digital-signatures}

PDF È possibile verificare che le firme digitali non siano state modificate e che la firma digitale sia valida. Durante la verifica di una firma digitale, è possibile controllare lo stato della firma e le relative proprietà, ad esempio l&#39;identità del firmatario. Prima di considerare attendibile una firma digitale, è consigliabile verificarla. Durante la verifica di una firma digitale, fare riferimento a un documento PDF contenente una firma digitale.

Supponiamo che l’identità del firmatario sia sconosciuta. Quando apri il documento PDF in Acrobat, un messaggio di avviso indica che l’identità del firmatario è sconosciuta, come illustrato nella figura seguente.

![vd_vd_verifysig](assets/vd_vd_verifysig.png)

Analogamente, quando si verifica una firma digitale a livello di programmazione, è possibile determinare lo stato dell&#39;identità del firmatario. Se ad esempio si verifica la firma digitale nel documento illustrato nell&#39;illustrazione precedente, l&#39;identità del firmatario risulterà sconosciuta.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Firma e sulla verifica delle firme digitali, vedere [Guida di riferimento dei servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-6}

Per verificare una firma digitale, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Creare un client di firma.
1. Ottiene il documento PDF contenente la firma da verificare.
1. Impostare le opzioni di runtime della PKI.
1. Verificare la firma digitale.
1. Determinare lo stato della firma.
1. Determina l’identità del firmatario.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se si utilizzano servizi Web, includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è implementato su JBoss)
* jbossall-client.jar (obbligatorio se AEM Forms è distribuito su JBoss)

Per informazioni sulla posizione di questi file JAR, vedi [Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un client di firma**

Prima di eseguire un&#39;operazione del servizio di firma a livello di programmazione, creare un client del servizio.

**Ottieni il documento PDF contenente la firma da verificare**

Per verificare una firma utilizzata per firmare o certificare digitalmente un documento PDF, ottenere un documento PDF contenente una firma.

**Impostare le opzioni di runtime della PKI**

Impostare le seguenti opzioni di runtime PKI utilizzate dal servizio di firma per la verifica delle firme in un documento PDF:

* Tempo di verifica
* Verifica della revoca
* Valori di marca temporale

L&#39;impostazione di queste opzioni consente di specificare il tempo di verifica. Ad esempio, è possibile selezionare l&#39;ora corrente (l&#39;ora nel computer del validatore), che indica di utilizzare l&#39;ora corrente. Per informazioni sui diversi valori di tempo, vedere `VerificationTime` valore di enumerazione in [Riferimento API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

È inoltre possibile specificare se eseguire il controllo di revoca come parte del processo di verifica. È ad esempio possibile eseguire un controllo di revoca per determinare se il certificato è stato revocato. Per informazioni sulle opzioni di controllo della revoca, vedere `RevocationCheckStyle` valore di enumerazione in [Riferimento API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

Per eseguire il controllo di revoca su un certificato, specificare un URL di un server di elenco di revoche di certificati (CRL) utilizzando un `CRLOptionSpec` oggetto. Tuttavia, se non si specifica un URL per il server CRL, il servizio di firma ottiene l&#39;URL dal certificato.

Anziché utilizzare un server CRL, è possibile utilizzare un server OCSP (Certificate Status Protocol) online durante la verifica della revoca. In genere, quando si utilizza un server OCSP anziché un server CRL, il controllo di revoca viene eseguito più rapidamente. (vedere [Protocollo per lo stato dei certificati online](https://tools.ietf.org/html/rfc2560).)

È possibile impostare l&#39;ordine dei server CRL e OCSP utilizzato dal servizio di firma utilizzando Adobe Applications and Services. Se, ad esempio, il server OCSP è impostato prima in Adobe Applications and Services, viene selezionato il server OCSP, seguito dal server CRL.

Se non si esegue il controllo della revoca, il servizio di firma non verifica se il certificato è stato revocato. In altre parole, le informazioni del server CRL e OCSP vengono ignorate.

>[!NOTE]
>
>Puoi sovrascrivere l’URL specificato nel certificato utilizzando un’ `CRLOptionSpec` e un `OCSPOptionSpec` oggetto. Ad esempio, per ignorare il server CRL, puoi richiamare `CRLOptionSpec` dell&#39;oggetto `setLocalURI` metodo.

La marca temporale è il processo di registrazione dell&#39;ora in cui un documento firmato o certificato è stato modificato. Dopo aver firmato un documento, nessuno può modificarlo. La marca temporale consente di applicare la validità di un documento firmato o certificato. È possibile impostare le opzioni di marca temporale utilizzando un `TSPOptionSpec` oggetto. Ad esempio, puoi specificare l’URL di un server provider di marca temporale (TSP).

>[!NOTE]
>
>Nei servizi Java e web di avvio rapido, il tempo di verifica è impostato su `VerificationTime.CURRENT_TIME` e la verifica della revoca è impostata su `RevocationCheckStyle.BestEffort`. Poiché non vengono specificate informazioni sul server CRL o OCSP, le informazioni sul server vengono ottenute dal certificato.

**Verificare la firma digitale**

Per verificare correttamente una firma, specificare il nome completo del campo firma che contiene la firma, ad esempio `form1[0].#subform[1].SignatureField3[3]`. Quando si utilizza un campo modulo XFA, è inoltre possibile utilizzare il nome parziale del campo firma: `SignatureField3`.

Per impostazione predefinita, il servizio di firma limita a 65 minuti la durata della firma di un documento dopo il periodo di convalida. Se un utente tenta di verificare una firma all’ora corrente e l’ora della firma è successiva all’ora corrente ed è compresa entro 65 minuti, il servizio di firma non crea un errore di verifica.

>[!NOTE]
>
>Per altri valori necessari per la verifica di una firma, vedere [Riferimento API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Determinare lo stato della firma**

Durante la verifica di una firma digitale è possibile controllare lo stato della firma.

**Determinare l’identità del firmatario**

Puoi determinare l’identità del firmatario, che può corrispondere a uno dei seguenti valori:

* **Sconosciuto**: firmatario sconosciuto. Impossibile eseguire la verifica del firmatario.
* **Attendibile**: firmatario attendibile.
* **Non attendibile**: firmatario non attendibile.

**Consulta anche**

[Verificare le firme digitali tramite API Java](#verify-digital-signatures-using-the-java-api)

[Verificare le firme digitali utilizzando l’API del servizio web](#verify-digital-signatures-using-the-web-service-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Verificare le firme digitali tramite API Java {#verify-digital-signatures-using-the-java-api}

Verifica una firma digitale utilizzando l’API Signature Service (Java):

1. Includi file di progetto

   Includi i file JAR dei client, ad esempio adobe-signatures-client.jar, nel percorso di classe del progetto Java.

1. Creare un client di firma

   * Creare un `ServiceClientFactory` oggetto che contiene proprietà di connessione.
   * Creare un `SignatureServiceClient` mediante il costruttore e passando il `ServiceClientFactory` oggetto.

1. Ottieni il documento PDF contenente la firma da verificare

   * Creare un `java.io.FileInputStream` oggetto che rappresenta il documento PDF che contiene la firma da verificare utilizzando il relativo costruttore. Passa un valore stringa che specifica la posizione del documento PDF.
   * Creare un `com.adobe.idp.Document` mediante il costruttore e passando il `java.io.FileInputStream` oggetto.

1. Impostare le opzioni di runtime della PKI

   * Creare un `PKIOptions` mediante il costruttore.
   * Impostare l&#39;ora di verifica richiamando `PKIOptions` dell&#39;oggetto `setVerificationTime` e il passaggio di un `VerificationTime` valore di enumerazione che specifica il tempo di verifica.
   * Impostare l&#39;opzione di verifica della revoca richiamando `PKIOptions` dell&#39;oggetto `setRevocationCheckStyle` e il passaggio di un `RevocationCheckStyle` valore di enumerazione che specifica se eseguire il controllo di revoca.

1. Verificare la firma digitale

   Verificare la firma richiamando `SignatureServiceClient` dell&#39;oggetto `verify2` e fornendo i seguenti valori:

   * A `com.adobe.idp.Document` oggetto contenente un documento PDF con firma digitale o certificato.
   * Valore stringa che rappresenta il nome del campo della firma contenente la firma da verificare.
   * A `PKIOptions` oggetto contenente le opzioni di runtime della PKI.
   * A `VerifySPIOptions` istanza che contiene informazioni SPI. È possibile specificare `null` per questo parametro.

   Il `verify2` il metodo restituisce un `PDFSignatureVerificationInfo` oggetto contenente informazioni che possono essere utilizzate per verificare la firma digitale.

1. Determinare lo stato della firma

   * Determinare lo stato della firma richiamando `PDFSignatureVerificationInfo` dell&#39;oggetto `getStatus` metodo. Questo metodo restituisce un `SignatureStatus` oggetto che specifica lo stato della firma. Se, ad esempio, un documento PDF firmato non viene modificato, questo metodo restituisce `SignatureStatus.DocumentSigNoChanges`.

1. Determinare l’identità del firmatario

   * Determinare l’identità del firmatario richiamando `PDFSignatureVerificationInfo` dell&#39;oggetto `getSigner` metodo. Questo metodo restituisce un `IdentityInformation` oggetto.
   * Richiama `IdentityInformation` dell&#39;oggetto `getStatus` metodo per determinare l’identità del firmatario. Questo metodo restituisce un `IdentityStatus` valore di enumerazione che specifica l&#39;identità. Ad esempio, se il firmatario è attendibile, questo metodo restituisce `IdentityStatus.TRUSTED`.

**Consulta anche**

[Verifica delle firme digitali](#verify-digital-signatures-using-the-java-api)

[Quick Start (modalità SOAP): verifica di una firma digitale tramite l’API Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-verifying-a-digital-signature-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Verificare le firme digitali utilizzando l’API del servizio web {#verify-digital-signatures-using-the-web-service-api}

Verifica una firma digitale utilizzando l’API del servizio di firma (servizio web):

1. Includi file di progetto

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l’indirizzo IP del server che ospita AEM Forms.

1. Creare un client di firma

   * Creare un `SignatureServiceClient` utilizzando il costruttore predefinito.
   * Creare un `SignatureServiceClient.Endpoint.Address` oggetto utilizzando `System.ServiceModel.EndpointAddress` costruttore. Passa un valore stringa che specifica il file WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/SignatureService?WSDL`). Non è necessario utilizzare il `lc_version` attributo. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Creare un `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto ottenendo il valore del `SignatureServiceClient.Endpoint.Binding` campo. Invia il valore restituito a `BasicHttpBinding`.
   * Imposta il `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegna al campo il nome utente dei moduli AEM `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore password corrispondente al campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Ottieni il documento PDF contenente la firma da verificare

   * Creare un `BLOB` mediante il costruttore. Il `BLOB` L&#39;oggetto viene utilizzato per memorizzare un documento PDF contenente una firma digitale o certificata da verificare.
   * Creare un `System.IO.FileStream` richiamando il relativo costruttore. Passa un valore stringa che rappresenta la posizione del file del documento PDF firmato e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto della `System.IO.FileStream` oggetto. È possibile determinare le dimensioni della matrice di byte ottenendo `System.IO.FileStream` dell&#39;oggetto `Length` proprietà.
   * Compilare la matrice di byte con i dati di flusso richiamando `System.IO.FileStream` dell&#39;oggetto `Read` metodo. Passare la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare il `BLOB` oggetto assegnando il relativo `MTOM` proprietà il contenuto della matrice di byte.

1. Impostare le opzioni di runtime della PKI

   * Creare un `PKIOptions` mediante il costruttore.
   * Impostare l&#39;ora di verifica assegnando `PKIOptions` dell&#39;oggetto `verificationTime` membro dati a `VerificationTime` valore di enumerazione che specifica il tempo di verifica.
   * Impostare l&#39;opzione di controllo delle revoche assegnando `PKIOptions` dell&#39;oggetto `revocationCheckStyle` membro dati a `RevocationCheckStyle` valore di enumerazione che specifica se eseguire il controllo di revoca.

1. Verificare la firma digitale

   Verificare la firma richiamando `SignatureServiceClient` dell&#39;oggetto `verify2` e fornendo i seguenti valori:

   * Il `BLOB` oggetto contenente un documento PDF con firma digitale o certificato.
   * Valore stringa che rappresenta il nome del campo della firma contenente la firma da verificare.
   * A `PKIOptions` oggetto contenente le opzioni di runtime della PKI.
   * A `VerifySPIOptions` istanza che contiene informazioni SPI. È possibile specificare `null` per questo parametro.

   Il `verify2` il metodo restituisce un `PDFSignatureVerificationInfo` oggetto contenente informazioni che possono essere utilizzate per verificare la firma digitale.

1. Determinare lo stato della firma

   Determinare lo stato della firma ottenendo il valore del `PDFSignatureVerificationInfo` dell&#39;oggetto `status` membro dati. Questo membro dati memorizza un `SignatureStatus` oggetto che specifica lo stato della firma. Se, ad esempio, viene modificato un documento PDF firmato, il `status` il membro dati memorizza il valore `SignatureStatus.DocumentSigNoChanges`.

1. Determinare l’identità del firmatario

   * Determinare l’identità del firmatario recuperando il valore del `PDFSignatureVerificationInfo` dell&#39;oggetto `signer` membro dati. Questo membro restituisce un `IdentityInformation` oggetto.
   * Recupera il `IdentityInformation` dell&#39;oggetto `status` membro dati per determinare l&#39;identità del firmatario. Questo membro dati restituisce un `IdentityStatus` valore di enumerazione che specifica l&#39;identità. Ad esempio, se il firmatario è attendibile, questo membro restituisce `IdentityStatus.TRUSTED`.

**Consulta anche**

[Verifica delle firme digitali](#verify-digital-signatures-using-the-java-api)

[Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamare AEM Forms con SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Verifica di più firme digitali {#verifying-multiple-digital-signatures}

AEM Forms fornisce i mezzi per verificare tutte le firme digitali presenti in un documento PDF. Si supponga che un documento PDF contenga più firme digitali come risultato di un processo aziendale che richiede firme da più firmatari. Ad esempio, si consideri una transazione finanziaria che richiede la firma sia di un addetto al prestito che di un manager. È possibile utilizzare l’API Java di Signature Service o l’API del servizio Web per verificare tutte le firme all’interno del documento PDF. Quando si verificano più firme digitali, è possibile controllare lo stato e le proprietà di ogni firma. Prima di considerare attendibile una firma digitale, è consigliabile verificarla. È consigliabile avere familiarità con la verifica di una singola firma digitale.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Firma e sulla verifica delle firme digitali, vedere [Guida di riferimento dei servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-7}

Per verificare la presenza di più firme digitali, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Creare un client di firma.
1. Ottiene il documento PDF contenente le firme da verificare.
1. Impostare le opzioni di runtime della PKI.
1. Recuperare tutte le firme digitali.
1. Scorre tutte le firme.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se si utilizzano servizi Web, includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è implementato su JBoss)
* jbossall-client.jar (obbligatorio se AEM Forms è distribuito su JBoss)

Per informazioni sulla posizione di questi file JAR, vedi [Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un client di firma**

Prima di eseguire un&#39;operazione del servizio di firma a livello di programmazione, creare un client del servizio.

**Ottiene il documento PDF contenente le firme da verificare**

Per verificare una firma utilizzata per firmare o certificare digitalmente un documento PDF, ottenere un documento PDF contenente una firma.

**Imposta opzioni runtime PKI**

Impostare le seguenti opzioni di runtime PKI utilizzate dal servizio di firma per la verifica di tutte le firme in un documento PDF:

* Tempo di verifica
* Verifica della revoca
* Valori di marca temporale

L&#39;impostazione di queste opzioni consente di specificare il tempo di verifica. Ad esempio, è possibile selezionare l&#39;ora corrente (l&#39;ora nel computer del validatore), che indica di utilizzare l&#39;ora corrente. Per informazioni sui diversi valori di tempo, vedere `VerificationTime` valore di enumerazione in [Riferimento API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

È inoltre possibile specificare se eseguire il controllo di revoca come parte del processo di verifica. È ad esempio possibile eseguire un controllo di revoca per determinare se il certificato è stato revocato. Per informazioni sulle opzioni di controllo della revoca, vedere `RevocationCheckStyle` valore di enumerazione in [Riferimento API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

Per eseguire il controllo di revoca su un certificato, specificare un URL di un server di elenco di revoche di certificati (CRL) utilizzando un `CRLOptionSpec` oggetto. Tuttavia, se non si specifica un URL per un server CRL, il servizio di firma ottiene l&#39;URL dal certificato.

Anziché utilizzare un server CRL, è possibile utilizzare un server OCSP (Certificate Status Protocol) online durante la verifica della revoca. In genere, quando si utilizza un server OCSP invece di un server CRL, il controllo di revoca viene eseguito più rapidamente. (vedere [Protocollo per lo stato dei certificati online](https://tools.ietf.org/html/rfc2560).)

È possibile impostare l&#39;ordine dei server CRL e OCSP utilizzato dal servizio di firma utilizzando Adobe Applications and Services. Se, ad esempio, il server OCSP è impostato per primo in Adobe Applications and Services, viene controllato il server OCSP, seguito dal server CRL.

Se non si esegue il controllo della revoca, il servizio di firma non verifica se il certificato è stato revocato. In altre parole, le informazioni del server CRL e OCSP vengono ignorate.

>[!NOTE]
>
>Puoi sovrascrivere l’URL specificato nel certificato utilizzando un’ `CRLOptionSpec` e un `OCSPOptionSpec` oggetto. Ad esempio, per ignorare il server CRL, puoi richiamare `CRLOptionSpec` dell&#39;oggetto `setLocalURI` metodo.

La marca temporale è il processo di registrazione dell&#39;ora in cui un documento firmato o certificato è stato modificato. Dopo aver firmato un documento, nessuno può modificarlo. La marca temporale consente di applicare la validità di un documento firmato o certificato. È possibile impostare le opzioni di marca temporale utilizzando un `TSPOptionSpec` oggetto. Ad esempio, puoi specificare l’URL di un server provider di marca temporale (TSP).

>[!NOTE]
>
>Nei servizi Java e web di avvio rapido, il tempo di verifica è impostato su `VerificationTime.CURRENT_TIME` e la verifica della revoca è impostata su `RevocationCheckStyle.BestEffort`. Poiché non vengono specificate informazioni sul server CRL o OCSP, le informazioni sul server vengono ottenute dal certificato.

**Recupera tutte le firme digitali**

Per verificare tutte le firme digitali in un documento di PDF, recuperare le firme digitali dal documento di PDF. Tutte le firme vengono restituite in un elenco. Per verificare una firma digitale, controllare lo stato della firma.

>[!NOTE]
>
>A differenza di quando si verifica una singola firma digitale, quando si verificano più firme non è necessario specificare il nome del campo firma.

**Iterazione di tutte le firme**

Scorrere ogni firma. In altre parole, per ogni firma, verificare la firma digitale e verificare l&#39;identità del firmatario e lo stato di ogni firma. (vedere [Verifica delle firme digitali](#verify-digital-signatures-using-the-java-api).)

>[!NOTE]
>
>Non è necessario scorrere tutte le firme se il requisito è l&#39;intero documento.

**Consulta anche**

[Verificare più firme digitali tramite API Java](#verify-digital-signatures-using-the-java-api)

[Verifica di più firme digitali tramite l’API del servizio web](#verify-digital-signatures-using-the-web-service-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Verificare più firme digitali tramite API Java {#verify-multiple-digital-signatures-using-the-java-api}

Verificare più firme digitali utilizzando l&#39;API Signature Service (Java):

1. Includi file di progetto

   Includi i file JAR dei client, ad esempio adobe-signatures-client.jar, nel percorso di classe del progetto Java.

1. Creare un client di firma

   * Creare un `ServiceClientFactory` oggetto che contiene proprietà di connessione.
   * Creare un `SignatureServiceClient` mediante il costruttore e passando il `ServiceClientFactory` oggetto.

1. Ottiene il documento PDF contenente le firme da verificare

   * Creare un `java.io.FileInputStream` oggetto che rappresenta il documento PDF contenente più firme digitali da verificare mediante il relativo costruttore. Passa un valore stringa che specifica la posizione del documento PDF.
   * Creare un `com.adobe.idp.Document` mediante il costruttore e passando il `java.io.FileInputStream` oggetto.

1. Imposta opzioni runtime PKI

   * Creare un `PKIOptions` mediante il costruttore.
   * Impostare l&#39;ora di verifica richiamando `PKIOptions` dell&#39;oggetto `setVerificationTime` e il passaggio di un `VerificationTime` valore di enumerazione che specifica il tempo di verifica.
   * Impostare l&#39;opzione di verifica della revoca richiamando `PKIOptions` dell&#39;oggetto `setRevocationCheckStyle` e il passaggio di un `RevocationCheckStyle` valore di enumerazione che specifica se eseguire il controllo di revoca.

1. Recupera tutte le firme digitali

   Richiama `SignatureServiceClient` dell&#39;oggetto `verifyPDFDocument` e trasmettere i seguenti valori:

   * A `com.adobe.idp.Document` oggetto contenente un documento PDF contenente più firme digitali.
   * A `PKIOptions` oggetto contenente le opzioni di runtime della PKI.
   * A `VerifySPIOptions` istanza che contiene informazioni SPI. È possibile specificare `null` per questo parametro.

   Il `verifyPDFDocument` il metodo restituisce un `PDFDocumentVerificationInfo` oggetto che contiene informazioni su tutte le firme digitali nel documento di PDF.

1. Iterazione di tutte le firme

   * Scorrere tutte le firme richiamando `PDFDocumentVerificationInfo` dell&#39;oggetto `getVerificationInfos` metodo. Questo metodo restituisce un `java.util.List` oggetto in cui ogni elemento è un `PDFSignatureVerificationInfo` oggetto. Utilizza un `java.util.Iterator` oggetto per scorrere l&#39;elenco delle firme.
   * Utilizzo di `PDFSignatureVerificationInfo` oggetto, è possibile eseguire attività quali la determinazione dello stato della firma richiamando `PDFSignatureVerificationInfo` dell&#39;oggetto `getStatus` metodo. Questo metodo restituisce un `SignatureStatus` oggetto il cui membro dati statico fornisce informazioni sullo stato della firma. Ad esempio, se la firma è sconosciuta, questo metodo restituisce `SignatureStatus.DocumentSignatureUnknown`.

**Consulta anche**

[Verifica di più firme digitali](#verifying-multiple-digital-signatures)

[Quick Start (modalità SOAP): verifica di più firme digitali tramite l’API Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-verifying-multiple-digital-signatures-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Verifica delle firme digitali](#verify-digital-signatures-using-the-java-api)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Verifica di più firme digitali tramite l’API del servizio web {#verifying-multiple-digital-signatures-using-the-web-service-api}

Verificare più firme digitali utilizzando l&#39;API del servizio di firma (servizio Web):

1. Includi file di progetto

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l’indirizzo IP del server che ospita AEM Forms.

1. Creare un client di firma

   * Creare un `SignatureServiceClient` utilizzando il costruttore predefinito.
   * Creare un `SignatureServiceClient.Endpoint.Address` oggetto utilizzando `System.ServiceModel.EndpointAddress` costruttore. Passa un valore stringa che specifica il file WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/SignatureService?WSDL`). Non è necessario utilizzare il `lc_version` attributo. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Creare un `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto ottenendo il valore del `SignatureServiceClient.Endpoint.Binding` campo. Invia il valore restituito a `BasicHttpBinding`.
   * Imposta il `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegna al campo il nome utente dei moduli AEM `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore password corrispondente al campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Ottiene il documento PDF contenente le firme da verificare

   * Creare un `BLOB` mediante il costruttore. Il `BLOB` L&#39;oggetto memorizza un documento PDF contenente più firme digitali da verificare.
   * Creare un `System.IO.FileStream` richiamando il relativo costruttore. Passa un valore stringa che rappresenta la posizione del file del documento PDF e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto della `System.IO.FileStream` oggetto. È possibile determinare le dimensioni della matrice di byte ottenendo `System.IO.FileStream` dell&#39;oggetto `Length` proprietà.
   * Compilare la matrice di byte con i dati di flusso richiamando `System.IO.FileStream` dell&#39;oggetto `Read` metodo. Passare la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare il `BLOB` oggetto assegnando il relativo `MTOM` proprietà il contenuto della matrice di byte.

1. Imposta opzioni runtime PKI

   * Creare un `PKIOptions` mediante il costruttore.
   * Impostare l&#39;ora di verifica assegnando `PKIOptions` dell&#39;oggetto `verificationTime` membro dati a `VerificationTime` valore di enumerazione che specifica il tempo di verifica.
   * Impostare l&#39;opzione di controllo delle revoche assegnando `PKIOptions` dell&#39;oggetto `revocationCheckStyle` membro dati a `RevocationCheckStyle` valore di enumerazione che specifica se eseguire il controllo di revoca.

1. Recupera tutte le firme digitali

   Richiama `SignatureServiceClient` dell&#39;oggetto `verifyPDFDocument` e trasmettere i seguenti valori:

   * A `BLOB` oggetto contenente un documento PDF contenente più firme digitali.
   * A `PKIOptions` oggetto contenente le opzioni di runtime della PKI.
   * A `VerifySPIOptions` istanza che contiene informazioni SPI. È possibile specificare null per questo parametro.

   Il `verifyPDFDocument` il metodo restituisce un `PDFDocumentVerificationInfo` oggetto che contiene informazioni su tutte le firme digitali nel documento di PDF.

1. Iterazione di tutte le firme

   * Scorrere tutte le firme ottenendo il `PDFDocumentVerificationInfo` dell&#39;oggetto `verificationInfos` membro dati. Questo membro dati restituisce un `Object` in cui ogni elemento è un `PDFSignatureVerificationInfo` oggetto.
   * Utilizzo di `PDFSignatureVerificationInfo` , è possibile eseguire attività quali la determinazione dello stato della firma ottenendo `PDFSignatureVerificationInfo` dell&#39;oggetto `status` membro dati. Questo membro dati restituisce un `SignatureStatus` oggetto il cui membro dati statico fornisce informazioni sullo stato della firma. Ad esempio, se la firma è sconosciuta, questo metodo restituisce `SignatureStatus.DocumentSignatureUnknown`.

**Consulta anche**

[Verifica di più firme digitali](#verifying-multiple-digital-signatures)

[Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamare AEM Forms con SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Rimozione di firme digitali {#removing-digital-signatures}

Per poter applicare una firma digitale più recente, è necessario rimuovere le firme digitali da un campo di firma. Impossibile sovrascrivere una firma digitale. Se si tenta di applicare una firma digitale a un campo firma contenente una firma, si verifica un&#39;eccezione.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio di firma, vedere [Guida di riferimento dei servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-8}

Per rimuovere una firma digitale da un campo firma, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Creare un client di firma.
1. Ottiene il documento PDF contenente una firma da rimuovere.
1. Rimuovere la firma digitale dal campo firma.
1. Salvare il documento PDF come file PDF.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è implementato su JBoss)
* jbossall-client.jar (obbligatorio se AEM Forms è distribuito su JBoss)

Per informazioni sulla posizione di questi file JAR, vedi [Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un client di firma**

Prima di poter eseguire un&#39;operazione del servizio di firma a livello di programmazione, è necessario creare un client del servizio di firma.

**Ottiene il documento PDF contenente una firma da rimuovere**

Per rimuovere una firma da un documento PDF, è necessario ottenere un documento PDF contenente una firma.

**Rimuovi la firma digitale dal campo firma**

Per rimuovere correttamente una firma digitale da un documento PDF, è necessario specificare il nome del campo firma che contiene la firma digitale. È inoltre necessario disporre dell&#39;autorizzazione per rimuovere la firma digitale. In caso contrario, si verificherà un&#39;eccezione.

**Salvare il documento PDF come file PDF**

Dopo che il servizio di firma rimuove una firma digitale da un campo di firma, è possibile salvare il documento PDF come file PDF in modo che gli utenti possano aprirlo in Acrobat o Adobe Reader.

**Consulta anche**

[Rimuovere le firme digitali utilizzando l’API Java](digitally-signing-certifying-documents.md#remove-digital-signatures-using-the-java-api)

[Rimuovere le firme digitali utilizzando l’API del servizio web](digitally-signing-certifying-documents.md#remove-digital-signatures-using-the-web-service-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Aggiunta di campi firma](digitally-signing-certifying-documents.md#adding-signature-fields)

### Rimuovere le firme digitali utilizzando l’API Java {#remove-digital-signatures-using-the-java-api}

Rimuovere una firma digitale utilizzando Signature API (Java):

1. Includi file di progetto

   Includi i file JAR dei client, ad esempio adobe-signatures-client.jar, nel percorso di classe del progetto Java.

1. Creare un client di firma.

   * Creare un `ServiceClientFactory` oggetto che contiene proprietà di connessione.
   * Creare un `SignatureServiceClient` mediante il costruttore e passando il `ServiceClientFactory` oggetto.

1. Ottiene il documento PDF contenente una firma da rimuovere

   * Creare un `java.io.FileInputStream` oggetto che rappresenta il documento PDF contenente la firma da rimuovere mediante il costruttore e passando un valore stringa che specifica la posizione del documento PDF.
   * Creare un `com.adobe.idp.Document` mediante il costruttore e passando il `java.io.FileInputStream` oggetto.

1. Rimuovi la firma digitale dal campo firma

   Rimuovere una firma digitale da un campo di firma richiamando `SignatureServiceClient` dell&#39;oggetto `clearSignatureField` e fornendo i seguenti valori:

   * A `com.adobe.idp.Document` oggetto che rappresenta il documento PDF contenente la firma da rimuovere.
   * Valore string che specifica il nome del campo firma contenente la firma digitale.

   Il `clearSignatureField` il metodo restituisce un `com.adobe.idp.Document` oggetto che rappresenta il documento PDF da cui è stata rimossa la firma digitale.

1. Salvare il documento PDF come file PDF

   * Creare un `java.io.File` e assicurarsi che l&#39;estensione del file sia .pdf.
   * Richiama `com.adobe.idp.Document` dell&#39;oggetto `copyToFile` metodo. Passa il `java.io.File` oggetto per copiare il contenuto del `com.adobe.idp.Document` al file. Assicurati di utilizzare `Document` oggetto restituito da `clearSignatureField` metodo.

**Consulta anche**

[Rimozione di firme digitali](digitally-signing-certifying-documents.md#removing-digital-signatures)

[Quick Start (modalità SOAP): rimozione di una firma digitale tramite l’API Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-removing-a-digital-signature-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Rimuovere le firme digitali utilizzando l’API del servizio web {#remove-digital-signatures-using-the-web-service-api}

Rimuovere una firma digitale utilizzando l’API di firma (servizio web):

1. Includi file di progetto

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l’indirizzo IP del server che ospita AEM Forms.

1. Creare un client di firma

   * Creare un `SignatureServiceClient` utilizzando il costruttore predefinito.
   * Creare un `SignatureServiceClient.Endpoint.Address` oggetto utilizzando `System.ServiceModel.EndpointAddress` costruttore. Passa un valore stringa che specifica il file WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/SignatureService?WSDL`). Non è necessario utilizzare il `lc_version` attributo. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Creare un `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto ottenendo il valore del `SignatureServiceClient.Endpoint.Binding` campo. Invia il valore restituito a `BasicHttpBinding`.
   * Imposta il `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegna al campo il nome utente dei moduli AEM `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore password corrispondente al campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Ottiene il documento PDF contenente una firma da rimuovere

   * Creare un `BLOB` mediante il costruttore. Il `BLOB` L&#39;oggetto viene utilizzato per memorizzare un documento PDF contenente una firma digitale da rimuovere.
   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore stringa che rappresenta la posizione del file del documento PDF firmato e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto della `System.IO.FileStream` oggetto. È possibile determinare le dimensioni della matrice di byte ottenendo `System.IO.FileStream` dell&#39;oggetto `Length` proprietà.
   * Compilare la matrice di byte con i dati di flusso richiamando `System.IO.FileStream` dell&#39;oggetto `Read` metodo. Passare la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare il `BLOB` oggetto assegnando il relativo `MTOM` con il contenuto della matrice di byte.

1. Rimuovi la firma digitale dal campo firma

   Rimuovere la firma digitale richiamando `SignatureServiceClient` dell&#39;oggetto `clearSignatureField` e fornendo i seguenti valori:

   * A `BLOB` oggetto che contiene il documento PDF firmato.
   * Valore string che rappresenta il nome del campo firma contenente la firma digitale da rimuovere.

   Il `clearSignatureField` il metodo restituisce un `BLOB` oggetto che rappresenta il documento PDF da cui è stata rimossa la firma digitale.

1. Salvare il documento PDF come file PDF

   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore stringa che rappresenta la posizione del file del documento PDF contenente un campo di firma vuoto e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto della `BLOB` oggetto restituito da `sign` metodo. Popolare la matrice di byte ottenendo il valore della `BLOB` dell&#39;oggetto `MTOM` membro dati.
   * Creare un `System.IO.BinaryWriter` oggetto richiamando il relativo costruttore e passando il `System.IO.FileStream` oggetto.
   * Scrivere il contenuto della matrice di byte nel file PDF richiamando `System.IO.BinaryWriter` dell&#39;oggetto `Write` e passando la matrice di byte.

**Consulta anche**

[Rimozione di firme digitali](digitally-signing-certifying-documents.md#removing-digital-signatures)

[Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamare AEM Forms con SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
