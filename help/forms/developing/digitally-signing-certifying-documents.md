---
title: Firma digitale e certificazione dei documenti
description: Utilizzare il servizio Firma per aggiungere ed eliminare campi di firma digitale in un documento PDF, recuperare i nomi dei campi di firma in un documento PDF, modificare i campi di firma, firmare digitalmente i documenti PDF, certificare i documenti PDF, convalidare le firme digitali in un documento PDF, convalidare tutte le firme digitali in un documento PDF e rimuovere una firma digitale da un campo di firma.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: c200f345-40ab-46fd-b6ed-f3af0a23796b
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '16917'
ht-degree: 0%

---

# Firma digitale e certificazione dei documenti {#digitally-signing-and-certifying-documents}

**Gli esempi e gli esempi contenuti in questo documento sono solo per AEM Forms in ambiente JEE.**

**Informazioni su Signature Service**

Il servizio di firma consente all&#39;organizzazione di proteggere la sicurezza e la privacy dei documenti Adobe PDF che distribuisce e riceve. Questo servizio utilizza firme digitali e certificazione per garantire che solo i destinatari desiderati possano modificare i documenti. Poiché le funzioni di protezione vengono applicate al documento stesso, quest&#39;ultimo rimane protetto e controllato per l&#39;intero ciclo di vita. Un documento rimane protetto oltre il firewall, quando viene scaricato offline e quando viene inviato di nuovo alla tua organizzazione.

>[!NOTE]
>
>È possibile creare un gestore di firma personalizzato per il servizio di firma che viene richiamato quando vengono richiamate determinate operazioni, ad esempio la firma di un documento PDF.

**Nomi campi firma**

Per alcune operazioni del servizio di firma è necessario specificare il nome del campo firma in cui viene eseguita un&#39;operazione. Quando si firma un documento PDF, ad esempio, si specifica il nome del campo firma da firmare. Si supponga che il nome completo di un campo firma sia `form1[0].Form1[0].SignatureField1[0]`. È possibile specificare `SignatureField1[0]` invece di `form1[0].Form1[0].SignatureField1[0]`.

