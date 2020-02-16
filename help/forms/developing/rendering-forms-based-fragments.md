---
title: Rendering di moduli basati su frammenti
seo-title: Rendering di moduli basati su frammenti
description: 'null'
seo-description: 'null'
uuid: 9c9a730d-f970-41f8-afed-4e6b6d3d393d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: a65c5303-0ebd-43a9-a777-401042d8fcad
translation-type: tm+mt
source-git-commit: 413af4ef9bc3652e05da78d622183bcf20a8bee7

---


# Rendering di moduli basati su frammenti {#rendering-forms-based-on-fragments}

## Rendering di moduli basati su frammenti {#rendering-forms-based-on-fragments-inner}

Il servizio Forms consente di eseguire il rendering dei moduli basati su frammenti creati con Designer. Un *frammento* è una parte riutilizzabile di un modulo e viene salvato come file XDP separato che può essere inserito in più strutture del modulo. Ad esempio, un frammento può contenere un blocco indirizzo o note legali.

Utilizzando i frammenti è possibile creare e gestire in modo semplice e veloce anche grandi quantità di moduli. Durante la creazione di un nuovo modulo, è possibile inserire un riferimento al frammento desiderato e il frammento viene visualizzato nel modulo. Il riferimento al frammento contiene un sottomodulo che punta al file XDP fisico. Per informazioni sulla creazione di strutture del modulo basate sui frammenti, vedere [Designer](https://www.adobe.com/go/learn_aemforms_designer_63)

Un frammento può includere diversi sottomoduli racchiusi in un set sottomodulo selezionato. I set sottomodulo selezionati controllano la visualizzazione dei sottomoduli in base al flusso di dati proveniente da una connessione dati. È possibile utilizzare istruzioni condizionali per determinare quale sottomodulo del set visualizzare nel modulo finale. Ad esempio, ogni sottomodulo di un set può includere informazioni per una particolare posizione geografica e il sottomodulo visualizzato può essere determinato in base alla posizione dell&#39;utente.

A *script fragment* contains reusable JavaScript functions or values that are stored separately from any particular object, such as a date parser or a web service invocation. Questi frammenti includono un singolo oggetto script visualizzato come elemento secondario delle variabili nella palette Gerarchia. Non è consentito creare frammenti derivati da script di proprietà di altri oggetti, ad esempio script di evento che eseguono operazioni di convalida, calcolo o inizializzazione.

L’uso dei frammenti presenta i seguenti vantaggi:

* **Riuso** del contenuto: È possibile utilizzare i frammenti per riutilizzare il contenuto in più strutture del modulo. Se è necessario utilizzare parte dello stesso contenuto in più moduli, l&#39;uso di un frammento risulta più semplice e rapido rispetto alla copia o alla ricreazione del contenuto. I frammenti garantiscono inoltre che le parti di un modello di modulo usate di frequente siano uniformi, per aspetto e contenuto, in tutti i moduli che vi fanno riferimento.
* **Aggiornamenti** globali: È possibile utilizzare i frammenti per apportare modifiche globali a più moduli una sola volta, in un unico file. È possibile modificare il contenuto, gli oggetti script, i binding dei dati, il layout o gli stili di un frammento e tutti i moduli XDP che fanno riferimento al frammento rifletteranno le modifiche.
* Ad esempio, un elemento comune in molti moduli potrebbe essere un blocco indirizzo che include un oggetto elenco a discesa per il paese. Se è necessario aggiornare i valori per l&#39;oggetto elenco a discesa, è necessario aprire molti moduli per apportare le modifiche. Se si inserisce il blocco indirizzo in un frammento, è necessario aprire un solo file di frammento per apportare le modifiche.
* Per aggiornare un frammento in un modulo PDF, è necessario salvare nuovamente il modulo in Designer.
* **Creazione** di moduli condivisi: È possibile utilizzare i frammenti per condividere la creazione di moduli tra diverse risorse. Gli sviluppatori di moduli con una conoscenza approfondita delle funzioni di script o di altre funzioni avanzate di Designer possono creare e condividere frammenti che si avvalgono di proprietà dinamiche e script. I progettisti di moduli possono utilizzare tali frammenti per configurare strutture del moduli e per garantire che tutte le parti di un modulo abbiano aspetto e funzionalità uniformi, indipendentemente dall’autore del modulo.

### Assemblaggio di una struttura del modulo assemblata utilizzando i frammenti {#assembling-a-form-design-assembled-using-fragments}

È possibile assemblare una struttura del modulo per passare al servizio Forms in base a più frammenti. Per assemblare più frammenti, utilizzare il servizio Assembler. Per un esempio di utilizzo del servizio Assemble per creare una struttura del modulo utilizzata da altri servizi Forms (il servizio Output), vedere [Creazione di documenti PDF utilizzando i frammenti](/help/forms/developing/creating-document-output-streams.md#creating-pdf-documents-using-fragments). Invece di utilizzare il servizio Output, è possibile eseguire lo stesso flusso di lavoro utilizzando il servizio Forms.

Quando si utilizza il servizio Assembler, si passa una struttura del modulo assemblata utilizzando i frammenti. La struttura del modulo creata non fa riferimento ad altri frammenti. In questo argomento viene invece discusso il passaggio di una struttura del modulo che fa riferimento ad altri frammenti al servizio Forms. Tuttavia, la struttura del modulo non è stata assemblata da Assembler. È stato creato in Designer.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Forms, consultate Riferimento [servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Per informazioni sulla creazione di un&#39;applicazione basata sul Web per il rendering di moduli basati sui frammenti, vedere [Creazione di applicazioni Web per il rendering di moduli](/help/forms/developing/creating-web-applications-renders-forms.md).

### Riepilogo dei passaggi {#summary-of-steps}

Per eseguire il rendering di un modulo basato su frammenti, effettuare le operazioni seguenti:

1. Includere i file di progetto.
1. Creare un oggetto API client Forms.
1. Specificate i valori URI.
1. Eseguire il rendering del modulo.
1. Scrivere il flusso di dati del modulo nel browser Web del client.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, accertatevi di includere i file proxy.

**Creare un oggetto API client Forms**

Prima di eseguire un&#39;operazione API client del servizio Forms a livello di programmazione, è necessario creare un client del servizio Forms.

**Specificare i valori URI**

Per eseguire correttamente il rendering di un modulo basato su frammenti, è necessario assicurarsi che il servizio Forms sia in grado di individuare il modulo e i frammenti (file XDP) a cui fa riferimento la struttura del modulo. Ad esempio, si supponga che il modulo sia denominato PO.xdp e che utilizzi due frammenti denominati FooterUS.xdp e FooterCanada.xdp. In questa situazione, il servizio Forms deve essere in grado di individuare tutti e tre i file XDP.

È possibile organizzare un modulo e i relativi frammenti inserendo il modulo in un&#39;unica posizione e i frammenti in un&#39;altra posizione, oppure posizionare tutti i file XDP nella stessa posizione. Ai fini di questa sezione, si supponga che tutti i file XDP si trovino nell&#39;archivio di AEM Forms. Per informazioni sull&#39;inserimento di file XDP nell&#39;archivio di AEM Forms, consultate [Creazione di risorse](/help/forms/developing/aem-forms-repository.md#writing-resources).

Durante il rendering di un modulo basato su frammenti, è necessario fare riferimento solo al modulo stesso e non ai frammenti. Ad esempio, è necessario fare riferimento a PO.xdp e non a FooterUS.xdp o FooterCanada.xdp. Assicurarsi di posizionare i frammenti in un percorso in cui il servizio Forms è in grado di individuarli.

**Eseguire il rendering del modulo**

È possibile eseguire il rendering di un modulo basato su frammenti allo stesso modo dei moduli non frammentati. In altre parole, è possibile eseguire il rendering del modulo come PDF, HTML o guide del modulo (obsoleto). L&#39;esempio riportato in questa sezione esegue il rendering di un modulo basato sui frammenti come modulo PDF interattivo. (Vedere [Rendering di moduli](/help/forms/developing/rendering-interactive-pdf-forms.md)PDF interattivi.)

**Scrivere il flusso di dati del modulo nel browser Web del client**

Quando il servizio Forms esegue il rendering di un modulo, restituisce un flusso di dati del modulo che è necessario scrivere nel browser Web del client. Una volta scritto nel browser Web del client, il modulo è visibile all&#39;utente.

**Consulta anche**

[Rendering di moduli basati su frammenti mediante l&#39;API Java](#render-forms-based-on-fragments-using-the-java-api)

[Rendering di moduli basati su frammenti tramite l&#39;API del servizio Web](#render-forms-based-on-fragments-using-the-web-service-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido dell&#39;API di Forms Service](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Rendering di moduli PDF interattivi](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Creazione di applicazioni Web per il rendering di moduli](/help/forms/developing/creating-web-applications-renders-forms.md)

### Rendering di moduli basati su frammenti mediante l&#39;API Java {#render-forms-based-on-fragments-using-the-java-api}

Eseguire il rendering di un modulo basato sui frammenti utilizzando l&#39;API Forms (Java):

1. Includi file di progetto

   Includete file JAR client, ad esempio adobe-forms-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto API client Forms

   * Creare un `ServiceClientFactory` oggetto che contenga proprietà di connessione.
   * Creare un `FormsServiceClient` oggetto utilizzando il relativo costruttore e passando l&#39; `ServiceClientFactory` oggetto.

1. Specificare i valori URI

   * Creare un `URLSpec` oggetto che memorizza i valori URI utilizzando il relativo costruttore.
   * Richiamare il metodo dell&#39; `URLSpec` oggetto `setApplicationWebRoot` e passare un valore di stringa che rappresenta la radice Web dell&#39;applicazione.
   * Richiamate il metodo dell&#39; `URLSpec` oggetto `setContentRootURI` e passate un valore di stringa che specifica il valore URI della radice del contenuto. Verificare che la struttura del modulo e i frammenti si trovino nell&#39;URI principale del contenuto. In caso contrario, il servizio Forms genera un&#39;eccezione. Per fare riferimento alla directory archivio, specificare `repository://`.
   * Richiamare il metodo dell&#39; `URLSpec` oggetto `setTargetURL` e passare un valore stringa che specifica il valore dell&#39;URL di destinazione in cui vengono inviati i dati del modulo. Se si definisce l&#39;URL di destinazione nella struttura del modulo, è possibile passare una stringa vuota. È inoltre possibile specificare l&#39;URL al quale viene inviato il modulo per eseguire i calcoli.

1. Eseguire il rendering del modulo

   Richiama il metodo dell’ `FormsServiceClient` oggetto `renderPDFForm` e passa i seguenti valori:

   * Una stringa che specifica il nome della struttura del modulo, inclusa l&#39;estensione del nome file. Se si fa riferimento a una struttura del modulo che fa parte di un&#39;applicazione Forms, è necessario specificare il percorso completo, ad esempio `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Un `com.adobe.idp.Document` oggetto che contiene i dati da unire al modulo. Se non si desidera unire i dati, passare un `com.adobe.idp.Document` oggetto vuoto.
   * Un `PDFFormRenderSpec` oggetto che memorizza le opzioni di esecuzione.
   * Un `URLSpec` oggetto che contiene valori URI richiesti dal servizio Forms per eseguire il rendering di un modulo basato su frammenti.
   * Un `java.util.HashMap` oggetto che memorizza gli allegati. Si tratta di un parametro facoltativo e potete specificare `null` se non desiderate allegare file al modulo.
   Il `renderPDFForm` metodo restituisce un `FormsResult` oggetto che contiene un flusso di dati del modulo da scrivere nel browser Web del client.

1. Scrivere il flusso di dati del modulo nel browser Web del client

   * Creare un `com.adobe.idp.Document` oggetto richiamando il `FormsResult` metodo ‘s `getOutputContent` .
   * Ottenere il tipo di contenuto dell&#39; `com.adobe.idp.Document` oggetto richiamandone il `getContentType` metodo.
   * Impostare il tipo di contenuto dell&#39; `javax.servlet.http.HttpServletResponse` oggetto richiamandone `setContentType` il metodo e passando il tipo di contenuto dell&#39; `com.adobe.idp.Document` oggetto.
   * Creare un `javax.servlet.ServletOutputStream` oggetto utilizzato per scrivere il flusso di dati del modulo nel browser Web del client richiamando il `javax.servlet.http.HttpServletResponse` metodo dell&#39; `getOutputStream` oggetto.
   * Creare un `java.io.InputStream` oggetto richiamando il `com.adobe.idp.Document` metodo dell&#39; `getInputStream` oggetto.
   * Per creare un array di byte, è necessario inserirlo nel flusso di dati del modulo richiamando il `InputStream` `read`metodo dell&#39;oggetto e passando l&#39;array di byte come argomento.
   * Richiamare il metodo dell&#39; `javax.servlet.ServletOutputStream` oggetto `write` per inviare il flusso di dati del modulo al browser Web del client. Passa l&#39;array di byte al `write` metodo.

**Consulta anche**

[Rendering di moduli basati su frammenti](#rendering-forms-based-on-fragments)

[Avvio rapido (modalità SOAP): Rendering di un modulo basato su frammenti utilizzando l&#39;API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-form-based-on-fragments-using-the-java-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Rendering di moduli basati su frammenti tramite l&#39;API del servizio Web {#render-forms-based-on-fragments-using-the-web-service-api}

Eseguire il rendering di un modulo basato su frammenti utilizzando l&#39;API di Forms (servizio Web):

1. Includi file di progetto

   * Creare classi proxy Java che utilizzano il WSDL del servizio Forms.
   * Includete le classi proxy Java nel percorso della classe.

1. Creare un oggetto API client Forms

   Creare un `FormsService` oggetto e impostare i valori di autenticazione.

1. Specificare i valori URI

   * Creare un `URLSpec` oggetto che memorizza i valori URI utilizzando il relativo costruttore.
   * Richiamare il metodo dell&#39; `URLSpec` oggetto `setApplicationWebRoot` e passare un valore di stringa che rappresenta la radice Web dell&#39;applicazione.
   * Richiamate il metodo dell&#39; `URLSpec` oggetto `setContentRootURI` e passate un valore di stringa che specifica il valore URI della radice del contenuto. Verificare che la struttura del modulo si trovi nell&#39;URI della directory principale del contenuto. In caso contrario, il servizio Forms genera un&#39;eccezione. Per fare riferimento alla directory archivio, specificare `repository://`.
   * Richiamare il metodo dell&#39; `URLSpec` oggetto `setTargetURL` e passare un valore stringa che specifica il valore dell&#39;URL di destinazione in cui vengono inviati i dati del modulo. Se si definisce l&#39;URL di destinazione nella struttura del modulo, è possibile passare una stringa vuota. È inoltre possibile specificare l&#39;URL al quale viene inviato il modulo per eseguire i calcoli.

1. Eseguire il rendering del modulo

   Richiama il metodo dell’ `FormsService` oggetto `renderPDFForm` e passa i seguenti valori:

   * Una stringa che specifica il nome della struttura del modulo, inclusa l&#39;estensione del nome file. Se si fa riferimento a una struttura del modulo che fa parte di un&#39;applicazione Forms, è necessario specificare il percorso completo, ad esempio `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Un `BLOB` oggetto che contiene i dati da unire al modulo. Se non si desidera unire i dati, passare `null`.
   * Un `PDFFormRenderSpec` oggetto che memorizza le opzioni di esecuzione. L&#39;opzione PDF con tag non può essere impostata se il documento di input è un documento PDF. Se il file di input è un file XDP, è possibile impostare l&#39;opzione PDF con tag.
   * Un `URLSpec` oggetto che contiene i valori URI richiesti dal servizio Forms.
   * Un `java.util.HashMap` oggetto che memorizza gli allegati. Si tratta di un parametro facoltativo e potete specificare `null` se non desiderate allegare file al modulo.
   * Un oggetto vuoto `com.adobe.idp.services.holders.BLOBHolder` compilato dal metodo. Questo parametro viene utilizzato per memorizzare il modulo di cui è stato effettuato il rendering.
   * Un oggetto vuoto `javax.xml.rpc.holders.LongHolder` compilato dal metodo. Questo argomento memorizza il numero di pagine nel modulo.
   * Un oggetto vuoto `javax.xml.rpc.holders.StringHolder` compilato dal metodo. Questo argomento memorizzerà il valore delle impostazioni internazionali.
   * Un oggetto vuoto `com.adobe.idp.services.holders.FormsResultHolder` che conterrà i risultati dell&#39;operazione.
   Il `renderPDFForm` metodo compila l&#39; `com.adobe.idp.services.holders.FormsResultHolder` oggetto passato come ultimo valore argomento con un flusso di dati del modulo che deve essere scritto nel browser Web del client.

1. Scrivere il flusso di dati del modulo nel browser Web del client

   * Creare un `FormResult` oggetto ottenendo il valore del membro `com.adobe.idp.services.holders.FormsResultHolder` dati dell&#39; `value` oggetto.
   * Creare un `BLOB` oggetto che contenga dati del modulo richiamando il `FormsResult` metodo dell&#39; `getOutputContent` oggetto.
   * Ottenere il tipo di contenuto dell&#39; `BLOB` oggetto richiamandone il `getContentType` metodo.
   * Impostare il tipo di contenuto dell&#39; `javax.servlet.http.HttpServletResponse` oggetto richiamandone `setContentType` il metodo e passando il tipo di contenuto dell&#39; `BLOB` oggetto.
   * Creare un `javax.servlet.ServletOutputStream` oggetto utilizzato per scrivere il flusso di dati del modulo nel browser Web del client richiamando il `javax.servlet.http.HttpServletResponse` metodo dell&#39; `getOutputStream` oggetto.
   * Creare un array di byte e compilarlo richiamando il metodo dell&#39; `BLOB` oggetto `getBinaryData` . Questa attività assegna il contenuto dell&#39; `FormsResult` oggetto all&#39;array di byte.
   * Richiamare il metodo dell&#39; `javax.servlet.http.HttpServletResponse` oggetto `write` per inviare il flusso di dati del modulo al browser Web del client. Passa l&#39;array di byte al `write` metodo.

**Consulta anche**

[Rendering di moduli basati su frammenti](#rendering-forms-based-on-fragments)

[Richiamo di moduli AEM con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
