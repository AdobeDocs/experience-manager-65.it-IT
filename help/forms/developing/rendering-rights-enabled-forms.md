---
title: Forms con diritti di rendering
seo-title: Forms con diritti di rendering
description: 'null'
seo-description: 'null'
uuid: ce5e4be6-d9b0-4989-a0e1-a8c3b98aed77
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: d4c2b2f0-613a-409d-b39b-8e37fdb96eea
translation-type: tm+mt
source-git-commit: 7cbe3e94eddb81925072f68388649befbb027e6d
workflow-type: tm+mt
source-wordcount: '1441'
ht-degree: 0%

---


# Forms con diritti di rendering {#rendering-rights-enabled-forms}

Il servizio Forms può eseguire il rendering dei moduli a cui sono stati applicati diritti di utilizzo. I diritti di utilizzo si riferiscono a funzionalità disponibili per impostazione predefinita in  Acrobat ma non in  Adobe Reader, ad esempio la possibilità di aggiungere commenti a un modulo o di compilare campi modulo e salvare il modulo. I Forms a cui sono stati applicati diritti di utilizzo sono denominati moduli abilitati per i diritti. L&#39;utente che apre un modulo con diritti in  Adobe Reader può eseguire le operazioni abilitate per tale modulo.

Per applicare diritti di utilizzo a un modulo, il servizio di estensione Acrobat Reader DC deve far parte dell&#39;installazione dei moduli AEM. Inoltre, è necessario disporre di una credenziale valida che consenta di applicare diritti di utilizzo ai documenti PDF. In altre parole, è necessario configurare correttamente il servizio di estensione Acrobat Reader DC prima di poter eseguire il rendering di un modulo abilitato per i diritti. (Vedere [Informazioni su Acrobat Reader DC extensions Service](/help/forms/developing/assigning-usage-rights.md#about-the-acrobat-reader-dc-extensions-service).)

>[!NOTE]
>
>Per eseguire il rendering di un modulo che contiene diritti di utilizzo, è necessario utilizzare un file XDP come input, non come file PDF. Se si utilizza un file PDF come input, viene comunque eseguito il rendering del modulo; tuttavia, non sarà un modulo abilitato per i diritti.

