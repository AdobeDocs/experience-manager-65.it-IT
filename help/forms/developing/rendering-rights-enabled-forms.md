---
title: Forms con diritti di rendering
seo-title: Forms con diritti di rendering
description: Utilizza il servizio Forms per eseguire il rendering dei moduli a cui sono applicati diritti di utilizzo. È possibile eseguire il rendering dei moduli abilitati per i diritti utilizzando l’API Java e l’API Web Service.
seo-description: Utilizza il servizio Forms per eseguire il rendering dei moduli a cui sono applicati diritti di utilizzo. È possibile eseguire il rendering dei moduli abilitati per i diritti utilizzando l’API Java e l’API Web Service.
uuid: ce5e4be6-d9b0-4989-a0e1-a8c3b98aed77
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: d4c2b2f0-613a-409d-b39b-8e37fdb96eea
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1494'
ht-degree: 0%

---


# Rendering di Forms abilitato per diritti {#rendering-rights-enabled-forms}

Il servizio Forms può eseguire il rendering dei moduli a cui sono stati applicati diritti di utilizzo. I diritti di utilizzo si riferiscono a funzionalità disponibili per impostazione predefinita in Acrobat ma non in Adobe Reader, ad esempio la possibilità di aggiungere commenti a un modulo o di compilare campi modulo e salvare il modulo. I moduli abilitati per i diritti di utilizzo applicati a Forms sono denominati moduli abilitati per i diritti. L’utente che apre un modulo abilitato per i diritti in Adobe Reader può eseguire le operazioni abilitate per tale modulo.

