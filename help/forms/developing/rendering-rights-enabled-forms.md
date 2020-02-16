---
title: Rendering di moduli abilitati per i diritti
seo-title: Rendering di moduli abilitati per i diritti
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

---


# Rendering di moduli abilitati per i diritti {#rendering-rights-enabled-forms}

Il servizio Forms consente di eseguire il rendering dei moduli a cui sono stati applicati diritti di utilizzo. I diritti di utilizzo si riferiscono a funzionalità disponibili per impostazione predefinita in Acrobat ma non in Adobe Reader, ad esempio la possibilità di aggiungere commenti a un modulo o di compilare campi modulo e salvare il modulo. I moduli a cui sono stati applicati diritti di utilizzo sono denominati moduli abilitati per i diritti. L&#39;utente che apre un modulo con diritti in Adobe Reader può eseguire le operazioni abilitate per tale modulo.

Per applicare diritti di utilizzo a un modulo, il servizio di estensione Acrobat Reader DC deve far parte dell&#39;installazione dei moduli AEM. Inoltre, è necessario disporre di una credenziale valida che consenta di applicare diritti di utilizzo ai documenti PDF. In altre parole, è necessario configurare correttamente il servizio di estensione Acrobat Reader DC per poter eseguire il rendering di un modulo con diritti. (Vedere [Informazioni su Acrobat Reader DC Extensions Service](/help/forms/developing/assigning-usage-rights.md#about-the-acrobat-reader-dc-extensions-service).)

>[!NOTE]
>
>Per eseguire il rendering di un modulo che contiene diritti di utilizzo, è necessario utilizzare un file XDP come input, non come file PDF. Se si utilizza un file PDF come input, viene comunque eseguito il rendering del modulo; tuttavia, non sarà un modulo abilitato per i diritti.

