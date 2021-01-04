---
title: Assegnazione dei diritti di utilizzo
seo-title: Assegnazione dei diritti di utilizzo
description: Utilizzate l'API Java Client e l'API Web Service di Acrobat Reader DC Extensions per applicare e rimuovere i diritti di utilizzo dai documenti PDF.
seo-description: Utilizzate l'API Java Client e l'API Web Service di Acrobat Reader DC Extensions per applicare e rimuovere i diritti di utilizzo dai documenti PDF.
uuid: 8c2020df-ea3c-49fa-916f-38a458f40d2b
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9e8db506-9ace-4e1f-8a7b-c4e9b15dde7e
translation-type: tm+mt
source-git-commit: 07889ead2ae402b5fb738ca08c7efe076ef33e44
workflow-type: tm+mt
source-wordcount: '3937'
ht-degree: 0%

---


# Assegnazione di diritti di utilizzo {#assigning-usage-rights}

## Informazioni su Acrobat Reader DC extensions Service {#about-the-acrobat-reader-dc-extensions-service}

Il servizio di estensione Acrobat Reader DC consente alla vostra azienda di condividere facilmente documenti PDF interattivi estendendo le funzionalità di  Adobe Reader. Il servizio di estensione Acrobat Reader DC supporta completamente qualsiasi documento PDF, fino a PDF 1.7 incluso. Funziona con  Adobe Reader 7.0 e versioni successive. Il servizio aggiunge i diritti di utilizzo a un documento PDF, attivando le funzioni normalmente non disponibili quando un documento PDF viene aperto tramite  Adobe Reader. Gli utenti di terze parti non richiedono software o plug-in aggiuntivi per lavorare con i documenti abilitati per i diritti.

È possibile eseguire le seguenti attività utilizzando il servizio di estensione Acrobat Reader DC:

* Applicazione dei diritti di utilizzo ai documenti PDF. Per ulteriori informazioni, vedere [Applicazione dei diritti di utilizzo ai documenti PDF](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents).
* Rimuovere i diritti di utilizzo dai documenti PDF. Per ulteriori informazioni, vedere [Rimozione dei diritti di utilizzo dai documenti PDF](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents).
* Recuperare i dettagli delle credenziali. Per informazioni, vedere [Recupero di informazioni sulle credenziali](assigning-usage-rights.md#retrieving-credential-information).

>[!NOTE]
>
>Per ulteriori informazioni sul servizio delle estensioni Acrobat Reader DC, vedere [Guida di riferimento dei servizi per  AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Applicazione dei diritti di utilizzo ai documenti PDF {#applying-usage-rights-to-pdf-documents}

Potete applicare i diritti di utilizzo ai documenti PDF utilizzando l&#39;API Java Client e il servizio Web di Acrobat Reader DC Extensions. I diritti di utilizzo si riferiscono a funzionalità disponibili per impostazione predefinita in  Acrobat ma non in  Adobe Reader, ad esempio la possibilità di aggiungere commenti a un modulo o di compilare campi modulo e salvare il modulo. I documenti PDF a cui sono stati applicati diritti di utilizzo sono denominati documenti abilitati per i diritti. Un utente che apre un documento con diritti in  Adobe Reader può eseguire operazioni abilitate per tale documento specifico.

>[!NOTE]
>
>Quando si applicano diritti di utilizzo ai documenti PDF utilizzando il metodo `applyUsageRights`, che fa parte dell&#39;API Java, è possibile impostare il parametro `isModeFinal` dell&#39;oggetto `ReaderExtensionsOptionSpec` su `false`. Ciò impedisce l&#39;aggiornamento del contatore di elaborazione dei moduli e migliora le prestazioni. Se non si desidera aggiornare il contatore dei moduli elaborati, è consigliabile impostare il parametro `isModeFinal` su `false`.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio delle estensioni Acrobat Reader DC, vedere [Guida di riferimento dei servizi per  AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary-of-steps}

Per applicare diritti di utilizzo a un documento PDF, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un oggetto client con estensioni Acrobat Reader DC.
1. Recuperare un documento PDF.
1. Specificate i diritti di utilizzo da applicare.
1. Applicare i diritti di utilizzo al documento PDF.
1. Salvare il documento PDF con diritti.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se state creando un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate servizi Web, accertatevi di includere i file proxy.

**Creare un oggetto client con estensioni Acrobat Reader DC**

Per eseguire un&#39;operazione di Acrobat Reader DC Extension Service a livello di programmazione, è necessario creare un oggetto client del servizio di estensione Acrobat Reader DC. Se utilizzate l&#39;API Java delle estensioni Acrobat Reader DC, create un oggetto `ReaderExtensionsServiceClient`. Se utilizzate l&#39;API del servizio Web con estensione Acrobat Reader DC, create un oggetto `ReaderExtensionsServiceService`.

**Recupero di un documento PDF**

È necessario recuperare un documento PDF per applicare i diritti di utilizzo. I documenti PDF con diritti di utilizzo contengono un dizionario dei diritti di utilizzo. Quando  Adobe Reader apre un documento contenente tale dizionario, attiva i diritti di utilizzo specificati nel dizionario solo per tale documento. Se il documento non contiene un dizionario dei diritti di utilizzo, il servizio di estensione Acrobat Reader DC ne crea uno. Se contiene già un dizionario, il servizio di estensione Acrobat Reader DC sovrascrive i diritti di utilizzo esistenti con quelli specificati. Il dizionario specifica quali diritti di utilizzo sono abilitati. Quando un utente apre il documento in  Adobe Reader, sono consentiti solo i diritti di utilizzo specificati nel dizionario.

**Specificare i diritti di utilizzo da applicare**

I diritti di utilizzo che è possibile impostare sono determinati da una credenziale acquistata da Adobe Systems Incorporated. Le credenziali forniscono in genere l&#39;autorizzazione per impostare un gruppo di diritti di utilizzo correlati, ad esempio quelli relativi ai moduli interattivi. Ciascuna credenziale consente di creare un certo numero di documenti PDF abilitati per i diritti. Una credenziale di valutazione dà il diritto di creare un numero illimitato di bozze di documenti.

>[!NOTE]
>
>Se si tenta di assegnare un diritto di utilizzo non consentito dalla credenziale, si causerà un&#39;eccezione.

**Applicazione dei diritti di utilizzo al documento PDF**

Per applicare diritti di utilizzo a un documento PDF, è necessario fare riferimento all&#39;alias della credenziale utilizzata per applicare diritti di utilizzo (una credenziale viene in genere installata durante l&#39;installazione di  AEM Forms). È inoltre necessario specificare il documento PDF a cui vengono applicati i diritti di utilizzo. Per informazioni sulla configurazione di una credenziale, consultate la guida all&#39;installazione e alla distribuzione per il server delle applicazioni.

**Salvare il documento PDF con diritti**

Dopo che il servizio di estensione Acrobat Reader DC applica i diritti di utilizzo a un documento PDF, è possibile salvare il documento PDF abilitato per i diritti come file PDF.

**Consulta anche**

[Applicazione dei diritti di utilizzo tramite l&#39;API Java](assigning-usage-rights.md#apply-usage-rights-using-the-java-api)

[Applicazione dei diritti di utilizzo tramite l&#39;API del servizio Web](assigning-usage-rights.md#apply-usage-rights-using-the-web-service-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido di Acrobat Reader DC Extensions Service API](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

### Applicazione dei diritti di utilizzo tramite l&#39;API Java {#apply-usage-rights-using-the-java-api}

Applicazione dei diritti di utilizzo a un documento PDF tramite l&#39;API Acrobat Reader DC Extensions (Java):

1. Includi file di progetto

   Includete file JAR client, ad esempio adobe-reader-extensions-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto client con estensioni Acrobat Reader DC.

   * Creare un oggetto `ServiceClientFactory` che contiene le proprietà di connessione.
   * Creare un oggetto `ReaderExtensionsServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Recuperare un documento PDF.

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento PDF utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del documento PDF.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Specificate i diritti di utilizzo da applicare.

   * Creare un oggetto `UsageRights` che rappresenti i diritti di utilizzo utilizzando il relativo costruttore.
   * Per ogni diritto di utilizzo da applicare, richiamare un metodo corrispondente che appartiene all&#39;oggetto `UsageRights`. Ad esempio, per aggiungere il diritto di utilizzo `enableFormFillIn`, richiamare il metodo `UsageRights` dell&#39;oggetto `enableFormFillIn` e passare `true`. Ripetete questo passaggio per ogni diritto di utilizzo da applicare.

1. Applicare i diritti di utilizzo al documento PDF.

   * Creare un oggetto `ReaderExtensionsOptionSpec` utilizzando il relativo costruttore. Questo oggetto contiene le opzioni di esecuzione richieste dal servizio di estensione Acrobat Reader DC. Quando si richiama questo costruttore, è necessario specificare i seguenti valori:

      * L&#39;oggetto `UsageRights` che contiene i diritti di utilizzo da applicare al documento.
      * Una valore di stringa che specifica un messaggio visualizzato dall&#39;utente all&#39;apertura in  Adobe Reader 7.x del documento PDF abilitato per i diritti. Questo messaggio non viene visualizzato in  Adobe Reader 8.0.
   * Per applicare i diritti di utilizzo al documento PDF, richiamare il metodo `ReaderExtensionsServiceClient` dell&#39;oggetto &lt;a1/> e passare i valori seguenti:`applyUsageRights`

      * L&#39;oggetto `com.adobe.idp.Document` che contiene il documento PDF a cui sono applicati i diritti di utilizzo.
      * Valore stringa che specifica l&#39;alias della credenziale che consente di applicare diritti di utilizzo.
      * Un valore di stringa che specifica il valore della password corrispondente. (Attualmente questo parametro viene ignorato. È possibile passare `null`.
   * L&#39;oggetto `ReaderExtensionsOptionSpec` che contiene le opzioni di esecuzione.

   Il metodo `applyUsageRights` restituisce un oggetto `com.adobe.idp.Document` che contiene il documento PDF abilitato per i diritti.

1. Salvare il documento PDF con diritti.

   * Create un oggetto `java.io.File` e accertatevi che l&#39;estensione del file sia .pdf.
   * Richiamare il metodo `com.adobe.idp.Document` dell&#39;oggetto `copyToFile` per copiare nel file il contenuto dell&#39;oggetto `com.adobe.idp.Document` (assicurarsi di utilizzare l&#39;oggetto `com.adobe.idp.Document` restituito dal metodo `applyUsageRights`).

**Consulta anche**

[Applicazione dei diritti di utilizzo ai documenti PDF](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[Avvio rapido (modalità SOAP):applicazione dei diritti di utilizzo tramite l&#39;API Java](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-applying-usage-rights-using-the-java-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Applicazione dei diritti di utilizzo tramite l&#39;API del servizio Web {#apply-usage-rights-using-the-web-service-api}

Applicazione dei diritti di utilizzo a un documento PDF tramite l&#39;API delle estensioni Acrobat Reader DC (servizio Web):

1. Includere i file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituire `localhost` con l&#39;indirizzo IP del server che ospita  AEM Forms.

1. Creare un oggetto client con estensioni Acrobat Reader DC.

   * Creare un oggetto `ReaderExtensionsServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `ReaderExtensionsServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passate un valore di stringa che specifica il WSDL al servizio AEM Forms  (ad esempio, `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`). Assicurarsi di specificare `?blob=mtom`.
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `ReaderExtensionsServiceClient.Endpoint.Binding`. Inserite il valore restituito in `BasicHttpBinding`.
   * Impostare il campo `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto `MessageEncoding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilitate l&#39;autenticazione HTTP di base eseguendo le seguenti operazioni:

      * Assegnare il nome utente del modulo AEM al campo `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recuperare un documento PDF.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare un documento PDF a cui vengono applicati i diritti di utilizzo.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà `System.IO.FileStream` dell&#39;oggetto `Length`.
   * Compilare l&#39;array di byte con i dati del flusso richiamando il metodo `System.IO.FileStream` dell&#39;oggetto `Read`. Passare l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnandone la proprietà `MTOM` con il contenuto dell&#39;array di byte.

1. Specificate i diritti di utilizzo da applicare.

   * Creare un oggetto `UsageRights` che rappresenti i diritti di utilizzo utilizzando il relativo costruttore.
   * Per ogni diritto di utilizzo da applicare, assegnare il valore `true` al membro di dati corrispondente che appartiene all&#39;oggetto `UsageRights`. Ad esempio, per aggiungere il diritto di utilizzo `enableFormFillIn`, assegnare `true` al membro di dati `UsageRights` dell&#39;oggetto `enableFormFillIn`. Ripetete questo passaggio per ogni diritto di utilizzo da applicare.

1. Applicare i diritti di utilizzo al documento PDF.

   * Creare un oggetto `ReaderExtensionsOptionSpec` utilizzando il relativo costruttore. Questo oggetto contiene le opzioni di esecuzione richieste dal servizio di estensione Acrobat Reader DC.
   * Assegnare l&#39;oggetto `UsageRights` al membro di dati `ReaderExtensionsOptionSpec` dell&#39;oggetto `usageRights`.
   * Assegnare un valore di stringa che specifica il messaggio visualizzato dall&#39;utente all&#39;apertura del documento PDF con diritti in  Adobe Reader al membro di dati `ReaderExtensionsOptionSpec` dell&#39;oggetto `message`.
   * Per applicare i diritti di utilizzo al documento PDF, richiamare il metodo `ReaderExtensionsServiceClient` dell&#39;oggetto &lt;a1/> e passare i valori seguenti:`applyUsageRights`

      * L&#39;oggetto `BLOB` che contiene il documento PDF a cui sono applicati i diritti di utilizzo.
      * Valore stringa che specifica l&#39;alias della credenziale che consente di applicare diritti di utilizzo.
      * Un valore di stringa che specifica il valore della password corrispondente. (Attualmente questo parametro viene ignorato. È possibile passare `null`.
   * L&#39;oggetto `ReaderExtensionsOptionSpec` che contiene le opzioni di esecuzione.

   Il metodo `applyUsageRights` restituisce un oggetto `BLOB` che contiene il documento PDF abilitato per i diritti.

1. Salvare il documento PDF con diritti.

   * Creare un oggetto `System.IO.FileStream` richiamandone il costruttore. Passa un valore di stringa che rappresenta la posizione del file del documento PDF abilitato per i diritti.
   * Creare un array di byte che memorizza il contenuto dei dati dell&#39;oggetto `BLOB` restituito dal metodo `applyUsageRights`. Compilare l&#39;array di byte ottenendo il valore del membro di dati `BLOB` dell&#39;oggetto `MTOM`.
   * Creare un oggetto `System.IO.BinaryWriter` richiamandone il costruttore e passando l&#39;oggetto `System.IO.FileStream`.
   * Scrivere il contenuto dell&#39;array di byte in un file PDF richiamando il metodo `System.IO.BinaryWriter` dell&#39;oggetto `Write` e passando l&#39;array di byte.

**Consulta anche**

[Applicazione dei diritti di utilizzo ai documenti PDF](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[Chiamata  AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chiamata  AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Rimozione dei diritti di utilizzo dai documenti PDF {#removing-usage-rights-from-pdf-documents}

Potete rimuovere i diritti di utilizzo da un documento con diritti. La rimozione dei diritti di utilizzo da un documento PDF con diritti è necessaria anche per eseguire altre operazioni AEM Forms su di esso . Ad esempio, è necessario firmare (o certificare) digitalmente un documento PDF prima di impostare i diritti di utilizzo. Pertanto, se si desidera eseguire operazioni su un documento con diritti, è necessario rimuovere i diritti di utilizzo dal documento PDF, eseguire altre operazioni, ad esempio firmare digitalmente il documento e quindi riapplicare i diritti di utilizzo al documento.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio delle estensioni Acrobat Reader DC, vedere [Guida di riferimento dei servizi per  AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-1}

Per rimuovere i diritti di utilizzo da un documento PDF abilitato per i diritti, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un oggetto client con estensioni Acrobat Reader DC.
1. Recuperare un documento PDF abilitato per diritti.
1. Rimuovere i diritti di utilizzo dal documento PDF.
1. Salvare il documento PDF.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se state creando un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate servizi Web, accertatevi di includere i file proxy.

**Creare un oggetto client con estensioni Acrobat Reader DC**

Prima di eseguire un&#39;operazione del servizio di estensione Acrobat Reader DC a livello di programmazione, è necessario creare un oggetto client del servizio di estensione Acrobat Reader DC. Se utilizzate l&#39;API Java, create un oggetto `ReaderExtensionsServiceClient`. Se utilizzate l&#39;API del servizio Web con estensione Acrobat Reader DC, create un oggetto `ReaderExtensionsServiceService`.

**Recupero di un documento PDF con diritti**

Per rimuovere i diritti di utilizzo, recuperate un documento PDF abilitato per i diritti.

**Rimozione dei diritti di utilizzo dal documento PDF**

Dopo aver ottenuto un documento PDF con diritti, potete rimuovere i diritti di utilizzo. Dopo aver rimosso i diritti di utilizzo, il documento PDF non disporrà di alcuna funzionalità aggiuntiva durante la visualizzazione in  Adobe Reader.

**Salvare il documento PDF**

È possibile salvare come file PDF il documento PDF che non contiene più i diritti di utilizzo. Una volta salvato come file PDF, il documento PDF può essere visualizzato in  Adobe Reader o  Acrobat.

**Consulta anche**

[Rimuovere i diritti di utilizzo mediante l&#39;API Java](assigning-usage-rights.md#remove-usage-rights-using-the-java-api)

[Rimozione dei diritti di utilizzo tramite l&#39;API del servizio Web](assigning-usage-rights.md#remove-usage-rights-using-the-web-service-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido di Acrobat Reader DC Extensions Service API](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

[Applicazione dei diritti di utilizzo ai documenti PDF](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

### Rimuovere i diritti di utilizzo mediante l&#39;API Java {#remove-usage-rights-using-the-java-api}

Per rimuovere i diritti di utilizzo da un documento PDF abilitato per i diritti, utilizzate l&#39;API delle estensioni Acrobat Reader DC (Java):

1. Includere i file di progetto.

   Includete file JAR client, ad esempio adobe-reader-extensions-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto client con estensioni Acrobat Reader DC.

   Creare un oggetto `ReaderExtensionsServiceClient` utilizzando il relativo costruttore e passando un oggetto `ServiceClientFactory` che contiene proprietà di connessione.

1. Recuperare un documento PDF.

   * Creare un oggetto `java.io.FileInputStream` che rappresenti il documento PDF abilitato per i diritti utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del documento PDF.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Rimuovere i diritti di utilizzo dal documento PDF.

   Rimuovere i diritti di utilizzo dal documento PDF richiamando il metodo `ReaderExtensionsServiceClient` dell&#39;oggetto `removeUsageRights` e passando l&#39;oggetto &lt;a2/> che contiene il documento PDF abilitato per i diritti. `com.adobe.idp.Document` Questo metodo restituisce un oggetto `com.adobe.idp.Document` contenente un documento PDF che non dispone dei diritti di utilizzo.

1. Applicare i diritti di utilizzo al documento PDF.

   * Creare un oggetto `java.io.File` e assicurarsi che l&#39;estensione del file sia .PDF.
   * Richiamare il metodo `Document` dell&#39;oggetto `copyToFile` per copiare nel file il contenuto dell&#39;oggetto `Document` (assicurarsi di utilizzare l&#39;oggetto `Document` restituito dal metodo `removeUsageRights`).

**Consulta anche**

[Rimozione dei diritti di utilizzo dai documenti PDF](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)

[Avvio rapido (modalità SOAP): Rimozione di diritti di utilizzo da un documento PDF tramite l&#39;API Java](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-removing-usage-rights-from-a-pdf-document-using-the-java-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Rimuovere i diritti di utilizzo mediante l&#39;API del servizio Web {#remove-usage-rights-using-the-web-service-api}

Per rimuovere i diritti di utilizzo da un documento PDF abilitato per i diritti, utilizzate l&#39;API delle estensioni Acrobat Reader DC (servizio Web):

1. Includere i file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituire `localhost` con l&#39;indirizzo IP del server che ospita  AEM Forms.

1. Creare un oggetto client con estensioni Acrobat Reader DC.

   * Creare un oggetto `ReaderExtensionsServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `ReaderExtensionsServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passate un valore di stringa che specifica il WSDL al servizio AEM Forms  (ad esempio, `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`). Assicurarsi di specificare `?blob=mtom`.
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `ReaderExtensionsServiceClient.Endpoint.Binding`. Inserite il valore restituito in `BasicHttpBinding`.
   * Impostare il campo `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto `MessageEncoding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilitate l&#39;autenticazione HTTP di base eseguendo le seguenti operazioni:

      * Assegnare il nome utente del modulo AEM al campo `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recuperare un documento PDF.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare il documento PDF con diritti abilitati dal quale vengono rimossi i diritti di utilizzo.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà `System.IO.FileStream` dell&#39;oggetto `Length`.
   * Compilare l&#39;array di byte con i dati del flusso richiamando il metodo `Read` dell&#39;oggetto `System.IO.FileStream` e passando l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnandone la proprietà `MTOM` con il contenuto dell&#39;array di byte.

1. Rimuovere i diritti di utilizzo dal documento PDF.

   Rimuovere i diritti di utilizzo dal documento PDF richiamando il metodo `ReaderExtensionsServiceClient` dell&#39;oggetto `removeUsageRights` e passando l&#39;oggetto &lt;a2/> che contiene il documento PDF abilitato per i diritti. `BLOB` Questo metodo restituisce un oggetto `BLOB` contenente un documento PDF che non dispone dei diritti di utilizzo.

1. Applicare i diritti di utilizzo al documento PDF.

   * Creare un oggetto `System.IO.FileStream` richiamandone il costruttore e passando un valore di stringa che rappresenta il percorso del file PDF.
   * Creare un array di byte che memorizza il contenuto dei dati dell&#39;oggetto `BLOB` restituito dal metodo `removeUsageRights`. Compilare l&#39;array di byte ottenendo il valore del membro di dati `BLOB` dell&#39;oggetto `MTOM`.
   * Creare un oggetto `System.IO.BinaryWriter` richiamandone il costruttore e passando l&#39;oggetto `System.IO.FileStream`.

**Consulta anche**

[Rimozione dei diritti di utilizzo dai documenti PDF](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)

[Chiamata  AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chiamata  AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Recupero delle informazioni sulle credenziali {#retrieving-credential-information}

È possibile recuperare informazioni sulle credenziali utilizzate per applicare i diritti di utilizzo a un documento PDF abilitato per i diritti. Recuperando informazioni su una credenziale, è possibile ottenere informazioni quali la data dopo la quale il certificato non è più valido.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio delle estensioni Acrobat Reader DC, vedere [Guida di riferimento dei servizi per  AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-2}

Per recuperare informazioni sulle credenziali utilizzate per applicare diritti di utilizzo a un documento PDF, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un oggetto client con estensioni Acrobat Reader DC.
1. Recuperare un documento PDF abilitato per diritti.
1. Recuperare informazioni sulla credenziale.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se state creando un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate servizi Web, accertatevi di includere i file proxy.

**Creare un oggetto client con estensioni Acrobat Reader DC**

Prima di eseguire un&#39;operazione del servizio di estensione Acrobat Reader DC a livello di programmazione, è necessario creare un oggetto client del servizio di estensione Acrobat Reader DC. Se utilizzate l&#39;API Java, create un oggetto `ReaderExtensionsServiceClient`. Se utilizzate l&#39;API del servizio Web con estensione Acrobat Reader DC, create un oggetto `ReaderExtensionsServiceService`.

**Recupero di un documento PDF con diritti**

Per recuperare informazioni sulle credenziali, è necessario recuperare un documento PDF abilitato per i diritti. È inoltre possibile recuperare informazioni su una credenziale specificandone l&#39;alias; tuttavia, se si desidera recuperare informazioni su una credenziale utilizzata per applicare diritti di utilizzo a un documento PDF con diritti specifici, è necessario recuperare il documento.

**Recupero di informazioni sulla credenziale**

Dopo aver ottenuto un documento PDF con diritti, potete ottenere informazioni sulle credenziali utilizzate per applicarvi i diritti di utilizzo. È possibile ottenere le seguenti informazioni sulla credenziale:

* Messaggio visualizzato in  Adobe Reader all&#39;apertura del documento PDF con diritti.
* Data dopo la quale la credenziale non è più valida.
* Data prima della quale la credenziale non è valida.
* I diritti di utilizzo impostati per questo documento PDF con diritti.
* Il numero di volte in cui è stata utilizzata la credenziale.

**Consulta anche**

[Rimuovere i diritti di utilizzo mediante l&#39;API Java](assigning-usage-rights.md#remove-usage-rights-using-the-java-api)

[Rimozione dei diritti di utilizzo tramite l&#39;API del servizio Web](assigning-usage-rights.md#remove-usage-rights-using-the-web-service-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido di Acrobat Reader DC Extensions Service API](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

### Recuperare le informazioni sulle credenziali utilizzando l&#39;API Java {#retrieve-credential-information-using-the-java-api}

Recuperate le informazioni sulle credenziali utilizzando l&#39;API delle estensioni Acrobat Reader DC (Java):

1. Includere i file di progetto.

   Includete file JAR client, ad esempio adobe-reader-extensions-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto client con estensioni Acrobat Reader DC.

   Creare un oggetto `ReaderExtensionsServiceClient` utilizzando il relativo costruttore e passando un oggetto `ServiceClientFactory` che contiene proprietà di connessione.

1. Recuperare un documento PDF.

   * Creare un oggetto `java.io.FileInputStream` che rappresenti il documento PDF abilitato per i diritti utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del documento PDF abilitato per i diritti.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Rimuovere i diritti di utilizzo dal documento PDF.

   * Recuperare informazioni sulle credenziali utilizzate per applicare diritti di utilizzo al documento PDF richiamando il metodo `ReaderExtensionsServiceClient` dell&#39;oggetto `getDocumentUsageRights` e passando l&#39;oggetto `com.adobe.idp.Document` che contiene il documento PDF abilitato per i diritti. Questo metodo restituisce un oggetto `GetUsageRightsResult` che contiene informazioni sulle credenziali.
   * Recuperare la data dopo la quale la credenziale non è più valida richiamando il metodo `GetUsageRightsResult` dell&#39;oggetto `getNotAfter`. Questo metodo restituisce un oggetto `java.util.Date` che rappresenta la data dopo la quale la credenziale non è più valida.
   * Recuperare il messaggio visualizzato in  Adobe Reader quando il documento PDF abilitato per i diritti viene aperto richiamando il metodo `GetUsageRightsResult` dell&#39;oggetto `getMessage`. Questo metodo restituisce un valore di stringa che rappresenta il messaggio.

**Consulta anche**

[Recupero delle informazioni sulle credenziali](assigning-usage-rights.md#retrieving-credential-information)

[Avvio rapido (modalità SOAP): Recupero delle informazioni sulle credenziali tramite l&#39;API Java](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-retrieving-credential-information-using-the-java-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Recupero delle informazioni sulle credenziali tramite l&#39;API del servizio Web {#retrieve-credential-information-using-the-web-service-api}

Recuperate le informazioni sulle credenziali utilizzando l&#39;API delle estensioni Acrobat Reader DC (servizio Web):

1. Includere i file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituire `localhost` con l&#39;indirizzo IP del server che ospita  AEM Forms.

1. Creare un oggetto client con estensioni Acrobat Reader DC.

   * Creare un oggetto `ReaderExtensionsServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `ReaderExtensionsServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passate un valore di stringa che specifica il WSDL al servizio AEM Forms  (ad esempio, `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`). Assicurarsi di specificare `?blob=mtom`.
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `ReaderExtensionsServiceClient.Endpoint.Binding`. Inserite il valore restituito in `BasicHttpBinding`.
   * Impostare il campo `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto `MessageEncoding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilitate l&#39;autenticazione HTTP di base eseguendo le seguenti operazioni:

      * Assegnare il nome utente del modulo AEM al campo `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recuperare un documento PDF.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare un documento PDF abilitato per i diritti.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta il percorso del file del documento PDF abilitato per i diritti e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà `System.IO.FileStream` dell&#39;oggetto `Length`.
   * Compilare l&#39;array di byte con i dati del flusso richiamando il metodo `Read` dell&#39;oggetto `System.IO.FileStream` e passando l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnandone la proprietà `MTOM` con il contenuto dell&#39;array di byte.

1. Rimuovere i diritti di utilizzo dal documento PDF.

   * Recuperare informazioni sulle credenziali utilizzate per applicare diritti di utilizzo al documento PDF richiamando il metodo `ReaderExtensionsServiceClient` dell&#39;oggetto `getDocumentUsageRights` e passando l&#39;oggetto `com.adobe.idp.Document` che contiene il documento PDF abilitato per i diritti. Questo metodo restituisce un oggetto `GetUsageRightsResult` che contiene informazioni sulle credenziali.
   * Recuperare la data dopo la quale la credenziale non è più valida ottenendo il valore del membro di dati `GetUsageRightsResult` dell&#39;oggetto `notAfter`. Il tipo di dati di questo membro è `System.DateTime`.
   * Recuperare il messaggio visualizzato quando il documento PDF con diritti viene aperto in  Adobe Reader ottenendo il valore del membro di dati `GetUsageRightsResult` dell&#39;oggetto `message`. Il tipo di dati di questo membro è una stringa.
   * Recuperare il numero di volte in cui la credenziale viene utilizzata ottenendo il valore del membro di dati `GetUsageRightsResult` dell&#39;oggetto `useCount`. Il tipo di dati di questo membro dati è un numero intero.

**Consulta anche**

[Recupero delle informazioni sulle credenziali](assigning-usage-rights.md#retrieving-credential-information)

[Chiamata  AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chiamata  AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
