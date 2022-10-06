---
title: Forms con diritti di rendering
seo-title: Rendering Rights-Enabled Forms
description: Utilizza il servizio Forms per eseguire il rendering dei moduli a cui sono applicati diritti di utilizzo. È possibile eseguire il rendering dei moduli abilitati per i diritti utilizzando l’API Java e l’API Web Service.
seo-description: Use the Forms service to render forms that have usage rights applied to them. You can render rights-enabled forms using the Java API and Web Service API.
uuid: ce5e4be6-d9b0-4989-a0e1-a8c3b98aed77
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: d4c2b2f0-613a-409d-b39b-8e37fdb96eea
role: Developer
exl-id: 012a3a9f-542c-4ed1-a092-572bfccbdf21
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1463'
ht-degree: 0%

---

# Forms con diritti di rendering {#rendering-rights-enabled-forms}

Il servizio Forms può eseguire il rendering dei moduli a cui sono stati applicati diritti di utilizzo. I diritti di utilizzo si riferiscono a funzionalità disponibili per impostazione predefinita in Acrobat ma non in Adobe Reader, ad esempio la possibilità di aggiungere commenti a un modulo o di compilare campi modulo e salvare il modulo. I moduli abilitati per i diritti di utilizzo applicati a Forms sono denominati moduli abilitati per i diritti. L’utente che apre un modulo abilitato per i diritti in Adobe Reader può eseguire le operazioni abilitate per tale modulo.

