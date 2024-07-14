---
title: Crittografia e decrittografia dei documenti di PDF
description: Utilizzare il servizio Crittografia per crittografare e decrittografare i documenti. Le attività del servizio Crittografia includono la crittografia di un documento PDF con una password, la crittografia di un documento PDF con un certificato, la rimozione della crittografia basata su password da un documento PDF, la rimozione della crittografia basata su certificato da un documento PDF, lo sblocco del documento PDF in modo da consentire l'esecuzione di altre operazioni del servizio e la determinazione del tipo di crittografia di un documento PDF protetto.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: d3cbca7f-9277-4d61-b198-abf4bb008f15
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '8133'
ht-degree: 0%

---

# Crittografia e decrittografia dei documenti di PDF {#encrypting-and-decrypting-pdf-documents}

**Gli esempi e gli esempi contenuti in questo documento sono solo per AEM Forms in ambiente JEE.**

**Informazioni sul servizio di crittografia**

Il servizio Crittografia consente di crittografare e decrittografare i documenti. Quando un documento viene crittografato, il suo contenuto diventa illeggibile. Un utente autorizzato può decrittografare il documento per ottenere l’accesso al contenuto. Se un documento PDF è crittografato con una password, l’utente deve specificare la password di apertura prima che il documento possa essere visualizzato in Adobe Reader o Adobe Acrobat. Analogamente, se un documento PDF è crittografato con un certificato, l’utente deve decrittografare il documento PDF con la chiave pubblica corrispondente al certificato (chiave privata) utilizzato per crittografare il documento PDF.

È possibile eseguire queste operazioni utilizzando il servizio Crittografia:

* Crittografa un documento PDF con una password. (Vedi [Crittografia dei documenti di PDF con una password](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password).)
* Crittografa un documento PDF con un certificato. (Vedi [Crittografia dei documenti di PDF con i certificati](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates).)
* Rimuovere la crittografia basata su password da un documento PDF. (Vedi [Rimozione della crittografia password](encrypting-decrypting-pdf-documents.md#removing-password-encryption).)
* Rimuovere la crittografia basata su certificato da un documento PDF. (Vedi [Rimozione della crittografia basata su certificato](encrypting-decrypting-pdf-documents.md#removing-certificate-based-encryption).)
* Sblocca il documento PDF in modo da poter eseguire altre operazioni di servizio. Dopo lo sblocco di un documento PDF crittografato con password, ad esempio, è possibile applicare una firma digitale. (Vedi [Sblocco dei documenti di Crittografia PDF](encrypting-decrypting-pdf-documents.md#unlocking-encrypted-pdf-documents).)
* Determinare il tipo di crittografia di un documento PDF protetto. (Vedere [Determinazione del tipo di crittografia](encrypting-decrypting-pdf-documents.md#determining-encryption-type).)

>[!NOTE]
>
>Per ulteriori informazioni sul servizio di crittografia, vedere [Riferimento ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Crittografia di documenti PDF con una password {#encrypting-pdf-documents-with-a-password}

Quando crittografi un documento PDF con una password, un utente deve specificare la password per aprire il documento PDF in Adobe Reader o Acrobat. Inoltre, prima di poter eseguire sul documento un’altra operazione di AEM Forms, ad esempio la firma digitale del documento di PDF, è necessario sbloccare un documento di PDF crittografato con password.

>[!NOTE]
>
>Se carichi un documento PDF crittografato nell’archivio AEM Forms, non può decrittografare il documento PDF ed estrarre il contenuto XDP. È consigliabile non crittografare un documento prima di caricarlo nell’archivio AEM Forms. (Vedi [Scrittura delle risorse](/help/forms/developing/aem-forms-repository.md#writing-resources).)

>[!NOTE]
>
>Per ulteriori informazioni sul servizio di crittografia, vedere [Riferimento ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary-of-steps}

Per crittografare un documento PDF con una password, effettuare le seguenti operazioni:

1. Includi file di progetto.
1. Creare un oggetto API client di crittografia.
1. Ottieni un documento PDF da crittografare.
1. Impostare le opzioni di runtime della crittografia.
1. Aggiungi la password.
1. Salvare il documento PDF crittografato come file PDF.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso della classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è implementato su JBoss)
* jbossall-client.jar (obbligatorio se AEM Forms è distribuito su JBoss)

**Creare un oggetto API client di crittografia**

Per eseguire un&#39;operazione del servizio di crittografia a livello di programmazione, è necessario creare un client del servizio di crittografia.

**Ottieni un documento PDF da crittografare**

Ottieni un documento PDF non crittografato per crittografare il documento con una password. Se si tenta di proteggere un documento PDF già crittografato, viene generata un&#39;eccezione.

**Impostare le opzioni di runtime della crittografia**

Per crittografare un documento PDF con una password, è necessario specificare quattro valori, inclusi due valori di password. Il primo valore della password viene utilizzato per crittografare il documento PDF e deve essere specificato all&#39;apertura del documento PDF. Il secondo valore della password, denominato password master, viene utilizzato per rimuovere la crittografia dal documento PDF. I valori delle password fanno distinzione tra maiuscole e minuscole e non possono essere uguali.

Specificare le risorse del documento PDF da crittografare. È possibile crittografare l’intero documento PDF, tutto tranne i metadati del documento o solo gli allegati del documento. Se si crittografano solo gli allegati del documento, a un utente viene richiesta una password quando tenta di accedere ai file allegati.

Quando si crittografa un documento PDF, è possibile specificare le autorizzazioni associate al documento protetto. Specificando le autorizzazioni, è possibile controllare le azioni che un utente che apre un documento PDF crittografato con password può eseguire. Ad esempio, per estrarre correttamente i dati del modulo, è necessario impostare le seguenti autorizzazioni:

* PASSWORD_EDIT_ADD
* PASSWORD_EDIT_MODIFY

>[!NOTE]
>
>Le autorizzazioni sono specificate come `PasswordEncryptionPermission` valori di enumerazione.

**Aggiungi la password**

Dopo aver recuperato un documento di PDF non protetto e aver impostato i valori di runtime della crittografia, è possibile aggiungere una password al documento di PDF.

**Salvare il documento PDF crittografato come file PDF**

È possibile salvare il documento PDF crittografato con password come file PDF.

**Consulta anche**

[Crittografare un documento PDF utilizzando l’API Java](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-using-the-java-api)

[Crittografia di un documento PDF tramite l’API del servizio web](encrypting-decrypting-pdf-documents.md#encrypting-a-pdf-document-using-the-web-service-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API servizio di crittografia](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[Crittografia di documenti PDF con certificati](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates)

### Crittografare un documento PDF utilizzando l’API Java {#encrypt-a-pdf-document-using-the-java-api}

Crittografa un documento PDF con una password utilizzando l’API di crittografia (Java):

1. Includi file di progetto.

   Includi i file JAR dei client, ad esempio adobe-encryption-client.jar, nel percorso di classe del progetto Java.

1. Creare un&#39;API client di crittografia.

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `EncryptionServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Ottieni un documento PDF da crittografare.

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento PDF da crittografare utilizzando il relativo costruttore e passando un valore stringa che specifica la posizione del documento PDF.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Impostare le opzioni di runtime della crittografia.

   * Creare un oggetto `PasswordEncryptionOptionSpec` richiamando il relativo costruttore.
   * Specificare le risorse documento PDF da crittografare richiamando il metodo `setEncryptOption` dell&#39;oggetto `PasswordEncryptionOptionSpec` e passando un valore di enumerazione `PasswordEncryptionOption` che specifica le risorse documento da crittografare. Per crittografare, ad esempio, l&#39;intero documento di PDF, inclusi i metadati e gli allegati, specificare `PasswordEncryptionOption.ALL`.
   * Creare un oggetto `java.util.List` che memorizza le autorizzazioni di crittografia utilizzando il costruttore `ArrayList`.
   * Specificare un&#39;autorizzazione richiamando il metodo `add` dell&#39;oggetto `java.util.List` e passando un valore di enumerazione corrispondente all&#39;autorizzazione che si desidera impostare. Per impostare ad esempio l&#39;autorizzazione che consente a un utente di copiare i dati nel documento PDF, specificare `PasswordEncryptionPermission.PASSWORD_EDIT_COPY`. (Ripeti questo passaggio per ogni autorizzazione da impostare).
   * Specificare l&#39;opzione di compatibilità Acrobat richiamando il metodo `setCompatability` dell&#39;oggetto `PasswordEncryptionOptionSpec` e passando un valore di enumerazione che specifica il livello di compatibilità Acrobat. Ad esempio, è possibile specificare `PasswordEncryptionCompatability.ACRO_7`.
   * Specificare il valore della password che consente a un utente di aprire il documento PDF crittografato richiamando il metodo `setDocumentOpenPassword` dell&#39;oggetto `PasswordEncryptionOptionSpec` e passando un valore stringa che rappresenta la password di apertura.
   * Specificare il valore della password master che consente a un utente di rimuovere la crittografia dal documento PDF richiamando il metodo `setPermissionPassword` dell&#39;oggetto `PasswordEncryptionOptionSpec` e passando un valore stringa che rappresenta la password master.

1. Aggiungi la password.

   Crittografare il documento PDF richiamando il metodo `encryptPDFUsingPassword` dell&#39;oggetto `EncryptionServiceClient` e passando i valori seguenti:

   * L&#39;oggetto `com.adobe.idp.Document` che contiene il documento PDF da crittografare con la password.
   * L&#39;oggetto `PasswordEncryptionOptionSpec` che contiene le opzioni di runtime della crittografia.

   Il metodo `encryptPDFUsingPassword` restituisce un oggetto `com.adobe.idp.Document` contenente un documento PDF crittografato con password.

1. Salvare il documento PDF crittografato come file PDF.

   * Creare un oggetto `java.io.File` e verificare che l&#39;estensione del file sia .pdf.
   * Richiama il metodo `copyToFile` dell&#39;oggetto `com.adobe.idp.Document` per copiare il contenuto dell&#39;oggetto `com.adobe.idp.Document` nel file. Assicurarsi di utilizzare l&#39;oggetto `com.adobe.idp.Document` restituito dal metodo `encryptPDFUsingPassword`.

**Consulta anche**

[Riepilogo dei passaggi](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Quick Start (modalità SOAP): crittografia di un documento PDF tramite l’API Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-encrypting-a-pdf-document-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)


[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Crittografia di un documento PDF tramite l’API del servizio web {#encrypting-a-pdf-document-using-the-web-service-api}

Crittografa un documento PDF con una password utilizzando l’API di crittografia (servizio web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Creare un oggetto API client di crittografia.

   * Creare un oggetto `EncryptionServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `EncryptionServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/EncryptionService?WSDL`). Non è necessario utilizzare l&#39;attributo `lc_version`. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `EncryptionServiceClient.Endpoint.Binding`. Eseguire il cast del valore restituito in `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegnare il nome utente dei moduli AEM al campo `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Ottieni un documento PDF da crittografare.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare un documento PDF crittografato con una password.
   * Creare un oggetto `System.IO.FileStream` richiamandone il costruttore e passando un valore stringa che rappresenta la posizione del file del documento PDF da crittografare e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni della matrice di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare la matrice di byte con i dati di flusso richiamando il metodo `Read` dell&#39;oggetto `System.IO.FileStream` e passando la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando il contenuto della matrice di byte al membro dati `MTOM` dell&#39;oggetto `BLOB`.

1. Impostare le opzioni di runtime della crittografia.

   * Creare un oggetto `PasswordEncryptionOptionSpec` utilizzando il relativo costruttore.
   * Specificare le risorse del documento PDF da crittografare assegnando un valore di enumerazione `PasswordEncryptionOption` al membro dati `encryptOption` dell&#39;oggetto `PasswordEncryptionOptionSpec`. Per crittografare l&#39;intero PDF, inclusi i metadati e gli allegati, assegnare `PasswordEncryptionOption.ALL` a questo membro dati.
   * Specificare l&#39;opzione di compatibilità di Acrobat assegnando un valore di enumerazione `PasswordEncryptionCompatability` al membro dati `compatability` dell&#39;oggetto `PasswordEncryptionOptionSpec`. Ad esempio, assegnare `PasswordEncryptionCompatability.ACRO_7` a questo membro dati.
   * Specificare il valore della password che consente a un utente di aprire il documento PDF crittografato assegnando un valore stringa che rappresenta la password di apertura al membro dati `documentOpenPassword` dell&#39;oggetto `PasswordEncryptionOptionSpec`.
   * Specificare il valore della password che consente a un utente di rimuovere la crittografia dal documento PDF assegnando un valore stringa che rappresenta la password master al membro dati `permissionPassword` dell&#39;oggetto `PasswordEncryptionOptionSpec`.

1. Aggiungi la password.

   Crittografare il documento PDF richiamando il metodo `encryptPDFUsingPassword` dell&#39;oggetto `EncryptionServiceClient` e passando i valori seguenti:

   * L&#39;oggetto `BLOB` che contiene il documento PDF da crittografare con la password.
   * L&#39;oggetto `PasswordEncryptionOptionSpec` che contiene le opzioni di runtime della crittografia.

   Il metodo `encryptPDFUsingPassword` restituisce un oggetto `BLOB` contenente un documento PDF crittografato con password.

1. Salvare il documento PDF crittografato come file PDF.

   * Creare un oggetto `System.IO.FileStream` richiamandone il costruttore e passando un valore stringa che rappresenta la posizione del file del documento PDF protetto.
   * Creare una matrice di byte che memorizza il contenuto dei dati dell&#39;oggetto `BLOB` restituito dal metodo `encryptPDFUsingPassword`. Popolare la matrice di byte ottenendo il valore del membro dati `MTOM` dell&#39;oggetto `BLOB`.
   * Creare un oggetto `System.IO.BinaryWriter` richiamandone il costruttore e passando l&#39;oggetto `System.IO.FileStream`.
   * Scrivere il contenuto della matrice di byte in un file PDF richiamando il metodo `Write` dell&#39;oggetto `System.IO.BinaryWriter` e passando la matrice di byte.

**Consulta anche**

[Riepilogo dei passaggi](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamare AEM Forms con SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Crittografia di documenti PDF con certificati {#encrypting-pdf-documents-with-certificates}

La crittografia basata su certificato consente di crittografare un documento per destinatari specifici tramite la tecnologia a chiave pubblica. È possibile assegnare a diversi destinatari autorizzazioni diverse per il documento. Molti aspetti della crittografia sono resi possibili dalla tecnologia a chiave pubblica. Viene utilizzato un algoritmo per generare due numeri di grandi dimensioni, noti come *chiavi*, che hanno le seguenti proprietà:

* Una chiave viene utilizzata per crittografare un set di dati. Successivamente, solo l&#39;altra chiave può essere utilizzata per decrittografare i dati.
* È impossibile distinguere una chiave dall&#39;altra.

Una delle chiavi funge da chiave privata dell’utente. È importante che solo l’utente abbia accesso a questa chiave. L’altra chiave è la chiave pubblica dell’utente, che può essere condivisa con altri utenti.

Un certificato a chiave pubblica contiene la chiave pubblica e le informazioni di identificazione di un utente. Il formato X.509 viene utilizzato per l’archiviazione dei certificati. I certificati vengono generalmente rilasciati e firmati digitalmente da un&#39;autorità di certificazione (CA), un&#39;entità riconosciuta che fornisce una misura di affidabilità nella validità del certificato. I certificati hanno una data di scadenza dopo la quale non sono più validi. Inoltre, gli elenchi di revoche di certificati (CRL) forniscono informazioni sui certificati revocati prima della data di scadenza. I CRL vengono pubblicati periodicamente dalle autorità di certificazione. Lo stato di revoca di un certificato può essere recuperato anche tramite il protocollo OCSP (Online Certificate Status Protocol) in rete.

>[!NOTE]
>
>Se carichi un documento PDF crittografato nell’archivio AEM Forms, non può decrittografare il documento PDF ed estrarre il contenuto XDP. È consigliabile non crittografare un documento prima di caricarlo nell’archivio AEM Forms. (Vedi [Scrittura delle risorse](/help/forms/developing/aem-forms-repository.md#writing-resources).)

>[!NOTE]
>
>Prima di poter crittografare un documento PDF con un certificato, è necessario assicurarsi di aggiungere il certificato ad AEM Forms. Un certificato viene aggiunto utilizzando la console di amministrazione o a livello di programmazione utilizzando l’API di Trust Manager. (Vedere [Importazione delle credenziali tramite l&#39;API di Gestione trust](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api).)

>[!NOTE]
>
>Per ulteriori informazioni sul servizio di crittografia, vedere [Riferimento ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-1}

Per crittografare un documento PDF con un certificato, effettuare le seguenti operazioni:

1. Includi file di progetto.
1. Creare un oggetto API client di crittografia.
1. Ottieni un documento PDF da crittografare.
1. Fai riferimento al certificato.
1. Impostare le opzioni di runtime della crittografia.
1. Crea un documento PDF crittografato con certificato.
1. Salvare il documento PDF crittografato come file PDF.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso della classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è distribuito sul server applicazioni JBoss)
* jbossall-client.jar (richiesto se AEM Forms è distribuito sul server applicazioni JBoss)

**Creare un oggetto API client di crittografia**

Per eseguire un&#39;operazione del servizio di crittografia a livello di programmazione, è necessario creare un client del servizio di crittografia. Se si utilizza l&#39;API del servizio di crittografia Java, creare un oggetto `EncrytionServiceClient`. Se si utilizza l&#39;API Servizio di crittografia del servizio Web, creare un oggetto `EncryptionServiceService`.

**Ottieni un documento PDF da crittografare**

Ottieni un documento PDF non crittografato da crittografare. Se si tenta di proteggere un documento PDF già crittografato, viene generata un&#39;eccezione.

**Fai riferimento al certificato**

Per crittografare un documento PDF con un certificato, fare riferimento a un certificato utilizzato per crittografare un documento PDF. Il certificato è un file cer, crt o pem. Un file PKCS#12 viene utilizzato per memorizzare le chiavi private con i certificati corrispondenti.

Quando si crittografa un documento PDF con un certificato, specificare le autorizzazioni associate al documento protetto. Specificando le autorizzazioni, è possibile controllare le azioni che un utente che apre un documento PDF crittografato con certificato può eseguire.

**Impostare le opzioni di runtime della crittografia**

Specificare le risorse del documento PDF da crittografare. È possibile crittografare l’intero documento PDF, tutto tranne i metadati del documento o solo gli allegati del documento.

**Crea un documento PDF crittografato con certificato**

Dopo aver recuperato un documento di PDF non protetto, aver fatto riferimento al certificato e aver impostato le opzioni di runtime, è possibile creare un documento di PDF crittografato con certificato. Dopo aver crittografato il documento PDF, è necessario utilizzare la chiave pubblica corrispondente per decrittografarlo.

**Salvare il documento PDF crittografato come file PDF**

È possibile salvare il documento PDF crittografato come file PDF.

**Consulta anche**

[Crittografare un documento PDF con un certificato utilizzando l’API Java](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-with-a-certificate-using-the-java-api)

[Crittografare un documento PDF con un certificato utilizzando l’API del servizio web](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-with-a-certificate-using-the-web-service-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API servizio di crittografia](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[Crittografia di documenti PDF con una password](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Crittografare un documento PDF con un certificato utilizzando l’API Java {#encrypt-a-pdf-document-with-a-certificate-using-the-java-api}

Crittografa un documento PDF con un certificato utilizzando l’API di crittografia (Java):

1. Includi file di progetto.

   Includi i file JAR dei client, ad esempio adobe-encryption-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto API client di crittografia.

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `EncryptionServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Ottieni un documento PDF da crittografare.

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento PDF da crittografare utilizzando il relativo costruttore e passando un valore stringa che specifica la posizione del documento PDF.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Fai riferimento al certificato.

   * Creare un oggetto `java.util.List` che memorizza le informazioni sulle autorizzazioni utilizzando il relativo costruttore.
   * Specificare l&#39;autorizzazione associata al documento crittografato richiamando il metodo `add` dell&#39;oggetto `java.util.List` e passando un valore di enumerazione `CertificateEncryptionPermissions` che rappresenta le autorizzazioni concesse all&#39;utente che apre il documento PDF protetto. Ad esempio, per specificare tutte le autorizzazioni, passare `CertificateEncryptionPermissions.PKI_ALL_PERM`.
   * Creare un oggetto `Recipient` utilizzando il relativo costruttore.
   * Creare un oggetto `java.io.FileInputStream` che rappresenta il certificato utilizzato per crittografare il documento PDF utilizzando il relativo costruttore e passando un valore stringa che specifica la posizione del certificato.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream` che rappresenta il certificato.
   * Richiama il metodo `setX509Cert` dell&#39;oggetto `Recipient` e passa l&#39;oggetto `com.adobe.idp.Document` che contiene il certificato. Inoltre, l&#39;oggetto `Recipient` può avere un alias di certificato Truststore o un URL LDAP come origine di certificato.
   * Creare un oggetto `CertificateEncryptionIdentity` che memorizza le informazioni sulle autorizzazioni e sui certificati utilizzando il relativo costruttore.
   * Richiama il metodo `setPerms` dell&#39;oggetto `CertificateEncryptionIdentity` e passa l&#39;oggetto `java.util.List` che memorizza le informazioni sulle autorizzazioni.
   * Richiama il metodo `setRecipient` dell&#39;oggetto `CertificateEncryptionIdentity` e passa l&#39;oggetto `Recipient` che memorizza le informazioni sul certificato.
   * Creare un oggetto `java.util.List` che memorizza le informazioni sul certificato utilizzando il relativo costruttore.
   * Richiama il metodo add dell&#39;oggetto `java.util.List` e passa l&#39;oggetto `CertificateEncryptionIdentity`. L&#39;oggetto `java.util.List` viene passato come parametro al metodo `encryptPDFUsingCertificates`.

1. Impostare le opzioni di runtime della crittografia.

   * Creare un oggetto `CertificateEncryptionOptionSpec` richiamando il relativo costruttore.
   * Specificare le risorse documento PDF da crittografare richiamando il metodo `setOption` dell&#39;oggetto `CertificateEncryptionOptionSpec` e passando un valore di enumerazione `CertificateEncryptionOption` che specifica le risorse documento da crittografare. Per crittografare, ad esempio, l&#39;intero documento di PDF, inclusi i metadati e gli allegati, specificare `CertificateEncryptionOption.ALL`.
   * Specificare l&#39;opzione di compatibilità Acrobat richiamando il metodo `setCompat` dell&#39;oggetto `CertificateEncryptionOptionSpec` e passando un valore di enumerazione `CertificateEncryptionCompatibility` che specifica il livello di compatibilità Acrobat. Ad esempio, è possibile specificare `CertificateEncryptionCompatibility.ACRO_7`.

1. Crea un documento PDF crittografato con certificato.

   Crittografare il documento PDF con un certificato richiamando il metodo `encryptPDFUsingCertificates` dell&#39;oggetto `EncryptionServiceClient` e passando i valori seguenti:

   * L&#39;oggetto `com.adobe.idp.Document` che contiene il documento PDF da crittografare.
   * Oggetto `java.util.List` che memorizza le informazioni sul certificato.
   * L&#39;oggetto `CertificateEncryptionOptionSpec` che contiene le opzioni di runtime della crittografia.

   Il metodo `encryptPDFUsingCertificates` restituisce un oggetto `com.adobe.idp.Document` contenente un documento PDF crittografato con certificato.

1. Salvare il documento PDF crittografato come file PDF.

   * Creare un oggetto `java.io.File` e verificare che l&#39;estensione del nome file sia pdf.
   * Richiama il metodo `copyToFile` dell&#39;oggetto `com.adobe.idp.Document` per copiare il contenuto dell&#39;oggetto `com.adobe.idp.Document` nel file. Assicurarsi di utilizzare l&#39;oggetto `com.adobe.idp.Document` restituito dal metodo `encryptPDFUsingCertificates`.

**Consulta anche**

[Riepilogo dei passaggi](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Guida rapida (modalità SOAP): crittografia di un documento PDF con un certificato tramite l’API Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-encrypting-a-pdf-document-with-a-certificate-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Crittografare un documento PDF con un certificato utilizzando l’API del servizio web {#encrypt-a-pdf-document-with-a-certificate-using-the-web-service-api}

Crittografa un documento PDF con un certificato utilizzando l’API di crittografia (servizio web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Creare un oggetto API client di crittografia.

   * Creare un oggetto `EncryptionServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `EncryptionServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/EncryptionService?WSDL`). Non è necessario utilizzare l&#39;attributo `lc_version`. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `EncryptionServiceClient.Endpoint.Binding`. Eseguire il cast del valore restituito in `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegnare il nome utente dei moduli AEM al campo `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Ottieni un documento PDF da crittografare.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per archiviare un documento PDF crittografato con un certificato.
   * Creare un oggetto `System.IO.FileStream` richiamandone il costruttore e passando un valore stringa che rappresenta la posizione del file del documento PDF da crittografare e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni della matrice di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare la matrice di byte con i dati di flusso richiamando il metodo `Read` dell&#39;oggetto `System.IO.FileStream` e passando la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando la relativa proprietà `MTOM` al contenuto della matrice di byte.

1. Fai riferimento al certificato.

   * Creare un oggetto `Recipient` utilizzando il relativo costruttore. Questo oggetto memorizzerà le informazioni sul certificato.
   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. Questo oggetto `BLOB` memorizzerà il certificato che crittografa il documento PDF.
   * Creare un oggetto `System.IO.FileStream` richiamandone il costruttore e passando un valore stringa che rappresenta la posizione del file del certificato e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni della matrice di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare la matrice di byte con i dati di flusso richiamando il metodo `Read` dell&#39;oggetto `System.IO.FileStream` e passando la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando il contenuto della matrice di byte al membro dati `MTOM` dell&#39;oggetto `BLOB`.
   * Assegnare l&#39;oggetto `BLOB` che memorizza il certificato al membro dati `x509Cert` dell&#39;oggetto `Recipient`.
   * Creare un oggetto `CertificateEncryptionIdentity` che memorizza le informazioni sul certificato utilizzando il relativo costruttore.
   * Assegnare l&#39;oggetto `Recipient` che memorizza il certificato al membro dati destinatario dell&#39;oggetto `CertificateEncryptionIdentity`.
   * Creare un array `Object` e assegnare l&#39;oggetto `CertificateEncryptionIdentity` al primo elemento dell&#39;array `Object`. Questo array `Object` è passato come parametro al metodo `encryptPDFUsingCertificates`.

1. Impostare le opzioni di runtime della crittografia.

   * Creare un oggetto `CertificateEncryptionOptionSpec` utilizzando il relativo costruttore.
   * Specificare le risorse del documento PDF da crittografare assegnando un valore di enumerazione `CertificateEncryptionOption` al membro dati `option` dell&#39;oggetto `CertificateEncryptionOptionSpec`. Per crittografare l&#39;intero documento PDF, inclusi i metadati e gli allegati, assegnare `CertificateEncryptionOption.ALL` a questo membro dati.
   * Specificare l&#39;opzione di compatibilità di Acrobat assegnando un valore di enumerazione `CertificateEncryptionCompatibility` al membro dati `compat` dell&#39;oggetto `CertificateEncryptionOptionSpec`. Ad esempio, assegnare `CertificateEncryptionCompatibility.ACRO_7` a questo membro dati.

1. Crea un documento PDF crittografato con certificato.

   Crittografare il documento PDF con un certificato richiamando il metodo `encryptPDFUsingCertificates` dell&#39;oggetto `EncryptionServiceService` e passando i valori seguenti:

   * L&#39;oggetto `BLOB` che contiene il documento PDF da crittografare.
   * L&#39;array `Object` che memorizza le informazioni sul certificato.
   * L&#39;oggetto `CertificateEncryptionOptionSpec` che contiene le opzioni di runtime della crittografia.

   Il metodo `encryptPDFUsingCertificates` restituisce un oggetto `BLOB` contenente un documento PDF crittografato con certificato.

1. Salvare il documento PDF crittografato come file PDF.

   * Creare un oggetto `System.IO.FileStream` richiamandone il costruttore e passando un valore stringa che rappresenta la posizione del file del documento PDF protetto.
   * Creare una matrice di byte che memorizza il contenuto dei dati dell&#39;oggetto `BLOB` restituito dal metodo `encryptPDFUsingCertificates`. Popolare la matrice di byte ottenendo il valore del membro dati `binaryData` dell&#39;oggetto `BLOB`.
   * Creare un oggetto `System.IO.BinaryWriter` richiamandone il costruttore e passando l&#39;oggetto `System.IO.FileStream`.
   * Scrivere il contenuto della matrice di byte in un file PDF richiamando il metodo `Write` dell&#39;oggetto `System.IO.BinaryWriter` e passando la matrice di byte.

**Consulta anche**

[Riepilogo dei passaggi](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamare AEM Forms con SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Rimozione della crittografia basata su certificati {#removing-certificate-based-encryption}

La crittografia basata su certificato può essere rimossa da un documento PDF PDF in modo che gli utenti possano aprirlo in Adobe Reader o Acrobat. Per rimuovere la crittografia da un documento PDF crittografato con un certificato, è necessario fare riferimento a una chiave pubblica. Una volta rimossa da un documento PDF, la crittografia non è più protetta.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio di crittografia, vedere [Riferimento ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-2}

Per rimuovere la crittografia basata su certificato da un documento PDF, effettuare le seguenti operazioni:

1. Includi file di progetto.
1. Creare un client del servizio di crittografia.
1. Ottieni il documento PDF crittografato.
1. Rimuovi la crittografia.
1. Salvare il documento PDF come file PDF.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso della classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è distribuito sul server applicazioni JBoss)
* jbossall-client.jar (richiesto se AEM Forms è distribuito sul server applicazioni JBoss)

**Creare un client del servizio di crittografia**

Per eseguire un&#39;operazione del servizio di crittografia a livello di programmazione, è necessario creare un client del servizio di crittografia. Se si utilizza l&#39;API del servizio di crittografia Java, creare un oggetto `EncrytionServiceClient`. Se si utilizza l&#39;API Servizio di crittografia del servizio Web, creare un oggetto `EncryptionServiceService`.

**Ottieni il documento crittografato di PDF**

Ottieni un documento PDF crittografato per rimuovere la crittografia basata su certificati. Se si tenta di rimuovere la crittografia da un documento PDF non crittografato, viene generata un&#39;eccezione. Analogamente, se si tenta di rimuovere la crittografia basata su certificato da un documento crittografato con password, viene generata un&#39;eccezione.

**Rimuovi crittografia**

Per rimuovere la crittografia basata su certificato da un documento PDF crittografato, è necessario disporre di un documento PDF crittografato e della chiave privata corrispondente alla chiave utilizzata per crittografare il documento PDF. Il valore alias della chiave privata viene specificato quando si rimuove la crittografia basata su certificati da un documento di PDF crittografato. Per informazioni sulla chiave pubblica, vedere [Crittografia dei documenti di PDF con i certificati](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates).

>[!NOTE]
>
>Una chiave privata viene memorizzata nell&#39;archivio fonti attendibili di AEM Forms. Quando viene inserito un certificato, viene specificato un valore alias.

**Salva il documento PDF**

Dopo aver rimosso la crittografia basata su certificati da un documento PDF crittografato, è possibile salvare il documento PDF come file PDF. Gli utenti possono aprire il documento PDF in Adobe Reader o Acrobat.

**Consulta anche**

[Rimuovere la crittografia basata su certificati utilizzando l’API Java](encrypting-decrypting-pdf-documents.md#remove-certificate-based-encryption-using-the-java-api)

[Rimuovi la crittografia basata su certificati utilizzando l’API del servizio web](encrypting-decrypting-pdf-documents.md#remove-certificate-based-encryption-using-the-web-service-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API servizio di crittografia](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

### Rimuovere la crittografia basata su certificati utilizzando l’API Java {#remove-certificate-based-encryption-using-the-java-api}

Rimuovi la crittografia basata su certificato da un documento PDF utilizzando l’API di crittografia (Java):

1. Includi file di progetto.

   Includi i file JAR dei client, ad esempio adobe-encryption-client.jar, nel percorso di classe del progetto Java.

1. Creare un client del servizio di crittografia.

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `EncryptionServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Ottieni il documento PDF crittografato.

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento PDF crittografato utilizzando il relativo costruttore e passando un valore stringa che specifica la posizione del documento PDF crittografato.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Rimuovi la crittografia.

   Rimuovere la crittografia basata su certificato dal documento PDF richiamando il metodo `removePDFCertificateSecurity` dell&#39;oggetto `EncryptionServiceClient` e passando i valori seguenti:

   * L&#39;oggetto `com.adobe.idp.Document` che contiene il documento PDF crittografato.
   * Valore stringa che specifica il nome alias della chiave privata corrispondente alla chiave utilizzata per crittografare il documento PDf.

   Il metodo `removePDFCertificateSecurity` restituisce un oggetto `com.adobe.idp.Document` contenente un documento PDF non protetto.

1. Salvare il documento PDF.

   * Creare un oggetto `java.io.File` e verificare che l&#39;estensione del file sia .pdf.
   * Richiama il metodo `copyToFile` dell&#39;oggetto `com.adobe.idp.Document` per copiare il contenuto dell&#39;oggetto `Document` nel file. Assicurarsi di utilizzare l&#39;oggetto `com.adobe.idp.Document` restituito dal metodo `removePDFCredentialSecurity`.

**Consulta anche**

[Riepilogo dei passaggi](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Quick Start (modalità SOAP): rimozione della crittografia basata su certificati tramite l’API Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-removing-certificate-based-encryption-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Rimuovi la crittografia basata su certificati utilizzando l’API del servizio web {#remove-certificate-based-encryption-using-the-web-service-api}

Rimuovi la crittografia basata su certificato utilizzando l’API di crittografia (servizio web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Creare un client del servizio di crittografia.

   * Creare un oggetto `EncryptionServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `EncryptionServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/EncryptionService?WSDL`). Non è necessario utilizzare l&#39;attributo `lc_version`. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `EncryptionServiceClient.Endpoint.Binding`. Eseguire il cast del valore restituito in `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegnare il nome utente dei moduli AEM al campo `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Ottieni il documento PDF crittografato.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per archiviare il documento PDF crittografato.
   * Creare un oggetto `System.IO.FileStream` richiamandone il costruttore e passando un valore stringa che rappresenta la posizione del file del documento PDF crittografato e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni della matrice di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare la matrice di byte con i dati di flusso richiamando il metodo `Read` dell&#39;oggetto `System.IO.FileStream` e passando la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando il contenuto della matrice di byte al membro dati `MTOM` dell&#39;oggetto `BLOB`.

1. Rimuovi la crittografia.

   Richiama il metodo `removePDFCertificateSecurity` dell&#39;oggetto `EncryptionServiceClient` e passa i seguenti valori:

   * L&#39;oggetto `BLOB` che contiene i dati del flusso di file che rappresenta un documento PDF crittografato.
   * Valore string che specifica il nome alias della chiave pubblica corrispondente alla chiave privata utilizzata per crittografare il documento PDf.

   Il metodo `removePDFCredentialSecurity` restituisce un oggetto `BLOB` contenente un documento PDF non protetto.

1. Salvare il documento PDF.

   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore stringa che rappresenta la posizione del file del documento PDF non protetto.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `BLOB` restituito dal metodo `removePDFPasswordSecurity`. Popolare la matrice di byte ottenendo il valore del membro dati `MTOM` dell&#39;oggetto `BLOB`.
   * Creare un oggetto `System.IO.BinaryWriter` richiamandone il costruttore e passando l&#39;oggetto `System.IO.FileStream`.
   * Scrivere il contenuto della matrice di byte in un file PDF richiamando il metodo `Write` dell&#39;oggetto `System.IO.BinaryWriter` e passando la matrice di byte.

**Consulta anche**

[Riepilogo dei passaggi](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamare AEM Forms con SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Rimozione di Crittografia password {#removing-password-encryption}

La crittografia basata su password può essere rimossa da un documento PDF PDF in modo che gli utenti possano aprirlo in Adobe Reader o Acrobat senza dover specificare una password. Dopo la rimozione della crittografia basata su password da un documento PDF, il documento non è più protetto.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio di crittografia, vedere [Riferimento ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-3}

Per rimuovere la crittografia basata su password da un documento PDF, effettuare le seguenti operazioni:

1. Includi file di progetto
1. Creare un client del servizio di crittografia.
1. Ottieni il documento PDF crittografato.
1. Rimuovi la password.
1. Salvare il documento PDF come file PDF.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso della classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è implementato su JBoss)
* jbossall-client.jar (obbligatorio se AEM Forms è distribuito su JBoss)

**Creare un client del servizio di crittografia**

Per eseguire un&#39;operazione del servizio di crittografia a livello di programmazione, è necessario creare un client del servizio di crittografia. Se si utilizza l&#39;API del servizio di crittografia Java, creare un oggetto `EncrytionServiceClient`. Se si utilizza l&#39;API Servizio di crittografia del servizio Web, creare un oggetto `EncryptionServiceService`.

**Ottieni il documento crittografato di PDF**

Ottieni un documento PDF crittografato per rimuovere la crittografia basata su password. Se si tenta di rimuovere la crittografia da un documento PDF non crittografato, viene generata un&#39;eccezione.

**Rimuovi la password**

Per rimuovere la crittografia basata su password da un documento PDF crittografato, è necessario disporre di un documento PDF crittografato e di un valore di password master utilizzato per rimuovere la crittografia dal documento PDF. La password utilizzata per aprire un documento PDF crittografato con password non può essere utilizzata per rimuovere la crittografia. Quando il documento PDF viene crittografato con una password, viene specificata una password master. (Vedi [Crittografia dei documenti di PDF con una password](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password).)

**Salva il documento PDF**

Dopo che il servizio Crittografia rimuove la crittografia basata su password da un documento PDF, è possibile salvare il documento PDF come file PDF. Gli utenti possono aprire il documento PDF in Adobe Reader o Acrobat senza specificare una password.

**Consulta anche**

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API servizio di crittografia](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[Crittografia di documenti PDF con una password](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Rimuovere la crittografia basata su password utilizzando l’API Java {#remove-password-based-encryption-using-the-java-api}

Rimuovi la crittografia basata su password da un documento PDF utilizzando l’API di crittografia (Java):

1. Includi file di progetto.

   Includi i file JAR dei client, come adobe-encryption-client.jar, nel percorso di classe del progetto Java.

1. Creare un client del servizio di crittografia.

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `EncryptionServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Ottieni il documento PDF crittografato.

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento PDF crittografato utilizzando il relativo costruttore e passando un valore stringa che specifica la posizione del documento PDF.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Rimuovi la password.

   Rimuovere la crittografia basata su password dal documento PDF richiamando il metodo `removePDFPasswordSecurity` dell&#39;oggetto `EncryptionServiceClient` e passando i valori seguenti:

   * Oggetto `com.adobe.idp.Document` contenente il documento PDF crittografato.
   * Valore string che specifica il valore della password master utilizzato per rimuovere la crittografia dal documento PDF.

   Il metodo `removePDFPasswordSecurity` restituisce un oggetto `com.adobe.idp.Document` contenente un documento PDF non protetto.

1. Salvare il documento PDF.

   * Creare un oggetto `java.io.File` e verificare che l&#39;estensione del nome file sia pdf.
   * Richiama il metodo `copyToFile` dell&#39;oggetto `com.adobe.idp.Document` per copiare il contenuto dell&#39;oggetto `Document` nel file. Assicurarsi di utilizzare l&#39;oggetto `Document` restituito dal metodo `removePDFPasswordSecurity`.

**Consulta anche**

[Quick Start (modalità SOAP): rimozione della crittografia basata su password tramite API Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-removing-password-based-encryption-using-the-java-api)

### Rimuovi la crittografia basata su password tramite l’API del servizio web {#remove-password-based-encryption-using-the-web-service-api}

Rimuovi la crittografia basata su password utilizzando l’API di crittografia (servizio web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Creare un client del servizio di crittografia.

   * Creare un oggetto `EncryptionServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `EncryptionServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/EncryptionService?WSDL`). Non è necessario utilizzare l&#39;attributo `lc_version`. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `EncryptionServiceClient.Endpoint.Binding`. Eseguire il cast del valore restituito in `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegnare il nome utente dei moduli AEM al campo `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Ottieni il documento PDF crittografato.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare un documento PDF crittografato con password.
   * Creare un oggetto `System.IO.FileStream` richiamandone il costruttore e passando un valore stringa che rappresenta la posizione del file del documento PDF crittografato e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni della matrice di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare la matrice di byte con i dati di flusso richiamando il metodo `Read` dell&#39;oggetto `System.IO.FileStream` e passando la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando il contenuto della matrice di byte al membro dati `MTOM` dell&#39;oggetto `BLOB`.

1. Rimuovi la password.

   Richiama il metodo `removePDFPasswordSecurity` dell&#39;oggetto `EncryptionServiceService` e passa i seguenti valori:

   * L&#39;oggetto `BLOB` che contiene i dati del flusso di file che rappresenta un documento PDF crittografato.
   * Valore stringa che specifica il valore della password utilizzato per rimuovere la crittografia dal documento PDF. Questo valore viene specificato quando si crittografa il documento PDF con una password.

   Il metodo `removePDFPasswordSecurity` restituisce un oggetto `BLOB` contenente un documento PDF non protetto.

1. Salvare il documento PDF.

   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore stringa che rappresenta la posizione del file del documento PDF non protetto.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `BLOB` restituito dal metodo `removePDFPasswordSecurity`. Popolare la matrice di byte ottenendo il valore del membro dati `MTOM` dell&#39;oggetto `BLOB`.
   * Creare un oggetto `System.IO.BinaryWriter` richiamandone il costruttore e passando l&#39;oggetto `System.IO.FileStream`.
   * Scrivere il contenuto della matrice di byte in un file PDF richiamando il metodo `Write` dell&#39;oggetto `System.IO.BinaryWriter` e passando la matrice di byte.

**Consulta anche**

[Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamare AEM Forms con SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Sblocco di documenti PDF crittografati {#unlocking-encrypted-pdf-documents}

Un documento PDF crittografato con password o con certificato deve essere sbloccato prima di poter essere sottoposto a un’altra operazione AEM Forms. Se si tenta di eseguire un&#39;operazione su un documento di PDF crittografato, verrà generata un&#39;eccezione. Dopo aver sbloccato un documento PDF crittografato, è possibile eseguirvi una o più operazioni. Queste operazioni possono appartenere ad altri servizi, come il servizio Acrobat Reader DC extensions.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio di crittografia, vedere [Riferimento ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-4}

Per sbloccare un documento PDF crittografato, effettuare le seguenti operazioni:

1. Includi file di progetto.
1. Creare un client del servizio di crittografia.
1. Ottieni il documento PDF crittografato.
1. Sblocca il documento.
1. Eseguire un’operazione AEM Forms.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso della classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è distribuito sul server applicazioni JBoss)
* jbossall-client.jar (richiesto se AEM Forms è distribuito sul server applicazioni JBoss)

**Creare un client del servizio di crittografia**

Per eseguire un&#39;operazione del servizio di crittografia a livello di programmazione, è necessario creare un client del servizio di crittografia. Se si utilizza l&#39;API del servizio di crittografia Java, creare un oggetto `EncrytionServiceClient`. Se si utilizza l&#39;API Servizio di crittografia del servizio Web, creare un oggetto `EncryptionServiceService`.

**Ottieni il documento crittografato di PDF**

Ottieni un documento PDF crittografato per sbloccarlo. Se si tenta di sbloccare un documento PDF non crittografato, viene generata un&#39;eccezione.

**Sblocca il documento**

Per sbloccare un documento PDF crittografato con password, è necessario disporre di un documento PDF crittografato e di un valore di password utilizzato per aprire un documento PDF crittografato con password. Questo valore viene specificato quando si crittografa il documento PDF con una password. (Vedi [Crittografia dei documenti di PDF con una password](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password).)

Per sbloccare un documento PDF crittografato con certificato, è necessario sia un documento PDF crittografato che il valore alias della chiave pubblica corrispondente alla chiave privata utilizzata per crittografare il documento PDF.

**Esegui un&#39;operazione AEM Forms**

Dopo lo sblocco di un documento PDF crittografato, è possibile eseguire un&#39;altra operazione di servizio su di esso, ad esempio l&#39;applicazione dei diritti di utilizzo. Questa operazione appartiene al servizio Acrobat Reader DC Extensions.

**Consulta anche**

[Sbloccare un documento PDF crittografato utilizzando l’API Java](encrypting-decrypting-pdf-documents.md#unlock-an-encrypted-pdf-document-using-the-java-api)

[Sblocca un documento PDF crittografato utilizzando l’API del servizio web](encrypting-decrypting-pdf-documents.md#unlock-an-encrypted-pdf-document-using-the-web-service-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API servizio di crittografia](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

### Sbloccare un documento PDF crittografato utilizzando l’API Java {#unlock-an-encrypted-pdf-document-using-the-java-api}

Sblocca un documento PDF crittografato utilizzando l’API di crittografia (Java):

1. Includi file di progetto.

   Includi i file JAR dei client, ad esempio adobe-encryption-client.jar, nel percorso di classe del progetto Java.

1. Creare un client del servizio di crittografia.

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `EncryptionServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Ottieni il documento PDF crittografato.

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento PDF crittografato utilizzando il relativo costruttore e passando un valore stringa che specifica la posizione del documento PDF crittografato.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Sblocca il documento.

   Sbloccare un documento PDF crittografato richiamando il metodo `unlockPDFUsingPassword` o `unlockPDFUsingCredential` dell&#39;oggetto `EncryptionServiceClient`.

   Per sbloccare un documento PDF crittografato con una password, richiamare il metodo `unlockPDFUsingPassword` e passare i valori seguenti:

   * Oggetto `com.adobe.idp.Document` contenente il documento PDF crittografato con password.
   * Valore string che specifica il valore della password utilizzato per aprire un documento PDF crittografato con password. Questo valore viene specificato quando si crittografa il documento PDF con una password.

   Per sbloccare un documento PDF crittografato con un certificato, richiamare il metodo `unlockPDFUsingCredential` e passare i valori seguenti:

   * Oggetto `com.adobe.idp.Document` contenente il documento PDF crittografato con certificato.
   * Valore string che specifica il nome alias della chiave pubblica corrispondente alla chiave privata utilizzata per crittografare il documento PDF.

   I metodi `unlockPDFUsingPassword` e `unlockPDFUsingCredential` restituiscono entrambi un oggetto `com.adobe.idp.Document` passato a un altro metodo Java AEM Forms per eseguire un&#39;operazione.

1. Eseguire un’operazione AEM Forms.

   Esegui un’operazione AEM Forms sul documento PDF sbloccato per soddisfare i requisiti aziendali. Se ad esempio si desidera applicare i diritti di utilizzo a un documento PDF sbloccato, passare l&#39;oggetto `com.adobe.idp.Document` restituito dai metodi `unlockPDFUsingPassword` o `unlockPDFUsingCredential` al metodo `applyUsageRights` dell&#39;oggetto `ReaderExtensionsServiceClient`.

**Consulta anche**

[Riepilogo dei passaggi](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Guida rapida (modalità SOAP): sblocco di un documento PDF crittografato tramite l&#39;API Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-unlocking-an-encrypted-pdf-document-using-the-java-api) (modalità SOAP)

[Applicazione dei diritti di utilizzo ai documenti di PDF](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Sblocca un documento PDF crittografato utilizzando l’API del servizio web {#unlock-an-encrypted-pdf-document-using-the-web-service-api}

Sblocca un documento PDF crittografato utilizzando l’API di crittografia (servizio web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Creare un client del servizio di crittografia.

   * Creare un oggetto `EncryptionServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `EncryptionServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/EncryptionService?WSDL`). Non è necessario utilizzare l&#39;attributo `lc_version`. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `EncryptionServiceClient.Endpoint.Binding`. Eseguire il cast del valore restituito in `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegnare il nome utente dei moduli AEM al campo `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Ottieni un documento PDF crittografato.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore.
   * Creare un oggetto `System.IO.FileStream` richiamandone il costruttore e passando un valore stringa che rappresenta la posizione del file del documento PDF crittografato e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni della matrice di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare la matrice di byte con i dati di flusso richiamando il metodo `Read` dell&#39;oggetto `System.IO.FileStream` e passando la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando il contenuto della matrice di byte al membro dati `MTOM` dell&#39;oggetto `BLOB`.

1. Sblocca il documento.

   Sbloccare un documento PDF crittografato richiamando il metodo `unlockPDFUsingPassword` o `unlockPDFUsingCredential` dell&#39;oggetto `EncryptionServiceClient`.

   Per sbloccare un documento PDF crittografato con una password, richiamare il metodo `unlockPDFUsingPassword` e passare i valori seguenti:

   * Oggetto `BLOB` contenente il documento PDF crittografato con password.
   * Valore string che specifica il valore della password utilizzato per aprire un documento PDF crittografato con password. Questo valore viene specificato quando si crittografa il documento PDF con una password.

   Per sbloccare un documento PDF crittografato con un certificato, richiamare il metodo `unlockPDFUsingCredential` e passare i valori seguenti:

   * Oggetto `BLOB` contenente il documento PDF crittografato con certificato.
   * Valore string che specifica il nome alias della chiave pubblica corrispondente alla chiave privata utilizzata per crittografare il documento PDf.

   I metodi `unlockPDFUsingPassword` e `unlockPDFUsingCredential` restituiscono entrambi un oggetto `com.adobe.idp.Document` passato a un altro metodo AEM Forms per eseguire un&#39;operazione.

1. Eseguire un’operazione AEM Forms.

   Esegui un’operazione AEM Forms sul documento PDF sbloccato per soddisfare i requisiti aziendali. Se ad esempio si desidera applicare i diritti di utilizzo al documento PDF sbloccato, passare l&#39;oggetto `BLOB` restituito dai metodi `unlockPDFUsingPassword` o `unlockPDFUsingCredential` al metodo `applyUsageRights` dell&#39;oggetto `ReaderExtensionsServiceClient`.

**Consulta anche**

[Riepilogo dei passaggi](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamare AEM Forms con SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Determinazione del tipo di crittografia {#determining-encryption-type}

È possibile determinare a livello di programmazione il tipo di crittografia che protegge un documento PDF utilizzando l&#39;API Servizio di crittografia Java o l&#39;API Servizio di crittografia del servizio Web. A volte è necessario determinare dinamicamente se un documento PDF è crittografato e, in tal caso, il tipo di crittografia. Ad esempio, è possibile determinare se un documento PDF è protetto con una crittografia basata su password o con una policy di Rights Management.

Un documento PDF può essere protetto dai seguenti tipi di crittografia:

* Crittografia basata su password
* Crittografia basata su certificati
* Criterio creato dal servizio di Rights Management
* Un altro tipo di crittografia

>[!NOTE]
>
>Per ulteriori informazioni sul servizio di crittografia, vedere [Riferimento ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-5}

Per determinare il tipo di crittografia che protegge un documento PDF, effettuare le seguenti operazioni:

1. Includi file di progetto.
1. Creare un client del servizio di crittografia.
1. Ottieni il documento PDF crittografato.
1. Determinare il tipo di crittografia.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso della classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è distribuito sul server applicazioni JBoss)
* jbossall-client.jar (richiesto se AEM Forms è distribuito sul server applicazioni JBoss)

**Crea un client di servizio**

Per eseguire un&#39;operazione del servizio di crittografia a livello di programmazione, è necessario creare un client del servizio di crittografia. Se si utilizza l&#39;API del servizio di crittografia Java, creare un oggetto `EncrytionServiceClient`. Se si utilizza l&#39;API Servizio di crittografia del servizio Web, creare un oggetto `EncryptionServiceService`.

**Ottieni il documento crittografato di PDF**

Ottieni un documento PDF per determinare il tipo di crittografia che lo protegge.

**Determinare il tipo di crittografia**

È possibile determinare il tipo di crittografia che protegge un documento PDF. Se il documento PDF non è protetto, il servizio di crittografia informa che il documento PDF non è protetto.

**Consulta anche**

[Determinare il tipo di crittografia utilizzando l’API Java](encrypting-decrypting-pdf-documents.md#determine-the-encryption-type-using-the-java-api)

[Determinare il tipo di crittografia utilizzando l’API del servizio web](encrypting-decrypting-pdf-documents.md#determine-the-encryption-type-using-the-web-service-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API servizio di crittografia](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[Protezione di documenti con criteri](/help/forms/developing/protecting-documents-policies.md#protecting-documents-with-policies)

### Determinare il tipo di crittografia utilizzando l’API Java {#determine-the-encryption-type-using-the-java-api}

Determina il tipo di crittografia che protegge un documento PDF utilizzando l’API di crittografia (Java):

1. Includi file di progetto.

   Includi i file JAR dei client, ad esempio adobe-encryption-client.jar, nel percorso di classe del progetto Java.

1. Crea un client di servizio.

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `EncryptionServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Ottieni il documento PDF crittografato.

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento PDF utilizzando il relativo costruttore e passando un valore stringa che specifica la posizione del documento PDF.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Determinare il tipo di crittografia.

   * Determinare il tipo di crittografia richiamando il metodo `getPDFEncryption` dell&#39;oggetto `EncryptionServiceClient` e passando l&#39;oggetto `com.adobe.idp.Document` che contiene il documento PDF. Questo metodo restituisce un oggetto `EncryptionTypeResult`.
   * Richiama il metodo `getEncryptionType` dell&#39;oggetto `EncryptionTypeResult`. Questo metodo restituisce un valore enum `EncryptionType` che specifica il tipo di crittografia. Se ad esempio il documento PDF è protetto con la crittografia basata su password, questo metodo restituisce `EncryptionType.PASSWORD`.

**Consulta anche**

[Riepilogo dei passaggi](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Quick Start (modalità SOAP): determinazione del tipo di crittografia tramite l’API Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-determining-encryption-type-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Determinare il tipo di crittografia utilizzando l’API del servizio web {#determine-the-encryption-type-using-the-web-service-api}

Determina il tipo di crittografia che protegge un documento PDF utilizzando l’API di crittografia (servizio web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Crea un client di servizio.

   * Creare un oggetto `EncryptionServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `EncryptionServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/EncryptionService?WSDL`). Non è necessario utilizzare l&#39;attributo `lc_version`. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `EncryptionServiceClient.Endpoint.Binding`. Eseguire il cast del valore restituito in `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegnare il nome utente dei moduli AEM al campo `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Ottieni il documento PDF crittografato.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore.
   * Creare un oggetto `System.IO.FileStream` richiamandone il costruttore e passando un valore stringa che rappresenta la posizione del file del documento PDF crittografato e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni della matrice di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare la matrice di byte con i dati di flusso richiamando il metodo `Read` dell&#39;oggetto `System.IO.FileStream` e passando la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando il contenuto della matrice di byte al membro dati `MTOM` dell&#39;oggetto `BLOB`.

1. Determinare il tipo di crittografia.

   * Richiama il metodo `getPDFEncryption` dell&#39;oggetto `EncryptionServiceClient` e passa l&#39;oggetto `BLOB` che contiene il documento PDF. Questo metodo restituisce un oggetto `EncryptionTypeResult`.
   * Ottiene il valore del metodo dati `encryptionType` dell&#39;oggetto `EncryptionTypeResult`. Se ad esempio il documento PDF è protetto con crittografia basata su password, il valore di questo membro dati è `EncryptionType.PASSWORD`.

**Consulta anche**

[Riepilogo dei passaggi](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamare AEM Forms con SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
