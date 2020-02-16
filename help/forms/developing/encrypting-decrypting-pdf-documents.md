---
title: Cifratura e decrittografia di documenti PDF
seo-title: Cifratura e decrittografia di documenti PDF
description: 'null'
seo-description: 'null'
uuid: 4e4e2716-c21f-4bfe-ae7a-7e91442414ef
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 5e4bda3a-5648-4c0f-b2f8-bdbebb88f537
translation-type: tm+mt
source-git-commit: 413af4ef9bc3652e05da78d622183bcf20a8bee7

---


# Cifratura e decrittografia di documenti PDF {#encrypting-and-decrypting-pdf-documents}

**Informazioni sul servizio di cifratura**

Il servizio di cifratura consente di cifrare e decrittografare i documenti. Quando un documento viene crittografato, il relativo contenuto diventa illeggibile. Un utente autorizzato può decifrare il documento per ottenere l&#39;accesso ai contenuti. Se un documento PDF è crittografato con una password, l&#39;utente deve specificare la password aperta per poter visualizzare il documento in Adobe Reader o Adobe Acrobat. Analogamente, se un documento PDF è crittografato con un certificato, l&#39;utente deve decrittografare il documento PDF con la chiave pubblica che corrisponde al certificato (chiave privata) utilizzato per cifrare il documento PDF.

Il servizio di cifratura consente di effettuare le seguenti operazioni:

* Crittografare un documento PDF con una password. (vedere [Cifratura di documenti PDF con una password](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)).
* Cifrare un documento PDF con un certificato. (vedere [Cifratura di documenti PDF con certificati](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates)).
* Rimuovere la cifratura basata su password da un documento PDF. (Vedere [Rimozione della crittografia](encrypting-decrypting-pdf-documents.md#removing-password-encryption)della password.)
* Rimuovere la cifratura basata su certificato da un documento PDF. (Vedere [Rimozione della cifratura](encrypting-decrypting-pdf-documents.md#removing-certificate-based-encryption)basata su certificato.)
* Sbloccare il documento PDF per eseguire altre operazioni di servizio. Ad esempio, dopo aver sbloccato un documento PDF con password, è possibile apporvi una firma digitale. (Vedere [Sblocco di documenti](encrypting-decrypting-pdf-documents.md#unlocking-encrypted-pdf-documents)PDF crittografati.)
* Determinare il tipo di cifratura di un documento PDF protetto. (Vedere [Determinazione del tipo](encrypting-decrypting-pdf-documents.md#determining-encryption-type)di cifratura.)

   ***Nota **: Per ulteriori informazioni sul servizio di cifratura, consultate[Servizi di riferimento per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).*

## Cifratura di documenti PDF con una password {#encrypting-pdf-documents-with-a-password}

Quando si esegue la cifratura di un documento PDF con una password, l&#39;utente deve specificare la password per aprire il documento PDF in Adobe Reader o Acrobat. Inoltre, prima di poter eseguire un&#39;altra operazione AEM Forms, ad esempio la firma digitale del documento PDF, è necessario sbloccare un documento PDF crittografato con password.

>[!NOTE]
>
>Se si carica un documento PDF crittografato nell&#39;archivio di AEM Forms, non sarà possibile decifrare il documento PDF ed estrarre il contenuto XDP. È consigliabile non crittografare un documento prima di caricarlo nell&#39;archivio di AEM Forms. (Vedere [Creazione di risorse](/help/forms/developing/aem-forms-repository.md#writing-resources)).

>[!NOTE]
>
> Per ulteriori informazioni sul servizio di cifratura, consultate [Servizi di riferimento per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary-of-steps}

Per cifrare un documento PDF con una password, procedere come segue:

1. Includere i file di progetto.
1. Creare un oggetto API client di cifratura.
1. Ottenere un documento PDF da cifrare.
1. Impostare le opzioni di esecuzione della crittografia.
1. Aggiungete la password.
1. Salvare il documento PDF crittografato come file PDF.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, accertatevi di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encry-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è distribuito su JBoss)
* jbossall-client.jar (richiesto se AEM Forms è distribuito su JBoss)

**Creare un oggetto API client di cifratura**

Per eseguire un&#39;operazione del servizio di cifratura a livello di programmazione, è necessario creare un client del servizio di cifratura.

**Ottenere un documento PDF da cifrare**

È necessario ottenere un documento PDF non crittografato per cifrare il documento con una password. Se si tenta di proteggere un documento PDF già crittografato, si crea un&#39;eccezione.

**Impostazione delle opzioni di esecuzione della crittografia**

Per cifrare un documento PDF con una password, è necessario specificare quattro valori, inclusi due valori di password. Il primo valore password viene utilizzato per cifrare il documento PDF e deve essere specificato all&#39;apertura del documento PDF. Per rimuovere la cifratura dal documento PDF viene utilizzato il secondo valore della password, denominato valore della password principale. I valori della password sono sensibili alle maiuscole e minuscole e questi due valori non possono essere identici.

È necessario specificare le risorse del documento PDF da cifrare. È possibile cifrare l’intero documento PDF, tutti gli elementi tranne i metadati del documento o solo gli allegati del documento. Se si cifrano solo gli allegati del documento, all&#39;utente viene richiesta una password quando tenta di accedere agli allegati del file.

Durante la cifratura di un documento PDF, è possibile specificare le autorizzazioni associate al documento protetto. Specificando le autorizzazioni, è possibile controllare le azioni consentite da un utente che apre un documento PDF crittografato con password. Ad esempio, per estrarre correttamente i dati del modulo, è necessario impostare le seguenti autorizzazioni:

* PASSWORD_EDIT_ADD
* PASSWORD_EDIT_MODIFY

>[!NOTE]
>
>Le autorizzazioni sono specificate come valori di `PasswordEncryptionPermission` enumerazione.

**Aggiungere la password**

Dopo aver recuperato un documento PDF non protetto e impostato i valori di esecuzione della cifratura, è possibile aggiungere una password al documento PDF.

**Salvare il documento PDF crittografato come file PDF**

È possibile salvare il documento PDF crittografato con password come file PDF.

**Consulta anche**

[Cifratura di un documento PDF tramite l&#39;API Java](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-using-the-java-api)

[Cifratura di un documento PDF tramite l&#39;API del servizio Web](encrypting-decrypting-pdf-documents.md#encrypting-a-pdf-document-using-the-web-service-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API Servizio crittografia](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[Cifratura di documenti PDF con certificati](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates)

### Cifratura di un documento PDF tramite l&#39;API Java {#encrypt-a-pdf-document-using-the-java-api}

Crittografare un documento PDF con una password utilizzando l&#39;API di cifratura (Java):

1. Includere i file di progetto.

   Includete file JAR client, ad esempio adobe-Encryption-client.jar, nel percorso di classe del progetto Java.

1. Creare un&#39;API client di cifratura.

   * Creare un `ServiceClientFactory` oggetto che contenga proprietà di connessione.
   * Creare un `EncryptionServiceClient` oggetto utilizzando il relativo costruttore e passando l&#39; `ServiceClientFactory` oggetto.

1. Ottenere un documento PDF da cifrare.

   * Creare un `java.io.FileInputStream` oggetto che rappresenta il documento PDF da cifrare utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del documento PDF.
   * Creare un `com.adobe.idp.Document` oggetto utilizzando il relativo costruttore e passando l&#39; `java.io.FileInputStream` oggetto.

1. Impostare le opzioni di esecuzione della crittografia.

   * Creare un `PasswordEncryptionOptionSpec` oggetto richiamandone il costruttore.
   * Specificare le risorse del documento PDF da cifrare richiamando il metodo dell&#39; `PasswordEncryptionOptionSpec` oggetto `setEncryptOption` e passando un valore di `PasswordEncryptionOption` enumerazione che specifica le risorse del documento da cifrare. Ad esempio, per cifrare l’intero documento PDF, inclusi i metadati e gli allegati, specificare `PasswordEncryptionOption.ALL`.
   * Creare un `java.util.List` oggetto che memorizza le autorizzazioni di cifratura utilizzando il `ArrayList` costruttore.
   * Specificate un&#39;autorizzazione richiamando il metodo `java.util.List` ‘s `add` dell&#39;oggetto e passando un valore di enumerazione che corrisponde all&#39;autorizzazione che desiderate impostare. Ad esempio, per impostare l&#39;autorizzazione che consente a un utente di copiare i dati presenti nel documento PDF, specificare `PasswordEncryptionPermission.PASSWORD_EDIT_COPY`. Ripetete questo passaggio per ogni autorizzazione da impostare.
   * Specificare l&#39;opzione di compatibilità Acrobat richiamando il metodo dell&#39; `PasswordEncryptionOptionSpec` oggetto `setCompatability` e passando un valore di enumerazione che specifica il livello di compatibilità di Acrobat. Ad esempio, potete specificare `PasswordEncryptionCompatability.ACRO_7`.
   * Specificare il valore della password che consente a un utente di aprire il documento PDF crittografato richiamando il metodo dell&#39; `PasswordEncryptionOptionSpec` `setDocumentOpenPassword` oggetto e passando un valore di stringa che rappresenta la password aperta.
   * Specificare il valore della password master che consente a un utente di rimuovere la cifratura dal documento PDF richiamando il metodo dell&#39; `PasswordEncryptionOptionSpec` oggetto `setPermissionPassword` e passando un valore di stringa che rappresenta la password master.

1. Aggiungete la password.

   Crittografare il documento PDF richiamando il metodo dell&#39; `EncryptionServiceClient` oggetto `encryptPDFUsingPassword` e passando i seguenti valori:

   * L&#39; `com.adobe.idp.Document` oggetto che contiene il documento PDF da cifrare con la password.
   * L&#39; `PasswordEncryptionOptionSpec` oggetto che contiene le opzioni di esecuzione della crittografia.
   Il `encryptPDFUsingPassword` metodo restituisce un `com.adobe.idp.Document` oggetto che contiene un documento PDF crittografato con password.

1. Salvare il documento PDF crittografato come file PDF.

   * Create un `java.io.File` oggetto e accertatevi che l&#39;estensione sia .pdf.
   * Richiamare il metodo dell&#39; `com.adobe.idp.Document` oggetto `copyToFile` per copiare il contenuto dell&#39; `com.adobe.idp.Document` oggetto nel file. Assicurarsi di utilizzare l&#39; `com.adobe.idp.Document` oggetto restituito dal `encryptPDFUsingPassword` metodo.

**Consulta anche**

[Riepilogo dei passaggi](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Avvio rapido (modalità SOAP): Cifratura di un documento PDF tramite l&#39;API Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-encrypting-a-pdf-document-using-the-java-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Cifratura di un documento PDF tramite l&#39;API del servizio Web {#encrypting-a-pdf-document-using-the-web-service-api}

Crittografare un documento PDF con una password utilizzando l&#39;API di cifratura (servizio Web):

1. Includere i file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituire `localhost` con l&#39;indirizzo IP del server in cui è installato AEM Forms.

1. Creare un oggetto API client di cifratura.

   * Creare un `EncryptionServiceClient` oggetto utilizzando il relativo costruttore predefinito.
   * Creare un `EncryptionServiceClient.Endpoint.Address` oggetto utilizzando il `System.ServiceModel.EndpointAddress` costruttore. Passa un valore di stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/EncryptionService?WSDL`.) Non è necessario utilizzare l&#39; `lc_version` attributo. Questo attributo viene utilizzato quando create un riferimento a un servizio.
   * Creare un `System.ServiceModel.BasicHttpBinding` oggetto ottenendo il valore del `EncryptionServiceClient.Endpoint.Binding` campo. Inserite il valore restituito in `BasicHttpBinding`.
   * Impostare il campo `System.ServiceModel.BasicHttpBinding` dell&#39; `MessageEncoding` oggetto su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilitate l&#39;autenticazione HTTP di base eseguendo le seguenti operazioni:

      * Assegnare il nome utente dei moduli AEM al campo `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Ottenere un documento PDF da cifrare.

   * Creare un `BLOB` oggetto utilizzando il relativo costruttore. L&#39; `BLOB` oggetto viene utilizzato per memorizzare un documento PDF cifrato con una password.
   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF da cifrare e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto dell&#39; `System.IO.FileStream` oggetto. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà dell&#39; `System.IO.FileStream` oggetto `Length` .
   * Compilare l&#39;array di byte con i dati del flusso richiamando il `System.IO.FileStream` `Read` metodo dell&#39;oggetto e passando l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39; `BLOB` oggetto assegnando il contenuto dell&#39;array di byte al membro `BLOB` dati dell&#39; `MTOM` oggetto.

1. Impostare le opzioni di esecuzione della crittografia.

   * Creare un `PasswordEncryptionOptionSpec` oggetto utilizzando il relativo costruttore.
   * Specificare le risorse del documento PDF da cifrare assegnando un valore di `PasswordEncryptionOption` enumerazione al membro `PasswordEncryptionOptionSpec` dati dell&#39; `encryptOption` oggetto. Per cifrare l’intero PDF, inclusi i metadati e gli allegati, assegnare `PasswordEncryptionOption.ALL` a tale membro dati.
   * Specificare l&#39;opzione di compatibilità Acrobat assegnando un valore di `PasswordEncryptionCompatability` enumerazione al membro dati dell&#39; `PasswordEncryptionOptionSpec` oggetto `compatability` . Ad esempio, assegna `PasswordEncryptionCompatability.ACRO_7` a questo membro dati.
   * Specificare il valore della password che consente all&#39;utente di aprire il documento PDF crittografato assegnando un valore di stringa che rappresenta la password aperta al membro `PasswordEncryptionOptionSpec` dati `documentOpenPassword` dell&#39;oggetto.
   * Specificare il valore della password che consente a un utente di rimuovere la cifratura dal documento PDF assegnando al membro dati dell&#39; `PasswordEncryptionOptionSpec` oggetto un valore di stringa che rappresenta la password master `permissionPassword` .

1. Aggiungete la password.

   Crittografare il documento PDF richiamando il metodo dell&#39; `EncryptionServiceClient` oggetto `encryptPDFUsingPassword` e passando i seguenti valori:

   * L&#39; `BLOB` oggetto che contiene il documento PDF da cifrare con la password.
   * L&#39; `PasswordEncryptionOptionSpec` oggetto che contiene le opzioni di esecuzione della crittografia.
   Il `encryptPDFUsingPassword` metodo restituisce un `BLOB` oggetto che contiene un documento PDF crittografato con password.

1. Salvare il documento PDF crittografato come file PDF.

   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF protetto.
   * Creare un array di byte che memorizza il contenuto dei dati dell&#39; `BLOB` oggetto restituito dal `encryptPDFUsingPassword` metodo. Compilare l&#39;array di byte ottenendo il valore del membro `BLOB` dati dell&#39; `MTOM` oggetto.
   * Creare un `System.IO.BinaryWriter` oggetto richiamando il relativo costruttore e passando l&#39; `System.IO.FileStream` oggetto.
   * Scrivere il contenuto dell&#39;array di byte in un file PDF richiamando il metodo dell&#39; `System.IO.BinaryWriter` oggetto `Write` e passando l&#39;array di byte.

**Consulta anche**

[Riepilogo dei passaggi](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Attivazione di moduli AEM tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamo di moduli AEM con SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Cifratura di documenti PDF con certificati {#encrypting-pdf-documents-with-certificates}

La cifratura basata su certificato consente di cifrare un documento per destinatari specifici mediante la tecnologia a chiave pubblica. A diversi destinatari possono essere assegnate diverse autorizzazioni per il documento. Molti aspetti della crittografia sono resi possibili dalla tecnologia a chiave pubblica. Un algoritmo viene utilizzato per generare due numeri grandi, noti come *chiavi*, con le seguenti proprietà:

* Una chiave viene utilizzata per cifrare un set di dati. Successivamente, solo l&#39;altra chiave può essere utilizzata per decrittografare i dati.
* È impossibile distinguere una chiave dall&#39;altra.

Una delle chiavi funge da chiave privata dell&#39;utente. È importante che solo l&#39;utente abbia accesso a questa chiave. L’altra chiave è la chiave pubblica dell’utente, che può essere condivisa con altri utenti.

Un certificato a chiave pubblica contiene la chiave pubblica di un utente e le informazioni di identificazione. Il formato X.509 viene utilizzato per memorizzare i certificati. I certificati sono generalmente rilasciati e firmati digitalmente da un&#39;autorità di certificazione (CA), che è un&#39;entità riconosciuta che fornisce una misura di affidabilità nella validità del certificato. I certificati hanno una data di scadenza, dopo la quale non sono più validi. Inoltre, gli elenchi di revoche di certificati (CRL) forniscono informazioni sui certificati revocati prima della data di scadenza. I CRL vengono pubblicati periodicamente dalle autorità di certificazione. Lo stato di revoca di un certificato può essere recuperato anche tramite il protocollo di stato del certificato online (OCSP) sulla rete.

>[!NOTE]
>
>Se si carica un documento PDF crittografato nell&#39;archivio di AEM Forms, non sarà possibile decifrare il documento PDF ed estrarre il contenuto XDP. È consigliabile non crittografare un documento prima di caricarlo nell&#39;archivio di AEM Forms. (Vedere [Creazione di risorse](/help/forms/developing/aem-forms-repository.md#writing-resources)).

>[!NOTE]
>
>Prima di poter cifrare un documento PDF con un certificato, è necessario assicurarsi di aggiungere il certificato ad AEM Forms. Un certificato viene aggiunto utilizzando la console di amministrazione o a livello di programmazione tramite l&#39;API di Trust Manager. (vedere [Importazione di credenziali tramite l&#39;API](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api)di Trust Manager).

>[!NOTE]
>
> Per ulteriori informazioni sul servizio di cifratura, consultate [Servizi di riferimento per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-1}

Per cifrare un documento PDF con un certificato, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un oggetto API client di cifratura.
1. Ottenere un documento PDF da cifrare.
1. Fate riferimento al certificato.
1. Impostare le opzioni di esecuzione della crittografia.
1. Creare un documento PDF cifrato da certificato.
1. Salvare il documento PDF crittografato come file PDF.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, accertatevi di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encry-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è distribuito sul server applicazioni JBoss)
* jbossall-client.jar (richiesto se AEM Forms è distribuito sul server applicazioni JBoss)

**Creare un oggetto API client di cifratura**

Per eseguire un&#39;operazione del servizio di cifratura a livello di programmazione, è necessario creare un client del servizio di cifratura. Se utilizzate l&#39;API Java Encryption Service, create un `EncrytionServiceClient` oggetto. Se utilizzate l&#39;API del servizio Web Encryption Service, create un `EncryptionServiceService` oggetto.

**Ottenere un documento PDF da cifrare**

Per eseguire la cifratura, è necessario ottenere un documento PDF non crittografato. Se si tenta di proteggere un documento PDF già crittografato, viene generata un&#39;eccezione.

**Riferimento al certificato**

Per cifrare un documento PDF con un certificato, fare riferimento a un certificato utilizzato per cifrare un documento PDF. Il certificato è un file .cer, .crt o .pem. Un file PKCS#12 viene utilizzato per memorizzare le chiavi private con i certificati corrispondenti.

Durante la cifratura di un documento PDF con un certificato, specificare le autorizzazioni associate al documento protetto. Specificando le autorizzazioni, è possibile controllare le azioni che un utente che apre un documento PDF crittografato con certificato può eseguire.

**Impostazione delle opzioni di esecuzione della crittografia**

Specificare le risorse del documento PDF da cifrare. È possibile cifrare l&#39;intero documento PDF, tutti gli elementi tranne i metadati del documento o solo gli allegati del documento.

**Creare un documento PDF crittografato con certificato**

Dopo aver recuperato un documento PDF non protetto, fatto riferimento al certificato e impostato le opzioni di esecuzione, è possibile creare un documento PDF crittografato con certificato. Una volta crittografato il documento PDF, è necessario disporre della chiave pubblica corrispondente per decrittografarlo.

**Salvare il documento PDF crittografato come file PDF**

È possibile salvare il documento PDF crittografato come file PDF.

**Consulta anche**

[Cifratura di un documento PDF con un certificato tramite l&#39;API Java](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-with-a-certificate-using-the-java-api)

[Cifratura di un documento PDF con un certificato tramite l&#39;API del servizio Web](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-with-a-certificate-using-the-web-service-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API Servizio crittografia](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[Cifratura di documenti PDF con una password](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Cifratura di un documento PDF con un certificato tramite l&#39;API Java {#encrypt-a-pdf-document-with-a-certificate-using-the-java-api}

Crittografare un documento PDF con un certificato utilizzando l&#39;API di cifratura (Java):

1. Includere i file di progetto.

   Includete file JAR client, ad esempio adobe-Encryption-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto API client di cifratura.

   * Creare un `ServiceClientFactory` oggetto che contenga proprietà di connessione.
   * Creare un `EncryptionServiceClient` oggetto utilizzando il relativo costruttore e passando l&#39; `ServiceClientFactory` oggetto.

1. Ottenere un documento PDF da cifrare.

   * Creare un `java.io.FileInputStream` oggetto che rappresenta il documento PDF da cifrare utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del documento PDF.
   * Creare un `com.adobe.idp.Document` oggetto utilizzando il relativo costruttore e passando l&#39; `java.io.FileInputStream` oggetto.

1. Fate riferimento al certificato.

   * Creare un `java.util.List` oggetto che memorizza le informazioni sulle autorizzazioni utilizzando il relativo costruttore.
   * Specificare l&#39;autorizzazione associata al documento crittografato richiamando il `java.util.List` metodo dell&#39;oggetto e passando un valore di `add` `CertificateEncryptionPermissions` enumerazione che rappresenta le autorizzazioni concesse all&#39;utente che apre il documento PDF protetto. Ad esempio, per specificare tutte le autorizzazioni, passate `CertificateEncryptionPermissions.PKI_ALL_PERM`.
   * Creare un `Recipient` oggetto utilizzando il relativo costruttore.
   * Creare un `java.io.FileInputStream` oggetto che rappresenta il certificato utilizzato per cifrare il documento PDF utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del certificato.
   * Creare un `com.adobe.idp.Document` oggetto utilizzando il relativo costruttore e passando l&#39; `java.io.FileInputStream` oggetto che rappresenta il certificato.
   * Richiamare il metodo dell&#39; `Recipient` oggetto `setX509Cert` e passare l&#39; `com.adobe.idp.Document` oggetto che contiene il certificato. Inoltre, l&#39; `Recipient`oggetto può avere un alias di certificato Truststore o un URL LDAP come origine di certificato.
   * Creare un oggetto `CertificateEncryptionIdentity` che memorizza le informazioni relative alle autorizzazioni e ai certificati utilizzando il relativo costruttore.
   * Richiamare il metodo dell&#39; `CertificateEncryptionIdentity` oggetto `setPerms` e passare l&#39; `java.util.List` oggetto che memorizza le informazioni sulle autorizzazioni.
   * Richiamare il metodo dell&#39; `CertificateEncryptionIdentity` oggetto `setRecipient` e passare l&#39; `Recipient` oggetto che memorizza le informazioni sul certificato.
   * Creare un `java.util.List` oggetto che memorizza le informazioni sul certificato utilizzando il relativo costruttore.
   * Richiamare il metodo add dell&#39; `java.util.List` oggetto e passare l&#39; `CertificateEncryptionIdentity` oggetto. (Questo `java.util.List` oggetto viene passato come parametro al `encryptPDFUsingCertificates` metodo.)

1. Impostare le opzioni di esecuzione della crittografia.

   * Creare un `CertificateEncryptionOptionSpec` oggetto richiamandone il costruttore.
   * Specificare le risorse del documento PDF da cifrare richiamando il metodo dell&#39; `CertificateEncryptionOptionSpec` oggetto `setOption` e passando un valore di `CertificateEncryptionOption` enumerazione che specifica le risorse del documento da cifrare. Ad esempio, per cifrare l’intero documento PDF, inclusi i metadati e gli allegati, specificare `CertificateEncryptionOption.ALL`.
   * Specificare l&#39;opzione di compatibilità Acrobat richiamando il metodo dell&#39; `CertificateEncryptionOptionSpec` oggetto `setCompat` e passando un valore di `CertificateEncryptionCompatibility` enumerazione che specifica il livello di compatibilità di Acrobat. Ad esempio, potete specificare `CertificateEncryptionCompatibility.ACRO_7`.

1. Creare un documento PDF cifrato da certificato.

   Cifrare il documento PDF con un certificato richiamando il metodo dell&#39; `EncryptionServiceClient` oggetto `encryptPDFUsingCertificates` e passando i seguenti valori:

   * L&#39; `com.adobe.idp.Document` oggetto che contiene il documento PDF da cifrare.
   * L&#39; `java.util.List` oggetto che memorizza le informazioni sul certificato.
   * L&#39; `CertificateEncryptionOptionSpec` oggetto che contiene le opzioni di esecuzione della crittografia.
   Il `encryptPDFUsingCertificates` metodo restituisce un `com.adobe.idp.Document` oggetto che contiene un documento PDF crittografato con certificato.

1. Salvare il documento PDF crittografato come file PDF.

   * Create un `java.io.File` oggetto e accertatevi che l&#39;estensione del nome del file sia .pdf.
   * Richiamare il metodo dell&#39; `com.adobe.idp.Document` oggetto `copyToFile` per copiare il contenuto dell&#39; `com.adobe.idp.Document` oggetto nel file. Assicurarsi di utilizzare l&#39; `com.adobe.idp.Document` oggetto restituito dal `encryptPDFUsingCertificates` metodo.

**Consulta anche**

[Riepilogo dei passaggi](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Avvio rapido (modalità SOAP): Cifratura di un documento PDF con un certificato tramite l&#39;API Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-encrypting-a-pdf-document-with-a-certificate-using-the-java-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Cifratura di un documento PDF con un certificato tramite l&#39;API del servizio Web {#encrypt-a-pdf-document-with-a-certificate-using-the-web-service-api}

Crittografare un documento PDF con un certificato utilizzando l&#39;API di cifratura (servizio Web):

1. Includere i file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituire `localhost` con l&#39;indirizzo IP del server in cui è installato AEM Forms.

1. Creare un oggetto API client di cifratura.

   * Creare un `EncryptionServiceClient` oggetto utilizzando il relativo costruttore predefinito.
   * Creare un `EncryptionServiceClient.Endpoint.Address` oggetto utilizzando il `System.ServiceModel.EndpointAddress` costruttore. Passa un valore di stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/EncryptionService?WSDL`.) Non è necessario utilizzare l&#39; `lc_version` attributo. Questo attributo viene utilizzato quando create un riferimento a un servizio.
   * Creare un `System.ServiceModel.BasicHttpBinding` oggetto ottenendo il valore del `EncryptionServiceClient.Endpoint.Binding` campo. Inserite il valore restituito in `BasicHttpBinding`.
   * Impostare il campo `System.ServiceModel.BasicHttpBinding` dell&#39; `MessageEncoding` oggetto su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilitate l&#39;autenticazione HTTP di base eseguendo le seguenti operazioni:

      * Assegnare il nome utente dei moduli AEM al campo `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Ottenere un documento PDF da cifrare.

   * Creare un `BLOB` oggetto utilizzando il relativo costruttore. L&#39; `BLOB` oggetto viene utilizzato per memorizzare un documento PDF cifrato con un certificato.
   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF da cifrare e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto dell&#39; `System.IO.FileStream` oggetto. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà dell&#39; `System.IO.FileStream` oggetto `Length` .
   * Compilare l&#39;array di byte con i dati del flusso richiamando il `System.IO.FileStream` `Read` metodo dell&#39;oggetto e passando l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39; `BLOB` oggetto assegnandone `MTOM` la proprietà con il contenuto dell&#39;array di byte.

1. Fate riferimento al certificato.

   * Creare un `Recipient` oggetto utilizzando il relativo costruttore. Questo oggetto memorizzerà le informazioni sul certificato.
   * Creare un `BLOB` oggetto utilizzando il relativo costruttore. Questo `BLOB` oggetto memorizzerà il certificato per la cifratura del documento PDF.
   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del certificato e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto dell&#39; `System.IO.FileStream` oggetto. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà dell&#39; `System.IO.FileStream` oggetto `Length` .
   * Compilare l&#39;array di byte con i dati del flusso richiamando il `System.IO.FileStream` `Read` metodo dell&#39;oggetto e passando l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39; `BLOB` oggetto assegnando il contenuto dell&#39;array di byte al membro `BLOB` dati dell&#39; `MTOM` oggetto.
   * Assegnare l&#39; `BLOB` oggetto che memorizza il certificato al membro `Recipient` dati dell&#39; `x509Cert` oggetto.
   * Creare un `CertificateEncryptionIdentity` oggetto che memorizza le informazioni sul certificato utilizzando il relativo costruttore.
   * Assegnare l&#39; `Recipient` oggetto che memorizza il certificato al membro dati del destinatario dell&#39; `CertificateEncryptionIdentity`oggetto.
   * Create un `Object` array e assegnate l&#39; `CertificateEncryptionIdentity` oggetto al primo elemento dell&#39; `Object` array. Questa `Object` matrice viene passata al `encryptPDFUsingCertificates` metodo come parametro.

1. Impostare le opzioni di esecuzione della crittografia.

   * Creare un `CertificateEncryptionOptionSpec` oggetto utilizzando il relativo costruttore.
   * Specificare le risorse del documento PDF da cifrare assegnando un valore di `CertificateEncryptionOption` enumerazione al membro `CertificateEncryptionOptionSpec` dati dell&#39; `option` oggetto. Per cifrare l&#39;intero documento PDF, inclusi i metadati e gli allegati, assegnare `CertificateEncryptionOption.ALL` a tale membro dati.
   * Specificare l&#39;opzione di compatibilità Acrobat assegnando un valore di `CertificateEncryptionCompatibility` enumerazione al membro dati dell&#39; `CertificateEncryptionOptionSpec` oggetto `compat` . Ad esempio, assegna `CertificateEncryptionCompatibility.ACRO_7` a questo membro dati.

1. Creare un documento PDF cifrato da certificato.

   Cifrare il documento PDF con un certificato richiamando il metodo dell&#39; `EncryptionServiceService` oggetto `encryptPDFUsingCertificates` e passando i seguenti valori:

   * L&#39; `BLOB` oggetto che contiene il documento PDF da cifrare.
   * L&#39; `Object` array che memorizza le informazioni sul certificato.
   * L&#39; `CertificateEncryptionOptionSpec` oggetto che contiene le opzioni di esecuzione della crittografia.
   Il `encryptPDFUsingCertificates` metodo restituisce un `BLOB` oggetto che contiene un documento PDF crittografato con certificato.

1. Salvare il documento PDF crittografato come file PDF.

   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF protetto.
   * Creare un array di byte che memorizza il contenuto dei dati dell&#39; `BLOB` oggetto restituito dal `encryptPDFUsingCertificates` metodo. Compilare l&#39;array di byte ottenendo il valore del membro `BLOB` dati dell&#39; `binaryData` oggetto.
   * Creare un `System.IO.BinaryWriter` oggetto richiamando il relativo costruttore e passando l&#39; `System.IO.FileStream` oggetto.
   * Scrivere il contenuto dell&#39;array di byte in un file PDF richiamando il metodo dell&#39; `System.IO.BinaryWriter` oggetto `Write` e passando l&#39;array di byte.

**Consulta anche**

[Riepilogo dei passaggi](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Attivazione di moduli AEM tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamo di moduli AEM con SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Rimozione della crittografia basata su certificato {#removing-certificate-based-encryption}

È possibile rimuovere la cifratura basata su certificato da un documento PDF per consentire agli utenti di aprire il documento PDF in Adobe Reader o Acrobat. Per rimuovere la cifratura da un documento PDF cifrato con un certificato, è necessario fare riferimento a una chiave pubblica. Una volta rimossa la cifratura da un documento PDF, questa non è più protetta.

>[!NOTE]
>
> Per ulteriori informazioni sul servizio di cifratura, consultate [Servizi di riferimento per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-2}

Per rimuovere la cifratura basata su certificato da un documento PDF, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un client del servizio di cifratura.
1. Ottenere il documento PDF crittografato.
1. Rimuovere la crittografia.
1. Salvare il documento PDF come file PDF.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, accertatevi di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encry-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è distribuito sul server applicazioni JBoss)
* jbossall-client.jar (richiesto se AEM Forms è distribuito sul server applicazioni JBoss)

**Creare un client del servizio di crittografia**

Per eseguire un&#39;operazione del servizio di cifratura a livello di programmazione, è necessario creare un client del servizio di cifratura. Se utilizzate l&#39;API Java Encryption Service, create un `EncrytionServiceClient` oggetto. Se utilizzate l&#39;API del servizio Web Encryption Service, create un `EncryptionServiceService` oggetto.

**Ottenere il documento PDF crittografato**

Per rimuovere la cifratura basata su certificato, è necessario ottenere un documento PDF crittografato. Se si tenta di rimuovere la cifratura da un documento PDF non crittografato, viene generata un&#39;eccezione. Analogamente, se tentate di rimuovere la cifratura basata su certificato da un documento crittografato con password, viene generata un&#39;eccezione.

**Rimuovi crittografia**

Per rimuovere la cifratura basata su certificato da un documento PDF cifrato, è necessario un documento PDF cifrato e la chiave privata corrispondente alla chiave utilizzata per cifrare il documento PDF. Il valore alias della chiave privata viene specificato quando si rimuove la cifratura basata su certificato da un documento PDF crittografato. Per informazioni sulla chiave pubblica, vedere [Cifratura di documenti PDF con certificati](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates).

>[!NOTE]
>
>Una chiave privata viene memorizzata nell&#39;archivio certificati attendibili di AEM Forms. Quando un certificato è posizionato in tale posizione, viene specificato un valore alias.

**Salvare il documento PDF**

Dopo aver rimosso la cifratura basata su certificato da un documento PDF cifrato, è possibile salvare il documento PDF come file PDF. Gli utenti possono aprire il documento PDF in Adobe Reader o Acrobat.

**Consulta anche**

[Rimozione della crittografia basata su certificato tramite l&#39;API Java](encrypting-decrypting-pdf-documents.md#remove-certificate-based-encryption-using-the-java-api)

[Rimozione della crittografia basata su certificato tramite l&#39;API del servizio Web](encrypting-decrypting-pdf-documents.md#remove-certificate-based-encryption-using-the-web-service-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API Servizio crittografia](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

### Rimozione della crittografia basata su certificato tramite l&#39;API Java {#remove-certificate-based-encryption-using-the-java-api}

Rimuovere la cifratura basata su certificato da un documento PDF utilizzando l&#39;API di cifratura (Java):

1. Includere i file di progetto.

   Includete file JAR client, ad esempio adobe-Encryption-client.jar, nel percorso di classe del progetto Java.

1. Creare un client del servizio di cifratura.

   * Creare un `ServiceClientFactory` oggetto che contenga proprietà di connessione.
   * Creare un `EncryptionServiceClient` oggetto utilizzando il relativo costruttore e passando l&#39; `ServiceClientFactory` oggetto.

1. Ottenere il documento PDF crittografato.

   * Creare un `java.io.FileInputStream` oggetto che rappresenta il documento PDF crittografato utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del documento PDF crittografato.
   * Creare un `com.adobe.idp.Document` oggetto utilizzando il relativo costruttore e passando l&#39; `java.io.FileInputStream` oggetto.

1. Rimuovere la crittografia.

   Rimuovere la cifratura basata su certificato dal documento PDF richiamando il metodo dell&#39; `EncryptionServiceClient` oggetto `removePDFCertificateSecurity` e passando i seguenti valori:

   * L&#39; `com.adobe.idp.Document` oggetto che contiene il documento PDF crittografato.
   * Un valore di stringa che specifica il nome alias della chiave privata che corrisponde alla chiave utilizzata per cifrare il documento PDF.
   Il `removePDFCertificateSecurity` metodo restituisce un `com.adobe.idp.Document` oggetto contenente un documento PDF non protetto.

1. Salvare il documento PDF.

   * Create un `java.io.File` oggetto e accertatevi che l&#39;estensione sia .pdf.
   * Richiamare il metodo dell&#39; `com.adobe.idp.Document` oggetto `copyToFile` per copiare il contenuto dell&#39; `Document` oggetto nel file. Assicurarsi di utilizzare l&#39; `com.adobe.idp.Document` oggetto restituito dal `removePDFCredentialSecurity` metodo.

**Consulta anche**

[Riepilogo dei passaggi](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Avvio rapido (modalità SOAP): Rimozione della crittografia basata su certificato tramite l&#39;API Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-removing-certificate-based-encryption-using-the-java-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Rimozione della crittografia basata su certificato tramite l&#39;API del servizio Web {#remove-certificate-based-encryption-using-the-web-service-api}

Rimuovete la cifratura basata su certificato utilizzando l&#39;API di cifratura (servizio Web):

1. Includere i file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituire `localhost` con l&#39;indirizzo IP del server in cui è installato AEM Forms.

1. Creare un client del servizio di cifratura.

   * Creare un `EncryptionServiceClient` oggetto utilizzando il relativo costruttore predefinito.
   * Creare un `EncryptionServiceClient.Endpoint.Address` oggetto utilizzando il `System.ServiceModel.EndpointAddress` costruttore. Passa un valore di stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/EncryptionService?WSDL`.) Non è necessario utilizzare l&#39; `lc_version` attributo. Questo attributo viene utilizzato quando create un riferimento a un servizio.
   * Creare un `System.ServiceModel.BasicHttpBinding` oggetto ottenendo il valore del `EncryptionServiceClient.Endpoint.Binding` campo. Inserite il valore restituito in `BasicHttpBinding`.
   * Impostare il campo `System.ServiceModel.BasicHttpBinding` dell&#39; `MessageEncoding` oggetto su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilitate l&#39;autenticazione HTTP di base eseguendo le seguenti operazioni:

      * Assegnare il nome utente dei moduli AEM al campo `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Ottenere il documento PDF crittografato.

   * Creare un `BLOB` oggetto utilizzando il relativo costruttore. L&#39; `BLOB` oggetto viene utilizzato per memorizzare il documento PDF crittografato.
   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF crittografato e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto dell&#39; `System.IO.FileStream` oggetto. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà dell&#39; `System.IO.FileStream` oggetto `Length` .
   * Compilare l&#39;array di byte con i dati del flusso richiamando il `System.IO.FileStream` `Read` metodo dell&#39;oggetto e passando l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39; `BLOB` oggetto assegnando il contenuto dell&#39;array di byte al membro `BLOB` dati dell&#39; `MTOM` oggetto.

1. Rimuovere la crittografia.

   Richiama il metodo dell’ `EncryptionServiceClient` oggetto `removePDFCertificateSecurity` e passa i seguenti valori:

   * L&#39; `BLOB` oggetto che contiene i dati del flusso di file che rappresenta un documento PDF crittografato.
   * Un valore di stringa che specifica il nome alias della chiave pubblica corrispondente alla chiave privata utilizzata per cifrare il documento PDF.
   Il `removePDFCredentialSecurity` metodo restituisce un `BLOB` oggetto contenente un documento PDF non protetto.

1. Salvare il documento PDF.

   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF non protetto.
   * Creare un array di byte che memorizza il contenuto dell&#39; `BLOB` oggetto restituito dal `removePDFPasswordSecurity` metodo. Compilare l&#39;array di byte ottenendo il valore del membro `BLOB` dati dell&#39; `MTOM` oggetto.
   * Creare un `System.IO.BinaryWriter` oggetto richiamando il relativo costruttore e passando l&#39; `System.IO.FileStream` oggetto.
   * Scrivere il contenuto dell&#39;array di byte in un file PDF richiamando il metodo dell&#39; `System.IO.BinaryWriter` oggetto `Write` e passando l&#39;array di byte.

**Consulta anche**

[Riepilogo dei passaggi](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Attivazione di moduli AEM tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamo di moduli AEM con SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Rimozione crittografia password {#removing-password-encryption}

La cifratura basata su password può essere rimossa da un documento PDF per consentire agli utenti di aprire il documento PDF in Adobe Reader o Acrobat senza dover specificare una password. Una volta rimossa la cifratura basata su password da un documento PDF, il documento non è più protetto.

>[!NOTE]
>
> Per ulteriori informazioni sul servizio di cifratura, consultate [Servizi di riferimento per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-3}

Per rimuovere la cifratura basata su password da un documento PDF, effettuare le seguenti operazioni:

1. Includi file di progetto
1. Creare un client del servizio di cifratura.
1. Ottenere il documento PDF crittografato.
1. Rimuovere la password.
1. Salvare il documento PDF come file PDF.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate servizi Web, accertatevi di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encry-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è distribuito su JBoss)
* jbossall-client.jar (richiesto se AEM Forms è distribuito su JBoss)

**Creare un client del servizio di crittografia**

Per eseguire un&#39;operazione del servizio di cifratura a livello di programmazione, è necessario creare un client del servizio di cifratura. Se utilizzate l&#39;API Java Encryption Service, create un `EncrytionServiceClient` oggetto. Se utilizzate l&#39;API del servizio Web Encryption Service, create un `EncryptionServiceService` oggetto.

**Ottenere il documento PDF crittografato**

È necessario ottenere un documento PDF crittografato per rimuovere la cifratura basata su password. Se si tenta di rimuovere la cifratura da un documento PDF non crittografato, viene generata un&#39;eccezione.

**Rimuovere la password**

Per rimuovere la cifratura basata su password da un documento PDF cifrato, è necessario un documento PDF cifrato e un valore della password master utilizzato per rimuovere la cifratura dal documento PDF. La password utilizzata per aprire un documento PDF crittografato con password non può essere utilizzata per rimuovere la cifratura. Una password master è specificata quando il documento PDF è crittografato con una password. (vedere [Cifratura di documenti PDF con una password](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)).

**Salvare il documento PDF**

Dopo che il servizio di cifratura ha rimosso la cifratura basata su password da un documento PDF, è possibile salvare il documento PDF come file PDF. Gli utenti possono aprire il documento PDF in Adobe Reader o Acrobat senza specificare una password.

**Consulta anche**

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API Servizio crittografia](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[Cifratura di documenti PDF con una password](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Rimozione della crittografia basata su password tramite l&#39;API Java {#remove-password-based-encryption-using-the-java-api}

Rimuovere la cifratura basata su password da un documento PDF utilizzando l&#39;API di cifratura (Java):

1. Includere i file di progetto.

   Includete file JAR client, ad esempio adobe-Encryption-client.jar, nel percorso di classe del progetto Java.

1. Creare un client del servizio di cifratura.

   * Creare un `ServiceClientFactory` oggetto che contenga proprietà di connessione.
   * Creare un `EncryptionServiceClient` oggetto utilizzando il relativo costruttore e passando l&#39; `ServiceClientFactory` oggetto.

1. Ottenere il documento PDF crittografato.

   * Creare un oggetto `java.io.FileInputStream` che rappresenti il documento PDF crittografato utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del documento PDF.
   * Creare un `com.adobe.idp.Document` oggetto utilizzando il relativo costruttore e passando l&#39; `java.io.FileInputStream` oggetto.

1. Rimuovere la password.

   Rimuovere la cifratura basata su password dal documento PDF richiamando il metodo dell&#39; `EncryptionServiceClient` oggetto `removePDFPasswordSecurity` e passando i seguenti valori:

   * Un `com.adobe.idp.Document` oggetto che contiene il documento PDF crittografato.
   * Valore stringa che specifica il valore della password master utilizzato per rimuovere la cifratura dal documento PDF.
   Il `removePDFPasswordSecurity` metodo restituisce un `com.adobe.idp.Document` oggetto contenente un documento PDF non protetto.

1. Salvare il documento PDF.

   * Create un `java.io.File` oggetto e accertatevi che l&#39;estensione del nome del file sia .pdf.
   * Richiamare il metodo dell&#39; `com.adobe.idp.Document` oggetto `copyToFile` per copiare il contenuto dell&#39; `Document` oggetto nel file. Assicurarsi di utilizzare l&#39; `Document` oggetto restituito dal `removePDFPasswordSecurity` metodo.

**Consulta anche**

[Avvio rapido (modalità SOAP): Rimozione della crittografia basata su password tramite l&#39;API Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-removing-password-based-encryption-using-the-java-api)

### Rimozione della crittografia basata su password tramite l&#39;API del servizio Web {#remove-password-based-encryption-using-the-web-service-api}

Rimuovere la cifratura basata su password utilizzando l&#39;API di cifratura (servizio Web):

1. Includere i file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituire `localhost` con l&#39;indirizzo IP del server in cui è installato AEM Forms.

1. Creare un client del servizio di cifratura.

   * Creare un `EncryptionServiceClient` oggetto utilizzando il relativo costruttore predefinito.
   * Creare un `EncryptionServiceClient.Endpoint.Address` oggetto utilizzando il `System.ServiceModel.EndpointAddress` costruttore. Passa un valore di stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/EncryptionService?WSDL`.) Non è necessario utilizzare l&#39; `lc_version` attributo. Questo attributo viene utilizzato quando create un riferimento a un servizio.
   * Creare un `System.ServiceModel.BasicHttpBinding` oggetto ottenendo il valore del `EncryptionServiceClient.Endpoint.Binding` campo. Inserite il valore restituito in `BasicHttpBinding`.
   * Impostare il campo `System.ServiceModel.BasicHttpBinding` dell&#39; `MessageEncoding` oggetto su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilitate l&#39;autenticazione HTTP di base eseguendo le seguenti operazioni:

      * Assegnare il nome utente dei moduli AEM al campo `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Ottenere il documento PDF crittografato.

   * Creare un `BLOB` oggetto utilizzando il relativo costruttore. L&#39; `BLOB` oggetto viene utilizzato per memorizzare un documento PDF crittografato con password.
   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF crittografato e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto dell&#39; `System.IO.FileStream` oggetto. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà dell&#39; `System.IO.FileStream` oggetto `Length` .
   * Compilare l&#39;array di byte con i dati del flusso richiamando il `System.IO.FileStream` `Read` metodo dell&#39;oggetto e passando l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39; `BLOB` oggetto assegnando il contenuto dell&#39;array di byte al membro `BLOB` dati dell&#39; `MTOM` oggetto.

1. Rimuovere la password.

   Richiama il metodo dell’ `EncryptionServiceService` oggetto `removePDFPasswordSecurity` e passa i seguenti valori:

   * L&#39; `BLOB` oggetto che contiene i dati del flusso di file che rappresenta un documento PDF crittografato.
   * Valore stringa che specifica il valore della password utilizzato per rimuovere la cifratura dal documento PDF. Questo valore viene specificato durante la cifratura del documento PDF con una password.
   Il `removePDFPasswordSecurity` metodo restituisce un `BLOB` oggetto contenente un documento PDF non protetto.

1. Salvare il documento PDF.

   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF non protetto.
   * Creare un array di byte che memorizza il contenuto dell&#39; `BLOB` oggetto restituito dal `removePDFPasswordSecurity` metodo. Compilare l&#39;array di byte ottenendo il valore del membro `BLOB` dati dell&#39; `MTOM` oggetto.
   * Creare un `System.IO.BinaryWriter` oggetto richiamando il relativo costruttore e passando l&#39; `System.IO.FileStream` oggetto.
   * Scrivere il contenuto dell&#39;array di byte in un file PDF richiamando il metodo dell&#39; `System.IO.BinaryWriter` oggetto `Write` e passando l&#39;array di byte.

**Consulta anche**

[Attivazione di moduli AEM tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamo di moduli AEM con SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Sblocco di documenti PDF crittografati {#unlocking-encrypted-pdf-documents}

Per poter eseguire un&#39;altra operazione AEM Forms, è necessario sbloccare un documento PDF crittografato con password o con certificato. Se si tenta di eseguire un&#39;operazione su un documento PDF crittografato, verrà generata un&#39;eccezione. Dopo aver sbloccato un documento PDF crittografato, è possibile eseguire una o più operazioni su di esso. Queste operazioni possono appartenere ad altri servizi, ad esempio Acrobat Reader DC Extensions Service.

>[!NOTE]
>
> Per ulteriori informazioni sul servizio di cifratura, consultate [Servizi di riferimento per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-4}

Per sbloccare un documento PDF crittografato, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un client del servizio di cifratura.
1. Ottenere il documento PDF crittografato.
1. Sblocca il documento.
1. Eseguire un&#39;operazione AEM Forms.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate servizi Web, accertatevi di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encry-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è distribuito sul server applicazioni JBoss)
* jbossall-client.jar (richiesto se AEM Forms è distribuito sul server applicazioni JBoss)

**Creare un client del servizio di crittografia**

Per eseguire un&#39;operazione del servizio di cifratura a livello di programmazione, è necessario creare un client del servizio di cifratura. Se utilizzate l&#39;API Java Encryption Service, create un `EncrytionServiceClient` oggetto. Se utilizzate l&#39;API del servizio Web Encryption Service, create un `EncryptionServiceService` oggetto.

**Ottenere il documento PDF crittografato**

Per sbloccare un documento PDF crittografato è necessario ottenerlo. Se si tenta di sbloccare un documento PDF non crittografato, viene generata un&#39;eccezione.

**Sblocca documento**

Per sbloccare un documento PDF crittografato con password, è necessario un documento PDF crittografato e un valore di password utilizzato per aprire un documento PDF crittografato con password. Questo valore viene specificato durante la cifratura del documento PDF con una password. (vedere [Cifratura di documenti PDF con una password](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)).

Per sbloccare un documento PDF crittografato con certificato, è necessario un documento PDF crittografato e il valore alias della chiave pubblica che corrisponde alla chiave privata utilizzata per cifrare il documento PDF.

**Esecuzione di un&#39;operazione AEM Forms**

Dopo aver sbloccato un documento PDF crittografato, è possibile eseguire un&#39;altra operazione del servizio, ad esempio l&#39;applicazione dei diritti di utilizzo. Questa operazione appartiene al servizio Acrobat Reader DC Extensions.

**Consulta anche**

[Sbloccare un documento PDF crittografato mediante l&#39;API Java](encrypting-decrypting-pdf-documents.md#unlock-an-encrypted-pdf-document-using-the-java-api)

[Sblocco di un documento PDF crittografato tramite l&#39;API del servizio Web](encrypting-decrypting-pdf-documents.md#unlock-an-encrypted-pdf-document-using-the-web-service-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API Servizio crittografia](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

### Sbloccare un documento PDF crittografato mediante l&#39;API Java {#unlock-an-encrypted-pdf-document-using-the-java-api}

Sbloccare un documento PDF crittografato utilizzando l&#39;API di cifratura (Java):

1. Includere i file di progetto.

   Includete file JAR client, ad esempio adobe-Encryption-client.jar, nel percorso di classe del progetto Java.

1. Creare un client del servizio di cifratura.

   * Creare un `ServiceClientFactory` oggetto che contenga proprietà di connessione.
   * Creare un `EncryptionServiceClient` oggetto utilizzando il relativo costruttore e passando l&#39; `ServiceClientFactory` oggetto.

1. Ottenere il documento PDF crittografato.

   * Creare un `java.io.FileInputStream` oggetto che rappresenta il documento PDF crittografato utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del documento PDF crittografato.
   * Creare un `com.adobe.idp.Document` oggetto utilizzando il relativo costruttore e passando l&#39; `java.io.FileInputStream` oggetto.

1. Sblocca il documento.

   Sbloccare un documento PDF crittografato richiamando il `EncryptionServiceClient` metodo `unlockPDFUsingPassword` o l&#39;oggetto `unlockPDFUsingCredential` .

   Per sbloccare un documento PDF cifrato con una password, richiamare il `unlockPDFUsingPassword` metodo e passare i seguenti valori:

   * Un `com.adobe.idp.Document` oggetto che contiene il documento PDF crittografato con password.
   * Valore stringa che specifica il valore della password utilizzata per aprire un documento PDF crittografato con password. Questo valore viene specificato durante la cifratura del documento PDF con una password.
   Per sbloccare un documento PDF cifrato con un certificato, richiamare il `unlockPDFUsingCredential` metodo e passare i seguenti valori:

   * Un `com.adobe.idp.Document` oggetto che contiene il documento PDF crittografato con certificato.
   * Una stringa che specifica il nome alias della chiave pubblica corrispondente alla chiave privata utilizzata per cifrare il documento PDF.
   Entrambi i metodi `unlockPDFUsingPassword` e `unlockPDFUsingCredential` restituiscono un `com.adobe.idp.Document` oggetto passato a un altro metodo Java AEM Forms per eseguire un’operazione.

1. Eseguire un&#39;operazione AEM Forms.

   Eseguite un&#39;operazione AEM Forms sul documento PDF sbloccato per soddisfare i requisiti aziendali. Ad esempio, se si desidera applicare diritti di utilizzo a un documento PDF non bloccato, passare l&#39; `com.adobe.idp.Document` oggetto restituito dai `unlockPDFUsingPassword` metodi o `unlockPDFUsingCredential` al `ReaderExtensionsServiceClient` metodo dell&#39; `applyUsageRights` oggetto.

**Consulta anche**

[Riepilogo dei passaggi](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Avvio rapido (modalità SOAP): Sblocco di un documento PDF crittografato tramite l&#39;API](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-unlocking-an-encrypted-pdf-document-using-the-java-api) Java (modalità SOAP)

[Applicazione dei diritti di utilizzo ai documenti PDF](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Sblocco di un documento PDF crittografato tramite l&#39;API del servizio Web {#unlock-an-encrypted-pdf-document-using-the-web-service-api}

Sbloccare un documento PDF crittografato utilizzando l&#39;API di cifratura (servizio Web):

1. Includere i file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituire `localhost` con l&#39;indirizzo IP del server in cui è installato AEM Forms.

1. Creare un client del servizio di cifratura.

   * Creare un `EncryptionServiceClient` oggetto utilizzando il relativo costruttore predefinito.
   * Creare un `EncryptionServiceClient.Endpoint.Address` oggetto utilizzando il `System.ServiceModel.EndpointAddress` costruttore. Passa un valore di stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/EncryptionService?WSDL`.) Non è necessario utilizzare l&#39; `lc_version` attributo. Questo attributo viene utilizzato quando create un riferimento a un servizio.
   * Creare un `System.ServiceModel.BasicHttpBinding` oggetto ottenendo il valore del `EncryptionServiceClient.Endpoint.Binding` campo. Inserite il valore restituito in `BasicHttpBinding`.
   * Impostare il campo `System.ServiceModel.BasicHttpBinding` dell&#39; `MessageEncoding` oggetto su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilitate l&#39;autenticazione HTTP di base eseguendo le seguenti operazioni:

      * Assegnare il nome utente dei moduli AEM al campo `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Ottenere un documento PDF crittografato.

   * Creare un `BLOB` oggetto utilizzando il relativo costruttore.
   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF crittografato e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto dell&#39; `System.IO.FileStream` oggetto. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà dell&#39; `System.IO.FileStream` oggetto `Length` .
   * Compilare l&#39;array di byte con i dati del flusso richiamando il `System.IO.FileStream` `Read` metodo dell&#39;oggetto e passando l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39; `BLOB` oggetto assegnando il contenuto dell&#39;array di byte al membro `BLOB` dati dell&#39; `MTOM` oggetto.

1. Sblocca il documento.

   Sbloccare un documento PDF crittografato richiamando il `EncryptionServiceClient` metodo `unlockPDFUsingPassword` o l&#39;oggetto `unlockPDFUsingCredential` .

   Per sbloccare un documento PDF cifrato con una password, richiamare il `unlockPDFUsingPassword` metodo e passare i seguenti valori:

   * Un `BLOB` oggetto che contiene il documento PDF crittografato con password.
   * Valore stringa che specifica il valore della password utilizzata per aprire un documento PDF crittografato con password. Questo valore viene specificato durante la cifratura del documento PDF con una password.
   Per sbloccare un documento PDF cifrato con un certificato, richiamare il `unlockPDFUsingCredential` metodo e passare i seguenti valori:

   * Un `BLOB` oggetto che contiene il documento PDF crittografato con certificato.
   * Un valore di stringa che specifica il nome alias della chiave pubblica corrispondente alla chiave privata utilizzata per cifrare il documento PDF.
   Entrambi i metodi `unlockPDFUsingPassword` e `unlockPDFUsingCredential` restituiscono un `com.adobe.idp.Document` oggetto passato a un altro metodo AEM Forms per eseguire un’operazione.

1. Eseguire un&#39;operazione AEM Forms.

   Eseguite un&#39;operazione AEM Forms sul documento PDF sbloccato per soddisfare i requisiti aziendali. Ad esempio, se si desidera applicare diritti di utilizzo al documento PDF non bloccato, passare l&#39; `BLOB` oggetto restituito dai `unlockPDFUsingPassword` metodi o `unlockPDFUsingCredential` al `ReaderExtensionsServiceClient` metodo dell&#39; `applyUsageRights` oggetto.

**Consulta anche**

[Riepilogo dei passaggi](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Attivazione di moduli AEM tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamo di moduli AEM con SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Determinazione del tipo di cifratura {#determining-encryption-type}

È possibile determinare a livello di programmazione il tipo di cifratura che protegge un documento PDF utilizzando l&#39;API Java Encryption Service o l&#39;API del servizio Web Encryption Service. A volte è necessario determinare in modo dinamico se un documento PDF è crittografato e, in tal caso, il tipo di cifratura. Ad esempio, potete stabilire se un documento PDF è protetto tramite cifratura basata su password o criteri Rights Management.

Un documento PDF può essere protetto tramite i seguenti tipi di cifratura:

* Cifratura basata su password
* Cifratura basata su certificato
* Criterio creato dal servizio Rights Management
* Un altro tipo di crittografia

>[!NOTE]
>
> Per ulteriori informazioni sul servizio di cifratura, consultate [Servizi di riferimento per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-5}

Per determinare il tipo di cifratura che protegge un documento PDF, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un client del servizio di cifratura.
1. Ottenere il documento PDF crittografato.
1. Determinare il tipo di crittografia.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, accertatevi di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encry-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è distribuito sul server applicazioni JBoss)
* jbossall-client.jar (richiesto se AEM Forms è distribuito sul server applicazioni JBoss)

**Creare un client di servizio**

Per eseguire un&#39;operazione del servizio di cifratura a livello di programmazione, è necessario creare un client del servizio di cifratura. Se utilizzate l&#39;API Java Encryption Service, create un `EncrytionServiceClient` oggetto. Se utilizzate l&#39;API del servizio Web Encryption Service, create un `EncryptionServiceService` oggetto.

**Ottenere il documento PDF crittografato**

È necessario ottenere un documento PDF per determinare il tipo di cifratura che lo protegge.

**Determinare il tipo di crittografia**

È possibile determinare il tipo di cifratura che protegge un documento PDF. Se il documento PDF non è protetto, il servizio di cifratura vi informerà che il documento PDF non è protetto.

**Consulta anche**

[Determinare il tipo di crittografia utilizzando l&#39;API Java](encrypting-decrypting-pdf-documents.md#determine-the-encryption-type-using-the-java-api)

[Determinare il tipo di crittografia utilizzando l&#39;API del servizio Web](encrypting-decrypting-pdf-documents.md#determine-the-encryption-type-using-the-web-service-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API Servizio crittografia](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[Protezione dei documenti con i criteri](/help/forms/developing/protecting-documents-policies.md#protecting-documents-with-policies)

### Determinare il tipo di crittografia utilizzando l&#39;API Java {#determine-the-encryption-type-using-the-java-api}

Determinare il tipo di cifratura che protegge un documento PDF utilizzando l&#39;API di cifratura (Java):

1. Includere i file di progetto.

   Includete file JAR client, ad esempio adobe-Encryption-client.jar, nel percorso di classe del progetto Java.

1. Creare un client di servizi.

   * Creare un `ServiceClientFactory` oggetto che contenga proprietà di connessione.
   * Creare un `EncryptionServiceClient` oggetto utilizzando il relativo costruttore e passando l&#39; `ServiceClientFactory` oggetto.

1. Ottenere il documento PDF crittografato.

   * Creare un oggetto `java.io.FileInputStream` che rappresenti il documento PDF utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del documento PDF.
   * Creare un `com.adobe.idp.Document` oggetto utilizzando il relativo costruttore e passando l&#39; `java.io.FileInputStream` oggetto.

1. Determinare il tipo di crittografia.

   * Determinare il tipo di cifratura richiamando il metodo dell&#39; `EncryptionServiceClient` oggetto `getPDFEncryption` e passando l&#39; `com.adobe.idp.Document` oggetto che contiene il documento PDF. Questo metodo restituisce un `EncryptionTypeResult` oggetto.
   * Richiama il metodo dell’ `EncryptionTypeResult` oggetto `getEncryptionType` . Questo metodo restituisce un valore `EncryptionType` enum che specifica il tipo di crittografia. Ad esempio, se il documento PDF è protetto tramite crittografia basata su password, questo metodo restituisce `EncryptionType.PASSWORD`.

**Consulta anche**

[Riepilogo dei passaggi](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Avvio rapido (modalità SOAP): Determinazione del tipo di crittografia tramite l&#39;API Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-determining-encryption-type-using-the-java-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Determinare il tipo di crittografia utilizzando l&#39;API del servizio Web {#determine-the-encryption-type-using-the-web-service-api}

Determinare il tipo di cifratura che protegge un documento PDF utilizzando l&#39;API di cifratura (servizio Web):

1. Includere i file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituire `localhost` con l&#39;indirizzo IP del server in cui è installato AEM Forms.

1. Creare un client di servizi.

   * Creare un `EncryptionServiceClient` oggetto utilizzando il relativo costruttore predefinito.
   * Creare un `EncryptionServiceClient.Endpoint.Address` oggetto utilizzando il `System.ServiceModel.EndpointAddress` costruttore. Passa un valore di stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/EncryptionService?WSDL`.) Non è necessario utilizzare l&#39; `lc_version` attributo. Questo attributo viene utilizzato quando create un riferimento a un servizio.
   * Creare un `System.ServiceModel.BasicHttpBinding` oggetto ottenendo il valore del `EncryptionServiceClient.Endpoint.Binding` campo. Inserite il valore restituito in `BasicHttpBinding`.
   * Impostare il campo `System.ServiceModel.BasicHttpBinding` dell&#39; `MessageEncoding` oggetto su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilitate l&#39;autenticazione HTTP di base eseguendo le seguenti operazioni:

      * Assegnare il nome utente dei moduli AEM al campo `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Ottenere il documento PDF crittografato.

   * Creare un `BLOB` oggetto utilizzando il relativo costruttore.
   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF crittografato e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto dell&#39; `System.IO.FileStream` oggetto. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà dell&#39; `System.IO.FileStream` oggetto `Length` .
   * Compilare l&#39;array di byte con i dati del flusso richiamando il `System.IO.FileStream` `Read` metodo dell&#39;oggetto e passando l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39; `BLOB` oggetto assegnando il contenuto dell&#39;array di byte al membro `BLOB` dati dell&#39; `MTOM` oggetto.

1. Determinare il tipo di crittografia.

   * Richiamare il metodo dell&#39; `EncryptionServiceClient` oggetto `getPDFEncryption` e passare l&#39; `BLOB` oggetto che contiene il documento PDF. Questo metodo restituisce un `EncryptionTypeResult` oggetto.
   * Ottenere il valore del metodo di dati dell&#39; `EncryptionTypeResult` oggetto `encryptionType` . Ad esempio, se il documento PDF è protetto con crittografia basata su password, il valore di questo membro dati è `EncryptionType.PASSWORD`.

**Consulta anche**

[Riepilogo dei passaggi](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Attivazione di moduli AEM tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamo di moduli AEM con SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)