Per applicare i diritti di utilizzo a un modulo, il servizio Acrobat Reader DC extensions deve far parte dell’installazione dei moduli di AEM. Inoltre, è necessario disporre di una credenziale valida che consenta di applicare diritti di utilizzo ai documenti PDF. In altre parole, è necessario configurare correttamente il servizio Acrobat Reader DC extensions prima di poter eseguire il rendering di un modulo abilitato per i diritti. (Vedi [Informazioni sul servizio Acrobat Reader DC extensions](/help/forms/developing/assigning-usage-rights.md#about-the-acrobat-reader-dc-extensions-service).)

>[!NOTE]
>
>Per eseguire il rendering di un modulo contenente diritti di utilizzo, è necessario utilizzare un file XDP come input, non come file PDF. Se si utilizza un file PDF come input, viene comunque eseguito il rendering del modulo; tuttavia, non sarà un modulo abilitato per i diritti.

>[!NOTE]
>
>Non è possibile precompilare un modulo con dati XML quando si specificano i seguenti diritti di utilizzo: `enableComments`, `enableCommentsOnline`, `enableEmbeddedFiles`oppure `enableDigitalSignatures`. (Vedi [Precompilazione di Forms con layout fluidi](/help/forms/developing/prepopulating-forms-flowable-layouts.md).)

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Forms, vedi [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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

### Eseguire il rendering dei moduli abilitati per i diritti tramite l’API Java {#render-rights-enabled-forms-using-the-java-api}

Eseguire il rendering di un modulo abilitato per i diritti utilizzando l’API Forms (Java):

1. Includi file di progetto

   Includi file JAR client, come adobe-forms-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto API client Forms

   * Crea un `ServiceClientFactory` oggetto contenente le proprietà di connessione.
   * Crea un `FormsServiceClient` utilizzando il relativo costruttore e passando `ServiceClientFactory` oggetto.

1. Impostare le opzioni di esecuzione dei diritti di utilizzo

   * Crea un `ReaderExtensionSpec` utilizzando il relativo costruttore.
   * Specifica l&#39;alias della credenziale richiamando il `ReaderExtensionSpec` dell’oggetto `setReCredentialAlias` e specificare un valore stringa che rappresenta il valore alias.
   * Imposta ogni diritto di utilizzo richiamando il metodo corrispondente che appartiene al `ReaderExtensionSpec` oggetto. Tuttavia, è possibile impostare un diritto di utilizzo solo se la credenziale a cui si fa riferimento consente di farlo. In altre parole, non è possibile impostare un diritto di utilizzo se la credenziale non consente di impostarlo. Esempio. per impostare il diritto d’uso che consente all’utente di compilare i campi del modulo e salvarlo, richiama il `ReaderExtensionSpec` dell’oggetto `setReFillIn` metodo e passaggio `true`.

   >[!NOTE]
   >
   >Non è necessario invocare il `ReaderExtensionSpec` dell’oggetto `setReCredentialPassword` metodo . Questo metodo non viene utilizzato dal servizio Forms.

1. Rendering di un modulo abilitato per i diritti

   Richiama il `FormsServiceClient` dell’oggetto `renderPDFFormWithUsageRights` e passare i seguenti valori:

   * Valore stringa che specifica il nome della struttura del modulo, inclusa l&#39;estensione del nome file. Se si fa riferimento a una struttura del modulo che fa parte di un&#39;applicazione Forms, verificare di specificare il percorso completo, ad esempio `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `com.adobe.idp.Document` oggetto contenente i dati da unire al modulo. Se non si desidera unire i dati, passare un valore vuoto `com.adobe.idp.Document` oggetto.
   * A `PDFFormRenderSpec` oggetto che memorizza le opzioni di esecuzione.
   * A `ReaderExtensionSpec` oggetto che memorizza le opzioni di esecuzione dei diritti di utilizzo.
   * A `URLSpec` oggetto che contiene i valori URI richiesti dal servizio Forms.

   La `renderPDFFormWithUsageRights` restituisce un `FormsResult` oggetto che contiene un flusso di dati del modulo che deve essere scritto nel browser Web client.

1. Scrivere il flusso di dati del modulo sul browser Web client

   * Crea un `com.adobe.idp.Document` richiamando l&#39;oggetto `FormsResult` oggetto ‘s `getOutputContent` metodo .
   * Ottieni il tipo di contenuto del `com.adobe.idp.Document` richiamandone l&#39;oggetto `getContentType` metodo .
   * Imposta la `javax.servlet.http.HttpServletResponse` tipo di contenuto dell’oggetto richiamandone il tipo `setContentType` e passare il tipo di contenuto `com.adobe.idp.Document` oggetto.
   * Crea un `javax.servlet.ServletOutputStream` oggetto utilizzato per scrivere il flusso di dati del modulo nel browser Web client richiamando il `javax.servlet.http.HttpServletResponse` dell’oggetto `getOutputStream` metodo .
   * Crea un `java.io.InputStream` richiamando l&#39;oggetto `com.adobe.idp.Document` dell’oggetto `getInputStream` metodo .
   * Creare un array di byte popolarlo con il flusso di dati del modulo richiamando il `InputStream` dell’oggetto `read` e passare l&#39;array di byte come argomento.
   * Richiama il `javax.servlet.ServletOutputStream` dell’oggetto `write` per inviare il flusso di dati del modulo al browser Web client. Passa l&#39;array di byte al `write` metodo .

**Consulta anche**

[Avvio rapido (modalità SOAP): Rendering di un modulo abilitato per i diritti utilizzando l’API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-rights-enabled-form-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Rendering di moduli abilitati per i diritti tramite l’API del servizio Web {#render-rights-enabled-forms-using-the-web-service-api}

Eseguire il rendering di un modulo abilitato per i diritti utilizzando l’API Forms (servizio Web):

1. Includi file di progetto

   * Creare classi proxy Java che utilizzano il servizio WSDL di Forms.
   * Includi le classi proxy Java nel percorso della classe.

1. Creare un oggetto API client Forms

   Crea un `FormsService` e impostare i valori di autenticazione.

1. Impostare le opzioni di esecuzione dei diritti di utilizzo

   * Crea un `ReaderExtensionSpec` utilizzando il relativo costruttore.
   * Specifica l&#39;alias della credenziale richiamando il `ReaderExtensionSpec` dell’oggetto `setReCredentialAlias` e specificare un valore stringa che rappresenta il valore alias.
   * Imposta ogni diritto di utilizzo richiamando il metodo corrispondente che appartiene al `ReaderExtensionSpec` oggetto. Tuttavia, è possibile impostare un diritto di utilizzo solo se la credenziale a cui si fa riferimento consente di farlo. In altre parole, non è possibile impostare un diritto di utilizzo se la credenziale non consente di impostarlo. Per impostare il diritto d’uso che consente all’utente di compilare i campi del modulo e salvarlo, richiamare l’ `ReaderExtensionSpec` dell’oggetto `setReFillIn` metodo e passaggio `true`.

1. Rendering di un modulo abilitato per i diritti

   Richiama il `FormsService` dell’oggetto `renderPDFFormWithUsageRights` e passare i seguenti valori:

   * Valore stringa che specifica il nome della struttura del modulo, inclusa l&#39;estensione del nome file. Se si fa riferimento a una struttura del modulo che fa parte di un&#39;applicazione Forms, verificare di specificare il percorso completo, ad esempio `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `BLOB` oggetto contenente i dati da unire al modulo. Se non si desidera unire i dati al modulo, è necessario passare un `BLOB` oggetto basato su un&#39;origine dati XML vuota. Non è possibile passare un `BLOB` oggetto nullo; in caso contrario, viene generata un&#39;eccezione.
   * A `PDFFormRenderSpec` oggetto che memorizza le opzioni di esecuzione.
   * A `ReaderExtensionSpec` oggetto che memorizza le opzioni di esecuzione dei diritti di utilizzo.
   * A `URLSpec` oggetto che contiene i valori URI richiesti dal servizio Forms.

   La `renderPDFFormWithUsageRights` restituisce un `FormsResult` oggetto che contiene un flusso di dati del modulo che deve essere scritto nel browser Web client.

1. Scrivere il flusso di dati del modulo sul browser Web client

   * Crea un `BLOB` oggetto che contiene i dati del modulo richiamando il `FormsResult` dell’oggetto `getOutputContent` metodo .
   * Ottieni il tipo di contenuto del `BLOB` richiamandone l&#39;oggetto `getContentType` metodo .
   * Imposta la `javax.servlet.http.HttpServletResponse` tipo di contenuto dell’oggetto richiamandone il tipo `setContentType` e passare il tipo di contenuto `BLOB` oggetto.
   * Crea un `javax.servlet.ServletOutputStream` oggetto utilizzato per scrivere il flusso di dati del modulo nel browser Web client richiamando il `javax.servlet.http.HttpServletResponse` dell’oggetto `getOutputStream` metodo .
   * Creare un array di byte e compilarlo richiamando il `BLOB` dell’oggetto `getBinaryData` metodo . Questa attività assegna il contenuto del `FormsResult` all&#39;array di byte.
   * Richiama il `javax.servlet.http.HttpServletResponse` dell’oggetto `write` per inviare il flusso di dati del modulo al browser Web client. Passa l&#39;array di byte al `write` metodo .

**Consulta anche**

[Forms con diritti di rendering](#rendering-rights-enabled-forms)

[Richiamo di AEM Forms con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