Per applicare i diritti di utilizzo a un modulo, il servizio Acrobat Reader DC extensions deve far parte dell’installazione dei moduli di AEM. Inoltre, è necessario disporre di una credenziale valida che consenta di applicare diritti di utilizzo ai documenti PDF. In altre parole, è necessario configurare correttamente il servizio Acrobat Reader DC extensions prima di poter eseguire il rendering di un modulo abilitato per i diritti. (Consulta [Informazioni sul servizio Acrobat Reader DC extensions](/help/forms/developing/assigning-usage-rights.md#about-the-acrobat-reader-dc-extensions-service).)

>[!NOTE]
>
>Per eseguire il rendering di un modulo contenente diritti di utilizzo, è necessario utilizzare un file XDP come input, non come file PDF. Se si utilizza un file PDF come input, viene comunque eseguito il rendering del modulo; tuttavia, non sarà un modulo abilitato per i diritti.

>[!NOTE]
>
>Non è possibile precompilare un modulo con dati XML quando si specificano i seguenti diritti di utilizzo: `enableComments`, `enableCommentsOnline`, `enableEmbeddedFiles` o `enableDigitalSignatures`. (Consultare [Precompilazione di Forms con layout fluidi](/help/forms/developing/prepopulating-forms-flowable-layouts.md).)

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Forms, consulta [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Riepilogo dei passaggi {#summary-of-steps}

Per eseguire il rendering di un modulo abilitato per i diritti, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Creare un oggetto API client Forms.
1. Impostare le opzioni di esecuzione dei diritti di utilizzo.
1. Eseguire il rendering di un modulo abilitato per i diritti.
1. Scrivi il modulo abilitato per i diritti nel browser Web del client.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

**Creare un oggetto API client Forms**

Prima di poter eseguire programmaticamente un’operazione API client del servizio Forms, è necessario creare un client di servizio Forms.

**Impostare le opzioni di esecuzione dei diritti di utilizzo**

Per eseguire il rendering di un modulo abilitato per i diritti di utilizzo, è necessario impostare le opzioni di esecuzione dei diritti di utilizzo. È inoltre necessario specificare l’alias della credenziale utilizzata per applicare i diritti di utilizzo a un modulo. Dopo aver specificato il valore di alias, è necessario specificare ogni diritto di utilizzo da applicare al modulo.

**Rendering di un modulo abilitato per i diritti**

Per eseguire il rendering di un modulo abilitato per i diritti, è necessario utilizzare la stessa logica applicativa del rendering di un modulo senza diritti di utilizzo. L’unica differenza consiste nel garantire che le opzioni di runtime dei diritti di utilizzo siano incluse nella logica dell’applicazione.

>[!NOTE]
>
>Quando si esegue il rendering di un modulo abilitato per i diritti utilizzando l’API del servizio Web Forms, non è possibile allegare file al modulo.

**Scrivere il flusso di dati del modulo sul browser Web client**

Quando il servizio Forms esegue il rendering di un modulo abilitato per i diritti, restituisce un flusso di dati del modulo che è necessario scrivere nel browser Web client. Una volta scritto nel browser Web client, il modulo è visibile all’utente. Un utente che visualizza il modulo abilitato per i diritti in Adobe Reader è in grado di eseguire le operazioni abilitate per quel modulo.

**Consulta anche**

[Eseguire il rendering dei moduli abilitati per i diritti tramite l’API Java](#render-rights-enabled-forms-using-the-java-api)

[Rendering di moduli abilitati per i diritti tramite l’API del servizio Web](#render-rights-enabled-forms-using-the-web-service-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API di Forms Service](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Rendering di PDF forms interattivi](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Creazione di applicazioni Web per il rendering di Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

### Eseguire il rendering dei moduli abilitati per i diritti utilizzando l’API Java {#render-rights-enabled-forms-using-the-java-api}

Eseguire il rendering di un modulo abilitato per i diritti utilizzando l’API Forms (Java):

1. Includi file di progetto

   Includi file JAR client, come adobe-forms-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto API client Forms

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `FormsServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Impostare le opzioni di esecuzione dei diritti di utilizzo

   * Creare un oggetto `ReaderExtensionSpec` utilizzando il relativo costruttore.
   * Specificare l&#39;alias della credenziale richiamando il metodo `setReCredentialAlias` dell&#39;oggetto `ReaderExtensionSpec` e specificare un valore stringa che rappresenta il valore dell&#39;alias.
   * Impostare ogni diritto di utilizzo richiamando il metodo corrispondente che appartiene all&#39;oggetto `ReaderExtensionSpec`. Tuttavia, è possibile impostare un diritto di utilizzo solo se la credenziale a cui si fa riferimento consente di farlo. In altre parole, non è possibile impostare un diritto di utilizzo se la credenziale non consente di impostarlo. Esempio. per impostare il diritto di utilizzo che consente all’utente di compilare i campi del modulo e salvarlo, richiamare il metodo `setReFillIn` dell’oggetto `ReaderExtensionSpec` e passare `true`.

   >[!NOTE]
   >
   >Non è necessario richiamare il metodo `ReaderExtensionSpec` dell&#39;oggetto `setReCredentialPassword`. Questo metodo non viene utilizzato dal servizio Forms.

1. Rendering di un modulo abilitato per i diritti

   Richiama il metodo `renderPDFFormWithUsageRights` dell&#39;oggetto `FormsServiceClient` e passa i seguenti valori:

   * Valore stringa che specifica il nome della struttura del modulo, inclusa l&#39;estensione del nome file. Se si fa riferimento a una struttura del modulo che fa parte di un&#39;applicazione Forms, assicurarsi di specificare il percorso completo, ad esempio `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Un oggetto `com.adobe.idp.Document` contenente i dati da unire al modulo. Se non si desidera unire i dati, passare un oggetto `com.adobe.idp.Document` vuoto.
   * Un oggetto `PDFFormRenderSpec` che memorizza le opzioni di esecuzione.
   * Un oggetto `ReaderExtensionSpec` che memorizza le opzioni di runtime dei diritti di utilizzo.
   * Un oggetto `URLSpec` contenente valori URI richiesti dal servizio Forms.

   Il metodo `renderPDFFormWithUsageRights` restituisce un oggetto `FormsResult` contenente un flusso di dati del modulo che deve essere scritto nel browser Web client.

1. Scrivere il flusso di dati del modulo sul browser Web client

   * Creare un oggetto `com.adobe.idp.Document` richiamando il metodo `FormsResult` object ‘s `getOutputContent` .
   * Ottenere il tipo di contenuto dell&#39;oggetto `com.adobe.idp.Document` richiamandone il metodo `getContentType`.
   * Impostare il tipo di contenuto dell&#39;oggetto `javax.servlet.http.HttpServletResponse` richiamandone il metodo `setContentType` e passando il tipo di contenuto dell&#39;oggetto `com.adobe.idp.Document`.
   * Creare un oggetto `javax.servlet.ServletOutputStream` utilizzato per scrivere il flusso di dati del modulo nel browser Web client richiamando il metodo `javax.servlet.http.HttpServletResponse` dell&#39;oggetto `getOutputStream`.
   * Creare un oggetto `java.io.InputStream` richiamando il metodo `com.adobe.idp.Document` dell&#39;oggetto `getInputStream`.
   * Creare un array di byte popolarlo con il flusso di dati del modulo richiamando il metodo `read` dell&#39;oggetto `InputStream` e passando l&#39;array di byte come argomento.
   * Richiamare il metodo `write` dell’oggetto `javax.servlet.ServletOutputStream` per inviare il flusso di dati del modulo al browser Web client. Passa l&#39;array di byte al metodo `write` .

**Consulta anche**

[Avvio rapido (modalità SOAP): Rendering di un modulo abilitato per i diritti utilizzando l’API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-rights-enabled-form-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Eseguire il rendering dei moduli abilitati per i diritti utilizzando l’API del servizio Web {#render-rights-enabled-forms-using-the-web-service-api}

Eseguire il rendering di un modulo abilitato per i diritti utilizzando l’API Forms (servizio Web):

1. Includi file di progetto

   * Creare classi proxy Java che utilizzano il servizio WSDL di Forms.
   * Includi le classi proxy Java nel percorso della classe.

1. Creare un oggetto API client Forms

   Creare un oggetto `FormsService` e impostare i valori di autenticazione.

1. Impostare le opzioni di esecuzione dei diritti di utilizzo

   * Creare un oggetto `ReaderExtensionSpec` utilizzando il relativo costruttore.
   * Specificare l&#39;alias della credenziale richiamando il metodo `setReCredentialAlias` dell&#39;oggetto `ReaderExtensionSpec` e specificare un valore stringa che rappresenta il valore dell&#39;alias.
   * Impostare ogni diritto di utilizzo richiamando il metodo corrispondente che appartiene all&#39;oggetto `ReaderExtensionSpec`. Tuttavia, è possibile impostare un diritto di utilizzo solo se la credenziale a cui si fa riferimento consente di farlo. In altre parole, non è possibile impostare un diritto di utilizzo se la credenziale non consente di impostarlo. Per impostare il diritto di utilizzo che consente all’utente di compilare i campi del modulo e salvarlo, richiamare il metodo `setReFillIn` dell’oggetto `ReaderExtensionSpec` e passare `true`.

1. Rendering di un modulo abilitato per i diritti

   Richiama il metodo `renderPDFFormWithUsageRights` dell&#39;oggetto `FormsService` e passa i seguenti valori:

   * Valore stringa che specifica il nome della struttura del modulo, inclusa l&#39;estensione del nome file. Se si fa riferimento a una struttura del modulo che fa parte di un&#39;applicazione Forms, assicurarsi di specificare il percorso completo, ad esempio `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Un oggetto `BLOB` contenente i dati da unire al modulo. Se non si desidera unire i dati al modulo, è necessario passare un oggetto `BLOB` basato su un&#39;origine dati XML vuota. Non è possibile passare un oggetto `BLOB` nullo; in caso contrario, viene generata un&#39;eccezione.
   * Un oggetto `PDFFormRenderSpec` che memorizza le opzioni di esecuzione.
   * Un oggetto `ReaderExtensionSpec` che memorizza le opzioni di runtime dei diritti di utilizzo.
   * Un oggetto `URLSpec` contenente valori URI richiesti dal servizio Forms.

   Il metodo `renderPDFFormWithUsageRights` restituisce un oggetto `FormsResult` contenente un flusso di dati del modulo che deve essere scritto nel browser Web client.

1. Scrivere il flusso di dati del modulo sul browser Web client

   * Creare un oggetto `BLOB` che contiene dati del modulo richiamando il metodo `FormsResult` dell&#39;oggetto `getOutputContent`.
   * Ottenere il tipo di contenuto dell&#39;oggetto `BLOB` richiamandone il metodo `getContentType`.
   * Impostare il tipo di contenuto dell&#39;oggetto `javax.servlet.http.HttpServletResponse` richiamandone il metodo `setContentType` e passando il tipo di contenuto dell&#39;oggetto `BLOB`.
   * Creare un oggetto `javax.servlet.ServletOutputStream` utilizzato per scrivere il flusso di dati del modulo nel browser Web client richiamando il metodo `javax.servlet.http.HttpServletResponse` dell&#39;oggetto `getOutputStream`.
   * Creare una matrice di byte e compilarla richiamando il metodo `getBinaryData` dell&#39;oggetto `BLOB`. Questa attività assegna il contenuto dell&#39;oggetto `FormsResult` all&#39;array di byte.
   * Richiamare il metodo `write` dell’oggetto `javax.servlet.http.HttpServletResponse` per inviare il flusso di dati del modulo al browser Web client. Passa l&#39;array di byte al metodo `write` .

**Consulta anche**

[Forms con diritti di rendering](#rendering-rights-enabled-forms)

[Richiamo di AEM Forms con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
