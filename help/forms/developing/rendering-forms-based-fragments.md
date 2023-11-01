---
title: Rendering di Forms basato su frammenti
seo-title: Rendering Forms Based on Fragments
description: Utilizzare il servizio Forms per eseguire il rendering di moduli basati su frammenti creati mediante Designer.
seo-description: Use the Forms service to render forms that are based on fragments created using Designer.
uuid: 9c9a730d-f970-41f8-afed-4e6b6d3d393d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: a65c5303-0ebd-43a9-a777-401042d8fcad
role: Developer
exl-id: febf5350-3fc5-48c0-8bc5-198daff15936
source-git-commit: 1807919078996b1cf1cbd1f2d90c3b14cb660e2c
workflow-type: tm+mt
source-wordcount: '2205'
ht-degree: 0%

---

# Rendering di Forms basato su frammenti {#rendering-forms-based-on-fragments}

**Gli esempi e gli esempi contenuti in questo documento sono solo per l’ambiente AEM Forms su JEE.**

## Rendering di Forms basato su frammenti {#rendering-forms-based-on-fragments-inner}

Il servizio Forms può eseguire il rendering di moduli basati su frammenti creati mediante Designer. A *frammento* è una parte riutilizzabile di un modulo e viene salvato come file XDP separato che può essere inserito in più progettazioni di moduli. Ad esempio, un frammento può includere un blocco di indirizzi o un testo legale.

L’utilizzo di frammenti semplifica e velocizza la creazione e la manutenzione di un gran numero di moduli. Durante la creazione di un nuovo modulo, viene inserito un riferimento al frammento richiesto e il frammento viene visualizzato nel modulo. Il riferimento al frammento contiene un sottomodulo che punta al file XDP fisico. Per informazioni sulla creazione di strutture di moduli basate su frammenti, vedere [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63_it)

Un frammento può includere diverse sottomaschere racchiuse in un set di sottomaschere di scelta. I set di sottomaschere di scelta controllano la visualizzazione delle sottomaschere in base al flusso di dati provenienti da una connessione dati. È possibile utilizzare le istruzioni condizionali per determinare quale sottomaschera all&#39;interno della serie viene visualizzata nella maschera consegnata. Ad esempio, ogni sottomaschera di un set può includere informazioni relative a una particolare posizione geografica e la sottomaschera visualizzata può essere determinata in base alla posizione dell&#39;utente.

A *frammento di script* contiene funzioni o valori JavaScript riutilizzabili memorizzati separatamente da qualsiasi oggetto particolare, ad esempio un parser di date o una chiamata a un servizio web. Questi frammenti includono un singolo oggetto script che viene visualizzato come elemento figlio di variabili nella tavolozza Gerarchia. I frammenti non possono essere creati da script che sono proprietà di altri oggetti, ad esempio script di eventi come validate, calculate o initialize.

Di seguito sono riportati i vantaggi dell’utilizzo dei frammenti:

* **Riutilizzo dei contenuti**: è possibile utilizzare i frammenti per riutilizzare il contenuto in più progettazioni di moduli. Quando è necessario utilizzare parte dello stesso contenuto in più moduli, l’utilizzo di un frammento è più rapido e semplice rispetto alla copia o alla ricreazione del contenuto. L’utilizzo dei frammenti assicura inoltre che le parti utilizzate di frequente di una progettazione di moduli abbiano contenuto e aspetto coerenti in tutti i moduli di riferimento.
* **Aggiornamenti globali**: è possibile utilizzare i frammenti per apportare modifiche globali a più moduli una sola volta, in un unico file. È possibile modificare il contenuto, gli oggetti script, le associazioni di dati, il layout o gli stili di un frammento. Le modifiche verranno applicate a tutti i moduli XDP che fanno riferimento al frammento.
* Ad esempio, un elemento comune in molti moduli potrebbe essere un blocco di indirizzi che include un oggetto elenco a discesa per il paese. Se è necessario aggiornare i valori dell&#39;oggetto elenco a discesa, è necessario aprire più maschere per apportare le modifiche. Se includi il blocco di indirizzi in un frammento, per apportare le modifiche dovrai aprire un solo file di frammento.
* Per aggiornare un frammento in un modulo PDF, è necessario salvare nuovamente il modulo in Designer.
* **Creazione di moduli condivisi**: puoi utilizzare i frammenti per condividere la creazione di moduli tra diverse risorse. Gli sviluppatori di moduli con esperienza nello scripting o altre funzioni avanzate di Designer possono sviluppare e condividere frammenti che sfruttano le proprietà di script e dinamiche. I progettisti di moduli possono utilizzare tali frammenti per disporre le progettazioni dei moduli e per garantire che tutte le parti di un modulo abbiano un aspetto e una funzionalità coerenti in più moduli progettati da più persone.

