---
title: Assegnazione dei diritti di utilizzo
seo-title: Assegnazione dei diritti di utilizzo
description: 'null'
seo-description: 'null'
uuid: 8c2020df-ea3c-49fa-916f-38a458f40d2b
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9e8db506-9ace-4e1f-8a7b-c4e9b15dde7e
translation-type: tm+mt
source-git-commit: 413af4ef9bc3652e05da78d622183bcf20a8bee7

---


# Assegnazione dei diritti di utilizzo {#assigning-usage-rights}

## Informazioni su Acrobat Reader DC extensions Service {#about-the-acrobat-reader-dc-extensions-service}

Il servizio di estensioni Acrobat Reader DC consente alla vostra azienda di condividere facilmente i documenti PDF interattivi estendendo le funzionalità di Adobe Reader. Il servizio di estensione Acrobat Reader DC supporta completamente qualsiasi documento PDF, fino a PDF 1.7 incluso. Funziona con Adobe Reader 7.0 e versioni successive. Il servizio consente di aggiungere diritti di utilizzo a un documento PDF, attivando le funzioni normalmente non disponibili all&#39;apertura di un documento PDF tramite Adobe Reader. Gli utenti di terze parti non richiedono software o plug-in aggiuntivi per lavorare con i documenti abilitati per i diritti.

È possibile eseguire le seguenti attività utilizzando il servizio di estensioni Acrobat Reader DC:

