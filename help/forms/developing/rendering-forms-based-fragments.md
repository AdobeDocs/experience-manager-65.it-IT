---
title: Rendering di Forms basato su frammenti
seo-title: Rendering di Forms basato su frammenti
description: Utilizzare il servizio Forms per eseguire il rendering dei moduli basati sui frammenti creati con Designer.
seo-description: Utilizzare il servizio Forms per eseguire il rendering dei moduli basati sui frammenti creati con Designer.
uuid: 9c9a730d-f970-41f8-afed-4e6b6d3d393d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: a65c5303-0ebd-43a9-a777-401042d8fcad
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2230'
ht-degree: 8%

---


# Rendering di Forms basato su frammenti {#rendering-forms-based-on-fragments}

**Esempi ed esempi in questo documento sono solo per AEM Forms in ambiente JEE.**

## Rendering di Forms basato su frammenti {#rendering-forms-based-on-fragments-inner}

Il servizio Forms può eseguire il rendering dei moduli basati sui frammenti creati con Designer. Un *frammento* è una parte riutilizzabile di un modulo e viene salvato come file XDP separato che può essere inserito in più strutture del modulo. Ad esempio, un frammento può contenere un blocco indirizzo o note legali.

Utilizzando i frammenti è possibile creare e gestire in modo semplice e veloce anche grandi quantità di moduli. Durante la creazione di un nuovo modulo, è possibile inserire un riferimento al frammento desiderato e il frammento viene visualizzato nel modulo. Il riferimento al frammento contiene un sottomodulo che punta al file XDP fisico. Per informazioni sulla creazione di strutture del modulo basate sui frammenti, vedere [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63)

Un frammento può includere diversi sottomoduli racchiusi in un set sottomodulo selezionato. I set sottomodulo selezionati controllano la visualizzazione dei sottomoduli in base al flusso di dati da una connessione dati. È possibile utilizzare istruzioni condizionali per determinare quale sottomodulo del set visualizzare nel modulo finale. Ad esempio, ogni sottomodulo di un set può includere informazioni relative a una particolare posizione geografica; il sottomodulo visualizzato può essere determinato in base alla posizione dell’utente.

Un *frammento di script* contiene funzioni o valori JavaScript riutilizzabili che sono memorizzati separatamente da qualsiasi oggetto particolare, ad esempio un parser di date o una chiamata a un servizio Web. Questi frammenti includono un singolo oggetto script visualizzato come elemento secondario delle variabili nella palette Gerarchia. Non è consentito creare frammenti derivati da script di proprietà di altri oggetti, ad esempio script di evento che eseguono operazioni di convalida, calcolo o inizializzazione.

Di seguito sono riportati i vantaggi dell’utilizzo dei frammenti:

* **Riutilizzo** del contenuto: È possibile utilizzare i frammenti per riutilizzare il contenuto in più strutture del modulo. Se è necessario utilizzare parte dello stesso contenuto in più moduli, l’utilizzo di un frammento è più rapido e semplice rispetto alla copia o alla ricreazione del contenuto. I frammenti garantiscono inoltre che le parti di un modello di modulo usate di frequente siano uniformi, per aspetto e contenuto, in tutti i moduli che vi fanno riferimento.
* **Aggiornamenti** globali: È possibile utilizzare i frammenti per apportare modifiche globali a più moduli una sola volta, in un unico file. È possibile modificare il contenuto, gli oggetti script, i binding dei dati, il layout o gli stili di un frammento, mentre tutti i moduli XDP che fanno riferimento al frammento rifletteranno le modifiche apportate.
* Ad esempio, un elemento comune in molti moduli potrebbe essere un blocco indirizzo che include un oggetto elenco a discesa per il paese. Se è necessario aggiornare i valori dell’oggetto elenco a discesa, è necessario aprire molti moduli per apportare le modifiche. Se si include il blocco indirizzo in un frammento, per apportare le modifiche è necessario aprire un solo file di frammento.
* Per aggiornare un frammento in un modulo PDF, è necessario salvare nuovamente il modulo in Designer.
* **Creazione** di moduli condivisi: È possibile utilizzare i frammenti per condividere la creazione di moduli tra diverse risorse. Gli sviluppatori di moduli con una conoscenza approfondita delle funzioni di script o di altre funzioni avanzate di Designer possono creare e condividere frammenti che si avvalgono di proprietà dinamiche e script. I progettisti di moduli possono utilizzare tali frammenti per configurare strutture del moduli e per garantire che tutte le parti di un modulo abbiano aspetto e funzionalità uniformi, indipendentemente dall’autore del modulo.

