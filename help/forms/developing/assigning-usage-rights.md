---
title: Assegnazione dei diritti di utilizzo
description: Utilizza le estensioni Acrobat Reader DC Java Client API e Web Service API per applicare e rimuovere i diritti di utilizzo dai documenti PDF.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 6af148eb-427a-4b54-9c5f-8750736882d8
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,Reader Extensions
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '3897'
ht-degree: 0%

---

# Assegnazione dei diritti di utilizzo {#assigning-usage-rights}

**Gli esempi e gli esempi contenuti in questo documento sono solo per AEM Forms in ambiente JEE.**

## Informazioni sul servizio estensioni Acrobat Reader DC {#about-the-acrobat-reader-dc-extensions-service}

Il servizio Estensioni di Acrobat Reader DC consente all’organizzazione di condividere facilmente i documenti interattivi di PDF estendendo le funzionalità di Adobe Reader. Il servizio Estensioni di Acrobat Reader DC supporta completamente qualsiasi documento PDF, fino a PDF 1.7 incluso. Funziona con Adobe Reader 7.0 e versioni successive. Il servizio aggiunge diritti di utilizzo a un documento PDF, attivando funzionalità che in genere non sono disponibili quando un documento PDF viene aperto tramite Adobe Reader. Gli utenti di terze parti non richiedono software o plug-in aggiuntivi per lavorare con i documenti abilitati per i diritti.

Puoi eseguire queste attività utilizzando il servizio Estensioni di Acrobat Reader DC:

* Applica i diritti di utilizzo ai documenti di PDF. Per informazioni, vedere [Applicazione dei diritti di utilizzo ai documenti di PDF](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents).
* Rimuovere i diritti di utilizzo dai documenti PDF. Per informazioni, vedere [Rimozione dei diritti di utilizzo dai documenti di PDF](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents).
* Recupera i dettagli delle credenziali. Per informazioni, vedere [Recupero delle informazioni sulle credenziali](assigning-usage-rights.md#retrieving-credential-information).

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Acrobat Reader DC extensions, vedere [Riferimento ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Applicazione dei diritti di utilizzo ai documenti di PDF {#applying-usage-rights-to-pdf-documents}

Puoi applicare i diritti di utilizzo ai documenti PDF utilizzando l’API client Java e il servizio web per le estensioni di Acrobat Reader DC. I diritti di utilizzo riguardano funzionalità disponibili per impostazione predefinita in Acrobat ma non in Adobe Reader, ad esempio la possibilità di aggiungere commenti a un modulo o di compilare campi modulo e salvare il modulo. I documenti PDF a cui sono applicati diritti di utilizzo sono denominati documenti abilitati per i diritti. L’utente che apre un documento abilitato ai diritti in Adobe Reader può eseguire operazioni abilitate per quel documento specifico.

>[!NOTE]
>
>Quando si applicano i diritti di utilizzo ai documenti PDF utilizzando il metodo `applyUsageRights`, che fa parte dell&#39;API Java, è possibile impostare il parametro `isModeFinal` dell&#39;oggetto `ReaderExtensionsOptionSpec` su `false`. In questo modo il contatore dei moduli elaborati non viene aggiornato e si ottiene un miglioramento delle prestazioni. Se non si desidera aggiornare il contatore dei moduli elaborati, è consigliabile impostare il parametro `isModeFinal` su `false`.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Acrobat Reader DC extensions, vedere [Riferimento ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary-of-steps}

Per applicare i diritti di utilizzo a un documento PDF, effettuare le seguenti operazioni:

1. Includi file di progetto.
1. Crea un oggetto client per estensioni Acrobat Reader DC.
1. Recuperare un documento PDF.
1. Specificare i diritti di utilizzo da applicare.
1. Applica i diritti di utilizzo al documento PDF.
1. Salva il documento di PDF con abilitazione per i diritti.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

**Creare un oggetto client di estensioni Acrobat Reader DC**

Per eseguire a livello di programmazione un&#39;operazione del servizio di estensione di Acrobat Reader DC, è necessario creare un oggetto client del servizio di estensione di Acrobat Reader DC. Se si utilizza l&#39;API Java delle estensioni Acrobat Reader DC, creare un oggetto `ReaderExtensionsServiceClient`. Se si utilizza l&#39;API del servizio Web Estensioni di Acrobat Reader DC, creare un oggetto `ReaderExtensionsServiceService`.

**Recuperare un documento PDF**

Recupera un documento PDF per applicare i diritti di utilizzo. I documenti PDF con abilitazione per i diritti contengono un dizionario dei diritti di utilizzo. Quando Adobe Reader apre un documento contenente tale dizionario, abilita i diritti di utilizzo specificati nel dizionario solo per quel documento. Se il documento non contiene un dizionario dei diritti di utilizzo, il servizio Acrobat Reader DC Extension ne crea uno. Se contiene già un dizionario, il servizio Acrobat Reader DC extensions sovrascrive i diritti di utilizzo esistenti con quelli specificati. Il dizionario specifica quali diritti di utilizzo sono abilitati. Quando un utente apre il documento in Adobe Reader, sono consentiti solo i diritti di utilizzo specificati nel dizionario.

**Specificare i diritti di utilizzo da applicare**

I diritti di utilizzo che è possibile impostare sono determinati da una credenziale acquistata da Adobe Systems Incorporated. Le credenziali forniscono in genere l&#39;autorizzazione per impostare un gruppo di diritti di utilizzo correlati, ad esempio quelli relativi ai moduli interattivi. Ogni credenziale consente di creare un determinato numero di documenti di PDF abilitati per i diritti. Una credenziale di valutazione consente di creare un numero illimitato di bozze di documenti.

>[!NOTE]
>
>Se si tenta di assegnare un diritto di utilizzo non consentito dalle credenziali, verrà generata un&#39;eccezione.

**Applica i diritti di utilizzo al documento di PDF**

Per applicare i diritti di utilizzo a un documento PDF, si fa riferimento all&#39;alias delle credenziali utilizzate per applicare i diritti di utilizzo (una credenziale viene in genere installata durante l&#39;installazione di AEM Forms). È inoltre necessario specificare il documento PDF al quale vengono applicati i diritti di utilizzo. Per informazioni sulla configurazione di una credenziale, vedere la guida all&#39;installazione e alla distribuzione per il server applicazioni.

**Salvare il documento di PDF con abilitazione dei diritti**

Dopo aver applicato i diritti di utilizzo a un documento di Acrobat Reader DC PDF, è possibile salvare il documento di PDF con abilitazione per i diritti come file di PDF.

**Consulta anche**

[Applicare i diritti di utilizzo utilizzando l’API Java](assigning-usage-rights.md#apply-usage-rights-using-the-java-api)

[Applicare i diritti di utilizzo utilizzando l’API del servizio web](assigning-usage-rights.md#apply-usage-rights-using-the-web-service-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API del servizio Estensioni di Acrobat Reader DC](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

### Applicare i diritti di utilizzo utilizzando l’API Java {#apply-usage-rights-using-the-java-api}

Applica i diritti di utilizzo a un documento PDF utilizzando l’API delle estensioni Acrobat Reader DC (Java):

1. Includi file di progetto

   Includi i file JAR client, ad esempio adobe-reader-extensions-client.jar, nel percorso della classe del progetto Java.

1. Crea un oggetto client per estensioni Acrobat Reader DC.

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `ReaderExtensionsServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Recuperare un documento PDF.

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento PDF utilizzando il relativo costruttore e passando un valore stringa che specifica la posizione del documento PDF.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Specificare i diritti di utilizzo da applicare.

   * Creare un oggetto `UsageRights` che rappresenta i diritti di utilizzo utilizzando il relativo costruttore.
   * Per ogni diritto di utilizzo da applicare, richiamare un metodo corrispondente appartenente all&#39;oggetto `UsageRights`. Ad esempio, per aggiungere il diritto di utilizzo `enableFormFillIn`, richiamare il metodo `enableFormFillIn` dell&#39;oggetto `UsageRights` e passare `true`. (Ripeti questo passaggio per ogni diritto d’uso da applicare).

1. Applica i diritti di utilizzo al documento PDF.

   * Creare un oggetto `ReaderExtensionsOptionSpec` utilizzando il relativo costruttore. Questo oggetto contiene le opzioni di runtime richieste dal servizio Acrobat Reader DC extensions. Quando si richiama questo costruttore, è necessario specificare i seguenti valori:

      * Oggetto `UsageRights` contenente i diritti di utilizzo da applicare al documento.
      * Valore stringa che specifica un messaggio visualizzato da un utente quando il documento di PDF con abilitazione per i diritti viene aperto in Adobe Reader 7.x. Questo messaggio non viene visualizzato in Adobe Reader 8.0.

   * Applicare i diritti di utilizzo al documento PDF richiamando il metodo `applyUsageRights` dell&#39;oggetto `ReaderExtensionsServiceClient` e passando i valori seguenti:

      * L&#39;oggetto `com.adobe.idp.Document` che contiene il documento PDF a cui sono applicati i diritti di utilizzo.
      * Valore stringa che specifica l&#39;alias della credenziale che consente di applicare i diritti di utilizzo.
      * Valore stringa che specifica il valore password corrispondente. (Attualmente questo parametro viene ignorato. È possibile passare `null`.)

   * L&#39;oggetto `ReaderExtensionsOptionSpec` che contiene le opzioni di runtime.

   Il metodo `applyUsageRights` restituisce un oggetto `com.adobe.idp.Document` che contiene il documento PDF con abilitazione per i diritti.

1. Salva il documento di PDF con abilitazione per i diritti.

   * Creare un oggetto `java.io.File` e verificare che l&#39;estensione del file sia .pdf.
   * Richiamare il metodo `copyToFile` dell&#39;oggetto `com.adobe.idp.Document` per copiare il contenuto dell&#39;oggetto `com.adobe.idp.Document` nel file (assicurarsi di utilizzare l&#39;oggetto `com.adobe.idp.Document` restituito dal metodo `applyUsageRights`).

**Consulta anche**

[Applicazione dei diritti di utilizzo ai documenti di PDF](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[Quick Start (modalità SOAP):Applicazione dei diritti di utilizzo tramite API Java](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-applying-usage-rights-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Applicare i diritti di utilizzo utilizzando l’API del servizio web {#apply-usage-rights-using-the-web-service-api}

Applica i diritti di utilizzo a un documento PDF utilizzando l’API delle estensioni di Acrobat Reader DC (servizio web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Crea un oggetto client per estensioni Acrobat Reader DC.

   * Creare un oggetto `ReaderExtensionsServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `ReaderExtensionsServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`. Assicurarsi di specificare `?blob=mtom`.)
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `ReaderExtensionsServiceClient.Endpoint.Binding`. Eseguire il cast del valore restituito in `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegnare il nome utente dei moduli AEM al campo `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recuperare un documento PDF.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare un documento PDF a cui sono applicati diritti di utilizzo.
   * Creare un oggetto `System.IO.FileStream` richiamandone il costruttore e passando un valore stringa che rappresenta la posizione del file del documento PDF e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni della matrice di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare la matrice di byte con i dati di flusso richiamando il metodo `Read` dell&#39;oggetto `System.IO.FileStream`. Passare la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando la relativa proprietà `MTOM` al contenuto della matrice di byte.

1. Specificare i diritti di utilizzo da applicare.

   * Creare un oggetto `UsageRights` che rappresenta i diritti di utilizzo utilizzando il relativo costruttore.
   * Per ogni diritto di utilizzo da applicare, assegnare il valore `true` al membro dati corrispondente che appartiene all&#39;oggetto `UsageRights`. Ad esempio, per aggiungere il diritto di utilizzo `enableFormFillIn`, assegnare `true` al membro dati `enableFormFillIn` dell&#39;oggetto `UsageRights`. (Ripeti questo passaggio per ogni diritto d’uso da applicare).

1. Applica i diritti di utilizzo al documento PDF.

   * Creare un oggetto `ReaderExtensionsOptionSpec` utilizzando il relativo costruttore. Questo oggetto contiene le opzioni di runtime richieste dal servizio Acrobat Reader DC extensions.
   * Assegnare l&#39;oggetto `UsageRights` al membro dati `usageRights` dell&#39;oggetto `ReaderExtensionsOptionSpec`.
   * Assegnare un valore stringa che specifichi il messaggio visualizzato da un utente quando il documento PDF con abilitazione per i diritti viene aperto in Adobe Reader al membro dati `message` dell&#39;oggetto `ReaderExtensionsOptionSpec`.
   * Applicare i diritti di utilizzo al documento PDF richiamando il metodo `applyUsageRights` dell&#39;oggetto `ReaderExtensionsServiceClient` e passando i valori seguenti:

      * L&#39;oggetto `BLOB` che contiene il documento PDF a cui sono applicati i diritti di utilizzo.
      * Valore stringa che specifica l&#39;alias della credenziale che consente di applicare i diritti di utilizzo.
      * Valore stringa che specifica il valore password corrispondente. (Attualmente questo parametro viene ignorato. È possibile passare `null`.)

   * L&#39;oggetto `ReaderExtensionsOptionSpec` che contiene le opzioni di runtime.

   Il metodo `applyUsageRights` restituisce un oggetto `BLOB` che contiene il documento PDF con abilitazione per i diritti.

1. Salva il documento di PDF con abilitazione per i diritti.

   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore. Passa un valore stringa che rappresenta la posizione del file del documento di PDF con abilitazione per i diritti.
   * Creare una matrice di byte che memorizza il contenuto dei dati dell&#39;oggetto `BLOB` restituito dal metodo `applyUsageRights`. Popolare la matrice di byte ottenendo il valore del membro dati `MTOM` dell&#39;oggetto `BLOB`.
   * Creare un oggetto `System.IO.BinaryWriter` richiamandone il costruttore e passando l&#39;oggetto `System.IO.FileStream`.
   * Scrivere il contenuto della matrice di byte in un file PDF richiamando il metodo `Write` dell&#39;oggetto `System.IO.BinaryWriter` e passando la matrice di byte.

**Consulta anche**

[Applicazione dei diritti di utilizzo ai documenti di PDF](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamare AEM Forms con SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Rimozione dei diritti di utilizzo dai documenti di PDF {#removing-usage-rights-from-pdf-documents}

È possibile rimuovere i diritti di utilizzo da un documento abilitato per i diritti. La rimozione dei diritti di utilizzo da un documento PDF abilitato ai diritti è necessaria anche per eseguire altre operazioni AEM Forms su di esso. È ad esempio necessario firmare digitalmente (o certificare) un documento di PDF prima di impostare i diritti di utilizzo. Pertanto, se si desidera eseguire operazioni su un documento abilitato ai diritti, è necessario rimuovere i diritti di utilizzo dal documento PDF, eseguire le altre operazioni, ad esempio la firma digitale del documento, quindi riapplicare i diritti di utilizzo al documento.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Acrobat Reader DC extensions, vedere [Riferimento ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-1}

Per rimuovere i diritti di utilizzo da un documento di PDF abilitato per i diritti, effettuare le seguenti operazioni:

1. Includi file di progetto.
1. Crea un oggetto client per estensioni Acrobat Reader DC.
1. Recuperare un documento di PDF abilitato per i diritti.
1. Rimuovi i diritti di utilizzo dal documento PDF.
1. Salvare il documento PDF.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

**Creare un oggetto client di estensioni Acrobat Reader DC**

Prima di poter eseguire un&#39;operazione del servizio Acrobat Reader DC extensions a livello di programmazione, è necessario creare un oggetto client del servizio Acrobat Reader DC extensions. Se si utilizza l&#39;API Java, creare un oggetto `ReaderExtensionsServiceClient`. Se si utilizza l&#39;API del servizio Web Estensioni di Acrobat Reader DC, creare un oggetto `ReaderExtensionsServiceService`.

**Recuperare un documento di PDF abilitato per i diritti**

Recupera un documento PDF con abilitazione dei diritti per rimuovere i diritti di utilizzo.

**Rimuovi i diritti di utilizzo dal documento PDF**

Dopo aver recuperato un documento di PDF con abilitazione dei diritti, è possibile rimuovere i diritti di utilizzo. Dopo aver rimosso i diritti di utilizzo, il documento PDF non avrà alcuna funzionalità aggiuntiva durante la visualizzazione in Adobe Reader.

**Salva il documento PDF**

È possibile salvare il documento PDF che non contiene più diritti di utilizzo come file PDF. Una volta salvato come file PDF, il documento PDF può essere visualizzato in Adobe Reader o Acrobat.

**Consulta anche**

[Rimuovere i diritti di utilizzo utilizzando l’API Java](assigning-usage-rights.md#remove-usage-rights-using-the-java-api)

[Rimuovere i diritti di utilizzo utilizzando l’API del servizio web](assigning-usage-rights.md#remove-usage-rights-using-the-web-service-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API del servizio Estensioni di Acrobat Reader DC](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

[Applicazione dei diritti di utilizzo ai documenti di PDF](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

### Rimuovere i diritti di utilizzo utilizzando l’API Java {#remove-usage-rights-using-the-java-api}

Rimuovere i diritti di utilizzo da un documento PDF con abilitazione per i diritti utilizzando l’API delle estensioni Acrobat Reader DC (Java):

1. Includi file di progetto.

   Includi i file JAR client, ad esempio adobe-reader-extensions-client.jar, nel percorso della classe del progetto Java.

1. Crea un oggetto client per estensioni Acrobat Reader DC.

   Creare un oggetto `ReaderExtensionsServiceClient` utilizzando il relativo costruttore e passando un oggetto `ServiceClientFactory` che contiene proprietà di connessione.

1. Recuperare un documento PDF.

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento PDF con abilitazione per i diritti utilizzando il relativo costruttore e passando un valore stringa che specifica la posizione del documento PDF.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Rimuovi i diritti di utilizzo dal documento PDF.

   Rimuovere i diritti di utilizzo dal documento PDF richiamando il metodo `removeUsageRights` dell&#39;oggetto `ReaderExtensionsServiceClient` e passando l&#39;oggetto `com.adobe.idp.Document` che contiene il documento PDF abilitato per i diritti. Questo metodo restituisce un oggetto `com.adobe.idp.Document` contenente un documento PDF che non dispone di diritti di utilizzo.

1. Applica i diritti di utilizzo al documento PDF.

   * Creare un oggetto `java.io.File` e verificare che l&#39;estensione del file sia .PDF.
   * Richiamare il metodo `copyToFile` dell&#39;oggetto `Document` per copiare il contenuto dell&#39;oggetto `Document` nel file (assicurarsi di utilizzare l&#39;oggetto `Document` restituito dal metodo `removeUsageRights`).

**Consulta anche**

[Rimozione dei diritti di utilizzo dai documenti di PDF](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)

[Guida rapida (modalità SOAP): rimozione dei diritti di utilizzo da un documento PDF tramite l’API Java](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-removing-usage-rights-from-a-pdf-document-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Rimuovere i diritti di utilizzo utilizzando l’API del servizio web {#remove-usage-rights-using-the-web-service-api}

Rimuovi i diritti di utilizzo da un documento di PDF abilitato ai diritti utilizzando l’API delle estensioni di Acrobat Reader DC (servizio web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Crea un oggetto client per estensioni Acrobat Reader DC.

   * Creare un oggetto `ReaderExtensionsServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `ReaderExtensionsServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`. Assicurarsi di specificare `?blob=mtom`.)
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `ReaderExtensionsServiceClient.Endpoint.Binding`. Eseguire il cast del valore restituito in `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegnare il nome utente dei moduli AEM al campo `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recuperare un documento PDF.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per archiviare il documento PDF con diritti di utilizzo da cui vengono rimossi i diritti di utilizzo.
   * Creare un oggetto `System.IO.FileStream` richiamandone il costruttore e passando un valore stringa che rappresenta la posizione del file del documento PDF e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni della matrice di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare la matrice di byte con i dati di flusso richiamando il metodo `Read` dell&#39;oggetto `System.IO.FileStream` e passando la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando la relativa proprietà `MTOM` al contenuto della matrice di byte.

1. Rimuovi i diritti di utilizzo dal documento PDF.

   Rimuovere i diritti di utilizzo dal documento PDF richiamando il metodo `removeUsageRights` dell&#39;oggetto `ReaderExtensionsServiceClient` e passando l&#39;oggetto `BLOB` che contiene il documento PDF abilitato per i diritti. Questo metodo restituisce un oggetto `BLOB` contenente un documento PDF che non dispone di diritti di utilizzo.

1. Applica i diritti di utilizzo al documento PDF.

   * Creare un oggetto `System.IO.FileStream` richiamandone il costruttore e passando un valore stringa che rappresenta il percorso del file PDF.
   * Creare una matrice di byte che memorizza il contenuto dei dati dell&#39;oggetto `BLOB` restituito dal metodo `removeUsageRights`. Popolare la matrice di byte ottenendo il valore del membro dati `MTOM` dell&#39;oggetto `BLOB`.
   * Creare un oggetto `System.IO.BinaryWriter` richiamandone il costruttore e passando l&#39;oggetto `System.IO.FileStream`.

**Consulta anche**

[Rimozione dei diritti di utilizzo dai documenti di PDF](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)

[Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamare AEM Forms con SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Recupero informazioni sulle credenziali {#retrieving-credential-information}

È possibile recuperare informazioni sulle credenziali utilizzate per applicare i diritti di utilizzo a un documento di PDF abilitato per i diritti. Recuperando le informazioni su una credenziale, è possibile ottenere informazioni quali la data dopo la quale il certificato non è più valido.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Acrobat Reader DC extensions, vedere [Riferimento ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-2}

Per recuperare informazioni sulle credenziali utilizzate per applicare i diritti di utilizzo a un documento PDF, effettuare le seguenti operazioni:

1. Includi file di progetto.
1. Crea un oggetto client per estensioni Acrobat Reader DC.
1. Recuperare un documento di PDF abilitato per i diritti.
1. Recuperare le informazioni sulle credenziali.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

**Creare un oggetto client di estensioni Acrobat Reader DC**

Prima di poter eseguire un&#39;operazione del servizio Acrobat Reader DC extensions a livello di programmazione, è necessario creare un oggetto client del servizio Acrobat Reader DC extensions. Se si utilizza l&#39;API Java, creare un oggetto `ReaderExtensionsServiceClient`. Se si utilizza l&#39;API del servizio Web Estensioni di Acrobat Reader DC, creare un oggetto `ReaderExtensionsServiceService`.

**Recuperare un documento di PDF abilitato per i diritti**

Recuperare un documento PDF abilitato per i diritti per recuperare informazioni sulle credenziali. È inoltre possibile recuperare informazioni su una credenziale specificandone l&#39;alias. Tuttavia, se si desidera recuperare informazioni su una credenziale utilizzata per applicare i diritti di utilizzo a un documento PDF con diritti specifici, è necessario recuperare il documento.

**Recupera informazioni sulle credenziali**

Dopo aver recuperato un documento di PDF abilitato per i diritti, è possibile ottenere informazioni sulle credenziali utilizzate per applicare i diritti di utilizzo. È possibile ottenere le seguenti informazioni sulle credenziali:

* Messaggio visualizzato in Adobe Reader quando viene aperto il documento di PDF con abilitazione per i diritti.
* Data dopo la quale le credenziali non sono più valide.
* Data prima della quale le credenziali non sono valide.
* Diritti di utilizzo impostati per questo documento di PDF con abilitazione per i diritti.
* Il numero di volte in cui le credenziali sono state utilizzate.

**Consulta anche**

[Rimuovere i diritti di utilizzo utilizzando l’API Java](assigning-usage-rights.md#remove-usage-rights-using-the-java-api)

[Rimuovere i diritti di utilizzo utilizzando l’API del servizio web](assigning-usage-rights.md#remove-usage-rights-using-the-web-service-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API del servizio Estensioni di Acrobat Reader DC](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

### Recuperare le informazioni sulle credenziali tramite API Java {#retrieve-credential-information-using-the-java-api}

Recupera le informazioni sulle credenziali utilizzando l’API delle estensioni Acrobat Reader DC (Java):

1. Includi file di progetto.

   Includi i file JAR client, ad esempio adobe-reader-extensions-client.jar, nel percorso della classe del progetto Java.

1. Crea un oggetto client per estensioni Acrobat Reader DC.

   Creare un oggetto `ReaderExtensionsServiceClient` utilizzando il relativo costruttore e passando un oggetto `ServiceClientFactory` che contiene proprietà di connessione.

1. Recuperare un documento PDF.

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento PDF con abilitazione per i diritti utilizzando il relativo costruttore e passando un valore stringa che specifica la posizione del documento PDF con abilitazione per i diritti.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Rimuovi i diritti di utilizzo dal documento PDF.

   * Recuperare le informazioni sulle credenziali utilizzate per applicare i diritti di utilizzo al documento PDF richiamando il metodo `getDocumentUsageRights` dell&#39;oggetto `ReaderExtensionsServiceClient` e passando l&#39;oggetto `com.adobe.idp.Document` che contiene il documento PDF abilitato per i diritti. Questo metodo restituisce un oggetto `GetUsageRightsResult` contenente informazioni sulle credenziali.
   * Recuperare la data dopo la quale le credenziali non sono più valide richiamando il metodo `getNotAfter` dell&#39;oggetto `GetUsageRightsResult`. Questo metodo restituisce un oggetto `java.util.Date` che rappresenta la data dopo la quale le credenziali non sono più valide.
   * Recuperare il messaggio visualizzato in Adobe Reader quando il documento di PDF con abilitazione per i diritti viene aperto richiamando il metodo `getMessage` dell&#39;oggetto `GetUsageRightsResult`. Questo metodo restituisce un valore stringa che rappresenta il messaggio.

**Consulta anche**

[Recupero informazioni sulle credenziali](assigning-usage-rights.md#retrieving-credential-information)

[Quick Start (modalità SOAP): recupero delle informazioni sulle credenziali tramite l’API Java](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-retrieving-credential-information-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Recuperare le informazioni sulle credenziali tramite l’API del servizio web {#retrieve-credential-information-using-the-web-service-api}

Recupera le informazioni sulle credenziali tramite l’API delle estensioni di Acrobat Reader DC (servizio web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Crea un oggetto client per estensioni Acrobat Reader DC.

   * Creare un oggetto `ReaderExtensionsServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `ReaderExtensionsServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`. Assicurarsi di specificare `?blob=mtom`.)
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `ReaderExtensionsServiceClient.Endpoint.Binding`. Eseguire il cast del valore restituito in `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegnare il nome utente dei moduli AEM al campo `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recuperare un documento PDF.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare un documento PDF con abilitazione per i diritti.
   * Creare un oggetto `System.IO.FileStream` richiamandone il costruttore e passando un valore stringa che rappresenta la posizione del file del documento PDF con abilitazione per i diritti e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni della matrice di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare la matrice di byte con i dati di flusso richiamando il metodo `Read` dell&#39;oggetto `System.IO.FileStream` e passando la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando la relativa proprietà `MTOM` al contenuto della matrice di byte.

1. Rimuovi i diritti di utilizzo dal documento PDF.

   * Recuperare le informazioni sulle credenziali utilizzate per applicare i diritti di utilizzo al documento PDF richiamando il metodo `getDocumentUsageRights` dell&#39;oggetto `ReaderExtensionsServiceClient` e passando l&#39;oggetto `com.adobe.idp.Document` che contiene il documento PDF abilitato per i diritti. Questo metodo restituisce un oggetto `GetUsageRightsResult` che contiene informazioni sulle credenziali.
   * Recuperare la data dopo la quale le credenziali non sono più valide ottenendo il valore del membro dati `notAfter` dell&#39;oggetto `GetUsageRightsResult`. Il tipo di dati di questo membro dati è `System.DateTime`.
   * Recuperare il messaggio visualizzato quando il documento PDF con abilitazione per i diritti viene aperto in Adobe Reader ottenendo il valore del membro dati `message` dell&#39;oggetto `GetUsageRightsResult`. Il tipo di dati di questo membro dati è una stringa.
   * Recuperare il numero di volte in cui le credenziali vengono utilizzate ottenendo il valore del membro dati `useCount` dell&#39;oggetto `GetUsageRightsResult`. Il tipo di dati di questo membro dati è un numero intero.

**Consulta anche**

[Recupero informazioni sulle credenziali](assigning-usage-rights.md#retrieving-credential-information)

[Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamare AEM Forms con SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
