---
title: Cifratura e decrittografia di documenti PDF
seo-title: Cifratura e decrittografia di documenti PDF
description: Utilizzate il servizio di cifratura per cifrare e decifrare i documenti. Le attività del servizio di cifratura includono la cifratura di un documento PDF con una password, la cifratura di un documento PDF con un certificato, la rimozione della cifratura basata su password da un documento PDF, la rimozione della cifratura basata su certificato da un documento PDF, lo sblocco del documento PDF per eseguire altre operazioni di servizio e la determinazione del tipo di cifratura di un documento PDF protetto.
seo-description: Utilizzate il servizio di cifratura per cifrare e decifrare i documenti. Le attività del servizio di cifratura includono la cifratura di un documento PDF con una password, la cifratura di un documento PDF con un certificato, la rimozione della cifratura basata su password da un documento PDF, la rimozione della cifratura basata su certificato da un documento PDF, lo sblocco del documento PDF per eseguire altre operazioni di servizio e la determinazione del tipo di cifratura di un documento PDF protetto.
uuid: 4e4e2716-c21f-4bfe-ae7a-7e91442414ef
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 5e4bda3a-5648-4c0f-b2f8-bdbebb88f537
translation-type: tm+mt
source-git-commit: 9cf46a26d2aa2e41b924a4de89cf8ab5fdeeefc6
workflow-type: tm+mt
source-wordcount: '8258'
ht-degree: 0%

---


# Cifratura e decrittografia di documenti PDF {#encrypting-and-decrypting-pdf-documents}

**Esempi ed esempi in questo documento sono disponibili solo per  AEM Forms nell&#39;ambiente JEE.**

**Informazioni sul servizio di cifratura**

Il servizio di cifratura consente di cifrare e decrittografare i documenti. Quando un documento viene crittografato, il relativo contenuto diventa illeggibile. Un utente autorizzato può decifrare il documento per ottenere l&#39;accesso ai contenuti. Se un documento PDF è crittografato con una password, l&#39;utente deve specificare la password aperta per poter visualizzare il documento in  Adobe Reader o  Adobe Acrobat. Analogamente, se un documento PDF è crittografato con un certificato, l&#39;utente deve decrittografare il documento PDF con la chiave pubblica che corrisponde al certificato (chiave privata) utilizzato per cifrare il documento PDF.

Il servizio di cifratura consente di effettuare le seguenti operazioni:

* Crittografare un documento PDF con una password. (Vedere [Cifratura di documenti PDF con una password](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password).)
* Cifrare un documento PDF con un certificato. (Vedere [Cifratura di documenti PDF con certificati](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates).)
* Rimuovere la cifratura basata su password da un documento PDF. (Vedere [Rimozione della crittografia della password](encrypting-decrypting-pdf-documents.md#removing-password-encryption).)
* Rimuovere la cifratura basata su certificato da un documento PDF. (Vedere [Rimozione di crittografia basata su certificato](encrypting-decrypting-pdf-documents.md#removing-certificate-based-encryption).)
* Sbloccare il documento PDF per eseguire altre operazioni di servizio. Ad esempio, dopo aver sbloccato un documento PDF con password, è possibile apporvi una firma digitale. (Vedere [Sblocco di documenti PDF crittografati](encrypting-decrypting-pdf-documents.md#unlocking-encrypted-pdf-documents).)
* Determinare il tipo di cifratura di un documento PDF protetto. (Vedere [Determinazione del tipo di cifratura](encrypting-decrypting-pdf-documents.md#determining-encryption-type).)

>[!NOTE]
>
>Per ulteriori informazioni sul servizio di cifratura, vedere [Guida di riferimento dei servizi per  AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Cifratura di documenti PDF con password {#encrypting-pdf-documents-with-a-password}

Quando si esegue la cifratura di un documento PDF con una password, l&#39;utente deve specificare la password per aprire il documento PDF in  Adobe Reader o  Acrobat. Inoltre, prima di poter eseguire un&#39;altra operazione AEM Forms , ad esempio la firma digitale del documento PDF, è necessario sbloccare un documento PDF crittografato con password.

>[!NOTE]
>
>Se si carica un documento PDF crittografato nell&#39;archivio di AEM Forms , non sarà possibile decifrare il documento PDF ed estrarre il contenuto XDP. È consigliabile non crittografare un documento prima di caricarlo nell&#39;archivio AEM Forms . (Vedere [Risorse di scrittura](/help/forms/developing/aem-forms-repository.md#writing-resources).)

>[!NOTE]
>
>Per ulteriori informazioni sul servizio di cifratura, vedere [Guida di riferimento dei servizi per  AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary-of-steps}

Per cifrare un documento PDF con una password, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un oggetto API client di cifratura.
1. Richiedere la cifratura di un documento PDF.
1. Impostare le opzioni di esecuzione della crittografia.
1. Aggiungete la password.
1. Salvare il documento PDF crittografato come file PDF.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, accertatevi di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar (richiesto se  AEM Forms è distribuito su JBoss)
* jbossall-client.jar (richiesto se  AEM Forms è distribuito su JBoss)

**Creare un oggetto API client di cifratura**

Per eseguire un&#39;operazione del servizio di cifratura a livello di programmazione, è necessario creare un client del servizio di cifratura.

**Ottenere un documento PDF da cifrare**

È necessario ottenere un documento PDF non crittografato per cifrare il documento con una password. Se si tenta di proteggere un documento PDF già crittografato, si crea un&#39;eccezione.

**Impostazione delle opzioni di esecuzione della crittografia**

Per cifrare un documento PDF con una password, è necessario specificare quattro valori, inclusi due valori di password. Il primo valore password viene utilizzato per cifrare il documento PDF e deve essere specificato all&#39;apertura del documento PDF. Per rimuovere la cifratura dal documento PDF viene utilizzato il secondo valore della password, denominato valore della password principale. I valori della password sono sensibili alle maiuscole e minuscole e questi due valori non possono essere identici.

Per eseguire la cifratura, è necessario specificare le risorse del documento PDF. È possibile cifrare l’intero documento PDF, tutti gli elementi tranne i metadati del documento o solo gli allegati del documento. Se si cifrano solo gli allegati del documento, all&#39;utente viene richiesta una password quando tenta di accedere agli allegati del file.

Durante la cifratura di un documento PDF, è possibile specificare le autorizzazioni associate al documento protetto. Specificando le autorizzazioni, è possibile controllare le azioni consentite da un utente che apre un documento PDF crittografato con password. Ad esempio, per estrarre correttamente i dati del modulo, è necessario impostare le seguenti autorizzazioni:

* PASSWORD_EDIT_ADD
* PASSWORD_EDIT_MODIFY

>[!NOTE]
>
>Le autorizzazioni sono specificate come valori di enumerazione `PasswordEncryptionPermission`.

**Aggiungere la password**

Dopo aver recuperato un documento PDF non protetto e impostato i valori di esecuzione della cifratura, è possibile aggiungere una password al documento PDF.

**Salvare il documento PDF crittografato come file PDF**

È possibile salvare il documento PDF crittografato con password come file PDF.

**Consulta anche**

[Cifratura di un documento PDF tramite l&#39;API Java](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-using-the-java-api)

[Cifratura di un documento PDF tramite l&#39;API del servizio Web](encrypting-decrypting-pdf-documents.md#encrypting-a-pdf-document-using-the-web-service-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API Servizio crittografia](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[Cifratura di documenti PDF con certificati](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates)

### Crittografare un documento PDF utilizzando l&#39;API Java {#encrypt-a-pdf-document-using-the-java-api}

Crittografare un documento PDF con una password utilizzando l&#39;API di cifratura (Java):

1. Includere i file di progetto.

   Includete file JAR client, ad esempio adobe-Encryption-client.jar, nel percorso di classe del progetto Java.

1. Creare un&#39;API client di cifratura.

   * Creare un oggetto `ServiceClientFactory` che contiene le proprietà di connessione.
   * Creare un oggetto `EncryptionServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Richiedere la cifratura di un documento PDF.

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento PDF da cifrare utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del documento PDF.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Impostare le opzioni di esecuzione della crittografia.

   * Creare un oggetto `PasswordEncryptionOptionSpec` richiamandone il costruttore.
   * Specificare le risorse del documento PDF da cifrare richiamando il metodo `setEncryptOption` dell&#39;oggetto `PasswordEncryptionOption` e passando un valore di enumerazione `PasswordEncryptionOptionSpec` che specifica le risorse del documento da cifrare. Ad esempio, per cifrare l&#39;intero documento PDF, inclusi i metadati e gli allegati, specificare `PasswordEncryptionOption.ALL`.
   * Creare un oggetto `java.util.List` che memorizza le autorizzazioni di cifratura utilizzando il costruttore `ArrayList`.
   * Specificate un&#39;autorizzazione richiamando il metodo `java.util.List` dell&#39;oggetto ‘s `add` e passando un valore di enumerazione che corrisponde all&#39;autorizzazione che desiderate impostare. Ad esempio, per impostare l&#39;autorizzazione che consente a un utente di copiare i dati presenti nel documento PDF, specificare `PasswordEncryptionPermission.PASSWORD_EDIT_COPY`. Ripetete questo passaggio per ogni autorizzazione da impostare.
   * Specificate l&#39;opzione di compatibilità  Acrobat richiamando il metodo `setCompatability` dell&#39;oggetto `PasswordEncryptionOptionSpec` e passando un valore di enumerazione che specifica il livello di compatibilità  Acrobat. Ad esempio, è possibile specificare `PasswordEncryptionCompatability.ACRO_7`.
   * Specificare il valore della password che consente all&#39;utente di aprire il documento PDF crittografato richiamando il metodo `setDocumentOpenPassword` dell&#39;oggetto `PasswordEncryptionOptionSpec` e passando un valore di stringa che rappresenta la password aperta.
   * Specificare il valore della password master che consente a un utente di rimuovere la cifratura dal documento PDF richiamando il metodo `PasswordEncryptionOptionSpec` dell&#39;oggetto `setPermissionPassword` e passando un valore di stringa che rappresenta la password master.

1. Aggiungete la password.

   Per crittografare il documento PDF, richiamare il metodo `encryptPDFUsingPassword` dell&#39;oggetto `EncryptionServiceClient` e passare i valori seguenti:

   * L&#39;oggetto `com.adobe.idp.Document` che contiene il documento PDF da cifrare con la password.
   * L&#39;oggetto `PasswordEncryptionOptionSpec` che contiene le opzioni di esecuzione della crittografia.

   Il metodo `encryptPDFUsingPassword` restituisce un oggetto `com.adobe.idp.Document` contenente un documento PDF crittografato con password.

1. Salvare il documento PDF crittografato come file PDF.

   * Create un oggetto `java.io.File` e accertatevi che l&#39;estensione del file sia .pdf.
   * Richiamare il metodo `com.adobe.idp.Document` dell&#39;oggetto `copyToFile` per copiare nel file il contenuto dell&#39;oggetto `com.adobe.idp.Document`. Assicurarsi di utilizzare l&#39;oggetto `com.adobe.idp.Document` restituito dal metodo `encryptPDFUsingPassword`.

**Consulta anche**

[Riepilogo dei passaggi](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Avvio rapido (modalità SOAP): Cifratura di un documento PDF tramite l&#39;API Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-encrypting-a-pdf-document-using-the-java-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Cifratura di un documento PDF tramite l&#39;API del servizio Web {#encrypting-a-pdf-document-using-the-web-service-api}

Crittografare un documento PDF con una password utilizzando l&#39;API di cifratura (servizio Web):

1. Includere i file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituire `localhost` con l&#39;indirizzo IP del server che ospita  AEM Forms.

1. Creare un oggetto API client di cifratura.

   * Creare un oggetto `EncryptionServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `EncryptionServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passate un valore di stringa che specifica il WSDL al servizio AEM Forms  (ad esempio, `http://localhost:8080/soap/services/EncryptionService?WSDL`). Non è necessario utilizzare l&#39;attributo `lc_version`. Questo attributo viene utilizzato quando create un riferimento a un servizio.
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `EncryptionServiceClient.Endpoint.Binding`. Inserite il valore restituito in `BasicHttpBinding`.
   * Impostare il campo `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto `MessageEncoding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilitate l&#39;autenticazione HTTP di base eseguendo le seguenti operazioni:

      * Assegnare il nome utente del modulo AEM al campo `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Richiedere la cifratura di un documento PDF.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare un documento PDF cifrato con una password.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF da cifrare e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà `System.IO.FileStream` dell&#39;oggetto `Length`.
   * Compilare l&#39;array di byte con i dati del flusso richiamando il metodo `Read` dell&#39;oggetto `System.IO.FileStream` e passando l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando il contenuto dell&#39;array di byte al membro di dati `BLOB` dell&#39;oggetto `MTOM`.

1. Impostare le opzioni di esecuzione della crittografia.

   * Creare un oggetto `PasswordEncryptionOptionSpec` utilizzando il relativo costruttore.
   * Specificare le risorse del documento PDF da cifrare assegnando un valore di enumerazione `PasswordEncryptionOption` al membro di dati `PasswordEncryptionOptionSpec` dell&#39;oggetto `encryptOption`. Per cifrare l&#39;intero PDF, inclusi i metadati e gli allegati, assegnare `PasswordEncryptionOption.ALL` al membro di dati.
   * Specificate l&#39;opzione di compatibilità Acrobat  assegnando un valore di enumerazione `PasswordEncryptionCompatability` al membro di dati `PasswordEncryptionOptionSpec` dell&#39;oggetto `compatability`. Ad esempio, assegnare `PasswordEncryptionCompatability.ACRO_7` a questo membro dati.
   * Specificare il valore della password che consente all&#39;utente di aprire il documento PDF crittografato assegnando un valore di stringa che rappresenta la password aperta al membro di dati `PasswordEncryptionOptionSpec` dell&#39;oggetto `documentOpenPassword`.
   * Specificare il valore della password che consente a un utente di rimuovere la cifratura dal documento PDF assegnando un valore di stringa che rappresenta la password master al membro di dati `PasswordEncryptionOptionSpec` dell&#39;oggetto `permissionPassword`.

1. Aggiungete la password.

   Per crittografare il documento PDF, richiamare il metodo `encryptPDFUsingPassword` dell&#39;oggetto `EncryptionServiceClient` e passare i valori seguenti:

   * L&#39;oggetto `BLOB` che contiene il documento PDF da cifrare con la password.
   * L&#39;oggetto `PasswordEncryptionOptionSpec` che contiene le opzioni di esecuzione della crittografia.

   Il metodo `encryptPDFUsingPassword` restituisce un oggetto `BLOB` contenente un documento PDF crittografato con password.

1. Salvare il documento PDF crittografato come file PDF.

   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF protetto.
   * Creare un array di byte che memorizza il contenuto dei dati dell&#39;oggetto `BLOB` restituito dal metodo `encryptPDFUsingPassword`. Compilare l&#39;array di byte ottenendo il valore del membro di dati `BLOB` dell&#39;oggetto `MTOM`.
   * Creare un oggetto `System.IO.BinaryWriter` richiamandone il costruttore e passando l&#39;oggetto `System.IO.FileStream`.
   * Scrivere il contenuto dell&#39;array di byte in un file PDF richiamando il metodo `System.IO.BinaryWriter` dell&#39;oggetto `Write` e passando l&#39;array di byte.

**Consulta anche**

[Riepilogo dei passaggi](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Chiamata  AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chiamata  AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Cifratura di documenti PDF con certificati {#encrypting-pdf-documents-with-certificates}

La cifratura basata su certificato consente di cifrare un documento per destinatari specifici mediante la tecnologia a chiave pubblica. A diversi destinatari possono essere assegnate diverse autorizzazioni per il documento. Molti aspetti della crittografia sono resi possibili dalla tecnologia a chiave pubblica. Un algoritmo viene utilizzato per generare due numeri grandi, noti come *key*, con le seguenti proprietà:

* Una chiave viene utilizzata per cifrare un set di dati. Successivamente, solo l&#39;altra chiave può essere utilizzata per decrittografare i dati.
* È impossibile distinguere una chiave dall&#39;altra.

Una delle chiavi funge da chiave privata dell&#39;utente. È importante che solo l&#39;utente abbia accesso a questa chiave. L’altra chiave è la chiave pubblica dell’utente, che può essere condivisa con altri utenti.

Un certificato a chiave pubblica contiene la chiave pubblica di un utente e le informazioni di identificazione. Il formato X.509 viene utilizzato per la memorizzazione dei certificati. I certificati sono generalmente rilasciati e firmati digitalmente da un&#39;autorità di certificazione (CA), che è un&#39;entità riconosciuta che fornisce una misura di confidenza nella validità del certificato. I certificati hanno una data di scadenza, dopo la quale non sono più validi. Inoltre, gli elenchi di revoche di certificati (CRL) forniscono informazioni sui certificati revocati prima della data di scadenza. I CRL vengono pubblicati periodicamente dalle autorità di certificazione. Lo stato di revoca di un certificato può essere recuperato anche tramite il protocollo di stato del certificato online (OCSP) sulla rete.

>[!NOTE]
>
>Se si carica un documento PDF crittografato nell&#39;archivio di AEM Forms , non sarà possibile decifrare il documento PDF ed estrarre il contenuto XDP. È consigliabile non crittografare un documento prima di caricarlo nell&#39;archivio AEM Forms . (Vedere [Risorse di scrittura](/help/forms/developing/aem-forms-repository.md#writing-resources).)

>[!NOTE]
>
>Prima di poter cifrare un documento PDF con un certificato, è necessario assicurarsi di aggiungere il certificato  AEM Forms. Un certificato viene aggiunto utilizzando la console di amministrazione o a livello di programmazione tramite l&#39;API di Trust Manager. (Vedere [Importazione di credenziali tramite l&#39;API di Trust Manager](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api).)

>[!NOTE]
>
>Per ulteriori informazioni sul servizio di cifratura, vedere [Guida di riferimento dei servizi per  AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-1}

Per cifrare un documento PDF con un certificato, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un oggetto API client di cifratura.
1. Richiedere la cifratura di un documento PDF.
1. Fate riferimento al certificato.
1. Impostare le opzioni di esecuzione della crittografia.
1. Creare un documento PDF cifrato da certificato.
1. Salvare il documento PDF crittografato come file PDF.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, accertatevi di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar (richiesto se  AEM Forms è distribuito sul server applicazioni JBoss)
* jbossall-client.jar (richiesto se  AEM Forms è distribuito sul server applicazioni JBoss)

**Creare un oggetto API client di cifratura**

Per eseguire un&#39;operazione del servizio di cifratura a livello di programmazione, è necessario creare un client del servizio di cifratura. Se utilizzate l&#39;API Java Encryption Service, create un oggetto `EncrytionServiceClient`. Se utilizzate l&#39;API del servizio Web Encryption Service, create un oggetto `EncryptionServiceService`.

**Ottenere un documento PDF da cifrare**

Per eseguire la cifratura, è necessario ottenere un documento PDF non crittografato. Se si tenta di proteggere un documento PDF già crittografato, viene generata un&#39;eccezione.

**Riferimento al certificato**

Per cifrare un documento PDF con un certificato, fare riferimento a un certificato utilizzato per cifrare un documento PDF. Il certificato è un file .cer, un file .crt o un file .pem. Un file PKCS#12 viene utilizzato per memorizzare le chiavi private con i certificati corrispondenti.

Durante la cifratura di un documento PDF con un certificato, specificare le autorizzazioni associate al documento protetto. Specificando le autorizzazioni, è possibile controllare le azioni che possono essere eseguite da un utente che apre un documento PDF crittografato con un certificato.

**Impostazione delle opzioni di esecuzione della crittografia**

Specificare le risorse del documento PDF da cifrare. È possibile cifrare l&#39;intero documento PDF, tutti gli elementi tranne i metadati del documento o solo gli allegati del documento.

**Creare un documento PDF crittografato con certificato**

Dopo aver recuperato un documento PDF non protetto, fatto riferimento al certificato e impostato le opzioni di esecuzione, è possibile creare un documento PDF crittografato con certificato. Una volta crittografato il documento PDF, è necessario disporre della chiave pubblica corrispondente per decrittografarlo.

**Salvare il documento PDF crittografato come file PDF**

È possibile salvare il documento PDF crittografato come file PDF.

**Consulta anche**

[Cifratura di un documento PDF con un certificato tramite l&#39;API Java](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-with-a-certificate-using-the-java-api)

[Cifratura di un documento PDF con un certificato tramite l&#39;API del servizio Web](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-with-a-certificate-using-the-web-service-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API Servizio crittografia](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[Cifratura di documenti PDF con una password](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Crittografare un documento PDF con un certificato utilizzando l&#39;API Java {#encrypt-a-pdf-document-with-a-certificate-using-the-java-api}

Crittografare un documento PDF con un certificato utilizzando l&#39;API di cifratura (Java):

1. Includere i file di progetto.

   Includete file JAR client, ad esempio adobe-Encryption-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto API client di cifratura.

   * Creare un oggetto `ServiceClientFactory` che contiene le proprietà di connessione.
   * Creare un oggetto `EncryptionServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Richiedere la cifratura di un documento PDF.

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento PDF da cifrare utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del documento PDF.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Fate riferimento al certificato.

   * Creare un oggetto `java.util.List` che memorizza le informazioni sulle autorizzazioni utilizzando il relativo costruttore.
   * Specificare l&#39;autorizzazione associata al documento crittografato richiamando il metodo `add` dell&#39;oggetto `CertificateEncryptionPermissions` e passando un valore di enumerazione `java.util.List` che rappresenta le autorizzazioni concesse all&#39;utente che apre il documento PDF protetto. Ad esempio, per specificare tutte le autorizzazioni, passare `CertificateEncryptionPermissions.PKI_ALL_PERM`.
   * Creare un oggetto `Recipient` utilizzando il relativo costruttore.
   * Creare un oggetto `java.io.FileInputStream` che rappresenta il certificato utilizzato per cifrare il documento PDF utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del certificato.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream` che rappresenta il certificato.
   * Richiamare il metodo `Recipient` dell&#39;oggetto `setX509Cert` e passare l&#39;oggetto `com.adobe.idp.Document` che contiene il certificato. Inoltre, l&#39;oggetto `Recipient`può avere un alias di certificato Truststore o un URL LDAP come origine di certificato.
   * Creare un oggetto `CertificateEncryptionIdentity` che memorizza le informazioni sulle autorizzazioni e sui certificati utilizzando il relativo costruttore.
   * Richiamare il metodo `CertificateEncryptionIdentity` dell&#39;oggetto `setPerms` e passare l&#39;oggetto `java.util.List` che memorizza le informazioni sulle autorizzazioni.
   * Richiamare il metodo `CertificateEncryptionIdentity` dell&#39;oggetto `setRecipient` e passare l&#39;oggetto `Recipient` che memorizza le informazioni sul certificato.
   * Creare un oggetto `java.util.List` che memorizza le informazioni sul certificato utilizzando il relativo costruttore.
   * Richiamare il metodo add dell&#39;oggetto `java.util.List` e passare l&#39;oggetto `CertificateEncryptionIdentity`. (Questo oggetto `java.util.List` viene passato come parametro al metodo `encryptPDFUsingCertificates`.)

1. Impostare le opzioni di esecuzione della crittografia.

   * Creare un oggetto `CertificateEncryptionOptionSpec` richiamandone il costruttore.
   * Specificare le risorse del documento PDF da cifrare richiamando il metodo `setOption` dell&#39;oggetto `CertificateEncryptionOption` e passando un valore di enumerazione `CertificateEncryptionOptionSpec` che specifica le risorse del documento da cifrare. Ad esempio, per cifrare l&#39;intero documento PDF, inclusi i metadati e gli allegati, specificare `CertificateEncryptionOption.ALL`.
   * Specificate l&#39;opzione di compatibilità  Acrobat richiamando il metodo `setCompat` dell&#39;oggetto `CertificateEncryptionCompatibility` e passando un valore di enumerazione `CertificateEncryptionOptionSpec` che specifica il livello di compatibilità  Acrobat. Ad esempio, è possibile specificare `CertificateEncryptionCompatibility.ACRO_7`.

1. Creare un documento PDF cifrato da certificato.

   Crittografare il documento PDF con un certificato richiamando il metodo `encryptPDFUsingCertificates` dell&#39;oggetto `EncryptionServiceClient` e passando i valori seguenti:

   * L&#39;oggetto `com.adobe.idp.Document` che contiene il documento PDF da cifrare.
   * L&#39;oggetto `java.util.List` che memorizza le informazioni sul certificato.
   * L&#39;oggetto `CertificateEncryptionOptionSpec` che contiene le opzioni di esecuzione della crittografia.

   Il metodo `encryptPDFUsingCertificates` restituisce un oggetto `com.adobe.idp.Document` contenente un documento PDF crittografato con certificato.

1. Salvare il documento PDF crittografato come file PDF.

   * Create un oggetto `java.io.File` e accertatevi che l&#39;estensione del nome del file sia .pdf.
   * Richiamare il metodo `com.adobe.idp.Document` dell&#39;oggetto `copyToFile` per copiare nel file il contenuto dell&#39;oggetto `com.adobe.idp.Document`. Assicurarsi di utilizzare l&#39;oggetto `com.adobe.idp.Document` restituito dal metodo `encryptPDFUsingCertificates`.

**Consulta anche**

[Riepilogo dei passaggi](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Avvio rapido (modalità SOAP): Cifratura di un documento PDF con un certificato tramite l&#39;API Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-encrypting-a-pdf-document-with-a-certificate-using-the-java-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Crittografare un documento PDF con un certificato utilizzando l&#39;API del servizio Web {#encrypt-a-pdf-document-with-a-certificate-using-the-web-service-api}

Crittografare un documento PDF con un certificato utilizzando l&#39;API di cifratura (servizio Web):

1. Includere i file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituire `localhost` con l&#39;indirizzo IP del server che ospita  AEM Forms.

1. Creare un oggetto API client di cifratura.

   * Creare un oggetto `EncryptionServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `EncryptionServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passate un valore di stringa che specifica il WSDL al servizio AEM Forms  (ad esempio, `http://localhost:8080/soap/services/EncryptionService?WSDL`). Non è necessario utilizzare l&#39;attributo `lc_version`. Questo attributo viene utilizzato quando create un riferimento a un servizio.
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `EncryptionServiceClient.Endpoint.Binding`. Inserite il valore restituito in `BasicHttpBinding`.
   * Impostare il campo `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto `MessageEncoding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilitate l&#39;autenticazione HTTP di base eseguendo le seguenti operazioni:

      * Assegnare il nome utente del modulo AEM al campo `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Richiedere la cifratura di un documento PDF.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare un documento PDF cifrato con un certificato.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF da cifrare e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà `System.IO.FileStream` dell&#39;oggetto `Length`.
   * Compilare l&#39;array di byte con i dati del flusso richiamando il metodo `Read` dell&#39;oggetto `System.IO.FileStream` e passando l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnandone la proprietà `MTOM` con il contenuto dell&#39;array di byte.

1. Fate riferimento al certificato.

   * Creare un oggetto `Recipient` utilizzando il relativo costruttore. Questo oggetto memorizzerà le informazioni sul certificato.
   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. Questo oggetto `BLOB` archivierà il certificato per la cifratura del documento PDF.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del certificato e la modalità in cui aprire il file.
   * Creare un array di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà `System.IO.FileStream` dell&#39;oggetto `Length`.
   * Compilare l&#39;array di byte con i dati del flusso richiamando il metodo `Read` dell&#39;oggetto `System.IO.FileStream` e passando l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando il contenuto dell&#39;array di byte al membro di dati `BLOB` dell&#39;oggetto `MTOM`.
   * Assegnare l&#39;oggetto `BLOB` che memorizza il certificato al membro di dati `Recipient` dell&#39;oggetto `x509Cert`.
   * Creare un oggetto `CertificateEncryptionIdentity` che memorizza le informazioni sul certificato utilizzando il relativo costruttore.
   * Assegnare l&#39;oggetto `Recipient` che memorizza il certificato al membro di dati del destinatario dell&#39;oggetto `CertificateEncryptionIdentity`.
   * Creare un array `Object` e assegnare l&#39;oggetto `CertificateEncryptionIdentity` al primo elemento dell&#39;array `Object`. Questa matrice `Object` viene passata come parametro al metodo `encryptPDFUsingCertificates`.

1. Impostare le opzioni di esecuzione della crittografia.

   * Creare un oggetto `CertificateEncryptionOptionSpec` utilizzando il relativo costruttore.
   * Specificare le risorse del documento PDF da cifrare assegnando un valore di enumerazione `CertificateEncryptionOption` al membro di dati `CertificateEncryptionOptionSpec` dell&#39;oggetto `option`. Per cifrare l&#39;intero documento PDF, inclusi i relativi metadati e i relativi allegati, assegnare `CertificateEncryptionOption.ALL` al membro di dati.
   * Specificate l&#39;opzione di compatibilità Acrobat  assegnando un valore di enumerazione `CertificateEncryptionCompatibility` al membro di dati `CertificateEncryptionOptionSpec` dell&#39;oggetto `compat`. Ad esempio, assegnare `CertificateEncryptionCompatibility.ACRO_7` a questo membro dati.

1. Creare un documento PDF cifrato da certificato.

   Crittografare il documento PDF con un certificato richiamando il metodo `encryptPDFUsingCertificates` dell&#39;oggetto `EncryptionServiceService` e passando i valori seguenti:

   * L&#39;oggetto `BLOB` che contiene il documento PDF da cifrare.
   * L&#39;array `Object` che memorizza le informazioni sul certificato.
   * L&#39;oggetto `CertificateEncryptionOptionSpec` che contiene le opzioni di esecuzione della crittografia.

   Il metodo `encryptPDFUsingCertificates` restituisce un oggetto `BLOB` contenente un documento PDF crittografato con certificato.

1. Salvare il documento PDF crittografato come file PDF.

   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF protetto.
   * Creare un array di byte che memorizza il contenuto dei dati dell&#39;oggetto `BLOB` restituito dal metodo `encryptPDFUsingCertificates`. Compilare l&#39;array di byte ottenendo il valore del membro di dati `BLOB` dell&#39;oggetto `binaryData`.
   * Creare un oggetto `System.IO.BinaryWriter` richiamandone il costruttore e passando l&#39;oggetto `System.IO.FileStream`.
   * Scrivere il contenuto dell&#39;array di byte in un file PDF richiamando il metodo `System.IO.BinaryWriter` dell&#39;oggetto `Write` e passando l&#39;array di byte.

**Consulta anche**

[Riepilogo dei passaggi](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Chiamata  AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chiamata  AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Rimozione della crittografia basata su certificato {#removing-certificate-based-encryption}

È possibile rimuovere la cifratura basata su certificato da un documento PDF per consentire agli utenti di aprire il documento PDF in  Adobe Reader o  Acrobat. Per rimuovere la cifratura da un documento PDF cifrato con un certificato, è necessario fare riferimento a una chiave pubblica. Dopo la rimozione della cifratura da un documento PDF, la cifratura non è più protetta.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio di cifratura, vedere [Guida di riferimento dei servizi per  AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-2}

Per rimuovere la cifratura basata su certificato da un documento PDF, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un client del servizio di cifratura.
1. Ottenere il documento PDF crittografato.
1. Rimuovere la cifratura.
1. Salvare il documento PDF come file PDF.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, accertatevi di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar (richiesto se  AEM Forms è distribuito sul server applicazioni JBoss)
* jbossall-client.jar (richiesto se  AEM Forms è distribuito sul server applicazioni JBoss)

**Creare un client del servizio di crittografia**

Per eseguire un&#39;operazione del servizio di cifratura a livello di programmazione, è necessario creare un client del servizio di cifratura. Se utilizzate l&#39;API Java Encryption Service, create un oggetto `EncrytionServiceClient`. Se utilizzate l&#39;API del servizio Web Encryption Service, create un oggetto `EncryptionServiceService`.

**Ottenere il documento PDF crittografato**

Per rimuovere la cifratura basata su certificato, è necessario ottenere un documento PDF crittografato. Se si tenta di rimuovere la cifratura da un documento PDF non crittografato, viene generata un&#39;eccezione. Analogamente, se tentate di rimuovere la cifratura basata su certificato da un documento crittografato con password, viene generata un&#39;eccezione.

**Rimuovi crittografia**

Per rimuovere la cifratura basata su certificato da un documento PDF cifrato, è necessario un documento PDF cifrato e la chiave privata corrispondente alla chiave utilizzata per cifrare il documento PDF. Il valore alias della chiave privata viene specificato quando si rimuove la cifratura basata su certificato da un documento PDF crittografato. Per informazioni sulla chiave pubblica, vedere [Cifratura di documenti PDF con certificati](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates).

>[!NOTE]
>
>Una chiave privata viene memorizzata nell&#39; AEM Forms Trust Store. Quando un certificato è posizionato in tale posizione, viene specificato un valore alias.

**Salvare il documento PDF**

Dopo aver rimosso la cifratura basata su certificato da un documento PDF cifrato, è possibile salvare il documento PDF come file PDF. Gli utenti possono aprire il documento PDF in  Adobe Reader o  Acrobat.

**Consulta anche**

[Rimozione della crittografia basata su certificato tramite l&#39;API Java](encrypting-decrypting-pdf-documents.md#remove-certificate-based-encryption-using-the-java-api)

[Rimozione della crittografia basata su certificato tramite l&#39;API del servizio Web](encrypting-decrypting-pdf-documents.md#remove-certificate-based-encryption-using-the-web-service-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API Servizio crittografia](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

### Rimuovere la crittografia basata su certificato utilizzando l&#39;API Java {#remove-certificate-based-encryption-using-the-java-api}

Rimuovere la cifratura basata su certificato da un documento PDF utilizzando l&#39;API di cifratura (Java):

1. Includere i file di progetto.

   Includete file JAR client, ad esempio adobe-Encryption-client.jar, nel percorso di classe del progetto Java.

1. Creare un client del servizio di cifratura.

   * Creare un oggetto `ServiceClientFactory` che contiene le proprietà di connessione.
   * Creare un oggetto `EncryptionServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Ottenere il documento PDF crittografato.

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento PDF crittografato utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del documento PDF crittografato.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Rimuovere la cifratura.

   Rimuovere la cifratura basata su certificato dal documento PDF richiamando il metodo `EncryptionServiceClient` dell&#39;oggetto `removePDFCertificateSecurity` e passando i valori seguenti:

   * L&#39;oggetto `com.adobe.idp.Document` che contiene il documento PDF crittografato.
   * Un valore di stringa che specifica il nome alias della chiave privata che corrisponde alla chiave utilizzata per cifrare il documento PDF.

   Il metodo `removePDFCertificateSecurity` restituisce un oggetto `com.adobe.idp.Document` contenente un documento PDF non protetto.

1. Salvare il documento PDF.

   * Create un oggetto `java.io.File` e accertatevi che l&#39;estensione del file sia .pdf.
   * Richiamare il metodo `com.adobe.idp.Document` dell&#39;oggetto `copyToFile` per copiare nel file il contenuto dell&#39;oggetto `Document`. Assicurarsi di utilizzare l&#39;oggetto `com.adobe.idp.Document` restituito dal metodo `removePDFCredentialSecurity`.

**Consulta anche**

[Riepilogo dei passaggi](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Avvio rapido (modalità SOAP): Rimozione della crittografia basata su certificato tramite l&#39;API Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-removing-certificate-based-encryption-using-the-java-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Rimuovere la crittografia basata su certificato utilizzando l&#39;API del servizio Web {#remove-certificate-based-encryption-using-the-web-service-api}

Rimuovete la cifratura basata su certificato utilizzando l&#39;API di cifratura (servizio Web):

1. Includere i file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituire `localhost` con l&#39;indirizzo IP del server che ospita  AEM Forms.

1. Creare un client del servizio di cifratura.

   * Creare un oggetto `EncryptionServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `EncryptionServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passate un valore di stringa che specifica il WSDL al servizio AEM Forms  (ad esempio, `http://localhost:8080/soap/services/EncryptionService?WSDL`). Non è necessario utilizzare l&#39;attributo `lc_version`. Questo attributo viene utilizzato quando create un riferimento a un servizio.
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `EncryptionServiceClient.Endpoint.Binding`. Inserite il valore restituito in `BasicHttpBinding`.
   * Impostare il campo `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto `MessageEncoding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilitate l&#39;autenticazione HTTP di base eseguendo le seguenti operazioni:

      * Assegnare il nome utente del modulo AEM al campo `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Ottenere il documento PDF crittografato.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare il documento PDF crittografato.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF crittografato e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà `System.IO.FileStream` dell&#39;oggetto `Length`.
   * Compilare l&#39;array di byte con i dati del flusso richiamando il metodo `Read` dell&#39;oggetto `System.IO.FileStream` e passando l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando il contenuto dell&#39;array di byte al membro di dati `BLOB` dell&#39;oggetto `MTOM`.

1. Rimuovere la cifratura.

   Richiamare il metodo `EncryptionServiceClient` dell&#39;oggetto `removePDFCertificateSecurity` e trasmettere i seguenti valori:

   * L&#39;oggetto `BLOB` che contiene i dati del flusso di file che rappresenta un documento PDF crittografato.
   * Un valore di stringa che specifica il nome alias della chiave pubblica che corrisponde alla chiave privata utilizzata per cifrare il documento PDF.

   Il metodo `removePDFCredentialSecurity` restituisce un oggetto `BLOB` contenente un documento PDF non protetto.

1. Salvare il documento PDF.

   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF non protetto.
   * Creare un array di byte che memorizza il contenuto dell&#39;oggetto `BLOB` restituito dal metodo `removePDFPasswordSecurity`. Compilare l&#39;array di byte ottenendo il valore del membro di dati `BLOB` dell&#39;oggetto `MTOM`.
   * Creare un oggetto `System.IO.BinaryWriter` richiamandone il costruttore e passando l&#39;oggetto `System.IO.FileStream`.
   * Scrivere il contenuto dell&#39;array di byte in un file PDF richiamando il metodo `System.IO.BinaryWriter` dell&#39;oggetto `Write` e passando l&#39;array di byte.

**Consulta anche**

[Riepilogo dei passaggi](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Chiamata  AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chiamata  AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Rimozione crittografia password {#removing-password-encryption}

La cifratura basata su password può essere rimossa da un documento PDF per consentire agli utenti di aprire il documento PDF in  Adobe Reader o  Acrobat senza dover specificare una password. Una volta rimossa la cifratura basata su password da un documento PDF, il documento non è più protetto.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio di cifratura, vedere [Guida di riferimento dei servizi per  AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-3}

Per rimuovere la cifratura basata su password da un documento PDF, effettuare le seguenti operazioni:

1. Includi file di progetto
1. Creare un client del servizio di cifratura.
1. Ottenere il documento PDF crittografato.
1. Rimuovere la password.
1. Salvare il documento PDF come file PDF.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, accertatevi di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar (richiesto se  AEM Forms è distribuito su JBoss)
* jbossall-client.jar (richiesto se  AEM Forms è distribuito su JBoss)

**Creare un client del servizio di crittografia**

Per eseguire un&#39;operazione del servizio di cifratura a livello di programmazione, è necessario creare un client del servizio di cifratura. Se utilizzate l&#39;API Java Encryption Service, create un oggetto `EncrytionServiceClient`. Se utilizzate l&#39;API del servizio Web Encryption Service, create un oggetto `EncryptionServiceService`.

**Ottenere il documento PDF crittografato**

È necessario ottenere un documento PDF crittografato per rimuovere la cifratura basata su password. Se si tenta di rimuovere la cifratura da un documento PDF non crittografato, viene generata un&#39;eccezione.

**Rimuovere la password**

Per rimuovere la cifratura basata su password da un documento PDF cifrato, è necessario un documento PDF cifrato e un valore della password master utilizzato per rimuovere la cifratura dal documento PDF. La password utilizzata per aprire un documento PDF crittografato con password non può essere utilizzata per rimuovere la cifratura. Una password master è specificata quando il documento PDF è crittografato con una password. (Vedere [Cifratura di documenti PDF con una password](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password).)

**Salvare il documento PDF**

Dopo che il servizio di cifratura ha rimosso la cifratura basata su password da un documento PDF, è possibile salvare il documento PDF come file PDF. Gli utenti possono aprire il documento PDF in  Adobe Reader o  Acrobat senza specificare una password.

**Consulta anche**

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API Servizio crittografia](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[Cifratura di documenti PDF con una password](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Rimuovere la crittografia basata su password utilizzando l&#39;API Java {#remove-password-based-encryption-using-the-java-api}

Rimuovere la cifratura basata su password da un documento PDF utilizzando l&#39;API di cifratura (Java):

1. Includere i file di progetto.

   Includete file JAR client, ad esempio adobe-Encryption-client.jar, nel percorso di classe del progetto Java.

1. Creare un client del servizio di cifratura.

   * Creare un oggetto `ServiceClientFactory` che contiene le proprietà di connessione.
   * Creare un oggetto `EncryptionServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Ottenere il documento PDF crittografato.

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento PDF crittografato utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del documento PDF.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Rimuovere la password.

   Rimuovere la cifratura basata su password dal documento PDF richiamando il metodo `EncryptionServiceClient` dell&#39;oggetto `removePDFPasswordSecurity` e passando i seguenti valori:

   * Un oggetto `com.adobe.idp.Document` che contiene il documento PDF crittografato.
   * Valore stringa che specifica il valore della password master utilizzato per rimuovere la cifratura dal documento PDF.

   Il metodo `removePDFPasswordSecurity` restituisce un oggetto `com.adobe.idp.Document` contenente un documento PDF non protetto.

1. Salvare il documento PDF.

   * Create un oggetto `java.io.File` e accertatevi che l&#39;estensione del nome del file sia .pdf.
   * Richiamare il metodo `com.adobe.idp.Document` dell&#39;oggetto `copyToFile` per copiare nel file il contenuto dell&#39;oggetto `Document`. Assicurarsi di utilizzare l&#39;oggetto `Document` restituito dal metodo `removePDFPasswordSecurity`.

**Consulta anche**

[Avvio rapido (modalità SOAP): Rimozione della crittografia basata su password tramite l&#39;API Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-removing-password-based-encryption-using-the-java-api)

### Rimuovere la crittografia basata su password utilizzando l&#39;API del servizio Web {#remove-password-based-encryption-using-the-web-service-api}

Rimuovere la cifratura basata su password utilizzando l&#39;API di cifratura (servizio Web):

1. Includere i file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituire `localhost` con l&#39;indirizzo IP del server che ospita  AEM Forms.

1. Creare un client del servizio di cifratura.

   * Creare un oggetto `EncryptionServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `EncryptionServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passate un valore di stringa che specifica il WSDL al servizio AEM Forms  (ad esempio, `http://localhost:8080/soap/services/EncryptionService?WSDL`). Non è necessario utilizzare l&#39;attributo `lc_version`. Questo attributo viene utilizzato quando create un riferimento a un servizio.
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `EncryptionServiceClient.Endpoint.Binding`. Inserite il valore restituito in `BasicHttpBinding`.
   * Impostare il campo `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto `MessageEncoding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilitate l&#39;autenticazione HTTP di base eseguendo le seguenti operazioni:

      * Assegnare il nome utente del modulo AEM al campo `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Ottenere il documento PDF crittografato.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare un documento PDF crittografato con password.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF crittografato e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà `System.IO.FileStream` dell&#39;oggetto `Length`.
   * Compilare l&#39;array di byte con i dati del flusso richiamando il metodo `Read` dell&#39;oggetto `System.IO.FileStream` e passando l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando il contenuto dell&#39;array di byte al membro di dati `BLOB` dell&#39;oggetto `MTOM`.

1. Rimuovere la password.

   Richiamare il metodo `EncryptionServiceService` dell&#39;oggetto `removePDFPasswordSecurity` e trasmettere i seguenti valori:

   * L&#39;oggetto `BLOB` che contiene i dati del flusso di file che rappresenta un documento PDF crittografato.
   * Valore stringa che specifica il valore della password utilizzato per rimuovere la cifratura dal documento PDF. Questo valore viene specificato durante la cifratura del documento PDF con una password.

   Il metodo `removePDFPasswordSecurity` restituisce un oggetto `BLOB` contenente un documento PDF non protetto.

1. Salvare il documento PDF.

   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF non protetto.
   * Creare un array di byte che memorizza il contenuto dell&#39;oggetto `BLOB` restituito dal metodo `removePDFPasswordSecurity`. Compilare l&#39;array di byte ottenendo il valore del membro di dati `BLOB` dell&#39;oggetto `MTOM`.
   * Creare un oggetto `System.IO.BinaryWriter` richiamandone il costruttore e passando l&#39;oggetto `System.IO.FileStream`.
   * Scrivere il contenuto dell&#39;array di byte in un file PDF richiamando il metodo `System.IO.BinaryWriter` dell&#39;oggetto `Write` e passando l&#39;array di byte.

**Consulta anche**

[Chiamata  AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chiamata  AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Sblocco di documenti PDF crittografati {#unlocking-encrypted-pdf-documents}

È necessario sbloccare un documento PDF crittografato con password o con certificato prima di poter eseguire un&#39;altra operazione AEM Forms . Se si tenta di eseguire un&#39;operazione su un documento PDF crittografato, verrà generata un&#39;eccezione. Dopo aver sbloccato un documento PDF crittografato, è possibile eseguire una o più operazioni su di esso. Queste operazioni possono appartenere ad altri servizi, ad esempio Acrobat Reader DC Extensions Service.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio di cifratura, vedere [Guida di riferimento dei servizi per  AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-4}

Per sbloccare un documento PDF crittografato, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un client del servizio di cifratura.
1. Ottenere il documento PDF crittografato.
1. Sblocca il documento.
1. Eseguire un&#39;operazione AEM Forms .

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, accertatevi di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar (richiesto se  AEM Forms è distribuito sul server applicazioni JBoss)
* jbossall-client.jar (richiesto se  AEM Forms è distribuito sul server applicazioni JBoss)

**Creare un client del servizio di crittografia**

Per eseguire un&#39;operazione del servizio di cifratura a livello di programmazione, è necessario creare un client del servizio di cifratura. Se utilizzate l&#39;API Java Encryption Service, create un oggetto `EncrytionServiceClient`. Se utilizzate l&#39;API del servizio Web Encryption Service, create un oggetto `EncryptionServiceService`.

**Ottenere il documento PDF crittografato**

Per sbloccare un documento PDF crittografato è necessario ottenerlo. Se si tenta di sbloccare un documento PDF non crittografato, viene generata un&#39;eccezione.

**Sblocca documento**

Per sbloccare un documento PDF crittografato con password, è necessario un documento PDF crittografato e un valore di password utilizzato per aprire un documento PDF crittografato con password. Questo valore viene specificato durante la cifratura del documento PDF con una password. (Vedere [Cifratura di documenti PDF con una password](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password).)

Per sbloccare un documento PDF crittografato con certificato, è necessario un documento PDF crittografato e il valore alias della chiave pubblica che corrisponde alla chiave privata utilizzata per cifrare il documento PDF.

**Eseguire un&#39;operazione AEM Forms**

Dopo aver sbloccato un documento PDF crittografato, è possibile eseguire un&#39;altra operazione del servizio, ad esempio l&#39;applicazione dei diritti di utilizzo. Questa operazione appartiene al servizio Acrobat Reader DC Extensions.

**Consulta anche**

[Sbloccare un documento PDF crittografato mediante l&#39;API Java](encrypting-decrypting-pdf-documents.md#unlock-an-encrypted-pdf-document-using-the-java-api)

[Sblocco di un documento PDF crittografato tramite l&#39;API del servizio Web](encrypting-decrypting-pdf-documents.md#unlock-an-encrypted-pdf-document-using-the-web-service-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API Servizio crittografia](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

### Sbloccare un documento PDF crittografato utilizzando l&#39;API Java {#unlock-an-encrypted-pdf-document-using-the-java-api}

Sbloccare un documento PDF crittografato utilizzando l&#39;API di cifratura (Java):

1. Includere i file di progetto.

   Includete file JAR client, ad esempio adobe-Encryption-client.jar, nel percorso di classe del progetto Java.

1. Creare un client del servizio di cifratura.

   * Creare un oggetto `ServiceClientFactory` che contiene le proprietà di connessione.
   * Creare un oggetto `EncryptionServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Ottenere il documento PDF crittografato.

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento PDF crittografato utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del documento PDF crittografato.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Sblocca il documento.

   Sbloccare un documento PDF crittografato richiamando il metodo `unlockPDFUsingPassword` o `unlockPDFUsingCredential` dell&#39;oggetto `EncryptionServiceClient`.

   Per sbloccare un documento PDF crittografato con una password, richiamare il metodo `unlockPDFUsingPassword` e trasmettere i valori seguenti:

   * Un oggetto `com.adobe.idp.Document` che contiene il documento PDF crittografato con password.
   * Valore stringa che specifica il valore della password utilizzata per aprire un documento PDF crittografato con password. Questo valore viene specificato durante la cifratura del documento PDF con una password.

   Per sbloccare un documento PDF cifrato con un certificato, richiamare il metodo `unlockPDFUsingCredential` e passare i seguenti valori:

   * Un oggetto `com.adobe.idp.Document` che contiene il documento PDF crittografato con certificato.
   * Una stringa che specifica il nome alias della chiave pubblica corrispondente alla chiave privata utilizzata per cifrare il documento PDF.

   I metodi `unlockPDFUsingPassword` e `unlockPDFUsingCredential` restituiscono entrambi un oggetto `com.adobe.idp.Document` passato a un altro metodo Java di AEM Forms  per eseguire un&#39;operazione.

1. Eseguire un&#39;operazione AEM Forms .

   Eseguire un&#39;operazione AEM Forms  sul documento PDF sbloccato per soddisfare i requisiti aziendali. Ad esempio, se si desidera applicare diritti di utilizzo a un documento PDF non bloccato, passare l&#39;oggetto `com.adobe.idp.Document` restituito dai metodi `unlockPDFUsingPassword` o `unlockPDFUsingCredential` al metodo `ReaderExtensionsServiceClient` dell&#39;oggetto `applyUsageRights`.

**Consulta anche**

[Riepilogo dei passaggi](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Avvio rapido (modalità SOAP): Sblocco di un documento PDF crittografato tramite l&#39;API](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-unlocking-an-encrypted-pdf-document-using-the-java-api)  Java (modalità SOAP)

[Applicazione dei diritti di utilizzo ai documenti PDF](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Sbloccare un documento PDF crittografato utilizzando l&#39;API del servizio Web {#unlock-an-encrypted-pdf-document-using-the-web-service-api}

Sbloccare un documento PDF crittografato utilizzando l&#39;API di cifratura (servizio Web):

1. Includere i file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituire `localhost` con l&#39;indirizzo IP del server che ospita  AEM Forms.

1. Creare un client del servizio di cifratura.

   * Creare un oggetto `EncryptionServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `EncryptionServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passate un valore di stringa che specifica il WSDL al servizio AEM Forms  (ad esempio, `http://localhost:8080/soap/services/EncryptionService?WSDL`). Non è necessario utilizzare l&#39;attributo `lc_version`. Questo attributo viene utilizzato quando create un riferimento a un servizio.
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `EncryptionServiceClient.Endpoint.Binding`. Inserite il valore restituito in `BasicHttpBinding`.
   * Impostare il campo `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto `MessageEncoding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilitate l&#39;autenticazione HTTP di base eseguendo le seguenti operazioni:

      * Assegnare il nome utente del modulo AEM al campo `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Ottenere un documento PDF crittografato.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF crittografato e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà `System.IO.FileStream` dell&#39;oggetto `Length`.
   * Compilare l&#39;array di byte con i dati del flusso richiamando il metodo `Read` dell&#39;oggetto `System.IO.FileStream` e passando l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando il contenuto dell&#39;array di byte al membro di dati `BLOB` dell&#39;oggetto `MTOM`.

1. Sblocca il documento.

   Sbloccare un documento PDF crittografato richiamando il metodo `unlockPDFUsingPassword` o `unlockPDFUsingCredential` dell&#39;oggetto `EncryptionServiceClient`.

   Per sbloccare un documento PDF crittografato con una password, richiamare il metodo `unlockPDFUsingPassword` e trasmettere i valori seguenti:

   * Un oggetto `BLOB` che contiene il documento PDF crittografato con password.
   * Valore stringa che specifica il valore della password utilizzata per aprire un documento PDF crittografato con password. Questo valore viene specificato durante la cifratura del documento PDF con una password.

   Per sbloccare un documento PDF cifrato con un certificato, richiamare il metodo `unlockPDFUsingCredential` e passare i seguenti valori:

   * Un oggetto `BLOB` che contiene il documento PDF crittografato con certificato.
   * Un valore di stringa che specifica il nome alias della chiave pubblica che corrisponde alla chiave privata utilizzata per cifrare il documento PDF.

   I metodi `unlockPDFUsingPassword` e `unlockPDFUsingCredential` restituiscono entrambi un oggetto `com.adobe.idp.Document` passato a un altro metodo AEM Forms  per eseguire un&#39;operazione.

1. Eseguire un&#39;operazione AEM Forms .

   Eseguire un&#39;operazione AEM Forms  sul documento PDF sbloccato per soddisfare i requisiti aziendali. Ad esempio, se si desidera applicare diritti di utilizzo al documento PDF non bloccato, passare l&#39;oggetto `BLOB` restituito dai metodi `unlockPDFUsingPassword` o `unlockPDFUsingCredential` al metodo `ReaderExtensionsServiceClient` dell&#39;oggetto `applyUsageRights`.

**Consulta anche**

[Riepilogo dei passaggi](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Chiamata  AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chiamata  AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Determinazione del tipo di crittografia {#determining-encryption-type}

È possibile determinare a livello di programmazione il tipo di cifratura che protegge un documento PDF utilizzando l&#39;API Java Encryption Service o l&#39;API del servizio Web Encryption Service. A volte è necessario determinare in modo dinamico se un documento PDF è crittografato e, in tal caso, il tipo di cifratura. Ad esempio, è possibile determinare se un documento PDF è protetto tramite cifratura basata su password o criteri di Rights Management.

Un documento PDF può essere protetto tramite i seguenti tipi di cifratura:

* Cifratura basata su password
* Cifratura basata su certificato
* Criterio creato dal servizio Rights Management
* Un altro tipo di crittografia

>[!NOTE]
>
>Per ulteriori informazioni sul servizio di cifratura, vedere [Guida di riferimento dei servizi per  AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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
* adobe-encryption-client.jar
* adobe-utilities.jar (richiesto se  AEM Forms è distribuito sul server applicazioni JBoss)
* jbossall-client.jar (richiesto se  AEM Forms è distribuito sul server applicazioni JBoss)

**Creare un client di servizio**

Per eseguire un&#39;operazione del servizio di cifratura a livello di programmazione, è necessario creare un client del servizio di cifratura. Se utilizzate l&#39;API Java Encryption Service, create un oggetto `EncrytionServiceClient`. Se utilizzate l&#39;API del servizio Web Encryption Service, create un oggetto `EncryptionServiceService`.

**Ottenere il documento PDF crittografato**

È necessario ottenere un documento PDF per determinare il tipo di cifratura che lo protegge.

**Determinare il tipo di crittografia**

È possibile determinare il tipo di cifratura che protegge un documento PDF. Se il documento PDF non è protetto, il servizio di cifratura vi informerà che il documento PDF non è protetto.

**Consulta anche**

[Determinare il tipo di crittografia utilizzando l&#39;API Java](encrypting-decrypting-pdf-documents.md#determine-the-encryption-type-using-the-java-api)

[Determinare il tipo di crittografia utilizzando l&#39;API del servizio Web](encrypting-decrypting-pdf-documents.md#determine-the-encryption-type-using-the-web-service-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API Servizio crittografia](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[Protezione dei documenti con i criteri](/help/forms/developing/protecting-documents-policies.md#protecting-documents-with-policies)

### Determinare il tipo di crittografia utilizzando l&#39;API Java {#determine-the-encryption-type-using-the-java-api}

Determinare il tipo di cifratura che protegge un documento PDF utilizzando l&#39;API di cifratura (Java):

1. Includere i file di progetto.

   Includete file JAR client, ad esempio adobe-Encryption-client.jar, nel percorso di classe del progetto Java.

1. Creare un client di servizi.

   * Creare un oggetto `ServiceClientFactory` che contiene le proprietà di connessione.
   * Creare un oggetto `EncryptionServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Ottenere il documento PDF crittografato.

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento PDF utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del documento PDF.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Determinare il tipo di crittografia.

   * Determinare il tipo di cifratura richiamando il metodo `getPDFEncryption` dell&#39;oggetto `com.adobe.idp.Document` e passando l&#39;oggetto `EncryptionServiceClient` che contiene il documento PDF. Questo metodo restituisce un oggetto `EncryptionTypeResult`.
   * Richiamare il metodo `EncryptionTypeResult` dell&#39;oggetto `getEncryptionType`. Questo metodo restituisce un valore enum `EncryptionType` che specifica il tipo di crittografia. Ad esempio, se il documento PDF è protetto con crittografia basata su password, questo metodo restituisce `EncryptionType.PASSWORD`.

**Consulta anche**

[Riepilogo dei passaggi](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Avvio rapido (modalità SOAP): Determinazione del tipo di crittografia tramite l&#39;API Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-determining-encryption-type-using-the-java-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Determinare il tipo di crittografia utilizzando l&#39;API del servizio Web {#determine-the-encryption-type-using-the-web-service-api}

Determinare il tipo di cifratura che protegge un documento PDF utilizzando l&#39;API di cifratura (servizio Web):

1. Includere i file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituire `localhost` con l&#39;indirizzo IP del server che ospita  AEM Forms.

1. Creare un client di servizi.

   * Creare un oggetto `EncryptionServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `EncryptionServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passate un valore di stringa che specifica il WSDL al servizio AEM Forms  (ad esempio, `http://localhost:8080/soap/services/EncryptionService?WSDL`). Non è necessario utilizzare l&#39;attributo `lc_version`. Questo attributo viene utilizzato quando create un riferimento a un servizio.
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `EncryptionServiceClient.Endpoint.Binding`. Inserite il valore restituito in `BasicHttpBinding`.
   * Impostare il campo `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto `MessageEncoding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilitate l&#39;autenticazione HTTP di base eseguendo le seguenti operazioni:

      * Assegnare il nome utente del modulo AEM al campo `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Ottenere il documento PDF crittografato.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF crittografato e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà `System.IO.FileStream` dell&#39;oggetto `Length`.
   * Compilare l&#39;array di byte con i dati del flusso richiamando il metodo `Read` dell&#39;oggetto `System.IO.FileStream` e passando l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando il contenuto dell&#39;array di byte al membro di dati `BLOB` dell&#39;oggetto `MTOM`.

1. Determinare il tipo di crittografia.

   * Richiamare il metodo `EncryptionServiceClient` dell&#39;oggetto `getPDFEncryption` e passare l&#39;oggetto `BLOB` che contiene il documento PDF. Questo metodo restituisce un oggetto `EncryptionTypeResult`.
   * Ottenere il valore del metodo di dati `EncryptionTypeResult` dell&#39;oggetto `encryptionType`. Ad esempio, se il documento PDF è protetto con crittografia basata su password, il valore di questo membro dati è `EncryptionType.PASSWORD`.

**Consulta anche**

[Riepilogo dei passaggi](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Chiamata  AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chiamata  AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)