>[!NOTE]
>
>Non è possibile precompilare un modulo con dati XML se si specificano i seguenti diritti di utilizzo: `enableComments`, `enableCommentsOnline`, `enableEmbeddedFiles`o `enableDigitalSignatures`. (Vedere [Precompilazione dei moduli con layout](/help/forms/developing/prepopulating-forms-flowable-layouts.md)scorrevoli.)

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Forms, consultate Riferimento [servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Riepilogo dei passaggi {#summary-of-steps}

Per eseguire il rendering di un modulo con diritti, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un oggetto API client Forms.
1. Impostare le opzioni di esecuzione dei diritti di utilizzo.
1. Eseguire il rendering di un modulo abilitato per i diritti.
1. Scrivete il modulo abilitato per i diritti nel browser Web del client.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, accertatevi di includere i file proxy.

**Creare un oggetto API client Forms**

Prima di eseguire un&#39;operazione API client del servizio Forms a livello di programmazione, è necessario creare un client del servizio Forms.

**Impostazione delle opzioni di esecuzione dei diritti di utilizzo**

È necessario impostare le opzioni di esecuzione dei diritti di utilizzo per eseguire il rendering di un modulo abilitato per i diritti. È inoltre necessario specificare l&#39;alias della credenziale utilizzata per applicare i diritti di utilizzo a un modulo. Dopo aver specificato il valore alias, è possibile specificare ogni diritto di utilizzo da applicare al modulo.

**Rendering di un modulo abilitato per i diritti**

Per eseguire il rendering di un modulo abilitato per i diritti, è necessario utilizzare la stessa logica di applicazione utilizzata per il rendering di un modulo senza diritti di utilizzo. L&#39;unica differenza è che devi assicurarti che le opzioni di runtime dei diritti di utilizzo siano incluse nella logica dell&#39;applicazione.

>[!NOTE]
>
>Quando si esegue il rendering di un modulo abilitato per i diritti tramite l&#39;API del servizio Web Forms, non è possibile allegare file al modulo.

**Scrivere il flusso di dati del modulo nel browser Web del client**

Quando il servizio Forms esegue il rendering di un modulo abilitato per i diritti, restituisce un flusso di dati del modulo che è necessario scrivere nel browser Web del client. Una volta scritto nel browser Web del client, il modulo è visibile all&#39;utente. Un utente che visualizza il modulo con diritti abilitati in Adobe Reader può eseguire le operazioni abilitate per tale modulo.

**Consulta anche**

[Rendering di moduli abilitati per i diritti tramite l&#39;API Java](#render-rights-enabled-forms-using-the-java-api)

[Rendering di moduli abilitati per i diritti tramite l&#39;API del servizio Web](#render-rights-enabled-forms-using-the-web-service-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido dell&#39;API di Forms Service](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Rendering di moduli PDF interattivi](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Creazione di applicazioni Web per il rendering di moduli](/help/forms/developing/creating-web-applications-renders-forms.md)

### Rendering di moduli abilitati per i diritti tramite l&#39;API Java {#render-rights-enabled-forms-using-the-java-api}

Eseguire il rendering di un modulo abilitato per i diritti utilizzando l&#39;API Forms (Java):

1. Includi file di progetto

   Includete file JAR client, ad esempio adobe-forms-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto API client Forms

   * Creare un `ServiceClientFactory` oggetto che contenga proprietà di connessione.
   * Creare un `FormsServiceClient` oggetto utilizzando il relativo costruttore e passando l&#39; `ServiceClientFactory` oggetto.

1. Impostazione delle opzioni di esecuzione dei diritti di utilizzo

   * Creare un `ReaderExtensionSpec` oggetto utilizzando il relativo costruttore.
   * Specificare l&#39;alias della credenziale richiamando il metodo dell&#39; `ReaderExtensionSpec` oggetto `setReCredentialAlias` e specificare un valore di stringa che rappresenta il valore alias.
   * Impostare ogni diritto di utilizzo richiamando il metodo corrispondente che appartiene all&#39; `ReaderExtensionSpec` oggetto. Tuttavia, è possibile impostare un diritto di utilizzo solo se la credenziale a cui si fa riferimento consente di farlo. In altre parole, non è possibile impostare un diritto di utilizzo se la credenziale non consente di impostarlo. Esempio. per impostare il diritto di utilizzo che consente all&#39;utente di compilare i campi del modulo e salvarlo, richiamare il metodo dell&#39; `ReaderExtensionSpec` oggetto `setReFillIn` e passare `true`.
   >[!NOTE]
   >
   >Non è necessario richiamare il metodo `ReaderExtensionSpec` dell&#39;oggetto `setReCredentialPassword` . Questo metodo non è utilizzato dal servizio Forms.

1. Rendering di un modulo abilitato per i diritti

   Richiama il metodo dell’ `FormsServiceClient` oggetto `renderPDFFormWithUsageRights` e passa i seguenti valori:

   * Una stringa che specifica il nome della struttura del modulo, inclusa l&#39;estensione del nome file. Se si fa riferimento a una struttura del modulo che fa parte di un&#39;applicazione Forms, è necessario specificare il percorso completo, ad esempio `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Un `com.adobe.idp.Document` oggetto che contiene i dati da unire al modulo. Se non si desidera unire i dati, passare un `com.adobe.idp.Document` oggetto vuoto.
   * Un `PDFFormRenderSpec` oggetto che memorizza le opzioni di esecuzione.
   * Un `ReaderExtensionSpec` oggetto che memorizza le opzioni di esecuzione dei diritti di utilizzo.
   * Un `URLSpec` oggetto che contiene valori URI richiesti dal servizio Forms.
   Il `renderPDFFormWithUsageRights` metodo restituisce un `FormsResult` oggetto che contiene un flusso di dati del modulo da scrivere nel browser Web del client.

1. Scrivere il flusso di dati del modulo nel browser Web del client

   * Creare un `com.adobe.idp.Document` oggetto richiamando il `FormsResult` metodo ‘s `getOutputContent` .
   * Ottenere il tipo di contenuto dell&#39; `com.adobe.idp.Document` oggetto richiamandone il `getContentType` metodo.
   * Impostare il tipo di contenuto dell&#39; `javax.servlet.http.HttpServletResponse` oggetto richiamandone `setContentType` il metodo e passando il tipo di contenuto dell&#39; `com.adobe.idp.Document` oggetto.
   * Creare un `javax.servlet.ServletOutputStream` oggetto utilizzato per scrivere il flusso di dati del modulo nel browser Web del client richiamando il `javax.servlet.http.HttpServletResponse` metodo dell&#39; `getOutputStream` oggetto.
   * Creare un `java.io.InputStream` oggetto richiamando il `com.adobe.idp.Document` metodo dell&#39; `getInputStream` oggetto.
   * Per creare un array di byte, è necessario inserirlo nel flusso di dati del modulo richiamando il metodo dell&#39; `InputStream` `read` oggetto e passando l&#39;array di byte come argomento.
   * Richiamare il metodo dell&#39; `javax.servlet.ServletOutputStream` oggetto `write` per inviare il flusso di dati del modulo al browser Web del client. Passa l&#39;array di byte al `write` metodo.

**Consulta anche**

[Avvio rapido (modalità SOAP): Rendering di un modulo abilitato per i diritti mediante l&#39;API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-rights-enabled-form-using-the-java-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Rendering di moduli abilitati per i diritti tramite l&#39;API del servizio Web {#render-rights-enabled-forms-using-the-web-service-api}

Eseguire il rendering di un modulo abilitato per i diritti utilizzando l&#39;API Forms (servizio Web):

1. Includi file di progetto

   * Creare classi proxy Java che utilizzano il WSDL del servizio Forms.
   * Includete le classi proxy Java nel percorso della classe.

1. Creare un oggetto API client Forms

   Creare un `FormsService` oggetto e impostare i valori di autenticazione.

1. Impostazione delle opzioni di esecuzione dei diritti di utilizzo

   * Creare un `ReaderExtensionSpec` oggetto utilizzando il relativo costruttore.
   * Specificare l&#39;alias della credenziale richiamando il metodo dell&#39; `ReaderExtensionSpec` oggetto `setReCredentialAlias` e specificare un valore di stringa che rappresenta il valore alias.
   * Impostare ogni diritto di utilizzo richiamando il metodo corrispondente che appartiene all&#39; `ReaderExtensionSpec` oggetto. Tuttavia, è possibile impostare un diritto di utilizzo solo se la credenziale a cui si fa riferimento consente di farlo. In altre parole, non è possibile impostare un diritto di utilizzo se la credenziale non consente di impostarlo. Per impostare il diritto di utilizzo che consente all&#39;utente di compilare i campi del modulo e salvarlo, richiamare il metodo dell&#39; `ReaderExtensionSpec` oggetto `setReFillIn` e passare `true`.

1. Rendering di un modulo abilitato per i diritti

   Richiama il metodo dell’ `FormsService` oggetto `renderPDFFormWithUsageRights` e passa i seguenti valori:

   * Una stringa che specifica il nome della struttura del modulo, inclusa l&#39;estensione del nome file. Se si fa riferimento a una struttura del modulo che fa parte di un&#39;applicazione Forms, è necessario specificare il percorso completo, ad esempio `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Un `BLOB` oggetto che contiene i dati da unire al modulo. Se non si desidera unire i dati al modulo, è necessario passare un `BLOB` oggetto basato su un&#39;origine dati XML vuota. Non è possibile trasmettere un `BLOB` oggetto nullo; in caso contrario, viene generata un&#39;eccezione.
   * Un `PDFFormRenderSpec` oggetto che memorizza le opzioni di esecuzione.
   * Un `ReaderExtensionSpec` oggetto che memorizza le opzioni di esecuzione dei diritti di utilizzo.
   * Un `URLSpec` oggetto che contiene valori URI richiesti dal servizio Forms.
   Il `renderPDFFormWithUsageRights` metodo restituisce un `FormsResult` oggetto che contiene un flusso di dati del modulo da scrivere nel browser Web del client.

1. Scrivere il flusso di dati del modulo nel browser Web del client

   * Creare un `BLOB` oggetto che contenga dati del modulo richiamando il `FormsResult` metodo dell&#39; `getOutputContent` oggetto.
   * Ottenere il tipo di contenuto dell&#39; `BLOB` oggetto richiamandone il `getContentType` metodo.
   * Impostare il tipo di contenuto dell&#39; `javax.servlet.http.HttpServletResponse` oggetto richiamandone `setContentType` il metodo e passando il tipo di contenuto dell&#39; `BLOB` oggetto.
   * Creare un `javax.servlet.ServletOutputStream` oggetto utilizzato per scrivere il flusso di dati del modulo nel browser Web del client richiamando il `javax.servlet.http.HttpServletResponse` metodo dell&#39; `getOutputStream` oggetto.
   * Creare un array di byte e compilarlo richiamando il metodo dell&#39; `BLOB` oggetto `getBinaryData` . Questa attività assegna il contenuto dell&#39; `FormsResult` oggetto all&#39;array di byte.
   * Richiamare il metodo dell&#39; `javax.servlet.http.HttpServletResponse` oggetto `write` per inviare il flusso di dati del modulo al browser Web del client. Passa l&#39;array di byte al `write` metodo.

**Consulta anche**

[Rendering di moduli abilitati per i diritti](#rendering-rights-enabled-forms)

[Richiamo di moduli AEM con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
