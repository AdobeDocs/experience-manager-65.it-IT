---
title: Forms con diritti di rendering
description: Utilizza il servizio Forms per eseguire il rendering dei moduli a cui sono applicati diritti di utilizzo. Puoi eseguire il rendering di moduli abilitati per i diritti utilizzando l’API Java e l’API del servizio web.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 012a3a9f-542c-4ed1-a092-572bfccbdf21
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1447'
ht-degree: 0%

---

# Forms con diritti di rendering {#rendering-rights-enabled-forms}

Il servizio Forms può eseguire il rendering di moduli a cui sono applicati diritti di utilizzo. I diritti di utilizzo riguardano funzionalità disponibili per impostazione predefinita in Acrobat ma non in Adobe Reader, ad esempio la possibilità di aggiungere commenti a un modulo o di compilare campi modulo e salvare il modulo. I Forms a cui sono applicati diritti di utilizzo sono denominati moduli abilitati per i diritti. L’utente che apre un modulo abilitato ai diritti in Adobe Reader può eseguire operazioni che sono abilitate per tale modulo.

Per applicare i diritti di utilizzo a un modulo, il servizio Acrobat Reader DC extensions deve far parte dell’installazione dei moduli AEM. Inoltre, è necessario disporre di una credenziale valida che consenta di applicare i diritti di utilizzo ai documenti PDF. In altre parole, è necessario configurare correttamente il servizio Estensioni di Acrobat Reader DC prima di poter eseguire il rendering di un modulo abilitato per i diritti. (vedere [Informazioni sul servizio estensioni Acrobat Reader DC](/help/forms/developing/assigning-usage-rights.md#about-the-acrobat-reader-dc-extensions-service).)

>[!NOTE]
>
>Per eseguire il rendering di un modulo che contiene diritti di utilizzo, è necessario utilizzare un file XDP come input, non un file PDF. Se si utilizza un file PDF come input, il modulo viene comunque sottoposto a rendering, ma non sarà un modulo abilitato per i diritti.

>[!NOTE]
>
>Non è possibile precompilare un modulo con dati XML quando si specificano i seguenti diritti di utilizzo: `enableComments`, `enableCommentsOnline`, `enableEmbeddedFiles`, o `enableDigitalSignatures`. (vedere [Precompilazione di Forms con layout fluibili](/help/forms/developing/prepopulating-forms-flowable-layouts.md).)

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Forms, consulta [Guida di riferimento dei servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Riepilogo dei passaggi {#summary-of-steps}

Per eseguire il rendering di un modulo abilitato per i diritti, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Crea un oggetto API client di Forms.
1. Impostare le opzioni di runtime dei diritti di utilizzo.
1. Eseguire il rendering di un modulo abilitato per i diritti.
1. Scrivere il modulo abilitato ai diritti nel browser Web client.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

**Creare un oggetto API client di Forms**

Prima di poter eseguire a livello di programmazione un&#39;operazione API client del servizio Forms, è necessario creare un client del servizio Forms.

**Impostare le opzioni di runtime dei diritti di utilizzo**

Impostare le opzioni di runtime relative ai diritti di utilizzo per eseguire il rendering di un modulo abilitato ai diritti. Specificare l&#39;alias delle credenziali utilizzato per applicare i diritti di utilizzo a un modulo. Dopo aver specificato il valore dell&#39;alias, specificare ogni diritto di utilizzo da applicare al modulo.

**Eseguire il rendering di un modulo abilitato per i diritti**

Per eseguire il rendering di un modulo abilitato per i diritti, utilizzare la stessa logica di applicazione utilizzata per il rendering di un modulo senza diritti di utilizzo. L&#39;unica differenza consiste nel fatto che è necessario assicurarsi che le opzioni di runtime dei diritti di utilizzo siano incluse nella logica dell&#39;applicazione.

>[!NOTE]
>
>Quando si esegue il rendering di un modulo abilitato ai diritti tramite l’API del servizio Web Forms, non è possibile allegare file al modulo.

**Scrivere il flusso di dati del modulo nel browser Web client**

Quando il servizio Forms esegue il rendering di un modulo abilitato ai diritti, restituisce un flusso di dati del modulo che è necessario scrivere nel browser Web client. Una volta scritto sul browser web client, il modulo è visibile all’utente. Un utente che visualizza il modulo abilitato ai diritti in Adobe Reader è in grado di eseguire operazioni abilitate per tale modulo.

**Consulta anche**

[Eseguire il rendering di moduli abilitati per i diritti tramite l’API Java](#render-rights-enabled-forms-using-the-java-api)

[Eseguire il rendering di moduli abilitati per i diritti tramite l’API del servizio web](#render-rights-enabled-forms-using-the-web-service-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Guida introduttiva all’API di servizio Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Rendering dei PDF forms interattivi](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Creazione di applicazioni Web per il rendering di Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

### Eseguire il rendering di moduli abilitati per i diritti tramite l’API Java {#render-rights-enabled-forms-using-the-java-api}

Eseguire il rendering di un modulo abilitato ai diritti tramite l’API Forms (Java):

1. Includi file di progetto

   Includi i file JAR client, ad esempio adobe-forms-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto API client di Forms

   * Creare un `ServiceClientFactory` oggetto che contiene proprietà di connessione.
   * Creare un `FormsServiceClient` mediante il costruttore e passando il `ServiceClientFactory` oggetto.

1. Impostare le opzioni di runtime dei diritti di utilizzo

   * Creare un `ReaderExtensionSpec` mediante il costruttore.
   * Specificare l&#39;alias delle credenziali richiamando `ReaderExtensionSpec` dell&#39;oggetto `setReCredentialAlias` e specificare un valore stringa che rappresenti il valore alias.
   * Impostare ogni diritto di utilizzo richiamando il metodo corrispondente che appartiene al `ReaderExtensionSpec` oggetto. È tuttavia possibile impostare un diritto di utilizzo solo se le credenziali a cui si fa riferimento lo consentono. In altre parole, non è possibile impostare un diritto di utilizzo se le credenziali non consentono di impostarlo. Ad esempio. per impostare il diritto di utilizzo che consente a un utente di compilare i campi del modulo e salvare il modulo, richiamare `ReaderExtensionSpec` dell&#39;oggetto `setReFillIn` metodo e passaggio `true`.

   >[!NOTE]
   >
   >Non è necessario invocare `ReaderExtensionSpec` dell&#39;oggetto `setReCredentialPassword` metodo. Questo metodo non viene utilizzato dal servizio Forms.

1. Eseguire il rendering di un modulo abilitato per i diritti

   Richiama `FormsServiceClient` dell&#39;oggetto `renderPDFFormWithUsageRights` e trasmettere i seguenti valori:

   * Valore stringa che specifica il nome della struttura del modulo, inclusa l&#39;estensione del nome file. Se si fa riferimento a una struttura di modulo che fa parte di un&#39;applicazione Forms, assicurarsi di specificare il percorso completo, ad esempio `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `com.adobe.idp.Document` oggetto contenente dati da unire con il modulo. Se non desideri unire i dati, passa un campo vuoto `com.adobe.idp.Document` oggetto.
   * A `PDFFormRenderSpec` oggetto che memorizza le opzioni di runtime.
   * A `ReaderExtensionSpec` oggetto che memorizza le opzioni di runtime dei diritti di utilizzo.
   * A `URLSpec` oggetto contenente valori URI richiesti dal servizio Forms.

   Il `renderPDFFormWithUsageRights` il metodo restituisce un `FormsResult` oggetto contenente un flusso di dati modulo che deve essere scritto nel browser web client.

1. Scrivere il flusso di dati del modulo nel browser Web client

   * Creare un `com.adobe.idp.Document` oggetto richiamando il `FormsResult` dell&#39;oggetto `getOutputContent` metodo.
   * Ottieni il tipo di contenuto del `com.adobe.idp.Document` oggetto richiamando il relativo `getContentType` metodo.
   * Imposta il `javax.servlet.http.HttpServletResponse` tipo di contenuto dell&#39;oggetto richiamando il relativo `setContentType` e passando il tipo di contenuto del `com.adobe.idp.Document` oggetto.
   * Creare un `javax.servlet.ServletOutputStream` oggetto utilizzato per scrivere il flusso di dati del modulo nel browser web client richiamando `javax.servlet.http.HttpServletResponse` dell&#39;oggetto `getOutputStream` metodo.
   * Creare un `java.io.InputStream` oggetto richiamando il `com.adobe.idp.Document` dell&#39;oggetto `getInputStream` metodo.
   * Creare una matrice di byte compilarla con il flusso di dati del modulo richiamando `InputStream` dell&#39;oggetto `read` e passando la matrice di byte come argomento.
   * Richiama `javax.servlet.ServletOutputStream` dell&#39;oggetto `write` metodo per inviare il flusso di dati del modulo al browser web client. Passare la matrice di byte al `write` metodo.

**Consulta anche**

[Quick Start (modalità SOAP): rendering di un modulo abilitato ai diritti tramite l’API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-rights-enabled-form-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Eseguire il rendering di moduli abilitati per i diritti tramite l’API del servizio web {#render-rights-enabled-forms-using-the-web-service-api}

Eseguire il rendering di un modulo abilitato ai diritti tramite l’API di Forms (servizio web):

1. Includi file di progetto

   * Creare classi proxy Java che utilizzano il servizio Forms WSDL.
   * Includi le classi proxy Java nel percorso della classe.

1. Creare un oggetto API client di Forms

   Creare un `FormsService` e impostare i valori di autenticazione.

1. Impostare le opzioni di runtime dei diritti di utilizzo

   * Creare un `ReaderExtensionSpec` mediante il costruttore.
   * Specificare l&#39;alias delle credenziali richiamando `ReaderExtensionSpec` dell&#39;oggetto `setReCredentialAlias` e specificare un valore stringa che rappresenti il valore alias.
   * Impostare ogni diritto di utilizzo richiamando il metodo corrispondente che appartiene al `ReaderExtensionSpec` oggetto. È tuttavia possibile impostare un diritto di utilizzo solo se le credenziali a cui si fa riferimento lo consentono. In altre parole, non è possibile impostare un diritto di utilizzo se le credenziali non consentono di impostarlo. Per impostare il diritto di utilizzo che consente a un utente di compilare i campi del modulo e salvare il modulo, richiamare `ReaderExtensionSpec` dell&#39;oggetto `setReFillIn` metodo e passaggio `true`.

1. Eseguire il rendering di un modulo abilitato per i diritti

   Richiama `FormsService` dell&#39;oggetto `renderPDFFormWithUsageRights` e trasmettere i seguenti valori:

   * Valore stringa che specifica il nome della struttura del modulo, inclusa l&#39;estensione del nome file. Se si fa riferimento a una struttura di modulo che fa parte di un&#39;applicazione Forms, assicurarsi di specificare il percorso completo, ad esempio `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `BLOB` oggetto contenente dati da unire con il modulo. Se non si desidera unire i dati con il modulo, è necessario trasmettere un `BLOB` oggetto basato su un&#39;origine dati XML vuota. Non è possibile trasmettere un `BLOB` oggetto null; in caso contrario, viene generata un&#39;eccezione.
   * A `PDFFormRenderSpec` oggetto che memorizza le opzioni di runtime.
   * A `ReaderExtensionSpec` oggetto che memorizza le opzioni di runtime dei diritti di utilizzo.
   * A `URLSpec` oggetto contenente valori URI richiesti dal servizio Forms.

   Il `renderPDFFormWithUsageRights` il metodo restituisce un `FormsResult` oggetto contenente un flusso di dati modulo che deve essere scritto nel browser web client.

1. Scrivere il flusso di dati del modulo nel browser Web client

   * Creare un `BLOB` oggetto che contiene i dati del modulo richiamando `FormsResult` dell&#39;oggetto `getOutputContent` metodo.
   * Ottieni il tipo di contenuto del `BLOB` oggetto richiamando il relativo `getContentType` metodo.
   * Imposta il `javax.servlet.http.HttpServletResponse` tipo di contenuto dell&#39;oggetto richiamando il relativo `setContentType` e passando il tipo di contenuto del `BLOB` oggetto.
   * Creare un `javax.servlet.ServletOutputStream` oggetto utilizzato per scrivere il flusso di dati del modulo nel browser web client richiamando `javax.servlet.http.HttpServletResponse` dell&#39;oggetto `getOutputStream` metodo.
   * Creare una matrice di byte e popolarla richiamando il `BLOB` dell&#39;oggetto `getBinaryData` metodo. Questa attività assegna il contenuto del `FormsResult` alla matrice di byte.
   * Richiama `javax.servlet.http.HttpServletResponse` dell&#39;oggetto `write` metodo per inviare il flusso di dati del modulo al browser web client. Passare la matrice di byte al `write` metodo.

**Consulta anche**

[Forms con diritti di rendering](#rendering-rights-enabled-forms)

[Richiamare AEM Forms utilizzando la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
