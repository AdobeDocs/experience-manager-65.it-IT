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
source-git-commit: 29cc7281e34487881ff9334f4cf00f3d013de11b
workflow-type: tm+mt
source-wordcount: '8133'
ht-degree: 0%

---

# Crittografia e decrittografia dei documenti di PDF {#encrypting-and-decrypting-pdf-documents}

**Gli esempi e gli esempi contenuti in questo documento sono solo per l’ambiente AEM Forms su JEE.**

**Informazioni sul servizio Encryption**

Il servizio Crittografia consente di crittografare e decrittografare i documenti. Quando un documento viene crittografato, il suo contenuto diventa illeggibile. Un utente autorizzato può decrittografare il documento per ottenere l’accesso al contenuto. Se un documento PDF è crittografato con una password, l’utente deve specificare la password di apertura prima che il documento possa essere visualizzato in Adobe Reader o Adobe Acrobat. Analogamente, se un documento PDF è crittografato con un certificato, l’utente deve decrittografare il documento PDF con la chiave pubblica corrispondente al certificato (chiave privata) utilizzato per crittografare il documento PDF.

È possibile eseguire queste operazioni utilizzando il servizio Crittografia:

* Crittografa un documento PDF con una password. (vedere [Crittografia di documenti PDF con una password](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password).)
* Crittografa un documento PDF con un certificato. (vedere [Crittografia di documenti PDF con certificati](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates).)
* Rimuovere la crittografia basata su password da un documento PDF. (vedere [Rimozione di Crittografia password](encrypting-decrypting-pdf-documents.md#removing-password-encryption).)
* Rimuovere la crittografia basata su certificato da un documento PDF. (vedere [Rimozione della crittografia basata su certificati](encrypting-decrypting-pdf-documents.md#removing-certificate-based-encryption).)
* Sblocca il documento PDF in modo da poter eseguire altre operazioni di servizio. Dopo lo sblocco di un documento PDF crittografato con password, ad esempio, è possibile applicare una firma digitale. (vedere [Sblocco di documenti PDF crittografati](encrypting-decrypting-pdf-documents.md#unlocking-encrypted-pdf-documents).)
* Determinare il tipo di crittografia di un documento PDF protetto. (vedere [Determinazione del tipo di crittografia](encrypting-decrypting-pdf-documents.md#determining-encryption-type).)

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Encryption, vedere [Guida di riferimento dei servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Crittografia di documenti PDF con una password {#encrypting-pdf-documents-with-a-password}

Quando crittografi un documento PDF con una password, un utente deve specificare la password per aprire il documento PDF in Adobe Reader o Acrobat. Inoltre, prima di poter eseguire sul documento un’altra operazione di AEM Forms, ad esempio la firma digitale del documento di PDF, è necessario sbloccare un documento di PDF crittografato con password.

>[!NOTE]
>
>Se carichi un documento PDF crittografato nell’archivio AEM Forms, non può decrittografare il documento PDF ed estrarre il contenuto XDP. È consigliabile non crittografare un documento prima di caricarlo nell’archivio AEM Forms. (vedere [Scrittura delle risorse](/help/forms/developing/aem-forms-repository.md#writing-resources).)

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Encryption, vedere [Guida di riferimento dei servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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

   * Creare un `ServiceClientFactory` oggetto che contiene proprietà di connessione.
   * Creare un `EncryptionServiceClient` mediante il costruttore e passando il `ServiceClientFactory` oggetto.

1. Ottieni un documento PDF da crittografare.

   * Creare un `java.io.FileInputStream` oggetto che rappresenta il documento PDF da crittografare utilizzando il relativo costruttore e passando un valore stringa che specifica la posizione del documento PDF.
   * Creare un `com.adobe.idp.Document` mediante il costruttore e passando il `java.io.FileInputStream` oggetto.

1. Impostare le opzioni di runtime della crittografia.

   * Creare un `PasswordEncryptionOptionSpec` richiamando il relativo costruttore.
   * Specificare le risorse del documento PDF da crittografare richiamando `PasswordEncryptionOptionSpec` dell&#39;oggetto `setEncryptOption` e il passaggio di un `PasswordEncryptionOption` valore di enumerazione che specifica le risorse del documento da crittografare. Ad esempio, per crittografare l&#39;intero documento PDF, inclusi i metadati e gli allegati, specificare `PasswordEncryptionOption.ALL`.
   * Creare un `java.util.List` oggetto che memorizza le autorizzazioni di crittografia utilizzando `ArrayList` costruttore.
   * Specificare un&#39;autorizzazione richiamando `java.util.List` oggetto &quot;s `add` e passando un valore di enumerazione che corrisponde all&#39;autorizzazione da impostare. Ad esempio, per impostare l’autorizzazione che consente a un utente di copiare i dati nel documento PDF, specifica `PasswordEncryptionPermission.PASSWORD_EDIT_COPY`. (Ripeti questo passaggio per ogni autorizzazione da impostare).
   * Specifica l’opzione di compatibilità per Acrobat richiamando `PasswordEncryptionOptionSpec` dell&#39;oggetto `setCompatability` e passando un valore di enumerazione che specifica il livello di compatibilità di Acrobat. Ad esempio, puoi specificare `PasswordEncryptionCompatability.ACRO_7`.
   * Specificare il valore della password che consente a un utente di aprire il documento PDF crittografato richiamando `PasswordEncryptionOptionSpec` dell&#39;oggetto `setDocumentOpenPassword` e passando un valore stringa che rappresenta la password di apertura.
   * Specificare il valore della password master che consente a un utente di rimuovere la crittografia dal documento PDF richiamando `PasswordEncryptionOptionSpec` dell&#39;oggetto `setPermissionPassword` e passando un valore stringa che rappresenta la password principale.

1. Aggiungi la password.

   Crittografare il documento PDF richiamando `EncryptionServiceClient` dell&#39;oggetto `encryptPDFUsingPassword` e fornendo i seguenti valori:

   * Il `com.adobe.idp.Document` oggetto che contiene il documento PDF da crittografare con la password.
   * Il `PasswordEncryptionOptionSpec` oggetto contenente opzioni di crittografia in fase di esecuzione.

   Il `encryptPDFUsingPassword` il metodo restituisce un `com.adobe.idp.Document` oggetto contenente un documento PDF crittografato con password.

1. Salvare il documento PDF crittografato come file PDF.

   * Creare un `java.io.File` e assicurarsi che l&#39;estensione del file sia .pdf.
   * Richiama `com.adobe.idp.Document` dell&#39;oggetto `copyToFile` metodo per copiare il contenuto del `com.adobe.idp.Document` al file. Assicurati di utilizzare `com.adobe.idp.Document` oggetto restituito da `encryptPDFUsingPassword` metodo.

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
   >Sostituisci `localhost` con l’indirizzo IP del server che ospita AEM Forms.

1. Creare un oggetto API client di crittografia.

   * Creare un `EncryptionServiceClient` utilizzando il costruttore predefinito.
   * Creare un `EncryptionServiceClient.Endpoint.Address` oggetto utilizzando `System.ServiceModel.EndpointAddress` costruttore. Passa un valore stringa che specifica il file WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/EncryptionService?WSDL`.) Non è necessario utilizzare il `lc_version` attributo. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Creare un `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto ottenendo il valore del `EncryptionServiceClient.Endpoint.Binding` campo. Invia il valore restituito a `BasicHttpBinding`.
   * Imposta il `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegna al campo il nome utente dei moduli AEM `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore password corrispondente al campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Ottieni un documento PDF da crittografare.

   * Creare un `BLOB` mediante il costruttore. Il `BLOB` L&#39;oggetto viene utilizzato per memorizzare un documento PDF crittografato con una password.
   * Creare un `System.IO.FileStream` richiamando il costruttore e passando un valore stringa che rappresenta la posizione del file del documento PDF da crittografare e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto della `System.IO.FileStream` oggetto. È possibile determinare le dimensioni della matrice di byte ottenendo `System.IO.FileStream` dell&#39;oggetto `Length` proprietà.
   * Compilare la matrice di byte con i dati di flusso richiamando `System.IO.FileStream` dell&#39;oggetto `Read` e passando la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare il `BLOB` mediante l&#39;assegnazione del contenuto della matrice di byte `BLOB` dell&#39;oggetto `MTOM` membro dati.

1. Impostare le opzioni di runtime della crittografia.

   * Creare un `PasswordEncryptionOptionSpec` mediante il costruttore.
   * Specificare le risorse del documento PDF da crittografare assegnando un `PasswordEncryptionOption` valore di enumerazione per `PasswordEncryptionOptionSpec` dell&#39;oggetto `encryptOption` membro dati. Per crittografare l&#39;intero PDF, inclusi i metadati e gli allegati, assegnare `PasswordEncryptionOption.ALL` a questo membro dati.
   * Specifica l’opzione di compatibilità per Acrobat assegnando un `PasswordEncryptionCompatability` valore di enumerazione per `PasswordEncryptionOptionSpec` dell&#39;oggetto `compatability` membro dati. Ad esempio, assegna `PasswordEncryptionCompatability.ACRO_7` a questo membro dati.
   * Specifica il valore della password che consente a un utente di aprire il documento PDF crittografato assegnando un valore stringa che rappresenta la password di apertura al `PasswordEncryptionOptionSpec` dell&#39;oggetto `documentOpenPassword` membro dati.
   * Specificare il valore della password che consente a un utente di rimuovere la crittografia dal documento PDF assegnando un valore stringa che rappresenta la password master al `PasswordEncryptionOptionSpec` dell&#39;oggetto `permissionPassword` membro dati.

1. Aggiungi la password.

   Crittografare il documento PDF richiamando `EncryptionServiceClient` dell&#39;oggetto `encryptPDFUsingPassword` e fornendo i seguenti valori:

   * Il `BLOB` oggetto che contiene il documento PDF da crittografare con la password.
   * Il `PasswordEncryptionOptionSpec` oggetto contenente opzioni di crittografia in fase di esecuzione.

   Il `encryptPDFUsingPassword` il metodo restituisce un `BLOB` oggetto contenente un documento PDF crittografato con password.

1. Salvare il documento PDF crittografato come file PDF.

   * Creare un `System.IO.FileStream` richiamando il relativo costruttore e passando un valore stringa che rappresenta la posizione del file del documento PDF protetto.
   * Creare una matrice di byte che memorizza il contenuto dei dati `BLOB` oggetto restituito da `encryptPDFUsingPassword` metodo. Popolare la matrice di byte ottenendo il valore della `BLOB` dell&#39;oggetto `MTOM` membro dati.
   * Creare un `System.IO.BinaryWriter` oggetto richiamando il relativo costruttore e passando il `System.IO.FileStream` oggetto.
   * Scrivere il contenuto della matrice di byte in un file PDF richiamando `System.IO.BinaryWriter` dell&#39;oggetto `Write` e passando la matrice di byte.

**Consulta anche**

[Riepilogo dei passaggi](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamare AEM Forms con SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Crittografia di documenti PDF con certificati {#encrypting-pdf-documents-with-certificates}

La crittografia basata su certificato consente di crittografare un documento per destinatari specifici tramite la tecnologia a chiave pubblica. È possibile assegnare a diversi destinatari autorizzazioni diverse per il documento. Molti aspetti della crittografia sono resi possibili dalla tecnologia a chiave pubblica. Un algoritmo viene utilizzato per generare due numeri grandi, noti come *tasti*, che hanno le seguenti proprietà:

* Una chiave viene utilizzata per crittografare un set di dati. Successivamente, solo l&#39;altra chiave può essere utilizzata per decrittografare i dati.
* È impossibile distinguere una chiave dall&#39;altra.

Una delle chiavi funge da chiave privata dell’utente. È importante che solo l’utente abbia accesso a questa chiave. L’altra chiave è la chiave pubblica dell’utente, che può essere condivisa con altri utenti.

Un certificato a chiave pubblica contiene la chiave pubblica e le informazioni di identificazione di un utente. Il formato X.509 viene utilizzato per l’archiviazione dei certificati. I certificati vengono generalmente rilasciati e firmati digitalmente da un&#39;autorità di certificazione (CA), un&#39;entità riconosciuta che fornisce una misura di affidabilità nella validità del certificato. I certificati hanno una data di scadenza dopo la quale non sono più validi. Inoltre, gli elenchi di revoche di certificati (CRL) forniscono informazioni sui certificati revocati prima della data di scadenza. I CRL vengono pubblicati periodicamente dalle autorità di certificazione. Lo stato di revoca di un certificato può essere recuperato anche tramite il protocollo OCSP (Online Certificate Status Protocol) in rete.

>[!NOTE]
>
>Se carichi un documento PDF crittografato nell’archivio AEM Forms, non può decrittografare il documento PDF ed estrarre il contenuto XDP. È consigliabile non crittografare un documento prima di caricarlo nell’archivio AEM Forms. (vedere [Scrittura delle risorse](/help/forms/developing/aem-forms-repository.md#writing-resources).)

>[!NOTE]
>
>Prima di poter crittografare un documento PDF con un certificato, è necessario assicurarsi di aggiungere il certificato ad AEM Forms. Un certificato viene aggiunto utilizzando la console di amministrazione o a livello di programmazione utilizzando l’API di Trust Manager. (vedere [Importazione delle credenziali tramite l&#39;API di Gestione trust](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api).)

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Encryption, vedere [Guida di riferimento dei servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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

Per eseguire un&#39;operazione del servizio di crittografia a livello di programmazione, è necessario creare un client del servizio di crittografia. Se utilizzi l’API Java Encryption Service, crea un’ `EncrytionServiceClient` oggetto. Se utilizzi l’API del servizio Web Encryption Service, crea un’ `EncryptionServiceService` oggetto.

**Ottieni un documento PDF da crittografare**

Ottieni un documento PDF non crittografato da crittografare. Se si tenta di proteggere un documento PDF già crittografato, viene generata un&#39;eccezione.

**Fai riferimento al certificato**

Per crittografare un documento PDF con un certificato, fare riferimento a un certificato utilizzato per crittografare un documento PDF. Il certificato è un file cer, crt o pem. Un file PKCS#12 viene utilizzato per memorizzare le chiavi private con i certificati corrispondenti.

Quando si crittografa un documento PDF con un certificato, specificare le autorizzazioni associate al documento protetto. Specificando le autorizzazioni, è possibile controllare le azioni che un utente che apre un documento PDF crittografato con certificato può eseguire.

**Impostare le opzioni di runtime della crittografia**

Specificare le risorse del documento PDF da crittografare. È possibile crittografare l’intero documento PDF, tutto tranne i metadati del documento o solo gli allegati del documento.

**Creazione di un documento PDF crittografato con certificato**

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

   * Creare un `ServiceClientFactory` oggetto che contiene proprietà di connessione.
   * Creare un `EncryptionServiceClient` mediante il costruttore e passando il `ServiceClientFactory` oggetto.

1. Ottieni un documento PDF da crittografare.

   * Creare un `java.io.FileInputStream` oggetto che rappresenta il documento PDF da crittografare utilizzando il relativo costruttore e passando un valore stringa che specifica la posizione del documento PDF.
   * Creare un `com.adobe.idp.Document` mediante il costruttore e passando il `java.io.FileInputStream` oggetto.

1. Fai riferimento al certificato.

   * Creare un `java.util.List` oggetto che memorizza le informazioni sulle autorizzazioni utilizzando il relativo costruttore.
   * Specificare l&#39;autorizzazione associata al documento crittografato richiamando `java.util.List` dell&#39;oggetto `add` e il passaggio di un `CertificateEncryptionPermissions` valore di enumerazione che rappresenta le autorizzazioni concesse all&#39;utente che apre il documento PDF protetto. Ad esempio, per specificare tutte le autorizzazioni, passare `CertificateEncryptionPermissions.PKI_ALL_PERM`.
   * Creare un `Recipient` mediante il costruttore.
   * Creare un `java.io.FileInputStream` oggetto che rappresenta il certificato utilizzato per crittografare il documento PDF utilizzando il relativo costruttore e passando un valore stringa che specifica la posizione del certificato.
   * Creare un `com.adobe.idp.Document` mediante il costruttore e passando il `java.io.FileInputStream` oggetto che rappresenta il certificato.
   * Richiama `Recipient` dell&#39;oggetto `setX509Cert` e trasmettere il `com.adobe.idp.Document` oggetto che contiene il certificato. (Inoltre, il `Recipient`L&#39;oggetto può avere un alias del certificato Truststore o un URL LDAP come origine del certificato.)
   * Creare un `CertificateEncryptionIdentity` oggetto che memorizza le informazioni su autorizzazioni e certificati utilizzando il relativo costruttore.
   * Richiama `CertificateEncryptionIdentity` dell&#39;oggetto `setPerms` e trasmettere il `java.util.List` oggetto che memorizza le informazioni sulle autorizzazioni.
   * Richiama `CertificateEncryptionIdentity` dell&#39;oggetto `setRecipient` e trasmettere il `Recipient` oggetto che memorizza le informazioni sul certificato.
   * Creare un `java.util.List` oggetto che memorizza le informazioni sul certificato utilizzando il relativo costruttore.
   * Richiama `java.util.List` metodo add dell&#39;oggetto e passare il `CertificateEncryptionIdentity` oggetto. (Questo `java.util.List` l&#39;oggetto viene passato come parametro al `encryptPDFUsingCertificates` metodo.)

1. Impostare le opzioni di runtime della crittografia.

   * Creare un `CertificateEncryptionOptionSpec` richiamando il relativo costruttore.
   * Specificare le risorse del documento PDF da crittografare richiamando `CertificateEncryptionOptionSpec` dell&#39;oggetto `setOption` e il passaggio di un `CertificateEncryptionOption` valore di enumerazione che specifica le risorse del documento da crittografare. Ad esempio, per crittografare l&#39;intero documento PDF, inclusi i metadati e gli allegati, specificare `CertificateEncryptionOption.ALL`.
   * Specifica l’opzione di compatibilità per Acrobat richiamando `CertificateEncryptionOptionSpec` dell&#39;oggetto `setCompat` e il passaggio di un `CertificateEncryptionCompatibility` valore di enumerazione che specifica il livello di compatibilità di Acrobat. Ad esempio, puoi specificare `CertificateEncryptionCompatibility.ACRO_7`.

1. Crea un documento PDF crittografato con certificato.

   Crittografare il documento PDF con un certificato richiamando il `EncryptionServiceClient` dell&#39;oggetto `encryptPDFUsingCertificates` e fornendo i seguenti valori:

   * Il `com.adobe.idp.Document` oggetto che contiene il documento PDF da crittografare.
   * Il `java.util.List` oggetto che memorizza le informazioni sul certificato.
   * Il `CertificateEncryptionOptionSpec` oggetto contenente opzioni di crittografia in fase di esecuzione.

   Il `encryptPDFUsingCertificates` il metodo restituisce un `com.adobe.idp.Document` oggetto contenente un documento PDF crittografato con certificato.

1. Salvare il documento PDF crittografato come file PDF.

   * Creare un `java.io.File` e assicurarsi che l&#39;estensione del nome file sia .pdf.
   * Richiama `com.adobe.idp.Document` dell&#39;oggetto `copyToFile` metodo per copiare il contenuto del `com.adobe.idp.Document` al file. Assicurati di utilizzare `com.adobe.idp.Document` oggetto restituito da `encryptPDFUsingCertificates` metodo.

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
   >Sostituisci `localhost` con l’indirizzo IP del server che ospita AEM Forms.

1. Creare un oggetto API client di crittografia.

   * Creare un `EncryptionServiceClient` utilizzando il costruttore predefinito.
   * Creare un `EncryptionServiceClient.Endpoint.Address` oggetto utilizzando `System.ServiceModel.EndpointAddress` costruttore. Passa un valore stringa che specifica il file WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/EncryptionService?WSDL`.) Non è necessario utilizzare il `lc_version` attributo. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Creare un `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto ottenendo il valore del `EncryptionServiceClient.Endpoint.Binding` campo. Invia il valore restituito a `BasicHttpBinding`.
   * Imposta il `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegna al campo il nome utente dei moduli AEM `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore password corrispondente al campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Ottieni un documento PDF da crittografare.

   * Creare un `BLOB` mediante il costruttore. Il `BLOB` L&#39;oggetto viene utilizzato per memorizzare un documento PDF crittografato con un certificato.
   * Creare un `System.IO.FileStream` richiamando il costruttore e passando un valore stringa che rappresenta la posizione del file del documento PDF da crittografare e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto della `System.IO.FileStream` oggetto. È possibile determinare le dimensioni della matrice di byte ottenendo `System.IO.FileStream` dell&#39;oggetto `Length` proprietà.
   * Compilare la matrice di byte con i dati di flusso richiamando `System.IO.FileStream` dell&#39;oggetto `Read` e passando la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare il `BLOB` oggetto assegnando il relativo `MTOM` con il contenuto della matrice di byte.

1. Fai riferimento al certificato.

   * Creare un `Recipient` mediante il costruttore. Questo oggetto memorizzerà le informazioni sul certificato.
   * Creare un `BLOB` mediante il costruttore. Questo `BLOB` L&#39;oggetto memorizzerà il certificato che crittografa il documento PDF.
   * Creare un `System.IO.FileStream` richiamando il costruttore e passando un valore stringa che rappresenta la posizione del file del certificato e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto della `System.IO.FileStream` oggetto. È possibile determinare le dimensioni della matrice di byte ottenendo `System.IO.FileStream` dell&#39;oggetto `Length` proprietà.
   * Compilare la matrice di byte con i dati di flusso richiamando `System.IO.FileStream` dell&#39;oggetto `Read` e passando la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare il `BLOB` mediante l&#39;assegnazione del contenuto della matrice di byte `BLOB` dell&#39;oggetto `MTOM` membro dati.
   * Assegna la `BLOB` oggetto che memorizza il certificato in `Recipient` dell&#39;oggetto `x509Cert` membro dati.
   * Creare un `CertificateEncryptionIdentity` oggetto che memorizza le informazioni sul certificato utilizzando il relativo costruttore.
   * Assegna la `Recipient` oggetto che memorizza il certificato in `CertificateEncryptionIdentity`membro dati destinatario dell&#39;oggetto.
   * Creare un `Object` e assegna il `CertificateEncryptionIdentity` oggetto al primo elemento del `Object` array. Questo `Object` viene passato come parametro al `encryptPDFUsingCertificates` metodo.

1. Impostare le opzioni di runtime della crittografia.

   * Creare un `CertificateEncryptionOptionSpec` mediante il costruttore.
   * Specificare le risorse del documento PDF da crittografare assegnando un `CertificateEncryptionOption` valore di enumerazione per `CertificateEncryptionOptionSpec` dell&#39;oggetto `option` membro dati. Per crittografare l&#39;intero documento PDF, inclusi i metadati e gli allegati, assegnare `CertificateEncryptionOption.ALL` a questo membro dati.
   * Specifica l’opzione di compatibilità per Acrobat assegnando un `CertificateEncryptionCompatibility` valore di enumerazione per `CertificateEncryptionOptionSpec` dell&#39;oggetto `compat` membro dati. Ad esempio, assegna `CertificateEncryptionCompatibility.ACRO_7` a questo membro dati.

1. Crea un documento PDF crittografato con certificato.

   Crittografare il documento PDF con un certificato richiamando il `EncryptionServiceService` dell&#39;oggetto `encryptPDFUsingCertificates` e fornendo i seguenti valori:

   * Il `BLOB` oggetto che contiene il documento PDF da crittografare.
   * Il `Object` array che memorizza le informazioni sui certificati.
   * Il `CertificateEncryptionOptionSpec` oggetto contenente opzioni di crittografia in fase di esecuzione.

   Il `encryptPDFUsingCertificates` il metodo restituisce un `BLOB` oggetto contenente un documento PDF crittografato con certificato.

1. Salvare il documento PDF crittografato come file PDF.

   * Creare un `System.IO.FileStream` richiamando il relativo costruttore e passando un valore stringa che rappresenta la posizione del file del documento PDF protetto.
   * Creare una matrice di byte che memorizza il contenuto dei dati `BLOB` oggetto restituito da `encryptPDFUsingCertificates` metodo. Popolare la matrice di byte ottenendo il valore della `BLOB` dell&#39;oggetto `binaryData` membro dati.
   * Creare un `System.IO.BinaryWriter` oggetto richiamando il relativo costruttore e passando il `System.IO.FileStream` oggetto.
   * Scrivere il contenuto della matrice di byte in un file PDF richiamando `System.IO.BinaryWriter` dell&#39;oggetto `Write` e passando la matrice di byte.

**Consulta anche**

[Riepilogo dei passaggi](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamare AEM Forms con SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Rimozione della crittografia basata su certificati {#removing-certificate-based-encryption}

La crittografia basata su certificato può essere rimossa da un documento PDF PDF in modo che gli utenti possano aprirlo in Adobe Reader o Acrobat. Per rimuovere la crittografia da un documento PDF crittografato con un certificato, è necessario fare riferimento a una chiave pubblica. Una volta rimossa da un documento PDF, la crittografia non è più protetta.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Encryption, vedere [Guida di riferimento dei servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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

Per eseguire un&#39;operazione del servizio di crittografia a livello di programmazione, è necessario creare un client del servizio di crittografia. Se utilizzi l’API Java Encryption Service, crea un’ `EncrytionServiceClient` oggetto. Se utilizzi l’API del servizio Web Encryption Service, crea un’ `EncryptionServiceService` oggetto.

**Ottieni il documento PDF crittografato**

Ottieni un documento PDF crittografato per rimuovere la crittografia basata su certificati. Se si tenta di rimuovere la crittografia da un documento PDF non crittografato, viene generata un&#39;eccezione. Analogamente, se si tenta di rimuovere la crittografia basata su certificato da un documento crittografato con password, viene generata un&#39;eccezione.

**Rimuovi crittografia**

Per rimuovere la crittografia basata su certificato da un documento PDF crittografato, è necessario disporre di un documento PDF crittografato e della chiave privata corrispondente alla chiave utilizzata per crittografare il documento PDF. Il valore alias della chiave privata viene specificato quando si rimuove la crittografia basata su certificati da un documento di PDF crittografato. Per informazioni sulla chiave pubblica, vedi [Crittografia di documenti PDF con certificati](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates).

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

   * Creare un `ServiceClientFactory` oggetto che contiene proprietà di connessione.
   * Creare un `EncryptionServiceClient` mediante il costruttore e passando il `ServiceClientFactory` oggetto.

1. Ottieni il documento PDF crittografato.

   * Creare un `java.io.FileInputStream` oggetto che rappresenta il documento PDF crittografato utilizzando il relativo costruttore e passando un valore stringa che specifica la posizione del documento PDF crittografato.
   * Creare un `com.adobe.idp.Document` mediante il costruttore e passando il `java.io.FileInputStream` oggetto.

1. Rimuovi la crittografia.

   Rimuovere la crittografia basata su certificato dal documento PDF richiamando `EncryptionServiceClient` dell&#39;oggetto `removePDFCertificateSecurity` e fornendo i seguenti valori:

   * Il `com.adobe.idp.Document` oggetto che contiene il documento PDF crittografato.
   * Valore stringa che specifica il nome alias della chiave privata corrispondente alla chiave utilizzata per crittografare il documento PDf.

   Il `removePDFCertificateSecurity` il metodo restituisce un `com.adobe.idp.Document` oggetto contenente un documento PDF non protetto.

1. Salvare il documento PDF.

   * Creare un `java.io.File` e assicurarsi che l&#39;estensione del file sia .pdf.
   * Richiama `com.adobe.idp.Document` dell&#39;oggetto `copyToFile` metodo per copiare il contenuto del `Document` al file. Assicurati di utilizzare `com.adobe.idp.Document` oggetto restituito da `removePDFCredentialSecurity` metodo.

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
   >Sostituisci `localhost` con l’indirizzo IP del server che ospita AEM Forms.

1. Creare un client del servizio di crittografia.

   * Creare un `EncryptionServiceClient` utilizzando il costruttore predefinito.
   * Creare un `EncryptionServiceClient.Endpoint.Address` oggetto utilizzando `System.ServiceModel.EndpointAddress` costruttore. Passa un valore stringa che specifica il file WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/EncryptionService?WSDL`.) Non è necessario utilizzare il `lc_version` attributo. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Creare un `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto ottenendo il valore del `EncryptionServiceClient.Endpoint.Binding` campo. Invia il valore restituito a `BasicHttpBinding`.
   * Imposta il `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegna al campo il nome utente dei moduli AEM `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore password corrispondente al campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Ottieni il documento PDF crittografato.

   * Creare un `BLOB` mediante il costruttore. Il `BLOB` L&#39;oggetto viene utilizzato per memorizzare il documento PDF crittografato.
   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore stringa che rappresenta la posizione del file del documento PDF crittografato e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto della `System.IO.FileStream` oggetto. È possibile determinare le dimensioni della matrice di byte ottenendo `System.IO.FileStream` dell&#39;oggetto `Length` proprietà.
   * Compilare la matrice di byte con i dati di flusso richiamando `System.IO.FileStream` dell&#39;oggetto `Read` e passando la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare il `BLOB` mediante l&#39;assegnazione del contenuto della matrice di byte `BLOB` dell&#39;oggetto `MTOM` membro dati.

1. Rimuovi la crittografia.

   Richiama `EncryptionServiceClient` dell&#39;oggetto `removePDFCertificateSecurity` e trasmettere i seguenti valori:

   * Il `BLOB` oggetto contenente dati di flusso di file che rappresenta un documento PDF crittografato.
   * Valore string che specifica il nome alias della chiave pubblica corrispondente alla chiave privata utilizzata per crittografare il documento PDf.

   Il `removePDFCredentialSecurity` il metodo restituisce un `BLOB` oggetto contenente un documento PDF non protetto.

1. Salvare il documento PDF.

   * Creare un `System.IO.FileStream` richiamando il relativo costruttore e passando un valore stringa che rappresenta la posizione del file del documento di PDF non protetto.
   * Creare una matrice di byte che memorizza il contenuto della `BLOB` oggetto restituito da `removePDFPasswordSecurity` metodo. Popolare la matrice di byte ottenendo il valore della `BLOB` dell&#39;oggetto `MTOM` membro dati.
   * Creare un `System.IO.BinaryWriter` oggetto richiamando il relativo costruttore e passando il `System.IO.FileStream` oggetto.
   * Scrivere il contenuto della matrice di byte in un file PDF richiamando `System.IO.BinaryWriter` dell&#39;oggetto `Write` e passando la matrice di byte.

**Consulta anche**

[Riepilogo dei passaggi](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamare AEM Forms con SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Rimozione di Crittografia password {#removing-password-encryption}

La crittografia basata su password può essere rimossa da un documento PDF PDF in modo che gli utenti possano aprirlo in Adobe Reader o Acrobat senza dover specificare una password. Dopo la rimozione della crittografia basata su password da un documento PDF, il documento non è più protetto.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Encryption, vedere [Guida di riferimento dei servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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

Per eseguire un&#39;operazione del servizio di crittografia a livello di programmazione, è necessario creare un client del servizio di crittografia. Se utilizzi l’API Java Encryption Service, crea un’ `EncrytionServiceClient` oggetto. Se utilizzi l’API del servizio Web Encryption Service, crea un’ `EncryptionServiceService` oggetto.

**Ottieni il documento PDF crittografato**

Ottieni un documento PDF crittografato per rimuovere la crittografia basata su password. Se si tenta di rimuovere la crittografia da un documento PDF non crittografato, viene generata un&#39;eccezione.

**Rimuovi la password**

Per rimuovere la crittografia basata su password da un documento PDF crittografato, è necessario disporre di un documento PDF crittografato e di un valore di password master utilizzato per rimuovere la crittografia dal documento PDF. La password utilizzata per aprire un documento PDF crittografato con password non può essere utilizzata per rimuovere la crittografia. Quando il documento PDF viene crittografato con una password, viene specificata una password master. (vedere [Crittografia di documenti PDF con una password](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password).)

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

   * Creare un `ServiceClientFactory` oggetto che contiene proprietà di connessione.
   * Creare un `EncryptionServiceClient` mediante il costruttore e passando il `ServiceClientFactory` oggetto.

1. Ottieni il documento PDF crittografato.

   * Creare un `java.io.FileInputStream` oggetto che rappresenta il documento PDF crittografato utilizzando il relativo costruttore e passando un valore stringa che specifica la posizione del documento PDF.
   * Creare un `com.adobe.idp.Document` mediante il costruttore e passando il `java.io.FileInputStream` oggetto.

1. Rimuovi la password.

   Rimuovere la crittografia basata su password dal documento PDF richiamando `EncryptionServiceClient` dell&#39;oggetto `removePDFPasswordSecurity` e fornendo i seguenti valori:

   * A `com.adobe.idp.Document` oggetto che contiene il documento PDF crittografato.
   * Valore string che specifica il valore della password master utilizzato per rimuovere la crittografia dal documento PDF.

   Il `removePDFPasswordSecurity` il metodo restituisce un `com.adobe.idp.Document` oggetto contenente un documento PDF non protetto.

1. Salvare il documento PDF.

   * Creare un `java.io.File` e assicurarsi che l&#39;estensione del nome file sia .pdf.
   * Richiama `com.adobe.idp.Document` dell&#39;oggetto `copyToFile` metodo per copiare il contenuto del `Document` al file. Assicurati di utilizzare `Document` oggetto restituito da `removePDFPasswordSecurity` metodo.

**Consulta anche**

[Quick Start (modalità SOAP): rimozione della crittografia basata su password tramite API Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-removing-password-based-encryption-using-the-java-api)

### Rimuovi la crittografia basata su password tramite l’API del servizio web {#remove-password-based-encryption-using-the-web-service-api}

Rimuovi la crittografia basata su password utilizzando l’API di crittografia (servizio web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l’indirizzo IP del server che ospita AEM Forms.

1. Creare un client del servizio di crittografia.

   * Creare un `EncryptionServiceClient` utilizzando il costruttore predefinito.
   * Creare un `EncryptionServiceClient.Endpoint.Address` oggetto utilizzando `System.ServiceModel.EndpointAddress` costruttore. Passa un valore stringa che specifica il file WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/EncryptionService?WSDL`.) Non è necessario utilizzare il `lc_version` attributo. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Creare un `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto ottenendo il valore del `EncryptionServiceClient.Endpoint.Binding` campo. Invia il valore restituito a `BasicHttpBinding`.
   * Imposta il `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegna al campo il nome utente dei moduli AEM `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore password corrispondente al campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Ottieni il documento PDF crittografato.

   * Creare un `BLOB` mediante il costruttore. Il `BLOB` L&#39;oggetto viene utilizzato per memorizzare un documento PDF crittografato con password.
   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore stringa che rappresenta la posizione del file del documento PDF crittografato e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto della `System.IO.FileStream` oggetto. È possibile determinare le dimensioni della matrice di byte ottenendo `System.IO.FileStream` dell&#39;oggetto `Length` proprietà.
   * Compilare la matrice di byte con i dati di flusso richiamando `System.IO.FileStream` dell&#39;oggetto `Read` e passando la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare il `BLOB` mediante l&#39;assegnazione del contenuto della matrice di byte `BLOB` dell&#39;oggetto `MTOM` membro dati.

1. Rimuovi la password.

   Richiama `EncryptionServiceService` dell&#39;oggetto `removePDFPasswordSecurity` e trasmettere i seguenti valori:

   * Il `BLOB` oggetto contenente dati di flusso di file che rappresenta un documento PDF crittografato.
   * Valore stringa che specifica il valore della password utilizzato per rimuovere la crittografia dal documento PDF. Questo valore viene specificato quando si crittografa il documento PDF con una password.

   Il `removePDFPasswordSecurity` il metodo restituisce un `BLOB` oggetto contenente un documento PDF non protetto.

1. Salvare il documento PDF.

   * Creare un `System.IO.FileStream` richiamando il relativo costruttore e passando un valore stringa che rappresenta la posizione del file del documento di PDF non protetto.
   * Creare una matrice di byte che memorizza il contenuto della `BLOB` oggetto restituito da `removePDFPasswordSecurity` metodo. Popolare la matrice di byte ottenendo il valore della `BLOB` dell&#39;oggetto `MTOM` membro dati.
   * Creare un `System.IO.BinaryWriter` oggetto richiamando il relativo costruttore e passando il `System.IO.FileStream` oggetto.
   * Scrivere il contenuto della matrice di byte in un file PDF richiamando `System.IO.BinaryWriter` dell&#39;oggetto `Write` e passando la matrice di byte.

**Consulta anche**

[Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamare AEM Forms con SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Sblocco di documenti PDF crittografati {#unlocking-encrypted-pdf-documents}

Un documento PDF crittografato con password o con certificato deve essere sbloccato prima di poter essere sottoposto a un’altra operazione AEM Forms. Se si tenta di eseguire un&#39;operazione su un documento di PDF crittografato, verrà generata un&#39;eccezione. Dopo aver sbloccato un documento PDF crittografato, è possibile eseguirvi una o più operazioni. Queste operazioni possono appartenere ad altri servizi, come il servizio Acrobat Reader DC extensions.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Encryption, vedere [Guida di riferimento dei servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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

Per eseguire un&#39;operazione del servizio di crittografia a livello di programmazione, è necessario creare un client del servizio di crittografia. Se utilizzi l’API Java Encryption Service, crea un’ `EncrytionServiceClient` oggetto. Se utilizzi l’API del servizio Web Encryption Service, crea un’ `EncryptionServiceService` oggetto.

**Ottieni il documento PDF crittografato**

Ottieni un documento PDF crittografato per sbloccarlo. Se si tenta di sbloccare un documento PDF non crittografato, viene generata un&#39;eccezione.

**Sblocca il documento**

Per sbloccare un documento PDF crittografato con password, è necessario disporre di un documento PDF crittografato e di un valore di password utilizzato per aprire un documento PDF crittografato con password. Questo valore viene specificato quando si crittografa il documento PDF con una password. (vedere [Crittografia di documenti PDF con una password](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password).)

Per sbloccare un documento PDF crittografato con certificato, è necessario sia un documento PDF crittografato che il valore alias della chiave pubblica corrispondente alla chiave privata utilizzata per crittografare il documento PDF.

**Eseguire un’operazione AEM Forms**

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

   * Creare un `ServiceClientFactory` oggetto che contiene proprietà di connessione.
   * Creare un `EncryptionServiceClient` mediante il costruttore e passando il `ServiceClientFactory` oggetto.

1. Ottieni il documento PDF crittografato.

   * Creare un `java.io.FileInputStream` oggetto che rappresenta il documento PDF crittografato utilizzando il relativo costruttore e passando un valore stringa che specifica la posizione del documento PDF crittografato.
   * Creare un `com.adobe.idp.Document` mediante il costruttore e passando il `java.io.FileInputStream` oggetto.

1. Sblocca il documento.

   Sblocca un documento PDF crittografato richiamando `EncryptionServiceClient` dell&#39;oggetto `unlockPDFUsingPassword` o `unlockPDFUsingCredential` metodo.

   Per sbloccare un documento PDF crittografato con una password, richiamare `unlockPDFUsingPassword` e trasmettere i seguenti valori:

   * A `com.adobe.idp.Document` oggetto contenente il documento PDF crittografato con password.
   * Valore string che specifica il valore della password utilizzato per aprire un documento PDF crittografato con password. Questo valore viene specificato quando si crittografa il documento PDF con una password.

   Per sbloccare un documento PDF crittografato con un certificato, richiama `unlockPDFUsingCredential` e trasmettere i seguenti valori:

   * A `com.adobe.idp.Document` oggetto che contiene il documento PDF crittografato con certificato.
   * Valore string che specifica il nome alias della chiave pubblica corrispondente alla chiave privata utilizzata per crittografare il documento PDF.

   Il `unlockPDFUsingPassword` e `unlockPDFUsingCredential` entrambi i metodi restituiscono un `com.adobe.idp.Document` oggetto passato a un altro metodo Java AEM Forms per eseguire un&#39;operazione.

1. Eseguire un’operazione AEM Forms.

   Esegui un’operazione AEM Forms sul documento PDF sbloccato per soddisfare i requisiti aziendali. Se ad esempio si desidera applicare i diritti di utilizzo a un documento di PDF non bloccato, passare il `com.adobe.idp.Document` oggetto restituito da uno dei due `unlockPDFUsingPassword` o `unlockPDFUsingCredential` metodi per `ReaderExtensionsServiceClient` dell&#39;oggetto `applyUsageRights` metodo.

**Consulta anche**

[Riepilogo dei passaggi](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Guida rapida (modalità SOAP): sblocco di un documento PDF crittografato tramite l’API Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-unlocking-an-encrypted-pdf-document-using-the-java-api) (modalità SOAP)

[Applicazione dei diritti di utilizzo ai documenti di PDF](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Sblocca un documento PDF crittografato utilizzando l’API del servizio web {#unlock-an-encrypted-pdf-document-using-the-web-service-api}

Sblocca un documento PDF crittografato utilizzando l’API di crittografia (servizio web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l’indirizzo IP del server che ospita AEM Forms.

1. Creare un client del servizio di crittografia.

   * Creare un `EncryptionServiceClient` utilizzando il costruttore predefinito.
   * Creare un `EncryptionServiceClient.Endpoint.Address` oggetto utilizzando `System.ServiceModel.EndpointAddress` costruttore. Passa un valore stringa che specifica il file WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/EncryptionService?WSDL`.) Non è necessario utilizzare il `lc_version` attributo. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Creare un `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto ottenendo il valore del `EncryptionServiceClient.Endpoint.Binding` campo. Invia il valore restituito a `BasicHttpBinding`.
   * Imposta il `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegna al campo il nome utente dei moduli AEM `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore password corrispondente al campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Ottieni un documento PDF crittografato.

   * Creare un `BLOB` mediante il costruttore.
   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore stringa che rappresenta la posizione del file del documento PDF crittografato e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto della `System.IO.FileStream` oggetto. È possibile determinare le dimensioni della matrice di byte ottenendo `System.IO.FileStream` dell&#39;oggetto `Length` proprietà.
   * Compilare la matrice di byte con i dati di flusso richiamando `System.IO.FileStream` dell&#39;oggetto `Read` e passando la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare il `BLOB` mediante l&#39;assegnazione del contenuto della matrice di byte `BLOB` dell&#39;oggetto `MTOM` membro dati.

1. Sblocca il documento.

   Sblocca un documento PDF crittografato richiamando `EncryptionServiceClient` dell&#39;oggetto `unlockPDFUsingPassword` o `unlockPDFUsingCredential` metodo.

   Per sbloccare un documento PDF crittografato con una password, richiamare `unlockPDFUsingPassword` e trasmettere i seguenti valori:

   * A `BLOB` oggetto contenente il documento PDF crittografato con password.
   * Valore string che specifica il valore della password utilizzato per aprire un documento PDF crittografato con password. Questo valore viene specificato quando si crittografa il documento PDF con una password.

   Per sbloccare un documento PDF crittografato con un certificato, richiama `unlockPDFUsingCredential` e trasmettere i seguenti valori:

   * A `BLOB` oggetto che contiene il documento PDF crittografato con certificato.
   * Valore string che specifica il nome alias della chiave pubblica corrispondente alla chiave privata utilizzata per crittografare il documento PDf.

   Il `unlockPDFUsingPassword` e `unlockPDFUsingCredential` entrambi i metodi restituiscono un `com.adobe.idp.Document` oggetto passato a un altro metodo AEM Forms per eseguire un&#39;operazione.

1. Eseguire un’operazione AEM Forms.

   Esegui un’operazione AEM Forms sul documento PDF sbloccato per soddisfare i requisiti aziendali. Se ad esempio si desidera applicare i diritti di utilizzo al documento di PDF sbloccato, passare il `BLOB` oggetto restituito da uno dei due `unlockPDFUsingPassword` o `unlockPDFUsingCredential` metodi per `ReaderExtensionsServiceClient` dell&#39;oggetto `applyUsageRights` metodo.

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
>Per ulteriori informazioni sul servizio Encryption, vedere [Guida di riferimento dei servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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

**Creare un client di servizio**

Per eseguire un&#39;operazione del servizio di crittografia a livello di programmazione, è necessario creare un client del servizio di crittografia. Se utilizzi l’API Java Encryption Service, crea un’ `EncrytionServiceClient` oggetto. Se utilizzi l’API del servizio Web Encryption Service, crea un’ `EncryptionServiceService` oggetto.

**Ottieni il documento PDF crittografato**

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

   * Creare un `ServiceClientFactory` oggetto che contiene proprietà di connessione.
   * Creare un `EncryptionServiceClient` mediante il costruttore e passando il `ServiceClientFactory` oggetto.

1. Ottieni il documento PDF crittografato.

   * Creare un `java.io.FileInputStream` oggetto che rappresenta il documento PDF utilizzando il relativo costruttore e passando un valore stringa che specifica la posizione del documento PDF.
   * Creare un `com.adobe.idp.Document` mediante il costruttore e passando il `java.io.FileInputStream` oggetto.

1. Determinare il tipo di crittografia.

   * Determinare il tipo di crittografia richiamando `EncryptionServiceClient` dell&#39;oggetto `getPDFEncryption` e passando il `com.adobe.idp.Document` oggetto che contiene il documento PDF. Questo metodo restituisce un `EncryptionTypeResult` oggetto.
   * Richiama `EncryptionTypeResult` dell&#39;oggetto `getEncryptionType` metodo. Questo metodo restituisce un `EncryptionType` valore enum che specifica il tipo di crittografia. Se, ad esempio, il documento PDF è protetto con la crittografia basata su password, questo metodo restituirà `EncryptionType.PASSWORD`.

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
   >Sostituisci `localhost` con l’indirizzo IP del server che ospita AEM Forms.

1. Crea un client di servizio.

   * Creare un `EncryptionServiceClient` utilizzando il costruttore predefinito.
   * Creare un `EncryptionServiceClient.Endpoint.Address` oggetto utilizzando `System.ServiceModel.EndpointAddress` costruttore. Passa un valore stringa che specifica il file WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/EncryptionService?WSDL`.) Non è necessario utilizzare il `lc_version` attributo. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Creare un `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto ottenendo il valore del `EncryptionServiceClient.Endpoint.Binding` campo. Invia il valore restituito a `BasicHttpBinding`.
   * Imposta il `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegna al campo il nome utente dei moduli AEM `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore password corrispondente al campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Ottieni il documento PDF crittografato.

   * Creare un `BLOB` mediante il costruttore.
   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore stringa che rappresenta la posizione del file del documento PDF crittografato e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto della `System.IO.FileStream` oggetto. È possibile determinare le dimensioni della matrice di byte ottenendo `System.IO.FileStream` dell&#39;oggetto `Length` proprietà.
   * Compilare la matrice di byte con i dati di flusso richiamando `System.IO.FileStream` dell&#39;oggetto `Read` e passando la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare il `BLOB` mediante l&#39;assegnazione del contenuto della matrice di byte `BLOB` dell&#39;oggetto `MTOM` membro dati.

1. Determinare il tipo di crittografia.

   * Richiama `EncryptionServiceClient` dell&#39;oggetto `getPDFEncryption` e trasmettere il `BLOB` oggetto che contiene il documento PDF. Questo metodo restituisce un `EncryptionTypeResult` oggetto.
   * Ottieni il valore di `EncryptionTypeResult` dell&#39;oggetto `encryptionType` metodo dati. Se, ad esempio, il documento PDF è protetto con la crittografia basata su password, il valore di questo membro dati è `EncryptionType.PASSWORD`.

**Consulta anche**

[Riepilogo dei passaggi](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamare AEM Forms con SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