### Assemblaggio di una struttura di modulo assemblata mediante frammenti {#assembling-a-form-design-assembled-using-fragments}

È possibile assemblare una struttura di modulo da passare al servizio Forms in base a più frammenti. Per assemblare più frammenti, utilizzare il servizio Assembler. Per visualizzare un esempio di utilizzo del servizio Assemble per la creazione di una struttura di modulo utilizzata da altri servizi Forms (il servizio di output), vedere [Creazione di documenti PDF tramite frammenti](/help/forms/developing/creating-document-output-streams.md#creating-pdf-documents-using-fragments). Invece di utilizzare il servizio di output, puoi eseguire lo stesso flusso di lavoro utilizzando il servizio Forms.

Quando si utilizza il servizio Assembler, si passa una progettazione di modulo che è stata assemblata utilizzando frammenti. La struttura del modulo creata non fa riferimento ad altri frammenti. In questo argomento viene invece illustrato come passare al servizio Forms una struttura di modulo che fa riferimento ad altri frammenti. Tuttavia, la progettazione del modulo non è stata assemblata da Assembler. È stato creato in Designer.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Forms, consulta [Guida di riferimento dei servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Per informazioni sulla creazione di un&#39;applicazione basata sul Web per il rendering di moduli basati su frammenti, vedere [Creazione di applicazioni Web per il rendering di Forms](/help/forms/developing/creating-web-applications-renders-forms.md).

### Riepilogo dei passaggi {#summary-of-steps}

Per eseguire il rendering di un modulo basato su frammenti, effettuare le seguenti operazioni:

1. Includi file di progetto.
1. Crea un oggetto API client di Forms.
1. Specifica i valori URI.
1. Eseguire il rendering del modulo.
1. Scrivere il flusso di dati del modulo nel browser Web client.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

**Creare un oggetto API client di Forms**

Prima di poter eseguire a livello di programmazione un&#39;operazione API client del servizio Forms, è necessario creare un client del servizio Forms.

**Specificare i valori URI**

Per eseguire correttamente il rendering di un modulo basato su frammenti, è necessario assicurarsi che il servizio Forms sia in grado di individuare sia il modulo che i frammenti (i file XDP) a cui fa riferimento il progetto del modulo. Si supponga ad esempio che il modulo sia denominato PO.xdp e che utilizzi due frammenti denominati FooterUS.xdp e FooterCanada.xdp. In questa situazione, il servizio Forms deve essere in grado di individuare tutti e tre i file XDP.

È possibile organizzare un modulo e i relativi frammenti posizionando il modulo in una posizione e i frammenti in un&#39;altra, oppure è possibile posizionare tutti i file XDP nella stessa posizione. Ai fini di questa sezione, supponiamo che tutti i file XDP si trovino nell’archivio AEM Forms. Per informazioni sul posizionamento dei file XDP nell’archivio AEM Forms, consulta [Scrittura delle risorse](/help/forms/developing/aem-forms-repository.md#writing-resources).

Quando si esegue il rendering di un modulo basato su frammenti, è necessario fare riferimento solo al modulo stesso e non ai frammenti. Ad esempio, è necessario fare riferimento a PO.xdp e non a FooterUS.xdp o FooterCanada.xdp. Assicurati di posizionare i frammenti in una posizione in cui il servizio Forms possa individuarli.

**Rendering del modulo**

Un modulo basato su frammenti può essere renderizzato nello stesso modo dei moduli non frammentati. In altre parole, è possibile eseguire il rendering del modulo come PDF, HTML o Guide del modulo (obsoleto). Nell&#39;esempio di questa sezione viene eseguito il rendering di un modulo basato su frammenti come modulo PDF interattivo. (vedere [Rendering dei PDF forms interattivi](/help/forms/developing/rendering-interactive-pdf-forms.md).)

**Scrivere il flusso di dati del modulo nel browser Web client**

Quando il servizio Forms esegue il rendering di un modulo, restituisce un flusso di dati del modulo che è necessario scrivere nel browser Web client. Quando viene scritto nel browser Web client, il modulo è visibile all&#39;utente.

**Consulta anche**

[Eseguire il rendering di moduli basati su frammenti utilizzando l’API Java](#render-forms-based-on-fragments-using-the-java-api)

[Eseguire il rendering di moduli basati su frammenti utilizzando l’API del servizio web](#render-forms-based-on-fragments-using-the-web-service-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Guida introduttiva all’API di servizio Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Rendering dei PDF forms interattivi](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Creazione di applicazioni Web per il rendering di Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

### Eseguire il rendering di moduli basati su frammenti utilizzando l’API Java {#render-forms-based-on-fragments-using-the-java-api}

Eseguire il rendering di un modulo basato su frammenti utilizzando l’API Forms (Java):

1. Includi file di progetto

   Includi i file JAR client, ad esempio adobe-forms-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto API client di Forms

   * Creare un `ServiceClientFactory` oggetto che contiene proprietà di connessione.
   * Creare un `FormsServiceClient` mediante il costruttore e passando il `ServiceClientFactory` oggetto.

1. Specificare i valori URI

   * Creare un `URLSpec` oggetto che memorizza i valori URI utilizzando il relativo costruttore.
   * Richiama `URLSpec` dell&#39;oggetto `setApplicationWebRoot` e passa un valore stringa che rappresenta la directory principale del web dell’applicazione.
   * Richiama `URLSpec` dell&#39;oggetto `setContentRootURI` e passa un valore stringa che specifica il valore URI della directory principale del contenuto. Assicurati che la progettazione del modulo e i frammenti si trovino nell’URI della directory principale del contenuto. In caso contrario, il servizio Forms genera un&#39;eccezione. Per fare riferimento all’archivio, specifica `repository://`.
   * Richiama `URLSpec` dell&#39;oggetto `setTargetURL` e passa un valore stringa che specifica il valore dell&#39;URL di destinazione in cui vengono pubblicati i dati del modulo. Se definisci l’URL di destinazione nella progettazione del modulo, puoi trasmettere una stringa vuota. È inoltre possibile specificare l&#39;URL a cui viene inviato un modulo per eseguire i calcoli.

1. Rendering del modulo

   Richiama `FormsServiceClient` dell&#39;oggetto `renderPDFForm` e trasmettere i seguenti valori:

   * Valore stringa che specifica il nome della struttura del modulo, inclusa l&#39;estensione del nome file. Se si fa riferimento a una struttura di modulo che fa parte di un&#39;applicazione Forms, assicurarsi di specificare il percorso completo, ad esempio `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `com.adobe.idp.Document` oggetto contenente dati da unire con il modulo. Se non desideri unire i dati, passa un campo vuoto `com.adobe.idp.Document` oggetto.
   * A `PDFFormRenderSpec` oggetto che memorizza le opzioni di runtime.
   * A `URLSpec` oggetto contenente valori URI richiesti dal servizio Forms per eseguire il rendering di un modulo basato su frammenti.
   * A `java.util.HashMap` oggetto che memorizza gli allegati. Questo è un parametro facoltativo e puoi specificare `null` se non si desidera allegare file al modulo.

   Il `renderPDFForm` il metodo restituisce un `FormsResult` oggetto contenente un flusso di dati modulo che deve essere scritto nel browser web client.

1. Scrivere il flusso di dati del modulo nel browser Web client

   * Creare un `com.adobe.idp.Document` oggetto richiamando il `FormsResult` oggetto &quot;s `getOutputContent` metodo.
   * Ottieni il tipo di contenuto del `com.adobe.idp.Document` oggetto richiamando il relativo `getContentType` metodo.
   * Imposta il `javax.servlet.http.HttpServletResponse` tipo di contenuto dell&#39;oggetto richiamando il relativo `setContentType` e passando il tipo di contenuto del `com.adobe.idp.Document` oggetto.
   * Creare un `javax.servlet.ServletOutputStream` oggetto utilizzato per scrivere il flusso di dati del modulo nel browser web client richiamando `javax.servlet.http.HttpServletResponse` dell&#39;oggetto `getOutputStream` metodo.
   * Creare un `java.io.InputStream` oggetto richiamando il `com.adobe.idp.Document` dell&#39;oggetto `getInputStream` metodo.
   * Creare una matrice di byte compilarla con il flusso di dati del modulo richiamando `InputStream` dell&#39;oggetto `read`e passando la matrice di byte come argomento.
   * Richiama `javax.servlet.ServletOutputStream` dell&#39;oggetto `write` metodo per inviare il flusso di dati del modulo al browser web client. Passare la matrice di byte al `write` metodo.

**Consulta anche**

[Rendering di Forms basato su frammenti](#rendering-forms-based-on-fragments)

[Quick Start (modalità SOAP): rendering di un modulo basato su frammenti tramite API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-form-based-on-fragments-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Eseguire il rendering di moduli basati su frammenti utilizzando l’API del servizio web {#render-forms-based-on-fragments-using-the-web-service-api}

Eseguire il rendering di un modulo basato su frammenti utilizzando l’API di Forms (servizio web):

1. Includi file di progetto

   * Creare classi proxy Java che utilizzano il servizio Forms WSDL.
   * Includi le classi proxy Java nel percorso della classe.

1. Creare un oggetto API client di Forms

   Creare un `FormsService` e impostare i valori di autenticazione.

1. Specificare i valori URI

   * Creare un `URLSpec` oggetto che memorizza i valori URI utilizzando il relativo costruttore.
   * Richiama `URLSpec` dell&#39;oggetto `setApplicationWebRoot` e passa un valore stringa che rappresenta la directory principale del web dell’applicazione.
   * Richiama `URLSpec` dell&#39;oggetto `setContentRootURI` e passa un valore stringa che specifica il valore URI della directory principale del contenuto. Assicurati che la progettazione del modulo si trovi nell’URI della directory principale del contenuto. In caso contrario, il servizio Forms genera un&#39;eccezione. Per fare riferimento all’archivio, specifica `repository://`.
   * Richiama `URLSpec` dell&#39;oggetto `setTargetURL` e passa un valore stringa che specifica il valore dell&#39;URL di destinazione in cui vengono pubblicati i dati del modulo. Se definisci l’URL di destinazione nella progettazione del modulo, puoi trasmettere una stringa vuota. È inoltre possibile specificare l&#39;URL a cui viene inviato un modulo per eseguire i calcoli.

1. Rendering del modulo

   Richiama `FormsService` dell&#39;oggetto `renderPDFForm` e trasmettere i seguenti valori:

   * Valore stringa che specifica il nome della struttura del modulo, inclusa l&#39;estensione del nome file. Se si fa riferimento a una struttura di modulo che fa parte di un&#39;applicazione Forms, assicurarsi di specificare il percorso completo, ad esempio `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `BLOB` oggetto contenente dati da unire con il modulo. Se non si desidera unire i dati, passare `null`.
   * A `PDFFormRenderSpec` oggetto che memorizza le opzioni di runtime. L&#39;opzione PDF con tag non può essere impostata se il documento di input è un documento PDF. Se il file di input è un file XDP, è possibile impostare l&#39;opzione PDF con tag.
   * A `URLSpec` oggetto contenente i valori URI richiesti dal servizio Forms.
   * A `java.util.HashMap` oggetto che memorizza gli allegati. Questo è un parametro facoltativo e puoi specificare `null` se non si desidera allegare file al modulo.
   * Un campo vuoto `com.adobe.idp.services.holders.BLOBHolder` oggetto popolato dal metodo. Questo parametro viene utilizzato per memorizzare il modulo di cui è stato eseguito il rendering.
   * Un campo vuoto `javax.xml.rpc.holders.LongHolder` oggetto popolato dal metodo. Questo argomento consente di memorizzare il numero di pagine nel modulo.
   * Un campo vuoto `javax.xml.rpc.holders.StringHolder` oggetto popolato dal metodo. Questo argomento consente di memorizzare il valore delle impostazioni locali.
   * Un campo vuoto `com.adobe.idp.services.holders.FormsResultHolder` oggetto che conterrà i risultati dell&#39;operazione.

   Il `renderPDFForm` il metodo compila `com.adobe.idp.services.holders.FormsResultHolder` oggetto passato come ultimo valore di argomento con un flusso di dati del modulo che deve essere scritto nel browser web client.

1. Scrivere il flusso di dati del modulo nel browser Web client

   * Creare un `FormResult` dell&#39;oggetto ottenendo il valore del `com.adobe.idp.services.holders.FormsResultHolder` dell&#39;oggetto `value` membro dati.
   * Creare un `BLOB` oggetto che contiene i dati del modulo richiamando `FormsResult` dell&#39;oggetto `getOutputContent` metodo.
   * Ottieni il tipo di contenuto del `BLOB` oggetto richiamando il relativo `getContentType` metodo.
   * Imposta il `javax.servlet.http.HttpServletResponse` tipo di contenuto dell&#39;oggetto richiamando il relativo `setContentType` e passando il tipo di contenuto del `BLOB` oggetto.
   * Creare un `javax.servlet.ServletOutputStream` oggetto utilizzato per scrivere il flusso di dati del modulo nel browser web client richiamando `javax.servlet.http.HttpServletResponse` dell&#39;oggetto `getOutputStream` metodo.
   * Creare una matrice di byte e popolarla richiamando il `BLOB` dell&#39;oggetto `getBinaryData` metodo. Questa attività assegna il contenuto del `FormsResult` alla matrice di byte.
   * Richiama `javax.servlet.http.HttpServletResponse` dell&#39;oggetto `write` metodo per inviare il flusso di dati del modulo al browser web client. Passare la matrice di byte al `write` metodo.

**Consulta anche**

[Rendering di Forms basato su frammenti](#rendering-forms-based-on-fragments)

[Richiamare AEM Forms utilizzando la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
