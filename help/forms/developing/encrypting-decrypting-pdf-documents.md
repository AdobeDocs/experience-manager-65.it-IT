---
title: Crittografia e decrittografia dei documenti PDF
seo-title: Encrypting and Decrypting PDF Documents
description: Utilizza il servizio di crittografia per crittografare e decrittografare i documenti. Le attività del servizio di cifratura includono la cifratura di un documento PDF con una password, la cifratura di un documento PDF con un certificato, la rimozione della cifratura basata su password da un documento PDF, la rimozione della cifratura basata su certificato da un documento PDF, lo sblocco del documento PDF per consentire l’esecuzione di altre operazioni del servizio e la determinazione del tipo di cifratura di un documento PDF protetto.
seo-description: Use the Encryption service to encrypt and decrypt documents. The Encryption service tasks include encrypting a PDF document with a password, encrypting a PDF document with a certificate, removing password-based encryption from a PDF document, removing certificate-based encryption from a PDF document, unlocking the PDF document so that other service operations can be performed, and determining the encryption type of a secured PDF document.
uuid: 4e4e2716-c21f-4bfe-ae7a-7e91442414ef
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 5e4bda3a-5648-4c0f-b2f8-bdbebb88f537
role: Developer
exl-id: d3cbca7f-9277-4d61-b198-abf4bb008f15
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '8189'
ht-degree: 0%

---

# Crittografia e decrittografia dei documenti PDF {#encrypting-and-decrypting-pdf-documents}

**Esempi ed esempi in questo documento sono solo per AEM Forms in ambiente JEE.**

**Informazioni sul servizio di crittografia**

Il servizio di cifratura consente di cifrare e decrittografare i documenti. Quando un documento viene crittografato, il suo contenuto diventa illeggibile. Un utente autorizzato può decrittografare il documento per ottenere l&#39;accesso ai contenuti. Se un documento PDF è crittografato con una password, è necessario specificare la password aperta prima di poter visualizzare il documento in Adobe Reader o Adobe Acrobat. Analogamente, se un documento PDF è crittografato con un certificato, l’utente deve decrittografare il documento PDF con la chiave pubblica corrispondente al certificato (chiave privata) utilizzato per cifrare il documento PDF.

Puoi eseguire queste attività utilizzando il servizio di cifratura:

* Cifrare un documento PDF con una password. (Vedi [Crittografia dei documenti PDF con una password](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password).)
* Cifrare un documento PDF con un certificato. (Vedi [Cifratura di documenti PDF con certificati](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates).)
* Rimuovere la crittografia basata su password da un documento PDF. (Vedi [Rimozione della crittografia della password](encrypting-decrypting-pdf-documents.md#removing-password-encryption).)
* Rimuovere la crittografia basata su certificato da un documento PDF. (Vedi [Rimozione della crittografia basata su certificato](encrypting-decrypting-pdf-documents.md#removing-certificate-based-encryption).)
* Sblocca il documento di PDF in modo da eseguire altre operazioni del servizio. Ad esempio, dopo lo sblocco di un documento PDF crittografato con password, è possibile applicarvi una firma digitale. (Vedi [Sblocco dei documenti PDF crittografati](encrypting-decrypting-pdf-documents.md#unlocking-encrypted-pdf-documents).)
* Determinare il tipo di crittografia di un documento PDF protetto. (Vedi [Determinazione del tipo di crittografia](encrypting-decrypting-pdf-documents.md#determining-encryption-type).)

>[!NOTE]
>
>Per ulteriori informazioni sul servizio di cifratura, vedi [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Crittografia dei documenti PDF con una password {#encrypting-pdf-documents-with-a-password}

Quando si crittografa un documento PDF con una password, un utente deve specificare la password per aprire il documento PDF in Adobe Reader o Acrobat. Inoltre, prima di poter eseguire un’altra operazione AEM Forms, ad esempio la firma digitale del documento PDF, è necessario sbloccare un documento PDF crittografato con password.

>[!NOTE]
>
>Se carichi un documento PDF crittografato nell’archivio AEM Forms, non sarà possibile decrittografare il documento PDF ed estrarre il contenuto XDP. È consigliabile non crittografare un documento prima di caricarlo nell’archivio AEM Forms. (Vedi [Scrittura delle risorse](/help/forms/developing/aem-forms-repository.md#writing-resources).)

>[!NOTE]
>
>Per ulteriori informazioni sul servizio di cifratura, vedi [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary-of-steps}

Per crittografare un documento PDF con una password, effettua le seguenti operazioni:

1. Includi file di progetto.
1. Creare un oggetto API client di crittografia.
1. Ottenere un documento PDF da crittografare.
1. Impostare le opzioni di esecuzione della crittografia.
1. Aggiungi la password.
1. Salvare il documento PDF crittografato come file PDF.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso della classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è distribuito su JBoss)
* jbossall-client.jar (richiesto se AEM Forms è distribuito su JBoss)

**Creare un oggetto API client di crittografia**

Per eseguire un&#39;operazione del servizio di cifratura a livello di programmazione, è necessario creare un client del servizio di cifratura.

**Ottenere un documento PDF da crittografare**

Per crittografare il documento con una password, è necessario ottenere un documento PDF non crittografato. Se si tenta di proteggere un documento PDF già crittografato, viene generata un&#39;eccezione.

**Impostare le opzioni di esecuzione della crittografia**

Per crittografare un documento PDF con una password, è necessario specificare quattro valori, inclusi due valori di password. Il primo valore password viene utilizzato per cifrare il documento PDF e deve essere specificato all’apertura del documento PDF. Il secondo valore della password, denominato valore della password master, viene utilizzato per rimuovere la crittografia dal documento PDF. I valori delle password sono sensibili all&#39;uso di maiuscole e minuscole e questi due valori non possono essere gli stessi.

È necessario specificare le risorse del documento PDF da crittografare. È possibile crittografare l’intero documento di PDF, tutti gli elementi eccetto i metadati del documento o solo gli allegati del documento. Se si crittografano solo gli allegati del documento, all&#39;utente viene richiesta una password quando tenta di accedere agli allegati del file.

Durante la cifratura di un documento PDF, è possibile specificare le autorizzazioni associate al documento protetto. Specificando le autorizzazioni, è possibile controllare le azioni che un utente che apre un documento PDF crittografato con password può eseguire. Ad esempio, per estrarre correttamente i dati del modulo, è necessario impostare le seguenti autorizzazioni:

* PASSWORD_EDIT_ADD
* PASSWORD_EDIT_MODIFY

>[!NOTE]
>
>Le autorizzazioni vengono specificate come `PasswordEncryptionPermission` valori di enumerazione.

**Aggiungi la password**

Dopo aver recuperato un documento PDF non protetto e impostato i valori di esecuzione della crittografia, è possibile aggiungere una password al documento PDF.

**Salvare il documento PDF crittografato come file PDF**

È possibile salvare il documento PDF crittografato con password come file PDF.

**Consulta anche**

[Crittografare un documento PDF utilizzando l’API Java](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-using-the-java-api)

[Crittografia di un documento PDF tramite l’API del servizio Web](encrypting-decrypting-pdf-documents.md#encrypting-a-pdf-document-using-the-web-service-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API del servizio di crittografia](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[Cifratura di documenti PDF con certificati](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates)

### Crittografare un documento PDF utilizzando l’API Java {#encrypt-a-pdf-document-using-the-java-api}

Crittografa un documento PDF con una password utilizzando l’API di cifratura (Java):

1. Includi file di progetto.

   Includi file JAR client, come adobe-encryption-client.jar, nel percorso di classe del progetto Java.

1. Creare un’API client di crittografia.

   * Crea un `ServiceClientFactory` oggetto contenente le proprietà di connessione.
   * Crea un `EncryptionServiceClient` utilizzando il relativo costruttore e passando `ServiceClientFactory` oggetto.

1. Ottenere un documento PDF da crittografare.

   * Crea un `java.io.FileInputStream` oggetto che rappresenta il documento PDF da crittografare utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del documento PDF.
   * Crea un `com.adobe.idp.Document` utilizzando il relativo costruttore e passando `java.io.FileInputStream` oggetto.

1. Impostare le opzioni di esecuzione della crittografia.

   * Crea un `PasswordEncryptionOptionSpec` richiamando il relativo costruttore.
   * Specificare le risorse del documento PDF da crittografare richiamando il `PasswordEncryptionOptionSpec` dell’oggetto `setEncryptOption` e passare un `PasswordEncryptionOption` valore di enumerazione che specifica le risorse del documento da crittografare. Ad esempio, per crittografare l’intero documento PDF, inclusi i relativi metadati e i relativi allegati, specificare `PasswordEncryptionOption.ALL`.
   * Crea un `java.util.List` oggetto che memorizza le autorizzazioni di crittografia utilizzando `ArrayList` costruttore.
   * Specifica un&#39;autorizzazione richiamando il `java.util.List` oggetto ‘s `add` e passare un valore di enumerazione corrispondente all&#39;autorizzazione che si desidera impostare. Ad esempio, per impostare l’autorizzazione che consente all’utente di copiare i dati presenti nel documento PDF, specificare `PasswordEncryptionPermission.PASSWORD_EDIT_COPY`. (Ripeti questo passaggio per ogni autorizzazione da impostare).
   * Specifica l’opzione di compatibilità di Acrobat richiamando il `PasswordEncryptionOptionSpec` dell’oggetto `setCompatability` e passare un valore di enumerazione che specifica il livello di compatibilità Acrobat. Ad esempio, puoi specificare `PasswordEncryptionCompatability.ACRO_7`.
   * Specifica il valore della password che consente a un utente di aprire il documento PDF crittografato richiamando il `PasswordEncryptionOptionSpec` dell’oggetto `setDocumentOpenPassword` e passare un valore stringa che rappresenta la password aperta.
   * Specificare il valore della password master che consente a un utente di rimuovere la crittografia dal documento PDF richiamando il `PasswordEncryptionOptionSpec` dell’oggetto `setPermissionPassword` e passare un valore stringa che rappresenta la password master.

1. Aggiungi la password.

   Cifrare il documento PDF richiamando il `EncryptionServiceClient` dell’oggetto `encryptPDFUsingPassword` e passando i seguenti valori:

   * La `com.adobe.idp.Document` oggetto contenente il documento PDF da crittografare con la password.
   * La `PasswordEncryptionOptionSpec` oggetto contenente le opzioni di esecuzione della crittografia.

   La `encryptPDFUsingPassword` restituisce un `com.adobe.idp.Document` oggetto contenente un documento PDF crittografato con password.

1. Salvare il documento PDF crittografato come file PDF.

   * Crea un `java.io.File` e assicurati che l&#39;estensione del file sia .pdf.
   * Richiama il `com.adobe.idp.Document` dell’oggetto `copyToFile` per copiare il contenuto del `com.adobe.idp.Document` al file. Assicurati di utilizzare `com.adobe.idp.Document` oggetto restituito da `encryptPDFUsingPassword` metodo .

**Consulta anche**

[Riepilogo dei passaggi](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Avvio rapido (modalità SOAP): Crittografia di un documento PDF tramite l’API Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-encrypting-a-pdf-document-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Crittografia di un documento PDF tramite l’API del servizio Web {#encrypting-a-pdf-document-using-the-web-service-api}

Crittografare un documento PDF con una password utilizzando l’API di cifratura (servizio Web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurati di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l’indirizzo IP del server che ospita AEM Forms.

1. Creare un oggetto API client di crittografia.

   * Crea un `EncryptionServiceClient` utilizzando il relativo costruttore predefinito.
   * Crea un `EncryptionServiceClient.Endpoint.Address` utilizzando `System.ServiceModel.EndpointAddress` costruttore. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/EncryptionService?WSDL`.) Non è necessario utilizzare il `lc_version` attributo. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Crea un `System.ServiceModel.BasicHttpBinding` ottenendo il valore del `EncryptionServiceClient.Endpoint.Binding` campo . Imposta il valore restituito su `BasicHttpBinding`.
   * Imposta la `System.ServiceModel.BasicHttpBinding` dell’oggetto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegnare il nome utente del modulo di AEM al campo `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore della password corrispondente al campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Ottenere un documento PDF da crittografare.

   * Crea un `BLOB` utilizzando il relativo costruttore. La `BLOB` viene utilizzato per memorizzare un documento PDF crittografato con una password.
   * Crea un `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF da crittografare e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto del `System.IO.FileStream` oggetto. È possibile determinare le dimensioni dell&#39;array di byte ottenendo il `System.IO.FileStream` dell’oggetto `Length` proprietà.
   * Compilare l&#39;array di byte con i dati del flusso richiamando il `System.IO.FileStream` dell’oggetto `Read` e passare l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare `BLOB` assegnando il contenuto dell&#39;array di byte al `BLOB` dell’oggetto `MTOM` membro dati.

1. Impostare le opzioni di esecuzione della crittografia.

   * Crea un `PasswordEncryptionOptionSpec` utilizzando il relativo costruttore.
   * Specificare le risorse del documento PDF da crittografare tramite l’assegnazione di un `PasswordEncryptionOption` valore di enumerazione nel `PasswordEncryptionOptionSpec` dell’oggetto `encryptOption` membro dati. Per crittografare l’intero PDF, inclusi i relativi metadati e i relativi allegati, assegna `PasswordEncryptionOption.ALL` a questo membro dati.
   * Specifica l’opzione di compatibilità Acrobat assegnando un `PasswordEncryptionCompatability` valore di enumerazione nel `PasswordEncryptionOptionSpec` dell’oggetto `compatability` membro dati. Ad esempio, assegna `PasswordEncryptionCompatability.ACRO_7` a questo membro dati.
   * Specificare il valore della password che consente all&#39;utente di aprire il documento PDF crittografato assegnando un valore di stringa che rappresenta la password aperta al `PasswordEncryptionOptionSpec` dell’oggetto `documentOpenPassword` membro dati.
   * Specificare il valore della password che consente all&#39;utente di rimuovere la crittografia dal documento PDF assegnando un valore di stringa che rappresenta la password master al `PasswordEncryptionOptionSpec` dell’oggetto `permissionPassword` membro dati.

1. Aggiungi la password.

   Cifrare il documento PDF richiamando il `EncryptionServiceClient` dell’oggetto `encryptPDFUsingPassword` e passando i seguenti valori:

   * La `BLOB` oggetto contenente il documento PDF da crittografare con la password.
   * La `PasswordEncryptionOptionSpec` oggetto contenente le opzioni di esecuzione della crittografia.

   La `encryptPDFUsingPassword` restituisce un `BLOB` oggetto contenente un documento PDF crittografato con password.

1. Salvare il documento PDF crittografato come file PDF.

   * Crea un `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento protetto PDF.
   * Creare un array di byte che memorizza il contenuto dei dati del `BLOB` oggetto restituito da `encryptPDFUsingPassword` metodo . Compilare l’array di byte ottenendo il valore del `BLOB` dell’oggetto `MTOM` membro dati.
   * Crea un `System.IO.BinaryWriter` richiamando il relativo costruttore e passando `System.IO.FileStream` oggetto.
   * Scrivi il contenuto dell’array di byte in un file PDF richiamando il `System.IO.BinaryWriter` dell’oggetto `Write` e passare l&#39;array di byte.

**Consulta anche**

[Riepilogo dei passaggi](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Richiamo di AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamo di AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Cifratura di documenti PDF con certificati {#encrypting-pdf-documents-with-certificates}

La crittografia basata su certificato consente di crittografare un documento per destinatari specifici tramite la tecnologia a chiave pubblica. A diversi destinatari possono essere assegnate autorizzazioni diverse per il documento. Molti aspetti della crittografia sono resi possibili dalla tecnologia a chiave pubblica. Viene utilizzato un algoritmo per generare due numeri di grandi dimensioni, noti come *chiavi*, che hanno le seguenti proprietà:

* Una chiave viene utilizzata per crittografare un set di dati. Successivamente, solo l’altra chiave può essere utilizzata per decrittografare i dati.
* È impossibile distinguere una chiave dall&#39;altra.

Una delle chiavi funge da chiave privata dell’utente. È importante che solo l’utente abbia accesso a questa chiave. L’altra chiave è la chiave pubblica dell’utente, che può essere condivisa con altri utenti.

Un certificato a chiave pubblica contiene la chiave pubblica di un utente e le informazioni di identificazione. Il formato X.509 viene utilizzato per memorizzare i certificati. I certificati sono generalmente rilasciati e firmati digitalmente da un’autorità di certificazione (CA), un’entità riconosciuta che fornisce una misura di affidabilità nella validità del certificato. I certificati hanno una data di scadenza, dopo la quale non sono più validi. Inoltre, gli elenchi di revoche di certificati (CRL) forniscono informazioni sui certificati revocati prima della data di scadenza. I LCR sono pubblicati periodicamente dalle autorità di certificazione. Lo stato di revoca di un certificato può essere recuperato anche tramite il protocollo OCSP (Online Certificate Status Protocol) in rete.

>[!NOTE]
>
>Se carichi un documento PDF crittografato nell’archivio AEM Forms, non sarà possibile decrittografare il documento PDF ed estrarre il contenuto XDP. È consigliabile non crittografare un documento prima di caricarlo nell’archivio AEM Forms. (Vedi [Scrittura delle risorse](/help/forms/developing/aem-forms-repository.md#writing-resources).)

>[!NOTE]
>
>Prima di poter crittografare un documento PDF con un certificato, è necessario assicurarsi di aggiungere il certificato ad AEM Forms. Un certificato viene aggiunto tramite la console di amministrazione o a livello di programmazione utilizzando l’API di Trust Manager. (Vedi [Importazione delle credenziali tramite l’API di Trust Manager](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api).)

>[!NOTE]
>
>Per ulteriori informazioni sul servizio di cifratura, vedi [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-1}

Per crittografare un documento PDF con un certificato, effettua le seguenti operazioni:

1. Includi file di progetto.
1. Creare un oggetto API client di crittografia.
1. Ottenere un documento PDF da crittografare.
1. Fai riferimento al certificato.
1. Impostare le opzioni di esecuzione della crittografia.
1. Creare un documento PDF crittografato con certificato.
1. Salvare il documento PDF crittografato come file PDF.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso della classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è distribuito su JBoss Application Server)
* jbossall-client.jar (richiesto se AEM Forms è distribuito su JBoss Application Server)

**Creare un oggetto API client di crittografia**

Per eseguire un&#39;operazione del servizio di cifratura a livello di programmazione, è necessario creare un client del servizio di cifratura. Se utilizzi l’API del servizio Java Encryption, crea un `EncrytionServiceClient` oggetto. Se utilizzi l’API del servizio Web Encryption Service, crea un `EncryptionServiceService` oggetto.

**Ottenere un documento PDF da crittografare**

Per eseguire la cifratura, è necessario ottenere un documento PDF non crittografato. Se si tenta di proteggere un documento PDF già crittografato, viene generata un&#39;eccezione.

**Riferimento al certificato**

Per cifrare un documento PDF con un certificato, fare riferimento a un certificato utilizzato per cifrare un documento PDF. Il certificato è un file .cer, un file .crt o un file .pem. Un file PKCS#12 viene utilizzato per memorizzare le chiavi private con i certificati corrispondenti.

Quando si crittografa un documento PDF con un certificato, specificare le autorizzazioni associate al documento protetto. Specificando le autorizzazioni, è possibile controllare le azioni eseguibili da un utente che apre un documento PDF crittografato con certificato.

**Impostare le opzioni di esecuzione della crittografia**

Specificare le risorse del documento PDF da crittografare. È possibile crittografare l’intero documento PDF, tutti gli elementi eccetto i metadati del documento o solo gli allegati del documento.

**Creare un documento PDF crittografato con un certificato**

Dopo aver recuperato un documento PDF non protetto, fatto riferimento al certificato e impostato le opzioni di esecuzione, è possibile creare un documento PDF crittografato tramite certificato. Una volta crittografato il documento PDF, è necessario disporre della chiave pubblica corrispondente per decrittografarlo.

**Salvare il documento PDF crittografato come file PDF**

È possibile salvare il documento PDF crittografato come file PDF.

**Consulta anche**

[Crittografare un documento PDF con un certificato utilizzando l’API Java](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-with-a-certificate-using-the-java-api)

[Crittografare un documento PDF con un certificato utilizzando l’API del servizio Web](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-with-a-certificate-using-the-web-service-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API del servizio di crittografia](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[Crittografia dei documenti PDF con una password](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Crittografare un documento PDF con un certificato utilizzando l’API Java {#encrypt-a-pdf-document-with-a-certificate-using-the-java-api}

Crittografare un documento PDF con un certificato utilizzando l’API di cifratura (Java):

1. Includi file di progetto.

   Includi file JAR client, come adobe-encryption-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto API client di crittografia.

   * Crea un `ServiceClientFactory` oggetto contenente le proprietà di connessione.
   * Crea un `EncryptionServiceClient` utilizzando il relativo costruttore e passando `ServiceClientFactory` oggetto.

1. Ottenere un documento PDF da crittografare.

   * Crea un `java.io.FileInputStream` oggetto che rappresenta il documento PDF da crittografare utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del documento PDF.
   * Crea un `com.adobe.idp.Document` utilizzando il relativo costruttore e passando `java.io.FileInputStream` oggetto.

1. Fai riferimento al certificato.

   * Crea un `java.util.List` oggetto che memorizza le informazioni sulle autorizzazioni utilizzando il relativo costruttore.
   * Specifica l&#39;autorizzazione associata al documento crittografato richiamando il `java.util.List` dell’oggetto `add` e passare un `CertificateEncryptionPermissions` valore di enumerazione che rappresenta le autorizzazioni concesse all&#39;utente che apre il documento protetto PDF. Ad esempio, per specificare tutte le autorizzazioni, passare `CertificateEncryptionPermissions.PKI_ALL_PERM`.
   * Crea un `Recipient` utilizzando il relativo costruttore.
   * Crea un `java.io.FileInputStream` oggetto che rappresenta il certificato utilizzato per crittografare il documento PDF utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del certificato.
   * Crea un `com.adobe.idp.Document` utilizzando il relativo costruttore e passando `java.io.FileInputStream` oggetto che rappresenta il certificato.
   * Richiama il `Recipient` dell’oggetto `setX509Cert` e passare il `com.adobe.idp.Document` oggetto contenente il certificato. (Inoltre, il `Recipient`può avere un alias di certificato Truststore o un URL LDAP come origine del certificato.)
   * Crea un `CertificateEncryptionIdentity` oggetto che memorizza le informazioni sulle autorizzazioni e sui certificati utilizzando il relativo costruttore.
   * Richiama il `CertificateEncryptionIdentity` dell’oggetto `setPerms` e passare il `java.util.List` oggetto che memorizza le informazioni sulle autorizzazioni.
   * Richiama il `CertificateEncryptionIdentity` dell’oggetto `setRecipient` e passare il `Recipient` oggetto che memorizza le informazioni sul certificato.
   * Crea un `java.util.List` oggetto che memorizza le informazioni sul certificato utilizzando il relativo costruttore.
   * Richiama il `java.util.List` il metodo add dell&#39;oggetto e trasmettere `CertificateEncryptionIdentity` oggetto. (Questa `java.util.List` viene passato come parametro al `encryptPDFUsingCertificates` metodo).

1. Impostare le opzioni di esecuzione della crittografia.

   * Crea un `CertificateEncryptionOptionSpec` richiamando il relativo costruttore.
   * Specificare le risorse del documento PDF da crittografare richiamando il `CertificateEncryptionOptionSpec` dell’oggetto `setOption` e passare un `CertificateEncryptionOption` valore di enumerazione che specifica le risorse del documento da crittografare. Ad esempio, per crittografare l’intero documento PDF, inclusi i relativi metadati e i relativi allegati, specificare `CertificateEncryptionOption.ALL`.
   * Specifica l’opzione di compatibilità di Acrobat richiamando il `CertificateEncryptionOptionSpec` dell’oggetto `setCompat` e passare un `CertificateEncryptionCompatibility` valore di enumerazione che specifica il livello di compatibilità Acrobat. Ad esempio, puoi specificare `CertificateEncryptionCompatibility.ACRO_7`.

1. Creare un documento PDF crittografato con certificato.

   Cifrare il documento PDF con un certificato richiamando il `EncryptionServiceClient` dell’oggetto `encryptPDFUsingCertificates` e passando i seguenti valori:

   * La `com.adobe.idp.Document` oggetto contenente il documento PDF da crittografare.
   * La `java.util.List` oggetto che memorizza le informazioni sul certificato.
   * La `CertificateEncryptionOptionSpec` oggetto contenente le opzioni di esecuzione della crittografia.

   La `encryptPDFUsingCertificates` restituisce un `com.adobe.idp.Document` oggetto contenente un documento PDF crittografato con certificato.

1. Salvare il documento PDF crittografato come file PDF.

   * Crea un `java.io.File` e assicurati che l&#39;estensione del nome del file sia .pdf.
   * Richiama il `com.adobe.idp.Document` dell’oggetto `copyToFile` per copiare il contenuto del `com.adobe.idp.Document` al file. Assicurati di utilizzare `com.adobe.idp.Document` oggetto restituito da `encryptPDFUsingCertificates` metodo .

**Consulta anche**

[Riepilogo dei passaggi](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Avvio rapido (modalità SOAP): Crittografia di un documento PDF con un certificato tramite l’API Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-encrypting-a-pdf-document-with-a-certificate-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Crittografare un documento PDF con un certificato utilizzando l’API del servizio Web {#encrypt-a-pdf-document-with-a-certificate-using-the-web-service-api}

Crittografare un documento PDF con un certificato utilizzando l’API di cifratura (servizio Web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurati di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l’indirizzo IP del server che ospita AEM Forms.

1. Creare un oggetto API client di crittografia.

   * Crea un `EncryptionServiceClient` utilizzando il relativo costruttore predefinito.
   * Crea un `EncryptionServiceClient.Endpoint.Address` utilizzando `System.ServiceModel.EndpointAddress` costruttore. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/EncryptionService?WSDL`.) Non è necessario utilizzare il `lc_version` attributo. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Crea un `System.ServiceModel.BasicHttpBinding` ottenendo il valore del `EncryptionServiceClient.Endpoint.Binding` campo . Imposta il valore restituito su `BasicHttpBinding`.
   * Imposta la `System.ServiceModel.BasicHttpBinding` dell’oggetto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegnare il nome utente del modulo di AEM al campo `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore della password corrispondente al campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Ottenere un documento PDF da crittografare.

   * Crea un `BLOB` utilizzando il relativo costruttore. La `BLOB` viene utilizzato per memorizzare un documento PDF crittografato con un certificato.
   * Crea un `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF da crittografare e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto del `System.IO.FileStream` oggetto. È possibile determinare le dimensioni dell&#39;array di byte ottenendo il `System.IO.FileStream` dell’oggetto `Length` proprietà.
   * Compilare l&#39;array di byte con i dati del flusso richiamando il `System.IO.FileStream` dell’oggetto `Read` e passare l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare `BLOB` oggetto assegnando il relativo `MTOM` con il contenuto dell&#39;array di byte.

1. Fai riferimento al certificato.

   * Crea un `Recipient` utilizzando il relativo costruttore. Questo oggetto memorizzerà le informazioni sul certificato.
   * Crea un `BLOB` utilizzando il relativo costruttore. Questo `BLOB` l’oggetto memorizzerà il certificato che crittografa il documento PDF.
   * Crea un `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del certificato e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto del `System.IO.FileStream` oggetto. È possibile determinare le dimensioni dell&#39;array di byte ottenendo il `System.IO.FileStream` dell’oggetto `Length` proprietà.
   * Compilare l&#39;array di byte con i dati del flusso richiamando il `System.IO.FileStream` dell’oggetto `Read` e passare l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare `BLOB` assegnando il contenuto dell&#39;array di byte al `BLOB` dell’oggetto `MTOM` membro dati.
   * Assegna `BLOB` oggetto che memorizza il certificato nel `Recipient` dell’oggetto `x509Cert` membro dati.
   * Crea un `CertificateEncryptionIdentity` oggetto che memorizza le informazioni sul certificato utilizzando il relativo costruttore.
   * Assegna `Recipient` oggetto che memorizza il certificato nel `CertificateEncryptionIdentity`membro dati destinatario dell’oggetto.
   * Crea un `Object` e assegna `CertificateEncryptionIdentity` al primo elemento del `Object` array. Questo `Object` viene passato come parametro al `encryptPDFUsingCertificates` metodo .

1. Impostare le opzioni di esecuzione della crittografia.

   * Crea un `CertificateEncryptionOptionSpec` utilizzando il relativo costruttore.
   * Specificare le risorse del documento PDF da crittografare tramite l’assegnazione di un `CertificateEncryptionOption` valore di enumerazione nel `CertificateEncryptionOptionSpec` dell’oggetto `option` membro dati. Per crittografare l’intero documento PDF, inclusi i relativi metadati e i relativi allegati, assegnare `CertificateEncryptionOption.ALL` a questo membro dati.
   * Specifica l’opzione di compatibilità Acrobat assegnando un `CertificateEncryptionCompatibility` valore di enumerazione nel `CertificateEncryptionOptionSpec` dell’oggetto `compat` membro dati. Ad esempio, assegna `CertificateEncryptionCompatibility.ACRO_7` a questo membro dati.

1. Creare un documento PDF crittografato con certificato.

   Cifrare il documento PDF con un certificato richiamando il `EncryptionServiceService` dell’oggetto `encryptPDFUsingCertificates` e passando i seguenti valori:

   * La `BLOB` oggetto contenente il documento PDF da crittografare.
   * La `Object` array in cui sono memorizzate le informazioni sul certificato.
   * La `CertificateEncryptionOptionSpec` oggetto contenente le opzioni di esecuzione della crittografia.

   La `encryptPDFUsingCertificates` restituisce un `BLOB` oggetto contenente un documento PDF crittografato con certificato.

1. Salvare il documento PDF crittografato come file PDF.

   * Crea un `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento protetto PDF.
   * Creare un array di byte che memorizza il contenuto dei dati del `BLOB` oggetto restituito da `encryptPDFUsingCertificates` metodo . Compilare l’array di byte ottenendo il valore del `BLOB` dell’oggetto `binaryData` membro dati.
   * Crea un `System.IO.BinaryWriter` richiamando il relativo costruttore e passando `System.IO.FileStream` oggetto.
   * Scrivi il contenuto dell’array di byte in un file PDF richiamando il `System.IO.BinaryWriter` dell’oggetto `Write` e passare l&#39;array di byte.

**Consulta anche**

[Riepilogo dei passaggi](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Richiamo di AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamo di AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Rimozione della crittografia basata su certificato {#removing-certificate-based-encryption}

È possibile rimuovere la crittografia basata su certificato da un documento PDF per consentire agli utenti di aprire il documento PDF in Adobe Reader o Acrobat. Per rimuovere la crittografia da un documento PDF crittografato con un certificato, è necessario fare riferimento a una chiave pubblica. Una volta rimossa la crittografia da un documento PDF, questa non sarà più protetta.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio di cifratura, vedi [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-2}

Per rimuovere la crittografia basata su certificato da un documento PDF, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Crea un client del servizio di crittografia.
1. Ottenere il documento PDF crittografato.
1. Rimuovi crittografia.
1. Salvare il documento PDF come file PDF.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso della classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è distribuito su JBoss Application Server)
* jbossall-client.jar (richiesto se AEM Forms è distribuito su JBoss Application Server)

**Creare un client del servizio di crittografia**

Per eseguire un&#39;operazione del servizio di cifratura a livello di programmazione, è necessario creare un client del servizio di cifratura. Se utilizzi l’API del servizio Java Encryption, crea un `EncrytionServiceClient` oggetto. Se utilizzi l’API del servizio Web Encryption Service, crea un `EncryptionServiceService` oggetto.

**Ottenere il documento PDF crittografato**

Per rimuovere la crittografia basata su certificato, è necessario ottenere un documento PDF crittografato. Se si tenta di rimuovere la crittografia da un documento PDF non crittografato, viene generata un&#39;eccezione. Analogamente, se si tenta di rimuovere la crittografia basata su certificato da un documento crittografato con password, viene generata un&#39;eccezione.

**Rimuovi crittografia**

Per rimuovere la crittografia basata su certificato da un documento PDF crittografato, è necessario disporre sia di un documento PDF crittografato che della chiave privata corrispondente alla chiave utilizzata per crittografare il documento PDF. Il valore alias della chiave privata viene specificato durante la rimozione della crittografia basata su certificato da un documento PDF crittografato. Per informazioni sulla chiave pubblica, vedi [Cifratura di documenti PDF con certificati](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates).

>[!NOTE]
>
>Una chiave privata viene memorizzata nell&#39;archivio attendibilità di AEM Forms. Quando un certificato è posizionato in tale posizione, viene specificato un valore di alias.

**Salvare il documento PDF**

Dopo aver rimosso la crittografia basata su certificato da un documento PDF crittografato, è possibile salvare il documento PDF come file PDF. Gli utenti possono aprire il documento PDF in Adobe Reader o Acrobat.

**Consulta anche**

[Rimuovere la crittografia basata su certificato utilizzando l’API Java](encrypting-decrypting-pdf-documents.md#remove-certificate-based-encryption-using-the-java-api)

[Rimuovere la crittografia basata su certificato utilizzando l’API del servizio Web](encrypting-decrypting-pdf-documents.md#remove-certificate-based-encryption-using-the-web-service-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API del servizio di crittografia](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

### Rimuovere la crittografia basata su certificato utilizzando l’API Java {#remove-certificate-based-encryption-using-the-java-api}

È possibile rimuovere la crittografia basata su certificato da un documento PDF utilizzando l’API di cifratura (Java):

1. Includi file di progetto.

   Includi file JAR client, come adobe-encryption-client.jar, nel percorso di classe del progetto Java.

1. Crea un client del servizio di crittografia.

   * Crea un `ServiceClientFactory` oggetto contenente le proprietà di connessione.
   * Crea un `EncryptionServiceClient` utilizzando il relativo costruttore e passando `ServiceClientFactory` oggetto.

1. Ottenere il documento PDF crittografato.

   * Crea un `java.io.FileInputStream` oggetto che rappresenta il documento PDF crittografato utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del documento PDF crittografato.
   * Crea un `com.adobe.idp.Document` utilizzando il relativo costruttore e passando `java.io.FileInputStream` oggetto.

1. Rimuovi crittografia.

   Rimuovi la crittografia basata su certificato dal documento PDF richiamando il `EncryptionServiceClient` dell’oggetto `removePDFCertificateSecurity` e passando i seguenti valori:

   * La `com.adobe.idp.Document` oggetto contenente il documento PDF crittografato.
   * Valore stringa che specifica il nome alias della chiave privata corrispondente alla chiave utilizzata per crittografare il documento PDf.

   La `removePDFCertificateSecurity` restituisce un `com.adobe.idp.Document` oggetto contenente un documento PDF non protetto.

1. Salvare il documento PDF.

   * Crea un `java.io.File` e assicurati che l&#39;estensione del file sia .pdf.
   * Richiama il `com.adobe.idp.Document` dell’oggetto `copyToFile` per copiare il contenuto del `Document` al file. Assicurati di utilizzare `com.adobe.idp.Document` oggetto restituito da `removePDFCredentialSecurity` metodo .

**Consulta anche**

[Riepilogo dei passaggi](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Avvio rapido (modalità SOAP): Rimozione della crittografia basata su certificato tramite l’API Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-removing-certificate-based-encryption-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Rimuovere la crittografia basata su certificato utilizzando l’API del servizio Web {#remove-certificate-based-encryption-using-the-web-service-api}

Rimuovi la crittografia basata su certificato utilizzando l’API di cifratura (servizio Web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurati di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l’indirizzo IP del server che ospita AEM Forms.

1. Crea un client del servizio di crittografia.

   * Crea un `EncryptionServiceClient` utilizzando il relativo costruttore predefinito.
   * Crea un `EncryptionServiceClient.Endpoint.Address` utilizzando `System.ServiceModel.EndpointAddress` costruttore. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/EncryptionService?WSDL`.) Non è necessario utilizzare il `lc_version` attributo. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Crea un `System.ServiceModel.BasicHttpBinding` ottenendo il valore del `EncryptionServiceClient.Endpoint.Binding` campo . Imposta il valore restituito su `BasicHttpBinding`.
   * Imposta la `System.ServiceModel.BasicHttpBinding` dell’oggetto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegnare il nome utente del modulo di AEM al campo `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore della password corrispondente al campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Ottenere il documento PDF crittografato.

   * Crea un `BLOB` utilizzando il relativo costruttore. La `BLOB` viene utilizzato per memorizzare il documento PDF crittografato.
   * Crea un `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF crittografato e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto del `System.IO.FileStream` oggetto. È possibile determinare le dimensioni dell&#39;array di byte ottenendo il `System.IO.FileStream` dell’oggetto `Length` proprietà.
   * Compilare l&#39;array di byte con i dati del flusso richiamando il `System.IO.FileStream` dell’oggetto `Read` e passare l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare `BLOB` assegnando il contenuto dell&#39;array di byte al `BLOB` dell’oggetto `MTOM` membro dati.

1. Rimuovi crittografia.

   Richiama il `EncryptionServiceClient` dell’oggetto `removePDFCertificateSecurity` e passare i seguenti valori:

   * La `BLOB` oggetto che contiene dati di flusso di file che rappresentano un documento PDF crittografato.
   * Valore stringa che specifica il nome alias della chiave pubblica corrispondente alla chiave privata utilizzata per crittografare il documento PDf.

   La `removePDFCredentialSecurity` restituisce un `BLOB` oggetto contenente un documento PDF non protetto.

1. Salvare il documento PDF.

   * Crea un `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF non protetto.
   * Creare un array di byte che memorizza il contenuto del `BLOB` oggetto restituito da `removePDFPasswordSecurity` metodo . Compilare l’array di byte ottenendo il valore del `BLOB` dell’oggetto `MTOM` membro dati.
   * Crea un `System.IO.BinaryWriter` richiamando il relativo costruttore e passando `System.IO.FileStream` oggetto.
   * Scrivi il contenuto dell’array di byte in un file PDF richiamando il `System.IO.BinaryWriter` dell’oggetto `Write` e passare l&#39;array di byte.

**Consulta anche**

[Riepilogo dei passaggi](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Richiamo di AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamo di AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Rimozione della crittografia della password {#removing-password-encryption}

È possibile rimuovere la crittografia basata su password da un documento PDF per consentire agli utenti di aprire il documento PDF in Adobe Reader o Acrobat senza dover specificare una password. Dopo la rimozione della crittografia basata su password da un documento PDF, il documento non è più protetto.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio di cifratura, vedi [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-3}

Per rimuovere la crittografia basata su password da un documento PDF, eseguire le operazioni seguenti:

1. Includi file di progetto
1. Crea un client del servizio di crittografia.
1. Ottenere il documento PDF crittografato.
1. Rimuovi la password.
1. Salvare il documento PDF come file PDF.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso della classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è distribuito su JBoss)
* jbossall-client.jar (richiesto se AEM Forms è distribuito su JBoss)

**Creare un client del servizio di crittografia**

Per eseguire un&#39;operazione del servizio di cifratura a livello di programmazione, è necessario creare un client del servizio di cifratura. Se utilizzi l’API del servizio Java Encryption, crea un `EncrytionServiceClient` oggetto. Se utilizzi l’API del servizio Web Encryption Service, crea un `EncryptionServiceService` oggetto.

**Ottenere il documento PDF crittografato**

Per rimuovere la crittografia basata su password, è necessario ottenere un documento PDF crittografato. Se si tenta di rimuovere la crittografia da un documento PDF non crittografato, viene generata un&#39;eccezione.

**Rimuovere la password**

Per rimuovere la crittografia basata su password da un documento PDF crittografato, è necessario disporre sia di un documento PDF crittografato sia di un valore password master utilizzato per rimuovere la crittografia dal documento PDF. La password utilizzata per aprire un documento PDF crittografato con password non può essere utilizzata per rimuovere la crittografia. Una password master viene specificata quando il documento PDF viene crittografato con una password. (Vedi [Crittografia dei documenti PDF con una password](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password).)

**Salvare il documento PDF**

Dopo la rimozione della crittografia basata su password da un documento PDF, è possibile salvare il documento PDF come file PDF. Gli utenti possono aprire il documento PDF in Adobe Reader o Acrobat senza specificare una password.

**Consulta anche**

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API del servizio di crittografia](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[Crittografia dei documenti PDF con una password](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Rimuovere la crittografia basata su password utilizzando l’API Java {#remove-password-based-encryption-using-the-java-api}

È possibile rimuovere la crittografia basata su password da un documento PDF utilizzando l’API di cifratura (Java):

1. Includi file di progetto.

   Includi file JAR client, come adobe-encryption-client.jar, nel percorso di classe del progetto Java.

1. Crea un client del servizio di crittografia.

   * Crea un `ServiceClientFactory` oggetto contenente le proprietà di connessione.
   * Crea un `EncryptionServiceClient` utilizzando il relativo costruttore e passando `ServiceClientFactory` oggetto.

1. Ottenere il documento PDF crittografato.

   * Crea un `java.io.FileInputStream` oggetto che rappresenta il documento PDF crittografato utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del documento PDF.
   * Crea un `com.adobe.idp.Document` utilizzando il relativo costruttore e passando `java.io.FileInputStream` oggetto.

1. Rimuovi la password.

   Rimuovere la crittografia basata su password dal documento PDF richiamando il `EncryptionServiceClient` dell’oggetto `removePDFPasswordSecurity` e passando i seguenti valori:

   * A `com.adobe.idp.Document` oggetto contenente il documento PDF crittografato.
   * Valore stringa che specifica il valore della password master utilizzato per rimuovere la crittografia dal documento PDF.

   La `removePDFPasswordSecurity` restituisce un `com.adobe.idp.Document` oggetto contenente un documento PDF non protetto.

1. Salvare il documento PDF.

   * Crea un `java.io.File` e assicurati che l&#39;estensione del nome del file sia .pdf.
   * Richiama il `com.adobe.idp.Document` dell’oggetto `copyToFile` per copiare il contenuto del `Document` al file. Assicurati di utilizzare `Document` oggetto restituito da `removePDFPasswordSecurity` metodo .

**Consulta anche**

[Avvio rapido (modalità SOAP): Rimozione della crittografia basata su password tramite l’API Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-removing-password-based-encryption-using-the-java-api)

### Rimuovere la crittografia basata su password utilizzando l’API del servizio Web {#remove-password-based-encryption-using-the-web-service-api}

È possibile rimuovere la crittografia basata su password utilizzando l’API di cifratura (servizio Web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurati di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l’indirizzo IP del server che ospita AEM Forms.

1. Crea un client del servizio di crittografia.

   * Crea un `EncryptionServiceClient` utilizzando il relativo costruttore predefinito.
   * Crea un `EncryptionServiceClient.Endpoint.Address` utilizzando `System.ServiceModel.EndpointAddress` costruttore. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/EncryptionService?WSDL`.) Non è necessario utilizzare il `lc_version` attributo. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Crea un `System.ServiceModel.BasicHttpBinding` ottenendo il valore del `EncryptionServiceClient.Endpoint.Binding` campo . Imposta il valore restituito su `BasicHttpBinding`.
   * Imposta la `System.ServiceModel.BasicHttpBinding` dell’oggetto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegnare il nome utente del modulo di AEM al campo `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore della password corrispondente al campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Ottenere il documento PDF crittografato.

   * Crea un `BLOB` utilizzando il relativo costruttore. La `BLOB` viene utilizzato per memorizzare un documento PDF crittografato con password.
   * Crea un `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF crittografato e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto del `System.IO.FileStream` oggetto. È possibile determinare le dimensioni dell&#39;array di byte ottenendo il `System.IO.FileStream` dell’oggetto `Length` proprietà.
   * Compilare l&#39;array di byte con i dati del flusso richiamando il `System.IO.FileStream` dell’oggetto `Read` e passare l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare `BLOB` assegnando il contenuto dell&#39;array di byte al `BLOB` dell’oggetto `MTOM` membro dati.

1. Rimuovi la password.

   Richiama il `EncryptionServiceService` dell’oggetto `removePDFPasswordSecurity` e passare i seguenti valori:

   * La `BLOB` oggetto che contiene dati di flusso di file che rappresentano un documento PDF crittografato.
   * Valore stringa che specifica il valore della password utilizzato per rimuovere la crittografia dal documento PDF. Questo valore viene specificato durante la cifratura del documento PDF con una password.

   La `removePDFPasswordSecurity` restituisce un `BLOB` oggetto contenente un documento PDF non protetto.

1. Salvare il documento PDF.

   * Crea un `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF non protetto.
   * Creare un array di byte che memorizza il contenuto del `BLOB` oggetto restituito da `removePDFPasswordSecurity` metodo . Compilare l’array di byte ottenendo il valore del `BLOB` dell’oggetto `MTOM` membro dati.
   * Crea un `System.IO.BinaryWriter` richiamando il relativo costruttore e passando `System.IO.FileStream` oggetto.
   * Scrivi il contenuto dell’array di byte in un file PDF richiamando il `System.IO.BinaryWriter` dell’oggetto `Write` e passare l&#39;array di byte.

**Consulta anche**

[Richiamo di AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamo di AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Sblocco dei documenti PDF crittografati {#unlocking-encrypted-pdf-documents}

È necessario sbloccare un documento PDF crittografato con password o certificato prima di eseguire un’altra operazione AEM Forms. Se si tenta di eseguire un&#39;operazione su un documento PDF crittografato, verrà generata un&#39;eccezione. Dopo aver sbloccato un documento PDF crittografato, è possibile eseguire una o più operazioni su di esso. Queste operazioni possono appartenere ad altri servizi, ad esempio il servizio Acrobat Reader DC extensions.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio di cifratura, vedi [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-4}

Per sbloccare un documento PDF crittografato, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Crea un client del servizio di crittografia.
1. Ottenere il documento PDF crittografato.
1. Sblocca il documento.
1. Esegui un’operazione AEM Forms.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso della classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è distribuito su JBoss Application Server)
* jbossall-client.jar (richiesto se AEM Forms è distribuito su JBoss Application Server)

**Creare un client del servizio di crittografia**

Per eseguire un&#39;operazione del servizio di cifratura a livello di programmazione, è necessario creare un client del servizio di cifratura. Se utilizzi l’API del servizio Java Encryption, crea un `EncrytionServiceClient` oggetto. Se utilizzi l’API del servizio Web Encryption Service, crea un `EncryptionServiceService` oggetto.

**Ottenere il documento PDF crittografato**

Per sbloccarlo, è necessario ottenere un documento PDF crittografato. Se si tenta di sbloccare un documento PDF non crittografato, viene generata un&#39;eccezione.

**Sblocca il documento**

Per sbloccare un documento PDF crittografato con password, è necessario disporre sia di un documento PDF crittografato sia di un valore di password utilizzato per aprire un documento PDF crittografato con password. Questo valore viene specificato durante la cifratura del documento PDF con una password. (Vedi [Crittografia dei documenti PDF con una password](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password).)

Per sbloccare un documento PDF crittografato tramite certificato, è necessario disporre sia di un documento PDF crittografato che del valore alias della chiave pubblica corrispondente alla chiave privata utilizzata per cifrare il documento PDF.

**Eseguire un’operazione AEM Forms**

Dopo lo sblocco di un documento PDF crittografato, è possibile eseguire un&#39;altra operazione del servizio, ad esempio l&#39;applicazione di diritti di utilizzo. Questa operazione appartiene al servizio Acrobat Reader DC Extensions.

**Consulta anche**

[Sblocca un documento PDF crittografato utilizzando l’API Java](encrypting-decrypting-pdf-documents.md#unlock-an-encrypted-pdf-document-using-the-java-api)

[Sblocca un documento PDF crittografato utilizzando l’API del servizio Web](encrypting-decrypting-pdf-documents.md#unlock-an-encrypted-pdf-document-using-the-web-service-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API del servizio di crittografia](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

### Sblocca un documento PDF crittografato utilizzando l’API Java {#unlock-an-encrypted-pdf-document-using-the-java-api}

Sblocca un documento PDF crittografato utilizzando l’API di cifratura (Java):

1. Includi file di progetto.

   Includi file JAR client, come adobe-encryption-client.jar, nel percorso di classe del progetto Java.

1. Crea un client del servizio di crittografia.

   * Crea un `ServiceClientFactory` oggetto contenente le proprietà di connessione.
   * Crea un `EncryptionServiceClient` utilizzando il relativo costruttore e passando `ServiceClientFactory` oggetto.

1. Ottenere il documento PDF crittografato.

   * Crea un `java.io.FileInputStream` oggetto che rappresenta il documento PDF crittografato utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del documento PDF crittografato.
   * Crea un `com.adobe.idp.Document` utilizzando il relativo costruttore e passando `java.io.FileInputStream` oggetto.

1. Sblocca il documento.

   Sblocca un documento PDF crittografato richiamando il `EncryptionServiceClient` dell’oggetto `unlockPDFUsingPassword` o `unlockPDFUsingCredential` metodo .

   Per sbloccare un documento PDF crittografato con una password, richiama `unlockPDFUsingPassword` e passare i seguenti valori:

   * A `com.adobe.idp.Document` oggetto contenente il documento PDF crittografato con password.
   * Valore stringa che specifica il valore della password utilizzato per aprire un documento PDF crittografato con password. Questo valore viene specificato durante la cifratura del documento PDF con una password.

   Per sbloccare un documento PDF crittografato con un certificato, richiama `unlockPDFUsingCredential` e passare i seguenti valori:

   * A `com.adobe.idp.Document` oggetto contenente il documento PDF crittografato con certificato.
   * Valore stringa che specifica il nome alias della chiave pubblica corrispondente alla chiave privata utilizzata per crittografare il documento PDF.

   La `unlockPDFUsingPassword` e `unlockPDFUsingCredential` entrambi i metodi restituiscono un `com.adobe.idp.Document` oggetto passato a un altro metodo Java di AEM Forms per eseguire un&#39;operazione.

1. Esegui un’operazione AEM Forms.

   Esegui un’operazione AEM Forms sul documento PDF sbloccato per soddisfare i requisiti aziendali. Ad esempio, se si desidera applicare diritti di utilizzo a un documento PDF sbloccato, passare il `com.adobe.idp.Document` oggetto restituito da `unlockPDFUsingPassword` o `unlockPDFUsingCredential` metodi `ReaderExtensionsServiceClient` dell’oggetto `applyUsageRights` metodo .

**Consulta anche**

[Riepilogo dei passaggi](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Avvio rapido (modalità SOAP): Sblocco di un documento PDF crittografato tramite API Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-unlocking-an-encrypted-pdf-document-using-the-java-api) (modalità SOAP)

[Applicazione dei diritti di utilizzo ai documenti PDF](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Sblocca un documento PDF crittografato utilizzando l’API del servizio Web {#unlock-an-encrypted-pdf-document-using-the-web-service-api}

Sblocca un documento PDF crittografato utilizzando l’API di cifratura (servizio Web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurati di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l’indirizzo IP del server che ospita AEM Forms.

1. Crea un client del servizio di crittografia.

   * Crea un `EncryptionServiceClient` utilizzando il relativo costruttore predefinito.
   * Crea un `EncryptionServiceClient.Endpoint.Address` utilizzando `System.ServiceModel.EndpointAddress` costruttore. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/EncryptionService?WSDL`.) Non è necessario utilizzare il `lc_version` attributo. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Crea un `System.ServiceModel.BasicHttpBinding` ottenendo il valore del `EncryptionServiceClient.Endpoint.Binding` campo . Imposta il valore restituito su `BasicHttpBinding`.
   * Imposta la `System.ServiceModel.BasicHttpBinding` dell’oggetto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegnare il nome utente del modulo di AEM al campo `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore della password corrispondente al campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Ottieni un documento PDF crittografato.

   * Crea un `BLOB` utilizzando il relativo costruttore.
   * Crea un `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF crittografato e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto del `System.IO.FileStream` oggetto. È possibile determinare le dimensioni dell&#39;array di byte ottenendo il `System.IO.FileStream` dell’oggetto `Length` proprietà.
   * Compilare l&#39;array di byte con i dati del flusso richiamando il `System.IO.FileStream` dell’oggetto `Read` e passare l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare `BLOB` assegnando il contenuto dell&#39;array di byte al `BLOB` dell’oggetto `MTOM` membro dati.

1. Sblocca il documento.

   Sblocca un documento PDF crittografato richiamando il `EncryptionServiceClient` dell’oggetto `unlockPDFUsingPassword` o `unlockPDFUsingCredential` metodo .

   Per sbloccare un documento PDF crittografato con una password, richiama `unlockPDFUsingPassword` e passare i seguenti valori:

   * A `BLOB` oggetto contenente il documento PDF crittografato con password.
   * Valore stringa che specifica il valore della password utilizzato per aprire un documento PDF crittografato con password. Questo valore viene specificato durante la cifratura del documento PDF con una password.

   Per sbloccare un documento PDF crittografato con un certificato, richiama `unlockPDFUsingCredential` e passare i seguenti valori:

   * A `BLOB` oggetto contenente il documento PDF crittografato con certificato.
   * Valore stringa che specifica il nome alias della chiave pubblica corrispondente alla chiave privata utilizzata per crittografare il documento PDf.

   La `unlockPDFUsingPassword` e `unlockPDFUsingCredential` entrambi i metodi restituiscono un `com.adobe.idp.Document` oggetto passato a un altro metodo AEM Forms per eseguire un&#39;operazione.

1. Esegui un’operazione AEM Forms.

   Esegui un’operazione AEM Forms sul documento PDF sbloccato per soddisfare i requisiti aziendali. Ad esempio, se si desidera applicare diritti di utilizzo al documento PDF sbloccato, passare il `BLOB` oggetto restituito da `unlockPDFUsingPassword` o `unlockPDFUsingCredential` metodi `ReaderExtensionsServiceClient` dell’oggetto `applyUsageRights` metodo .

**Consulta anche**

[Riepilogo dei passaggi](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Richiamo di AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamo di AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Determinazione del tipo di crittografia {#determining-encryption-type}

È possibile determinare programmaticamente il tipo di crittografia che protegge un documento PDF utilizzando l’API Java Encryption Service o il servizio Web Encryption Service API. A volte è necessario determinare in modo dinamico se un documento PDF è crittografato e, in tal caso, il tipo di crittografia. Ad esempio, è possibile determinare se un documento di PDF è protetto da crittografia basata su password o da criteri di Rights Management.

Un documento PDF può essere protetto dai seguenti tipi di cifratura:

* Crittografia basata su password
* Crittografia basata su certificato
* Criterio creato dal servizio Rights Management
* Un altro tipo di crittografia

>[!NOTE]
>
>Per ulteriori informazioni sul servizio di cifratura, vedi [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-5}

Per determinare il tipo di crittografia che protegge un documento PDF, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Crea un client del servizio di crittografia.
1. Ottenere il documento PDF crittografato.
1. Determina il tipo di crittografia.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso della classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è distribuito su JBoss Application Server)
* jbossall-client.jar (richiesto se AEM Forms è distribuito su JBoss Application Server)

**Creare un client di servizio**

Per eseguire un&#39;operazione del servizio di cifratura a livello di programmazione, è necessario creare un client del servizio di cifratura. Se utilizzi l’API del servizio Java Encryption, crea un `EncrytionServiceClient` oggetto. Se utilizzi l’API del servizio Web Encryption Service, crea un `EncryptionServiceService` oggetto.

**Ottenere il documento PDF crittografato**

È necessario ottenere un documento PDF per determinare il tipo di crittografia che lo protegge.

**Determinare il tipo di crittografia**

È possibile determinare il tipo di crittografia che protegge un documento PDF. Se il documento PDF non è protetto, il servizio di crittografia informa l&#39;utente che il documento PDF non è protetto.

**Consulta anche**

[Determinare il tipo di crittografia utilizzando l’API Java](encrypting-decrypting-pdf-documents.md#determine-the-encryption-type-using-the-java-api)

[Determinare il tipo di crittografia utilizzando l’API del servizio Web](encrypting-decrypting-pdf-documents.md#determine-the-encryption-type-using-the-web-service-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API del servizio di crittografia](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[Protezione dei documenti con i criteri](/help/forms/developing/protecting-documents-policies.md#protecting-documents-with-policies)

### Determinare il tipo di crittografia utilizzando l’API Java {#determine-the-encryption-type-using-the-java-api}

Determina il tipo di crittografia che protegge un documento PDF utilizzando l’API di cifratura (Java):

1. Includi file di progetto.

   Includi file JAR client, come adobe-encryption-client.jar, nel percorso di classe del progetto Java.

1. Crea un client di servizio.

   * Crea un `ServiceClientFactory` oggetto contenente le proprietà di connessione.
   * Crea un `EncryptionServiceClient` utilizzando il relativo costruttore e passando `ServiceClientFactory` oggetto.

1. Ottenere il documento PDF crittografato.

   * Crea un `java.io.FileInputStream` oggetto che rappresenta il documento PDF utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del documento PDF.
   * Crea un `com.adobe.idp.Document` utilizzando il relativo costruttore e passando `java.io.FileInputStream` oggetto.

1. Determina il tipo di crittografia.

   * Determina il tipo di crittografia richiamando il `EncryptionServiceClient` dell’oggetto `getPDFEncryption` e passare `com.adobe.idp.Document` oggetto contenente il documento PDF. Questo metodo restituisce un `EncryptionTypeResult` oggetto.
   * Richiama il `EncryptionTypeResult` dell’oggetto `getEncryptionType` metodo . Questo metodo restituisce un `EncryptionType` valore enum che specifica il tipo di crittografia. Ad esempio, se il documento PDF è protetto con crittografia basata su password, questo metodo restituisce `EncryptionType.PASSWORD`.

**Consulta anche**

[Riepilogo dei passaggi](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Avvio rapido (modalità SOAP): Determinazione del tipo di crittografia tramite l’API Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-determining-encryption-type-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Determinare il tipo di crittografia utilizzando l’API del servizio Web {#determine-the-encryption-type-using-the-web-service-api}

Determinare il tipo di crittografia che protegge un documento PDF utilizzando l’API di cifratura (servizio Web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurati di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l’indirizzo IP del server che ospita AEM Forms.

1. Crea un client di servizio.

   * Crea un `EncryptionServiceClient` utilizzando il relativo costruttore predefinito.
   * Crea un `EncryptionServiceClient.Endpoint.Address` utilizzando `System.ServiceModel.EndpointAddress` costruttore. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/EncryptionService?WSDL`.) Non è necessario utilizzare il `lc_version` attributo. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Crea un `System.ServiceModel.BasicHttpBinding` ottenendo il valore del `EncryptionServiceClient.Endpoint.Binding` campo . Imposta il valore restituito su `BasicHttpBinding`.
   * Imposta la `System.ServiceModel.BasicHttpBinding` dell’oggetto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegnare il nome utente del modulo di AEM al campo `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore della password corrispondente al campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Ottenere il documento PDF crittografato.

   * Crea un `BLOB` utilizzando il relativo costruttore.
   * Crea un `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF crittografato e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto del `System.IO.FileStream` oggetto. È possibile determinare le dimensioni dell&#39;array di byte ottenendo il `System.IO.FileStream` dell’oggetto `Length` proprietà.
   * Compilare l&#39;array di byte con i dati del flusso richiamando il `System.IO.FileStream` dell’oggetto `Read` e passare l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare `BLOB` assegnando il contenuto dell&#39;array di byte al `BLOB` dell’oggetto `MTOM` membro dati.

1. Determina il tipo di crittografia.

   * Richiama il `EncryptionServiceClient` dell’oggetto `getPDFEncryption` e passare il `BLOB` oggetto contenente il documento PDF. Questo metodo restituisce un `EncryptionTypeResult` oggetto.
   * Ottieni il valore del `EncryptionTypeResult` dell’oggetto `encryptionType` metodo data. Ad esempio, se il documento PDF è protetto con crittografia basata su password, il valore di questo membro dati è `EncryptionType.PASSWORD`.

**Consulta anche**

[Riepilogo dei passaggi](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Richiamo di AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamo di AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