>[!NOTE]
>
>Non è possibile precompilare un modulo con dati XML se si specificano i seguenti diritti di utilizzo: `enableComments`, `enableCommentsOnline`, `enableEmbeddedFiles` o `enableDigitalSignatures`. (Vedere [Precompilazione di Forms con layout scorrevoli](/help/forms/developing/prepopulating-forms-flowable-layouts.md).)

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Forms, vedere [Guida di riferimento dei servizi per  AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Riepilogo dei passaggi {#summary-of-steps}

Per eseguire il rendering di un modulo abilitato per i diritti, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un oggetto Forms Client API.
1. Impostare le opzioni di esecuzione dei diritti di utilizzo.
1. Eseguire il rendering di un modulo abilitato per i diritti.
1. Scrivete il modulo abilitato per i diritti nel browser Web del client.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, accertatevi di includere i file proxy.

**Creare un oggetto Forms Client API**

Prima di eseguire un&#39;operazione API client di Forms Service a livello di programmazione, è necessario creare un client di servizi Forms.

**Impostazione delle opzioni di esecuzione dei diritti di utilizzo**

È necessario impostare le opzioni di esecuzione dei diritti di utilizzo per eseguire il rendering di un modulo abilitato per i diritti. È inoltre necessario specificare l&#39;alias della credenziale utilizzata per applicare i diritti di utilizzo a un modulo. Dopo aver specificato il valore alias, è possibile specificare ogni diritto di utilizzo da applicare al modulo.

**Rendering di un modulo abilitato per i diritti**

Per eseguire il rendering di un modulo abilitato per i diritti, è necessario utilizzare la stessa logica di applicazione utilizzata per il rendering di un modulo senza diritti di utilizzo. L&#39;unica differenza è che devi assicurarti che le opzioni di runtime dei diritti di utilizzo siano incluse nella logica dell&#39;applicazione.

>[!NOTE]
>
>Quando si esegue il rendering di un modulo abilitato per i diritti tramite l&#39;API del servizio Web di Forms, non è possibile allegare file al modulo.

**Scrivere il flusso di dati del modulo nel browser Web del client**

Quando il servizio Forms esegue il rendering di un modulo abilitato per i diritti, restituisce un flusso di dati del modulo che è necessario scrivere nel browser Web del client. Una volta scritto nel browser Web del client, il modulo è visibile all&#39;utente. Un utente che visualizza il modulo con diritti abilitati in  Adobe Reader è in grado di eseguire le operazioni abilitate per tale modulo.

**Consulta anche**

[Rendering di moduli abilitati per i diritti tramite l&#39;API Java](#render-rights-enabled-forms-using-the-java-api)

[Rendering di moduli abilitati per i diritti tramite l&#39;API del servizio Web](#render-rights-enabled-forms-using-the-web-service-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido di Forms Service API](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Rendering di PDF forms interattivi](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Creazione di applicazioni Web per il rendering di Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

### Eseguire il rendering dei moduli abilitati per i diritti tramite l&#39;API Java {#render-rights-enabled-forms-using-the-java-api}

Eseguire il rendering di un modulo abilitato per i diritti utilizzando l&#39;API Forms (Java):

1. Includi file di progetto

   Includete file JAR client, ad esempio adobe-forms-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto Forms Client API

   * Creare un oggetto `ServiceClientFactory` che contiene le proprietà di connessione.
   * Creare un oggetto `FormsServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Impostazione delle opzioni di esecuzione dei diritti di utilizzo

   * Creare un oggetto `ReaderExtensionSpec` utilizzando il relativo costruttore.
   * Specificare l&#39;alias della credenziale richiamando il metodo `setReCredentialAlias` dell&#39;oggetto `ReaderExtensionSpec` e specificare un valore di stringa che rappresenta il valore alias.
   * Impostare ogni diritto di utilizzo richiamando il metodo corrispondente che appartiene all&#39;oggetto `ReaderExtensionSpec`. Tuttavia, è possibile impostare un diritto di utilizzo solo se la credenziale a cui si fa riferimento consente di farlo. In altre parole, non è possibile impostare un diritto di utilizzo se la credenziale non consente di impostarlo. Esempio. per impostare il diritto di utilizzo che consente all&#39;utente di compilare i campi del modulo e salvarlo, richiamare il metodo `ReaderExtensionSpec` dell&#39;oggetto `setReFillIn` e passare `true`.

   >[!NOTE]
   >
   >Non è necessario richiamare il metodo `ReaderExtensionSpec` dell&#39;oggetto `setReCredentialPassword`. Questo metodo non è utilizzato dal servizio Forms.

1. Rendering di un modulo abilitato per i diritti

   Richiamare il metodo `FormsServiceClient` dell&#39;oggetto `renderPDFFormWithUsageRights` e trasmettere i seguenti valori:

   * Una stringa che specifica il nome della struttura del modulo, inclusa l&#39;estensione del nome file. Se si fa riferimento a una struttura del modulo che fa parte di un&#39;applicazione Forms, è necessario specificare il percorso completo, ad esempio `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Un oggetto `com.adobe.idp.Document` che contiene i dati da unire al modulo. Se non si desidera unire i dati, passare un oggetto `com.adobe.idp.Document` vuoto.
   * Un oggetto `PDFFormRenderSpec` che memorizza le opzioni di esecuzione.
   * Un oggetto `ReaderExtensionSpec` che memorizza le opzioni di esecuzione dei diritti di utilizzo.
   * Un oggetto `URLSpec` che contiene valori URI richiesti dal servizio Forms.

   Il metodo `renderPDFFormWithUsageRights` restituisce un oggetto `FormsResult` contenente un flusso di dati del modulo che deve essere scritto nel browser Web del client.

1. Scrivere il flusso di dati del modulo nel browser Web del client

   * Creare un oggetto `com.adobe.idp.Document` richiamando il metodo `FormsResult` object ‘s `getOutputContent`.
   * Ottenere il tipo di contenuto dell&#39;oggetto `com.adobe.idp.Document` richiamandone il metodo `getContentType`.
   * Impostare il tipo di contenuto dell&#39;oggetto `javax.servlet.http.HttpServletResponse` richiamandone il metodo `setContentType` e passando il tipo di contenuto dell&#39;oggetto `com.adobe.idp.Document`.
   * Creare un oggetto `javax.servlet.ServletOutputStream` utilizzato per scrivere il flusso di dati del modulo nel browser Web del client richiamando il metodo `javax.servlet.http.HttpServletResponse` dell&#39;oggetto `getOutputStream`.
   * Creare un oggetto `java.io.InputStream` richiamando il metodo `com.adobe.idp.Document` dell&#39;oggetto `getInputStream`.
   * Per creare un array di byte, è necessario inserirlo nel flusso di dati del modulo richiamando il metodo `InputStream` dell&#39;oggetto &lt;a1/> e passando l&#39;array di byte come argomento.`read`
   * Richiamare il metodo `javax.servlet.ServletOutputStream` dell&#39;oggetto `write` per inviare il flusso di dati del modulo al browser Web del client. Passate l&#39;array di byte al metodo `write`.

**Consulta anche**

[Avvio rapido (modalità SOAP): Rendering di un modulo abilitato per i diritti mediante l&#39;API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-rights-enabled-form-using-the-java-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Eseguire il rendering dei moduli abilitati per i diritti tramite l&#39;API del servizio Web {#render-rights-enabled-forms-using-the-web-service-api}

Eseguire il rendering di un modulo abilitato per i diritti utilizzando l&#39;API di Forms (servizio Web):

1. Includi file di progetto

   * Creare classi proxy Java che utilizzano il servizio WSDL di Forms.
   * Includete le classi proxy Java nel percorso della classe.

1. Creare un oggetto Forms Client API

   Creare un oggetto `FormsService` e impostare i valori di autenticazione.

1. Impostazione delle opzioni di esecuzione dei diritti di utilizzo

   * Creare un oggetto `ReaderExtensionSpec` utilizzando il relativo costruttore.
   * Specificare l&#39;alias della credenziale richiamando il metodo `setReCredentialAlias` dell&#39;oggetto `ReaderExtensionSpec` e specificare un valore di stringa che rappresenta il valore alias.
   * Impostare ogni diritto di utilizzo richiamando il metodo corrispondente che appartiene all&#39;oggetto `ReaderExtensionSpec`. Tuttavia, è possibile impostare un diritto di utilizzo solo se la credenziale a cui si fa riferimento consente di farlo. In altre parole, non è possibile impostare un diritto di utilizzo se la credenziale non consente di impostarlo. Per impostare il diritto di utilizzo che consente all&#39;utente di compilare i campi del modulo e salvare il modulo, richiamare il metodo `ReaderExtensionSpec` dell&#39;oggetto `setReFillIn` e passare `true`.

1. Rendering di un modulo abilitato per i diritti

   Richiamare il metodo `FormsService` dell&#39;oggetto `renderPDFFormWithUsageRights` e trasmettere i seguenti valori:

   * Una stringa che specifica il nome della struttura del modulo, inclusa l&#39;estensione del nome file. Se si fa riferimento a una struttura del modulo che fa parte di un&#39;applicazione Forms, è necessario specificare il percorso completo, ad esempio `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Un oggetto `BLOB` che contiene i dati da unire al modulo. Se non si desidera unire i dati al modulo, è necessario passare un oggetto `BLOB` basato su un&#39;origine dati XML vuota. Non è possibile passare un oggetto `BLOB` nullo; in caso contrario, viene generata un&#39;eccezione.
   * Un oggetto `PDFFormRenderSpec` che memorizza le opzioni di esecuzione.
   * Un oggetto `ReaderExtensionSpec` che memorizza le opzioni di esecuzione dei diritti di utilizzo.
   * Un oggetto `URLSpec` che contiene valori URI richiesti dal servizio Forms.

   Il metodo `renderPDFFormWithUsageRights` restituisce un oggetto `FormsResult` contenente un flusso di dati del modulo che deve essere scritto nel browser Web del client.

1. Scrivere il flusso di dati del modulo nel browser Web del client

   * Creare un oggetto `BLOB` contenente dati del modulo richiamando il metodo `FormsResult` dell&#39;oggetto `getOutputContent`.
   * Ottenere il tipo di contenuto dell&#39;oggetto `BLOB` richiamandone il metodo `getContentType`.
   * Impostare il tipo di contenuto dell&#39;oggetto `javax.servlet.http.HttpServletResponse` richiamandone il metodo `setContentType` e passando il tipo di contenuto dell&#39;oggetto `BLOB`.
   * Creare un oggetto `javax.servlet.ServletOutputStream` utilizzato per scrivere il flusso di dati del modulo nel browser Web del client richiamando il metodo `javax.servlet.http.HttpServletResponse` dell&#39;oggetto `getOutputStream`.
   * Creare un array di byte e compilarlo richiamando il metodo `BLOB` dell&#39;oggetto `getBinaryData`. Questa attività assegna il contenuto dell&#39;oggetto `FormsResult` all&#39;array di byte.
   * Richiamare il metodo `javax.servlet.http.HttpServletResponse` dell&#39;oggetto `write` per inviare il flusso di dati del modulo al browser Web del client. Passate l&#39;array di byte al metodo `write`.

**Consulta anche**

[Forms con diritti di rendering](#rendering-rights-enabled-forms)

[Richiamo  AEM Forms con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