* Applicazione dei diritti di utilizzo ai documenti PDF. Per ulteriori informazioni, vedere [Applicazione dei diritti di utilizzo ai documenti](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)PDF.
* Rimuovere i diritti di utilizzo dai documenti PDF. Per ulteriori informazioni, vedere [Rimozione dei diritti di utilizzo dai documenti](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)PDF.
* Recuperare i dettagli delle credenziali. Per ulteriori informazioni, vedere [Recupero di informazioni](assigning-usage-rights.md#retrieving-credential-information)sulle credenziali.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio delle estensioni Acrobat Reader DC, consultate Guida di riferimento [ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Applicazione dei diritti di utilizzo ai documenti PDF {#applying-usage-rights-to-pdf-documents}

È possibile applicare diritti di utilizzo ai documenti PDF utilizzando l&#39;API Java Client e il servizio Web Acrobat Reader DC Extensions. I diritti di utilizzo si riferiscono a funzionalità disponibili per impostazione predefinita in Acrobat ma non in Adobe Reader, ad esempio la possibilità di aggiungere commenti a un modulo o di compilare campi modulo e salvare il modulo. I documenti PDF a cui sono stati applicati diritti di utilizzo sono denominati documenti abilitati per i diritti. L&#39;utente che apre un documento con diritti in Adobe Reader può eseguire operazioni abilitate per tale documento specifico.

>[!NOTE]
>
>Quando si applicano diritti di utilizzo ai documenti PDF utilizzando il `applyUsageRights` metodo, che fa parte dell&#39;API Java, è possibile impostare il `isModeFinal` parametro dell&#39; `ReaderExtensionsOptionSpec` oggetto su `false`. Ciò impedisce l&#39;aggiornamento del contatore di elaborazione dei moduli e migliora le prestazioni. Se non si desidera aggiornare il contatore dei moduli elaborati, è consigliabile impostare il `isModeFinal` parametro su `false`.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio delle estensioni Acrobat Reader DC, consultate Guida di riferimento [ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary-of-steps}

Per applicare diritti di utilizzo a un documento PDF, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un oggetto Client di estensioni Acrobat Reader DC.
1. Recuperare un documento PDF.
1. Specificate i diritti di utilizzo da applicare.
1. Applicare diritti di utilizzo al documento PDF.
1. Salvare il documento PDF con diritti.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se state creando un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate servizi Web, accertatevi di includere i file proxy.

**Creazione di un oggetto Client di estensioni Acrobat Reader DC**

Per eseguire a livello di programmazione un&#39;operazione di servizio di estensione di Acrobat Reader DC, è necessario creare un oggetto client del servizio di estensione di Acrobat Reader DC. Se si utilizza l&#39;API Java delle estensioni Acrobat Reader DC, creare un `ReaderExtensionsServiceClient` oggetto. Se si utilizza l&#39;API del servizio Web delle estensioni Acrobat Reader DC, creare un `ReaderExtensionsServiceService` oggetto.

**Recupero di un documento PDF**

È necessario recuperare un documento PDF per applicare i diritti di utilizzo. I documenti PDF con diritti di utilizzo contengono un dizionario dei diritti di utilizzo. Quando Adobe Reader apre un documento contenente tale dizionario, abilita i diritti di utilizzo specificati nel dizionario solo per tale documento. Se il documento non contiene un dizionario dei diritti di utilizzo, il servizio di estensione Acrobat Reader DC ne crea uno. Se contiene già un dizionario, il servizio di estensione Acrobat Reader DC sovrascrive i diritti di utilizzo esistenti con quelli specificati. Il dizionario specifica quali diritti di utilizzo sono abilitati. Quando un utente apre il documento in Adobe Reader, sono consentiti solo i diritti di utilizzo specificati nel dizionario.

**Specificare i diritti di utilizzo da applicare**

I diritti di utilizzo che è possibile impostare sono determinati da una credenziale acquistata da Adobe Systems Incorporated. Le credenziali forniscono in genere l&#39;autorizzazione per impostare un gruppo di diritti di utilizzo correlati, ad esempio quelli relativi ai moduli interattivi. Ciascuna credenziale consente di creare un certo numero di documenti PDF abilitati per i diritti. Una credenziale di valutazione dà il diritto di creare un numero illimitato di bozze di documenti.

>[!NOTE]
>
>Se si tenta di assegnare un diritto di utilizzo non consentito dalla credenziale, si causerà un&#39;eccezione.

**Applicazione dei diritti di utilizzo al documento PDF**

Per applicare i diritti di utilizzo a un documento PDF, è necessario fare riferimento all&#39;alias della credenziale utilizzata per applicare i diritti di utilizzo. In genere, durante l&#39;installazione di AEM Forms viene installata una credenziale. È inoltre necessario specificare il documento PDF a cui vengono applicati i diritti di utilizzo. Per informazioni sulla configurazione di una credenziale, consultate la guida all&#39;installazione e alla distribuzione per il server delle applicazioni.

**Salvare il documento PDF con diritti**

Dopo che il servizio di estensione Acrobat Reader DC ha applicato i diritti di utilizzo a un documento PDF, è possibile salvare il documento PDF con diritti come file PDF.

**Consulta anche**

[Applicazione dei diritti di utilizzo tramite l&#39;API Java](assigning-usage-rights.md#apply-usage-rights-using-the-java-api)

[Applicazione dei diritti di utilizzo tramite l&#39;API del servizio Web](assigning-usage-rights.md#apply-usage-rights-using-the-web-service-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Guida rapida di Acrobat Reader DC Extensions Service API](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

### Applicazione dei diritti di utilizzo tramite l&#39;API Java {#apply-usage-rights-using-the-java-api}

Per applicare i diritti di utilizzo a un documento PDF, utilizzare l’API Acrobat Reader DC Extensions (Java):

1. Includi file di progetto

   Includete file JAR client, ad esempio adobe-reader-extensions-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto Client di estensioni Acrobat Reader DC.

   * Creare un `ServiceClientFactory` oggetto che contenga proprietà di connessione.
   * Creare un `ReaderExtensionsServiceClient` oggetto utilizzando il relativo costruttore e passando l&#39; `ServiceClientFactory` oggetto.

1. Recuperare un documento PDF.

   * Creare un oggetto `java.io.FileInputStream` che rappresenti il documento PDF utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del documento PDF.
   * Creare un `com.adobe.idp.Document` oggetto utilizzando il relativo costruttore e passando l&#39; `java.io.FileInputStream` oggetto.

1. Specificate i diritti di utilizzo da applicare.

   * Creare un `UsageRights` oggetto che rappresenti i diritti di utilizzo utilizzando il relativo costruttore.
   * Per ogni diritto di utilizzo da applicare, richiamare un metodo corrispondente che appartiene all&#39; `UsageRights` oggetto. Ad esempio, per aggiungere il diritto di `enableFormFillIn` utilizzo, richiamare il metodo dell&#39; `UsageRights` oggetto `enableFormFillIn` e passare `true`. Ripetete questo passaggio per ogni diritto di utilizzo da applicare.

1. Applicare diritti di utilizzo al documento PDF.

   * Creare un `ReaderExtensionsOptionSpec` oggetto utilizzando il relativo costruttore. Questo oggetto contiene le opzioni di esecuzione richieste dal servizio delle estensioni Acrobat Reader DC. Quando si richiama questo costruttore, è necessario specificare i seguenti valori:

      * L&#39; `UsageRights` oggetto che contiene i diritti di utilizzo da applicare al documento.
      * Una stringa che specifica un messaggio visualizzato dall&#39;utente all&#39;apertura del documento PDF con diritti in Adobe Reader 7.x. Questo messaggio non viene visualizzato in Adobe Reader 8.0.
   * Per applicare i diritti di utilizzo al documento PDF, richiamare il metodo dell&#39; `ReaderExtensionsServiceClient` oggetto `applyUsageRights` e passare i seguenti valori:

      * L&#39; `com.adobe.idp.Document` oggetto che contiene il documento PDF a cui sono applicati i diritti di utilizzo.
      * Valore stringa che specifica l&#39;alias della credenziale che consente di applicare diritti di utilizzo.
      * Un valore di stringa che specifica il valore della password corrispondente. (Attualmente questo parametro viene ignorato. Potete passare `null`.)
   * L&#39; `ReaderExtensionsOptionSpec` oggetto che contiene le opzioni di esecuzione.
   Il `applyUsageRights` metodo restituisce un `com.adobe.idp.Document` oggetto che contiene il documento PDF abilitato per i diritti.

1. Salvare il documento PDF con diritti.

   * Create un `java.io.File` oggetto e accertatevi che l&#39;estensione sia .pdf.
   * Richiamare il metodo dell&#39; `com.adobe.idp.Document` oggetto `copyToFile` per copiare il contenuto dell&#39; `com.adobe.idp.Document` oggetto nel file (assicurarsi di utilizzare l&#39; `com.adobe.idp.Document` oggetto restituito dal `applyUsageRights` metodo).

**Consulta anche**

[Applicazione dei diritti di utilizzo ai documenti PDF](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[Avvio rapido (modalità SOAP):applicazione dei diritti di utilizzo tramite l&#39;API Java](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-applying-usage-rights-using-the-java-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Applicazione dei diritti di utilizzo tramite l&#39;API del servizio Web {#apply-usage-rights-using-the-web-service-api}

Per applicare i diritti di utilizzo a un documento PDF, utilizzare l’API Acrobat Reader DC Extensions (servizio Web):

1. Includere i file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituire `localhost` con l&#39;indirizzo IP del server in cui è installato AEM Forms.

1. Creare un oggetto Client di estensioni Acrobat Reader DC.

   * Creare un `ReaderExtensionsServiceClient` oggetto utilizzando il relativo costruttore predefinito.
   * Creare un `ReaderExtensionsServiceClient.Endpoint.Address` oggetto utilizzando il `System.ServiceModel.EndpointAddress` costruttore. Passa un valore di stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`. Assicurarsi di specificare `?blob=mtom`.)
   * Creare un `System.ServiceModel.BasicHttpBinding` oggetto ottenendo il valore del `ReaderExtensionsServiceClient.Endpoint.Binding` campo. Inserite il valore restituito in `BasicHttpBinding`.
   * Impostare il campo `System.ServiceModel.BasicHttpBinding` dell&#39; `MessageEncoding` oggetto su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilitate l&#39;autenticazione HTTP di base eseguendo le seguenti operazioni:

      * Assegnare il nome utente dei moduli AEM al campo `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recuperare un documento PDF.

   * Creare un `BLOB` oggetto utilizzando il relativo costruttore. L&#39; `BLOB` oggetto viene utilizzato per memorizzare un documento PDF a cui sono applicati i diritti di utilizzo.
   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto dell&#39; `System.IO.FileStream` oggetto. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà dell&#39; `System.IO.FileStream` oggetto `Length` .
   * Compilare l&#39;array di byte con i dati del flusso richiamando il metodo dell&#39; `System.IO.FileStream` oggetto `Read` . Passare l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39; `BLOB` oggetto assegnandone `MTOM` la proprietà con il contenuto dell&#39;array di byte.

1. Specificate i diritti di utilizzo da applicare.

   * Creare un `UsageRights` oggetto che rappresenti i diritti di utilizzo utilizzando il relativo costruttore.
   * Per ogni diritto di utilizzo da applicare, assegnare il valore `true` al membro di dati corrispondente che appartiene all&#39; `UsageRights` oggetto. Ad esempio, per aggiungere il diritto di `enableFormFillIn` utilizzo, assegnare `true` al membro dati dell&#39; `UsageRights` oggetto `enableFormFillIn` . Ripetete questo passaggio per ogni diritto di utilizzo da applicare.

1. Applicare diritti di utilizzo al documento PDF.

   * Creare un `ReaderExtensionsOptionSpec` oggetto utilizzando il relativo costruttore. Questo oggetto contiene le opzioni di esecuzione richieste dal servizio delle estensioni Acrobat Reader DC.
   * Assegnare l&#39; `UsageRights` oggetto al membro dati dell&#39; `ReaderExtensionsOptionSpec` oggetto `usageRights` .
   * Assegnare un valore stringa che specifica il messaggio visualizzato dall&#39;utente all&#39;apertura del documento PDF con diritti in Adobe Reader al membro `ReaderExtensionsOptionSpec` dati `message` dell&#39;oggetto.
   * Per applicare i diritti di utilizzo al documento PDF, richiamare il metodo dell&#39; `ReaderExtensionsServiceClient` oggetto `applyUsageRights` e passare i seguenti valori:

      * L&#39; `BLOB` oggetto che contiene il documento PDF a cui sono applicati i diritti di utilizzo.
      * Valore stringa che specifica l&#39;alias della credenziale che consente di applicare diritti di utilizzo.
      * Un valore di stringa che specifica il valore della password corrispondente. (Attualmente questo parametro viene ignorato. Potete passare `null`.)
   * L&#39; `ReaderExtensionsOptionSpec` oggetto che contiene le opzioni di esecuzione.
   Il `applyUsageRights` metodo restituisce un `BLOB` oggetto che contiene il documento PDF abilitato per i diritti.

1. Salvare il documento PDF con diritti.

   * Creare un `System.IO.FileStream` oggetto richiamandone il costruttore. Passa un valore di stringa che rappresenta la posizione del file del documento PDF abilitato per i diritti.
   * Creare un array di byte che memorizza il contenuto dei dati dell&#39; `BLOB` oggetto restituito dal `applyUsageRights` metodo. Compilare l&#39;array di byte ottenendo il valore del membro `BLOB` dati dell&#39; `MTOM` oggetto.
   * Creare un `System.IO.BinaryWriter` oggetto richiamando il relativo costruttore e passando l&#39; `System.IO.FileStream` oggetto.
   * Scrivere il contenuto dell&#39;array di byte in un file PDF richiamando il metodo dell&#39; `System.IO.BinaryWriter` oggetto `Write` e passando l&#39;array di byte.

**Consulta anche**

[Applicazione dei diritti di utilizzo ai documenti PDF](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[Attivazione di moduli AEM tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamo di moduli AEM con SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Rimozione dei diritti di utilizzo dai documenti PDF {#removing-usage-rights-from-pdf-documents}

Potete rimuovere i diritti di utilizzo da un documento con diritti. È inoltre necessario rimuovere i diritti di utilizzo da un documento PDF con diritti per eseguire altre operazioni su AEM Forms. Ad esempio, è necessario firmare (o certificare) digitalmente un documento PDF prima di impostare i diritti di utilizzo. Pertanto, se si desidera eseguire operazioni su un documento con diritti, è necessario rimuovere i diritti di utilizzo dal documento PDF, eseguire altre operazioni, ad esempio firmare digitalmente il documento e quindi riapplicare i diritti di utilizzo al documento.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio delle estensioni Acrobat Reader DC, consultate Guida di riferimento [ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-1}

Per rimuovere i diritti di utilizzo da un documento PDF abilitato per i diritti, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un oggetto Client di estensioni Acrobat Reader DC.
1. Recuperare un documento PDF abilitato per diritti.
1. Rimuovere i diritti di utilizzo dal documento PDF.
1. Salvare il documento PDF.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se state creando un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate servizi Web, accertatevi di includere i file proxy.

**Creazione di un oggetto Client di estensioni Acrobat Reader DC**

Prima di poter eseguire a livello di programmazione un&#39;operazione del servizio di estensione di Acrobat Reader DC, è necessario creare un oggetto client del servizio di estensione di Acrobat Reader DC. Se utilizzate l&#39;API Java, create un `ReaderExtensionsServiceClient` oggetto. Se si utilizza l&#39;API del servizio Web delle estensioni Acrobat Reader DC, creare un `ReaderExtensionsServiceService` oggetto.

**Recupero di un documento PDF con diritti**

Per rimuovere i diritti di utilizzo, recuperate un documento PDF abilitato per i diritti.

**Rimozione dei diritti di utilizzo dal documento PDF**

Dopo aver ottenuto un documento PDF con diritti, potete rimuovere i diritti di utilizzo. Dopo aver rimosso i diritti di utilizzo, il documento PDF non disporrà di alcuna funzionalità aggiuntiva durante la visualizzazione in Adobe Reader.

**Salvare il documento PDF**

È possibile salvare come file PDF il documento PDF che non contiene più diritti di utilizzo. Una volta salvato il file come PDF, il documento PDF può essere visualizzato in Adobe Reader o Acrobat.

**Consulta anche**

[Rimuovere i diritti di utilizzo mediante l&#39;API Java](assigning-usage-rights.md#remove-usage-rights-using-the-java-api)

[Rimozione dei diritti di utilizzo tramite l&#39;API del servizio Web](assigning-usage-rights.md#remove-usage-rights-using-the-web-service-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Guida rapida di Acrobat Reader DC Extensions Service API](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

[Applicazione dei diritti di utilizzo ai documenti PDF](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

### Rimuovere i diritti di utilizzo mediante l&#39;API Java {#remove-usage-rights-using-the-java-api}

Per rimuovere i diritti di utilizzo da un documento PDF con diritti, utilizzare l’API delle estensioni Acrobat Reader DC (Java):

1. Includere i file di progetto.

   Includete file JAR client, ad esempio adobe-reader-extensions-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto Client di estensioni Acrobat Reader DC.

   Creare un `ReaderExtensionsServiceClient` oggetto utilizzando il relativo costruttore e passando un `ServiceClientFactory` oggetto che contiene le proprietà di connessione.

1. Recuperare un documento PDF.

   * Creare un oggetto `java.io.FileInputStream` che rappresenti il documento PDF con diritti, utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del documento PDF.
   * Creare un `com.adobe.idp.Document` oggetto utilizzando il relativo costruttore e passando l&#39; `java.io.FileInputStream` oggetto.

1. Rimuovere i diritti di utilizzo dal documento PDF.

   Rimuovere i diritti di utilizzo dal documento PDF richiamando il `ReaderExtensionsServiceClient` metodo dell&#39; `removeUsageRights` oggetto e passando l&#39; `com.adobe.idp.Document` oggetto che contiene il documento PDF abilitato per i diritti. Questo metodo restituisce un `com.adobe.idp.Document` oggetto contenente un documento PDF che non dispone dei diritti di utilizzo.

1. Applicare diritti di utilizzo al documento PDF.

   * Creare un `java.io.File` oggetto e assicurarsi che l&#39;estensione del file sia .PDF.
   * Richiamare il metodo dell&#39; `Document` oggetto `copyToFile` per copiare il contenuto dell&#39; `Document` oggetto nel file (assicurarsi di utilizzare l&#39; `Document` oggetto restituito dal `removeUsageRights` metodo).

**Consulta anche**

[Rimozione dei diritti di utilizzo dai documenti PDF](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)

[Avvio rapido (modalità SOAP): Rimozione di diritti di utilizzo da un documento PDF tramite l&#39;API Java](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-removing-usage-rights-from-a-pdf-document-using-the-java-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Rimozione dei diritti di utilizzo tramite l&#39;API del servizio Web {#remove-usage-rights-using-the-web-service-api}

Per rimuovere i diritti di utilizzo da un documento PDF con diritti, utilizzare l’API delle estensioni Acrobat Reader DC (servizio Web):

1. Includere i file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituire `localhost` con l&#39;indirizzo IP del server in cui è installato AEM Forms.

1. Creare un oggetto Client di estensioni Acrobat Reader DC.

   * Creare un `ReaderExtensionsServiceClient` oggetto utilizzando il relativo costruttore predefinito.
   * Creare un `ReaderExtensionsServiceClient.Endpoint.Address` oggetto utilizzando il `System.ServiceModel.EndpointAddress` costruttore. Passa un valore di stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`. Assicurarsi di specificare `?blob=mtom`.)
   * Creare un `System.ServiceModel.BasicHttpBinding` oggetto ottenendo il valore del `ReaderExtensionsServiceClient.Endpoint.Binding` campo. Inserite il valore restituito in `BasicHttpBinding`.
   * Impostare il campo `System.ServiceModel.BasicHttpBinding` dell&#39; `MessageEncoding` oggetto su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilitate l&#39;autenticazione HTTP di base eseguendo le seguenti operazioni:

      * Assegnare il nome utente dei moduli AEM al campo `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recuperare un documento PDF.

   * Creare un `BLOB` oggetto utilizzando il relativo costruttore. L&#39; `BLOB` oggetto viene utilizzato per memorizzare il documento PDF con diritti abilitati dal quale vengono rimossi i diritti di utilizzo.
   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto dell&#39; `System.IO.FileStream` oggetto. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà dell&#39; `System.IO.FileStream` oggetto `Length` .
   * Compilare l&#39;array di byte con i dati del flusso richiamando il `System.IO.FileStream` `Read` metodo dell&#39;oggetto e passando l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39; `BLOB` oggetto assegnandone `MTOM` la proprietà con il contenuto dell&#39;array di byte.

1. Rimuovere i diritti di utilizzo dal documento PDF.

   Rimuovere i diritti di utilizzo dal documento PDF richiamando il `ReaderExtensionsServiceClient` metodo dell&#39; `removeUsageRights` oggetto e passando l&#39; `BLOB` oggetto che contiene il documento PDF abilitato per i diritti. Questo metodo restituisce un `BLOB` oggetto contenente un documento PDF che non dispone dei diritti di utilizzo.

1. Applicare diritti di utilizzo al documento PDF.

   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file PDF.
   * Creare un array di byte che memorizza il contenuto dei dati dell&#39; `BLOB` oggetto restituito dal `removeUsageRights` metodo. Compilare l&#39;array di byte ottenendo il valore del membro `BLOB` dati dell&#39; `MTOM` oggetto.
   * Creare un `System.IO.BinaryWriter` oggetto richiamando il relativo costruttore e passando l&#39; `System.IO.FileStream` oggetto.

**Consulta anche**

[Rimozione dei diritti di utilizzo dai documenti PDF](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)

[Attivazione di moduli AEM tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamo di moduli AEM con SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Recupero delle informazioni sulle credenziali {#retrieving-credential-information}

È possibile recuperare informazioni sulle credenziali utilizzate per applicare diritti di utilizzo a un documento PDF abilitato per i diritti. Recuperando informazioni su una credenziale, è possibile ottenere informazioni quali la data dopo la quale il certificato non è più valido.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio delle estensioni Acrobat Reader DC, consultate Guida di riferimento [ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-2}

Per recuperare informazioni sulle credenziali utilizzate per applicare diritti di utilizzo a un documento PDF, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un oggetto Client di estensioni Acrobat Reader DC.
1. Recuperare un documento PDF abilitato per diritti.
1. Recuperare informazioni sulla credenziale.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se state creando un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate servizi Web, accertatevi di includere i file proxy.

**Creazione di un oggetto Client di estensioni Acrobat Reader DC**

Prima di poter eseguire a livello di programmazione un&#39;operazione del servizio di estensione di Acrobat Reader DC, è necessario creare un oggetto client del servizio di estensione di Acrobat Reader DC. Se utilizzate l&#39;API Java, create un `ReaderExtensionsServiceClient` oggetto. Se si utilizza l&#39;API del servizio Web delle estensioni Acrobat Reader DC, creare un `ReaderExtensionsServiceService` oggetto.

**Recupero di un documento PDF con diritti**

Per recuperare informazioni sulle credenziali, è necessario recuperare un documento PDF abilitato per i diritti. È inoltre possibile recuperare informazioni su una credenziale specificandone l&#39;alias; tuttavia, se si desidera recuperare informazioni su una credenziale utilizzata per applicare diritti di utilizzo a un documento PDF con diritti specifici, è necessario recuperare il documento.

**Recupero di informazioni sulla credenziale**

Dopo aver ottenuto un documento PDF con diritti, potete ottenere informazioni sulle credenziali utilizzate per applicarvi i diritti di utilizzo. È possibile ottenere le seguenti informazioni sulla credenziale:

* Messaggio visualizzato in Adobe Reader all’apertura del documento PDF con diritti.
* Data dopo la quale la credenziale non è più valida.
* Data prima della quale la credenziale non è valida.
* I diritti di utilizzo impostati per questo documento PDF con diritti.
* Il numero di volte in cui è stata utilizzata la credenziale.

**Consulta anche**

[Rimuovere i diritti di utilizzo mediante l&#39;API Java](assigning-usage-rights.md#remove-usage-rights-using-the-java-api)

[Rimozione dei diritti di utilizzo tramite l&#39;API del servizio Web](assigning-usage-rights.md#remove-usage-rights-using-the-web-service-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Guida rapida di Acrobat Reader DC Extensions Service API](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

### Recupero delle informazioni sulle credenziali tramite l&#39;API Java {#retrieve-credential-information-using-the-java-api}

Ottenere le informazioni sulle credenziali utilizzando l’API delle estensioni Acrobat Reader DC (Java):

1. Includere i file di progetto.

   Includete file JAR client, ad esempio adobe-reader-extensions-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto Client di estensioni Acrobat Reader DC.

   Creare un `ReaderExtensionsServiceClient` oggetto utilizzando il relativo costruttore e passando un `ServiceClientFactory` oggetto che contiene le proprietà di connessione.

1. Recuperare un documento PDF.

   * Creare un oggetto `java.io.FileInputStream` che rappresenti il documento PDF abilitato per i diritti utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del documento PDF abilitato per i diritti.
   * Creare un `com.adobe.idp.Document` oggetto utilizzando il relativo costruttore e passando l&#39; `java.io.FileInputStream` oggetto.

1. Rimuovere i diritti di utilizzo dal documento PDF.

   * Recuperare informazioni sulle credenziali utilizzate per applicare diritti di utilizzo al documento PDF richiamando il metodo dell&#39; `ReaderExtensionsServiceClient` oggetto `getDocumentUsageRights` e passando l&#39; `com.adobe.idp.Document` oggetto che contiene il documento PDF abilitato per i diritti. Questo metodo restituisce un `GetUsageRightsResult` oggetto che contiene informazioni sulle credenziali.
   * Recuperare la data dopo la quale la credenziale non è più valida richiamando il `GetUsageRightsResult` metodo dell&#39;oggetto `getNotAfter` . Questo metodo restituisce un oggetto `java.util.Date` che rappresenta la data dopo la quale la credenziale non è più valida.
   * Per recuperare il messaggio visualizzato in Adobe Reader all&#39;apertura del documento PDF con diritti, è necessario richiamare il `GetUsageRightsResult` metodo `getMessage` dell&#39;oggetto. Questo metodo restituisce un valore di stringa che rappresenta il messaggio.

**Consulta anche**

[Recupero delle informazioni sulle credenziali](assigning-usage-rights.md#retrieving-credential-information)

[Avvio rapido (modalità SOAP): Recupero delle informazioni sulle credenziali tramite l&#39;API Java](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-retrieving-credential-information-using-the-java-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Recupero delle informazioni sulle credenziali tramite l&#39;API del servizio Web {#retrieve-credential-information-using-the-web-service-api}

Recuperare le informazioni sulle credenziali utilizzando l’API delle estensioni Acrobat Reader DC (servizio Web):

1. Includere i file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituire `localhost` con l&#39;indirizzo IP del server in cui è installato AEM Forms.

1. Creare un oggetto Client di estensioni Acrobat Reader DC.

   * Creare un `ReaderExtensionsServiceClient` oggetto utilizzando il relativo costruttore predefinito.
   * Creare un `ReaderExtensionsServiceClient.Endpoint.Address` oggetto utilizzando il `System.ServiceModel.EndpointAddress` costruttore. Passa un valore di stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`. Assicurarsi di specificare `?blob=mtom`.)
   * Creare un `System.ServiceModel.BasicHttpBinding` oggetto ottenendo il valore del `ReaderExtensionsServiceClient.Endpoint.Binding` campo. Inserite il valore restituito in `BasicHttpBinding`.
   * Impostare il campo `System.ServiceModel.BasicHttpBinding` dell&#39; `MessageEncoding` oggetto su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilitate l&#39;autenticazione HTTP di base eseguendo le seguenti operazioni:

      * Assegnare il nome utente dei moduli AEM al campo `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recuperare un documento PDF.

   * Creare un `BLOB` oggetto utilizzando il relativo costruttore. L&#39; `BLOB` oggetto viene utilizzato per memorizzare un documento PDF abilitato per i diritti.
   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF abilitato per i diritti e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto dell&#39; `System.IO.FileStream` oggetto. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà dell&#39; `System.IO.FileStream` oggetto `Length` .
   * Compilare l&#39;array di byte con i dati del flusso richiamando il `System.IO.FileStream` `Read` metodo dell&#39;oggetto e passando l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39; `BLOB` oggetto assegnandone `MTOM` la proprietà con il contenuto dell&#39;array di byte.

1. Rimuovere i diritti di utilizzo dal documento PDF.

   * Recuperare informazioni sulle credenziali utilizzate per applicare diritti di utilizzo al documento PDF richiamando il metodo dell&#39; `ReaderExtensionsServiceClient` oggetto `getDocumentUsageRights` e passando l&#39; `com.adobe.idp.Document` oggetto che contiene il documento PDF abilitato per i diritti. Questo metodo restituisce un `GetUsageRightsResult` oggetto che contiene informazioni sulle credenziali.
   * Recuperare la data dopo la quale la credenziale non è più valida ottenendo il valore del membro `GetUsageRightsResult` dati dell&#39; `notAfter` oggetto. Il tipo di dati di questo membro è `System.DateTime`.
   * Per ottenere il messaggio visualizzato quando il documento PDF con diritti è aperto in Adobe Reader, è necessario recuperare il valore del membro `GetUsageRightsResult` dati `message` dell&#39;oggetto. Il tipo di dati di questo membro è una stringa.
   * Recuperare il numero di volte in cui la credenziale viene utilizzata ottenendo il valore del membro `GetUsageRightsResult` dati dell&#39; `useCount` oggetto. Il tipo di dati di questo membro è un numero intero.

**Consulta anche**

[Recupero delle informazioni sulle credenziali](assigning-usage-rights.md#retrieving-credential-information)

[Attivazione di moduli AEM tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamo di moduli AEM con SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
