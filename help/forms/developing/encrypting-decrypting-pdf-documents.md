---
title: Crittografia e decrittografia di documenti PDF
seo-title: Crittografia e decrittografia di documenti PDF
description: Utilizza il servizio di crittografia per crittografare e decrittografare i documenti. Le attività del servizio di cifratura includono la cifratura di un documento PDF con una password, la cifratura di un documento PDF con un certificato, la rimozione della cifratura basata su password da un documento PDF, la rimozione della cifratura basata su certificato da un documento PDF, lo sblocco del documento PDF per consentire l’esecuzione di altre operazioni di servizio e la determinazione del tipo di cifratura di un documento PDF protetto.
seo-description: Utilizza il servizio di crittografia per crittografare e decrittografare i documenti. Le attività del servizio di cifratura includono la cifratura di un documento PDF con una password, la cifratura di un documento PDF con un certificato, la rimozione della cifratura basata su password da un documento PDF, la rimozione della cifratura basata su certificato da un documento PDF, lo sblocco del documento PDF per consentire l’esecuzione di altre operazioni di servizio e la determinazione del tipo di cifratura di un documento PDF protetto.
uuid: 4e4e2716-c21f-4bfe-ae7a-7e91442414ef
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 5e4bda3a-5648-4c0f-b2f8-bdbebb88f537
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '8259'
ht-degree: 0%

---


# Crittografia e decrittografia di documenti PDF {#encrypting-and-decrypting-pdf-documents}

**Esempi ed esempi in questo documento sono solo per AEM Forms in ambiente JEE.**

**Informazioni sul servizio di crittografia**

Il servizio di cifratura consente di cifrare e decrittografare i documenti. Quando un documento viene crittografato, il suo contenuto diventa illeggibile. Un utente autorizzato può decrittografare il documento per ottenere l&#39;accesso ai contenuti. Se un documento PDF è crittografato con una password, è necessario specificare la password aperta prima di poter visualizzare il documento in Adobe Reader o Adobe Acrobat. Analogamente, se un documento PDF è crittografato con un certificato, l’utente deve decrittografare il documento PDF con la chiave pubblica corrispondente al certificato (chiave privata) utilizzato per cifrare il documento PDF.

Puoi eseguire queste attività utilizzando il servizio di cifratura:

* Crittografare un documento PDF con una password. (Vedere [Cifratura di documenti PDF con una password](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password).)
* Cifrare un documento PDF con un certificato. (Vedere [Cifratura di documenti PDF con certificati](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates).)
* Rimuovere la crittografia basata su password da un documento PDF. (Vedere [Rimozione della crittografia della password](encrypting-decrypting-pdf-documents.md#removing-password-encryption).)
* Rimuovere la cifratura basata su certificato da un documento PDF. (Vedere [Rimozione della crittografia basata su certificato](encrypting-decrypting-pdf-documents.md#removing-certificate-based-encryption).)
* Sblocca il documento PDF in modo da poter eseguire altre operazioni di servizio. Ad esempio, dopo lo sblocco di un documento PDF crittografato con password, è possibile apporvi una firma digitale. (Consultare [Sblocco di documenti PDF crittografati](encrypting-decrypting-pdf-documents.md#unlocking-encrypted-pdf-documents).)
* Determinare il tipo di crittografia di un documento PDF protetto. (Consultare [Determinazione del tipo di cifratura](encrypting-decrypting-pdf-documents.md#determining-encryption-type).)

>[!NOTE]
>
>Per ulteriori informazioni sul servizio di cifratura, consulta [Guida di riferimento dei servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Cifratura di documenti PDF con password {#encrypting-pdf-documents-with-a-password}

Quando si crittografa un documento PDF con una password, l’utente deve specificare la password per aprire il documento PDF in Adobe Reader o Acrobat. Inoltre, prima di poter eseguire un’altra operazione AEM Forms, ad esempio la firma digitale del documento PDF, è necessario sbloccare un documento PDF crittografato con password.

>[!NOTE]
>
>Se carichi un documento PDF crittografato nell’archivio AEM Forms, non sarà possibile decrittografare il documento PDF ed estrarre il contenuto XDP. È consigliabile non crittografare un documento prima di caricarlo nell’archivio AEM Forms. (Vedere [Risorse di scrittura](/help/forms/developing/aem-forms-repository.md#writing-resources).)

>[!NOTE]
>
>Per ulteriori informazioni sul servizio di cifratura, consulta [Guida di riferimento dei servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary-of-steps}

Per crittografare un documento PDF con una password, eseguire le operazioni seguenti:

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

Per crittografare un documento PDF con una password, è necessario specificare quattro valori, inclusi due valori password. Il primo valore password viene utilizzato per cifrare il documento PDF e deve essere specificato all’apertura del documento PDF. Il secondo valore della password, denominato valore della password master, viene utilizzato per rimuovere la crittografia dal documento PDF. I valori delle password sono sensibili all&#39;uso di maiuscole e minuscole e questi due valori non possono essere gli stessi.

È necessario specificare le risorse del documento PDF da crittografare. È possibile crittografare l’intero documento PDF, tutti gli elementi eccetto i metadati del documento o solo gli allegati del documento. Se si crittografano solo gli allegati del documento, all&#39;utente viene richiesta una password quando tenta di accedere agli allegati del file.

Durante la cifratura di un documento PDF, è possibile specificare le autorizzazioni associate al documento protetto. Specificando le autorizzazioni, è possibile controllare le azioni che un utente che apre un documento PDF crittografato con password può eseguire. Ad esempio, per estrarre correttamente i dati del modulo, è necessario impostare le seguenti autorizzazioni:

* PASSWORD_EDIT_ADD
* PASSWORD_EDIT_MODIFY

>[!NOTE]
>
>Le autorizzazioni sono specificate come valori di enumerazione `PasswordEncryptionPermission`.

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

### Crittografare un documento PDF utilizzando l&#39;API Java {#encrypt-a-pdf-document-using-the-java-api}

Crittografare un documento PDF con una password utilizzando l’API di cifratura (Java):

1. Includi file di progetto.

   Includi file JAR client, come adobe-encryption-client.jar, nel percorso di classe del progetto Java.

1. Creare un’API client di crittografia.

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `EncryptionServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Ottenere un documento PDF da crittografare.

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento PDF da crittografare utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del documento PDF.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Impostare le opzioni di esecuzione della crittografia.

   * Creare un oggetto `PasswordEncryptionOptionSpec` richiamando il relativo costruttore.
   * Specificare le risorse del documento PDF da crittografare richiamando il metodo `setEncryptOption` dell&#39;oggetto `PasswordEncryptionOptionSpec` e passando un valore di enumerazione `PasswordEncryptionOption` che specifica le risorse del documento da crittografare. Ad esempio, per cifrare l’intero documento PDF, inclusi i relativi metadati e i relativi allegati, specificare `PasswordEncryptionOption.ALL`.
   * Creare un oggetto `java.util.List` che memorizza le autorizzazioni di crittografia utilizzando il costruttore `ArrayList`.
   * Specificare un&#39;autorizzazione richiamando il metodo `java.util.List` dell&#39;oggetto `add` e passando un valore di enumerazione corrispondente all&#39;autorizzazione che si desidera impostare. Ad esempio, per impostare l’autorizzazione che consente all’utente di copiare i dati presenti nel documento PDF, specificare `PasswordEncryptionPermission.PASSWORD_EDIT_COPY`. (Ripeti questo passaggio per ogni autorizzazione da impostare).
   * Specifica l’opzione di compatibilità Acrobat richiamando il metodo `setCompatability` dell’oggetto `PasswordEncryptionOptionSpec` e passando un valore di enumerazione che specifica il livello di compatibilità Acrobat. Ad esempio, puoi specificare `PasswordEncryptionCompatability.ACRO_7`.
   * Specificare il valore della password che consente all&#39;utente di aprire il documento PDF crittografato richiamando il metodo `setDocumentOpenPassword` dell&#39;oggetto `PasswordEncryptionOptionSpec` e passando un valore di stringa che rappresenta la password aperta.
   * Specificare il valore della password master che consente all&#39;utente di rimuovere la crittografia dal documento PDF richiamando il metodo `setPermissionPassword` dell&#39;oggetto `PasswordEncryptionOptionSpec` e passando un valore di stringa che rappresenta la password master.

1. Aggiungi la password.

   Crittografare il documento PDF richiamando il metodo `encryptPDFUsingPassword` dell’oggetto `EncryptionServiceClient` e passando i seguenti valori:

   * L&#39;oggetto `com.adobe.idp.Document` che contiene il documento PDF da crittografare con la password.
   * L&#39;oggetto `PasswordEncryptionOptionSpec` contenente le opzioni di esecuzione della crittografia.

   Il metodo `encryptPDFUsingPassword` restituisce un oggetto `com.adobe.idp.Document` contenente un documento PDF crittografato con password.

1. Salvare il documento PDF crittografato come file PDF.

   * Crea un oggetto `java.io.File` e assicurati che l&#39;estensione del file sia .pdf.
   * Richiamare il metodo `copyToFile` dell&#39;oggetto `com.adobe.idp.Document` per copiare nel file il contenuto dell&#39;oggetto `com.adobe.idp.Document`. Assicurarsi di utilizzare l&#39;oggetto `com.adobe.idp.Document` restituito dal metodo `encryptPDFUsingPassword`.

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
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Creare un oggetto API client di crittografia.

   * Creare un oggetto `EncryptionServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `EncryptionServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/EncryptionService?WSDL`). Non è necessario utilizzare l&#39;attributo `lc_version` . Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Crea un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `EncryptionServiceClient.Endpoint.Binding` . Imposta il valore restituito su `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegna il nome utente del modulo di AEM al campo `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore della password corrispondente al campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Ottenere un documento PDF da crittografare.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare un documento PDF crittografato con una password.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF da cifrare e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni dell&#39;array di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare l’array di byte con i dati del flusso richiamando il metodo `Read` dell’oggetto `System.IO.FileStream` e passando l’array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando il contenuto dell&#39;array di byte al membro dati `BLOB` dell&#39;oggetto `MTOM`.

1. Impostare le opzioni di esecuzione della crittografia.

   * Creare un oggetto `PasswordEncryptionOptionSpec` utilizzando il relativo costruttore.
   * Specificare le risorse del documento PDF da crittografare assegnando un valore di enumerazione `PasswordEncryptionOption` al membro dati `PasswordEncryptionOptionSpec` dell&#39;oggetto `encryptOption`. Per cifrare l’intero PDF, inclusi i relativi metadati e i relativi allegati, assegna `PasswordEncryptionOption.ALL` a questo membro dati.
   * Specifica l’opzione di compatibilità Acrobat assegnando un valore di enumerazione `PasswordEncryptionCompatability` al membro dati `PasswordEncryptionOptionSpec` dell’oggetto `compatability`. Ad esempio, assegna `PasswordEncryptionCompatability.ACRO_7` a questo membro dati.
   * Specificare il valore della password che consente all&#39;utente di aprire il documento PDF crittografato assegnando un valore di stringa che rappresenta la password aperta al membro dati `documentOpenPassword` dell&#39;oggetto `PasswordEncryptionOptionSpec`.
   * Specificare il valore della password che consente all&#39;utente di rimuovere la cifratura dal documento PDF assegnando un valore stringa che rappresenta la password master al membro dati `permissionPassword` dell&#39;oggetto `PasswordEncryptionOptionSpec`.

1. Aggiungi la password.

   Crittografare il documento PDF richiamando il metodo `encryptPDFUsingPassword` dell’oggetto `EncryptionServiceClient` e passando i seguenti valori:

   * L&#39;oggetto `BLOB` che contiene il documento PDF da crittografare con la password.
   * L&#39;oggetto `PasswordEncryptionOptionSpec` contenente le opzioni di esecuzione della crittografia.

   Il metodo `encryptPDFUsingPassword` restituisce un oggetto `BLOB` contenente un documento PDF crittografato con password.

1. Salvare il documento PDF crittografato come file PDF.

   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF protetto.
   * Creare una matrice di byte che memorizza il contenuto dei dati dell&#39;oggetto `BLOB` restituito dal metodo `encryptPDFUsingPassword`. Compilare l&#39;array di byte ottenendo il valore del membro dati `BLOB` dell&#39;oggetto `MTOM`.
   * Creare un oggetto `System.IO.BinaryWriter` richiamandone il costruttore e passando l&#39;oggetto `System.IO.FileStream`.
   * Scrivi il contenuto dell’array di byte in un file PDF richiamando il metodo `Write` dell’oggetto `System.IO.BinaryWriter` e passando l’array di byte.

**Consulta anche**

[Riepilogo dei passaggi](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Richiamo di AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamo di AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Cifratura di documenti PDF con certificati {#encrypting-pdf-documents-with-certificates}

La crittografia basata su certificato consente di crittografare un documento per destinatari specifici tramite la tecnologia a chiave pubblica. A diversi destinatari possono essere assegnate autorizzazioni diverse per il documento. Molti aspetti della crittografia sono resi possibili dalla tecnologia a chiave pubblica. Un algoritmo viene utilizzato per generare due numeri grandi, noti come *chiavi*, con le seguenti proprietà:

* Una chiave viene utilizzata per crittografare un set di dati. Successivamente, solo l’altra chiave può essere utilizzata per decrittografare i dati.
* È impossibile distinguere una chiave dall&#39;altra.

Una delle chiavi funge da chiave privata dell’utente. È importante che solo l’utente abbia accesso a questa chiave. L’altra chiave è la chiave pubblica dell’utente, che può essere condivisa con altri utenti.

Un certificato a chiave pubblica contiene la chiave pubblica di un utente e le informazioni di identificazione. Il formato X.509 viene utilizzato per memorizzare i certificati. I certificati sono generalmente rilasciati e firmati digitalmente da un’autorità di certificazione (CA), un’entità riconosciuta che fornisce una misura di affidabilità nella validità del certificato. I certificati hanno una data di scadenza, dopo la quale non sono più validi. Inoltre, gli elenchi di revoche di certificati (CRL) forniscono informazioni sui certificati revocati prima della data di scadenza. I LCR sono pubblicati periodicamente dalle autorità di certificazione. Lo stato di revoca di un certificato può essere recuperato anche tramite il protocollo OCSP (Online Certificate Status Protocol) in rete.

>[!NOTE]
>
>Se carichi un documento PDF crittografato nell’archivio AEM Forms, non sarà possibile decrittografare il documento PDF ed estrarre il contenuto XDP. È consigliabile non crittografare un documento prima di caricarlo nell’archivio AEM Forms. (Vedere [Risorse di scrittura](/help/forms/developing/aem-forms-repository.md#writing-resources).)

>[!NOTE]
>
>Prima di poter crittografare un documento PDF con un certificato, è necessario assicurarsi di aggiungere il certificato ad AEM Forms. Un certificato viene aggiunto tramite la console di amministrazione o a livello di programmazione utilizzando l’API di Trust Manager. (Vedere [Importazione delle credenziali tramite l&#39;API di Trust Manager](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api).)

>[!NOTE]
>
>Per ulteriori informazioni sul servizio di cifratura, consulta [Guida di riferimento dei servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-1}

Per crittografare un documento PDF con un certificato, eseguire le operazioni seguenti:

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

Per eseguire un&#39;operazione del servizio di cifratura a livello di programmazione, è necessario creare un client del servizio di cifratura. Se utilizzi l’API Java Encryption Service, crea un oggetto `EncrytionServiceClient` . Se utilizzi l’API del servizio Web Encryption Service, crea un oggetto `EncryptionServiceService` .

**Ottenere un documento PDF da crittografare**

Per eseguire la cifratura è necessario ottenere un documento PDF non crittografato. Se si tenta di proteggere un documento PDF già crittografato, viene generata un&#39;eccezione.

**Riferimento al certificato**

Per cifrare un documento PDF con un certificato, fare riferimento a un certificato utilizzato per cifrare un documento PDF. Il certificato è un file .cer, un file .crt o un file .pem. Un file PKCS#12 viene utilizzato per memorizzare le chiavi private con i certificati corrispondenti.

Durante la cifratura di un documento PDF con un certificato, specificare le autorizzazioni associate al documento protetto. Specificando le autorizzazioni, è possibile controllare le azioni che possono essere eseguite da un utente che apre un documento PDF crittografato con certificato.

**Impostare le opzioni di esecuzione della crittografia**

Specificare le risorse del documento PDF da crittografare. È possibile crittografare l’intero documento PDF, tutti gli elementi eccetto i metadati del documento o solo gli allegati del documento.

**Creare un documento PDF crittografato con certificato**

Dopo aver recuperato un documento PDF non protetto, fatto riferimento al certificato e impostato le opzioni di esecuzione, è possibile creare un documento PDF crittografato con certificato. Una volta crittografato il documento PDF, è necessario disporre della chiave pubblica corrispondente per decrittografarlo.

**Salvare il documento PDF crittografato come file PDF**

È possibile salvare il documento PDF crittografato come file PDF.

**Consulta anche**

[Crittografare un documento PDF con un certificato utilizzando l’API Java](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-with-a-certificate-using-the-java-api)

[Crittografare un documento PDF con un certificato utilizzando l’API del servizio Web](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-with-a-certificate-using-the-web-service-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API del servizio di crittografia](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[Cifratura di documenti PDF con password](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Crittografare un documento PDF con un certificato utilizzando l’API Java {#encrypt-a-pdf-document-with-a-certificate-using-the-java-api}

Crittografare un documento PDF con un certificato utilizzando l’API di cifratura (Java):

1. Includi file di progetto.

   Includi file JAR client, come adobe-encryption-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto API client di crittografia.

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `EncryptionServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Ottenere un documento PDF da crittografare.

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento PDF da crittografare utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del documento PDF.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Fai riferimento al certificato.

   * Creare un oggetto `java.util.List` che memorizza le informazioni sulle autorizzazioni utilizzando il relativo costruttore.
   * Specificare l&#39;autorizzazione associata al documento crittografato richiamando il metodo `add` dell&#39;oggetto `java.util.List` e passando un valore di enumerazione `CertificateEncryptionPermissions` che rappresenta le autorizzazioni concesse all&#39;utente che apre il documento PDF protetto. Ad esempio, per specificare tutte le autorizzazioni, passare `CertificateEncryptionPermissions.PKI_ALL_PERM`.
   * Creare un oggetto `Recipient` utilizzando il relativo costruttore.
   * Creare un oggetto `java.io.FileInputStream` che rappresenta il certificato utilizzato per cifrare il documento PDF utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del certificato.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream` che rappresenta il certificato.
   * Richiama il metodo `setX509Cert` dell&#39;oggetto `Recipient` e passa l&#39;oggetto `com.adobe.idp.Document` che contiene il certificato. (Inoltre, l&#39;oggetto `Recipient`può avere un alias di certificato Truststore o un URL LDAP come origine del certificato.)
   * Creare un oggetto `CertificateEncryptionIdentity` che memorizza le informazioni sulle autorizzazioni e sui certificati utilizzando il relativo costruttore.
   * Richiamare il metodo `setPerms` dell&#39;oggetto `CertificateEncryptionIdentity` e passare l&#39;oggetto `java.util.List` che memorizza le informazioni sulle autorizzazioni.
   * Richiamare il metodo `setRecipient` dell&#39;oggetto `CertificateEncryptionIdentity` e passare l&#39;oggetto `Recipient` che memorizza le informazioni sul certificato.
   * Creare un oggetto `java.util.List` che memorizza le informazioni sul certificato utilizzando il relativo costruttore.
   * Richiamare il metodo add dell&#39;oggetto `java.util.List` e passare l&#39;oggetto `CertificateEncryptionIdentity`. (Questo oggetto `java.util.List` viene passato come parametro al metodo `encryptPDFUsingCertificates` .)

1. Impostare le opzioni di esecuzione della crittografia.

   * Creare un oggetto `CertificateEncryptionOptionSpec` richiamando il relativo costruttore.
   * Specificare le risorse del documento PDF da crittografare richiamando il metodo `setOption` dell&#39;oggetto `CertificateEncryptionOptionSpec` e passando un valore di enumerazione `CertificateEncryptionOption` che specifica le risorse del documento da crittografare. Ad esempio, per cifrare l’intero documento PDF, inclusi i relativi metadati e i relativi allegati, specificare `CertificateEncryptionOption.ALL`.
   * Specifica l’opzione di compatibilità Acrobat richiamando il metodo `setCompat` dell’oggetto `CertificateEncryptionOptionSpec` e passando un valore di enumerazione `CertificateEncryptionCompatibility` che specifica il livello di compatibilità Acrobat. Ad esempio, puoi specificare `CertificateEncryptionCompatibility.ACRO_7`.

1. Creare un documento PDF crittografato con certificato.

   Crittografare il documento PDF con un certificato richiamando il metodo `encryptPDFUsingCertificates` dell’oggetto `EncryptionServiceClient` e passando i seguenti valori:

   * L&#39;oggetto `com.adobe.idp.Document` che contiene il documento PDF da cifrare.
   * L&#39;oggetto `java.util.List` che memorizza le informazioni sul certificato.
   * L&#39;oggetto `CertificateEncryptionOptionSpec` contenente le opzioni di esecuzione della crittografia.

   Il metodo `encryptPDFUsingCertificates` restituisce un oggetto `com.adobe.idp.Document` contenente un documento PDF crittografato con certificato.

1. Salvare il documento PDF crittografato come file PDF.

   * Crea un oggetto `java.io.File` e assicurati che l&#39;estensione del nome file sia .pdf.
   * Richiamare il metodo `copyToFile` dell&#39;oggetto `com.adobe.idp.Document` per copiare nel file il contenuto dell&#39;oggetto `com.adobe.idp.Document`. Assicurarsi di utilizzare l&#39;oggetto `com.adobe.idp.Document` restituito dal metodo `encryptPDFUsingCertificates`.

**Consulta anche**

[Riepilogo dei passaggi](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Avvio rapido (modalità SOAP): Crittografia di un documento PDF con un certificato tramite l’API Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-encrypting-a-pdf-document-with-a-certificate-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Crittografare un documento PDF con un certificato utilizzando l&#39;API del servizio Web {#encrypt-a-pdf-document-with-a-certificate-using-the-web-service-api}

Crittografare un documento PDF con un certificato utilizzando l’API di cifratura (servizio Web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurati di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Creare un oggetto API client di crittografia.

   * Creare un oggetto `EncryptionServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `EncryptionServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/EncryptionService?WSDL`). Non è necessario utilizzare l&#39;attributo `lc_version` . Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Crea un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `EncryptionServiceClient.Endpoint.Binding` . Imposta il valore restituito su `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegna il nome utente del modulo di AEM al campo `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore della password corrispondente al campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Ottenere un documento PDF da crittografare.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare un documento PDF crittografato con un certificato.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF da cifrare e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni dell&#39;array di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare l’array di byte con i dati del flusso richiamando il metodo `Read` dell’oggetto `System.IO.FileStream` e passando l’array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando la relativa proprietà `MTOM` con il contenuto dell&#39;array di byte.

1. Fai riferimento al certificato.

   * Creare un oggetto `Recipient` utilizzando il relativo costruttore. Questo oggetto memorizzerà le informazioni sul certificato.
   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. Questo oggetto `BLOB` memorizzerà il certificato che crittografa il documento PDF.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del certificato e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni dell&#39;array di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare l’array di byte con i dati del flusso richiamando il metodo `Read` dell’oggetto `System.IO.FileStream` e passando l’array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando il contenuto dell&#39;array di byte al membro dati `BLOB` dell&#39;oggetto `MTOM`.
   * Assegna l&#39;oggetto `BLOB` che memorizza il certificato al membro dati `Recipient` dell&#39;oggetto `x509Cert`.
   * Creare un oggetto `CertificateEncryptionIdentity` che memorizza le informazioni sul certificato utilizzando il relativo costruttore.
   * Assegna l&#39;oggetto `Recipient` che memorizza il certificato al membro dati del destinatario dell&#39;oggetto `CertificateEncryptionIdentity`.
   * Creare una matrice `Object` e assegnare l&#39;oggetto `CertificateEncryptionIdentity` al primo elemento dell&#39;array `Object`. Questa matrice `Object` viene passata come parametro al metodo `encryptPDFUsingCertificates` .

1. Impostare le opzioni di esecuzione della crittografia.

   * Creare un oggetto `CertificateEncryptionOptionSpec` utilizzando il relativo costruttore.
   * Specificare le risorse del documento PDF da crittografare assegnando un valore di enumerazione `CertificateEncryptionOption` al membro dati `CertificateEncryptionOptionSpec` dell&#39;oggetto `option`. Per crittografare l’intero documento PDF, inclusi i relativi metadati e i relativi allegati, assegnare `CertificateEncryptionOption.ALL` al membro dati.
   * Specifica l’opzione di compatibilità Acrobat assegnando un valore di enumerazione `CertificateEncryptionCompatibility` al membro dati `CertificateEncryptionOptionSpec` dell’oggetto `compat`. Ad esempio, assegna `CertificateEncryptionCompatibility.ACRO_7` a questo membro dati.

1. Creare un documento PDF crittografato con certificato.

   Crittografare il documento PDF con un certificato richiamando il metodo `encryptPDFUsingCertificates` dell’oggetto `EncryptionServiceService` e passando i seguenti valori:

   * L&#39;oggetto `BLOB` che contiene il documento PDF da cifrare.
   * Array `Object` in cui sono memorizzate le informazioni sul certificato.
   * L&#39;oggetto `CertificateEncryptionOptionSpec` contenente le opzioni di esecuzione della crittografia.

   Il metodo `encryptPDFUsingCertificates` restituisce un oggetto `BLOB` contenente un documento PDF crittografato con certificato.

1. Salvare il documento PDF crittografato come file PDF.

   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF protetto.
   * Creare una matrice di byte che memorizza il contenuto dei dati dell&#39;oggetto `BLOB` restituito dal metodo `encryptPDFUsingCertificates`. Compilare l&#39;array di byte ottenendo il valore del membro dati `BLOB` dell&#39;oggetto `binaryData`.
   * Creare un oggetto `System.IO.BinaryWriter` richiamandone il costruttore e passando l&#39;oggetto `System.IO.FileStream`.
   * Scrivi il contenuto dell’array di byte in un file PDF richiamando il metodo `Write` dell’oggetto `System.IO.BinaryWriter` e passando l’array di byte.

**Consulta anche**

[Riepilogo dei passaggi](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Richiamo di AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamo di AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Rimozione della crittografia basata su certificato {#removing-certificate-based-encryption}

È possibile rimuovere la cifratura basata su certificato da un documento PDF per consentire agli utenti di aprire il documento PDF in Adobe Reader o Acrobat. Per rimuovere la crittografia da un documento PDF crittografato con un certificato, è necessario fare riferimento a una chiave pubblica. Dopo la rimozione della cifratura da un documento PDF, la cifratura non è più protetta.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio di cifratura, consulta [Guida di riferimento dei servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-2}

Per rimuovere la cifratura basata su certificato da un documento PDF, eseguire le operazioni seguenti:

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

Per eseguire un&#39;operazione del servizio di cifratura a livello di programmazione, è necessario creare un client del servizio di cifratura. Se utilizzi l’API Java Encryption Service, crea un oggetto `EncrytionServiceClient` . Se utilizzi l’API del servizio Web Encryption Service, crea un oggetto `EncryptionServiceService` .

**Ottenere il documento PDF crittografato**

Per rimuovere la crittografia basata su certificato, è necessario ottenere un documento PDF crittografato. Se si tenta di rimuovere la crittografia da un documento PDF non crittografato, viene generata un&#39;eccezione. Analogamente, se si tenta di rimuovere la crittografia basata su certificato da un documento crittografato con password, viene generata un&#39;eccezione.

**Rimuovi crittografia**

Per rimuovere la cifratura basata su certificato da un documento PDF crittografato, è necessario disporre sia di un documento PDF crittografato sia della chiave privata corrispondente alla chiave utilizzata per cifrare il documento PDF. Il valore alias della chiave privata viene specificato durante la rimozione della crittografia basata su certificato da un documento PDF crittografato. Per informazioni sulla chiave pubblica, vedere [Cifratura di documenti PDF con certificati](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates).

>[!NOTE]
>
>Una chiave privata viene memorizzata nell&#39;archivio attendibilità di AEM Forms. Quando un certificato è posizionato in tale posizione, viene specificato un valore di alias.

**Salvare il documento PDF**

Dopo la rimozione della cifratura basata su certificato da un documento PDF crittografato, è possibile salvare il documento PDF come file PDF. Gli utenti possono aprire il documento PDF in Adobe Reader o Acrobat.

**Consulta anche**

[Rimuovere la crittografia basata su certificato utilizzando l’API Java](encrypting-decrypting-pdf-documents.md#remove-certificate-based-encryption-using-the-java-api)

[Rimuovere la crittografia basata su certificato utilizzando l’API del servizio Web](encrypting-decrypting-pdf-documents.md#remove-certificate-based-encryption-using-the-web-service-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API del servizio di crittografia](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

### Rimuovere la crittografia basata su certificato utilizzando l&#39;API Java {#remove-certificate-based-encryption-using-the-java-api}

È possibile rimuovere la cifratura basata su certificato da un documento PDF utilizzando l’API di cifratura (Java):

1. Includi file di progetto.

   Includi file JAR client, come adobe-encryption-client.jar, nel percorso di classe del progetto Java.

1. Crea un client del servizio di crittografia.

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `EncryptionServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Ottenere il documento PDF crittografato.

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento PDF crittografato utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del documento PDF crittografato.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Rimuovi crittografia.

   Rimuovere la crittografia basata su certificato dal documento PDF richiamando il metodo `removePDFCertificateSecurity` dell’oggetto `EncryptionServiceClient` e passando i seguenti valori:

   * L&#39;oggetto `com.adobe.idp.Document` che contiene il documento PDF crittografato.
   * Valore stringa che specifica il nome alias della chiave privata corrispondente alla chiave utilizzata per crittografare il documento PDf.

   Il metodo `removePDFCertificateSecurity` restituisce un oggetto `com.adobe.idp.Document` contenente un documento PDF non protetto.

1. Salvare il documento PDF.

   * Crea un oggetto `java.io.File` e assicurati che l&#39;estensione del file sia .pdf.
   * Richiamare il metodo `copyToFile` dell&#39;oggetto `com.adobe.idp.Document` per copiare nel file il contenuto dell&#39;oggetto `Document`. Assicurarsi di utilizzare l&#39;oggetto `com.adobe.idp.Document` restituito dal metodo `removePDFCredentialSecurity`.

**Consulta anche**

[Riepilogo dei passaggi](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Avvio rapido (modalità SOAP): Rimozione della crittografia basata su certificato tramite l’API Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-removing-certificate-based-encryption-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Rimuovere la crittografia basata su certificato utilizzando l&#39;API del servizio Web {#remove-certificate-based-encryption-using-the-web-service-api}

Rimuovi la crittografia basata su certificato utilizzando l’API di cifratura (servizio Web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurati di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Crea un client del servizio di crittografia.

   * Creare un oggetto `EncryptionServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `EncryptionServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/EncryptionService?WSDL`). Non è necessario utilizzare l&#39;attributo `lc_version` . Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Crea un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `EncryptionServiceClient.Endpoint.Binding` . Imposta il valore restituito su `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegna il nome utente del modulo di AEM al campo `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore della password corrispondente al campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Ottenere il documento PDF crittografato.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare il documento PDF crittografato.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF crittografato e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni dell&#39;array di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare l’array di byte con i dati del flusso richiamando il metodo `Read` dell’oggetto `System.IO.FileStream` e passando l’array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando il contenuto dell&#39;array di byte al membro dati `BLOB` dell&#39;oggetto `MTOM`.

1. Rimuovi crittografia.

   Richiama il metodo `removePDFCertificateSecurity` dell&#39;oggetto `EncryptionServiceClient` e passa i seguenti valori:

   * L&#39;oggetto `BLOB` che contiene i dati del flusso di file che rappresenta un documento PDF crittografato.
   * Valore stringa che specifica il nome alias della chiave pubblica corrispondente alla chiave privata utilizzata per crittografare il documento PDf.

   Il metodo `removePDFCredentialSecurity` restituisce un oggetto `BLOB` contenente un documento PDF non protetto.

1. Salvare il documento PDF.

   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF non protetto.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `BLOB` restituito dal metodo `removePDFPasswordSecurity`. Compilare l&#39;array di byte ottenendo il valore del membro dati `BLOB` dell&#39;oggetto `MTOM`.
   * Creare un oggetto `System.IO.BinaryWriter` richiamandone il costruttore e passando l&#39;oggetto `System.IO.FileStream`.
   * Scrivi il contenuto dell’array di byte in un file PDF richiamando il metodo `Write` dell’oggetto `System.IO.BinaryWriter` e passando l’array di byte.

**Consulta anche**

[Riepilogo dei passaggi](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Richiamo di AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamo di AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Rimozione della crittografia della password {#removing-password-encryption}

È possibile rimuovere la cifratura basata su password da un documento PDF per consentire agli utenti di aprire il documento PDF in Adobe Reader o Acrobat senza dover specificare una password. Dopo la rimozione della cifratura basata su password da un documento PDF, il documento non è più protetto.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio di cifratura, consulta [Guida di riferimento dei servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-3}

Per rimuovere la cifratura basata su password da un documento PDF, eseguire le operazioni seguenti:

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

Per eseguire un&#39;operazione del servizio di cifratura a livello di programmazione, è necessario creare un client del servizio di cifratura. Se utilizzi l’API Java Encryption Service, crea un oggetto `EncrytionServiceClient` . Se utilizzi l’API del servizio Web Encryption Service, crea un oggetto `EncryptionServiceService` .

**Ottenere il documento PDF crittografato**

Per rimuovere la crittografia basata su password, è necessario ottenere un documento PDF crittografato. Se si tenta di rimuovere la crittografia da un documento PDF non crittografato, viene generata un&#39;eccezione.

**Rimuovere la password**

Per rimuovere la cifratura basata su password da un documento PDF crittografato, è necessario disporre sia di un documento PDF crittografato sia di un valore password master utilizzato per rimuovere la cifratura dal documento PDF. La password utilizzata per aprire un documento PDF crittografato con password non può essere utilizzata per rimuovere la crittografia. Una password master viene specificata quando il documento PDF è crittografato con una password. (Vedere [Cifratura di documenti PDF con una password](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password).)

**Salvare il documento PDF**

Dopo la rimozione della cifratura basata su password da un documento PDF, è possibile salvare il documento PDF come file PDF. Gli utenti possono aprire il documento PDF in Adobe Reader o Acrobat senza specificare una password.

**Consulta anche**

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API del servizio di crittografia](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[Cifratura di documenti PDF con password](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Rimuovere la crittografia basata su password utilizzando l&#39;API Java {#remove-password-based-encryption-using-the-java-api}

È possibile rimuovere la cifratura basata su password da un documento PDF utilizzando l’API di cifratura (Java):

1. Includi file di progetto.

   Includi file JAR client, come adobe-encryption-client.jar, nel percorso di classe del progetto Java.

1. Crea un client del servizio di crittografia.

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `EncryptionServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Ottenere il documento PDF crittografato.

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento PDF crittografato utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del documento PDF.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Rimuovi la password.

   Rimuovere la crittografia basata su password dal documento PDF richiamando il metodo `removePDFPasswordSecurity` dell&#39;oggetto `EncryptionServiceClient` e passando i seguenti valori:

   * Un oggetto `com.adobe.idp.Document` contenente il documento PDF crittografato.
   * Valore stringa che specifica il valore della password master utilizzato per rimuovere la cifratura dal documento PDF.

   Il metodo `removePDFPasswordSecurity` restituisce un oggetto `com.adobe.idp.Document` contenente un documento PDF non protetto.

1. Salvare il documento PDF.

   * Crea un oggetto `java.io.File` e assicurati che l&#39;estensione del nome file sia .pdf.
   * Richiamare il metodo `copyToFile` dell&#39;oggetto `com.adobe.idp.Document` per copiare nel file il contenuto dell&#39;oggetto `Document`. Assicurarsi di utilizzare l&#39;oggetto `Document` restituito dal metodo `removePDFPasswordSecurity`.

**Consulta anche**

[Avvio rapido (modalità SOAP): Rimozione della crittografia basata su password tramite l’API Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-removing-password-based-encryption-using-the-java-api)

### Rimuovere la crittografia basata su password utilizzando l&#39;API del servizio Web {#remove-password-based-encryption-using-the-web-service-api}

È possibile rimuovere la crittografia basata su password utilizzando l’API di cifratura (servizio Web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurati di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Crea un client del servizio di crittografia.

   * Creare un oggetto `EncryptionServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `EncryptionServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/EncryptionService?WSDL`). Non è necessario utilizzare l&#39;attributo `lc_version` . Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Crea un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `EncryptionServiceClient.Endpoint.Binding` . Imposta il valore restituito su `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegna il nome utente del modulo di AEM al campo `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore della password corrispondente al campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Ottenere il documento PDF crittografato.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare un documento PDF crittografato con password.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF crittografato e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni dell&#39;array di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare l’array di byte con i dati del flusso richiamando il metodo `Read` dell’oggetto `System.IO.FileStream` e passando l’array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando il contenuto dell&#39;array di byte al membro dati `BLOB` dell&#39;oggetto `MTOM`.

1. Rimuovi la password.

   Richiama il metodo `removePDFPasswordSecurity` dell&#39;oggetto `EncryptionServiceService` e passa i seguenti valori:

   * L&#39;oggetto `BLOB` che contiene i dati del flusso di file che rappresenta un documento PDF crittografato.
   * Valore stringa che specifica il valore della password utilizzato per rimuovere la cifratura dal documento PDF. Questo valore viene specificato durante la cifratura del documento PDF con una password.

   Il metodo `removePDFPasswordSecurity` restituisce un oggetto `BLOB` contenente un documento PDF non protetto.

1. Salvare il documento PDF.

   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF non protetto.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `BLOB` restituito dal metodo `removePDFPasswordSecurity`. Compilare l&#39;array di byte ottenendo il valore del membro dati `BLOB` dell&#39;oggetto `MTOM`.
   * Creare un oggetto `System.IO.BinaryWriter` richiamandone il costruttore e passando l&#39;oggetto `System.IO.FileStream`.
   * Scrivi il contenuto dell’array di byte in un file PDF richiamando il metodo `Write` dell’oggetto `System.IO.BinaryWriter` e passando l’array di byte.

**Consulta anche**

[Richiamo di AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamo di AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Sblocco dei documenti PDF crittografati {#unlocking-encrypted-pdf-documents}

È necessario sbloccare un documento PDF crittografato con password o certificato prima di eseguire un’altra operazione AEM Forms. Se si tenta di eseguire un&#39;operazione su un documento PDF crittografato, verrà generata un&#39;eccezione. Dopo aver sbloccato un documento PDF crittografato, è possibile eseguire una o più operazioni su di esso. Queste operazioni possono appartenere ad altri servizi, ad esempio il servizio Acrobat Reader DC extensions.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio di cifratura, consulta [Guida di riferimento dei servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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

Per eseguire un&#39;operazione del servizio di cifratura a livello di programmazione, è necessario creare un client del servizio di cifratura. Se utilizzi l’API Java Encryption Service, crea un oggetto `EncrytionServiceClient` . Se utilizzi l’API del servizio Web Encryption Service, crea un oggetto `EncryptionServiceService` .

**Ottenere il documento PDF crittografato**

Per sbloccarlo, è necessario ottenere un documento PDF crittografato. Se si tenta di sbloccare un documento PDF non crittografato, viene generata un&#39;eccezione.

**Sblocca il documento**

Per sbloccare un documento PDF crittografato con password, è necessario disporre sia di un documento PDF crittografato sia di un valore di password utilizzato per aprire un documento PDF crittografato con password. Questo valore viene specificato durante la cifratura del documento PDF con una password. (Vedere [Cifratura di documenti PDF con una password](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password).)

Per sbloccare un documento PDF crittografato con certificato, è necessario disporre sia di un documento PDF crittografato sia del valore alias della chiave pubblica corrispondente alla chiave privata utilizzata per cifrare il documento PDF.

**Eseguire un’operazione AEM Forms**

Quando un documento PDF crittografato viene sbloccato, è possibile eseguire un&#39;altra operazione del servizio, ad esempio l&#39;applicazione di diritti di utilizzo. Questa operazione appartiene al servizio Acrobat Reader DC Extensions.

**Consulta anche**

[Sblocca un documento PDF crittografato utilizzando l’API Java](encrypting-decrypting-pdf-documents.md#unlock-an-encrypted-pdf-document-using-the-java-api)

[Sblocca un documento PDF crittografato utilizzando l’API del servizio Web](encrypting-decrypting-pdf-documents.md#unlock-an-encrypted-pdf-document-using-the-web-service-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API del servizio di crittografia](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

### Sblocca un documento PDF crittografato utilizzando l&#39;API Java {#unlock-an-encrypted-pdf-document-using-the-java-api}

Sblocca un documento PDF crittografato utilizzando l’API di cifratura (Java):

1. Includi file di progetto.

   Includi file JAR client, come adobe-encryption-client.jar, nel percorso di classe del progetto Java.

1. Crea un client del servizio di crittografia.

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `EncryptionServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Ottenere il documento PDF crittografato.

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento PDF crittografato utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del documento PDF crittografato.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Sblocca il documento.

   Sblocca un documento PDF crittografato richiamando il metodo `unlockPDFUsingPassword` dell&#39;oggetto `EncryptionServiceClient` o `unlockPDFUsingCredential`.

   Per sbloccare un documento PDF crittografato con una password, richiama il metodo `unlockPDFUsingPassword` e passa i seguenti valori:

   * Un oggetto `com.adobe.idp.Document` che contiene il documento PDF crittografato con password.
   * Valore stringa che specifica il valore della password utilizzato per aprire un documento PDF crittografato con password. Questo valore viene specificato durante la cifratura del documento PDF con una password.

   Per sbloccare un documento PDF crittografato con un certificato, richiamare il metodo `unlockPDFUsingCredential` e passare i seguenti valori:

   * Un oggetto `com.adobe.idp.Document` contenente il documento PDF crittografato con certificato.
   * Valore stringa che specifica il nome alias della chiave pubblica corrispondente alla chiave privata utilizzata per cifrare il documento PDF.

   I metodi `unlockPDFUsingPassword` e `unlockPDFUsingCredential` restituiscono entrambi un oggetto `com.adobe.idp.Document` passato a un altro metodo Java di AEM Forms per eseguire un’operazione.

1. Esegui un’operazione AEM Forms.

   Eseguire un&#39;operazione AEM Forms sul documento PDF sbloccato per soddisfare i requisiti aziendali. Ad esempio, supponendo di voler applicare diritti di utilizzo a un documento PDF sbloccato, passare l&#39;oggetto `com.adobe.idp.Document` restituito dai metodi `unlockPDFUsingPassword` o `unlockPDFUsingCredential` al metodo `ReaderExtensionsServiceClient` dell&#39;oggetto `applyUsageRights`.

**Consulta anche**

[Riepilogo dei passaggi](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Avvio rapido (modalità SOAP): Sblocco di un documento PDF crittografato tramite l’API Java ](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-unlocking-an-encrypted-pdf-document-using-the-java-api)  (modalità SOAP)

[Applicazione dei diritti di utilizzo ai documenti PDF](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Sblocca un documento PDF crittografato utilizzando l&#39;API del servizio Web {#unlock-an-encrypted-pdf-document-using-the-web-service-api}

Sblocca un documento PDF crittografato utilizzando l’API di cifratura (servizio Web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurati di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Crea un client del servizio di crittografia.

   * Creare un oggetto `EncryptionServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `EncryptionServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/EncryptionService?WSDL`). Non è necessario utilizzare l&#39;attributo `lc_version` . Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Crea un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `EncryptionServiceClient.Endpoint.Binding` . Imposta il valore restituito su `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegna il nome utente del modulo di AEM al campo `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore della password corrispondente al campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Ottenere un documento PDF crittografato.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF crittografato e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni dell&#39;array di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare l’array di byte con i dati del flusso richiamando il metodo `Read` dell’oggetto `System.IO.FileStream` e passando l’array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando il contenuto dell&#39;array di byte al membro dati `BLOB` dell&#39;oggetto `MTOM`.

1. Sblocca il documento.

   Sblocca un documento PDF crittografato richiamando il metodo `unlockPDFUsingPassword` dell&#39;oggetto `EncryptionServiceClient` o `unlockPDFUsingCredential`.

   Per sbloccare un documento PDF crittografato con una password, richiama il metodo `unlockPDFUsingPassword` e passa i seguenti valori:

   * Un oggetto `BLOB` che contiene il documento PDF crittografato con password.
   * Valore stringa che specifica il valore della password utilizzato per aprire un documento PDF crittografato con password. Questo valore viene specificato durante la cifratura del documento PDF con una password.

   Per sbloccare un documento PDF crittografato con un certificato, richiamare il metodo `unlockPDFUsingCredential` e passare i seguenti valori:

   * Un oggetto `BLOB` contenente il documento PDF crittografato con certificato.
   * Valore stringa che specifica il nome alias della chiave pubblica corrispondente alla chiave privata utilizzata per crittografare il documento PDf.

   I metodi `unlockPDFUsingPassword` e `unlockPDFUsingCredential` restituiscono entrambi un oggetto `com.adobe.idp.Document` passato a un altro metodo AEM Forms per eseguire un&#39;operazione.

1. Esegui un’operazione AEM Forms.

   Eseguire un&#39;operazione AEM Forms sul documento PDF sbloccato per soddisfare i requisiti aziendali. Ad esempio, supponendo di voler applicare diritti di utilizzo al documento PDF sbloccato, passare l&#39;oggetto `BLOB` restituito dai metodi `unlockPDFUsingPassword` o `unlockPDFUsingCredential` al metodo `ReaderExtensionsServiceClient` dell&#39;oggetto `applyUsageRights`.

**Consulta anche**

[Riepilogo dei passaggi](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Richiamo di AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamo di AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Determinazione del tipo di crittografia {#determining-encryption-type}

È possibile determinare programmaticamente il tipo di crittografia che protegge un documento PDF utilizzando l’API Java Encryption Service o il servizio Web Encryption Service API. A volte è necessario determinare in modo dinamico se un documento PDF è crittografato e, in tal caso, il tipo di crittografia. Ad esempio, è possibile determinare se un documento PDF è protetto tramite crittografia basata su password o criteri di Rights Management.

Un documento PDF può essere protetto dai seguenti tipi di cifratura:

* Crittografia basata su password
* Crittografia basata su certificato
* Criterio creato dal servizio Rights Management
* Un altro tipo di crittografia

>[!NOTE]
>
>Per ulteriori informazioni sul servizio di cifratura, consulta [Guida di riferimento dei servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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

Per eseguire un&#39;operazione del servizio di cifratura a livello di programmazione, è necessario creare un client del servizio di cifratura. Se utilizzi l’API Java Encryption Service, crea un oggetto `EncrytionServiceClient` . Se utilizzi l’API del servizio Web Encryption Service, crea un oggetto `EncryptionServiceService` .

**Ottenere il documento PDF crittografato**

È necessario ottenere un documento PDF per determinare il tipo di crittografia che lo protegge.

**Determinare il tipo di crittografia**

È possibile determinare il tipo di crittografia che protegge un documento PDF. Se il documento PDF non è protetto, il servizio di cifratura informa che il documento PDF non è protetto.

**Consulta anche**

[Determinare il tipo di crittografia utilizzando l’API Java](encrypting-decrypting-pdf-documents.md#determine-the-encryption-type-using-the-java-api)

[Determinare il tipo di crittografia utilizzando l’API del servizio Web](encrypting-decrypting-pdf-documents.md#determine-the-encryption-type-using-the-web-service-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API del servizio di crittografia](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[Protezione dei documenti con i criteri](/help/forms/developing/protecting-documents-policies.md#protecting-documents-with-policies)

### Determina il tipo di crittografia utilizzando l&#39;API Java {#determine-the-encryption-type-using-the-java-api}

Determinare il tipo di crittografia che protegge un documento PDF utilizzando l’API di cifratura (Java):

1. Includi file di progetto.

   Includi file JAR client, come adobe-encryption-client.jar, nel percorso di classe del progetto Java.

1. Crea un client di servizio.

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `EncryptionServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Ottenere il documento PDF crittografato.

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento PDF utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del documento PDF.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Determina il tipo di crittografia.

   * Determinare il tipo di crittografia richiamando il metodo `getPDFEncryption` dell’oggetto `EncryptionServiceClient` e passando l’oggetto `com.adobe.idp.Document` che contiene il documento PDF. Questo metodo restituisce un oggetto `EncryptionTypeResult`.
   * Richiama il metodo `getEncryptionType` dell&#39;oggetto `EncryptionTypeResult`. Questo metodo restituisce un valore enum `EncryptionType` che specifica il tipo di crittografia. Ad esempio, se il documento PDF è protetto con crittografia basata su password, questo metodo restituisce `EncryptionType.PASSWORD`.

**Consulta anche**

[Riepilogo dei passaggi](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Avvio rapido (modalità SOAP): Determinazione del tipo di crittografia tramite l’API Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-determining-encryption-type-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Determinare il tipo di crittografia utilizzando l&#39;API del servizio Web {#determine-the-encryption-type-using-the-web-service-api}

Determinare il tipo di crittografia che protegge un documento PDF utilizzando l’API di cifratura (servizio Web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurati di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Crea un client di servizio.

   * Creare un oggetto `EncryptionServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `EncryptionServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/EncryptionService?WSDL`). Non è necessario utilizzare l&#39;attributo `lc_version` . Questo attributo viene utilizzato quando si crea un riferimento a un servizio.)
   * Crea un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `EncryptionServiceClient.Endpoint.Binding` . Imposta il valore restituito su `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegna il nome utente del modulo di AEM al campo `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore della password corrispondente al campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Ottenere il documento PDF crittografato.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF crittografato e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni dell&#39;array di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare l’array di byte con i dati del flusso richiamando il metodo `Read` dell’oggetto `System.IO.FileStream` e passando l’array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando il contenuto dell&#39;array di byte al membro dati `BLOB` dell&#39;oggetto `MTOM`.

1. Determina il tipo di crittografia.

   * Richiamare il metodo `getPDFEncryption` dell&#39;oggetto `EncryptionServiceClient` e passare l&#39;oggetto `BLOB` che contiene il documento PDF. Questo metodo restituisce un oggetto `EncryptionTypeResult`.
   * Ottenere il valore del metodo dati `encryptionType` dell&#39;oggetto `EncryptionTypeResult`. Ad esempio, se il documento PDF è protetto con crittografia basata su password, il valore di questo membro dati è `EncryptionType.PASSWORD`.

**Consulta anche**

[Riepilogo dei passaggi](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Richiamo di AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamo di AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)