A volte un conflitto causa la firma del campo errato da parte del servizio di firma (o l&#39;esecuzione di un&#39;altra operazione che richiede il nome del campo della firma). Questo conflitto è il risultato della visualizzazione del nome `SignatureField1[0]` in due o più posizioni nello stesso documento di PDF. Si consideri ad esempio un documento PDF contenente due campi firma denominati `form1[0].Form1[0].SignatureField1[0]` e `form1[0].Form1[0].SubForm1[0].SignatureField1[0]` e si specifichi `SignatureField1[0]`. In questa situazione, il servizio Firma firma il primo campo firma trovato durante l&#39;iterazione di tutti i campi firma del documento.

Se in un documento PDF sono presenti più campi firma, è consigliabile specificare i nomi completi dei campi firma. In altre parole, specifica `form1[0].Form1[0].SignatureField1[0]`invece di `SignatureField1[0]`.

È possibile eseguire queste attività utilizzando il servizio di firma:

* Aggiungere ed eliminare campi di firma digitale in un documento PDF. (Vedi [Aggiunta di campi firma](digitally-signing-certifying-documents.md#adding-signature-fields).)
* Recuperare i nomi dei campi firma in un documento PDF. (Vedere [Recupero dei nomi dei campi di firma](digitally-signing-certifying-documents.md#retrieving-signature-field-names).)
* Modificare i campi della firma. (Vedi [Modifica dei campi di firma](digitally-signing-certifying-documents.md#modifying-signature-fields).)
* Apporre una firma digitale ai documenti PDF. (Vedi [Documenti PDF Con Firma Digitale](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents).)
* Certifica i documenti di PDF. (Vedi [Certificazione dei documenti di PDF](digitally-signing-certifying-documents.md#certifying-pdf-documents).)
* Convalidare le firme digitali in un documento PDF. (Vedi [Verifica delle firme digitali](digitally-signing-certifying-documents.md#verifying-digital-signatures).)
* Convalida tutte le firme digitali in un documento PDF. (Vedi [Verifica di più firme digitali](digitally-signing-certifying-documents.md#verifying-digital-signatures).)
* Rimuovere una firma digitale da un campo firma. (Vedi [Rimozione delle firme digitali](digitally-signing-certifying-documents.md#removing-digital-signatures).)

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Signature, vedere [Riferimento ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Aggiunta di campi firma {#adding-signature-fields}

Le firme digitali vengono visualizzate nei campi firma, ovvero nei campi modulo che contengono una rappresentazione grafica della firma. I campi di firma possono essere visibili o invisibili. I firmatari possono utilizzare un campo di firma preesistente oppure è possibile aggiungere un campo di firma a livello di programmazione. In entrambi i casi, il campo firma deve esistere prima che un documento PDF possa essere firmato.

Puoi aggiungere un campo di firma a livello di programmazione utilizzando l’API Java di Signature Service o l’API del servizio web di firma. È possibile aggiungere più di un campo firma a un documento di PDF; tuttavia, ogni nome di campo firma deve essere univoco.

>[!NOTE]
>
>Alcuni tipi di documenti di PDF non consentono di aggiungere un campo firma a livello di programmazione. Per ulteriori informazioni sul servizio di firma e sull&#39;aggiunta di campi di firma, vedere [Riferimento ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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

Ottenere un documento PDF a cui viene aggiunto un campo firma.

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

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `SignatureServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Ottieni un documento PDF a cui viene aggiunto un campo firma

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento PDF al quale viene aggiunto un campo firma utilizzando il relativo costruttore e passando un valore stringa che specifica la posizione del documento PDF.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Aggiungi un campo firma

   * Creare un oggetto `PositionRectangle` che specifica la posizione del campo della firma utilizzando il relativo costruttore. All&#39;interno del costruttore, specificate i valori delle coordinate.
   * Se lo si desidera, creare un oggetto `FieldMDPOptions` che specifichi i campi bloccati quando viene applicata una firma digitale al campo firma.
   * Aggiungere un campo di firma a un documento PDF richiamando il metodo `addSignatureField` dell&#39;oggetto `SignatureServiceClient` e passando i valori seguenti:

      * `com.adobe.idp`. Oggetto `Document` che rappresenta il documento PDF al quale viene aggiunto un campo firma.
      * Valore stringa che specifica il nome del campo della firma.
      * Valore `java.lang.Integer` che rappresenta il numero di pagina a cui viene aggiunto un campo firma.
      * Oggetto `PositionRectangle` che specifica la posizione del campo firma.
      * Oggetto `FieldMDPOptions` che specifica i campi del documento PDF bloccati dopo l&#39;applicazione di una firma digitale al campo firma. Il valore di questo parametro è facoltativo ed è possibile trasmettere `null`.

   * Oggetto `PDFSeedValueOptions` che specifica vari valori di runtime. Il valore di questo parametro è facoltativo ed è possibile trasmettere `null`.

     Il metodo `addSignatureField` restituisce un `com.adobe.idp`. Oggetto `Document` che rappresenta un documento PDF contenente un campo firma.

   >[!NOTE]
   >
   >È possibile richiamare il metodo `addInvisibleSignatureField` dell&#39;oggetto `SignatureServiceClient` per aggiungere un campo firma invisibile.

1. Salvare il documento PDF come file PDF

   * Creare un oggetto `java.io.File` e verificare che l&#39;estensione del file sia .pdf.
   * Richiama `com.adobe.idp`. Metodo `copyToFile` dell&#39;oggetto `Document` per copiare il contenuto dell&#39;oggetto `Document` nel file. Assicurarsi di utilizzare `com.adobe.idp`. Oggetto `Document` restituito dal metodo `addSignatureField`.

**Consulta anche**

[Avvio rapido API di Signature Service](/help/forms/developing/signature-service-java-api-quick.md#signature-service-java-api-quick-start-soap)

### Aggiungere campi di firma utilizzando l’API del servizio web {#add-signature-fields-using-the-web-service-api}

Per aggiungere un campo di firma utilizzando l’API di firma (servizio web):

1. Includi file di progetto

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Creare un client di firma

   * Creare un oggetto `SignatureServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `SignatureServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/SignatureService?WSDL`). Non è necessario utilizzare l&#39;attributo `lc_version`. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `SignatureServiceClient.Endpoint.Binding`. Eseguire il cast del valore restituito in `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegnare il nome utente dei moduli AEM al campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Ottieni un documento PDF a cui viene aggiunto un campo firma

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare il documento PDF che conterrà un campo di firma.
   * Creare un oggetto `System.IO.FileStream` richiamandone il costruttore e passando un valore stringa che rappresenta la posizione del file del documento PDF e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni della matrice di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare la matrice di byte con i dati di flusso richiamando il metodo `Read` dell&#39;oggetto `System.IO.FileStream` e passando la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando la relativa proprietà `MTOM` al contenuto della matrice di byte.

1. Aggiungi un campo firma

   Aggiungere un campo di firma al documento PDF richiamando il metodo `addSignatureField` dell&#39;oggetto `SignatureServiceClient` e passando i valori seguenti:

   * Oggetto `BLOB` che rappresenta il documento PDF al quale viene aggiunto un campo firma.
   * Valore stringa che specifica il nome del campo della firma.
   * Valore intero che rappresenta il numero di pagina a cui viene aggiunto un campo firma.
   * Oggetto `PositionRect` che specifica la posizione del campo firma.
   * Oggetto `FieldMDPOptions` che specifica i campi del documento PDF bloccati dopo l&#39;applicazione di una firma digitale al campo firma. Il valore di questo parametro è facoltativo ed è possibile trasmettere `null`.
   * Oggetto `PDFSeedValueOptions` che specifica vari valori di runtime. Il valore di questo parametro è facoltativo ed è possibile trasmettere `null`.

   Il metodo `addSignatureField` restituisce un oggetto `BLOB` che rappresenta un documento PDF contenente un campo firma.

1. Salvare il documento PDF come file PDF

   * Creare un oggetto `System.IO.FileStream` richiamandone il costruttore e passando un valore stringa che rappresenta la posizione del file del documento PDF che conterrà il campo firma e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `BLOB` restituito dal metodo `addSignatureField`. Popolare la matrice di byte ottenendo il valore del membro dati `binaryData` dell&#39;oggetto `BLOB`.
   * Creare un oggetto `System.IO.BinaryWriter` richiamandone il costruttore e passando l&#39;oggetto `System.IO.FileStream`.
   * Scrivere il contenuto della matrice di byte in un file PDF richiamando il metodo `Write` dell&#39;oggetto `System.IO.BinaryWriter` e passando la matrice di byte.

**Consulta anche**

[Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamare AEM Forms con SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Recupero dei nomi dei campi firma {#retrieving-signature-field-names}

È possibile recuperare i nomi di tutti i campi firma presenti in un documento PDF che si desidera firmare o certificare. Se non si è certi dei nomi dei campi firma presenti in un documento PDF o si desidera verificarli, è possibile recuperarli a livello di programmazione. Il servizio di firma restituisce il nome completo del campo della firma, ad esempio `form1[0].grantApplication[0].page1[0].SignatureField1[0]`.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Signature, vedere [Riferimento ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)

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

Per informazioni sul percorso di questi file JAR, vedi [Inclusi i file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un client di firma**

Prima di poter eseguire un&#39;operazione del servizio di firma a livello di programmazione, è necessario creare un client del servizio di firma.

**Ottieni il documento PDF contenente i campi della firma**

Recuperare un documento PDF contenente campi di firma.

**Recupera i nomi dei campi della firma**

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

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `SignatureServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Ottieni il documento PDF contenente i campi firma

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento PDF contenente campi di firma utilizzando il relativo costruttore e passando un valore stringa che specifica la posizione del documento PDF.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Recuperare i nomi dei campi firma

   * Recuperare i nomi dei campi firma richiamando il metodo `getSignatureFieldList` dell&#39;oggetto `SignatureServiceClient` e passando l&#39;oggetto `com.adobe.idp.Document` che contiene il documento PDF contenente i campi firma. Questo metodo restituisce un oggetto `java.util.List`, in cui ogni elemento contiene un oggetto `PDFSignatureField`. Utilizzando questo oggetto, è possibile ottenere ulteriori informazioni su un campo firma, ad esempio se è visibile o meno.
   * Scorrere l&#39;oggetto `java.util.List` per determinare se sono presenti nomi di campi di firma. Per ogni campo firma nel documento PDF, è possibile ottenere un oggetto `PDFSignatureField` separato. Per ottenere il nome del campo firma, richiamare il metodo `getName` dell&#39;oggetto `PDFSignatureField`. Questo metodo restituisce un valore stringa che specifica il nome del campo della firma.

**Consulta anche**

[Recupero dei nomi dei campi firma](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

[Quick Start (modalità SOAP): recupero dei nomi dei campi della firma utilizzando l’API Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-retrieving-signature-field-names-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Recuperare il campo della firma utilizzando l’API del servizio web {#retrieve-signature-field-using-the-web-service-api}

Recupera i nomi dei campi della firma utilizzando Signature API (servizio web):

1. Includi file di progetto

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Creare un client di firma

   * Creare un oggetto `SignatureServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `SignatureServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/SignatureService?WSDL`). Non è necessario utilizzare l&#39;attributo `lc_version`. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `SignatureServiceClient.Endpoint.Binding`. Eseguire il cast del valore restituito in `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegnare il nome utente dei moduli AEM al campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Ottieni il documento PDF contenente i campi firma

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare il documento PDF contenente i campi della firma.
   * Creare un oggetto `System.IO.FileStream` richiamandone il costruttore e passando un valore stringa che rappresenta la posizione del file del documento PDF e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni della matrice di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare la matrice di byte con i dati di flusso richiamando il metodo `Read` dell&#39;oggetto `System.IO.FileStream` e passando la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando al relativo campo `MTOM` il contenuto della matrice di byte.

1. Recuperare i nomi dei campi firma

   * Recuperare i nomi dei campi firma richiamando il metodo `getSignatureFieldList` dell&#39;oggetto `SignatureServiceClient` e passando l&#39;oggetto `BLOB` che contiene il documento PDF contenente i campi firma. Questo metodo restituisce un insieme `MyArrayOfPDFSignatureField` in cui ogni elemento contiene un oggetto `PDFSignatureField`.
   * Scorrere l&#39;oggetto `MyArrayOfPDFSignatureField` per determinare se sono presenti nomi di campi di firma. Per ogni campo firma nel documento PDF, è possibile ottenere un oggetto `PDFSignatureField`. Per ottenere il nome del campo firma, richiamare il metodo `getName` dell&#39;oggetto `PDFSignatureField`. Questo metodo restituisce un valore stringa che specifica il nome del campo della firma.

**Consulta anche**

[Recupero dei nomi dei campi firma](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

[Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamare AEM Forms con SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Modifica dei campi della firma {#modifying-signature-fields}

Puoi modificare i campi della firma presenti in un documento PDF utilizzando l’API Java e l’API del servizio web. La modifica di un campo di firma comporta la modifica dei valori del dizionario del blocco del campo di firma o dei valori del dizionario dei valori iniziali.

Un dizionario di blocco dei campi ** specifica un elenco di campi bloccati quando il campo firma è firmato. Un campo bloccato impedisce agli utenti di apportare modifiche al campo. Un *dizionario dei valori seed* contiene informazioni di vincolo utilizzate al momento dell&#39;applicazione della firma. È ad esempio possibile modificare le autorizzazioni che controllano le azioni che possono essere eseguite senza invalidare una firma.

Modificando un campo di firma esistente, è possibile modificare il documento PDF in modo che rifletta i requisiti aziendali in continua evoluzione. Ad esempio, un nuovo requisito aziendale potrebbe richiedere il blocco di tutti i campi del documento dopo la firma del documento.

In questa sezione viene illustrato come modificare un campo di firma modificando i valori del dizionario dei blocchi di campi e del dizionario dei valori iniziali. Le modifiche apportate al dizionario di blocco dei campi della firma determinano il blocco di tutti i campi del documento PDF quando viene firmato un campo della firma. Le modifiche apportate al dizionario dei valori iniziali non consentono tipi specifici di modifiche al documento.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio di firma e sulla modifica dei campi della firma, vedere [Riferimento ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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

Per informazioni sul percorso di questi file JAR, vedi [Inclusi i file della libreria Java di LiveCycle](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un client di firma**

Prima di poter eseguire un&#39;operazione del servizio di firma a livello di programmazione, è necessario creare un client del servizio di firma.

**Ottieni il documento PDF contenente il campo firma da modificare**

Recuperare un documento PDF contenente il campo firma da modificare.

**Imposta valori dizionario**

Per modificare un campo di firma, assegnare valori al relativo dizionario di blocco dei campi o al dizionario dei valori iniziali. Per specificare i valori del dizionario di blocco del campo firma è necessario specificare i campi del documento PDF che vengono bloccati quando il campo firma viene firmato. Questa sezione illustra come bloccare tutti i campi.

È possibile impostare i seguenti valori del dizionario dei valori iniziali:

* **Controllo revisioni**: specifica se viene eseguito il controllo delle revoche quando viene applicata una firma al campo firma.
* **Opzioni certificato**: assegna valori al dizionario dei valori iniziali del certificato. Prima di specificare le opzioni del certificato, è consigliabile acquisire familiarità con un dizionario dei valori iniziali del certificato. (Vedi [Riferimento PDF](https://www.adobe.com/devnet/acrobat/pdfs/pdf_reference_1-7.pdf).)
* **Opzioni digest**: assegna gli algoritmi di digest utilizzati per la firma. I valori validi sono SHA1, SHA256, SHA384, SHA512 e RIPEMD160.
* **Filtro**: specifica il filtro utilizzato con il campo firma. È ad esempio possibile utilizzare il filtro Adobe.PPKLite. (Vedi [Riferimento PDF](https://www.adobe.com/devnet/acrobat/pdfs/pdf_reference_1-7.pdf).)
* **Opzioni contrassegno**: specifica i valori del contrassegno associati al campo della firma. Il valore 1 indica che un firmatario deve utilizzare solo i valori specificati per la voce. Il valore 0 indica che sono consentiti altri valori. Di seguito sono riportate le posizioni di bit:

   * **1(Filtro):** Gestore della firma da utilizzare per firmare il campo della firma
   * **2 (Filtro secondario):** Matrice di nomi che indicano le codifiche accettabili da utilizzare per la firma
   * **3 (V)**: numero di versione minimo richiesto del gestore di firma da utilizzare per firmare il campo firma
   * **4 (motivi):** Matrice di stringhe che specifica i possibili motivi per la firma di un documento
   * **5 (PDFLegalWarnings):** Matrice di stringhe che specifica le possibili attestazioni legali

* **Attestazioni legali**: quando un documento viene certificato, viene automaticamente analizzato per individuare tipi specifici di contenuto che possono rendere ambiguo o fuorviante il contenuto visibile di un documento. Ad esempio, un’annotazione può oscurare il testo importante per comprendere ciò che viene certificato. Il processo di scansione genera avvisi che indicano la presenza di questo tipo di contenuto. Fornisce inoltre una spiegazione aggiuntiva del contenuto che potrebbe aver generato avvisi.
* **Autorizzazioni**: specifica le autorizzazioni che possono essere utilizzate in un documento PDF senza invalidare la firma.
* **Motivi**: specifica i motivi per cui il documento deve essere firmato.
* **Timestamp**: specifica le opzioni di timestamp. È possibile, ad esempio, impostare l&#39;URL del server di marca temporale utilizzato.
* **Versione**: specifica il numero di versione minimo del gestore di firma da utilizzare per firmare il campo firma.

**Modifica il campo della firma**

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

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `SignatureServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Ottiene il documento PDF contenente il campo firma da modificare

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento PDF contenente il campo firma da modificare utilizzando il relativo costruttore e passando un valore stringa che specifica la posizione del documento PDF.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Impostare i valori del dizionario

   * Creare un oggetto `PDFSignatureFieldProperties` utilizzando il relativo costruttore. Un oggetto `PDFSignatureFieldProperties` memorizza le informazioni del dizionario di blocco del campo della firma e del dizionario dei valori iniziali.
   * Creare un oggetto `PDFSeedValueOptionSpec` utilizzando il relativo costruttore. Questo oggetto consente di impostare i valori del dizionario dei valori iniziali.
   * Non consentire modifiche al documento PDF richiamando il metodo `setMdpValue` dell&#39;oggetto `PDFSeedValueOptionSpec` e passando il valore di enumerazione `MDPPermissions.NoChanges`.
   * Creare un oggetto `FieldMDPOptionSpec` utilizzando il relativo costruttore. Questo oggetto consente di impostare i valori del dizionario di blocco del campo della firma.
   * Blocca tutti i campi nel documento PDF richiamando il metodo `setMdpValue` dell&#39;oggetto `FieldMDPOptionSpec` e passando il valore di enumerazione `FieldMDPAction.ALL`.
   * Impostare le informazioni sul dizionario dei valori iniziali richiamando il metodo `setSeedValue` dell&#39;oggetto `PDFSignatureFieldProperties` e passando l&#39;oggetto `PDFSeedValueOptionSpec`.
   * Impostare le informazioni del dizionario di blocco del campo della firma richiamando il metodo `setFieldMDP` dell&#39;oggetto `PDFSignatureFieldProperties` e passando l&#39;oggetto `FieldMDPOptionSpec`.

   >[!NOTE]
   >
   >Per visualizzare tutti i valori del dizionario dei valori iniziali che è possibile impostare, vedere il riferimento alla classe `PDFSeedValueOptionSpec`. (Vedi [Riferimento API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).)

1. Modificare il campo firma

   Modificare il campo firma richiamando il metodo `modifySignatureField` dell&#39;oggetto `SignatureServiceClient` e passando i valori seguenti:

   * L&#39;oggetto `com.adobe.idp.Document` che memorizza il documento PDF contenente il campo firma da modificare
   * Valore stringa che specifica il nome del campo della firma
   * L&#39;oggetto `PDFSignatureFieldProperties` che memorizza le informazioni del dizionario del blocco del campo della firma e del dizionario dei valori iniziali

   Il metodo `modifySignatureField` restituisce un oggetto `com.adobe.idp.Document` che memorizza un documento PDF contenente il campo firma modificato.

1. Salvare il documento PDF come file PDF

   * Creare un oggetto `java.io.File` e verificare che l&#39;estensione del nome file sia pdf.
   * Richiama il metodo `copyToFile` dell&#39;oggetto `com.adobe.idp.Document` per copiare il contenuto dell&#39;oggetto `com.adobe.idp.Document` nel file. Assicurarsi di utilizzare l&#39;oggetto `com.adobe.idp.Document` restituito dal metodo `modifySignatureField`.

### Modificare i campi della firma utilizzando l’API del servizio web {#modify-signature-fields-using-the-web-service-api}

Modifica un campo di firma utilizzando Signature API (servizio web):

1. Includi file di progetto

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Creare un client di firma

   * Creare un oggetto `SignatureServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `SignatureServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/SignatureService?WSDL`). Non è necessario utilizzare l&#39;attributo `lc_version`. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `SignatureServiceClient.Endpoint.Binding`. Eseguire il cast del valore restituito in `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegnare il nome utente dei moduli AEM al campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Ottiene il documento PDF contenente il campo firma da modificare

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare il documento PDF contenente il campo firma da modificare.
   * Creare un oggetto `System.IO.FileStream` richiamandone il costruttore e passando un valore stringa che rappresenta la posizione del file del documento PDF e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni della matrice di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare la matrice di byte con i dati di flusso richiamando il metodo `Read` dell&#39;oggetto `System.IO.FileStream` e passando la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando alla relativa proprietà `MTOM` il contenuto della matrice di byte.

1. Impostare i valori del dizionario

   * Creare un oggetto `PDFSignatureFieldProperties` utilizzando il relativo costruttore. Questo oggetto memorizza le informazioni del dizionario del blocco del campo della firma e del dizionario dei valori iniziali.
   * Creare un oggetto `PDFSeedValueOptionSpec` utilizzando il relativo costruttore. Questo oggetto consente di impostare i valori del dizionario dei valori iniziali.
   * Non consentire modifiche al documento PDF assegnando il valore di enumerazione `MDPPermissions.NoChanges` al membro dati `mdpValue` dell&#39;oggetto `PDFSeedValueOptionSpec`.
   * Creare un oggetto `FieldMDPOptionSpec` utilizzando il relativo costruttore. Questo oggetto consente di impostare i valori del dizionario di blocco del campo della firma.
   * Blocca tutti i campi nel documento PDF assegnando il valore di enumerazione `FieldMDPAction.ALL` al membro dati `mdpValue` dell&#39;oggetto `FieldMDPOptionSpec`.
   * Impostare le informazioni del dizionario del valore di inizializzazione assegnando l&#39;oggetto `PDFSeedValueOptionSpec` al membro dati `seedValue` dell&#39;oggetto `PDFSignatureFieldProperties`.
   * Impostare le informazioni del dizionario di blocco del campo della firma assegnando l&#39;oggetto `FieldMDPOptionSpec` al membro dati `fieldMDP` dell&#39;oggetto `PDFSignatureFieldProperties`.

   >[!NOTE]
   >
   >Per visualizzare tutti i valori del dizionario dei valori iniziali che è possibile impostare, vedere il riferimento alla classe `PDFSeedValueOptionSpec`. (Vedi [Riferimento API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)).

1. Modificare il campo firma

   Modificare il campo firma richiamando il metodo `modifySignatureField` dell&#39;oggetto `SignatureServiceClient` e passando i valori seguenti:

   * L&#39;oggetto `BLOB` che memorizza il documento PDF contenente il campo firma da modificare
   * Valore stringa che specifica il nome del campo della firma
   * L&#39;oggetto `PDFSignatureFieldProperties` che memorizza le informazioni del dizionario del blocco del campo della firma e del dizionario dei valori iniziali

   Il metodo `modifySignatureField` restituisce un oggetto `BLOB` che memorizza un documento PDF contenente il campo firma modificato.

1. Salvare il documento PDF come file PDF

   * Creare un oggetto `System.IO.FileStream` richiamandone il costruttore e passando un valore stringa che rappresenta la posizione del file del documento PDF che conterrà il campo firma e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `BLOB` restituito dal metodo `addSignatureField`. Popolare la matrice di byte ottenendo il valore del membro dati `MTOM` dell&#39;oggetto `BLOB`.
   * Creare un oggetto `System.IO.BinaryWriter` richiamandone il costruttore e passando l&#39;oggetto `System.IO.FileStream`.
   * Scrivere il contenuto della matrice di byte in un file PDF richiamando il metodo `Write` dell&#39;oggetto `System.IO.BinaryWriter` e passando la matrice di byte.

**Consulta anche**

[Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamare AEM Forms con SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Firma digitale dei documenti di PDF {#digitally-signing-pdf-documents}

Le firme digitali possono essere applicate ai documenti PDF per garantire un livello di sicurezza adeguato. Le firme digitali, come le firme scritte a mano, forniscono un mezzo mediante il quale i firmatari si identificano e rilasciano dichiarazioni su un documento. La tecnologia utilizzata per apporre la firma digitale ai documenti consente di garantire che il firmatario e i destinatari siano chiari su ciò che è stato firmato e certi che il documento non sia stato modificato dopo la firma.

I documenti PDF sono firmati mediante una tecnologia a chiave pubblica. Un firmatario ha due chiavi: una chiave pubblica e una chiave privata. La chiave privata viene memorizzata nelle credenziali di un utente che devono essere disponibili al momento della firma. La chiave pubblica viene archiviata nel certificato dell&#39;utente che deve essere disponibile per i destinatari per convalidare la firma. Le informazioni sui certificati revocati si trovano nelle risposte CRL (Certificate Revocation List) e OCSP (Online Certificate Status Protocol) distribuite dalle autorità di certificazione (CA). L’ora della firma può essere ottenuta da una fonte attendibile nota come autorità di marca temporale.

>[!NOTE]
>
>Prima di poter aggiungere una firma digitale a un documento di PDF, è necessario assicurarsi di aggiungere il certificato ad AEM Forms. Un certificato viene aggiunto utilizzando la console di amministrazione o a livello di programmazione utilizzando l’API di Trust Manager. (Vedere [Importazione delle credenziali tramite l&#39;API di Gestione trust](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api).)

È possibile apporre una firma digitale ai documenti PDF a livello di programmazione. Quando si firma digitalmente un documento PDF, è necessario fare riferimento a una credenziale di sicurezza esistente in AEM Forms. Le credenziali sono la chiave privata utilizzata per la firma.

Il servizio di firma esegue i passaggi seguenti quando viene firmato un documento di PDF:

1. Il servizio di firma recupera le credenziali dal Truststore passando l&#39;alias specificato nella richiesta.
1. Truststore cerca le credenziali specificate.
1. Le credenziali vengono restituite al servizio di firma e utilizzate per firmare il documento. Le credenziali vengono anche memorizzate nella cache in base all’alias per le richieste future.

Per informazioni sulla gestione delle credenziali di protezione, vedere la *Guida all&#39;installazione e alla distribuzione di AEM Forms* per il server applicazioni.

>[!NOTE]
>
>Esistono differenze tra la firma e la certificazione dei documenti. (Vedi [Certificazione dei documenti di PDF](digitally-signing-certifying-documents.md#certifying-pdf-documents).)

>[!NOTE]
>
>Non tutti i documenti di PDF supportano la firma. Per ulteriori informazioni sul servizio Firma e sulla firma digitale dei documenti, vedere [Riferimento ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Il servizio di firma non supporta file XDP con dati PDF incorporati come input per un&#39;operazione, ad esempio la certificazione di un documento. Questa azione fa sì che il servizio di firma generi `PDFOperationException`. Per risolvere il problema, convertire il file XDP in un file PDF utilizzando il servizio Utilità PDF, quindi passare il file PDF convertito a un&#39;operazione del servizio di firma. (Vedi [Utilizzo delle utilità PDF](/help/forms/developing/pdf-utilities.md#working-with-pdf-utilities).)

**Credenziali HSM nShield crittografia**

Quando si utilizza una credenziale HSM nShield di crittografia per firmare o certificare un documento PDF, non è possibile utilizzare la nuova credenziale fino al riavvio del server applicazioni J2EE in cui è distribuito AEM Forms. Tuttavia, è possibile impostare un valore di configurazione, in modo che l&#39;operazione di firma o di certificazione funzioni senza riavviare il server applicazioni J2EE.

È possibile aggiungere il seguente valore di configurazione nel file cknfastrc, che si trova in /opt/nfast/cknfastrc (o c:\nfast\cknfastrc):

```shell
    CKNFAST_ASSUME_SINGLE_PROCESS=0
```

Dopo aver aggiunto questo valore di configurazione al file cknfastrc, è possibile utilizzare le nuove credenziali senza riavviare il server applicazioni J2EE.

    >[!NOTE]
    >
    > Si consiglia di utilizzare il comando &#39;Ctrl + C&#39; per riavviare l&#39;SDK. Il riavvio dell&#39;SDK dell&#39;AEM con metodi alternativi, ad esempio l&#39;arresto dei processi Java, può causare incoerenze nell&#39;ambiente di sviluppo dell&#39;AEM.

**La firma non è attendibile**

Quando si certifica e firma lo stesso documento PDF, se la firma di certificazione non è attendibile, sulla prima firma viene visualizzato un triangolo giallo all’apertura del documento PDF in Acrobat o Adobe Reader. La firma di certificazione deve essere attendibile per evitare questa situazione.

**Firma di documenti basati su XFA**

Se si tenta di firmare un modulo basato su XFA utilizzando l&#39;API del servizio di firma, è possibile che i dati non siano presenti in Acrobat in `View` `Signed` `Version`. Ad esempio, considera il seguente flusso di lavoro:

* Utilizzando un file XDP creato con Designer, si unisce una struttura di modulo contenente un campo firma e dati XML contenenti dati modulo. Puoi utilizzare il servizio Forms per generare un documento interattivo di PDF.
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

**Firma il documento di PDF**

Quando si firma un documento di PDF, è possibile impostare le opzioni di runtime utilizzate dal servizio di firma. È possibile impostare le seguenti opzioni:

* Opzioni di aspetto
* Verifica della revoca
* Valori di marca temporale

È possibile impostare le opzioni di aspetto utilizzando un oggetto `PDFSignatureAppearanceOptionSpec`. È ad esempio possibile visualizzare la data all&#39;interno di una firma richiamando il metodo `setShowDate` dell&#39;oggetto `PDFSignatureAppearanceOptionSpec` e passando `true`.

È inoltre possibile specificare se eseguire o meno un controllo di revoca che determini se il certificato utilizzato per firmare digitalmente un documento di PDF è stato revocato. Per eseguire il controllo della revoca, è possibile specificare uno dei seguenti valori:

* **NoCheck**: non eseguire il controllo della revoca.
* **BestEffort**: tentare sempre di verificare la revoca di tutti i certificati della catena. Se si verificano problemi durante il controllo, la revoca viene considerata valida. In caso di errori, si supponga che il certificato non venga revocato.
* **CheckIfAvailable:** Verificare la revoca di tutti i certificati della catena se sono disponibili informazioni sulla revoca. Se si verificano problemi durante il controllo, la revoca viene considerata non valida. In caso di errori, si supponga che il certificato sia stato revocato e che non sia valido. Questo è il valore predefinito.
* **AlwaysCheck**: verifica la revoca di tutti i certificati della catena. Se le informazioni sulla revoca non sono presenti in alcun certificato, la revoca verrà considerata non valida.

Per eseguire il controllo di revoca su un certificato, è possibile specificare un URL di un server di elenco di revoche di certificati (CRL) utilizzando un oggetto `CRLOptionSpec`. Tuttavia, se si desidera eseguire il controllo di revoca e non si specifica un URL per un server CRL, il servizio di firma ottiene l&#39;URL dal certificato.

Anziché utilizzare un server CRL, è possibile utilizzare un server OCSP (Certificate Status Protocol) online durante la verifica della revoca. In genere, quando si utilizza un server OCSP anziché un server CRL, il controllo di revoca viene eseguito più rapidamente. (Vedi &quot;Online Certificate Status Protocol&quot; all&#39;indirizzo [https://tools.ietf.org/html/rfc2560](https://tools.ietf.org/html/rfc2560).)

È possibile impostare l&#39;ordine dei server CRL e OCSP utilizzato dal servizio di firma utilizzando Adobe Applications and Services. Se, ad esempio, il server OCSP è impostato prima in Adobe Applications and Services, viene selezionato il server OCSP, seguito dal server CRL. Consultate &quot;Gestione di certificati e credenziali tramite l&#39;archivio fonti attendibili&quot; nella Guida di AAC.

Se si specifica di non eseguire il controllo di revoca, il servizio di firma non verifica se il certificato utilizzato per firmare o certificare un documento è stato revocato. In altre parole, le informazioni del server CRL e OCSP vengono ignorate.

>[!NOTE]
>
>Sebbene nel certificato sia possibile specificare un CRL o un server OCSP, è possibile sovrascrivere l&#39;URL specificato nel certificato utilizzando un oggetto `CRLOptionSpec` e un oggetto `OCSPOptionSpec`. Ad esempio, per ignorare il server CRL, è possibile richiamare il metodo `setLocalURI` dell&#39;oggetto `CRLOptionSpec`.

La marca temporale si riferisce al processo di tracciamento dell’ora in cui un documento firmato o certificato è stato modificato. Una volta firmato, il documento non deve essere modificato, nemmeno dal proprietario del documento. La marca temporale consente di applicare la validità di un documento firmato o certificato. È possibile impostare le opzioni di marca temporale utilizzando un oggetto `TSPOptionSpec`. Ad esempio, puoi specificare l’URL di un server provider di marca temporale (TSP).

>[!NOTE]
>
>Nelle sezioni di Java e del servizio web, e nei relativi avvii rapidi, viene utilizzato il controllo delle revoche. Poiché non vengono specificate informazioni sul server CRL o OCSP, le informazioni sul server vengono ottenute dal certificato utilizzato per firmare digitalmente il documento PDF.

Per firmare un documento PDF, è possibile specificare il nome completo del campo firma che conterrà la firma digitale, ad esempio `form1[0].#subform[1].SignatureField3[3]`. Quando si utilizza un campo modulo XFA, è possibile utilizzare anche il nome parziale del campo firma: `SignatureField3[3]`.

Per apporre la firma digitale a un documento PDF, è inoltre necessario fare riferimento a una credenziale di protezione. Per fare riferimento a una credenziale di protezione, specificare un alias. L’alias è un riferimento a una credenziale effettiva che può trovarsi in un file PKCS#12 (con estensione .pfx) o in un modulo di sicurezza hardware (HSM). Per informazioni sulle credenziali di protezione, vedere la *Guida all&#39;installazione e alla distribuzione di AEM Forms* per il server applicazioni.

**Salvare il documento PDF firmato**

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

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `SignatureServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Ottieni il documento PDF da firmare

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento PDF da firmare digitalmente utilizzando il relativo costruttore e passando un valore stringa che specifica la posizione del documento PDF.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Firma il documento PDF

   Firmare il documento PDF richiamando il metodo `sign` dell&#39;oggetto `SignatureServiceClient` e passando i valori seguenti:

   * Oggetto `com.adobe.idp.Document` che rappresenta il documento PDF da firmare.
   * Valore string che rappresenta il nome del campo firma che conterrà la firma digitale.
   * Oggetto `Credential` che rappresenta le credenziali utilizzate per firmare digitalmente il documento PDF. Creare un oggetto `Credential` richiamando il metodo `getInstance` statico dell&#39;oggetto `Credential` e passando un valore stringa che specifica il valore alias corrispondente alle credenziali di sicurezza.
   * Oggetto `HashAlgorithm` che specifica un membro dati statico che rappresenta l&#39;algoritmo hash da utilizzare per digerire il documento PDF. Ad esempio, è possibile specificare `HashAlgorithm.SHA1` per utilizzare l&#39;algoritmo SHA1.
   * Valore stringa che rappresenta il motivo per cui il documento PDF è stato firmato digitalmente.
   * Valore stringa che rappresenta le informazioni di contatto del firmatario.
   * Oggetto `PDFSignatureAppearanceOptions` che controlla l&#39;aspetto della firma digitale. È ad esempio possibile utilizzare questo oggetto per aggiungere un logo personalizzato a una firma digitale.
   * Oggetto `java.lang.Boolean` che specifica se eseguire il controllo di revoca sul certificato del firmatario.
   * Oggetto `OCSPOptionSpec` che memorizza le preferenze per il supporto del protocollo di stato del certificato online (OCSP). Se il controllo della revoca non viene eseguito, il parametro non viene utilizzato ed è possibile specificare `null`.
   * Oggetto `CRLPreferences` che memorizza le preferenze dell&#39;elenco di revoche di certificati (CRL). Se il controllo della revoca non viene eseguito, il parametro non viene utilizzato ed è possibile specificare `null`.
   * Un oggetto `TSPPreferences` che memorizza le preferenze per il supporto del provider di marca temporale (TSP). Questo parametro è facoltativo e può essere `null`. Per ulteriori informazioni, consulta [Riferimento API AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

   Il metodo `sign` restituisce un oggetto `com.adobe.idp.Document` che rappresenta il documento PDF firmato.

1. Salva il documento PDF firmato

   * Creare un oggetto `java.io.File` e verificare che l&#39;estensione del file sia .pdf.
   * Richiama il metodo `copyToFile` dell&#39;oggetto `com.adobe.idp.Document` e passa `java.io.File` per copiare il contenuto dell&#39;oggetto `Document` nel file. Assicurarsi di utilizzare l&#39;oggetto `com.adobe.idp.Document` restituito dal metodo `sign`.

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
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Creare un client Firme

   * Creare un oggetto `SignatureServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `SignatureServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/SignatureService?WSDL`). Non è necessario utilizzare l&#39;attributo `lc_version`. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `SignatureServiceClient.Endpoint.Binding`. Eseguire il cast del valore restituito in `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegnare il nome utente dei moduli AEM al campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Ottieni il documento PDF da firmare

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare un documento PDF firmato.
   * Creare un oggetto `System.IO.FileStream` richiamandone il costruttore e passando un valore stringa che rappresenta la posizione del file del documento PDF da firmare e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni della matrice di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare la matrice di byte con i dati di flusso richiamando il metodo `Read` dell&#39;oggetto `System.IO.FileStream` e passando la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando alla relativa proprietà `MTOM` il contenuto della matrice di byte.

1. Firma il documento PDF

   Firmare il documento PDF richiamando il metodo `sign` dell&#39;oggetto `SignatureServiceClient` e passando i valori seguenti:

   * Oggetto `BLOB` che rappresenta il documento PDF da firmare.
   * Valore string che rappresenta il nome del campo firma che conterrà la firma digitale.
   * Oggetto `Credential` che rappresenta le credenziali utilizzate per firmare digitalmente il documento PDF. Creare un oggetto `Credential` utilizzando il relativo costruttore e specificare l&#39;alias assegnando un valore alla proprietà `alias` dell&#39;oggetto `Credential`.
   * Oggetto `HashAlgorithm` che specifica un membro dati statico che rappresenta l&#39;algoritmo hash da utilizzare per digerire il documento PDF. Ad esempio, è possibile specificare `HashAlgorithm.SHA1` per utilizzare l&#39;algoritmo SHA1.
   * Un valore booleano che specifica se viene utilizzato l’algoritmo hash.
   * Valore stringa che rappresenta il motivo per cui il documento PDF è stato firmato digitalmente.
   * Valore stringa che rappresenta la posizione del firmatario.
   * Valore stringa che rappresenta le informazioni di contatto del firmatario.
   * Oggetto `PDFSignatureAppearanceOptions` che controlla l&#39;aspetto della firma digitale. È ad esempio possibile utilizzare questo oggetto per aggiungere un logo personalizzato a una firma digitale.
   * Oggetto `System.Boolean` che specifica se eseguire il controllo di revoca sul certificato del firmatario. Se la verifica della revoca viene eseguita, viene incorporata nella firma. Il valore predefinito è `false`.
   * Oggetto `OCSPOptionSpec` che memorizza le preferenze per il supporto del protocollo di stato del certificato online (OCSP). Se il controllo della revoca non viene eseguito, il parametro non viene utilizzato ed è possibile specificare `null`. Per informazioni su questo oggetto, vedere [Riferimento API AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * Oggetto `CRLPreferences` che memorizza le preferenze dell&#39;elenco di revoche di certificati (CRL). Se il controllo della revoca non viene eseguito, il parametro non viene utilizzato ed è possibile specificare `null`.
   * Un oggetto `TSPPreferences` che memorizza le preferenze per il supporto del provider di marca temporale (TSP). Questo parametro è facoltativo e può essere `null`.

   Il metodo `sign` restituisce un oggetto `BLOB` che rappresenta il documento PDF firmato.

1. Salva il documento PDF firmato

   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore. Passa un valore stringa che rappresenta la posizione del file del documento PDF firmato e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `BLOB` restituito dal metodo `sign`. Popolare la matrice di byte ottenendo il valore del membro dati `MTOM` dell&#39;oggetto `BLOB`.
   * Creare un oggetto `System.IO.BinaryWriter` richiamandone il costruttore e passando l&#39;oggetto `System.IO.FileStream`.
   * Scrivere il contenuto della matrice di byte in un file PDF richiamando il metodo `Write` dell&#39;oggetto `System.IO.BinaryWriter` e passando la matrice di byte.

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
>Prima di poter aggiungere una firma digitale a un modulo interattivo, è necessario assicurarsi di aggiungere il certificato ad AEM Forms. Un certificato viene aggiunto utilizzando la console di amministrazione o a livello di programmazione utilizzando l’API di Trust Manager. (Vedere [Importazione delle credenziali tramite l&#39;API di Gestione trust](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api).)

Quando si utilizza l&#39;API del servizio Forms, impostare l&#39;opzione di runtime `GenerateServerAppearance` su `true`. Questa opzione di runtime garantisce che l&#39;aspetto del modulo generato sul server rimanga valido quando viene aperto in Acrobat o Adobe Reader. È consigliabile impostare questa opzione di runtime durante la generazione di un modulo interattivo da firmare utilizzando l’API Forms.

>[!NOTE]
>
>Prima di leggere Digitally Signing Interactive Forms, è consigliabile avere familiarità con la firma dei documenti di PDF. (Vedi [Documenti PDF Con Firma Digitale](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents).)

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

Per informazioni sul percorso di questi file JAR, vedi [Inclusi i file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un client Forms and Signatures**

Poiché questo flusso di lavoro richiama sia i servizi Forms che Signature, creare sia un client di servizi Forms che un client di servizi Signature.

**Ottieni il modulo interattivo tramite il servizio Forms**

Puoi utilizzare il servizio Forms per ottenere il modulo interattivo di PDF da firmare. A partire da AEM Forms, è possibile passare un oggetto `com.adobe.idp.Document` al servizio Forms che contiene il modulo da riprodurre. Il nome di questo metodo è `renderPDFForm2`. Questo metodo restituisce un oggetto `com.adobe.idp.Document` che contiene il modulo da firmare. È possibile passare questa istanza `com.adobe.idp.Document` al servizio di firma.

Analogamente, se si utilizzano i servizi Web, è possibile passare l&#39;istanza `BLOB` restituita dal servizio Forms al servizio Signature.

>[!NOTE]
>
>L&#39;avvio rapido associato alla sezione Forms interattiva con firma digitale richiama il metodo `renderPDFForm2`.

**Firma il modulo interattivo**

Quando si firma un documento di PDF, è possibile impostare le opzioni di runtime utilizzate dal servizio di firma. È possibile impostare le seguenti opzioni:

* Opzioni di aspetto
* Verifica della revoca
* Valori di marca temporale

È possibile impostare le opzioni di aspetto utilizzando un oggetto `PDFSignatureAppearanceOptionSpec`. È ad esempio possibile visualizzare la data all&#39;interno di una firma richiamando il metodo `setShowDate` dell&#39;oggetto `PDFSignatureAppearanceOptionSpec` e passando `true`.

**Salvare il documento PDF firmato**

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

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `SignatureServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.
   * Creare un oggetto `FormsServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Ottenere il modulo interattivo utilizzando il servizio Forms

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento PDF da passare al servizio Forms utilizzando il relativo costruttore. Passa un valore stringa che specifica la posizione del documento PDF.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.
   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento XML contenente i dati del modulo da passare al servizio Forms utilizzando il relativo costruttore. Passa un valore stringa che specifica la posizione del file XML.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.
   * Creare un oggetto `PDFFormRenderSpec` utilizzato per impostare le opzioni di runtime. Richiama il metodo `setGenerateServerAppearance` dell&#39;oggetto `PDFFormRenderSpec` e passa `true`.
   * Richiama il metodo `renderPDFForm2` dell&#39;oggetto `FormsServiceClient` e passa i seguenti valori:

      * Oggetto `com.adobe.idp.Document` contenente il modulo PDF da riprodurre.
      * Oggetto `com.adobe.idp.Document` contenente dati da unire al modulo.
      * Un oggetto `PDFFormRenderSpec` che memorizza le opzioni di runtime.
      * Oggetto `URLSpec` contenente i valori URI richiesti dal servizio Forms. È possibile specificare `null` per il valore di questo parametro.
      * Oggetto `java.util.HashMap` che memorizza gli allegati. Questo è un parametro facoltativo ed è possibile specificare `null` se non si desidera allegare file al modulo.

     Il metodo `renderPDFForm2` restituisce un oggetto `FormsResult` che contiene un flusso di dati del modulo

   * Recuperare il modulo PDF richiamando il metodo `getOutputContent` dell&#39;oggetto `FormsResult`. Questo metodo restituisce un oggetto `com.adobe.idp.Document` che rappresenta il modulo interattivo.

1. Firma il modulo interattivo

   Firmare il documento PDF richiamando il metodo `sign` dell&#39;oggetto `SignatureServiceClient` e passando i valori seguenti:

   * Oggetto `com.adobe.idp.Document` che rappresenta il documento PDF da firmare. Verificare che questo oggetto sia l&#39;oggetto `com.adobe.idp.Document` ottenuto dal servizio Forms.
   * Valore stringa che rappresenta il nome del campo firma firmato.
   * Oggetto `Credential` che rappresenta le credenziali utilizzate per firmare digitalmente il documento PDF. Creare un oggetto `Credential` richiamando il metodo `getInstance` statico dell&#39;oggetto `Credential`. Passa un valore stringa che specifica il valore alias corrispondente alle credenziali di sicurezza.
   * Oggetto `HashAlgorithm` che specifica un membro dati statico che rappresenta l&#39;algoritmo hash da utilizzare per digerire il documento PDF. Ad esempio, è possibile specificare `HashAlgorithm.SHA1` per utilizzare l&#39;algoritmo SHA1.
   * Valore stringa che rappresenta il motivo per cui il documento PDF è stato firmato digitalmente.
   * Valore stringa che rappresenta le informazioni di contatto del firmatario.
   * Oggetto `PDFSignatureAppearanceOptions` che controlla l&#39;aspetto della firma digitale. È ad esempio possibile utilizzare questo oggetto per aggiungere un logo personalizzato a una firma digitale.
   * Oggetto `java.lang.Boolean` che specifica se eseguire il controllo di revoca sul certificato del firmatario.
   * Oggetto `OCSPPreferences` che memorizza le preferenze per il supporto del protocollo di stato del certificato online (OCSP). Se il controllo della revoca non viene eseguito, il parametro non viene utilizzato ed è possibile specificare `null`.
   * Oggetto `CRLPreferences` che memorizza le preferenze dell&#39;elenco di revoche di certificati (CRL). Se il controllo della revoca non viene eseguito, il parametro non viene utilizzato ed è possibile specificare `null`.
   * Un oggetto `TSPPreferences` che memorizza le preferenze per il supporto del provider di marca temporale (TSP). Questo parametro è facoltativo e può essere `null`.

   Il metodo `sign` restituisce un oggetto `com.adobe.idp.Document` che rappresenta il documento PDF firmato.

1. Salva il documento PDF firmato

   * Creare un oggetto `java.io.File` e verificare che l&#39;estensione del nome file sia .pdf.
   * Richiama il metodo `copyToFile` dell&#39;oggetto `com.adobe.idp.Document` e passa `java.io.File` per copiare il contenuto dell&#39;oggetto `Document` nel file. Assicurarsi di utilizzare l&#39;oggetto `com.adobe.idp.Document` restituito dal metodo `sign`.

**Consulta anche**

[Forms interattivo con firma digitale](digitally-signing-certifying-documents.md#digitally-signing-interactive-forms)

[Quick Start (modalità SOAP): firma digitale di un documento PDF tramite l’API Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-pdf-document-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Firmare digitalmente un modulo interattivo utilizzando l’API del servizio web {#digitally-sign-an-interactive-form-using-the-web-service-api}

Firmare digitalmente un modulo interattivo utilizzando Forms e Signature API (servizio web):

1. Includi file di progetto

   Creare un progetto Microsoft .NET che utilizza MTOM. Poiché questa applicazione client richiama due servizi AEM Forms, creare due riferimenti al servizio. Utilizzare la seguente definizione WSDL per il riferimento al servizio associato al servizio di firma: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   Utilizzare la seguente definizione WSDL per il riferimento al servizio associato al servizio Forms: `http://localhost:8080/soap/services/FormsService?WSDL&lc_version=9.0.1`.

   Poiché il tipo di dati `BLOB` è comune a entrambi i riferimenti al servizio, il tipo di dati `BLOB` viene completamente qualificato quando viene utilizzato. Nel servizio Web corrispondente, avvio rapido, tutte le `BLOB` istanze sono completamente qualificate.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Creazione di un client Forms e Signatures

   * Creare un oggetto `SignatureServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `SignatureServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/SignatureService?WSDL`). Non è necessario utilizzare l&#39;attributo `lc_version`. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `SignatureServiceClient.Endpoint.Binding`. Eseguire il cast del valore restituito in `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegnare il nome utente dei moduli AEM al campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

   >[!NOTE]
   >
   >Ripetere questi passaggi per il client del servizio Forms.

1. Ottenere il modulo interattivo utilizzando il servizio Forms

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare un documento PDF firmato.
   * Creare un oggetto `System.IO.FileStream` richiamandone il costruttore e passando un valore stringa che rappresenta la posizione del file del documento PDF da firmare e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni della matrice di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare la matrice di byte con i dati di flusso richiamando il metodo `Read` dell&#39;oggetto `System.IO.FileStream` e passando la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando alla relativa proprietà `MTOM` il contenuto della matrice di byte.
   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare i dati del modulo.
   * Creare un oggetto `System.IO.FileStream` richiamandone il costruttore e passando un valore stringa che rappresenta la posizione del file XML contenente i dati del modulo e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni della matrice di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare la matrice di byte con i dati di flusso richiamando il metodo `Read` dell&#39;oggetto `System.IO.FileStream` e passando la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando alla relativa proprietà `MTOM` il contenuto della matrice di byte.
   * Creare un oggetto `PDFFormRenderSpec` utilizzato per impostare le opzioni di runtime. Assegnare il valore `true` al campo `generateServerAppearance` dell&#39;oggetto `PDFFormRenderSpec`.
   * Richiama il metodo `renderPDFForm2` dell&#39;oggetto `FormsServiceClient` e passa i seguenti valori:

      * Oggetto `BLOB` contenente il modulo PDF da riprodurre.
      * Oggetto `BLOB` contenente dati da unire al modulo.
      * Un oggetto `PDFFormRenderSpec` che memorizza le opzioni di runtime.
      * Oggetto `URLSpec` contenente i valori URI richiesti dal servizio Forms. È possibile specificare `null` per il valore di questo parametro.
      * Oggetto `java.util.HashMap` che memorizza gli allegati. Questo è un parametro facoltativo ed è possibile specificare `null` se non si desidera allegare file al modulo.
      * Parametro di output lungo utilizzato per memorizzare il numero di pagine nel modulo.
      * Parametro di output stringa utilizzato per il valore locale.
      * Valore `FormResult` che è un parametro di output utilizzato per memorizzare il modulo interattivo.

   * Recuperare il modulo PDF richiamando il campo `outputContent` dell&#39;oggetto `FormsResult`. Questo campo memorizza un oggetto `BLOB` che rappresenta il modulo interattivo.

1. Firma il modulo interattivo

   Firmare il documento PDF richiamando il metodo `sign` dell&#39;oggetto `SignatureServiceClient` e passando i valori seguenti:

   * Oggetto `BLOB` che rappresenta il documento PDF da firmare. Utilizzare l&#39;istanza `BLOB` restituita dal servizio Forms.
   * Valore stringa che rappresenta il nome del campo firma firmato.
   * Oggetto `Credential` che rappresenta le credenziali utilizzate per firmare digitalmente il documento PDF. Creare un oggetto `Credential` utilizzando il relativo costruttore e specificare l&#39;alias assegnando un valore alla proprietà `alias` dell&#39;oggetto `Credential`.
   * Oggetto `HashAlgorithm` che specifica un membro dati statico che rappresenta l&#39;algoritmo hash da utilizzare per digerire il documento PDF. Ad esempio, è possibile specificare `HashAlgorithm.SHA1` per utilizzare l&#39;algoritmo SHA1.
   * Un valore booleano che specifica se viene utilizzato l’algoritmo hash.
   * Valore stringa che rappresenta il motivo per cui il documento PDF è stato firmato digitalmente.
   * Valore stringa che rappresenta la posizione del firmatario.
   * Valore stringa che rappresenta le informazioni di contatto del firmatario.
   * Oggetto `PDFSignatureAppearanceOptions` che controlla l&#39;aspetto della firma digitale. È ad esempio possibile utilizzare questo oggetto per aggiungere un logo personalizzato a una firma digitale.
   * Oggetto `System.Boolean` che specifica se eseguire il controllo di revoca sul certificato del firmatario. Se la verifica della revoca viene eseguita, viene incorporata nella firma. Il valore predefinito è `false`.
   * Oggetto `OCSPPreferences` che memorizza le preferenze per il supporto del protocollo di stato del certificato online (OCSP). Se il controllo della revoca non viene eseguito, il parametro non viene utilizzato ed è possibile specificare `null`. Per informazioni su questo oggetto, vedere [Riferimento API AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * Oggetto `CRLPreferences` che memorizza le preferenze dell&#39;elenco di revoche di certificati (CRL). Se il controllo della revoca non viene eseguito, il parametro non viene utilizzato ed è possibile specificare `null`.
   * Un oggetto `TSPPreferences` che memorizza le preferenze per il supporto del provider di marca temporale (TSP). Questo parametro è facoltativo e può essere `null`.

   Il metodo `sign` restituisce un oggetto `BLOB` che rappresenta il documento PDF firmato.

1. Salva il documento PDF firmato

   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore. Passa un valore stringa che rappresenta la posizione del file del documento PDF firmato e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `BLOB` restituito dal metodo `sign`. Popolare la matrice di byte ottenendo il valore del membro dati `MTOM` dell&#39;oggetto `BLOB`.
   * Creare un oggetto `System.IO.BinaryWriter` richiamandone il costruttore e passando l&#39;oggetto `System.IO.FileStream`.
   * Scrivere il contenuto della matrice di byte in un file PDF richiamando il metodo `Write` dell&#39;oggetto `System.IO.BinaryWriter` e passando la matrice di byte.

**Consulta anche**

[Forms interattivo con firma digitale](digitally-signing-certifying-documents.md#digitally-signing-interactive-forms)

[Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## Certificazione dei documenti di PDF {#certifying-pdf-documents}

È possibile proteggere un documento PDF certificandolo con un tipo particolare di firma, denominata firma certificata. Una firma certificata si distingue da una firma digitale nei seguenti modi:

* Deve essere la prima firma applicata al documento PDF, ovvero, al momento dell&#39;applicazione della firma certificata, tutti gli altri campi della firma presenti nel documento devono essere non firmati. In un documento PDF è consentita una sola firma certificata. Se si desidera firmare e certificare un documento PDF, è necessario certificarlo prima di firmarlo. Dopo aver certificato un documento PDF, è possibile firmare digitalmente ulteriori campi di firma.
* L&#39;autore o l&#39;originatore del documento può specificare che il documento può essere modificato in alcuni modi senza invalidare la firma certificata. Ad esempio, il documento può consentire la compilazione di moduli o la creazione di commenti. Se l’autore specifica che una determinata modifica non è consentita, Acrobat impedisce agli utenti di modificare il documento in questo modo. Se vengono apportate tali modifiche, ad esempio utilizzando un’altra applicazione, la firma certificata non è valida e Acrobat genera un avviso quando un utente apre il documento. Con le firme non certificate, le modifiche non vengono impedite e le normali operazioni di modifica non invalidano la firma originale.
* Al momento della firma, il documento viene analizzato per individuare tipi specifici di contenuto che potrebbero rendere ambiguo o fuorviante il contenuto di un documento. Ad esempio, un’annotazione potrebbe oscurare del testo su una pagina importante per comprendere cosa viene certificato. Su tale contenuto può essere fornita una spiegazione (attestazione legale).

Puoi certificare i documenti di PDF a livello di programmazione utilizzando l’API Java di Signature Service o l’API del servizio web di Signature. Quando si certifica un documento PDF, è necessario fare riferimento a una credenziale di protezione esistente nel servizio Credenziali. Per informazioni sulle credenziali di protezione, vedere la *Guida all&#39;installazione e alla distribuzione di AEM Forms* per il server applicazioni.

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
>Per ulteriori informazioni sul servizio di firma e sulla certificazione di un documento, vedere [Riferimento ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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

Per informazioni sul percorso di questi file JAR, vedi [Inclusi i file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un client di firma**

Prima di poter eseguire un&#39;operazione di firma a livello di programmazione, è necessario creare un client di firma.

**Ottieni il documento PDF da certificare**

Per certificare un documento di PDF, è necessario ottenere un documento di PDF contenente un campo firma. Se un documento PDF non contiene un campo firma, non può essere certificato. È possibile aggiungere un campo firma utilizzando Designer o a livello di programmazione. Per informazioni sull&#39;aggiunta a livello di programmazione di un campo firma, vedere [Aggiunta di campi firma](digitally-signing-certifying-documents.md#adding-signature-fields).

**Certificare il documento di PDF**

Per certificare un documento PDF, è necessario disporre dei seguenti valori di input utilizzati dal servizio di firma per certificare un documento PDF:

* **documento PDF**: documento PDF che contiene un campo firma, ovvero un campo modulo che contiene una rappresentazione grafica della firma certificata. Un documento PDF deve contenere un campo firma prima di poter essere certificato. È possibile aggiungere un campo firma utilizzando Designer o a livello di programmazione. (Vedi [Aggiunta di campi firma](digitally-signing-certifying-documents.md#adding-signature-fields).)
* **Nome campo firma**: nome completo del campo firma certificato. Il valore seguente è un esempio: `form1[0].#subform[1].SignatureField3[3]`. Quando si utilizza un campo modulo XFA, è possibile utilizzare anche il nome parziale del campo firma: `SignatureField3[3]`. Se viene passato un valore nullo per il nome del campo, viene creato e certificato dinamicamente un campo di firma invisibile.
* **Credenziali di sicurezza**: credenziali utilizzate per certificare il documento PDF. Questa credenziale di protezione contiene una password e un alias, che devono corrispondere a un alias visualizzato nella credenziale che si trova nel servizio Credenziale. L’alias è un riferimento a una credenziale effettiva che può trovarsi in un file PKCS#12 (con estensione .pfx) o in un modulo di sicurezza hardware (HSM).
* **Algoritmo hash**: algoritmo hash da utilizzare per il digest del documento PDF.
* **Motivo della firma**: valore visualizzato in Acrobat o Adobe Reader in modo che gli altri utenti conoscano il motivo per cui il documento PDF è stato certificato.
* **Posizione del firmatario**: posizione del firmatario specificata dalle credenziali.
* **Informazioni di contatto**: informazioni di contatto del firmatario, ad esempio indirizzo e numero di telefono.
* **Informazioni sulle autorizzazioni**: autorizzazioni che controllano le azioni che un utente finale può eseguire su un documento senza che la firma certificata non sia valida. È ad esempio possibile impostare l&#39;autorizzazione in modo che qualsiasi modifica apportata al documento PDF provochi la mancata validità della firma certificata.
* **Spiegazione legale**: quando un documento viene certificato, viene automaticamente analizzato per individuare tipi specifici di contenuto che potrebbero rendere ambiguo o fuorviante il contenuto di un documento. Ad esempio, un’annotazione potrebbe oscurare del testo su una pagina importante per comprendere cosa viene certificato. Il processo di scansione genera avvisi su questi tipi di contenuto. Questo valore fornisce una spiegazione aggiuntiva del contenuto che potrebbe aver generato avvisi.
* **Opzioni di aspetto**: opzioni che controllano l&#39;aspetto della firma certificata. Ad esempio, la firma certificata può visualizzare informazioni sulla data.
* **Controllo revoca**: questo valore specifica se viene eseguito il controllo di revoca per il certificato del firmatario. L&#39;impostazione predefinita di `false` indica che la verifica della revoca non è stata eseguita.
* **Impostazioni OCSP**: Impostazioni per il supporto del protocollo OCSP (Online Certificate Status Protocol), che fornisce informazioni sullo stato delle credenziali utilizzate per certificare il documento PDF. È possibile, ad esempio, specificare l&#39;URL del server che fornisce informazioni sulle credenziali utilizzate per accedere al documento PDF.
* **Impostazioni CRL**: Impostazioni per le preferenze dell&#39;elenco di revoche di certificati (CRL) se la verifica della revoca è stata eseguita. Ad esempio, è possibile specificare di controllare sempre se una credenziale è stata revocata.
* **Timestamp**: impostazioni che definiscono le informazioni di timestamp applicate alla firma certificata. Una marca temporale indica che dati specifici sono stati stabiliti prima di un certo periodo di tempo. Questa conoscenza consente di creare una relazione di affidabilità tra il firmatario e il verificatore.

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

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `SignatureServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Ottieni il documento PDF da certificare

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento PDF da certificare utilizzando il relativo costruttore e passando un valore stringa che specifica la posizione del documento PDF.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Certifica il documento PDF

   Certifica il documento PDF richiamando il metodo `certify` dell&#39;oggetto `SignatureServiceClient` e passando i valori seguenti:

   * Oggetto `com.adobe.idp.Document` che rappresenta il documento PDF da certificare.
   * Valore stringa che rappresenta il nome del campo firma che conterrà la firma.
   * Oggetto `Credential` che rappresenta le credenziali utilizzate per certificare il documento PDF. Creare un oggetto `Credential` richiamando il metodo `getInstance` statico dell&#39;oggetto `Credential` e passando un valore stringa che specifica il valore alias corrispondente alle credenziali di sicurezza.
   * Oggetto `HashAlgorithm` che specifica un membro dati statico che rappresenta l&#39;algoritmo hash utilizzato per digerire il documento PDF. Ad esempio, è possibile specificare `HashAlgorithm.SHA1` per utilizzare l&#39;algoritmo SHA1.
   * Valore stringa che rappresenta il motivo per cui il documento PDF è stato certificato.
   * Valore stringa che rappresenta le informazioni di contatto del firmatario.
   * Oggetto `MDPPermissions` che specifica le azioni che possono essere eseguite sul documento PDF che invalidano la firma.
   * Oggetto `PDFSignatureAppearanceOptions` che controlla l&#39;aspetto della firma certificata. Se lo si desidera, modificare l&#39;aspetto della firma richiamando un metodo, ad esempio `setShowDate`.
   * Valore stringa che fornisce una spiegazione delle azioni che invalidano la firma.
   * Oggetto `java.lang.Boolean` che specifica se eseguire il controllo di revoca sul certificato del firmatario. Se la verifica della revoca viene eseguita, viene incorporata nella firma. Il valore predefinito è `false`.
   * Oggetto `java.lang.Boolean` che specifica se il campo firma da certificare è bloccato. Se il campo è bloccato, il campo firma viene contrassegnato come di sola lettura, le relative proprietà non possono essere modificate e non possono essere cancellate da utenti che non dispongono delle autorizzazioni necessarie. Il valore predefinito è `false`.
   * Oggetto `OCSPPreferences` che memorizza le preferenze per il supporto del protocollo di stato del certificato online (OCSP). Se il controllo della revoca non viene eseguito, il parametro non viene utilizzato ed è possibile specificare `null`. Per informazioni su questo oggetto, vedere [Riferimento API AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * Oggetto `CRLPreferences` che memorizza le preferenze dell&#39;elenco di revoche di certificati (CRL). Se il controllo della revoca non viene eseguito, il parametro non viene utilizzato ed è possibile specificare `null`.
   * Un oggetto `TSPPreferences` che memorizza le preferenze per il supporto del provider di marca temporale (TSP). Ad esempio, dopo aver creato un oggetto `TSPPreferences`, è possibile impostare l&#39;URL del server TSP richiamando il metodo `setTspServerURL` dell&#39;oggetto `TSPPreferences`. Questo parametro è facoltativo e può essere `null`. Per ulteriori informazioni, vedere [Riferimento ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

   Il metodo `certify` restituisce un oggetto `com.adobe.idp.Document` che rappresenta il documento PDF certificato.

1. Salvare il documento PDF certificato come file PDF

   * Creare un oggetto `java.io.File` e verificare che l&#39;estensione del file sia .pdf.
   * Richiama il metodo `copyToFile` dell&#39;oggetto `com.adobe.idp.Document` per copiare il contenuto dell&#39;oggetto `com.adobe.idp.Document` nel file.

**Consulta anche**

[Certificazione dei documenti di PDF](digitally-signing-certifying-documents.md#certifying-pdf-documents)

[Quick Start (modalità SOAP): certificazione di un documento PDF tramite API Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-certifying-a-pdf-document-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Certifica i documenti di PDF utilizzando l’API del servizio web {#certify-pdf-documents-using-the-web-service-api}

Certifica un documento PDF utilizzando l’API di firma (servizio web):

1. Includi file di progetto

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Creare un client di firma

   * Creare un oggetto `SignatureServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `SignatureServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/SignatureService?WSDL`). Non è necessario utilizzare l&#39;attributo `lc_version`. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `SignatureServiceClient.Endpoint.Binding`. Eseguire il cast del valore restituito in `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegnare il nome utente dei moduli AEM al campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Ottieni il documento PDF da certificare

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per archiviare un documento PDF certificato.
   * Creare un oggetto `System.IO.FileStream` richiamandone il costruttore e passando un valore stringa che rappresenta la posizione del file del documento PDF da certificare e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni della matrice di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare la matrice di byte con i dati di flusso richiamando il metodo `Read` dell&#39;oggetto `System.IO.FileStream` e passando la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando al relativo membro dati `MTOM` il contenuto della matrice di byte.

1. Certifica il documento PDF

   Certifica il documento PDF richiamando il metodo `certify` dell&#39;oggetto `SignatureServiceClient` e passando i valori seguenti:

   * Oggetto `BLOB` che rappresenta il documento PDF da certificare.
   * Valore stringa che rappresenta il nome del campo firma che conterrà la firma.
   * Oggetto `Credential` che rappresenta le credenziali utilizzate per certificare il documento PDF. Creare un oggetto `Credential` utilizzando il relativo costruttore e specificare l&#39;alias assegnando un valore alla proprietà `alias` dell&#39;oggetto `Credential`.
   * Oggetto `HashAlgorithm` che specifica un membro dati statico che rappresenta l&#39;algoritmo hash utilizzato per digerire il documento PDF. Ad esempio, è possibile specificare `HashAlgorithm.SHA1` per utilizzare l&#39;algoritmo SHA1.
   * Un valore booleano che specifica se viene utilizzato l’algoritmo hash.
   * Valore stringa che rappresenta il motivo per cui il documento PDF è stato certificato.
   * Valore stringa che rappresenta la posizione del firmatario.
   * Valore stringa che rappresenta le informazioni di contatto del firmatario.
   * Membro dati statico di un oggetto `MDPPermissions` che specifica le azioni che possono essere eseguite sul documento PDF che invalidano la firma.
   * Valore booleano che specifica se utilizzare l&#39;oggetto `MDPPermissions` passato come valore del parametro precedente.
   * Valore stringa che spiega quali azioni invalidano la firma.
   * Oggetto `PDFSignatureAppearanceOptions` che controlla l&#39;aspetto della firma certificata. Creare un oggetto `PDFSignatureAppearanceOptions` utilizzando il relativo costruttore. È possibile modificare l&#39;aspetto della firma impostandone uno dei membri dati.
   * Oggetto `System.Boolean` che specifica se eseguire il controllo di revoca sul certificato del firmatario. Se la verifica della revoca viene eseguita, viene incorporata nella firma. Il valore predefinito è `false`.
   * Oggetto `System.Boolean` che specifica se il campo firma da certificare è bloccato. Se il campo è bloccato, il campo firma viene contrassegnato come di sola lettura, le relative proprietà non possono essere modificate e non possono essere cancellate da utenti che non dispongono delle autorizzazioni necessarie. Il valore predefinito è `false`.
   * Oggetto `System.Boolean` che specifica se il campo firma è bloccato. In altre parole, se passi `true` al parametro precedente, passa `true` a questo parametro.
   * Oggetto `OCSPPreferences` che memorizza le preferenze per il supporto del protocollo di stato del certificato online (OCSP), che fornisce informazioni sullo stato delle credenziali utilizzate per certificare il documento PDF. Se il controllo della revoca non viene eseguito, il parametro non viene utilizzato ed è possibile specificare `null`.
   * Oggetto `CRLPreferences` che memorizza le preferenze dell&#39;elenco di revoche di certificati (CRL). Se il controllo della revoca non viene eseguito, il parametro non viene utilizzato ed è possibile specificare `null`.
   * Un oggetto `TSPPreferences` che memorizza le preferenze per il supporto del provider di marca temporale (TSP). Ad esempio, dopo aver creato un oggetto `TSPPreferences`, è possibile impostare l&#39;URL del TSP impostando il membro dati `tspServerURL` dell&#39;oggetto `TSPPreferences`. Questo parametro è facoltativo e può essere `null`.

   Il metodo `certify` restituisce un oggetto `BLOB` che rappresenta il documento PDF certificato.

1. Salvare il documento PDF certificato come file PDF

   * Creare un oggetto `System.IO.FileStream` richiamandone il costruttore e passando un valore stringa che rappresenta la posizione del file del documento PDF che conterrà il documento PDF certificato e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `BLOB` restituito dal metodo `certify`. Popolare la matrice di byte ottenendo il valore del membro dati `binaryData` dell&#39;oggetto `BLOB`.
   * Creare un oggetto `System.IO.BinaryWriter` richiamandone il costruttore e passando l&#39;oggetto `System.IO.FileStream`.
   * Scrivere il contenuto della matrice di byte in un file PDF richiamando il metodo `Write` dell&#39;oggetto `System.IO.BinaryWriter` e passando la matrice di byte.

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
>Per ulteriori informazioni sul servizio di firma e sulla verifica delle firme digitali, vedere [Riferimento ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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

Per informazioni sul percorso di questi file JAR, vedi [Inclusi i file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un client di firma**

Prima di eseguire un&#39;operazione del servizio di firma a livello di programmazione, creare un client del servizio.

**Ottieni il documento PDF che contiene la firma da verificare**

Per verificare una firma utilizzata per firmare o certificare digitalmente un documento PDF, ottenere un documento PDF contenente una firma.

**Impostare le opzioni di runtime della PKI**

Impostare le seguenti opzioni di runtime PKI utilizzate dal servizio di firma per la verifica delle firme in un documento PDF:

* Tempo di verifica
* Verifica della revoca
* Valori di marca temporale

L&#39;impostazione di queste opzioni consente di specificare il tempo di verifica. Ad esempio, è possibile selezionare l&#39;ora corrente (l&#39;ora nel computer del validatore), che indica di utilizzare l&#39;ora corrente. Per informazioni sui diversi valori di ora, vedere il valore di enumerazione `VerificationTime` in [Riferimento API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

È inoltre possibile specificare se eseguire il controllo di revoca come parte del processo di verifica. È ad esempio possibile eseguire un controllo di revoca per determinare se il certificato è stato revocato. Per informazioni sulle opzioni di controllo delle revoche, vedere il valore di enumerazione `RevocationCheckStyle` in [Riferimento API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

Per eseguire il controllo di revoca su un certificato, specificare un URL di un server di elenco di revoche di certificati (CRL) utilizzando un oggetto `CRLOptionSpec`. Tuttavia, se non si specifica un URL per il server CRL, il servizio di firma ottiene l&#39;URL dal certificato.

Anziché utilizzare un server CRL, è possibile utilizzare un server OCSP (Certificate Status Protocol) online durante la verifica della revoca. In genere, quando si utilizza un server OCSP anziché un server CRL, il controllo di revoca viene eseguito più rapidamente. (Vedi [Protocollo di stato del certificato in linea](https://tools.ietf.org/html/rfc2560).)

È possibile impostare l&#39;ordine dei server CRL e OCSP utilizzato dal servizio di firma utilizzando Adobe Applications and Services. Se, ad esempio, il server OCSP è impostato prima in Adobe Applications and Services, viene selezionato il server OCSP, seguito dal server CRL.

Se non si esegue il controllo della revoca, il servizio di firma non verifica se il certificato è stato revocato. In altre parole, le informazioni del server CRL e OCSP vengono ignorate.

>[!NOTE]
>
>È possibile ignorare l&#39;URL specificato nel certificato utilizzando un oggetto `CRLOptionSpec` e un oggetto `OCSPOptionSpec`. Ad esempio, per ignorare il server CRL, è possibile richiamare il metodo `setLocalURI` dell&#39;oggetto `CRLOptionSpec`.

La marca temporale è il processo di registrazione dell&#39;ora in cui un documento firmato o certificato è stato modificato. Dopo aver firmato un documento, nessuno può modificarlo. La marca temporale consente di applicare la validità di un documento firmato o certificato. È possibile impostare le opzioni di marca temporale utilizzando un oggetto `TSPOptionSpec`. Ad esempio, puoi specificare l’URL di un server provider di marca temporale (TSP).

>[!NOTE]
>
>Negli avvii rapidi di Java e del servizio Web, l&#39;ora di verifica è impostata su `VerificationTime.CURRENT_TIME` e la verifica della revoca su `RevocationCheckStyle.BestEffort`. Poiché non vengono specificate informazioni sul server CRL o OCSP, le informazioni sul server vengono ottenute dal certificato.

**Verifica la firma digitale**

Per verificare correttamente una firma, specificare il nome completo del campo firma che contiene la firma, ad esempio `form1[0].#subform[1].SignatureField3[3]`. Quando si utilizza un campo modulo XFA, è inoltre possibile utilizzare il nome parziale del campo firma: `SignatureField3`.

Per impostazione predefinita, il servizio di firma limita a 65 minuti la durata della firma di un documento dopo il periodo di convalida. Se un utente tenta di verificare una firma all’ora corrente e l’ora della firma è successiva all’ora corrente ed è compresa entro 65 minuti, il servizio di firma non crea un errore di verifica.

>[!NOTE]
>
>Per gli altri valori necessari per la verifica di una firma, vedere [Riferimento API AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Determinare lo stato della firma**

Durante la verifica di una firma digitale è possibile controllare lo stato della firma.

**Determinare l&#39;identità del firmatario**

Puoi determinare l’identità del firmatario, che può corrispondere a uno dei seguenti valori:

* **Sconosciuto**: firmatario sconosciuto perché non è possibile eseguire la verifica del firmatario.
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

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `SignatureServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Ottieni il documento PDF contenente la firma da verificare

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento PDF contenente la firma da verificare utilizzando il relativo costruttore. Passa un valore stringa che specifica la posizione del documento PDF.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Impostare le opzioni di runtime della PKI

   * Creare un oggetto `PKIOptions` utilizzando il relativo costruttore.
   * Impostare il tempo di verifica richiamando il metodo `setVerificationTime` dell&#39;oggetto `PKIOptions` e passando un valore di enumerazione `VerificationTime` che specifica il tempo di verifica.
   * Impostare l&#39;opzione di verifica della revoca richiamando il metodo `setRevocationCheckStyle` dell&#39;oggetto `PKIOptions` e passando un valore di enumerazione `RevocationCheckStyle` che specifica se eseguire il controllo della revoca.

1. Verificare la firma digitale

   Verificare la firma richiamando il metodo `verify2` dell&#39;oggetto `SignatureServiceClient` e passando i valori seguenti:

   * Oggetto `com.adobe.idp.Document` contenente un documento PDF con firma digitale o certificato.
   * Valore stringa che rappresenta il nome del campo della firma contenente la firma da verificare.
   * Oggetto `PKIOptions` contenente opzioni di runtime PKI.
   * Istanza `VerifySPIOptions` contenente informazioni SPI. È possibile specificare `null` per questo parametro.

   Il metodo `verify2` restituisce un oggetto `PDFSignatureVerificationInfo` che contiene informazioni che possono essere utilizzate per verificare la firma digitale.

1. Determinare lo stato della firma

   * Determinare lo stato della firma richiamando il metodo `getStatus` dell&#39;oggetto `PDFSignatureVerificationInfo`. Questo metodo restituisce un oggetto `SignatureStatus` che specifica lo stato della firma. Se ad esempio un documento di PDF firmato non viene modificato, questo metodo restituisce `SignatureStatus.DocumentSigNoChanges`.

1. Determinare l’identità del firmatario

   * Determinare l&#39;identità del firmatario richiamando il metodo `getSigner` dell&#39;oggetto `PDFSignatureVerificationInfo`. Questo metodo restituisce un oggetto `IdentityInformation`.
   * Richiama il metodo `getStatus` dell&#39;oggetto `IdentityInformation` per determinare l&#39;identità del firmatario. Questo metodo restituisce un valore di enumerazione `IdentityStatus` che specifica l&#39;identità. Ad esempio, se il firmatario è attendibile, questo metodo restituisce `IdentityStatus.TRUSTED`.

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
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Creare un client di firma

   * Creare un oggetto `SignatureServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `SignatureServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/SignatureService?WSDL`). Non è necessario utilizzare l&#39;attributo `lc_version`. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `SignatureServiceClient.Endpoint.Binding`. Eseguire il cast del valore restituito in `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegnare il nome utente dei moduli AEM al campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Ottieni il documento PDF contenente la firma da verificare

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare un documento PDF contenente una firma digitale o certificata da verificare.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore. Passa un valore stringa che rappresenta la posizione del file del documento PDF firmato e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni della matrice di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare la matrice di byte con i dati di flusso richiamando il metodo `Read` dell&#39;oggetto `System.IO.FileStream`. Passare la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando alla relativa proprietà `MTOM` il contenuto della matrice di byte.

1. Impostare le opzioni di runtime della PKI

   * Creare un oggetto `PKIOptions` utilizzando il relativo costruttore.
   * Impostare il tempo di verifica assegnando al membro dati `verificationTime` dell&#39;oggetto `PKIOptions` un valore di enumerazione `VerificationTime` che specifica il tempo di verifica.
   * Impostare l&#39;opzione di controllo delle revoche assegnando al membro dati `revocationCheckStyle` dell&#39;oggetto `PKIOptions` un valore di enumerazione `RevocationCheckStyle` che specifica se eseguire il controllo delle revoche.

1. Verificare la firma digitale

   Verificare la firma richiamando il metodo `verify2` dell&#39;oggetto `SignatureServiceClient` e passando i valori seguenti:

   * L&#39;oggetto `BLOB` che contiene un documento PDF con firma digitale o certificato.
   * Valore stringa che rappresenta il nome del campo della firma contenente la firma da verificare.
   * Oggetto `PKIOptions` contenente opzioni di runtime PKI.
   * Istanza `VerifySPIOptions` contenente informazioni SPI. È possibile specificare `null` per questo parametro.

   Il metodo `verify2` restituisce un oggetto `PDFSignatureVerificationInfo` che contiene informazioni che possono essere utilizzate per verificare la firma digitale.

1. Determinare lo stato della firma

   Determinare lo stato della firma ottenendo il valore del membro dati `status` dell&#39;oggetto `PDFSignatureVerificationInfo`. Questo membro dati memorizza un oggetto `SignatureStatus` che specifica lo stato della firma. Se ad esempio un documento di PDF firmato viene modificato, il membro dati `status` memorizza il valore `SignatureStatus.DocumentSigNoChanges`.

1. Determinare l’identità del firmatario

   * Determinare l&#39;identità del firmatario recuperando il valore del membro dati `signer` dell&#39;oggetto `PDFSignatureVerificationInfo`. Questo membro restituisce un oggetto `IdentityInformation`.
   * Recuperare il membro dati `status` dell&#39;oggetto `IdentityInformation` per determinare l&#39;identità del firmatario. Questo membro dati restituisce un valore di enumerazione `IdentityStatus` che specifica l&#39;identità. Ad esempio, se il firmatario è attendibile, questo membro restituisce `IdentityStatus.TRUSTED`.

**Consulta anche**

[Verifica delle firme digitali](#verify-digital-signatures-using-the-java-api)

[Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamare AEM Forms con SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Verifica di più firme digitali {#verifying-multiple-digital-signatures}

AEM Forms fornisce i mezzi per verificare tutte le firme digitali presenti in un documento PDF. Si supponga che un documento PDF contenga più firme digitali come risultato di un processo aziendale che richiede firme da più firmatari. Ad esempio, si consideri una transazione finanziaria che richiede la firma sia di un addetto al prestito che di un manager. È possibile utilizzare l’API Java di Signature Service o l’API del servizio Web per verificare tutte le firme all’interno del documento PDF. Quando si verificano più firme digitali, è possibile controllare lo stato e le proprietà di ogni firma. Prima di considerare attendibile una firma digitale, è consigliabile verificarla. È consigliabile avere familiarità con la verifica di una singola firma digitale.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio di firma e sulla verifica delle firme digitali, vedere [Riferimento ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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

Per informazioni sul percorso di questi file JAR, vedi [Inclusi i file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un client di firma**

Prima di eseguire un&#39;operazione del servizio di firma a livello di programmazione, creare un client del servizio.

**Ottieni il documento PDF contenente le firme da verificare**

Per verificare una firma utilizzata per firmare o certificare digitalmente un documento PDF, ottenere un documento PDF contenente una firma.

**Imposta opzioni runtime PKI**

Impostare le seguenti opzioni di runtime PKI utilizzate dal servizio di firma per la verifica di tutte le firme in un documento PDF:

* Tempo di verifica
* Verifica della revoca
* Valori di marca temporale

L&#39;impostazione di queste opzioni consente di specificare il tempo di verifica. Ad esempio, è possibile selezionare l&#39;ora corrente (l&#39;ora nel computer del validatore), che indica di utilizzare l&#39;ora corrente. Per informazioni sui diversi valori di ora, vedere il valore di enumerazione `VerificationTime` in [Riferimento API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

È inoltre possibile specificare se eseguire il controllo di revoca come parte del processo di verifica. È ad esempio possibile eseguire un controllo di revoca per determinare se il certificato è stato revocato. Per informazioni sulle opzioni di controllo delle revoche, vedere il valore di enumerazione `RevocationCheckStyle` in [Riferimento API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

Per eseguire il controllo di revoca su un certificato, specificare un URL di un server di elenco di revoche di certificati (CRL) utilizzando un oggetto `CRLOptionSpec`. Tuttavia, se non si specifica un URL per un server CRL, il servizio di firma ottiene l&#39;URL dal certificato.

Anziché utilizzare un server CRL, è possibile utilizzare un server OCSP (Certificate Status Protocol) online durante la verifica della revoca. In genere, quando si utilizza un server OCSP invece di un server CRL, il controllo di revoca viene eseguito più rapidamente. (Vedi [Protocollo di stato del certificato in linea](https://tools.ietf.org/html/rfc2560).)

È possibile impostare l&#39;ordine dei server CRL e OCSP utilizzato dal servizio di firma utilizzando Adobe Applications and Services. Se, ad esempio, il server OCSP è impostato per primo in Adobe Applications and Services, viene controllato il server OCSP, seguito dal server CRL.

Se non si esegue il controllo della revoca, il servizio di firma non verifica se il certificato è stato revocato. In altre parole, le informazioni del server CRL e OCSP vengono ignorate.

>[!NOTE]
>
>È possibile ignorare l&#39;URL specificato nel certificato utilizzando un oggetto `CRLOptionSpec` e un oggetto `OCSPOptionSpec`. Ad esempio, per ignorare il server CRL, è possibile richiamare il metodo `setLocalURI` dell&#39;oggetto `CRLOptionSpec`.

La marca temporale è il processo di registrazione dell&#39;ora in cui un documento firmato o certificato è stato modificato. Dopo aver firmato un documento, nessuno può modificarlo. La marca temporale consente di applicare la validità di un documento firmato o certificato. È possibile impostare le opzioni di marca temporale utilizzando un oggetto `TSPOptionSpec`. Ad esempio, puoi specificare l’URL di un server provider di marca temporale (TSP).

>[!NOTE]
>
>Negli avvii rapidi di Java e del servizio Web, l&#39;ora di verifica è impostata su `VerificationTime.CURRENT_TIME` e la verifica della revoca su `RevocationCheckStyle.BestEffort`. Poiché non vengono specificate informazioni sul server CRL o OCSP, le informazioni sul server vengono ottenute dal certificato.

**Recupera tutte le firme digitali**

Per verificare tutte le firme digitali in un documento di PDF, recuperare le firme digitali dal documento di PDF. Tutte le firme vengono restituite in un elenco. Per verificare una firma digitale, controllare lo stato della firma.

>[!NOTE]
>
>A differenza di quando si verifica una singola firma digitale, quando si verificano più firme non è necessario specificare il nome del campo firma.

**Iterare tutte le firme**

Scorrere ogni firma. In altre parole, per ogni firma, verificare la firma digitale e verificare l&#39;identità del firmatario e lo stato di ogni firma. (Vedi [Verifica delle firme digitali](#verify-digital-signatures-using-the-java-api).)

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

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `SignatureServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Ottiene il documento PDF contenente le firme da verificare

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento PDF contenente più firme digitali da verificare utilizzando il relativo costruttore. Passa un valore stringa che specifica la posizione del documento PDF.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Imposta opzioni runtime PKI

   * Creare un oggetto `PKIOptions` utilizzando il relativo costruttore.
   * Impostare il tempo di verifica richiamando il metodo `setVerificationTime` dell&#39;oggetto `PKIOptions` e passando un valore di enumerazione `VerificationTime` che specifica il tempo di verifica.
   * Impostare l&#39;opzione di controllo della revoca richiamando il metodo `setRevocationCheckStyle` dell&#39;oggetto `PKIOptions` e passando un valore di enumerazione `RevocationCheckStyle` che specifica se eseguire il controllo della revoca.

1. Recupera tutte le firme digitali

   Richiama il metodo `verifyPDFDocument` dell&#39;oggetto `SignatureServiceClient` e passa i seguenti valori:

   * Oggetto `com.adobe.idp.Document` contenente un documento PDF contenente più firme digitali.
   * Oggetto `PKIOptions` contenente opzioni di runtime PKI.
   * Istanza `VerifySPIOptions` contenente informazioni SPI. È possibile specificare `null` per questo parametro.

   Il metodo `verifyPDFDocument` restituisce un oggetto `PDFDocumentVerificationInfo` che contiene informazioni su tutte le firme digitali nel documento di PDF.

1. Iterazione di tutte le firme

   * Scorrere tutte le firme richiamando il metodo `getVerificationInfos` dell&#39;oggetto `PDFDocumentVerificationInfo`. Questo metodo restituisce un oggetto `java.util.List` in cui ogni elemento è un oggetto `PDFSignatureVerificationInfo`. Utilizzare un oggetto `java.util.Iterator` per scorrere l&#39;elenco delle firme.
   * Utilizzando l&#39;oggetto `PDFSignatureVerificationInfo`, è possibile eseguire attività quali la determinazione dello stato della firma richiamando il metodo `getStatus` dell&#39;oggetto `PDFSignatureVerificationInfo`. Questo metodo restituisce un oggetto `SignatureStatus` il cui membro dati statico fornisce informazioni sullo stato della firma. Se ad esempio la firma è sconosciuta, questo metodo restituisce `SignatureStatus.DocumentSignatureUnknown`.

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
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Creare un client di firma

   * Creare un oggetto `SignatureServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `SignatureServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/SignatureService?WSDL`). Non è necessario utilizzare l&#39;attributo `lc_version`. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `SignatureServiceClient.Endpoint.Binding`. Eseguire il cast del valore restituito in `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegnare il nome utente dei moduli AEM al campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Ottiene il documento PDF contenente le firme da verificare

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` memorizza un documento PDF contenente più firme digitali da verificare.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore. Passa un valore stringa che rappresenta la posizione del file del documento PDF e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni della matrice di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare la matrice di byte con i dati di flusso richiamando il metodo `Read` dell&#39;oggetto `System.IO.FileStream`. Passare la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando alla relativa proprietà `MTOM` il contenuto della matrice di byte.

1. Imposta opzioni runtime PKI

   * Creare un oggetto `PKIOptions` utilizzando il relativo costruttore.
   * Impostare il tempo di verifica assegnando al membro dati `verificationTime` dell&#39;oggetto `PKIOptions` un valore di enumerazione `VerificationTime` che specifica il tempo di verifica.
   * Impostare l&#39;opzione di controllo della revoca assegnando al membro dati `revocationCheckStyle` dell&#39;oggetto `PKIOptions` un valore di enumerazione `RevocationCheckStyle` che specifica se eseguire il controllo della revoca.

1. Recupera tutte le firme digitali

   Richiama il metodo `verifyPDFDocument` dell&#39;oggetto `SignatureServiceClient` e passa i seguenti valori:

   * Oggetto `BLOB` contenente un documento PDF contenente più firme digitali.
   * Oggetto `PKIOptions` contenente opzioni di runtime PKI.
   * Istanza `VerifySPIOptions` contenente informazioni SPI. È possibile specificare null per questo parametro.

   Il metodo `verifyPDFDocument` restituisce un oggetto `PDFDocumentVerificationInfo` che contiene informazioni su tutte le firme digitali nel documento di PDF.

1. Iterazione di tutte le firme

   * Scorrere tutte le firme ottenendo il membro dati `verificationInfos` dell&#39;oggetto `PDFDocumentVerificationInfo`. Questo membro dati restituisce un array `Object` in cui ogni elemento è un oggetto `PDFSignatureVerificationInfo`.
   * Utilizzando l&#39;oggetto `PDFSignatureVerificationInfo`, è possibile eseguire attività quali la determinazione dello stato della firma ottenendo il membro dati `status` dell&#39;oggetto `PDFSignatureVerificationInfo`. Questo membro dati restituisce un oggetto `SignatureStatus` il cui membro dati statico fornisce informazioni sullo stato della firma. Se ad esempio la firma è sconosciuta, questo metodo restituisce `SignatureStatus.DocumentSignatureUnknown`.

**Consulta anche**

[Verifica di più firme digitali](#verifying-multiple-digital-signatures)

[Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamare AEM Forms con SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Rimozione di firme digitali {#removing-digital-signatures}

Per poter applicare una firma digitale più recente, è necessario rimuovere le firme digitali da un campo di firma. Impossibile sovrascrivere una firma digitale. Se si tenta di applicare una firma digitale a un campo firma contenente una firma, si verifica un&#39;eccezione.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Signature, vedere [Riferimento ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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

Per informazioni sul percorso di questi file JAR, vedi [Inclusi i file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un client di firma**

Prima di poter eseguire un&#39;operazione del servizio di firma a livello di programmazione, è necessario creare un client del servizio di firma.

**Ottieni il documento PDF che contiene una firma da rimuovere**

Per rimuovere una firma da un documento PDF, è necessario ottenere un documento PDF contenente una firma.

**Rimuovi la firma digitale dal campo della firma**

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

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `SignatureServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Ottiene il documento PDF contenente una firma da rimuovere

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento PDF contenente la firma da rimuovere utilizzando il relativo costruttore e passando un valore stringa che specifica la posizione del documento PDF.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Rimuovi la firma digitale dal campo firma

   Rimuovere una firma digitale da un campo di firma richiamando il metodo `clearSignatureField` dell&#39;oggetto `SignatureServiceClient` e passando i valori seguenti:

   * Oggetto `com.adobe.idp.Document` che rappresenta il documento PDF contenente la firma da rimuovere.
   * Valore string che specifica il nome del campo firma contenente la firma digitale.

   Il metodo `clearSignatureField` restituisce un oggetto `com.adobe.idp.Document` che rappresenta il documento PDF da cui è stata rimossa la firma digitale.

1. Salvare il documento PDF come file PDF

   * Creare un oggetto `java.io.File` e verificare che l&#39;estensione del file sia .pdf.
   * Richiama il metodo `copyToFile` dell&#39;oggetto `com.adobe.idp.Document`. Passa l&#39;oggetto `java.io.File` per copiare il contenuto dell&#39;oggetto `com.adobe.idp.Document` nel file. Assicurarsi di utilizzare l&#39;oggetto `Document` restituito dal metodo `clearSignatureField`.

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
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Creare un client di firma

   * Creare un oggetto `SignatureServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `SignatureServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/SignatureService?WSDL`). Non è necessario utilizzare l&#39;attributo `lc_version`. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `SignatureServiceClient.Endpoint.Binding`. Eseguire il cast del valore restituito in `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegnare il nome utente dei moduli AEM al campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Ottiene il documento PDF contenente una firma da rimuovere

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare un documento PDF che contiene una firma digitale da rimuovere.
   * Creare un oggetto `System.IO.FileStream` richiamandone il costruttore e passando un valore stringa che rappresenta la posizione del file del documento PDF firmato e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni della matrice di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare la matrice di byte con i dati di flusso richiamando il metodo `Read` dell&#39;oggetto `System.IO.FileStream`. Passare la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando la relativa proprietà `MTOM` al contenuto della matrice di byte.

1. Rimuovi la firma digitale dal campo firma

   Rimuovere la firma digitale richiamando il metodo `clearSignatureField` dell&#39;oggetto `SignatureServiceClient` e passando i valori seguenti:

   * Oggetto `BLOB` contenente il documento PDF firmato.
   * Valore string che rappresenta il nome del campo firma contenente la firma digitale da rimuovere.

   Il metodo `clearSignatureField` restituisce un oggetto `BLOB` che rappresenta il documento PDF da cui è stata rimossa la firma digitale.

1. Salvare il documento PDF come file PDF

   * Creare un oggetto `System.IO.FileStream` richiamandone il costruttore e passando un valore stringa che rappresenta la posizione del file del documento PDF contenente un campo firma vuoto e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `BLOB` restituito dal metodo `sign`. Popolare la matrice di byte ottenendo il valore del membro dati `MTOM` dell&#39;oggetto `BLOB`.
   * Creare un oggetto `System.IO.BinaryWriter` richiamandone il costruttore e passando l&#39;oggetto `System.IO.FileStream`.
   * Scrivere il contenuto della matrice di byte nel file PDF richiamando il metodo `Write` dell&#39;oggetto `System.IO.BinaryWriter` e passando la matrice di byte.

**Consulta anche**

[Rimozione di firme digitali](digitally-signing-certifying-documents.md#removing-digital-signatures)

[Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamare AEM Forms con SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
