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

Per applicare i diritti di utilizzo a un modulo, il servizio Acrobat Reader DC extensions deve far parte dell’installazione dei moduli AEM. Inoltre, è necessario disporre di una credenziale valida che consenta di applicare i diritti di utilizzo ai documenti PDF. In altre parole, è necessario configurare correttamente il servizio Estensioni di Acrobat Reader DC prima di poter eseguire il rendering di un modulo abilitato per i diritti. (Vedi [Informazioni sul servizio estensioni di Acrobat Reader DC](/help/forms/developing/assigning-usage-rights.md#about-the-acrobat-reader-dc-extensions-service).)

>[!NOTE]
>
>Per eseguire il rendering di un modulo che contiene diritti di utilizzo, è necessario utilizzare un file XDP come input, non un file PDF. Se si utilizza un file PDF come input, il modulo viene comunque sottoposto a rendering, ma non sarà un modulo abilitato per i diritti.

>[!NOTE]
>
>Impossibile precompilare un modulo con dati XML quando si specificano i seguenti diritti di utilizzo: `enableComments`, `enableCommentsOnline`, `enableEmbeddedFiles` o `enableDigitalSignatures`. (Vedi [Precompilazione di Forms con layout percorribili](/help/forms/developing/prepopulating-forms-flowable-layouts.md).)

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Forms, vedere [Riferimento ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `FormsServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Impostare le opzioni di runtime dei diritti di utilizzo

   * Creare un oggetto `ReaderExtensionSpec` utilizzando il relativo costruttore.
   * Specificare l&#39;alias delle credenziali richiamando il metodo `setReCredentialAlias` dell&#39;oggetto `ReaderExtensionSpec` e specificare un valore stringa che rappresenti il valore alias.
   * Impostare ogni diritto di utilizzo richiamando il metodo corrispondente che appartiene all&#39;oggetto `ReaderExtensionSpec`. È tuttavia possibile impostare un diritto di utilizzo solo se le credenziali a cui si fa riferimento lo consentono. In altre parole, non è possibile impostare un diritto di utilizzo se le credenziali non consentono di impostarlo. Ad esempio. per impostare il diritto di utilizzo che consente a un utente di compilare i campi del modulo e salvare il modulo, richiamare il metodo `setReFillIn` dell&#39;oggetto `ReaderExtensionSpec` e passare `true`.

   >[!NOTE]
   >
   >Impossibile richiamare il metodo `setReCredentialPassword` dell&#39;oggetto `ReaderExtensionSpec`. Questo metodo non viene utilizzato dal servizio Forms.

1. Eseguire il rendering di un modulo abilitato per i diritti

   Richiama il metodo `renderPDFFormWithUsageRights` dell&#39;oggetto `FormsServiceClient` e passa i seguenti valori:

   * Valore stringa che specifica il nome della struttura del modulo, inclusa l&#39;estensione del nome file. Se si fa riferimento a una struttura di modulo che fa parte di un&#39;applicazione Forms, assicurarsi di specificare il percorso completo, ad esempio `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Oggetto `com.adobe.idp.Document` contenente dati da unire al modulo. Se non si desidera unire i dati, passare un oggetto `com.adobe.idp.Document` vuoto.
   * Un oggetto `PDFFormRenderSpec` che memorizza le opzioni di runtime.
   * Oggetto `ReaderExtensionSpec` che memorizza le opzioni di runtime dei diritti di utilizzo.
   * Oggetto `URLSpec` contenente i valori URI richiesti dal servizio Forms.

   Il metodo `renderPDFFormWithUsageRights` restituisce un oggetto `FormsResult` che contiene un flusso di dati del modulo che deve essere scritto nel browser Web client.

1. Scrivere il flusso di dati del modulo nel browser Web client

   * Creare un oggetto `com.adobe.idp.Document` richiamando il metodo `getOutputContent` dell&#39;oggetto `FormsResult`.
   * Ottenere il tipo di contenuto dell&#39;oggetto `com.adobe.idp.Document` richiamando il relativo metodo `getContentType`.
   * Impostare il tipo di contenuto dell&#39;oggetto `javax.servlet.http.HttpServletResponse` richiamando il relativo metodo `setContentType` e passando il tipo di contenuto dell&#39;oggetto `com.adobe.idp.Document`.
   * Creare un oggetto `javax.servlet.ServletOutputStream` utilizzato per scrivere il flusso di dati del modulo nel browser Web client richiamando il metodo `getOutputStream` dell&#39;oggetto `javax.servlet.http.HttpServletResponse`.
   * Creare un oggetto `java.io.InputStream` richiamando il metodo `getInputStream` dell&#39;oggetto `com.adobe.idp.Document`.
   * Creare una matrice di byte popolarla con il flusso di dati del modulo richiamando il metodo `read` dell&#39;oggetto `InputStream` e passando la matrice di byte come argomento.
   * Richiama il metodo `write` dell&#39;oggetto `javax.servlet.ServletOutputStream` per inviare il flusso di dati del modulo al browser Web client. Passare la matrice di byte al metodo `write`.

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

   Creare un oggetto `FormsService` e impostare i valori di autenticazione.

1. Impostare le opzioni di runtime dei diritti di utilizzo

   * Creare un oggetto `ReaderExtensionSpec` utilizzando il relativo costruttore.
   * Specificare l&#39;alias delle credenziali richiamando il metodo `setReCredentialAlias` dell&#39;oggetto `ReaderExtensionSpec` e specificare un valore stringa che rappresenti il valore alias.
   * Impostare ogni diritto di utilizzo richiamando il metodo corrispondente che appartiene all&#39;oggetto `ReaderExtensionSpec`. È tuttavia possibile impostare un diritto di utilizzo solo se le credenziali a cui si fa riferimento lo consentono. In altre parole, non è possibile impostare un diritto di utilizzo se le credenziali non consentono di impostarlo. Per impostare il diritto di utilizzo che consente a un utente di compilare i campi del modulo e salvare il modulo, richiamare il metodo `setReFillIn` dell&#39;oggetto `ReaderExtensionSpec` e passare `true`.

1. Eseguire il rendering di un modulo abilitato per i diritti

   Richiama il metodo `renderPDFFormWithUsageRights` dell&#39;oggetto `FormsService` e passa i seguenti valori:

   * Valore stringa che specifica il nome della struttura del modulo, inclusa l&#39;estensione del nome file. Se si fa riferimento a una struttura di modulo che fa parte di un&#39;applicazione Forms, assicurarsi di specificare il percorso completo, ad esempio `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Oggetto `BLOB` contenente dati da unire al modulo. Se non si desidera unire i dati con il modulo, è necessario passare un oggetto `BLOB` basato su un&#39;origine dati XML vuota. Impossibile passare un oggetto `BLOB` null. In caso contrario, viene generata un&#39;eccezione.
   * Un oggetto `PDFFormRenderSpec` che memorizza le opzioni di runtime.
   * Oggetto `ReaderExtensionSpec` che memorizza le opzioni di runtime dei diritti di utilizzo.
   * Oggetto `URLSpec` contenente i valori URI richiesti dal servizio Forms.

   Il metodo `renderPDFFormWithUsageRights` restituisce un oggetto `FormsResult` che contiene un flusso di dati del modulo che deve essere scritto nel browser Web client.

1. Scrivere il flusso di dati del modulo nel browser Web client

   * Creare un oggetto `BLOB` contenente dati del modulo richiamando il metodo `getOutputContent` dell&#39;oggetto `FormsResult`.
   * Ottenere il tipo di contenuto dell&#39;oggetto `BLOB` richiamando il relativo metodo `getContentType`.
   * Impostare il tipo di contenuto dell&#39;oggetto `javax.servlet.http.HttpServletResponse` richiamando il relativo metodo `setContentType` e passando il tipo di contenuto dell&#39;oggetto `BLOB`.
   * Creare un oggetto `javax.servlet.ServletOutputStream` utilizzato per scrivere il flusso di dati del modulo nel browser Web client richiamando il metodo `getOutputStream` dell&#39;oggetto `javax.servlet.http.HttpServletResponse`.
   * Creare una matrice di byte e popolarla richiamando il metodo `getBinaryData` dell&#39;oggetto `BLOB`. Questa attività assegna il contenuto dell&#39;oggetto `FormsResult` alla matrice di byte.
   * Richiama il metodo `write` dell&#39;oggetto `javax.servlet.http.HttpServletResponse` per inviare il flusso di dati del modulo al browser Web client. Passare la matrice di byte al metodo `write`.

**Consulta anche**

[Forms con diritti di rendering](#rendering-rights-enabled-forms)

[Richiamare AEM Forms utilizzando la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