### Assemblaggio di una struttura del modulo assemblata utilizzando i frammenti {#assembling-a-form-design-assembled-using-fragments}

È possibile assemblare una struttura del modulo da passare al servizio Forms in base a più frammenti. Per assemblare più frammenti, utilizzare il servizio Assembler. Per visualizzare un esempio di utilizzo del servizio Assemble per creare una struttura del modulo utilizzata da un altro servizio Forms (il servizio Output), vedere [Creazione di documenti PDF utilizzando frammenti](/help/forms/developing/creating-document-output-streams.md#creating-pdf-documents-using-fragments). Invece di utilizzare il servizio Output, puoi eseguire lo stesso flusso di lavoro utilizzando il servizio Forms.

Quando si utilizza il servizio Assembler, si passa una struttura del modulo assemblata utilizzando i frammenti. La struttura del modulo creata non fa riferimento ad altri frammenti. In questo argomento viene invece discusso il passaggio al servizio Forms di una struttura del modulo che fa riferimento ad altri frammenti. Tuttavia, la struttura del modulo non è stata assemblata da Assembler. È stato creato in Designer.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Forms, consulta [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Per informazioni sulla creazione di un&#39;applicazione basata sul Web per il rendering di moduli basati sui frammenti, vedere [Creazione di applicazioni Web per il rendering di Forms](/help/forms/developing/creating-web-applications-renders-forms.md).

### Riepilogo dei passaggi {#summary-of-steps}

Per eseguire il rendering di un modulo basato su frammenti, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Creare un oggetto API client Forms.
1. Specificare i valori URI.
1. Eseguire il rendering del modulo.
1. Scrivere il flusso di dati del modulo sul browser Web client.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

**Creare un oggetto API client Forms**

Prima di poter eseguire programmaticamente un’operazione API client del servizio Forms, è necessario creare un client di servizio Forms.

**Specificare i valori URI**

Per eseguire correttamente il rendering di un modulo basato su frammenti, è necessario assicurarsi che il servizio Forms sia in grado di individuare sia il modulo che i frammenti (file XDP) a cui fa riferimento la struttura del modulo. Ad esempio, si supponga che il modulo sia denominato PO.xdp e che in questo modulo siano utilizzati due frammenti denominati FooterUS.xdp e FooterCanada.xdp. In questa situazione, il servizio Forms deve essere in grado di individuare tutti e tre i file XDP.

È possibile organizzare un modulo e i relativi frammenti inserendo il modulo in un’unica posizione e i frammenti in un’altra posizione oppure inserendo tutti i file XDP nella stessa posizione. Ai fini di questa sezione, si supponga che tutti i file XDP si trovino nell’archivio AEM Forms. Per informazioni sul posizionamento di file XDP nell&#39;archivio AEM Forms, consulta [Risorse di scrittura](/help/forms/developing/aem-forms-repository.md#writing-resources).

Quando si esegue il rendering di un modulo basato su frammenti, è necessario fare riferimento solo al modulo stesso e non ai frammenti. Ad esempio, è necessario fare riferimento a PO.xdp e non a FooterUS.xdp o FooterCanada.xdp. Assicurati di posizionare i frammenti in un percorso in cui il servizio Forms possa individuarli.

**Rendering del modulo**

È possibile eseguire il rendering di un modulo basato su frammenti allo stesso modo dei moduli non frammentati. In altre parole, è possibile eseguire il rendering del modulo in formato PDF, HTML o Guide modulo (obsoleto). Nell’esempio riportato in questa sezione viene eseguito il rendering di un modulo basato sui frammenti come modulo PDF interattivo. (Vedere [Rendering di PDF forms interattivi](/help/forms/developing/rendering-interactive-pdf-forms.md).)

**Scrivere il flusso di dati del modulo sul browser Web client**

Quando il servizio Forms esegue il rendering di un modulo, restituisce un flusso di dati del modulo che è necessario scrivere nel browser Web client. Una volta scritto nel browser Web client, il modulo è visibile all’utente.

**Consulta anche**

[Rendering di moduli basati su frammenti utilizzando l’API Java](#render-forms-based-on-fragments-using-the-java-api)

[Rendering di moduli basati su frammenti utilizzando l’API del servizio Web](#render-forms-based-on-fragments-using-the-web-service-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API di Forms Service](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Rendering di PDF forms interattivi](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Creazione di applicazioni Web per il rendering di Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

### Rendering di moduli basati su frammenti utilizzando l’API Java {#render-forms-based-on-fragments-using-the-java-api}

Eseguire il rendering di un modulo basato su frammenti utilizzando l’API Forms (Java):

1. Includi file di progetto

   Includi file JAR client, come adobe-forms-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto API client Forms

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `FormsServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Specificare i valori URI

   * Creare un oggetto `URLSpec` che memorizza i valori URI utilizzando il relativo costruttore.
   * Richiama il metodo `setApplicationWebRoot` dell&#39;oggetto `URLSpec` e passa un valore stringa che rappresenta la radice Web dell&#39;applicazione.
   * Richiama il metodo `setContentRootURI` dell&#39;oggetto `URLSpec` e passa un valore stringa che specifica il valore URI della directory principale del contenuto. Verificare che la struttura del modulo e i frammenti si trovino nell’URI della directory principale del contenuto. In caso contrario, il servizio Forms genera un&#39;eccezione. Per fare riferimento al repository, specifica `repository://`.
   * Richiama il metodo `setTargetURL` dell&#39;oggetto `URLSpec` e passa un valore stringa che specifica il valore dell&#39;URL di destinazione in cui vengono inviati i dati del modulo. Se si definisce l’URL di destinazione nella struttura del modulo, è possibile passare una stringa vuota. È inoltre possibile specificare l’URL a cui viene inviato un modulo per eseguire i calcoli.

1. Rendering del modulo

   Richiama il metodo `renderPDFForm` dell&#39;oggetto `FormsServiceClient` e passa i seguenti valori:

   * Valore stringa che specifica il nome della struttura del modulo, inclusa l&#39;estensione del nome file. Se si fa riferimento a una struttura del modulo che fa parte di un&#39;applicazione Forms, assicurarsi di specificare il percorso completo, ad esempio `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Un oggetto `com.adobe.idp.Document` contenente i dati da unire al modulo. Se non si desidera unire i dati, passare un oggetto `com.adobe.idp.Document` vuoto.
   * Un oggetto `PDFFormRenderSpec` che memorizza le opzioni di esecuzione.
   * Un oggetto `URLSpec` contenente valori URI richiesti dal servizio Forms per il rendering di un modulo basato su frammenti.
   * Un oggetto `java.util.HashMap` che memorizza gli allegati di file. Questo è un parametro facoltativo ed è possibile specificare `null` se non si desidera allegare file al modulo.

   Il metodo `renderPDFForm` restituisce un oggetto `FormsResult` contenente un flusso di dati del modulo che deve essere scritto nel browser Web client.

1. Scrivere il flusso di dati del modulo sul browser Web client

   * Creare un oggetto `com.adobe.idp.Document` richiamando il metodo `FormsResult` object ‘s `getOutputContent` .
   * Ottenere il tipo di contenuto dell&#39;oggetto `com.adobe.idp.Document` richiamandone il metodo `getContentType`.
   * Impostare il tipo di contenuto dell&#39;oggetto `javax.servlet.http.HttpServletResponse` richiamandone il metodo `setContentType` e passando il tipo di contenuto dell&#39;oggetto `com.adobe.idp.Document`.
   * Creare un oggetto `javax.servlet.ServletOutputStream` utilizzato per scrivere il flusso di dati del modulo nel browser Web client richiamando il metodo `javax.servlet.http.HttpServletResponse` dell&#39;oggetto `getOutputStream`.
   * Creare un oggetto `java.io.InputStream` richiamando il metodo `com.adobe.idp.Document` dell&#39;oggetto `getInputStream`.
   * Creare un array di byte popolarlo con il flusso di dati del modulo richiamando il metodo `read`dell&#39;oggetto `InputStream` e passando l&#39;array di byte come argomento.
   * Richiamare il metodo `write` dell’oggetto `javax.servlet.ServletOutputStream` per inviare il flusso di dati del modulo al browser Web client. Passa l&#39;array di byte al metodo `write` .

**Consulta anche**

[Rendering di Forms basato su frammenti](#rendering-forms-based-on-fragments)

[Avvio rapido (modalità SOAP): Rendering di un modulo basato su frammenti utilizzando l’API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-form-based-on-fragments-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Rendering di moduli basati su frammenti utilizzando l’API del servizio Web {#render-forms-based-on-fragments-using-the-web-service-api}

Eseguire il rendering di un modulo basato su frammenti utilizzando l’API Forms (servizio Web):

1. Includi file di progetto

   * Creare classi proxy Java che utilizzano il servizio WSDL di Forms.
   * Includi le classi proxy Java nel percorso della classe.

1. Creare un oggetto API client Forms

   Creare un oggetto `FormsService` e impostare i valori di autenticazione.

1. Specificare i valori URI

   * Creare un oggetto `URLSpec` che memorizza i valori URI utilizzando il relativo costruttore.
   * Richiama il metodo `setApplicationWebRoot` dell&#39;oggetto `URLSpec` e passa un valore stringa che rappresenta la radice Web dell&#39;applicazione.
   * Richiama il metodo `setContentRootURI` dell&#39;oggetto `URLSpec` e passa un valore stringa che specifica il valore URI della directory principale del contenuto. Verificare che la struttura del modulo si trovi nell’URI della directory principale del contenuto. In caso contrario, il servizio Forms genera un&#39;eccezione. Per fare riferimento al repository, specifica `repository://`.
   * Richiama il metodo `setTargetURL` dell&#39;oggetto `URLSpec` e passa un valore stringa che specifica il valore dell&#39;URL di destinazione in cui vengono inviati i dati del modulo. Se si definisce l’URL di destinazione nella struttura del modulo, è possibile passare una stringa vuota. È inoltre possibile specificare l’URL a cui viene inviato un modulo per eseguire i calcoli.

1. Rendering del modulo

   Richiama il metodo `renderPDFForm` dell&#39;oggetto `FormsService` e passa i seguenti valori:

   * Valore stringa che specifica il nome della struttura del modulo, inclusa l&#39;estensione del nome file. Se si fa riferimento a una struttura del modulo che fa parte di un&#39;applicazione Forms, assicurarsi di specificare il percorso completo, ad esempio `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Un oggetto `BLOB` contenente i dati da unire al modulo. Se non desideri unire i dati, passa `null`.
   * Un oggetto `PDFFormRenderSpec` che memorizza le opzioni di esecuzione. L’opzione PDF con tag non può essere impostata se il documento di input è un documento PDF. Se il file di input è un file XDP, è possibile impostare l’opzione PDF con tag.
   * Un oggetto `URLSpec` che contiene i valori URI richiesti dal servizio Forms.
   * Un oggetto `java.util.HashMap` che memorizza gli allegati di file. Questo è un parametro facoltativo ed è possibile specificare `null` se non si desidera allegare file al modulo.
   * Un oggetto `com.adobe.idp.services.holders.BLOBHolder` vuoto compilato dal metodo . Questo parametro viene utilizzato per memorizzare il modulo di cui è stato effettuato il rendering.
   * Un oggetto `javax.xml.rpc.holders.LongHolder` vuoto compilato dal metodo . Questo argomento memorizza il numero di pagine nel modulo.
   * Un oggetto `javax.xml.rpc.holders.StringHolder` vuoto compilato dal metodo . Questo argomento memorizza il valore delle impostazioni internazionali.
   * Un oggetto `com.adobe.idp.services.holders.FormsResultHolder` vuoto che conterrà i risultati dell&#39;operazione.

   Il metodo `renderPDFForm` popola l&#39;oggetto `com.adobe.idp.services.holders.FormsResultHolder` passato come ultimo valore dell&#39;argomento con un flusso di dati del modulo che deve essere scritto nel browser Web client.

1. Scrivere il flusso di dati del modulo sul browser Web client

   * Creare un oggetto `FormResult` ottenendo il valore del membro dati `com.adobe.idp.services.holders.FormsResultHolder` dell&#39;oggetto `value`.
   * Creare un oggetto `BLOB` che contiene dati del modulo richiamando il metodo `FormsResult` dell&#39;oggetto `getOutputContent`.
   * Ottenere il tipo di contenuto dell&#39;oggetto `BLOB` richiamandone il metodo `getContentType`.
   * Impostare il tipo di contenuto dell&#39;oggetto `javax.servlet.http.HttpServletResponse` richiamandone il metodo `setContentType` e passando il tipo di contenuto dell&#39;oggetto `BLOB`.
   * Creare un oggetto `javax.servlet.ServletOutputStream` utilizzato per scrivere il flusso di dati del modulo nel browser Web client richiamando il metodo `javax.servlet.http.HttpServletResponse` dell&#39;oggetto `getOutputStream`.
   * Creare una matrice di byte e compilarla richiamando il metodo `getBinaryData` dell&#39;oggetto `BLOB`. Questa attività assegna il contenuto dell&#39;oggetto `FormsResult` all&#39;array di byte.
   * Richiamare il metodo `write` dell’oggetto `javax.servlet.http.HttpServletResponse` per inviare il flusso di dati del modulo al browser Web client. Passa l&#39;array di byte al metodo `write` .

**Consulta anche**

[Rendering di Forms basato su frammenti](#rendering-forms-based-on-fragments)

[Richiamo di AEM Forms con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
