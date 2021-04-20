---
title: Assegnazione dei diritti di utilizzo
seo-title: Assegnazione dei diritti di utilizzo
description: Utilizza l’API client Java e l’API servizio Web di Acrobat Reader DC extensions per applicare e rimuovere i diritti di utilizzo dai documenti PDF.
seo-description: Utilizza l’API client Java e l’API servizio Web di Acrobat Reader DC extensions per applicare e rimuovere i diritti di utilizzo dai documenti PDF.
uuid: 8c2020df-ea3c-49fa-916f-38a458f40d2b
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9e8db506-9ace-4e1f-8a7b-c4e9b15dde7e
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '3952'
ht-degree: 0%

---


# Assegnazione dei diritti di utilizzo {#assigning-usage-rights}

**Esempi ed esempi in questo documento sono solo per AEM Forms in ambiente JEE.**

## Informazioni sul servizio Acrobat Reader DC extensions {#about-the-acrobat-reader-dc-extensions-service}

Il servizio Acrobat Reader DC extensions consente alla tua organizzazione di condividere facilmente i documenti PDF interattivi estendendo le funzionalità di Adobe Reader. Il servizio Acrobat Reader DC extensions supporta completamente qualsiasi documento PDF, fino a PDF 1.7 incluso, e funziona con Adobe Reader 7.0 e versioni successive. Il servizio aggiunge diritti di utilizzo a un documento PDF, attivando funzioni che di solito non sono disponibili quando un documento PDF viene aperto con Adobe Reader. Gli utenti di terze parti non richiedono software o plug-in aggiuntivi per lavorare con i documenti abilitati per i diritti.

Puoi eseguire queste attività utilizzando il servizio Acrobat Reader DC extensions:

* Applicare diritti di utilizzo ai documenti PDF. Per informazioni, vedere [Applicazione dei diritti di utilizzo ai documenti PDF](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents).
* Rimuovere i diritti di utilizzo dai documenti PDF. Per informazioni, vedere [Rimozione dei diritti di utilizzo dai documenti PDF](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents).
* Recupera i dettagli delle credenziali. Per informazioni, vedere [Recupero delle informazioni sulle credenziali](assigning-usage-rights.md#retrieving-credential-information).

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Acrobat Reader DC extensions, consulta [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Applicazione dei diritti di utilizzo ai documenti PDF {#applying-usage-rights-to-pdf-documents}

Puoi applicare i diritti di utilizzo ai documenti PDF utilizzando l’API Java Client e il servizio Web di Acrobat Reader DC extensions. I diritti di utilizzo si riferiscono a funzionalità disponibili per impostazione predefinita in Acrobat ma non in Adobe Reader, ad esempio la possibilità di aggiungere commenti a un modulo o di compilare campi modulo e salvare il modulo. I documenti PDF a cui sono applicati i diritti di utilizzo sono denominati documenti abilitati per i diritti. Un utente che apre un documento abilitato per i diritti in Adobe Reader può eseguire operazioni abilitate per quel documento specifico.

>[!NOTE]
>
>Quando si applicano diritti di utilizzo ai documenti PDF utilizzando il metodo `applyUsageRights`, che fa parte dell’API Java, è possibile impostare il parametro `isModeFinal` dell’oggetto `ReaderExtensionsOptionSpec` su `false`. Ciò impedisce l’aggiornamento del contatore di elaborazione dei moduli e migliora le prestazioni. Se non si desidera aggiornare il contatore dei moduli elaborati, è consigliabile impostare il parametro `isModeFinal` su `false`.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Acrobat Reader DC extensions, consulta [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary-of-steps}

Per applicare i diritti di utilizzo a un documento PDF, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Crea un oggetto client Acrobat Reader DC extensions.
1. Recupera un documento PDF.
1. Specifica i diritti di utilizzo da applicare.
1. Applicare i diritti di utilizzo al documento PDF.
1. Salvare il documento PDF abilitato per i diritti.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

**Creare un oggetto client Acrobat Reader DC extensions**

Per eseguire programmaticamente un’operazione del servizio di estensione Acrobat Reader DC, devi creare un oggetto client del servizio di estensione Acrobat Reader DC. Se utilizzi l’API Java per le estensioni Acrobat Reader DC, crea un oggetto `ReaderExtensionsServiceClient` . Se utilizzi l’API del servizio Web Acrobat Reader DC extensions, crea un oggetto `ReaderExtensionsServiceService` .

**Recuperare un documento PDF**

È necessario recuperare un documento PDF per applicare i diritti di utilizzo. I documenti PDF abilitati per i diritti contengono un dizionario dei diritti di utilizzo. Quando Adobe Reader apre un documento contenente tale dizionario, abilita i diritti di utilizzo specificati nel dizionario solo per quel documento. Se il documento non contiene un dizionario dei diritti di utilizzo, il servizio Acrobat Reader DC extensions ne crea uno. Se contiene già un dizionario, il servizio Acrobat Reader DC extensions sovrascrive i diritti di utilizzo esistenti con quelli specificati. Il dizionario specifica quali diritti di utilizzo sono abilitati. Quando un utente apre il documento in Adobe Reader, sono consentiti solo i diritti di utilizzo specificati nel dizionario.

**Specificare i diritti di utilizzo da applicare**

I diritti di utilizzo che è possibile impostare sono determinati da una credenziale acquistata da Adobe Systems Incorporated. Le credenziali forniscono in genere l’autorizzazione per impostare un gruppo di diritti di utilizzo correlati, ad esempio quelli relativi ai moduli interattivi. Ciascuna credenziale consente di creare un certo numero di documenti PDF abilitati per i diritti. Una credenziale di valutazione dà il diritto di creare un numero illimitato di bozze di documenti.

>[!NOTE]
>
>Se tenti di assegnare un diritto di utilizzo non consentito dalla credenziale, causerai un&#39;eccezione.

**Applicazione dei diritti di utilizzo al documento PDF**

Per applicare i diritti di utilizzo a un documento PDF, è necessario fare riferimento all’alias della credenziale utilizzata per applicare i diritti di utilizzo. In genere, durante l’installazione di AEM Forms viene installata una credenziale. È inoltre necessario specificare il documento PDF a cui vengono applicati i diritti di utilizzo. Per informazioni sulla configurazione di una credenziale, consulta la guida all’installazione e alla distribuzione per il server delle applicazioni.

**Salvare il documento PDF abilitato per i diritti**

Dopo aver applicato i diritti di utilizzo a un documento PDF da parte del servizio Acrobat Reader DC extensions, è possibile salvare il documento PDF abilitato per i diritti come file PDF.

**Consulta anche**

[Applicazione dei diritti di utilizzo tramite l’API Java](assigning-usage-rights.md#apply-usage-rights-using-the-java-api)

[Applicazione dei diritti di utilizzo tramite l’API del servizio Web](assigning-usage-rights.md#apply-usage-rights-using-the-web-service-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido dell&#39;API del servizio Acrobat Reader DC Extensions](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

### Applica i diritti di utilizzo utilizzando l&#39;API Java {#apply-usage-rights-using-the-java-api}

Applica i diritti di utilizzo a un documento PDF utilizzando l’API Acrobat Reader DC Extensions (Java):

1. Includi file di progetto

   Includi file JAR client, come adobe-reader-extensions-client.jar, nel percorso di classe del progetto Java.

1. Crea un oggetto client Acrobat Reader DC extensions.

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `ReaderExtensionsServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Recupera un documento PDF.

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento PDF utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del documento PDF.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Specifica i diritti di utilizzo da applicare.

   * Creare un oggetto `UsageRights` che rappresenta i diritti di utilizzo utilizzando il relativo costruttore.
   * Per ogni diritto di utilizzo da applicare, richiamare un metodo corrispondente che appartiene all&#39;oggetto `UsageRights`. Ad esempio, per aggiungere il diritto di utilizzo `enableFormFillIn`, richiamare il metodo `UsageRights` dell’oggetto `enableFormFillIn` e passare `true`. (Ripeti questo passaggio per ogni diritto di utilizzo da applicare).

1. Applicare i diritti di utilizzo al documento PDF.

   * Creare un oggetto `ReaderExtensionsOptionSpec` utilizzando il relativo costruttore. Questo oggetto contiene le opzioni di esecuzione richieste dal servizio Acrobat Reader DC extensions. Quando si richiama questo costruttore, è necessario specificare i seguenti valori:

      * L&#39;oggetto `UsageRights` che contiene i diritti di utilizzo da applicare al documento.
      * Valore stringa che specifica un messaggio visualizzato dall&#39;utente quando il documento PDF abilitato per i diritti viene aperto in Adobe Reader 7.x. Questo messaggio non viene visualizzato in Adobe Reader 8.0.
   * Per applicare i diritti di utilizzo al documento PDF, richiamare il metodo `applyUsageRights` dell’oggetto `ReaderExtensionsServiceClient` e passare i seguenti valori:

      * L&#39;oggetto `com.adobe.idp.Document` che contiene il documento PDF a cui vengono applicati i diritti di utilizzo.
      * Valore stringa che specifica l&#39;alias della credenziale che consente di applicare diritti di utilizzo.
      * Valore stringa che specifica il valore della password corrispondente. (Questo parametro viene attualmente ignorato. Puoi passare `null`.)
   * L&#39;oggetto `ReaderExtensionsOptionSpec` che contiene opzioni di esecuzione.

   Il metodo `applyUsageRights` restituisce un oggetto `com.adobe.idp.Document` contenente il documento PDF abilitato per i diritti.

1. Salvare il documento PDF abilitato per i diritti.

   * Crea un oggetto `java.io.File` e assicurati che l&#39;estensione del file sia .pdf.
   * Richiamare il metodo `copyToFile` dell&#39;oggetto `com.adobe.idp.Document` per copiare il contenuto dell&#39;oggetto `com.adobe.idp.Document` nel file (assicurarsi di utilizzare l&#39;oggetto `com.adobe.idp.Document` restituito dal metodo `applyUsageRights`).

**Consulta anche**

[Applicazione dei diritti di utilizzo ai documenti PDF](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[Avvio rapido (modalità SOAP):applicazione dei diritti di utilizzo tramite l’API Java](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-applying-usage-rights-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Applica i diritti di utilizzo utilizzando l&#39;API del servizio Web {#apply-usage-rights-using-the-web-service-api}

Applica i diritti di utilizzo a un documento PDF utilizzando l’API delle estensioni Acrobat Reader DC (servizio Web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurati di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Crea un oggetto client Acrobat Reader DC extensions.

   * Creare un oggetto `ReaderExtensionsServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `ReaderExtensionsServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`. Assicurati di specificare `?blob=mtom`.)
   * Crea un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `ReaderExtensionsServiceClient.Endpoint.Binding` . Imposta il valore restituito su `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegna il nome utente del modulo di AEM al campo `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore della password corrispondente al campo `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recupera un documento PDF.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare un documento PDF a cui vengono applicati i diritti di utilizzo.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni dell&#39;array di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare l’array di byte con i dati del flusso richiamando il metodo `Read` dell’oggetto `System.IO.FileStream`. Passa la matrice dei byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando la relativa proprietà `MTOM` con il contenuto dell&#39;array di byte.

1. Specifica i diritti di utilizzo da applicare.

   * Creare un oggetto `UsageRights` che rappresenta i diritti di utilizzo utilizzando il relativo costruttore.
   * Per ogni diritto di utilizzo da applicare, assegna il valore `true` al membro dati corrispondente che appartiene all&#39;oggetto `UsageRights`. Ad esempio, per aggiungere il diritto di utilizzo `enableFormFillIn`, assegna `true` al membro dati `UsageRights` dell’oggetto `enableFormFillIn`. (Ripeti questo passaggio per ogni diritto di utilizzo da applicare).

1. Applicare i diritti di utilizzo al documento PDF.

   * Creare un oggetto `ReaderExtensionsOptionSpec` utilizzando il relativo costruttore. Questo oggetto contiene le opzioni di esecuzione richieste dal servizio Acrobat Reader DC extensions.
   * Assegna l&#39;oggetto `UsageRights` al membro dati `ReaderExtensionsOptionSpec` dell&#39;oggetto `usageRights`.
   * Assegnare un valore stringa che specifica il messaggio visualizzato dall&#39;utente quando il documento PDF abilitato per i diritti viene aperto in Adobe Reader al membro dati `ReaderExtensionsOptionSpec` dell&#39;oggetto `message`.
   * Per applicare i diritti di utilizzo al documento PDF, richiamare il metodo `applyUsageRights` dell’oggetto `ReaderExtensionsServiceClient` e passare i seguenti valori:

      * L&#39;oggetto `BLOB` che contiene il documento PDF a cui vengono applicati i diritti di utilizzo.
      * Valore stringa che specifica l&#39;alias della credenziale che consente di applicare diritti di utilizzo.
      * Valore stringa che specifica il valore della password corrispondente. (Questo parametro viene attualmente ignorato. Puoi passare `null`.)
   * L&#39;oggetto `ReaderExtensionsOptionSpec` che contiene opzioni di esecuzione.

   Il metodo `applyUsageRights` restituisce un oggetto `BLOB` contenente il documento PDF abilitato per i diritti.

1. Salvare il documento PDF abilitato per i diritti.

   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore. Passa un valore stringa che rappresenta la posizione del file del documento PDF abilitato per i diritti.
   * Creare una matrice di byte che memorizza il contenuto dei dati dell&#39;oggetto `BLOB` restituito dal metodo `applyUsageRights`. Compilare l&#39;array di byte ottenendo il valore del membro dati `BLOB` dell&#39;oggetto `MTOM`.
   * Creare un oggetto `System.IO.BinaryWriter` richiamandone il costruttore e passando l&#39;oggetto `System.IO.FileStream`.
   * Scrivi il contenuto dell’array di byte in un file PDF richiamando il metodo `Write` dell’oggetto `System.IO.BinaryWriter` e passando l’array di byte.

**Consulta anche**

[Applicazione dei diritti di utilizzo ai documenti PDF](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[Richiamo di AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamo di AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Rimozione dei diritti di utilizzo dai documenti PDF {#removing-usage-rights-from-pdf-documents}

È possibile rimuovere i diritti di utilizzo da un documento abilitato per i diritti. È inoltre necessario rimuovere i diritti di utilizzo da un documento PDF abilitato per i diritti per eseguire altre operazioni AEM Forms al suo interno. Ad esempio, è necessario firmare (o certificare) digitalmente un documento PDF prima di impostare i diritti di utilizzo. Pertanto, se si desidera eseguire operazioni su un documento abilitato per i diritti, è necessario rimuovere i diritti di utilizzo dal documento PDF, eseguire le altre operazioni, ad esempio la firma digitale del documento e quindi riapplicare i diritti di utilizzo al documento.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Acrobat Reader DC extensions, consulta [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-1}

Per rimuovere i diritti di utilizzo da un documento PDF abilitato per i diritti, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Crea un oggetto client Acrobat Reader DC extensions.
1. Recupera un documento PDF abilitato per i diritti.
1. Rimuovere i diritti di utilizzo dal documento PDF.
1. Salvare il documento PDF.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

**Creare un oggetto client Acrobat Reader DC extensions**

Prima di poter eseguire programmaticamente un’operazione del servizio Acrobat Reader DC extensions, devi creare un oggetto client del servizio Acrobat Reader DC extensions. Se utilizzi l’API Java, crea un oggetto `ReaderExtensionsServiceClient`. Se utilizzi l’API del servizio Web Acrobat Reader DC extensions, crea un oggetto `ReaderExtensionsServiceService` .

**Recuperare un documento PDF abilitato per i diritti**

Recuperare un documento PDF abilitato per i diritti per rimuovere i diritti di utilizzo.

**Rimuovere i diritti di utilizzo dal documento PDF**

Dopo aver recuperato un documento PDF abilitato per i diritti, è possibile rimuovere i diritti di utilizzo. Dopo aver rimosso i diritti di utilizzo, il documento PDF non disporrà di funzionalità aggiuntive durante la visualizzazione in Adobe Reader.

**Salvare il documento PDF**

È possibile salvare il documento PDF che non contiene più diritti di utilizzo come file PDF. Una volta salvato come file PDF, il documento PDF può essere visualizzato in Adobe Reader o Acrobat.

**Consulta anche**

[Rimuovere i diritti di utilizzo tramite l’API Java](assigning-usage-rights.md#remove-usage-rights-using-the-java-api)

[Rimuovere i diritti di utilizzo tramite l’API del servizio Web](assigning-usage-rights.md#remove-usage-rights-using-the-web-service-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido dell&#39;API del servizio Acrobat Reader DC Extensions](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

[Applicazione dei diritti di utilizzo ai documenti PDF](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

### Rimuovere i diritti di utilizzo utilizzando l&#39;API Java {#remove-usage-rights-using-the-java-api}

È possibile rimuovere i diritti di utilizzo da un documento PDF abilitato per i diritti utilizzando l’API Acrobat Reader DC extensions (Java):

1. Includi file di progetto.

   Includi file JAR client, come adobe-reader-extensions-client.jar, nel percorso di classe del progetto Java.

1. Crea un oggetto client Acrobat Reader DC extensions.

   Creare un oggetto `ReaderExtensionsServiceClient` utilizzando il relativo costruttore e passando un oggetto `ServiceClientFactory` contenente proprietà di connessione.

1. Recupera un documento PDF.

   * Creare un oggetto `java.io.FileInputStream` che rappresenti il documento PDF abilitato per i diritti utilizzando il relativo costruttore e passando un valore di stringa che specifichi la posizione del documento PDF.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Rimuovere i diritti di utilizzo dal documento PDF.

   Rimuovere i diritti di utilizzo dal documento PDF richiamando il metodo `removeUsageRights` dell’oggetto `com.adobe.idp.Document` e passando l’oggetto `ReaderExtensionsServiceClient` che contiene il documento PDF abilitato per i diritti. Questo metodo restituisce un oggetto `com.adobe.idp.Document` che contiene un documento PDF privo di diritti di utilizzo.

1. Applicare i diritti di utilizzo al documento PDF.

   * Crea un oggetto `java.io.File` e assicurati che l&#39;estensione del file sia .PDF.
   * Richiamare il metodo `copyToFile` dell&#39;oggetto `Document` per copiare il contenuto dell&#39;oggetto `Document` nel file (assicurarsi di utilizzare l&#39;oggetto `Document` restituito dal metodo `removeUsageRights`).

**Consulta anche**

[Rimozione dei diritti di utilizzo dai documenti PDF](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)

[Avvio rapido (modalità SOAP): Rimozione dei diritti di utilizzo da un documento PDF tramite l’API Java](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-removing-usage-rights-from-a-pdf-document-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Rimuovere i diritti di utilizzo utilizzando l&#39;API del servizio Web {#remove-usage-rights-using-the-web-service-api}

È possibile rimuovere i diritti di utilizzo da un documento PDF abilitato per i diritti utilizzando l’API delle estensioni Acrobat Reader DC (servizio Web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurati di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Crea un oggetto client Acrobat Reader DC extensions.

   * Creare un oggetto `ReaderExtensionsServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `ReaderExtensionsServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`. Assicurati di specificare `?blob=mtom`.)
   * Crea un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `ReaderExtensionsServiceClient.Endpoint.Binding` . Imposta il valore restituito su `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegna il nome utente del modulo di AEM al campo `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore della password corrispondente al campo `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recupera un documento PDF.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare il documento PDF abilitato per i diritti da cui vengono rimossi i diritti di utilizzo.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni dell&#39;array di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare l’array di byte con i dati del flusso richiamando il metodo `Read` dell’oggetto `System.IO.FileStream` e passando l’array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando la relativa proprietà `MTOM` con il contenuto dell&#39;array di byte.

1. Rimuovere i diritti di utilizzo dal documento PDF.

   Rimuovere i diritti di utilizzo dal documento PDF richiamando il metodo `removeUsageRights` dell’oggetto `BLOB` e passando l’oggetto `ReaderExtensionsServiceClient` che contiene il documento PDF abilitato per i diritti. Questo metodo restituisce un oggetto `BLOB` che contiene un documento PDF privo di diritti di utilizzo.

1. Applicare i diritti di utilizzo al documento PDF.

   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file PDF.
   * Creare una matrice di byte che memorizza il contenuto dei dati dell&#39;oggetto `BLOB` restituito dal metodo `removeUsageRights`. Compilare l&#39;array di byte ottenendo il valore del membro dati `BLOB` dell&#39;oggetto `MTOM`.
   * Creare un oggetto `System.IO.BinaryWriter` richiamandone il costruttore e passando l&#39;oggetto `System.IO.FileStream`.

**Consulta anche**

[Rimozione dei diritti di utilizzo dai documenti PDF](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)

[Richiamo di AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamo di AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Recupero informazioni sulle credenziali {#retrieving-credential-information}

È possibile recuperare informazioni sulle credenziali utilizzate per applicare diritti di utilizzo a un documento PDF abilitato per i diritti. Il recupero di informazioni su una credenziale consente di ottenere informazioni quali la data successiva alla quale il certificato non è più valido.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Acrobat Reader DC extensions, consulta [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary_of_steps-2}

Per recuperare informazioni sulle credenziali utilizzate per applicare diritti di utilizzo a un documento PDF, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Crea un oggetto client Acrobat Reader DC extensions.
1. Recupera un documento PDF abilitato per i diritti.
1. Recupera informazioni sulla credenziale.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

**Creare un oggetto client Acrobat Reader DC extensions**

Prima di poter eseguire programmaticamente un’operazione del servizio Acrobat Reader DC extensions, devi creare un oggetto client del servizio Acrobat Reader DC extensions. Se utilizzi l’API Java, crea un oggetto `ReaderExtensionsServiceClient`. Se utilizzi l’API del servizio Web Acrobat Reader DC extensions, crea un oggetto `ReaderExtensionsServiceService` .

**Recuperare un documento PDF abilitato per i diritti**

Per recuperare informazioni sulle credenziali, è necessario recuperare un documento PDF abilitato per i diritti. È inoltre possibile recuperare informazioni su una credenziale specificando il relativo alias; tuttavia, se si desidera recuperare le informazioni relative a una credenziale utilizzata per applicare diritti di utilizzo a un documento PDF con diritti specifici, è necessario recuperare il documento.

**Recupera informazioni sulla credenziale**

Dopo aver recuperato un documento PDF abilitato per i diritti, è possibile ottenere informazioni sulla credenziale utilizzata per applicarvi i diritti di utilizzo. È possibile ottenere le seguenti informazioni sulle credenziali:

* Messaggio visualizzato in Adobe Reader all’apertura del documento PDF abilitato per i diritti.
* La data successiva alla quale la credenziale non è più valida.
* Data prima della quale la credenziale non è valida.
* I diritti di utilizzo impostati per questo documento PDF abilitato per i diritti.
* Il numero di volte in cui la credenziale è stata utilizzata.

**Consulta anche**

[Rimuovere i diritti di utilizzo tramite l’API Java](assigning-usage-rights.md#remove-usage-rights-using-the-java-api)

[Rimuovere i diritti di utilizzo tramite l’API del servizio Web](assigning-usage-rights.md#remove-usage-rights-using-the-web-service-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido dell&#39;API del servizio Acrobat Reader DC Extensions](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

### Recupera le informazioni sulle credenziali utilizzando l&#39;API Java {#retrieve-credential-information-using-the-java-api}

Recupera le informazioni sulle credenziali utilizzando l’API delle estensioni Acrobat Reader DC (Java):

1. Includi file di progetto.

   Includi file JAR client, come adobe-reader-extensions-client.jar, nel percorso di classe del progetto Java.

1. Crea un oggetto client Acrobat Reader DC extensions.

   Creare un oggetto `ReaderExtensionsServiceClient` utilizzando il relativo costruttore e passando un oggetto `ServiceClientFactory` contenente proprietà di connessione.

1. Recupera un documento PDF.

   * Creare un oggetto `java.io.FileInputStream` che rappresenti il documento PDF abilitato per i diritti utilizzando il relativo costruttore e passando un valore di stringa che specifichi la posizione del documento PDF abilitato per i diritti.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Rimuovere i diritti di utilizzo dal documento PDF.

   * Recuperare le informazioni sulla credenziale utilizzata per applicare diritti di utilizzo al documento PDF richiamando il metodo `getDocumentUsageRights` dell’oggetto `ReaderExtensionsServiceClient` e passando l’oggetto `com.adobe.idp.Document` che contiene il documento PDF abilitato per i diritti. Questo metodo restituisce un oggetto `GetUsageRightsResult` contenente informazioni sulle credenziali.
   * Recupera la data successiva alla quale la credenziale non è più valida richiamando il metodo `getNotAfter` dell’oggetto `GetUsageRightsResult`. Questo metodo restituisce un oggetto `java.util.Date` che rappresenta la data successiva alla quale la credenziale non è più valida.
   * Recupera il messaggio visualizzato in Adobe Reader all’apertura del documento PDF abilitato per i diritti richiamando il metodo `getMessage` dell’oggetto `GetUsageRightsResult` . Questo metodo restituisce un valore stringa che rappresenta il messaggio.

**Consulta anche**

[Recupero delle informazioni sulle credenziali](assigning-usage-rights.md#retrieving-credential-information)

[Avvio rapido (modalità SOAP): Recupero delle informazioni sulle credenziali tramite l’API Java](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-retrieving-credential-information-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Recupera le informazioni sulle credenziali utilizzando l&#39;API del servizio Web {#retrieve-credential-information-using-the-web-service-api}

Recupera le informazioni sulle credenziali utilizzando l’API delle estensioni Acrobat Reader DC (servizio Web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurati di utilizzare la seguente definizione WSDL: `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Crea un oggetto client Acrobat Reader DC extensions.

   * Creare un oggetto `ReaderExtensionsServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `ReaderExtensionsServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms (ad esempio, `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`. Assicurati di specificare `?blob=mtom`.)
   * Crea un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `ReaderExtensionsServiceClient.Endpoint.Binding` . Imposta il valore restituito su `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegna il nome utente del modulo di AEM al campo `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`.
      * Assegna il valore della password corrispondente al campo `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recupera un documento PDF.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare un documento PDF abilitato per i diritti.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF abilitato per i diritti e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni dell&#39;array di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare l’array di byte con i dati del flusso richiamando il metodo `Read` dell’oggetto `System.IO.FileStream` e passando l’array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando la relativa proprietà `MTOM` con il contenuto dell&#39;array di byte.

1. Rimuovere i diritti di utilizzo dal documento PDF.

   * Recuperare le informazioni sulla credenziale utilizzata per applicare diritti di utilizzo al documento PDF richiamando il metodo `getDocumentUsageRights` dell’oggetto `ReaderExtensionsServiceClient` e passando l’oggetto `com.adobe.idp.Document` che contiene il documento PDF abilitato per i diritti. Questo metodo restituisce un oggetto `GetUsageRightsResult` contenente informazioni sulle credenziali.
   * Recupera la data successiva alla quale la credenziale non è più valida ottenendo il valore del membro dati `GetUsageRightsResult` dell’oggetto `notAfter`. Il tipo di dati del membro è `System.DateTime`.
   * Recupera il messaggio visualizzato quando il documento PDF abilitato per i diritti viene aperto in Adobe Reader ottenendo il valore del membro dati `GetUsageRightsResult` dell’oggetto `message`. Il tipo di dati di questo membro dati è una stringa.
   * Recupera il numero di volte in cui la credenziale viene utilizzata ottenendo il valore del membro dati `GetUsageRightsResult` dell’oggetto `useCount`. Il tipo di dati del membro dati è un numero intero.

**Consulta anche**

[Recupero delle informazioni sulle credenziali](assigning-usage-rights.md#retrieving-credential-information)

[Richiamo di AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Richiamo di AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
